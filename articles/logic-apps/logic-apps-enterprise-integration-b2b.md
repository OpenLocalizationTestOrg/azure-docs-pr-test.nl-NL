---
title: Oplossingen voor B2B - Azure Logic Apps maken | Microsoft Docs
description: Ontvangt gegevens in logische apps met behulp van de B2B-functies in de Enterprise-integratiepakket
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
ms.openlocfilehash: 0625787ddcbc0091e70b111f687e25929720ad15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="receive-data-in-logic-apps-with-the-b2b-features-in-the-enterprise-integration-pack"></a><span data-ttu-id="4d59f-103">Ontvangt gegevens in logische apps met de B2B-functies in de Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="4d59f-103">Receive data in logic apps with the B2B features in the Enterprise Integration Pack</span></span>

<span data-ttu-id="4d59f-104">Nadat u een account voor integratie met partners en overeenkomsten hebt gemaakt, bent u klaar voor het maken van een werkstroom bedrijven (B2B) voor uw logische app met de [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d59f-104">After you create an integration account that has partners and agreements, you are ready to create a business to business (B2B) workflow for your logic app with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d59f-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4d59f-105">Prerequisites</span></span>

<span data-ttu-id="4d59f-106">Gebruik de AS2 en X12 acties, moet u een Enterprise Integration-Account hebben.</span><span class="sxs-lookup"><span data-stu-id="4d59f-106">To use the AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="4d59f-107">Meer informatie over [een Enterprise Integration-Account maken](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="4d59f-107">Learn [how to create an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="4d59f-108">Een logische app maken met B2B-connectors</span><span class="sxs-lookup"><span data-stu-id="4d59f-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="4d59f-109">Volg deze stappen voor het maken van een B2B logische app die gebruikmaakt van de AS2 en X12 acties mag gegevens ontvangen van een trading partner:</span><span class="sxs-lookup"><span data-stu-id="4d59f-109">Follow these steps to create a B2B logic app that uses the AS2 and X12 actions to receive data from a trading partner:</span></span>

1. <span data-ttu-id="4d59f-110">Maak een logische app, klikt u vervolgens [uw app koppelen aan uw account integratie](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="4d59f-110">Create a logic app, then [link your app to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="4d59f-111">Voeg een **aanvraag: wanneer een HTTP-aanvraag wordt ontvangen** trigger aan uw logische app.</span><span class="sxs-lookup"><span data-stu-id="4d59f-111">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="4d59f-112">Om toe te voegen de **decoderen AS2** actie, selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4d59f-112">To add the **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="4d59f-113">Als u wilt alle acties die u wilt filteren, voer dan het woord **as2** in het zoekvak.</span><span class="sxs-lookup"><span data-stu-id="4d59f-113">To filter all actions to the one that you want, enter the word **as2** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="4d59f-114">Selecteer de **AS2 - decoderen AS2-bericht** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="4d59f-114">Select the **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="4d59f-115">Voeg de **hoofdtekst** die u wilt gebruiken als invoer.</span><span class="sxs-lookup"><span data-stu-id="4d59f-115">Add the **Body** that you want to use as input.</span></span> <span data-ttu-id="4d59f-116">Selecteer de hoofdtekst van de HTTP-aanvraag die de logische app getriggerd in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4d59f-116">In this example, select the body of the HTTP request that triggers the logic app.</span></span> <span data-ttu-id="4d59f-117">Of typ een expressie die de invoer van de kopteksten in de **HEADERS** veld:</span><span class="sxs-lookup"><span data-stu-id="4d59f-117">Or enter an expression that inputs the headers in the **HEADERS** field:</span></span>

    <span data-ttu-id="4d59f-118">@triggerOutputs([headers])</span><span class="sxs-lookup"><span data-stu-id="4d59f-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="4d59f-119">Voeg de vereiste **Headers** voor AS2, kunt u vinden in de headers van de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="4d59f-119">Add the required **Headers** for AS2, which you can find in the HTTP request headers.</span></span> <span data-ttu-id="4d59f-120">Selecteer in de headers van de HTTP-aanvraag die de logische app activeren in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4d59f-120">In this example, select the headers of the HTTP request that trigger the logic app.</span></span>

8. <span data-ttu-id="4d59f-121">Nu de berichtactie decoderen X12 toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4d59f-121">Now add the Decode X12 message action.</span></span> <span data-ttu-id="4d59f-122">Selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4d59f-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="4d59f-123">Als u wilt alle acties die u wilt filteren, voer dan het woord **x12** in het zoekvak.</span><span class="sxs-lookup"><span data-stu-id="4d59f-123">To filter all actions to the one that you want, enter the word **x12** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="4d59f-124">Selecteer de **X12-decoderen X12 bericht** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="4d59f-124">Select the **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="4d59f-125">Nu moet u de invoer voor deze actie.</span><span class="sxs-lookup"><span data-stu-id="4d59f-125">Now you must specify the input to this action.</span></span> <span data-ttu-id="4d59f-126">Deze invoer is de uitvoer van de vorige AS2-actie.</span><span class="sxs-lookup"><span data-stu-id="4d59f-126">This input is the output from the previous AS2 action.</span></span>

    <span data-ttu-id="4d59f-127">Inhoud van het werkelijke bericht in een JSON-object is en is met base64 gecodeerd, dus u een expressie als invoer opgeven moet.</span><span class="sxs-lookup"><span data-stu-id="4d59f-127">The actual message content is in a JSON object and is base64 encoded, so you must specify an expression as the input.</span></span> 
    <span data-ttu-id="4d59f-128">Voer de volgende expressie in de **X12 PLATTE bestand bericht te decoderen** invoerveld:</span><span class="sxs-lookup"><span data-stu-id="4d59f-128">Enter the following expression in the **X12 FLAT FILE MESSAGE TO DECODE** input field:</span></span>
    
    <span data-ttu-id="4d59f-129">@base64ToString(body('Decode_AS2_message')? ['AS2Message']? ['Inhoud'])</span><span class="sxs-lookup"><span data-stu-id="4d59f-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="4d59f-130">Voeg nu de stappen voor het decoderen van de X12 gegevens ontvangen van de trading partner en uitvoer van de items in een JSON-object.</span><span class="sxs-lookup"><span data-stu-id="4d59f-130">Now add steps to decode the X12 data received from the trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="4d59f-131">Als u wilt de partner waarschuwen dat de gegevens zijn ontvangen, kunt u verzenden weer een antwoord met de AS2 bericht Disposition melding (MDN) in een HTTP-antwoord-actie.</span><span class="sxs-lookup"><span data-stu-id="4d59f-131">To notify the partner that the data was received, you can send back a response containing the AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="4d59f-132">Om toe te voegen de **antwoord** actie, kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4d59f-132">To add the **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="4d59f-133">Als u wilt alle acties die u wilt filteren, voer dan het woord **antwoord** in het zoekvak.</span><span class="sxs-lookup"><span data-stu-id="4d59f-133">To filter all actions to the one that you want, enter the word **response** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="4d59f-134">Selecteer de **antwoord** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="4d59f-134">Select the **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="4d59f-135">Voor toegang tot de MDN uit de uitvoer van de **decoderen X12 bericht** actie, het antwoord ingesteld **hoofdtekst** veld met deze expressie:</span><span class="sxs-lookup"><span data-stu-id="4d59f-135">To access the MDN from the output of the **Decode X12 message** action, set the response **BODY** field with this expression:</span></span>

    <span data-ttu-id="4d59f-136">@base64ToString(body('Decode_AS2_message')? ['OutgoingMdn']? ['Inhoud'])</span><span class="sxs-lookup"><span data-stu-id="4d59f-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="4d59f-137">Sla uw werk op.</span><span class="sxs-lookup"><span data-stu-id="4d59f-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="4d59f-138">U bent nu klaar uw B2B logische app in te stellen.</span><span class="sxs-lookup"><span data-stu-id="4d59f-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="4d59f-139">In een toepassing praktijk wilt u mogelijk de gedecodeerde X12 opslaan gegevens in een line-of-business (LOB)-app of de gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="4d59f-139">In a real world application, you might want to store the decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="4d59f-140">Als u wilt verbinding maken met uw eigen LOB-apps en het gebruik van deze API's in uw logische app, kunt u verdere acties toevoegen of schrijven van aangepaste API's.</span><span class="sxs-lookup"><span data-stu-id="4d59f-140">To connect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="4d59f-141">Functies en gebruiksvoorbeelden</span><span class="sxs-lookup"><span data-stu-id="4d59f-141">Features and use cases</span></span>

* <span data-ttu-id="4d59f-142">De AS2 en X12 decoderen en coderen acties kunnen uitwisselen van gegevens tussen handelspartners via standaardprotocollen in logic apps.</span><span class="sxs-lookup"><span data-stu-id="4d59f-142">The AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="4d59f-143">U kunt voor het uitwisselen van gegevens met handelspartners AS2 en X12 gebruiken met of zonder elkaar.</span><span class="sxs-lookup"><span data-stu-id="4d59f-143">To exchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="4d59f-144">De acties B2B kunnen u eenvoudig partners en -overeenkomsten maken in uw account integratie en gebruiken in een logische app.</span><span class="sxs-lookup"><span data-stu-id="4d59f-144">The B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="4d59f-145">Wanneer u uw logische app met andere acties uitbreidt, kunt u deze kunt verzenden en ontvangen van gegevens tussen andere apps en services zoals SalesForce.</span><span class="sxs-lookup"><span data-stu-id="4d59f-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="4d59f-146">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="4d59f-146">Learn more</span></span>
[<span data-ttu-id="4d59f-147">Meer informatie over het Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="4d59f-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
