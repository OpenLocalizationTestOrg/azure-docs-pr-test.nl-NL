---
title: aaaConnection activa in Azure Automation | Microsoft Docs
description: Verbindingsassets in Azure Automation bevatten Hallo vereiste informatie op tooconnect tooan externe service of toepassing vanuit een runbook of de DSC-configuratie. Dit artikel wordt uitgelegd Hallo details van verbindingen en hoe toowork ermee in tekstvorm en grafisch ontwerpen.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
ms.author: magoedte; bwren
ms.openlocfilehash: f0f6b9fb960789b34af7b60eb1069313fdcf071c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connection-assets-in-azure-automation"></a>Verbindingsassets in Azure Automation

Een Automation-verbindingsasset bevat Hallo vereiste informatie op tooconnect tooan externe service of toepassing vanuit een runbook of de DSC-configuratie. Dit kan de vereiste informatie voor verificatie, zoals een gebruikersnaam en wachtwoord in aanvullende tooconnection informatie zoals een URL of een poort omvatten. Hallo-waarde van een verbinding is het houden van alle eigenschappen voor het verbinden van bepaalde toepassing tooa in één asset als tegengestelde toocreating Hallo meerdere variabelen. Hallo-gebruiker kan waarden voor een verbinding op één plek Hallo bewerken en kunt u Hallo-naam van een verbinding tooa runbook of de DSC-configuratie in een enkele parameter doorgeven. Hallo eigenschappen voor een verbinding kan worden geopend in Hallo runbook of de DSC-configuratie met Hallo **Get-AutomationConnection** activiteit.

Wanneer u een verbinding maakt, moet u een *verbindingstype*. Hallo-verbindingstype is een sjabloon met een definitie van een set eigenschappen. Hallo verbinding definieert waarden voor elke eigenschap die is gedefinieerd in het bijbehorende verbindingstype. Verbindingstypen worden toegevoegd tooAzure automatisering in integratiemodules of gemaakt met de Hallo [Azure Automation-API](http://msdn.microsoft.com/library/azure/mt163818.aspx) als Hallo integratiemodule een verbindingstype bevat en is geïmporteerd in uw Automation-account. Anders moet u toocreate een metagegevens bestand toospecify een Automation-verbindingstype.  Zie voor meer informatie over dit [integratiemodules](automation-integration-modules.md).  

>[!NOTE] 
>Beveiligde activa in Azure Automation zijn referenties, certificaten, verbindingen en gecodeerde variabelen. Deze activa zijn versleuteld en opgeslagen in hello Azure Automation, met een unieke sleutel die wordt gegenereerd voor elk automation-account. Deze sleutel is versleuteld met een basiscertificaat en opgeslagen in Azure Automation. Voordat u een beveiligd bedrijfsmiddel op te slaan, Hallo-sleutel voor Hallo automation-account wordt ontsleuteld met behulp van het basiscertificaat Hallo en vervolgens gebruikt tooencrypt Hallo asset.

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell-Cmdlets

Hallo-cmdlets in de volgende tabel Hallo gebruikte toocreate zijn en beheren van Automation-verbindingen met Windows PowerShell. Ze worden verzonden als onderdeel van Hallo [Azure PowerShell-module](/powershell/azure/overview) die beschikbaar is voor gebruik in Automation-runbooks en DSC-configuraties.

|Cmdlet|Beschrijving|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|Hiermee haalt u een verbinding. Hash-tabel met waarden van Hallo Verbindingsvelden Hallo bevat.|
|[Nieuwe AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection)|Maakt een nieuwe verbinding.|
|[Verwijder AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|Verwijder een bestaande verbinding.|
|[Set-AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|Hallo-waarde van een bepaald veld voor een bestaande verbinding ingesteld.|

## <a name="activities"></a>Activiteiten

Hallo activiteiten in de volgende tabel Hallo zijn gebruikte tooaccess verbindingen in een runbook of de DSC-configuratie.

|Activiteiten|Beschrijving|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|Hiermee haalt u een toouse verbinding. Retourneert een hashtabel met Hallo eigenschappen van Hallo-verbinding.|

>[!NOTE] 
>Vermijd het gebruik van variabelen met Hallo – Name-parameter van **Get - AutomationConnection** omdat dit detecteren van afhankelijkheden tussen runbooks of DSC-configuraties en verbindingsassets in de ontwerpfase kan bemoeilijken.

## <a name="creating-a-new-connection"></a>Een nieuwe verbinding maken

### <a name="toocreate-a-new-connection-with-hello-azure-portal"></a>toocreate een nieuwe verbinding met hello Azure-portal

1. Klik op Hallo van uw automation-account **activa** onderdeel tooopen hello **activa** blade.
2. Klik op Hallo **verbindingen** onderdeel tooopen hello **verbindingen** blade.
3. Klik op **een verbinding toevoegen** Hallo boven aan het Hallo-blade.
4. In Hallo **Type** vervolgkeuzelijst, selecteer Hallo type verbinding dat u wilt dat toocreate. Hallo-formulier wordt Hallo-eigenschappen voor dat type aanwezig.
5. Vul Hallo formulier in en klik op **maken** toosave Hallo nieuwe verbinding.

### <a name="toocreate-a-new-connection-with-hello-azure-classic-portal"></a>een nieuwe verbinding met de klassieke Azure-portal Hallo toocreate

1. Van uw automation-account, klikt u op **activa** Hallo boven aan het Hallo-venster.
2. Aan de onderkant van de Hallo van Hallo-venster, klikt u op **instelling toevoegen**.
3. Klik op **verbinding toevoegen**.
4. In Hallo **verbindingstype** vervolgkeuzelijst, selecteer Hallo type verbinding dat u wilt dat toocreate.  Hallo-wizard biedt Hallo-eigenschappen voor dat type zijn.
5. Hallo-wizard hebt voltooid en klik op Hallo selectievakje toosave Hallo nieuwe verbinding.

### <a name="toocreate-a-new-connection-with-windows-powershell"></a>toocreate een nieuwe verbinding met Windows PowerShell

Een nieuwe verbinding maken met Windows PowerShell met Hallo [nieuw AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) cmdlet. Deze cmdlet heeft een parameter genaamd **ConnectionFieldValues** die verwacht een [hash-tabel](http://technet.microsoft.com/library/hh847780.aspx) waarden voor elk van de Hallo-eigenschappen die zijn gedefinieerd door het verbindingstype Hallo definiëren.

Als u bekend met de Hallo Automation bent [Run As-account](automation-sec-configure-azure-runas-account.md) tooauthenticate runbooks met Hallo-service-principal Hallo PowerShell-script, opgegeven als een alternatieve toocreating Hallo Hallo Run As-account van Hallo-portal maakt een nieuwe verbindingsasset met behulp van de volgende voorbeeldopdrachten Hallo.  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

U kunt toouse Hallo script toocreate Hallo-verbindingsasset zijn omdat wanneer u uw Automation-account maakt, wordt automatisch meerdere globale modules standaard samen met het verbindingstype Hallo bevat **AzurServicePrincipal**toocreate hello **AzureRunAsConnection** verbindingstype-asset.  Dit is belangrijk tookeep in gedachten, omdat het als u toocreate een nieuwe verbinding asset tooconnect tooa service of toepassing met een andere verificatiemethode probeert, mislukken zal omdat verbindingstype Hallo is niet gedefinieerd in uw Automation-account.  Voor meer informatie over hoe toocreate uw eigen verbinding typt u voor uw aangepaste of de module op basis van Hallo [PowerShell Gallery](https://www.powershellgallery.com), Zie [integratiemodules](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>Met behulp van een verbinding in een runbook of de DSC-configuratie

Ophalen van een verbinding in een runbook of de DSC-configuratie met Hallo **Get-AutomationConnection** cmdlet.  U kunt geen hello gebruiken [Get-AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) activiteit.  Deze activiteit haalt Hallo waarden van verschillende velden in Hallo verbinding Hallo en retourneert ze als een [hash-tabel](http://go.microsoft.com/fwlink/?LinkID=324844) die vervolgens kan worden gebruikt met de juiste opdrachten Hallo in Hallo runbook of de DSC-configuratie.

### <a name="textual-runbook-sample"></a>Voorbeeld van tekstueel runbook

Hallo volgende voorbeeldopdrachten laten zien hoe toouse Hallo Run As-account eerder vermeld, tooauthenticate met Azure Resource Manager-resources in uw runbook.  Het Hallo-verbinding gebruikt asset Hallo Run As-account, die verwijst naar Hallo op basis van certificaten service-principal, die niet-referenties.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>Grafische runbook-voorbeelden

U toevoegen een **Get-AutomationConnection** activiteit tooa grafisch runbook door met de rechtermuisknop op het Hallo-verbinding in het deelvenster van de bibliotheek Hallo Hallo grafische editor en het selecteren van **toocanvas toevoegen**.

![](media/automation-connections/connection-add-canvas.png)

Hallo toont volgende afbeelding een voorbeeld van het gebruik van een verbinding in een grafisch runbook.  Dit is Hallo voor verificatie met Hallo Run As-account met tekstueel runbook bovenstaande voorbeeld.  In dit voorbeeld wordt Hallo **constante waarde** gegevensset voor Hallo **RunAs-verbinding ophalen** activiteit die een verbindingsobject voor verificatie gebruikt.  Een [pijplijnkoppeling](automation-graphical-authoring-intro.md#links-and-workflow) wordt hier gebruikt sinds Hallo parameterset ServicePrincipalCertificate een enkel object verwacht.

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>Volgende stappen

- Bekijk [koppelingen in het grafisch ontwerpen](automation-graphical-authoring-intro.md#links-and-workflow) toounderstand hoe toodirect en beheer Hallo stromen van logica in uw runbooks.  

- Zie toolearn meer informatie over het gebruik van Azure Automation van PowerShell-modules en aanbevolen procedures voor het maken van uw eigen PowerShell-modules toowork als integratiemodules binnen Azure Automation [integratiemodules](automation-integration-modules.md).  
