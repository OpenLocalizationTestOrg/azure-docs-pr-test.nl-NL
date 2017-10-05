---
title: Adressen van de beheerserver Azure App Service-omgeving
description: Geeft een lijst van de adressen van de beheerserver gebruikt voor de opdracht van een App-serviceomgeving
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
ms.openlocfilehash: e97a084772fd16252d925b62498d2e696629a25d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="46774-103">Adressen van de beheerserver App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="46774-103">App Service Environment management addresses</span></span>

<span data-ttu-id="46774-104">De App Service-Environment(ASE) is een implementatie van de Azure App Service in een subnet in uw Azure Virtual Network (VNet).</span><span class="sxs-lookup"><span data-stu-id="46774-104">The App Service Environment(ASE) is a deployment of the Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="46774-105">De as-omgeving moet toegankelijk is vanaf de Azure App Service, zodat deze kan worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="46774-105">The ASE must be accessible from the Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="46774-106">Deze as-omgeving beheer van verkeer over de gebruiker beheerde netwerk wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="46774-106">This ASE management traffic traverses the user controlled network.</span></span>  <span data-ttu-id="46774-107">Ze afkomstig zijn van Azure App Service-beheerservers naar het openbare VIP die is gekoppeld aan het as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="46774-107">It comes from Azure App Service management servers to the public VIP that is associated with the ASE.</span></span>  <span data-ttu-id="46774-108">Voor meer informatie over de as-omgeving networking afhankelijkheden lezen [-overwegingen en de App-serviceomgeving][networking].</span><span class="sxs-lookup"><span data-stu-id="46774-108">For details on the ASE networking dependencies read [Networking considerations and the App Service Environment][networking].</span></span>  <span data-ttu-id="46774-109">Voor algemene informatie over de as-omgeving kunt u beginnen met [Inleiding tot de App-serviceomgeving][intro].</span><span class="sxs-lookup"><span data-stu-id="46774-109">For general information on the ASE you can start with [Introduction to the App Service Environment][intro].</span></span>

<span data-ttu-id="46774-110">Dit document worden de bron-IP-adressen voor beheer van verkeer naar de as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="46774-110">This document lists the source IPs for management traffic to the ASE.</span></span> <span data-ttu-id="46774-111">U kunt deze adressen gebruiken voor het maken van Netwerkbeveiligingsgroepen voor binnenkomend verkeer vergrendelen of ze in routetabellen gebruiken indien nodig.</span><span class="sxs-lookup"><span data-stu-id="46774-111">You can use these addresses to create Network Security Groups to lock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="46774-112">U moet gebruiken voor het gebruik van deze informatie:</span><span class="sxs-lookup"><span data-stu-id="46774-112">To use this information you need to use:</span></span>

* <span data-ttu-id="46774-113">de IP-adressen die worden vermeld voor alle regio 's</span><span class="sxs-lookup"><span data-stu-id="46774-113">the IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="46774-114">de IP-adressen die met de regio die overeenkomen in uw as-omgeving is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="46774-114">the IP addresses that match to the region that your ASE is deployed into.</span></span>

<span data-ttu-id="46774-115">Het binnenkomende beheerverkeer afkomstig zijn deze IP-adressen via poorten 454 en 455.</span><span class="sxs-lookup"><span data-stu-id="46774-115">The incoming management traffic comes in from these IP addresses to ports 454 and 455.</span></span>

| <span data-ttu-id="46774-116">Regio</span><span class="sxs-lookup"><span data-stu-id="46774-116">Region</span></span> | <span data-ttu-id="46774-117">Adressen</span><span class="sxs-lookup"><span data-stu-id="46774-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="46774-118">Alle regio 's</span><span class="sxs-lookup"><span data-stu-id="46774-118">All regions</span></span> | <span data-ttu-id="46774-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="46774-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="46774-120">Zuid-centraal VS & Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="46774-120">South Central US & North Central US</span></span> | <span data-ttu-id="46774-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="46774-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="46774-122">Australië-Zuidoost & Australië Oost</span><span class="sxs-lookup"><span data-stu-id="46774-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="46774-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="46774-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="46774-124">VS West & VS Oost</span><span class="sxs-lookup"><span data-stu-id="46774-124">US West & US East</span></span> | <span data-ttu-id="46774-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="46774-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="46774-126">West-Europa & Noord-Europa</span><span class="sxs-lookup"><span data-stu-id="46774-126">West Europe & North Europe</span></span> | <span data-ttu-id="46774-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="46774-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="46774-128">West-Centraal VS & VS-West 2</span><span class="sxs-lookup"><span data-stu-id="46774-128">West Central US & West US 2</span></span> | <span data-ttu-id="46774-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="46774-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="46774-130">VS-midden & VS-Oost 2</span><span class="sxs-lookup"><span data-stu-id="46774-130">Central US & East US 2</span></span> | <span data-ttu-id="46774-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="46774-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="46774-132">Oost-Azië & Zuidoost-Azië</span><span class="sxs-lookup"><span data-stu-id="46774-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="46774-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="46774-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="46774-134">Japan-Oost & Japan-West</span><span class="sxs-lookup"><span data-stu-id="46774-134">Japan East & Japan West</span></span> | <span data-ttu-id="46774-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="46774-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="46774-136">Canada-midden & Canada Oost</span><span class="sxs-lookup"><span data-stu-id="46774-136">Canada Central & Canada East</span></span> | <span data-ttu-id="46774-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="46774-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="46774-138">VK West & VK Zuid</span><span class="sxs-lookup"><span data-stu-id="46774-138">UK West & UK South</span></span> | <span data-ttu-id="46774-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="46774-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="46774-140">Zuid-Korea & Korea-centraal</span><span class="sxs-lookup"><span data-stu-id="46774-140">Korea South & Korea Central</span></span> | <span data-ttu-id="46774-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="46774-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="46774-142">Brazilië-Zuid & Zuid-centraal VS</span><span class="sxs-lookup"><span data-stu-id="46774-142">Brazil South & South Central US</span></span>| <span data-ttu-id="46774-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="46774-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="46774-144">Centrale India en India Zuid</span><span class="sxs-lookup"><span data-stu-id="46774-144">Central India & South India</span></span> | <span data-ttu-id="46774-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="46774-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="46774-146">West, India en India Zuid</span><span class="sxs-lookup"><span data-stu-id="46774-146">West India & South India</span></span> | <span data-ttu-id="46774-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="46774-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
