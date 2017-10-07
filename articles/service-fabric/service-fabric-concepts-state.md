---
title: aaaDefinine en beheren van de status in Azure microservices | Microsoft Docs
description: Hoe toodefine en beheren van de status in Service Fabric-service
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
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a><span data-ttu-id="018ec-103">Servicestatus</span><span class="sxs-lookup"><span data-stu-id="018ec-103">Service state</span></span>
<span data-ttu-id="018ec-104">**Status service** toohello in het geheugen of op dat een service toofunction vereist schijfgegevens verwijst.</span><span class="sxs-lookup"><span data-stu-id="018ec-104">**Service state** refers toohello in-memory or on disk data that a service requires toofunction.</span></span> <span data-ttu-id="018ec-105">Deze omvatten, bijvoorbeeld Hallo gegevensstructuren en lidvariabelen die Hallo-service leest en schrijft toodo werk.</span><span class="sxs-lookup"><span data-stu-id="018ec-105">It includes, for example, hello data structures and member variables that hello service reads and writes toodo work.</span></span> <span data-ttu-id="018ec-106">Afhankelijk van hoe Hallo-service is ontworpen, kan deze ook bestanden of andere bronnen die zijn opgeslagen op schijf bevatten.</span><span class="sxs-lookup"><span data-stu-id="018ec-106">Depending on how hello service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="018ec-107">Bijvoorbeeld Hallo bestanden voor een database toostore gegevens en transactie-logboeken zou gebruiken.</span><span class="sxs-lookup"><span data-stu-id="018ec-107">For example, hello files a database would use toostore data and transaction logs.</span></span>

<span data-ttu-id="018ec-108">Als een service voorbeeld laten we eens een rekenmachine.</span><span class="sxs-lookup"><span data-stu-id="018ec-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="018ec-109">Een service basisrekenmachine neemt twee getallen en retourneert de som.</span><span class="sxs-lookup"><span data-stu-id="018ec-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="018ec-110">Uitvoeren van deze berekening omvat geen lidvariabelen of andere informatie.</span><span class="sxs-lookup"><span data-stu-id="018ec-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="018ec-111">Bekijk nu dezelfde Rekenmachine hello, maar met een aanvullende methode voor het opslaan en retourneren van de laatste som Hallo het berekend.</span><span class="sxs-lookup"><span data-stu-id="018ec-111">Now consider hello same calculator, but with an additional method for storing and returning hello last sum it has computed.</span></span> <span data-ttu-id="018ec-112">Deze service is nu stateful.</span><span class="sxs-lookup"><span data-stu-id="018ec-112">This service is now stateful.</span></span> <span data-ttu-id="018ec-113">Stateful betekent dat deze bevat een aantal met toowhen deze wordt een nieuwe som berekend en leest uit wanneer u deze tooreturn Hallo laatste berekende som vraagt worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="018ec-113">Stateful means it contains some state that it writes toowhen it computes a new sum and reads from when you ask it tooreturn hello last computed sum.</span></span>

<span data-ttu-id="018ec-114">In de Azure Service Fabric Hallo eerste service een stateless service genoemd.</span><span class="sxs-lookup"><span data-stu-id="018ec-114">In Azure Service Fabric, hello first service is called a stateless service.</span></span> <span data-ttu-id="018ec-115">Hallo tweede service wordt een stateful service genoemd.</span><span class="sxs-lookup"><span data-stu-id="018ec-115">hello second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="018ec-116">Opslaan van de status van service</span><span class="sxs-lookup"><span data-stu-id="018ec-116">Storing service state</span></span>
<span data-ttu-id="018ec-117">Status worden ofwel externalized of CO-locaties met Hallo-code die is Hallo status bewerken.</span><span class="sxs-lookup"><span data-stu-id="018ec-117">State can be either externalized or co-located with hello code that is manipulating hello state.</span></span> <span data-ttu-id="018ec-118">Externalization van staat gewoonlijk wordt uitgevoerd met behulp van een externe database of ander gegevensarchief dat wordt uitgevoerd op verschillende computers via Hallo netwerk of buiten het proces op dezelfde machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="018ec-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over hello network or out of process on hello same machine.</span></span> <span data-ttu-id="018ec-119">In ons voorbeeld Rekenmachine Hallo gegevensarchief mogelijk een SQL-database of een exemplaar van Azure Table-Store.</span><span class="sxs-lookup"><span data-stu-id="018ec-119">In our calculator example, hello data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="018ec-120">Elke aanvraag toocompute Hallo som voert een update op deze gegevens en toohello service tooreturn Hallo waarde resultaat in de huidige Hallo-waarde wordt opgehaald uit de store Hallo-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="018ec-120">Every request toocompute hello sum performs an update on this data, and requests toohello service tooreturn hello value result in hello current value being fetched from hello store.</span></span> 

<span data-ttu-id="018ec-121">Status kan ook worden geplaatst met Hallo-code die Hallo status bewerkt.</span><span class="sxs-lookup"><span data-stu-id="018ec-121">State can also be co-located with hello code that manipulates hello state.</span></span> <span data-ttu-id="018ec-122">Stateful services in Service Fabric zijn doorgaans gebouwd met behulp van dit model.</span><span class="sxs-lookup"><span data-stu-id="018ec-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="018ec-123">Service Fabric bevat Hallo infrastructuur tooensure dat deze status maximaal beschikbaar, consistent en duurzame is en dat Hallo-services op deze manier opgebouwd eenvoudig kunt schalen.</span><span class="sxs-lookup"><span data-stu-id="018ec-123">Service Fabric provides hello infrastructure tooensure that this state is highly available, consistent, and durable, and that hello services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="018ec-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="018ec-124">Next steps</span></span>
<span data-ttu-id="018ec-125">Zie voor meer informatie over Service Fabric-concepten Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="018ec-125">For more information on Service Fabric concepts, see hello following articles:</span></span>

* [<span data-ttu-id="018ec-126">Beschikbaarheid van Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="018ec-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="018ec-127">Schaalbaarheid van Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="018ec-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="018ec-128">Partitionering Service Fabric-services</span><span class="sxs-lookup"><span data-stu-id="018ec-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="018ec-129">Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="018ec-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
