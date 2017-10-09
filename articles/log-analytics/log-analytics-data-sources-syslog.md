---
title: aaaCollect en analyseren van Syslog-berichten in OMS Log Analytics | Microsoft Docs
description: Syslog is een gebeurtenis logboekregistratie-protocol die algemene tooLinux. In dit artikel wordt beschreven hoe tooconfigure verzameling van Syslog-berichten in Log Analytics en details van records Hallo ze in Hallo OMS-opslagplaats maken.
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a>Syslog-gegevensbronnen in Log Analytics
Syslog is een gebeurtenis logboekregistratie-protocol die algemene tooLinux.  Toepassingen worden verzonden berichten die kunnen worden opgeslagen op de lokale machine Hallo of tooa Syslog collector geleverd.  Wanneer Hallo OMS-Agent voor Linux is geïnstalleerd, configureert het Hallo lokale Syslog-daemon tooforward berichten toohello agent.  Hallo-agent verzendt vervolgens Hallo-bericht tooLog Analytics waarop een record in Hallo OMS-opslagplaats is gemaakt.  

> [!NOTE]
> Log Analytics biedt ondersteuning voor verzameling van berichten is verzonden door rsyslog of syslog-ng, waarbij rsyslog Hallo standaard daemon is. Hallo standaard syslog-daemon op versie 5 van Red Hat Enterprise Linux en CentOS, Oracle Linux-versie (sysklog) wordt niet ondersteund voor de verzameling van syslog-gebeurtenis. toocollect syslog-gegevens van deze versie van deze verdelingen Hallo [rsyslog daemon](http://rsyslog.com) moet worden geïnstalleerd en geconfigureerd tooreplace sysklog.
>
>

![Syslog-verzameling](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a>Syslog configureren
Hallo OMS-Agent voor Linux worden alleen verzameld van gebeurtenissen met de Hallo opslagruimten en de ernst die zijn opgegeven in de configuratie.  U kunt Syslog configureren via Hallo OMS-portal of met het beheren van configuratiebestanden op uw Linux-agents.

### <a name="configure-syslog-in-hello-oms-portal"></a>Syslog in Hallo OMS-portal configureren
Syslog configureren vanuit Hallo [menu Data in logboekanalyse-instellingen](log-analytics-data-sources.md#configuring-data-sources).  Deze configuratie wordt doorgegeven toohello-configuratiebestand op elke Linux-agent.

U kunt een nieuwe opslagruimte toevoegen door in de naam te typen en op  **+** .  Voor elke faciliteit worden alleen berichten met Hallo geselecteerd ernst verzameld.  Hallo ernstcategorieën voor bepaalde Hallo-opslagruimte die u toocollect wilt controleren.  U kan niet alle aanvullende criteria opgeven toofilter berichten.

![Syslog configureren](media/log-analytics-data-sources-syslog/configure.png)

Standaard zijn alle configuratiewijzigingen tooall agents automatisch gepusht.  Als u tooconfigure Syslog handmatig op elke Linux-agent wilt, schakelt u Hallo vak *toepassen onder configuratie toomy Linux-machines*.

### <a name="configure-syslog-on-linux-agent"></a>Syslog op Linux-agent configureren
Wanneer Hallo [OMS-agent is geïnstalleerd op een client voor Linux](log-analytics-linux-agents.md), het installeren van een standaard syslog-configuratiebestand dat Hallo-faciliteit definieert en ernst van het Hallo-berichten die worden verzameld.  U kunt dit bestand toochange Hallo-configuratie wijzigen.  Hallo-configuratiebestand is verschillend, afhankelijk van Hallo Syslog-daemon die Hallo van client is geïnstalleerd.

> [!NOTE]
> Als u syslog-configuratie Hallo bewerkt, moet u Hallo syslog-daemon voor Hallo wijzigingen tootake effect opnieuw.
>
>

#### <a name="rsyslog"></a>Rsyslog
Hallo-configuratiebestand voor rsyslog bevindt zich op **/etc/rsyslog.d/95-omsagent.conf**.  De Standaardinhoud worden hieronder weergegeven.  Hiermee verzamelt syslog-berichten is verzonden vanaf de lokale agent Hallo voor alle installaties met een niveau van de waarschuwing of hoger.

    kern.warning       @127.0.0.1:25224
    user.warning       @127.0.0.1:25224
    daemon.warning     @127.0.0.1:25224
    auth.warning       @127.0.0.1:25224
    syslog.warning     @127.0.0.1:25224
    uucp.warning       @127.0.0.1:25224
    authpriv.warning   @127.0.0.1:25224
    ftp.warning        @127.0.0.1:25224
    cron.warning       @127.0.0.1:25224
    local0.warning     @127.0.0.1:25224
    local1.warning     @127.0.0.1:25224
    local2.warning     @127.0.0.1:25224
    local3.warning     @127.0.0.1:25224
    local4.warning     @127.0.0.1:25224
    local5.warning     @127.0.0.1:25224
    local6.warning     @127.0.0.1:25224
    local7.warning     @127.0.0.1:25224

U kunt een faciliteit verwijderen door het verwijderen van de sectie van Hallo-configuratiebestand.  Hallo ernst die door het wijzigen van deze faciliteit vermelding voor een bepaalde opslagruimte worden verzameld, kunt u beperken.  Bijvoorbeeld toolimit Hallo gebruiker faciliteit toomessages met een ernst van de fout of hoger wijzigt u deze regel Hallo configuratie bestand toohello te volgen:

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a>Syslog-ng
Hallo-configuratiebestand voor de syslog-ng is de locatie op **/etc/syslog-ng/syslog-ng.conf**.  De Standaardinhoud worden hieronder weergegeven.  Dit verzamelt syslog-berichten is verzonden vanaf de lokale agent Hallo voor alle installaties en alles.   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

U kunt een faciliteit verwijderen door het verwijderen van de sectie van Hallo-configuratiebestand.  Hallo ernst die door deze te verwijderen uit de lijst voor een bepaalde opslagruimte worden verzameld, kunt u beperken.  Bijvoorbeeld: toolimit Hallo gebruiker faciliteit toojust waarschuwingen en kritieke berichten, wijzigt u die sectie van Hallo configuratie bestand toohello te volgen:

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a>Verzamelen van gegevens van aanvullende Syslog-poorten
Hallo OMS-agent luistert naar de Syslog-berichten op de lokale client Hallo op poort 25224.  Wanneer het Hallo-agent is geïnstalleerd, wordt een standaardconfiguratie syslog toegepast en gevonden in Hallo locatie te volgen:

* Rsyslog:`/etc/rsyslog.d/95-omsagent.conf`
* Syslog-ng:`/etc/syslog-ng/syslog-ng.conf`

U kunt Hallo poortnummer wijzigen door het maken van twee configuratiebestanden: een configuratiebestand FluentD en een bestand rsyslog of syslog-ng, afhankelijk van Hallo Syslog-daemon is geïnstalleerd.  

* Hallo FluentD config-bestand moet een nieuw bestand in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` en vervang de waarde in Hallo Hallo **poort** vermelding met het nummer van uw aangepaste poort.

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* Voor rsyslog, moet u een nieuw configuratiebestand in maken: `/etc/rsyslog.d/` en Hallo waarde % SYSLOG_PORT % vervangt door uw aangepast poortnummer.  

    > [!NOTE]
    > Als u deze waarde in het configuratiebestand Hallo wijzigt `95-omsagent.conf`, wordt deze overschreven wanneer Hallo-agent van toepassing een standaardconfiguratie is.
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* Hallo syslog ng config moet worden gewijzigd door te kopiëren Hallo voorbeeldconfiguratie hieronder wordt weergegeven en toe te voegen Hallo aangepaste gewijzigde instellingen toohello einde van Hallo syslog-ng.conf-configuratiebestand te vinden in `/etc/syslog-ng/`.  Doen **niet** standaardlabel hello gebruiken **% WORKSPACE_ID % _oms** of **% WORKSPACE_ID_OMS**, definieert u een aangepast label toohelp onderscheid uw wijzigingen.  

    > [!NOTE]
    > Als u standaardwaarden Hallo in het configuratiebestand Hallo wijzigt, wordt deze overschreven wanneer Hallo-agent van toepassing een standaardconfiguratie is.
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

Na het voltooien van Hallo wijzigingen, Hallo Syslog en Hallo moet OMS-agent-service opnieuw gestart toobe tooensure Hallo configuratie wijzigingen pas van kracht.   

## <a name="syslog-record-properties"></a>Eigenschappen van de record Syslog
Syslog-records hebben een soort **Syslog** en Hallo eigenschappen in de volgende tabel Hallo hebben.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Computer |Computer die gebeurtenis Hallo is verzameld. |
| Opslagruimte |Hiermee definieert u Hallo-onderdeel van het Hallo-systeem dat het Hallo-bericht heeft gegenereerd. |
| HostIP |IP-adres van het Hallo-bericht verzenden Hallo-systeem. |
| Hostnaam |Naam van Hallo Hallo-bericht verzenden. |
| Foutcode |Ernst van gebeurtenis Hallo. |
| SyslogMessage |Tekst van het Hallo-bericht. |
| Proces-id |ID van Hallo-proces dat het Hallo-bericht gegenereerd. |
| eventTime |Datum en tijd waarop Hallo gebeurtenis is gegenereerd. |

## <a name="log-queries-with-syslog-records"></a>Logboek-query's met Syslog-records
Hallo bevat volgende tabel voorbeelden van logboek-query's die Syslog-records ophalen.

| Query’s uitvoeren | Beschrijving |
|:--- |:--- |
| Type = Syslog |Alle Syslogs. |
| Type = Syslog SeverityLevel fout = |Alle Syslog-records met de ernst van de fout. |
| Type = Syslog &#124; meting count() door Computer |Telling van Syslog-records op de computer. |
| Type = Syslog &#124; meting count() door faciliteit |Telling van Syslog-records door de faciliteit. |

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query's toohello volgende wilt wijzigen.

> | Query’s uitvoeren | Beschrijving |
|:--- |:--- |
| Syslog |Alle Syslogs. |
| Syslog &#124; waar foutcode == "error" |Alle Syslog-records met de ernst van de fout. |
| Syslog &#124; overzicht van AggregatedValue = count() door Computer |Telling van Syslog-records op de computer. |
| Syslog &#124; overzicht van AggregatedValue count() door faciliteit = |Telling van Syslog-records door de faciliteit. |

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen.
* Gebruik [aangepaste velden](log-analytics-custom-fields.md) tooparse gegevens van syslog-records in afzonderlijke velden.
* [Linux-agents configureren](log-analytics-linux-agents.md) toocollect andere typen gegevens.
