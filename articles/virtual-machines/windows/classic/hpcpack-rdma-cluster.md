---
title: aaaSet van een Windows-RDMA cluster toorun MPI-toepassingen | Microsoft Docs
description: Meer informatie over hoe een cluster met Windows HPC Pack met de grootte van H16r, H16mr, A8 of A9-VM's toouse toocreate hello Azure RDMA netwerk toorun MPI-apps.
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 7d9f5bc8-012f-48dd-b290-db81c7592215
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 23bc8740dbd05a7c7ab3f998489a41d0df4520a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-rdma-cluster-with-hpc-pack-toorun-mpi-applications"></a>Instellen van een cluster met Windows RDMA met HPC Pack toorun MPI-toepassingen
Instellen van een Windows-RDMA-cluster in Azure met [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) en [hoge prestaties compute-VM-grootten](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun parallelle Message Passing Interface (MPI)-toepassingen. Wanneer u RDMA-functionaliteit, Windows Server gebaseerde knooppunten in een cluster HPC Pack instelt, wordt MPI-toepassingen efficiënt communiceren via een lage latentie en hoge doorvoersnelheid netwerk in Azure die is gebaseerd op remote direct memory access (RDMA)-technologie.

Als u toorun MPI-belastingen op Linux virtuele machines die toegang tot het netwerk hello Azure RDMA wilt, Zie [instellen van een Linux RDMA cluster toorun MPI-toepassingen](../../linux/classic/rdma-cluster.md).

## <a name="hpc-pack-cluster-deployment-options"></a>HPC Pack cluster implementatieopties
Microsoft HPC Pack is een hulpprogramma voor zover op niets extra kosten toocreate HPC-clusters lokaal of in Azure toorun Windows of Linux-HPC-toepassingen. HPC Pack bevat een runtime-omgeving voor Microsoft-implementatie Hallo Hallo-bericht wordt doorgegeven Interface voor Windows (MS-MPI). Bij gebruik met RDMA-compatibel is met een ondersteund besturingssysteem voor Windows Server-exemplaren is biedt HPC Pack een efficiënte optie toorun Windows MPI-toepassingen die toegang tot het netwerk hello Azure RDMA. 

In dit artikel maakt u kennis met twee scenario's en koppelingen toodetailed richtlijnen tooset van een cluster met Windows RDMA met Microsoft HPC Pack. 

* Scenario 1. Rekenintensieve worker rolexemplaren (PaaS) implementeren
* Scenario 2. Implementeer de rekenknooppunten in rekenintensieve VM's (IaaS)

Raadpleeg voor algemene vereisten toouse rekenintensieve exemplaren met Windows [hoge prestaties compute-VM-grootten](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="scenario-1-deploy-compute-intensive-worker-role-instances-paas"></a>Scenario 1: Rekenintensieve worker rolexemplaren (PaaS) implementeren
Toevoegen van een bestaand cluster HPC Pack, extra rekenresources in Azure worker-rolexemplaren (Azure knooppunten) uitgevoerd in een cloudservice (PaaS). Deze functie, ook wel 'burst tooAzure' van HPC Pack ondersteunt een aantal formaten voor exemplaren van Hallo worker-rol. Bij het toevoegen van hello Azure knooppunten, één RDMA-compatibele Hallo grootten opgeven.

Hieronder vindt u overwegingen en stappen tooburst tooRDMA-compatibele Azure-exemplaren van een bestaand (meestal on-premises) cluster. Gebruik dezelfde procedures tooadd worker rol exemplaren tooan HPC Pack hoofdknooppunt dat in een Azure VM is geïmplementeerd.

> [!NOTE]
> Zie voor een zelfstudie tooburst tooAzure HPC Pack, [een hybride-cluster met HPC Pack instellen](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Houd er rekening mee Hallo overwegingen in de volgende stappen uit die van toepassing zijn specifiek tooRDMA-compatibele Azure knooppunten Hallo.
> 
> 

![Burst tooAzure][burst]

### <a name="steps"></a>Stappen
1. **Implementeer en configureer een hoofdknooppunt HPC Pack 2012 R2**
   
    Meest recente HPC Pack Hallo-installatiepakket downloaden van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922). Zie voor tooprepare vereisten en instructies voor de implementatie van een ' burst ' in Azure, [tooAzure Werkrolinstanties met Microsoft HPC Pack Burst](https://technet.microsoft.com/library/gg481749.aspx).
2. **Een beheercertificaat in hello Azure-abonnement configureren**
   
    Configureer een certificaat toosecure Hallo-verbinding tussen Hallo hoofdknooppunt en Azure. Zie voor opties en -procedures, [scenario's tooConfigure hello Azure-Beheercertificaat voor HPC Pack](http://technet.microsoft.com/library/gg481759.aspx). HPC Pack installeert voor testimplementaties een standaard Microsoft HPC Azure-Beheercertificaat tooyour Azure-abonnement kunt u snel uploaden.
3. **Een nieuwe cloudservice en een opslagaccount maken**
   
    Gebruik hello Azure portal toocreate een cloudservice en een opslagaccount voor Hallo-implementatie in een regio waar Hallo RDMA-compatibele exemplaren beschikbaar zijn.
4. **Een op Azure-knooppuntsjabloon maken**
   
    Gebruik hello maken knooppunt sjabloonwizard in HPC Cluster Manager. Zie voor stappen [maken van een knooppuntsjabloon Azure](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Templ) in 'Stappen tooDeploy Azure knooppunten met Microsoft HPC Pack'.
   
    Voor de eerste tests, is het raadzaam een handmatige beschikbaarheid-beleid in Hallo sjabloon te configureren.
5. **Knooppunten toohello cluster toevoegen**
   
    De Wizard knooppunt toevoegen Hallo in HPC Cluster Manager gebruiken. Zie voor meer informatie [Azure knooppunten toevoegen toohello Windows HPC-Cluster](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Add).
   
    Bij het opgeven van de grootte van knooppunten Hallo Hallo Selecteer een van de RDMA-compatibele exemplaar grootten Hallo.
   
   > [!NOTE]
   > In elke implementatie van de tooAzure burst met Hallo rekenintensieve exemplaren HPC Pack automatisch een minimum van twee RDMA-compatibele exemplaren (zoals A8) wordt geïmplementeerd als proxy-knooppunten, Daarnaast toohello Azure worker-rolexemplaren die u opgeeft. Hallo proxy knooppunten gebruik kernen die toohello abonnement worden toegewezen en kosten samen met exemplaren van hello Azure worker-rol.
   > 
   > 
6. **Start (ingericht) Hallo knooppunten te brengen en online toorun taken**
   
    Hallo-knooppunten te selecteren en gebruik Hallo **Start** actie in HPC Cluster Manager. Bij het inrichten is voltooid, Hallo knooppunten te selecteren en gebruik Hallo **Online brengen** actie in HPC Cluster Manager. Hallo-knooppunten zijn gereed toorun taken.
7. **Verzenden van taken toohello cluster**
   
   HPC Pack taak verzending van hulpprogramma's voor toorun cluster taken gebruiken. Zie [Microsoft HPC Pack: Taakbeheer](http://technet.microsoft.com/library/jj899585.aspx).
8. **Hallo-knooppunten (deprovision) stoppen**
   
   Wanneer u klaar bent met het actieve taken Hallo knooppunten offline nemen en Hallo **stoppen** actie in HPC Cluster Manager.

## <a name="scenario-2-deploy-compute-nodes-in-compute-intensive-vms-iaas"></a>Scenario 2: Implementeer rekenknooppunten in rekenintensieve VM's (IaaS)
In dit scenario door Hallo HPC Pack hoofdknooppunt en cluster rekenknooppunten op virtuele machines in een Azure-netwerk op te implementeren. HPC Pack bevat diverse [implementatieopties in Azure VM's](../../linux/hpcpack-cluster-options.md), met inbegrip van geautomatiseerde implementatiescripts en Azure-snelstartsjablonen. Hallo bijvoorbeeld na overwegingen en stappen begeleiden u toouse hello [HPC Pack IaaS-implementatiescript](hpcpack-cluster-powershell-script.md) Hallo-implementatie van een HPC Pack 2012 R2-cluster in Azure automatiseren.

![Cluster in virtuele machines in Azure][iaas]

### <a name="steps"></a>Stappen
1. **Maken van het hoofdknooppunt van een cluster en virtuele machines knooppunt berekenen door het Hallo HPC Pack IaaS-implementatiescript uitvoeren op een clientcomputer**
   
    Het downloadpakket Hallo HPC Pack IaaS-implementatiescript van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922).
   
    Hallo clientcomputer tooprepare Hallo script configuratiebestand en Voer Hallo script maken, Zie [een HPC-Cluster maken met Hallo HPC Pack IaaS-implementatiescript](hpcpack-cluster-powershell-script.md). 
   
    RDMA-compatibele toodeploy rekenknooppunten, opmerking Hallo na aanvullende overwegingen:
   
   * **Virtueel netwerk**: Geef een nieuw virtueel netwerk in een regio in welke Hallo RDMA-compatibele exemplaargrootte gewenste toouse beschikbaar is.
   * **Windows Server-besturingssysteem**: toosupport RDMA connectiviteit, Geef een besturingssysteem Windows Server 2012 R2 of Windows Server 2012 voor Hallo rekenknooppunt virtuele machines.
   * **Cloudservices**: het is raadzaam uw hoofdknooppunt in een cloudservice en uw rekenknooppunten in een andere cloudservice implementeren.
   * **De grootte van knooppunt HEAD**: voor dit scenario kunt u een grootte van ten minste A4 (Extra groot) voor Hallo hoofdknooppunt.
   * **De extensie HpcVmDrivers**: implementatiescript Hallo hello Azure VM-Agent en Hallo HpcVmDrivers uitbreiding wordt automatisch geïnstalleerd wanneer u de grootte van rekenknooppunten A8 of A9 met een Windows Server-besturingssysteem implementeert. HpcVmDrivers stuurprogramma's worden geïnstalleerd op het rekenknooppunt Hallo virtuele machines zodat ze toohello RDMA netwerk verbinding kunnen maken. Op virtuele machines RDMA-compatibele H-serie, moet u handmatig Hallo HpcVmDrivers uitbreiding te installeren. Zie [hoge prestaties compute-VM-grootten](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
   * **De netwerkconfiguratie**: implementatiescript Hallo worden automatisch ingesteld Hallo HPC Pack cluster in de topologie 5 (alle knooppunten in het bedrijfsnetwerk Hallo). Deze topologie is vereist voor alle implementaties van HPC Pack cluster in virtuele machines. Hallo cluster netwerktopologie niet later wijzigen.
2. **Breng Hallo rekenknooppunten online toorun taken**
   
    Hallo-knooppunten te selecteren en gebruik Hallo **Online brengen** actie in HPC Cluster Manager. Hallo-knooppunten zijn gereed toorun taken.
3. **Verzenden van taken toohello cluster**
   
    Verbind toohello hoofdknooppunt toosubmit taken of instellen van een lokale computer toodo dit. Zie voor informatie [taken verzenden tooan HPC-cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
4. **Los het Hallo knooppunten offline en stoppen (toewijzing ongedaan maken) ze**
   
    Wanneer u klaar bent met het actieve taken duren Hallo knooppunten offline in HPC Cluster Manager. Vervolgens gebruikt u Azure management tools tooshut ze omlaag.

## <a name="run-mpi-applications-on-hello-cluster"></a>MPI-toepassingen op Hallo cluster uitvoeren
### <a name="example-run-mpipingpong-on-an-hpc-pack-cluster"></a>Voorbeeld: Mpipingpong uitgevoerd op een cluster HPC Pack
een implementatie HPC Pack Hallo RDMA-compatibele exemplaren, uitvoeren van tooverify HPC Pack Hallo **mpipingpong** opdracht op Hallo-cluster. **mpipingpong** verzendt pakketten van gegevens tussen knooppunten gekoppelde herhaaldelijk toocalculate latentie en doorvoer metingen en statistieken voor Hallo toepassingsnetwerk RDMA-functionaliteit. Dit voorbeeld ziet u een doorsnee patroon voor het uitvoeren van een MPI-taak (in dit geval **mpipingpong**) met behulp van de cluster Hallo **mpiexec** opdracht.

In dit voorbeeld wordt ervan uitgegaan dat u Azure knooppunten in de configuratie van een 'burst tooAzure' toegevoegd ([Scenario 1](#scenario-1.-deploy-compute-intensive-worker-role-instances-\(PaaS\) in this article). Als u HPC Pack geïmplementeerd op een cluster van virtuele Azure-machines, u moet toomodify Hallo opdracht syntaxis toospecify een ander knooppunt groep en stel extra omgeving variabelen toodirect toohello RDMA-netwerk-verkeer.

toorun mpipingpong op Hallo-cluster:

1. Open een opdrachtprompt op Hallo hoofdknooppunt of op een clientcomputer juist is geconfigureerd.
2. tooestimate latentie tussen paren van knooppunten in een implementatie Azure burst met vier knooppunten, type Hallo opdracht toosubmit een taak toorun mpipingpong met een kleine pakketten, grootte en veel iteraties te volgen:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 1:100000 -op -s nul
    ```
   
    Hallo opdracht retourneert Hallo-ID van Hallo-taak die wordt verzonden.
   
    Als u Hallo HPC Pack cluster is geïmplementeerd op Azure Virtual machines hebt geïmplementeerd, geeft u een knooppunt groep met compute knooppunt virtuele machines die zijn geïmplementeerd in een enkel cloudservice en Hallo wijzigen **mpiexec** opdracht als volgt:
   
    ```Command
    job submit /nodegroup:vmcomputenodes /numnodes:4 mpiexec -c 1 -affinity -env MSMPI_DISABLE_SOCK 1 -env MSMPI_PRECONNECT all -env MPICH_NETMASK 172.16.0.0/255.255.0.0 mpipingpong -p 1:100000 -op -s nul
    ```
3. Wanneer het Hallo-taak is voltooid, tooview Hallo de uitvoer (in dit geval Hallo-uitvoer van de taak 1 van de taak Hallo) type Hallo na
   
    ```Command
    task view <JobID>.1
    ```
   
    waar &lt; *JobID* &gt; is Hallo-ID van het Hallo-taak die is ingediend.
   
    Hallo uitvoer bevat de volgende vergelijkbare toohello resultaten latentie.
   
    ![Ping pong latentie][pingpong1]
4. tooestimate doorvoer tussen paren van Azure burst knooppunten, type Hallo volgende opdracht toosubmit een taak toorun **mpipingpong** met een grote pakketten, grootte en een aantal iteraties:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 4000000:1000 -op -s nul
    ```
   
    Hallo opdracht retourneert Hallo-ID van Hallo-taak die wordt verzonden.
   
    Wijzigen in een cluster HPC Pack is geïmplementeerd op Azure Virtual machines, Hallo opdracht zoals beschreven in stap 2.
5. Wanneer het Hallo-taak is voltooid, uitvoer tooview Hallo (in dit geval Hallo-uitvoer van de taak 1 van de taak Hallo) type hello te volgen:
   
    ```Command
    task view <JobID>.1
    ```
   
   Hallo uitvoer bevat de volgende vergelijkbare toohello resultaten doorvoer.
   
   ![Ping pong doorvoer][pingpong2]

### <a name="mpi-application-considerations"></a>Overwegingen met betrekking tot MPI-toepassing
Hieronder volgen enkele overwegingen voor het uitvoeren van MPI-toepassingen met HPC Pack in Azure. Sommige alleen toodeployments van Azure knooppunten (worker rolinstanties toegevoegd in de configuratie van een 'burst tooAzure') van toepassing.

* Werknemer-rolexemplaren in een cloudservice worden periodiek zonder voorafgaande kennisgeving ingericht door Azure (bijvoorbeeld voor systeemonderhoud of in geval die een exemplaar is mislukt). Een exemplaar is ingericht, terwijl deze een MPI-taak wordt uitgevoerd, Hallo exemplaar gegevens verliest als toohello status retourneert wanneer deze is geïmplementeerd, wat leiden Hallo MPI taak toofail tot kan. Hallo meer knooppunten die u gebruikt voor een enkele MPI-taak en Hallo meer hello taak wordt uitgevoerd, Hallo waarschijnlijk een van de exemplaren Hallo terwijl een taak wordt uitgevoerd is ingericht. U kunt ook dit als u één knooppunt in de implementatie Hallo als een bestandsserver aanwijzen.
* toorun MPI-jobs in Azure, u hebt geen RDMA-compatibele toouse Hallo-exemplaren. U kunt de exemplaargrootte van een dat wordt ondersteund door HPC Pack gebruiken. Hallo RDMA-compatibele exemplaren worden echter aanbevolen voor het uitvoeren van relatief grootschalige MPI-jobs die gevoelige toohello latentie en bandbreedte Hallo Hallo-netwerk dat verbinding Hallo knooppunten maakt zijn. Als u andere grootten toorun latentiegevoelig en bandbreedte MPI-taken gebruiken, raden wij kleine taken, waarin een enkele taak wordt uitgevoerd op slechts een paar knooppunten uitgevoerd.
* Toepassingen die zijn geïmplementeerd tooAzure exemplaren zijn onderwerp toohello verbonden met de toepassing hello licentievoorwaarden. Neem contact op met de leverancier van een commerciële toepassing voor licentieverlening of andere beperkingen voor het uitvoeren in de cloud Hallo Hallo. Niet alle leveranciers bieden licenties waarbij u betaalt naar gebruik.
* Azure-exemplaren moeten verder setup tooaccess lokale knooppunten, shares en licentieservers. U kunt bijvoorbeeld tooenable hello Azure knooppunten tooaccess een licentieserver lokale Azure-netwerk van site-naar-site configureren.
* toorun MPI-toepassingen op Azure-exemplaren elke MPI toepassing registreren met Windows Firewall op Hallo exemplaren door het uitvoeren van Hallo **hpcfwutil** opdracht. Hierdoor MPI communicatie tootake plaats op een poort die dynamisch wordt toegewezen door Hallo firewall.
  
  > [!NOTE]
  > Voor implementaties van burst tooAzure, kunt u ook configureren een firewall-uitzondering opdracht toorun automatisch op alle nieuwe Azure knooppunten die tooyour cluster worden toegevoegd. Na het uitvoeren van Hallo **hpcfwutil** opdracht in en controleer of dat uw toepassing werkt, Hallo opdracht tooa opstartscript voor uw Azure knooppunten toevoegt. Zie voor meer informatie [gebruik een opstartscript voor Azure knooppunten](https://technet.microsoft.com/library/jj899632.aspx).
  > 
  > 
* Hallo CCP_MPI_NETMASK cluster omgeving variabele toospecify een bereik van acceptabele adressen HPC Pack gebruikt voor MPI-communicatie. U start in HPC Pack 2012 R2, Hallo CCP_MPI_NETMASK cluster omgevingsvariabele alleen van invloed op MPI-communicatie tussen de rekenknooppunten van de domein-cluster (on-premises of in Azure VM's). Hallo-variabele wordt genegeerd door de knooppunten die zijn toegevoegd in een ' burst ' tooAzure-configuratie.
* MPI-taken uitvoeren niet op Azure-exemplaren die in een andere cloud-services (bijvoorbeeld burst tooAzure implementaties met een ander knooppunt sjablonen of Azure VM rekenknooppunten geïmplementeerd in meerdere cloudservices) zijn geïmplementeerd. Als u meerdere Azure knooppunt implementaties die zijn gestart met een ander knooppunt sjablonen hebt, worden Hallo MPI-taak moet uitvoeren op slechts één set met Azure knooppunten.
* Als u Azure knooppunten tooyour cluster toevoegen en ze brengt online Hallo HPC Job Scheduler-Service onmiddellijk probeert toostart taken op Hallo knooppunten. Als er slechts een deel van uw werkbelasting op Azure uitvoeren kunt, zorg ervoor dat u bijwerken of de taak sjablonen toodefine welke taak typen kunnen worden uitgevoerd op Azure maken. Bijvoorbeeld vereist tooensure dat taken die worden verzonden met een taaksjabloon voor alleen uitvoeren op Azure knooppunten Hallo-knooppuntgroepen eigenschap toohello taaksjabloon toevoegen en selecteer AzureNodes Hallo waarde. aangepaste groepen voor uw Azure knooppunten toocreate Hallo toevoegen HpcGroup HPC PowerShell-cmdlet gebruiken.

## <a name="next-steps"></a>Volgende stappen
* Als een alternatieve toousing HPC Pack ontwikkelen met hello Azure Batch service toorun MPI-toepassingen op de beheerde pools van rekenknooppunten in Azure. Zie [gebruik meerdere exemplaren taken toorun Message Passing Interface (MPI) applications in Azure Batch](../../../batch/batch-mpi.md).
* Als u wilt dat toorun Linux MPI-toepassingen die toegang hebben tot hello Azure RDMA netwerk, Zie [instellen van een Linux RDMA cluster toorun MPI-toepassingen](../../linux/classic/rdma-cluster.md).

<!--Image references-->
[burst]:media/hpcpack-rdma-cluster/burst.png
[iaas]:media/hpcpack-rdma-cluster/iaas.png
[pingpong1]:media/hpcpack-rdma-cluster/pingpong1.png
[pingpong2]:media/hpcpack-rdma-cluster/pingpong2.png
