---
title: aaaRun Capaciteitsplanner voor Hyper-V Hallo voor siteherstel | Microsoft Docs
description: Dit artikel wordt beschreven hoe toorun Capaciteitsplanner voor Hyper-V Hallo voor Azure Site Recovery
services: site-recovery
documentationcenter: na
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 2bc3832f-4d6e-458d-bf0c-f00567200ca0
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: b853598e5cd290c48b59794ba48eefc72ac8ded6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-hyper-v-capacity-planner-tool-for-site-recovery"></a>Hallo-Capaciteitsplanner voor Hyper-V uitvoeren voor de Site Recovery

Als onderdeel van uw Azure Site Recovery-implementatie moet u toofigure uit uw replicatie en de vereiste bandbreedte. Hallo Hyper-V-hulpprogramma capacity planner voor Site Recovery kunt u toodo, voor Hyper-V-replicatie voor virtuele machines.

Dit artikel wordt beschreven hoe toorun Hallo Capaciteitsplanner voor Hyper-V. Dit hulpprogramma moet worden gebruikt samen met de informatie in Hallo [capaciteitsplanning voor siteherstel](site-recovery-capacity-planner.md).

## <a name="before-you-start"></a>Voordat u begint
U uitvoeren Hallo hulpprogramma op een Hyper-V server of cluster-knooppunt in de primaire site. toorun hello hulpprogramma Hallo Hyper-V-hostservers moet:

* Besturingssysteem: WindowsServer 2012 of 2012 R2
* Geheugen: 20 MB (minimum)
* CPU: 5 procent overhead (minimum)
* Schijfruimte: 5 MB (minimum)

Voordat u Hallo hulpprogramma uitvoert, moet u tooprepare Hallo primaire site. Als u repliceert tussen twee on-premises sites en gewenste toocheck bandbreedte, moet u tooprepare een replica-server.

## <a name="step-1-prepare-hello-primary-site"></a>Stap 1: Voorbereiden Hallo primaire site

1. Controleer op Hallo primaire site, een lijst met alle Hallo Hyper-V-machines die u wilt dat tooreplicate en Hallo Hyper-V-hosts/clusters waarop ze zich bevinden. Hallo-hulpprogramma kan worden uitgevoerd voor meerdere zelfstandige hosts of voor een cluster, maar niet allebei tegelijk. Tevens moet toorun afzonderlijk voor elk besturingssysteem, dus u gegevens over Hyper-V-servers als volgt verzamelen moet:

   * Windows Server 2012 zelfstandige servers
   * Windows Server 2012-clusters
   * Zelfstandige servers voor Windows Server 2012 R2
   * Windows Server 2012 R2-clusters
2. Inschakelen van externe toegang tooWMI op alle Hallo Hyper-V-hosts en clusters. Deze opdracht uitvoert op elke servercluster zijn toomake ervoor firewallregels en machtigingen ingesteld:

        netsh firewall set service RemoteAdmin enable
3. Schakel de bewaking van toepassingsprestaties op servers en clusters, als volgt:

   * Open Hallo Windows Firewall met Hallo **geavanceerde beveiliging** module, en vervolgens regels voor binnenkomende verbindingen inschakelen Hallo volgende: **COM +-netwerktoegang (DCOM-IN)** en alle regels in Hallo **externe gebeurtenislogboek Beheergroep**.

## <a name="step-2-prepare-a-replica-server-on-premises-tooon-premises-replication"></a>Stap 2: Een replica-server (lokale tooon-premises replicatie) voorbereiden
U hoeft niet toodo dit als u tooAzure repliceert.

Wij raden u één Hyper-V-host als een herstelserver zodat een dummy VM gerepliceerde tooit toocheck bandbreedte kan worden.  U kunt dit overslaan, maar u niet kunt toomeasure bandbreedte tenzij u dit doen.

1. Als u wilt dat toouse configureren een clusterknooppunt als Hallo replica Hyper-V Replica broker:

   * In **Serverbeheer**Open **Failoverclusterbeheer**.
   * Verbinding maken met cluster toohello, markeer de naam van de cluster Hallo en klik op **acties** > **functie configureren** wizard maximale beschikbaarheid van tooopen Hallo.
   * In **rol selecteren**, klikt u op **Hyper-V Replica Broker**. In de wizard Hallo bieden een **NetBIOS-naam** en Hallo **IP-adres** toobe gebruikt als Hallo verbinding punt toohello cluster (een clienttoegangspunt genoemd). Hallo **Hyper-V Replica Broker** wordt geconfigureerd, wat resulteert in een client access point-naam die u Houd er rekening mee.
   * Controleer of u die rol Hallo-Hyper-V Replica Broker online beschikbaar is en failover naar alle knooppunten van het Hallo-cluster kan. toodo, klik met de rechtermuisknop op Hallo-rol, wijs te**verplaatsen**, en klik vervolgens op **knooppunt selecteren**. Selecteer een knooppunt > **OK**.
   * Als u verificatie op basis van certificaten gebruikt, zorg ervoor dat elk clusterknooppunt en Hallo clienttoegangspunt alle Hallo-certificaat hebben geïnstalleerd.
2. Een replica-server inschakelen:

   * Open Clusterbeheer is mislukt voor een cluster, verbinding toohello cluster en klikt u op **rollen** > Functieservices selecteren > **replicatie-instellingen** > **Maak van dit cluster als een Replica Server**. Als u een cluster als Hallo replica gebruikt, moet u aanwezig is op het Hallo-cluster in Hallo primaire site ook toohave Hallo Hyper-V Replica Broker-functie.
   * Open Hyper-V-beheer voor een zelfstandige server. In Hallo **acties** deelvenster, klikt u op **Hyper-V-instellingen** voor Hallo-server die u wilt tooenable, en in **replicatieconfiguratie** klikt u op **Schakel deze optie computer als een Replica-server**.
3. Verificatie instellen:

   * In **verificatie en poorten**, selecteer de manier waarop tooauthenticate Hallo primaire server en Hallo authenticatiepoorten. Als u een certificaat Klik **certificaat selecteren** tooselect een. Kerberos niet gebruiken als Hallo primaire en herstelsites Hyper-V-hosts in Hallo hetzelfde domein of in vertrouwde domeinen. Gebruik van certificaten voor verschillende domeinen bevinden, of voor de implementatie van een werkgroep.
   * In **autorisatie en opslag**, toestaan **eventuele** geverifieerde (primaire) servers toosend replicatie gegevens toothis replica-server.

     ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image1.png)
   * Voer **netsh http show servicestate**, toocheck die Hallo-listener wordt uitgevoerd voor Hallo protocol/opgegeven poort:  
4. Firewalls instellen. Firewallregels gemaakt tijdens de installatie van Hyper-V tooallow verkeer op Hallo standaardpoorten (HTTPS op 443, Kerberos op 80). Deze regels als volgt inschakelen:
  - Certificaatverificatie op cluster (443):``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}``
  - Kerberos-verificatie op cluster (80):``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}``
  - Certificaatverificatie op zelfstandige server:``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"``
  - Kerberos-verificatie op de zelfstandige server:``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"``

## <a name="step-3-run-hello-capacity-planner-tool"></a>Stap 3: Voer Hallo Capaciteitsplanner
Nadat u uw primaire site hebt voorbereid, en een herstelserver hebt ingesteld, kunt u Hallo hulpprogramma uitvoeren.

1. [Download](https://www.microsoft.com/download/details.aspx?id=39057) Hallo hulpprogramma van Hallo Microsoft Download Center.
2. Hallo hulpprogramma van een van de primaire servers hello (of een van de knooppunten van de primaire cluster Hallo Hallo) uitvoeren. Met de rechtermuisknop op Hallo .exe-bestand en kies vervolgens **als administrator uitvoeren**.
3. In **voordat u begint met**, geef aan hoe lang u toocollect gegevens. U wordt aangeraden dat u Hallo hulpprogramma uitvoeren tijdens de productie-uren tooensure dat gegevens representatief is. Als u alleen verbinding met het netwerk toovalidate probeert, kunt u alleen een minuut verzamelen.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image2.png)
4. In **details van de primaire site**Hallo-servernaam of de FQDN-naam opgeven voor een zelfstandige host of voor een cluster Geef Hallo FQDN-naam van de client Hallo accepteren punt, clusternaam of een willekeurig knooppunt in het Hallo-cluster en klik vervolgens op **volgende**. Hallo hulpprogramma detecteert automatisch Hallo-naam van Hallo-server die wordt uitgevoerd. virtuele machines die kunnen worden gecontroleerd voor Hallo hulpprogramma opgehaald Hallo gespecificeerde servers.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image3.png)
5. In **Replica sitegegevens**, als u tooAzure repliceert of als u tooa secundair datacenter repliceert en een replica-server hebt ingesteld selecteert **overslaan tests met betrekking tot de replica-site**. Als u tooa secundair datacenter repliceert en u een ReplicaType hebt ingesteld, FQDN invoert van Hallo zelfstandige server of Hallo client access point voor Hallo-cluster in **Server name (of) Hyper-V Replica Broker CAP**.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image4.png)
6. In **uitgebreide Replica Details**, inschakelen **overslaan Hallo tests met betrekking tot de uitgebreide Replica-site**. Deze tests worden niet ondersteund door Site Recovery.
7. In **VMs kiezen tooReplicate**, Hallo's verbindt toohello server of cluster en virtuele machines worden weergegeven en schijven op de primaire server Hallo, in overeenstemming met Hallo instellingen u opgegeven op Hallo **primaire Site-informatie**  pagina. Virtuele machines die al zijn ingeschakeld voor replicatie of die niet zijn uitgevoerd, worden niet weergegeven. Hallo VM's waarvoor u toocollect metrische gegevens wilt selecteren. Verzamelt gegevens voor Hallo virtuele machines te Hallo VHD's automatisch selecteren.
8. Als u een replica-server of cluster hebt geconfigureerd **netwerkgegevens**, geef Hallo geschatte WAN-bandbreedte u denkt dat als u hebt geconfigureerd tussen de primaire en replica sites Hallo en selecteer Hallo certificaten worden gebruikt certificaatverificatie.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image5.png)
9. In **samenvatting**, Hallo instellingen controleren en klikt u op **volgende** toobegin verzamelen van meetgegevens. Hulpprogramma voortgang en status wordt weergegeven op Hallo **berekenen capaciteit** pagina. Wanneer het Hallo-hulpprogramma is voltooid, klikt u op **rapport weergeven** tooview Hallo uitvoer. Logboeken en rapporten worden standaard opgeslagen in **%systemdrive%\Users\Public\Documents\Capacity Planner**.

   ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image6.png)

## <a name="step-4-interpret-hello-results"></a>Stap 4: Hallo resultaten interpreteren

Hier vindt u belangrijke metrische gegevens over Hallo. Metrische gegevens die hier niet worden weergegeven, kunt u negeren. Ze zijn niet relevant voor de Site Recovery.

### <a name="on-premises-tooon-premises-replication"></a>Lokale tooon-premises replicatie

* Gevolgen van replicatie op Hallo primaire host compute-, geheugen
* Gevolgen van replicatie op Hallo primaire, herstel-hosts opslag schijfruimte, IOP 's
* Totale bandbreedte die vereist zijn voor replicatie van verschillen (Mbps)
* Waargenomen netwerkbandbreedte tussen de primaire host Hallo en Hallo herstelhost (Mbps)
* Suggestie voor Hallo ideaal aantal actieve parallelle overdrachten tussen Hallo twee hosts/clusters

### <a name="on-premises-tooazure-replication"></a>Lokale tooAzure replicatie

* Gevolgen van replicatie op Hallo primaire host compute-, geheugen
* Gevolgen van replicatie op Hallo primaire host schijf opslagruimte IOP 's
* Totale bandbreedte die vereist zijn voor replicatie van verschillen (Mbps)

## <a name="more-resources"></a>Meer bronnen
* Lees voor gedetailleerde informatie over hulpprogramma Hallo Hallo-document die wordt meegestuurd met Hallo hulpprogramma voor downloaden.
* Bekijk een overzicht van het Hallo-hulpprogramma op van Keith Mayer [blog van TechNet](http://blogs.technet.com/b/keithmayer/archive/2014/02/27/guided-hands-on-lab-capacity-planner-for-windows-server-2012-hyper-v-replica.aspx).
* [Hallo resultaten](site-recovery-performance-and-scaling-testing-on-premises-to-on-premises.md) van onze prestatietests voor lokale tooon-premises Hyper-V-replicatie

## <a name="next-steps"></a>Volgende stappen

Nadat u klaar bent met het plannen van capaciteit kunt u beginnen met het implementeren van Site Recovery:

* [Hyper-V-machines in VMM-clouds tooAzure repliceren](site-recovery-vmm-to-azure.md)
* [TooAzure Hyper-V-machines (zonder VMM) repliceren](site-recovery-hyper-v-site-to-azure.md)
* [Hyper-V-machines repliceren tussen VMM-sites](site-recovery-vmm-to-vmm.md)
