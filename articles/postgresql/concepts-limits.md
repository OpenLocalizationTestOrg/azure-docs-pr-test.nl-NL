---
title: aaaLimitations in Azure-Database voor PostgreSQL | Microsoft Docs
description: Beschrijft de beperkingen in Azure-Database voor PostgreSQL.
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: f53dd240e55e0633bc1dfb8ad25e1818fa8ae18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="28bb7-103">Beperkingen in Azure-Database voor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="28bb7-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="28bb7-104">Hello Azure Database voor PostgreSQL-service is in de openbare preview.</span><span class="sxs-lookup"><span data-stu-id="28bb7-104">hello Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="28bb7-105">Hallo volgende secties beschrijven capaciteit en functionele limieten in Hallo database-service.</span><span class="sxs-lookup"><span data-stu-id="28bb7-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="28bb7-106">Service Tier maximumwaarden</span><span class="sxs-lookup"><span data-stu-id="28bb7-106">Service Tier Maximums</span></span>
<span data-ttu-id="28bb7-107">Azure PostgreSQL-Database heeft meerdere Servicelagen die u kiezen kunt uit bij het maken van een server.</span><span class="sxs-lookup"><span data-stu-id="28bb7-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="28bb7-108">Zie voor meer informatie [begrijpen wat er beschikbaar is in elke servicelaag](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="28bb7-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="28bb7-109">Er is een maximum aantal verbindingen, compute-eenheden en opslag in elke servicelaag tijdens Hallo service preview, als volgt:</span><span class="sxs-lookup"><span data-stu-id="28bb7-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="28bb7-110">**Maximum aantal verbindingen**</span><span class="sxs-lookup"><span data-stu-id="28bb7-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="28bb7-111">Basic 50 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="28bb7-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="28bb7-112">50-verbindingen</span><span class="sxs-lookup"><span data-stu-id="28bb7-112">50 connections</span></span>    |
| <span data-ttu-id="28bb7-113">Basic 100 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="28bb7-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="28bb7-114">100-verbindingen</span><span class="sxs-lookup"><span data-stu-id="28bb7-114">100 connections</span></span>   |
| <span data-ttu-id="28bb7-115">Standaard 100 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="28bb7-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="28bb7-116">200-verbindingen</span><span class="sxs-lookup"><span data-stu-id="28bb7-116">200 connections</span></span>   |
| <span data-ttu-id="28bb7-117">Standaard 200 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="28bb7-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="28bb7-118">300-verbindingen</span><span class="sxs-lookup"><span data-stu-id="28bb7-118">300 connections</span></span>   |
| <span data-ttu-id="28bb7-119">Standaard 400 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="28bb7-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="28bb7-120">400-verbindingen</span><span class="sxs-lookup"><span data-stu-id="28bb7-120">400 connections</span></span>   |
| <span data-ttu-id="28bb7-121">Standaard 800 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="28bb7-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="28bb7-122">500-verbindingen</span><span class="sxs-lookup"><span data-stu-id="28bb7-122">500 connections</span></span>   |
| <span data-ttu-id="28bb7-123">**Maximale Compute-eenheden**</span><span class="sxs-lookup"><span data-stu-id="28bb7-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="28bb7-124">Basisservicelaag</span><span class="sxs-lookup"><span data-stu-id="28bb7-124">Basic service tier</span></span>         | <span data-ttu-id="28bb7-125">100 compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="28bb7-125">100 Compute Units</span></span> |
| <span data-ttu-id="28bb7-126">Standaardservicelaag</span><span class="sxs-lookup"><span data-stu-id="28bb7-126">Standard service tier</span></span>      | <span data-ttu-id="28bb7-127">800 compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="28bb7-127">800 Compute Units</span></span> |
| <span data-ttu-id="28bb7-128">**Maximale opslag**</span><span class="sxs-lookup"><span data-stu-id="28bb7-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="28bb7-129">Basisservicelaag</span><span class="sxs-lookup"><span data-stu-id="28bb7-129">Basic service tier</span></span>         | <span data-ttu-id="28bb7-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="28bb7-130">1 TB</span></span>              |
| <span data-ttu-id="28bb7-131">Standaardservicelaag</span><span class="sxs-lookup"><span data-stu-id="28bb7-131">Standard service tier</span></span>      | <span data-ttu-id="28bb7-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="28bb7-132">1 TB</span></span>              |

<span data-ttu-id="28bb7-133">Wanneer er te veel verbindingen zijn bereikt, wordt het foutbericht Hallo volgende fout:</span><span class="sxs-lookup"><span data-stu-id="28bb7-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="28bb7-134">Onherstelbare fout: er al te veel clients</span><span class="sxs-lookup"><span data-stu-id="28bb7-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="28bb7-135">Functionele beperkingen Preview</span><span class="sxs-lookup"><span data-stu-id="28bb7-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="28bb7-136">Schaalbewerkingen</span><span class="sxs-lookup"><span data-stu-id="28bb7-136">Scale operations</span></span>
1.  <span data-ttu-id="28bb7-137">Dynamische schaalbaarheid van servers in Servicelagen is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="28bb7-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="28bb7-138">Dat wil zeggen, schakelen tussen servicecategorieën Basic en Standard.</span><span class="sxs-lookup"><span data-stu-id="28bb7-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="28bb7-139">Dynamische toename mogelijk op aanvraag van opslag op vooraf gemaakte server is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="28bb7-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="28bb7-140">Verkleinen storage server wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="28bb7-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="28bb7-141">Server-versie-upgrades</span><span class="sxs-lookup"><span data-stu-id="28bb7-141">Server version upgrades</span></span>
- <span data-ttu-id="28bb7-142">Automatische migratie tussen versies van de primaire database-engine is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="28bb7-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="28bb7-143">Beheer van abonnementen</span><span class="sxs-lookup"><span data-stu-id="28bb7-143">Subscription management</span></span>
- <span data-ttu-id="28bb7-144">Dynamisch vooraf gemaakte servers verplaatsen tussen abonnement en resourcegroep is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="28bb7-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="28bb7-145">Een punt in de tijd herstellen</span><span class="sxs-lookup"><span data-stu-id="28bb7-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="28bb7-146">Herstellen van de servicelaag toodifferent en/of Compute-eenheden en de opslaggrootte is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="28bb7-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="28bb7-147">Herstellen van een uitgevallen server wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="28bb7-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28bb7-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="28bb7-148">Next steps</span></span>
- <span data-ttu-id="28bb7-149">Begrijpen [wat is beschikbaar in elke prijscategorie](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="28bb7-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="28bb7-150">Begrijpen [ondersteunde versies van PostgreSQL-Database](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="28bb7-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="28bb7-151">Bekijk [tooBack up en herstel een server in Azure-Database voor het gebruik van PostgreSQL Hallo hoe Azure-portal](howto-restore-server-portal.md)</span><span class="sxs-lookup"><span data-stu-id="28bb7-151">Review [How tooBack up and Restore a server in Azure Database for PostgreSQL using hello Azure portal](howto-restore-server-portal.md)</span></span>
