---
title: aaaSQL Data Warehouse downlevel-clients ondersteuning voor gegevens controle | Microsoft Docs
description: Meer informatie over SQL Data Warehouse-ondersteuning voor downlevel-clients voor het controleren van gegevens
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a>Ondersteuning voor SQL datawarehouse - Downlevel-clients voor controle en dynamische Gegevensmaskering
[Controle](sql-data-warehouse-auditing-overview.md) werkt met SQL-clients die ondersteuning bieden voor omleiden van TDS.

Omleiding moet ook ondersteuning voor elke client waarmee de TDS-7.4 wordt geïmplementeerd. Uitzonderingen toothis omvatten JDBC 4.0 in welke functie u Hallo omleiding wordt niet volledig ondersteund en Tedious voor Node.JS waarin omleiding niet is geïmplementeerd.

Voor 'Downlevel-clients', moeten dat wil zeggen dat TDS-versie 7.3 ondersteunen en hieronder - FQDN van de server in de verbindingsreeks Hallo Hallo worden gewijzigd:

Oorspronkelijke server FQDN-naam in de verbindingsreeks Hallo: <*servernaam*>. database.windows.net

Gewijzigde FQDN van de server in de verbindingsreeks Hallo: <*servernaam*> .database. **beveiligde**. windows.net

Een gedeeltelijke lijst met 'Downlevel-clients' omvat:

* .NET 4.0 en lager,
* ODBC-10.0 en lager.
* JDBC (Hoewel JDBC TDS 7.4, Hallo TDS-omleiding functie wordt niet volledig ondersteund ondersteunt)
* Omslachtig (voor Node.JS)

**Opmerking:** Hallo hierboven server FDQN wijziging mogelijk van pas ook voor het toepassen van een beleid voor controle van SQL Server op zonder behoefte aan een configuratie stap in elke database (tijdelijke risicobeperking).     

