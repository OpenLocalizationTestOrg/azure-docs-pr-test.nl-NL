---
title: aaaTroubleshooting en bewaking van SAP HANA in Azure (grote exemplaren) | Microsoft Docs
description: Problemen oplossen en SAP HANA op een Azure (grote exemplaren) bewaken.
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a>Hoe tootroubleshoot en monitor SAP HANA (grote exemplaren) in Azure


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a>Bewaking in SAP HANA in Azure (grote exemplaren)

SAP HANA in Azure (grote exemplaren) gaat niet anders andere IaaS-implementatie, moet u toomonitor wat OS Hallo en toepassing hello is doen en hoe deze Hallo resources volgende gebruiken:

- CPU
- Geheugen
- Netwerkbandbreedte
- Schijfruimte

Als u met Azure Virtual Machines, moet u toofigure uit of Hallo resource klassen hierboven genoemde voldoende of deze ophalen of leeg. Hieronder vindt u meer details op elk van de verschillende klassen Hallo:

**Resource-CPU-verbruik:** Hallo verhouding die SAP gedefinieerd voor bepaalde werkbelasting tegen HANA is afgedwongen toomake ervoor dat er voldoende bronnen CPU toowork beschikbaar via het Hallo-gegevens die zijn opgeslagen in het geheugen moet zijn. Niettemin, kunnen er gevallen waarbij HANA verbruikt veel CPU uitvoeren van query's vanwege toomissing indexen of vergelijkbare problemen. Dit betekent dat, moet u CPU-resourceverbruik Hallo HANA grote exemplaar eenheid, evenals de CPU-resources verbruikt door services voor specifieke HANA Hallo van controleren.

**Geheugengebruik:** belangrijke toomonitor uit binnen HANA, evenals buiten HANA op Hallo-eenheid Is. Binnen HANA, controleren hoe de gegevens Hallo toegewezen geheugen in volgorde toostay binnen Hallo vereist het formaat van de richtlijnen van SAP HANA verbruikt. U wilt ook toomonitor geheugenverbruik op Hallo grote exemplaar niveau toomake ervoor dat aanvullende geïnstalleerde niet-HANA software niet te veel geheugen in beslag nemen, en daarom met HANA voor geheugen concurreren.

**De netwerkbandbreedte:** hello Azure VNet gateway beperkt is in de bandbreedte van gegevens naar hello Azure VNet te verplaatsen, dus is het handig toomonitor Hallo gegevens zijn ontvangen door alle Azure VM's binnen een VNet toofigure nagaan hoe sluit u toohello grenzen van hello Azure Hallo gateway-SKU die u hebt geselecteerd. Op Hallo HANA grote exemplaar eenheid maakt deze zin toomonitor binnenkomende en uitgaande netwerkverkeer ook en tookeep bijhouden van Hallo volumes die gedurende een periode worden verwerkt.

**Schijfruimte:** verbruik van schijfruimte wordt meestal verhoogd gedurende een bepaalde periode. Er zijn diverse redenen hiervoor, maar de meeste van alle zijn: gegevensvolume toeneemt, neemt de uitvoering van transactielogboeken, traceringsbestanden opslaan en uitvoeren van opslag-momentopnamen. Daarom is belangrijk toomonitor schijfruimtegebruik en Hallo schijfruimte die is gekoppeld aan Hallo HANA grote exemplaar eenheid beheren.

## <a name="monitoring-and-troubleshooting-from-hana-side"></a>Bewaking en probleemoplossing van HANA kant

In de volgorde tooeffectively analyseren problemen gerelateerde tooSAP HANA in Azure (grote exemplaren), is het nuttig toonarrow omlaag Hallo hoofdoorzaak van een probleem. SAP heeft een grote hoeveelheid documentatie toohelp gepubliceerd u.

Toepasselijke Veelgestelde vragen over verwante tooSAP HANA prestaties vindt u in de volgende opmerkingen bij de SAP Hallo:

- [SAP-notitie #2222200: veelgestelde vragen over: SAP HANA-netwerk](https://launchpad.support.sap.com/#/notes/2222200)
- [SAP-notitie #2100040: veelgestelde vragen over: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040)
- [SAP-notitie #199997: veelgestelde vragen over: SAP HANA-geheugen](https://launchpad.support.sap.com/#/notes/2177064)
- [SAP-notitie #200000: veelgestelde vragen over: Optimalisatie van de SAP HANA-prestaties](https://launchpad.support.sap.com/#/notes/2000000)
- [SAP-notitie #199930: veelgestelde vragen over: SAP HANA i/o-analyse](https://launchpad.support.sap.com/#/notes/1999930)
- [SAP-notitie #2177064: veelgestelde vragen over: SAP HANA-Service opnieuw starten en loopt vast](https://launchpad.support.sap.com/#/notes/2177064)

**SAP HANA-waarschuwingen**

Controleer Hallo huidige SAP HANA waarschuwing Logboeken als een eerste stap. Ga te in SAP HANA Studio**-beheerconsole: waarschuwingen: weergeven: alle waarschuwingen**. Op dit tabblad ziet alle SAP HANA-waarschuwingen voor specifieke waarden (beschikbaar fysiek geheugen, CPU-gebruik, enzovoort) die buiten Hallo ingesteld minimale en maximale drempelwaarden vallen. Standaard controles worden automatisch vernieuwd om de 15 minuten.

![Ga in de SAP HANA Studio tooAdministration Console: waarschuwingen: weergeven: alle waarschuwingen](./media/troubleshooting-monitoring/image1-show-alerts.png)

**CPU**

Voor een waarschuwing geactiveerd vanwege tooimproper drempelinstelling, is een resolutie tooreset toohello standaardwaarde of een meer redelijke drempelwaarde.

![Toohello standaardwaarde of een meer redelijke drempelwaarde opnieuw instellen](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

Hallo waarschuwingen na kan duiden op problemen voor CPU-resources:

- Host-CPU-gebruik (waarschuwing 5)
- Meest recente opslagpuntbewerking (waarschuwing 28)
- Duur van het opslagpunt (waarschuwing 54)

Hoog CPU-verbruik ziet u op uw SAP HANA-database van een van de volgende Hallo:

- 5 (Host-CPU-gebruik) van de waarschuwing wordt gegenereerd voor de huidige of eerdere CPU-gebruik
- Hallo weergegeven CPU-gebruik op Hallo overzicht scherm

![CPU-gebruik op Hallo overzicht scherm weergegeven](./media/troubleshooting-monitoring/image3-cpu-usage.png)

Hallo Load grafiek kan hoog CPU-verbruik of hoge verbruik in Hallo afgelopen weergeven:

![Hallo Load grafiek kan hoog CPU-verbruik of hoog verbruik in Hallo afgelopen weergeven](./media/troubleshooting-monitoring/image4-load-graph.png)

Een waarschuwing geactiveerd vanwege toohigh CPU-gebruik kan worden veroorzaakt door een aantal redenen, waaronder maar niet beperkt tot: de uitvoering van bepaalde transacties, het laden van gegevens, de verkeerd-om taken, langlopende SQL-instructies en ongeldige query-prestaties (bijvoorbeeld met BW op HANA kubussen).

Raadpleeg toohello [SAP HANA probleemoplossing: CPU gerelateerde veroorzaakt en oplossingen](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) site voor gedetailleerde stappen voor probleemoplossing.

**Besturingssysteem**

Een van de belangrijkste Hallo controleert voor SAP HANA op Linux is toomake ervoor dat transparante grote pagina's zijn uitgeschakeld, Zie [SAP-notitie #2131662 – transparante grote pagina's (THP) op Servers voor SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).

- U kunt controleren als transparant grote pagina's worden ingeschakeld via Hallo Linux-opdracht te volgen: **cat /sys/kernel/mm/transparent\_hugepage/ingeschakeld**
- Als _altijd_ is ingesloten door haakjes zoals hieronder, betekent dit dat de Hallo transparante grote pagina's zijn ingeschakeld: [altijd] madvise nooit; als _nooit_ is ingesloten door haakjes zoals hieronder, betekent dit dat Hallo transparant Grote pagina's zijn uitgeschakeld: altijd madvise [nooit]

niets Hallo volgende Linux-opdracht moet worden geretourneerd: **rpm - qa | grep ulimit.** Als het erop lijkt _ulimit_ is geïnstalleerd, verwijdert u deze onmiddellijk.

**Geheugen**

Waarnemen dat Hallo bedrag van het geheugen toegewezen door Hallo SAP HANA-database is hoger dan verwacht. Hallo na de waarschuwingen wijzen op problemen met hoog geheugengebruik:

- Host fysieke geheugengebruik (waarschuwing 1)
- Geheugengebruik van de naamserver (waarschuwing 12)
- Totale geheugengebruik van kolom Store tabellen (waarschuwing 40)
- Geheugengebruik van services (waarschuwing 43)
- Geheugengebruik van de belangrijkste opslag van kolom Store tabellen (waarschuwing 45)
- Runtime-dumpbestanden (waarschuwing 46)

Raadpleeg toohello [SAP HANA probleemoplossing: geheugenproblemen](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) site voor gedetailleerde stappen voor probleemoplossing.

**Netwerk**

Raadpleeg te[SAP-notitie #2081065 – SAP HANA-netwerk het oplossen van problemen](https://launchpad.support.sap.com/#/notes/2081065) en probleemoplossing van de stappen in deze SAP-notitie Hallo-netwerk uit te voeren.

1. Analyse van round trip-tijd tussen server en client.
  A. Hallo SQL-script uitvoeren [ _HANA\_netwerk\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._
  
2. Analyseer de communicatie tussen knooppunten.
  A. SQL-script uitvoeren [ _HANA\_netwerk\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._

3. Voer de opdracht Linux **ifconfig** (Hallo uitvoer ziet als een pakketverlies optreden).
4. Voer de opdracht Linux **tcpdump**.

Gebruik tevens Hallo open-source [IPERF](https://iperf.fr/) hulpprogramma (of vergelijkbaar) toomeasure echte toepassing netwerkprestaties.

Raadpleeg toohello [SAP HANA probleemoplossing: prestaties toegang en verbindingsproblemen](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) site voor gedetailleerde stappen voor probleemoplossing.

**Storage**

Vanuit het perspectief van een eindgebruiker wordt een toepassing (of het Hallo-systeem als geheel) wordt traag uitgevoerd, reageert niet of kan zelfs toohang lijken als er problemen met i/o-prestaties zijn. In Hallo **Volumes** tabblad in SAP HANA-Studio, kunt u zien Hallo gekoppelde volumes en welke volumes worden gebruikt door elke service.

![Hallo Volumes tabblad in SAP HANA Studio ziet u Hallo gekoppelde volumes en welke volumes worden gebruikt door elke service](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

Gekoppelde volumes in de onderste gedeelte Hallo van welkomstscherm u details van ziet Hallo volumes, zoals bestanden en i/o-statistieken.

![Gekoppelde volumes in de onderste gedeelte Hallo van welkomstscherm u details van ziet Hallo volumes, zoals bestanden en i/o-statistieken](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

Raadpleeg toohello [SAP HANA probleemoplossing: i/o-gerelateerde hoofdoorzaken en oplossingen](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) en [SAP HANA probleemoplossing: schijf gerelateerde hoofdoorzaken en oplossingen](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) site voor gedetailleerde stappen voor probleemoplossing.

**Diagnostische hulpprogramma 's**

Uitvoeren van een SAP HANA-statuscontrole via HANA\_configuratie\_Minichecks. Dit hulpprogramma retourneert een potentieel kritiek technische problemen die als waarschuwingen in SAP HANA Studio al moeten zijn opgetreden.

Raadpleeg te[SAP-notitie #1969700-verzameling van de SQL-instructie voor SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) en Hallo SQL Statements.zip bestand gekoppelde toothat opmerking te downloaden. Sla dit ZIP-bestand op Hallo van de lokale vaste schijf.

SAP HANA Studio Hallo **systeemgegevens** tabblad, met de rechtermuisknop op Hallo **naam** en selecteert u **SQL importinstructies**.

![SAP HANA Studio op Hallo systeemgegevens tabblad met de rechtermuisknop op in de kolom naam Hallo en selecteer SQL-instructies voor importeren](./media/troubleshooting-monitoring/image7-import-statements-a.png)

Selecteer Hallo SQL Statements.zip bestand lokaal opgeslagen en een map met de bijbehorende SQL-instructies hello wordt geïmporteerd. Op dit moment hello die veel verschillende diagnostische controles kunnen worden uitgevoerd met deze SQL-instructies.

Bijvoorbeeld: tootest SAP HANA System Replication bandbreedtevereisten, met de rechtermuisknop op Hallo **bandbreedte** instructie onder **replicatie: bandbreedte** en selecteer **Open** in SQL-Console.

Hallo volledige SQL-instructie wordt geopend zodat invoerparameters (wijziging sectie) toobe gewijzigd en vervolgens uitvoeren.

![Hallo volledige SQL-instructie wordt geopend zodat invoerparameters (wijziging sectie) toobe gewijzigd en vervolgens uitvoeren](./media/troubleshooting-monitoring/image8-import-statements-b.png)

Een ander voorbeeld is met de rechtermuisknop op op Hallo-overzichten onder **replicatie: overzicht**. Selecteer **Execute** in het contextmenu Hallo:

![Een ander voorbeeld is met de rechtermuisknop op op Hallo-overzichten onder replicatie: overzicht. Uitvoeren in het contextmenu Hallo selecteren](./media/troubleshooting-monitoring/image9-import-statements-c.png)

Dit resulteert in informatie die bij het oplossen van helpt:

![Dit leidt tot informatie die bij het oplossen van problemen helpt](./media/troubleshooting-monitoring/image10-import-statements-d.png)

Dezelfde Hallo voor HANA\_configuratie\_Minichecks en controleer of alle _X_ merken in Hallo _C_ kolom (Kritiek).

Voorbeeld van uitvoer:

**HANA\_configuratie\_MiniChecks\_Rev102.01 + 1** voor algemene SAP HANA-controles.

![HANA\_configuratie\_MiniChecks\_Rev102.01 + 1 voor algemene SAP HANA-controles](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

**HANA\_Services\_overzicht** voor een overzicht van wat SAP HANA-services die momenteel worden uitgevoerd.

![HANA\_Services\_overzicht voor een overzicht van wat SAP HANA-services die momenteel worden uitgevoerd](./media/troubleshooting-monitoring/image12-services-overview.png)

**HANA\_Services\_statistieken** voor SAP HANA servicegegevens (CPU, geheugen, etc.).

![HANA\_Services\_statistieken voor SAP HANA-servicegegevens ](./media/troubleshooting-monitoring/image13-services-statistics.png)

**HANA\_configuratie\_overzicht\_Rev110 +** voor algemene informatie over Hallo SAP HANA-exemplaar.

![HANA\_configuratie\_overzicht\_Rev110 + voor algemene informatie over Hallo SAP HANA-exemplaar](./media/troubleshooting-monitoring/image14-configuration-overview.png)

**HANA\_configuratie\_Parameters\_Rev70 +** toocheck SAP HANA-parameters.

![HANA\_configuratie\_Parameters\_Rev70 + toocheck SAP HANA parameters](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

