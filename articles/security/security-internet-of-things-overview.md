---
title: Beveiligen van uw Internet der dingen (IoT) in Azure | Microsoft Docs
description: " Azure internet der dingen (IoT)-services bieden een breed scala aan mogelijkheden. In dit artikel helpt u begrijpen hoe voor het beveiligen van uw IoT-oplossingen in Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 3793f5453b74b6c06d9e58b426d89099298e1288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="11937-104">Overzicht van Internet of Things-beveiliging</span><span class="sxs-lookup"><span data-stu-id="11937-104">Internet of Things security overview</span></span>
<span data-ttu-id="11937-105">Azure internet der dingen (IoT)-services bieden een breed scala aan mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="11937-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="11937-106">Met deze hoogwaardige services kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="11937-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="11937-107">Gegevens van apparaten verzamelen</span><span class="sxs-lookup"><span data-stu-id="11937-107">Collect data from devices</span></span>
* <span data-ttu-id="11937-108">Gegevensstromen in beweging analyseren</span><span class="sxs-lookup"><span data-stu-id="11937-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="11937-109">Grote gegevenssets opslaan en er query’s op uitvoeren</span><span class="sxs-lookup"><span data-stu-id="11937-109">Store and query large data sets</span></span>
* <span data-ttu-id="11937-110">Gegevens in realtime en historische gegevens visualiseren</span><span class="sxs-lookup"><span data-stu-id="11937-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="11937-111">Integraties met back-officesystemen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="11937-111">Integrate with back-office systems</span></span>

<span data-ttu-id="11937-112">Voor deze mogelijkheden, Azure IoT Suite-pakketten samen meerdere Azure-services met aangepaste extensies als vooraf geconfigureerde oplossingen.</span><span class="sxs-lookup"><span data-stu-id="11937-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="11937-113">Deze vooraf geconfigureerde oplossingen zijn basisimplementaties van algemene patronen van IoT-oplossingen die u helpen de tijd voor het leveren van uw IoT-oplossingen te verkorten.</span><span class="sxs-lookup"><span data-stu-id="11937-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="11937-114">Met behulp van de IoT-SDK's, kunt u aanpassen en uitbreiden van deze oplossingen om te voldoen aan uw eigen vereisten.</span><span class="sxs-lookup"><span data-stu-id="11937-114">Using the IoT software development kits, you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="11937-115">U kunt deze oplossingen gebruiken als voorbeelden of sjablonen als u nieuwe IoT-oplossingen ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="11937-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="11937-116">De Azure IoT suite is een krachtige oplossing voor uw IoT-behoeften.</span><span class="sxs-lookup"><span data-stu-id="11937-116">The Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="11937-117">Het is echter van upmost belang dat uw IoT-oplossingen zijn ontworpen met beveiligd zijn vanaf het begin.</span><span class="sxs-lookup"><span data-stu-id="11937-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from the start.</span></span> <span data-ttu-id="11937-118">Alle beveiligingsincidenten vanwege het grote aantal IoT-apparaten, kan snel een wijdverbreid gebeurtenis met grote gevolgen worden.</span><span class="sxs-lookup"><span data-stu-id="11937-118">Because of the sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="11937-119">We hebben de volgende informatie om te begrijpen hoe u voor het beveiligen van uw IoT-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="11937-119">To help you understand how to secure your IoT solutions, we have the following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="11937-120">Beveiligingsarchitectuur</span><span class="sxs-lookup"><span data-stu-id="11937-120">Security architecture</span></span>
<span data-ttu-id="11937-121">Bij het ontwerpen van een systeem, is het belangrijk om te begrijpen van de mogelijke bedreigingen tot dat systeem en dienovereenkomstig juiste beveiliging niet toevoegen als het systeem is ontworpen en ontworpen.</span><span class="sxs-lookup"><span data-stu-id="11937-121">When designing a system, it is important to understand the potential threats to that system, and add appropriate defenses accordingly, as the system is designed and architected.</span></span> <span data-ttu-id="11937-122">Het is belangrijk voor het ontwerpen van het product vanaf het begin rekening met beveiliging omdat informatie over hoe een aanvaller mogelijk een systeem kunt u ervoor dat de juiste oplossingen in plaats vanaf het begin.</span><span class="sxs-lookup"><span data-stu-id="11937-122">It is important to design the product from the start with security in mind because understanding how an attacker might be able to compromise a system helps make sure appropriate mitigations are in place from the beginning.</span></span>

<span data-ttu-id="11937-123">U kunt meer informatie over IoT-beveiligingsarchitectuur door te lezen [Internet van dingen beveiligingsarchitectuur](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="11937-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="11937-124">Dit artikel wordt beschreven in de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="11937-124">This article discusses the following topics:</span></span>

* [<span data-ttu-id="11937-125">Beveiliging begint met een risicomodel</span><span class="sxs-lookup"><span data-stu-id="11937-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="11937-126">Beveiliging in IoT</span><span class="sxs-lookup"><span data-stu-id="11937-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="11937-127">Threat Modeling de naslaginformatie over Azure IoT-architectuur</span><span class="sxs-lookup"><span data-stu-id="11937-127">Threat Modeling the Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-the-ground-up"></a><span data-ttu-id="11937-128">Fundamentele beveiliging</span><span class="sxs-lookup"><span data-stu-id="11937-128">Security from the ground up</span></span>
<span data-ttu-id="11937-129">De IoT vormt unieke beveiliging, privacy en naleving uitdagingen voor bedrijven overal ter wereld.</span><span class="sxs-lookup"><span data-stu-id="11937-129">The IoT poses unique security, privacy, and compliance challenges to businesses worldwide.</span></span> <span data-ttu-id="11937-130">In tegenstelling tot traditionele cyberbeveiliging technologie waar deze problemen gebaseerd op software- en hoe deze wordt geïmplementeerd, IoT heeft betrekking op wat er gebeurt wanneer de cyberbeveiliging en de fysieke werelden convergeren.</span><span class="sxs-lookup"><span data-stu-id="11937-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when the cyber and the physical worlds converge.</span></span> <span data-ttu-id="11937-131">Beveiligen van IoT-oplossingen vereist gezorgd beveiligde inrichting van de apparaten, beveiligde verbindingen tussen deze apparaten en de cloud en de bescherming van de beveiligde gegevens in de cloud tijdens verwerking en opslag.</span><span class="sxs-lookup"><span data-stu-id="11937-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and the cloud, and secure data protection in the cloud during processing and storage.</span></span> <span data-ttu-id="11937-132">Werken met dergelijke functionaliteit, zijn echter resource beperkte apparaten, geografische verdeling van implementaties en veel apparaten binnen een oplossing.</span><span class="sxs-lookup"><span data-stu-id="11937-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="11937-133">U leert hoe beveiliging in de volgende gebieden verwerkt door te lezen [beveiliging van Internet der dingen van een compleet nieuwe](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="11937-133">You can learn how to handle security in these areas by reading [Internet of Things security from the ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="11937-134">Het artikel worden de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="11937-134">The article discusses the following topics:</span></span>

* [<span data-ttu-id="11937-135">Beveiligde infrastructuur niet vanuit een compleet nieuwe</span><span class="sxs-lookup"><span data-stu-id="11937-135">Secure infrastructure from the ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="11937-136">Microsoft Azure: beveiligde IoT-infrastructuur voor uw bedrijf</span><span class="sxs-lookup"><span data-stu-id="11937-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="11937-137">Beste praktijken</span><span class="sxs-lookup"><span data-stu-id="11937-137">Best Practices</span></span>
<span data-ttu-id="11937-138">Een IoT-infrastructuur beveiligen vereist een strengere beveiliging-in-depth-strategie.</span><span class="sxs-lookup"><span data-stu-id="11937-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="11937-139">Elke laag is gebaseerd, is groter beveiligingscontrole in de algehele infrastructuur van de beveiliging van gegevens in de cloud, de integriteit van de gegevens onderweg te beschermen via het openbare internet, voor het inrichten van apparaten, veilig.</span><span class="sxs-lookup"><span data-stu-id="11937-139">From securing data in the cloud, protecting data integrity while in transit over the public internet, to securely provisioning devices, each layer builds greater security assurance in the overall infrastructure.</span></span>

<span data-ttu-id="11937-140">U kunt meer informatie over beveiliging van Internet der dingen aanbevolen procedures door te lezen [aanbevolen beveiligingsprocedures voor Internet der dingen](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="11937-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="11937-141">Het artikel worden de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="11937-141">The article discusses the following topics:</span></span>

* [<span data-ttu-id="11937-142">IoT hardware fabrikant/integrator</span><span class="sxs-lookup"><span data-stu-id="11937-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="11937-143">Ontwikkelaars van IoT-oplossing</span><span class="sxs-lookup"><span data-stu-id="11937-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="11937-144">Implementatie van IoT-oplossing</span><span class="sxs-lookup"><span data-stu-id="11937-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="11937-145">IoT-oplossing operator</span><span class="sxs-lookup"><span data-stu-id="11937-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
