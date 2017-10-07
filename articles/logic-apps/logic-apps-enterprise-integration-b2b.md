---
title: oplossingen voor aaaCreate B2B - Azure Logic Apps | Microsoft Docs
description: Gegevens in logische apps met behulp van Hallo B2B-functies in Enterprise Integration Pack Hallo ontvangen
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a><span data-ttu-id="9f2ee-103">Gegevens in logische apps met Hallo B2B-functies in Enterprise Integration Pack Hallo ontvangen</span><span class="sxs-lookup"><span data-stu-id="9f2ee-103">Receive data in logic apps with hello B2B features in hello Enterprise Integration Pack</span></span>

<span data-ttu-id="9f2ee-104">Nadat u een account voor integratie met partners en overeenkomsten maakt, bent u klaar toocreate een zakelijke toobusiness (B2B)-werkstroom voor uw logische app Hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9f2ee-104">After you create an integration account that has partners and agreements, you are ready toocreate a business toobusiness (B2B) workflow for your logic app with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f2ee-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9f2ee-105">Prerequisites</span></span>

<span data-ttu-id="9f2ee-106">toouse Hallo AS2 en X12 acties, moet u een Enterprise Integration-Account hebben.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-106">toouse hello AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="9f2ee-107">Meer informatie over [hoe toocreate een Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="9f2ee-107">Learn [how toocreate an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="9f2ee-108">Een logische app maken met B2B-connectors</span><span class="sxs-lookup"><span data-stu-id="9f2ee-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="9f2ee-109">Volg deze stappen toocreate een B2B logische app die gebruikmaakt van Hallo AS2 en X12 acties tooreceive gegevens uit een trading partner:</span><span class="sxs-lookup"><span data-stu-id="9f2ee-109">Follow these steps toocreate a B2B logic app that uses hello AS2 and X12 actions tooreceive data from a trading partner:</span></span>

1. <span data-ttu-id="9f2ee-110">Maak een logische app, klikt u vervolgens [Koppel uw app tooyour integratie account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="9f2ee-110">Create a logic app, then [link your app tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="9f2ee-111">Voeg een **aanvraag: wanneer een HTTP-aanvraag wordt ontvangen** trigger tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-111">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="9f2ee-112">Hallo tooadd **decoderen AS2** actie, selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-112">tooadd hello **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="9f2ee-113">toofilter alle acties toohello die u wilt, Voer Hallo word **as2** in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-113">toofilter all actions toohello one that you want, enter hello word **as2** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="9f2ee-114">Selecteer Hallo **AS2 - decoderen AS2-bericht** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-114">Select hello **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="9f2ee-115">Hallo toevoegen **hoofdtekst** dat u wilt dat toouse als invoer.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-115">Add hello **Body** that you want toouse as input.</span></span> <span data-ttu-id="9f2ee-116">Selecteer in dit voorbeeld Hallo hoofdtekst van HTTP-aanvraag Hallo dat triggers Hallo logische app.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-116">In this example, select hello body of hello HTTP request that triggers hello logic app.</span></span> <span data-ttu-id="9f2ee-117">Of typ een expressie die Hallo kopteksten in Hallo-ingangen **HEADERS** veld:</span><span class="sxs-lookup"><span data-stu-id="9f2ee-117">Or enter an expression that inputs hello headers in hello **HEADERS** field:</span></span>

    <span data-ttu-id="9f2ee-118">@triggerOutputs([headers])</span><span class="sxs-lookup"><span data-stu-id="9f2ee-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="9f2ee-119">Hallo vereist toevoegen **Headers** voor AS2, kunt u vinden in de aanvraagheaders Hallo HTTP.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-119">Add hello required **Headers** for AS2, which you can find in hello HTTP request headers.</span></span> <span data-ttu-id="9f2ee-120">In dit voorbeeld Hallo-headers van Hallo HTTP-aanvraag die trigger Hallo logic app selecteren.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-120">In this example, select hello headers of hello HTTP request that trigger hello logic app.</span></span>

8. <span data-ttu-id="9f2ee-121">Nu Hallo decoderen X12 berichtactie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-121">Now add hello Decode X12 message action.</span></span> <span data-ttu-id="9f2ee-122">Selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="9f2ee-123">toofilter alle acties toohello die u wilt, Voer Hallo word **x12** in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-123">toofilter all actions toohello one that you want, enter hello word **x12** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="9f2ee-124">Selecteer Hallo **X12-decoderen X12 bericht** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-124">Select hello **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="9f2ee-125">U moet nu Hallo invoer toothis actie opgeven.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-125">Now you must specify hello input toothis action.</span></span> <span data-ttu-id="9f2ee-126">Deze invoer is Hallo-uitvoer van de vorige AS2-actie Hallo.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-126">This input is hello output from hello previous AS2 action.</span></span>

    <span data-ttu-id="9f2ee-127">inhoud van het werkelijke bericht Hallo is in een JSON-object en is met base64 gecodeerd, dus u een expressie als invoer Hallo opgeven moet.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-127">hello actual message content is in a JSON object and is base64 encoded, so you must specify an expression as hello input.</span></span> 
    <span data-ttu-id="9f2ee-128">Voer Hallo expressie in Hallo na **X12 PLATTE bestand bericht tooDECODE** invoerveld:</span><span class="sxs-lookup"><span data-stu-id="9f2ee-128">Enter hello following expression in hello **X12 FLAT FILE MESSAGE tooDECODE** input field:</span></span>
    
    <span data-ttu-id="9f2ee-129">@base64ToString(body('Decode_AS2_message')? ['AS2Message']? ['Inhoud'])</span><span class="sxs-lookup"><span data-stu-id="9f2ee-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="9f2ee-130">Voeg nu stappen toodecode hello X12 gegevens ontvangen van Hallo trading partner en uitvoer van de items in een JSON-object.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-130">Now add steps toodecode hello X12 data received from hello trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="9f2ee-131">toonotify hello partner die gegevens Hallo is ontvangen, kunt u sturen weer een antwoord met Hallo AS2 bericht Disposition melding (MDN) in een HTTP-antwoord-actie.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-131">toonotify hello partner that hello data was received, you can send back a response containing hello AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="9f2ee-132">Hallo tooadd **antwoord** actie, kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-132">tooadd hello **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="9f2ee-133">toofilter alle acties toohello die u wilt, Voer Hallo word **antwoord** in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-133">toofilter all actions toohello one that you want, enter hello word **response** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="9f2ee-134">Selecteer Hallo **antwoord** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-134">Select hello **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="9f2ee-135">tooaccess MDN van uitvoer Hallo HALLO hallo **decoderen X12 bericht** actie, set Hallo antwoord **hoofdtekst** veld met deze expressie:</span><span class="sxs-lookup"><span data-stu-id="9f2ee-135">tooaccess hello MDN from hello output of hello **Decode X12 message** action, set hello response **BODY** field with this expression:</span></span>

    <span data-ttu-id="9f2ee-136">@base64ToString(body('Decode_AS2_message')? ['OutgoingMdn']? ['Inhoud'])</span><span class="sxs-lookup"><span data-stu-id="9f2ee-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="9f2ee-137">Sla uw werk op.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="9f2ee-138">U bent nu klaar uw B2B logische app in te stellen.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="9f2ee-139">In werkelijkheid toepassing, kunt u toostore Hallo gedecodeerd X12 gegevens in een line-of-business (LOB)-app of de gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-139">In a real world application, you might want toostore hello decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="9f2ee-140">tooconnect uw eigen LOB-apps en het gebruik van deze API's in uw logische app, kunt u verdere acties toevoegen of aangepaste API's schrijft.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-140">tooconnect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="9f2ee-141">Functies en gebruiksvoorbeelden</span><span class="sxs-lookup"><span data-stu-id="9f2ee-141">Features and use cases</span></span>

* <span data-ttu-id="9f2ee-142">Hallo AS2 en X12 decoderen en coderen acties kunnen uitwisselen van gegevens tussen handelspartners via standaardprotocollen in logic apps.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-142">hello AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="9f2ee-143">tooexchange gegevens met handelspartners, kunt u AS2 en X12 met of zonder elkaar.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-143">tooexchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="9f2ee-144">Hallo B2B acties kunnen u eenvoudig partners en -overeenkomsten maken in uw account integratie en gebruiken in een logische app.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-144">hello B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="9f2ee-145">Wanneer u uw logische app met andere acties uitbreidt, kunt u deze kunt verzenden en ontvangen van gegevens tussen andere apps en services zoals SalesForce.</span><span class="sxs-lookup"><span data-stu-id="9f2ee-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="9f2ee-146">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="9f2ee-146">Learn more</span></span>
[<span data-ttu-id="9f2ee-147">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="9f2ee-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
