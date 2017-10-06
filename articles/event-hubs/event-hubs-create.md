---
title: een Azure event hub aaaCreate | Microsoft Docs
description: Maak een Azure Event Hubs-naamruimte en een event hub met hello Azure-portal
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a><span data-ttu-id="0bdc3-103">Maak een Event Hubs-naamruimte en een event hub met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0bdc3-103">Create an Event Hubs namespace and an event hub using hello Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="0bdc3-104">Een Event Hubs-naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="0bdc3-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="0bdc3-105">Meld u aan toohello [Azure-portal][Azure portal], en klik op **nieuw** op Hallo linksboven welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-105">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
1. <span data-ttu-id="0bdc3-106">Klik op **Internet der dingen**, en klik vervolgens op **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="0bdc3-107">In Hallo **naamruimte maken** blade, voer de naam van een naamruimte.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-107">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="0bdc3-108">Hallo-systeem wordt onmiddellijk toosee gecontroleerd als Hallo naam beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-108">hello system immediately checks toosee if hello name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="0bdc3-109">Nadat u hebt ervoor Hallo naamruimtenaam is beschikbaar, kies Hallo prijscategorie (basis of standaard).</span><span class="sxs-lookup"><span data-stu-id="0bdc3-109">After making sure hello namespace name is available, choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="0bdc3-110">Ook een Azure-abonnement, resourcegroep en locatie kiezen in welke toocreate Hallo-resource.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-110">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> 
1. <span data-ttu-id="0bdc3-111">Klik op **maken** toocreate Hallo naamruimte.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-111">Click **Create** toocreate hello namespace.</span></span> <span data-ttu-id="0bdc3-112">Mogelijk hebt u toowait een paar minuten voordat Hallo toofully inrichten Hallo systeembronnen.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-112">You may have toowait a few minutes for hello system toofully provision hello resources.</span></span>
2. <span data-ttu-id="0bdc3-113">Klik in de Hallo portal lijst met naamruimten, Hallo zojuist-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-113">In hello portal list of namespaces, click hello newly created namespace.</span></span>
2. <span data-ttu-id="0bdc3-114">Klik op **gedeeld toegangsbeleid**, en klik vervolgens op **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="0bdc3-115">Klik op Hallo kopie knop toocopy Hallo **RootManageSharedAccessKey** connection string toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-115">Click hello copy button toocopy hello **RootManageSharedAccessKey** connection string toohello clipboard.</span></span> <span data-ttu-id="0bdc3-116">Sla deze verbindingsreeks in een tijdelijke locatie, zoals Kladblok, toouse later.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-116">Save this connection string in a temporary location, such as Notepad, toouse later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="0bdc3-117">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="0bdc3-117">Create an event hub</span></span>

1. <span data-ttu-id="0bdc3-118">Klik op nieuw gemaakte Hallo naamruimte in Hallo Event Hubs naamruimte lijst.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-118">In hello Event Hubs namespace list, click hello newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="0bdc3-119">Klik op Hallo naamruimte blade **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-119">In hello namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="0bdc3-120">Klik boven Hallo van Hallo-blade op **Event Hub toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-120">At hello top of hello blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="0bdc3-121">Typ een naam voor uw event hub en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="0bdc3-122">Uw event hub is nu gemaakt en u hebt de verbindingsreeksen Hallo u toosend nodig hebt en gebeurtenissen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="0bdc3-122">Your event hub is now created, and you have hello connection strings you need toosend and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bdc3-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0bdc3-123">Next steps</span></span>
<span data-ttu-id="0bdc3-124">toolearn meer informatie over Event Hubs, gaat u naar deze koppelingen:</span><span class="sxs-lookup"><span data-stu-id="0bdc3-124">toolearn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="0bdc3-125">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="0bdc3-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="0bdc3-126">Event Hubs-API-overzicht</span><span class="sxs-lookup"><span data-stu-id="0bdc3-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/