---
title: aaaSecure uw Internet der dingen (IoT) in Azure | Microsoft Docs
description: " Azure internet der dingen (IoT)-services bieden een breed scala aan mogelijkheden. In dit artikel helpt u begrijpen hoe toosecure uw IoT-oplossingen in Azure. "
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
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="dd6bf-104">Overzicht van Internet of Things-beveiliging</span><span class="sxs-lookup"><span data-stu-id="dd6bf-104">Internet of Things security overview</span></span>
<span data-ttu-id="dd6bf-105">Azure internet der dingen (IoT)-services bieden een breed scala aan mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="dd6bf-106">Met deze hoogwaardige services kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="dd6bf-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="dd6bf-107">Gegevens van apparaten verzamelen</span><span class="sxs-lookup"><span data-stu-id="dd6bf-107">Collect data from devices</span></span>
* <span data-ttu-id="dd6bf-108">Gegevensstromen in beweging analyseren</span><span class="sxs-lookup"><span data-stu-id="dd6bf-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="dd6bf-109">Grote gegevenssets opslaan en er query’s op uitvoeren</span><span class="sxs-lookup"><span data-stu-id="dd6bf-109">Store and query large data sets</span></span>
* <span data-ttu-id="dd6bf-110">Gegevens in realtime en historische gegevens visualiseren</span><span class="sxs-lookup"><span data-stu-id="dd6bf-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="dd6bf-111">Integraties met back-officesystemen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="dd6bf-111">Integrate with back-office systems</span></span>

<span data-ttu-id="dd6bf-112">toodeliver deze mogelijkheden kunnen Azure IoT Suite-pakketten meerdere Azure services met aangepaste extensies als vooraf geconfigureerde oplossingen.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="dd6bf-113">Deze vooraf geconfigureerde oplossingen zijn basisimplementaties van algemene patronen van IoT-oplossing waarmee tooreduce Hallo u tijd toodeliver uw IoT-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="dd6bf-114">Hallo IoT-SDK's gebruikt, kunt u aanpassen en uitbreiden van deze oplossingen toomeet uw eigen vereisten.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-114">Using hello IoT software development kits, you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="dd6bf-115">U kunt deze oplossingen gebruiken als voorbeelden of sjablonen als u nieuwe IoT-oplossingen ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="dd6bf-116">Hello Azure IoT suite is een krachtige oplossing voor uw IoT-behoeften.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-116">hello Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="dd6bf-117">Het is echter van upmost belang dat uw IoT-oplossingen zijn ontworpen met beveiligd zijn van Hallo starten.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from hello start.</span></span> <span data-ttu-id="dd6bf-118">Alle beveiligingsincidenten vanwege het grote aantal Hallo van IoT-apparaten, kan snel een wijdverbreid gebeurtenis met grote gevolgen worden.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-118">Because of hello sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="dd6bf-119">toohelp u begrijpt hoe toosecure uw IoT-oplossingen hebben we Hallo informatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-119">toohelp you understand how toosecure your IoT solutions, we have hello following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="dd6bf-120">Beveiligingsarchitectuur</span><span class="sxs-lookup"><span data-stu-id="dd6bf-120">Security architecture</span></span>
<span data-ttu-id="dd6bf-121">Bij het ontwerpen van een systeem is belangrijk toounderstand Hallo mogelijke bedreigingen toothat systeem en dienovereenkomstig juiste beveiliging niet toevoegen als Hallo system is ontworpen en ontworpen.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-121">When designing a system, it is important toounderstand hello potential threats toothat system, and add appropriate defenses accordingly, as hello system is designed and architected.</span></span> <span data-ttu-id="dd6bf-122">Het is belangrijk toodesign Hallo product van Hallo begin rekening met beveiliging omdat informatie over hoe een hacker mogelijk kunnen toocompromise een systeem zorgt ervoor geschikt oplossingen zijn in plaats van Hallo begin.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-122">It is important toodesign hello product from hello start with security in mind because understanding how an attacker might be able toocompromise a system helps make sure appropriate mitigations are in place from hello beginning.</span></span>

<span data-ttu-id="dd6bf-123">U kunt meer informatie over IoT-beveiligingsarchitectuur door te lezen [Internet van dingen beveiligingsarchitectuur](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="dd6bf-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="dd6bf-124">Dit artikel worden de volgende onderwerpen Hallo:</span><span class="sxs-lookup"><span data-stu-id="dd6bf-124">This article discusses hello following topics:</span></span>

* [<span data-ttu-id="dd6bf-125">Beveiliging begint met een risicomodel</span><span class="sxs-lookup"><span data-stu-id="dd6bf-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="dd6bf-126">Beveiliging in IoT</span><span class="sxs-lookup"><span data-stu-id="dd6bf-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="dd6bf-127">Threat modellering hello Azure IoT Reference Architecture</span><span class="sxs-lookup"><span data-stu-id="dd6bf-127">Threat Modeling hello Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a><span data-ttu-id="dd6bf-128">Beveiliging van Hallo gemalen</span><span class="sxs-lookup"><span data-stu-id="dd6bf-128">Security from hello ground up</span></span>
<span data-ttu-id="dd6bf-129">Hallo IoT vormt unieke beveiliging, privacy en naleving uitdagingen toobusinesses overal ter wereld.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-129">hello IoT poses unique security, privacy, and compliance challenges toobusinesses worldwide.</span></span> <span data-ttu-id="dd6bf-130">In tegenstelling tot traditionele cyberbeveiliging technologie waar deze problemen gebaseerd op software- en hoe deze wordt geïmplementeerd, IoT heeft betrekking op wat er gebeurt wanneer Hallo cyberbeveiliging en Hallo fysieke werelden convergeren.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when hello cyber and hello physical worlds converge.</span></span> <span data-ttu-id="dd6bf-131">Beveiligen van IoT-oplossingen vereist gezorgd beveiligde inrichting van de apparaten, beveiligde verbindingen tussen deze apparaten en het Hallo cloud en de beveiliging van de beveiligde gegevens in de cloud Hallo tijdens de verwerking en opslag.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and hello cloud, and secure data protection in hello cloud during processing and storage.</span></span> <span data-ttu-id="dd6bf-132">Werken met dergelijke functionaliteit, zijn echter resource beperkte apparaten, geografische verdeling van implementaties en veel apparaten binnen een oplossing.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="dd6bf-133">U leert hoe beveiliging toohandle in de volgende gebieden door te lezen [beveiliging van Internet der dingen van Hallo gemalen](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="dd6bf-133">You can learn how toohandle security in these areas by reading [Internet of Things security from hello ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="dd6bf-134">Hallo aan de orde Hallo volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="dd6bf-134">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="dd6bf-135">Infrastructuur niet vanuit Hallo gemalen beveiligen</span><span class="sxs-lookup"><span data-stu-id="dd6bf-135">Secure infrastructure from hello ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="dd6bf-136">Microsoft Azure: beveiligde IoT-infrastructuur voor uw bedrijf</span><span class="sxs-lookup"><span data-stu-id="dd6bf-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="dd6bf-137">Beste praktijken</span><span class="sxs-lookup"><span data-stu-id="dd6bf-137">Best Practices</span></span>
<span data-ttu-id="dd6bf-138">Een IoT-infrastructuur beveiligen vereist een strengere beveiliging-in-depth-strategie.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="dd6bf-139">Van de beveiliging van gegevens in de cloud hello, integriteit van gegevens beveiligt terwijl overdracht in Hallo builds openbare internet, toosecurely inrichting apparaten, elke laag groter beveiligingscontrole Hallo algehele infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="dd6bf-139">From securing data in hello cloud, protecting data integrity while in transit over hello public internet, toosecurely provisioning devices, each layer builds greater security assurance in hello overall infrastructure.</span></span>

<span data-ttu-id="dd6bf-140">U kunt meer informatie over beveiliging van Internet der dingen aanbevolen procedures door te lezen [aanbevolen beveiligingsprocedures voor Internet der dingen](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="dd6bf-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="dd6bf-141">Hallo aan de orde Hallo volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="dd6bf-141">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="dd6bf-142">IoT hardware fabrikant/integrator</span><span class="sxs-lookup"><span data-stu-id="dd6bf-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="dd6bf-143">Ontwikkelaars van IoT-oplossing</span><span class="sxs-lookup"><span data-stu-id="dd6bf-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="dd6bf-144">Implementatie van IoT-oplossing</span><span class="sxs-lookup"><span data-stu-id="dd6bf-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="dd6bf-145">IoT-oplossing operator</span><span class="sxs-lookup"><span data-stu-id="dd6bf-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
