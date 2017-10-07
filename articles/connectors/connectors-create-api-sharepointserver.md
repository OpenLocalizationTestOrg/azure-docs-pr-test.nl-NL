---
title: aaaUse hello SharePoint Server-Connector in uw logische Apps | Microsoft Docs
description: Aan de slag met Hallo Hallo SharePoint Server-Connector in Logic apps
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a><span data-ttu-id="468a7-103">Aan de slag met Hallo SharePoint-connector</span><span class="sxs-lookup"><span data-stu-id="468a7-103">Get started with hello SharePoint connector</span></span>
<span data-ttu-id="468a7-104">Hallo SharePoint Connector biedt een manier toowork met lijsten in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="468a7-104">hello SharePoint Connector provides an way toowork with Lists on SharePoint.</span></span>

<span data-ttu-id="468a7-105">Aan de slag door het maken van een logische app; Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="468a7-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toosharepoint"></a><span data-ttu-id="468a7-106">Een tooSharePoint verbinding maken</span><span class="sxs-lookup"><span data-stu-id="468a7-106">Create a connection tooSharePoint</span></span>
<span data-ttu-id="468a7-107">toouse Hallo SharePoint-Connector, maakt u eerst een **verbinding** vervolgens Hallo informatie opgeven voor deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="468a7-107">toouse hello SharePoint Connector , you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="468a7-108">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="468a7-108">Property</span></span> | <span data-ttu-id="468a7-109">Vereist</span><span class="sxs-lookup"><span data-stu-id="468a7-109">Required</span></span> | <span data-ttu-id="468a7-110">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="468a7-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="468a7-111">Token</span><span class="sxs-lookup"><span data-stu-id="468a7-111">Token</span></span> |<span data-ttu-id="468a7-112">Ja</span><span class="sxs-lookup"><span data-stu-id="468a7-112">Yes</span></span> |<span data-ttu-id="468a7-113">SharePoint-referenties opgeven</span><span class="sxs-lookup"><span data-stu-id="468a7-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="468a7-114">tooconnect te**SharePoint**, Voer uw tooSharePoint identiteit (gebruikersnaam en wachtwoord, smartcard-referenties, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="468a7-114">tooconnect too**SharePoint**, enter your identity (username and password, smart card credentials, etc.) tooSharePoint.</span></span> <span data-ttu-id="468a7-115">Zodra u hebt geverifieerd, kunt u toouse Hallo SharePoint connector doorgaan in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="468a7-115">Once you've been authenticated, you can proceed toouse hello SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="468a7-116">Terwijl op Hallo ontwerper van uw logische app, volgt u deze stappen toosign in SharePoint toocreate Hallo verbinding **verbinding** voor gebruik in uw logische app:</span><span class="sxs-lookup"><span data-stu-id="468a7-116">While on hello designer of your logic app, follow these steps toosign into SharePoint toocreate hello connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="468a7-117">Voer SharePoint in het zoekvak Hallo en Hallo zoeken tooreturn wacht totdat alle vermeldingen met SharePoint in Hallo-naam:</span><span class="sxs-lookup"><span data-stu-id="468a7-117">Enter SharePoint in hello search box and wait for hello search tooreturn all entries with SharePoint in hello name:</span></span>   
   ![SharePoint configureren][1]  
2. <span data-ttu-id="468a7-119">Selecteer **SharePoint - als een bestand is gemaakt**</span><span class="sxs-lookup"><span data-stu-id="468a7-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="468a7-120">Selecteer **tooSharePoint aanmelden**:</span><span class="sxs-lookup"><span data-stu-id="468a7-120">Select **Sign in tooSharePoint**:</span></span>   
   <span data-ttu-id="468a7-121">![SharePoint configureren][2]</span><span class="sxs-lookup"><span data-stu-id="468a7-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="468a7-122">Geef uw SharePoint-referenties toosign in tooauthenticate met SharePoint</span><span class="sxs-lookup"><span data-stu-id="468a7-122">Provide your SharePoint credentials toosign in tooauthenticate with SharePoint</span></span>   
   ![SharePoint configureren][3]     
5. <span data-ttu-id="468a7-124">Nadat het Hallo-verificatie is voltooid, moet u omgeleide tooyour logic app toocomplete door het configureren van SharePoint **wanneer een bestand wordt gemaakt** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="468a7-124">After hello authentication completes you'll be redirected tooyour logic app toocomplete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="468a7-125">![SharePoint configureren][4]</span><span class="sxs-lookup"><span data-stu-id="468a7-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="468a7-126">Vervolgens kunt u andere triggers en acties die u toocomplete uw logische app moet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="468a7-126">You can then add other triggers and actions that you need toocomplete your logic app.</span></span>   
7. <span data-ttu-id="468a7-127">Sla uw werk door te selecteren **opslaan** op Hallo menubalk hierboven.</span><span class="sxs-lookup"><span data-stu-id="468a7-127">Save your work by selecting **Save** on hello menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="468a7-128">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="468a7-128">Connector-specific details</span></span>

<span data-ttu-id="468a7-129">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="468a7-129">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="468a7-130">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="468a7-130">More connectors</span></span>
<span data-ttu-id="468a7-131">Ga terug toohello [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="468a7-131">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
