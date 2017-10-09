---
title: "aaaNever store gevoelige gegevens op aangepaste installatiekopieën voor Azure RemoteApp | Microsoft Docs"
description: "Informatie over Hallo richtlijnen voor het opslaan van gegevens in aangepaste installatiekopieën in Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a>Nooit gevoelige gegevens worden opgeslagen op aangepaste installatiekopieën
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Wanneer u uw eigen toepassing in Azure RemoteApp-host, is de eerste stap Hallo toocreate een aangepaste installatiekopie. We gebruiken deze aangepaste installatiekopie toocreate VM-exemplaren die uw apps tooyour gebruikers dienen. Hallo aangepaste installatiekopie moet alleen toepassingen en nooit gevoelige gegevens die verloren gaan, zoals SQL-databases, personeelsbestanden of bestanden zoals QuickBooks bedrijfsbestanden speciale gegevens bevatten. Alle gevoelige gegevens moet zich bevinden op externe tooAzure RemoteApp op een bestandsserver, een andere Azure-virtuele machine of in Azure SQL. Hallo installatiekopie moet NET host Hallo-toepassing die is verbonden gegevensbron toohello en presenteert Hallo-gegevens. Bekijk [vereisten voor Azure RemoteApp-installatiekopieën](remoteapp-imagereqs.md) voor meer informatie. 

Waarom moet u geen gevoelige gegevens opslaan toounderstand moet u de werking van Azure RemoteApp toounderstand. Wanneer een verzameling is gemaakt of bijgewerkt, achter de schermen Hallo worden meerdere klonen of kopieën van Hallo installatiekopie gemaakt. Alle exemplaren van deze virtuele machine zijn exacte kopieën van de aangepaste installatiekopie Hallo; Wanneer gebruikers toepassingen starten zijn ze verbonden tooone van deze VM-exemplaren. Maar hello hetzelfde exemplaar kan niet worden gegarandeerd en moet niet van belang omdat ze niet-persistent. Hallo VM-instanties hosting Hallo toepassingen zijn niet-permanente en kunnen worden vernietigd of verwijderd op basis, bijvoorbeeld tijdens het bijwerken van de verzameling. 

Zodra de Hallo verzameling is ingericht en starten gebruikers de verbindende toohello VM's, gebruikersgegevens is permanent en beveiligd, omdat het wordt opgeslagen op afzonderlijke opslag binnen een VHD die we noemen een [gebruikersprofielschijf (UDP)](remoteapp-upd.md), namelijk Hallo gebruikersprofiel in c:\users\<userprofile >. Wanneer een toepassing wordt gestart, wordt de Hallo UPD gekoppeld en de behandeld net als een lokaal gebruikersprofiel door Hallo-besturingssysteem. Lees meer over hoe [Azure RemoteApp slaat gebruikersgegevens en instellingen](remoteapp-upd.md).

Van de voorbeeldgegevens die niet zich in de installatiekopie van het Hallo bevinden moet:

* Gedeelde gegevensbron voor gebruikers tooaccess
* SQL-database of QuickBooks DB
* Alle gegevens in D:\

Van de voorbeeldgegevens die kunnen worden ondergebracht in Hallo standaard profiel toobe gekopieerd naar alle gebruikers UPD:

* Configuratiebestanden per gebruiker
* Scripts die gebruikers zouden moeten blijven behouden in hun UPD

Belangrijke punten:

* Sla nooit gevoelige gegevens die gaan op Hallo installatiekopie verloren kunnen bij het maken van een aangepaste installatiekopie.
* Gevoelige gegevens moet altijd zich bevinden op een afzonderlijke bestandsserver, afzonderlijke virtuele machine in Azure, op Hallo cloud en altijd externe toohello VM-exemplaren die als host fungeert voor uw toepassingen in Azure RemoteApp. 
* Gegevens worden opgeslagen en de gebruiker zich blijft voordoen in Hallo gebruikersprofielschijf (UDP)

