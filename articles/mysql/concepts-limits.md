---
title: Beperkingen in Azure-Database voor MySQL | Microsoft Docs
description: Preview-beperkingen in Azure-Database voor MySQL beschrijft.
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c61d70897b66c2ffee819ac98c38ab75000db907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a><span data-ttu-id="fb952-103">Beperkingen in Azure-Database voor MySQL (Preview)</span><span class="sxs-lookup"><span data-stu-id="fb952-103">Limitations in Azure Database for MySQL (Preview)</span></span>
<span data-ttu-id="fb952-104">De Azure-Database voor de MySQL-service is in de openbare preview.</span><span class="sxs-lookup"><span data-stu-id="fb952-104">The Azure Database for MySQL service is in public preview.</span></span> <span data-ttu-id="fb952-105">De volgende secties beschrijven de capaciteit en functionele limieten in de database-service.</span><span class="sxs-lookup"><span data-stu-id="fb952-105">The following sections describe capacity and functional limits in the database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="fb952-106">Service Tier maximumwaarden</span><span class="sxs-lookup"><span data-stu-id="fb952-106">Service Tier Maximums</span></span>
<span data-ttu-id="fb952-107">Azure MySQL-Database heeft meerdere Servicelagen die u kiezen kunt uit bij het maken van een server.</span><span class="sxs-lookup"><span data-stu-id="fb952-107">Azure Database for MySQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="fb952-108">Zie voor meer informatie [begrijpen wat er beschikbaar is in elke servicelaag](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="fb952-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="fb952-109">Er is een maximum aantal verbindingen, compute-eenheden en opslag in elke servicelaag tijdens de preview service als volgt:</span><span class="sxs-lookup"><span data-stu-id="fb952-109">There is a maximum number of connections, compute units, and storage in each service tier during the service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="fb952-110">**Maximum aantal verbindingen**</span><span class="sxs-lookup"><span data-stu-id="fb952-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="fb952-111">Basic 50 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="fb952-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="fb952-112">50-verbindingen</span><span class="sxs-lookup"><span data-stu-id="fb952-112">50 connections</span></span>    |
| <span data-ttu-id="fb952-113">Basic 100 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="fb952-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="fb952-114">100-verbindingen</span><span class="sxs-lookup"><span data-stu-id="fb952-114">100 connections</span></span>   |
| <span data-ttu-id="fb952-115">Standaard 100 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="fb952-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="fb952-116">200-verbindingen</span><span class="sxs-lookup"><span data-stu-id="fb952-116">200 connections</span></span>   |
| <span data-ttu-id="fb952-117">Standaard 200 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="fb952-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="fb952-118">300-verbindingen</span><span class="sxs-lookup"><span data-stu-id="fb952-118">300 connections</span></span>   |
| <span data-ttu-id="fb952-119">Standaard 400 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="fb952-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="fb952-120">400-verbindingen</span><span class="sxs-lookup"><span data-stu-id="fb952-120">400 connections</span></span>   |
| <span data-ttu-id="fb952-121">Standaard 800 Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="fb952-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="fb952-122">500-verbindingen</span><span class="sxs-lookup"><span data-stu-id="fb952-122">500 connections</span></span>   |
| <span data-ttu-id="fb952-123">**Maximale Compute-eenheden**</span><span class="sxs-lookup"><span data-stu-id="fb952-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="fb952-124">Basisservicelaag</span><span class="sxs-lookup"><span data-stu-id="fb952-124">Basic service tier</span></span>         | <span data-ttu-id="fb952-125">100 compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="fb952-125">100 Compute Units</span></span> |
| <span data-ttu-id="fb952-126">Standaardservicelaag</span><span class="sxs-lookup"><span data-stu-id="fb952-126">Standard service tier</span></span>      | <span data-ttu-id="fb952-127">800 compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="fb952-127">800 Compute Units</span></span> |
| <span data-ttu-id="fb952-128">**Maximale opslag**</span><span class="sxs-lookup"><span data-stu-id="fb952-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="fb952-129">Basisservicelaag</span><span class="sxs-lookup"><span data-stu-id="fb952-129">Basic service tier</span></span>         | <span data-ttu-id="fb952-130">1 TB</span><span class="sxs-lookup"><span data-stu-id="fb952-130">1 TB</span></span>              |
| <span data-ttu-id="fb952-131">Standaardservicelaag</span><span class="sxs-lookup"><span data-stu-id="fb952-131">Standard service tier</span></span>      | <span data-ttu-id="fb952-132">1 TB</span><span class="sxs-lookup"><span data-stu-id="fb952-132">1 TB</span></span>              |

<span data-ttu-id="fb952-133">Wanneer er te veel verbindingen zijn bereikt, wordt de volgende fout:</span><span class="sxs-lookup"><span data-stu-id="fb952-133">When too many connections are reached, you may receive the following error:</span></span>
> <span data-ttu-id="fb952-134">FOUT (08004) 1040: Te veel verbindingen</span><span class="sxs-lookup"><span data-stu-id="fb952-134">ERROR 1040 (08004): Too many connections</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="fb952-135">Preview functionele beperkingen:</span><span class="sxs-lookup"><span data-stu-id="fb952-135">Preview functional limitations:</span></span>
### <a name="scale-operations"></a><span data-ttu-id="fb952-136">Schaalbewerkingen:</span><span class="sxs-lookup"><span data-stu-id="fb952-136">Scale operations:</span></span>
1.  <span data-ttu-id="fb952-137">Dynamische schaalbaarheid van servers in Servicelagen is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="fb952-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="fb952-138">Dat wil zeggen, schakelen tussen servicecategorieën Basic en Standard.</span><span class="sxs-lookup"><span data-stu-id="fb952-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="fb952-139">Dynamische toename mogelijk op aanvraag van opslag op vooraf gemaakte server is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="fb952-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="fb952-140">Verkleinen storage server wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="fb952-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="fb952-141">Versie-upgrades voor server:</span><span class="sxs-lookup"><span data-stu-id="fb952-141">Server version upgrades:</span></span>
- <span data-ttu-id="fb952-142">Automatische migratie tussen versies van de primaire database-engine is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="fb952-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="fb952-143">Beheer van abonnementen:</span><span class="sxs-lookup"><span data-stu-id="fb952-143">Subscription management:</span></span>
- <span data-ttu-id="fb952-144">Dynamisch vooraf gemaakte servers verplaatsen tussen abonnement en resourcegroep is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="fb952-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="fb952-145">Punt-in-time-terugzetten:</span><span class="sxs-lookup"><span data-stu-id="fb952-145">Point-in-time-restore:</span></span>
1.  <span data-ttu-id="fb952-146">Herstellen naar andere servicelaag en/of Compute-eenheden en de opslaggrootte is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="fb952-146">Restoring to different service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="fb952-147">Herstellen van een uitgevallen server wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="fb952-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb952-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb952-148">Next Steps:</span></span>
<span data-ttu-id="fb952-149">[Wat is beschikbaar in elke servicelaag](concepts-service-tiers.md)
[MySQL-Database-versies ondersteund](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="fb952-149">[What’s available in each service tier](concepts-service-tiers.md)
[Supported MySQL Database Versions](concepts-supported-versions.md)</span></span>
