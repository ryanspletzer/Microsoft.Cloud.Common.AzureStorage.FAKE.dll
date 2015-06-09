1. Open elevated command prompt
2. Navigate to your SDK tools
  - eg. `cd C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.6 Tools\x64`
3. `sn -Vr Microsoft.Cloud.Common.AzureStorage.dll`
4. `gacutil /i Microsoft.Cloud.Common.AzureStorage.dll`