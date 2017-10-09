## <a name="set-up-your-development-environment"></a>De ontwikkelomgeving instellen
Vervolgens stelt u uw ontwikkelomgeving in Visual Studio zodat u klaar tootry Hallo-codevoorbeelden in deze handleiding bent.

### <a name="create-a-windows-console-application-project"></a>Een Windows-consoletoepassingsproject maken
Maak in Visual Studio een nieuwe Windows-consoletoepassing. Hallo stappen ziet u hoe toocreate een consoletoepassing in Visual Studio 2017 echter Hallo stappen zijn vergelijkbaar in andere versies van Visual Studio.

1. Selecteer **Bestand** > **Nieuw** > **Project**
2. Selecteer **Geïnstalleerd** > **Sjablonen** > **Visual C#** > **Klassiek Windows-bureaublad**
3. Selecteer **Consoletoepassing (.NET Framework)**
4. Voer een naam voor uw toepassing in Hallo **naam:** veld
5. Selecteer **OK**

![Dialoogvenster voor het maken van een project in Visual Studio](./media/storage-development-environment-include/storage-development-environment-include-1.png)

Alle codevoorbeelden in deze zelfstudie kunnen worden toegevoegd toohello `Main()` methode van uw consoletoepassing `Program.cs` bestand.

U kunt hello Azure Storage-clientbibliotheek gebruiken in elk type .NET-toepassing, met inbegrip van een Azure-cloud service of web-app en desktop- en mobiele toepassingen. In deze gids gebruiken we een consoletoepassing voor de eenvoud.

### <a name="use-nuget-tooinstall-hello-required-packages"></a>Gebruik NuGet tooinstall vereist hello-pakketten
Er zijn twee pakketten die u in deze zelfstudie tooreference in uw project toocomplete nodig:

* [Microsoft Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): dit pakket biedt programmatisch toegang toodata resources in uw opslagaccount.
* [Configuration Manager-bibliotheek van Microsoft Azure voor .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): dit pakket biedt een klasse voor het parseren van een verbindingsreeks in een configuratiebestand, ongeacht waar de toepassing wordt uitgevoerd.

U kunt beide pakketten NuGet tooobtain. Volg deze stappen:

1. Klik met de rechtermuisknop op het project in **Solution Explorer** en kies **NuGet-pakketten beheren**.
2. Zoek online naar 'WindowsAzure.Storage' en klik op **installeren** tooinstall Hallo Storage-clientbibliotheek en de bijbehorende afhankelijkheden.
3. Zoek online naar 'WindowsAzure.ConfigurationManager' en klik op **installeren** tooinstall hello Azure Configuration Manager.

> [!NOTE]
> Hallo-pakket voor Storage-clientbibliotheek is ook opgenomen in Hallo [Azure SDK voor .NET](https://azure.microsoft.com/downloads/). We raden echter aan dat u de Hallo Storage-clientbibliotheek vanuit NuGet tooensure altijd de meest recente versie van de clientbibliotheek Hallo Hallo te hebben ook installeert.
> 
> Hallo ODataLib-afhankelijkheden in Hallo Storage-clientbibliotheek voor .NET worden opgelost door Hallo ODataLib-pakketten zijn beschikbaar op NuGet niet van WCF Data Services. Hallo ODataLib-bibliotheken kunnen rechtstreeks worden gedownload of waarnaar wordt verwezen door het CodeProject via NuGet. Hallo specifieke ODataLib-pakketten die worden gebruikt door Hallo Storage-clientbibliotheek zijn [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), en [Spatial](http://nuget.org/packages/System.Spatial/). Hoewel deze bibliotheken door hello Azure Table-Opslagklassen worden gebruikt, zijn ze vereiste afhankelijkheden voor het programmeren met Hallo Storage-clientbibliotheek.
> 
> 

### <a name="determine-your-target-environment"></a>De doelomgeving bepalen
U hebt twee omgevingsopties voor het uitvoeren van Hallo voorbeelden in deze handleiding:

* U kunt de code uitvoeren met een Azure Storage-account in Hallo cloud. 
* U kunt de code uitvoeren met hello Azure-opslagemulator. Hallo-opslagemulator is een lokale omgeving die een Azure Storage-account in Hallo cloud emuleert. Hallo-emulator is een gratis optie voor het testen en foutopsporing van uw code terwijl de toepassing nog in ontwikkeling. Hallo-emulator maakt gebruik van een bekend account en de sleutel. Zie voor meer informatie [gebruik hello Azure-Opslagemulator voor ontwikkeling en testen](../articles/storage/common/storage-use-emulator.md)

Als u voor een opslagaccount in de cloud hello ontwikkelt, kopieert u Hallo primaire toegangssleutel voor uw storage-account van hello Azure-portal. Zie [Opslagtoegangssleutels bekijken en kopiëren](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys) voor meer informatie.

> [!NOTE]
> U kunt richten Hallo storage emulator tooavoid mogelijke kosten die zijn gekoppeld aan Azure Storage. Als u tootarget Azure storage-account in de cloud hello kiest, wordt kosten voor het uitvoeren van deze zelfstudie wel te verwaarlozen.
> 
> 

### <a name="configure-your-storage-connection-string"></a>De opslagverbindingsreeks configureren
Hello Azure Storage-clientbibliotheek voor .NET ondersteunt het gebruik van een storage connection string tooconfigure eindpunten en referenties voor toegang tot opslagservices. de beste manier toomaintain Hallo uw verbindingsreeks voor opslag is in een configuratiebestand. 

Zie voor meer informatie over verbindingsreeksen [configureren van een verbindingsreeks tooAzure opslag](../articles/storage/common/storage-configure-connection-string.md).

> [!NOTE]
> Sleutel van uw opslagaccount is vergelijkbaar toohello hoofdwachtwoord voor uw opslagaccount. Altijd worden zorgvuldige tooprotect sleutel van uw opslagaccount. Vermijd het distribueren van tooother gebruikers, bewaar of in een tekstbestand dat toegankelijk tooothers opslaat. Genereer een nieuwe sleutel met behulp van hello Azure-portal als u denkt dat is aangetast.
> 
> 

tooconfigure uw verbindingsreeks, open Hallo `app.config` bestand vanuit Solution Explorer in Visual Studio. Hallo-inhoud van Hallo toevoegen `<appSettings>` element hieronder weergegeven. Vervang `account-name` met Hallo-naam van uw opslagaccount en `account-key` door uw toegangssleutel voor account:

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

De configuratie-instelling ziet er ongeveer als volgt uit:

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

tootarget hello opslagemulator, kunt u een snelle manier toohello bekende accountnaam en de sleutel toewijzen. In dat geval heeft de verbindingsreeks de volgende instelling:

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

