
# Plainion.AppFw.Wpf.Infrastructure.ProjectBase

**Namespace:** Plainion.AppFw.Wpf.Infrastructure

**Assembly:** Plainion.AppFw.Wpf.Infrastructure


## Constructors

### Constructor()


## Properties

### System.String Location

The location can be empty for new projects and can be changed later on but follows write-once policy.

### System.Boolean IsDirty


## Methods

### void OnLocationChanged()

Provided by derived classes to adjust properties derived from Location. A notification that the location has changed does not mean that the file is already saved at this location. therefore the "IsDirty" flag has to considered as well.
