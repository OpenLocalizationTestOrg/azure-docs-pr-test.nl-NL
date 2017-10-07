---
title: aaaIntegrate logboeken van Azure Sleutelkluis met behulp van Event Hubs | Microsoft Docs
description: Zelfstudie waarmee Hallo nodige toomake Sleutelkluis aanmeldt beschikbaar tooa SIEM met behulp van de integratie van Azure-logboek
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a>Zelfstudie voor Azure Log-integratie: proces Azure Key Vault gebeurtenissen met behulp van Event Hubs

U kunt gebruiken Azure Log integratiegebeurtenissen tooretrieve vastgelegd en zodat ze beschikbaar tooyour informatie en event management (SIEM) beveiligingssysteem. Deze zelfstudie toont een voorbeeld van hoe Azure Log integratie gebruikte tooprocess logboeken die zijn verkregen via Azure Event Hubs kunnen worden.
 
Gebruik deze zelfstudie tooget te weten komen over hoe Azure Log-integratie en Event Hubs werk samen met de volgende voorbeelden van stappen Hallo en kennis van hoe elke stap Hallo-oplossing ondersteunt. En u wat nemen kunt u hebt geleerd hier toocreate uw eigen toosupport stappen unieke vereisten van uw bedrijf.

>[!WARNING]
Hallo stappen en opdrachten in deze zelfstudie zijn niet bedoeld toobe gekopieerd en geplakt. Ze zijn alleen voorbeelden. Gebruik geen Hallo PowerShell-opdrachten 'als zodanig' in uw productieomgeving. U moet deze op basis van uw omgeving aanpassen.


Deze zelfstudie wordt u begeleid Hallo proces duurt Azure Key Vault activiteit vastgelegd tooan event hub en het beschikbaar als JSON-bestanden tooyour SIEM-systeem. Vervolgens kunt u uw SIEM-systeem tooprocess Hallo JSON-bestanden.

>[!NOTE]
>De meeste Hallo stappen in deze zelfstudie hebben betrekking op het configureren van sleutelkluizen, opslagaccounts en event hubs. Hallo specifieke Azure Log integratiestappen zijn Hallo einde van deze zelfstudie. Voer deze stappen niet uit in een productieomgeving. Ze zijn bedoeld voor een testomgeving alleen. Voordat u ze in productie, moet u Hallo stappen aanpassen.

Informatie verstrekt langs Hallo manier helpt dat u begrijpen Hallo redenen achter elke stap. Koppelingen tooother artikelen kunnen u meer details op bepaalde onderwerpen.

Zie voor meer informatie over Hallo-services die in deze zelfstudie wordt vermeld: 

- [Azure Key Vault](../key-vault/key-vault-whatis.md)
- [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Azure-logboekanalyse-integratie](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a>Eerste installatie

Voordat u de stappen in dit artikel Hallo voltooien kunt, moet u Hallo volgende:

1. Een Azure-abonnement en de account op dat abonnement met beheerdersrechten. Als u geen een abonnement hebt, kunt u een [gratis account](https://azure.microsoft.com/free/).
 
2. Een systeem met toegang toohello internet die voldoet aan vereisten voor het installeren van de integratie van Azure Log Hallo. Hallo-systeem kan op een cloudservice of lokale gehost.

3. [Integratie van Azure Log](https://www.microsoft.com/download/details.aspx?id=53324) geïnstalleerd. tooinstall het:

   a. Gebruik extern bureaublad tooconnect toohello system vermeld in stap 2.   
   b. Kopieer hello Azure Log integratie installatieprogramma toohello system. U kunt [Hallo installatiebestanden downloaden](https://www.microsoft.com/download/details.aspx?id=53324).   
   c. Hallo-installatieprogramma start en Hallo-licentievoorwaarden voor Microsoft-Software accepteren.   
   d. Als u telemetrie informatie opgeeft wordt, laat u Hallo selectievakje is ingeschakeld. Schakel Hallo selectievakje uit als u gebruik van informatie tooMicrosoft in plaats daarvan niet verzenden.
   
   Voor meer informatie over de integratie van Azure-logboek en hoe tooinstall, Zie [Azure Log integratie met Azure Diagnostics logboekregistratie en Windows Event Forwarding](security-azure-log-integration-get-started.md).

4. Hallo nieuwste PowerShell-versie.
 
   Als u Windows Server 2016 geïnstalleerd hebt, hebt u ten minste PowerShell 5.0. Als u een andere versie van Windows Server, hebt u mogelijk een oudere versie van PowerShell is geïnstalleerd. U kunt Hallo versie controleren door te voeren ```get-host``` in een PowerShell-venster. Als er geen PowerShell 5.0 is geïnstalleerd, kunt u [downloaden](https://www.microsoft.com/download/details.aspx?id=50395).

   Nadat u ten minste hebt PowerShell 5.0, kunt u de meest recente versie van tooinstall Hallo doorgaan:
   
   a. Voer in een PowerShell-venster Hallo ```Install-Module Azure``` opdracht. Hallo installatiestappen voltooien.    
   b. Voer Hallo ```Install-Module AzureRM``` opdracht. Hallo installatiestappen voltooien.

   Zie voor meer informatie [Azure PowerShell installeren](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).


## <a name="create-supporting-infrastructure-elements"></a>Ondersteunende Infrastructuurelementen maken

1. Open een PowerShell-venster met verhoogde bevoegdheid en gaat u te**C:\Program Files\Microsoft Azure Log integratie**.
2. Importeer Hallo AzLog cmdlets Hallo script LoadAzLogModule.ps1 uit te voeren. Voer Hallo `.\LoadAzLogModule.ps1` opdracht. (Kennisgeving Hallo ". \ ' in die opdracht.) Deze lijst ziet er ongeveer zo uit:</br>

   ![Lijst met modules geladen](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. Voer Hallo `Login-AzureRmAccount` opdracht. Voer in Hallo aanmeldingsvenster Hallo referentie-informatie voor Hallo-abonnement dat u voor deze zelfstudie gebruiken wilt.

   >[!NOTE]
   >Als dit Hallo eerste keer is dat u in tooAzure van deze computer aanmeldt zich is, ziet u een bericht over het toestaan van gebruiksgegevens van Microsoft toocollect PowerShell. U wordt aangeraden deze gegevensverzameling in te schakelen omdat het gebruikte tooimprove Azure PowerShell.

4. U bent aangemeld en ziet u de informatie in de volgende schermafbeelding Hallo Hallo na een geslaagde authenticatie. Let op Hallo abonnement-ID en -abonnement naam, omdat u moet deze stappen toocomplete later.

   ![PowerShell-venster](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. Variabelen toostore waarden maken die later worden gebruikt. Geef alle Hallo volgende PowerShell-regels. Mogelijk moet u tooadjust Hallo waarden toomatch uw omgeving.
    - ```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(De abonnementsnaam van uw kan anders zijn. U ziet het als onderdeel van de uitvoer van de vorige opdracht Hallo Hallo.)
    - ```$location = 'West US'```(Deze variabele niet gebruikte toopass Hallo locatie waar de bronnen moeten worden gemaakt. U kunt deze variabele toobe elke locatie wijzigen van uw keuze.)
    - ```$random = Get-Random```
    - ``` $name = 'azlogtest' + $random```(Hallo-naam kan van alles zijn, maar deze alleen kleine letters en cijfers bevatten.)
    - ``` $storageName = $name```(U kunt deze variabele wordt gebruikt voor de opslagaccountnaam Hallo.)
    - ```$rgname = $name ```(U kunt deze variabele wordt gebruikt voor naam resourcegroep Hallo.)
    - ``` $eventHubNameSpaceName = $name```(Dit is de naam Hallo van Hallo event hub-naamruimte.)
6. Geef Hallo-abonnement dat u met werkt:
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. Een resourcegroep maken:
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   Als u `$rg` op dit moment ziet u uitvoer vergelijkbare toothis schermafbeelding:

   ![Uitvoer na het maken van een resourcegroep](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. Een opslagaccount die gebruikt tookeep bijhouden van informatie over de status worden maken:
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. Hallo event hub-naamruimte maken. Dit is vereiste toocreate een event hub.
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. Hallo regel-ID die wordt gebruikt met Hallo insights provider ophalen:
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. Ophalen van alle mogelijke Azure locaties en Hallo namen tooa variabele die kan worden gebruikt in een later stadium toevoegen:
    
    a. ```$locationObjects = Get-AzureRMLocation```    
    b. ```$locations = @('global') + $locationobjects.location```
    
    Als u `$locations` op dit moment ziet u Hallo locatienamen zonder Hallo aanvullende informatie die wordt geretourneerd door Get-AzureRmLocation.
12. Een Azure Resource Manager-logboek-profiel maken: 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    Zie voor meer informatie over Azure-logboekanalyse profiel Hallo [overzicht van hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

> [!NOTE]
> U mogelijk een foutbericht weergegeven wanneer u een profiel voor een logboek toocreate probeert. U kunt vervolgens Hallo-documentatie voor Get-AzureRmLogProfile en verwijder AzureRmLogProfile bekijken. Als u een Get-AzureRmLogProfile uitvoert, ziet u informatie over Hallo logboek profiel. Kunt u het bestaande logboek profiel Hallo verwijderen door te voeren Hallo ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` opdracht.
>
>![Fout bij het Resource Manager-profiel](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a>Een sleutelkluis maken

1. Hallo sleutelkluis maakt:

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. Logboekregistratie voor sleutelkluis Hallo configureren:

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a>Genereren van een activiteit

Aanvragen moeten toobe tooKey kluis toogenerate logboek activiteit verzonden. Acties zoals genereren van sleutels, geheimen, opslaan of logboekvermeldingen lezen van geheimen van Sleutelkluis maakt.

1. De huidige opslagsleutels Hallo weergegeven:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. Genereren van een nieuwe **key2**:
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. Hallo sleutels opnieuw weergegeven en u ziet dat **key2** bevat een andere waarde:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. Te stellen en een geheime toogenerate extra logboekvermeldingen lezen:
    
   a. ```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b. ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Geheime geretourneerd](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a>Azure-logboekanalyse-integratie configureren

Nu u alle Hallo vereiste elementen toohave logboekregistratie van Sleutelkluis tooan event hub hebt geconfigureerd, moet u tooconfigure Azure Log integratie:

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

Voer Hallo AzLog opdracht voor elke event hub:

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

Na een minuut of dus Hallo laatste twee opdrachten uitgevoerd, ziet u JSON-bestanden die worden gegenereerd. U hebt gecontroleerd of door de bewaking van Hallo directory **C:\users\AzLog\EventHubJson**.

## <a name="next-steps"></a>Volgende stappen

- [Veelgestelde vragen over Azure-logboekanalyse-integratie](security-azure-log-integration-faq.md)
- [Aan de slag met Azure Log-integratie](security-azure-log-integration-get-started.md)
- [Logboeken van de Azure-resources integreren in uw SIEM-systemen](security-azure-log-integration-overview.md)
