---
title: RemoteApp - aaaAzure hoe doet netwerkbandbreedte en de kwaliteit van zich werk samen? | Microsoft Docs
description: Meer informatie over hoe netwerkbandbreedte in Azure RemoteApp kan invloed hebben op de kwaliteit van uw gebruikers van ervaring.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 74ebc1fb-5187-4056-b08c-0e03b5ecaca6
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 62b0caadf63359eceb63d27fae6ad289b682ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Azure RemoteApp - hoe doet netwerkbandbreedte en de kwaliteit van zich werk samen?
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Wanneer u bekijkt hello [totale netwerkbandbreedte](remoteapp-bandwidth.md) vereist voor Azure RemoteApp, houd er rekening mee Hallo volgende factoren: dit zijn allemaal deel uit van een dynamisch systeem dat gevolgen Hallo algehele gebruikerservaring. 

* **De beschikbare netwerkbandbreedte en de huidige netwerkomstandigheden** -toepassing hello streaming-ervaring, wat betekent dat een verlaagde algehele gebruikerservaring kan van invloed zijn een aantal parameters (verlies, latentie en jitter) op Hallo netwerk op een bepaald moment. Hallo-bandbreedte die beschikbaar zijn in uw netwerk is een functie van de congestie, willekeurige gegevensverlies, latentie omdat deze alle volgende parameters invloed heeft op Hallo congestie mechanisme voor toegangsbeheer, die in Schakel besturingselementen Hallo transmission snelheid tooavoid conflicten.  Bijvoorbeeld brengt een netwerk met verlies of een netwerk met hoge wachttijd Hallo gebruikerservaring onjuiste zelfs op een netwerk met 1000 MB bandbreedte. Hallo en netwerklatentie variëren, afhankelijk van het aantal gebruikers die op Hallo Hallo hetzelfde netwerk en wat gebruikers doen (bijvoorbeeld video's bekijken, downloaden of uploaden van grote bestanden, afdrukken).
* **Gebruiksscenario** -Hallo ervaring is afhankelijk van welke Hallo gebruikers als personen en als een groep op Hallo hetzelfde doen netwerk. Bijvoorbeeld bij het lezen één dia moet alleen een enkel frame toobe bijgewerkt; Als gebruiker Hallo skims en over de inhoud van een document met tekst hello geschoven, moet een hoger aantal frames toobe per seconde is bijgewerkt. Hallo communicatie terug en weer toohello server in dit scenario uiteindelijk verbruikt meer netwerkbandbreedte. Denk ook na over een extreme voorbeeld: meerdere gebruikers worden hoogwaardige video's (zoals een resolutie van 4 kB) bekijkt, HD telefonische vergaderingen voeren houden, spelen van games met 3D-video of werken op CAD-systemen. Al deze waarden kunt onbruikbaar zelfs een echt hoge bandbreedte netwerk vrijwel.
* **Scherm resolutie en Hallo aantal schermen** -meer netwerkbandbreedte is vereist toofull update groter schermen dan kleinere schermen. de onderliggende technologie Hallo uitstekend vrij van codering en het overdragen van alleen Hallo gebieden van het Hallo-schermen die zijn bijgewerkt, maar en, heel welkomstscherm moet toobe bijgewerkt. Wanneer Hallo gebruiker heeft een hogere Resolutiescherm (bijvoorbeeld 4K-resolutie), is dat de update vereist meer netwerkbandbreedte dan een scherm met lagere resolutie (zoals 1024x768px). Deze dezelfde logica is van toepassing als u meer dan één scherm voor omleiding. Bandbreedte moet tooincrease met Hallo aantal schermen.
* **Klembord- en apparaatgroepen omleiding** : dit is een probleem niet erg duidelijk, maar in veel gevallen als een gebruiker opslaat in een grote hoeveelheid gegevens toohello Klembord, duurt een bits-tijd voor die informatie tootransfer van extern bureaublad-client Hallo toohello server. Hallo downstream-ervaring kan worden beïnvloed door het Hallo-ervaring van het verzenden van inhoud voor het Klembord Hallo stroomopwaarts. Hallo geldt ook voor de apparaatomleiding van - als een scanner of webcam produceert een grote hoeveelheid gegevens die toobe verzonden toohello upstream-server, moet een printer moet tooreceive een groot document of lokale opslag toobe beschikbaar tooan app uitgevoerd in de cloud-toocopy Hallo moet een grote bestanden gebruikers wellicht opgevallen dat frames verloren gaan of tijdelijk video 'bevroren' omdat het Hallo-gegevens die nodig zijn voor de omleiding van Hallo apparaat neemt Hallo netwerkbandbreedte moet. 

Bij het evalueren van de behoeften van uw netwerkbandbreedte, zorg ervoor dat tooconsider al deze factoren die als een systeem.

Nu gaat u terug toohello [hoofdnetwerk bandbreedte artikel](remoteapp-bandwidth.md), op tootesting of verplaats de [netwerkbandbreedte](remoteapp-bandwidthtests.md).

## <a name="learn-more"></a>Meer informatie
* [Gebruik van netwerkbandbreedte Azure RemoteApp schatten](remoteapp-bandwidth.md)
* [Azure RemoteApp: uw gebruik van netwerkbandbreedte met enkele algemene scenario's testen](remoteapp-bandwidthtests.md)
* [Azure RemoteApp netwerkbandbreedte - algemene richtlijnen (als u niet kunt uw eigen testen)](remoteapp-bandwidthguidelines.md)

