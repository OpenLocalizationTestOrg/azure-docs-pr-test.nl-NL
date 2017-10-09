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
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a>Inleiding toonetwork beveiliging groep weergeven in Azure-netwerk-Watcher

Netwerkbeveiligingsgroepen zijn gekoppeld op het subnetniveau van een of een NIC-niveau. Wanneer gekoppeld op het subnetniveau van een, geldt deze tooall Hallo VM-exemplaren in Hallo subnet. Netwerkbeveiligingsgroep weergave retourneert alle Hallo geconfigureerd nsg's en regels die zijn gekoppeld op een niveau-NIC en subnet voor een virtuele machine biedt meer informatie over het Hallo-configuratie. Bovendien worden Hallo effectieve beveiligingsregels voor verbindingen voor elk van de Hallo NIC's in een virtuele machine opgehaald. Met behulp van de Netwerkbeveiligingsgroep weergeven, kunt u een virtuele machine op netwerk beveiligingsproblemen zoals open poorten beoordelen. U kunt ook valideren als de Netwerkbeveiligingsgroep werkt zoals verwacht op basis van een [vergelijking tussen Hallo geconfigureerd en effectieve beveiligingsregels Hallo](network-watcher-nsg-auditing-powershell.md).

Er is een meer uitgebreide gebruiksvoorbeeld in security compatibiliteit en controle. U kunt een uitgebreide set beveiligingsregels als model voor beveiliging toezicht definiëren in uw organisatie. Een audit periodieke naleving kan worden geïmplementeerd op een programmatische manier door te vergelijken Hallo prescriptieve regels met Hallo effectieve regels voor elke Hallo VM's in uw netwerk.

Portal regels zijn in Hallo gedeeld door effectieve, Subnet, netwerkinterface en standaard. Dit biedt een eenvoudige weergave naar Hallo toegepaste regels tooa virtuele machine. Downloadknop wordt verstrekt tooeasily alle Hallo beveiligingsregels ongeacht Hallo tabblad downloaden naar een CSV-bestand.

![beveiliging groep weergeven][1]

Regels kunnen worden geselecteerd en tooshow Hallo voorvoegsels van Netwerkbeveiligingsgroep en bron- en doelserver wordt een nieuwe blade geopend. Vanaf deze blade kunt u navigeren rechtstreeks toohello Netwerkbeveiligingsgroep resource.

![DrillDown][2]

### <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooaudit de netwerkbeveiliging van uw groep instellingen in via [Netwerkbeveiligingsgroep controle-instellingen met PowerShell](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









