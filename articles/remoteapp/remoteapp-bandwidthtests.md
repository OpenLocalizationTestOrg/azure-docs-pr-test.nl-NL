---
title: 'aaaAzure RemoteApp: uw gebruik van netwerkbandbreedte met enkele algemene scenario''s testen | Microsoft Docs'
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
ms.openlocfilehash: 22c1dbb61d956d58d01eb4e11363266168e337e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---testing-your-network-bandwidth-usage-with-some-common-scenarios"></a>Azure RemoteApp: uw gebruik van netwerkbandbreedte met enkele algemene scenario's testen
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Zoals besproken [schatting Azure RemoteApp-netwerkbandbreedtegebruik](remoteapp-bandwidth.md), Hallo aanbevolen manier toofigure wat Hallo zijn de gevolgen van het netwerk van Azure RemoteApp tooyour is toorun sommige tests gebruik. Voer deze tests uit voor een set tijd en een metingexpressie Hallo bandbreedte nodig is voor elk scenario. Als u de mogelijkheid Hallo hebt, kunt u ook Hallo netwerk pakket verlies en netwerk jitter toounderstand Hallo netwerk patronen die worden gemaakt in uw specifieke omgeving te meten.

Bij het evalueren van het bandbreedtegebruik hello, houd er rekening mee dat gebruik voor verschillende gebruikers binnen uw bedrijf varieert. Bijvoorbeeld verbruikt tekst en schrijfprogramma meestal minder bandbreedte dan gebruikers die met video werken. Voor de beste resultaten bestuderen van uw eigen behoeften van gebruikers en maak een combinatie van Hallo volgen scenario's die het best Hallo gebruikers in uw bedrijf vertegenwoordigt. Houd er rekening mee te[revisie Hallo factoren die van invloed bandbreedtegebruik en de gebruiker zich](remoteapp-bandwidthexperience.md) -zodat u Hallo ideaal tests identificeren.

Eerst lezen over Hallo tests, kies uw mix en voert u deze. U kunt onderstaande toohelp bijhouden prestaties Hallo tabel gebruiken.

> [!NOTE]
> Als het niet mogelijk uw eigen netwerk testen of u hebt geen Hallo tijd toodo dus, Bekijk onze [Basisnetwerk bandbreedte maakt een schatting/aanbevelingen](remoteapp-bandwidthguidelines.md). Uw kilometers kan echter variëren, dus als u *kunt* uw eigen tests uitvoert, moet u.
> 
> 

## <a name="hello-usage-tests"></a>Hallo gebruik tests
Elk van deze tests uitgevoerd voor verschillende hoeveelheden tijd en testen van verschillende functies en-functies die de netwerkbandbreedte gebruiken. Houd er rekening mee toochoose Hallo combinatie van de test die het meest geschikt is voor de gebruikers van uw bedrijf.

### <a name="executivecomplex-powerpoint---run-for-900-1000-seconds"></a>Executive/complexe PowerPoint - 900-1000 seconden uitgevoerd
Een gebruiker geeft tussen 45 50 hoogwaardige dia's met behulp van Microsoft Office PowerPoint in modus volledig scherm. Hallo dia moeten bevatten, afbeeldingen, overgangen (met animaties) en achtergrond kleurverloop die typisch zijn voor uw bedrijf zijn. Hallo-gebruiker moet ten minste 20 seconden besteden aan elke dia.

Dit scenario maakt bursty verkeer, wanneer een dia toohello volgende dia in Hallo presentatie overgangen.

### <a name="simple-powerpoint---run-for-620-seconds"></a>Eenvoudige PowerPoint - ~ 620 seconden uitgevoerd
Een gebruiker geeft een eenvoudige PowerPoint-bestand met ongeveer 30 dia's met behulp van Microsoft Office PowerPoint in modus volledig scherm. Hallo dia tekst intensiever dan in Hallo PowerPoint Executive/complexe scenario zijn en eenvoudiger achtergrond en installatiekopieën (zwarte diagrammen). 

### <a name="internet-explorer---run-for-250-seconds"></a>Internet Explorer - 250 seconden uitgevoerd
Een gebruiker op Hallo web gezocht met behulp van Internet Explorer. Hallo gebruiker bladert en een combinatie van tekst, natuurlijke afbeeldingen en sommige schema's wordt geschoven. Hallo webpagina's die zijn opgeslagen op lokale schijf Hallo van Hallo extern bureaublad-sessiehost (RD Session Host)-server als een. MHT-bestand. Hallo wordt geschoven Page Up, Page Down omhoog en omlaag sleutels, gebruik met verschillende intervallen voor elke sleuteltype van schuifbalk:

    - Niet - actief 250 toetsaanslagen zeer 500 ms
    - Page Up - 36 toetsaanslagen elke 1000 ms
    - Pijl-omlaag - 75 toetsaanslagen elke 100 ms
    - Page Down - 20 toetsaanslagen elke 500 ms
    - Maximaal - toetsaanslagen 120 door elke 300 ms

### <a name="pdf-document---simple---run-for-610-seconds"></a>PDF-document - eenvoudig - ~ 610 seconden uitgevoerd
Een gebruiker leest en zoekt u een PDF-document op verschillende manieren met behulp van Adobe Acrobat Reader. Hallo-document moet bestaan uit tabellen, eenvoudige grafieken en meerdere lettertypen. Hallo document is 35 40 pagina's lang. Hallo gebruiker achterwaartse geschoven met twee verschillende snelheden, en stuurt op vier verschillende zoomen grootten (toopage, passend toowidth past 100%, en een andere van uw keuze). Hallo zoomen zorgt ervoor dat de tekst hello (lettertype) renders in verschillende grootten. Schuiven is niet beschikbaar met behulp van Hallo Page Up, Page Down omhoog en omlaag sleutels, met verschillende intervallen voor elke schuiven.

### <a name="pdf-document---mixed---run-for-320-seconds"></a>PDF-document - gemengde - Run voor ~ 320 seconden
Een gebruiker leest en zoekt u een PDF-document op verschillende manieren met behulp van Adobe Acrobat Reader. Hallo document bestaat uit de afbeeldingen van hoge kwaliteit (inclusief foto's), tabellen, eenvoudige grafieken en meerdere lettertypen. Hallo gebruiker achterwaartse geschoven met twee verschillende snelheden, en stuurt op vier verschillende zoomen grootten (toopage, passend toowidth past 100%, en een andere van uw keuze). Hallo zoomen zorgt ervoor dat de tekst hello (lettertype) renders in verschillende grootten. Schuiven is niet beschikbaar met behulp van Hallo Page Up, Page Down omhoog en omlaag sleutels, met verschillende intervallen voor elke schuiven.

### <a name="flash-video-playback---run-for-180-seconds"></a>Flash afspelen van video - ~ 180 seconden uitgevoerd
Een gebruiker weergeeft een video Adobe Flash-codering is ingesloten in een webpagina. Hallo-webpagina wordt opgeslagen in de lokale vaste schijf Hallo van Hallo RD Session Host-server. Hallo video wordt door een invoegtoepassing ingesloten speler gespeeld in Internet Explorer.

Dit scenario emuleert gebruikers uitgebreide inhoud webpagina's met multimedia bekijken. De meeste Hallo gegevens moet invoervak via VOBR.

### <a name="word-remote-typing---run-for-1800-seconds"></a>Externe te typen in Word - ~ 1800 seconden uitgevoerd
Een gebruiker typt een document via een RDP-sessie. Toetsaanslagen worden verzonden vanaf de clientzijde Hallo door Hallo RDP-sessie tooa document in Microsoft Word in Hallo externe sessie. Hallo typen snelheid is één teken elke 250 ms (totaal 7050 tekens). 

Dit is een Hallo meest voorkomende scenario's voor een werknemer kennis. Dit scenario wordt getest Hallo reactiesnelheid van een gebruiker te typen in een moderne werk processor. Dit scenario is gevoelige tooeven kleine wijzigingen in bandbreedtegebruik.

## <a name="tracking-hello-test-results"></a>De resultaten bekijkt hello bijhouden
U kunt Hallo tabel tooevaluate Hallo scenario's in uw omgeving te volgen. Hallo gegevens hieronder is alleen bedoeld ter illustratie - mogelijk aanzienlijk verschilt van wat u precies zien. 

Voor het gemak, nemen we aan dat alle scenario's worden getest met Hallo dezelfde 1920 x 1080 pixels schermresolutie en TCP-transport op een netwerk met een latentie (vertraging) minder dan 200 ms en netwerk jitter in Hallo 120 ms + merk van ongeveer 1%.

Over Hallo tabel:

* **Gemiddelde ervaring** bevat Hallo netwerkbandbreedte waarbij de productiviteit van de gebruiker heeft geen aanzienlijke gevolgen maar incidentele video of audio haperingen niet uitsluit. Hallo-systeem is kunnen toorecover snel door gebruik te maken van dynamische Hallo-logica. Hallo netwerkbandbreedte maakt een schatting poging tooguarantee Hallo kwaliteit van de gebruikerservaring Hallo.
  * **Merkbare problemen (einde-beheerpunt)** Hallo netwerkbandbreedte waar gebruikers wellicht opgevallen dat belangrijke problemen in hun ervaring en is van invloed op de productiviteit voor meetbare perioden bevat. Op dit moment Hallo RDP algoritmen hebben moeite en van de gebruiker Hallo kwaliteit vereisen vanwege onvoldoende netwerkbandbreedte kunnen niet worden gegarandeerd.
  * **Aanbevolen** Hallo netwerkbandbreedte voor goed of uitstekend aanbevolen bevat. Is gewoonlijk één stap hoger zijn dan de waarde Hallo in Hallo bijbehorende **gemiddelde ervaring** kolom.
  * **Opmerkingen bij de** opmerkingen bevatten.

| Test | Gemiddelde ervaring | Merkbare problemen (einde-beheerpunt) | Aanbevolen netwerkbandbreedte | Opmerkingen |
| --- | --- | --- | --- | --- |
| Executive/complexe PPT |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s voorkeur |Op 1 MB/s gaan veel animaties verloren |
| Eenvoudige PPT |5 MB/s |256 KB/s |10 MB/s |Om 256 KB/s laden Hallo dia met vertraging merkbaar |
| Internet Explorer |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s voorkeur |Web-video's zijn fuzzy op 1 MB/s en onregelmatig, snelle schuiven heeft problemen |
| Eenvoudige PDF |1 MB/s |256 KB/s |5 MB/s |Om 256 KB/s duurt het even tooload Hallo pagina |
| Gemengde PDF |1 MB/s |256 KB/s |5 MB/s |Op 256 KB/s neemt Hallo pagina een aanzienlijke hoeveelheid tijd tooload |
| Flash afspelen van video 's |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s voorkeur |Op 1 MB/s Hallo video grof is en sommige frames zijn verwijderd |
| Word externe typen |256 KB/s |128 KB/s |1 MB/s |Gebruiker merkt op 256 KB/s Hallo tijd tussen toetsaanslagen |

tooevaluate Hallo netwerkbandbreedte per gebruiker, maakt u een combinatie van Hallo bovenstaande scenario's en Hallo corresponderende gedeelte van de vereiste netwerkbandbreedte. Kies de hoogste aantal Hallo die nodig zijn voor uw scenario's. Omdat gebruikers bijna nooit alleen Hallo-systeem, kunt u sommige reserve voor gebruikers die werken gelijktijdig op Hallo hetzelfde netwerk.

## <a name="learn-more"></a>Meer informatie
* [Gebruik van netwerkbandbreedte Azure RemoteApp schatten](remoteapp-bandwidth.md)
* [Azure RemoteApp - hoe doet netwerkbandbreedte en de kwaliteit van zich werk samen?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp netwerkbandbreedte - algemene richtlijnen (als u niet kunt uw eigen testen)](remoteapp-bandwidthguidelines.md)

