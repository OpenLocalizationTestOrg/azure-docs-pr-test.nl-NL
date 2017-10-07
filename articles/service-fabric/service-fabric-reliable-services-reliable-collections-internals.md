---
title: interne werking van Service Fabric betrouwbare status Manager en betrouwbare verzameling aaaAzure | Microsoft Docs
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
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="064f5-103">Interne werking van Azure Service Fabric betrouwbaar status Manager en betrouwbare verzameling</span><span class="sxs-lookup"><span data-stu-id="064f5-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="064f5-104">Dit document delves binnen betrouwbare statusbeheer en betrouwbare verzamelingen toosee hoe kernonderdelen achter de schermen Hallo werken.</span><span class="sxs-lookup"><span data-stu-id="064f5-104">This document delves inside Reliable State Manager and Reliable Collections toosee how core components work behind hello scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="064f5-105">Dit document is werk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="064f5-105">This document is work in-progress.</span></span> <span data-ttu-id="064f5-106">Voeg opmerkingen toothis artikel tootell ons welke onderwerp u graag meer informatie over toolearn.</span><span class="sxs-lookup"><span data-stu-id="064f5-106">Add comments toothis article tootell us what topic you would like toolearn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="064f5-107">Lokale persistentie model: logboek- en controlepunt</span><span class="sxs-lookup"><span data-stu-id="064f5-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="064f5-108">Ga als volgt een persistentie model dat wordt aangeroepen logboek- en controlepunt Hallo betrouwbare statusbeheer en betrouwbare verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="064f5-108">hello Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="064f5-109">In dit model wordt elke wijziging in de status op de schijf voor het eerst geregistreerd en vervolgens toegepast in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="064f5-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="064f5-110">Hallo voltooid staat zelf is alleen sporadisch persistent (ook</span><span class="sxs-lookup"><span data-stu-id="064f5-110">hello complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="064f5-111">Controlepunt).</span><span class="sxs-lookup"><span data-stu-id="064f5-111">Checkpoint).</span></span>
<span data-ttu-id="064f5-112">Hallo voordeel is dat de delta's zijn ingeschakeld in opeenvolgende alleen toevoegen schrijfbewerkingen op de schijf voor betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="064f5-112">hello benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="064f5-113">toobetter hello logboek- en controlepunt model begrijpen, laten we eerst bekijkt hello oneindige schijf scenario.</span><span class="sxs-lookup"><span data-stu-id="064f5-113">toobetter understand hello Log and Checkpoint model, let’s first look at hello infinite disk scenario.</span></span>
<span data-ttu-id="064f5-114">Hallo betrouwbare status Manager registreert elke bewerking voordat deze worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="064f5-114">hello Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="064f5-115">Hallo betrouwbare verzamelingen tooapply Hallo bewerking kan logboekregistratie alleen in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="064f5-115">Logging allows hello Reliable Collections tooapply hello operation only in memory.</span></span>
<span data-ttu-id="064f5-116">Omdat logboeken zijn persistent hebt gemaakt, zelfs wanneer Hallo replica mislukt en toobe opnieuw is opgestart, moet heeft Hallo betrouwbare statusbeheer voldoende informatie in het logboek tooreplay alle Hallo bewerkingen Hallo replica heeft verloren.</span><span class="sxs-lookup"><span data-stu-id="064f5-116">Since logs are persisted, even when hello replica fails and needs toobe restarted, hello Reliable State Manager has enough information in its log tooreplay all hello operations hello replica has lost.</span></span>
<span data-ttu-id="064f5-117">Als het Hallo-schijf is oneindig, logboekrecords nooit moeten toobe verwijderd en hello betrouwbare verzameling moet toomanage alleen Hallo geheugenstatus.</span><span class="sxs-lookup"><span data-stu-id="064f5-117">As hello disk is infinite, log records never need toobe removed and hello Reliable Collection needs toomanage only hello in-memory state.</span></span>

<span data-ttu-id="064f5-118">Nu gaan we kijken Hallo eindig schijf scenario.</span><span class="sxs-lookup"><span data-stu-id="064f5-118">Now let’s look at hello finite disk scenario.</span></span>
<span data-ttu-id="064f5-119">Zoals logboekrecords verzamelen, voert Hallo betrouwbare statusbeheer onvoldoende schijfruimte.</span><span class="sxs-lookup"><span data-stu-id="064f5-119">As log records accumulate, hello Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="064f5-120">Voordat dit gebeurt, moet Hallo betrouwbare statusbeheer tootruncate de logboek toomake ruimte voor nieuwere Hallo-records.</span><span class="sxs-lookup"><span data-stu-id="064f5-120">Before that happens, hello Reliable State Manager needs tootruncate its log toomake room for hello newer records.</span></span>
<span data-ttu-id="064f5-121">Betrouwbaar status Manager aanvragen Hallo betrouwbare verzamelingen toocheckpoint hun toodisk geheugenstatus.</span><span class="sxs-lookup"><span data-stu-id="064f5-121">Reliable State Manager requests hello Reliable Collections toocheckpoint their in-memory state toodisk.</span></span>
<span data-ttu-id="064f5-122">Op dit moment zou Hallo betrouwbare verzamelingen blijven behouden de status in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="064f5-122">At this point, hello Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="064f5-123">Zodra het Hallo betrouwbare verzamelingen hun controlepunten hebt voltooid, kunt Hallo betrouwbare statusbeheer Hallo logboek toofree schijfruimte vrij afkappen.</span><span class="sxs-lookup"><span data-stu-id="064f5-123">Once hello Reliable Collections complete their checkpoints, hello Reliable State Manager can truncate hello log toofree up disk space.</span></span>
<span data-ttu-id="064f5-124">Wanneer Hallo replica toobe opnieuw opgestart moet, betrouwbare verzamelingen hun controlepunt herstellen en hello betrouwbare statusbeheer herstelt en alle Hallo statuswijzigingen die sinds de laatste controlepunt Hallo afspeelt.</span><span class="sxs-lookup"><span data-stu-id="064f5-124">When hello replica needs toobe restarted, Reliable Collections recover their checkpointed state, and hello Reliable State Manager recovers and plays back all hello state changes that occurred since hello last checkpoint.</span></span>

<span data-ttu-id="064f5-125">Een andere waarde toevoegen van controlepunten is dat het verbetert de hersteltijden in algemene scenario's.</span><span class="sxs-lookup"><span data-stu-id="064f5-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="064f5-126">Het logboek bevat alle bewerkingen die sinds de laatste controlepunt Hallo zich hebben voorgedaan.</span><span class="sxs-lookup"><span data-stu-id="064f5-126">Log contains all operations that have happened since hello last checkpoint.</span></span>
<span data-ttu-id="064f5-127">Deze kan dus meerdere versies van een item, zoals meerdere waarden voor een bepaalde rij in betrouwbare woordenlijst bevatten.</span><span class="sxs-lookup"><span data-stu-id="064f5-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="064f5-128">De controlepunten van een betrouwbare verzameling Hallo daarentegen alleen meest recente versie van elke waarde voor een sleutel.</span><span class="sxs-lookup"><span data-stu-id="064f5-128">In contrast, a Reliable Collection checkpoints only hello latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="064f5-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="064f5-129">Next steps</span></span>
* [<span data-ttu-id="064f5-130">Transacties en vergrendelingen</span><span class="sxs-lookup"><span data-stu-id="064f5-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

