---
title: Gebruik van de Connector Slack in Azure logic apps | Microsoft Docs
description: Verbinding maken met Slack in logic apps
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
ms.openlocfilehash: fc5fc128efe01bd0727e3ff30d8938918e89ac3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-slack-connector"></a><span data-ttu-id="0e012-103">Aan de slag met de toegestane connector</span><span class="sxs-lookup"><span data-stu-id="0e012-103">Get started with the Slack connector</span></span>
<span data-ttu-id="0e012-104">Vertraging is een hulpprogramma team communicatie, die samenbrengt alle van uw team communicatie in een plaatst, onmiddellijk doorzoekbare en beschikbaar waar u ook bent.</span><span class="sxs-lookup"><span data-stu-id="0e012-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="0e012-105">Aan de slag door het maken van een logische app nu; Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0e012-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-slack"></a><span data-ttu-id="0e012-106">Maak een verbinding met Slack</span><span class="sxs-lookup"><span data-stu-id="0e012-106">Create a connection to Slack</span></span>
<span data-ttu-id="0e012-107">Voor het gebruik van de toegestane connector maakt u eerst een **verbinding** Geef vervolgens de details voor deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="0e012-107">To use the Slack connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="0e012-108">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="0e012-108">Property</span></span> | <span data-ttu-id="0e012-109">Vereist</span><span class="sxs-lookup"><span data-stu-id="0e012-109">Required</span></span> | <span data-ttu-id="0e012-110">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0e012-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0e012-111">Token</span><span class="sxs-lookup"><span data-stu-id="0e012-111">Token</span></span> |<span data-ttu-id="0e012-112">Ja</span><span class="sxs-lookup"><span data-stu-id="0e012-112">Yes</span></span> |<span data-ttu-id="0e012-113">Toegestane referenties opgeven</span><span class="sxs-lookup"><span data-stu-id="0e012-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="0e012-114">Volg deze stappen voor het aanmelden bij de vertraging en voltooi de configuratie van de toegestane vertraging **verbinding** in uw logische app:</span><span class="sxs-lookup"><span data-stu-id="0e012-114">Follow these steps to sign into Slack, and complete the configuration of the Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="0e012-115">Selecteer **terugkeerpatroon**</span><span class="sxs-lookup"><span data-stu-id="0e012-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="0e012-116">Selecteer een **frequentie** en voer een **Interval**</span><span class="sxs-lookup"><span data-stu-id="0e012-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="0e012-117">Selecteer **een actie toevoegen**</span><span class="sxs-lookup"><span data-stu-id="0e012-117">Select **Add an action**</span></span>  
   <span data-ttu-id="0e012-118">![Vertraging configureren][1]</span><span class="sxs-lookup"><span data-stu-id="0e012-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="0e012-119">Vertraging in het zoekvak invoert en wacht tot de zoekopdracht te retourneren van alle vermeldingen met vertraging in de naam</span><span class="sxs-lookup"><span data-stu-id="0e012-119">Enter Slack in the search box and wait for the search to return all entries with Slack in the name</span></span>
5. <span data-ttu-id="0e012-120">Selecteer **Slack - bericht posten**</span><span class="sxs-lookup"><span data-stu-id="0e012-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="0e012-121">Selecteer **aanmelden met Slack**:</span><span class="sxs-lookup"><span data-stu-id="0e012-121">Select **Sign in to Slack**:</span></span>  
   <span data-ttu-id="0e012-122">![Vertraging configureren][2]</span><span class="sxs-lookup"><span data-stu-id="0e012-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="0e012-123">De toegestane referenties opgeven voor het aanmelden bij de toepassing</span><span class="sxs-lookup"><span data-stu-id="0e012-123">Provide your Slack credentials to sign in to authorize the  application</span></span>    
   ![Vertraging configureren][3]  
8. <span data-ttu-id="0e012-125">U moet worden omgeleid naar de aanmeldingspagina van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="0e012-125">You'll be redirected to your organization's Log in page.</span></span> <span data-ttu-id="0e012-126">**Autoriseren** Slack om te communiceren met uw logische app:</span><span class="sxs-lookup"><span data-stu-id="0e012-126">**Authorize** Slack to interact with your logic app:</span></span>      
   <span data-ttu-id="0e012-127">![Vertraging configureren][5]</span><span class="sxs-lookup"><span data-stu-id="0e012-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="0e012-128">Nadat de autorisatie is voltooid wordt u omgeleid naar uw logische app om deze te voltooien door het configureren van de **vertraging - alle berichten ophalen** sectie.</span><span class="sxs-lookup"><span data-stu-id="0e012-128">After the authorization completes you'll be redirected to your logic app to complete it by configuring the **Slack - Get all messages** section.</span></span> <span data-ttu-id="0e012-129">Toevoegen van andere triggers en acties die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="0e012-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="0e012-130">![Vertraging configureren][6]</span><span class="sxs-lookup"><span data-stu-id="0e012-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="0e012-131">Sla uw werk door te selecteren **opslaan** boven in het menu.</span><span class="sxs-lookup"><span data-stu-id="0e012-131">Save your work by selecting **Save** on the menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="0e012-132">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="0e012-132">Connector-specific details</span></span>

<span data-ttu-id="0e012-133">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="0e012-133">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="0e012-134">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="0e012-134">More connectors</span></span>
<span data-ttu-id="0e012-135">Ga terug naar de [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="0e012-135">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
