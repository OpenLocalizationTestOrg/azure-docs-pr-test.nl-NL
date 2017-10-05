---
title: Integratie account artefact metagegevens - Azure Logic Apps beheren | Microsoft Docs
description: Toevoegen of artefact metagegevens ophalen uit integratieaccounts voor Azure Logic Apps
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 28bb8296ddd820ec5aa9793dc0928b4b1e67bf6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="8a9f7-103">De metagegevens van de artefacten in integratieaccounts voor logic apps beheren</span><span class="sxs-lookup"><span data-stu-id="8a9f7-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="8a9f7-104">U kunt aangepaste metagegevens voor artefacten in integratieaccounts definiëren en ophalen van metagegevens tijdens de runtime voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="8a9f7-105">Bijvoorbeeld, kunt u metagegevens voor artefacten zoals partners, overeenkomsten, schema's en maps - alle sleutelwaarde-paren met metagegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="8a9f7-106">Op dit moment artefacten metagegevens via de gebruikersinterface kunnen niet worden gemaakt, maar u kunt REST-API's gebruiken voor het maken van metagegevens.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata.</span></span> <span data-ttu-id="8a9f7-107">Om toe te voegen metagegevens wanneer u maakt of selecteert u een partner, een overeenkomst of een schema in de Azure-portal, kies **bewerken als JSON**.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-107">To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="8a9f7-108">Voor het ophalen van metagegevens van het artefact in logic apps, kunt u de functie Integratie Account artefact opzoeken.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-108">To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a><span data-ttu-id="8a9f7-109">Metagegevens toevoegen aan artefacten in integratieaccounts</span><span class="sxs-lookup"><span data-stu-id="8a9f7-109">Add metadata to artifacts in integration accounts</span></span>

1. <span data-ttu-id="8a9f7-110">Maak een [integratie account](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="8a9f7-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="8a9f7-111">Voeg bijvoorbeeld een artefact toe aan uw account integratie, een [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [overeenkomst](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), of [schema](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="8a9f7-111">Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="8a9f7-112">Selecteer het artefact, kies **bewerken als JSON**, en voer de details van de metagegevens.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-112">Select the artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Voer de metagegevens](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="8a9f7-114">Ophalen van metagegevens van artefacten voor logic apps</span><span class="sxs-lookup"><span data-stu-id="8a9f7-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="8a9f7-115">Maak een [logische app](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8a9f7-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="8a9f7-116">Maak een [koppeling van uw logische app naar uw account integratie](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="8a9f7-116">Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="8a9f7-117">In Logic App-ontwerper, voegt u een trigger zoals *aanvragen* of *HTTP* aan uw logische app.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-117">In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.</span></span>

4.  <span data-ttu-id="8a9f7-118">Kies **doornemen** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="8a9f7-119">Zoeken naar *integratie* zodat u kunt zoeken naar en selecteer vervolgens **integratie Account - integratie Account artefact Lookup**.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Selecteer integratie Account artefact Lookup](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="8a9f7-121">Selecteer de **artefact Type**, en geef de **artefact naam**.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-121">Select the **Artifact Type**, and provide the **Artifact Name**.</span></span>

    ![Selecteer artefact type en geef de naam van het artefact](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="8a9f7-123">Voorbeeld: Ophalen partner metagegevens</span><span class="sxs-lookup"><span data-stu-id="8a9f7-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="8a9f7-124">Partner metagegevens bevat deze `routingUrl` details:</span><span class="sxs-lookup"><span data-stu-id="8a9f7-124">Partner metadata has these `routingUrl` details:</span></span>

![Partner 'routingURL' metagegevens vinden](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="8a9f7-126">Voeg de trigger in uw logische app, een **integratie Account - integratie Account artefact Lookup** actie voor uw partner en een **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Trigger, artefacten opzoeken en 'HTTP' toevoegen aan uw logische app](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="8a9f7-128">Voor het ophalen van de URI, gaat u naar de codeweergave voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="8a9f7-128">To retrieve the URI, go to Code View for your logic app.</span></span> <span data-ttu-id="8a9f7-129">De definitie van de logische app moet eruitzien als in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8a9f7-129">Your logic app definition should look like this example:</span></span>

    ![Zoeken zoeken](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="8a9f7-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a9f7-131">Next steps</span></span>
* [<span data-ttu-id="8a9f7-132">Meer informatie over de overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="8a9f7-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  
