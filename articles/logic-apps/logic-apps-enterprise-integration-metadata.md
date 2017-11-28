---
title: aaaManage integratie artefact metagegevens - account Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="5e64a-103">De metagegevens van de artefacten in integratieaccounts voor logic apps beheren</span><span class="sxs-lookup"><span data-stu-id="5e64a-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="5e64a-104">U kunt aangepaste metagegevens voor artefacten in integratieaccounts definiëren en ophalen van metagegevens tijdens de runtime voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="5e64a-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="5e64a-105">Bijvoorbeeld, kunt u metagegevens voor artefacten zoals partners, overeenkomsten, schema's en maps - alle sleutelwaarde-paren met metagegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="5e64a-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="5e64a-106">Momenteel artefacten metagegevens via de gebruikersinterface kunnen niet worden gemaakt, maar u kunt met behulp van REST-API's toocreate metagegevens.</span><span class="sxs-lookup"><span data-stu-id="5e64a-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs toocreate metadata.</span></span> <span data-ttu-id="5e64a-107">tooadd metagegevens wanneer u maakt of selecteert u een partner, een overeenkomst of een schema in hello Azure-portal, kies **bewerken als JSON**.</span><span class="sxs-lookup"><span data-stu-id="5e64a-107">tooadd metadata when you create or select a partner, agreement, or schema in hello Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="5e64a-108">tooretrieve artefact metagegevens in logic apps, kunt u Hallo integratie Account artefact Lookup-functie.</span><span class="sxs-lookup"><span data-stu-id="5e64a-108">tooretrieve artifact metadata in logic apps, you can use hello Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a><span data-ttu-id="5e64a-109">Metagegevens tooartifacts in integratieaccounts toevoegen</span><span class="sxs-lookup"><span data-stu-id="5e64a-109">Add metadata tooartifacts in integration accounts</span></span>

1. <span data-ttu-id="5e64a-110">Maak een [integratie account](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="5e64a-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="5e64a-111">Toevoegen van een artefact tooyour integratie-account, bijvoorbeeld, een [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [overeenkomst](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), of [schema](logic-apps-enterprise-integration-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="5e64a-111">Add an artifact tooyour integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="5e64a-112">Hallo artefact selecteert, kiest u **bewerken als JSON**, en voer de details van de metagegevens.</span><span class="sxs-lookup"><span data-stu-id="5e64a-112">Select hello artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![Voer de metagegevens](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="5e64a-114">Ophalen van metagegevens van artefacten voor logic apps</span><span class="sxs-lookup"><span data-stu-id="5e64a-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="5e64a-115">Maak een [logische app](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5e64a-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="5e64a-116">Maak een [koppeling van uw logische app tooyour integratie account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span><span class="sxs-lookup"><span data-stu-id="5e64a-116">Create a [link from your logic app tooyour integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="5e64a-117">In Logic App-ontwerper, voegt u een trigger zoals *aanvragen* of *HTTP* tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="5e64a-117">In Logic App Designer, add a trigger like *Request* or *HTTP* tooyour logic app.</span></span>

4.  <span data-ttu-id="5e64a-118">Kies **doornemen** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5e64a-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="5e64a-119">Zoeken naar *integratie* zodat u kunt zoeken naar en selecteer vervolgens **integratie Account - integratie Account artefact Lookup**.</span><span class="sxs-lookup"><span data-stu-id="5e64a-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![Selecteer integratie Account artefact Lookup](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="5e64a-121">Selecteer Hallo **artefact Type**, en geef Hallo **artefact naam**.</span><span class="sxs-lookup"><span data-stu-id="5e64a-121">Select hello **Artifact Type**, and provide hello **Artifact Name**.</span></span>

    ![Selecteer artefact type en geef de naam van het artefact](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="5e64a-123">Voorbeeld: Ophalen partner metagegevens</span><span class="sxs-lookup"><span data-stu-id="5e64a-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="5e64a-124">Partner metagegevens bevat deze `routingUrl` details:</span><span class="sxs-lookup"><span data-stu-id="5e64a-124">Partner metadata has these `routingUrl` details:</span></span>

![Partner 'routingURL' metagegevens vinden](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="5e64a-126">Voeg de trigger in uw logische app, een **integratie Account - integratie Account artefact Lookup** actie voor uw partner en een **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="5e64a-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![Trigger, artefacten opzoeken en 'HTTP' tooyour logische app toevoegen](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="5e64a-128">tooretrieve hello URI, gaat u tooCode weergeven voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="5e64a-128">tooretrieve hello URI, go tooCode View for your logic app.</span></span> <span data-ttu-id="5e64a-129">De definitie van de logische app moet eruitzien als in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5e64a-129">Your logic app definition should look like this example:</span></span>

    ![Zoeken zoeken](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="5e64a-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e64a-131">Next steps</span></span>
* [<span data-ttu-id="5e64a-132">Meer informatie over de overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="5e64a-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  
