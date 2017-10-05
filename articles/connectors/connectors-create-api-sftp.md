---
title: Informatie over het gebruik van de SFTP-connector in logic apps | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met SFTP-API voor het verzenden en ontvangen van bestanden. U kunt verschillende bewerkingen zoals maken, bijwerken, ophalen of verwijdert u bestanden kunt uitvoeren.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 31253d8daee1581167a96a20ba8ad529a04b3e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sftp-connector"></a><span data-ttu-id="c9356-105">Aan de slag met de SFTP-connector</span><span class="sxs-lookup"><span data-stu-id="c9356-105">Get started with the SFTP connector</span></span>
<span data-ttu-id="c9356-106">De SFTP-connector gebruiken voor toegang tot een SFTP-account om te verzenden en ontvangen van bestanden.</span><span class="sxs-lookup"><span data-stu-id="c9356-106">Use the SFTP connector to access an SFTP account to send and receive files.</span></span> <span data-ttu-id="c9356-107">U kunt verschillende bewerkingen zoals maken, bijwerken, ophalen of verwijdert u bestanden kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c9356-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="c9356-108">Gebruik [elke connector](apis-list.md), moet u eerst een logische app maken.</span><span class="sxs-lookup"><span data-stu-id="c9356-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="c9356-109">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c9356-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sftp"></a><span data-ttu-id="c9356-110">Verbinding maken met SFTP</span><span class="sxs-lookup"><span data-stu-id="c9356-110">Connect to SFTP</span></span>
<span data-ttu-id="c9356-111">Om uw logische app toegang alle services tot, moet u eerst maken een *verbinding* naar de service.</span><span class="sxs-lookup"><span data-stu-id="c9356-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="c9356-112">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="c9356-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sftp"></a><span data-ttu-id="c9356-113">Maak een verbinding met SFTP</span><span class="sxs-lookup"><span data-stu-id="c9356-113">Create a connection to SFTP</span></span>
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="c9356-114">Gebruik een trigger SFTP</span><span class="sxs-lookup"><span data-stu-id="c9356-114">Use an SFTP trigger</span></span>
<span data-ttu-id="c9356-115">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die is gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="c9356-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="c9356-116">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c9356-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="c9356-117">In dit voorbeeld wordt de **SFTP - wanneer een bestand wordt toegevoegd of gewijzigd** trigger wordt gebruikt voor het initiëren van een logische app werkstroom wanneer een bestand wordt toegevoegd aan of gewijzigd op een SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="c9356-117">In this example, the **SFTP - When a file is added or modified** trigger is used to initiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="c9356-118">U ook toevoegen een voorwaarde waarmee de inhoud van de nieuwe of gewijzigde bestand controleert en maakt een beslissing uitpakken van het bestand als de inhoud ervan aangeven dat deze moet worden opgehaald voordat u de inhoud.</span><span class="sxs-lookup"><span data-stu-id="c9356-118">You also add a condition that checks the contents of the new or modified file, and makes a decision to extract the file if its contents indicate that it should be extracted before using the contents.</span></span> <span data-ttu-id="c9356-119">Ten slotte een actie voor het uitpakken van de inhoud van een bestand toevoegen en plaatst de geëxtraheerde inhoud in een map op de SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="c9356-119">Finally, add an action to extract the contents of a file, and place the extracted contents in a folder on the SFTP server.</span></span> 

<span data-ttu-id="c9356-120">In een enterprise-voorbeeld: u kunt deze trigger voor het bewaken van een map voor SFTP voor nieuwe bestanden die die klantorders vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="c9356-120">In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="c9356-121">U kunt vervolgens een actie van de connector SFTP zoals **bestandsinhoud ophalen**, de inhoud van de volgorde voor verdere verwerking en opslag in een orderdatabase ophalen.</span><span class="sxs-lookup"><span data-stu-id="c9356-121">You could then use an SFTP connector action, such as **Get file content**, to get the contents of the order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="c9356-122">Een voorwaarde toevoegen</span><span class="sxs-lookup"><span data-stu-id="c9356-122">Add a condition</span></span>
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="c9356-123">Gebruik een SFTP-actie</span><span class="sxs-lookup"><span data-stu-id="c9356-123">Use an SFTP action</span></span>
<span data-ttu-id="c9356-124">Een actie is een bewerking uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="c9356-124">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="c9356-125">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c9356-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="c9356-126">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="c9356-126">Connector-specific details</span></span>

<span data-ttu-id="c9356-127">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="c9356-127">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c9356-128">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="c9356-128">More connectors</span></span>
<span data-ttu-id="c9356-129">Ga terug naar de [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c9356-129">Go back to the [APIs list](apis-list.md).</span></span>