---
title: aaaEnterprise-integratie voor B2B - Azure Logic Apps | Microsoft Docs
description: B2B-werkstromen bouwen en ondersteuning voor enterprise integration-scenario's voor logische apps Hello Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a><span data-ttu-id="fcc33-103">Overzicht: B2B-scenario's en communicatie met de Hallo Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="fcc33-103">Overview: B2B scenarios and communication with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="fcc33-104">U kunt enterprise integratiescenario's met Microsoft cloud-gebaseerde oplossing voor Enterprise Integration Pack Hallo inschakelen voor business-to-business (B2B) werkstromen en naadloze communicatie met Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="fcc33-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, hello Enterprise Integration Pack.</span></span> <span data-ttu-id="fcc33-105">Organisaties kunnen uitwisselen berichten elektronisch, zelfs als ze verschillende protocollen en indelingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fcc33-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="fcc33-106">Hallo pack transformeert verschillende indelingen in een indeling die organisaties systemen kunnen interpreteren en verwerken.</span><span class="sxs-lookup"><span data-stu-id="fcc33-106">hello pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="fcc33-107">Organisaties kunnen berichten via industriestandaard-protocollen, zoals uitwisselen [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), en [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="fcc33-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="fcc33-108">U kunt ook berichten met zowel versleuteling als digitale handtekeningen beveiligen.</span><span class="sxs-lookup"><span data-stu-id="fcc33-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="fcc33-109">Als u bekend met BizTalk Server of Microsoft Azure BizTalk Services bent, zijn Hallo Enterprise Integration-functies eenvoudig toouse, omdat de meeste concepten vergelijkbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="fcc33-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, hello Enterprise Integration features are easy toouse because most concepts are similar.</span></span> <span data-ttu-id="fcc33-110">Een belangrijk verschil is dat Enterprise Integration integratie accounts toosimplify Hallo opslag en het beheer van artefacten die worden gebruikt in B2B-communicatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fcc33-110">One major difference is that Enterprise Integration uses integration accounts toosimplify hello storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="fcc33-111">Enterprise Integration Pack Hallo is qua architectuur is gebaseerd op 'integratieaccounts'.</span><span class="sxs-lookup"><span data-stu-id="fcc33-111">Architecturally, hello Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="fcc33-112">Deze accounts zijn cloud-gebaseerde containers waarin alle uw artefacten, zoals schema's, partners, certificaten, maps en overeenkomsten.</span><span class="sxs-lookup"><span data-stu-id="fcc33-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="fcc33-113">U kunt deze artefacten toodesign gebruiken, implementeren en onderhouden van uw B2B-apps en ook toobuild B2B-werkstromen voor logic apps.</span><span class="sxs-lookup"><span data-stu-id="fcc33-113">You can use these artifacts toodesign, deploy, and maintain your B2B apps and also toobuild B2B workflows for logic apps.</span></span> <span data-ttu-id="fcc33-114">Maar voordat u deze artefacten gebruiken kunt, moet u eerst uw integratie account tooyour logische app koppelen.</span><span class="sxs-lookup"><span data-stu-id="fcc33-114">But before you can use these artifacts, you must first link your integration account tooyour logic app.</span></span> <span data-ttu-id="fcc33-115">Daarna uw logische app toegang tot uw integratie-account artefacten.</span><span class="sxs-lookup"><span data-stu-id="fcc33-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="fcc33-116">Waarom moet u de enterprise-integratie gebruiken?</span><span class="sxs-lookup"><span data-stu-id="fcc33-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="fcc33-117">Met enterprise-integratie kunt u alle uw artefacten opslaan op één plek--uw integratie-account.</span><span class="sxs-lookup"><span data-stu-id="fcc33-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="fcc33-118">U kunt B2B werkstromen bouwen en integreren met software-as-service (SaaS)-apps van derden, lokale apps en aangepaste apps met behulp van hello Azure Logic Apps-engine en alle bijbehorende connectors.</span><span class="sxs-lookup"><span data-stu-id="fcc33-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using hello Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="fcc33-119">U kunt aangepaste code maken voor uw logische apps met Azure functions.</span><span class="sxs-lookup"><span data-stu-id="fcc33-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-tooget-started-with-enterprise-integration"></a><span data-ttu-id="fcc33-120">Hoe tooget gestart met enterprise-integratie?</span><span class="sxs-lookup"><span data-stu-id="fcc33-120">How tooget started with enterprise integration?</span></span>

<span data-ttu-id="fcc33-121">U kunt maken en beheren van B2B-apps met Enterprise Integration Pack Hallo via Hallo Logic App-ontwerper in Hallo **Azure-portal**.</span><span class="sxs-lookup"><span data-stu-id="fcc33-121">You can build and manage B2B apps with hello Enterprise Integration Pack through hello Logic App Designer in hello **Azure portal**.</span></span> <span data-ttu-id="fcc33-122">U kunt ook uw logische apps met beheren [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell-onderwerpen").</span><span class="sxs-lookup"><span data-stu-id="fcc33-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="fcc33-123">Hier volgen Hallo geavanceerde stappen die u nemen moet voordat u apps in hello Azure-portal maken kunt:</span><span class="sxs-lookup"><span data-stu-id="fcc33-123">Here are hello high-level steps you must take before you can create apps in hello Azure portal:</span></span>

![Overzicht van de installatiekopie](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="fcc33-125">Wat zijn enkele algemene scenario's?</span><span class="sxs-lookup"><span data-stu-id="fcc33-125">What are some common scenarios?</span></span>

<span data-ttu-id="fcc33-126">Enterprise Integration ondersteunt deze industrienormen:</span><span class="sxs-lookup"><span data-stu-id="fcc33-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="fcc33-127">EDI - Electronic Data Interchange</span><span class="sxs-lookup"><span data-stu-id="fcc33-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="fcc33-128">EAI - Enterprise toepassingsintegratie</span><span class="sxs-lookup"><span data-stu-id="fcc33-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-tooget-started"></a><span data-ttu-id="fcc33-129">Dit is wat u moet tooget gestart</span><span class="sxs-lookup"><span data-stu-id="fcc33-129">Here's what you need tooget started</span></span>

* <span data-ttu-id="fcc33-130">Een Azure-abonnement met een account voor de integratie</span><span class="sxs-lookup"><span data-stu-id="fcc33-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="fcc33-131">Visual Studio 2015 toocreate maps en schema 's</span><span class="sxs-lookup"><span data-stu-id="fcc33-131">Visual Studio 2015 toocreate maps and schemas</span></span>
* [<span data-ttu-id="fcc33-132">Microsoft Azure Logic Apps Enterprise Integration-Tools voor Visual Studio 2015 2.0</span><span class="sxs-lookup"><span data-stu-id="fcc33-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="fcc33-133">Probeer het nu</span><span class="sxs-lookup"><span data-stu-id="fcc33-133">Try it now</span></span>

<span data-ttu-id="fcc33-134">[Implementeren van een volledig operationeel voorbeeld AS2 verzenden en ontvangen van de logische app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) die gebruikmaakt van Hallo B2B-functies voor Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="fcc33-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses hello B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="fcc33-135">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="fcc33-135">Learn more</span></span>
* [<span data-ttu-id="fcc33-136">Overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="fcc33-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")
* [<span data-ttu-id="fcc33-137">Bedrijfsscenario tooBusiness (B2B)</span><span class="sxs-lookup"><span data-stu-id="fcc33-137">Business tooBusiness (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "leren hoe toocreate Logic apps met B2B-functies")  
* [<span data-ttu-id="fcc33-138">Certificaten</span><span class="sxs-lookup"><span data-stu-id="fcc33-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "meer informatie over certificaten voor ondernemingen-integratie")
* [<span data-ttu-id="fcc33-139">Platte bestand codering/decodering</span><span class="sxs-lookup"><span data-stu-id="fcc33-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "leren hoe tooencode en decoderen plat bestand-inhoud")  
* [<span data-ttu-id="fcc33-140">Integratieaccounts</span><span class="sxs-lookup"><span data-stu-id="fcc33-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "meer informatie over integratieaccounts")
* [<span data-ttu-id="fcc33-141">Toegewezen</span><span class="sxs-lookup"><span data-stu-id="fcc33-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "meer informatie over enterprise integration maps")
* [<span data-ttu-id="fcc33-142">Partners</span><span class="sxs-lookup"><span data-stu-id="fcc33-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "meer informatie over enterprise integration-partners")
* [<span data-ttu-id="fcc33-143">Schema's</span><span class="sxs-lookup"><span data-stu-id="fcc33-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "meer informatie over enterprise integration-schema's")
* [<span data-ttu-id="fcc33-144">XML-bericht validatie</span><span class="sxs-lookup"><span data-stu-id="fcc33-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "meer informatie over hoe toovalidate XML berichten met Logic apps")
* [<span data-ttu-id="fcc33-145">XML-transformatie</span><span class="sxs-lookup"><span data-stu-id="fcc33-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "meer informatie over enterprise integration maps")
* [<span data-ttu-id="fcc33-146">Enterprise Integration-Connectors</span><span class="sxs-lookup"><span data-stu-id="fcc33-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "meer informatie over enterprise integration pack-connectors")
* [<span data-ttu-id="fcc33-147">Integratie Account metagegevens</span><span class="sxs-lookup"><span data-stu-id="fcc33-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "meer informatie over de metagegevens van de integratie-account")
* [<span data-ttu-id="fcc33-148">B2B-berichten</span><span class="sxs-lookup"><span data-stu-id="fcc33-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "meer informatie over het bewaken van B2B-berichten")
* [<span data-ttu-id="fcc33-149">B2B-berichten in de OMS-portal bijhouden</span><span class="sxs-lookup"><span data-stu-id="fcc33-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "meer informatie over het bijhouden van B2B-berichten in de OMS-portal")

