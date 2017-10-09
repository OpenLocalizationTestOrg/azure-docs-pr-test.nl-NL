---
title: Azure Database aaaServer zich aanmeldt voor PostgreSQL | Microsoft Docs
description: Query's en fout-Logboeken in Azure-Database voor PostgreSQL genereert.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 22575f3882ce67fe640952f0a8dbfd8dcb4b16fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Serverlogboekbestanden in Azure-Database voor PostgreSQL 
Azure-Database voor PostgreSQL query en de fout genereert logboeken. Tootransaction toegangslogboeken wordt echter niet ondersteund. Deze logboeken worden gebruikte tooidentify, oplossen en herstellen van fouten in de configuratie en suboptimale prestaties. Zie voor meer informatie [foutrapportage en de logboekregistratie](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html).

## <a name="access-server-logs"></a>Access server-Logboeken
Kunt u de lijst en downloaden van server-foutlogboeken Azure PostgreSQL hello Azure-Portal met [Azure CLI](howto-configure-server-logs-using-cli.md) en Azure REST-API's.

## <a name="log-retention"></a>Logboek bewaren
U kunt instellen Hallo bewaarperiode voor het systeemlogboek in Logboeken met behulp van de **logboek\_bewaren\_periode** parameter die is gekoppeld aan uw server. Hallo-eenheid op voor deze parameter is dagen (tooconfirm nodig). de standaardwaarde Hallo is drie dagen. Hallo maximumwaarde is 7 dagen. Houd er rekening mee dat de server voldoende logboekbestanden toegewezen opslag toocontain Hallo bewaard moet hebben.
Hallo-logboekbestanden draait elke 1 uur of de grootte van 100MB, afhankelijk van wat zich het eerste voordoet.

## <a name="configure-logging-for-azure-postgresql-server"></a>Logboekregistratie voor Azure PostgreSQL-server configureren
U kunt queryregistratie en foutenregistratie inschakelen voor uw server. Foutenlogboeken kunnen automatisch onderdruk, de verbinding en de controlepunten informatie bevatten.

U kunt queryregistratie voor uw PostgreSQL-database-exemplaar inschakelen door het instellen van de twee serverparameters: logboek\_-instructie en logboekbestanden\_min\_duur\_instructie.

Hallo **logboek\_instructie** parameter bepaalt welke SQL-instructies worden geregistreerd. Het is raadzaam als deze parameter te***alle*** toolog alle instructies; Hallo standaardwaarde is geen (moet tooconfirm).

Hallo **logboek\_min\_duur\_instructie** parametersets Hallo limiet in milliseconden van een instructie toobe in het logboek geregistreerd. Alle SQL-instructies die langer dan de instelling van de parameter Hallo uitgevoerd worden geregistreerd. Deze parameter is uitgeschakeld en stel toominus 1 (-1) standaard (tooconfirm nodig). Inschakelen van deze parameter is handig bij het volgen van niet-geoptimaliseerde query's in uw toepassingen.

Hallo **logboek\_min\_berichten** kunt u toocontrol welke Berichtniveaus toohello server logboekbestand worden geschreven. Hallo standaard is een waarschuwing. (moet tooconfirm)

Zie voor meer informatie over deze instellingen [foutrapportage en de logboekregistratie](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) documentatie. Zie voor vooral Azure-Database configureren voor parameters van de server PostgreSQL, [Server-logboeken in Azure-Database voor PostgreSQL](concepts-server-logs.md).

## <a name="next-steps"></a>Volgende stappen
- tooaccess logboeken met Azure CLI-opdrachtregelinterface, Zie [configureren en access server-logboeken met Azure CLI](howto-configure-server-logs-using-cli.md)
- Zie voor meer informatie over parameters van de server [aanpassen configuratieparameters server met Azure CLI](howto-configure-server-parameters-using-cli.md).