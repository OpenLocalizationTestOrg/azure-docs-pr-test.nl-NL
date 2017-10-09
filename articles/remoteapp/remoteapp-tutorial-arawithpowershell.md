---
title: aaaUse PowerShell-cmdlets met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toouse Windows PowerShell-cmdlets in Azure RemoteApp.
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
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Windows PowerShell-cmdlets gebruiken met Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

 U kunt hello Azure RemoteApp-PowerShell-cmdlets tooadminister gebruiken en onderhouden van uw verzamelingen. Hallo informatie tooget gestart na gebruiken.

## <a name="get-hello-cmdlets"></a>Hallo-cmdlets ophalen
- - -
Eerst hello Azure Powershell-cmdlets downloaden [hier](http://go.microsoft.com/?linkid=9811175), Hallo RemoteApp-cmdlets in is opgenomen. 

Bekijk Hallo [help van cmdlet voor Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a>Uw abonnement voor Azure-cmdlets toouse configureren
- - -
Ga als volgt [in deze handleiding](/powershell/azure/overview) zodat u Hallo-cmdlets op basis van uw Azure-abonnement gebruiken kunt.

U kunt deze stappen tooget snel aan de slag:

1. Download en installeer Hallo [Azure PowerShell-cmdlets](http://go.microsoft.com/?linkid=9811175).
2. Start Microsoft Azure PowerShell.
3. Voer **Add-AzureAccount** tooauthenticate tooyour Azure-abonnement. Wanneer u wordt gevraagd, typt u Hallo dezelfde gebruikersnaam en wachtwoord toosign in tooAzure portal te gebruiken.  
4. Voer **Get-AzureSubscription** toolist Hallo abonnementen die zijn gekoppeld aan uw gebruikersaccount. 
5. Voer **Select-AzureSubscription - SubscriptionName &lt;abonnementsnaam&gt;**  of **Select-AzureSubscription - SubscriptionId &lt;abonnements-ID&gt;**  toospecify Hallo abonnement toouse.

Gefeliciteerd, uw Azure PowerShell-console is geconfigureerd en klaar toouse. Let erop dat u moet toorepeate stappen 2 t/m 5 telkens wanneer die u Hallo hello Azure PowerShell-console start.  


## <a name="list-all-collections"></a>Lijst van alle verzamelingen
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Een verzameling verwijderen
- - -
    Verwijder AzureRemoteAppCollection<enter collection name>

Voorbeeld: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Een cloudverzameling maken
- - -
Het is eenvoudig, Hallo volgende opdracht uitvoeren:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

Hallo hierboven opdracht publiceert automatisch Microsoft Office 365-toepassingen (Excel, OneNote, Outlook, PowerPoint, Visio en Word).

Maken van een siteverzameling duurt 30 minuten of langer toocomplete. Deze opdracht retourneert daarom een tracerings-ID die u kunt als volgt gebruiken:

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Nadat Hallo verzameling is voltooid, kunt u gebruikers toohello verzameling kunt toevoegen met de volgende opdracht Hallo:

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

En u klaar bent! Deze gebruiker moet kunnen tooconnect toohello toepassing hello Azure RemoteApp-client gevonden met [hier](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Beschikbare cmdlets
Er zijn veel andere opdrachten die we hebben, Hallo-documentatie voor ze is binnenkort binnenkort:

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

