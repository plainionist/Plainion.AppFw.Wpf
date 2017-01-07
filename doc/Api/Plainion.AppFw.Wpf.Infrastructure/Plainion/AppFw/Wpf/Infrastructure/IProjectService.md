
# Plainion.AppFw.Wpf.Infrastructure.IProjectService`1

**Namespace:** Plainion.AppFw.Wpf.Infrastructure

**Assembly:** Plainion.AppFw.Wpf.Infrastructure


## Properties

###  Project


## Events

###  ProjectChanging

###  ProjectChanged


## Methods

### void Create(System.String location,System.Boolean autoSave)

### void Load(System.String location)

### void Save()

### System.Threading.Tasks.Task CreateAsync(System.String location,System.Boolean autoSave,System.IProgress`1[Plainion.Progress.IProgressInfo] progress,System.Threading.CancellationToken cancellationToken)

### System.Threading.Tasks.Task LoadAsync(System.String location,System.IProgress`1[Plainion.Progress.IProgressInfo] progress,System.Threading.CancellationToken cancellationToken)

### System.Threading.Tasks.Task SaveAsync(System.IProgress`1[Plainion.Progress.IProgressInfo] progress,System.Threading.CancellationToken cancellationToken)
