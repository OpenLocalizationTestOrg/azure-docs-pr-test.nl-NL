---
title: toegangssleutels aaaUpdate Media Services na opslag rolling | Microsoft Docs
description: In dit artikel krijgt u informatie over hoe de toegangssleutels voor tooupdate Media Services na het implementeren van opslag.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a>Media Services bijwerken na rolling toegangssleutels voor opslag

Wanneer u een nieuw Azure Media Services (AMS)-account maakt, wordt u ook gevraagd een Azure Storage-account dat tooselect gebruikt toostore uw media-inhoud. U kunt meer dan één storage accounts tooyour Media Services-account toevoegen. Dit onderwerp wordt beschreven hoe toorotate opslagsleutels. U ziet ook hoe tooadd opslagaccounts tooa media-account. 

tooperform hello acties beschreven in dit onderwerp, moet u [ARM API's](https://docs.microsoft.com/rest/api/media/mediaservice) en [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).  Zie voor meer informatie [hoe toomanage Azure-resources met PowerShell en Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).

## <a name="overview"></a>Overzicht

Wanneer een nieuw opslagaccount is gemaakt, genereert Azure twee 512-bits opslagtoegangssleutels, die gebruikt tooauthenticate zijn tooyour opslagaccount. tookeep uw Opslagverbindingen veiliger, verdient het tooperiodically genereren en draaien van uw toegangssleutel voor opslag. Twee toegangssleutels (primair en secundair) zijn opgegeven in de volgorde tooenable u toomaintain verbindingen toohello storage-account met behulp van een toegangstoets tijdens het genereren van Hallo andere toegangssleutel. Deze procedure is een afkorting voor 'toegangssleutels rolling'.

Media Services is afhankelijk van een opgegeven tooit-opslagsleutel. Hallo-locators die gebruikte toostream of downloaden van uw assets is specifiek, afhankelijk van toegangssleutel voor Hallo opgegeven opslag. Wanneer een AMS-account is gemaakt duurt een afhankelijkheid op Hallo-toegangssleutel voor primaire opslag standaard maar als een gebruiker u Hallo-opslagsleutel met AMS kunt bijwerken. U moet ervoor zorgen dat toolet Media Services weten welke sleutel toouse door de stappen die worden beschreven in dit onderwerp.  

>[!NOTE]
> Als u meerdere opslagaccounts hebt, kunt u deze procedure met elk opslagaccount wilt uitvoeren. Hallo-volgorde op waarin u opslagsleutels draaien is niet opgelost. Als u eerst de secundaire sleutel Hallo draaien en vervolgens Hallo primaire sleutel of vice versa.
>
> Voordat u de stappen in dit onderwerp beschreven voor een productie-account, zorg ervoor dat tootest ze op een preproductie-account.
>

## <a name="steps-toorotate-storage-keys"></a>Stappen toorotate opslagsleutels 
 
 1. Wijziging Hallo primaire opslagaccountsleutel via powershell-cmdlet Hallo of [Azure](https://portal.azure.com/) portal.
 2. Roep de cmdlet Sync AzureRmMediaServiceStorageKeys met de juiste parameters tooforce media account toopick up toegangscodes voor opslag
 
    Hallo volgende voorbeeld ziet u hoe toosync toostorage accounts sleutels.
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. Wacht een uur. Controleer of Hallo streaming scenario's werken.
 4. Secundaire opslagaccountsleutel via de powershell-cmdlet Hallo of Azure-portal wijzigen.
 5. Aanroepen Sync AzureRmMediaServiceStorageKeys powershell met de juiste parameters tooforce media account toopick van nieuwe toegangscodes voor opslag. 
 6. Wacht een uur. Controleer of Hallo streaming scenario's werken.
 
### <a name="a-powershell-cmdlet-example"></a>Een voorbeeld van een powershell-cmdlet 

Hallo volgende voorbeeld laat zien hoe tooget Hallo storage-account en deze te synchroniseren met Hallo AMS-account.

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a>Stappen tooadd opslagaccounts tooyour AMS-account

Hallo volgende onderwerp wordt uitgelegd hoe tooadd opslagaccounts tooyour AMS-account: [meerdere storage accounts tooa Media Services-account koppelen](meda-services-managing-multiple-storage-accounts.md).

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Bevestigingen
Willen we graag tooacknowledge Hallo personen die hebben bijgedragen tot de verwezenlijking van dit document te volgen: Cenk Dingiloglu, Milaan Gada, Seva Titov.
