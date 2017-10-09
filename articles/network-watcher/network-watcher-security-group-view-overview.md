---
title: aaaIntroduction toosecurity groep weergeven in Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo mogelijkheid tot de weergave van de netwerk-Watcher beveiliging
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="cf10c-103">Inleiding toonetwork beveiliging groep weergeven in Azure-netwerk-Watcher</span><span class="sxs-lookup"><span data-stu-id="cf10c-103">Introduction toonetwork security group view in Azure Network Watcher</span></span>

<span data-ttu-id="cf10c-104">Netwerkbeveiligingsgroepen zijn gekoppeld op het subnetniveau van een of een NIC-niveau.</span><span class="sxs-lookup"><span data-stu-id="cf10c-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="cf10c-105">Wanneer gekoppeld op het subnetniveau van een, geldt deze tooall Hallo VM-exemplaren in Hallo subnet.</span><span class="sxs-lookup"><span data-stu-id="cf10c-105">When associated at a subnet level, it applies tooall hello VM instances in hello subnet.</span></span> <span data-ttu-id="cf10c-106">Netwerkbeveiligingsgroep weergave retourneert alle Hallo geconfigureerd nsg's en regels die zijn gekoppeld op een niveau-NIC en subnet voor een virtuele machine biedt meer informatie over het Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="cf10c-106">Network Security Group view returns all hello configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into hello configuration.</span></span> <span data-ttu-id="cf10c-107">Bovendien worden Hallo effectieve beveiligingsregels voor verbindingen voor elk van de Hallo NIC's in een virtuele machine opgehaald.</span><span class="sxs-lookup"><span data-stu-id="cf10c-107">In addition, hello effective security rules are returned for each of hello NICs in a VM.</span></span> <span data-ttu-id="cf10c-108">Met behulp van de Netwerkbeveiligingsgroep weergeven, kunt u een virtuele machine op netwerk beveiligingsproblemen zoals open poorten beoordelen.</span><span class="sxs-lookup"><span data-stu-id="cf10c-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="cf10c-109">U kunt ook valideren als de Netwerkbeveiligingsgroep werkt zoals verwacht op basis van een [vergelijking tussen Hallo geconfigureerd en effectieve beveiligingsregels Hallo](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cf10c-109">You can also validate if your Network Security Group is working as expected based on a [comparison between hello configured and hello effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="cf10c-110">Er is een meer uitgebreide gebruiksvoorbeeld in security compatibiliteit en controle.</span><span class="sxs-lookup"><span data-stu-id="cf10c-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="cf10c-111">U kunt een uitgebreide set beveiligingsregels als model voor beveiliging toezicht definiëren in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="cf10c-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="cf10c-112">Een audit periodieke naleving kan worden geïmplementeerd op een programmatische manier door te vergelijken Hallo prescriptieve regels met Hallo effectieve regels voor elke Hallo VM's in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="cf10c-112">A periodic compliance audit can be implemented in a programmatic way by comparing hello prescriptive rules with hello effective rules for each of hello VMs in your network.</span></span>

<span data-ttu-id="cf10c-113">Portal regels zijn in Hallo gedeeld door effectieve, Subnet, netwerkinterface en standaard.</span><span class="sxs-lookup"><span data-stu-id="cf10c-113">In hello portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="cf10c-114">Dit biedt een eenvoudige weergave naar Hallo toegepaste regels tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="cf10c-114">This provides a simple view into hello rules applied tooa virtual machine.</span></span> <span data-ttu-id="cf10c-115">Downloadknop wordt verstrekt tooeasily alle Hallo beveiligingsregels ongeacht Hallo tabblad downloaden naar een CSV-bestand.</span><span class="sxs-lookup"><span data-stu-id="cf10c-115">A download button is provided tooeasily download all hello security rules no matter hello tab into a CSV file.</span></span>

![beveiliging groep weergeven][1]

<span data-ttu-id="cf10c-117">Regels kunnen worden geselecteerd en tooshow Hallo voorvoegsels van Netwerkbeveiligingsgroep en bron- en doelserver wordt een nieuwe blade geopend.</span><span class="sxs-lookup"><span data-stu-id="cf10c-117">Rules can be selected and a new blade opens up tooshow hello Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="cf10c-118">Vanaf deze blade kunt u navigeren rechtstreeks toohello Netwerkbeveiligingsgroep resource.</span><span class="sxs-lookup"><span data-stu-id="cf10c-118">From this blade you can navigate directly toohello Network Security Group resource.</span></span>

![DrillDown][2]

### <a name="next-steps"></a><span data-ttu-id="cf10c-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cf10c-120">Next steps</span></span>

<span data-ttu-id="cf10c-121">Meer informatie over hoe tooaudit de netwerkbeveiliging van uw groep instellingen in via [Netwerkbeveiligingsgroep controle-instellingen met PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="cf10c-121">Learn how tooaudit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









