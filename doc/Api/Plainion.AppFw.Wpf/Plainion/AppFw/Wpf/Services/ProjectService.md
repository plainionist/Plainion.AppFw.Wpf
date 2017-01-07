
# Plainion.AppFw.Wpf.Services.ProjectService`1

**Namespace:** Plainion.AppFw.Wpf.Services

**Assembly:** Plainion.AppFw.Wpf


## Constructors

### Constructor()


## Properties

###  Project


## Events

###  ProjectChanging

###  ProjectChanged


## Methods

### void OnProjectChanging(TProject oldProject)

### void OnProjectChanged(TProject newProject)

### void Create(System.String location,System.Boolean autoSave)

### void InitializeProject(TProject project,System.IProgress`1[Plainion.Progress.IProgressInfo] progress,System.Threading.CancellationToken cancellationToken)

### System.Threading.Tasks.Task CreateAsync(System.String location,System.Boolean autoSave,System.IProgress`1[Plainion.Progress.IProgressInfo] progress,System.Threading.CancellationToken cancellationToken)

### void Load(System.String location)

###  Deserialize(System.String location,System.IProgress`1[Plainion.Progress.IProgressInfo] progress,System.Threading.CancellationToken cancellationToken)

### System.Threading.Tasks.Task LoadAsync(System.String location,System.IProgress`1[Plainion.Progress.IProgressInfo] progress,System.Threading.CancellationToken cancellationToken)

### void Save()

### void Serialize(TProject project,System.IProgress`1[Plainion.Progress.IProgressInfo] progress,System.Threading.CancellationToken cancellationToken)

### System.Threading.Tasks.Task SaveAsync(System.IProgress`1[Plainion.Progress.IProgressInfo] progress,System.Threading.CancellationToken cancellationToken)
