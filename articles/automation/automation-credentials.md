---
title: aaaCredential activa in Azure Automation | Microsoft Docs
description: Referentieassets in Azure Automation bevatten beveiligingsreferenties op die gebruikt tooauthenticate tooresources toegankelijk is voor het Hallo-runbook of de DSC-configuratie worden kunnen. Dit artikel wordt beschreven hoe toocreate referentieassets en deze gebruiken in een runbook of de DSC-configuratie.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a>Referentieassets in Azure Automation
Een Automation-referentieasset bevat een [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) object met beveiligingsgegevens zoals een gebruikersnaam en wachtwoord. Runbooks en DSC-configuraties kunt cmdlets die een PSCredential-object voor verificatie accepteren of ze kunnen extraheren Hallo gebruikersnaam en wachtwoord Hallo PSCredential-object tooprovide toosome toepassing of service-verificatie vereist. Hallo-eigenschappen van een referentie worden veilig opgeslagen in Azure Automation en kunnen worden geopend in Hallo runbook of de DSC-configuratie met Hallo [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) activiteit.

> [!NOTE]
> Beveiligde activa in Azure Automation zijn referenties, certificaten, verbindingen en gecodeerde variabelen. Deze activa zijn versleuteld en opgeslagen in hello Azure Automation, met een unieke sleutel die wordt gegenereerd voor elk automation-account. Deze sleutel is versleuteld met een basiscertificaat en opgeslagen in Azure Automation. Voordat u een beveiligd bedrijfsmiddel op te slaan, Hallo-sleutel voor Hallo automation-account wordt ontsleuteld met behulp van het basiscertificaat Hallo en vervolgens gebruikt tooencrypt Hallo asset.  

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell-cmdlets
Hallo-cmdlets in de volgende tabel Hallo gebruikte toocreate zijn en beheren van automation referentieassets met Windows PowerShell.  Ze worden verzonden als onderdeel van Hallo [Azure PowerShell-module](/powershell/azure/overview) die beschikbaar is voor gebruik in Automation-runbooks en DSC-configuraties.

| Cmdlets | Beschrijving |
|:--- |:--- |
| [Get-AzureAutomationCredential](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |Informatie over een referentieasset opgehaald. U kunt alleen Hallo referentie zelf ophalen uit **Get-AutomationPSCredential** activiteit. |
| [Nieuwe AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Hiermee maakt u een nieuw Automation-referentie. |
| [Remove - AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Hiermee verwijdert u een Automation-referentie. |
| [Set - AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Sets Hallo eigenschappen voor een bestaand Automation-referentie. |

## <a name="runbook-activities"></a>Runbookactiviteiten
Hallo activiteiten in de volgende tabel Hallo zijn gebruikte tooaccess referenties in een runbook en DSC-configuraties.

| Activiteiten | Beschrijving |
|:--- |:--- |
| Get-AutomationPSCredential |Hiermee haalt u een referentie toouse in een runbook of de DSC-configuratie. Retourneert een [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) object. |

> [!NOTE]
> Vermijd het gebruik van variabelen in Hallo – parameter Name van Get-AutomationPSCredential omdat dit kan detecteren van afhankelijkheden tussen runbooks of DSC-configuraties bemoeilijken en referentieassets in de ontwerpfase.
> 
> 

## <a name="creating-a-new-credential-asset"></a>Een nieuwe referentieasset maken

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a>toocreate een nieuwe referentieasset Hello Azure-portal
1. Klik op Hallo van uw automation-account **activa** onderdeel tooopen hello **activa** blade.
2. Klik op Hallo **referenties** onderdeel tooopen hello **referenties** blade.
3. Klik op **toevoegen van een referentie** Hallo boven aan het Hallo-blade.
4. Vul Hallo formulier in en klik op **maken** toosave Hallo nieuwe referentie.

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a>toocreate een nieuwe referentieasset met Windows PowerShell
Hallo volgende voorbeeldopdrachten laten zien hoe een nieuwe automation toocreate referenties. Een PSCredential-object wordt gemaakt met het Hallo-naam en het wachtwoord en vervolgens gebruikt toocreate Hallo referentie-element. U kunt ook kunt u Hallo **Get-Credential** cmdlet toobe tootype in een naam en wachtwoord gevraagd.

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a>toocreate een nieuwe referentieasset Hello klassieke Azure-portal
1. Van uw automation-account, klikt u op **activa** Hallo boven aan het Hallo-venster.
2. Aan de onderkant van de Hallo van Hallo-venster, klikt u op **instelling toevoegen**.
3. Klik op **gebruikersreferentie toevoegen**.
4. In Hallo **referentietype** vervolgkeuzelijst **PowerShell-referentie**.
5. Hallo-wizard hebt voltooid en klik op Hallo selectievakje toosave Hallo nieuwe referentie.

## <a name="using-a-powershell-credential"></a>Met behulp van een PowerShell-referentie
Ophalen van een referentie-element in een runbook of de DSC-configuratie met Hallo **Get-AutomationPSCredential** activiteit. Hiermee wordt een [PSCredential-object](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) die u kunt gebruiken met een activiteit of cmdlet waarvoor een PSCredential-parameter. U kunt ook afzonderlijk Hallo eigenschappen van Hallo referentie object toouse ophalen. Hallo-object heeft een eigenschap voor het Hallo-gebruikersnaam en het Hallo beveiligd wachtwoord of kunt u Hallo **GetNetworkCredential** methode tooreturn een [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) -object dat een niet-beveiligde bieden versie van het Hallo-wachtwoord.

### <a name="textual-runbook-sample"></a>Voorbeeld van tekstueel runbook
Hallo volgende voorbeeldopdrachten laten zien hoe een PowerShell toouse referentie in een runbook. In dit voorbeeld Hallo referentie wordt opgehaald en de gebruikersnaam en wachtwoord toovariables toegewezen.

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>Grafisch runbook-voorbeeld
U toevoegen een **Get-AutomationPSCredential** activiteit tooa grafisch runbook door met de rechtermuisknop op het Hallo-referentie in Hallo bibliotheek deelvenster van de grafische editor Hallo en het selecteren van **toocanvas toevoegen**.

![Referentie toocanvas toevoegen](media/automation-credentials/credential-add-canvas.png)

Hallo toont volgende afbeelding een voorbeeld van het gebruik van een referentie in een grafisch runbook.  In dit geval wordt gebruikte tooprovide-verificatie voor een runbook tooAzure-bronnen zoals beschreven in [Runbooks verifiëren met Azure AD-gebruikersaccount](automation-create-aduser-account.md).  de eerste activiteit Hallo haalt Hallo referentie toegang toohello Azure-abonnement.  Hallo **Add-AzureAccount** activiteit gebruikt deze referentie tooprovide verificatie voor alle activiteiten die na deze komen.  Een [pijplijnkoppeling](automation-graphical-authoring-intro.md#links-and-workflow) is hier sinds **Get-AutomationPSCredential** een enkel object verwacht.  

![Referentie toocanvas toevoegen](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>Met behulp van een PowerShell-referentie in DSC
Terwijl in Azure Automation DSC-configuraties kunnen verwijzen naar referentieassets met **Get-AutomationPSCredential**, referentieassets kunnen ook worden doorgegeven via parameters, indien gewenst. Zie voor meer informatie [compileren van configuraties in Azure Automation DSC](automation-dsc-compile.md#credential-assets).

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn meer informatie over de koppelingen in het grafisch ontwerpen [koppelingen in het grafisch ontwerpen](automation-graphical-authoring-intro.md#links-and-workflow)
* toounderstand hello verschillende verificatiemethoden met Automation, Zie [Azure Automation-beveiliging](automation-security-overview.md)
* Zie tooget gestart met grafische runbooks [Mijn eerste grafische runbook](automation-first-runbook-graphical.md)
* tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md) 

