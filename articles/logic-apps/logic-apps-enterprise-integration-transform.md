---
title: Converteren van XML-gegevens met transformaties - Azure Logic Apps | Microsoft Docs
description: Maken van transformaties of mapps converteren van XML-gegevens tussen indelingen in logic apps met behulp van de Enterprise Integration-SDK
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
ms.openlocfilehash: fb6027769377b3527b11f7831dab3bb8d7061c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="4e0bb-103">Enterprise-integratie met XML-transformaties</span><span class="sxs-lookup"><span data-stu-id="4e0bb-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="4e0bb-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4e0bb-104">Overview</span></span>
<span data-ttu-id="4e0bb-105">De Enterprise integration transformatie-connector worden gegevens van de ene indeling geconverteerd naar een andere indeling.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-105">The Enterprise integration Transform connector converts data from one format to another format.</span></span> <span data-ttu-id="4e0bb-106">Bijvoorbeeld wellicht hebt u een binnenkomend bericht met de huidige datum in de notatie YearMonthDay.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-106">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span></span> <span data-ttu-id="4e0bb-107">U kunt een transformatie opnieuw indelen van de datum in de indeling MonthDayYear.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-107">You can use a transform to reformat the date to be in the MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="4e0bb-108">Wat is een transformatie?</span><span class="sxs-lookup"><span data-stu-id="4e0bb-108">What does a transform do?</span></span>
<span data-ttu-id="4e0bb-109">Een transformatie die ook wel bekend als een kaart, bestaat uit een bron-XML-schema (invoer) en een doel-XML-schema (uitvoer).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-109">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span></span> <span data-ttu-id="4e0bb-110">U kunt verschillende ingebouwde functies gebruiken om te bewerken of beheren van de gegevens, waaronder tekenreeksmanipulatie, voorwaardelijke toewijzingen, aritmetische expressies, datum tijd formatters en zelfs lussen constructies.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-110">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-to-create-a-transform"></a><span data-ttu-id="4e0bb-111">Het maken van een transformatie?</span><span class="sxs-lookup"><span data-stu-id="4e0bb-111">How to create a transform?</span></span>
<span data-ttu-id="4e0bb-112">U kunt een transformatie/map maken met behulp van de Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-112">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="4e0bb-113">Als u klaar maken en testen van de transformatie bent, moet u de transformatie toegang tot je account integratie uploaden.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-113">When you are finished creating and testing the transform, you upload the transform into your integration account.</span></span> 

## <a name="how-to-use-a-transform"></a><span data-ttu-id="4e0bb-114">Het gebruik van een transformatie</span><span class="sxs-lookup"><span data-stu-id="4e0bb-114">How to use a transform</span></span>
<span data-ttu-id="4e0bb-115">Nadat u de transformatie/kaart bij uw account integratie geüpload, kunt u het maken van een logische app.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-115">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span></span> <span data-ttu-id="4e0bb-116">De logische app wordt uw transformaties uitgevoerd wanneer de logische app wordt geactiveerd (en er is invoer inhoud die moet worden omgezet).</span><span class="sxs-lookup"><span data-stu-id="4e0bb-116">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span></span>

<span data-ttu-id="4e0bb-117">**Hier volgen de stappen voor het gebruik van een transformatie**:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-117">**Here are the steps to use a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4e0bb-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4e0bb-118">Prerequisites</span></span>

* <span data-ttu-id="4e0bb-119">Een integratie-account maken en een toewijzing aan toe te voegen</span><span class="sxs-lookup"><span data-stu-id="4e0bb-119">Create an integration account and add a map to it</span></span>  

<span data-ttu-id="4e0bb-120">Nu dat u hebt gezorgd voor de vereisten, is het tijd om uw logische app maken:</span><span class="sxs-lookup"><span data-stu-id="4e0bb-120">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span></span>  

1. <span data-ttu-id="4e0bb-121">Een logische app maken en [koppelen aan uw account integratie](../logic-apps/logic-apps-enterprise-integration-accounts.md "informatie over het koppelen van een integratie-account aan een logische app") die de kaart bevat.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-121">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span></span>
2. <span data-ttu-id="4e0bb-122">Voeg een **aanvragen** trigger aan uw logische app</span><span class="sxs-lookup"><span data-stu-id="4e0bb-122">Add a **Request** trigger to your Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="4e0bb-123">Toevoegen de **XML-transformatie** actie selecteren **een actie toevoegen** </span><span class="sxs-lookup"><span data-stu-id="4e0bb-123">Add the **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="4e0bb-124">Voer het woord *transformeren* in het zoekvak voor het filteren van de acties met de fout die u wilt gebruiken</span><span class="sxs-lookup"><span data-stu-id="4e0bb-124">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="4e0bb-125">Selecteer de **XML-transformatie** actie</span><span class="sxs-lookup"><span data-stu-id="4e0bb-125">Select the **Transform XML** action</span></span>   
6. <span data-ttu-id="4e0bb-126">Voeg het XML-bestand **inhoud** die u transformeren.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-126">Add the XML **CONTENT** that you transform.</span></span> <span data-ttu-id="4e0bb-127">U in de HTTP-aanvraag als ontvangt XML-gegevens kunt u de **inhoud**.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-127">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span></span> <span data-ttu-id="4e0bb-128">Selecteer de hoofdtekst van de HTTP-aanvraag die de logische app heeft geactiveerd in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-128">In this example, select the body of the HTTP request that triggered the Logic app.</span></span>
7. <span data-ttu-id="4e0bb-129">Selecteer de naam van de **kaart** dat u gebruiken wilt voor het uitvoeren van de transformatie.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-129">Select the name of the **MAP** that you want to use to perform the transformation.</span></span> <span data-ttu-id="4e0bb-130">De kaart moet al in uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-130">The map must already be in your integration account.</span></span> <span data-ttu-id="4e0bb-131">In een eerdere stap hebt u al gegeven uw logische apptoegang tot je account integratie met uw kaart.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-131">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="4e0bb-132">Sla uw werk</span><span class="sxs-lookup"><span data-stu-id="4e0bb-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="4e0bb-133">Op dit moment bent u klaar instellen van de kaart.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="4e0bb-134">In een toepassing praktijk wilt u mogelijk de getransformeerde gegevens opslaan in een LOB-toepassing zoals SalesForce.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-134">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="4e0bb-135">U kunt gemakkelijk als een actie voor het verzenden van de uitvoer van de transformatie bij Salesforce.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-135">You can easily as an action to send the output of the transform to Salesforce.</span></span> 

<span data-ttu-id="4e0bb-136">U kunt nu de transformatie testen door een aanvraag voor het HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-136">You can now test your transform by making a request to the HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="4e0bb-137">Functies en gebruiksvoorbeelden</span><span class="sxs-lookup"><span data-stu-id="4e0bb-137">Features and use cases</span></span>
* <span data-ttu-id="4e0bb-138">De transformatie die wordt gemaakt in een map is eenvoudig, zoals het kopiëren van een naam en adres van het ene document naar de andere.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-138">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span></span> <span data-ttu-id="4e0bb-139">Of u complexere transformaties met behulp van de kaart out-of-the-box-bewerkingen kunt maken.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-139">Or, you can create more complex transformations using the out-of-the-box map operations.</span></span>  
* <span data-ttu-id="4e0bb-140">Meerdere bewerkingen van de kaart of functies zijn direct beschikbaar is, met inbegrip van tekenreeksen, Datum tijdfuncties, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="4e0bb-141">U kunt een kopie van de directe gegevens tussen de schema's kunt doen.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-141">You can do a direct data copy between the schemas.</span></span> <span data-ttu-id="4e0bb-142">In de Mapper die deel uitmaakt van de SDK is net zo eenvoudig als het tekenen van een regel die de elementen in het schema van de gegevensbron met hun collega's in het doelschema verbindt.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-142">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span></span>  
* <span data-ttu-id="4e0bb-143">Wanneer u een toewijzing maakt, weergave u een grafische van de kaart, waarin de relaties en koppelingen die u maakt.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-143">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span></span>
* <span data-ttu-id="4e0bb-144">Gebruik de functie Test-kaart toevoegen van een bericht van de XML-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-144">Use the Test Map feature to add a sample XML message.</span></span> <span data-ttu-id="4e0bb-145">U kunt met een enkele klik testen van de kaart die u hebt gemaakt en verschijnt de gegenereerde uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-145">With a simple click, you can test the map you created, and see the generated output.</span></span>  
* <span data-ttu-id="4e0bb-146">Bestaande maps uploaden</span><span class="sxs-lookup"><span data-stu-id="4e0bb-146">Upload existing maps</span></span>  
* <span data-ttu-id="4e0bb-147">Biedt ondersteuning voor de XML-indeling.</span><span class="sxs-lookup"><span data-stu-id="4e0bb-147">Includes support for the XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="4e0bb-148">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="4e0bb-148">Learn more</span></span>
* [<span data-ttu-id="4e0bb-149">Meer informatie over het Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="4e0bb-149">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")  
* [<span data-ttu-id="4e0bb-150">Meer informatie over maps</span><span class="sxs-lookup"><span data-stu-id="4e0bb-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "meer informatie over enterprise integration maps")  

