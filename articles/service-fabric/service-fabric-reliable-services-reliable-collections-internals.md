---
title: Interne werking van Azure Service Fabric betrouwbaar status Manager en betrouwbare verzameling | Microsoft Docs
description: Deep dive op betrouwbare verzameling concepten en ontwerp in Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: d607449a16e886337ab1bd96213fbb4231124353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="9bd7a-103">Interne werking van Azure Service Fabric betrouwbaar status Manager en betrouwbare verzameling</span><span class="sxs-lookup"><span data-stu-id="9bd7a-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="9bd7a-104">Dit document delves in een betrouwbare statusbeheer en betrouwbare verzamelingen om te zien hoe de basisonderdelen die achter de schermen werken.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-104">This document delves inside Reliable State Manager and Reliable Collections to see how core components work behind the scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="9bd7a-105">Dit document is werk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-105">This document is work in-progress.</span></span> <span data-ttu-id="9bd7a-106">Opmerkingen toevoegen aan dit artikel voor Vertel ons wat u meer informatie wilt over onderwerp.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-106">Add comments to this article to tell us what topic you would like to learn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="9bd7a-107">Lokale persistentie model: logboek- en controlepunt</span><span class="sxs-lookup"><span data-stu-id="9bd7a-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="9bd7a-108">De betrouwbare statusbeheer en betrouwbare verzamelingen Volg een model voor persistentie logboek- en controlepunt wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-108">The Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="9bd7a-109">In dit model wordt elke wijziging in de status op de schijf voor het eerst geregistreerd en vervolgens toegepast in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="9bd7a-110">De status van de volledige zelf is alleen sporadisch persistent (ook</span><span class="sxs-lookup"><span data-stu-id="9bd7a-110">The complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="9bd7a-111">Controlepunt).</span><span class="sxs-lookup"><span data-stu-id="9bd7a-111">Checkpoint).</span></span>
<span data-ttu-id="9bd7a-112">Het voordeel is dat de delta's zijn ingeschakeld in opeenvolgende alleen toevoegen schrijfbewerkingen op de schijf voor betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-112">The benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="9bd7a-113">Om het logboek en controlepunt model beter te begrijpen we eerst kijken naar het scenario voor oneindige schijven.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-113">To better understand the Log and Checkpoint model, let’s first look at the infinite disk scenario.</span></span>
<span data-ttu-id="9bd7a-114">Statusbeheer voor het betrouwbare registreert elke bewerking voordat deze worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-114">The Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="9bd7a-115">Logboekregistratie kan de betrouwbare verzamelingen om toe te passen van de bewerking alleen in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-115">Logging allows the Reliable Collections to apply the operation only in memory.</span></span>
<span data-ttu-id="9bd7a-116">Omdat logboeken zijn persistent hebt gemaakt, zelfs wanneer de replica is mislukt en moet opnieuw worden opgestart, heeft de betrouwbare status Manager voldoende informatie in het logboek voor de replay van alle bewerkingen van die de replica is verbroken.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-116">Since logs are persisted, even when the replica fails and needs to be restarted, the Reliable State Manager has enough information in its log to replay all the operations the replica has lost.</span></span>
<span data-ttu-id="9bd7a-117">Als de schijf oneindig is, logboekrecords nooit moeten worden verwijderd en de betrouwbare verzameling moet de status van de in het geheugen te beheren.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-117">As the disk is infinite, log records never need to be removed and the Reliable Collection needs to manage only the in-memory state.</span></span>

<span data-ttu-id="9bd7a-118">Nu bekijken we het scenario voor eindig schijven.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-118">Now let’s look at the finite disk scenario.</span></span>
<span data-ttu-id="9bd7a-119">Zoals logboekrecords verzamelen, voert de betrouwbare statusbeheer onvoldoende schijfruimte.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-119">As log records accumulate, the Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="9bd7a-120">Voordat dit gebeurt, moet betrouwbare statusbeheer voor het afkappen van het logboek ruimte te maken voor de nieuwere records.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-120">Before that happens, the Reliable State Manager needs to truncate its log to make room for the newer records.</span></span>
<span data-ttu-id="9bd7a-121">Statusbeheer voor betrouwbare aanvragen de betrouwbare verzamelingen controlepunt hun status in het geheugen naar schijf.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-121">Reliable State Manager requests the Reliable Collections to checkpoint their in-memory state to disk.</span></span>
<span data-ttu-id="9bd7a-122">Op dit moment zou de betrouwbare verzamelingen blijven behouden de status in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-122">At this point, the Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="9bd7a-123">Zodra de betrouwbare verzamelingen hun controlepunten hebt voltooid, kan de betrouwbare status Manager het logboek aan schijfruimte vrij afkappen.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-123">Once the Reliable Collections complete their checkpoints, the Reliable State Manager can truncate the log to free up disk space.</span></span>
<span data-ttu-id="9bd7a-124">Als de replica moet opnieuw worden opgestart, betrouwbare verzamelingen hun controlepunt herstellen en statusbeheer voor het betrouwbare herstelt en alle wijzigingen die sinds het laatste controlepunt afspeelt.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-124">When the replica needs to be restarted, Reliable Collections recover their checkpointed state, and the Reliable State Manager recovers and plays back all the state changes that occurred since the last checkpoint.</span></span>

<span data-ttu-id="9bd7a-125">Een andere waarde toevoegen van controlepunten is dat het verbetert de hersteltijden in algemene scenario's.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="9bd7a-126">Het logboek bevat alle bewerkingen die zich hebben voorgedaan sinds het laatste controlepunt.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-126">Log contains all operations that have happened since the last checkpoint.</span></span>
<span data-ttu-id="9bd7a-127">Deze kan dus meerdere versies van een item, zoals meerdere waarden voor een bepaalde rij in betrouwbare woordenlijst bevatten.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="9bd7a-128">Een betrouwbare verzameling controlepunten daarentegen alleen de meest recente versie van elke waarde voor een sleutel.</span><span class="sxs-lookup"><span data-stu-id="9bd7a-128">In contrast, a Reliable Collection checkpoints only the latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bd7a-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9bd7a-129">Next steps</span></span>
* [<span data-ttu-id="9bd7a-130">Transacties en vergrendelingen</span><span class="sxs-lookup"><span data-stu-id="9bd7a-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

