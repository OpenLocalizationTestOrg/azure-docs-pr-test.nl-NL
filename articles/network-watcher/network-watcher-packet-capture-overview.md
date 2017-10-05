---
title: Inleiding tot pakketopname in Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van de mogelijkheid van netwerk-Watcher pakket vastleggen
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
ms.openlocfilehash: 4fdd007c2cfad7b42f26ab2cacfba06d95c8dad3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-variable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="2318c-103">Inleiding tot variabele pakketopname in Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="2318c-103">Introduction to variable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="2318c-104">Netwerk-Watcher variabele pakketopname kunt u om pakket vastleggen sessies om bij te houden van verkeer van en naar een virtuele machine te maken.</span><span class="sxs-lookup"><span data-stu-id="2318c-104">Network Watcher variable packet capture allows you to create packet capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="2318c-105">Helpt bij het vastleggen van pakket op te sporen netwerk afwijkingen beide reactief en proactivity.</span><span class="sxs-lookup"><span data-stu-id="2318c-105">Packet capture helps to diagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="2318c-106">Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's voor foutopsporing van client-servercommunicaties en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="2318c-106">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span>

<span data-ttu-id="2318c-107">Pakketopname is een uitbreiding van virtuele machine die op afstand via het netwerk-Watcher wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2318c-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="2318c-108">Deze mogelijkheid kan de werkbelasting van een pakketopname handmatig worden uitgevoerd op de gewenste virtuele machine, die kostbare tijd bespaart vergemakkelijken.</span><span class="sxs-lookup"><span data-stu-id="2318c-108">This capability eases the burden of running a packet capture manually on the desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="2318c-109">Pakketopname kan worden geactiveerd via de portal, PowerShell, CLI of REST-API.</span><span class="sxs-lookup"><span data-stu-id="2318c-109">Packet capture can be triggered through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="2318c-110">Er is een voorbeeld van hoe pakketopname kan worden geactiveerd met waarschuwingen van de virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="2318c-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="2318c-111">Filters zijn beschikbaar voor de opnamesessie om ervoor te zorgen vastleggen van verkeer dat u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="2318c-111">Filters are provided for the capture session to ensure you capture traffic you want to monitor.</span></span> <span data-ttu-id="2318c-112">Filters zijn gebaseerd op 5-tuple (protocol, lokale IP-adres, extern IP-adres, poort lokale en externe poort) informatie.</span><span class="sxs-lookup"><span data-stu-id="2318c-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="2318c-113">De vastgelegde gegevens wordt opgeslagen in de lokale schijf of een blob storage.</span><span class="sxs-lookup"><span data-stu-id="2318c-113">The captured data is stored in the local disk or a storage blob.</span></span> <span data-ttu-id="2318c-114">Er is een limiet van 10 pakket vastleggen sessies per regio per abonnement.</span><span class="sxs-lookup"><span data-stu-id="2318c-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="2318c-115">Deze beperking geldt alleen voor de sessies en niet van toepassing op de bestanden van de capture opgeslagen pakket lokaal op de virtuele machine of in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2318c-115">This limit applies only to the sessions and does not apply to the saved packet capture files either locally on the VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2318c-116">Pakketopname vereist dat de extensie van een virtuele machine `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="2318c-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="2318c-117">Voor het installeren van de extensie op een Windows-virtuele machine gaat u naar [extensie voor het virtuele machine voor Windows Azure-netwerk-Watcher Agent](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="2318c-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="2318c-118">Als u de informatie die u alleen de informatie die u wilt vastleggen, zijn de volgende opties beschikbaar voor een sessie voor het vastleggen van pakket:</span><span class="sxs-lookup"><span data-stu-id="2318c-118">To reduce the information you capture to only the information you want, the following options are available for a packet capture session:</span></span>

<span data-ttu-id="2318c-119">**Configuratie vastleggen**</span><span class="sxs-lookup"><span data-stu-id="2318c-119">**Capture configuration**</span></span>

|<span data-ttu-id="2318c-120">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="2318c-120">Property</span></span>|<span data-ttu-id="2318c-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2318c-121">Description</span></span>|
|---|---|
|<span data-ttu-id="2318c-122">**Maximum aantal bytes per pakket (in bytes)**</span><span class="sxs-lookup"><span data-stu-id="2318c-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="2318c-123">Het aantal bytes van elk pakket die zijn vastgelegd, alle bytes zijn vastgelegd als leeg is.</span><span class="sxs-lookup"><span data-stu-id="2318c-123">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="2318c-124">Het aantal bytes van elk pakket die zijn vastgelegd, alle bytes zijn vastgelegd als leeg is.</span><span class="sxs-lookup"><span data-stu-id="2318c-124">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="2318c-125">Als u alleen de IPv4-header – moet geven 34 hier</span><span class="sxs-lookup"><span data-stu-id="2318c-125">If you need only the IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="2318c-126">**Maximum aantal bytes per sessie (bytes)**</span><span class="sxs-lookup"><span data-stu-id="2318c-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="2318c-127">Totaal aantal bytes in die zijn vastgelegd, zodra de sessie wordt beëindigd door de waarde is bereikt.</span><span class="sxs-lookup"><span data-stu-id="2318c-127">Total number of bytes in that are captured, once the value is reached the session ends.</span></span>|
|<span data-ttu-id="2318c-128">**Tijdslimiet (seconden)**</span><span class="sxs-lookup"><span data-stu-id="2318c-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="2318c-129">Stelt een tijdsbeperking van de voor het pakket vastleggen sessie.</span><span class="sxs-lookup"><span data-stu-id="2318c-129">Sets a time constraint on the packet capture session.</span></span> <span data-ttu-id="2318c-130">De standaardwaarde is 18000 seconden of vijf uur.</span><span class="sxs-lookup"><span data-stu-id="2318c-130">The default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="2318c-131">**Filteren (optioneel)**</span><span class="sxs-lookup"><span data-stu-id="2318c-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="2318c-132">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="2318c-132">Property</span></span>|<span data-ttu-id="2318c-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2318c-133">Description</span></span>|
|---|---|
|<span data-ttu-id="2318c-134">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="2318c-134">**Protocol**</span></span> | <span data-ttu-id="2318c-135">Het protocol voor het filteren van voor het vastleggen van het pakket.</span><span class="sxs-lookup"><span data-stu-id="2318c-135">The protocol to filter for the packet capture.</span></span> <span data-ttu-id="2318c-136">De beschikbare waarden zijn TCP, UDP en alle.</span><span class="sxs-lookup"><span data-stu-id="2318c-136">The available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="2318c-137">**Lokaal IP-adres**</span><span class="sxs-lookup"><span data-stu-id="2318c-137">**Local IP address**</span></span> | <span data-ttu-id="2318c-138">Deze waarde filtert de pakketopname voor de pakketten waar het lokale IP-adres overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="2318c-138">This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>|
|<span data-ttu-id="2318c-139">**Lokale poort**</span><span class="sxs-lookup"><span data-stu-id="2318c-139">**Local port**</span></span> | <span data-ttu-id="2318c-140">Deze waarde filtert de pakketopname om pakketten van de lokale poort overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="2318c-140">This value filters the packet capture to packets where the local port matches this filter value.</span></span>|
|<span data-ttu-id="2318c-141">**Extern IP-adres**</span><span class="sxs-lookup"><span data-stu-id="2318c-141">**Remote IP address**</span></span> | <span data-ttu-id="2318c-142">Deze waarde filtert de pakketopname voor de pakketten waar het externe IP-adres overeenkomt met de filterwaarde van dit.</span><span class="sxs-lookup"><span data-stu-id="2318c-142">This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>|
|<span data-ttu-id="2318c-143">**Externe poort**</span><span class="sxs-lookup"><span data-stu-id="2318c-143">**Remote port**</span></span> | <span data-ttu-id="2318c-144">Deze waarde filtert de pakketopname pakketten waarbij de externe poort overeenkomt met de waarde voor dit filter.</span><span class="sxs-lookup"><span data-stu-id="2318c-144">This value filters the packet capture to packets where the remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="2318c-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2318c-145">Next steps</span></span>

<span data-ttu-id="2318c-146">Meer informatie over hoe u het pakket mogelijk via de portal kunt beheren in via [pakketopname in de Azure portal beheren](network-watcher-packet-capture-manage-portal.md) of met PowerShell in via [pakket vastleggen beheren met PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2318c-146">Learn how you can manage packet captures through the portal by visiting [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="2318c-147">Informatie over het maken van proactieve pakket opnamen op basis van waarschuwingen van de virtuele machine in via [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="2318c-147">Learn how to create proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













