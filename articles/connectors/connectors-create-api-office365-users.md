---
title: De connector voor Office 365-gebruikers toevoegen in Logic Apps | Microsoft Docs
description: Overzicht van de connector voor Office 365-gebruikers met de parameters van de REST-API
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 330f733440932a769eb0fe6031cd0d947a820080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-users-connector"></a><span data-ttu-id="e7c69-103">Aan de slag met de connector voor Office 365-gebruikers</span><span class="sxs-lookup"><span data-stu-id="e7c69-103">Get started with the Office 365 Users connector</span></span>
<span data-ttu-id="e7c69-104">Verbinding maken met Office 365-gebruikers om op te halen van profielen en gebruikers van de zoekfunctie.</span><span class="sxs-lookup"><span data-stu-id="e7c69-104">Connect to Office 365 Users to get profiles, search users, and more.</span></span> <span data-ttu-id="e7c69-105">Met Office 365-gebruikers, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="e7c69-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="e7c69-106">Bouw uw zakelijke flow op basis van de gegevens die u van Office 365-gebruikers krijgt.</span><span class="sxs-lookup"><span data-stu-id="e7c69-106">Build your business flow based on the data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="e7c69-107">Gebruik acties die directe ondergeschikten ophalen ophalen van een manager gebruikersprofiel en meer.</span><span class="sxs-lookup"><span data-stu-id="e7c69-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="e7c69-108">Deze acties reageert en vervolgens de uitvoer beschikbaar maken voor andere acties.</span><span class="sxs-lookup"><span data-stu-id="e7c69-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="e7c69-109">Bijvoorbeeld, ophalen van een persoon directe ondergeschikten, nemen deze informatie en een Azure SQL-database bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e7c69-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="e7c69-110">U kunt aan de slag door het maken van een logische app nu, Zie [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e7c69-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office-365-users"></a><span data-ttu-id="e7c69-111">Maak een verbinding met Office 365-gebruikers</span><span class="sxs-lookup"><span data-stu-id="e7c69-111">Create a connection to Office 365 Users</span></span>
<span data-ttu-id="e7c69-112">Wanneer u deze connector aan uw logische apps toevoegen, moet u aanmelden bij uw account Office 365-gebruikers en toestaan dat logic apps verbinding maken met uw account.</span><span class="sxs-lookup"><span data-stu-id="e7c69-112">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="e7c69-113">Nadat u de verbinding hebt gemaakt, voert u de eigenschappen van de Office 365-gebruikers, zoals de gebruikers-ID.</span><span class="sxs-lookup"><span data-stu-id="e7c69-113">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span></span> <span data-ttu-id="e7c69-114">De **naslaginformatie over REST API** in dit onderwerp beschrijft deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="e7c69-114">The **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="e7c69-115">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="e7c69-115">Connector-specific details</span></span>

<span data-ttu-id="e7c69-116">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/officeusers/).</span><span class="sxs-lookup"><span data-stu-id="e7c69-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e7c69-117">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="e7c69-117">More connectors</span></span>
<span data-ttu-id="e7c69-118">Ga terug naar de [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e7c69-118">Go back to the [APIs list](apis-list.md).</span></span>