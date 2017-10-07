---
title: aaaCreate een Import-taak voor Azure Import/Export | Microsoft Docs
description: Meer informatie over hoe toocreate importeren voor Hallo Microsoft Azure Import/Export-service.
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a><span data-ttu-id="ec4a4-103">Maken van een import-taak voor hello Azure Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="ec4a4-103">Creating an import job for hello Azure Import/Export service</span></span>

<span data-ttu-id="ec4a4-104">Maken van een import-taak voor Hallo Hallo REST-API met Microsoft Azure Import/Export-service omvat Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec4a4-104">Creating an import job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="ec4a4-105">Schijven met hello Azure-hulpprogramma voor importeren/exporteren wordt voorbereid.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-105">Preparing drives with hello Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="ec4a4-106">Het verkrijgen van Hallo locatie toowhich tooship Hallo station.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-106">Obtaining hello location toowhich tooship hello drive.</span></span>

-   <span data-ttu-id="ec4a4-107">Hallo import-taak maken.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-107">Creating hello import job.</span></span>

-   <span data-ttu-id="ec4a4-108">Back-upfunctie Hallo tooMicrosoft stations via een ondersteunde Provider-service.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-108">Shipping hello drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="ec4a4-109">Hallo import-taak met details van de back-upfunctie Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-109">Updating hello import job with hello shipping details.</span></span>

 <span data-ttu-id="ec4a4-110">Zie [Hallo Microsoft Azure Import/Export-service tooTransfer gegevens tooBlob opslag met](storage-import-export-service.md) voor een overzicht van Hallo Import/Export-service en een zelfstudie die u laat zien hoe toouse hello [Azure-portal](https://portal.azure.com/) toocreate en beheren van importeren en exporteren van taken.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-110">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure  portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a><span data-ttu-id="ec4a4-111">Voorbereiden van schijven met hello Azure-hulpprogramma voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="ec4a4-111">Preparing drives with hello Azure Import/Export Tool</span></span>

<span data-ttu-id="ec4a4-112">Hallo stappen tooprepare stations voor een import-taak zijn Hallo dezelfde of hebt u Hallo jobvia Hallo portal of via Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-112">hello steps tooprepare drives for an import job are hello same whether you create hello jobvia hello portal or via hello REST API.</span></span>

<span data-ttu-id="ec4a4-113">Hieronder vindt u een kort overzicht van de voorbereiding van het station.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="ec4a4-114">Raadpleeg toohello [Azure Import-ExportTool verwijzing](storage-import-export-tool-how-to-v1.md) voor volledige instructies.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-114">Refer toohello [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="ec4a4-115">U kunt hello Azure-hulpprogramma voor importeren/exporteren downloaden [hier](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="ec4a4-115">You can download hello Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="ec4a4-116">Voorbereiden van de schijf omvat:</span><span class="sxs-lookup"><span data-stu-id="ec4a4-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="ec4a4-117">Identificerende Hallo gegevens toobe geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-117">Identifying hello data toobe imported.</span></span>

-   <span data-ttu-id="ec4a4-118">Hallo bestemming blobs in Windows Azure-opslagservice identificeren.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-118">Identifying hello destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="ec4a4-119">Met behulp van hello Azure-hulpprogramma voor importeren/exporteren toocopy uw gegevens tooone of meer harde schijven.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-119">Using hello Azure Import/Export Tool toocopy your data tooone or more hard drives.</span></span>

 <span data-ttu-id="ec4a4-120">Hello Azure-hulpprogramma voor importeren/exporteren wordt ook een manifestbestand genereren voor elk van de stations Hallo als deze wordt voorbereid.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-120">hello Azure Import/Export Tool will also generate a manifest file for each of hello drives as it is prepared.</span></span> <span data-ttu-id="ec4a4-121">Een manifestbestand bevat:</span><span class="sxs-lookup"><span data-stu-id="ec4a4-121">A manifest file contains:</span></span>

-   <span data-ttu-id="ec4a4-122">Een opsomming van alle Hallo bestanden die zijn bedoeld voor het uploaden en Hallo toewijzingen van deze bestanden tooblobs.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-122">An enumeration of all hello files intended for upload and hello mappings from these files tooblobs.</span></span>

-   <span data-ttu-id="ec4a4-123">Controlesommen van Hallo segmenten van elk bestand.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-123">Checksums of hello segments of each file.</span></span>

-   <span data-ttu-id="ec4a4-124">Informatie over de metagegevens en eigenschappen tooassociate Hallo met elke blob.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-124">Information about hello metadata and properties tooassociate with each blob.</span></span>

-   <span data-ttu-id="ec4a4-125">Een lijst van Hallo actie tootake als een blob die wordt geüpload Hallo heeft dezelfde naam als een bestaande blob in Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-125">A listing of hello action tootake if a blob that is being uploaded has hello same name as an existing blob in hello container.</span></span> <span data-ttu-id="ec4a4-126">Mogelijke opties zijn: a) blob Hallo overschrijven met Hallo-bestand, b) houden Hallo bestaande blob- en skip Hallo-bestand uploadt, c) toevoegen aan de naam van een achtervoegsel toohello dat geen met andere bestanden conflict.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-126">Possible options are: a) overwrite hello blob with hello file, b) keep hello existing blob and skip uploading hello file, c) append a suffix toohello name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="ec4a4-127">Het verkrijgen van de locatie van uw back-ups</span><span class="sxs-lookup"><span data-stu-id="ec4a4-127">Obtaining your shipping location</span></span>

<span data-ttu-id="ec4a4-128">Voordat u een import-taak maakt, moet u tooobtain de naam van een locatie en het adres door de aanroepende Hallo [lijst locaties](/rest/api/storageimportexport/listlocations) bewerking.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-128">Before creating an import job, you need tooobtain a shipping location name and address by calling hello [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="ec4a4-129">`List Locations`retourneert een lijst met locaties en hun e-mailadressen.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="ec4a4-130">U kunt een locatie selecteren van Hallo lijst geretourneerd en verzendadres uw toothat harde schijven.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-130">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="ec4a4-131">U kunt ook Hallo `Get Location` bewerking tooobtain Hallo verzendadres rechtstreeks voor een specifieke locatie.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-131">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

 <span data-ttu-id="ec4a4-132">Hallo stappen hieronder tooobtain Hallo back-upfunctie locatie:</span><span class="sxs-lookup"><span data-stu-id="ec4a4-132">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="ec4a4-133">Geef de naam Hallo Hallo-locatie van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-133">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="ec4a4-134">Deze waarde kan worden gevonden in het Hallo **locatie** op Hallo van het opslagaccount **Dashboard** in Azure portal of voor de query met behulp van Hallo service management API-bewerking Hallo [opslag ophalen Eigenschappen van account](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="ec4a4-134">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello Azure portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="ec4a4-135">Hallo-locatie die beschikbaar tooprocess dit opslagaccount ophalen door de aanroepende Hallo `Get Location` bewerking.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-135">Retrieve hello location that is available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="ec4a4-136">Als hello `AlternateLocations` eigenschap Hallo locatie Hallo locatie zelf bevat, dan is dit geen probleem toouse deze locatie.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-136">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="ec4a4-137">Anders aanroepen Hallo `Get Location` opnieuw met een van de alternatieve locaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-137">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="ec4a4-138">de oorspronkelijke locatie Hallo mogelijk tijdelijk worden gesloten voor onderhoud.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-138">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-import-job"></a><span data-ttu-id="ec4a4-139">Hallo import-taak maken</span><span class="sxs-lookup"><span data-stu-id="ec4a4-139">Creating hello import job</span></span>
<span data-ttu-id="ec4a4-140">toocreate hello import-taak, aanroep Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-140">toocreate hello import job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="ec4a4-141">U moet tooprovide Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="ec4a4-141">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="ec4a4-142">Een naam voor het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-142">A name for hello job.</span></span>

-   <span data-ttu-id="ec4a4-143">Hallo opslagaccountnaam.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-143">hello storage account name.</span></span>

-   <span data-ttu-id="ec4a4-144">Hallo locatienaam, verkregen van de vorige stap Hallo back-upfunctie.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-144">hello shipping location name, obtained from hello previous step.</span></span>

-   <span data-ttu-id="ec4a4-145">Een taaktype (importeren).</span><span class="sxs-lookup"><span data-stu-id="ec4a4-145">A job type (Import).</span></span>

-   <span data-ttu-id="ec4a4-146">Hallo-retouradres waar Hallo schijven moeten worden verzonden nadat Hallo import-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-146">hello return address where hello drives should be sent after hello import job has completed.</span></span>

-   <span data-ttu-id="ec4a4-147">Hallo-lijst met stations in Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-147">hello list of drives in hello job.</span></span> <span data-ttu-id="ec4a4-148">Voor elk station moet u de volgende informatie die is verkregen tijdens de stap ter voorbereiding van Hallo station Hallo opnemen:</span><span class="sxs-lookup"><span data-stu-id="ec4a4-148">For each drive, you must include hello following information that was obtained during hello drive preparation step:</span></span>

    -   <span data-ttu-id="ec4a4-149">Hallo station Id</span><span class="sxs-lookup"><span data-stu-id="ec4a4-149">hello drive Id</span></span>

    -   <span data-ttu-id="ec4a4-150">Hallo BitLocker-sleutel</span><span class="sxs-lookup"><span data-stu-id="ec4a4-150">hello BitLocker key</span></span>

    -   <span data-ttu-id="ec4a4-151">Hallo manifestbestand relatief pad op de harde schijf Hallo</span><span class="sxs-lookup"><span data-stu-id="ec4a4-151">hello manifest file relative path on hello hard drive</span></span>

    -   <span data-ttu-id="ec4a4-152">Hallo Base16 gecodeerd manifestbestand MD5-hash</span><span class="sxs-lookup"><span data-stu-id="ec4a4-152">hello Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="ec4a4-153">Verzending van uw schijven</span><span class="sxs-lookup"><span data-stu-id="ec4a4-153">Shipping your drives</span></span>
<span data-ttu-id="ec4a4-154">U moet uw stations toohello-adres dat u hebt ontvangen van de vorige stap Hallo verzenden en u Hallo Import/Export-service met het volgnummer van het pakket Hallo Hallo moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-154">You must ship your drives toohello address that you obtained from hello previous step, and you must provide hello Import/Export service with hello tracking number of hello package.</span></span>

> [!NOTE]
>  <span data-ttu-id="ec4a4-155">U moet uw stations via een ondersteunde Provider-service, die het pakket van een volgnummer voorzien verzenden.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-import-job-with-your-shipping-information"></a><span data-ttu-id="ec4a4-156">Hallo import-taak wordt bijgewerkt met uw back-ups van gegevens</span><span class="sxs-lookup"><span data-stu-id="ec4a4-156">Updating hello import job with your shipping information</span></span>
<span data-ttu-id="ec4a4-157">Nadat u het volgnummer hebt, roept u Hallo [Update taakeigenschappen](/api/storageimportexport/jobs#Jobs_Update) bewerking tooupdate Hallo carrier naam, Hallo volgnummer voor Hallo taak en Hallo carrier nummer voor return back-ups van de back-upfunctie.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-157">After you have your tracking number, call hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation tooupdate hello shipping carrier name, hello tracking number for hello job, and hello carrier account number for return shipping.</span></span> <span data-ttu-id="ec4a4-158">U kunt optioneel Hallo aantal stations- en back-upfunctie ook datum Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="ec4a4-158">You can optionally specify hello number of drives and hello shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec4a4-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec4a4-159">Next steps</span></span>

* [<span data-ttu-id="ec4a4-160">Met behulp van REST-API voor Hallo Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="ec4a4-160">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
