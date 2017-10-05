---
title: Aan de slag met hybride Relay-verbindingen van Azure in .NET | Microsoft Docs
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
ms.openlocfilehash: 1af23bfd46dd7d3781505473f7c1d86e65ea9bc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="d4b48-103">Aan de slag met hybride Relay-verbindingen</span><span class="sxs-lookup"><span data-stu-id="d4b48-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="d4b48-104">Deze zelfstudie biedt een inleiding tot [hybride Relay-verbindingen van Azure](relay-what-is-it.md#hybrid-connections) en laat zien hoe u .NET gebruikt om een clienttoepassing te maken waarmee berichten worden verzonden naar een corresponderende listener-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d4b48-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use .NET to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="d4b48-105">Wat wordt bereikt</span><span class="sxs-lookup"><span data-stu-id="d4b48-105">What will be accomplished</span></span>
<span data-ttu-id="d4b48-106">Omdat hybride verbindingen zowel een client- als een serveronderdeel vereisen, worden in de zelfstudie twee consoletoepassingen gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d4b48-106">Because Hybrid Connections requires both a client and a server component, the tutorial creates two console applications.</span></span> <span data-ttu-id="d4b48-107">Dit zijn de stappen:</span><span class="sxs-lookup"><span data-stu-id="d4b48-107">Here are the steps:</span></span>

1. <span data-ttu-id="d4b48-108">Een Relay-naamruimte maken met behulp van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d4b48-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="d4b48-109">Een hybride verbinding maken in die naamruimte, met behulp van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d4b48-109">Create a hybrid connection in that namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="d4b48-110">Een serverconsoletoepassing (listener) schrijven om berichten te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d4b48-110">Write a server (listener) console application to receive messages.</span></span>
4. <span data-ttu-id="d4b48-111">Een clientconsoletoepassing (afzender) schrijven om berichten te verzenden.</span><span class="sxs-lookup"><span data-stu-id="d4b48-111">Write a client (sender) console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4b48-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d4b48-112">Prerequisites</span></span>

<span data-ttu-id="d4b48-113">Voor het voltooien van deze zelfstudie moet aan de volgende vereisten worden voldaan:</span><span class="sxs-lookup"><span data-stu-id="d4b48-113">To complete this tutorial, you'll need the following prerequisites:</span></span>

1. <span data-ttu-id="d4b48-114">[Visual Studio 2015 of hoger](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="d4b48-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="d4b48-115">In de voorbeelden in deze zelfstudie wordt Visual Studio 2017 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d4b48-115">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="d4b48-116">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d4b48-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="d4b48-117">1. Een naamruimte maken met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d4b48-117">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="d4b48-118">Als u al een Relay-naamruimte hebt gemaakt, gaat u naar de sectie [Een hybride verbinding maken met behulp van Azure Portal](#2-create-a-hybrid-connection-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="d4b48-118">If you have already created a Relay namespace, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="d4b48-119">2. Een hybride verbinding maken met behulp van Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d4b48-119">2. Create a hybrid connection using the Azure portal</span></span>
<span data-ttu-id="d4b48-120">Als u al een hybride verbinding hebt gemaakt, gaat u naar de sectie [Een servertoepassing maken](#3-create-a-server-application-listener).</span><span class="sxs-lookup"><span data-stu-id="d4b48-120">If you have already created a hybrid connection, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="d4b48-121">3. Een servertoepassing (listener) maken</span><span class="sxs-lookup"><span data-stu-id="d4b48-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="d4b48-122">We maken een C#-consoletoepassing met Visual Studio om berichten van de Relay te beluisteren en te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d4b48-122">To listen and receive messages from the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="d4b48-123">4. Een clienttoepassing maken (afzender)</span><span class="sxs-lookup"><span data-stu-id="d4b48-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="d4b48-124">We maken een C#-consoletoepassing met Visual Studio om berichten naar de Relay te verzenden.</span><span class="sxs-lookup"><span data-stu-id="d4b48-124">To send messages to the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="d4b48-125">5. De toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d4b48-125">5. Run the applications</span></span>
1. <span data-ttu-id="d4b48-126">Voer de servertoepassing uit.</span><span class="sxs-lookup"><span data-stu-id="d4b48-126">Run the server application.</span></span>
2. <span data-ttu-id="d4b48-127">Voer de clienttoepassing uit en voer wat tekst in.</span><span class="sxs-lookup"><span data-stu-id="d4b48-127">Run the client application and enter some text.</span></span>
3. <span data-ttu-id="d4b48-128">Zorg ervoor dat de servertoepassingsconsole de tekst uitvoert die in de clienttoepassing is ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="d4b48-128">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![actieve-toepassingen](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="d4b48-130">Gefeliciteerd, u hebt een end-to-end toepassing met hybride verbindingen gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d4b48-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4b48-131">Volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="d4b48-131">Next steps:</span></span>
* [<span data-ttu-id="d4b48-132">Veelgestelde vragen over Relay</span><span class="sxs-lookup"><span data-stu-id="d4b48-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="d4b48-133">Een naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="d4b48-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="d4b48-134">Aan de slag met knooppunten</span><span class="sxs-lookup"><span data-stu-id="d4b48-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

