---
title: prestatieniveaus aaaDocumentDB API | Microsoft Docs
description: Meer informatie over hoe prestatieniveaus DocumentDB API u tooreserve doorvoer op basis van de per-container kunnen.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a><span data-ttu-id="4b9cd-103">Hallo S1, S2 en S3 prestatieniveaus buiten gebruik stellen</span><span class="sxs-lookup"><span data-stu-id="4b9cd-103">Retiring hello S1, S2, and S3 performance levels</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4b9cd-104">Hallo te S1, S2 en S3 prestatieniveaus, besproken in dit artikel worden buiten gebruik gesteld en zijn niet meer beschikbaar voor nieuwe DocumentDB-API-accounts.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-104">hello S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB API accounts.</span></span>
>

<span data-ttu-id="4b9cd-105">Dit artikel biedt een overzicht van S1, S2 en S3 prestatieniveaus en wordt beschreven hoe Hallo verzamelingen die gebruikmaken van deze prestatieniveaus gemigreerde toosingle partitie verzamelingen op 1e augustus 2017 zijn.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how hello collections that use these performance levels will be migrated toosingle partition collections on August 1st, 2017.</span></span> <span data-ttu-id="4b9cd-106">Na het lezen van dit artikel, moet u kunnen tooanswer Hallo vragen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b9cd-106">After reading this article, you'll be able tooanswer hello following questions:</span></span>

- [<span data-ttu-id="4b9cd-107">Waarom worden Hallo S1, S2 en S3 prestaties niveaus buiten gebruik gesteld?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-107">Why are hello S1, S2, and S3 performance levels being retired?</span></span>](#why-retired)
- [<span data-ttu-id="4b9cd-108">Hoe verzamelingen met één partitie en gepartitioneerde verzamelingen Vergelijk toohello S1, S2 S3 prestatieniveaus?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-108">How do single partition collections and partitioned collections compare toohello S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="4b9cd-109">Wat kan ik moet toodo tooensure ononderbroken toegangsgegevens toomy?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-109">What do I need toodo tooensure uninterrupted access toomy data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="4b9cd-110">Hoe wordt mijn verzameling wijzigen na de migratie Hallo?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-110">How will my collection change after hello migration?</span></span>](#collection-change)
- [<span data-ttu-id="4b9cd-111">Hoe wordt mijn facturering wijzigen nadat ik gemigreerde toosingle partitie verzamelingen?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-111">How will my billing change after I’m migrated toosingle partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="4b9cd-112">Wat gebeurt er als ik meer dan 10 GB aan opslagruimte nodig?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="4b9cd-113">Kan ik tussen Hallo S1, S2 en S3 prestatieniveaus vóór 1 augustus 2017 wijzigen?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-113">Can I change between hello S1, S2, and S3 performance levels before August 1, 2017?</span></span>](#change-before)
- [<span data-ttu-id="4b9cd-114">Hoe weet ik wanneer de verzameling is gemigreerd?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-114">How will I know when my collection has migrated?</span></span>](#when-migrated)
- [<span data-ttu-id="4b9cd-115">Hoe Migreer ik van Hallo S1, S2, S3 prestaties niveaus toosingle verzamelingen partitie zelf?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-115">How do I migrate from hello S1, S2, S3 performance levels toosingle partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="4b9cd-116">Hoe ben ik als ik een klant EA beïnvloed?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-116">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="4b9cd-117">Waarom worden Hallo S1, S2 en S3 prestaties niveaus buiten gebruik gesteld?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-117">Why are hello S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="4b9cd-118">Hallo S1, S2 en S3 prestatieniveaus doen niet aanbieding Hallo flexibiliteit die verzamelingen van DocumentDB API biedt.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-118">hello S1, S2, and S3 performance levels do not offer hello flexibility that DocumentDB API collections offers.</span></span> <span data-ttu-id="4b9cd-119">Hello S1, S2, S3 prestatieniveaus, beide Hallo doorvoer en de opslagcapaciteit vooraf zijn ingesteld en is niet aangeboden elasticiteit.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-119">With hello S1, S2, S3 performance levels, both hello throughput and storage capacity were pre-set and did not offer elasticity.</span></span> <span data-ttu-id="4b9cd-120">Azure Cosmos DB biedt nu Hallo mogelijkheid toocustomize uw doorvoer en opslag, biedt veel meer flexibiliteit in uw tooscale mogelijkheid naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-120">Azure Cosmos DB now offers hello ability toocustomize your throughput and storage, offering you much more flexibility in your ability tooscale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a><span data-ttu-id="4b9cd-121">Hoe verzamelingen met één partitie en gepartitioneerde verzamelingen Vergelijk toohello S1, S2 S3 prestatieniveaus?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-121">How do single partition collections and partitioned collections compare toohello S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="4b9cd-122">Hallo volgende tabel vergelijkt Hallo doorvoer en opslag beschikbare opties in verzamelingen met één partitie, gepartitioneerde verzamelingen en S1, S2, S3 prestatieniveaus.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-122">hello following table compares hello throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="4b9cd-123">Hier volgt een voorbeeld voor de regio VS Oost 2:</span><span class="sxs-lookup"><span data-stu-id="4b9cd-123">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="4b9cd-124">Gepartitioneerde verzameling</span><span class="sxs-lookup"><span data-stu-id="4b9cd-124">Partitioned collection</span></span>|<span data-ttu-id="4b9cd-125">Verzameling van één partitie</span><span class="sxs-lookup"><span data-stu-id="4b9cd-125">Single partition collection</span></span>|<span data-ttu-id="4b9cd-126">S1</span><span class="sxs-lookup"><span data-stu-id="4b9cd-126">S1</span></span>|<span data-ttu-id="4b9cd-127">S2</span><span class="sxs-lookup"><span data-stu-id="4b9cd-127">S2</span></span>|<span data-ttu-id="4b9cd-128">S3</span><span class="sxs-lookup"><span data-stu-id="4b9cd-128">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="4b9cd-129">Maximale doorvoer</span><span class="sxs-lookup"><span data-stu-id="4b9cd-129">Maximum throughput</span></span>|<span data-ttu-id="4b9cd-130">Onbeperkt</span><span class="sxs-lookup"><span data-stu-id="4b9cd-130">Unlimited</span></span>|<span data-ttu-id="4b9cd-131">10 K RU/s</span><span class="sxs-lookup"><span data-stu-id="4b9cd-131">10K RU/s</span></span>|<span data-ttu-id="4b9cd-132">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="4b9cd-132">250 RU/s</span></span>|<span data-ttu-id="4b9cd-133">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="4b9cd-133">1 K RU/s</span></span>|<span data-ttu-id="4b9cd-134">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="4b9cd-134">2.5 K RU/s</span></span>|
|<span data-ttu-id="4b9cd-135">Minimaal doorvoer</span><span class="sxs-lookup"><span data-stu-id="4b9cd-135">Minimum throughput</span></span>|<span data-ttu-id="4b9cd-136">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="4b9cd-136">2.5K RU/s</span></span>|<span data-ttu-id="4b9cd-137">400 RU/s</span><span class="sxs-lookup"><span data-stu-id="4b9cd-137">400 RU/s</span></span>|<span data-ttu-id="4b9cd-138">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="4b9cd-138">250 RU/s</span></span>|<span data-ttu-id="4b9cd-139">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="4b9cd-139">1 K RU/s</span></span>|<span data-ttu-id="4b9cd-140">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="4b9cd-140">2.5 K RU/s</span></span>|
|<span data-ttu-id="4b9cd-141">Maximale opslag</span><span class="sxs-lookup"><span data-stu-id="4b9cd-141">Maximum storage</span></span>|<span data-ttu-id="4b9cd-142">Onbeperkt</span><span class="sxs-lookup"><span data-stu-id="4b9cd-142">Unlimited</span></span>|<span data-ttu-id="4b9cd-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="4b9cd-143">10 GB</span></span>|<span data-ttu-id="4b9cd-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="4b9cd-144">10 GB</span></span>|<span data-ttu-id="4b9cd-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="4b9cd-145">10 GB</span></span>|<span data-ttu-id="4b9cd-146">10 GB</span><span class="sxs-lookup"><span data-stu-id="4b9cd-146">10 GB</span></span>|
|<span data-ttu-id="4b9cd-147">Prijs (maandelijks)</span><span class="sxs-lookup"><span data-stu-id="4b9cd-147">Price (monthly)</span></span>|<span data-ttu-id="4b9cd-148">Doorvoer: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="4b9cd-148">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="4b9cd-149">Opslag: $ 0,25/GB</span><span class="sxs-lookup"><span data-stu-id="4b9cd-149">Storage: $0.25/GB</span></span>|<span data-ttu-id="4b9cd-150">Doorvoer: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="4b9cd-150">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="4b9cd-151">Opslag: $ 0,25/GB</span><span class="sxs-lookup"><span data-stu-id="4b9cd-151">Storage: $0.25/GB</span></span>|<span data-ttu-id="4b9cd-152">25 USD $</span><span class="sxs-lookup"><span data-stu-id="4b9cd-152">$25 USD</span></span>|<span data-ttu-id="4b9cd-153">50 USD $</span><span class="sxs-lookup"><span data-stu-id="4b9cd-153">$50 USD</span></span>|<span data-ttu-id="4b9cd-154">100 USD $</span><span class="sxs-lookup"><span data-stu-id="4b9cd-154">$100 USD</span></span>|

<span data-ttu-id="4b9cd-155">Weet u een klant EA?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-155">Are you an EA customer?</span></span> <span data-ttu-id="4b9cd-156">Zo ja, Zie [hoe ben ik beïnvloed als ik een klant EA?](#ea-customer)</span><span class="sxs-lookup"><span data-stu-id="4b9cd-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a><span data-ttu-id="4b9cd-157">Wat kan ik moet toodo tooensure ononderbroken toegangsgegevens toomy?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-157">What do I need toodo tooensure uninterrupted access toomy data?</span></span>

<span data-ttu-id="4b9cd-158">Er is niets, Cosmos DB Hallo migratie voor u verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-158">Nothing, Cosmos DB handles hello migration for you.</span></span> <span data-ttu-id="4b9cd-159">Als u een verzameling S1, S2 of S3 hebt, worden uw huidige verzameling gemigreerde tooa één partitie verzameling op 31 juli 2017.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-159">If you have an S1, S2, or S3 collection, your current collection will be migrated tooa single partition collection on July 31, 2017.</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a><span data-ttu-id="4b9cd-160">Hoe wordt mijn verzameling wijzigen na de migratie Hallo?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-160">How will my collection change after hello migration?</span></span>

<span data-ttu-id="4b9cd-161">Als u een verzameling S1 hebt, kunt u zich gemigreerde tooa één partitie verzameling met 400 RU/s-doorvoer.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-161">If you have an S1 collection, you will be migrated tooa single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="4b9cd-162">400 RU/s is Hallo laagste doorvoer beschikbaar met verzamelingen met één partitie.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-162">400 RU/s is hello lowest throughput available with single partition collections.</span></span> <span data-ttu-id="4b9cd-163">Hallo-kosten voor 400 RU/s in een verzameling één partitie is ongeveer Hallo gelijk zijn aan u zijn betaling met uw verzameling S1 Hallo en 250 RU/s – zodat u niet betalen Hallo echter extra 150 RU/s beschikbaar tooyou.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-163">However, hello cost for 400 RU/s in hello a single partition collection is approximately hello same as you were paying with your S1 collection and 250 RU/s – so you are not paying for hello extra 150 RU/s available tooyou.</span></span>

<span data-ttu-id="4b9cd-164">Als u een verzameling S2 hebt, kunt u zich gemigreerde tooa één partitie verzameling met 1 K RU/s.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-164">If you have an S2 collection, you will be migrated tooa single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="4b9cd-165">Hier ziet u geen wijziging tooyour doorvoerniveau.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-165">You will see no change tooyour throughput level.</span></span>

<span data-ttu-id="4b9cd-166">Als u een verzameling S3 hebt, kunt u zich gemigreerde tooa één partitie verzameling met 2,5 K RU/s.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-166">If you have an S3 collection, you will be migrated tooa single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="4b9cd-167">Hier ziet u geen wijziging tooyour doorvoerniveau.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-167">You will see no change tooyour throughput level.</span></span>

<span data-ttu-id="4b9cd-168">In elk van deze gevallen, nadat uw verzameling wordt gemigreerd, u worden kunnen toocustomize uw doorvoerniveau of het omhoog en omlaag schalen als benodigde tooprovide lage latentie toegang tooyour gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-168">In each of these cases, after your collection is migrated, you will be able toocustomize your throughput level, or scale it up and down as needed tooprovide low-latency access tooyour users.</span></span> <span data-ttu-id="4b9cd-169">toochange hello doorvoerniveau nadat uw verzameling is gemigreerd, gewoon uw account Cosmos DB in hello Azure-portal openen, klikt u op schaal, kies uw verzameling en pas Hallo doorvoerniveau, zoals wordt weergegeven in de volgende schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="4b9cd-169">toochange hello throughput level after your collection has migrated, simply open your Cosmos DB account in hello Azure portal, click Scale, choose your collection, and then adjust hello throughput level, as shown in hello following screenshot:</span></span>

![Hoe tooscale doorvoer in hello Azure-portal](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a><span data-ttu-id="4b9cd-171">Hoe wordt mijn facturering wijzigen nadat ik verzamelingen met één partitie gemigreerde toohello?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-171">How will my billing change after I’m migrated toohello single partition collections?</span></span>

<span data-ttu-id="4b9cd-172">Ervan uitgaande dat u 10 S1 verzamelingen, 1 GB aan opslagruimte voor elk in de regio VS-Oost Hallo hebt en u deze 10 S1 verzamelingen too10 verzamelingen met één partitie op 400 RU per seconde (minimaal niveau hebben Hallo) migreert.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in hello US East region, and you migrate these 10 S1 collections too10 single partition collections at 400 RU/sec (hello minimum level).</span></span> <span data-ttu-id="4b9cd-173">Uw factuur wordt er als volgt uitzien als u verzamelingen met Hallo 10 één partitie voor een volledige maand behouden:</span><span class="sxs-lookup"><span data-stu-id="4b9cd-173">Your bill will look as follows if you keep hello 10 single partition collections for a full month:</span></span>

![Hoe too10 verzamelingen S1 prijzen voor 10 verzamelingen vergelijkt met prijzen voor een verzameling van één partitie](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="4b9cd-175">Wat gebeurt er als ik meer dan 10 GB aan opslagruimte nodig?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-175">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="4b9cd-176">Of u een verzameling met een prestatieniveau S1, S2 of S3 of een verzameling van één partitie, die allemaal 10 GB aan opslagruimte hebt, kunt u Hallo Cosmos DB Data Migration tool toomigrate uw gegevens tooa gepartitioneerd verzameling met vrijwel onbeperkte opslag.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use hello Cosmos DB Data Migration tool toomigrate your data tooa partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="4b9cd-177">Zie voor meer informatie over Hallo voordelen van een gepartitioneerde verzameling [partitionering en schalen in Azure Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="4b9cd-177">For information about hello benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="4b9cd-178">Voor informatie over het toomigrate uw S1, S2, S3 of één partitie verzameling tooa gepartitioneerd verzameling, Zie [migreren van één partitie toopartitioned verzamelingen](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="4b9cd-178">For information about how toomigrate your S1, S2, S3, or single partition collection tooa partitioned collection, see [Migrating from single-partition toopartitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a><span data-ttu-id="4b9cd-179">Kan ik tussen Hallo S1, S2 en S3 prestatieniveaus vóór 1 augustus 2017 wijzigen?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-179">Can I change between hello S1, S2, and S3 performance levels before August 1, 2017?</span></span>

<span data-ttu-id="4b9cd-180">Alleen bestaande accounts met S1, S2 en S3 prestaties wordt kunnen toochange en alter niveau prestatielagen via Hallo portal of programmatisch.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-180">Only existing accounts with S1, S2, and S3 performance will be able toochange and alter performance level tiers through hello portal or programmatically.</span></span> <span data-ttu-id="4b9cd-181">1 augustus 2017 Hallo S1, S2 en prestatieniveaus S3 niet langer beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-181">By August 1, 2017, hello S1, S2, and S3 performance levels will no longer be available.</span></span> <span data-ttu-id="4b9cd-182">Als u uit S1, S3 of S3 tooa één partitie verzameling wijzigt, kunt niet u teruggaan toohello S1, S2 of S3 prestatieniveaus.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-182">If you change from S1, S3, or S3 tooa single partition collection, you cannot return toohello S1, S2, or S3 performance levels.</span></span>

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a><span data-ttu-id="4b9cd-183">Hoe weet ik wanneer de verzameling is gemigreerd?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-183">How will I know when my collection has migrated?</span></span>

<span data-ttu-id="4b9cd-184">Hallo migratie wordt uitgevoerd op 31 juli 2017.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-184">hello migration will occur on July 31, 2017.</span></span> <span data-ttu-id="4b9cd-185">Als u een verzameling hebt die gebruikmaakt van Hallo S1, S2 of S3 prestatieniveaus, Hallo Cosmos-DB-team neemt contact met u per e-mail voordat Hallo migratie plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-185">If you have a collection that uses hello S1, S2 or S3 performance levels, hello Cosmos DB team will contact you by email before hello migration takes place.</span></span> <span data-ttu-id="4b9cd-186">Wanneer Hallo migratie voltooid, op 1 augustus 2017 is weergegeven hello Azure-portal dat gebruikmaakt van uw verzameling standaardprijzen.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-186">Once hello migration is complete, on August 1, 2017, hello Azure portal will show that your collection uses Standard pricing.</span></span>

![Hoe tooconfirm uw verzameling is gemigreerd toohello standaardcategorie prijzen](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a><span data-ttu-id="4b9cd-188">Hoe Migreer ik van Hallo S1, S2, S3 prestaties niveaus toosingle verzamelingen partitie zelf?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-188">How do I migrate from hello S1, S2, S3 performance levels toosingle partition collections on my own?</span></span>

<span data-ttu-id="4b9cd-189">U kunt migreren vanaf Hallo S1, S2 en S3 prestaties niveaus toosingle partitie verzamelingen met hello Azure-portal of programmatisch.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-189">You can migrate from hello S1, S2, and S3 performance levels toosingle partition collections using hello Azure portal or programmatically.</span></span> <span data-ttu-id="4b9cd-190">U kunt dit doen op uw eigen vóór 1 augustus toobenefit uit Hallo doorvoer flexibele opties beschikbaar met verzamelingen met één partitie of we uw verzamelingen die u wilt migreren op 31 juli 2017.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-190">You can do this on your own before August 1 toobenefit from hello flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span></span>

<span data-ttu-id="4b9cd-191">**verzamelingen toomigrate toosingle partitie met hello Azure-portal**</span><span class="sxs-lookup"><span data-stu-id="4b9cd-191">**toomigrate toosingle partition collections using hello Azure portal**</span></span>

1. <span data-ttu-id="4b9cd-192">In Hallo [ **Azure-portal**](https://portal.azure.com), klikt u op **Azure Cosmos DB**, selecteer vervolgens Hallo Cosmos DB account toomodify.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-192">In hello [**Azure portal**](https://portal.azure.com), click **Azure Cosmos DB**, then select hello Cosmos DB account toomodify.</span></span> 
 
    <span data-ttu-id="4b9cd-193">Als **Azure Cosmos DB** is niet op Hallo van Snelbalk, klikt u op >, te schuiven**Databases**, selecteer **Azure Cosmos DB**, en selecteer vervolgens Hallo DocumentDB-account.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-193">If **Azure Cosmos DB** is not on hello Jumpbar, click >, scroll too**Databases**, select **Azure Cosmos DB**, and then select hello DocumentDB account.</span></span>  

2. <span data-ttu-id="4b9cd-194">Hallo resource menu onder **Containers**, klikt u op **Scale**Hallo verzameling toomodify selecteert in de vervolgkeuzelijst Hallo en klik vervolgens op **prijscategorie**.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-194">On hello resource menu, under **Containers**, click **Scale**, select hello collection toomodify from hello drop-down list, and then click **Pricing Tier**.</span></span> <span data-ttu-id="4b9cd-195">Accounts met behulp van vooraf gedefinieerde doorvoer hebben een prijscategorie S1, S2 of S3.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span></span>  <span data-ttu-id="4b9cd-196">In Hallo **Kies uw prijscategorie** blade, klikt u op **standaard** toochange toouser gedefinieerde doorvoer en klik vervolgens op **Selecteer** toosave uw wijziging.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-196">In hello **Choose your pricing tier** blade, click **Standard** toochange toouser-defined throughput, and then click **Select** toosave your change.</span></span>

    ![Schermopname van de blade instellingen Hallo weergegeven waar toochange doorvoercapaciteit Hallo](./media/performance-levels/change-performance-set-thoughput.png)

3. <span data-ttu-id="4b9cd-198">Terug in Hallo **Scale** blade, Hallo **prijscategorie** wordt gewijzigd te**standaard** en Hallo **doorvoer (RU/s)** wordt weergegeven met een de standaardwaarde van 400.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-198">Back in hello **Scale** blade, hello **Pricing Tier** is changed too**Standard** and hello **Throughput (RU/s)** box is displayed with a default value of 400.</span></span> <span data-ttu-id="4b9cd-199">Set Hallo doorvoer tussen 400 en 10.000 [Aanvraageenheden](request-units.md)/second (RU/s).</span><span class="sxs-lookup"><span data-stu-id="4b9cd-199">Set hello throughput between 400 and 10,000 [Request units](request-units.md)/second (RU/s).</span></span> <span data-ttu-id="4b9cd-200">Hallo **maandelijkse factuur geschatte** onderin Hallo Hallo pagina wordt automatisch bijgewerkt tooprovide een schatting maken van Hallo maandelijkse kosten.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-200">hello **Estimated Monthly Bill** at hello bottom of hello page updates automatically tooprovide an estimate of hello monthly cost.</span></span> 

    >[!IMPORTANT] 
    > <span data-ttu-id="4b9cd-201">Nadat u uw wijzigingen hebt opgeslagen en de Standard-prijscategorie toohello verplaatsen, terugdraaien u niet toohello S1, S2 of S3 prestatieniveaus.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-201">Once you save your changes and move toohello Standard pricing tier, you cannot roll back toohello S1, S2, or S3 performance levels.</span></span>

4. <span data-ttu-id="4b9cd-202">Klik op **opslaan** toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-202">Click **Save** toosave your changes.</span></span>

    <span data-ttu-id="4b9cd-203">Als u vaststelt dat u meer doorvoer (groter dan 10.000 RU/s) of meer opslagruimte moet (groter dan 10GB), kunt u een gepartitioneerde verzameling kunt maken.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span></span> <span data-ttu-id="4b9cd-204">Zie voor een verzameling van één partitie verzameling tooa gepartitioneerd, toomigrate [migreren van één partitie toopartitioned verzamelingen](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="4b9cd-204">toomigrate a single partition collection tooa partitioned collection, see [Migrating from single-partition toopartitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4b9cd-205">Het wijzigen van S1, S2 of S3 tooStandard kan up too2 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-205">Changing from S1, S2, or S3 tooStandard may take up too2 minutes.</span></span>
    > 
    > 

<span data-ttu-id="4b9cd-206">**verzamelingen toomigrate toosingle partitie met Hallo .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="4b9cd-206">**toomigrate toosingle partition collections using hello .NET SDK**</span></span>

<span data-ttu-id="4b9cd-207">Er is een andere optie voor het wijzigen van de uw verzamelingen prestatieniveaus via onze SDK's.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-207">Another option for changing your collections' performance levels is through our SDKs.</span></span> <span data-ttu-id="4b9cd-208">Deze sectie bevat alleen de prestaties van een verzameling wijzigen met behulp van het serviceniveau onze [DocumentDB .NET API](documentdb-sdk-dotnet.md), maar het Hallo-proces is vergelijkbaar voor onze andere SDK.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-208">This section only covers changing a collection's performance level using our [DocumentDB .NET API](documentdb-sdk-dotnet.md), but hello process is similar for our other SDKs.</span></span>

<span data-ttu-id="4b9cd-209">Hier volgt een codefragment voor het wijzigen van Hallo verzameling doorvoer too5 000 aanvraageenheden per seconde:</span><span class="sxs-lookup"><span data-stu-id="4b9cd-209">Here is a code snippet for changing hello collection throughput too5,000 request units per second:</span></span>
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="4b9cd-210">Ga naar [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview aanvullende voorbeelden en meer informatie over onze aanbieding methoden:</span><span class="sxs-lookup"><span data-stu-id="4b9cd-210">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="4b9cd-211">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="4b9cd-211">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="4b9cd-212">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="4b9cd-212">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="4b9cd-213">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="4b9cd-213">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="4b9cd-214">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="4b9cd-214">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="4b9cd-215">Hoe ben ik als ik een klant EA beïnvloed?</span><span class="sxs-lookup"><span data-stu-id="4b9cd-215">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="4b9cd-216">EA klanten worden beveiligd tot einde van het huidige contract Hallo prijs.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-216">EA customers will be price protected until hello end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b9cd-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b9cd-217">Next steps</span></span>
<span data-ttu-id="4b9cd-218">toolearn meer informatie over prijzen en het beheren van gegevens met Azure Cosmos DB, bekijk deze resources:</span><span class="sxs-lookup"><span data-stu-id="4b9cd-218">toolearn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span></span>

1.  <span data-ttu-id="4b9cd-219">[Partitioneren van gegevens in Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="4b9cd-219">[Partitioning data in Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="4b9cd-220">Hallo verschil tussen één partitie container en gepartitioneerde containers, evenals tips voor het implementeren van een partitionering strategie tooscale naadloos.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-220">Understand hello difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy tooscale seamlessly.</span></span>
2.  <span data-ttu-id="4b9cd-221">[Prijzen voor cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="4b9cd-221">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> <span data-ttu-id="4b9cd-222">Meer informatie over Hallo kosten van de inrichting van de doorvoer en opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-222">Learn about hello cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="4b9cd-223">[Aanvraageenheden](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="4b9cd-223">[Request units](request-units.md).</span></span> <span data-ttu-id="4b9cd-224">Hallo-verbruik van doorvoer voor een andere bewerkingstypen, bijvoorbeeld lezen, schrijven, Query begrijpen.</span><span class="sxs-lookup"><span data-stu-id="4b9cd-224">Understand hello consumption of throughput for different operation types, for example Read, Write, Query.</span></span>
