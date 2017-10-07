---
title: aaaSet van een hybride HPC Pack-cluster in Azure | Microsoft Docs
description: Meer informatie over hoe Microsoft HPC Pack toouse en Azure tooset-up maken van een klein, hybride hoge prestaties computing (HPC)-cluster
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a>Een hybride high performance computing-cluster (HPC) met Microsoft HPC Pack en Azure rekenknooppunten op aanvraag instellen
Gebruik Microsoft HPC Pack 2012 R2 en Azure tooset van een klein, hybride high performance computing-cluster (HPC). Hallo-cluster wordt weergegeven in dit artikel bestaat uit een lokale HPC Pack-hoofdknooppunt en enkele berekeningen knooppunten die u implementeert op aanvraag in een Azure-cloudservice. Vervolgens kunt u de compute-taken uitvoeren op Hallo hybride cluster.

![Hybride HPC-cluster][Overview] 

Deze zelfstudie ziet u een benadering soms cluster 'burst toohello cloud,' toouse schaalbare, on-demand Azure-resources toorun compute-intensieve toepassingen genoemd.

Deze zelfstudie wordt ervan uitgegaan dat geen ervaring met rekenclusters of HPC Pack. Het is beoogde alleen toohelp implementeren van een hybride rekencluster snel voor demonstratiedoeleinden. Voor overwegingen en stappen toodeploy een hybride HPC Pack cluster op groter schaal in een productieomgeving of toouse HPC Pack 2016, Zie Hallo [gedetailleerde richtlijnen](http://go.microsoft.com/fwlink/p/?LinkID=200493). Voor andere scenario's met HPC Pack, met inbegrip van geautomatiseerde implementatie van het cluster in Azure virtuele machines, Zie [opties voor HPC-cluster met Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="prerequisites"></a>Vereisten
* **Azure-abonnement** -als u geen Azure-abonnement hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten.
* **Een on-premises-computer met Windows Server 2012 R2 of Windows Server 2012** -deze computer gebruiken als het hoofdknooppunt Hallo van Hallo HPC-cluster. Als u al Windows Server worden niet uitgevoerd, kunt u downloaden en installeren van een [evaluatieversie](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).
  
  * Hallo-computer moet lid tooan Active Directory-domein. Voor testdoeleinden kunt u Hallo hoofdknooppunt computer configureren als een domeincontroller. tooadd Hallo Active Directory Domain Services-serverfunctie en Hallo hoofdknooppunt computer als een domeincontroller te bevorderen, Zie Hallo-documentatie voor Windows Server.
  * toosupport HPC Pack Hallo-besturingssysteem moet worden geïnstalleerd in een van de volgende talen: Engels, Japans of Chinees (Vereenvoudigd).
  * Controleer of belangrijke en kritieke updates zijn geïnstalleerd.
* **HPC Pack 2012 R2** - [downloaden](http://go.microsoft.com/fwlink/p/?linkid=328024) Hallo-installatiepakket voor de meest recente versie Hallo gratis kosten en kopieer Hallo bestanden toohello hoofdknooppunt computer. Kies installatiebestanden in Hallo dezelfde taal als de installatie van Windows Server.

    >[!NOTE]
    > Als u toouse HPC Pack 2016 in plaats van HPC Pack 2012 R2 wilt, is aanvullende configuratie nodig. Zie Hallo [gedetailleerde richtlijnen](http://go.microsoft.com/fwlink/p/?LinkID=200493).
    > 
* **Domeinaccount** -dit account moet worden geconfigureerd met lokale beheermachtigingen op Hallo hoofdknooppunt tooinstall HPC Pack.
* **TCP-verbinding op poort 443** van Hallo hoofdknooppunt tooAzure.

## <a name="install-hpc-pack-on-hello-head-node"></a>HPC Pack installeren op het hoofdknooppunt Hallo
U eerst installeren Microsoft HPC Pack op uw lokale computer met Windows Server. Deze computer wordt Hallo hoofdknooppunt van Hallo-cluster.

1. Hoofdknooppunt toohello aanmelden met een domeinaccount met lokale beheerdersmachtigingen heeft.

2. Start Hallo HPC Pack installatiewizard door het uitvoeren van Setup.exe uit Hallo HPC Pack-installatiebestanden.

3. Op Hallo **HPC Pack 2012 R2 installeren** scherm, klikt u op **nieuwe installatie of het toevoegen van nieuwe functies tooan bestaande installatie**.

    ![HPC Pack 2012 Setup][install_hpc1]

4. Op Hallo **Microsoft Software gebruikersovereenkomst pagina**, klikt u op **volgende**.

5. Op Hallo **Type installatie selecteren** pagina, klikt u op **een nieuw HPC-cluster maken door het maken van een hoofdknooppunt**, en klik vervolgens op **volgende**.

6. Hallo wizard voert verschillende voorafgaand aan installatie tests uit. Klik op **volgende** op Hallo **installatieregels** pagina als u alle tests zijn geslaagd. Anders Hallo informatie bekijken en breng eventueel benodigde wijzigingen in uw omgeving. Voer Hallo tests opnieuw, of als Hallo nodig start de installatiewizard opnieuw.
7. Op Hallo **HPC DB configuratie** pagina, controleert u of **hoofdknooppunt** is ingeschakeld voor alle HPC-databases en klik vervolgens op **volgende**. 

    ![DB-configuratie][install_hpc4]

8. Accepteer de standaardselecties op Hallo overige pagina's van de wizard Hallo. Op Hallo **vereiste onderdelen installeren** pagina, klikt u op **installeren**.
   
    ![Installeren][install_hpc6]

9. Nadat het Hallo-installatie is voltooid, schakel het selectievakje **Start HPC Cluster Manager** en klik vervolgens op **voltooien**. (U start HPC Cluster Manager in een latere stap.)
   
    ![Voltooien][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a>Hello Azure-abonnement voorbereiden
Uitvoeren van de stappen te volgen in Hallo Hallo [Azure-portal](https://portal.azure.com) met uw Azure-abonnement. Na het voltooien van deze stappen kunt u Azure knooppunten uit Hallo lokale hoofdknooppunt implementeren. 
  
  > [!NOTE]
  > Maak ook een notitie van uw Azure-abonnement-ID, die u later nodig. Hallo-ID vinden in **abonnementen** in Hallo-portal.
  > 

### <a name="upload-hello-default-management-certificate"></a>Hallo standaard management-certificaat uploaden
HPC Pack installeert een zelfondertekend certificaat op de hoofdknooppunt hello, Hallo standaard Microsoft HPC Azure Management certificaat genaamd, die u als een Azure-beheercertificaat uploaden kunt. Dit certificaat is opgegeven voor het testen en bewijs van concept implementaties toosecure Hallo verbinding tussen Hallo hoofdknooppunt en Azure.

1. Aanmelden van Hallo hoofdknooppunt computer, toohello [Azure-portal](https://portal.azure.com).

2. Klik op **abonnementen** > *your_subscription_name*.

3. Klik op **beheercertificaten** > **uploaden**.4. Blader op Hallo hoofdknooppunt voor Hallo bestand C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer. Klik vervolgens op **uploaden**.

   
Hallo **standaard HPC Azure Management** certificaat wordt weergegeven in de lijst met beheercertificaten Hallo.

### <a name="create-an-azure-cloud-service"></a>Een Azure-cloudservice maken
> [!NOTE]
> Voor de beste prestaties door Hallo-cloudservice en Hallo storage-account (in een later stadium) te maken in Hallo dezelfde geografische regio.
> 
> 

1. Klik in de portal Hallo op **Cloudservices (klassiek)** > **+ toevoegen**.

2.  Een DNS-naam voor de service hello, kiest u een resourcegroep en een locatie en klik op **maken**.


### <a name="create-an-azure-storage-account"></a>Een Azure-opslagaccount maken
1. Klik in de portal Hallo op **opslagaccounts (klassiek)** > **+ toevoegen**.

2. Typ een naam voor het Hallo-account en selecteer Hallo **klassieke** implementatiemodel.

3. Kies een resourcegroep en een locatie en andere instellingen laten op standaardwaarden. Klik vervolgens op **Maken**.

## <a name="configure-hello-head-node"></a>Hallo-hoofdknooppunt configureren
toouse HPC Cluster Manager toodeploy Azure knooppunten en toosubmit taken, voert u eerst een aantal configuratiestappen vereist cluster.

1. Start op het hoofdknooppunt Hallo HPC Cluster Manager. Als hello **hoofdknooppunt selecteren** dialoogvenster wordt weergegeven, klikt u op **lokale Computer**. Hallo **implementatie takenlijst** wordt weergegeven.

2. Onder **implementatietaken vereist**, klikt u op **configureren van uw netwerk**.
   
    ![Netwerk configureren][config_hpc2]

3. Selecteer in de Wizard netwerkconfiguratie hello, **alle knooppunten alleen op een bedrijfsnetwerk** (topologie 5). Deze netwerkconfiguratie is Hallo eenvoudigste voor demonstratiedoeleinden.
   
    ![Topologie 5][config_hpc3]
   
4. Klik op **volgende** tooaccept standaardwaarden op pagina's van de wizard Hallo resterende Hallo. Klik vervolgens op Hallo **revisie** tabblad **configureren** toocomplete Hallo-netwerkconfiguratie.

5. In Hallo **implementatie takenlijst**, klikt u op **referenties van de installatie**.

6. In Hallo **Installatiereferenties** in het dialoogvenster Hallo typt u de referenties van Hallo-domeinaccount dat u tooinstall HPC Pack gebruikt. Klik vervolgens op **OK**. 
   
    ![Van Installatiereferenties][config_hpc6]
   
7. In Hallo **implementatie takenlijst**, klikt u op **configureren Hallo naamgeving van nieuwe knooppunten**.

8. In Hallo **Geef knooppunt Naming reeks** dialoogvenster accepteer Hallo-standaard naamgevingscontext reeks en klik op **OK**. Hoewel hello Azure knooppunten die u in deze zelfstudie toevoegen zijn benoemde automatisch deze stap hebt voltooid.
   
    ![Naamgeving van knooppunt][config_hpc8]
   
9. In Hallo **implementatie takenlijst**, klikt u op **maken van een knooppuntsjabloon**. Later in de zelfstudie hello gebruikt u Hallo sjabloon tooadd Azure knooppunten toohello knooppunten.

10. Hallo in Wizard-knooppunt sjabloon maken, Hallo volgende doen:
    
    a. Op Hallo **knooppunttype sjabloon kiezen** pagina, klikt u op **Windows Azure-knooppuntsjabloon**, en klik vervolgens op **volgende**.
    
    ![Knooppuntsjabloon][config_hpc10]
    
    b. Klik op **volgende** tooaccept Hallo standaardnaam sjabloon.
    
    c. Op Hallo **abonnementsgegevens bieden** pagina, Voer uw Azure-abonnement-ID (beschikbaar in uw Azure-account-informatie). Klik op **beheercertificaat**, zoeken naar **Microsoft HPC Azure Management Default.** Klik op **Volgende**.
    
    ![Knooppuntsjabloon][config_hpc12]
    
    d. Op Hallo **servicegegevens bieden** pagina, selecteer Hallo-cloudservice en Hallo storage-account dat u in de vorige stap hebt gemaakt. Klik op **Volgende**.
    
    ![Knooppuntsjabloon][config_hpc13]
    
    e. Klik op **volgende** tooaccept standaardwaarden op pagina's van de wizard Hallo resterende Hallo. Klik vervolgens op Hallo **revisie** tabblad **maken** toocreate Hallo knooppuntsjabloon.
    
    > [!NOTE]
    > Standaard bevat hello Azure knooppuntsjabloon instellingen voor toostart (ingericht) en stop Hallo knooppunten handmatig met behulp van HPC Cluster Manager. U kunt desgewenst een toostart planning configureren en Azure knooppunten automatisch Hallo stoppen.
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a>Azure knooppunten toohello cluster toevoegen
Hallo sjabloon tooadd Azure knooppunten toohello knooppunten nu gebruiken. Toe te voegen Hallo knooppunten toohello cluster hun configuratiegegevens worden opgeslagen zodat u starten kunt (ingericht) ze op elk gewenst moment in Hallo-cloudservice. Uw abonnement alleen opgehaald in rekening gebracht voor Azure knooppunten nadat Hallo exemplaren worden uitgevoerd in Hallo-cloudservice.

Volg deze stappen tooadd twee kleine knooppunten.

1. In HPC Cluster Manager, klikt u op **knooppunt Management** (aangeroepen **bronbeheer** in huidige versies van HPC Pack) > **knooppunt toevoegen**.
   
    ![Knooppunt toevoegen][add_node1]

2. Hallo in de Wizard knooppunt toevoegen op Hallo **implementatiemethode selecteren** pagina, klikt u op **toevoegen Windows Azure knooppunten**, en klik vervolgens op **volgende**.
   
    ![Azure knooppunt toevoegen][add_node1_1]

3. Op Hallo **nieuwe knooppunten opgeven** pagina, selecteer hello Azure knooppuntsjabloon die u eerder hebt gemaakt (standaard genoemd **AzureNode standaardsjabloon**). Geef vervolgens **2** knooppunten van de grootte van **kleine**, en klik vervolgens op **volgende**.
   
    ![Knooppunten opgeven][add_node2]
   
4. Op Hallo **voltooien Hallo Wizard knooppunt toevoegen** pagina, klikt u op **voltooien**.
    
     Twee Azure knooppunten, met de naam **AzureCN 0001** en **AzureCN 0002**, worden nu weergegeven in HPC Cluster Manager. Beide zijn in Hallo **niet geïmplementeerd** status.
   
    ![Toegevoegde knooppunten][add_node3]

## <a name="start-hello-azure-nodes"></a>Start hello Azure knooppunten
Als u wilt dat wordt toouse Hallo-clusterbronnen in Azure, gebruik HPC Cluster Manager toostart (ingericht) hello Azure knooppunten en ze online brengt.

1. In HPC Cluster Manager, klikt u op **knooppunt Management** (aangeroepen **bronbeheer** in huidige versies van HPC Pack), en selecteer hello Azure knooppunten.

2. Klik op **Start**, en klik vervolgens op **OK**.
   
   ![Beginknooppunten][add_node4]
   
    Hallo knooppunten overgang toohello **inrichten** status. Weergave hello inrichting logboek tootrack Hallo inrichting uitgevoerd.
   
    ![Inrichten knooppunten][add_node6]

3. Na een paar minuten hello Azure knooppunten klaar bent met het inrichten en in Hallo **Offline** status. In deze status is Hallo rolinstanties worden uitgevoerd, maar taken cluster nog niet accepteren.

4. tooconfirm die Hallo rolinstanties in hello Azure-portal worden uitgevoerd, klikt u op **Cloudservices (klassiek)** > *your_cloud_service_name*.
   
   U ziet twee **HpcWorkerRole** exemplaren (knooppunten) uitgevoerd in Hallo-service. HPC Pack implementeert ook automatisch twee **HpcProxy** (grootte normaal) toohandle communicatie tussen Hallo hoofdknooppunt en Azure-exemplaren.

   ![Exemplaren die worden uitgevoerd][view_instances1]

5. toobring hello Azure knooppunten online toorun taken, selecteer Hallo knooppunten, klik met de rechtermuisknop en klik vervolgens op het cluster **Online brengen**.
   
    ![Offline knooppunten][add_node7]
   
    HPC Cluster Manager geeft aan dat de knooppunten Hallo in Hallo **Online** status.

## <a name="run-a-command-across-hello-cluster"></a>Een opdracht over Hallo-cluster wordt uitgevoerd
toocheck hello installatie, gebruik Hallo HPC Pack **clusrun** opdracht toorun een opdracht of een toepassing op een of meer clusterknooppunten. Als een eenvoudig voorbeeld gebruiken **clusrun** tooget Hallo IP-adresconfiguratie van hello Azure knooppunten.

1. Op het hoofdknooppunt hello, open een opdrachtprompt als beheerder.

2. Type Hallo volgende opdracht:
   
    `clusrun /nodes:azurecn* ipconfig`

3. Als u wordt gevraagd, voert u het wachtwoord van de cluster. U ziet opdracht vergelijkbare toohello volgende uitvoer.
   
    ![Clusrun][clusrun1]

## <a name="run-a-test-job"></a>Voer een test
Nu een testtaak die wordt uitgevoerd op Hallo hybride cluster indienen. In dit voorbeeld is een eenvoudige parametrische taak (een soort intrinsiek parallelle berekeningen). In dit voorbeeld wordt uitgevoerd subtaken met Hallo voor het toevoegen van een geheel getal tooitself **/a ingesteld** opdracht. Alle Hallo knooppunten in cluster Hallo bijdragen toofinishing Hallo subtaken voor gehele getallen van 1 too100.

1. Klik in HPC Cluster Manager op **Jobbeheer** > **nieuwe parametrische Sweep taak**.
   
    ![Nieuwe taak][test_job1]

2. In Hallo **nieuwe parametrische Sweep taak** het dialoogvenster **opdrachtregel**, type `set /a *+*` (overschrijven Hallo standaardopdrachtregel die wordt weergegeven). Laat de standaardwaarden voor Hallo resterende instellingen en klik vervolgens op **indienen** toosubmit Hallo taak.
   
    ![Parametrische opschoning][param_sweep1]

3. Wanneer het Hallo-taak is voltooid, dubbelklikt u op Hallo **mijn Sweep taak** taak.

4. Klik op **taken weergeven**, en klik vervolgens op een subtaak tooview Hallo berekend uitvoer van deze subtaak.
   
    ![Resultaten van de taak][view_job361]

5. toosee welk knooppunt Hallo berekening uitgevoerd voor deze subtaak, klikt u op **toegewezen knooppunten**. (U mogelijk de naam van een ander knooppunt weergegeven voor uw cluster.)
   
    ![Resultaten van de taak][view_job362]

## <a name="stop-hello-azure-nodes"></a>Stop hello Azure knooppunten
Nadat u de cluster Hallo uitproberen, stop hello Azure knooppunten tooavoid onnodige kosten tooyour account. Deze stap Hallo cloudservice stopt en verwijdert hello Azure rolinstanties.

1. In HPC Cluster Manager in **knooppunt Management** (aangeroepen **bronbeheer** in eerdere versies van HPC Pack), selecteert u beide Azure knooppunten. Klik vervolgens op **stoppen**.
   
    ![Knooppunten stoppen][stop_node1]

2. In Hallo **stoppen Windows Azure knooppunten** in het dialoogvenster, klikt u op **stoppen**. 
   
3. Hallo knooppunten overgang toohello **stoppen** status. Na een paar minuten HPC Cluster Manager geeft aan dat de knooppunten Hallo **niet geïmplementeerd**.
   
    ![Niet-geïmplementeerde knooppunten][stop_node4]

4. tooconfirm die Hallo rolinstanties worden niet meer in Azure worden uitgevoerd in Azure portal op Hallo **Cloudservices (klassiek)** > *your_cloud_service_name*. Er zijn geen exemplaren worden geïmplementeerd in de productieomgeving Hallo. 
   
    Deze zelfstudie Hallo is voltooid.

## <a name="next-steps"></a>Volgende stappen
* Hallo-documentatie voor verkennen [HPC Pack](https://technet.microsoft.com/library/cc514029).
* Zie tooset van een hybride implementatie van het cluster op groter schaal HPC Pack [tooAzure Worker-Rolexemplaren met Microsoft HPC Pack Burst](http://go.microsoft.com/fwlink/p/?LinkID=200493).
* Voor andere manieren toocreate een HPC Pack-cluster in Azure, met inbegrip van met behulp van Azure Resource Manager-sjablonen, Zie [opties voor HPC-cluster met Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
