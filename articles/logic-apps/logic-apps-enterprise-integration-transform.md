---
title: aaaConvert XML-gegevens met transformaties - Azure Logic Apps | Microsoft Docs
description: Maken van transformaties of mapps tooconvert XML-gegevens tussen indelingen in logic apps met behulp van Hallo Enterprise Integration-SDK
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="8647e-103">Enterprise-integratie met XML-transformaties</span><span class="sxs-lookup"><span data-stu-id="8647e-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="8647e-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8647e-104">Overview</span></span>
<span data-ttu-id="8647e-105">Hallo Enterprise integration transformatie connector worden gegevens van de ene indeling tooanother indeling geconverteerd.</span><span class="sxs-lookup"><span data-stu-id="8647e-105">hello Enterprise integration Transform connector converts data from one format tooanother format.</span></span> <span data-ttu-id="8647e-106">Bijvoorbeeld wellicht hebt u een binnenkomend bericht Hallo met huidige datum in Hallo YearMonthDay indeling.</span><span class="sxs-lookup"><span data-stu-id="8647e-106">For example, you may have an incoming message that contains hello current date in hello YearMonthDay format.</span></span> <span data-ttu-id="8647e-107">U kunt een transformatie tooreformat Hallo datum toobe hello MonthDayYear indeling.</span><span class="sxs-lookup"><span data-stu-id="8647e-107">You can use a transform tooreformat hello date toobe in hello MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="8647e-108">Wat is een transformatie?</span><span class="sxs-lookup"><span data-stu-id="8647e-108">What does a transform do?</span></span>
<span data-ttu-id="8647e-109">Een transformatie die ook wel bekend als een kaart, bestaat uit een bron-XML-schema (hello invoer) en een doel-XML-schema (Hallo uitvoer).</span><span class="sxs-lookup"><span data-stu-id="8647e-109">A Transform, which is also known as a map, consists of a Source XML schema (hello input) and a Target XML schema (hello output).</span></span> <span data-ttu-id="8647e-110">Kunt u verschillende ingebouwde functies toohelp manipuleren of onder uw beheer Hallo gegevens, waaronder tekenreeksmanipulatie, voorwaardelijke toewijzingen, aritmetische expressies, datum tijd formatters en zelfs lussen constructies.</span><span class="sxs-lookup"><span data-stu-id="8647e-110">You can use different built-in functions toohelp manipulate or control hello data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-toocreate-a-transform"></a><span data-ttu-id="8647e-111">Hoe een transformatie toocreate?</span><span class="sxs-lookup"><span data-stu-id="8647e-111">How toocreate a transform?</span></span>
<span data-ttu-id="8647e-112">U kunt een transformatie/map maken met behulp van Visual Studio Hallo [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span><span class="sxs-lookup"><span data-stu-id="8647e-112">You can create a transform/map by using hello Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="8647e-113">Wanneer u bent klaar te maken en te testen Hallo transformatie, moet u Hallo transformatie toegang tot je account integratie uploaden.</span><span class="sxs-lookup"><span data-stu-id="8647e-113">When you are finished creating and testing hello transform, you upload hello transform into your integration account.</span></span> 

## <a name="how-toouse-a-transform"></a><span data-ttu-id="8647e-114">Hoe toouse transformatie</span><span class="sxs-lookup"><span data-stu-id="8647e-114">How toouse a transform</span></span>
<span data-ttu-id="8647e-115">Nadat u Hallo transformatie/kaart naar uw integratie-account uploaden, kunt u deze toocreate een logische app.</span><span class="sxs-lookup"><span data-stu-id="8647e-115">After you upload hello transform/map into your integration account, you can use it toocreate a Logic app.</span></span> <span data-ttu-id="8647e-116">Hallo logische app uitgevoerd uw transformaties wanneer Hallo logische app wordt geactiveerd (en er is invoer inhoud die toobe getransformeerd moet).</span><span class="sxs-lookup"><span data-stu-id="8647e-116">hello Logic app runs your transformations whenever hello Logic app is triggered (and there is input content that needs toobe transformed).</span></span>

<span data-ttu-id="8647e-117">**Hier vindt u Hallo stappen toouse transformatie**:</span><span class="sxs-lookup"><span data-stu-id="8647e-117">**Here are hello steps toouse a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8647e-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8647e-118">Prerequisites</span></span>

* <span data-ttu-id="8647e-119">Een integratie-account maken en toevoegen van een kaart tooit</span><span class="sxs-lookup"><span data-stu-id="8647e-119">Create an integration account and add a map tooit</span></span>  

<span data-ttu-id="8647e-120">Nu u hebt gezorgd voor Hallo vereisten, is het tijd toocreate uw logische app:</span><span class="sxs-lookup"><span data-stu-id="8647e-120">Now that you've taken care of hello prerequisites, it's time toocreate your Logic app:</span></span>  

1. <span data-ttu-id="8647e-121">Een logische app maken en [tooyour integratie account een koppeling](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink een integratie account tooa logische app meer") die Hallo kaart bevat.</span><span class="sxs-lookup"><span data-stu-id="8647e-121">Create a Logic app and [link it tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that contains hello map.</span></span>
2. <span data-ttu-id="8647e-122">Voeg een **aanvragen** trigger tooyour logische app</span><span class="sxs-lookup"><span data-stu-id="8647e-122">Add a **Request** trigger tooyour Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="8647e-123">Hallo toevoegen **XML-transformatie** actie selecteren **een actie toevoegen** </span><span class="sxs-lookup"><span data-stu-id="8647e-123">Add hello **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="8647e-124">Voer Hallo word *transformeren* in Hallo zoeken vak toofilter alle acties toohello een gewenste toouse Hallo</span><span class="sxs-lookup"><span data-stu-id="8647e-124">Enter hello word *transform* in hello search box toofilter all hello actions toohello one that you want toouse</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="8647e-125">Selecteer Hallo **XML-transformatie** actie</span><span class="sxs-lookup"><span data-stu-id="8647e-125">Select hello **Transform XML** action</span></span>   
6. <span data-ttu-id="8647e-126">Hallo XML toevoegen **inhoud** die u transformeren.</span><span class="sxs-lookup"><span data-stu-id="8647e-126">Add hello XML **CONTENT** that you transform.</span></span> <span data-ttu-id="8647e-127">U kunt een XML-gegevens die u in Hallo HTTP-aanvraag als Hallo ontvangt **inhoud**.</span><span class="sxs-lookup"><span data-stu-id="8647e-127">You can use any XML data you receive in hello HTTP request as hello **CONTENT**.</span></span> <span data-ttu-id="8647e-128">Selecteer in dit voorbeeld Hallo hoofdtekst van Hallo HTTP-aanvraag die Hallo logische app heeft geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="8647e-128">In this example, select hello body of hello HTTP request that triggered hello Logic app.</span></span>
7. <span data-ttu-id="8647e-129">Selecteer Hallo-naam van Hallo **kaart** die u wilt dat toouse tooperform Hallo transformatie.</span><span class="sxs-lookup"><span data-stu-id="8647e-129">Select hello name of hello **MAP** that you want toouse tooperform hello transformation.</span></span> <span data-ttu-id="8647e-130">Hallo-kaart moet al in uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="8647e-130">hello map must already be in your integration account.</span></span> <span data-ttu-id="8647e-131">In een eerdere stap hebt u al uw logische app access tooyour integratie-account dat de kaart bevat gegeven.</span><span class="sxs-lookup"><span data-stu-id="8647e-131">In an earlier step, you already gave your Logic app access tooyour integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="8647e-132">Sla uw werk</span><span class="sxs-lookup"><span data-stu-id="8647e-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="8647e-133">Op dit moment bent u klaar instellen van de kaart.</span><span class="sxs-lookup"><span data-stu-id="8647e-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="8647e-134">U kunt in een toepassing concrete toostore Hallo getransformeerd gegevens in een LOB-toepassing zoals SalesForce.</span><span class="sxs-lookup"><span data-stu-id="8647e-134">In a real world application, you may want toostore hello transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="8647e-135">U kunt eenvoudig als actie toosend Hallo uitvoer Hallo tooSalesforce transformeren.</span><span class="sxs-lookup"><span data-stu-id="8647e-135">You can easily as an action toosend hello output of hello transform tooSalesforce.</span></span> 

<span data-ttu-id="8647e-136">U kunt nu de transformatie testen door het maken van een aanvraag toohello HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8647e-136">You can now test your transform by making a request toohello HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="8647e-137">Functies en gebruiksvoorbeelden</span><span class="sxs-lookup"><span data-stu-id="8647e-137">Features and use cases</span></span>
* <span data-ttu-id="8647e-138">Hallo-transformatie die zijn gemaakt in een kaart kan eenvoudig, zoals het kopiëren van een naam en adres van een document tooanother zijn.</span><span class="sxs-lookup"><span data-stu-id="8647e-138">hello transformation created in a map can be simple, such as copying a name and address from one document tooanother.</span></span> <span data-ttu-id="8647e-139">Of u complexere transformaties Hallo out-of-the-box-kaart bewerkingen kunt maken.</span><span class="sxs-lookup"><span data-stu-id="8647e-139">Or, you can create more complex transformations using hello out-of-the-box map operations.</span></span>  
* <span data-ttu-id="8647e-140">Meerdere bewerkingen van de kaart of functies zijn direct beschikbaar is, met inbegrip van tekenreeksen, Datum tijdfuncties, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="8647e-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="8647e-141">U kunt een kopie van de gegevens direct tussen Hallo schema's kunt doen.</span><span class="sxs-lookup"><span data-stu-id="8647e-141">You can do a direct data copy between hello schemas.</span></span> <span data-ttu-id="8647e-142">In Hallo die toewijzen in Hallo SDK is opgenomen, is dit net zo eenvoudig als een lijn die Hallo-elementen in Hallo gegevensbronschema regenereren met hun collega's in doelschema Hallo verbindt.</span><span class="sxs-lookup"><span data-stu-id="8647e-142">In hello Mapper included in hello SDK, this is as simple as drawing a line that connects hello elements in hello source schema with their counterparts in hello destination schema.</span></span>  
* <span data-ttu-id="8647e-143">Wanneer u een toewijzing maakt, weergave u een grafische van Hallo-kaart, waarin alle Hallo relaties en koppelingen die u maakt.</span><span class="sxs-lookup"><span data-stu-id="8647e-143">When creating a map, you view a graphical representation of hello map, which shows all hello relationships and links you create.</span></span>
* <span data-ttu-id="8647e-144">Hallo Test kaart functie tooadd een bericht van de XML-voorbeeld gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8647e-144">Use hello Test Map feature tooadd a sample XML message.</span></span> <span data-ttu-id="8647e-145">U kunt met een enkele klik Hallo kaart hebt gemaakt Zie Hallo gegenereerde uitvoer testen.</span><span class="sxs-lookup"><span data-stu-id="8647e-145">With a simple click, you can test hello map you created, and see hello generated output.</span></span>  
* <span data-ttu-id="8647e-146">Bestaande maps uploaden</span><span class="sxs-lookup"><span data-stu-id="8647e-146">Upload existing maps</span></span>  
* <span data-ttu-id="8647e-147">Biedt ondersteuning voor Hallo XML-indeling.</span><span class="sxs-lookup"><span data-stu-id="8647e-147">Includes support for hello XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="8647e-148">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="8647e-148">Learn more</span></span>
* [<span data-ttu-id="8647e-149">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="8647e-149">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")  
* [<span data-ttu-id="8647e-150">Meer informatie over maps</span><span class="sxs-lookup"><span data-stu-id="8647e-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "meer informatie over enterprise integration maps")  

