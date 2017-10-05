---
title: Definine en beheren van de status in Azure microservices | Microsoft Docs
description: "Het definiëren en beheren van de status in Service Fabric-service"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 2f7835fab175bdb7ef7ce3894cab9e09a39457f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="service-state"></a><span data-ttu-id="b95ea-103">Servicestatus</span><span class="sxs-lookup"><span data-stu-id="b95ea-103">Service state</span></span>
<span data-ttu-id="b95ea-104">**Status service** verwijst naar het geheugen of van schijfgegevens die een service nodig heeft om de functie.</span><span class="sxs-lookup"><span data-stu-id="b95ea-104">**Service state** refers to the in-memory or on disk data that a service requires to function.</span></span> <span data-ttu-id="b95ea-105">Het kan bijvoorbeeld omvat de gegevensstructuren en variabelen die de service leest en schrijft om te werken.</span><span class="sxs-lookup"><span data-stu-id="b95ea-105">It includes, for example, the data structures and member variables that the service reads and writes to do work.</span></span> <span data-ttu-id="b95ea-106">Afhankelijk van hoe de service is ontworpen, kan deze ook bestanden of andere bronnen die zijn opgeslagen op schijf bevatten.</span><span class="sxs-lookup"><span data-stu-id="b95ea-106">Depending on how the service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="b95ea-107">Bijvoorbeeld, de bestanden een database wilt gebruiken voor het opslaan van gegevens en de transactielogboeken.</span><span class="sxs-lookup"><span data-stu-id="b95ea-107">For example, the files a database would use to store data and transaction logs.</span></span>

<span data-ttu-id="b95ea-108">Als een service voorbeeld laten we eens een rekenmachine.</span><span class="sxs-lookup"><span data-stu-id="b95ea-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="b95ea-109">Een service basisrekenmachine neemt twee getallen en retourneert de som.</span><span class="sxs-lookup"><span data-stu-id="b95ea-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="b95ea-110">Uitvoeren van deze berekening omvat geen lidvariabelen of andere informatie.</span><span class="sxs-lookup"><span data-stu-id="b95ea-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="b95ea-111">Bekijk nu de Rekenmachine van dezelfde, maar met een aanvullende methode voor het opslaan en retourneert de som van de laatste het berekend.</span><span class="sxs-lookup"><span data-stu-id="b95ea-111">Now consider the same calculator, but with an additional method for storing and returning the last sum it has computed.</span></span> <span data-ttu-id="b95ea-112">Deze service is nu stateful.</span><span class="sxs-lookup"><span data-stu-id="b95ea-112">This service is now stateful.</span></span> <span data-ttu-id="b95ea-113">Stateful betekent dat deze een status waarin schrijft naar wanneer dit wordt een nieuwe som berekend en leest uit wanneer u vraagt om de laatste berekende som terug te bevat.</span><span class="sxs-lookup"><span data-stu-id="b95ea-113">Stateful means it contains some state that it writes to when it computes a new sum and reads from when you ask it to return the last computed sum.</span></span>

<span data-ttu-id="b95ea-114">In de Azure Service Fabric is de eerste service een stateless service genoemd.</span><span class="sxs-lookup"><span data-stu-id="b95ea-114">In Azure Service Fabric, the first service is called a stateless service.</span></span> <span data-ttu-id="b95ea-115">De tweede service een stateful service genoemd.</span><span class="sxs-lookup"><span data-stu-id="b95ea-115">The second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="b95ea-116">Opslaan van de status van service</span><span class="sxs-lookup"><span data-stu-id="b95ea-116">Storing service state</span></span>
<span data-ttu-id="b95ea-117">Status worden ofwel externalized of door de code die de status is bewerken met CO-locaties.</span><span class="sxs-lookup"><span data-stu-id="b95ea-117">State can be either externalized or co-located with the code that is manipulating the state.</span></span> <span data-ttu-id="b95ea-118">Externalization van staat gewoonlijk wordt uitgevoerd met behulp van een externe database of ander gegevensarchief die wordt uitgevoerd op verschillende computers via het netwerk of buiten het proces op dezelfde machine.</span><span class="sxs-lookup"><span data-stu-id="b95ea-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over the network or out of process on the same machine.</span></span> <span data-ttu-id="b95ea-119">In ons voorbeeld Rekenmachine kan het gegevensarchief worden een SQL-database of een exemplaar van Azure Table-Store.</span><span class="sxs-lookup"><span data-stu-id="b95ea-119">In our calculator example, the data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="b95ea-120">Elke aanvraag voor het berekenen van de som, voert een update op deze gegevens en aanvragen bij de service te retourneren van het resultaat van de waarde in de huidige waarde wordt opgehaald uit de store.</span><span class="sxs-lookup"><span data-stu-id="b95ea-120">Every request to compute the sum performs an update on this data, and requests to the service to return the value result in the current value being fetched from the store.</span></span> 

<span data-ttu-id="b95ea-121">Status kan ook worden geplaatst met de code die de status wordt bewerkt.</span><span class="sxs-lookup"><span data-stu-id="b95ea-121">State can also be co-located with the code that manipulates the state.</span></span> <span data-ttu-id="b95ea-122">Stateful services in Service Fabric zijn doorgaans gebouwd met behulp van dit model.</span><span class="sxs-lookup"><span data-stu-id="b95ea-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="b95ea-123">Service Fabric levert de infrastructuur om ervoor te zorgen dat deze status maximaal beschikbaar, consistent en duurzame is en dat de services op deze manier opgebouwd eenvoudig kunt schalen.</span><span class="sxs-lookup"><span data-stu-id="b95ea-123">Service Fabric provides the infrastructure to ensure that this state is highly available, consistent, and durable, and that the services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b95ea-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b95ea-124">Next steps</span></span>
<span data-ttu-id="b95ea-125">Zie de volgende artikelen voor meer informatie over Service Fabric-concepten:</span><span class="sxs-lookup"><span data-stu-id="b95ea-125">For more information on Service Fabric concepts, see the following articles:</span></span>

* [<span data-ttu-id="b95ea-126">Beschikbaarheid van Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="b95ea-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="b95ea-127">Schaalbaarheid van Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="b95ea-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="b95ea-128">Partitionering Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="b95ea-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="b95ea-129">Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="b95ea-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
