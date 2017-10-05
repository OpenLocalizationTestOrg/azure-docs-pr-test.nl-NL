---
title: 'Azure RemoteApp: uw gebruik van netwerkbandbreedte met enkele algemene scenario''s testen | Microsoft Docs'
description: Meer informatie over hoe veelvoorkomende gebruiksscenario's waarmee u kunnen nagaan wat de behoeften van uw netwerkbandbreedte voor de Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 06417c75-0c63-4ecf-b9d1-66a7af6b7b91
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 8ad172a06e34cd0647079d787097cb2696cf116e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp---testing-your-network-bandwidth-usage-with-some-common-scenarios"></a>Azure RemoteApp: uw gebruik van netwerkbandbreedte met enkele algemene scenario's testen
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Zoals besproken [schatting Azure RemoteApp-netwerkbandbreedtegebruik](remoteapp-bandwidth.md), de beste manier om te achterhalen wat de invloed van Azure RemoteApp op uw netwerk is sommige gebruik tests uitvoeren. Deze tests voor een gegeven periode uitvoeren en de bandbreedte die nodig zijn voor elk scenario meten. Als u de mogelijkheid hebt, kunt u ook de netwerk-pakket verloren gaan en het netwerk jitter voor informatie over de netwerk-patronen die worden gemaakt in uw specifieke omgeving te meten.

Bij het evalueren van het bandbreedtegebruik, houd er rekening mee dat gebruik voor verschillende gebruikers binnen uw bedrijf varieert. Bijvoorbeeld verbruikt tekst en schrijfprogramma meestal minder bandbreedte dan gebruikers die met video werken. Voor de beste resultaten bestuderen van uw eigen behoeften van gebruikers en maak een combinatie van de volgende scenario's die het best de gebruikers in uw bedrijf vertegenwoordigt. Vergeet niet te [revisie optreden van de factoren die van invloed bandbreedtegebruik en gebruiker](remoteapp-bandwidthexperience.md) -zodat u de ideale tests identificeren.

Eerst lezen over de tests, kies uw mix en voer deze uit. U kunt de onderstaande tabel op te sporen prestaties.

> [!NOTE]
> Als u niet uw eigen netwerk testen of u hebt niet de tijd om dit te doen, Bekijk onze [Basisnetwerk bandbreedte maakt een schatting/aanbevelingen](remoteapp-bandwidthguidelines.md). Uw kilometers kan echter variëren, dus als u *kunt* uw eigen tests uitvoert, moet u.
> 
> 

## <a name="the-usage-tests"></a>De tests gebruik
Elk van deze tests uitgevoerd voor verschillende hoeveelheden tijd en testen van verschillende functies en-functies die de netwerkbandbreedte gebruiken. Vergeet niet de combinatie van test kiezen die het beste overeenkomt met de gebruikers van uw bedrijf.

### <a name="executivecomplex-powerpoint---run-for-900-1000-seconds"></a>Executive/complexe PowerPoint - 900-1000 seconden uitgevoerd
Een gebruiker geeft tussen 45 50 hoogwaardige dia's met behulp van Microsoft Office PowerPoint in modus volledig scherm. De dia moeten bevatten, afbeeldingen, overgangen (met animaties) en achtergrond kleurverloop die typisch zijn voor uw bedrijf zijn. De gebruiker moet ten minste 20 seconden besteden aan elke dia.

Dit scenario maakt bursty verkeer, wanneer een dia naar de volgende dia in de presentatie overgezet.

### <a name="simple-powerpoint---run-for-620-seconds"></a>Eenvoudige PowerPoint - ~ 620 seconden uitgevoerd
Een gebruiker geeft een eenvoudige PowerPoint-bestand met ongeveer 30 dia's met behulp van Microsoft Office PowerPoint in modus volledig scherm. De dia tekst intensiever dan in het scenario Executive/complexe PowerPoint en eenvoudigere achtergrond en installatiekopieën (zwarte diagrammen). 

### <a name="internet-explorer---run-for-250-seconds"></a>Internet Explorer - 250 seconden uitgevoerd
Een gebruiker op het web gezocht met behulp van Internet Explorer. De gebruiker op gezocht en een combinatie van tekst, natuurlijke afbeeldingen en sommige schema's wordt geschoven. De webpagina's opgeslagen op de lokale vaste schijf van de extern bureaublad-sessiehost (RD Session Host)-server als een. MHT-bestand. De gebruiker schuift Page Up, Page Down omhoog en omlaag sleutels, gebruik met verschillende intervallen voor elke sleuteltype van schuifbalk:

    - Niet - actief 250 toetsaanslagen zeer 500 ms
    - Page Up - 36 toetsaanslagen elke 1000 ms
    - Pijl-omlaag - 75 toetsaanslagen elke 100 ms
    - Page Down - 20 toetsaanslagen elke 500 ms
    - Maximaal - toetsaanslagen 120 door elke 300 ms

### <a name="pdf-document---simple---run-for-610-seconds"></a>PDF-document - eenvoudig - ~ 610 seconden uitgevoerd
Een gebruiker leest en zoekt u een PDF-document op verschillende manieren met behulp van Adobe Acrobat Reader. Het document moet bestaan uit tabellen, eenvoudige grafieken en meerdere lettertypen. Het document is 35 40 pagina's lang. De gebruiker wordt geschoven met twee verschillende snelheden, achterwaartse en stuurt op vier verschillende zoomen grootten (aanpassen aan pagina, aanpassen aan de breedte van 100%, en een andere van uw keuze). De zoomen zorgt ervoor dat de tekst (lettertype) in verschillende grootten rendert. Schuiven is niet beschikbaar met behulp van de Page Up, Page Down omhoog en omlaag sleutels, met verschillende intervallen voor elke schuiven.

### <a name="pdf-document---mixed---run-for-320-seconds"></a>PDF-document - gemengde - Run voor ~ 320 seconden
Een gebruiker leest en zoekt u een PDF-document op verschillende manieren met behulp van Adobe Acrobat Reader. Het document bestaat uit de afbeeldingen van hoge kwaliteit (inclusief foto's), tabellen, eenvoudige grafieken en meerdere lettertypen. De gebruiker wordt geschoven met twee verschillende snelheden, achterwaartse en stuurt op vier verschillende zoomen grootten (aanpassen aan pagina, aanpassen aan de breedte van 100%, en een andere van uw keuze). De zoomen zorgt ervoor dat de tekst (lettertype) in verschillende grootten rendert. Schuiven is niet beschikbaar met behulp van de Page Up, Page Down omhoog en omlaag sleutels, met verschillende intervallen voor elke schuiven.

### <a name="flash-video-playback---run-for-180-seconds"></a>Flash afspelen van video - ~ 180 seconden uitgevoerd
Een gebruiker weergeeft een video Adobe Flash-codering is ingesloten in een webpagina. De webpagina wordt opgeslagen in de lokale vaste schijf van de RD Session Host-server. De video wordt door een invoegtoepassing ingesloten speler gespeeld in Internet Explorer.

Dit scenario emuleert gebruikers uitgebreide inhoud webpagina's met multimedia bekijken. De meeste van de gegevens moet invoervak via VOBR.

### <a name="word-remote-typing---run-for-1800-seconds"></a>Externe te typen in Word - ~ 1800 seconden uitgevoerd
Een gebruiker typt een document via een RDP-sessie. Toetsaanslagen worden verzonden vanaf de client via de RDP-sessie aan een Microsoft Word-document in de externe sessie uitgevoerd. De frequentie van de typen is één teken elke 250 ms (totaal 7050 tekens). 

Dit is een van de meest voorkomende scenario's voor een werknemer kennis. Dit scenario wordt de reactiesnelheid van een gebruiker te typen in een processor moderne werk getest. Dit scenario is gevoelig voor zelfs kleine wijzigingen in bandbreedtegebruik.

## <a name="tracking-the-test-results"></a>Het bijhouden van de testresultaten
De volgende tabel kunt u de scenario's in uw omgeving te evalueren. De onderstaande gegevens is alleen bedoeld ter illustratie - mogelijk aanzienlijk verschilt van wat u precies zien. 

Voor het gemak, nemen we aan dat alle scenario's worden getest met de dezelfde schermresolutie van 1920 x 1080 pixels en TCP-transport op een netwerk met een latentie (vertraging) minder dan 200 ms en netwerk jitter in de markering 120 ms + van ongeveer 1%.

Over de tabel:

* **Gemiddelde ervaring** bevat van de netwerkbandbreedte waarbij de productiviteit van de gebruiker heeft geen aanzienlijke gevolgen maar incidentele video of audio haperingen niet uitsluit. Het systeem is snel herstellen door gebruik te maken van de dynamische logica. Maakt een schatting poging van de netwerk-bandbreedte te waarborgen van de kwaliteit van de gebruikerservaring.
  * **Merkbare problemen (einde-beheerpunt)** de netwerkbandbreedte waar gebruikers wellicht opgevallen dat belangrijke problemen in hun ervaring en is van invloed op de productiviteit voor meetbare perioden bevat. Op dit moment de RDP-algoritmen hebben moeite en kwaliteit van de ervaring van de gebruiker kunnen niet worden gegarandeerd vanwege onvoldoende netwerkbandbreedte.
  * **Aanbevolen** bevat van de netwerkbandbreedte voor goed of uitstekend aanbevolen. Dit is gewoonlijk één stap hoger dan de waarde in het bijbehorende **gemiddelde ervaring** kolom.
  * **Opmerkingen bij de** opmerkingen bevatten.

| Test | Gemiddelde ervaring | Merkbare problemen (einde-beheerpunt) | Aanbevolen netwerkbandbreedte | Opmerkingen |
| --- | --- | --- | --- | --- |
| Executive/complexe PPT |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s voorkeur |Op 1 MB/s gaan veel animaties verloren |
| Eenvoudige PPT |5 MB/s |256 KB/s |10 MB/s |Om 256 KB/s laden de dia met vertraging merkbaar |
| Internet Explorer |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s voorkeur |Web-video's zijn fuzzy op 1 MB/s en onregelmatig, snelle schuiven heeft problemen |
| Eenvoudige PDF |1 MB/s |256 KB/s |5 MB/s |Om 256 KB/s duurt het even om de pagina te laden |
| Gemengde PDF |1 MB/s |256 KB/s |5 MB/s |Op 256 KB/s neemt de pagina een aanzienlijke hoeveelheid tijd voor het laden |
| Flash afspelen van video 's |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s voorkeur |1 MB/s de video is korrelig en sommige frames zijn verwijderd |
| Word externe typen |256 KB/s |128 KB/s |1 MB/s |Gebruiker merkt op 256 KB/s de tijd tussen toetsaanslagen |

Om de netwerkbandbreedte per gebruiker, een combinatie van de bovenstaande scenario's en het overeenkomstige deel van de vereiste netwerkbandbreedte te maken. Kies op het hoogste aantal die nodig zijn voor uw scenario's. Omdat het systeem alleen bijna nooit door gebruikers worden gebruikt, kunt u sommige reserveren voor gebruikers die tegelijk op hetzelfde netwerk werken.

## <a name="learn-more"></a>Meer informatie
* [Gebruik van netwerkbandbreedte Azure RemoteApp schatten](remoteapp-bandwidth.md)
* [Azure RemoteApp - hoe doet netwerkbandbreedte en de kwaliteit van zich werk samen?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp netwerkbandbreedte - algemene richtlijnen (als u niet kunt uw eigen testen)](remoteapp-bandwidthguidelines.md)

