---
title: Opmerkingen bij de release van de aaaMicrosoft Azure Opslagverkenner (Preview) | Microsoft Docs
description: Releaseopmerkingen voor Microsoft Azure Opslagverkenner (Preview)
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a>Opmerkingen bij de release van Microsoft Azure Opslagverkenner (Preview)

Dit artikel bevat Hallo release-opmerkingen voor Azure Storage Explorer 0.8.16 (Preview), evenals release-opmerkingen voor eerdere versies vrijgeven.

[Microsoft Azure Opslagverkenner (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is een zelfstandige app waarmee u tooeasily werken met Azure Storage-gegevens op Windows-, Mac OS- en Linux.

## <a name="version-0816-preview"></a>Versie 0.8.16 (Preview)
8/21/2017

### <a name="download-azure-storage-explorer-0816-preview"></a>Azure Storage Explorer 0.8.16 (Preview) downloaden
- [Azure Opslagverkenner (Preview) 0.8.16 voor Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Azure Opslagverkenner (Preview) 0.8.16 voor Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Azure Opslagverkenner (Preview) 0.8.16 voor Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a>Nieuw
* Wanneer u een blob opent, wordt Opslagverkenner u gevraagd tooupload Hallo gedownload bestand als een wijziging wordt gedetecteerd
* Verbeterde Azure Stack-aanmeldingservaring aanpast
* Hallo verbeterde prestaties van uploaden/downloaden van veel kleine bestanden op Hallo dezelfde tijd


### <a name="fixes"></a>Oplossingen
* Voor bepaalde typen blob zou kiezen te "vervangen" tijdens een upload-conflict soms leiden tot Hallo uploaden wordt opnieuw opgestart. 
* In versie 0.8.15, zou soms uploads achterstallige voor 99%.
* Tijdens het uploaden van bestanden tooa bestandsshare, als u hebt gekozen tooupload tooa directory, die nog niet bestaat, mislukt het uploaden.
* Opslagverkenner is niet juist genereren van tijdstempels voor handtekeningen voor gedeelde toegang en tabel query's.


Bekende problemen
* Met behulp van een naam en sleutel verbindingsreeks werkt momenteel niet. Het wordt opgelost in de volgende release Hallo. Tot die tijd kunt u met de naam en sleutel koppelen.
* Als u een bestand met een ongeldige naam van de Windows-bestand tooopen probeert, resulteren Hallo downloaden in een bestand niet gevonden fout.
* Wanneer u op 'Annuleren' voor een taak, duurt het even voor die taak toocancel. Dit is een beperking van hello Azure Opslagknooppunt bibliotheek.
* Nadat het uploaden van een blob wordt Hallo tabblad die Hallo uploaden gestart vernieuwd. Dit is een wijziging ten opzichte van vorige gedrag en ook wordt u toobe genomen terug toohello hoofdmap van Hallo-container in.
* Als u ervoor kiest verkeerde PINCODE/smartcardcertificaat hello, moet u toorestart in volgorde toohave vergeet Opslagverkenner dat besluit.
* paneel met toepassingsinstellingen Hallo-account kan worden weergegeven dat u nodig hebt tooreenter referenties toofilter abonnementen.
* Naam van de BLOB's (afzonderlijk of in een nieuwe naam blob-container) behoudt niet momentopnamen. Alle andere eigenschappen en metagegevens voor blobs, bestanden en entiteiten blijven behouden tijdens een naam te wijzigen.
* Hoewel Azure Stack momenteel geen bestandsshares ondersteunt, wordt een knooppunt bestandsshares nog steeds wordt weergegeven onder een gekoppelde Azure-Stack storage-account.
* Voor gebruikers op Ubuntu 14.04, moet u tooensure GCC toodate is-kunt u dit doen door het uitvoeren van Hallo opdrachten te volgen en de computer opnieuw te starten:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* Voor gebruikers op Ubuntu 17.04, moet u tooinstall GConf - kunt dit doen door Hallo de volgende opdrachten en opnieuw starten van de computer uitgevoerd:

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a>Versie 0.8.14 (Preview)
06/22/2017

### <a name="download-azure-storage-explorer-0814-preview"></a>Azure Storage Explorer 0.8.14 (Preview) downloaden
* [Download de Azure Opslagverkenner (Preview) 0.8.14 voor Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Download de Azure Opslagverkenner (Preview) 0.8.14 voor Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Azure Opslagverkenner (Preview) 0.8.14 voor Linux downloaden](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a>Nieuw

* Bijgewerkte Electron versie too1.7.2 in volgorde tootake profiteren van verschillende essentiële updates
* U kunt nu snel toegang tot Hallo online probleemoplossingsgids van Hallo help-menu
* Opslagverkenner probleemoplossing [handleiding][2]
* [Instructies] [ 3] voor het verbinden van tooan Stack Azure-abonnement

### <a name="known-issues"></a>Bekende problemen

* Knoppen op het Hallo-dialoogvenster voor bevestiging van verwijderen-map registreren niet bij Hallo muisklikken op Linux. Tijdelijke oplossing is toouse Hallo Enter-toets
* Als u ervoor kiest verkeerde PINCODE/smartcardcertificaat hello, moet u toorestart in volgorde toohave Opslagverkenner vergeet Hallo besluit
* Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken
* paneel met toepassingsinstellingen Hallo-account kan tonen, moet u referenties tooreenter in volgorde toofilter abonnementen
* Naam van de BLOB's (afzonderlijk of in een nieuwe naam blob-container) behoudt niet momentopnamen. Alle andere eigenschappen en metagegevens voor blobs, bestanden en entiteiten blijven behouden tijdens een naam te wijzigen.
* Hoewel Azure Stack momenteel geen bestandsshares ondersteunt, wordt een knooppunt bestandsshares nog steeds wordt weergegeven onder een gekoppelde Azure-Stack storage-account. 
* Ubuntu 14.04 installeren behoeften gcc versie bijwerken of bijgewerkt – stappen tooupgrade zijn hieronder:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a>Eerdere versies

* [Versie 0.8.13](#version-0813)
* [Versie 0.8.12 / 0.8.11 / 0.8.10](#version-0812--0811--0810)
* [Versie 0.8.9 / 0.8.8](#version-089--088)
* [Versie 0.8.7](#version-087)
* [Versie 0.8.6](#version-086)
* [Versie 0.8.5](#version-085)
* [Versie 0.8.4](#version-084)
* [Versie 0.8.3](#version-083)
* [Versie 0.8.2](#version-082)
* [Versie 0.8.0](#version-080)
* [Versie 0.7.20160509.0](#version-07201605090)
* [Versie 0.7.20160325.0](#version-07201603250)
* [Versie 0.7.20160129.1](#version-07201601291)
* [Versie 0.7.20160105.0](#version-07201601050)
* [Versie 0.7.20151116.0](#version-07201511160)


### <a name="version-0813"></a>Versie 0.8.13
12/05/2017

#### <a name="new"></a>Nieuw

* Opslagverkenner probleemoplossing [handleiding][2]
* [Instructies] [ 3] voor het verbinden van tooan Stack Azure-abonnement

#### <a name="fixes"></a>Oplossingen

* Vaste: Uploaden bestand heeft een hoog risico dat een out-of geheugenfout
* Vaste: U kunt nu aanmelden met PINCODE/Smartcard
* Vaste: Open in de Portal nu werkt met Azure China, Duitse Azure, Azure US Government en Azure-Stack
* Vaste: Tijdens het uploaden van een map tooa blob-container 'Ongeldige bewerking' zou soms treedt er een fout
* Vaste: Alles selecteren is uitgeschakeld terwijl het beheer van momentopnamen
* Vaste: Hallo metagegevens van Hallo base blob mogelijk overschreven na het Hallo-eigenschappen van de momentopnamen weer te geven

#### <a name="known-issues"></a>Bekende problemen

* Als u ervoor kiest verkeerde PINCODE/smartcardcertificaat hello, moet u toorestart in volgorde toohave Opslagverkenner vergeet Hallo besluit
* Tijdens het in- of uitzoomen op schaal, opnieuw Hallo zoomniveau tijdelijk worden toohello standaardniveau
* Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken
* paneel met toepassingsinstellingen Hallo-account kan tonen, moet u referenties tooreenter in volgorde toofilter abonnementen
* Naam van de BLOB's (afzonderlijk of in een nieuwe naam blob-container) behoudt niet momentopnamen. Alle andere eigenschappen en metagegevens voor blobs, bestanden en entiteiten blijven behouden tijdens een naam te wijzigen.
* Hoewel Azure Stack momenteel geen bestandsshares ondersteunt, wordt een knooppunt bestandsshares nog steeds wordt weergegeven onder een gekoppelde Azure-Stack storage-account. 
* Ubuntu 14.04 installeren behoeften gcc versie bijwerken of bijgewerkt – stappen tooupgrade zijn hieronder:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a>Versie 0.8.12 / 0.8.11 / 0.8.10
04/07/2017

#### <a name="new"></a>Nieuw

* Opslagverkenner wordt nu automatisch gesloten wanneer u een update vanaf Hallo updatebericht installeert
* In-place snelle toegang biedt een verbeterde ervaring voor het werken met uw vaak gebruikte resources
* In de Blob-Container-editor Hallo nu ziet u welke virtuele machine een geleaste blob behoort
* U kunt nu Hallo linkerkant Configuratiescherm samenvouwen
* Detectie nu wordt uitgevoerd op Hallo dezelfde tijd als download
* Gebruik maken van statistieken in Hallo Blob-Container, bestandsshare en tabel editors toosee Hallo grootte van de resource of selectie
* U kunt nu aanmelden tooAzure Active Directory (AAD) op basis van Azure-Stack-accounts. 
* U kunt nu uploaden meer dan 32 MB tooPremium storage-accounts archiefbestanden
* Verbeterde Toegankelijkheidsondersteuning voor
* U kunt nu toevoegen vertrouwde Base64-gecodeerd x.509-SSL-certificaten gaat tooEdit -&gt; SSL-certificaten -&gt; certificaten importeren

#### <a name="fixes"></a>Oplossingen

* Vaste: na het vernieuwen van een account referenties Hallo structuurweergave zou soms niet automatisch vernieuwd
* Vaste: genereren van een SAS voor emulator wachtrijen en tabellen zou leiden tot een ongeldige URL
* Vaste: premium storage-accounts kunnen nu worden uitgebreid terwijl een proxy is ingeschakeld
* Vaste: Hallo knop toepassen op Hallo accounts management-pagina werkt niet als u had 1 of 0 accounts die zijn geselecteerd
* Vaste: het uploaden van BLOB's waarvoor oplossingen mislukken - 0.8.11, vast 
* Vaste: feedback sturen is onderverdeeld in 0.8.11 - 0.8.12, vast 

#### <a name="known-issues"></a>Bekende problemen

* Na de upgrade too0.8.10, moet u toorefresh alle uw referenties.
* Terwijl het in- of uitzoomen op schaal, Hallo zoomniveau kan tijdelijk worden opnieuw ingesteld toohello standaardniveau.
* Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken.
* paneel met toepassingsinstellingen Hallo-account kan worden weergegeven dat u referenties tooreenter in volgorde toofilter abonnementen moet.
* Naam van de BLOB's (afzonderlijk of in een nieuwe naam blob-container) behoudt niet momentopnamen. Alle andere eigenschappen en metagegevens voor blobs, bestanden en entiteiten blijven behouden tijdens een naam te wijzigen.
* Hoewel Azure Stack momenteel geen bestandsshares ondersteunt, wordt een knooppunt bestandsshares nog steeds wordt weergegeven onder een gekoppelde Azure-Stack storage-account. 
* Ubuntu 14.04 installeren behoeften gcc versie bijwerken of bijgewerkt – stappen tooupgrade zijn hieronder:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a>Versie 0.8.9 / 0.8.8
02/23/2017

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Nieuw

* Opslagverkenner 0.8.9 downloadt automatisch de meest recente versie Hallo voor updates.
* Hotfix: met behulp van een portal SAS-URI tooattach die een opslagaccount tot een fout leiden zou gegenereerd.
* U kunt nu maken, beheren en blob momentopnamen promoveren.
* U kunt nu tooAzure China, Duitse Azure en Azure US Government accounts aanmelden.
* U kunt nu Hallo zoomniveau wijzigen. Hallo-opties in Hallo weergave menu tooZoom In uitzoomen en zoomen opnieuw gebruiken.
* Unicode-tekens worden nu ondersteund in de metagegevens van de gebruiker voor blobs en bestanden.
* Toegankelijkheid is verbeterd.
* Opmerkingen bij de release van Hallo volgende versie kunnen worden bekeken in Hallo updatebericht. U kunt ook de huidige release-opmerkingen Hallo van Hallo Help-menu weergeven.

#### <a name="fixes"></a>Oplossingen

* Vaste: Hallo versienummer nu juist wordt weergegeven in het Configuratiescherm in Windows
* Vaste: search is niet langer beperkt too50, 000 knooppunten
* Vaste: bestandsshare voor het uploaden van tooa ingezet permanent verloren als doelmap Hallo al niet bestaat
* Vaste: verbeterde stabiliteit voor lange uploaden en downloaden

#### <a name="known-issues"></a>Bekende problemen

* Terwijl het in- of uitzoomen op schaal, Hallo zoomniveau kan tijdelijk worden opnieuw ingesteld toohello standaardniveau.
* Snelle toegang werkt alleen met een abonnement op basis van items. Lokale resources of resources via de sleutel- of SAS-token is gekoppeld, worden niet ondersteund in deze release.
* Het duurt een paar seconden toonavigate toohello doelresource, afhankelijk van hoeveel resources die u hebt Snelweergavetoegang.
* Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken.

12/16/2016
### <a name="version-087"></a>Versie 0.8.7

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nieuw

* U kunt kiezen hoe tooresolve conflicten op Hallo begin van een update downloaden of sessie in Hallo activiteiten venster kopiëren
* Beweeg de muisaanwijzer over een tabblad toosee Hallo volledig pad van Hallo storage resource
* Wanneer u op een tabblad klikt, synchroniseert het met de locatie in het navigatiedeelvenster van Hallo linkerkant

#### <a name="fixes"></a>Oplossingen

* Vaste: Opslagverkenner is nu een vertrouwd app op Mac
* Vaste: Ubuntu 14.04 wordt opnieuw ondersteund
* Vaste: Soms Hallo-account toevoegen UI knippert bij het laden van abonnementen
* Vaste: Soms niet alle opslagbronnen zijn vermeld in Hallo linkerkant navigatiedeelvenster
* Vaste: Hallo actievenster soms weergegeven leeg acties
* Vaste: venstergrootte Hallo van Hallo laatste gesloten sessie wordt nu bewaard
* Vaste: U kunt openen meerdere tabbladen voor Hallo dezelfde resource met Hallo contextmenu

#### <a name="known-issues"></a>Bekende problemen

* Snelle toegang werkt alleen met een abonnement op basis van items. Lokale resources of resources via de sleutel- of SAS-token is gekoppeld, worden niet ondersteund in deze release
* Het kan een paar seconden toonavigate toohello doelresource, afhankelijk van hoeveel resources die u hebt duren voor Snelweergavetoegang
* Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken
* Zoeken ingangen zoeken over ongeveer 50.000 knooppunten - hierna prestaties kan van invloed zijn of niet-verwerkte uitzondering veroorzaken
* Voor Hallo eerst met Hallo Opslagverkenner op Mac OS, ziet u mogelijk meerdere prompts van de gebruiker toestemming tooaccess sleutelhanger daarvoor. We raden dat u altijd toestaan selecteren zodat het Hallo-prompt opnieuw niet weergegeven

11/18/2016
### <a name="version-086"></a>Versie 0.8.6

#### <a name="new"></a>Nieuw

* U kunt nu services toohello Snelweergavetoegang pincode doorgaans voor eenvoudige navigatie gebruikt
* U kunt nu meerdere editors openen in andere tabbladen. Een tijdelijke tabblad; tooopen met één klik Dubbelklik tooopen een permanente tabblad. U kunt ook klikken op Hallo tijdelijke tabblad toomake dit een permanente tabblad
* We hebben aangebracht merkbare prestaties en stabiliteitsverbeteringen voor uploadt en downloads, met name voor grote bestanden op snelle machines
* Lege 'virtuele' mappen kunnen nu worden gemaakt in de blob-containers
* We hebben afgebakende zoekopdracht met onze nieuwe verbeterde subtekenreeks search, zodat u nu twee opties voor het zoeken hebt opnieuw zijn geïntroduceerd: 
    * Globale zoeken: Geef een zoekterm in het Zoektekstvak Hallo
    * Afgebakende zoekopdracht - Hallo Vergrootglas pictogram volgende tooa knooppunt, klik op vervolgens het einde van een zoekopdracht term toohello van Hallo-pad toevoegen of met de rechtermuisknop op en selecteer 'Zoeken vanaf hier'
* We hebben verschillende thema's toegevoegd: licht (standaard), donker, Hoog Contrast zwart en Hoog Contrast wit. Ga tooEdit -&gt; thema's toochange uw voorkeur thema's
* U kunt eigenschappen van Blob en de bestandsnaam wijzigen
* Er wordt nu ondersteuning gecodeerde (base64) en ongecodeerde Wachtrijberichten
* Op Linux, een 64-bits besturingssysteem is nu vereist. Voor deze release wordt alleen ondersteund 64-bits Ubuntu 16.04.1 TNS
* We hebben onze logo bijgewerkt!

#### <a name="fixes"></a>Oplossingen

* Opgelost: Blokkering problemen scherm
* Vaste: Verbeterde beveiliging
* Vaste: Soms dubbele gekoppelde accounts kunnen worden weergegeven
* Vaste: Een blob met een niet-gedefinieerde type inhoud kan genereren een uitzondering
* Vaste: Openen Hallo deelvenster van de Query op een lege tabel was het niet mogelijk
* Vaste: Varieert fouten in de zoekopdracht
* Vaste: Het aantal resources die worden geladen vanuit 50 too100 wanneer te klikken op 'Meer Load' Hallo verhoogd
* Vaste: Op de eerste keer uitvoert als een account is aangemeld, we nu alle abonnementen voor dat account standaard selecteren 

#### <a name="known-issues"></a>Bekende problemen

* Deze release van Hallo Opslagverkenner kan niet worden uitgevoerd op Ubuntu 14.04
* tooopen meerdere tabbladen voor dezelfde resource, komen niet continu klikt u op Hallo Hallo dezelfde resource. Klik op een andere resource en vervolgens terug en klik vervolgens op de oorspronkelijke bron tooopen Hallo deze opnieuw in een ander tabblad 
* Snelle toegang werkt alleen met een abonnement op basis van items. Lokale resources of resources via de sleutel- of SAS-token is gekoppeld, worden niet ondersteund in deze release
* Het kan een paar seconden toonavigate toohello doelresource, afhankelijk van hoeveel resources die u hebt duren voor Snelweergavetoegang
* Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken
* Zoeken ingangen zoeken over ongeveer 50.000 knooppunten - hierna prestaties kan van invloed zijn of niet-verwerkte uitzondering veroorzaken

10/03/2016
### <a name="version-085"></a>Versie 0.8.5

#### <a name="new"></a>Nieuw

* Kan zich nu gebruik Portal gegenereerde SAS-codes tooattach tooStorage Accounts en resources

#### <a name="fixes"></a>Oplossingen

* Vaste: race condition tijdens de zoekopdracht soms veroorzaakt knooppunten toobecome niet uitbreidbaar
* Vaste: 'HTTP gebruiken' werkt niet bij het verbinden van tooStorage Accounts met de naam en sleutel
* Vaste: SAS-sleutels (die speciaal Portal gegenereerde) retourneren een foutmelding 'afsluitende slash'
* Vaste: tabel importeren problemen
    * Soms zijn partitiesleutel en de rijsleutel teruggedraaid
    * Kan geen tooread 'null' partitiesleutels

#### <a name="known-issues"></a>Bekende problemen

* Zoeken ingangen zoeken over ongeveer 50.000 knooppunten - hierna gevolgen voor de prestaties
* Azure Stack ondersteunt momenteel geen bestanden, zodat tooexpand bestanden bij een fout wordt weergegeven

09/12/2016
### <a name="version-084"></a>Versie 0.8.4

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nieuw

* Genereren, directe koppelingen toostorage accounts, containers, wachtrijen, tabellen, of bestandsshares voor delen en eenvoudig toegang krijgen tot bronnen tooyour - Windows en Mac OS-ondersteuning
* Zoeken naar de blob-containers, tabellen, wachtrijen, bestandsshares of storage-accounts in het zoekvak Hallo
* U kunt nu componenten in de opbouwfunctie voor query's Hallo tabel groeperen
* Wijzig de naam en de blob-containers, bestandsshares, tabellen, blobs, blob-mappen, bestanden en mappen uit binnen SAS gekoppelde accounts en containers kopiëren en plakken
* Naam en het kopiëren van blob-containers en bestandsshares nu behouden eigenschappen en metagegevens

#### <a name="fixes"></a>Oplossingen

* Vaste: kan niet worden bewerkt tabelentiteiten als ze Booleaanse of binaire eigenschappen bevatten

#### <a name="known-issues"></a>Bekende problemen

* Zoeken ingangen zoeken over ongeveer 50.000 knooppunten - hierna gevolgen voor de prestaties

08/03/2016
### <a name="version-083"></a>Versie 0.8.3

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nieuw

* Wijzig de naam van containers, tabellen, bestandsshares
* Verbeterde ervaring voor de opbouwfunctie voor Query
* Mogelijkheid toosave en de belasting query 's
* Directe koppelingen toostorage accounts of containers, wachtrijen, tabellen of bestandsshares voor het delen en eenvoudige toegang tot uw resources (alleen Windows - Mac OS ondersteunen binnenkort beschikbaar.)
* Mogelijkheid toomanage en CORS-regels configureren

#### <a name="fixes"></a>Oplossingen

* Vaste: Microsoft-Accounts hernieuwde verificatie vereist is om de 8-12 uur

#### <a name="known-issues"></a>Bekende problemen

* Soms hello UI lijkt bevroren - maximaliseren Hallo venster helpt dit probleem oplossen
* Mac OS-installatie mogelijk verhoogde machtigingen
* Paneel met toepassingsinstellingen account kan tonen, moet u referenties tooreenter in volgorde toofilter abonnementen
* Naamswijzigingen bestandsshares, blob-containers en tabellen blijven niet behouden metagegevens of andere eigenschappen van het Hallo-container, zoals het quotum voor de bestandsshare, openbare toegangsniveau of beleidsregels voor toegang
* Naam van de BLOB's (afzonderlijk of in een nieuwe naam blob-container) behoudt niet momentopnamen. Alle andere eigenschappen en metagegevens voor blobs, bestanden en entiteiten blijven behouden tijdens een naam wijzigen
* Kopiëren of verwijderen van resources werkt niet in SAS gekoppelde accounts

07/07/2016
### <a name="version-082"></a>Versie 0.8.2

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nieuw

* Storage-Accounts zijn gegroepeerd op abonnementen. opslag van de ontwikkeling en resources die zijn aangesloten via een sleutel- of SAS worden weergegeven onder het knooppunt (lokaal en bijlage)
* Afmelden bij accounts in Configuratiescherm van de 'Azure Accountinstellingen'
* Proxy-instellingen tooenable configureren en beheren van aanmeldingspagina
* Maken en de blob-leases opsplitsen
* Open blob-containers, wachtrijen, tabellen en bestanden met één klik

#### <a name="fixes"></a>Oplossingen

* Vaste: Wachtrijberichten ingevoegd met .NET of Java-bibliotheken zijn niet goed gedecodeerd van base64
* Vaste: $metrics tabellen worden niet weergegeven voor Blob Storage-accounts
* Vaste: tabellen knooppunt werkt niet voor lokale opslag van (ontwikkeling)

#### <a name="known-issues"></a>Bekende problemen

* Mac OS-installatie mogelijk verhoogde machtigingen

06/15/2016
### <a name="version-080"></a>Versie 0.8.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nieuw

* Share-ondersteuning: weergeven, uploaden, downloaden, kopiëren van bestanden en mappen, SAS URI's (maken en verbinding maken)
* Verbeterde gebruikerservaring voor tooStorage verbinden met SAS URI's of toegangscodes
* De resultaten van de query exporteren
* De tabel kolom volgorde en aanpassen
* $Logs blob-containers en $metrics tabellen bekijken voor Storage-Accounts met ingeschakelde metrische gegevens
* Verbeterde exporteren en importeren van gedrag, bevat nu het soort waarde

#### <a name="fixes"></a>Oplossingen

* Vaste: uploaden of grote blobs downloaden kan leiden tot onvolledige uploads/downloads
* Vaste: bewerken, toevoegen of importeren van een entity met een numerieke waarde ('1') wordt converteren toodouble
* Vaste: Kan geen tooexpand Hallo tabelknooppunt in de lokale ontwikkelingsomgeving Hallo

#### <a name="known-issues"></a>Bekende problemen

* $metrics tabellen zijn niet zichtbaar voor Blob Storage-accounts
* Berichten in wachtrij plaatsen toegevoegd via een programma mogelijk niet correct weergegeven als het Hallo-berichten moeten worden gecodeerd met Base64-codering

05/17/2016
### <a name="version-07201605090"></a>Versie 0.7.20160509.0

#### <a name="new"></a>Nieuw

* Betere foutafhandeling voor de app vastloopt

#### <a name="fixes"></a>Oplossingen

* Vaste bug waar informatiebalk berichten soms worden niet weergegeven als aanmeldingsreferenties vereist zijn

#### <a name="known-issues"></a>Bekende problemen

* Tabellen: Toevoegen, bewerken of importeren van een entiteit die een eigenschap met een ambiguously numerieke waarde, zoals "1" of "1.0 heeft" en gebruiker probeert toosend Hallo als een `Edm.String`, Hallo waarde wordt terugkeren via Hallo client-API als een Edm.Double

03/31/2016

### <a name="version-07201603250"></a>Versie 0.7.20160325.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Nieuw

* Tabel ondersteuning: weergeven, query, export, importeren en CRUD-bewerkingen voor entiteiten
* Wachtrij-ondersteuning: bekijken, toe te voegen, dequeueing berichten
* Genereren van SAS-URI's voor Opslagaccounts
* TooStorage Accounts verbinden met SAS URI 's
* Meldingen voor toekomstige updates tooStorage Explorer updates
* Bijgewerkte uiterlijk

#### <a name="fixes"></a>Oplossingen

* Verbeteringen in prestaties en betrouwbaarheid

### <a name="known-issues-amp-mitigations"></a>Bekende problemen &amp; oplossingen

* Downloaden van bestanden van de grote blob werkt niet correct - wordt u aangeraden AzCopy terwijl we dit probleem op te lossen 
* Accountreferenties wordt niet opgehaald of in de cache opgeslagen als basismap Hallo kan niet worden gevonden of kan niet naar worden geschreven
* Als we zijn toevoegen, bewerken of importeren van een entiteit die een eigenschap met een ambiguously numerieke waarde, zoals "1" of "1.0 heeft" en Hallo gebruiker toosend probeert als een `Edm.String`, Hallo waarde wordt terugkeren via Hallo client-API als een Edm.Double
* Bij het importeren van CSV-bestanden met meerdere regels records kunnen Hallo gegevens ophalen afgekapt of versleuteld

02/03/2016

### <a name="version-07201601291"></a>Versie 0.7.20160129.1

#### <a name="fixes"></a>Oplossingen

* Verbeterde prestaties bij het uploaden, downloaden en blobs kopiëren

01/14/2016

### <a name="version-07201601050"></a>Versie 0.7.20160105.0

#### <a name="new"></a>Nieuw

* Linux-ondersteuning (pariteit functies tooOSX)
* Blob-containers met Shared Access Signatures (SAS)-sleutel niet toevoegen
* Storage-Accounts voor Azure China toevoegen
* Storage-Accounts met aangepaste eindpunten toevoegen
* Openen en bekijken Hallo inhoud tekst en afbeeldingen blobs
* Blob-eigenschappen en metagegevens weergeven en bewerken

#### <a name="fixes"></a>Oplossingen

* Vaste: uploaden of downloaden van een groot aantal blobs (500 +) soms mogelijk Hallo app toohave een wit scherm 
* Vaste: bij het instellen van blob-container openbaar toegangsniveau Hallo nieuwe waarde is niet bijgewerkt totdat u Hallo focus op Hallo container opnieuw instelt. Bovendien Hallo dialoogvenster standaard altijd te 'geen enkele openbare toegang' en niet Hallo werkelijke huidige waarde.
* Ondersteuning voor betere algehele toetsenbord toegankelijkheid en -gebruikersinterface
* Breadcrumbs tekstomloop geschiedenis wanneer het lang met witruimte
* Dialoogvenster SAS ondersteunt validatie voor invoer
* Lokale opslag blijft toobe beschikbaar, zelfs als de gebruikersreferenties zijn verlopen
* Wanneer een geopende blob-container wordt verwijderd, is Hallo blob explorer aan de rechterkant Hallo gesloten

#### <a name="known-issues"></a>Bekende problemen

* Linux installeren behoeften gcc versie bijwerken of bijgewerkt – stappen tooupgrade zijn hieronder: 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

11/18/2015
### <a name="version-07201511160"></a>Versie 0.7.20151116.0

#### <a name="new"></a>Nieuw

* Mac OS en Windows-versies
* Tooview aanmelden met uw Storage-Accounts: gebruik uw Org-Account, Microsoft-Account, 2FA, enzovoort.
* Opslag voor lokale ontwikkeling (opslagemulator, gebruiken alleen-Windows)
* Ondersteuning voor Azure Resource Manager en Classic resource
* Maken en verwijderen van blobs, wachtrijen of tabellen
* Zoeken naar specifieke blobs, wachtrijen of tabellen
* Bekijk de inhoud Hallo van blob-containers
* Navigeren door mappen
* Uploaden, downloaden en verwijderen van blobs en mappen
* Blob-eigenschappen en metagegevens weergeven en bewerken
* SAS sleutels genereren
* Beheren en opgeslagen toegang beleid (SAP) maken
* Blobs op voorvoegsel zoeken
* Sleep n neerzetten van bestanden tooupload of downloaden

#### <a name="known-issues"></a>Bekende problemen

* Bij het instellen van blob-container openbaar toegangsniveau wordt Hallo nieuwe waarde pas bijgewerkt wanneer u Hallo focus op Hallo container opnieuw instellen
* Wanneer u Hallo dialoogvenster tooset Hallo openbare toegangsniveau opent, bevat wordt altijd 'Geen openbare toegang' hello standaard en niet Hallo werkelijke huidige waarde
* Gedownloade blobs hernoemen niet
* Logboekvermeldingen activiteit wordt soms 'hangen' een onderhanden status wanneer er een fout optreedt en het Hallo-fout niet wordt weergegeven
* Soms crashes of schakelt volledig wit wanneer u probeert tooupload of een groot aantal blobs downloaden
* Soms annuleren van een kopieerbewerking werkt niet
* Tijdens het maken van een container (wachtrij-blob/tabelnaam) als u een ongeldige naam invoeren en doorgaan toocreate andere onder een andere containertype u kan niet de focus instelt op het nieuwe type Hallo
* Kan geen nieuwe map maken of wijzig de map




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md