## <a name="set-up-your-development-environment"></a>De ontwikkelomgeving instellen
Vervolgens stelt u in Visual Studio uw ontwikkelomgeving in, zodat u de codevoorbeelden in deze handleiding kunt uitproberen.

### <a name="create-a-windows-console-application-project"></a>Een Windows-consoletoepassingsproject maken
Maak in Visual Studio een nieuwe Windows-consoletoepassing. In de volgende stappen ziet u hoe u een consoletoepassing maakt in Visual Studio 2017. De stappen zijn nagenoeg gelijk in andere versies van Visual Studio.

1. Selecteer **Bestand** > **Nieuw** > **Project**.
2. Selecteer **Geïnstalleerd** > **Sjablonen** > **Visual C#** > **Klassiek Windows-bureaublad**.
3. Selecteer **Consoletoepassing (.NET Framework)**.
4. Typ een naam voor de toepassing in het veld **Naam:**.
5. Selecteer **OK**.

![Schermopname van het dialoogvenster Nieuw project in Visual Studio](./media/storage-development-environment-include/storage-development-environment-include-1.png)

Alle codevoorbeelden in deze zelfstudie kunnen worden toegevoegd aan de methode `Main()` van het bestand `Program.cs` van de consoletoepassing.

U kunt de Azure Storage-clientbibliotheek gebruiken in elk type .NET-toepassing, waaronder een Azure-cloudservice of -web-app en bureaublad- en mobiele toepassingen. In deze gids gebruiken we een consoletoepassing voor de eenvoud.

### <a name="use-nuget-to-install-the-required-packages"></a>NuGet gebruiken om de vereiste pakketten te installeren
Er zijn twee pakketten waarnaar u in uw project moet verwijzen om deze zelfstudie te kunnen voltooien:

* [Microsoft Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): dit pakket biedt programmatisch toegang tot gegevensbronnen in uw opslagaccount.
* [Configuration Manager-bibliotheek van Microsoft Azure voor .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): dit pakket biedt een klasse voor het parseren van een verbindingsreeks in een configuratiebestand, ongeacht waar de toepassing wordt uitgevoerd.

Met NuGet kunt u beide pakketten verkrijgen. Volg deze stappen:

1. Klik met de rechtermuisknop op het project in **Solution Explorer** en kies **NuGet-pakketten beheren**.
2. Zoek online naar 'WindowsAzure.Storage' en selecteer **Installeren** om de Storage-clientbibliotheek en de afhankelijkheden ervan te installeren.
3. Zoek online naar 'WindowsAzure.ConfigurationManager' en selecteer **Installeren** om Azure Configuration Manager te installeren.

> [!NOTE]
> Het pakket met de Storage-clientbibliotheek is ook opgenomen in de [Azure-SDK voor .NET](https://azure.microsoft.com/downloads/). We raden u echter aan om ook de Storage-clientbibliotheek vanuit NuGet te installeren, zodat u zeker weet dat u altijd de meest recente versie van de clientbibliotheek hebt geïnstalleerd.
> 
> De ODataLib-afhankelijkheden in de Storage-clientbibliotheek voor .NET worden opgelost met de ODataLib-pakketten, die beschikbaar zijn op NuGet, en niet vanuit WCF Data Services. U kunt de ODataLib-bibliotheken rechtstreeks downloaden of u kunt er via NuGet in uw codeproject naar verwijzen. De specifieke ODataLib-pakketten die door de Storage-clientbibliotheek worden gebruikt, zijn [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/) en [Spatial](http://nuget.org/packages/System.Spatial/). Hoewel deze bibliotheken door de Azure Table-opslagklassen worden gebruikt, zijn het verplichte afhankelijkheden voor het programmeren met de Storage-clientbibliotheek.
> 
> 

### <a name="determine-your-target-environment"></a>De doelomgeving bepalen
U kunt de voorbeelden in deze gids in twee omgevingen uitvoeren:

* U kunt de code uitvoeren met een Azure Storage-account in de cloud. 
* U kunt de code uitvoeren met de Azure-opslagemulator. De opslagemulator is een lokale omgeving die een Azure Storage-account in de cloud emuleert. De emulator is een gratis optie waarmee u uw code kunt testen en fouten in de code kunt opsporen terwijl de toepassing nog in ontwikkeling is. De emulator maakt gebruik van een bekend account en een bekende sleutel. Zie [De Azure-opslagemulator gebruiken voor ontwikkeling en testen](../articles/storage/common/storage-use-emulator.md) voor meer informatie.

Als u een opslagaccount in de cloud wilt gebruiken, kopieert u de primaire toegangssleutel voor uw opslagaccount vanuit Azure Portal. Zie [Opslagtoegangssleutels bekijken en kopiëren](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys) voor meer informatie.

> [!NOTE]
> Gebruik de opslagemulator als u mogelijke kosten in verband met Azure-opslag wilt vermijden. Als u er echter voor kiest om een Azure-opslagaccount in de cloud te gebruiken, zijn de kosten voor de uitvoering van deze zelfstudie te verwaarlozen.
> 
> 

### <a name="configure-your-storage-connection-string"></a>De opslagverbindingsreeks configureren
De clientbibliotheek van Azure Storage voor .NET ondersteunt het gebruik van een opslagverbindingsreeks om eindpunten en referenties voor toegang tot opslagservices te configureren. De beste manier om de opslagverbindingsreeks te onderhouden, is met een configuratiebestand. 

Zie [Azure Storage-verbindingsreeksen configureren](../articles/storage/common/storage-configure-connection-string.md) voor meer informatie over verbindingsreeksen.

> [!NOTE]
> De sleutel van uw opslagaccount is vergelijkbaar met het hoofdwachtwoord voor uw opslagaccount. Zorg dat de sleutel van uw opslagaccount altijd is beveiligd. Geef deze niet aan andere gebruikers en bewaar of noteer de sleutel op een veilige manier en plaats. Genereer een nieuwe sleutel via de Azure-portal als er mogelijk inbreuk op de sleutel heeft plaatsgevonden.
> 
> 

U configureert de verbindingsreeks door het bestand `app.config` te openen vanuit Solution Explorer in Visual Studio. Voeg de inhoud van het element `<appSettings>` hieronder toe. Vervang `account-name` door de naam van uw opslagaccount en `account-key` door de toegangssleutel van uw account:

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

Als u de opslagemulator wilt gebruiken, kunt u de bekende accountnaam en -sleutel op een snelle manier toewijzen. In dat geval heeft de verbindingsreeks de volgende instelling:

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

