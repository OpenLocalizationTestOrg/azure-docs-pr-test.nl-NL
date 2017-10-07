---
title: aaaCollect Nagios en Zabbix waarschuwingen in OMS Log Analytics | Microsoft Docs
description: Nagios en Zabbix zijn open-source hulpprogramma's voor controle. U kunt verzamelen waarschuwingen van deze hulpprogramma's in logboekanalyse in volgorde tooanalyze ze samen met waarschuwingen uit andere bronnen.  Dit artikel wordt beschreven hoe tooconfigure Hallo OMS-Agent voor Linux toocollect waarschuwingen uit deze systemen.
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a>Waarschuwingen verzamelen van Nagios en Zabbix in logboekanalyse van OMS-Agent voor Linux 
[Nagios](https://www.nagios.org/) en [Zabbix](http://www.zabbix.com/) open-source hulpprogramma's voor controle zijn.  U kunt verzamelen waarschuwingen van deze hulpprogramma's in logboekanalyse in volgorde tooanalyze ze samen met [waarschuwingen uit andere bronnen](log-analytics-alerts.md).  Dit artikel wordt beschreven hoe tooconfigure Hallo OMS-Agent voor Linux toocollect waarschuwingen uit deze systemen.
 
## <a name="configure-alert-collection"></a>Verzamelen van waarschuwingen configureren

### <a name="configuring-nagios-alert-collection"></a>Nagios verzamelen van waarschuwingen configureren
Hallo volgende stappen uit op waarschuwingen toocollect hello Nagios-servers uitvoeren.

1. Verleen Hallo gebruiker **omsagent** leestoegang toohello Nagios-logboekbestand (dat wil zeggen `/var/log/nagios/nagios.log`). Ervan uitgaande dat Hallo nagios.log bestand eigendom is van de groep Hallo `nagios`, kunt u Hallo gebruiker toevoegen **omsagent** toohello **nagios** groep. 

    sudo usermod - a -G nagios omsagent

2.  Hallo-configuratiebestand op wijzigen (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Zorg ervoor Hallo volgende vermeldingen zijn aanwezig en niet opmerkingen uit:  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. Hallo omsagent daemon starten

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a>Zabbix verzamelen van waarschuwingen configureren
toocollect waarschuwingen van een Zabbix-server, moet u een gebruiker toospecify en het wachtwoord in *leesbare tekst*. Dit is niet ideaal, maar we raden u Hallo-gebruiker maken en verlenen van machtigingen toomonitor onlu.

Hallo volgende stappen uit op waarschuwingen toocollect hello Nagios-servers uitvoeren.

1. Hallo-configuratiebestand op wijzigen (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`). Zorg ervoor Hallo volgende vermeldingen zijn aanwezig en niet opmerkingen uit.  Hallo gebruiker naam en het wachtwoord toovalues voor uw omgeving Zabbix wijzigen.

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. Hallo omsagent daemon starten

    sudo servicel /opt/microsoft/omsagent/bin/service_control opnieuw starten


## <a name="alert-records"></a>Waarschuwing records
U kunt waarschuwingen records ophalen uit Nagios en Zabbix met [Meld zoekopdrachten](log-analytics-log-searches.md) in logboekanalyse.

### <a name="nagios-alert-records"></a>Waarschuwing Nagios records

Waarschuwing die is verzameld door Nagios-records hebben een **Type** van **waarschuwing** en een **SourceSystem** van **Nagios**.  Ze hebben Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Type |*Een waarschuwing* |
| SourceSystem |*Nagios* |
| AlertName |Naam van het Hallo-waarschuwing. |
| AlertDescription | Beschrijving van waarschuwing Hallo. |
| AlertState | Status van het Hallo-service of de host.<br><br>OK<br>WAARSCHUWING<br>OMHOOG<br>OMLAAG |
| Hostnaam | Naam van het Hallo-host die Hallo waarschuwing gemaakt. |
| PriorityNumber | Het prioriteitsniveau van Hallo waarschuwing. |
| StateType | Hallo-type van de status van waarschuwing Hallo.<br><br>SOFT - probleem dat niet opnieuw is gecontroleerd.<br>HARDE - probleem dat is een opgegeven aantal keren opnieuw gecontroleerd.  |
| TimeGenerated |Datum en tijd Hallo waarschuwing is gemaakt. |


### <a name="zabbix-alert-records"></a>Waarschuwing Zabbix-records
Waarschuwing die is verzameld door Zabbix-records hebben een **Type** van **waarschuwing** en een **SourceSystem** van **Zabbix**.  Ze hebben Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Type |*Een waarschuwing* |
| SourceSystem |*Zabbix* |
| AlertName | Naam van het Hallo-waarschuwing. |
| AlertPriority | Ernst van waarschuwing Hallo.<br><br>niet geclassificeerd<br>Informatie<br>Waarschuwing<br>Gemiddelde<br>Hoog<br>noodherstel  |
| AlertState | De status van waarschuwing Hallo.<br><br>0 - status is maximaal toodate.<br>1 - status is onbekend.  |
| AlertTypeNumber | Hiermee geeft u op of in een waarschuwing meerdere gebeurtenissen van het probleem kan worden gegenereerd.<br><br>0 - status is maximaal toodate.<br>1 - status is onbekend.    |
| Opmerkingen | Aanvullende opmerkingen voor waarschuwing. |
| Hostnaam | Naam van het Hallo-host die Hallo waarschuwing gemaakt. |
| PriorityNumber | Waarde die aangeeft ernst van waarschuwing Hallo.<br><br>0 - niet geclassificeerd<br>1 - informatie<br>2 - waarschuwing<br>3 - gemiddelde<br>4 - hoog<br>5 - noodherstel |
| TimeGenerated |Datum en tijd Hallo waarschuwing is gemaakt. |
| TimeLastModified |Datum en tijd Hallo-status van waarschuwing Hallo het laatst is gewijzigd. |


## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [waarschuwingen](log-analytics-alerts.md) in logboekanalyse.
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen. 
