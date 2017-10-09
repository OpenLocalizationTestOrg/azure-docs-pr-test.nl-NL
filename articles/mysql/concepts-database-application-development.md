---
title: een overzicht voor de ontwikkelaars voor Azure-Database voor MySQL aaaDatabase | Microsoft Docs
description: Overwegingen bij het ontwerpen die een ontwikkelaar volgen moet bij het schrijven van toepassing code tooconnect tooAzure Database voor MySQL introduceert
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a>Overzicht van toepassing voor ontwikkelaars voor Azure-Database voor MySQL 
Dit artikel wordt beschreven ontwerpoverwegingen die een ontwikkelaar volgen moet bij het schrijven van toepassing code tooconnect tooAzure Database voor MySQL 

> [!TIP]
> Zie voor een zelfstudie waarin u hoe toocreate een server, een firewall op de server maken weergeven van de eigenschappen van server, database maken, verbinding maken en query uitvoert met behulp van de workbench en mysql.exe [ontwerpen van uw eerste Azure MySQL-database](tutorial-design-database-using-portal.md)

## <a name="language-and-platform"></a>Taal en platform
Er zijn codevoorbeelden beschikbaar voor verschillende programmeertalen en platforms. Vindt u koppelingen toohello codevoorbeelden op: [bibliotheken voor databaseconnectiviteit tooconnect tooAzure Database gebruikt voor MySQL](concepts-connection-libraries.md)

## <a name="tools"></a>Hulpprogramma's
Azure MySQL-Database maakt gebruik van Hallo MySQL community-versie, compatibel zijn met algemene beheerprogramma's zoals Workbench of MySQL hulpprogramma's zoals mysql.exe, MySQL [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), en andere. U kunt ook hello Azure-portal, Azure CLI en toointeract REST-API's gebruiken met Hallo database-service.

## <a name="resource-limitations"></a>Resourcebeperkingen
Azure MySQL-Database beheert Hallo bronnen beschikbaar tooa server met twee verschillende mechanismen: 
- Beheer van resources 
- Afdwinging van limieten.

## <a name="security"></a>Beveiliging
Azure MySQL-Database bevat bronnen voor beperkende toegang, beschermen gegevens configureren gebruikers en rol en bewaking van activiteiten in een MySQL-Database.

## <a name="authentication"></a>Authentication
Azure MySQL-Database biedt ondersteuning voor server-verificatie van gebruikers en aanmeldingen.

## <a name="resiliency"></a>Flexibiliteit
Wanneer een tijdelijke fout optreedt tijdens het verbinden van tooMySQL Database, moet uw code Hallo-aanroep in opnieuw proberen. Het is raadzaam Hallo opnieuw logica gebruik uit logica, zodat deze biedt Hallo SQL-Database niet overbelast met meerdere clients tegelijkertijd opnieuw uit te voeren.

- Codevoorbeelden: codevoorbeelden die aangeven Pogingslogica, vindt u voorbeelden voor de taal van uw keuze op Hallo: [bibliotheken voor databaseconnectiviteit tooconnect tooAzure Database gebruikt voor MySQL](concepts-connection-libraries.md)

## <a name="managing-connections"></a>Verbindingen beheren
Databaseverbindingen zijn een beperkte resource daarom logisch verbindingen worden gebruikt aangeraden bij het openen van uw MySQL-Database tooachieve betere prestaties.
- Access Hallo-database met behulp van verbindingsgroepering of permanente verbindingen.
- Met behulp van de levensduur van een korte verbinding Access Hallo-database. 
- Pogingslogica voor gebruik in uw toepassing bij de verbindingspoging hello, toocatch fouten vanwege tooconcurrent verbindingen Hallo Hallo maximale toegestane bereikt. In Hallo Pogingslogica, een korte vertraging instellen en vervolgens wachten op een willekeurige tijd voordat de aanvullende verbindingspogingen Hallo.
