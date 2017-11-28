---
title: New Relic met Azure aaaUsing | Microsoft Docs
description: Ontdek hoe toouse Hallo toomanage van New Relic-service en bewaken van uw Azure-toepassing.
services: 
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: 
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: 81e5f1b694264e3586ac75d40edd8afe185493d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="1d6be-103">Nieuwe Relic prestaties Toepassingsbeheer op Azure</span><span class="sxs-lookup"><span data-stu-id="1d6be-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="1d6be-104">U kunt toevoegen hoogwaardige prestaties van New Relic tooyour bewaking Azure gehoste toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1d6be-104">You can add New Relic's world-class performance monitoring tooyour Azure hosted applications.</span></span> <span data-ttu-id="1d6be-105">Samen met uitgebreide mogelijkheden voor bewaking, het oplossen van problemen en het afstemmen van uw Azure-apps, bent u ook in aanmerking komen voor een gereduceerd tarief voor New Relic-producten met behulp van Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6be-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="1d6be-106">What's New Relic?</span><span class="sxs-lookup"><span data-stu-id="1d6be-106">What is New Relic?</span></span>
<span data-ttu-id="1d6be-107">Met [New Relic-producten](https://newrelic.com/products), app-fouten oplossen, wees potentiële problemen en begrijpen Hallo prestaties van uw hele omgeving.</span><span class="sxs-lookup"><span data-stu-id="1d6be-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand hello performance of your entire environment.</span></span> <span data-ttu-id="1d6be-108">Is ontworpen toosave u tijd bij het identificeren en het onderzoeken van prestatieproblemen en plaatst het Hallo informatie die u nodig toosolve deze problemen bij de hand.</span><span class="sxs-lookup"><span data-stu-id="1d6be-108">It is designed toosave you time when identifying and diagnosing performance issues, and it puts hello information you need toosolve these issues at your fingertips.</span></span>

<span data-ttu-id="1d6be-109">Nieuwe Relic houdt Hallo laden tijd en de doorvoer voor uw webtransacties, zowel naar Hallo-server en de browsers van uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1d6be-109">New Relic tracks hello load time and throughput for your web transactions, both from hello server and your users' browsers.</span></span> <span data-ttu-id="1d6be-110">Na hoeveel tijd in Hallo-database, analyseert trage query's en webaanvragen, biedt bedrijfstijd bewaking en waarschuwingen, houdt toepassingsuitzonderingen en nog veel meer worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1d6be-110">It shows how much time you spend in hello database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="1d6be-111">Speciale prijzen</span><span class="sxs-lookup"><span data-stu-id="1d6be-111">Special pricing</span></span>
<span data-ttu-id="1d6be-112">Nieuwe Relic Standard is gratis tooAzure gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1d6be-112">New Relic Standard is free tooAzure users.</span></span> <span data-ttu-id="1d6be-113">Nieuwe Relic Pro wordt aangeboden op basis van de exemplaargrootte van het voor Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="1d6be-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="1d6be-114">Zie voor informatie over prijzen, Hallo [New Relic pagina](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) Hallo in Azure Marketplace of neem contact op met de New Relic (sales@newrelic.com) voor de prijzen op bedrijfsniveau.</span><span class="sxs-lookup"><span data-stu-id="1d6be-114">For pricing information, see hello [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in hello Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="1d6be-115">Azure-klanten ontvangen een proefabonnement op twee weken van nieuwe Relic Pro wanneer ze Hallo New Relic-agent te implementeren.</span><span class="sxs-lookup"><span data-stu-id="1d6be-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy hello New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-hello-azure-store"></a><span data-ttu-id="1d6be-116">Aanmelden voor New Relic met hello Azure Store</span><span class="sxs-lookup"><span data-stu-id="1d6be-116">Sign up for New Relic using hello Azure Store</span></span>
<span data-ttu-id="1d6be-117">New Relic naadloos geïntegreerd met Azure webrollen en werkrollen.</span><span class="sxs-lookup"><span data-stu-id="1d6be-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="1d6be-118">U kunt snel en eenvoudig melden voor New Relic rechtstreeks vanuit hello Azure Store.</span><span class="sxs-lookup"><span data-stu-id="1d6be-118">You can quickly and easily sign up for New Relic directly from hello Azure Store.</span></span> <span data-ttu-id="1d6be-119">Zie voor instructies Hallo [Azure opslaan registratie-instructies](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) van New Relic.</span><span class="sxs-lookup"><span data-stu-id="1d6be-119">For instructions, see hello [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="1d6be-120">Bekijk uw gegevens</span><span class="sxs-lookup"><span data-stu-id="1d6be-120">View your data</span></span>
<span data-ttu-id="1d6be-121">Zodra u zich hebt aangemeld, kunt u profiteren van New Relic fantastische toepassingsbewaking en gegevensgestuurde analyse.</span><span class="sxs-lookup"><span data-stu-id="1d6be-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="1d6be-122">toocheck van uw app-prestaties van New Relic:</span><span class="sxs-lookup"><span data-stu-id="1d6be-122">toocheck your app's performance in New Relic:</span></span>

1. <span data-ttu-id="1d6be-123">Selecteer in Azure Portal hello, beheren.</span><span class="sxs-lookup"><span data-stu-id="1d6be-123">From hello Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="1d6be-124">Aanmelden met uw e-mailadres van New Relic-account en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="1d6be-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="1d6be-125">Selecteer uw app uit Hallo toepassing index tooview van uw app-gegevens in Hallo [APM overzichtspagina](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="1d6be-125">Select your app from hello Application index tooview all your app's data in hello [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="1d6be-126">Met behulp van New Relic met Azure</span><span class="sxs-lookup"><span data-stu-id="1d6be-126">Using New Relic with Azure</span></span>
<span data-ttu-id="1d6be-127">Zie voor meer informatie over het gebruik van New Relic en Azure [New Relic-documentatiesite](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), waaronder:</span><span class="sxs-lookup"><span data-stu-id="1d6be-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="1d6be-128">New Relic voor .NET</span><span class="sxs-lookup"><span data-stu-id="1d6be-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="1d6be-129">Een .NET-Werkrol op Azure Cloud service softwareontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="1d6be-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="1d6be-130">New Relic voor Hallo Microsoft Azure-Cloud-platform</span><span class="sxs-lookup"><span data-stu-id="1d6be-130">New Relic for hello Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="1d6be-131">New Relic voor Hallo Microsoft Azure App Services</span><span class="sxs-lookup"><span data-stu-id="1d6be-131">New Relic for hello Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="1d6be-132">Nieuwe Relic/Azure oplossen</span><span class="sxs-lookup"><span data-stu-id="1d6be-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

