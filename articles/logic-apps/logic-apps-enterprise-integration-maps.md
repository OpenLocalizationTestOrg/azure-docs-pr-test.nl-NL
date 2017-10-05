---
title: XML transformeren met maps XSLT - Azure Logic Apps | Microsoft Docs
description: XSLT toegewezen voor het transformeren van XML-gegevens met Azure Logic Apps en de Enterprise Integration Pack toevoegen
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
ms.openlocfilehash: 4445a84a6c6425110e7d705019a28b5cc5447046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="1fcf1-103">Toewijzingen voor transformatie van XML-gegevens toevoegen</span><span class="sxs-lookup"><span data-stu-id="1fcf1-103">Add maps for XML data transform</span></span>

<span data-ttu-id="1fcf1-104">Enterprise-integratie gebruikt kaarten voor het transformeren van XML-gegevens tussen indelingen.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-104">Enterprise integration uses maps to transform XML data between formats.</span></span> <span data-ttu-id="1fcf1-105">Een kaart is een XML-document waarin de gegevens in een document dat moet worden omgezet in een andere indeling.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="1fcf1-106">Waarom maps gebruiken?</span><span class="sxs-lookup"><span data-stu-id="1fcf1-106">Why use maps?</span></span>

<span data-ttu-id="1fcf1-107">Stel dat u regelmatig ontvangt B2B orders of facturen van een klant die de indeling YYYMMDD voor datums gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span></span> <span data-ttu-id="1fcf1-108">Echter in uw organisatie slaat u datums in de indeling MMDDYYY.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-108">However, in your organization, you store dates in the MMDDYYY format.</span></span> <span data-ttu-id="1fcf1-109">U kunt een kaart om te gebruiken *transformeren* de datumnotatie YYYMMDD in de MMDDYYY voordat de details van de order of factuur wordt opgeslagen in de database van de activiteit klant.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="1fcf1-110">Hoe maak ik een kaart</span><span class="sxs-lookup"><span data-stu-id="1fcf1-110">How do I create a map?</span></span>

<span data-ttu-id="1fcf1-111">Kunt u de projecten BizTalk-integratie met de [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "meer informatie over het enterprise-integratiepakket") voor Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="1fcf1-112">Vervolgens kunt u een Integratiekaart-bestand waarmee u artikelen tussen twee XML-schemabestanden visueel toewijzen.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="1fcf1-113">Nadat u dit project bouwen, hebt u een XSLT-document.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="1fcf1-114">Hoe kan ik een kaart toevoegen</span><span class="sxs-lookup"><span data-stu-id="1fcf1-114">How do I add a map?</span></span>

1. <span data-ttu-id="1fcf1-115">Selecteer in de Azure-portal **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-115">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="1fcf1-116">Voer in het zoekvak filter **integratie**, selecteer daarna **Integratieaccounts** uit de lijst met resultaten.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-116">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="1fcf1-117">Selecteer het integratie account waar u toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-117">Select the integration account where you want to add the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="1fcf1-118">Selecteer de **Maps** tegel.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-118">Select the **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="1fcf1-119">Nadat de Maps-blade wordt geopend, kiest u **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-119">After the Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="1fcf1-120">Voer een **naam** voor uw kaart.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="1fcf1-121">Kies het pictogram van de map aan de rechterkant van de kaart om bestand te uploaden, de **kaart** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-121">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span></span> <span data-ttu-id="1fcf1-122">Nadat het uploadproces is voltooid, kiest u **OK**.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-122">After the upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="1fcf1-123">Nadat de kaart Azure aan uw account integratie toevoegt, krijgen het bericht op het scherm waarin u of uw toewijzingsbestand of niet is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-123">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="1fcf1-124">Nadat u dit bericht ontvangt, kiest u de **Maps** tegel zodat u de zojuist toegevoegde kaart kunt bekijken.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-124">After you get this message, choose the **Maps** tile so you can view the newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="1fcf1-125">Hoe kan ik een kaart bewerken?</span><span class="sxs-lookup"><span data-stu-id="1fcf1-125">How do I edit a map?</span></span>

<span data-ttu-id="1fcf1-126">U moet een nieuwe kaart-bestand met de wijzigingen die u wilt uploaden.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-126">You must upload a new map file with the changes that you want.</span></span> <span data-ttu-id="1fcf1-127">U kunt de kaart voor het bewerken van eerst downloaden.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-127">You can first download the map for editing.</span></span>

<span data-ttu-id="1fcf1-128">Volg deze stappen voor het uploaden van een nieuwe kaart die wordt vervangen door de bestaande toewijzing.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-128">To upload a new map that replaces the existing map, follow these steps.</span></span>

1. <span data-ttu-id="1fcf1-129">Kies de **Maps** tegel.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-129">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="1fcf1-130">Nadat de Maps-blade wordt geopend, selecteert u de toewijzing die u wilt bewerken.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-130">After the Maps blade opens, select the map that you want to edit.</span></span>

3. <span data-ttu-id="1fcf1-131">Op de **Maps** blade kiezen **Update**.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-131">On the **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="1fcf1-132">Selecteer het toewijzingsbestand die u wilt uploaden en selecteer vervolgens in de bestandskiezer **Open**.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-132">In the file picker, select the map file that you want to upload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-to-delete-a-map"></a><span data-ttu-id="1fcf1-133">Het verwijderen van een kaart?</span><span class="sxs-lookup"><span data-stu-id="1fcf1-133">How to delete a map?</span></span>

1. <span data-ttu-id="1fcf1-134">Kies de **Maps** tegel.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-134">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="1fcf1-135">Nadat de Maps-blade wordt geopend, selecteert u de kaart die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-135">After the Maps blade opens, select the map you want to delete.</span></span>

3. <span data-ttu-id="1fcf1-136">Kies **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="1fcf1-137">Bevestig dat u wilt verwijderen van de kaart.</span><span class="sxs-lookup"><span data-stu-id="1fcf1-137">Confirm that you want to delete the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="1fcf1-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1fcf1-138">Next Steps</span></span>
* [<span data-ttu-id="1fcf1-139">Meer informatie over het Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="1fcf1-139">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")  
* [<span data-ttu-id="1fcf1-140">Meer informatie over de overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="1fcf1-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  
* [<span data-ttu-id="1fcf1-141">Meer informatie over transformaties</span><span class="sxs-lookup"><span data-stu-id="1fcf1-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "meer informatie over enterprise integration-transformaties")  

