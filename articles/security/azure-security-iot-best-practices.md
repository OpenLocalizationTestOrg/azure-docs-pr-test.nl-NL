---
title: aaaInternet van aanbevolen beveiligingsprocedures voor dingen | Microsoft Docs
description: Hallo artikel bevat een samengestelde lijst met Microsoft Internet van dingen Best Practices voor beveiliging en algemene aanbevelingen.
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="841cf-103">Internet der dingen Best Practices voor beveiliging</span><span class="sxs-lookup"><span data-stu-id="841cf-103">Internet of Things Security Best Practices</span></span>
<span data-ttu-id="841cf-104">Beveiligen Hallo Internet der dingen (IoT)-infrastructuur is een kritieke onderneming voor iedereen die betrokken zijn bij IoT-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="841cf-104">Securing hello Internet of Things (IoT) infrastructure is a critical undertaking for anyone involved with IoT solutions.</span></span> <span data-ttu-id="841cf-105">Vanwege het aantal apparaten bij betrokken zijn hello en Hallo verwante gedistribueerde aard van deze apparaten, Hallo impact een beveiligingsgebeurtenis toocompromise miljoenen IoT-apparaten is niet-triviale en wijdverbreid invloed kan hebben.</span><span class="sxs-lookup"><span data-stu-id="841cf-105">Because of hello number of devices involved and hello distributed nature of these devices, hello impact a security event related toocompromise of millions of IoT devices is non-trivial and can have widespread impact.</span></span>

<span data-ttu-id="841cf-106">IoT-beveiliging moet daarom een security-in-depth-benadering.</span><span class="sxs-lookup"><span data-stu-id="841cf-106">For this reason, IoT security needs a security-in-depth approach.</span></span> <span data-ttu-id="841cf-107">Gegevens behoeften toobe beveiligd in cloud Hallo en die worden verplaatst via persoonlijke en openbare netwerken.</span><span class="sxs-lookup"><span data-stu-id="841cf-107">Data needs toobe secure in hello cloud and as it moves over private and public networks.</span></span> <span data-ttu-id="841cf-108">Methoden moeten toobe in place toosecurely inrichten Hallo IoT-apparaten zelf.</span><span class="sxs-lookup"><span data-stu-id="841cf-108">Methods need toobe in place toosecurely provision hello IoT devices themselves.</span></span> <span data-ttu-id="841cf-109">Elke laag van het apparaat, toonetwork, toocloud back-end moet sterke beveiliging garantie.</span><span class="sxs-lookup"><span data-stu-id="841cf-109">Each layer, from device, toonetwork, toocloud back-end needs strong security assurances.</span></span>

<span data-ttu-id="841cf-110">Aanbevolen procedures van IoT kunnen worden ingedeeld in de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="841cf-110">IoT best practices can be categorized in hello following way:</span></span>

* <span data-ttu-id="841cf-111">IoT-hardwarefabrikant of integrator</span><span class="sxs-lookup"><span data-stu-id="841cf-111">IoT hardware manufacturer or integrator</span></span>
* <span data-ttu-id="841cf-112">Ontwikkelaars van IoT-oplossing</span><span class="sxs-lookup"><span data-stu-id="841cf-112">IoT solution developer</span></span>
* <span data-ttu-id="841cf-113">Implementatie van IoT-oplossing</span><span class="sxs-lookup"><span data-stu-id="841cf-113">IoT solution deployer</span></span>
* <span data-ttu-id="841cf-114">IoT-oplossing operator</span><span class="sxs-lookup"><span data-stu-id="841cf-114">IoT solution operator</span></span>

<span data-ttu-id="841cf-115">In dit artikel bevat een overzicht van [Internet van dingen aanbevolen beveiligingsprocedures](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="841cf-115">This article summarizes [Internet of Things Security Best Practices](../iot-suite/iot-security-best-practices.md).</span></span> <span data-ttu-id="841cf-116">Raadpleeg toothat artikel voor meer gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="841cf-116">Please refer toothat article for more detailed information.</span></span>

## <a name="iot-hardware-manufacturer-or-integrator"></a><span data-ttu-id="841cf-117">IoT-hardwarefabrikant of integrator</span><span class="sxs-lookup"><span data-stu-id="841cf-117">IoT hardware manufacturer or integrator</span></span>
<span data-ttu-id="841cf-118">Volg de aanbevolen procedures Hallo hieronder als u een hardwarefabrikant IoT of een integrator hardware:</span><span class="sxs-lookup"><span data-stu-id="841cf-118">Follow hello best practices below if you are an IoT hardware manufacture or a hardware integrator:</span></span>

* <span data-ttu-id="841cf-119">**Bereik toominimum hardwarevereisten**: Hallo hardwareontwerp minimale functies die vereist zijn voor de werking van Hallo hardware, en niets meer moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="841cf-119">**Scope hardware toominimum requirements**: hello hardware design should include minimum features required for operation of hello hardware, and nothing more.</span></span> 
* <span data-ttu-id="841cf-120">**Controleer hardware bewijs knoeien**: bouwen in mechanismen toodetect fysieke knoeien met hardware, zoals het openen van Hallo apparaat behandeld, verwijderen van een deel van het Hallo-apparaat, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="841cf-120">**Make hardware tamper proof**: build in mechanisms toodetect physical tampering of hardware, such as opening hello device cover, removing a part of hello device, etc.</span></span> 
* <span data-ttu-id="841cf-121">**Bouwen om beveiligde hardware**: als [omzet](https://en.wikipedia.org/wiki/Cost_of_goods_sold) toestaan, beveiligingsfuncties zoals beveiligd en versleuteld opslag en functionaliteit van de Trusted Platform Module TPM-opstart opbouwen.</span><span class="sxs-lookup"><span data-stu-id="841cf-121">**Build around secure hardware**: if [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permit, build security features such as secure and encrypted storage and Trusted Platform Module (TPM)-based boot functionality.</span></span>
* <span data-ttu-id="841cf-122">**Beveiligen van upgrades**: firmware bijwerken tijdens de levensduur van Hallo-apparaat is onvermijdelijk.</span><span class="sxs-lookup"><span data-stu-id="841cf-122">**Make upgrades secure**: upgrading firmware during lifetime of hello device is inevitable.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="841cf-123">Ontwikkelaars van IoT-oplossing</span><span class="sxs-lookup"><span data-stu-id="841cf-123">IoT solution developer</span></span>
<span data-ttu-id="841cf-124">Volg de aanbevolen procedures Hallo hieronder als u een ontwikkelaar IoT-oplossing:</span><span class="sxs-lookup"><span data-stu-id="841cf-124">Follow hello best practices below if you are an IoT solution developer:</span></span>

* <span data-ttu-id="841cf-125">**Ga als volgt beveiligde software development methodologie**: a t/m nadenkt over de beveiliging van Hallo begin van Hallo project alle Hallo manier tooits implementatie, testen en de implementatie ontwikkelen van beveiligde software vereist.</span><span class="sxs-lookup"><span data-stu-id="841cf-125">**Follow secure software development methodology**: developing secure software requires ground-up thinking about security from hello inception of hello project all hello way tooits implementation, testing, and deployment.</span></span>
* <span data-ttu-id="841cf-126">**Kies open-sourcesoftware zorgvuldig**: open-sourcesoftware biedt de mogelijkheid tooquickly oplossingen ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="841cf-126">**Choose open source software with care**: open source software provides an opportunity tooquickly develop solutions.</span></span>
* <span data-ttu-id="841cf-127">**Integreren met zorg**: veel Hallo software beveiligingsfouten bestaat op Hallo grens van bibliotheken en -API.</span><span class="sxs-lookup"><span data-stu-id="841cf-127">**Integrate with care**: many of hello software security flaws exist at hello boundary of libraries and APIs.</span></span> 

## <a name="iot-solution-deployer"></a><span data-ttu-id="841cf-128">Implementatie van IoT-oplossing</span><span class="sxs-lookup"><span data-stu-id="841cf-128">IoT solution deployer</span></span>
<span data-ttu-id="841cf-129">Volg de aanbevolen procedures Hallo hieronder als u een deployer IoT-oplossing:</span><span class="sxs-lookup"><span data-stu-id="841cf-129">Follow hello best practices below if you are an IoT solution deployer:</span></span>

* <span data-ttu-id="841cf-130">**Hardware veilig implementeren**: IoT-implementaties kunnen hardware toobe geïmplementeerd in niet-beveiligde locaties, zoals in openbare ruimten of zonder supervisie landinstellingen in beslag.</span><span class="sxs-lookup"><span data-stu-id="841cf-130">**Deploy hardware securely**: IoT deployments may require hardware toobe deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span>
* <span data-ttu-id="841cf-131">**Verificatiesleutels veilig te houden**: tijdens de implementatie van elk apparaat vereist dat apparaat-id's en bijbehorende verificatiesleutels gegenereerd door Hallo cloud-service.</span><span class="sxs-lookup"><span data-stu-id="841cf-131">**Keep authentication keys safe**: during deployment, each device requires device IDs and associated authentication keys generated by hello cloud service.</span></span> <span data-ttu-id="841cf-132">Beveilig deze sleutels fysiek zelfs na het Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="841cf-132">Keep these keys physically safe even after hello deployment.</span></span> <span data-ttu-id="841cf-133">Een willekeurige toets waarmee is geknoeid kan worden gebruikt door een kwaadwillende apparaat toomasquerade als een bestaand apparaat.</span><span class="sxs-lookup"><span data-stu-id="841cf-133">Any compromised key can be used by a malicious device toomasquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="841cf-134">IoT-oplossing operator</span><span class="sxs-lookup"><span data-stu-id="841cf-134">IoT solution operator</span></span>
<span data-ttu-id="841cf-135">Volg de aanbevolen procedures Hallo hieronder als u een IoT-oplossing operator:</span><span class="sxs-lookup"><span data-stu-id="841cf-135">Follow hello best practices below if you are an IoT solution operator:</span></span>

* <span data-ttu-id="841cf-136">**Houd systemen toodate**: Zorg ervoor dat de besturingssystemen van apparaten en alle apparaatstuurprogramma's zijn de meest recente versies bijgewerkte toohello.</span><span class="sxs-lookup"><span data-stu-id="841cf-136">**Keep systems up toodate**: ensure device operating systems and all device drivers are updated toohello latest versions.</span></span> 
* <span data-ttu-id="841cf-137">**Bescherming tegen schadelijke activiteiten**: als het Hallo-besturingssysteem toestaat, Hallo nieuwste antivirus- en anti-malware-mogelijkheden op elk besturingssysteem plaatsen.</span><span class="sxs-lookup"><span data-stu-id="841cf-137">**Protect against malicious activity**: if hello operating system permits, place hello latest anti-virus and anti-malware capabilities on each device operating system.</span></span> 
* <span data-ttu-id="841cf-138">**Regelmatig controleren**: controle IoT-infrastructuur voor beveiliging problemen is sleutel verwante wanneer toosecurity incidenten reageert.</span><span class="sxs-lookup"><span data-stu-id="841cf-138">**Audit frequently**: auditing IoT infrastructure for security related issues is key when responding toosecurity incidents.</span></span>
* <span data-ttu-id="841cf-139">**Fysiek Hallo IoT-infrastructuur beveiligen**: Hallo slechtste beveiligingsaanvallen tegen IoT-infrastructuur met behulp van de fysieke toegang toodevices worden gestart.</span><span class="sxs-lookup"><span data-stu-id="841cf-139">**Physically protect hello IoT infrastructure**: hello worst security attacks against IoT infrastructure are launched using physical access toodevices.</span></span>
* <span data-ttu-id="841cf-140">**Beveiligen van referenties van de cloud**: referenties voor cloud-verificatie gebruikt voor het configureren en gebruiken van een IoT-implementatie zijn mogelijk Hallo gemakkelijkste manier toogain toegang en een IoT-systeem.</span><span class="sxs-lookup"><span data-stu-id="841cf-140">**Protect cloud credentials**: cloud authentication credentials used for configuring and operating an IoT deployment are possibly hello easiest way toogain access and compromise an IoT system.</span></span> 

