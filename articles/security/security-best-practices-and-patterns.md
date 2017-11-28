---
title: aaaAzure security best practices en patronen | Microsoft Docs
description: Hallo artikel bevat een inleiding over aanbevolen beveiligingsprocedures voor Azure en patronen en een geselecteerde lijst met aanbevolen beveiligingsprocedures voor verschillende Azure-resources.
services: azure-security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1cbbf8dc-ea94-4a7e-8fa0-c2cb198956c5
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: terrylan
ms.openlocfilehash: eaaa9457faa1d5906275eb1fd8988d4d4aad101a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-best-practices-and-patterns"></a><span data-ttu-id="46009-103">Azure-beveiliging aanbevolen procedures en patronen</span><span class="sxs-lookup"><span data-stu-id="46009-103">Azure security best practices and patterns</span></span>
<span data-ttu-id="46009-104">Momenteel hebben we hello Azure-beveiliging aanbevolen procedures en patronen artikelen te volgen.</span><span class="sxs-lookup"><span data-stu-id="46009-104">We currently have hello following Azure security best practices and patterns articles.</span></span> <span data-ttu-id="46009-105">Zorg ervoor dat toovisit deze site werkt periodiek toosee tooour groeiende lijst met Azure-beveiliging aanbevolen procedures en patronen:</span><span class="sxs-lookup"><span data-stu-id="46009-105">Make sure toovisit this site periodically toosee updates tooour growing list of Azure security best practices and patterns:</span></span>  

* [<span data-ttu-id="46009-106">Aanbevolen beveiligingsprocedures voor Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="46009-106">Azure network security best practices</span></span>](azure-security-network-security-best-practices.md)
* [<span data-ttu-id="46009-107">Aanbevolen procedures voor beveiliging van gegevens van Azure en versleuteling</span><span class="sxs-lookup"><span data-stu-id="46009-107">Azure data security and encryption best practices</span></span>](azure-security-data-encryption-best-practices.md)
* [<span data-ttu-id="46009-108">Toegang voor identiteits- en aanbevolen procedures voor beveiliging beheren</span><span class="sxs-lookup"><span data-stu-id="46009-108">Identity management and access control security best practices</span></span>](azure-security-identity-management-best-practices.md)
* [<span data-ttu-id="46009-109">Aanbevolen beveiligingsprocedures voor Internet der dingen</span><span class="sxs-lookup"><span data-stu-id="46009-109">Internet of Things security best practices</span></span>](azure-security-iot-best-practices.md)
* <span data-ttu-id="46009-110">[Azure IaaS Best Practices voor beveiliging] (azure-beveiliging-iaas.md)</span><span class="sxs-lookup"><span data-stu-id="46009-110">[Azure IaaS Security Best Practices] (azure-security-iaas.md)</span></span>
* [<span data-ttu-id="46009-111">Aanbevolen beveiligingsprocedures voor Azure grens</span><span class="sxs-lookup"><span data-stu-id="46009-111">Azure boundary security best practices</span></span>](../best-practices-network-security.md)
* [<span data-ttu-id="46009-112">Een beveiligde, hybride netwerkarchitectuur implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="46009-112">Implementing a secure hybrid network architecture in Azure</span></span>](../guidance/guidance-iaas-ra-secure-vnet-hybrid.md)
* <span data-ttu-id="46009-113">[Azure PaaS-Best Practices] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span><span class="sxs-lookup"><span data-stu-id="46009-113">[Azure PaaS Best Practices] (https://docs.microsoft.com/en-us/azure/security/security-paas-deployments)</span></span>

<span data-ttu-id="46009-114">Azure biedt een veilige platform waarop u uw oplossingen kunt bouwen.</span><span class="sxs-lookup"><span data-stu-id="46009-114">Azure provides a secure platform on which you can build your solutions.</span></span> <span data-ttu-id="46009-115">We bieden ook services en -technologieën toomake uw oplossingen in Azure beter te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="46009-115">We also provide services and technologies toomake your solutions on Azure more secure.</span></span> <span data-ttu-id="46009-116">Vanwege Hallo veel opties beschikbaar tooyou, hebt u veel geïnteresseerd zijn in wat Microsoft raadt u aan als best practices en patronen voor het verbeteren van de beveiliging uitgesproken.</span><span class="sxs-lookup"><span data-stu-id="46009-116">Because of hello many options available tooyou, many of you have voiced an interest in what Microsoft recommends as best practices and patterns for improving security.</span></span>

<span data-ttu-id="46009-117">We uw interesse begrijpen en een verzameling van documenten die wordt beschreven wat u, gegeven Hallo juiste context tooimprove Hallo beveiliging van Azure implementaties doen kunt hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46009-117">We understand your interest and have created a collection of documents that describe things you can do, given hello right context, tooimprove hello security of Azure deployments.</span></span>

<span data-ttu-id="46009-118">Een verzameling van best practices en nuttig patronen voor bepaalde onderwerpen besproken in deze aanbevolen procedures en patronen artikelen.</span><span class="sxs-lookup"><span data-stu-id="46009-118">In these best practices and patterns articles, we discuss a collection of best practices and useful patterns for specific topics.</span></span> <span data-ttu-id="46009-119">Deze aanbevolen procedures en patronen zijn afgeleid van onze ervaring met deze technologieën en Hallo ervaringen van klanten, zoals zelf.</span><span class="sxs-lookup"><span data-stu-id="46009-119">These best practices and patterns are derived from our experiences with these technologies and hello experiences of customers like yourself.</span></span>

<span data-ttu-id="46009-120">Voor elke beste streven we ernaar tooexplain:</span><span class="sxs-lookup"><span data-stu-id="46009-120">For each best practice we strive tooexplain:</span></span>

* <span data-ttu-id="46009-121">Welke beste Hallo</span><span class="sxs-lookup"><span data-stu-id="46009-121">What hello best practice is</span></span>
* <span data-ttu-id="46009-122">Waarom u wilt dat tooenable die best practices</span><span class="sxs-lookup"><span data-stu-id="46009-122">Why you want tooenable that best practice</span></span>
* <span data-ttu-id="46009-123">Wat zijn Hallo resultaat als u niet tooenable Hallo aanbevolen</span><span class="sxs-lookup"><span data-stu-id="46009-123">What might be hello result if you fail tooenable hello best practice</span></span>
* <span data-ttu-id="46009-124">Mogelijke alternatieven toohello best practices</span><span class="sxs-lookup"><span data-stu-id="46009-124">Possible alternatives toohello best practice</span></span>
* <span data-ttu-id="46009-125">Hoe meer u tooenable Hallo best practices</span><span class="sxs-lookup"><span data-stu-id="46009-125">How you can learn tooenable hello best practice</span></span>

<span data-ttu-id="46009-126">We hopen tooincluding veel meer artikelen over Azure-beveiligingsarchitectuur en aanbevolen procedures.</span><span class="sxs-lookup"><span data-stu-id="46009-126">We look forward tooincluding many more articles on Azure security architecture and best practices.</span></span> <span data-ttu-id="46009-127">Als er onderwerpen die u graag tooinclude, laat ons weten in Hallo discussie gebied op Hallo onder aan deze pagina.</span><span class="sxs-lookup"><span data-stu-id="46009-127">If there are topics that you'd like us tooinclude, let us know in hello discussion area at hello bottom of this page.</span></span>
