---
title: aaaGet de slag met Azure Relay hybride verbindingen in knooppunt | Microsoft Docs
description: Een knooppuntconsoletoepassing schrijven voor hybride Relay-verbindingen van Azure.
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="d9e3e-103">Aan de slag met hybride Relay-verbindingen</span><span class="sxs-lookup"><span data-stu-id="d9e3e-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="d9e3e-104">Deze zelfstudie bevat een inleiding te[Azure Relay hybride verbindingen](relay-what-is-it.md#hybrid-connections), en wordt aangegeven hoe toouse Node.js toocreate een clienttoepassing die verzendt berichten tooa bijbehorende listener-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse Node.js toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="d9e3e-105">Wat wordt bereikt</span><span class="sxs-lookup"><span data-stu-id="d9e3e-105">What will be accomplished</span></span>

<span data-ttu-id="d9e3e-106">Omdat voor hybride verbindingen zowel een client- als een serveronderdeel is vereist, maken we in deze zelfstudie twee consoletoepassingen.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="d9e3e-107">Hier volgen Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="d9e3e-107">Here are hello steps:</span></span>

1. <span data-ttu-id="d9e3e-108">Maak een Relay-naamruimte met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="d9e3e-109">Een hybride verbinding maken, met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-109">Create a hybrid connection, using hello Azure portal.</span></span>
3. <span data-ttu-id="d9e3e-110">Een server console toepassing tooreceive berichten schrijven.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-110">Write a server console application tooreceive messages.</span></span>
4. <span data-ttu-id="d9e3e-111">Een client console toepassing toosend berichten schrijven.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-111">Write a client console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9e3e-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d9e3e-112">Prerequisites</span></span>

1. <span data-ttu-id="d9e3e-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="d9e3e-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="d9e3e-114">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="d9e3e-115">1. Maken van een naamruimte met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d9e3e-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="d9e3e-116">Als u al een Relay-naamruimte gemaakt, gaan toohello [een hybride verbinding maken met Azure-portal Hallo](#2-create-a-hybrid-connection-using-the-azure-portal) sectie.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-116">If you already have a Relay namespace created, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="d9e3e-117">2. Een hybride verbinding maken met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d9e3e-117">2. Create a hybrid connection using hello Azure portal</span></span>

<span data-ttu-id="d9e3e-118">Als u al een hybride verbinding gemaakt, gaan toohello [maken van een servertoepassing](#3-create-a-server-application-listener) sectie.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-118">If you already have a hybrid connection created, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="d9e3e-119">3. Een servertoepassing (listener) maken</span><span class="sxs-lookup"><span data-stu-id="d9e3e-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="d9e3e-120">toolisten en ontvangen van Hallo Relay, wordt er een Node.js-consoletoepassing schrijven.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-120">toolisten and receive messages from hello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="d9e3e-121">4. Een clienttoepassing maken (afzender)</span><span class="sxs-lookup"><span data-stu-id="d9e3e-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="d9e3e-122">toosend berichten toohello Relay, wordt er een Node.js-consoletoepassing schrijven.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-122">toosend messages toohello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="d9e3e-123">5. Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d9e3e-123">5. Run hello applications</span></span>

1. <span data-ttu-id="d9e3e-124">Uitvoeren van de servertoepassing Hallo: vanaf een opdrachtprompt te typen Node.js `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-124">Run hello server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="d9e3e-125">Hallo-clienttoepassing uitvoert: vanaf een opdrachtprompt te typen Node.js `node sender.js`, en voer tekst in.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-125">Run hello client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="d9e3e-126">Zorg ervoor dat die server Hallo toepassing console uitvoer Hallo tekst die is ingevoerd in de clienttoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9e3e-126">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![actieve-toepassingen](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="d9e3e-128">Gefeliciteerd, u hebt een end-to-endtoepassing met hybride verbindingen gemaakt met behulp van Node.js!</span><span class="sxs-lookup"><span data-stu-id="d9e3e-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9e3e-129">Volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="d9e3e-129">Next steps:</span></span>

* [<span data-ttu-id="d9e3e-130">Veelgestelde vragen over Relay</span><span class="sxs-lookup"><span data-stu-id="d9e3e-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="d9e3e-131">Een naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="d9e3e-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="d9e3e-132">Aan de slag met .NET</span><span class="sxs-lookup"><span data-stu-id="d9e3e-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="d9e3e-133">Aan de slag met knooppunten</span><span class="sxs-lookup"><span data-stu-id="d9e3e-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

