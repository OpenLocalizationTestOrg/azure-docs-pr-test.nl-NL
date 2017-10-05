---
title: De SharePoint-Server-Connector in uw logische Apps gebruiken | Microsoft Docs
description: Aan de slag met de de SharePoint-Server-Connector in Logic apps
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
ms.openlocfilehash: 0f3274816e279a1aa57febaa2f8294914900799a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-connector"></a><span data-ttu-id="8da77-103">Aan de slag met de SharePoint-connector</span><span class="sxs-lookup"><span data-stu-id="8da77-103">Get started with the SharePoint connector</span></span>
<span data-ttu-id="8da77-104">De SharePoint-Connector biedt een manier om te werken met lijsten in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8da77-104">The SharePoint Connector provides an way to work with Lists on SharePoint.</span></span>

<span data-ttu-id="8da77-105">Aan de slag door het maken van een logische app; Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8da77-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sharepoint"></a><span data-ttu-id="8da77-106">Maak een verbinding met SharePoint</span><span class="sxs-lookup"><span data-stu-id="8da77-106">Create a connection to SharePoint</span></span>
<span data-ttu-id="8da77-107">Voor het gebruik van de SharePoint-Connector maakt u eerst een **verbinding** Geef vervolgens de details voor deze eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="8da77-107">To use the SharePoint Connector , you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="8da77-108">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8da77-108">Property</span></span> | <span data-ttu-id="8da77-109">Vereist</span><span class="sxs-lookup"><span data-stu-id="8da77-109">Required</span></span> | <span data-ttu-id="8da77-110">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8da77-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8da77-111">Token</span><span class="sxs-lookup"><span data-stu-id="8da77-111">Token</span></span> |<span data-ttu-id="8da77-112">Ja</span><span class="sxs-lookup"><span data-stu-id="8da77-112">Yes</span></span> |<span data-ttu-id="8da77-113">SharePoint-referenties opgeven</span><span class="sxs-lookup"><span data-stu-id="8da77-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="8da77-114">Verbinding maken met **SharePoint**, voert u uw identiteit (gebruikersnaam en wachtwoord, smart card-referenties, enz.) naar SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8da77-114">To connect to **SharePoint**, enter your identity (username and password, smart card credentials, etc.) to SharePoint.</span></span> <span data-ttu-id="8da77-115">Zodra u hebt geverifieerd, kunt u doorgaan met het gebruik van de SharePoint-connector in uw logische app.</span><span class="sxs-lookup"><span data-stu-id="8da77-115">Once you've been authenticated, you can proceed to use the SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="8da77-116">Volg deze stappen voor aanmelding bij SharePoint om de verbinding te maken terwijl op de ontwerper van uw logische app, **verbinding** voor gebruik in uw logische app:</span><span class="sxs-lookup"><span data-stu-id="8da77-116">While on the designer of your logic app, follow these steps to sign into SharePoint to create the connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="8da77-117">Voer SharePoint in het zoekvak en wacht totdat de zoekopdracht te retourneren van alle vermeldingen met SharePoint in de naam:</span><span class="sxs-lookup"><span data-stu-id="8da77-117">Enter SharePoint in the search box and wait for the search to return all entries with SharePoint in the name:</span></span>   
   ![SharePoint configureren][1]  
2. <span data-ttu-id="8da77-119">Selecteer **SharePoint - als een bestand is gemaakt**</span><span class="sxs-lookup"><span data-stu-id="8da77-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="8da77-120">Selecteer **aanmelden bij SharePoint**:</span><span class="sxs-lookup"><span data-stu-id="8da77-120">Select **Sign in to SharePoint**:</span></span>   
   <span data-ttu-id="8da77-121">![SharePoint configureren][2]</span><span class="sxs-lookup"><span data-stu-id="8da77-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="8da77-122">Geef uw SharePoint-referenties om aan te melden om te verifiëren met SharePoint</span><span class="sxs-lookup"><span data-stu-id="8da77-122">Provide your SharePoint credentials to sign in to authenticate with SharePoint</span></span>   
   ![SharePoint configureren][3]     
5. <span data-ttu-id="8da77-124">Nadat de verificatie is voltooid wordt u omgeleid naar uw logische app om deze te voltooien door het configureren van SharePoint **wanneer een bestand wordt gemaakt** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8da77-124">After the authentication completes you'll be redirected to your logic app to complete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="8da77-125">![SharePoint configureren][4]</span><span class="sxs-lookup"><span data-stu-id="8da77-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="8da77-126">Vervolgens kunt u andere triggers en acties die u moet voltooien van uw logische app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8da77-126">You can then add other triggers and actions that you need to complete your logic app.</span></span>   
7. <span data-ttu-id="8da77-127">Sla uw werk door te selecteren **opslaan** boven in het menu.</span><span class="sxs-lookup"><span data-stu-id="8da77-127">Save your work by selecting **Save** on the menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="8da77-128">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="8da77-128">Connector-specific details</span></span>

<span data-ttu-id="8da77-129">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="8da77-129">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="8da77-130">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="8da77-130">More connectors</span></span>
<span data-ttu-id="8da77-131">Ga terug naar de [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8da77-131">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
