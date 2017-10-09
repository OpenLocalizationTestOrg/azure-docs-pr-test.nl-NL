---
title: aaaGetting gestart met Cloud Foundry op Microsoft Azure | Microsoft Docs
description: OSS of belangrijke Cloud Foundry uitvoeren in Microsoft Azure
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a><span data-ttu-id="a6f6d-103">Cloud Foundry op Azure</span><span class="sxs-lookup"><span data-stu-id="a6f6d-103">Cloud Foundry on Azure</span></span>

<span data-ttu-id="a6f6d-104">Cloud Foundry is een open source platform-as-a-service (PaaS) voor het bouwen, te implementeren en gebruiken van 12-factor-toepassingen die in verschillende talen en frameworks ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-104">Cloud Foundry is an open-source platform-as-a-service (PaaS) for building, deploying, and operating 12-factor applications developed in various languages and frameworks.</span></span> <span data-ttu-id="a6f6d-105">Dit document beschrijft Hallo-opties die u hebt voor het uitvoeren van de Cloud Foundry op Azure en hoe u kunt aan de slag.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-105">This document describes hello options you have for running Cloud Foundry on Azure and how you can get started.</span></span>

## <a name="cloud-foundry-offerings"></a><span data-ttu-id="a6f6d-106">De offerings Foundry cloud</span><span class="sxs-lookup"><span data-stu-id="a6f6d-106">Cloud Foundry offerings</span></span>

<span data-ttu-id="a6f6d-107">Er zijn twee soorten Cloud Foundry beschikbaar toorun op Azure: open source Cloud Foundry (OSS CF) en belangrijke Cloud Foundry (PCF).</span><span class="sxs-lookup"><span data-stu-id="a6f6d-107">There are two forms of Cloud Foundry available toorun on Azure: open-source Cloud Foundry (OSS CF) and Pivotal Cloud Foundry (PCF).</span></span> <span data-ttu-id="a6f6d-108">OSS CF is een volledig [open source](https://github.com/cloudfoundry) versie van Cloud Foundry beheerd door Hallo Cloud Foundry Foundation.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-108">OSS CF is an entirely [open-source](https://github.com/cloudfoundry) version of Cloud Foundry managed by hello Cloud Foundry Foundation.</span></span> <span data-ttu-id="a6f6d-109">Belangrijke Cloud Foundry is een enterprise-distributie van Cloud Foundry van belangrijke Software, Inc. Kijken we enkele Hallo verschillen tussen de twee Hallo-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-109">Pivotal Cloud Foundry is an enterprise distribution of Cloud Foundry from Pivotal Software Inc. We look at some of hello differences between hello two offerings.</span></span>

### <a name="open-source-cloud-foundry"></a><span data-ttu-id="a6f6d-110">Open-source Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="a6f6d-110">Open-source Cloud Foundry</span></span>

<span data-ttu-id="a6f6d-111">U kunt OSS Cloud Foundry in Azure implementeren door eerst een directeur BOSH implementeren en het implementeren van Cloud Foundry, met behulp van Hallo [-instructies op GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span><span class="sxs-lookup"><span data-stu-id="a6f6d-111">You can deploy OSS Cloud Foundry on Azure by first deploying a BOSH director and then deploying Cloud Foundry, using hello [instructions provided on GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span></span> <span data-ttu-id="a6f6d-112">toolearn meer over het gebruik van OSS-CF Zie Hallo [documentatie](https://docs.cloudfoundry.org/) geleverd door Hallo Cloud Foundry Foundation.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-112">toolearn more about using OSS CF, see hello [documentation](https://docs.cloudfoundry.org/) provided by hello Cloud Foundry Foundation.</span></span>

<span data-ttu-id="a6f6d-113">Microsoft biedt ondersteuning voor het best-effort voor OSS CF via Hallo community kanalen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a6f6d-113">Microsoft provides best-effort support for OSS CF through hello following community channels:</span></span>

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a><span data-ttu-id="a6f6d-114">bosh-azure-KPI-kanaal op [Cloud Foundry Slack](https://slack.cloudfoundry.org/)</span><span class="sxs-lookup"><span data-stu-id="a6f6d-114">bosh-azure-cpi channel on [Cloud Foundry Slack](https://slack.cloudfoundry.org/)</span></span>
- [<span data-ttu-id="a6f6d-115">CF bosh mailinglijst</span><span class="sxs-lookup"><span data-stu-id="a6f6d-115">cf-bosh mailing list</span></span>](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- <span data-ttu-id="a6f6d-116">Problemen met GitHub hello [KPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) en [service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span><span class="sxs-lookup"><span data-stu-id="a6f6d-116">GitHub issues for hello [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) and [service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span></span>

>[!NOTE]
> <span data-ttu-id="a6f6d-117">Hallo-niveau van ondersteuning voor uw Azure-resources, zoals Hallo virtuele machines waarop u Cloud-Foundry uitvoert is gebaseerd op de ondersteuning van Azure-overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-117">hello level of support for your Azure resources, such as hello virtual machines where you run Cloud Foundry, is based on your Azure support agreement.</span></span> <span data-ttu-id="a6f6d-118">Communityondersteuning best effort is alleen van toepassing toohello Cloud Foundry-specifieke onderdelen.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-118">Best-effort community support only applies toohello Cloud Foundry-specific components.</span></span>

### <a name="pivotal-cloud-foundry"></a><span data-ttu-id="a6f6d-119">Belangrijke Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="a6f6d-119">Pivotal Cloud Foundry</span></span>

<span data-ttu-id="a6f6d-120">Belangrijke Cloud Foundry Hallo bevat dezelfde kernplatform als Hallo OSS-distributiepunt, samen met een reeks bedrijfseigen beheerhulpprogramma's en enterprise-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-120">Pivotal Cloud Foundry includes hello same core platform as hello OSS distribution, along with a set of proprietary management tools and enterprise support.</span></span> <span data-ttu-id="a6f6d-121">toorun PCF op Azure, moet u een licentie van Pivotal verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-121">toorun PCF on Azure, you must acquire a license from Pivotal.</span></span> <span data-ttu-id="a6f6d-122">Hallo PCF aanbieding van hello Azure marketplace omvat proeflicentie is 90 dagen.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-122">hello PCF offer from hello Azure marketplace includes a 90-day trial license.</span></span>

<span data-ttu-id="a6f6d-123">Hallo's bevatten [belangrijke Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), een webtoepassing die vereenvoudigt de implementatie en beheer van een basis Cloud Foundry en [belangrijke Apps Manager](https://docs.pivotal.io/pivotalcf/console/), een webtoepassing voor het beheren van gebruikers en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-123">hello tools include [Pivotal Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), a web application that simplifies deployment and management of a Cloud Foundry foundation, and [Pivotal Apps Manager](https://docs.pivotal.io/pivotalcf/console/), a web application for managing users and applications.</span></span>

<span data-ttu-id="a6f6d-124">Bovendien toohello ondersteuningskanalen voor OSS CF hierboven vermeld, kunt een licentie PCF u toocontact Pivotal voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-124">In addition toohello support channels listed for OSS CF above, a PCF license entitles you toocontact Pivotal for support.</span></span> <span data-ttu-id="a6f6d-125">Microsoft Pivotal ondersteuning werkstromen waarmee u toocontact beide partijen voor hulp hebben ingeschakeld en en hebben uw vraag op de juiste wijze worden doorgestuurd, afhankelijk van waar Hallo probleem wordt veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-125">Microsoft and Pivotal have also enabled support workflows that allow you toocontact either party for assistance and have your inquiry routed appropriately depending on where hello issue lies.</span></span>

## <a name="azure-service-broker"></a><span data-ttu-id="a6f6d-126">Azure Service Broker</span><span class="sxs-lookup"><span data-stu-id="a6f6d-126">Azure Service Broker</span></span>

<span data-ttu-id="a6f6d-127">Cloud Foundry moedigt Hallo ['twaalf factor app'](https://12factor.net/) methodologie die bijdraagt aan een schone scheiding van toepassingsprocessen staatloze en stateful services back-ups.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-127">Cloud Foundry encourages hello ["twelve-factor app"](https://12factor.net/) methodology, which promotes a clean separation of stateless application processes and stateful backing services.</span></span> <span data-ttu-id="a6f6d-128">[Service beleggingsmakelaars](https://docs.cloudfoundry.org/services/api.html) bieden een consistente manier tooprovision en ondersteunende services tooapplications binden.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-128">[Service brokers](https://docs.cloudfoundry.org/services/api.html) offer a consistent way tooprovision and bind backing services tooapplications.</span></span> <span data-ttu-id="a6f6d-129">Hallo [Azure service broker](https://github.com/Azure/meta-azure-service-broker) staan enkele Hallo belangrijke Azure-services via dit kanaal, met inbegrip van Azure storage en Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-129">hello [Azure service broker](https://github.com/Azure/meta-azure-service-broker) provides some of hello key Azure services through this channel, including Azure storage and Azure SQL.</span></span>

<span data-ttu-id="a6f6d-130">Als u van belangrijke Cloud Foundry gebruikmaakt, Hallo service broker is ook [beschikbaar als een tegel](https://docs.pivotal.io/azure-sb/installing.html) van Hallo centrale netwerk.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-130">If you are using Pivotal Cloud Foundry, hello service broker is also [available as a tile](https://docs.pivotal.io/azure-sb/installing.html) from hello Pivotal Network.</span></span>

## <a name="related-resources"></a><span data-ttu-id="a6f6d-131">Gerelateerde resources</span><span class="sxs-lookup"><span data-stu-id="a6f6d-131">Related resources</span></span>

### <a name="visual-studio-team-services-plugin"></a><span data-ttu-id="a6f6d-132">Visual Studio Team Services-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="a6f6d-132">Visual Studio Team Services plugin</span></span>

<span data-ttu-id="a6f6d-133">Cloud Foundry is uitermate geschikt tooagile software development, waaronder Hallo gebruik van doorlopende integratie (CI) en continue levering (CD).</span><span class="sxs-lookup"><span data-stu-id="a6f6d-133">Cloud Foundry is well suited tooagile software development, including hello use of continuous integration (CI) and continuous delivery (CD).</span></span> <span data-ttu-id="a6f6d-134">Als u Visual Studio Team Services (VSTS) toomanage projecten en wilt tooset van een Cloud Foundry targeting CI/CD-pijplijn, kunt u Hallo [VSTS Cloud Foundry-opbouwextensie](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span><span class="sxs-lookup"><span data-stu-id="a6f6d-134">If you use Visual Studio Team Services (VSTS) toomanage your projects and would like tooset up a CI/CD pipeline targeting Cloud Foundry, you can use hello [VSTS Cloud Foundry build extension](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span></span> <span data-ttu-id="a6f6d-135">Hallo-invoegtoepassing kunt u eenvoudige tooconfigure en implementaties tooCloud Foundry, automatiseren of uitgevoerd in Azure of een andere omgeving.</span><span class="sxs-lookup"><span data-stu-id="a6f6d-135">hello plugin makes it simple tooconfigure and automate deployments tooCloud Foundry, whether running in Azure or another environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6f6d-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6f6d-136">Next steps</span></span>

- [<span data-ttu-id="a6f6d-137">Belangrijke Cloud Foundry implementeren vanuit Azure Marketplace Hallo</span><span class="sxs-lookup"><span data-stu-id="a6f6d-137">Deploy Pivotal Cloud Foundry from hello Azure Marketplace</span></span>](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [<span data-ttu-id="a6f6d-138">Een app tooCloud Foundry in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="a6f6d-138">Deploy an app tooCloud Foundry in Azure</span></span>](./cloudfoundry-deploy-your-first-app.md)
