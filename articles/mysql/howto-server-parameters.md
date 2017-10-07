---
title: aaaHow tooConfigure Parameters van de Server in Azure-Database voor MySQL | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooconfigure beschikbare parameters van de server in Azure-Database voor het gebruik van MySQL hello Azure-portal.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 8292c8eda605854a06b6a9c82185c857bd353cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-server-parameters-in-azure-database-for-mysql-using-hello-azure-portal"></a>Hoe tooconfigure parameters van de server in Azure-Database voor het gebruik van MySQL hello Azure-portal

Azure MySQL-Database ondersteunt de configuratie van bepaalde parameters van de server. Dit artikel wordt beschreven hoe tooconfigure deze parameters met hello Azure-portal en lijsten Hallo ondersteund parameters, Hallo standaardwaarden en Hallo bereik van geldige waarden. Niet alle parameters van de server kunnen worden aangepast. Alleen Hallo hier vermeld die worden ondersteund.

## <a name="navigate-tooserver-parameters-blade-on-azure-portal"></a>Navigeer tooServer Parameters blade in Azure portal

Meld u bij toohello Azure-portal en klik vervolgens op uw Azure-Database voor de naam van de MySQL-server. Onder Hallo **instellingen** sectie, klikt u op **serverparameters** tooopen Hallo parameters serverblade voor hello Azure voor MySQL-Database.

![De blade parameters Azure portal-server](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>Lijst met parameters van de server worden geconfigureerd

Hallo volgende tabel geeft een lijst serverparameters Hallo momenteel niet ondersteund. Hallo-parameters kunnen worden geconfigureerd volgens tooyour toepassingsvereisten.

> [!div class="mx-tableFixed"]
|Parameternaam|Standaardwaarde|bereik|Beschrijving|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11-1000000|Bepaalt Hallo hoeveel microseconden binair logboek commit wacht voordat het Hallo binair logboek bestand toodisk synchroniseren.|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|Hallo maximumaantal transacties toowait voor vóór de huidige vertraging Hallo zoals opgegeven door binlog-groep-doorvoeren-sync-vertraging wordt afgebroken.|
|character_set_server|LATIN1|BIG5, UTF8MB4, enzovoort.|Gebruik charset_name als Hallo server standaardtekenset.|
|div_precision_increment|4|0-30|Het aantal cijfers door welke schaal tooincrease Hallo Hallo resultaat van de deling-bewerkingen.|
|group_concat_max_len|1024|4-16777216|Maximaal toegestane lengte in bytes voor Hallo GROUP_CONCAT().|
|innodb_adaptive_hash_index|AAN|UITGESCHAKELD|Hiermee wordt aangegeven of innodb adaptieve hash-indexen zijn ingeschakeld of uitgeschakeld.|
|innodb_lock_wait_timeout|50|1-3600|Hallo tijdsduur in seconden een transactie InnoDB wordt gewacht op een vergrendeling rij voordat geeft.|
|interactive_timeout|1800|10-1800|Het aantal seconden Hallo server wacht voor activiteiten in een interactieve verbinding voordat u deze sluit.|
|log_bin_trust_function_creators|UIT|UITGESCHAKELD|Deze variabele is van toepassing als binaire logboekregistratie is ingeschakeld. Dit bepaalt of opgeslagen functie auteurs kunnen worden niet opgeslagen toocreate-functies die ertoe leiden onveilige gebeurtenissen toobe toohello binair logboek geschreven dat vertrouwd.|
|log_queries_not_using_indexes|UIT|UITGESCHAKELD|Logboeken-query's die zijn verwacht tooretrieve alle rijen tooslow query-logboek.|
|log_slow_admin_statements|UIT|UITGESCHAKELD|Neem trage beheerdersrechten instructies in Hallo instructies toohello trage querylogboek geschreven.|
|log_throttle_queries_not_using_indexes|0|0-4294967295|Limieten Hallo aantal dergelijke query's per minuut dat toohello trage query-logboek kan worden geschreven.|
|long_query_time|10|1 1E + 100|Als een query langer dan dit aantal seconden duurt, verhoogt Hallo server Hallo Slow_queries status variabele.|
|max_allowed_packet|536870912|1024-1073741824|Hallo maximale grootte van een pakket of een willekeurige tekenreeks gegenereerd/tussenliggende of elke parameter die is verzonden door Hallo mysql_stmt_send_long_data() C-API-functie.|
|min_examined_row_limit|0|0-18446744073709551615|Logboekregistratie van query's die groter dan het aantal rijen in de trage querylogboek Hallo Hallo geconfigureerd. |
|server_id|3293747068|1000-4294967295|Hallo-ID, gebruikt in replicatie toogive elk master en server slave een unieke identiteit.|
|slave_net_timeout|60|30-3600|het aantal seconden toowait voor meer gegevens van Hallo master voordat Hallo slave Hallo-verbinding is verbroken, beschouwt Hallo Hallo lezen afgebroken en tooreconnect probeert.|
|slow_query_log|UIT|UITGESCHAKELD|In- of uitschakelen van de trage querylogboek Hallo.|
|sql_mode|0 geselecteerd|ALLOW_INVALID_DATES, IGNORE_SPACE, enzovoort.|Hallo huidige SQL servermodus.|
|time_zone|SYSTEEM|Voorbeelden:-8: 00, +05: 30|Hallo servertijdzone.|
|wait_timeout|120|60-240|het aantal seconden Hallo server Hallo wacht voor activiteiten in een niet-interactieve verbinding voordat u deze sluit.|

## <a name="next-steps"></a>Volgende stappen
- [Verbindingsbibliotheken voor Azure-Database voor MySQL](concepts-connection-libraries.md)
