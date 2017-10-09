---
title: aaaWorking met XML-berichten in uw werkstromen - Azure Logic Apps | Microsoft Docs
description: Verwerken, valideren, transformeren en XML verrijken berichten logic apps en het gebruik van zakelijke tooscenarios Enterprise Integration Pack Hallo
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="53a2a-103">Valideren en transformeren XML, coderen en decoderen platte bestanden en verrijken berichten functies in logic apps</span><span class="sxs-lookup"><span data-stu-id="53a2a-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="53a2a-104">Met behulp van logische apps hebt Hallo mogelijkheid tooprocess XML-berichten die u verzendt en ontvangt.</span><span class="sxs-lookup"><span data-stu-id="53a2a-104">Using logic apps, you have hello ability tooprocess XML messages that you send and receive.</span></span> <span data-ttu-id="53a2a-105">Deze functie is opgenomen in de Enterprise Integration Pack Hallo.</span><span class="sxs-lookup"><span data-stu-id="53a2a-105">This feature is included with hello Enterprise Integration Pack.</span></span> <span data-ttu-id="53a2a-106">Voor die gebruikers met een achtergrond BizTalk Server Enterprise Integration Pack Hallo biedt u dezelfde mogelijkheden tootransform en valideren van berichten, werken met platte bestanden, en zelfs XPath tooenrich gebruiken of specifieke eigenschappen ophalen uit een bericht.</span><span class="sxs-lookup"><span data-stu-id="53a2a-106">For those users with a BizTalk Server background, hello Enterprise Integration Pack gives you similar abilities tootransform and validate messages, work with flat files, and even use XPath tooenrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="53a2a-107">Voor gebruikers die nieuwe toothis ruimte zijn, vouw deze functies uit hoe u berichten verwerken binnen uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="53a2a-107">For those users who are new toothis space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="53a2a-108">Bijvoorbeeld, als u zich in een scenario voor business-to-business en met specifieke XML-schema's, werken kunt u Hallo Enterprise Integration Pack tooenhance hoe uw bedrijf deze berichten verwerkt.</span><span class="sxs-lookup"><span data-stu-id="53a2a-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use hello Enterprise Integration Pack tooenhance how your company processes these messages.</span></span> 

<span data-ttu-id="53a2a-109">Hallo Enterprise Integration Pack is omvat:</span><span class="sxs-lookup"><span data-stu-id="53a2a-109">hello Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="53a2a-110">[XML-validatie](logic-apps-enterprise-integration-xml-validation.md "meer informatie over XML-bericht validatie") -valideren van een XML-binnenkomende of uitgaande bericht ten opzichte van een specifieke schema.</span><span class="sxs-lookup"><span data-stu-id="53a2a-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="53a2a-111">[XML-transformatie](../logic-apps/logic-apps-enterprise-integration-transform.md "meer informatie over XML-bericht transformaties en maps") - converteren of aanpassen van een XML-bericht op basis van uw vereisten of Hallo vereisten van een partner.</span><span class="sxs-lookup"><span data-stu-id="53a2a-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or hello requirements of a partner.</span></span>
* <span data-ttu-id="53a2a-112">[Bestand coderen en decoderen van plat bestand platte](logic-apps-enterprise-integration-flatfile.md "meer informatie over een plat bestand-codering/decodering") - coderen of een plat bestand decoderen.</span><span class="sxs-lookup"><span data-stu-id="53a2a-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="53a2a-113">Bijvoorbeeld, SAP accepteert en IDOC bestanden in een plat bestand-indeling verzendt.</span><span class="sxs-lookup"><span data-stu-id="53a2a-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="53a2a-114">Veel integratie platforms maken XML-berichten, inclusief Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="53a2a-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="53a2a-115">U kunt dus een logische app dat gebruikt Hallo plat bestand-encoder te '' XML-bestanden tooflat bestanden converteren maken.</span><span class="sxs-lookup"><span data-stu-id="53a2a-115">So, you can create a logic app that uses hello flat file encoder too"convert" XML files tooflat files.</span></span> 
* <span data-ttu-id="53a2a-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - een bericht Sitmuleren en specifieke eigenschappen ophalen uit het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="53a2a-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from hello message.</span></span> <span data-ttu-id="53a2a-117">U kunt vervolgens gebruik Hallo eigenschappen tooroute Hallo-bericht tooa bestemming, of een tussenliggende eindpunt hebt uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="53a2a-117">You can then use hello extracted properties tooroute hello message tooa destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="53a2a-118">Probeer het</span><span class="sxs-lookup"><span data-stu-id="53a2a-118">Try it out</span></span>
<span data-ttu-id="53a2a-119">[Implementeren van een volledig operationeel logische app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub voorbeeld) met behulp van Hallo XML-functies in Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="53a2a-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using hello XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="53a2a-120">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="53a2a-120">Learn more</span></span>
[<span data-ttu-id="53a2a-121">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="53a2a-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")
