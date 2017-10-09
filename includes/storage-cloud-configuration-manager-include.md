Hallo [Microsoft Azure Configuration Manager-bibliotheek voor .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) biedt een klasse voor het parseren van een verbindingsreeks uit een configuratiebestand. Hallo [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) klasse parseert configuratie-instellingen, ongeacht of de client-toepassing hello op Hallo-bureaublad op een mobiel apparaat in Azure een virtuele machine of in een Azure cloudservice wordt uitgevoerd.

tooreference Hallo pakket CloudConfigurationManager, voeg de volgende Hallo `using` richtlijn:

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

Hier volgt een voorbeeld ziet u hoe tooretrieve een verbinding verbindingsreeks uit een configuratiebestand:

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

Gebruik hello Azure Configuration Manager is optioneel. U kunt ook een API zoals Hallo van .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) klasse.

