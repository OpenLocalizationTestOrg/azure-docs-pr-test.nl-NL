---
title: Overzicht van Azure IoT-rand | Microsoft Docs
description: Beschrijft de architectuur belangrijkste concepten in Azure IoT rand zoals gateways, modules en beleggingsmakelaars.
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
ms.openlocfilehash: ecdd56c91a8fc2011b3d7abe93b9d27c1e1e0bef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="d9ad5-103">Azure IoT rand architectuur concepten</span><span class="sxs-lookup"><span data-stu-id="d9ad5-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="d9ad5-104">Voordat u alle voorbeeldcode bekijken of uw eigen IoT rand met veldgateway maken, moet u de belangrijkste concepten die onderbouwing van de architectuur van IoT rand begrijpen.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand the key concepts that underpin the architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="d9ad5-105">Rand van de IoT-modules</span><span class="sxs-lookup"><span data-stu-id="d9ad5-105">IoT Edge modules</span></span>

<span data-ttu-id="d9ad5-106">U een gateway bouwen met Azure IoT rand door te maken en montage *IoT rand modules*.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="d9ad5-107">Modules gebruiken *berichten* om gegevens met elkaar uit te wisselen.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-107">Modules use *messages* to exchange data with each other.</span></span> <span data-ttu-id="d9ad5-108">Een module ontvangt een bericht, voert daarmee een bepaalde actie uit, zet het eventueel om in een nieuw bericht en publiceert dit bericht vervolgens zodat het door andere modules kan worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span></span> <span data-ttu-id="d9ad5-109">Sommige modules kunnen alleen nieuwe berichten produceren en verwerken nooit binnenkomende berichten.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="d9ad5-110">Een keten van modules vormt een gegevensverwerkingspijplijn waarbij elke module een transformatie uitvoert van de gegevens op één punt in die pijplijn.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-110">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span></span>

![Een keten van modules in de gateway gebouwd met de Azure IoT Edge][1]

<span data-ttu-id="d9ad5-112">IoT-rand bevat de volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="d9ad5-112">IoT Edge contains the following components:</span></span>

* <span data-ttu-id="d9ad5-113">Vooraf geschreven modules die algemene functies van de gateway uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="d9ad5-114">De interfaces die een ontwikkelaar kan gebruiken om aangepaste modules te schrijven.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-114">The interfaces a developer can use to write custom modules.</span></span>
* <span data-ttu-id="d9ad5-115">De infrastructuur die nodig is om een reeks modules te implementeren en uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-115">The infrastructure necessary to deploy and run a set of modules.</span></span>

<span data-ttu-id="d9ad5-116">De SDK biedt een abstractielaag waarmee u kunt bouwen gateways worden uitgevoerd op verschillende besturingssystemen en platforms.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-116">The SDK provides an abstraction layer that enables you to build gateways to run on various operating systems and platforms.</span></span>

![Azure IoT Edge-abstractielaag][2]

## <a name="messages"></a><span data-ttu-id="d9ad5-118">Berichten</span><span class="sxs-lookup"><span data-stu-id="d9ad5-118">Messages</span></span>

<span data-ttu-id="d9ad5-119">Hoewel de idee van modules die berichten aan elkaar doorgeven een handige manier is om te visualiseren hoe een gateway werkt, wordt hiermee niet nauwkeurig weergegeven wat er precies gebeurt.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-119">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="d9ad5-120">Een broker IoT Edge-modules gebruiken om te communiceren met elkaar.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-120">IoT Edge modules use a broker to communicate with each other.</span></span> <span data-ttu-id="d9ad5-121">Modules voor het publiceren van berichten naar de broker (messaging patronen, zoals bus of publiceren/abonneren met) en laat de broker routeren van het bericht met de modules die zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-121">Modules publish messages to the broker (using messaging patterns such as bus, or publish/subscribe) and then let the broker route the message to the modules connected to it.</span></span>

<span data-ttu-id="d9ad5-122">Een module gebruikt de functie **Broker_Publish** om een bericht naar de broker te publiceren.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-122">A module uses the **Broker_Publish** function to publish a message to the broker.</span></span> <span data-ttu-id="d9ad5-123">De broker levert berichten aan een module door een callbackfunctie te activeren.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-123">The broker delivers messages to a module by invoking a callback function.</span></span> <span data-ttu-id="d9ad5-124">Een bericht bestaat uit een reeks sleutel/waarde-eigenschappen en inhoud die als een blok geheugen worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![De rol van de broker in Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="d9ad5-126">Berichtroutering en filteren</span><span class="sxs-lookup"><span data-stu-id="d9ad5-126">Message routing and filtering</span></span>

<span data-ttu-id="d9ad5-127">Er zijn twee manieren om te leiden van berichten op de juiste IoT Edge-modules:</span><span class="sxs-lookup"><span data-stu-id="d9ad5-127">There are two ways to direct messages to the correct IoT Edge modules:</span></span>

* <span data-ttu-id="d9ad5-128">U kunt een set koppelingen doorgeven kunnen worden doorgegeven aan de broker, zodat de broker de bron- en sink voor elke module weet.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-128">You can pass a set of links can be passed to the broker so the broker knows the source and sink for each module.</span></span>
* <span data-ttu-id="d9ad5-129">Een module kunt filteren op de eigenschappen van het bericht.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-129">A module can filter on the properties of the message.</span></span>

<span data-ttu-id="d9ad5-130">Een module mag alleen reageren op een bericht als het bericht is bedoeld voor die module.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-130">A module should only act upon a message if the message is intended for it.</span></span> <span data-ttu-id="d9ad5-131">Koppelingen en effectief filteren bericht maakt een pijplijn bericht.</span><span class="sxs-lookup"><span data-stu-id="d9ad5-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9ad5-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d9ad5-132">Next steps</span></span>

<span data-ttu-id="d9ad5-133">Zie voor deze concepten die worden toegepast in een voorbeeld kunt u uitvoeren [verkennen Azure IoT rand architectuur][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="d9ad5-133">To see these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md