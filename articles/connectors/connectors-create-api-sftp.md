---
title: aaaLearn hoe toouse SFTP-connector in uw logische apps Hallo | Microsoft Docs
description: Logic apps maken met Azure App service. Verbinding maken met tooSFTP API toosend bestanden en ontvangen. U kunt verschillende bewerkingen zoals maken, bijwerken, ophalen of verwijdert u bestanden kunt uitvoeren.
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
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a><span data-ttu-id="9b53e-105">Aan de slag met Hallo SFTP-connector</span><span class="sxs-lookup"><span data-stu-id="9b53e-105">Get started with hello SFTP connector</span></span>
<span data-ttu-id="9b53e-106">Gebruik Hallo SFTP connector tooaccess een toosend SFTP-account en ontvangen van bestanden.</span><span class="sxs-lookup"><span data-stu-id="9b53e-106">Use hello SFTP connector tooaccess an SFTP account toosend and receive files.</span></span> <span data-ttu-id="9b53e-107">U kunt verschillende bewerkingen zoals maken, bijwerken, ophalen of verwijdert u bestanden kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9b53e-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="9b53e-108">toouse [elke connector](apis-list.md), moet u eerst toocreate een logische app.</span><span class="sxs-lookup"><span data-stu-id="9b53e-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="9b53e-109">U kunt aan de slag door [maken van een logische app nu](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9b53e-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosftp"></a><span data-ttu-id="9b53e-110">Verbinding maken met tooSFTP</span><span class="sxs-lookup"><span data-stu-id="9b53e-110">Connect tooSFTP</span></span>
<span data-ttu-id="9b53e-111">Om uw logische app toegang alle services tot, moet u eerst toocreate een *verbinding* toohello service.</span><span class="sxs-lookup"><span data-stu-id="9b53e-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="9b53e-112">Een [verbinding](connectors-overview.md) biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="9b53e-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosftp"></a><span data-ttu-id="9b53e-113">Een tooSFTP verbinding maken</span><span class="sxs-lookup"><span data-stu-id="9b53e-113">Create a connection tooSFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="9b53e-114">Gebruik een trigger SFTP</span><span class="sxs-lookup"><span data-stu-id="9b53e-114">Use an SFTP trigger</span></span>
<span data-ttu-id="9b53e-115">Een trigger is een gebeurtenis die gebruikt toostart Hallo werkstroom gedefinieerd in een logische app worden kan.</span><span class="sxs-lookup"><span data-stu-id="9b53e-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="9b53e-116">[Meer informatie over triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9b53e-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="9b53e-117">In dit voorbeeld Hallo **SFTP - wanneer een bestand wordt toegevoegd of gewijzigd** trigger gebruikte tooinitiate een logic app-werkstroom is wanneer een bestand wordt toegevoegd aan of gewijzigd op een SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="9b53e-117">In this example, hello **SFTP - When a file is added or modified** trigger is used tooinitiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="9b53e-118">U ook toevoegen een voorwaarde die inhoud van de nieuwe of gewijzigde bestand Hallo Hallo gecontroleerd en maakt een beslissing tooextract Hallo-bestand als de inhoud ervan aangeven dat deze moet worden opgehaald voordat u inhoud Hallo.</span><span class="sxs-lookup"><span data-stu-id="9b53e-118">You also add a condition that checks hello contents of hello new or modified file, and makes a decision tooextract hello file if its contents indicate that it should be extracted before using hello contents.</span></span> <span data-ttu-id="9b53e-119">Ten slotte een actie tooextract Hallo inhoud van een bestand toevoegen en Hallo uitgepakt inhoud in een map op Hallo SFTP-server plaatsen.</span><span class="sxs-lookup"><span data-stu-id="9b53e-119">Finally, add an action tooextract hello contents of a file, and place hello extracted contents in a folder on hello SFTP server.</span></span> 

<span data-ttu-id="9b53e-120">In een enterprise-voorbeeld: u kunt deze trigger toomonitor een SFTP-map voor nieuwe bestanden die die klantorders vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="9b53e-120">In an enterprise example, you could use this trigger toomonitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="9b53e-121">U kunt vervolgens een actie van de connector SFTP zoals **bestandsinhoud ophalen**, tooget Hallo inhoud van Hallo order voor verdere verwerking en opslag in een orderdatabase.</span><span class="sxs-lookup"><span data-stu-id="9b53e-121">You could then use an SFTP connector action, such as **Get file content**, tooget hello contents of hello order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="9b53e-122">Een voorwaarde toevoegen</span><span class="sxs-lookup"><span data-stu-id="9b53e-122">Add a condition</span></span>
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="9b53e-123">Gebruik een SFTP-actie</span><span class="sxs-lookup"><span data-stu-id="9b53e-123">Use an SFTP action</span></span>
<span data-ttu-id="9b53e-124">Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="9b53e-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="9b53e-125">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9b53e-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="9b53e-126">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="9b53e-126">Connector-specific details</span></span>

<span data-ttu-id="9b53e-127">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="9b53e-127">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="9b53e-128">Meer connectors</span><span class="sxs-lookup"><span data-stu-id="9b53e-128">More connectors</span></span>
<span data-ttu-id="9b53e-129">Ga terug toohello [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="9b53e-129">Go back toohello [APIs list](apis-list.md).</span></span>
