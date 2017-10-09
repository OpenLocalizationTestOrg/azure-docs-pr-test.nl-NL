---
title: aaaOverview van Azure IoT rand | Microsoft Docs
description: Hallo architectuur worden de basisconcepten beschreven in de Azure IoT rand zoals gateways, modules en beleggingsmakelaars.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="f68a1-103">Azure IoT rand architectuur concepten</span><span class="sxs-lookup"><span data-stu-id="f68a1-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="f68a1-104">Voordat u een voorbeeld van code bekijken of uw eigen IoT rand met veldgateway maken, moet u weten Hallo belangrijkste concepten die onderbouwing Hallo-architectuur van IoT rand.</span><span class="sxs-lookup"><span data-stu-id="f68a1-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand hello key concepts that underpin hello architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="f68a1-105">Rand van de IoT-modules</span><span class="sxs-lookup"><span data-stu-id="f68a1-105">IoT Edge modules</span></span>

<span data-ttu-id="f68a1-106">U een gateway bouwen met Azure IoT rand door te maken en montage *IoT rand modules*.</span><span class="sxs-lookup"><span data-stu-id="f68a1-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="f68a1-107">Modules gebruiken *berichten* tooexchange gegevens met elkaar.</span><span class="sxs-lookup"><span data-stu-id="f68a1-107">Modules use *messages* tooexchange data with each other.</span></span> <span data-ttu-id="f68a1-108">Een module een bericht ontvangt, voert een bepaalde actie op deze desgewenst getransformeerd tot een nieuw bericht en publiceert deze voor andere tooprocess modules.</span><span class="sxs-lookup"><span data-stu-id="f68a1-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules tooprocess.</span></span> <span data-ttu-id="f68a1-109">Sommige modules kunnen alleen nieuwe berichten produceren en verwerken nooit binnenkomende berichten.</span><span class="sxs-lookup"><span data-stu-id="f68a1-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="f68a1-110">Een keten van modules maakt een pijplijn gegevensverwerking met elke module voor het uitvoeren van een transformatie op Hallo van gegevens op één punt in deze pijplijn.</span><span class="sxs-lookup"><span data-stu-id="f68a1-110">A chain of modules creates a data processing pipeline with each module performing a transformation on hello data at one point in that pipeline.</span></span>

![Een keten van modules in de gateway gebouwd met de Azure IoT Edge][1]

<span data-ttu-id="f68a1-112">IoT-rand bevat Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="f68a1-112">IoT Edge contains hello following components:</span></span>

* <span data-ttu-id="f68a1-113">Vooraf geschreven modules die algemene functies van de gateway uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f68a1-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="f68a1-114">Hallo-interfaces een ontwikkelaar kan toowrite aangepaste modules kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f68a1-114">hello interfaces a developer can use toowrite custom modules.</span></span>
* <span data-ttu-id="f68a1-115">Hallo infrastructuur nodig toodeploy en een set van modules uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f68a1-115">hello infrastructure necessary toodeploy and run a set of modules.</span></span>

<span data-ttu-id="f68a1-116">Hallo SDK biedt een abstractielaag waarmee u toobuild gateways toorun op verschillende besturingssystemen en platforms.</span><span class="sxs-lookup"><span data-stu-id="f68a1-116">hello SDK provides an abstraction layer that enables you toobuild gateways toorun on various operating systems and platforms.</span></span>

![Azure IoT Edge-abstractielaag][2]

## <a name="messages"></a><span data-ttu-id="f68a1-118">Berichten</span><span class="sxs-lookup"><span data-stu-id="f68a1-118">Messages</span></span>

<span data-ttu-id="f68a1-119">Hoewel u nadenkt over modules doorgeven van berichten tooeach andere is een handige manier tooconceptualize hoe de functies van een gateway, komt deze niet nauwkeurig overeen met wat er gebeurt.</span><span class="sxs-lookup"><span data-stu-id="f68a1-119">Although thinking about modules passing messages tooeach other is a convenient way tooconceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="f68a1-120">Een broker toocommunicate IoT Edge-modules gebruiken met elkaar.</span><span class="sxs-lookup"><span data-stu-id="f68a1-120">IoT Edge modules use a broker toocommunicate with each other.</span></span> <span data-ttu-id="f68a1-121">Modules publiceren van berichten toohello broker (messaging patronen, zoals bus of publiceren/abonneren met) en vervolgens laat u Hallo broker route Hallo-bericht toohello modules verbonden tooit.</span><span class="sxs-lookup"><span data-stu-id="f68a1-121">Modules publish messages toohello broker (using messaging patterns such as bus, or publish/subscribe) and then let hello broker route hello message toohello modules connected tooit.</span></span>

<span data-ttu-id="f68a1-122">Hallo maakt gebruik van een module **Broker_Publish** toopublish bericht toohello broker werken.</span><span class="sxs-lookup"><span data-stu-id="f68a1-122">A module uses hello **Broker_Publish** function toopublish a message toohello broker.</span></span> <span data-ttu-id="f68a1-123">Hallo broker biedt berichten tooa module door een callback-functie wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f68a1-123">hello broker delivers messages tooa module by invoking a callback function.</span></span> <span data-ttu-id="f68a1-124">Een bericht bestaat uit een reeks sleutel/waarde-eigenschappen en inhoud die als een blok geheugen worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="f68a1-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![Hallo-rol van Hallo Broker in de Azure IoT rand][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="f68a1-126">Berichtroutering en filteren</span><span class="sxs-lookup"><span data-stu-id="f68a1-126">Message routing and filtering</span></span>

<span data-ttu-id="f68a1-127">Er zijn twee manieren toodirect berichten toohello juiste IoT rand modules:</span><span class="sxs-lookup"><span data-stu-id="f68a1-127">There are two ways toodirect messages toohello correct IoT Edge modules:</span></span>

* <span data-ttu-id="f68a1-128">U kunt een set koppelingen doorgeven kunnen worden doorgegeven, is de toohello broker zodat Hallo broker Hallo bron- en sink voor elke module.</span><span class="sxs-lookup"><span data-stu-id="f68a1-128">You can pass a set of links can be passed toohello broker so hello broker knows hello source and sink for each module.</span></span>
* <span data-ttu-id="f68a1-129">Een module kunt filteren op Hallo eigenschappen van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="f68a1-129">A module can filter on hello properties of hello message.</span></span>

<span data-ttu-id="f68a1-130">Een module moet alleen reageren op een bericht als het Hallo-bericht is bedoeld voor het.</span><span class="sxs-lookup"><span data-stu-id="f68a1-130">A module should only act upon a message if hello message is intended for it.</span></span> <span data-ttu-id="f68a1-131">Koppelingen en effectief filteren bericht maakt een pijplijn bericht.</span><span class="sxs-lookup"><span data-stu-id="f68a1-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f68a1-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f68a1-132">Next steps</span></span>

<span data-ttu-id="f68a1-133">toosee deze concepten die worden toegepast in een voorbeeld van een u kunt uitvoeren, Zie [verkennen Azure IoT rand architectuur][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="f68a1-133">toosee these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md