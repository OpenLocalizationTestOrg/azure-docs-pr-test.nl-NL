---
title: aaaUse hello Slack-Connector in Azure logic apps | Microsoft Docs
description: Verbinding maken met tooSlack in logic apps
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a><span data-ttu-id="74f26-103">Aan de slag met Slack Hallo-connector</span><span class="sxs-lookup"><span data-stu-id="74f26-103">Get started with hello Slack connector</span></span>
<span data-ttu-id="74f26-104">Vertraging is een hulpprogramma team communicatie, die samenbrengt alle van uw team communicatie in een plaatst, onmiddellijk doorzoekbare en beschikbaar waar u ook bent.</span><span class="sxs-lookup"><span data-stu-id="74f26-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="74f26-105">Aan de slag door het maken van een logische app nu; Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="74f26-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooslack"></a><span data-ttu-id="74f26-106">Een tooSlack verbinding maken</span><span class="sxs-lookup"><span data-stu-id="74f26-106">Create a connection tooSlack</span></span>
<span data-ttu-id="74f26-107">toouse hello Slack-connector maakt u eerst een **verbinding** vervolgens Hallo informatie opgeven voor deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="74f26-107">toouse hello Slack connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="74f26-108">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="74f26-108">Property</span></span> | <span data-ttu-id="74f26-109">Vereist</span><span class="sxs-lookup"><span data-stu-id="74f26-109">Required</span></span> | <span data-ttu-id="74f26-110">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="74f26-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="74f26-111">Token</span><span class="sxs-lookup"><span data-stu-id="74f26-111">Token</span></span> |<span data-ttu-id="74f26-112">Ja</span><span class="sxs-lookup"><span data-stu-id="74f26-112">Yes</span></span> |<span data-ttu-id="74f26-113">Toegestane referenties opgeven</span><span class="sxs-lookup"><span data-stu-id="74f26-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="74f26-114">Volg deze stappen toosign in Slack en configuratie van de volledige Hallo Hallo Slack **verbinding** in uw logische app:</span><span class="sxs-lookup"><span data-stu-id="74f26-114">Follow these steps toosign into Slack, and complete hello configuration of hello Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="74f26-115">Selecteer **terugkeerpatroon**</span><span class="sxs-lookup"><span data-stu-id="74f26-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="74f26-116">Selecteer een **frequentie** en voer een **Interval**</span><span class="sxs-lookup"><span data-stu-id="74f26-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="74f26-117">Selecteer **een actie toevoegen**</span><span class="sxs-lookup"><span data-stu-id="74f26-117">Select **Add an action**</span></span>  
   <span data-ttu-id="74f26-118">![Vertraging configureren][1]</span><span class="sxs-lookup"><span data-stu-id="74f26-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="74f26-119">Vertraging in het zoekvak Hallo invoeren en wachten op Hallo zoeken tooreturn alle vermeldingen met Slack in Hallo naam</span><span class="sxs-lookup"><span data-stu-id="74f26-119">Enter Slack in hello search box and wait for hello search tooreturn all entries with Slack in hello name</span></span>
5. <span data-ttu-id="74f26-120">Selecteer **Slack - bericht posten**</span><span class="sxs-lookup"><span data-stu-id="74f26-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="74f26-121">Selecteer **tooSlack aanmelden**:</span><span class="sxs-lookup"><span data-stu-id="74f26-121">Select **Sign in tooSlack**:</span></span>  
   <span data-ttu-id="74f26-122">![Vertraging configureren][2]</span><span class="sxs-lookup"><span data-stu-id="74f26-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="74f26-123">Geef uw toosign toegestane referenties in tooauthorize Hallo toepassing</span><span class="sxs-lookup"><span data-stu-id="74f26-123">Provide your Slack credentials toosign in tooauthorize hello  application</span></span>    
   ![Vertraging configureren][3]  
8. <span data-ttu-id="74f26-125">U zult de aanmeldingspagina van de organisatie van de omgeleide tooyour.</span><span class="sxs-lookup"><span data-stu-id="74f26-125">You'll be redirected tooyour organization's Log in page.</span></span> <span data-ttu-id="74f26-126">**Autoriseren** toegestane toointeract met uw logische app:</span><span class="sxs-lookup"><span data-stu-id="74f26-126">**Authorize** Slack toointeract with your logic app:</span></span>      
   <span data-ttu-id="74f26-127">![Vertraging configureren][5]</span><span class="sxs-lookup"><span data-stu-id="74f26-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="74f26-128">Nadat het Hallo-autorisatie is voltooid, moet u omgeleide tooyour logic app toocomplete door het configureren van Hallo **vertraging - alle berichten ophalen** sectie.</span><span class="sxs-lookup"><span data-stu-id="74f26-128">After hello authorization completes you'll be redirected tooyour logic app toocomplete it by configuring hello **Slack - Get all messages** section.</span></span> <span data-ttu-id="74f26-129">Toevoegen van andere triggers en acties die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="74f26-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="74f26-130">![Vertraging configureren][6]</span><span class="sxs-lookup"><span data-stu-id="74f26-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="74f26-131">Sla uw werk door te selecteren **opslaan** op Hallo menubalk hierboven.</span><span class="sxs-lookup"><span data-stu-id="74f26-131">Save your work by selecting **Save** on hello menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="74f26-132">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="74f26-132">Connector-specific details</span></span>

<span data-ttu-id="74f26-133">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="74f26-133">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="74f26-134">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="74f26-134">More connectors</span></span>
<span data-ttu-id="74f26-135">Ga terug toohello [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="74f26-135">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
