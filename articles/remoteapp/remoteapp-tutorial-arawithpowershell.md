---
title: PowerShell-cmdlets gebruiken met Azure RemoteApp | Microsoft Docs
description: Informatie over het gebruik van Windows PowerShell-cmdlets in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 699b20a4dadd4ecaff57e2cc80355fe545360663
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Windows PowerShell-cmdlets gebruiken met Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

 U kunt de Azure RemoteApp-PowerShell-cmdlets gebruiken voor het beheren en onderhouden van uw verzamelingen. Gebruik de volgende informatie om te beginnen.

## <a name="get-the-cmdlets"></a>De cmdlets ophalen
- - -
Downloadt u eerst de Azure Powershell-cmdlets [hier](http://go.microsoft.com/?linkid=9811175), de RemoteApp-cmdlets in is opgenomen. 

Bekijk de [help van cmdlet voor Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-to-use-your-subscription"></a>Azure-cmdlets voor het gebruik van uw abonnement configureren
- - -
Ga als volgt [in deze handleiding](/powershell/azure/overview) zodat u de cmdlets op basis van uw Azure-abonnement gebruiken kunt.

Volg deze stappen kunt u snel aan de slag:

1. Download en installeer de [Azure PowerShell-cmdlets](http://go.microsoft.com/?linkid=9811175).
2. Start Microsoft Azure PowerShell.
3. Voer **Add-AzureAccount** om uw Azure-abonnement te verifiëren. Wanneer u wordt gevraagd, typt u de dezelfde gebruikersnaam en wachtwoord dat u aan te melden bij Azure-portal.  
4. Voer **Get-AzureSubscription** voor een lijst met de abonnementen die zijn gekoppeld aan uw gebruikersaccount. 
5. Voer **Select-AzureSubscription - SubscriptionName &lt;abonnementsnaam&gt;**  of **Select-AzureSubscription - SubscriptionId &lt;abonnements-ID&gt;**  om op te geven van het abonnement te gebruiken.

Gefeliciteerd, uw Azure PowerShell-console is geconfigureerd en klaar voor gebruik. Houd er rekening mee dat u wilt herhaalt stappen 2 t/m 5 telkens wanneer u start de Azure PowerShell-console.  


## <a name="list-all-collections"></a>Lijst van alle verzamelingen
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Een verzameling verwijderen
- - -
    Verwijder AzureRemoteAppCollection<enter collection name>

Voorbeeld: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Een cloudverzameling maken
- - -
Het is eenvoudig, voer de volgende opdracht:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

De bovenstaande opdracht publiceert automatisch Microsoft Office 365-toepassingen (Excel, OneNote, Outlook, PowerPoint, Visio en Word).

Maken van een siteverzameling kan 30 minuten duren of langer duren. Deze opdracht retourneert daarom een tracerings-ID die u kunt als volgt gebruiken:

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Nadat de verzameling is voltooid, kunt u gebruikers kunt toevoegen aan de verzameling met de volgende opdracht:

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

En u klaar bent! Deze gebruiker moet verbinding maken met de toepassing met behulp van de Azure RemoteApp-client gevonden [hier](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Beschikbare cmdlets
Er zijn veel andere opdrachten die we hebben, de documentatie voor hen wordt binnenkort wel binnenkort:

Basic RemoteApp-collectie cmdlets: 

* New-AzureRemoteAppCollection
* Get-AzureRemoteAppCollection
* Set-AzureRemoteAppCollection
* Update-AzureRemoteAppCollection
* Remove-AzureRemoteAppCollection
* Add-AzureRemoteAppUser
* Get-AzureRemoteAppUser
* Remove-AzureRemoteAppUser
* Get-AzureRemoteAppSession
* Disconnect-AzureRemoteAppSession
* Invoke-AzureRemoteAppSessionLogoff
* Send-AzureRemoteAppSessionMessage
* Get-AzureRemoteAppProgram
* Get-AzureRemoteAppStartMenuProgram
* Publish-AzureRemoteAppProgram
* Unpublish-AzureRemoteAppProgram
* Get-AzureRemoteAppCollectionUsageDetails
* Get-AzureRemoteAppCollectionUsageSummary
* Get-AzureRemoteAppPlan

RemoteApp-cmdlets voor virtueel netwerk:

* New-AzureRemoteAppVNet
* Get-AzureRemoteAppVNet
* Set-AzureRemoteAppVNet
* Remove-AzureRemoteAppVNet
* Get-AzureRemoteAppVpnDevice
* Get--AzureRemoteAppVpnDeviceConfigScript
* Reset-AzureRemoteAppVpnSharedKey

RemoteApp-sjabloon installatiekopie cmdlets:

* New-AzureRemoteAppTemplateImage
* Get-AzureRemoteAppTemplateImage
* Rename-AzureRemoteAppTemplateImage
* Remove-AzureRemoteAppTemplateImage

Andere RemoteApp-cmdlets:

* Get-AzureRemoteAppLocation
* Get-AzureRemoteAppWorkspace
* Set-AzureRemoteAppWorkspace
* Get-AzureRemoteAppOperationResult

