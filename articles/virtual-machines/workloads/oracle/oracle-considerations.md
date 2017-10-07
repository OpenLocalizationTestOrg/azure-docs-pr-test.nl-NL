---
title: aaaOracle oplossingen in Microsoft Azure | Microsoft Docs
description: Meer informatie over ondersteunde configuraties en beperkingen van Oracle-oplossingen in Microsoft Azure.
services: virtual-machines-linux
documentationcenter: 
manager: timlt
author: rickstercdn
tags: azure-resource-management
ms.assetid: 5d71886b-463a-43ae-b61f-35c6fc9bae25
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: rclaus
ms.openlocfilehash: 54dc62e76129535da7fb6f131af90c83adfec6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="oracle-solutions-and-their-deployment-on-microsoft-azure"></a>Oracle-oplossingen en hun implementatie in Microsoft Azure
In dit artikel bevat informatie die vereist toosuccesfully implementeert verschillende Oracle-oplossingen in Microsoft Azure. Deze oplossingen zijn gebaseerd op de virtuele Machine installatiekopieën die zijn gepubliceerd door Oracle in hello Azure Marketplace. tooget een lijst van beschikbare installatiekopieën, Hallo volgende opdracht uitvoeren:
```azurecli-interactive
az vm image list --publisher oracle -o table --all
```
Zijn de volgende Hallo vanaf 6-16-2017 Hallo lijst met afbeeldingen:
```bash
Offer                   Publisher    Sku                     Urn                                                          Version
----------------------  -----------  ----------------------  -----------------------------------------------------------  -------------
Oracle-Database-Ee      Oracle       12.1.0.2                Oracle:Oracle-Database-Ee:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Database-Se      Oracle       12.1.0.2                Oracle:Oracle-Database-Se:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Linux            Oracle       6.4                     Oracle:Oracle-Linux:6.4:6.4.20141206                         6.4.20141206
Oracle-Linux            Oracle       6.7                     Oracle:Oracle-Linux:6.7:6.7.20161007                         6.7.20161007
Oracle-Linux            Oracle       6.8                     Oracle:Oracle-Linux:6.8:6.8.20161020                         6.8.20161020
Oracle-Linux            Oracle       6.9                     Oracle:Oracle-Linux:6.9:6.9.20170406                         6.9.20170406
Oracle-Linux            Oracle       7.0                     Oracle:Oracle-Linux:7.0:7.0.20141217                         7.0.20141217
Oracle-Linux            Oracle       7.2                     Oracle:Oracle-Linux:7.2:7.2.20161020                         7.2.20161020
Oracle-Linux            Oracle       7.3                     Oracle:Oracle-Linux:7.3:7.3.20170320                         7.3.20170320
Oracle-WebLogic-Server  Oracle       Oracle-WebLogic-Server  Oracle:Oracle-WebLogic-Server:Oracle-WebLogic-Server:12.1.2  12.1.2
```

Deze installatiekopieën worden beschouwd als 'Bring Your Own License' en als zodanig u alleen gefactureerd voor berekening, opslag en netwerken kosten die zijn gemaakt door het uitvoeren van een virtuele machine.  U staat op het juiste licentie toouse Oracle-software en dat u een huidige support-overeenkomst met Oracle hebt wordt aangenomen. Oracle heeft licentiemobiliteit van lokale tooAzure gegarandeerd. Zie Hallo gepubliceerd [Oracle en Microsoft](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html) Opmerking voor meer informatie over licentiemobiliteit. 

Personen kunt toobase ook hun oplossingen op aangepaste installatiekopieën ze maken in Azure of een aangepaste installatiekopieën van hun on-premises-omgevingen te uploaden.

## <a name="support-for-jd-edwards"></a>Ondersteuning voor JD Edwards
Op basis van tooOracle ondersteuning Opmerking [Doc-ID 2178595.1](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=573435677515785&id=2178595.1&_afrWindowMode=0&_adf.ctrl-state=o852dw7d_4) , JD Edwards EnterpriseOne versies 9.2 en hoger worden ondersteund op **openbare cloud aanbieding** die voldoet aan hun specifieke `Minimum Technical Requirements` (MTR).  U moet toocreate aangepaste installatiekopieën die voldoen aan hun MTR specificaties voor compatibiliteit van besturingssystemen en software-toepassing. 

## <a name="oracle-database-virtual-machine-images"></a>Installatiekopieën van virtuele machines voor Oracle-Database
Oracle biedt ondersteuning voor actieve Oracle DB 12.1 Standard en Enterprise-edities in Azure op installatiekopieën van virtuele machines op basis van Oracle Linux.  Voor de beste prestaties voor productieworkloads van Oracle-database op Azure Hallo ervoor tooproperly grootte Hallo VM-installatiekopie en gebruik van beheerde schijven die worden ondersteund door de Premium-opslag. Voor instructies over hoe tooquickly ervoor zorgen dat u een Oracle-database actief in Azure met behulp van Hallo Oracle gepubliceerde VM-installatiekopie [probeer Hallo Oracle DB Quick Start scenario](oracle-database-quick-create.md).

### <a name="attached-disk-configuration-options"></a>Gekoppelde schijf configuratieopties

Gekoppelde schijven zijn afhankelijk van hello Azure Blob storage-service. Elke schijf die standaard is geschikt voor een theoretisch maximumaantal ongeveer 500 i/o-bewerkingen per seconde (IOPS). Onze premium schijf aanbieding voorkeur geniet voor database werklasten met hoge prestaties en kunt bereiken up too5000 IOP's per schijf. Hoewel u gebruik kunt maken één schijf als die voldoet aan de prestaties van uw behoeften: u kunt Hallo effectieve IOPS-prestaties verbeteren als u meerdere gekoppelde schijven te gebruiken, databasegegevens verdeeld over deze en gebruik vervolgens Oracle automatische Storage Management (ASM). Zie [automatische opslag van Oracle-overzicht](http://www.oracle.com/technetwork/database/index-100339.html) voor Oracle ASM specifieke informatie. Voor een voorbeeld van hoe tooinstall en Oracle ASM configureren op een virtuele machine van Azure Linux - kunt u proberen Hallo [installeren en configureren van Oracle geautomatiseerde Storage Management](configure-oracle-asm.md) zelfstudie.

### <a name="oracle-realtime-application-cluster-rac"></a>Oracle Realtime toepassingscluster (RAC)
Oracle RAC is ontworpen toomitigate Hallo uitvallen van één knooppunt in een cluster met meerdere knooppunten on-premises configuratie.  Is afhankelijk van de twee technologieën van lokale die geen systeemeigen toohyper-scale openbare cloudomgevingen: gedeelde schijf en netwerk multicast. Er zijn door andere bedrijven gemaakt voor oplossingen van andere leveranciers [zoals FlashGrid](https://www.flashgrid.io/oracle-rac-in-azure/) die deze technologieën emuleren als u toodeploy Oracle RAC in Azure nodig. 

### <a name="high-availability-and-disaster-recovery-considerations"></a>Overwegingen voor hoge beschikbaarheid en noodherstel herstel
Wanneer u de Oracle-Databases in Azure, bent u verantwoordelijk voor het implementeren van een hoge beschikbaarheid en noodherstel herstel oplossing tooavoid uitvaltijd. 

Hoge beschikbaarheid en herstel na noodgevallen voor Oracle Database Enterprise Edition (zonder RAC) op Azure kan worden bereikt met [Data Guard, actieve Data Guard](http://www.oracle.com/technetwork/articles/oem/dataguardoverview-083155.html), of [Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate), met twee databases in twee afzonderlijke virtuele machines. Beide virtuele machines moet worden in Hallo dezelfde [virtueel netwerk](https://azure.microsoft.com/documentation/services/virtual-network/) tooensure toegang te krijgen tot elkaar via Hallo privé permanente IP-adres.  Bovendien wordt aangeraden Hallo virtuele machines te plaatsen in Hallo dezelfde beschikbaarheidsset tooallow Azure tooplace in afzonderlijke domeinen fault en upgradedomeinen.  U kunt deze twee databases repliceren tussen twee verschillende regio's en de twee exemplaren van Hallo verbinden met een VPN-Gateway als u wilt dat toohave geografische redundantie - hebben.

We hebben een zelfstudie '[implementeren Oracle DataGuard op Azure](configure-oracle-dataguard.md)' die wordt u begeleid bij Hallo basisinstellingen procedure tootrial dit op Azure.  

Met Oracle Data Guard hoge beschikbaarheid kan worden verkregen met een primaire database in één virtuele machine, een secundaire (stand-by) database in een andere virtuele machine en een replicatieverbinding tussen deze twee instellen. Hallo-resultaat is leestoegang toohello kopie van Hallo-database. Met Oracle GoldenGate, kunt u de replicatie in twee richtingen tussen de twee databases Hallo configureren. hoe tooset van een oplossing voor hoge beschikbaarheid voor uw databases met behulp van deze hulpprogramma's, Zie toolearn [Active Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) en [GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) documentatie op Hallo Oracle-website. Als u moet lezen-schrijven toegang toohello kopie van Hallo-database, kunt u [Oracle Active Data Guard](http://www.oracle.com/uk/products/database/options/active-data-guard/overview/index.html).

We hebben een zelfstudie '[implementeren Oracle GoldenGate op Azure](configure-oracle-golden-gate.md)' die wordt u begeleid bij Hallo basic seup procedure tootrial dit op Azure.

Ondanks dat een oplossing voor HA en Noodherstel ontworpen in Azure, zult u tooensure hebt u een back-upstrategie in place toorestore uw database.  We hebben een zelfstudie [back-up en herstel een Oracle-Database](oracle-backup-recovery.md) die u helpt bij Hallo eenvoudige procedure voor het tot stand brengen van een consistant back-up.

## <a name="oracle-weblogic-server-virtual-machine-images"></a>Installatiekopieën van virtuele machines voor Oracle WebLogic Server
* **Clustering wordt ondersteund op Enterprise-editie alleen.** U een licentie toouse WebLogic clustering alleen bij gebruik van Hallo WebLogic Server, Enterprise Edition. Gebruik geen clustering met WebLogic Server Standard Edition.
* **Multicast-UDP wordt niet ondersteund.** Azure ondersteunt unicasting UDP, maar niet multicasting of broadcasting. WebLogic Server is kunnen toorely op Azure UDP-unicast-mogelijkheden. Voor de beste resultaten vertrouwen op UDP-unicast, wordt aangeraden dat Hallo WebLogic clustergrootte wordt gehandhaafd statisch, of met niet meer dan 10 beheerde servers die zijn opgenomen in de cluster Hallo worden bewaard.
* **WebLogic Server verwacht openbare en particuliere poort toobe Hallo voor T3 dezelfde (bijvoorbeeld, als u Enterprise JavaBeans) openen.** Neem bijvoorbeeld een meerlaagse scenario waarbij een servicetoepassing laag (EJB) wordt uitgevoerd op een WebLogic Server-cluster dat bestaat uit twee of meer virtuele machines, in een vNet met de naam **SLWLS**. Hallo clientlaag bevindt zich in een ander subnet in Hallo hetzelfde vNet met een eenvoudige Java-programma probeert toocall EJB in Hallo-servicelaag. Omdat het benodigde tooload saldo Hallo-servicelaag, moet een openbaar eindpunt met gelijke taakverdeling toobe voor Hallo virtuele Machines in Hallo WebLogic Server-cluster gemaakt. Als Hallo particuliere poort die u opgeeft verschilt van Hallo openbare poort (bijvoorbeeld 7006:7008), wordt een foutbericht zoals Hallo volgende weergegeven:

       [java] javax.naming.CommunicationException [Root exception is java.net.ConnectException: t3://example.cloudapp.net:7006:

       Bootstrap to: example.cloudapp.net/138.91.142.178:7006' over: 't3' got an error or timed out]

   Dit komt doordat voor externe toegang T3, WebLogic Server Hallo load balancer poort verwacht en Hallo WebLogic beheerde server poort toobe Hallo dezelfde. Hallo-client heeft er toegang tot poort 7006 (Hallo load balancer-poort) in Hallo boven het geval is, en Hallo beheerde server luistert naar 7008 (Hallo particuliere poort). Deze beperking geldt alleen voor T3 access, niet HTTP.

   tooavoid dit probleem, het gebruik van Hallo volgende tijdelijke oplossingen:

  * Gebruik Hallo dezelfde persoonlijke en openbare poortnummers voor load balanced eindpunten toegewezen tooT3 toegang.
  * Hallo volgende JVM-parameter bij het starten van WebLogic Server omvatten:

         -Dweblogic.rjvm.enableprotocolswitch=true

Voor meer informatie, Zie KB-artikel **860340.1** op <http://support.oracle.com>.

* **Dynamische clustering en beperkingen voor taakverdeling.** Stel dat u wilt dat een dynamische cluster in WebLogic Server toouse en deze gebruiken via een enkele, openbare taakverdeling eindpunt in Azure. Dit kan gebeuren als u een vaste poortnummer voor elk van de Hallo servers beheerde (niet dynamisch toegewezen vanuit een bereik) en meer beheerde servers, dan is het bijhouden van Hallo beheerder machines niet worden gestart (dat wil zeggen, niet meer dan een beheerde server per virt ual-machine). Als uw configuratie in meer WebLogic servers worden gestart resulteert dan virtuele machines (dat wil zeggen waar meerdere WebLogic exemplaren servershare hello dezelfde virtuele machine), dan is het niet mogelijk meer dan één van deze exemplaren van WebLogic Server servers toobind tooa opgegeven poortnummer – Hallo anderen op deze virtuele machine mislukt.

   Op Hallo anderzijds, als u Hallo beheerder server tooautomatically configureert toewijzen unieke poortnummers tooits beheerde servers, en vervolgens de load balancer is niet mogelijk omdat Azure biedt geen ondersteuning voor toewijzing van een enkele openbare poort toomultiple particuliere poorten, worden vereist voor deze configuratie.
* **Meerdere exemplaren van Weblogic Server op een virtuele machine.** Afhankelijk van de vereisten van uw implementatie, kunt u overwegen Hallo-optie van het uitvoeren van meerdere exemplaren van WebLogic Server op Hallo dezelfde virtuele machine als Hallo virtuele machine groot genoeg is. Bijvoorbeeld: op een virtuele machine van gemiddelde grootte, die twee cores bevat, kunt u toorun twee exemplaren van WebLogic Server. Houd er echter rekening mee dat u dat nog steeds het is raadzaam dat u introductie van individuele foutpunten in uw architectuur die Hallo geval zijn vermijden zou als u slechts één virtuele machine met meerdere exemplaren van WebLogic Server gebruikt. Gebruik van ten minste twee virtuele machines kan een betere benadering, en elk van deze virtuele machines kan vervolgens meerdere exemplaren van WebLogic Server uitvoeren. Elk van deze exemplaren van WebLogic Server kan nog steeds deel uitmaken van Hallo hetzelfde cluster. Opmerking, maar het is momenteel niet mogelijk toouse tooload-saldo Azure-eindpunten die beschikbaar worden gesteld door dergelijke implementaties WebLogic Server binnen dezelfde virtuele machine Hallo omdat Azure load balancer Hallo netwerktaakverdelingsservers toobe verdeeld moeten over unieke virtuele machines.

## <a name="oracle-jdk-virtual-machine-images"></a>Installatiekopieën van virtuele machines JDK Oracle
* **JDK 6 en 7 van de meest recente updates.** Terwijl wordt u aangeraden Hallo nieuwste openbare, ondersteunde versie van Java (momenteel Java 8), wordt Azure ook JDK 6 en 7 installatiekopieën beschikbaar. Dit is bedoeld voor oudere toepassingen die nog niet klaar toobe bijgewerkt tooJDK 8 zijn. Tijdens het updates tooprevious JDK afbeeldingen mogelijk niet meer beschikbaar toohello publiek, gegeven Hallo Microsoft samen met de Oracle, Hallo JDK 6 en 7 afbeeldingen die zijn verstrekt door Azure worden bedoeld toocontain een meer recente update voor niet-openbaar die normaal gesproken worden aangeboden door Oracle tooonly een selecte groep Oracle de klanten ondersteund. Nieuwe versies van Hallo JDK installatiekopieën wordt gedurende een periode met bijgewerkte versies van JDK 6 en 7 beschikbaar gesteld.

   Hallo JDK die beschikbaar zijn in deze JDK 6 en 7 installatiekopieën en Hallo virtuele machines en installatiekopieën die zijn afgeleid, kunnen alleen worden gebruikt in Azure.
* **64-bits JDK.** Hallo Oracle WebLogic Server virtuele machine installatiekopieën en Hallo Oracle JDK installatiekopieën van virtuele machines die door Azure bevatten Hallo 64-bits versies van Windows Server- en Hallo JDK.

## <a name="next-steps"></a>Volgende stappen
U hebt nu een overzicht van de huidige Oracle-oplossingen in Microsoft Azure. De volgende stap is toogo en implementeren van uw eerste Oracle-Database in Azure.
- Probeer Hallo [een Oracle-Database maken op Azure](oracle-database-quick-create.md) zelfstudie tooget gestart.
