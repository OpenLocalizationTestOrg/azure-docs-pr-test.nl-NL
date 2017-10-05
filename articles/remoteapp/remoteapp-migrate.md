---
title: Gegevens migreren van Azure RemoteApp | Microsoft Docs
description: Informatie over het migreren van uw gebruikersgegevens in Azure RemoteApp.
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
ms.openlocfilehash: ba3cf4c6834279bbd7f94d666fd8abbb7ac05bf0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-migrate-data-into-and-out-of-azure-remoteapp"></a>Het migreren van gegevens naar en van Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

U kunt veel verschillende hulpprogramma's en -methoden gebruiken om over te dragen [gebruikersgegevens](remoteapp-upd.md) naar en van Azure RemoteApp. Hier volgen een aantal methoden:

* Kopiëren en plakken met behulp van het gedeelde Klembord
* Kopiëren van bestanden en gegevens op een bestandsserver
* Bestanden kopiëren naar OneDrive voor bedrijven via een browser
* Bestanden kopiëren met omleiding

> [!NOTE]
> U kunt de OneDrive niet inschakelen voor synchronisatie-agents, bedrijfs- of - ze [worden niet ondersteund](remoteapp-onedrive.md) in Azure RemoteApp.
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a>Kopiëren en plakken in Windows Verkenner
Kopiëren en plakken met behulp van het Klembord is ingeschakeld in RemoteApp-implementaties [standaard](remoteapp-redirection.md). Hiermee kunnen gebruikers bestanden kopiëren tussen hun lokale PC's en RemoteApp-apps. Vaak in de normale loop van het gebruik van apps in RemoteApp-hebben gebruikers opgeslagen bestanden in hun UPDs - verplaatsen van gegevens buiten RemoteApp is eenvoudig:

1. [Verkenner als een app publiceren](remoteapp-publish.md) in een RemoteApp-verzameling. (Houd er rekening mee dat dit kan een beheertaak.)
2. Uw gebruikers Start de Verkenner-app die u hebt gepubliceerd en gebruikt deze om te kopiëren en plakken van bestanden in hun UPD zowel buiten het rechtstreeks.

## <a name="upload-files-and-data-to-a-file-server-by-using-standard-network-file-copy"></a>Uploaden van bestanden en gegevens op een bestandsserver met behulp van standaard netwerk bestand kopiëren
Bestandsservers vaak organisaties gebruiken voor het opslaan van algemene gegevens. Als u de servernaam of locatie, kunnen uw gebruikers het lokale netwerk voor de server te bladeren en kopieert u hun bestanden, worden er veel zoals hierboven. Opnieuw moet u Windows Verkenner naar gepubliceerd RemoteApp en vervolgens te delen met uw gebruikers.

> [!NOTE]
> De bestandsserver moet op het routeerbaar netwerk die RemoteApp is geïmplementeerd in.
> 
> 

## <a name="copy-files-to-onedrive-for-business"></a>Bestanden kopiëren naar OneDrive voor bedrijven
Hoewel u de OneDrive voor bedrijven-synchronisatie-agent in RemoteApp niet inschakelen, kunt u nog steeds bestanden kopiëren vanaf uw UPD naar OneDrive voor bedrijven via een browser. 

1. Windows Verkenner naar RemoteApp publiceren en vervolgens instrueren dat gebruikers toegang krijgen tot de bestanden via die app. 
2. Het gemakkelijkst voor overdracht van bestanden als ze zijn gecomprimeerd, zodat gebruikers een ZIP-bestand met alle bestanden verplaatsen naar OneDrive voor bedrijven moeten maken.
3. Gebruikers vragen om gaat u naar de Office 365-portal en gaat u naar OneDrive en upload het ZIP-bestand.

## <a name="copy-files-by-using-drive-redirection"></a>Kopiëren van bestanden met behulp van stationsomleiding
Als u hebt ingeschakeld [station omleiding](remoteapp-redirection.md), u hebt al een toegewezen station gemaakt voor uw gebruikers. In dit geval kunnen ze hun bestanden op de omgeleide schijf zip en slaat u deze op hun lokale PC.

## <a name="how-administrators-can-export-data"></a>Hoe kunnen beheerders gegevens exporteren

Hiermee worden beheerd voor Azure RemoteApp alle gebruikersprofielschijven (UPD exporteren kunt) voor alle collecties binnen een abonnement op Azure Storage met Azure PowerShell-cmdlet Export-AzureRemoteAppUserDisk.  Er is geen mogelijkheid om afzonderlijke UPD selecteren.  Wanneer de PowerShell-opdracht wordt uitgevoerd, wordt elke schijf van de gebruiker is een 50gb in grootte van de vaste schijf en worden geëxporteerd naar Azure storage.  Kosten van Azure storage, onmiddellijk worden voor deze opslag.  Wanneer u deze opdracht uitvoert ervoor te zorgen zijn er geen sessies anders het exporteren mislukt.

UPD de voor lid van domein Azure RemoteApp-implementaties kan alleen opnieuw in een RDS-implementatie worden gebruikt, niet van het domein gekoppelde implementaties kunnen niet worden gebruikt.  Als u deze schijven worden gebruikt in een RDS-implementatie is het raadzaam om te gebruiken onze [geautomatiseerde scripts](https://github.com/arcadiahlyy/aramigration) die wordt exporteren, converteren en importeren van de UPD in een RDS-implementatie.

