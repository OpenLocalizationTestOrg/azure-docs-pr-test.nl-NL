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
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a>Inleiding toovariable pakketopname in Azure-netwerk-Watcher

Netwerk-Watcher variabele pakketopname kunt u toocreate pakket vastleggen sessies tootrack verkeer tooand van een virtuele machine. Pakketopname helpt toodiagnose netwerk afwijkingen beide reactief en proactivity. Andere toepassingen zijn onder andere het verzamelen van netwerkstatistieken, krijgt informatie over het netwerk beveiligingsrisico's, toodebug client / server-communicatie en nog veel meer.

Pakketopname is een uitbreiding van virtuele machine die op afstand via het netwerk-Watcher wordt gestart. Deze mogelijkheid kan Hallo last van een pakketopname handmatig worden uitgevoerd op de gewenste Hallo virtuele machine, die kostbare tijd bespaart vergemakkelijken. Pakketopname kan worden geactiveerd via Hallo-portal, PowerShell, CLI of REST-API. Er is een voorbeeld van hoe pakketopname kan worden geactiveerd met waarschuwingen van de virtuele Machine. Filters zijn opgegeven voor Hallo vastleggen sessie tooensure u verkeer u toomonitor wilt vastleggen. Filters zijn gebaseerd op 5-tuple (protocol, lokale IP-adres, extern IP-adres, poort lokale en externe poort) informatie. Hallo vastgelegd gegevens worden opgeslagen in de lokale schijf hello of een blob storage. Er is een limiet van 10 pakket vastleggen sessies per regio per abonnement. Deze beperking geldt alleen toohello sessies en toohello opgeslagen bestanden voor pakket lokaal op Hallo VM of in een opslagaccount is niet van toepassing.

> [!IMPORTANT]
> Pakketopname vereist dat de extensie van een virtuele machine `AzureNetworkWatcherExtension`. Ga voor het Hallo-uitbreiding installeren op een virtuele machine van Windows naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Windows](../virtual-machines/windows/extensions-nwa.md) en voor Linux-VM naar [Azure-netwerk-Watcher Agent de extensie van de virtuele machine voor Linux](../virtual-machines/linux/extensions-nwa.md).

tooreduce hello informatie u tooonly Hallo informatie die u wilt vastleggen, hello volgende opties zijn beschikbaar voor een sessie voor het vastleggen van pakket:

**Configuratie vastleggen**

|Eigenschap|Beschrijving|
|---|---|
|**Maximum aantal bytes per pakket (in bytes)** | Hallo aantal bytes van elk pakket die zijn vastgelegd, alle bytes zijn vastgelegd als leeg is. Hallo aantal bytes van elk pakket die zijn vastgelegd, alle bytes zijn vastgelegd als leeg is. Als u alleen Hallo IPv4-header – moet geven 34 hier |
|**Maximum aantal bytes per sessie (bytes)** | Totaal aantal bytes in die worden vastgelegd als Hallo waarde eindigt Hallo is bereikt.|
|**Tijdslimiet (seconden)** | Stelt een tijdsbeperking voor het Hallo-pakket vastleggen sessie. de standaardwaarde Hallo is 18000 seconden of vijf uur.|

**Filteren (optioneel)**

|Eigenschap|Beschrijving|
|---|---|
|**Protocol** | Hallo protocol toofilter voor Hallo pakket vastleggen. Hallo beschikbare waarden zijn TCP, UDP en alle.|
|**Lokaal IP-adres** | Deze waarde filtert Hallo pakket vastleggen toopackets Hallo lokale IP-adres overeenkomt met de filterwaarde van dit.|
|**Lokale poort** | Deze waarde filters Hallo pakket vastleggen toopackets Hallo lokale poort overeenkomt met de filterwaarde van dit.|
|**Extern IP-adres** | Deze waarde filters Hallo pakket vastleggen toopackets Hallo externe IP overeenkomt met de filterwaarde van dit.|
|**Externe poort** | Deze waarde filters Hallo pakket vastleggen toopackets Hallo externe poort overeenkomt met de filterwaarde van dit.|

### <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe u het pakket mogelijk via de portal Hallo kunt beheren in via [pakketopname in hello Azure-portal beheren](network-watcher-packet-capture-manage-portal.md) of met PowerShell in via [pakket vastleggen beheren met PowerShell](network-watcher-packet-capture-manage-powershell.md).

Meer informatie over hoe toocreate proactieve pakket worden vastgelegd op basis van waarschuwingen van de virtuele machine in via [maken van een waarschuwing geactiveerd pakketopname](network-watcher-alert-triggered-packet-capture.md)

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













