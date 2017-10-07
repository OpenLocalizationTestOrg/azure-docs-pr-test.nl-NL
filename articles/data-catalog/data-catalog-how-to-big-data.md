---
title: aaaHow toowork met gegevensbronnen 'big data' | Microsoft Docs
description: Hoe tooarticle markeren patronen voor het gebruik van Azure Data Catalog met 'big data' gegevensbronnen, waaronder Azure Blob Storage, Azure Data Lake en Hadoop HDFS.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a>Hoe toowork met big data in Azure Data Catalog gegevensbronnen
## <a name="introduction"></a>Inleiding
**Microsoft Azure Data Catalog** is een volledig beheerde cloudservice die als een systeem van registratie en systeem van detectie voor zakelijke gegevensbronnen fungeert. Het is over medewerkers detecteren, begrijpen en gebruiken van gegevensbronnen helpen en helpt organisaties tooget meerwaarde van hun bestaande gegevensbronnen, met inbegrip van big data.

**Azure Data Catalog** ondersteunt Hallo registratie van Azure Blog van Storage-blobs en mappen alsook Hadoop HDFS-bestanden en mappen. Hallo semi-gestructureerde aard van deze gegevensbronnen biedt hoge mate van flexibiliteit. Echter tooget optimaal zich kunnen registreren met Hallo **Azure Data Catalog**, gebruikers moeten rekening houden met het Hallo-gegevensbronnen worden ingedeeld.

## <a name="directories-as-logical-data-sets"></a>Mappen als logische gegevenssets
Een algemene patroon voor het ordenen van grote gegevensbronnen is tootreat mappen als logische gegevenssets. Op het hoogste niveau mappen zijn gebruikte toodefine een gegevensset terwijl submappen Definieer partities en Hallo-bestanden die ze bevatten opslaan Hallo gegevens zelf.

Een voorbeeld van dit patroon is mogelijk:

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

In dit voorbeeld vertegenwoordigen vehicle_maintenance_events en location_tracking_events logische gegevenssets. Elk van deze mappen bevat gegevensbestanden die zijn ingedeeld op jaar en maand in submappen. Elk van deze mappen zich mogelijk honderden of duizenden bestanden.

In dit patroon registratie van afzonderlijke bestanden met **Azure Data Catalog** waarschijnlijk niet logisch. In plaats daarvan registreert Hallo-mappen die Hallo gegevenssets die worden zinvolle toohello gebruikers werken met gegevens Hallo vertegenwoordigen.

## <a name="reference-data-files"></a>Verwijzing naar gegevensbestanden
Een aanvullende patroon is sets van verwijzingsgegevens toostore als afzonderlijke bestanden. Deze gegevenssets kunnen worden beschouwd als 'kleine' Hallo-zijde van big data en zijn vaak vergelijkbare toodimensions in een model analytische gegevens. Verwijzing naar gegevensbestanden bevatten records die gebruikt tooprovide context voor bulksgewijs Hallo van gegevensbestanden Hallo elders in Hallo big data-archief opgeslagen zijn.

Een voorbeeld van dit patroon is mogelijk:

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

Wanneer een analist of gegevens wetenschappelijk met gegevens in grotere mapstructuren Hallo hello werkt, kunnen Hallo-gegevens in deze bestanden verwijzing gebruikte tooprovide meer informatie gedetailleerde voor entiteiten die zijn bedoeld tooonly op naam of ID in grotere Hallo-gegevens worden set.

In dit patroon is het zinvol tooregister Hallo afzonderlijke verwijzing gegevensbestanden met **Azure Data Catalog**. Elk bestand vertegenwoordigt een set gegevens en elkaar kan worden aangetekend en afzonderlijk gedetecteerd.

## <a name="alternate-patterns"></a>Alternatieve patronen
Hallo patronen die zijn beschreven in voorgaande sectie Hallo zijn twee manieren die een big data store kan worden georganiseerd, maar elke implementatie verschilt. Ongeacht hoe uw gegevensbronnen zijn gestructureerd, bij het registreren van gegevensbronnen met big **Azure Data Catalog**, ligt de nadruk op het registreren van Hallo bestanden en mappen die vertegenwoordigen gegevenssets Hallo van waarde tooothers binnen uw de organisatie. Registratie van alle bestanden en mappen kan bruikbaar blijft Hallo-catalogus, waardoor het moeilijker voor gebruikers toofind die ze nodig hebben.

## <a name="summary"></a>Samenvatting
Registreren van gegevensbronnen met **Azure Data Catalog** maakt u ze eenvoudiger toodiscover en begrijpen. Door te registreren en aantekeningen Hallo big data-bestanden en mappen die logische gegevenssets vertegenwoordigen, kunt u gebruikers zoeken en Hallo big-gegevensbronnen die ze nodig hebben.
