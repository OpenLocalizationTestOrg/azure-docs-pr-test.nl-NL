---
title: aaaTransform XML met maps XSLT - Azure Logic Apps | Microsoft Docs
description: XSLT tootransform XML-gegevens met Azure Logic Apps en Enterprise Integration Pack Hallo toewijst toevoegen
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="24d84-103">Toewijzingen voor transformatie van XML-gegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="24d84-103">Add maps for XML data transform</span></span>

<span data-ttu-id="24d84-104">Enterprise integration maakt gebruik van maps tootransform XML-gegevens tussen indelingen.</span><span class="sxs-lookup"><span data-stu-id="24d84-104">Enterprise integration uses maps tootransform XML data between formats.</span></span> <span data-ttu-id="24d84-105">Een kaart is een XML-document dat wordt gedefinieerd op Hallo gegevens in een document dat moet worden omgezet in een andere indeling.</span><span class="sxs-lookup"><span data-stu-id="24d84-105">A map is an XML document that defines hello data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="24d84-106">Waarom maps gebruiken?</span><span class="sxs-lookup"><span data-stu-id="24d84-106">Why use maps?</span></span>

<span data-ttu-id="24d84-107">Stel dat u regelmatig ontvangt B2B orders of facturen van een klant die Hallo YYYMMDD indeling voor datums gebruikt.</span><span class="sxs-lookup"><span data-stu-id="24d84-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses hello YYYMMDD format for dates.</span></span> <span data-ttu-id="24d84-108">Echter in uw organisatie slaat u datums Hallo MMDDYYY indeling.</span><span class="sxs-lookup"><span data-stu-id="24d84-108">However, in your organization, you store dates in hello MMDDYYY format.</span></span> <span data-ttu-id="24d84-109">U kunt een kaart te gebruiken*transformeren* hello YYYMMDD datumnotatie in Hallo MMDDYYY voordat Hallo order of factuur informatie wordt opgeslagen in de database van de activiteit klant.</span><span class="sxs-lookup"><span data-stu-id="24d84-109">You can use a map too*transform* hello YYYMMDD date format into hello MMDDYYY before storing hello order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="24d84-110">Hoe maak ik een kaart</span><span class="sxs-lookup"><span data-stu-id="24d84-110">How do I create a map?</span></span>

<span data-ttu-id="24d84-111">U kunt BizTalk Integration projecten maken met de Hallo [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "meer informatie over Hallo enterprise integration pack") voor Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="24d84-111">You can create BizTalk Integration projects with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="24d84-112">Vervolgens kunt u een Integratiekaart-bestand waarmee u artikelen tussen twee XML-schemabestanden visueel toewijzen.</span><span class="sxs-lookup"><span data-stu-id="24d84-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="24d84-113">Nadat u dit project bouwen, hebt u een XSLT-document.</span><span class="sxs-lookup"><span data-stu-id="24d84-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="24d84-114">Hoe kan ik een kaart toevoegen</span><span class="sxs-lookup"><span data-stu-id="24d84-114">How do I add a map?</span></span>

1. <span data-ttu-id="24d84-115">Selecteer in de Azure-portal hello, **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="24d84-115">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="24d84-116">Voer in het zoekvak Hallo-filter, **integratie**, selecteer daarna **Integratieaccounts** uit de lijst met resultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="24d84-116">In hello filter search box, enter **integration**, then select **Integration Accounts** from hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="24d84-117">Hallo-integratie account waar u tooadd Hallo kaart wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="24d84-117">Select hello integration account where you want tooadd hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="24d84-118">Selecteer Hallo **Maps** tegel.</span><span class="sxs-lookup"><span data-stu-id="24d84-118">Select hello **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="24d84-119">Nadat het Hallo Maps blade wordt geopend, kiest u **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="24d84-119">After hello Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="24d84-120">Voer een **naam** voor uw kaart.</span><span class="sxs-lookup"><span data-stu-id="24d84-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="24d84-121">tooupload hello kaart bestand, kies Hallo mappictogram aan de rechterkant Hallo Hallo **kaart** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="24d84-121">tooupload hello map file, choose hello folder icon on hello right side of hello **Map** text box.</span></span> <span data-ttu-id="24d84-122">Nadat het uploadproces Hallo is voltooid, kiest u **OK**.</span><span class="sxs-lookup"><span data-stu-id="24d84-122">After hello upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="24d84-123">Nadat u Azure Hallo kaart tooyour integratie account toevoegt, krijgen het bericht op het scherm waarin u of uw toewijzingsbestand of niet is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="24d84-123">After Azure adds hello map tooyour integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="24d84-124">Nadat u dit bericht ontvangt, kiest u Hallo **Maps** tegel zodat u kunt nieuwe Hallo bekijken toewijzing toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="24d84-124">After you get this message, choose hello **Maps** tile so you can view hello newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="24d84-125">Hoe kan ik een kaart bewerken?</span><span class="sxs-lookup"><span data-stu-id="24d84-125">How do I edit a map?</span></span>

<span data-ttu-id="24d84-126">U moet een nieuwe toewijzingsbestand met Hallo-wijzigingen die u wilt uploaden.</span><span class="sxs-lookup"><span data-stu-id="24d84-126">You must upload a new map file with hello changes that you want.</span></span> <span data-ttu-id="24d84-127">Hallo-kaart voor bewerken kunt u eerst downloaden.</span><span class="sxs-lookup"><span data-stu-id="24d84-127">You can first download hello map for editing.</span></span>

<span data-ttu-id="24d84-128">tooupload een nieuwe kaart die wordt vervangen door de bestaande toewijzing hello, volg deze stappen.</span><span class="sxs-lookup"><span data-stu-id="24d84-128">tooupload a new map that replaces hello existing map, follow these steps.</span></span>

1. <span data-ttu-id="24d84-129">Kies Hallo **Maps** tegel.</span><span class="sxs-lookup"><span data-stu-id="24d84-129">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="24d84-130">Nadat het Hallo Maps blade wordt geopend, selecteert u dat u wilt dat tooedit Hallo-kaart.</span><span class="sxs-lookup"><span data-stu-id="24d84-130">After hello Maps blade opens, select hello map that you want tooedit.</span></span>

3. <span data-ttu-id="24d84-131">Op Hallo **Maps** blade kiezen **Update**.</span><span class="sxs-lookup"><span data-stu-id="24d84-131">On hello **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="24d84-132">Selecteer in de bestandskiezer hello, Hallo toewijzingsbestand dat u wilt dat tooupload en selecteer **Open**.</span><span class="sxs-lookup"><span data-stu-id="24d84-132">In hello file picker, select hello map file that you want tooupload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a><span data-ttu-id="24d84-133">Hoe een kaart toodelete?</span><span class="sxs-lookup"><span data-stu-id="24d84-133">How toodelete a map?</span></span>

1. <span data-ttu-id="24d84-134">Kies Hallo **Maps** tegel.</span><span class="sxs-lookup"><span data-stu-id="24d84-134">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="24d84-135">Nadat Hallo Maps blade wordt geopend, selecteert u de gewenste toodelete Hallo-kaart.</span><span class="sxs-lookup"><span data-stu-id="24d84-135">After hello Maps blade opens, select hello map you want toodelete.</span></span>

3. <span data-ttu-id="24d84-136">Kies **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="24d84-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="24d84-137">U wilt bevestigen dat toodelete Hallo-kaart.</span><span class="sxs-lookup"><span data-stu-id="24d84-137">Confirm that you want toodelete hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="24d84-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="24d84-138">Next Steps</span></span>
* [<span data-ttu-id="24d84-139">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="24d84-139">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")  
* [<span data-ttu-id="24d84-140">Meer informatie over de overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="24d84-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  
* [<span data-ttu-id="24d84-141">Meer informatie over transformaties</span><span class="sxs-lookup"><span data-stu-id="24d84-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "meer informatie over enterprise integration-transformaties")  

