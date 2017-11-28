---
title: adressen van de beheerserver aaaAzure App Service-omgeving
description: Adressen van de lijsten Hallo beheerserver gebruikt toocommand een App-serviceomgeving
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="e6828-103">Adressen van de beheerserver App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="e6828-103">App Service Environment management addresses</span></span>

<span data-ttu-id="e6828-104">Hallo-App Service Environment(ASE) is een implementatie van hello Azure App Service in een subnet in uw Azure Virtual Network (VNet).</span><span class="sxs-lookup"><span data-stu-id="e6828-104">hello App Service Environment(ASE) is a deployment of hello Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="e6828-105">Hallo as-omgeving moet toegankelijk is vanaf hello Azure App Service, zodat deze kan worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="e6828-105">hello ASE must be accessible from hello Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="e6828-106">Deze as-omgeving beheer van verkeer passeert Hallo gebruiker beheerd netwerk.</span><span class="sxs-lookup"><span data-stu-id="e6828-106">This ASE management traffic traverses hello user controlled network.</span></span>  <span data-ttu-id="e6828-107">Het is afkomstig uit Azure App Service management servers toohello openbare VIP die is gekoppeld aan het Hallo-as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="e6828-107">It comes from Azure App Service management servers toohello public VIP that is associated with hello ASE.</span></span>  <span data-ttu-id="e6828-108">Voor meer informatie over Hallo as-omgeving networking afhankelijkheden lezen [-overwegingen en Hallo App Service-omgeving][networking].</span><span class="sxs-lookup"><span data-stu-id="e6828-108">For details on hello ASE networking dependencies read [Networking considerations and hello App Service Environment][networking].</span></span>  <span data-ttu-id="e6828-109">Voor algemene informatie over het Hallo-as-omgeving kunt u beginnen met [inleiding toohello App Service-omgeving][intro].</span><span class="sxs-lookup"><span data-stu-id="e6828-109">For general information on hello ASE you can start with [Introduction toohello App Service Environment][intro].</span></span>

<span data-ttu-id="e6828-110">Dit document worden Hallo bron, IP-adressen voor beheer van verkeer toohello as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="e6828-110">This document lists hello source IPs for management traffic toohello ASE.</span></span> <span data-ttu-id="e6828-111">U kunt deze adressen toocreate Netwerkbeveiligingsgroepen toolock omlaag binnenkomend verkeer gebruiken of in routetabellen gebruiken, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="e6828-111">You can use these addresses toocreate Network Security Groups toolock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="e6828-112">toouse deze informatie moet u toouse:</span><span class="sxs-lookup"><span data-stu-id="e6828-112">toouse this information you need toouse:</span></span>

* <span data-ttu-id="e6828-113">Hallo IP-adressen die worden vermeld voor alle regio 's</span><span class="sxs-lookup"><span data-stu-id="e6828-113">hello IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="e6828-114">Hallo IP-adressen die overeenkomen toohello regio die uw as-omgeving is geïmplementeerd in.</span><span class="sxs-lookup"><span data-stu-id="e6828-114">hello IP addresses that match toohello region that your ASE is deployed into.</span></span>

<span data-ttu-id="e6828-115">Hallo binnenkomende beheer van verkeer binnenkomt van deze IP-adressen tooports 454 en 455.</span><span class="sxs-lookup"><span data-stu-id="e6828-115">hello incoming management traffic comes in from these IP addresses tooports 454 and 455.</span></span>

| <span data-ttu-id="e6828-116">Regio</span><span class="sxs-lookup"><span data-stu-id="e6828-116">Region</span></span> | <span data-ttu-id="e6828-117">Adressen</span><span class="sxs-lookup"><span data-stu-id="e6828-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="e6828-118">Alle regio 's</span><span class="sxs-lookup"><span data-stu-id="e6828-118">All regions</span></span> | <span data-ttu-id="e6828-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="e6828-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="e6828-120">Zuid-centraal VS & Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="e6828-120">South Central US & North Central US</span></span> | <span data-ttu-id="e6828-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="e6828-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="e6828-122">Australië-Zuidoost & Australië Oost</span><span class="sxs-lookup"><span data-stu-id="e6828-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="e6828-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="e6828-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="e6828-124">VS West & VS Oost</span><span class="sxs-lookup"><span data-stu-id="e6828-124">US West & US East</span></span> | <span data-ttu-id="e6828-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="e6828-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="e6828-126">West-Europa & Noord-Europa</span><span class="sxs-lookup"><span data-stu-id="e6828-126">West Europe & North Europe</span></span> | <span data-ttu-id="e6828-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="e6828-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="e6828-128">West-Centraal VS & VS-West 2</span><span class="sxs-lookup"><span data-stu-id="e6828-128">West Central US & West US 2</span></span> | <span data-ttu-id="e6828-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="e6828-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="e6828-130">VS-midden & VS-Oost 2</span><span class="sxs-lookup"><span data-stu-id="e6828-130">Central US & East US 2</span></span> | <span data-ttu-id="e6828-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="e6828-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="e6828-132">Oost-Azië & Zuidoost-Azië</span><span class="sxs-lookup"><span data-stu-id="e6828-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="e6828-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="e6828-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="e6828-134">Japan-Oost & Japan-West</span><span class="sxs-lookup"><span data-stu-id="e6828-134">Japan East & Japan West</span></span> | <span data-ttu-id="e6828-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="e6828-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="e6828-136">Canada-midden & Canada Oost</span><span class="sxs-lookup"><span data-stu-id="e6828-136">Canada Central & Canada East</span></span> | <span data-ttu-id="e6828-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="e6828-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="e6828-138">VK West & VK Zuid</span><span class="sxs-lookup"><span data-stu-id="e6828-138">UK West & UK South</span></span> | <span data-ttu-id="e6828-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="e6828-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="e6828-140">Zuid-Korea & Korea-centraal</span><span class="sxs-lookup"><span data-stu-id="e6828-140">Korea South & Korea Central</span></span> | <span data-ttu-id="e6828-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="e6828-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="e6828-142">Brazilië-Zuid & Zuid-centraal VS</span><span class="sxs-lookup"><span data-stu-id="e6828-142">Brazil South & South Central US</span></span>| <span data-ttu-id="e6828-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="e6828-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="e6828-144">Centrale India en India Zuid</span><span class="sxs-lookup"><span data-stu-id="e6828-144">Central India & South India</span></span> | <span data-ttu-id="e6828-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="e6828-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="e6828-146">West, India en India Zuid</span><span class="sxs-lookup"><span data-stu-id="e6828-146">West India & South India</span></span> | <span data-ttu-id="e6828-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="e6828-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
