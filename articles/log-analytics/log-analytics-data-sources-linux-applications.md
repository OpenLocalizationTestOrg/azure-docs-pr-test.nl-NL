---
title: aaaCollect Linux toepassingsprestaties in OMS Log Analytics | Microsoft Docs
description: Dit artikel bevat informatie voor het configureren van Hallo OMS-Agent voor Linux toocollect prestatiemeteritems voor MySQL en Apache HTTP-Server.
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
ms.openlocfilehash: 51105c6add5c7941a004570a76a4d94c02fc8a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a>Verzamelen van prestatiemeteritems voor Linux-toepassingen in Log Analytics 
Dit artikel bevat informatie voor het configureren van Hallo [OMS-Agent voor Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect prestatiemeteritems voor specifieke toepassingen.  Hallo-toepassingen die zijn opgenomen in dit artikel zijn:  

- [MySQL](#MySQL)
- [Apache HTTP-Server](#apache-http-server)

## <a name="mysql"></a>MySQL
Als MySQL-Server of MariaDB Server wordt gedetecteerd op de computer Hallo wanneer Hallo OMS-agent is geïnstalleerd, wordt een provider voor de MySQL-Server voor prestatiebewaking automatisch geïnstalleerd. Deze provider verbindt toohello lokale MySQL/MariaDB server tooexpose prestatiestatistieken weer. MySQL-gebruikersreferenties moeten worden geconfigureerd zodat hello provider toegang heeft tot Hallo MySQL-Server.

### <a name="configure-mysql-credentials"></a>MySQL-referenties configureren
Hallo MySQL OMI provider moet de gebruiker vooraf geconfigureerde MySQL en MySQL-clientbibliotheken geïnstalleerd in volgorde tooquery Hallo prestatie- en statusgegevens van Hallo MySQL-exemplaar.  Deze referenties worden opgeslagen in een verificatiebestand dat opgeslagen op Hallo Linux-agent.  Hallo verificatiebestand geeft aan welke bind-adres en poort Hallo MySQL exemplaar luistert en wat referenties toouse toogather metrische gegevens.  

Tijdens de installatie van Hallo OMS-Agent voor Linux Hallo MySQL OMI scant provider MySQL my.cnf configuratiebestanden (standaardlocaties) voor bind-adres en poort en gedeeltelijk set Hallo verificatiebestand MySQL OMI.

Hallo MySQL verificatie-bestand is opgeslagen op `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.


### <a name="authentication-file-format"></a>Verificatie-bestandsindeling
Hieronder vindt u Hallo-indeling voor Hallo MySQL OMI verificatiebestand

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

Hallo-vermeldingen in Hallo verificatiebestand worden beschreven in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--|:--|
| Poort | Hallo huidige poort Hallo MySQL exemplaar luistert op vertegenwoordigt. Poort 0 geeft aan dat na Hallo-eigenschappen worden gebruikt voor het standaardexemplaar. |
| BIND-adres| Huidige MySQL bind-adres. |
| gebruikersnaam| MySQL-gebruiker gebruikt toouse toomonitor Hallo MySQL server-exemplaar. |
| Base64-gecodeerd wachtwoord| Wachtwoord van Hallo MySQL bewaking gebruiker gecodeerd in Base64. |
| Automatisch bijwerken| Hiermee geeft u op of toorescan voor in Hallo my.cnf bestand wijzigingen en de Hallo MySQL OMI verificatiebestand overschrijven wanneer hello MySQL OMI Provider is bijgewerkt. |

### <a name="default-instance"></a>Standaard-instantie
Hallo MySQL OMI verificatiebestand kunt definiëren een standaardexemplaar en poort nummer toomake meerdere MySQL-exemplaren op een Linux-host eenvoudiger beheren.  Hallo-standaardexemplaar wordt aangeduid door een instantie met poort 0. Alle extra exemplaren worden overgenomen eigenschappen instellen van het standaardexemplaar hello, tenzij ze verschillende waarden opgeven. Bijvoorbeeld als MySQL exemplaar luisteren op poort '3308' wordt toegevoegd, Hallo standaardexemplaar bind-adres, gebruikersnaam en wachtwoord Base64-gecodeerd wordt gebruikte tootry worden en Hallo exemplaar luistert op 3308 bewaken. Hallo-exemplaar op 3308 is gebonden tooanother adres en maakt gebruik van Hallo dezelfde MySQL-gebruikersnaam en wachtwoord paar alleen Hallo bind-adres is vereist als hello andere eigenschappen worden overgenomen.

Hallo tabel heeft voorbeeld exemplaar instellingen 

| Beschrijving | File |
|:--|:--|
| Standaardexemplaar en -exemplaar met poort 3308. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| Standaardexemplaar en -exemplaar met poort 3308 en andere gebruikersnaam en wachtwoord. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a>Programma voor verificatie bestand MySQL OMI
Provider is een MySQL OMI verificatie programma die gebruikt tooedit Hallo MySQL OMI verificatiebestand worden kan opgenomen met Hallo-installatie van Hallo MySQL OMI. Hallo verificatie bestand programma kan worden gevonden op Hallo locatie te volgen.

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> Hallo referentiebestand moet worden gelezen door Hallo omsagent account. Hallo mycimprovauth opdracht uitgevoerd als omsgent wordt aanbevolen.

Hallo volgende tabel biedt details over Hallo-syntaxis voor het gebruik van mycimprovauth.

| Bewerking | Voorbeeld | Beschrijving
|:--|:--|:--|
| AutoUpdate * false\|waar * | mycimprovauth autoupdate false | Sets Hallo verificatiebestand al dan niet automatisch bijgewerkt op opnieuw opstarten of bijwerken. |
| standaard *gebruikersnaamwachtwoord bind-adres* | mycimprovauth standaard 127.0.0.1 hoofdmap pwd | Sets Hallo standaardexemplaar in Hallo verificatiebestand MySQL OMI.<br>het wachtwoordveld Hallo moet worden ingevoerd als tekst zonder opmaak - Hallo-wachtwoord in Hallo MySQL OMI verificatiebestand Base 64 gecodeerde worden. |
| Verwijder * default\|port_num * | mycimprovauth 3308 | Verwijdert het opgegeven exemplaar Hallo beide standaard of door poortnummer. |
| Help | mycimprov help | Een lijst met opdrachten toouse afdrukken. |
| afdrukken | mycimprov afdrukken | Een eenvoudig tooread MySQL OMI verificatiebestand afdrukken. |
| bijwerken van port_num *gebruikersnaamwachtwoord bind-adres* | mycimprov update 3307 127.0.0.1 hoofdmap pwd | Het opgegeven exemplaar Hallo updates of Hallo-exemplaar wordt toegevoegd als deze niet bestaat. |

Hallo definiëren volgende voorbeeldopdrachten een standaardgebruikersaccount voor Hallo MySQL-server op localhost.  het wachtwoordveld Hallo moet worden ingevoerd als tekst zonder opmaak - Hallo-wachtwoord in Hallo MySQL OMI verificatiebestand Base 64 gecodeerde

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a>Databasemachtigingen vereist voor de MySQL-prestatiemeteritems
Hallo MySQL gebruiker vereist toegang toohello volgende query's toocollect prestatiegegevens MySQL-Server. 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


Hallo MySQL ook is vereist, selecteer toegang toohello standaardtabellen te volgen.

- INFORMATION_SCHEMA
- MySQL. 

Deze rechten kunnen worden verleend door het uitvoeren van Hallo grant opdrachten te volgen.

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> toogrant machtigingen tooa MySQL gebruiker Hallo gebruiker verlenen bewaking moet hebben de bevoegdheid 'GRANT optie' hello, evenals Hallo bevoegdheid wordt verleend.

### <a name="define-performance-counters"></a>Prestatiemeteritems definiëren

Zodra u Hallo OMS-Agent voor Linux toosend gegevens tooLog Analytics configureert, moet u Hallo prestaties tellers toocollect configureren.  Gebruik de procedure Hallo in [Windows en Linux prestaties gegevensbronnen in Log Analytics](log-analytics-data-sources-windows-events.md) met items in de volgende tabel Hallo Hallo.

| Objectnaam | Naam van het meteritem |
|:--|:--|
| MySQL-database | Schijfruimte in Bytes |
| MySQL-database | Tabellen |
| MySQL-Server | Pct afgebroken verbinding |
| MySQL-Server | Verbinding gebruik Pct |
| MySQL-Server | Schijfruimtegebruik in Bytes |
| MySQL-Server | Volledige tabel Scan Pct |
| MySQL-Server | InnoDB buffergroep bereikt Pct |
| MySQL-Server | InnoDB groep gebruik bufferpercentage |
| MySQL-Server | InnoDB groep gebruik bufferpercentage |
| MySQL-Server | Sleutel Trefferfrequentie Pct |
| MySQL-Server | Cache voor gebruik Pct |
| MySQL-Server | Cache voor Write-Pct |
| MySQL-Server | Query-Cache treffers Pct |
| MySQL-Server | Query-Cache Prunes Pct |
| MySQL-Server | Query-Cache gebruiken Pct |
| MySQL-Server | Trefferfrequentie in tabel Pct |
| MySQL-Server | Tabel Cache gebruik Pct |
| MySQL-Server | Tabel vergrendelen conflicten Pct |

## <a name="apache-http-server"></a>Apache HTTP-Server 
Als de Apache HTTP-Server op Hallo-computer wordt gedetecteerd wanneer Hallo omsagent bundel is geïnstalleerd, wordt een provider voor de Apache HTTP-Server voor prestatiebewaking automatisch geïnstalleerd. Deze provider is afhankelijk van een Apache-module die moet worden geladen in Hallo Apache HTTP-Server in de volgorde tooaccess prestatiegegevens. Hallo-module kan worden geladen met de volgende opdracht Hallo:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello Apache bewakingsmodule, Hallo volgende opdracht uitvoeren:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a>Prestatiemeteritems definiëren

Zodra u Hallo OMS-Agent voor Linux toosend gegevens tooLog Analytics configureert, moet u Hallo prestaties tellers toocollect configureren.  Gebruik de procedure Hallo in [Windows en Linux prestaties gegevensbronnen in Log Analytics](log-analytics-data-sources-windows-events.md) met items in de volgende tabel Hallo Hallo.

| Objectnaam | Naam van het meteritem |
|:--|:--|
| Apache HTTP-Server | Bezet werknemers |
| Apache HTTP-Server | Niet-actieve werknemers |
| Apache HTTP-Server | PCT bezet werknemers |
| Apache HTTP-Server | Totaal aantal Pct CPU |
| Apache virtuele Host | Fouten per minuut - Client |
| Apache virtuele Host | Fouten per minuut - Server |
| Apache virtuele Host | KB per aanvraag |
| Apache virtuele Host | Aanvragen KB per seconde |
| Apache virtuele Host | Aanvragen per seconde |



## <a name="next-steps"></a>Volgende stappen
* [Verzamelen van prestatiemeteritems](log-analytics-data-sources-performance-counters.md) van Linux-agents.
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen. 
