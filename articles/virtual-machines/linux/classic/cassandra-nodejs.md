---
title: aaaRun Cassandra met Linux in Azure | Microsoft Docs
description: Hoe een Cassandra toorun-cluster op Linux in Azure Virtual Machines van een Node.js-app
services: virtual-machines-linux
documentationcenter: nodejs
author: tomarcher
manager: routlaw
editor: 
tags: azure-service-management
ms.assetid: 30de1f29-e97d-492f-ae34-41ec83488de0
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 381ca301bbe88d3740cf182f9c44fada5b9ba7cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="running-cassandra-with-linux-on-azure-and-accessing-it-from-nodejs"></a>Cassandra op Azure uitvoeren met Linux en vanaf Node.js openen
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie Resource Manager-sjablonen voor [Datastax Enterprise](https://azure.microsoft.com/documentation/templates/datastax) en [Spark-cluster en Cassandra op CentOS](https://azure.microsoft.com/documentation/templates/spark-and-cassandra-on-centos/).

## <a name="overview"></a>Overzicht
Microsoft Azure is een open cloudplatform die zowel Microsoft als goed als niet-Microsoft-software, waaronder besturingssystemen, toepassingsservers, messaging middleware, evenals SQL en NoSQL-databases van beide modellen commerciële en open-source wordt uitgevoerd. Robuuste services op openbare clouds, inclusief Azure bouwen vereist zorgvuldige planning en architectuur opzettelijk voor beide toepassingsservers als opslag en lagen. Cassandra van gedistribueerde opslagarchitectuur is natuurlijk helpt bij het bouwen van maximaal beschikbare systemen die fouttolerant voor clusters zijn. Cassandra is een cloud schaal NoSQL-database onderhouden door Apache Software Foundation op cassandra.apache.org; Cassandra is geschreven in Java en daarom wordt uitgevoerd op zowel op Windows en Linux platforms.

Hallo van dit artikel worden tooshow Cassandra wilt implementeren op een virtuele Ubuntu als een cluster met één of meerdere data center gebruik van Microsoft Azure Virtual Machines en virtuele netwerken. Hallo Clusterimplementatie voor geoptimaliseerde productieworkloads valt buiten het bereik van dit artikel omdat hiervoor meerdere schijf knooppuntconfiguratie, geschikte topologie voor ringtopologie en gegevens modelleren toosupport Hallo nodig replicatie, gegevensconsistentie, doorvoer en vereisten voor hoge beschikbaarheid.

Dit artikel wordt een fundamenteel benadering tooshow wat bij gebouw Hallo Cassandra cluster betrokken is vergeleken Docker, Chef of Puppet waardoor Hallo infrastructuur implementeren veel eenvoudiger.  

## <a name="hello-deployment-models"></a>Hallo-implementatiemodellen
Microsoft Azure-netwerken kunt Hallo-implementatie van geïsoleerde persoonlijke clusters Hallo-toegang die beperkt tooattain fijn gedetailleerde netwerkbeveiliging worden kan.  Omdat dit artikel over het weergeven van Hallo Cassandra implementatie op een fundamenteel niveau is, gaan we in niet op Hallo consistentieniveau en Hallo optimale Opslagontwerp voor doorvoer. Hier volgt de lijst Hallo van netwerkvereisten voor onze hypothetische cluster:

* Externe systemen geen toegang tot de database van de Cassandra van binnen of buiten Azure
* Cassandra cluster heeft toobe achter een load balancer voor thrift-verkeer
* Cassandra knooppunten in twee groepen in elk Datacenter voor de clusterbeschikbaarheid van een verbeterde implementeren
* Vergrendelen Hallo cluster zodanig dat alleen serverfarm toepassing toegang tot toohello database rechtstreeks heeft
* Er is geen openbare netwerken eindpunten dan SSH
* Elk knooppunt Cassandra moet een vaste IP-adres

Cassandra kan worden geïmplementeerd tooa één Azure-regio of toomultiple regio's op basis van Hallo gedistribueerde aard van Hallo werkbelasting. Meerdere landen/regio implementatiemodel kan worden overgenomen tooserve eindgebruikers dichter tooa bepaalde Geografie via Hallo dezelfde Cassandra-infrastructuur. Cassandra van ingebouwde knooppunt replicatie zorgt voor synchronisatie van meerdere master Hallo schrijft die afkomstig zijn van meerdere datacenters en geeft een consistente weergave van Hallo gegevens tooapplications. Implementatie van meerdere landen/regio kan ook helpen bij Hallo risicobeperking van Hallo breder serviceonderbrekingen van Azure. Instelbare consistentie van Cassandra en de replicatietopologie, kunt in de behoeften van diverse RPO van toepassingen.

### <a name="single-region-deployment"></a>Implementatie van één regio
We begint met een implementatie met één regio en oogst Hallo geleerde lessen bij het maken van een model meerdere landen/regio. Azure virtuele netwerken worden gebruikte toocreate geïsoleerd subnetten zodat Hallo beveiliging netwerkvereisten bovengenoemde kunnen worden voldaan.  Hallo-proces beschreven bij het maken van de implementatie van één regio Hallo gebruikt Ubuntu 14.04 TNS en Cassandra 2.08; Hallo-proces kan echter eenvoudig worden aangenomen toohello andere varianten van Linux. Hallo Hieronder volgen enkele van Hallo al kenmerken van Hallo één regio implementatie.  

**Hoge beschikbaarheid:** Hallo Cassandra knooppunten weergegeven in afbeelding 1 zijn geïmplementeerd Hallo beschikbaarheidssets tootwo zodat Hallo knooppunten worden verdeeld tussen meerdere domeinen met fouten voor hoge beschikbaarheid. Virtuele machines van aantekeningen voorzien met elke beschikbaarheidsset is toegewezen too2 domeinen met fouten.  Microsoft Azure gebruikt Hallo concept van fouttolerantie domein toomanage niet-geplande uitvaltijd (bijvoorbeeld hardware of software-fouten) tijdens het Hallo-concept van upgradedomein (zoals host of Gast OS patches of upgrades worden uitgevoerd, toepassingsupgrades) wordt gebruikt voor het beheer van geplande uitvaltijd. Zie [herstel na noodgevallen en hoge beschikbaarheid voor Azure-toepassingen](http://msdn.microsoft.com/library/dn251004.aspx) voor de rol Hallo probleem- en upgrade-domeinen in het bereiken van maximale beschikbaarheid.

![Implementatie van één regio](./media/cassandra-nodejs/cassandra-linux1.png)

Afbeelding 1: Implementatie van één regio

Houd er rekening mee dat op moment van schrijven van dit hello Azure niet is toegestaan Hallo expliciete toewijzing van een groep van virtuele machines tooa specifieke foutdomein; Als gevolg daarvan kan zelfs met Hallo implementatiemodel weergegeven in afbeelding 1, is het statistisch waarschijnlijk er mogelijk domeinen met fouten in plaats van vier toegewezen tootwo alle Hallo virtuele machines.

**Load Balancing Thrift-verkeer:** toohello cluster een Thrift-clientbibliotheken binnen Hallo webserver verbinding maken via een interne load balancer. Hiervoor Hallo-proces voor het Hallo interne load balancer toohello "gegevens" subnet toevoegen (Zie afbeelding 1) in de context Hallo van cloudservice Hallo Hallo Cassandra cluster hosten. Als Hallo interne load balancer is gedefinieerd, moet elk knooppunt Hallo taakverdeling eindpunt toobe toegevoegd met de Hallo aantekeningen van een set met gelijke taakverdeling met eerder gedefinieerde load balancer-naam. Zie [Azure interne Load Balancing ](../../../load-balancer/load-balancer-internal-overview.md)voor meer informatie.

**Cluster zaden:** is het belangrijk tooselect Hallo meeste maximaal beschikbare knooppunten voor zaden zoals Hallo nieuwe knooppunten zullen communiceren met een seed-knooppunten toodiscover Hallo-topologie van Hallo-cluster. Eén knooppunt uit elke beschikbaarheidsset is aangewezen als seed-knooppunten tooavoid storingspunt.

**Replicatie Factor en Consistentieniveau:** Cassandra van ingebouwde hoge beschikbaarheid en gegevens duurzaamheid wordt gekenmerkt door Hallo replicatie Factor (RF - aantal exemplaren van elke rij die is opgeslagen op Hallo cluster) en Consistentieniveau (aantal replica's toobe lezen/geschreven voordat Hallo resultaat toohello aanroeper wordt geretourneerd). Replicatie factor wordt opgegeven tijdens Hallo KEYSPACE (vergelijkbaar tooa relationele database) maken dat Hallo consistentieniveau is opgegeven tijdens het uitgeven van Hallo CRUD-query. Zie de documentatie bij Cassandra [configureren voor consistentie](http://www.datastax.com/documentation/cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) voor de details van de consistentie en Hallo formule voor quorum berekeningen.

Cassandra ondersteunt twee soorten integriteit gegevensmodellen – consistentie en uiteindelijke consistentie; Hallo Factor voor replicatie en het niveau van de consistentie wordt bepalen samen als Hallo consistent worden zodra een schrijfbewerking voltooid is of moeten uiteindelijk consistent is. Bijvoorbeeld: QUORUM opgeven als Hallo die consistentieniveau altijd wordt zorgt ervoor dat gegevens consistentie terwijl u elk consistentieniveau lager dan het aantal replica's toobe geschreven als de benodigde tooattain Hallo QUORUM (bijvoorbeeld een) resulteert in gegevens wordt uiteindelijk consistent is.

Hallo 8-node cluster hierboven, met een factor van de replicatie van 3 en QUORUM (2 knooppunten worden gelezen of geschreven voor consistentie) consistentieniveau lezen/schrijven, kunnen overleven Hallo theoretische verlies van op de meeste 1 knooppunt per replicatie groep voordat de start van de toepassing hello Hallo Hallo fout daar iets van merkt. Hierbij wordt ervan uitgegaan dat alle Hallo sleutel spaties hebben goed met gelijke taakverdeling lezen/schrijven-aanvragen.  Hallo volgen Hallo-parameters we voor cluster Hallo geïmplementeerd gebruiken:

Één regio Cassandra clusterconfiguratie:

| Cluster-Parameter | Waarde | Opmerkingen |
| --- | --- | --- |
| Het aantal knooppunten (N) |8 |Totaal aantal knooppunten in cluster Hallo |
| Replicatie Factor (RF) |3 |Aantal replica's van een bepaalde rij |
| Consistentieniveau (schrijven) |QUORUM[(RF/2) +1) = 2] Hallo resultaat Hallo formule naar beneden afgerond |Schrijft op Hallo meeste 2 replica's voordat antwoord Hallo toohello aanroepfunctie wordt verzonden 3e replica is geschreven in een manier uiteindelijk consistent is. |
| Consistentieniveau (lezen) |QUORUM [(RF/2) + 1 = 2] Hallo resultaat van Hallo formule wordt omlaag afgerond |2 replica's leest voor het verzenden van antwoord toohello aanroeper. |
| Een replicatiestrategie voor |Zie NetworkTopologyStrategy [gegevensreplicatie](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) in Cassandra-documentatie voor meer informatie |Hallo-implementatietopologie begrijpt en replica's op knooppunten geplaatst, zodat alle Hallo-replica's niet op Hallo dezelfde eindigen rack |
| Snitch |Zie GossipingPropertyFileSnitch [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) in Cassandra-documentatie voor meer informatie |NetworkTopologyStrategy maakt gebruik van een concept van snitch toounderstand Hallo-topologie. GossipingPropertyFileSnitch kunt beter bepalen in kaart brengen van elk knooppunt toodata center en rack. Hallo-cluster gebruikt roddels toopropagate vervolgens deze informatie. Dit is veel eenvoudiger in dynamische IP-instelling relatieve tooPropertyFileSnitch |

**Azure overwegingen voor het Cluster Cassandra:** Microsoft Azure Virtual Machines mogelijkheid gebruikt Azure Blob-opslag voor persistentie van de schijf; Azure-opslag bespaart 3 replica's van elke schijf voor maximale duurzaamheid. Dit betekent dat elke rij gegevens ingevoegd in een tabel Cassandra is al opgeslagen in 3 replica's en daarom gegevensconsistentie is al afgehandeld als Hallo replicatie Factor (RF) 1. Hallo belangrijkste probleem met replicatie Factor 1 is toepassing hello krijgen uitvaltijd zelfs als een enkel Cassandra knooppunt mislukt. Als een knooppunt is niet actief op Hallo problemen (zoals hardware, software systeemfouten) wordt herkend door de Azure-Infrastructuurcontroller is, wordt dit echter een nieuw knooppunt in de plaats met behulp van inrichten Hallo dezelfde opslagstations. Inrichting van een nieuw knooppunt tooreplace Hallo oude een kan enkele minuten duren.  Op dezelfde manier Cassandra upgrades voor gepland onderhoudsactiviteiten zoals gastbesturingssysteem wijzigingen, en wijzigingen in de toepassing Azure-Infrastructuurcontroller voert rolling upgrades van Hallo knooppunten in cluster Hallo.  Rolling upgrades ook kan duren voordat u een paar knooppunten tegelijk, en daarom Hallo cluster korte uitvaltijd voor enkele partities kan optreden. Hallo gegevens wordt echter niet meer verloren vanwege toohello ingebouwde Azure Storage redundantie.  

Voor systemen geïmplementeerd tooAzure die geen hoge beschikbaarheid vereist (bijvoorbeeld ongeveer 99,9 die gelijkwaardige too8.76 uur-jaar; Zie [hoge beschikbaarheid](http://en.wikipedia.org/wiki/High_availability) voor meer informatie) hebt u mogelijk kunnen toorun met RF = 1 en Consistentieniveau = een.  Voor toepassingen met hoge beschikbaarheidsvereisten, RF = 3 en Consistentieniveau = QUORUM wordt tolereren Hallo uitvaltijd van een van de Hallo knooppunten een Hallo replica's. RF = 1 in traditionele implementaties (bijvoorbeeld op locatie) kunnen niet worden gebruikt vanwege mogelijk gegevensverlies toohello ten gevolge van problemen zoals schijffouten.   

## <a name="multi-region-deployment"></a>Implementatie van meerdere landen/regio
Data center bewust replicatie- en consistent model hierboven helpt bij de implementatie van meerdere landen/regio Hallo out of box zonder Hallo Hallo Cassandra van nodig voor elke externe tooling. Dit is heel anders dan traditionele relationele databases Hallo waarbij Hallo-instellingen voor het spiegelen van databases voor meerdere masters schrijfacties erg complex kan zijn. Cassandra in een instellen in meerdere regio kan helpen bij het Hallo-gebruiksscenario's waaronder de volgende Hallo:

**Implementatie op basis van nabijheid:** multitenant-toepassingen met de toewijzing van gebruikers van de tenant wissen-naar-regio, kan worden geprofiteerd door lage latenties Hallo meerdere landen/regio van het cluster. Voorbeeld van een management learning systemen voor onderwijsinstellingen kunnen implementeren om een gedistribueerde cluster in VS-Oost en VS-West regio's tooserve Hallo respectieve campussen voor transactionele evenals analytics. Hallo-gegevens kan lokaal consistent op Hallo tijd lees- en schrijfbewerkingen en uiteindelijk consistent tussen beide Hallo regio's kunnen worden. Er zijn andere voorbeelden zoals distributie van de media, e-commerce en alles en alles wat u geconcentreerd geo-gebruiker basis fungeert een goede gebruiksvoorbeeld voor dit implementatiemodel is.

**Hoge beschikbaarheid:** redundantie is een belangrijke rol bij het bereiken van maximale beschikbaarheid van de software en hardware; Zie betrouwbare Cloudsystemen gebouw in Microsoft Azure voor meer informatie. In Microsoft Azure is Hallo alleen betrouwbare manier om dat te bereiken true redundantie door het implementeren van een cluster met meerdere landen/regio. Toepassingen kunnen worden geïmplementeerd in een actief-actief of actief / passief-modus en als een van de regio's Hallo niet actief is, Azure Traffic Manager verkeer toohello actieve regio kunt omleiden.  Implementatie voor één regio Hallo als Hallo beschikbaarheid 99,9, is een implementatie van de twee regio kan bereiken een beschikbaarheid van 99.9999 berekend door Hallo formule: (1-(1-0.999) * (1-0,999)) * 100); Zie Hallo bovenstaande artikel voor meer informatie.

**Herstel na noodgevallen:** meerdere landen/regio Cassandra cluster als goed ontworpen, kan tolereren onherstelbare data center storingen. Als één regio is niet actief is, kunnen Hallo toepassing geïmplementeerd tooother regio's starten voor de eindgebruikers Hallo. Net als elke andere zakelijke continuïteit-implementaties is de toepassing hello toobe fouttolerante voor sommige verlies van gegevens uit de gegevens in de asynchrone pijplijn Hallo Hallo. Cassandra heeft echter Hallo herstel veel sneller dan Hallo periode die door processen voor het herstellen van traditionele databases. Afbeelding 2 toont Hallo normale implementatie voor meerdere landen/regio-model met acht knooppunten in elke regio. Beide regio's spiegelbeeld van elkaar voor Hallo zijn dezelfde hoogte van het; concrete ontwerpen, is afhankelijk van type werkbelasting hello (bv. transactioneel of analytische), RPO, RTO, gegevensconsistentie en beschikbaarheidsvereisten.

![Implementatie van meerdere regio](./media/cassandra-nodejs/cassandra-linux2.png)

Afbeelding2: Implementatie van meerdere landen/regio Cassandra

### <a name="network-integration"></a>Netwerkintegratie
Sets van virtuele machines geïmplementeerde tooprivate netwerken zich op twee gebieden communiceert met elkaar met behulp van een VPN-tunnel. Hallo VPN-tunnel maakt verbinding met twee software-gateways geleverd tijdens de implementatie van hello netwerkgegevens. Beide regio's hebben vergelijkbare netwerkarchitectuur in termen van de subnetten 'web' en 'data'; Azure-netwerken kunnen Hallo maken van zoveel subnetten indien nodig en ACL's van toepassing als nodig is voor netwerkbeveiliging. Inter data center communicatie latentie en Hallo economische gevolgen van Hallo network-verkeer moeten toobe beschouwd als tijdens het Hallo-clustertopologie ontwerpen.

### <a name="data-consistency-for-multi-data-center-deployment"></a>Consistentie van de gegevens voor de implementatie van meerdere Datacenter
Gedistribueerde implementaties moeten toobe op de hoogte van Hallo cluster topologie gevolgen voor de doorvoer en hoge beschikbaarheid. Hallo RF en Consistentieniveau nodig toobe geselecteerd manier die quorum Hallo afhankelijk niet van Hallo beschikbaarheid van alle Hallo datacenters.
Voor een systeem dat hoge consistentie, een LOCAL_QUORUM moet voor consistentieniveau (voor lees- en schrijfbewerkingen) ervoor dat Hallo lokale zorgt leest en schrijft worden nageleefd van lokale Hallo knooppunten gegevens asynchroon gerepliceerd toohello externe datacenters.  Tabel 2 ziet u details voor Hallo meerdere landen/regio cluster die worden beschreven in hello later up schrijven Hallo-configuratie.

**Twee regio Cassandra clusterconfiguratie**

| Cluster-Parameter | Waarde | Opmerkingen |
| --- | --- | --- |
| Het aantal knooppunten (N) |8 + 8 |Totaal aantal knooppunten in cluster Hallo |
| Replicatie Factor (RF) |3 |Aantal replica's van een bepaalde rij |
| Consistentieniveau (schrijven) |LOCAL_QUORUM [(sum(RF)/2) +1) = 4] Hallo resultaat van Hallo formule wordt omlaag afgerond |2-knooppunten wordt geschreven toohello eerste Datacenter synchroon; Hallo extra 2 knooppunten die nodig zijn voor het quorum wordt geschreven asynchroon toohello 2e Datacenter. |
| Consistentieniveau (lezen) |LOCAL_QUORUM ((RF/2) + 1) = 2 Hallo resultaat van Hallo formule wordt omlaag afgerond |Alleen aanvragen wordt van slechts één regio; voldaan 2 knooppunten worden gelezen voordat antwoord Hallo back toohello client wordt verzonden. |
| Een replicatiestrategie voor |Zie NetworkTopologyStrategy [gegevensreplicatie](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) in Cassandra-documentatie voor meer informatie |Hallo-implementatietopologie begrijpt en replica's op knooppunten geplaatst, zodat alle Hallo-replica's niet op Hallo dezelfde eindigen rack |
| Snitch |Zie GossipingPropertyFileSnitch [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) in Cassandra-documentatie voor meer informatie |NetworkTopologyStrategy maakt gebruik van een concept van snitch toounderstand Hallo-topologie. GossipingPropertyFileSnitch kunt beter bepalen in kaart brengen van elk knooppunt toodata center en rack. Hallo-cluster gebruikt roddels toopropagate vervolgens deze informatie. Dit is veel eenvoudiger in dynamische IP-instelling relatieve tooPropertyFileSnitch |

## <a name="hello-software-configuration"></a>Hallo SOFTWARECONFIGURATIE
Hallo volgende softwareversies worden gebruikt tijdens de implementatie van Hallo:

<table>
<tr><th>Software</th><th>Bron</th><th>Versie</th></tr>
<tr><td>JAVA RUNTIME ENVIRONMENT    </td><td>[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) </td><td>8U5</td></tr>
<tr><td>JNA    </td><td>[JNA](https://github.com/twall/jna) </td><td> 3.2.7</td></tr>
<tr><td>Cassandra</td><td>[Apache Cassandra 2.0.8](http://www.apache.org/dist/cassandra/2.0.8/apache-cassandra-2.0.8-bin.tar.gz)</td><td> 2.0.8</td></tr>
<tr><td>Ubuntu    </td><td>[Microsoft Azure](https://azure.microsoft.com/) </td><td>14.04 TNS</td></tr>
</table>

Omdat het downloaden van JRE handmatige instemming met de Oracle-licentie, toosimplify Hallo implementatie, alle vereiste software toohello bureaublad vereist voor het uploaden van later in Hallo Ubuntu-sjablooninstallatiekopie die we als een cluster met precursor toohello maakt Hallo downloaden de implementatie.

Hallo hierboven software downloaden naar een bekende downloadmap (bijvoorbeeld %TEMP%/downloads op Windows of ~/Downloads op de meeste Linux-distributies of Mac) op de lokale computer Hallo.

### <a name="create-ubuntu-vm"></a>VIRTUELE UBUNTU-MACHINE MAKEN
In deze stap van Hallo gaan we maken Ubuntu installatiekopie met de vereiste software Hallo zodat hello installatiekopie opnieuw kan worden gebruikt voor het inrichten van verschillende Cassandra knooppunten.  

#### <a name="step-1-generate-ssh-key-pair"></a>STAP 1: De SSH-sleutelpaar genereren
Azure heeft een openbare sleutel die is PEM of DER-gecodeerd op Hallo tijd inrichten X509 nodig. Een openbaar/persoonlijk sleutelpaar dat zich bevindt op het Hallo-instructies genereren tooUse SSH met Linux op Azure. Als u van plan toouse putty.exe als SSH-client op Windows of Linux bent, hebt u tooconvert hello PEM gecodeerd RSA persoonlijke sleutel tooPPK indeling met behulp van puttygen.exe; Hallo instructies hiervoor vindt u in Hallo hierboven webpagina.

#### <a name="step-2-create-ubuntu-template-vm"></a>STAP 2: Ubuntu sjabloon VM maken
toocreate hello sjabloon VM, meld u aan bij hello Azure classic portal en gebruik Hallo volgende volgorde: klik op Nieuw, COMPUTE, virtuele MACHINE, FROM GALERIE, UBUNTU, Ubuntu Server 14.04 TNS, en klik vervolgens op pijl-rechts Hallo. Voor een zelfstudie waarin wordt beschreven hoe toocreate een Linux-VM zien een virtuele Machine waarop Linux maken.

Voer de volgende informatie op het scherm Hallo 'Virtuele-machineconfiguratie' #1 Hallo:

<table>
<tr><th>VELDNAAM              </td><td>       WAARDE VAN VELD               </td><td>         OPMERKINGEN                </td><tr>
<tr><td>RELEASEDATUM VERSIE    </td><td> Selecteer een datum in Hallo vervolgkeuzelijst</td><td></td><tr>
<tr><td>NAAM VAN VIRTUELE MACHINE    </td><td> Cass-sjabloon                   </td><td> Dit is Hallo hostnaam Hallo VM </td><tr>
<tr><td>LAAG                     </td><td> STANDARD                           </td><td> Laat de standaardwaarde Hallo              </td><tr>
<tr><td>GROOTTE                     </td><td> A1                              </td><td>Selecteer Hallo die VM op basis van Hallo i/o-behoeften; voor dit doel laat Hallo standaardwaarde </td><tr>
<tr><td> NIEUWE GEBRUIKERSNAAM             </td><td> localadmin                       </td><td> 'admin' is een gereserveerde gebruikersnaam in Ubuntu 12. xx en na</td><tr>
<tr><td> VERIFICATIE         </td><td> Klik op het selectievakje                 </td><td>Controleer als u wilt dat toosecure met een SSH-sleutel </td><tr>
<tr><td> CERTIFICAAT             </td><td> bestandsnaam van de openbare-sleutelcertificaat Hallo </td><td> De openbare sleutel Hallo eerder gegenereerde gebruiken</td><tr>
<tr><td> Nieuw wachtwoord    </td><td> sterk wachtwoord </td><td> </td><tr>
<tr><td> Wachtwoord bevestigen    </td><td> sterk wachtwoord </td><td></td><tr>
</table>

Voer de volgende informatie op het scherm Hallo 'Virtuele-machineconfiguratie' #2 Hallo:

<table>
<tr><th>VELDNAAM             </th><th> WAARDE VAN VELD                       </th><th> OPMERKINGEN                                 </th></tr>
<tr><td> CLOUDSERVICE    </td><td> Maak een nieuwe cloudservice    </td><td>Cloudservice is een container compute-bronnen zoals virtuele machines</td></tr>
<tr><td> DNS-NAAM VAN CLOUD-SERVICE    </td><td>Ubuntu template.cloudapp.net    </td><td>Geef de naam van een machine agnostisch load balancer</td></tr>
<tr><td> REGIO/AFFINITEITSGROEP/VIRTUEEL NETWERK </td><td>    VS - west    </td><td> Selecteer een regio van waaruit de toegang tot Hallo Cassandra cluster van uw webtoepassingen</td></tr>
<tr><td>STORAGE-ACCOUNT </td><td>    Standaard gebruiken    </td><td>Hallo standaardopslagaccount of een vooraf gemaakte opslagaccount gebruiken in een bepaald gebied</td></tr>
<tr><td>BESCHIKBAARHEIDSSET </td><td>    Geen </td><td>    Laat dit veld leeg</td></tr>
<tr><td>EINDPUNTEN    </td><td>Standaard gebruiken </td><td>    Hallo-standaard SSH-configuratie gebruiken </td></tr>
</table>

Pijl-rechts, Hallo standaardinstellingen laten staan op het welkomstscherm #3 en klik op Hallo 'selectievakje' knop toocomplete Hallo VM inrichtingsproces. Na een paar minuten moet Hallo VM met Hallo naam 'ubuntu-sjabloon' status 'actief'.

### <a name="install-hello-necessary-software"></a>Hallo benodigde SOFTWARE installeren
#### <a name="step-1-upload-tarballs"></a>STAP 1: Het uploaden van tarballs
Gebruik scp of pscp, kopie Hallo eerder gedownloade software te ~ / downloads directory Hallo volgende opdracht gebruiken:

##### <a name="pscp-server-jre-8u5-linux-x64targz-localadminhk-cas-templatecloudappnethomelocaladmindownloadsserver-jre-8u5-linux-x64targz"></a>pscp server-jre-8u5-linux-x64.tar.gzlocaladmin@hk-cas-template.cloudapp.net:/home/localadmin/downloads/server-jre-8u5-linux-x64.tar.gz
Herhaal Hallo hierboven opdracht voor JRE ook als voor Hallo Cassandra bits.

#### <a name="step-2-prepare-hello-directory-structure-and-extract-hello-archives"></a>STAP 2: Hallo mapstructuur voorbereiden en Hallo archieven uitpakken
Meld u aan bij Hallo VM en Hallo mapstructuur maken en software extraheren als supergebruiker met onderstaande Hallo bash-script:

    #!/bin/bash
    CASS_INSTALL_DIR="/opt/cassandra"
    JRE_INSTALL_DIR="/opt/java"
    CASS_DATA_DIR="/var/lib/cassandra"
    CASS_LOG_DIR="/var/log/cassandra"
    DOWNLOADS_DIR="~/downloads"
    JRE_TARBALL="server-jre-8u5-linux-x64.tar.gz"
    CASS_TARBALL="apache-cassandra-2.0.8-bin.tar.gz"
    SVC_USER="localadmin"

    RESET_ERROR=1
    MKDIR_ERROR=2

    reset_installation ()
    {
       rm -rf $CASS_INSTALL_DIR 2> /dev/null
       rm -rf $JRE_INSTALL_DIR 2> /dev/null
       rm -rf $CASS_DATA_DIR 2> /dev/null
       rm -rf $CASS_LOG_DIR 2> /dev/null
    }
    make_dir ()
    {
       if [ -z "$1" ]
       then
          echo "make_dir: invalid directory name"
          exit $MKDIR_ERROR
       fi

       if [ -d "$1" ]
       then
          echo "make_dir: directory already exists"
          exit $MKDIR_ERROR
       fi

       mkdir $1 2>/dev/null
       if [ $? != 0 ]
       then
          echo "directory creation failed"
          exit $MKDIR_ERROR
       fi
    }

    unzip()
    {
       if [ $# == 2 ]
       then
          tar xzf $1 -C $2
       else
          echo "archive error"
       fi

    }

    if [ -n "$1" ]
    then
       SVC_USER=$1
    fi

    reset_installation
    make_dir $CASS_INSTALL_DIR
    make_dir $JRE_INSTALL_DIR
    make_dir $CASS_DATA_DIR
    make_dir $CASS_LOG_DIR

    #unzip JRE and Cassandra
    unzip $HOME/downloads/$JRE_TARBALL $JRE_INSTALL_DIR
    unzip $HOME/downloads/$CASS_TARBALL $CASS_INSTALL_DIR

    #Change hello ownership toohello service credentials

    chown -R $SVC_USER:$GROUP $CASS_DATA_DIR
    chown -R $SVC_USER:$GROUP $CASS_LOG_DIR
    echo "edit /etc/profile tooadd JRE toohello PATH"
    echo "installation is complete"


Als u dit script in vim venster plakt, zorg ervoor dat tooremove Hallo regeleinde return ('\r ") met behulp van de volgende opdracht Hallo:

    tr -d '\r' <infile.sh >outfile.sh

#### <a name="step-3-edit-etcprofile"></a>Stap 3: Enzovoort/profiel bewerken
Hallo volgende Hallo eind toevoegen:

    JAVA_HOME=/opt/java/jdk1.8.0_05
    CASS_HOME= /opt/cassandra/apache-cassandra-2.0.8
    PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$CASS_HOME/bin
    export JAVA_HOME
    export CASS_HOME
    export PATH

#### <a name="step-4-install-jna-for-production-systems"></a>Stap 4: Installatie JNA voor productiesystemen
Gebruik Hallo volgende opdracht sequence: Hallo volgende opdracht zal installeren jna-3.2.7.jar en jna-platform-3.2.7.jar too/usr/share.java directory sudo apt get-libjna java installeren

Symbolische koppelingen in $CASS_HOME/lib directory maken, zodat het opstartscript Cassandra deze potten kunt vinden:

    ln -s /usr/share/java/jna-3.2.7.jar $CASS_HOME/lib/jna.jar

    ln -s /usr/share/java/jna-platform-3.2.7.jar $CASS_HOME/lib/jna-platform.jar

#### <a name="step-5-configure-cassandrayaml"></a>Stap 5: Cassandra.yaml configureren
Cassandra.yaml op elke virtuele machine tooreflect configuratie nodig is voor alle virtuele machines van het Hallo [we zullen dit aanpassen tijdens het inrichten van werkelijke Hallo] bewerken:

<table>
<tr><th>Veldnaam   </th><th> Waarde  </th><th>    Opmerkingen </th></tr>
<tr><td>clusternaam </td><td>    'CustomerService'    </td><td> Hallo-naam die overeenkomt met uw implementatie gebruiken</td></tr>
<tr><td>listen_address    </td><td>[laat dit veld leeg]    </td><td> Verwijderen van 'localhost' </td></tr>
<tr><td>rpc_addres   </td><td>[laat dit veld leeg]    </td><td> Verwijderen van 'localhost' </td></tr>
<tr><td>zaden    </td><td>"10.1.2.4, 10.1.2.6, 10.1.2.8"    </td><td>Lijst met alle Hallo IP-adressen die zijn aangewezen als basis.</td></tr>
<tr><td>endpoint_snitch </td><td> org.apache.cassandra.locator.GossipingPropertyFileSnitch </td><td> Dit wordt gebruikt door Hallo NetworkTopologyStrateg voor afleiden Hallo datacenter en Hallo rack Hallo VM</td></tr>
</table>

#### <a name="step-6-capture-hello-vm-image"></a>Stap 6: Hallo VM-installatiekopie vastleggen
Meld u aan bij Hallo virtuele machine met behulp van Hallo-hostnaam (hk-cas-template.cloudapp.net) en Hallo persoonlijke SSH-sleutel eerder hebt gemaakt. Zie hoe tooUse SSH met Linux op Azure voor meer informatie over hoe toolog bij het gebruik van Hallo opdracht ssh of putty.exe.

Hallo reeks acties toocapture Hallo installatiekopie volgende uitvoeren:

##### <a name="1-deprovision"></a>1. Identiteitsgegevens
Hallo-opdracht gebruiken ' sudo waagent-deprovision + user ' tooremove specifieke gegevens van virtuele Machine-exemplaar. Zie voor [hoe tooCapture virtuele Linux-Machine](capture-image.md) tooUse als een sjabloon om meer details op Hallo installatiekopie vastleggen.

##### <a name="2-shutdown-hello-vm"></a>2: afsluiten Hallo VM
Zorg ervoor dat de virtuele machine Hallo is geselecteerd en klik op de koppeling voor het afsluiten van Hallo onder opdrachtbalk Hallo.

##### <a name="3-capture-hello-image"></a>3: Hallo vastleginstallatiekopie
Zorg ervoor dat de virtuele machine Hallo is geselecteerd en klik op de koppeling voor het VASTLEGGEN van Hallo onder opdrachtbalk Hallo. In het volgende scherm hello, geven de naam van een INSTALLATIEKOPIE (bijvoorbeeld hk-cas-2-08-ub-14-04-2014071), beschrijving van afbeelding van toepassing en op Hallo 'selectievakje' markeren toofinish Hallo vastleggen.

Dit duurt een paar seconden en Hallo installatiekopie moet beschikbaar zijn in de sectie Mijn afbeeldingen van Hallo installatiekopie galerie. Hallo bron-VM wordt automatisch verwijderd nadat het Hallo-installatiekopie wordt vastgelegd. 

## <a name="single-region-deployment-process"></a>Implementatieproces voor één regio
**Stap 1: Maak een virtueel netwerk Hallo** Meld u aan bij hello Azure-portal en maak een virtueel netwerk (klassiek) met Hallo kenmerken weergegeven in de volgende tabel Hallo. Zie [maken van een virtueel netwerk (klassiek), hello Azure-portal met](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) voor gedetailleerde stappen voor het Hallo-proces.      

<table>
<tr><th>De naam van de VM-kenmerk</th><th>Waarde</th><th>Opmerkingen</th></tr>
<tr><td>Naam</td><td>vnet-cass-west-ons</td><td></td></tr>
<tr><td>Regio</td><td>VS - west</td><td></td></tr>
<tr><td>DNS-Servers</td><td>Geen</td><td>Negeer deze melding als er niet met behulp van een DNS-Server</td></tr>
<tr><td>Adresruimte</td><td>10.1.0.0/16</td><td></td></tr>    
<tr><td>IP-beginadres</td><td>10.1.0.0</td><td></td></tr>    
<tr><td>CIDR </td><td>/16 (65531)</td><td></td></tr>
</table>

Hallo volgende subnetten toevoegen:

<table>
<tr><th>Naam</th><th>IP-beginadres</th><th>CIDR</th><th>Opmerkingen</th></tr>
<tr><td>Web</td><td>10.1.1.0</td><td>/24 (251)</td><td>Subnet voor de webfarm Hallo</td></tr>
<tr><td>Gegevens</td><td>10.1.2.0</td><td>/24 (251)</td><td>Subnet voor de databaseknooppunten Hallo</td></tr>
</table>

Gegevens en Web subnetten kunnen worden beveiligd via netwerkbeveiligingsgroepen Hallo dekking waarvan buiten het bereik van dit artikel is.  

**Stap 2: Inrichten van virtuele Machines** met Hallo-installatiekopie die eerder is gemaakt, wordt gemaakt na van virtuele machines in de cloud Hallo Hallo server 'hk-c-svc-west' en maak ze afhankelijk van de respectieve subnetten toohello zoals hieronder wordt weergegeven:

<table>
<tr><th>Computernaam    </th><th>Subnet    </th><th>IP-adres    </th><th>Beschikbaarheidsset</th><th>DC/Rack</th><th>Seed?</th></tr>
<tr><td>HK-c1-west-ons    </td><td>Gegevens    </td><td>10.1.2.4    </td><td>HK-c-uit-1    </td><td>DC = WESTUS rack rack1 = </td><td>Ja</td></tr>
<tr><td>HK-c2-west-ons    </td><td>Gegevens    </td><td>10.1.2.5    </td><td>HK-c-uit-1    </td><td>DC = WESTUS rack rack1 =    </td><td>Nee </td></tr>
<tr><td>HK-c3-west-ons    </td><td>Gegevens    </td><td>10.1.2.6    </td><td>HK-c-uit-1    </td><td>DC = WESTUS rack rack2 =    </td><td>Ja</td></tr>
<tr><td>HK-c4-west-ons    </td><td>Gegevens    </td><td>10.1.2.7    </td><td>HK-c-uit-1    </td><td>DC = WESTUS rack rack2 =    </td><td>Nee </td></tr>
<tr><td>HK-c5-west-ons    </td><td>Gegevens    </td><td>10.1.2.8    </td><td>HK-c-uit-2    </td><td>DC = WESTUS rack rack3 =    </td><td>Ja</td></tr>
<tr><td>HK-c6-west-ons    </td><td>Gegevens    </td><td>10.1.2.9    </td><td>HK-c-uit-2    </td><td>DC = WESTUS rack rack3 =    </td><td>Nee </td></tr>
<tr><td>HK-c7-west-ons    </td><td>Gegevens    </td><td>10.1.2.10    </td><td>HK-c-uit-2    </td><td>DC = WESTUS rack rack4 =    </td><td>Ja</td></tr>
<tr><td>HK-c8-west-ons    </td><td>Gegevens    </td><td>10.1.2.11    </td><td>HK-c-uit-2    </td><td>DC = WESTUS rack rack4 =    </td><td>Nee </td></tr>
<tr><td>HK-w1-west-ons    </td><td>Web    </td><td>10.1.1.4    </td><td>HK-w-uit-1    </td><td>                       </td><td>N.v.t.</td></tr>
<tr><td>HK-w2-west-ons    </td><td>Web    </td><td>10.1.1.5    </td><td>HK-w-uit-1    </td><td>                       </td><td>N.v.t.</td></tr>
</table>

Maken van een Hallo boven lijst met virtuele machines moeten Hallo volgende proces:

1. Een lege cloudservice maken in een bepaald gebied
2. Een virtuele machine uit Hallo eerder vastgelegde installatiekopie maken en deze te koppelen toohello virtueel netwerk gemaakt eerder; Herhaal deze stap voor alle Hallo VM 's
3. Toevoegen van een interne load balancer toohello cloud-service en koppelt u dit subnet toohello "gegevens"
4. Voor elke virtuele machine die eerder is gemaakt, voegt u een eindpunt voor de taakverdeling voor thrift-verkeer via een interne load balancer voor taakverdeling set verbonden toohello eerder hebt gemaakt

Hallo hierboven proces kan worden uitgevoerd met behulp van de klassieke Azure-portal; Gebruik een Windows-machine (gebruik een VM op Azure als u geen toegang tot tooa Windows-computer), automatisch gebruikt voor het volgende PowerShell-script tooprovision Hallo alle 8 VM's.

**Lijst met 1: PowerShell-script voor het inrichten van virtuele machines**

        #Tested with Azure Powershell - November 2014
        #This powershell script deployes a number of VMs from an existing image inside an Azure region
        #Import your Azure subscription into hello current Powershell session before proceeding
        #hello process: 1. create Azure Storage account, 2. create virtual network, 3.create hello VM template, 2. crate a list of VMs from hello template

        #fundamental variables - change these tooreflect your subscription
        $country="us"; $region="west"; $vnetName = "your_vnet_name";$storageAccount="your_storage_account"
        $numVMs=8;$prefix = "hk-cass";$ilbIP="your_ilb_ip"
        $subscriptionName = "Azure_subscription_name";
        $vmSize="ExtraSmall"; $imageName="your_linux_image_name"
        $ilbName="ThriftInternalLB"; $thriftEndPoint="ThriftEndPoint"

        #generated variables
        $serviceName = "$prefix-svc-$region-$country"; $azureRegion = "$region $country"

        $vmNames = @()
        for ($i=0; $i -lt $numVMs; $i++)
        {
           $vmNames+=("$prefix-vm"+($i+1) + "-$region-$country" );
        }

        #select an Azure subscription already imported into Powershell session
        Select-AzureSubscription -SubscriptionName $subscriptionName -Current
        Set-AzureSubscription -SubscriptionName $subscriptionName -CurrentStorageAccountName $storageAccount

        #create an empty cloud service
        New-AzureService -ServiceName $serviceName -Label "hkcass$region" -Location $azureRegion
        Write-Host "Created $serviceName"

        $VMList= @()   # stores hello list of azure vm configuration objects
        #create hello list of VMs
        foreach($vmName in $vmNames)
        {
           $VMList += New-AzureVMConfig -Name $vmName -InstanceSize ExtraSmall -ImageName $imageName |
           Add-AzureProvisioningConfig -Linux -LinuxUser "localadmin" -Password "Local123" |
           Set-AzureSubnet "data"
        }

        New-AzureVM -ServiceName $serviceName -VNetName $vnetName -VMs $VMList

        #Create internal load balancer
        Add-AzureInternalLoadBalancer -ServiceName $serviceName -InternalLoadBalancerName $ilbName -SubnetName "data" -StaticVNetIPAddress "$ilbIP"
        Write-Host "Created $ilbName"
        #Add add hello thrift endpoint toohello internal load balancer for all hello VMs
        foreach($vmName in $vmNames)
        {
            Get-AzureVM -ServiceName $serviceName -Name $vmName |
                Add-AzureEndpoint -Name $thriftEndPoint -LBSetName "ThriftLBSet" -Protocol tcp -LocalPort 9160 -PublicPort 9160 -ProbePort 9160 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ilbName |
                Update-AzureVM

            Write-Host "created $vmName"     
        }

**Stap 3: Cassandra op elke virtuele machine configureren**

Meld u aan bij Hallo VM en Voer Hallo volgende stappen:

* $CASS_HOME/conf/cassandra-rackdc.properties toospecify Hallo data center en rack-eigenschappen bewerken:
  
       dc =EASTUS, rack =rack1
* Bewerk cassandra.yaml tooconfigure seed-knooppunten zoals hieronder:
  
       Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10"

**Stap 4: Hallo virtuele machines starten en Hallo cluster testen**

Meld u aan bij een van Hallo-knooppunten (bijvoorbeeld hk-c1-west-us) en Voer Hallo toosee Hallo Opdrachtstatus van Hallo-cluster te volgen:

       nodetool –h 10.1.2.4 –p 7199 status

U ziet Hallo weergave vergelijkbare toohello een hieronder voor een cluster met 8 knooppunten:

<table>
<tr><th>Status</th><th>Adres    </th><th>Belasting    </th><th>Tokens    </th><th>Eigenaar is van </th><th>Host-ID    </th><th>Rack</th></tr>
<tr><th>ONGEDAAN MAKEN    </td><td>10.1.2.4     </td><td>87.81 KB    </td><td>256    </td><td>38.0%    </td><td>GUID (verwijderd)</td><td>rack1</td></tr>
<tr><th>ONGEDAAN MAKEN    </td><td>10.1.2.5     </td><td>41.08 KB    </td><td>256    </td><td>68.9%    </td><td>GUID (verwijderd)</td><td>rack1</td></tr>
<tr><th>ONGEDAAN MAKEN    </td><td>10.1.2.6     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (verwijderd)</td><td>rack2</td></tr>
<tr><th>ONGEDAAN MAKEN    </td><td>10.1.2.7     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (verwijderd)</td><td>rack2</td></tr>
<tr><th>ONGEDAAN MAKEN    </td><td>10.1.2.8     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (verwijderd)</td><td>rack3</td></tr>
<tr><th>ONGEDAAN MAKEN    </td><td>10.1.2.9     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (verwijderd)</td><td>rack3</td></tr>
<tr><th>ONGEDAAN MAKEN    </td><td>10.1.2.10     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (verwijderd)</td><td>rack4</td></tr>
<tr><th>ONGEDAAN MAKEN    </td><td>10.1.2.11     </td><td>55.29 KB    </td><td>256    </td><td>68.8%    </td><td>GUID (verwijderd)</td><td>rack4</td></tr>
</table>

## <a name="test-hello-single-region-cluster"></a>Test Hallo één regio-Cluster
Volgende stappen tootest Hallo cluster Hallo gebruiken:

1. Hallo IP-adres van Hallo interne load balancer (bijvoorbeeld met de Hallo Powershell-opdracht Get-AzureInternalLoadbalancer commandlet, ophalen  10.1.2.101). Hallo-syntaxis van Hallo-opdracht wordt hieronder weergegeven: Get-AzureLoadbalancer – ServiceName 'hk-c-svc-west-us' [Hallo geeft details weer van Hallo interne load balancer samen met het IP-adres]
2. Meld u aan bij de webfarm Hallo VM (bijvoorbeeld hk-w1-west-us) met Putty of ssh
3. Uitvoeren van $CASS_HOME/bin/cqlsh 10.1.2.101 9160
4. Gebruik Hallo CQL opdrachten tooverify volgen als Hallo cluster werkt:
   
     Maak met KEYSPACE customers_ks met replicatie = {'class': 'SimpleStrategy', 'replication_factor': 3};   Gebruik customers_ks;   MAKEN van tabel Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INVOEGEN in Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INVOEGEN in Customers(customer_id, firstname, lastname) waarden (2, 'ANS', 'De Vries');
   
     Selecteer * van klanten;

U ziet een scherm zoals Hallo hieronder:

<table>
  <tr><th> customer_id </th><th> Voornaam </th><th> Achternaam </th></tr>
  <tr><td> 1 </td><td> John </td><td> De Vries </td></tr>
  <tr><td> 2 </td><td> ANS </td><td> De Vries </td></tr>
</table>

Houd er rekening mee dat Hallo keyspace gemaakt in stap 4 SimpleStrategy gebruikt met een replication_factor van 3. SimpleStrategy wordt aanbevolen voor één data center-implementaties terwijl NetworkTopologyStrategy voor meerdere data center-implementaties. Een replication_factor van 3, tolerantie voor knooppuntfouten krijgt.

## <a id="tworegion"></a>Meerdere landen/regio-implementatieproces
Zal gebruikmaken van de implementatie van Hallo één regio is voltooid en herhaal Hallo dezelfde verwerken voor het installeren van de tweede regio Hallo. Hallo belangrijkste verschil tussen één Hallo en distributie naar meerdere regio is Hallo VPN-tunnel instellen voor de communicatie tussen regio; We beginnen met netwerkinstallatie hello, Hallo virtuele machines inrichten en Cassandra configureren.

### <a name="step-1-create-hello-virtual-network-at-hello-2nd-region"></a>Stap 1: Hallo virtueel netwerk maken op Hallo 2e regio
Meld u aan bij de klassieke Azure-portal Hallo en maak een virtueel netwerk met Hallo kenmerken weergeven in de tabel Hallo. Zie [Cloud-Only virtueel netwerk configureren in de klassieke Azure-portal Hallo](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) voor gedetailleerde stappen voor het Hallo-proces.      

<table>
<tr><th>Naam van kenmerk    </th><th>Waarde    </th><th>Opmerkingen</th></tr>
<tr><td>Naam    </td><td>vnet-cass-Oost-ons</td><td></td></tr>
<tr><td>Regio    </td><td>VS - oost</td><td></td></tr>
<tr><td>DNS-Servers        </td><td></td><td>Negeer deze melding als er niet met behulp van een DNS-Server</td></tr>
<tr><td>Een punt-naar-site-VPN configureren</td><td></td><td>        Negeer deze melding</td></tr>
<tr><td>Configureer een site-to-site VPN</td><td></td><td>        Negeer deze melding</td></tr>
<tr><td>Adresruimte    </td><td>10.2.0.0/16</td><td></td></tr>
<tr><td>IP-beginadres    </td><td>10.2.0.0    </td><td></td></tr>
<tr><td>CIDR    </td><td>/16 (65531)</td><td></td></tr>
</table>

Hallo volgende subnetten toevoegen:

<table>
<tr><th>Naam    </th><th>IP-beginadres    </th><th>CIDR    </th><th>Opmerkingen</th></tr>
<tr><td>Web    </td><td>10.2.1.0    </td><td>/24 (251)    </td><td>Subnet voor de webfarm Hallo</td></tr>
<tr><td>Gegevens    </td><td>10.2.2.0    </td><td>/24 (251)    </td><td>Subnet voor de databaseknooppunten Hallo</td></tr>
</table>


### <a name="step-2-create-local-networks"></a>Stap 2: Lokale netwerken maken
Een lokaal netwerk in Azure virtuele netwerken is een proxy-adresruimte die is toegewezen tooa externe site, met inbegrip van een privécloud of een andere Azure-regio. Deze adresruimte proxy is gebonden tooa externe gateway voor routering netwerk toohello rechts networking bestemmingen. Zie [configureren van een VNet tooVNet verbinding](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) voor Hallo instructies voor het VNET-naar-VNET-verbinding tot stand brengen.

Maak twee lokale netwerken per Hallo volgende details:

| Netwerknaam | VPN-Gateway-adres | Adresruimte | Opmerkingen |
| --- | --- | --- | --- |
| HK-lnet-map-to-East-US |23.1.1.1 |10.2.0.0/16 |Geef een tijdelijke aanduiding gatewayadres tijdens het maken van Hallo lokale netwerk. Hallo echte gatewayadres wordt gevuld wanneer Hallo gateway is gemaakt. Zorg ervoor dat Hallo-adresruimte exact overeenkomt met Hallo respectieve externe VNET; in dit geval hello VNET gemaakt in Hallo regio VS-Oost. |
| HK-lnet-map-to-West-US |23.2.2.2 |10.1.0.0/16 |Geef een tijdelijke aanduiding gatewayadres tijdens het maken van Hallo lokale netwerk. Hallo echte gatewayadres wordt gevuld wanneer Hallo gateway is gemaakt. Zorg ervoor dat Hallo-adresruimte exact overeenkomt met Hallo respectieve externe VNET; in dit geval hello VNET gemaakt in Hallo regio VS-West. |

### <a name="step-3-map-local-network-toohello-respective-vnets"></a>Stap 3: Kaart "Local" netwerk toohello respectieve VNETs
Van Hallo klassieke Azure-portal, selecteer elke vnet, klik op 'Configureren', 'Connect toohello lokale netwerk' controleren, en selecteer Hallo lokale netwerken per Hallo volgende details:

| Virtual Network | Lokale netwerk |
| --- | --- |
| HK-vnet-west-ons |HK-lnet-map-to-East-US |
| HK-vnet-Oost-ons |HK-lnet-map-to-West-US |

### <a name="step-4-create-gateways-on-vnet1-and-vnet2"></a>Stap 4: Gateways op VNET1 en VNET2 maken
Hallo-dashboard van de virtuele netwerken van beide hello, klik op GATEWAY maken waarmee Hallo VPN-gateway inrichtingsproces wordt geactiveerd. Na een paar minuten Hallo dashboard van elke virtuele netwerk moeten de werkelijke gatewayadres Hallo worden weergegeven.

### <a name="step-5-update-local-networks-with-hello-respective-gateway-addresses"></a>Stap 5: Update "Local" netwerken met Hallo respectieve ' ' gatewayadressen
Beide gateways Hallo lokale netwerken tooreplace Hallo tijdelijke aanduiding voor gateway IP-adres met Hallo echte IP-adres van Hallo alleen ingericht bewerken. Gebruik Hallo toewijzing te volgen:

<table>
<tr><th>Lokale netwerk    </th><th>Gateway voor een virtueel netwerk</th></tr>
<tr><td>HK-lnet-map-to-East-US </td><td>De gateway van hk-vnet-west-ons</td></tr>
<tr><td>HK-lnet-map-to-West-US </td><td>De gateway van hk-vnet-Oost-ons</td></tr>
</table>

### <a name="step-6-update-hello-shared-key"></a>Stap 6: Update Hallo gedeelde sleutel
Gebruik Hallo volgende Powershell-script tooupdate Hallo IPSec-sleutel van elke VPN-gateway [Hallo verjaardagen sleutel gebruiken voor beide gateways Hallo]: Set-AzureVNetGatewayKey - VNetName hk-vnet-Oost-ons - LocalNetworkSiteName hk-lnet-map-to-west-us - SharedKey D9E76BKK Set-AzureVNetGatewayKey - VNetName hk-vnet-west-ons - LocalNetworkSiteName hk-lnet-map-to-east-us - SharedKey D9E76BKK

### <a name="step-7-establish-hello-vnet-to-vnet-connection"></a>Stap 7: Hallo VNET-naar-VNET-verbinding maken
Gebruik vanaf Hallo klassieke Azure-portal, Hallo 'DASHBOARD' menu van zowel Hallo virtuele netwerken tooestablish gateway-naar-gateway-verbinding. Hallo 'CONNECT' menu-items in Hallo onderste werkbalk gebruiken. Na een paar minuten moet Hallo dashboard Hallo Verbindingsdetails grafisch weergeven.

### <a name="step-8-create-hello-virtual-machines-in-region-2"></a>Stap 8: Maak Hallo virtuele machines in regio #2
Hallo Ubuntu installatiekopie maken zoals beschreven in de regio #1 implementatie door de volgende Hallo dezelfde stappen of kopieer Hallo installatiekopie VHD-bestand toohello Azure storage-account zich in de regio #2 en Hallo installatiekopie maken. Deze afbeelding niet gebruiken en maken van de volgende lijst met virtuele machines in een nieuwe cloudservice hk-c-svc-Oost-ons Hallo:

| Computernaam | Subnet | IP-adres | Beschikbaarheidsset | DC/Rack | Seed? |
| --- | --- | --- | --- | --- | --- |
| HK-c1-Oost-ons |Gegevens |10.2.2.4 |HK-c-uit-1 |DC = EASTUS rack rack1 = |Ja |
| HK-c2-Oost-ons |Gegevens |10.2.2.5 |HK-c-uit-1 |DC = EASTUS rack rack1 = |Nee |
| HK-c3-Oost-ons |Gegevens |10.2.2.6 |HK-c-uit-1 |DC = EASTUS rack rack2 = |Ja |
| HK-c5-Oost-ons |Gegevens |10.2.2.8 |HK-c-uit-2 |DC = EASTUS rack rack3 = |Ja |
| HK-c6-Oost-ons |Gegevens |10.2.2.9 |HK-c-uit-2 |DC = EASTUS rack rack3 = |Nee |
| HK-c7-Oost-ons |Gegevens |10.2.2.10 |HK-c-uit-2 |DC = EASTUS rack rack4 = |Ja |
| HK-c8-Oost-ons |Gegevens |10.2.2.11 |HK-c-uit-2 |DC = EASTUS rack rack4 = |Nee |
| HK-w1-Oost-ons |Web |10.2.1.4 |HK-w-uit-1 |N.v.t. |N.v.t. |
| HK-w2-Oost-ons |Web |10.2.1.5 |HK-w-uit-1 |N.v.t. |N.v.t. |

Volg dezelfde Hallo instructies als regio #1 maar 10.2.xxx.xxx-adresruimte wordt gebruikt.

### <a name="step-9-configure-cassandra-on-each-vm"></a>Stap 9: Cassandra op elke virtuele machine configureren
Meld u aan bij Hallo VM en Voer Hallo volgende stappen:

1. $CASS_HOME/conf/cassandra-rackdc.properties toospecify Hallo data center en rack eigenschappen bewerken in Hallo indeling: dc = EASTUS rack rack1 =
2. Cassandra.yaml tooconfigure seed-knooppunten bewerken: zaden: '10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10,10.2.2.4,10.2.2.6,10.2.2.8,10.2.2.10'

### <a name="step-10-start-cassandra"></a>Stap 10: Cassandra starten
Meld u aan bij elke virtuele machine en Cassandra starten op de achtergrond Hallo door het uitvoeren van de volgende opdracht Hallo: $CASS_HOME/bin/cassandra

## <a name="test-hello-multi-region-cluster"></a>Test Hallo meerdere landen/regio-Cluster
Nu is Cassandra geïmplementeerde too16 knooppunten met 8 knooppunten in elke Azure-regio. Deze knooppunten zijn in dezelfde algemene clusternaam Hallo en Hallo seed knooppuntconfiguratie cluster Hallo. Hallo proces tootest Hallo cluster volgende gebruiken:

### <a name="step-1-get-hello-internal-load-balancer-ip-for-both-hello-regions-using-powershell"></a>Stap 1: U Hallo interne load balancer IP-adres voor beide Hallo-regio's met behulp van PowerShell
* Get-AzureInternalLoadbalancer - ServiceName 'hk-c-svc-west-us'
* Get-AzureInternalLoadbalancer - ServiceName 'hk-c-svc-Oost-us'  
  
    Houd er rekening mee Hallo IP-adressen (bijvoorbeeld - 10.1.2.101, Oost - west 10.2.2.101) weergegeven.

### <a name="step-2-execute-hello-following-in-hello-west-region-after-logging-into-hk-w1-west-us"></a>Stap 2: Hallo volgende in de regio west Hallo uitvoeren nadat de aanmelding bij hk-w1-west-ons
1. Uitvoeren van $CASS_HOME/bin/cqlsh 10.1.2.101 9160
2. Hallo na CQL opdrachten uitvoeren:
   
     Maak met KEYSPACE customers_ks met replicatie = {'class': 'NetworkToplogyStrategy', 'WESTUS': 3, EASTUS: 3};   Gebruik customers_ks;   MAKEN van tabel Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INVOEGEN in Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INVOEGEN in Customers(customer_id, firstname, lastname) waarden (2, 'ANS', 'De Vries');   Selecteer * van klanten;

U ziet een scherm zoals Hallo hieronder:

| customer_id | Voornaam | Achternaam |
| --- | --- | --- |
| 1 |John |De Vries |
| 2 |ANS |De Vries |

### <a name="step-3-execute-hello-following-in-hello-east-region-after-logging-into-hk-w1-east-us"></a>Stap 3: Voor het uitvoeren van Hallo volgende in de regio Oost Hallo na de aanmelding bij hk-w1-Oost-ons:
1. Uitvoeren van $CASS_HOME/bin/cqlsh 10.2.2.101 9160
2. Hallo na CQL opdrachten uitvoeren:
   
     Gebruik customers_ks;   MAKEN van tabel Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INVOEGEN in Customers(customer_id, firstname, lastname) VALUES(1, 'John', 'Doe');   INVOEGEN in Customers(customer_id, firstname, lastname) waarden (2, 'ANS', 'De Vries');   Selecteer * van klanten;

U ziet Hallo dezelfde zoals te zien voor de regio West Hallo weergeven:

| customer_id | Voornaam | Achternaam |
| --- | --- | --- |
| 1 |John |De Vries |
| 2 |ANS |De Vries |

Enkele meer invoegingen uitvoeren en Zie dat de gerepliceerde toowest krijgen-ons deel uit van het Hallo-cluster.

## <a name="test-cassandra-cluster-from-nodejs"></a>Cassandra Testcluster met Node.js
Eerder in Hallo 'web' laag met behulp van een virtuele Linux-machines Hallo gemaakt, wordt een eenvoudige Node.js tooread Hallo eerder ingevoegd scriptgegevens wordt uitgevoerd

**Stap 1: Node.js en Cassandra-Client installeren**

1. Installeer Node.js en npm
2. Knooppunt pakket 'cassandra-client' installeren met npm
3. Hallo volgende script op Hallo shell-prompt waarin Hallo json-tekenreeks van de gegevens opgehaald Hallo uitvoeren:
   
        var pooledCon = require('cassandra-client').PooledConnection;
        var ksName = "custsupport_ks";
        var cfName = "customers_cf";
        var hostList = ['internal_loadbalancer_ip:9160'];
        var ksConOptions = { hosts: hostList,
                             keyspace: ksName, use_bigints: false };
   
        function createKeyspace(callback){
           var cql = 'CREATE KEYSPACE ' + ksName + ' WITH strategy_class=SimpleStrategy AND strategy_options:replication_factor=1';
           var sysConOptions = { hosts: hostList,  
                                 keyspace: 'system', use_bigints: false };
           var con = new pooledCon(sysConOptions);
           con.execute(cql,[],function(err) {
           if (err) {
             console.log("Failed toocreate Keyspace: " + ksName);
             console.log(err);
           }
           else {
             console.log("Created Keyspace: " + ksName);
             callback(ksConOptions, populateCustomerData);
           }
           });
           con.shutdown();
        }
   
        function createColumnFamily(ksConOptions, callback){
          var params = ['customers_cf','custid','varint','custname',
                        'text','custaddress','text'];
          var cql = 'CREATE COLUMNFAMILY ? (? ? PRIMARY KEY,? ?, ? ?)';
        var con =  new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) {
                 console.log("Failed toocreate column family: " + params[0]);
                 console.log(err);
              }
              else {
                 console.log("Created column family: " + params[0]);
                 callback();
              }
          });
          con.shutdown();
        }
   
        //populate Data
        function populateCustomerData() {
           var params = ['John','Infinity Dr, TX', 1];
           updateCustomer(ksConOptions,params);
   
           params = ['Tom','Fermat Ln, WA', 2];
           updateCustomer(ksConOptions,params);
        }
   
        //update will also insert hello record if none exists
        function updateCustomer(ksConOptions,params)
        {
          var cql = 'UPDATE customers_cf SET custname=?,custaddress=? where custid=?';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) console.log(err);
              else console.log("Inserted customer : " + params[0]);
          });
          con.shutdown();
        }
   
        //read hello two rows inserted above
        function readCustomer(ksConOptions)
        {
          var cql = 'SELECT * FROM customers_cf WHERE custid IN (1,2)';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,[],function(err,rows) {
              if (err)
                 console.log(err);
              else
                 for (var i=0; i<rows.length; i++)
                    console.log(JSON.stringify(rows[i]));
            });
           con.shutdown();
        }
   
        //exectue hello code
        createKeyspace(createColumnFamily);
        readCustomer(ksConOptions)

## <a name="conclusion"></a>Conclusie
Microsoft Azure is een flexibel platform waarmee Hallo uitvoeren van zowel Microsoft als open-sourcesoftware zoals blijkt uit deze oefening. Maximaal beschikbare Cassandra clusters kunnen worden geïmplementeerd op één datacenter via Hallo Hallo clusterknooppunten worden verspreid over meerdere domeinen met fouten. Cassandra clusters kunnen ook worden geïmplementeerd in meerdere geografisch verafgelegen Azure-regio's voor noodherstel bewijs systemen. Azure en Cassandra samen kunnen Hallo constructie van zeer schaalbaar, maximaal beschikbare en noodherstel herstelbare cloudservices die nodig is door de hedendaagse internet schalen services.  

## <a name="references"></a>Verwijzingen
* [http://cassandra.apache.org](http://cassandra.apache.org)
* [http://www.datastax.com](http://www.datastax.com)
* [http://www.nodejs.org](http://www.nodejs.org)

