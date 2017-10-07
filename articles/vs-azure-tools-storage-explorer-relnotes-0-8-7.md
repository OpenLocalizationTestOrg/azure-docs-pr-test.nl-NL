---
title: aaaMicrosoft Azure Storage Explorer 0.8.7 (Preview) | Microsoft Docs
description: Releaseopmerkingen voor Microsoft Azure Storage Explorer 0.8.7 (Preview)
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
ms.date: 01/18/2017
ms.author: cawa
ms.openlocfilehash: 9fdd491a3ea838e20f9d4f82c176cfb02fbe306b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-087-preview"></a>Microsoft Azure Opslagverkenner (Preview) 0.8.7
## <a name="overview"></a>Overzicht
Dit artikel bevat Hallo release-opmerkingen voor Azure Storage Explorer 0.8.7 preview-versie.

[Microsoft Azure Opslagverkenner (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is een zelfstandige app waarmee u tooeasily werken met Azure Storage-gegevens op Windows-, Mac OS- en Linux.

## <a name="azure-storage-explorer-087-preview"></a>Azure Opslagverkenner (Preview) 0.8.7
### <a name="download-azure-storage-explorer-087-preview"></a>Azure Storage Explorer 0.8.7 (Preview) downloaden
- [Azure Storage Explorer 0.8.7 Preview voor Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Azure Storage Explorer 0.8.7 Preview voor Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Azure Storage Explorer 0.8.7 Preview voor Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new-updates"></a>Nieuwe updates
* U kunt kiezen hoe tooresolve conflicten op Hallo begin van een update downloaden of kopiëren van de sessie in Hallo **activiteiten** venster.
* Beweeg de muisaanwijzer over een tabblad toosee Hallo volledig pad van Hallo storage resource.
* Wanneer u een tabblad klikt, wordt het met de locatie in het navigatiedeelvenster van Hallo linkerkant synchroniseert.

### <a name="fixes"></a>Oplossingen
* Vaste: Opslagverkenner is nu een vertrouwd app op Mac OS.
* Vaste: Omdat Ubuntu 14.04 opnieuw wordt ondersteund.
* Vaste: Soms hello toevoegen Account UI knippert bij het laden van abonnementen.
* Vaste: Soms niet alle opslagbronnen zijn vermeld in Hallo-navigatievenster aan de linkerkant.
* Vaste: Hallo actievenster soms weergegeven leeg acties.
* Vaste: venstergrootte Hallo van Hallo laatste gesloten sessie nu blijft behouden.
* Vaste: U kunt openen meerdere tabbladen voor Hallo dezelfde resource met Hallo contextmenu.

### <a name="known-issues"></a>Bekende problemen
* Snelle toegang werkt alleen met items op basis van abonnement. Lokale resources of resources via de sleutel- of SAS-token is gekoppeld, worden niet ondersteund in deze release.
* Het duurt een paar seconden toonavigate toohello doelresource, afhankelijk van hoeveel resources die u hebt Snelweergavetoegang.
* Als meer dan drie groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken.
* Zoeken ingangen zoeken over ongeveer 50.000 knooppunten - hierna prestaties kan van invloed zijn, of kan ertoe leiden dat niet-verwerkte uitzonderingen.
* Voor Hallo eerst met Hallo Opslagverkenner op Mac OS, ziet u mogelijk meerdere prompts van de gebruiker toestemming tooaccess Hallo sleutelhanger daarvoor. We raden u **altijd toestaan** zodat Hallo prompt niet opnieuw weergeven

## <a name="previous-releases"></a>Eerdere versies
### <a name="features"></a>Functies
#### <a name="main-features"></a>Belangrijkste functies
* Mac OS, Linux, en Windows-versies
* Tooview aanmelden met uw Opslagaccounts gegroepeerd op abonnement:
    * Gebruik uw Org-Account, Microsoft-Account, 2FA, enzovoort.
    * Proxyinstellingen configureren en beheren
    * Verwijderen van accounts met afmelden
* Verbinding maken met behulp van tooStorage-Accounts:
    * Naam en sleutel
    * Aangepaste eindpunten (met inbegrip van Azure voor China)
    * De SAS-URI voor Opslagaccounts
* Ondersteuning voor Azure Resource Manager en Classic opslag
* Genereren van SAS-sleutels voor blobs, blob-containers, tabellen, wachtrijen of bestandsshares
* Verbinding maken met tooblob containers, wachtrijen, tabellen of bestandsshares met Shared Access Signatures (SAS)-sleutel
* Toegangsbeleid opgeslagen voor blob-containers, wachtrijen, tabellen of bestandsshares beheren
* Ontwikkeling van lokale opslag met de Opslagemulator (alleen Windows)
* Blob-containers, wachtrijen of tabellen maken en verwijderen
* Weergave $logs blob-containers en $metrics tabellen
* Zoeken naar specifieke blobs, wachtrijen, tabellen of bestandsshares
* Directe koppelingen toostorage accounts of containers, tabellen, wachtrijen of bestand deelt voor het delen en eenvoudige toegang tot uw resources
* Wijzig de naam van blob-containers, tabellen, bestandsshares
* Mogelijkheid toomanage en CORS-regels configureren
* Kopieer eenvoudig primaire en secundaire sleutel voor Opslagaccounts
* MD5-controles op uploaden en downloaden voor gegevensintegriteit en consistentie
* Zoeken naar de blob-containers, tabellen, wachtrijen, bestandsshares of storage-accounts in het zoekvak Hallo
* U kunt nu services toohello Snelweergavetoegang pincode doorgaans voor eenvoudige navigatie gebruikt
* U kunt nu meerdere editors openen in andere tabbladen. Een tijdelijke tabblad; tooopen met één klik Dubbelklik op een permanente tabblad tooopen. U kunt ook klikken op Hallo tijdelijke tabblad toomake dit een permanente tabblad
* Prestaties en stabiliteit verbeteringen voor het uploaden en downloaden, met name voor grote bestanden op snelle machines
* We zijn reintroducing Hallo verbeterde afgebakende zoekopdracht en toegevoegde Hallo concept van het bereik. Voer Hallo pad tooa knooppunt via Hallo aanwijzen pictogram, -die 'Zoeken vanaf hier', of handmatig tooscope dat knooppunt rechtermuisknop te klikken op >. Als bereik, kunt u een zoekopdracht term toohello end van Hallo pad toodeep zoeken vanaf dat knooppunt toevoegen
* We hebben verschillende thema's toegevoegd: licht (standaard), donker, Hoog Contrast zwart en Hoog Contrast wit.
* Ga tooEdit toochange thema's -> uw voorkeur thema's
* Op Linux, een 64-bits besturingssysteem is nu vereist
* We hebben onze logo bijgewerkt!
#### <a name="blobs"></a>Blobs
* Blobs weergeven en navigeren door mappen
* Uploaden, downloaden, verwijderen en blobs en mappen kopiëren
* Openen en bekijken Hallo inhoud tekst en afbeeldingen blobs
* Blob-eigenschappen en metagegevens weergeven en bewerken
* Blobs op voorvoegsel zoeken
* Maken en leases voor blobs en blob-containers opsplitsen
* Sleep n tooupload bestanden verwijderen
* De naam van blobs en mappen
* Lege 'virtuele' mappen kunnen nu worden gemaakt in de blob-containers
* U kunt Hallo Blob en het bestand eigenschappen wijzigen
#### <a name="tables"></a>Tabellen
* Weergeven en entiteiten met ODATA query of gebruik een query builder toocreate complexe query 's
* Toevoegen, bewerken en verwijderen van entiteiten
* Importeren en exporteren van de inhoud van de tabel in CSV-indeling (inclusief queryresultaten exporteren)
* De volgorde van kolommen aanpassen
* Mogelijkheid toosave query 's
#### <a name="queues"></a>Wachtrijen
* De laatste 32 berichten kort weergeven
* Toevoegen, uit de wachtrij halen, berichten weergeven
* Wachtrij leegmaken
* Er wordt mogelijk gemaakt voor u toodecide of u tooencode/decoderen uw berichten in wachtrij plaatsen wilt
#### <a name="file-shares"></a>Bestandsshares
* Bestanden bekijken en te navigeren door mappen
* Bestanden en directory’s uploaden, downloaden, verwijderen en kopiëren
* Bestand-eigenschappen weergeven
* Wijzig de naam van bestanden en mappen

### <a name="bug-fixes"></a>Oplossingen voor problemen
* Opgelost: Blokkering problemen scherm
* Vaste: Verbeterde beveiliging

### <a name="known-issues"></a>Bekende problemen
* Zoeken ingangen zoeken over ongeveer 50.000 knooppunten - hierna, de prestaties mogelijk betrokken Mac OS-installatie mogelijk verhoogde machtigingen
* Paneel met toepassingsinstellingen account kan tonen, moet u tooreenter referenties toofilter abonnementen
* Naam van de BLOB's (afzonderlijk of in een nieuwe naam blob-container) behoudt niet momentopnamen. Alle andere eigenschappen en metagegevens voor blobs, bestanden en entiteiten blijven behouden tijdens een naam wijzigen
* Azure-Stack ondersteunt momenteel geen bestanden, dus probeert tooexpand hello **bestanden** knooppunt resulteert in een fout opgetreden
* Linux-14.04 installeren moet gcc versie bijwerken of bijgewerkt. Hallo volgende stappen laten zien hoe tooupgrade:

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

### <a name="previous-versions"></a>Vorige versies
#### <a name="october-2016-release-version-085"></a>Release van oktober 2016 (versie 0.8.5)
* [Download voor Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Download voor Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Download voor Linux](https://go.microsoft.com/fwlink/?LinkId=809308)
