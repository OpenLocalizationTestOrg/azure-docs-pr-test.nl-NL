---
title: aaaRun STER-CCM + met HPC Pack op de virtuele Linux-machines | Microsoft Docs
description: Een Microsoft HPC Pack cluster in Azure implementeren en uitvoeren van een STER-taak CCM + op meerdere Linux-rekenknooppunten via een netwerk RDMA.
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Uitvoeren van de STER-CCM + met Microsoft HPC Pack op een Linux RDMA-cluster in Azure
Dit artikel laat zien hoe een Microsoft HPC Pack toodeploy cluster op Azure en voer een [CD adapco STER-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) taak op meerdere Linux-rekenknooppunten die met elkaar door middel van InfiniBand verbonden zijn.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Microsoft HPC Pack biedt functies toorun tal van grootschalige HPC en parallelle toepassingen, waaronder MPI-toepassingen op clusters van Microsoft Azure virtuele machines. HPC Pack ondersteunt ook waarop Linux HPC-toepassingen op Linux-rekenknooppunt virtuele machines die zijn geïmplementeerd in een cluster HPC Pack. Zie voor een inleiding toousing Linux-rekenknooppunten met HPC Pack, [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md).

## <a name="set-up-an-hpc-pack-cluster"></a>Een cluster HPC Pack instellen
Hallo HPC Pack IaaS implementatiescripts downloaden van Hallo [Downloadcentrum](https://www.microsoft.com/en-us/download/details.aspx?id=44949) en pak ze lokaal.

Azure PowerShell is een vereiste. PowerShell is niet geconfigureerd op uw lokale computer, lees dan Hallo artikel [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

Op moment van schrijven van dit Hallo zijn Hallo Linux installatiekopieën van hello Azure Marketplace (met daarin Hallo InfiniBand-stuurprogramma's voor Azure) voor SLES 12, CentOS 6.5 en CentOS 7.1. In dit artikel is gebaseerd op Hallo gebruik van SLES 12. naam van de tooretrieve Hallo van alle Linux-installatiekopieën die ondersteuning bieden voor HPC in Hallo Marketplace, kunt u Hallo volgende PowerShell-opdracht uitvoeren:

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

Hallo-uitvoer geeft een lijst van Hallo locatie waarin deze installatiekopieën beschikbaar zijn en Hallo installatiekopie met de naam (**ImageName**) toobe in implementatiesjabloon hello later gebruikt.

Voordat u Hallo cluster implementeert, hebt u toobuild een sjabloonbestand HPC Pack-implementatie. Omdat we een klein cluster ontwikkelt je, wordt de Hallo hoofdknooppunt Hallo-domeincontroller en de host een lokale SQL-database.

Hallo volgende sjabloon een hoofdknooppunt implementeren, maakt u een XML-bestand met de naam **MyCluster.xml**, en vervang de waarden Hallo van **SubscriptionId**, **StorageAccount**,  **Locatie**, **VMName**, en **ServiceName** met jouw e-mailadres.

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

Start Hallo-hoofdknooppunt maken door het Hallo PowerShell-opdracht uitvoeren in een opdrachtprompt met verhoogde bevoegdheid:

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

Na 20 minuten too30 Hallo hoofdknooppunt moet gereed. U kunt tooit verbinden van hello Azure-portal door te klikken op Hallo **Connect** pictogram van Hallo virtuele machine.

U hebt mogelijk uiteindelijk toofix Hallo DNS-doorstuurserver. toodo starten, DNS-beheer.

1. Klik met de rechtermuisknop Hallo-servernaam in DNS-beheer, selecteer **eigenschappen**, en klik vervolgens op Hallo **doorstuurservers** tabblad.
2. Klik op Hallo **bewerken** knop tooremove doorstuurservers en klik vervolgens op **OK**.
3. Zorg ervoor dat Hallo **root-hints gebruiken als er geen doorstuurservers beschikbaar** selectievakje is ingeschakeld en klik vervolgens op **OK**.

## <a name="set-up-linux-compute-nodes"></a>Linux-rekenknooppunten instellen
U Hallo Linux-rekenknooppunten implementeren met behulp van Hallo dezelfde sjabloon voor de implementatie die u hebt gebruikt toocreate Hallo hoofdknooppunt.

Hallo-bestand kopiëren **MyCluster.xml** vanuit uw lokale machine toohello hoofdknooppunt en update Hallo **NodeCount** tag met het aantal knooppunten dat u wilt dat toodeploy hello (< = 20). Worden zorgvuldige toohave voldoende beschikbare kernen in uw Azure quotum omdat elk exemplaar A9 16 kernen in uw abonnement verbruikt. U kunt A8-exemplaren (8 kernen) gebruiken in plaats van A9 als u toouse meer virtuele machines in Hallo wilt hetzelfde budget.

Kopieer op Hallo hoofdknooppunt, Hallo HPC Pack IaaS implementatiescripts.

Voer Hallo volgende Azure PowerShell-opdrachten in een opdrachtprompt met verhoogde bevoegdheid:

1. Voer **Add-AzureAccount** tooconnect tooyour Azure-abonnement.
2. Als u meerdere abonnementen hebt, voert u **Get-AzureSubscription** toolist ze.
3. Een standaardabonnement ingesteld door Hallo **Select-AzureSubscription - SubscriptionName-xxxx-standaard** opdracht.
4. Voer **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart Linux-rekenknooppunten implementeren.
   
   ![Hoofdknooppunt implementatie in actie][hndeploy]

Open het hulpprogramma voor Hallo HPC Pack Cluster Manager. Linux-rekenknooppunten wordt regelmatig na enkele minuten weergegeven in de lijst met clusterknooppunten compute. Met de klassieke implementatiemodus Hallo worden opeenvolgend IaaS VM's gemaakt. Dus als het aantal knooppunten Hallo belangrijk is, alle geïmplementeerd ophalen kan duren voordat een aanzienlijke hoeveelheid tijd.

![Linux-knooppunten in HPC Pack Cluster Manager][clustermanager]

Nu dat alle knooppunten actief in het Hallo-cluster zijn, zijn er extra infrastructuur instellingen toomake.

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a>Instellen van een bestandsshare in Azure voor Windows en Linux-knooppunten
U kunt hello Azure File service toostore scripts, toepassingspakketten en gegevensbestanden worden opgeslagen. Azure-bestand biedt mogelijkheden voor CIFS boven op Azure Blob-opslag als een permanente opslag. Let erop dat dit geen Hallo meest schaalbare oplossing is, maar het Hallo eenvoudigste één is en geen toegewezen virtuele machines vereist.

Een Azure-bestandsshare maken door het Hallo-instructies in Hallo artikel [aan de slag met Azure File storage in Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).

Hallo-naam van uw opslagaccount als **saname**, Hallo bestandssharenaam als **sharename**, en de opslagaccountsleutel Hallo als **sakey**.

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a>Hallo Azure-bestandsshare op het hoofdknooppunt Hallo koppelen
Open een opdrachtprompt met verhoogde bevoegdheid en Voer Hallo opdracht toostore Hallo referenties in Hallo lokale machine kluis te volgen:

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

Vervolgens toomount Hallo bestandsshare in Azure, worden uitgevoerd:

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a>Hello Azure-bestandsshare op Linux-rekenknooppunten koppelen
Een nuttig hulpmiddel dat wordt geleverd met HPC Pack is Hallo clusrun hulpprogramma. U kunt dit opdrachtregelprogramma toorun Hallo dezelfde opdracht tegelijkertijd gebruiken in een set van rekenknooppunten. In ons geval het toomount hello Azure-bestandsshare wordt gebruikt en blijven behouden deze toosurvive opnieuw wordt opgestart.
In een opdrachtprompt met verhoogde bevoegdheid op Hallo hoofdknooppunt Hallo volgende opdrachten worden uitgevoerd.

toocreate hello Koppelmap:

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

toomount hello Azure-bestandsshare:

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

toopersist hello mount-share:

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a>Installeren van de STER-CCM +
Azure VM-instanties A8 en A9 bieden ondersteuning voor InfiniBand en RDMA-mogelijkheden. Hallo kernel-stuurprogramma's waarmee deze mogelijkheden zijn beschikbaar voor Windows Server 2012 R2, SUSE 12, CentOS 6.5 en CentOS 7.1 afbeeldingen in hello Azure Marketplace. Microsoft MPI en Intel MPI (versie 5.x) zijn Hallo twee MPI-bibliotheken die ondersteuning bieden voor de stuurprogramma's in Azure.

CD adapco STER-CCM + 11.x vrijgeven en later wordt meegeleverd met Intel MPI-versie 5.x, dus InfiniBand-ondersteuning voor Azure opgenomen is.

Hallo Linux64 ophalen STER-CCM + pakket van Hallo [CD adapco portal](https://steve.cd-adapco.com). In ons geval hebben we versie 11.02.010 in gemengde precisie gebruikt.

Hoofdknooppunt Hallo in Hallo van **/hpcdata** Azure File delen, maakt u een shell-script met de naam **setupstarccm.sh** Hello inhoud te volgen. Dit script wordt uitgevoerd op elke compute knooppunt tooset up STER-CCM + lokaal.

#### <a name="sample-setupstarcmsh-script"></a>Voorbeeldscript setupstarcm.sh
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
Nu tooset up STER-CCM + op alle uw Linux rekenknooppunten, open een opdrachtprompt met verhoogde bevoegdheid en Voer Hallo volgende opdracht:

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

Tijdens het Hallo-opdracht wordt uitgevoerd, kunt u Hallo CPU-gebruik controleren met behulp van heatmap Hallo van Clusterbeheer. Na enkele minuten alle knooppunten moeten correct zijn ingesteld.

## <a name="run-star-ccm-jobs"></a>Uitvoeren van de STER-CCM + taken
HPC Pack wordt gebruikt voor de taak scheduler-mogelijkheden in volgorde toorun STER-CCM + taken. toodo dus moeten we ondersteuning van een paar scripts die zijn gebruikt toostart Hallo taak en STER worden uitgevoerd Hallo-CCM +. Hallo invoergegevens wordt opgeslagen op het Azure-bestandsshare Hallo eerste voor eenvoud.

Hallo volgende PowerShell-script is gebruikte tooqueue een STER-CCM + taak. Het duurt drie argumenten:

* Hallo modelnaam
* het aantal knooppunten toobe gebruikt Hallo
* Hallo aantal kernen op elk knooppunt toobe gebruikt

Omdat STER-CCM + kunt vullen Hallo geheugenbandbreedte, het doorgaans beter toouse minder cores per rekenknooppunten en nieuwe knooppunten toe te voegen. Hallo exacte aantal kernen per knooppunt, is afhankelijk van Hallo processorfamilie en Hallo tussen geheugenonderdelen snelheid.

Hallo knooppunten exclusief voor Hallo taak worden toegewezen en kunnen niet worden gedeeld met andere taken. Hallo-taak is niet rechtstreeks als een MPI-taak gestart. Hallo **runstarccm.sh** shellscript Hallo MPI launcher wordt gestart.

Hallo invoercode model en Hallo **runstarccm.sh** script worden opgeslagen in Hallo **/hpcdata** -share die eerder is gekoppeld.

Logboekbestanden worden benoemd met Hallo taak-ID en worden opgeslagen in Hallo **/hpcdata share**, samen met de Hallo STER-CCM + uitvoerbestanden.

#### <a name="sample-submitstarccmjobps1-script"></a>Voorbeeldscript SubmitStarccmJob.ps1
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
Vervang **runner.java** met uw voorkeur STER-CCM + Java model linksboven en logboekregistratie-code.

#### <a name="sample-runstarccmsh-script"></a>Voorbeeldscript runstarccm.sh
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

In onze test hebben we een token Power-On-Demand-licentie gebruikt. Voor dit token, hebt u tooset hello **$CDLMD_LICENSE_FILE** omgevingsvariabele te **1999@flex.cd-adapco.com**  en Hallo-sleutel in Hallo **- podkey** optie van Hallo-opdrachtregel .

Na enkele initialisatie Hallo script extraheert--uit Hallo **$CCP_NODES_CORES** omgevingsvariabelen die HPC Pack ingesteld--Hallo lijst met knooppunten toobuild maakt gebruik van een hostfile die Hallo MPI starten. Deze hostfile bevat Hallo lijst met namen van de compute nodes die worden gebruikt voor de taak hello, één naam per regel.

Hallo-indeling van **$CCP_NODES_CORES** volgt dit patroon:

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

Waar:

* `<Number of nodes>`is het aantal knooppunten toegewezen toothis taak Hallo.
* `<Name of node_n_...>`Hallo-naam van elk knooppunt toothis taak toegewezen is.
* `<Cores of node_n_...>`is het aantal kernen op Hallo-knooppunt toegewezen toothis taak Hallo.

het aantal kernen Hallo (**$NBCORES**) is ook het aantal knooppunten berekend op basis van hello (**$NBNODES**) en het aantal kernen per knooppunt hello (opgegeven als parameter **$NBCORESPERNODE**).

Hallo MPI-opties, Hallo waarden die worden gebruikt met Intel MPI in Azure zijn:

* `-mpi intel`toospecify Intel MPI.
* `-fabric UDAPL`toouse Azure InfiniBand termen.
* `-cpubind bandwidth,v`toooptimize bandbreedte voor MPI met STER-CCM +.
* `-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI werken met Azure InfiniBand en tooset Hallo het vereiste aantal kernen per knooppunt.
* `-batch`toostart STER-CCM + in batchmodus met geen gebruikersinterface.

Ten slotte toostart een taak, zorg dat uw knooppunten actief zijn en online in de Cluster-beheer zijn. Vanuit een PowerShell-opdrachtprompt voert u dit:

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a>Knooppunten stoppen
Later in nadat u met de tests uitgevoerd bent klaar, kunt u gebruiken Hallo HPC Pack PowerShell-opdrachten toostop te volgen en start knooppunten:

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a>Volgende stappen
Probeer andere werkbelastingen Linux wordt uitgevoerd. Bijvoorbeeld, Zie:

* [Voer NAMD met Microsoft HPC Pack op Linux-rekenknooppunten in Azure](hpcpack-cluster-namd.md)
* [OpenFOAM met Microsoft HPC Pack uitvoeren op een Linux RDMA-cluster in Azure](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
