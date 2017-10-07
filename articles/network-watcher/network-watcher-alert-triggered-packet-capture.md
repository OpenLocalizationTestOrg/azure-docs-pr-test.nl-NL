---
title: netwerk-aaaUse pakket vastleggen toodo proactieve controle met waarschuwingen en Azure Functions | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocreate een waarschuwing geactiveerd pakketopname met Azure-netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a>Pakketopname voor proactieve netwerkbewaking met waarschuwingen en Azure Functions gebruiken

Netwerk-Watcher pakketopname maakt vastleggen sessies tootrack verkeer naar en vanuit virtuele machines. Hallo vastleggen bestand hebben een filter dat is gedefinieerd tootrack Hallo alleen verkeer dat u wilt dat toomonitor. Deze gegevens worden vervolgens opgeslagen in een blob storage of lokaal op de gastmachine Hallo.

Deze mogelijkheid kan op afstand worden gestart vanuit andere automation-scenario's zoals Azure Functions. Pakket vastleggen biedt die u de mogelijkheid toorun proactieve opnamen op basis van Hallo gedefinieerd netwerk afwijkingen. Andere toepassingen zijn onder andere netwerkstatistieken, informatie ophalen over het netwerk beveiligingsrisico's en foutopsporing client-servercommunicaties verzamelen.

Resources die zijn geïmplementeerd in Azure 24/7 worden uitgevoerd. U en uw medewerkers kan actief Hallo status van alle bronnen 24/7 niet bewaken. Wat gebeurt bijvoorbeeld als er een probleem optreedt op 2 uur?

Met behulp van de netwerk-Watcher, waarschuwingen en functies van binnen hello Azure ecosysteem, kunt u proactief reageren met Hallo gegevens en hulpprogramma's voor toosolve problemen in uw netwerk.

![Scenario][scenario]

## <a name="prerequisites"></a>Vereisten

* meest recente versie van Hallo [Azure PowerShell](/powershell/azure/install-azurerm-ps).
* Een bestaand exemplaar van netwerk-Watcher. Als u nog geen hebt, [geen exemplaar maken van netwerk-Watcher](network-watcher-create.md).
* Een bestaande virtuele machine in Hallo dezelfde regio bevinden als de netwerk-Watcher Hello [Windows extensie](../virtual-machines/windows/extensions-nwa.md) of [extensie van de virtuele machine Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="scenario"></a>Scenario

In dit voorbeeld wordt de virtuele machine verzendt TCP-segmenten meer dan normaal en gewenste toobe gewaarschuwd. TCP-segmenten als voorbeeld hier worden gebruikt, maar u kunt meldingsvoorwaarde.

Wanneer u wordt gewaarschuwd, wilt u tooreceive pakketniveau gegevens toounderstand waarom communicatie is toegenomen. Vervolgens kunt u stappen ondernemen tooreturn Hallo virtuele machine tooregular communicatie.

Dit scenario wordt ervan uitgegaan dat u een bestaand exemplaar van de netwerk-Watcher en een resourcegroep met een geldige virtuele machine hebt.

Hallo lijst volgende is een overzicht van Hallo werkstroom die uitgevoerd wordt:

1. Een waarschuwing wordt geactiveerd op de virtuele machine.
1. Hallo waarschuwing aanroepen uw Azure-functie via een webhook.
1. Uw Azure-functie Hallo waarschuwing verwerkt en wordt een netwerk-Watcher pakket capture-sessie gestart.
1. Hallo pakketopname op Hallo VM wordt uitgevoerd en verzamelt verkeer.
1. Hallo pakket vastleggen bestand wordt geüpload tooa opslagaccount voor controle en diagnose.

tooautomate dit proces we maken en een verbinding maken met een waarschuwing op onze tootrigger VM wanneer Hallo incident voordoet. We ook maken een functie toocall in netwerk-Watcher.

Dit scenario Hallo te volgen:

* Hiermee maakt u een Azure-functie die een pakketopname begint.
* Een waarschuwingsregel maakt op een virtuele machine en Hallo waarschuwingsregel toocall hello Azure functie configureert.

## <a name="create-an-azure-function"></a>Een Azure-functie maken

de eerste stap Hallo toocreate is een Azure-functie tooprocess Hallo waarschuwing en een pakketopname maken.

1. In Hallo [Azure-portal](https://portal.azure.com), selecteer **nieuw** > **Compute** > **functie-App**.

    ![Een functie-app maken][1-1]

2. Op Hallo **functie-App** blade Voer Hallo waarden te volgen en selecteer vervolgens **OK** toocreate Hallo app:

    |**Instelling** | **Waarde** | **Details** |
    |---|---|---|
    |**Naam van app**|PacketCaptureExample|Hallo-naam van Hallo functie-app.|
    |**Abonnement**|[Uw abonnement] Hallo abonnement voor welke toocreate Hallo functie-app.||
    |**Resourcegroep**|PacketCaptureRG|Hallo resource groep toocontain Hallo functie-app.|
    |**Hosting-Plan**|Plan voor verbruik| Hallo type plan uw app functie gebruikt. Opties zijn verbruik of Azure App Service-abonnement. |
    |**Locatie**|VS - midden| Hallo regio in welke toocreate Hallo functie-app.|
    |**Storage-Account**|{automatisch gegenereerde}| Hallo-opslagaccount waarvoor Azure Functions voor opslagaccounts voor algemeen gebruik.|

3. Op Hallo **PacketCaptureExample functie Apps** blade Selecteer **functies** > **aangepaste functie**  >  **+**.

4. Selecteer **HttpTrigger Powershell**, en voer vervolgens de resterende gegevens Hallo. Ten slotte toocreate Hallo functie, selecteer **maken**.

    |**Instelling** | **Waarde** | **Details** |
    |---|---|---|
    |**Scenario**|experimentele|Type van scenario|
    |**Een naam voor de functie opgeven**|AlertPacketCapturePowerShell|Naam van de functie Hallo|
    |**Machtigingsniveau**|Functie|Autorisatieniveau voor Hallo-functie|

![Voorbeeld van de functies][functions1]

> [!NOTE]
> Hallo PowerShell sjabloon experimentele is en geen volledige ondersteuning.

Aanpassingen zijn vereist voor dit voorbeeld en worden beschreven in Hallo stappen te volgen.

### <a name="add-modules"></a>Modules toevoegen

toouse netwerk-Watcher PowerShell-cmdlets Hallo nieuwste PowerShell-module toohello functie app uploaden.

1. Voer op uw lokale computer met de Hallo nieuwste Azure PowerShell-modules geïnstalleerd Hallo volgende PowerShell-opdracht:

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    Dit voorbeeld kunt u het lokale pad naar uw Azure PowerShell-modules Hallo. Deze mappen worden gebruikt in een later stadium. Hallo-modules die worden gebruikt in dit scenario zijn:

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

    ![PowerShell-mappen][functions5]

1. Selecteer **werken app-instellingen** > **tooApp Service Editor gaat**.

    ![De functie app-instellingen][functions2]

1. Klik met de rechtermuisknop Hallo **AlertPacketCapturePowershell** map, en maak vervolgens een map met de naam **azuremodules**. 

4. Maak een submap voor elke module die u nodig hebt.

    ![Map en submappen][functions3]

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

1. Klik met de rechtermuisknop Hallo **AzureRM.Network** submap en selecteer vervolgens **bestanden uploaden**. 

6. Ga tooyour Azure modules. In de lokale Hallo **AzureRM.Network** map, selecteert u alle Hallo-bestanden in Hallo-map. Selecteer vervolgens **OK**. 

7. Herhaal deze stappen voor **AzureRM.Profile** en **AzureRM.Resources**.

    ![Bestanden uploaden][functions6]

1. Nadat u klaar bent, elke map moet Hallo PowerShell-module bestanden naar uw lokale machine hebben.

    ![Bestanden met PowerShell][functions7]

### <a name="authentication"></a>Authentication

toouse hello PowerShell-cmdlets die u moet verifiëren. U configureren verificatie in Hallo functie-app. tooconfigure verificatie, moet u omgevingsvariabelen configureren en een versleutelde sleutelbestand toohello functie-app uploaden.

> [!NOTE]
> Dit scenario biedt één voorbeeld van hoe u tooimplement verificatie met Azure Functions. Er zijn andere manieren toodo dit.

#### <a name="encrypted-credentials"></a>Versleutelde referenties

Hallo volgende PowerShell-script maakt een sleutelbestand aangeroepen **PassEncryptKey.key**. Het bevat ook een versleutelde versie van Hallo wachtwoord dat wordt meegeleverd. Dit wachtwoord wordt Hallo hetzelfde wachtwoord dat is gedefinieerd voor hello Azure Active Directory-toepassing die wordt gebruikt voor verificatie.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

Maak een map met de naam in App Service-Editor van functie-app Hallo Hallo, **sleutels** onder **AlertPacketCapturePowerShell**. Vervolgens uploaden Hallo **PassEncryptKey.key** -bestand dat u hebt gemaakt in de vorige PowerShell-voorbeeld Hallo.

![Functies sleutel][functions8]

### <a name="retrieve-values-for-environment-variables"></a>Waarden voor omgevingsvariabelen ophalen

de laatste vereiste Hallo is tooset up Hallo omgevingsvariabelen die nodig zijn tooaccess Hallo waarden voor verificatie. Hallo bevat volgende lijst Hallo omgevingsvariabelen die zijn gemaakt:

* AzureClientID

* AzureTenant

* AzureCredPassword


#### <a name="azureclientid"></a>AzureClientID

Hallo client-ID is Hallo toepassings-ID van een toepassing in Azure Active Directory.

1. Als u een toepassing toouse nog geen hebt, een toepassing uitvoeren Hallo toocreate voorbeeld te volgen.

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > Hallo-wachtwoord dat u bij het maken van de toepassing hello moet Hallo hetzelfde wachtwoord dat u eerder hebt gemaakt bij het opslaan van Hallo-sleutelbestand.

1. Selecteer in de Azure-portal hello, **abonnementen**. Hallo abonnement toouse selecteren en selecteer vervolgens **toegangsbeheer (IAM)**.

    ![De IAM-functies][functions9]

1. Kies Hallo account toouse en selecteer vervolgens **eigenschappen**. Kopieer Hallo toepassing-ID.

    ![Functies toepassings-ID][functions10]

#### <a name="azuretenant"></a>AzureTenant

Hallo tenant-ID verkrijgen door het volgende PowerShell-voorbeeld Hallo uitvoeren:

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a>AzureCredPassword

Hallo-waarde van Hallo AzureCredPassword omgevingsvariabele is Hallo-waarde die u via de volgende PowerShell-voorbeeld Hallo uitgevoerd. In dit voorbeeld is dezelfde als die wordt weergegeven in de voorgaande Hallo Hallo **versleuteld referenties** sectie. Hallo-waarde die is er nodig is de uitvoer van de Hallo van Hallo `$Encryptedpassword` variabele.  Dit is Hallo service principal wachtwoord die u met behulp van PowerShell-script Hallo versleuteld.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a>Hallo omgevingsvariabelen opslaan

1. Ga toohello functie-app. Selecteer vervolgens **werken app-instellingen** > **app-instellingen configureren**.

    ![App-instellingen configureren][functions11]

1. Hallo omgevingsvariabelen en hun waarden toohello app-instellingen toevoegen en selecteer vervolgens **opslaan**.

    ![App-instellingen][functions12]

### <a name="add-powershell-toohello-function"></a>PowerShell toohello functie toevoegen

Het is nu tijd toomake in netwerk-Watcher van binnen hello Azure-functie aanroepen. Afhankelijk van de vereisten voor Hallo kan Hallo uitvoering van deze functie variëren. De algemene stroom Hallo Hallo code is echter als volgt:

1. Proces-invoerparameters.
2. Het bestaande pakket query tooverify limieten vastgelegd en Naamconflicten oplossen.
3. Maak een pakketopname met toepasselijke parameters.
4. Poll-pakket vastleggen periodiek totdat deze is voltooid.
5. Gebruiker een melding Hallo Hallo pakket opnamesessie is voltooid.

Hallo is volgende voorbeeld PowerShell-code die kan worden gebruikt in Hallo-functie. Er zijn waarden die vervangen moeten voor toobe **subscriptionId**, **resourceGroupName**, en **storageAccountName**.

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a>Hallo functie URL niet ophalen 
1. Nadat u uw functie hebt gemaakt, configureert u uw waarschuwing toocall Hallo-URL die is gekoppeld aan het Hallo-functie. tooget deze waarde kopiëren Hallo function URL van uw app functie.

    ![Hallo function URL zoeken][functions13]

2. Kopieer Hallo functie URL voor uw app functie.

    ![Hallo function URL kopiëren][2]

Als u aangepaste eigenschappen in de nettolading Hallo van Hallo webhook POST-aanvraag nodig hebt, raadpleeg dan te[een webhook configureren op een Azure metrische waarschuwing](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="configure-an-alert-on-a-vm"></a>Een waarschuwing te configureren op een virtuele machine

Waarschuwingen geconfigureerde toonotify personen kunnen zijn wanneer specifieke metrische gegevens overschrijdt de drempelwaarde die toegewezen tooit. In dit voorbeeld Hallo waarschuwing is op Hallo van TCP-segmenten die worden verzonden, maar Hallo-waarschuwing voor veel andere metrische gegevens kan worden geactiveerd. In dit voorbeeld wordt een waarschuwing geconfigureerde toocall een webhook toocall Hallo-functie.

### <a name="create-hello-alert-rule"></a>Hallo waarschuwingsregel maken

Ga tooan bestaande virtuele machine en vervolgens een waarschuwingsregel toevoegen. Meer gedetailleerde documentatie over het configureren van waarschuwingen kan worden gevonden op [waarschuwingen in de Azure-Monitor maken voor Azure-services - Azure-portal](../monitoring-and-diagnostics/insights-alerts-portal.md). Voer Hallo volgende waarden in Hallo **waarschuwingsregel** blade en selecteer vervolgens **OK**.

  |**Instelling** | **Waarde** | **Details** |
  |---|---|---|
  |**Naam**|TCP_Segments_Sent_Exceeded|Naam van de waarschuwingsregel Hallo.|
  |**Beschrijving**|TCP-segmenten verzonden drempelwaarde overschreden|Hallo beschrijving voor de waarschuwingsregel Hallo.||
  |**Gegevens**|TCP-segmenten die zijn verzonden| Hallo metrische toouse tootrigger Hallo waarschuwing. |
  |**Voorwaarde**|Groter dan| Hallo voorwaarde toouse bij het evalueren van Hallo metriek.|
  |**Drempelwaarde**|100| Hallo-waarde van Hallo metriek die Hallo waarschuwing activeert. Deze waarde moet worden ingesteld als tooa geldige waarde voor uw omgeving.|
  |**Periode**|Via Hallo laatste vijf minuten| Hallo periode in welke toolook voor Hallo drempelwaarde op Hallo metriek bepaalt.|
  |**Webhook**|[webhook-URL van de functie-app]| Hallo webhook-URL van Hallo functie-app die is gemaakt in de vorige stappen Hallo.|

> [!NOTE]
> Hallo TCP-segmenten metriek is niet standaard ingeschakeld. Meer informatie over het tooenable aanvullende gegevens in via [inschakelen bewaking en diagnostische gegevens](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).

## <a name="review-hello-results"></a>Bekijkt hello resultaten

Na het Hallo-criteria voor de waarschuwing triggers hello, wordt het vastleggen van een pakket gemaakt. Ga tooNetwork Watcher en selecteer vervolgens **pakketopname**. Op deze pagina kunt u Hallo pakket vastleggen bestand koppeling toodownload hello pakketopname selecteren.

![Weergave pakketopname][functions14]

Als Hallo vastleggen bestand lokaal is opgeslagen, kunt u deze ophalen door in toohello virtuele machine te ondertekenen.

Zie voor instructies over het downloaden van bestanden van Azure storage-accounts [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Een ander hulpprogramma kunt u is [Opslagverkenner](http://storageexplorer.com/).

Nadat het vastleggen is gedownload, kunt u deze bekijken met behulp van een hulpprogramma dat gelezen kan een **CAP** bestand. Hieronder vindt u koppelingen tootwo van deze hulpprogramma's:

- [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)
- [WireShark](https://www.wireshark.org/)

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooview uw pakket worden vastgelegd in via [pakket netwerkopname-analyse met Wireshark](network-watcher-deep-packet-inspection.md).


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
