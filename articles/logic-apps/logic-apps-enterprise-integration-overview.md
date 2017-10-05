---
title: Enterprise-integratie voor B2B - Azure Logic Apps | Microsoft Docs
description: B2B-werkstromen bouwen en ondersteuning voor enterprise integration-scenario's voor logische apps met de Enterprise-integratiepakket
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
ms.openlocfilehash: 9462707db03ecfcc3d5186ce7ded8655ad3bdcc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-the-enterprise-integration-pack"></a><span data-ttu-id="7c4ad-103">Overzicht: B2B-scenario's en communicatie met de Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="7c4ad-103">Overview: B2B scenarios and communication with the Enterprise Integration Pack</span></span>

<span data-ttu-id="7c4ad-104">U kunt enterprise integratiescenario's met Microsoft cloud-gebaseerde oplossing voor het integratiepakket Enterprise inschakelen voor business-to-business (B2B) werkstromen en naadloze communicatie met Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, the Enterprise Integration Pack.</span></span> <span data-ttu-id="7c4ad-105">Organisaties kunnen uitwisselen berichten elektronisch, zelfs als ze verschillende protocollen en indelingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="7c4ad-106">Het pack transformeert verschillende indelingen in een indeling die organisaties systemen kunnen interpreteren en verwerken.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-106">The pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="7c4ad-107">Organisaties kunnen berichten via industriestandaard-protocollen, zoals uitwisselen [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), en [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="7c4ad-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="7c4ad-108">U kunt ook berichten met zowel versleuteling als digitale handtekeningen beveiligen.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="7c4ad-109">Als u bekend met BizTalk Server of Microsoft Azure BizTalk Services bent, zijn de functies voor Enterprise Integration eenvoudig te gebruiken omdat de meeste concepten vergelijkbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, the Enterprise Integration features are easy to use because most concepts are similar.</span></span> <span data-ttu-id="7c4ad-110">Een belangrijk verschil is dat Enterprise Integration integratieaccounts gebruikt voor het vereenvoudigen van de opslag en het beheer van artefacten in B2B-communicatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-110">One major difference is that Enterprise Integration uses integration accounts to simplify the storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="7c4ad-111">Het integratiepakket Enterprise is qua architectuur is gebaseerd op 'integratieaccounts'.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-111">Architecturally, the Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="7c4ad-112">Deze accounts zijn cloud-gebaseerde containers waarin alle uw artefacten, zoals schema's, partners, certificaten, maps en overeenkomsten.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="7c4ad-113">U kunt deze artefacten ontwerpen, implementeren en onderhouden van uw B2B-apps en om B2B-werkstromen voor logic apps te bouwen.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-113">You can use these artifacts to design, deploy, and maintain your B2B apps and also to build B2B workflows for logic apps.</span></span> <span data-ttu-id="7c4ad-114">Maar voordat u deze artefacten gebruiken kunt, moet u eerst uw integratie-account koppelen aan uw logische app.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-114">But before you can use these artifacts, you must first link your integration account to your logic app.</span></span> <span data-ttu-id="7c4ad-115">Daarna uw logische app toegang tot uw integratie-account artefacten.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="7c4ad-116">Waarom moet u de enterprise-integratie gebruiken?</span><span class="sxs-lookup"><span data-stu-id="7c4ad-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="7c4ad-117">Met enterprise-integratie kunt u alle uw artefacten opslaan op één plek--uw integratie-account.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="7c4ad-118">U kunt B2B werkstromen bouwen en integreren met software-as-service (SaaS)-apps van derden, lokale apps en aangepaste apps met behulp van de Azure Logic Apps-engine en alle bijbehorende connectors.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using the Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="7c4ad-119">U kunt aangepaste code maken voor uw logische apps met Azure functions.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-to-get-started-with-enterprise-integration"></a><span data-ttu-id="7c4ad-120">Hoe kan ik aan de slag met enterprise-integratie?</span><span class="sxs-lookup"><span data-stu-id="7c4ad-120">How to get started with enterprise integration?</span></span>

<span data-ttu-id="7c4ad-121">U kunt bouwen en B2B apps beheren met de Enterprise Integration Pack via de App-ontwerper van de logica in de **Azure-portal**.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-121">You can build and manage B2B apps with the Enterprise Integration Pack through the Logic App Designer in the **Azure portal**.</span></span> <span data-ttu-id="7c4ad-122">U kunt ook uw logische apps met beheren [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell-onderwerpen").</span><span class="sxs-lookup"><span data-stu-id="7c4ad-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="7c4ad-123">Hier volgen de hoofdstappen die u nemen moet voordat u apps in de Azure portal maken kunt:</span><span class="sxs-lookup"><span data-stu-id="7c4ad-123">Here are the high-level steps you must take before you can create apps in the Azure portal:</span></span>

![Overzicht van de installatiekopie](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="7c4ad-125">Wat zijn enkele algemene scenario's?</span><span class="sxs-lookup"><span data-stu-id="7c4ad-125">What are some common scenarios?</span></span>

<span data-ttu-id="7c4ad-126">Enterprise Integration ondersteunt deze industrienormen:</span><span class="sxs-lookup"><span data-stu-id="7c4ad-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="7c4ad-127">EDI - Electronic Data Interchange</span><span class="sxs-lookup"><span data-stu-id="7c4ad-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="7c4ad-128">EAI - Enterprise toepassingsintegratie</span><span class="sxs-lookup"><span data-stu-id="7c4ad-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-to-get-started"></a><span data-ttu-id="7c4ad-129">Dit is wat u moet aan de slag</span><span class="sxs-lookup"><span data-stu-id="7c4ad-129">Here's what you need to get started</span></span>

* <span data-ttu-id="7c4ad-130">Een Azure-abonnement met een account voor de integratie</span><span class="sxs-lookup"><span data-stu-id="7c4ad-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="7c4ad-131">Visual Studio 2015 maps en schema's maken</span><span class="sxs-lookup"><span data-stu-id="7c4ad-131">Visual Studio 2015 to create maps and schemas</span></span>
* [<span data-ttu-id="7c4ad-132">Microsoft Azure Logic Apps Enterprise Integration-Tools voor Visual Studio 2015 2.0</span><span class="sxs-lookup"><span data-stu-id="7c4ad-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="7c4ad-133">Probeer het nu</span><span class="sxs-lookup"><span data-stu-id="7c4ad-133">Try it now</span></span>

<span data-ttu-id="7c4ad-134">[Implementeren van een volledig operationeel voorbeeld AS2 verzenden en ontvangen van de logische app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) die gebruikmaakt van de B2B-functies voor Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="7c4ad-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses the B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="7c4ad-135">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="7c4ad-135">Learn more</span></span>
* [<span data-ttu-id="7c4ad-136">Overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="7c4ad-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")
* [<span data-ttu-id="7c4ad-137">Scenario's voor Business-to-Business (B2B)</span><span class="sxs-lookup"><span data-stu-id="7c4ad-137">Business to Business (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "informatie over het maken van logische apps met B2B-functies")  
* [<span data-ttu-id="7c4ad-138">Certificaten</span><span class="sxs-lookup"><span data-stu-id="7c4ad-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "meer informatie over certificaten voor ondernemingen-integratie")
* [<span data-ttu-id="7c4ad-139">Platte bestand codering/decodering</span><span class="sxs-lookup"><span data-stu-id="7c4ad-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "informatie over het coderen en decoderen plat bestand-inhoud")  
* [<span data-ttu-id="7c4ad-140">Integratieaccounts</span><span class="sxs-lookup"><span data-stu-id="7c4ad-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "meer informatie over integratieaccounts")
* [<span data-ttu-id="7c4ad-141">Toegewezen</span><span class="sxs-lookup"><span data-stu-id="7c4ad-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "meer informatie over enterprise integration maps")
* [<span data-ttu-id="7c4ad-142">Partners</span><span class="sxs-lookup"><span data-stu-id="7c4ad-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "meer informatie over enterprise integration-partners")
* [<span data-ttu-id="7c4ad-143">Schema's</span><span class="sxs-lookup"><span data-stu-id="7c4ad-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "meer informatie over enterprise integration-schema's")
* [<span data-ttu-id="7c4ad-144">XML-bericht validatie</span><span class="sxs-lookup"><span data-stu-id="7c4ad-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "informatie over het valideren van XML-berichten met Logic apps")
* [<span data-ttu-id="7c4ad-145">XML-transformatie</span><span class="sxs-lookup"><span data-stu-id="7c4ad-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "meer informatie over enterprise integration maps")
* [<span data-ttu-id="7c4ad-146">Enterprise Integration-Connectors</span><span class="sxs-lookup"><span data-stu-id="7c4ad-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "meer informatie over enterprise integration pack-connectors")
* [<span data-ttu-id="7c4ad-147">Integratie Account metagegevens</span><span class="sxs-lookup"><span data-stu-id="7c4ad-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "meer informatie over de metagegevens van de integratie-account")
* [<span data-ttu-id="7c4ad-148">B2B-berichten</span><span class="sxs-lookup"><span data-stu-id="7c4ad-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "meer informatie over het bewaken van B2B-berichten")
* [<span data-ttu-id="7c4ad-149">B2B-berichten in de OMS-portal bijhouden</span><span class="sxs-lookup"><span data-stu-id="7c4ad-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "meer informatie over het bijhouden van B2B-berichten in de OMS-portal")

