---
title: aaaGet de slag met Azure Relay hybride verbindingen in .NET | Microsoft Docs
description: Een consoletoepassing in C# schrijven voor hybride Relay-verbindingen van Azure.
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="a7005-103">Aan de slag met hybride Relay-verbindingen</span><span class="sxs-lookup"><span data-stu-id="a7005-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="a7005-104">Deze zelfstudie bevat een inleiding te[Azure Relay hybride verbindingen](relay-what-is-it.md#hybrid-connections), en wordt aangegeven hoe toouse .NET toocreate een clienttoepassing die verzendt berichten tooa bijbehorende listener-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a7005-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse .NET toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="a7005-105">Wat wordt bereikt</span><span class="sxs-lookup"><span data-stu-id="a7005-105">What will be accomplished</span></span>
<span data-ttu-id="a7005-106">Omdat voor hybride verbindingen vereist zowel een client en een serveronderdeel, maakt Hallo zelfstudie twee consoletoepassingen.</span><span class="sxs-lookup"><span data-stu-id="a7005-106">Because Hybrid Connections requires both a client and a server component, hello tutorial creates two console applications.</span></span> <span data-ttu-id="a7005-107">Hier volgen Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="a7005-107">Here are hello steps:</span></span>

1. <span data-ttu-id="a7005-108">Maak een Relay-naamruimte met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a7005-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="a7005-109">Een hybride verbinding maken in waarmee de naamruimte, met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a7005-109">Create a hybrid connection in that namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="a7005-110">Een (listener) serverconsole tooreceive toepassingsberichten schrijven.</span><span class="sxs-lookup"><span data-stu-id="a7005-110">Write a server (listener) console application tooreceive messages.</span></span>
4. <span data-ttu-id="a7005-111">Schrijven van een console-client (afzender) toosend toepassingsberichten.</span><span class="sxs-lookup"><span data-stu-id="a7005-111">Write a client (sender) console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7005-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a7005-112">Prerequisites</span></span>

<span data-ttu-id="a7005-113">toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="a7005-113">toocomplete this tutorial, you'll need hello following prerequisites:</span></span>

1. <span data-ttu-id="a7005-114">[Visual Studio 2015 of hoger](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="a7005-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="a7005-115">Hallo-voorbeelden in deze zelfstudie gebruikt Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a7005-115">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="a7005-116">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a7005-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="a7005-117">1. Maken van een naamruimte met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="a7005-117">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="a7005-118">Als u al een Relay-naamruimte hebt gemaakt, gaan toohello [een hybride verbinding maken met Azure-portal Hallo](#2-create-a-hybrid-connection-using-the-azure-portal) sectie.</span><span class="sxs-lookup"><span data-stu-id="a7005-118">If you have already created a Relay namespace, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="a7005-119">2. Een hybride verbinding maken met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="a7005-119">2. Create a hybrid connection using hello Azure portal</span></span>
<span data-ttu-id="a7005-120">Als u al een hybride verbinding hebt gemaakt, gaan toohello [maken van een servertoepassing](#3-create-a-server-application-listener) sectie.</span><span class="sxs-lookup"><span data-stu-id="a7005-120">If you have already created a hybrid connection, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="a7005-121">3. Een servertoepassing (listener) maken</span><span class="sxs-lookup"><span data-stu-id="a7005-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="a7005-122">toolisten en ontvangen van berichten van Hallo Relay, we een C#-consoletoepassing met Visual Studio worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="a7005-122">toolisten and receive messages from hello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="a7005-123">4. Een clienttoepassing maken (afzender)</span><span class="sxs-lookup"><span data-stu-id="a7005-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="a7005-124">toosend berichten toohello sturen we een C#-consoletoepassing met Visual Studio worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="a7005-124">toosend messages toohello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="a7005-125">5. Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a7005-125">5. Run hello applications</span></span>
1. <span data-ttu-id="a7005-126">Hallo-servertoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a7005-126">Run hello server application.</span></span>
2. <span data-ttu-id="a7005-127">Voer Hallo-clienttoepassing en tekst opgeven.</span><span class="sxs-lookup"><span data-stu-id="a7005-127">Run hello client application and enter some text.</span></span>
3. <span data-ttu-id="a7005-128">Zorg ervoor dat die server Hallo toepassing console uitvoer Hallo tekst die is ingevoerd in de clienttoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="a7005-128">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![actieve-toepassingen](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="a7005-130">Gefeliciteerd, u hebt een end-to-end toepassing met hybride verbindingen gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a7005-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7005-131">Volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="a7005-131">Next steps:</span></span>
* [<span data-ttu-id="a7005-132">Veelgestelde vragen over Relay</span><span class="sxs-lookup"><span data-stu-id="a7005-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="a7005-133">Een naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="a7005-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="a7005-134">Aan de slag met knooppunten</span><span class="sxs-lookup"><span data-stu-id="a7005-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

