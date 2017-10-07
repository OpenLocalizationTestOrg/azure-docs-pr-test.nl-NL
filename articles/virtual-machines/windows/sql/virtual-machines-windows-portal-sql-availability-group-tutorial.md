---
title: aaaSQL Server-beschikbaarheidsgroepen - virtuele Machines van de Azure - zelfstudie | Microsoft Docs
description: Deze zelfstudie laat zien hoe toocreate een SQL Server altijd op beschikbaarheidsgroep op Azure Virtual Machines.
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a>Configureren AlwaysOn-beschikbaarheidsgroep in Azure VM handmatig

Deze zelfstudie laat zien hoe toocreate een SQL Server altijd op beschikbaarheidsgroep op Azure Virtual Machines. Hallo voltooid zelfstudie maakt een beschikbaarheidsgroep met een databasereplica op twee SQL-Servers.

**Tijd schatting**: duurt ongeveer 30 minuten toocomplete als Hallo vereisten is voldaan.

Hallo diagram ziet u wat u in de zelfstudie Hallo bouwen.

![Beschikbaarheidsgroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a>Vereisten

Hallo-zelfstudie wordt ervan uitgegaan dat u basiskennis van SQL Server altijd op beschikbaarheidsgroepen. Als u meer informatie, Zie [overzicht van AlwaysOn-beschikbaarheidsgroepen (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Hallo bevat volgende tabel dat u toocomplete nodig hebt voordat u deze zelfstudie Hallo-vereisten:

|  |Vereiste |Beschrijving |
|----- |----- |----- |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | Twee SQL-Servers | -In een Azure beschikbaarheidsset <br/> -In één domein <br/> -Met de functie Failover Clustering is geïnstalleerd |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| Windows Server | Bestandsshare voor cluster-witness |  
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|SQL Server-serviceaccount | Domeinaccount |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|SQL Server Agent-serviceaccount | Domeinaccount |  
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Firewall-poorten | -SQL Server: **1433** voor het standaardexemplaar <br/> -Eindpunt voor databasespiegeling: **5022** of een beschikbare poort <br/> -Azure load balancer-test: **59999** of een beschikbare poort |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Toevoegen van de functie Failoverclustering | Deze functie nodig hebben voor zowel SQL-Servers |
|![vierkante](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Installatieaccount van het domein | -Lokale beheerder zijn op elke SQL Server <br/> -Lid is van SQL Server vaste serverrol sysadmin voor elk exemplaar van SQL Server  |


Voordat u met Hallo zelfstudie begint, moet u deze te[voldoen aan vereisten voor het maken van AlwaysOn-beschikbaarheidsgroepen in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md). Als deze vereiste onderdelen zijn al voltooid, kunt u gaan te[Cluster maken](#CreateCluster).


<!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Hallo-cluster maken

Na Hallo vereisten zijn voltooid, is de eerste stap Hallo toocreate een Windows Server-failovercluster met twee SQL-servers en een witness-server.  

1. RDP-toohello eerste SQL-Server met behulp van een domeinaccount met een Administrator op SQL-Servers en Hallo witness-server.

   >[!TIP]
   >Als u Hallo gevolgd [vereisten document](virtual-machines-windows-portal-sql-availability-group-prereq.md), u hebt gemaakt met een account met de naam **CORP\Install**. Dit account gebruiken.

2. In Hallo **Serverbeheer** dashboard, selecteer **extra**, en klik vervolgens op **Failoverclusterbeheer**.
3. Klik in het linkerdeelvenster Hallo met de rechtermuisknop op **Failoverclusterbeheer**, en klik vervolgens op **maken van een Cluster**.
   ![Cluster maken](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)
4. In Hallo Wizard Cluster maken, een cluster met één knooppunt maken door het Hallo-pagina's met instellingen in de volgende tabel Hallo Hallo doorlopen:

   | Pagina | Instellingen |
   | --- | --- |
   | Voordat u begint |Standaardinstellingen gebruiken |
   | Servers selecteren |Type Hallo eerste SQL-Server in de naam **Enter servernaam** en klik op **toevoegen**. |
   | Van validatiewaarschuwing |Selecteer **nr. ik geen ondersteuning van Microsoft nodig hebt voor dit cluster, en daarom niet wilt dat toorun Hallo validatie wordt getest. Als ik op Volgende klikt, doorgaan met het Hallo-cluster maken**. |
   | Toegangspunt voor beheer Hallo Cluster |Typ de naam van een cluster, zoals **SQLAGCluster1** in **clusternaam**.|
   | Bevestiging |Gebruik de standaardwaarden tenzij u van opslagruimten gebruikmaakt. Zie Hallo opmerking onder deze tabel. |

### <a name="set-hello-cluster-ip-address"></a>Hallo cluster-IP-adres instellen

1. In **Failoverclusterbeheer**, schuif naar beneden te**Clusterkernresources** en vouw Hallo clusterdetails. Ziet u beide Hallo **naam** en Hallo **IP-adres** bronnen in Hallo **mislukt** status. Hallo bron van het IP-adres kan niet online worden gebracht omdat Hallo-cluster is toegewezen Hallo dezelfde IP-adres als Hallo machine zelf, is een dubbel adres.

2. Klik met de rechtermuisknop Hallo mislukt **IP-adres** bron en klik vervolgens op **eigenschappen**.

   ![Eigenschappen van cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. Selecteer **statisch IP-adres** en geef een beschikbaar adres van waarbij Hallo SQL Server in het tekstvak voor het Hallo is-subnet. Klik vervolgens op **OK**.
4. In Hallo **Clusterkernresources** sectie, met de rechtermuisknop op de clusternaam van het en klik op **Online brengen**. Vervolgens wacht u totdat beide bronnen online zijn. Wanneer de naam clusterbron Hallo online wordt gezet, Hallo DC-server wordt bijgewerkt met een nieuw AD-account. Gebruik deze AD-account toorun hello later beschikbaarheidsgroep geclusterde service.

### <a name="addNode"></a>Voeg andere SQL Server-toocluster Hallo

Voeg andere SQL Server-cluster toohello Hallo.

1. In de boomstructuur Hallo browser met de rechtermuisknop op het Hallo-cluster en klikt u op **knooppunt toevoegen**.

    ![Knooppunt toohello Cluster toevoegen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. In Hallo **Wizard knooppunt toevoegen**, klikt u op **volgende**. In Hallo **Servers selecteren** pagina, het toevoegen van Hallo tweede SQL Server. Type Hallo-servernaam in **Enter servernaam** en klik vervolgens op **toevoegen**. Wanneer u klaar bent, klikt u op **volgende**.

1. In Hallo **Validation Warning** pagina, klikt u op **Nee** (in een productiescenario u moet uitvoeren Hallo validatietests). Klik op **Volgende**.

8. In Hallo **bevestiging** pagina als u met opslagruimten kunt wissen Hallo selectievakje **Voeg alle in aanmerking komende opslag toohello cluster.**

   ![Knooppunt bevestiging toevoegen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   >Als u met behulp van opslagruimten en niet doen schakelt **Voeg alle in aanmerking komende opslag toohello cluster**, Windows hello virtuele schijven losgekoppeld tijdens Hallo clustering proces. Als gevolg hiervan worden niet weergegeven in Schijfbeheer of Explorer totdat Hallo opslagruimten zijn verwijderd uit de cluster Hallo en opnieuw gekoppeld met behulp van PowerShell. Opslagruimten gegroepeerd op meerdere schijven in toostorage groepen. Zie voor meer informatie [opslagruimten](https://technet.microsoft.com/library/hh831739).

1. Klik op **Volgende**.

1. Klik op **Voltooien**.

   Failover Cluster Manager blijkt dat het cluster een nieuw knooppunt heeft en wordt weergegeven in Hallo **knooppunten** container.

10. Afmelding Hallo extern bureaublad-sessiehost.

### <a name="add-a-cluster-quorum-file-share"></a>Toevoegen van een clusterquorum-bestandsshare

In dit voorbeeld gebruikt Hallo Windows-cluster een bestandsshare toocreate een clusterquorum. Deze zelfstudie maakt gebruik van een knooppunt en bestandssharemeerderheid quorum. Zie voor meer informatie [Quorumconfiguraties in een failovercluster](http://technet.microsoft.com/library/cc731739.aspx).

1. Toohello bestandsshare-witness lid bestandsserver verbinden met een extern bureaublad-sessiehost.

1. Op **Serverbeheer**, klikt u op **extra**. Open **Computerbeheer**.

1. Klik op **gedeelde mappen**.

1. Met de rechtermuisknop op **Shares**, en klik op **nieuwe Share...** .

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Gebruik **Wizard gedeelde map maken** toocreate een share.

1. Op **mappad**, klikt u op **Bladeren** en niet vinden of een pad voor de gedeelde map Hallo maken. Klik op **Volgende**.

1. In **naam, beschrijving en instellingen** Hallo sharenaam en het pad controleren. Klik op **Volgende**.

1. Op **machtigingen voor gedeelde mappen** ingesteld **machtigingen aanpassen**. Klik op **aangepaste...** .

1. Op **machtigingen aanpassen**, klikt u op **toevoegen...** .

1. Zorg ervoor dat Hallo account gebruikt toocreate Hallo cluster volledig beheer heeft.

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. Klik op **OK**.

1. In **machtigingen voor gedeelde mappen**, klikt u op **voltooien**. Klik op **voltooien** opnieuw.  

1. Meld u af bij Hallo-server

### <a name="configure-cluster-quorum"></a>Clusterquorum configureren

Vervolgens stelt u het clusterquorum Hallo.

1. Het eerste clusterknooppunt toohello verbinding met extern bureaublad.

1. In **Failoverclusterbeheer**, met de rechtermuisknop op het Hallo-cluster, wijst u te**meer acties**, en klik op **Clusterquoruminstellingen configureren...** .

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. In **Wizard clusterquorum configureren**, klikt u op **volgende**.

1. In **optie voor quorumconfiguratie**, kies **hello quorumwitness selecteren**, en klik op **volgende**.

1. Op **Quorumwitness selecteren**, klikt u op **een bestandssharewitness configureren**.

   >[!TIP]
   >Windows Server 2016 biedt ondersteuning voor een cloud-witness. Als u dit soort witness kiest, hoeft u niet een bestand witness delen. Zie voor meer informatie [een witness cloud voor een failover-Cluster implementeren](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness). Deze zelfstudie maakt gebruik van een bestandssharewitness wordt ondersteund door eerdere besturingssystemen.

1. Op **bestandssharewitness configureren**, tekst hello pad voor Hallo-share die u hebt gemaakt. Klik op **Volgende**.

1. Hallo-instellingen te controleren op **bevestiging**. Klik op **Volgende**.

1. Klik op **Voltooien**.

Hallo clusterkernresources zijn geconfigureerd met een bestandssharewitness.

## <a name="enable-availability-groups"></a>Beschikbaarheidsgroepen inschakelen

Schakel vervolgens Hallo **AlwaysOn Availability Groups** functie. Voer deze stappen uit op beide SQL-Servers.

1. Van Hallo **Start** scherm, starten **SQL Server Configuration Manager**.
2. Klik in de structuur van de browser Hallo op **SQL Server-Services**, vervolgens met de rechtermuisknop op Hallo **SQL Server (MSSQLSERVER)** service en klik op **eigenschappen**.
3. Klik op Hallo **AlwaysOn hoge beschikbaarheid** tabblad en selecteer vervolgens **Schakel AlwaysOn Availability Groups**als volgt:

    ![AlwaysOn-beschikbaarheidsgroepen inschakelen](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. Klik op **Toepassen**. Klik op **OK** in Hallo pop-upvenster.

5. Hallo SQL Server-service opnieuw starten.

Herhaal deze stappen op Hallo van andere SQL-Server.

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a>Een database maakt op Hallo eerste SQL-Server

1. Start Hallo RDP-bestand toohello eerste SQL-Server met een domein-account dat lid is van sysadmin vaste serverrol.
1. Open SQL Server Management Studio en maak verbinding toohello eerste SQL-Server.
7. In **Objectverkenner**, met de rechtermuisknop op **Databases** en klik op **nieuwe Database**.
8. In **databasenaam**, type **MyDB1**, klikt u vervolgens op **OK**.

### <a name="backupshare"></a>Maak een back-share

1. Hallo eerste SQL-Server in op **Serverbeheer**, klikt u op **extra**. Open **Computerbeheer**.

1. Klik op **gedeelde mappen**.

1. Met de rechtermuisknop op **Shares**, en klik op **nieuwe Share...** .

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Gebruik **Wizard gedeelde map maken** toocreate een share.

1. Op **mappad**, klikt u op **Bladeren** en vinden of een pad voor de gedeelde map voor Hallo database back-up te maken. Klik op **Volgende**.

1. In **naam, beschrijving en instellingen** Hallo sharenaam en het pad controleren. Klik op **Volgende**.

1. Op **machtigingen voor gedeelde mappen** ingesteld **machtigingen aanpassen**. Klik op **aangepaste...** .

1. Op **machtigingen aanpassen**, klikt u op **toevoegen...** .

1. Zorg ervoor dat SQL Server en SQL Server Agent-serviceaccounts Hallo voor beide servers volledig beheer hebben.

   ![Nieuwe Share](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. Klik op **OK**.

1. In **machtigingen voor gedeelde mappen**, klikt u op **voltooien**. Klik op **voltooien** opnieuw.  

### <a name="take-a-full-backup-of-hello-database"></a>Een volledige back-up van database Hallo duren

U moet tooback Hallo nieuwe database tooinitialize Hallo logboekketen van. Als u een back-up van de nieuwe database Hallo pas van kracht worden, kan deze kan niet worden opgenomen in een beschikbaarheidsgroep.

1. In **Objectverkenner**, met de rechtermuisknop op het Hallo-database, wijs het te**taken...** , klikt u op **Back-Up**.

1. Klik op **OK** tootake een volledige back-up toohello standaard back-uplocatie.

## <a name="create-hello-availability-group"></a>Hallo beschikbaarheidsgroep maken
U bent nu klaar tooconfigure een beschikbaarheidsgroep met Hallo volgende stappen:

* Een database maakt op Hallo eerste SQL-Server.
* Neem een volledige back-up en de een transactielogboek van Hallo-database
* Restore Hallo volledige en logboek back-ups toohello tweede SQL Server Hello **NORECOVERY** optie
* Hallo beschikbaarheidsgroep maken (**AG1**) met synchrone doorvoer en automatische failover leesbare secundaire replica's

### <a name="create-hello-availability-group"></a>Hallo beschikbaarheidsgroep maken:

1. Op de extern bureaublad-sessiehost toohello eerste SQL-Server. In **Objectverkenner** SSMS, met de rechtermuisknop op **AlwaysOn hoge beschikbaarheid** en klik op **nieuwe Wizard beschikbaarheidsgroep**.

    ![De Wizard Nieuwe beschikbaarheidsgroep starten](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. In Hallo **inleiding** pagina, klikt u op **volgende**. In Hallo **naam van de beschikbaarheidsgroep opgeven** pagina, typ een naam voor Hallo beschikbaarheidsgroep, bijvoorbeeld **AG1**in **naam van de beschikbaarheidsgroep**. Klik op **Volgende**.

    ![Wizard Nieuwe AG AG-naam opgeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. In Hallo **Databases selecteren** pagina, selecteer uw database en klik op **volgende**.

   >[!NOTE]
   >Hallo database voldoet Hallo-vereisten voor een beschikbaarheidsgroep aan omdat u ten minste één volledige back-up hebt uitgevoerd op Hallo beoogde primaire replica.

   ![Wizard Nieuwe AG Databases selecteren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. In Hallo **replica's opgeven** pagina, klikt u op **Replica toevoegen**.

   ![Wizard Nieuwe AG replica's opgeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. Hallo **tooServer verbinding** dialoogvenster verschijnt. Hallo-typenaam van de tweede server Hallo in **servernaam**. Klik op **Verbinden**.

   Terug in Hallo **replica's opgeven** pagina u ziet nu de tweede server Hallo die worden vermeld in **Beschikbaarheidsreplica**. Hallo-replica's als volgt configureren.

   ![Wizard Nieuwe AG replica's (voltooid) opgeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. Klik op **eindpunten** toosee Hallo eindpunt voor databasespiegeling voor deze beschikbaarheidsgroep. Gebruik Hallo dezelfde poort die u hebt gebruikt bij het instellen van Hallo [firewallregel voor databasespiegeling eindpunten](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

    ![Wizard Nieuwe AG eerste gegevenssynchronisatie selecteren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. In Hallo **eerste gegevenssynchronisatie selecteren** pagina **volledige** en geef een gedeelde netwerklocatie. Gebruiken voor de locatie van Hallo Hallo [back-upshare die u hebt gemaakt](#backupshare). In voorbeeld van Hallo was, **\\\\\<eerste SQL-Server\>\Backup\**. Klik op **Volgende**.

   >[!NOTE]
   >Volledige synchronisatie duurt een volledige back-up van de database op het eerste exemplaar van SQL Server Hallo Hallo en toohello tweede exemplaar te herstellen. Voor grote databases worden volledige synchronisatie wordt niet aanbevolen omdat het kan lang duren. U kunt deze tijd verkorten door handmatig een back-up van database Hallo duurt en herstellen van deze met `NO RECOVERY`. Als het Hallo-database is al teruggezet met `NO RECOVERY` op Hallo tweede SQL Server voordat u Hallo beschikbaarheidsgroep configureert, kies **alleen deelnemen**. Als u back-up van tootake Hallo na het Hallo-beschikbaarheidsgroep configureren, kiest **eerste gegevenssynchronisatie overslaan**.

    ![Wizard Nieuwe AG eerste gegevenssynchronisatie selecteren](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. In Hallo **validatie** pagina, klikt u op **volgende**. Deze pagina ziet vergelijkbare toohello installatiekopie te volgen:

    ![Wizard Nieuwe AG, validatie](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    >Er is een waarschuwing voor de configuratie van de listener Hallo omdat u een beschikbaarheidsgroep-listener niet hebt geconfigureerd. Omdat u op de virtuele Azure-machines na het maken van hello Azure load balancer Hallo listener maken, kunt u deze waarschuwing negeren.

10. In Hallo **samenvatting** pagina, klikt u op **voltooien**, en vervolgens een ogenblik geduld terwijl Hallo wizard configureert u Hallo nieuwe beschikbaarheidsgroep. In Hallo **voortgang** pagina, klikt u op **meer details** tooview Hallo gedetailleerde uitgevoerd. Zodra het Hallo-wizard is voltooid, controleert u Hallo **resultaten** pagina tooverify die Hallo beschikbaarheidsgroep is gemaakt.

     ![Wizard Nieuwe AG resulteert](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. Klik op **sluiten** tooexit Hallo-wizard.

### <a name="check-hello-availability-group"></a>Hallo beschikbaarheidsgroep controleren

1. In **Objectverkenner**, vouw **AlwaysOn hoge beschikbaarheid**, vouw vervolgens **beschikbaarheidsgroepen**. U ziet nu Hallo nieuwe Availability Group in deze container. Met de rechtermuisknop op Hallo Availability Group en klik op **Dashboard weergeven**.

   ![AG-Dashboard weergeven](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   Uw **AlwaysOn Dashboard** vergelijkbare toothis moet worden gezocht.

   ![AG-Dashboard](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   Hallo-replica's Hallo failover-modus van de synchronisatiestatus van elke replica en hello, kunt u zien.

2. In **Failoverclusterbeheer**, klikt u op het cluster. Selecteer **rollen**. Hallo beschikbaarheidsgroep naam die u gebruikt, is een rol op Hallo-cluster. Deze beschikbaarheidsgroep heeft geen een IP-adres voor clientverbindingen, omdat u niet een listener hebt geconfigureerd. U configureert Hallo listener nadat u een Azure load balancer maken.

   ![AG in Failoverclusterbeheer](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > Probeer niet toofail via Hallo Availability Group uit Hallo Failover Cluster Manager. Alle failover-bewerkingen moeten worden uitgevoerd vanuit **AlwaysOn Dashboard** in SSMS. Zie voor meer informatie [beperkingen op met Failover Cluster Manager met beschikbaarheidsgroepen Hallo](https://msdn.microsoft.com/library/ff929171.aspx).
    >

U hebt op dit moment een beschikbaarheidsgroep met replica's op twee exemplaren van SQL Server. U kunt Hallo beschikbaarheidsgroep verplaatsen tussen exemplaren. U kunt toohello beschikbaarheidsgroep nog kan geen verbinding omdat u niet over een listener. Hallo-listener vereist in virtuele machines in Azure, een load balancer. de volgende stap Hallo is toocreate Hallo load balancer in Azure.

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a>Een Azure load balancer maken

Op virtuele machines in Azure vereist een SQL Server-beschikbaarheidsgroep een load balancer. Hallo load balancer bevat Hallo IP-adres voor de beschikbaarheidsgroep-listener Hallo. Deze sectie ziet u hoe de toocreate Hallo load balancer in hello Azure-portal.

1. Ga in de Azure-portal hello, toohello resourcegroep waar uw SQL-Servers zijn en klik op **+ toevoegen**.
2. Zoeken naar **Load Balancer**. Kies Hallo load balancer gepubliceerd door Microsoft.

   ![AG in Failoverclusterbeheer](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  Klik op **Create**.
3. Hallo volgende parameters voor Hallo load balancer configureren.

   | Instelling | Veld |
   | --- | --- |
   | **Naam** |Gebruik een naam voor de Hallo load balancer, zoals **sqlLB**. |
   | **Type** |interne |
   | **Virtueel netwerk** |Hallo-naam van Hallo virtuele Azure-netwerk gebruiken. |
   | **Subnet** |Gebruik Hallo-naam van die virtuele machine Hallo Hallo subnet is in.  |
   | **IP-adrestoewijzing** |Statisch |
   | **IP-adres** |Gebruik een beschikbaar adres van subnet. |
   | **Abonnement** |Gebruik Hallo hetzelfde abonnement als Hallo virtuele machine. |
   | **Locatie** |Gebruik Hallo dezelfde locatie als Hallo virtuele machine. |

   Hello Azure portalblade moet er als volgt uitzien:

   ![Load Balancer maken](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. Klik op **maken**, toocreate Hallo load balancer.

tooconfigure hello load balancer, moet u een back-endpool toocreate, een test en set Hallo load-balancingregels. Voer deze in hello Azure-portal.

### <a name="add-backend-pool"></a>Back-endpool toevoegen

1. Ga in hello Azure-portal, tooyour beschikbaarheidsgroep. Mogelijk moet u taakverdeler toorefresh Hallo weergave toosee Hallo nieuw gemaakt.

   ![Load Balancer niet vinden in de resourcegroep](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. Hallo load balancer op, klik op **back-endpools**, en klik op **+ toevoegen**. Hallo back-endpool als volgt instellen:

   | Instelling | Beschrijving | Voorbeeld
   | --- | --- |---
   | **Naam** | Typ een naam | SQLLBBE
   | **Gekoppeld aan** | Kies uit de lijst | Beschikbaarheidsset
   | **Beschikbaarheidsset** | Gebruik een naam van de beschikbaarheidsset Hallo die uw SQL Server-VM's in | sqlAvailabilitySet |
   | **Virtuele machines** |Hallo twee namen van de virtuele machine in Azure SQL-Server | SQL Server-0, SQL Server-1

1. Typ de naam Hallo voor Hallo back-end-pool.

1. Klik op **+ toevoegen van een virtuele machine**.

1. Voor Hallo beschikbaarheidsset kiezen Hallo beschikbaarheidsset die Hallo SQL-Servers bevinden zich in.

1. Voor virtuele machines zijn beide Hallo SQL-Servers. Neem geen share Hallo-witness bestandsserver.

1. Klik op **OK** toocreate Hallo back-endpool.

### <a name="set-hello-probe"></a>Set Hallo test

1. Hallo load balancer op, klik op **statuscontroles**, en klik op **+ toevoegen**.

1. Hallo health test als volgt instellen:

   | Instelling | Beschrijving | Voorbeeld
   | --- | --- |---
   | **Naam** | Tekst | SQLAlwaysOnEndPointProbe |
   | **Protocol** | Kies TCP | TCP |
   | **Poort** | Een niet-gebruikte poort | 59999 |
   | **Interval**  | Hallo hoeveelheid tijd tussen test probeert (in seconden) |5 |
   | **Drempelwaarde voor onjuiste status** | het aantal opeenvolgende testfouten dat moet worden uitgevoerd voor een virtuele machine toobe niet in orde beschouwd Hallo  | 2 |

1. Klik op **OK** tooset Hallo health test.

### <a name="set-hello-load-balancing-rules"></a>Hallo taakverdelingsregels instellen

1. Hallo load balancer op, klik op **Taakverdelingsregels**, en klik op **+ toevoegen**.

1. Hallo load-balancingregels als volgt instellen.
   | Instelling | Beschrijving | Voorbeeld
   | --- | --- |---
   | **Naam** | Tekst | SQLAlwaysOnEndPointListener |
   | **Frontend IP-adres** | Kies een adres |Gebruik Hallo-adres dat u hebt gemaakt tijdens het maken van Hallo load balancer. |
   | **Protocol** | Kies TCP |TCP |
   | **Poort** | Hallo-poort gebruiken voor Hallo SQL Server-exemplaar | 1433 |
   | **Back-Endpoort** | Dit veld wordt niet gebruikt wanneer zwevend IP is ingesteld voor direct server return | 1433 |
   | **Test** |Hallo-naam die u hebt opgegeven voor de test Hallo | SQLAlwaysOnEndPointProbe |
   | **Sessiepersistentie** | Vervolgkeuzelijst | **Geen** |
   | **Time-out voor inactiviteit** | Minuten tookeep een TCP-verbinding openen | 4 |
   | **Zwevend IP (direct server return)** | |Ingeschakeld |

   > [!WARNING]
   > Direct server return is ingesteld tijdens het maken van. Deze kan niet worden gewijzigd.

1. Klik op **OK** tooset Hallo load-balancingregels.

## <a name="configure-listener"></a>Hallo-listener configureren

de volgende dingen toodo Hello is tooconfigure een beschikbaarheidsgroep-listener op Hallo failover-cluster.

> [!NOTE]
> Deze zelfstudie laat zien hoe toocreate één listener - met een ILB IP adres. toocreate een of meer listeners met behulp van een of meer IP-adressen, Zie [Create Availability Group-listener en load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a>Set-listener-poort

In SQL Server Management Studio ingesteld Hallo-listener-poort.

1. Start SQL Server Management Studio en maak verbinding toohello primaire replica.

1. Navigeer te**AlwaysOn hoge beschikbaarheid** | **beschikbaarheidsgroepen** | **beschikbaarheid Beschikbaarheidsgroeplisteners**.

1. U ziet nu Hallo-listener-naam die u hebt gemaakt in Failoverclusterbeheer. Met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello en klik op **eigenschappen**.

1. In Hallo **poort** Geef Hallo-poortnummer voor de beschikbaarheidsgroep-listener Hallo via Hallo $EndpointPort u eerder hebt gebruikt (1433 was Hallo standaard), klikt u vervolgens op **OK**.

U hebt nu een SQL Server-beschikbaarheidsgroep in Azure virtuele machines die worden uitgevoerd in de modus Resource Manager.

## <a name="test-connection-toolistener"></a>Test verbinding toolistener

tootest hello verbinding:

1. RDP-tooa SQL-Server die zich in Hallo hetzelfde virtuele netwerk, maar niet eigen Hallo replica. U kunt andere SQL-Server in de cluster Hallo Hallo.

1. Gebruik **sqlcmd** hulpprogramma tootest Hallo verbinding. Bijvoorbeeld Hallo script volgen stelt een **sqlcmd** verbinding toohello primaire replica via het Hallo-listener met de Windows-verificatie:

    ```
    sqlcmd -S <listenerName> -E
    ```

    Als het Hallo-listener poort wordt gebruikt door een andere waarde dan Hallo standaard poort (1433), Hallo-poort in de verbindingsreeks Hallo opgeven. Bijvoorbeeld: hello volgende sqlcmd-opdracht verbindt tooa listener op poort 1435:

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Hallo SQLCMD-verbinding verbinding automatisch toowhichever exemplaar van SQL Server-hosts Hallo primaire replica.

> [!TIP]
> Zorg ervoor dat Hallo poort die u opgeeft geopend op Hallo firewall beide SQL-servers is. Beide servers vereisen een inkomende regel voor Hallo TCP-poort die u gebruikt. Zie voor meer informatie [toevoegen of bewerken firewallregel](http://technet.microsoft.com/library/cc753558.aspx).
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a>Volgende stappen

- [Toevoegen van een IP-adres tooa load balancer voor een tweede beschikbaarheidsgroep](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).
