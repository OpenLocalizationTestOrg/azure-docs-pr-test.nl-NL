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
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="f9ded-103">Media Services bijwerken na rolling toegangssleutels voor opslag</span><span class="sxs-lookup"><span data-stu-id="f9ded-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="f9ded-104">Wanneer u een nieuw Azure Media Services (AMS)-account maakt, wordt u ook gevraagd een Azure Storage-account dat tooselect gebruikt toostore uw media-inhoud.</span><span class="sxs-lookup"><span data-stu-id="f9ded-104">When you create a new Azure Media Services (AMS) account, you are also asked tooselect an Azure Storage account that is used toostore your media content.</span></span> <span data-ttu-id="f9ded-105">U kunt meer dan één storage accounts tooyour Media Services-account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f9ded-105">You can add more than one storage accounts tooyour Media Services account.</span></span> <span data-ttu-id="f9ded-106">Dit onderwerp wordt beschreven hoe toorotate opslagsleutels.</span><span class="sxs-lookup"><span data-stu-id="f9ded-106">This topic shows how toorotate storage keys.</span></span> <span data-ttu-id="f9ded-107">U ziet ook hoe tooadd opslagaccounts tooa media-account.</span><span class="sxs-lookup"><span data-stu-id="f9ded-107">It also shows how tooadd storage accounts tooa media account.</span></span> 

<span data-ttu-id="f9ded-108">tooperform hello acties beschreven in dit onderwerp, moet u [ARM API's](https://docs.microsoft.com/rest/api/media/mediaservice) en [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="f9ded-108">tooperform hello actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="f9ded-109">Zie voor meer informatie [hoe toomanage Azure-resources met PowerShell en Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f9ded-109">For more information, see [How toomanage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="f9ded-110">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f9ded-110">Overview</span></span>

<span data-ttu-id="f9ded-111">Wanneer een nieuw opslagaccount is gemaakt, genereert Azure twee 512-bits opslagtoegangssleutels, die gebruikt tooauthenticate zijn tooyour opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f9ded-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used tooauthenticate access tooyour storage account.</span></span> <span data-ttu-id="f9ded-112">tookeep uw Opslagverbindingen veiliger, verdient het tooperiodically genereren en draaien van uw toegangssleutel voor opslag.</span><span class="sxs-lookup"><span data-stu-id="f9ded-112">tookeep your storage connections more secure, it is recommended tooperiodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="f9ded-113">Twee toegangssleutels (primair en secundair) zijn opgegeven in de volgorde tooenable u toomaintain verbindingen toohello storage-account met behulp van een toegangstoets tijdens het genereren van Hallo andere toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="f9ded-113">Two access keys (primary and secondary) are provided in order tooenable you toomaintain connections toohello storage account using one access key while you regenerate hello other access key.</span></span> <span data-ttu-id="f9ded-114">Deze procedure is een afkorting voor 'toegangssleutels rolling'.</span><span class="sxs-lookup"><span data-stu-id="f9ded-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="f9ded-115">Media Services is afhankelijk van een opgegeven tooit-opslagsleutel.</span><span class="sxs-lookup"><span data-stu-id="f9ded-115">Media Services depends on a storage key provided tooit.</span></span> <span data-ttu-id="f9ded-116">Hallo-locators die gebruikte toostream of downloaden van uw assets is specifiek, afhankelijk van toegangssleutel voor Hallo opgegeven opslag.</span><span class="sxs-lookup"><span data-stu-id="f9ded-116">Specifically, hello locators that are used toostream or download your assets depend on hello specified storage access key.</span></span> <span data-ttu-id="f9ded-117">Wanneer een AMS-account is gemaakt duurt een afhankelijkheid op Hallo-toegangssleutel voor primaire opslag standaard maar als een gebruiker u Hallo-opslagsleutel met AMS kunt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f9ded-117">When an AMS account is created it takes a dependency on hello primary storage access key by default but as a user you can update hello storage key that AMS has.</span></span> <span data-ttu-id="f9ded-118">U moet ervoor zorgen dat toolet Media Services weten welke sleutel toouse door de stappen die worden beschreven in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="f9ded-118">You must make sure toolet Media Services know which key toouse by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="f9ded-119">Als u meerdere opslagaccounts hebt, kunt u deze procedure met elk opslagaccount wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f9ded-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="f9ded-120">Hallo-volgorde op waarin u opslagsleutels draaien is niet opgelost.</span><span class="sxs-lookup"><span data-stu-id="f9ded-120">hello order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="f9ded-121">Als u eerst de secundaire sleutel Hallo draaien en vervolgens Hallo primaire sleutel of vice versa.</span><span class="sxs-lookup"><span data-stu-id="f9ded-121">You can rotate hello secondary key first and then hello primary key or vice versa.</span></span>
>
> <span data-ttu-id="f9ded-122">Voordat u de stappen in dit onderwerp beschreven voor een productie-account, zorg ervoor dat tootest ze op een preproductie-account.</span><span class="sxs-lookup"><span data-stu-id="f9ded-122">Before executing steps described in this topic on a production account, make sure tootest them on a pre-production account.</span></span>
>

## <a name="steps-toorotate-storage-keys"></a><span data-ttu-id="f9ded-123">Stappen toorotate opslagsleutels</span><span class="sxs-lookup"><span data-stu-id="f9ded-123">Steps toorotate storage keys</span></span> 
 
 1. <span data-ttu-id="f9ded-124">Wijziging Hallo primaire opslagaccountsleutel via powershell-cmdlet Hallo of [Azure](https://portal.azure.com/) portal.</span><span class="sxs-lookup"><span data-stu-id="f9ded-124">Change hello storage account Primary key through hello powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="f9ded-125">Roep de cmdlet Sync AzureRmMediaServiceStorageKeys met de juiste parameters tooforce media account toopick up toegangscodes voor opslag</span><span class="sxs-lookup"><span data-stu-id="f9ded-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params tooforce media account toopick up storage account keys</span></span>
 
    <span data-ttu-id="f9ded-126">Hallo volgende voorbeeld ziet u hoe toosync toostorage accounts sleutels.</span><span class="sxs-lookup"><span data-stu-id="f9ded-126">hello following example shows how toosync keys toostorage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="f9ded-127">Wacht een uur.</span><span class="sxs-lookup"><span data-stu-id="f9ded-127">Wait an hour or so.</span></span> <span data-ttu-id="f9ded-128">Controleer of Hallo streaming scenario's werken.</span><span class="sxs-lookup"><span data-stu-id="f9ded-128">Verify hello streaming scenarios are working.</span></span>
 4. <span data-ttu-id="f9ded-129">Secundaire opslagaccountsleutel via de powershell-cmdlet Hallo of Azure-portal wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f9ded-129">Change storage account secondary key through hello powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="f9ded-130">Aanroepen Sync AzureRmMediaServiceStorageKeys powershell met de juiste parameters tooforce media account toopick van nieuwe toegangscodes voor opslag.</span><span class="sxs-lookup"><span data-stu-id="f9ded-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params tooforce media account toopick up new storage account keys.</span></span> 
 6. <span data-ttu-id="f9ded-131">Wacht een uur.</span><span class="sxs-lookup"><span data-stu-id="f9ded-131">Wait an hour or so.</span></span> <span data-ttu-id="f9ded-132">Controleer of Hallo streaming scenario's werken.</span><span class="sxs-lookup"><span data-stu-id="f9ded-132">Verify hello streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="f9ded-133">Een voorbeeld van een powershell-cmdlet</span><span class="sxs-lookup"><span data-stu-id="f9ded-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="f9ded-134">Hallo volgende voorbeeld laat zien hoe tooget Hallo storage-account en deze te synchroniseren met Hallo AMS-account.</span><span class="sxs-lookup"><span data-stu-id="f9ded-134">hello following example demonstrates how tooget hello storage account and sync it with hello AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a><span data-ttu-id="f9ded-135">Stappen tooadd opslagaccounts tooyour AMS-account</span><span class="sxs-lookup"><span data-stu-id="f9ded-135">Steps tooadd storage accounts tooyour AMS account</span></span>

<span data-ttu-id="f9ded-136">Hallo volgende onderwerp wordt uitgelegd hoe tooadd opslagaccounts tooyour AMS-account: [meerdere storage accounts tooa Media Services-account koppelen](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f9ded-136">hello following topic shows how tooadd storage accounts tooyour AMS account: [Attach multiple storage accounts tooa Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f9ded-137">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="f9ded-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f9ded-138">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="f9ded-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="f9ded-139">Bevestigingen</span><span class="sxs-lookup"><span data-stu-id="f9ded-139">Acknowledgments</span></span>
<span data-ttu-id="f9ded-140">Willen we graag tooacknowledge Hallo personen die hebben bijgedragen tot de verwezenlijking van dit document te volgen: Cenk Dingiloglu, Milaan Gada, Seva Titov.</span><span class="sxs-lookup"><span data-stu-id="f9ded-140">We would like tooacknowledge hello following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
