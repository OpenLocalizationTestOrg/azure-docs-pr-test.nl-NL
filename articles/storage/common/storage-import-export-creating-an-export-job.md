---
title: exporteren van een taak voor Azure Import/Export aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate exporteren van een taak voor Hallo Microsoft Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a><span data-ttu-id="ea82e-103">Een exporttaak voor hello Azure Import/Export-service maken</span><span class="sxs-lookup"><span data-stu-id="ea82e-103">Creating an export job for hello Azure Import/Export service</span></span>
<span data-ttu-id="ea82e-104">Maken van een exporttaak voor Hallo Hallo REST-API met Microsoft Azure Import/Export-service omvat Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ea82e-104">Creating an export job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="ea82e-105">Hallo selecteren tooexport blobs.</span><span class="sxs-lookup"><span data-stu-id="ea82e-105">Selecting hello blobs tooexport.</span></span>

-   <span data-ttu-id="ea82e-106">Het verkrijgen van een back-ups van locatie.</span><span class="sxs-lookup"><span data-stu-id="ea82e-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="ea82e-107">Hallo exporttaak maken.</span><span class="sxs-lookup"><span data-stu-id="ea82e-107">Creating hello export job.</span></span>

-   <span data-ttu-id="ea82e-108">Verzending van uw tooMicrosoft lege stations via een ondersteunde Provider-service.</span><span class="sxs-lookup"><span data-stu-id="ea82e-108">Shipping your empty drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="ea82e-109">Hallo exporttaak met Hallo pakketgegevens bijwerken.</span><span class="sxs-lookup"><span data-stu-id="ea82e-109">Updating hello export job with hello package information.</span></span>

-   <span data-ttu-id="ea82e-110">Hallo ontvangen stations terug van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ea82e-110">Receiving hello drives back from Microsoft.</span></span>

 <span data-ttu-id="ea82e-111">Zie [Hallo Windows Azure Import/Export-service tooTransfer gegevens tooBlob opslag met](storage-import-export-service.md) voor een overzicht van Hallo Import/Export-service en een zelfstudie die u laat zien hoe toouse hello [Azure-portal](https://portal.azure.com/) toocreate en beheren van importeren en exporteren van taken.</span><span class="sxs-lookup"><span data-stu-id="ea82e-111">See [Using hello Windows Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="selecting-blobs-tooexport"></a><span data-ttu-id="ea82e-112">Blobs tooexport selecteren</span><span class="sxs-lookup"><span data-stu-id="ea82e-112">Selecting blobs tooexport</span></span>
 <span data-ttu-id="ea82e-113">een exporttaak toocreate, moet u tooprovide een lijst met blobs gewenste tooexport van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ea82e-113">toocreate an export job, you will need tooprovide a list of blobs that you want tooexport from your storage account.</span></span> <span data-ttu-id="ea82e-114">Er zijn een aantal manieren tooselect blobs toobe geëxporteerd:</span><span class="sxs-lookup"><span data-stu-id="ea82e-114">There are a few ways tooselect blobs toobe exported:</span></span>

-   <span data-ttu-id="ea82e-115">U kunt een pad relatief blob tooselect één blob en alle bijbehorende momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="ea82e-115">You can use a relative blob path tooselect a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="ea82e-116">U kunt een pad relatief blob tooselect één blob met uitzondering van de momentopnamen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ea82e-116">You can use a relative blob path tooselect a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="ea82e-117">U kunt een blobpad relatief en een momentopname tijd tooselect één momentopname gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ea82e-117">You can use a relative blob path and a snapshot time tooselect a single snapshot.</span></span>

-   <span data-ttu-id="ea82e-118">Kunt u een blob-voorvoegsel tooselect alle blobs en momentopnamen Hello voorvoegsel opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ea82e-118">You can use a blob prefix tooselect all blobs and snapshots with hello given prefix.</span></span>

-   <span data-ttu-id="ea82e-119">U kunt alle blobs en momentopnamen in de storage-account Hallo exporteren.</span><span class="sxs-lookup"><span data-stu-id="ea82e-119">You can export all blobs and snapshots in hello storage account.</span></span>

 <span data-ttu-id="ea82e-120">Zie voor meer informatie over het opgeven van blobs tooexport, Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking.</span><span class="sxs-lookup"><span data-stu-id="ea82e-120">For more information about specifying blobs tooexport, see hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="ea82e-121">Het verkrijgen van de locatie van uw back-ups</span><span class="sxs-lookup"><span data-stu-id="ea82e-121">Obtaining your shipping location</span></span>
<span data-ttu-id="ea82e-122">Voordat u maakt een taak voor het exporteren, moet u tooobtain de naam van een locatie en het adres door de aanroepende Hallo [locatie ophalen](https://portal.azure.com) of [lijst locaties](/rest/api/storageimportexport/listlocations) bewerking.</span><span class="sxs-lookup"><span data-stu-id="ea82e-122">Before creating an export job, you need tooobtain a shipping location name and address by calling hello [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="ea82e-123">`List Locations`retourneert een lijst met locaties en hun e-mailadressen.</span><span class="sxs-lookup"><span data-stu-id="ea82e-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="ea82e-124">U kunt een locatie selecteren van Hallo lijst geretourneerd en verzendadres uw toothat harde schijven.</span><span class="sxs-lookup"><span data-stu-id="ea82e-124">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="ea82e-125">U kunt ook Hallo `Get Location` bewerking tooobtain Hallo verzendadres rechtstreeks voor een specifieke locatie.</span><span class="sxs-lookup"><span data-stu-id="ea82e-125">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

<span data-ttu-id="ea82e-126">Hallo stappen hieronder tooobtain Hallo back-upfunctie locatie:</span><span class="sxs-lookup"><span data-stu-id="ea82e-126">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="ea82e-127">Geef de naam Hallo Hallo-locatie van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ea82e-127">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="ea82e-128">Deze waarde kan worden gevonden in het Hallo **locatie** op Hallo van het opslagaccount **Dashboard** in Hallo-classic portal of voor de query met behulp van Hallo service management API-bewerking [ophalen Eigenschappen van het opslagaccount](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="ea82e-128">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello classic portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="ea82e-129">Hallo-locatie die beschikbaar tooprocess dit opslagaccount ophalen door de aanroepende Hallo `Get Location` bewerking.</span><span class="sxs-lookup"><span data-stu-id="ea82e-129">Retrieve hello location that are available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="ea82e-130">Als hello `AlternateLocations` eigenschap Hallo locatie Hallo locatie zelf bevat, dan is dit geen probleem toouse deze locatie.</span><span class="sxs-lookup"><span data-stu-id="ea82e-130">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="ea82e-131">Anders aanroepen Hallo `Get Location` opnieuw met een van de alternatieve locaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="ea82e-131">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="ea82e-132">de oorspronkelijke locatie Hallo mogelijk tijdelijk worden gesloten voor onderhoud.</span><span class="sxs-lookup"><span data-stu-id="ea82e-132">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-export-job"></a><span data-ttu-id="ea82e-133">Hallo exporttaak maken</span><span class="sxs-lookup"><span data-stu-id="ea82e-133">Creating hello export job</span></span>
 <span data-ttu-id="ea82e-134">toocreate hello exporttaak, aanroep Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking.</span><span class="sxs-lookup"><span data-stu-id="ea82e-134">toocreate hello export job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="ea82e-135">U moet tooprovide Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="ea82e-135">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="ea82e-136">Een naam voor het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="ea82e-136">A name for hello job.</span></span>

-   <span data-ttu-id="ea82e-137">Hallo opslagaccountnaam.</span><span class="sxs-lookup"><span data-stu-id="ea82e-137">hello storage account name.</span></span>

-   <span data-ttu-id="ea82e-138">Hallo back-upfunctie locatienaam, in de vorige stap Hallo verkregen.</span><span class="sxs-lookup"><span data-stu-id="ea82e-138">hello shipping location name, obtained in hello previous step.</span></span>

-   <span data-ttu-id="ea82e-139">Een taaktype (exporteren).</span><span class="sxs-lookup"><span data-stu-id="ea82e-139">A job type (Export).</span></span>

-   <span data-ttu-id="ea82e-140">Hallo-retouradres waar Hallo schijven moeten worden verzonden nadat de exporttaak Hallo is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ea82e-140">hello return address where hello drives should be sent after hello export job has completed.</span></span>

-   <span data-ttu-id="ea82e-141">Hallo lijst met BLOB's (of blob voorvoegsels) toobe geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="ea82e-141">hello list of blobs (or blob prefixes) toobe exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="ea82e-142">Verzending van uw schijven</span><span class="sxs-lookup"><span data-stu-id="ea82e-142">Shipping your drives</span></span>
 <span data-ttu-id="ea82e-143">Vervolgens hello Azure-hulpprogramma voor importeren/exporteren toodetermine Hallo aantal stations dat u toosend, op basis van Hallo blobs die u hebt geselecteerd geëxporteerd toobe moet gebruiken en Hallo grootte van de schijf.</span><span class="sxs-lookup"><span data-stu-id="ea82e-143">Next, use hello Azure Import/Export Tool toodetermine hello number of drives you need toosend, based on hello blobs you have selected toobe exported and hello drive size.</span></span> <span data-ttu-id="ea82e-144">Zie Hallo [Azure Import/Export hulpprogramma verwijzing](storage-import-export-tool-how-to-v1.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ea82e-144">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="ea82e-145">Pakket Hallo stations in een enkel pakket en moeten worden verzonden toohello adres verkregen in Hallo eerder stap.</span><span class="sxs-lookup"><span data-stu-id="ea82e-145">Package hello drives in a single package and ship them toohello address obtained in hello earlier step.</span></span> <span data-ttu-id="ea82e-146">Houd er rekening mee Hallo nummer van uw pakket voor de volgende stap Hallo bijhouden.</span><span class="sxs-lookup"><span data-stu-id="ea82e-146">Note hello tracking number of your package for hello next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="ea82e-147">U moet uw stations via een ondersteunde Provider-service, die het pakket van een volgnummer voorzien verzenden.</span><span class="sxs-lookup"><span data-stu-id="ea82e-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-export-job-with-your-package-information"></a><span data-ttu-id="ea82e-148">Hallo exporttaak wordt bijgewerkt met de informatie van uw pakket</span><span class="sxs-lookup"><span data-stu-id="ea82e-148">Updating hello export job with your package information</span></span>
 <span data-ttu-id="ea82e-149">Nadat u het volgnummer hebt, roept u Hallo [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) bewerkingsnaam tooupdated Hallo carrier en het volgnummer voor Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="ea82e-149">After you have your tracking number, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation tooupdated hello carrier name and tracking number for hello job.</span></span> <span data-ttu-id="ea82e-150">U kunt optioneel Hallo aantal stations, Hallo retouradres en ook Hallo back-upfunctie voor datum opgeven.</span><span class="sxs-lookup"><span data-stu-id="ea82e-150">You can optionally specify hello number of drives, hello return address, and hello shipping date as well.</span></span>

## <a name="receiving-hello-package"></a><span data-ttu-id="ea82e-151">Hallo-pakket wordt ontvangen</span><span class="sxs-lookup"><span data-stu-id="ea82e-151">Receiving hello package</span></span>
 <span data-ttu-id="ea82e-152">Nadat de taak voor het exporteren is verwerkt, wordt uw stations tooyou met uw versleutelde gegevens worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ea82e-152">After your export job has been processed, your drives will be returned tooyou with your encrypted data.</span></span> <span data-ttu-id="ea82e-153">U kunt Hallo BitLocker-sleutel ophalen voor elke Hallo stations door aanroepen Hallo [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) bewerking.</span><span class="sxs-lookup"><span data-stu-id="ea82e-153">You can retrieve hello BitLocker key for each of hello drives by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="ea82e-154">U kunt vervolgens Hallo-station met de sleutel Hallo ontgrendelen.</span><span class="sxs-lookup"><span data-stu-id="ea82e-154">You can then unlock hello drive using hello key.</span></span> <span data-ttu-id="ea82e-155">Hallo station manifestbestand op elk station bevat Hallo lijst met bestanden op het Hallo-station, evenals de oorspronkelijke blobadres Hallo voor elk bestand.</span><span class="sxs-lookup"><span data-stu-id="ea82e-155">hello drive manifest file on each drive contains hello list of files on hello drive, as well as hello original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea82e-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ea82e-156">Next steps</span></span>

* [<span data-ttu-id="ea82e-157">Met behulp van REST-API voor Hallo Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="ea82e-157">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
