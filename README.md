All credit to [Arash Rahimi's](http://stackoverflow.com/users/4931970/arash-rahimi) answer on [Stack Overflow](http://stackoverflow.com/a/30413095/966609) regarding an issue with `Microsoft.Cloud.Common.AzureStorage` not being packaged with *Azure Service Bus 1.1*

1. Open elevated command prompt
2. Navigate to your SDK tools
  - eg. `cd C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.6 Tools\x64`
3. `sn -Vr Microsoft.Cloud.Common.AzureStorage.dll`
4. `gacutil /i Microsoft.Cloud.Common.AzureStorage.dll`

You may have found the following exceptions in Window's Event Viewer:

#### 1

    Exception during fabric service creation for container 1, Exception System.ArgumentException: At least one address must be provided if hostEndpoints is non-null
    Parameter name: hostEndpoints
    at System.Fabric.FabricClient.InitializeFabricClient(SecurityCredentials credential, TimeSpan keepAliveInterval, String[] hostEndpoints)
    at System.Fabric.FabricClient..ctor(SecurityCredentials credential, String[] hostEndpoints)
    at Microsoft.ServiceBus.Commands.ServiceBusGetCommands.CreateFabricClient()
    at Microsoft.ServiceBus.Commands.ServiceBusCommandBase.RegisterWinFabricService(Int64 containerId)

#### 2

    Service Bus Gateway service failed to start, retry count 1.  Exception message: An error occurred creating the configuration section handler for namespacePolicyDataStoreFactory: Could not load file or assembly 'Microsoft.Cloud.Common.AzureStorage, Version=2.1.0.0, Culture=neutral, PublicKeyToken=4fe77f22fa8374f3' or one of its dependencies. The system cannot find the file specified..  Stack Trace:    at System.Configuration.BaseConfigurationRecord.CallCreateSection(Boolean inputIsTrusted, FactoryRecord factoryRecord, SectionRecord sectionRecord, Object parentConfig, ConfigXmlReader reader, String filename, Int32 line)
    at System.Configuration.BaseConfigurationRecord.CreateSectionDefault(String configKey, Boolean getRuntimeObject, FactoryRecord factoryRecord, SectionRecord sectionRecord, Object& result, Object& resultRuntimeObject)
    at System.Configuration.BaseConfigurationRecord.GetSectionRecursive(String configKey, Boolean getLkg, Boolean checkPermission, Boolean getRuntimeObject, Boolean requestIsHere, Object& result, Object& resultRuntimeObject)
    at Microsoft.Cloud.ServiceBus.ServiceRegistryManagerContext.CreateNamespacePolicyDataManager(IComponentSite site)
    at Microsoft.Cloud.ServiceBus.ServiceRegistryManagerContext.LoadServices(IComponentSite site)
    at Microsoft.Cloud.ServiceBus.Common.Components.ComponentFactoryBase`1.CreateComponent()
    at Microsoft.Cloud.HostingModel.ComponentHost.CreateComponent(IComponentFactory componentFactory)
    at Microsoft.Cloud.HostingModel.ComponentHost.CreateComponents()
    at Microsoft.Cloud.HostingModel.ComponentHost.Open()
    at Microsoft.ServiceBus.Gateway.Gateway.OnStart(String[] args)
