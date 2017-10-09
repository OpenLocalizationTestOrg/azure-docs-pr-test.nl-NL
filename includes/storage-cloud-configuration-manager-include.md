<span data-ttu-id="5daaf-101">Hallo [Microsoft Azure Configuration Manager-bibliotheek voor .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) biedt een klasse voor het parseren van een verbindingsreeks uit een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="5daaf-101">hello [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="5daaf-102">Hallo [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) klasse parseert configuratie-instellingen, ongeacht of de client-toepassing hello op Hallo-bureaublad op een mobiel apparaat in Azure een virtuele machine of in een Azure cloudservice wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5daaf-102">hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether hello client application is running on hello desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="5daaf-103">tooreference Hallo pakket CloudConfigurationManager, voeg de volgende Hallo `using` richtlijn:</span><span class="sxs-lookup"><span data-stu-id="5daaf-103">tooreference hello CloudConfigurationManager package, add hello following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="5daaf-104">Hier volgt een voorbeeld ziet u hoe tooretrieve een verbinding verbindingsreeks uit een configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="5daaf-104">Here's an example that shows how tooretrieve a connection string from a configuration file:</span></span>

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="5daaf-105">Gebruik hello Azure Configuration Manager is optioneel.</span><span class="sxs-lookup"><span data-stu-id="5daaf-105">Using hello Azure Configuration Manager is optional.</span></span> <span data-ttu-id="5daaf-106">U kunt ook een API zoals Hallo van .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="5daaf-106">You can also use an API like hello .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

