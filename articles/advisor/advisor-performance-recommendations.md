---
title: aaaAzure Advisor prestaties aanbevelingen | Microsoft Docs
description: Gebruik Advisor toooptimize Hallo prestaties van uw Azure-implementaties.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a>Aanbevelingen van Advisor-prestaties

Azure aanbevelingen van Advisor prestaties worden verbeterd Hallo en reactiesnelheid van uw bedrijfskritieke toepassingen. Aanbevelingen voor prestaties kunt u krijgen via Advisor op Hallo **prestaties** van Hallo Advisor dashboard.

![Tabblad van Advisor-prestaties](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a>Verbeteren de databaseprestaties met SQL database Advisor

Advisor biedt een consistente, geconsolideerde weergave van aanbevelingen voor alle Azure-resources. Het is geïntegreerd met SQL Database Advisor toobring u aanbevelingen voor het verbeteren van Hallo prestaties van uw Azure SQL database. SQL Database Advisor beoordeelt Hallo prestaties van uw Azure SQL-database door een analyse van uw gebruiksgeschiedenis. Vervolgens biedt aanbevelingen die geschikt zijn voor het uitvoeren van de normale werkbelasting Hallo-database. 

> [!NOTE]
> tooget aanbevelingen, moet een database over een week van het gebruik van, en binnen een week moet er een consistente activiteit. SQL Database Advisor kunt eenvoudiger voor consistente querypatronen dan voor willekeurige lichtflitsen activiteit optimaliseren.

Zie voor meer informatie over SQL Database Advisor [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).

![Aanbevelingen voor SQL-database](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a>De Redis-Cache-prestaties en betrouwbaarheid verbeteren

Advisor identificeert exemplaren van Redis-Cache waarbij prestaties mogelijk negatief beïnvloed door hoog geheugengebruik, serverbelasting, bandbreedte van het netwerk of een groot aantal clientverbindingen. Advisor biedt ook best practices aanbevelingen toohelp u potentiële problemen voorkomen. Zie voor meer informatie over Redis-Cache aanbevelingen [Redis-Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).


## <a name="improve-app-service-performance-and-reliability"></a>App Service-prestaties en betrouwbaarheid te verbeteren

Azure Advisor kan worden geïntegreerd met aanbevelingen voor uw App Services-ervaring te verbeteren en relevante platformmogelijkheden detecteren. Voorbeelden van App Services aanbevelingen zijn:
* Detectie van exemplaren waar het geheugen of CPU-bronnen zijn uitgeput door app runtimes met risicobeperking opties.
* Detectie van exemplaren waar collocating resources, zoals web-apps en -databases kan de prestaties en lagere kosten verbeteren. 

Zie voor meer informatie over App-Services aanbevelingen [aanbevolen procedures voor het Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).
![Aanbevelingen voor App-Services](./media/advisor-performance-recommendations/advisor-performance-app-service.png)

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a>Hoe tooaccess prestaties aanbevelingen in Advisor

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Klik in het linkerdeelvenster Hallo **meer services**.

3. Service in Hallo menu deelvenster onder **bewaking en beheer**, klikt u op **Azure Advisor**.  
 Hallo Advisor dashboard wordt weergegeven.

4. Klik op Hallo Advisor dashboard Hallo **prestaties** tabblad.

5. Selecteer Hallo abonnement waarvoor u wilt dat tooreceive aanbevelingen en klik vervolgens op **aanbevelingen krijgen**.

> [!NOTE]
> tooaccess aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor. Een abonnement is geregistreerd als een *abonnement eigenaar* gestart Hallo dashboard en klikt op Hallo van Advisor **aanbevelingen krijgen** knop. Dit is een *eenmalige bewerking*. Nadat het Hallo-abonnement is geregistreerd, kunt u Advisor aanbevelingen als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, een resourcegroep of een bepaalde resource.

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over de aanbevelingen van Advisor, Zie:

* [Inleiding tooAdvisor](advisor-overview.md)
* [Aan de slag met Advisor](advisor-get-started.md)
* [Advisor kosten aanbevelingen](advisor-performance-recommendations.md)
* [Hoge beschikbaarheid aanbevelingen Advisor te ontvangen](advisor-high-availability-recommendations.md)
* [Aanbevelingen voor beveiliging van Advisor](advisor-security-recommendations.md)

