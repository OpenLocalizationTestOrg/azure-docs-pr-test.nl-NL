---
title: de gebruikersgegevens aaaMigrate van Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toomigrate uw gebruikersgegevens in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a>Hoe toomigrate gegevens naar en van Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Kunt u veel verschillende hulpprogramma's en methoden tootransfer [gebruikersgegevens](remoteapp-upd.md) naar en van Azure RemoteApp. Hier volgen een aantal methoden:

* Kopiëren en plakken met behulp van het gedeelde Klembord
* Kopiëren van bestanden en gegevens tooa bestandsserver
* Kopiëren van bestanden tooOneDrive voor bedrijven via een browser
* Bestanden kopiëren met omleiding

> [!NOTE]
> U kunt Hallo OneDrive niet inschakelen voor synchronisatie-agents, bedrijfs- of - ze [worden niet ondersteund](remoteapp-onedrive.md) in Azure RemoteApp.
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a>Kopiëren en plakken in Windows Verkenner
Kopiëren en plakken met de Hallo Klembord is ingeschakeld in RemoteApp-implementaties [standaard](remoteapp-redirection.md). Hiermee kunnen gebruikers bestanden kopiëren tussen hun lokale PC's en RemoteApp-apps. Vaak via normale Hallo van het gebruik van apps in RemoteApp-hebben gebruikers opgeslagen bestanden tootheir UPDs - verplaatsen van gegevens buiten RemoteApp is eenvoudig:

1. [Verkenner als een app publiceren](remoteapp-publish.md) in een RemoteApp-verzameling. (Houd er rekening mee dat dit kan een beheertaak.)
2. Directe uw gebruikers toolaunch Hallo Verkenner-app die u hebt gepubliceerd en toouse die bestanden toocopy en plakken zowel naar hun UPD en van deze.

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a>Uploaden van bestanden en gegevens tooa bestandsserver door standaardnetwerk bestand kopiëren
Vaak organisaties gebruiken om servers toostore algemene bestandsgegevens. Als u Hallo server-naam of locatie weet, kunnen uw gebruikers Hallo lokale netwerk voor Hallo server bladeren en kopieert u hun bestanden, worden er veel zoals hierboven. U zult opnieuw wilt toopublish Verkenner tooRemoteApp en vervolgens te delen met uw gebruikers.

> [!NOTE]
> Hallo-bestandsserver moet op Hallo routeerbaar netwerk met RemoteApp is geïmplementeerd in.
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a>Kopiëren van bestanden tooOneDrive voor bedrijven
Hoewel u Hallo OneDrive voor bedrijven-synchronisatie-agent in RemoteApp niet inschakelen, kunt u nog steeds bestanden kopiëren vanaf uw tooOneDrive UPD voor bedrijven via een browser. 

1. Verkenner tooRemoteApp publiceren en vervolgens instrueren dat gebruikers tooaccess Hallo bestanden via de app. 
2. Het is eenvoudigste tootransfer bestanden als ze worden gecomprimeerd, zodat gebruikers een ZIP-bestand waarin alle Hallo bestanden toomove tooOneDrive voor bedrijven moeten maken.
3. Vraag gebruikers toogo toohello Office 365-portal en gaat u tooOneDrive en Hallo ZIP-bestand uploaden.

## <a name="copy-files-by-using-drive-redirection"></a>Kopiëren van bestanden met behulp van stationsomleiding
Als u hebt ingeschakeld [station omleiding](remoteapp-redirection.md), u hebt al een toegewezen station gemaakt voor uw gebruikers. In dit geval ze kunnen hun bestanden op Hallo omgeleid station zip en slaat u deze tootheir lokale PC.

## <a name="how-administrators-can-export-data"></a>Hoe kunnen beheerders gegevens exporteren

Beheert voor Azure RemoteApp alle gebruikersprofielschijven (UPD exporteren kunt) voor alle collecties binnen een abonnement tooAzure opslag met Azure PowerShell-cmdlet Export-AzureRemoteAppUserDisk.  Er is geen mogelijkheid tooselect afzonderlijke UPD van.  Wanneer Hallo PowerShell-opdracht wordt uitgevoerd, wordt elke gebruiker schijf een 50gb in grootte van de vaste schijf en geëxporteerde tooAzure opslag.  Kosten van Azure storage, onmiddellijk worden voor deze opslag.  Wanneer u deze opdracht uitvoert ervoor te zorgen zijn er geen sessies anders Hallo exporteren mislukt.

UPD de voor lid van domein Azure RemoteApp-implementaties kan alleen opnieuw in een RDS-implementatie worden gebruikt, niet van het domein gekoppelde implementaties kunnen niet worden gebruikt.  Als deze schijven worden gebruikt in een RDS-implementatie raden wij aan toouse onze [geautomatiseerde scripts](https://github.com/arcadiahlyy/aramigration) die wordt exporteren, converteren en Hallo van UPD importeren in een RDS-implementatie.

