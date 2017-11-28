---
title: aaaIntroduction tooPacket vastleggen in Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo netwerk-Watcher pakket vastleggen mogelijkheid
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="d98f6-103">Inleiding toovariable pakketopname in Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="d98f6-103">Introduction toovariable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="d98f6-104">Netwerk-Watcher variabele pakketopname kunt u toocreate pakket vastleggen sessies tootrack verkeer tooand van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d98f6-104">Network Watcher variable packet capture allows you toocreate packet capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="d98f6-105">Pakketopname helpt toodiagnose netwerk afwijkingen beide reactief en proactivity.</span><span class="sxs-lookup"><span data-stu-id="d98f6-105">Packet capture helps toodiagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="d98f6-106">Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="d98f6-106">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span>

<span data-ttu-id="d98f6-107">Pakketopname is een uitbreiding van virtuele machine die op afstand via het netwerk-Watcher wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="d98f6-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="d98f6-108">Deze mogelijkheid kan Hallo last van een pakketopname handmatig worden uitgevoerd op de gewenste Hallo virtuele machine, die kostbare tijd bespaart vergemakkelijken.</span><span class="sxs-lookup"><span data-stu-id="d98f6-108">This capability eases hello burden of running a packet capture manually on hello desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="d98f6-109">Pakketopname kan worden geactiveerd via Hallo-portal, PowerShell, CLI of REST-API.</span><span class="sxs-lookup"><span data-stu-id="d98f6-109">Packet capture can be triggered through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="d98f6-110">Er is een voorbeeld van hoe pakketopname kan worden geactiveerd met waarschuwingen van de virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="d98f6-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="d98f6-111">Filters zijn opgegeven voor Hallo vastleggen sessie tooensure u verkeer u toomonitor wilt vastleggen.</span><span class="sxs-lookup"><span data-stu-id="d98f6-111">Filters are provided for hello capture session tooensure you capture traffic you want toomonitor.</span></span> <span data-ttu-id="d98f6-112">Filters zijn gebaseerd op 5-tuple (protocol, lokale IP-adres, extern IP-adres, poort lokale en externe poort) informatie.</span><span class="sxs-lookup"><span data-stu-id="d98f6-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="d98f6-113">Hallo vastgelegd gegevens worden opgeslagen in de lokale schijf hello of een blob storage.</span><span class="sxs-lookup"><span data-stu-id="d98f6-113">hello captured data is stored in hello local disk or a storage blob.</span></span> <span data-ttu-id="d98f6-114">Er is een limiet van 10 pakket vastleggen sessies per regio per abonnement.</span><span class="sxs-lookup"><span data-stu-id="d98f6-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="d98f6-115">Deze beperking geldt alleen toohello sessies en toohello opgeslagen bestanden voor pakket lokaal op Hallo VM of in een opslagaccount is niet van toepassing.</span><span class="sxs-lookup"><span data-stu-id="d98f6-115">This limit applies only toohello sessions and does not apply toohello saved packet capture files either locally on hello VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d98f6-116">Pakketopname vereist dat de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="d98f6-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="d98f6-117">Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="d98f6-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="d98f6-118">tooreduce hello informatie u tooonly Hallo informatie die u wilt vastleggen, hello volgende opties zijn beschikbaar voor een sessie voor het vastleggen van pakket:</span><span class="sxs-lookup"><span data-stu-id="d98f6-118">tooreduce hello information you capture tooonly hello information you want, hello following options are available for a packet capture session:</span></span>

<span data-ttu-id="d98f6-119">**Configuratie vastleggen**</span><span class="sxs-lookup"><span data-stu-id="d98f6-119">**Capture configuration**</span></span>

|<span data-ttu-id="d98f6-120">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d98f6-120">Property</span></span>|<span data-ttu-id="d98f6-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d98f6-121">Description</span></span>|
|---|---|
|<span data-ttu-id="d98f6-122">**Maximum aantal bytes per pakket (in bytes)**</span><span class="sxs-lookup"><span data-stu-id="d98f6-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="d98f6-123">Hallo aantal bytes van elk pakket die zijn vastgelegd, alle bytes zijn vastgelegd als leeg is.</span><span class="sxs-lookup"><span data-stu-id="d98f6-123">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="d98f6-124">Hallo aantal bytes van elk pakket die zijn vastgelegd, alle bytes zijn vastgelegd als leeg is.</span><span class="sxs-lookup"><span data-stu-id="d98f6-124">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="d98f6-125">Als u alleen Hallo IPv4-header – moet geven 34 hier</span><span class="sxs-lookup"><span data-stu-id="d98f6-125">If you need only hello IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="d98f6-126">**Maximum aantal bytes per sessie (bytes)**</span><span class="sxs-lookup"><span data-stu-id="d98f6-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="d98f6-127">Totaal aantal bytes in die worden vastgelegd als Hallo waarde eindigt Hallo is bereikt.</span><span class="sxs-lookup"><span data-stu-id="d98f6-127">Total number of bytes in that are captured, once hello value is reached hello session ends.</span></span>|
|<span data-ttu-id="d98f6-128">**Tijdslimiet (seconden)**</span><span class="sxs-lookup"><span data-stu-id="d98f6-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="d98f6-129">Stelt een tijdsbeperking voor het Hallo-pakket vastleggen sessie.</span><span class="sxs-lookup"><span data-stu-id="d98f6-129">Sets a time constraint on hello packet capture session.</span></span> <span data-ttu-id="d98f6-130">de standaardwaarde Hallo is 18000 seconden of vijf uur.</span><span class="sxs-lookup"><span data-stu-id="d98f6-130">hello default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="d98f6-131">**Filteren (optioneel)**</span><span class="sxs-lookup"><span data-stu-id="d98f6-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="d98f6-132">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d98f6-132">Property</span></span>|<span data-ttu-id="d98f6-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d98f6-133">Description</span></span>|
|---|---|
|<span data-ttu-id="d98f6-134">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="d98f6-134">**Protocol**</span></span> | <span data-ttu-id="d98f6-135">Hallo protocol toofilter voor Hallo pakket vastleggen.</span><span class="sxs-lookup"><span data-stu-id="d98f6-135">hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="d98f6-136">Hallo beschikbare waarden zijn TCP, UDP en alle.</span><span class="sxs-lookup"><span data-stu-id="d98f6-136">hello available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="d98f6-137">**Lokaal IP-adres**</span><span class="sxs-lookup"><span data-stu-id="d98f6-137">**Local IP address**</span></span> | <span data-ttu-id="d98f6-138">Deze waarde filtert Hallo pakket vastleggen toopackets Hallo lokale IP-adres overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="d98f6-138">This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>|
|<span data-ttu-id="d98f6-139">**Lokale poort**</span><span class="sxs-lookup"><span data-stu-id="d98f6-139">**Local port**</span></span> | <span data-ttu-id="d98f6-140">Deze waarde filters Hallo pakket vastleggen toopackets Hallo lokale poort overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="d98f6-140">This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>|
|<span data-ttu-id="d98f6-141">**Extern IP-adres**</span><span class="sxs-lookup"><span data-stu-id="d98f6-141">**Remote IP address**</span></span> | <span data-ttu-id="d98f6-142">Deze waarde filters Hallo pakket vastleggen toopackets Hallo externe IP overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="d98f6-142">This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>|
|<span data-ttu-id="d98f6-143">**Externe poort**</span><span class="sxs-lookup"><span data-stu-id="d98f6-143">**Remote port**</span></span> | <span data-ttu-id="d98f6-144">Deze waarde filters Hallo pakket vastleggen toopackets Hallo externe poort overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="d98f6-144">This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="d98f6-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d98f6-145">Next steps</span></span>

<span data-ttu-id="d98f6-146">Meer informatie over hoe u het pakket mogelijk via de portal Hallo kunt beheren in via [pakketopname in hello Azure-portal beheren](network-watcher-packet-capture-manage-portal.md) of met PowerShell in via [pakket vastleggen beheren met PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d98f6-146">Learn how you can manage packet captures through hello portal by visiting [Manage packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="d98f6-147">Meer informatie over hoe toocreate proactieve pakket worden vastgelegd op basis van waarschuwingen van de virtuele machine in via [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="d98f6-147">Learn how toocreate proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













