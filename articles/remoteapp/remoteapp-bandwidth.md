---
title: aaaEstimate gebruik van netwerkbandbreedte Azure RemoteApp | Microsoft Docs
description: Meer informatie over Hallo netwerkbandbreedte voor uw Azure RemoteApp-collecties en apps.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 3127f4c7-f532-46c3-ba9b-649f647abec1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 675ee82f26ddb46a3bb3e0ee95ed397e4064e45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="estimate-azure-remoteapp-network-bandwidth-usage"></a>Gebruik van netwerkbandbreedte Azure RemoteApp schatten
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp gebruikt Hallo Remote Desktop Protocol (RDP) toocommunicate tussen toepassingen die worden uitgevoerd in hello Azure-cloud- en uw gebruikers. Dit artikel vindt enkele richtlijnen kunt u tooestimate die netwerkgebruik en evalueren mogelijk gebruik van netwerkbandbreedte per gebruiker voor Azure RemoteApp.

Het schatten van bandbreedtegebruik per gebruiker is erg complex en vereist dat meerdere toepassingen tegelijkertijd uitgevoerd in multitasking scenario's waarin toepassingen mogelijk invloed op de prestaties van elkaars op basis van hun vraag voor netwerkbandbreedte. Zelfs Hallo-type van extern bureaublad-client (bijvoorbeeld Mac-client versus HTML5-client) kan toodifferent bandbreedte resultaten leiden. toohelp doorlopen van deze problemen, we je Hallo gebruiksscenario's in verschillende Hallo algemene categorieën tooreplicate praktijkscenario's opsplitsen. (Indien Hallo: Praktijkscenario natuurlijk een combinatie van de categorieën is en door de gebruiker verschilt.)

Voordat we verder - opmerking die we ervan uitgaan dat RDP biedt een goede tooexcellent ervaring voor de meeste gebruiksscenario's in netwerken met een latentie minder dan 120 ms en bandbreedte meer dan 5 MB - dit is gebaseerd op de RDP-mogelijkheid toodynamically aanpassen met behulp van Hallo beschikbaar netwerk bandbreedte en Hallo geschatte bandbreedte de behoeften van toepassing. In dit artikel gaat afgezien van wat toolook 'de meeste gebruiksscenario's ' aan de rand van hello, waarbij scenario's beginnen toounwind en gebruikerservaring toodegrade begint.

Controleer nu Hallo artikelen voor meer informatie de hello, inclusief factoren tooconsider, basislijnaanbevelingen en wat we hebt niet opgenomen in onze maakt een schatting te volgen.

* [Hoe doet netwerkbandbreedte en de kwaliteit van zich werk samen?](remoteapp-bandwidthexperience.md)
* [Uw gebruik van netwerkbandbreedte met enkele algemene scenario's testen](remoteapp-bandwidthtests.md)
* [Snelle richtlijnen als u geen Hallo tijd of mogelijkheid tootest](remoteapp-bandwidthguidelines.md)

## <a name="what-are-we-not-including"></a>Wat zijn er geen inclusief?
Wanneer u bekijkt hello voorgestelde tests en onze aanbevelingen algehele (en weliswaar algemeen), let er zijn verschillende factoren die we niet kon overwegen. Bijvoorbeeld, Hallo gebruikerservaring problemen geleverd door Hallo asymmetrische aard van uploaden versus downloaden bandbreedte. Hallo prestaties en Hallo gebruikerservaring perceptie ook van invloed op Hallo asymmetrische aard van de meeste Wi-Fi-netwerken. Voor interactieve scenario's Hallo downstream-verkeer kan prioriteit krijgen lager is dan Hallo upstream, die mogelijk Verhoog het aantal verloren video of audio frames Hallo en daarom invloed Hallo gebruiker perceptie van Hallo streaming-ervaring. U kunt uw eigen experimenten toosee wat goed is voor uw specifieke gebruiksvoorbeeld en het netwerk uitvoeren.

Hoewel we omleiding van apparaten bespreken, is er geen rekening gehouden overweging Hallo bandbreedte gevolgen van het Hallo-netwerkverkeer veroorzaakt door de gekoppelde apparaten, zoals opslag, printers, scanners, webcamera's en andere USB-apparaten. Hallo effect van deze apparaten is meestal Hallo bandbreedte behoeften tijdelijk bereikt en verdwijnt wanneer Hallo-taak voltooid is. Maar als u vaak doet, die vraag bandbreedte kan behoorlijk merkbare.

Wij ook niet aan de orde hoe een gebruiker kunnen invloed hebben op andere gebruikers binnen Hallo hetzelfde netwerk. Bijvoorbeeld één gebruiker verbruikt 4K video op 100 MB/s-netwerk mogelijk aanzienlijke gevolgen hebben voor andere gebruikers op hetzelfde netwerk toodo probeert Hallo dezelfde taak. Helaas krijgt geleidelijk moeilijker toodetermine Hallo-impact van gelijktijdig gebruik toogive een gemeenschappelijke of alle waarmee aanbeveling over hoe Hallo system op de statistische functie uitvoert. Alle je dat Hallo onderliggende protocol technologie wordt Hallo optimaal gebruik van de beschikbare netwerkbandbreedte hello, maar dit beschikt over de beperkingen is.

