---
title: aaaUnderstand en los WebHCat fouten op HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe tooabout veelvoorkomende fouten geretourneerd door WebHCat in HDInsight en hoe tooresolve ze.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a>Begrijpen en oplossen van fouten die zijn ontvangen van WebHCat in HDInsight

Meer informatie over fouten die zijn ontvangen bij het gebruik van WebHCat met HDInsight en hoe tooresolve ze. WebHCat wordt intern gebruikt door de client-side '-hulpprogramma's zoals Azure PowerShell en Hallo Data Lake Tools voor Visual Studio.

## <a name="what-is-webhcat"></a>Wat is WebHCat

[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is een REST-API voor [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), een tabel en storage management-laag voor Hadoop. WebHCat is standaard ingeschakeld op HDInsight-clusters en wordt gebruikt door verschillende hulpprogramma's voor toosubmit taken, kunt u de status van taak, enz. zonder logboekregistratie in toohello cluster.

## <a name="modifying-configuration"></a>Configuratie wijzigen

> [!IMPORTANT]
> Aantal Hallo fouten die in dit document optreden als een geconfigureerde maximum is overschreden. Wanneer Hallo resolutie stap u kunt een waarde wijzigen noemt, moet u een Hallo na wijziging van tooperform hello gebruiken:

* Voor **Windows** clusters: een script tooconfigure Hallo actiewaarde gebruiken tijdens het maken van het cluster. Zie voor meer informatie [ontwikkelen scriptacties](hdinsight-hadoop-script-actions.md).

* Voor **Linux** clusters: gebruik Ambari (web of REST-API) toomodify Hallo waarde. Zie voor meer informatie [beheren HDInsight met Ambari](hdinsight-hadoop-manage-ambari.md)

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

### <a name="default-configuration"></a>Standaardconfiguratie

Als Hallo na standaardwaarden zijn overschreden, kan deze WebHCat prestaties verslechteren of er fouten optreden:

| Instelling | Wat het doet | Standaardwaarde |
| --- | --- | --- |
| [yarn.scheduler.Capacity.maximum-toepassingen][maximum-applications] |maximum aantal taken dat gelijktijdig actief kunnen zijn Hallo (in behandeling of wordt uitgevoerd) |10.000 |
| [templeton.Exec.Max-processor][max-procs] |Hallo kunt u het maximum aantal aanvragen dat gelijktijdig kunnen worden geleverd |20 |
| [mapreduce.jobhistory.Max-leeftijd-ms][max-age-ms] |het aantal dagen dat de taakgeschiedenis Hallo blijven behouden |7 dagen |

## <a name="too-many-requests"></a>Te veel aanvragen

**HTTP-statuscode**: 429

| Oorzaak | Oplossing |
| --- | --- |
| Hallo maximum aantal gelijktijdige aanvragen afgehandeld door WebHCat per minuut (standaard 20) is overschreden |Uw werkbelasting tooensure dat u niet verzenden van meer dan Hallo maximum aantal gelijktijdige aanvragen of Hallo gelijktijdige aanvraaglimiet door het wijzigen van verhogen verminderen `templeton.exec.max-procs`. Zie voor meer informatie [configuratie wijzigen](#modifying-configuration) |

## <a name="server-unavailable"></a>Server niet beschikbaar

**HTTP-statuscode**: 503

| Oorzaak | Oplossing |
| --- | --- |
| Deze statuscode treedt meestal op tijdens de failover tussen Hallo primaire en secundaire HeadNode voor Hallo-cluster |Wacht twee minuten en probeer opnieuw Hallo |

## <a name="bad-request-content-could-not-find-job"></a>Onjuiste aanvraag inhoud: kan de taak niet vinden.

**HTTP-statuscode**: 400

| Oorzaak | Oplossing |
| --- | --- |
| Taakdetails zijn opgeschoond door Hallo Taakgeschiedenis schoner |bewaartermijn voor Taakgeschiedenis Hallo is 7 dagen. Hallo bewaartermijn kan worden gewijzigd door het wijzigen van `mapreduce.jobhistory.max-age-ms`. Zie voor meer informatie [configuratie wijzigen](#modifying-configuration) |
| Taak is afgebroken vanwege tooa failover |Verzending van de taak voor up tootwo minuten opnieuw proberen |
| Er is een ongeldige taak-id gebruikt |Controleer als Hallo taak-id juist is |

## <a name="bad-gateway"></a>Ongeldige gateway

**HTTP-statuscode**: 502

| Oorzaak | Oplossing |
| --- | --- |
| Interne garbagecollection plaatsvindt binnen Hallo WebHCat-proces |Wacht totdat garbagecollection verzameling toofinish of Hallo WebHCat-service opnieuw starten |
| Time-out opgetreden bij het wachten op een reactie van Hallo ResourceManager service. Deze fout kan optreden wanneer het aantal actieve toepassingen Hallo maximum Hallo geconfigureerd (standaard 10.000 gaat) |Wachten tot taken toocomplete momenteel wordt uitgevoerd of Hallo gelijktijdige taaklimiet verhogen door het wijzigen van `yarn.scheduler.capacity.maximum-applications`. Zie voor meer informatie, Hallo [wijzigen configuratie](#modifying-configuration) sectie. |
| Poging tooretrieve alle taken via Hallo [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) aanroep bij `Fields` te is ingesteld`*` |Geen opgehaald *alle* taakgegevens. Gebruik in plaats daarvan `jobid` tooretrieve details voor taken alleen groter is dan een bepaalde taak-id. Of gebruik geen`Fields` |
| Hallo WebHCat-service is niet actief tijdens de failover HeadNode |Wacht twee minuten en probeer Hallo opnieuw |
| Er zijn meer dan 500 in behandeling zijnde taken die worden verzonden via WebHCat |Wacht totdat het momenteel in behandeling zijnde taken vóór het verzenden van meer taken zijn voltooid |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
