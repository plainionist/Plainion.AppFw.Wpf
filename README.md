
Writing WPF/MMVM based applications always brings some boilerplate for

- opening documents
- savling documents
- closing with unsaved data
- handling main window title

# This project provides you an alternative ...

A simple but yet powerful WPF/MVVM application template which let you start with your actual features right away.

1. Download this package from [NuGet](https://www.nuget.org/packages/Plainion.AppFw.Wpf/) ![NuGet Version](https://img.shields.io/nuget/v/Plainion.AppFw.Wpf.svg?style=flat-square)
2. Write your Shell and ShellViewModel as usual
3. Derive from BootStrapperBase

```C#
public class Bootstrapper : BootstrapperBase<Shell>
{
    protected override void ConfigureAggregateCatalog()
    {
        base.ConfigureAggregateCatalog();

        AggregateCatalog.Catalogs.Add( new AssemblyCatalog( GetType().Assembly ) );
        AggregateCatalog.Catalogs.Add( new AssemblyCatalog( typeof( PopupWindowActionRegionAdapter ).Assembly ) );

        AggregateCatalog.Catalogs.Add( new TypeCatalog(
            typeof( ProjectLifecycleViewModel<Project> ),
            typeof( TitleViewModel<Project> )
            ) );
    }
}
```

4. Derive from ProjectService to handle empty new projects

```C#
    internal class ProjectService : ProjectService<Project>
    {
        public override Project CreateEmptyProject( string location )
        {
            ... how does a new project look like? ...
        }
    }
```

5. Integrate the ViewModels in your ShellViewModel

```C#
[Export( typeof( ShellViewModel ) )]
public class ShellViewModel : BindableBase
{
    private const string AppName = "Plainion.Forest";
    private IProjectService<Project> myProjectService;
    private IPersistenceService<Project> myPersistenceService;

    [ImportingConstructor]
    public ShellViewModel( IProjectService<Project> projectService, IEventAggregator eventAggregator, IPersistenceService<Project> persistenceService )
    {
        myProjectService = projectService;
        myPersistenceService = persistenceService;

        eventAggregator.GetEvent<ApplicationReadyEvent>().Subscribe( x => OnApplicationReady() );
    }

    [Import]
    public ProjectLifecycleViewModel<Project> ProjectLifecycleViewModel { get; set; }

    [Import]
    public TitleViewModel<Project> TitleViewModel { get; set; }

    private void OnApplicationReady()
    {
        TitleViewModel.ApplicationName = AppName;

        ProjectLifecycleViewModel.ApplicationName = AppName;
        ProjectLifecycleViewModel.FileFilter = "Plainion Forest Projects (*.bf)|*.bf";
        ProjectLifecycleViewModel.FileFilterIndex = 0;
        ProjectLifecycleViewModel.DefaultFileExtension = ".bf";

        var args = Environment.GetCommandLineArgs();
        if ( args.Length == 2 )
        {
            myProjectService.Project = myPersistenceService.Load( args[ 1 ] );
        }
        else
        {
            myProjectService.Project = myProjectService.CreateEmptyProject( null );
        }
    }
}
```

6. Integrate the views in the Shell.xaml

```Xaml
<Window.Resources>
    <ResourceDictionary>
        <xcad:VS2010Theme x:Key="DefaultTheme" />
        <ResourceDictionary.MergedDictionaries>
            <ResourceDictionary Source="pack://application:,,,/Plainion.AppFw.Wpf;component/Views/ProjectLifecycleStyles.xaml"/>
        </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
</Window.Resources>
<Window.Style>
    <pn:MultiStyle ResourceKeys="ProjectLifecycleStyle"/>
</Window.Style>
<Window.InputBindings>
    <KeyBinding Key="O" Modifiers="Control" Command="{Binding ProjectLifecycleViewModel.OpenCommand}"/>
    <KeyBinding Key="S" Modifiers="Control" Command="{Binding ProjectLifecycleViewModel.SaveCommand}"/>
    <KeyBinding Key="F4" Modifiers="Alt" Command="{Binding ProjectLifecycleViewModel.CloseCommand}"/>
</Window.InputBindings>
<DockPanel LastChildFill="True">
    <Menu DockPanel.Dock="Top">
        <MenuItem Header="_File">
            <MenuItem Header="_New" Command="{Binding ProjectLifecycleViewModel.NewCommand}" />
            <MenuItem Header="_Open" Command="{Binding ProjectLifecycleViewModel.OpenCommand}" InputGestureText="Ctrl+O"/>
            <MenuItem Header="_Save" Command="{Binding ProjectLifecycleViewModel.SaveCommand}" InputGestureText="Ctrl+S"/>
            <Separator/>
            <MenuItem Header="_Close" Command="{Binding ProjectLifecycleViewModel.CloseCommand}" InputGestureText="Alt+F4"/>
        </MenuItem>
    </Menu>
``` 

## ... and now start focusing on your features! :)