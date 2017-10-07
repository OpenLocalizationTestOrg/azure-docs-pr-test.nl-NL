---
title: aaaUsing Windows PowerShell-Scripts tooPublish tooDev en testomgevingen | Microsoft Docs
description: Meer informatie over hoe toouse Windows PowerShell scripts vanuit Visual Studio toopublish toodevelopment en testomgevingen.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a>Met Windows PowerShell scripts toopublish toodev en testomgevingen
Wanneer u een webtoepassing in Visual Studio maakt, kunt u een Windows PowerShell-script dat u later tooautomate Hallo-publicatie van uw website tooAzure als een Web-App in Azure App Service- of een virtuele machine gebruiken kunt genereren. U kunt bewerken en uw vereisten voor Windows PowerShell-script in Hallo Visual Studio-editor toosuit Hallo uitbreiden of Hallo script integreren met bestaande bouwen, testen en publiceren scripts.

Deze scripts kunt u aangepaste versies (ook wel bekend als dev- en testomgevingen) van uw site voor tijdelijk gebruik inrichten. U kan bijvoorbeeld instellen van een bepaalde versie van uw website op een virtuele machine van Azure of op Hallo staging site op een website toorun een test-suite, een bug reproduceren, een bug correctie proefversie test een voorgestelde wijziging of instellen van een aangepaste omgeving voor een demo of presentatie. Nadat u een script dat uw project publiceert hebt gemaakt, kunt u identieke omgevingen door Hallo script opnieuw uit te voeren indien nodig opnieuw of Hallo script uitgevoerd met uw eigen build van uw toepassing web toocreate een aangepaste omgeving voor het testen.

## <a name="what-you-need"></a>Wat u nodig hebt
* Azure SDK 2.3 of hoger. Zie [Visual Studio-Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) voor meer informatie.

U hoeft niet hello Azure SDK toogenerate Hallo scripts voor webprojecten. Deze functie is voor webprojecten, niet webrollen in cloudservices.

* Azure PowerShell 0.7.4 of hoger. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie.
* [Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) of hoger.

## <a name="additional-tools"></a>Extra hulpprogramma 's
Extra hulpprogramma's en bronnen voor het werken met PowerShell in Visual Studio voor het ontwikkelen van Azure zijn beschikbaar. Zie [PowerShell-Tools voor Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).

## <a name="generating-hello-publish-scripts"></a>Scripts genereren Hallo publiceren
U kunt genereren Hallo publiceren scripts voor een virtuele machine die als host fungeert voor uw website wanneer u een nieuw project met de volgende maakt [deze instructies](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). U kunt ook [genereren van scripts voor web-apps publiceren in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).

## <a name="scripts-that-visual-studio-generates"></a>Scripts die door Visual Studio gegenereerd
Visual Studio-oplossing niveau map met de naam gegenereerd **PublishScripts** die twee Windows PowerShell-bestanden bevat een script publiceren voor de virtuele machine of website en een module die bevat functies die u kunt in hello gebruiken scripts. Een bestand Visual Studio ook gegenereerd in JSON-indeling voor Hallo waarmee Hallo-details van Hallo-project die u implementeert.

### <a name="windows-powershell-publish-script"></a>Windows PowerShell publiceren script
Hallo publiceren script bevat specifieke stappen voor het implementeren van tooa website of virtuele machine te publiceren. Visual Studio biedt syntaxis kleuren voor de ontwikkeling van Windows PowerShell. Help voor Hallo functies beschikbaar is en u kunt Hallo-functies in Hallo script toosuit uw veranderende vereisten vrijelijk bewerken.

### <a name="windows-powershell-module"></a>Windows PowerShell-module
Windows PowerShell-module die Visual Studio gegenereerd bevat functies die Hallo Hallo publiceren script gebruikt. Dit zijn functies van Azure PowerShell en geen beoogde toobe gewijzigd. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie.

### <a name="json-configuration-file"></a>JSON-configuratiebestand
Hallo JSON-bestand wordt gemaakt in Hallo **configuraties** map en configuratiegegevens die Hiermee geeft u precies welke resources toodeploy tooAzure bevat. Hallo-naam van Hallo-bestand dat door Visual Studio gegenereerd is project-naam-WAWS-dev.json als u een website of project de naam van VM dev.json gemaakt als u een virtuele machine hebt gemaakt. Hier volgt een voorbeeld van een JSON-configuratiebestand die wordt gegenereerd wanneer u een website hebt gemaakt. De meeste waarden Hallo behoeven geen uitleg. naam van de website Hello wordt gegenereerd door Azure, zodat deze mogelijk niet overeen met de projectnaam van uw.

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
Wanneer u een virtuele machine maakt, lijkt de JSON-configuratiebestand Hallo vergelijkbare toohello volgende. Houd er rekening mee dat een service in de cloud als een container voor Hallo virtuele machine wordt gemaakt. Hallo virtuele machine bevat Hallo gebruikelijke eindpunten voor internettoegang via HTTP en HTTPS, evenals de eindpunten voor Web Deploy waarmee u toohello website vanuit uw lokale computer, extern bureaublad en Windows PowerShell publiceren.

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

U kunt bewerken Hallo JSON configuratie toochange wat er gebeurt tijdens het uitvoeren van Hallo scripts publiceren. Hallo `cloudService` en `virtualMachine` secties zijn vereist, maar u kunt verwijderen Hallo `databases` sectie als u deze niet nodig. Hallo-eigenschappen die zijn leeg in het configuratiebestand van het Hallo-standaard die door Visual Studio gegenereerd zijn optioneel. die waarden in het standaardconfiguratiebestand Hallo zijn vereist.

Als u een website met meerdere implementatieomgevingen (bekend als sleuven) in plaats van een productiesite één in Azure hebt, kunt u de naam van de site Hallo in Hallo-naam van Hallo-website in JSON-configuratiebestand Hallo kunt opnemen. Bijvoorbeeld, als er een website met de naam **persoonlijke site** en een site voor deze met de naam **testen** vervolgens Hallo URI persoonlijke site test.cloudapp.net is, maar Hallo juiste naam toouse in Hallo-configuratiebestand mysite(test) is . U kunt dit alleen doen als het Hallo-website en sleuven al in uw abonnement bestaat. Als deze nog niet bestaan, Hallo website maken met een Hallo script zonder op te geven Hallo sleuf en maak vervolgens Hallo sleuf in Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), en daarna Hallo script uitgevoerd met de naam van de aangepaste website Hallo. Zie voor meer informatie over implementatiesites voor web-apps, [faseringsomgevingen voor web-apps in Azure App Service instellen](app-service-web/web-sites-staged-publishing.md).

## <a name="how-toorun-hello-publish-scripts"></a>Hoe toorun Hallo scripts publiceren
Als u een Windows PowerShell-script voordat nooit hebt uitgevoerd, moet u eerst Hallo uitvoering beleid tooenable scripts toorun instellen. Dit is een functie voor beveiliging tooprevent gebruikers Windows PowerShell-scripts worden uitgevoerd als ze kwetsbaar toomalware of virussen die betrekking hebben op het uitvoeren van scripts.

### <a name="run-hello-script"></a>Hallo-script uitvoeren
1. Web Deploy Hallo-pakket voor uw project maken. Een Web Deploy-pakket is een gecomprimeerd archief (ZIP-bestand) met bestanden die u wilt toocopy tooyour website of virtuele machine. U kunt Web Deploy-pakketten in Visual Studio maken voor een webtoepassing.

![Maken van webinhoud pakket implementeren](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

Zie voor meer informatie [procedure: een Web-implementatiepakket maken in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx). U kunt ook Hallo maken van uw Web Deploy-pakket, automatiseren zoals beschreven in de sectie Hallo **aanpassen en uitbreiden van Hallo publiceren scripts** verderop in dit onderwerp.

1. In **Solution Explorer**, open Hallo contextmenu voor Hallo script en kies vervolgens **openen met de PowerShell ISE**.
2. Als dit Hallo eerst die u Windows PowerShell-scripts op deze computer uitvoeren hebt, open een opdrachtpromptvenster met Administrator-bevoegdheden en type Hallo volgende opdracht:

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. Meld u tooAzure met behulp van de volgende opdracht Hallo.

    ```powershell
    Add-AzureAccount
    ```

    Als u wordt gevraagd, geeft u uw gebruikersnaam en wachtwoord.

    Houd er rekening mee dat wanneer u Hallo script automatiseren, deze methode van het bieden van Azure-referenties werken niet. In plaats daarvan moet u Hallo .publishsettings-bestand tooprovide referenties gebruiken. Één keer alleen u Hallo-opdracht gebruiken **Get-AzurePublishSettingsFile** toodownload Hallo bestand van Azure, en gebruik daarna **importeren AzurePublishSettingsFile** tooimport Hallo-bestand. Zie voor gedetailleerde instructies [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

4. (Optioneel) Als u wilt dat toocreate Azure-resources, zoals Hallo virtuele machine, database en website zonder het publiceren van uw webtoepassing hello gebruiken **publiceren WebApplication.ps1** opdracht Hello **-configuratie** argument ingesteld toohello JSON-configuratiebestand. Met deze opdrachtregel wordt Hallo JSON configuration file toodetermine welke resources toocreate gebruikt. Omdat Hallo standaardinstellingen worden gebruikt voor andere opdrachtregelargumenten, Hallo resources maakt, maar uw webtoepassing niet publiceren. Hallo-biedt optie Verbose u meer informatie over wat er gebeurt.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. Gebruik Hallo **publiceren WebApplication.ps1** opdracht zoals weergegeven in een van de Hallo voorbeelden tooinvoke Hallo script volgen en publiceren van uw webtoepassing. Als u andere argumenten, zoals de naam voor het abonnement van Hallo toooverride Hallo standaardinstellingen voor alle Hallo moet publiceren pakketnaam, de referenties van de virtuele machine of de referenties voor de database, kunt u deze parameters opgeven. Gebruik Hallo **– uitgebreid** optie toosee meer informatie over de voortgang van Hallo Hallo publicatieproces.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    Als u een virtuele machine maakt, eruit Hallo opdracht Hallo volgende. In dit voorbeeld ziet ook hoe toospecify Hallo-referenties voor meerdere databases. Hallo virtuele machines die deze scripts maken, is Hallo SSL-certificaat niet van een vertrouwde basiscertificeringsinstantie. Daarom moet u toouse hello **– AllowUntrusted** optie.

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    Hallo script databases kunt maken, maar het database-servers niet maken. Als u een databaseserver toocreate wilt, kunt u Hallo **nieuw AzureSqlDatabaseServer** functie in hello Azure-module.

## <a name="customizing-and-extending-hello-publish-scripts"></a>Aanpassen en uitbreiden Hallo publiceren scripts
U kunt aanpassen Hallo script en JSON-configuratiebestand publiceren. functies in Windows PowerShell-module Hallo Hallo **AzureWebAppPublishModule.psm1** zijn niet bedoeld toobe gewijzigd. Als u alleen toospecify een andere database of bepaalde Hallo eigenschappen van Hallo virtuele machine wijzigen, moet u Hallo JSON-configuratiebestand bewerken. Als u wilt dat tooextend Hallo functionaliteit van Hallo script tooautomate maken en testen van uw project, kunt u de functie stubs in implementeren **publiceren WebApplication.ps1**.

het bouwen van uw project tooautomate code toevoegen die MSBuild-aanroepen te`New-WebDeployPackage` zoals in dit codevoorbeeld. Hallo pad toohello MSBuild-opdracht is verschillend, afhankelijk van het Hallo-versie van Visual Studio die u hebt geïnstalleerd. tooget Hallo juiste pad, kunt u de functie Hallo **Get-MSBuildCmd**, zoals wordt weergegeven in dit voorbeeld.

### <a name="tooautomate-building-your-project"></a>tooautomate bouwen van uw project
1. Hallo toevoegen `$ProjectFile` parameter in Hallo globale param sectie.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Hallo functie kopiëren `Get-MSBuildCmd` in het scriptbestand.

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. Vervang `New-WebDeployPackage` Hello volgende code en vervang de tijdelijke aanduidingen Hallo bij het maken van de regel Hallo `$msbuildCmd`. Deze code is voor Visual Studio 2015. Als u Visual Studio 2013, wijzigt u Hallo **VisualStudioVersion** eigenschap hieronder te`12.0`.

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    toobuild uw webtoepassing, MsBuild.exe gebruikt. Zie voor informatie over MSBuild-Naslaggids op: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a>Uitvoering van de opdracht build Hallo starten

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Hallo aanroepen `New-WebDeployPackage` functie voordat deze regel: `$Config = Read-ConfigFile $Configuration` voor web-apps of `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` voor virtuele machines.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. Hallo aangepast script vanaf de opdrachtregel met doorgeven Hallo aanroepen `$Project` argument, zoals in Hallo opdrachtregel voorbeeld te volgen.

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    code te tooautomate testen van uw toepassing toevoegen`Test-WebApplication`. Worden ervoor toouncomment Hallo regels in **publiceren WebApplication.ps1** waar deze functies worden aangeroepen. Als u een implementatie niet opgeeft, kunt u uw project met Visual Studio handmatig maken en vervolgens uitvoeren Hallo script toopublish tooAzure publiceren.

## <a name="publishing-function-summary"></a>Publishing functie samenvatting
tooget help voor functies die u bij Hallo Windows PowerShell-opdrachtprompt gebruiken kunt, gebruik Hallo opdracht `Get-Help function-name`. Hallo help bevat parameter help en voorbeelden. Hallo dezelfde help-tekst ook in Hallo-scriptbestanden bron is **AzureWebAppPublishModule.psm1** en **publiceren WebApplication.ps1**. Hallo-script en de help worden in uw taal Visual Studio gelokaliseerd.

**AzureWebAppPublishModule**

| Functienaam | Beschrijving |
| --- | --- |
| Voeg AzureSQLDatabase |Maakt een nieuwe Azure SQL-database. |
| Voeg AzureSQLDatabases |Maakt Azure SQL-databases van Hallo-waarden in Hallo JSON-configuratiebestand dat Visual Studio gegenereerd. |
| -AzureVM |Hiermee maakt u een virtuele machine van Azure en retourneert dat Hallo-URL van Hallo VM geïmplementeerd. Hallo functie stelt vereisten Hallo en vervolgens aanroepen Hallo **New-AzureVM** toocreate (Azure module) een nieuwe virtuele machine werkt. |
| Voeg AzureVMEndpoints |Nieuwe virtuele machine van de invoereindpunten tooa toegevoegd en Hallo virtuele machine met het nieuwe eindpunt Hallo retourneert. |
| Voeg AzureVMStorage |Maakt een nieuwe Azure storage-account in het huidige abonnement Hallo. Hallo-naam van Hallo account begint met 'devtest' gevolgd door een unieke alfanumerieke tekenreeks. Hallo-functie retourneert Hallo-naam van nieuw opslagaccount Hallo. U moet een locatie of een affiniteitsgroep voor Hallo nieuwe opslagaccount opgeven. |
| Voeg AzureWebsite |Hiermee maakt een website met Hallo opgegeven naam en locatie. Deze functie aanroepen Hallo **nieuw AzureWebsite** functie in hello Azure-module. Als het Hallo-abonnement niet al een website met de opgegeven naam Hallo bevat, wordt deze functie Hallo website maakt en retourneert een object van de website. Anders is het resultaat `$null`. |
| Back-up-abonnement |Slaat de huidige Azure-abonnement in Hallo Hallo `$Script:originalSubscription` variabele in script-bereik. Hiermee slaat u deze functie Hallo huidige Azure-abonnement (verkregen met `Get-AzureSubscription -Current`) en de storage-account en Hallo-abonnement dat door dit script wordt gewijzigd (opgeslagen in variabele Hallo `$UserSpecifiedSubscription`) en de opslagaccount in script-bereik. Hallo waarden opslaat, kunt u een functie, zoals `Restore-Subscription`, toorestore Hallo oorspronkelijke huidige abonnement en opslag toocurrent accountstatus als Hallo huidige status is gewijzigd. |
| Zoek-AzureVM |Hallo opgehaald opgegeven virtuele machine van Azure. |
| Indeling DevTestMessageWithTime |Voegt Hallo datum en tijd tooa bericht toe. Deze functie is ontworpen voor berichten die de fout en uitgebreid streams toohello worden geschreven. |
| Get-AzureSQLDatabaseConnectionString |Een verbinding tekenreeks tooconnect tooan Azure SQL database ophaalprotocol. |
| Get-AzureVMStorage |Retourneert de naam van eerste opslagaccount met naampatroon Hallo HALLO hallo ' devtest*' (hoofdlettergevoelig) in de opgegeven locatie of affiniteit groep Hallo. Als Hallo ' devtest*' storage-account komt niet overeen met Hallo locatie of affiniteitsgroep, Hallo functie negeert deze. U moet een locatie of een affiniteitsgroep opgeven. |
| Get-MSDeployCmd |Retourneert een opdracht toorun hello MsDeploy.exe hulpprogramma. |
| Nieuwe AzureVMEnvironment |Zoeken naar of maakt een virtuele machine in Hallo-abonnement dat overeenkomt met de waarden in de JSON-configuratiebestand Hallo Hallo. |
| Publiceren WebPackage |Maakt gebruik van MsDeploy.exe en een web-pakket niet publiceren. Het ZIP-bestand toodeploy resources tooa website. Deze functie biedt geen uitvoer gegenereerd. Als Hallo aanroep tooMSDeploy.exe mislukt, er Hallo functie een uitzondering gegenereerd. meer gedetailleerde uitvoer, gebruik Hallo tooget **-uitgebreide** optie. |
| Publiceren WebPackageToVM |Controleert of de parameterwaarden Hallo en roept vervolgens Hallo **publiceren WebPackage** functie. |
| Lees ConfigFile |Hallo JSON-configuratiebestand valideert en retourneert een hashtabel met geselecteerde waarden. |
| Restore-abonnement |Hiermee stelt u Hallo huidige abonnement toohello oorspronkelijke abonnement. |
| Test AzureModule |Retourneert `$true` als geïnstalleerd hello Azure moduleversie 0.7.4 of hoger. Retourneert `$false` als Hallo-module is niet geïnstalleerd of een eerdere versie. Deze functie heeft geen parameters. |
| Test AzureModuleVersion |Retourneert `$true` als Hallo-versie van hello Azure-module 0.7.4 is of hoger. Retourneert `$false` als Hallo-module is niet geïnstalleerd of een eerdere versie. Deze functie heeft geen parameters. |
| Test HttpsUrl |Converteert Hallo invoer-URL tooa System.Uri-object. Retourneert `$True` als Hallo-URL absoluut is en het bijbehorende schema https is. Retourneert `$false` als Hallo URL relatief is, het schema is niet HTTPS of Hallo invoerreeks geconverteerde tooa URL mag niet. |
| Test-lid |Retourneert `$true` als een eigenschap of methode lid is van Hallo-object. Anders retourneert `$false`. |
| Schrijven ErrorWithTime |Schrijft een foutbericht dat wordt voorafgegaan door Hallo huidige tijd. Deze functie aanroepen Hallo **indeling DevTestMessageWithTime** functie tooprepend Hallo altijd vóór het Hallo-bericht toohello foutstroom schrijven. |
| Schrijven HostWithTime |Een bericht toohello hostprogramma schrijft (**Write-Host**) voorafgegaan door Hallo huidige tijd. Hallo effect van het schrijven van toohello hostprogramma varieert. De meeste programma's die als host fungeren voor Windows PowerShell deze berichten toostandard uitvoer schrijven. |
| Schrijven VerboseWithTime |Schrijft een uitgebreid bericht voorafgegaan door Hallo huidige tijd. Omdat deze wordt aangeroepen **Write-Verbose**, het Hallo-bericht geeft alleen wanneer Hallo script wordt uitgevoerd met Hallo **uitgebreid** parameter of wanneer Hallo **VerbosePreference** voorkeur is Stel te**doorgaan**. |

**Publiceren WebApplication**

| Functienaam | Beschrijving |
| --- | --- |
| Nieuwe AzureWebApplicationEnvironment |Azure-resources, zoals een website of virtuele machine maakt. |
| Nieuwe WebDeployPackage |Deze functie is niet geïmplementeerd. U kunt opdrachten toevoegen in deze functie toobuild uw project. |
| Publiceren AzureWebApplication |Een web application tooAzure publiceert. |
| Publiceren WebApplication |Maakt en Web-Apps, virtuele machines, SQL-databases en storage-accounts voor een Visual Studio-webproject implementeert. |
| Test-WebApplication |Deze functie is niet geïmplementeerd. U kunt opdrachten toevoegen in deze functie tootest uw toepassing. |

## <a name="next-steps"></a>Volgende stappen
Meer informatie over PowerShell-scripts door te lezen [met Windows PowerShell-scripts](https://technet.microsoft.com/library/bb978526.aspx) en Zie andere Azure PowerShell-scripts op Hallo [Script Center](https://azure.microsoft.com/documentation/scripts/).
