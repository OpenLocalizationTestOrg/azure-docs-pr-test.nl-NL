---
title: aaaSet van een Linux RDMA cluster toorun MPI-toepassingen | Microsoft Docs
description: Een Linux-cluster van de grootte van H16r, H16mr, A8 of A9-VM's toouse hello Azure RDMA netwerk toorun MPI-apps maken
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a>Instellen van een Linux RDMA cluster toorun MPI-toepassingen
Meer informatie over hoe tooset van een Linux RDMA-cluster in Azure met [hoge prestaties compute-VM-grootten](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallelle Message Passing Interface (MPI)-toepassingen. Dit artikel bevat stappen tooprepare een Linux HPC installatiekopie toorun Intel MPI op een cluster. Nadat de voorbereiding, moet u een cluster van virtuele machines met behulp van deze installatiekopie en een van de Hallo RDMA-compatibele Azure VM-grootten (H16mr momenteel H16r A8 of A9) implementeert. Hallo cluster toorun MPI-toepassingen die efficiënt via een lage latentie, een hoge gegevensdoorvoer netwerk op basis van remote direct memory access (RDMA)-technologie communiceren gebruiken.

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) en klassieke. In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

## <a name="cluster-deployment-options"></a>Cluster-implementatieopties
Hieronder vindt u methoden kunt u een cluster Linux RDMA toocreate met of zonder een Taakplanner.

* **Azure CLI-scripts**: Zie verderop in dit artikel, gebruikt u Hallo [Azure-opdrachtregelinterface](../../../cli-install-nodejs.md) (CLI) tooscript Hallo implementatie van een cluster met RDMA-compatibele virtuele machines. Hallo CLI in Service Management-modus maakt Hallo clusterknooppunten opeenvolgend in het klassieke implementatiemodel hello, dus veel rekenknooppunten implementeren kan enkele minuten duren. tooenable hello RDMA-netwerkverbinding wanneer u het klassieke implementatiemodel hello, Hallo virtuele machines implementeren in Hallo dezelfde cloudservice.
* **Azure Resource Manager-sjablonen**: U kunt ook Hallo Resource Manager deployment model toodeploy een cluster met RDMA-compatibele virtuele machines die toohello RDMA netwerk verbindt. U kunt [uw eigen sjabloon maken](../../../resource-group-authoring-templates.md), of Controleer Hallo [Azure-snelstartsjablonen](https://azure.microsoft.com/documentation/templates/) voor sjablonen die is bijgedragen door Microsoft of Hallo community toodeploy Hallo gewenste oplossing. Resource Manager-sjablonen kunnen bieden een snelle en betrouwbare manier toodeploy een Linux-cluster. tooenable hello RDMA-netwerkverbinding wanneer u Hallo Resource Manager-implementatiemodel implementeren Hallo VM's in Hallo dezelfde beschikbaarheidsset.
* **HPC Pack**: een Microsoft HPC Pack-cluster in Azure maken en toevoegen van RDMA-compatibele rekenknooppunten waarop een ondersteunde Linux distributie tooaccess hello RDMA-netwerk wordt uitgevoerd. Zie voor meer informatie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md).

## <a name="sample-deployment-steps-in-hello-classic-model"></a>Voorbeeld-implementatiestappen in het klassieke model Hallo
Hallo volgende stappen laten zien hoe toouse hello Azure CLI toodeploy een SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM van hello Azure Marketplace, aanpassen en een aangepaste installatiekopie van de virtuele machine maken. Vervolgens kunt u Hallo tooscript Hallo implementatie van de installatiekopie van een cluster van RDMA-compatibele virtuele machines.

> [!TIP]
> Gebruik dezelfde stappen toodeploy die een cluster met RDMA-compatibele virtuele machines op basis van installatiekopieën op basis van CentOS HPC in hello Azure Marketplace. Een aantal stappen verschillen, zoals aangegeven. 
>
>

### <a name="prerequisites"></a>Vereisten
* **Clientcomputer**: U moet een Mac, Linux of Windows client computer toocommunicate met Azure. Deze stappen wordt ervan uitgegaan dat u een Linux-client.
* **Azure-abonnement**: als u geen een abonnement hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten. Voor grotere clusters kunt u een abonnement op gebruiksbasis of andere Aankoopopties.
* **Beschikbaarheid van de VM-grootte**: Hallo na instanties zijn RDMA-compatibele: H16r, H16mr A8 en A9. Controleer [producten die beschikbaar zijn in elke regio](https://azure.microsoft.com/regions/services/) voor beschikbaarheid in een Azure-regio's.
* **Quotum voor kernen**: tooincrease Hallo quotum van kernen toodeploy een cluster van virtuele machines rekenintensieve moet u mogelijk. Bijvoorbeeld, moet u ten minste 128 kernen als u wilt dat toodeploy 8 A9 VM's zoals in dit artikel. Uw abonnement mogelijk ook het aantal kernen dat u in bepaalde VM grootte families implementeren kunt, met inbegrip van Hallo H-serie Hallo beperken. toorequest een quotum verhogen, [opent u een ondersteuningsaanvraag online klant](../../../azure-supportability/how-to-create-azure-support-request.md) zonder kosten.
* **Azure CLI**: [installeren](../../../cli-install-nodejs.md) hello Azure CLI en [tooyour Azure-abonnement verbinden](../../../xplat-cli-connect.md) van Hallo-clientcomputer.

### <a name="provision-an-sles-12-sp1-hpc-vm"></a>Een VM SLES 12 SP1 HPC inrichten
Voer na het aanmelden tooAzure Hello Azure CLI, `azure config list` tooconfirm die Hallo uitvoer toont Service Management-modus. Als dit niet het geval is, stelt u Hallo-modus met deze opdracht:

    azure config mode asm


Hallo toolist na alle Hallo abonnementen zijn van bevoegde toouse typt u:

    azure account list

de huidige actieve abonnement Hallo wordt geïdentificeerd met `Current` instellen te`true`. Als dit abonnement niet Hallo u toouse toocreate Hallo cluster wilt toevoegen, Hallo juiste abonnements-ID als Hallo actief abonnement instellen:

    azure account set <subscription-Id>

toosee Hallo openbaar SLES 12 SP1 HPC-afbeeldingen in Azure, voert u een opdracht zoals hello te volgen, ervan uitgaande dat uw omgeving shell ondersteunt **grep**:

    azure vm image list | grep "suse.*hpc"

Richt een RDMA-compatibele virtuele machine met een installatiekopie SLES 12 SP1 HPC door het uitvoeren van een opdracht zoals Hallo volgende:

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

Waar:

* Hallo grootte (A9 in dit voorbeeld) is een van de VM-grootten Hallo RDMA-functionaliteit.
* Hallo externe SSH-poortnummer (22 in dit voorbeeld Hallo SSH standaard is) is een geldig poortnummer. Hallo interne SSH-poortnummer is too22 ingesteld.
* Een nieuwe cloudservice wordt gemaakt in hello Azure-regio op Hallo locatie opgegeven. Geef een locatie in welke Hallo VM grootte die u kiest beschikbaar is.
* Voor ondersteuning van prioriteit SUSE (die extra kosten in rekening worden gebracht), de naam van de installatiekopie Hallo SLES 12 SP1 momenteel kan bestaan uit een van deze twee opties: 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a>Hallo VM aanpassen
Nadat Hallo VM is ingericht, wordt SSH toohello VM via Hallo van het externe IP-adres van de virtuele machine (of DNS-naam) en Hallo externe poortnummer dat u hebt geconfigureerd en deze aanpassen. Zie voor meer informatie verbinding [hoe toolog op tooa virtuele machine met Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Opdrachten uitvoeren als Hallo-gebruiker die u hebt geconfigureerd op Hallo VM, tenzij de toegang tot de hoofdmap is vereist toocomplete een stap.

> [!IMPORTANT]
> Microsoft Azure biedt geen toegang tot de hoofdmap tooLinux virtuele machines. beheerderstoegang toogain wanneer verbonden als een gebruiker toohello VM, het uitvoeren van opdrachten via `sudo`.
>
>

* **Updates**: Installeer updates met behulp van zypper. U kunt ook tooinstall NFS-hulpprogramma's.

  > [!IMPORTANT]
  > U wordt aangeraden dat u kernel-updates, wat leiden problemen Hello Linux RDMA stuurprogramma's tot kunnen niet toe te passen in een VM SLES 12 SP1 HPC.
  >
  >
* **Intel MPI**: Hallo-installatie van Intel MPI op Hallo SLES 12 SP1 HPC VM voltooid door het uitvoeren van de volgende opdracht Hallo:

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* **Vergrendelen van geheugen**: voor MPI-codes toolock Hallo geheugen beschikbaar voor RDMA, toevoegen of wijzigen van de volgende instellingen in Hallo /etc/security/limits.conf bestand Hallo. U moet dit bestand hoofdmap toegang tooedit.

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > U kunt ook memlock toounlimited instellen voor testdoeleinden. Bijvoorbeeld: `<User or group name>    hard    memlock unlimited`. Zie voor meer informatie [aanbevolen bekende methoden voor instelling vergrendeld geheugengrootte](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).
  >
  >
* **SSH-sleutels voor virtuele machines SLES**: genereren SSH-sleutels tooestablish vertrouwensrelatie voor uw gebruikersaccount tussen Hallo rekenknooppunten in Hallo SLES cluster bij het uitvoeren van MPI-taken. Als u een VM op basis van CentOS HPC hebt geïmplementeerd, niet volgt u deze stap. Zie de instructies verderop in dit artikel tooset up passwordless SSH-vertrouwensrelatie tussen de clusterknooppunten Hallo na het Hallo-installatiekopie en Hallo-cluster implementeren.

    toocreate SSH-sleutels, Hallo volgende opdracht uitvoeren. Wanneer u wordt gevraagd om invoer, selecteert u **Enter** toogenerate Hallo sleutels in de standaardlocatie Hallo zonder een wachtwoord wordt ingesteld.

        ssh-keygen

    Toevoegen van Hallo openbare sleutel toohello authorized_keys voor bekende openbare sleutels.

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    In Hallo ~/.ssh directory bewerken of Hallo-configuratiebestand te maken. Hallo IP-adresbereik van het particuliere netwerk Hallo bieden dat u van plan toouse in Azure (10.32.0.0/16 in dit voorbeeld bent):

        host 10.32.0.*
        StrictHostKeyChecking no

    U kunt ook als volgt Hallo particulier netwerk-IP-adres van elke virtuele machine in het cluster weergeven:

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > Configureren van `StrictHostKeyChecking no` een beveiligingsrisico met zich mee kunt maken wanneer er een specifiek IP-adres of -bereik is opgegeven.
  >
  >
* **Toepassingen**: installeert u alle toepassingen die u nodig hebt of andere aanpassingen uitvoeren voordat u Hallo installatiekopie vastleggen.

### <a name="capture-hello-image"></a>Hallo installatiekopie vastleggen
toocapture hello afbeelding, Hallo volgende opdracht op Hallo Linux-VM voor het eerst uitvoert. Met deze opdracht Hallo VM deprovisions maar behoudt gebruikersaccounts en SSH-sleutels die u hebt ingesteld.

```
sudo waagent -deprovision
```

Uitvoeren vanaf de clientcomputer hello Azure CLI-opdrachten toocapture Hallo installatiekopie te volgen. Zie voor meer informatie [hoe toocapture klassieke virtuele Linux-machine als afbeelding](capture-image.md).  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

Nadat u deze opdrachten uitgevoerd, Hallo VM-installatiekopie wordt vastgelegd voor het gebruik en Hallo VM is verwijderd. Nu hebt u uw aangepaste installatiekopie gereed toodeploy een cluster.

### <a name="deploy-a-cluster-with-hello-image"></a>Een installatiekopie van het Hallo-cluster implementeren
Hallo Bash-script met de juiste waarden voor uw omgeving te volgen wijzigen en uitvoeren vanaf de clientcomputer. Omdat Azure Hallo VMs opeenvolgend in het klassieke implementatiemodel Hallo implementeert, duurt het enkele minuten toodeploy Hallo acht A9-VM's in dit script wordt voorgesteld.

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a>Overwegingen voor een CentOS HPC-cluster
Als u tooset van een op basis van een van de Hallo op basis van CentOS HPC-afbeeldingen in hello Azure Marketplace in plaats van SLES 12 voor HPC-cluster wilt, stappen Hallo Algemeen in de voorgaande sectie Hallo. Houd er rekening mee Hallo verschillen volgen wanneer u inricht en Hallo VM configureert:

- Intel MPI is al geïnstalleerd op een virtuele machine vanaf een installatiekopie van een HPC op basis van CentOS wordt ingericht.
- Vergrendeling geheugeninstellingen zijn al toegevoegd in Hallo van de virtuele machine /etc/security/limits.conf-bestand.
- Genereren geen SSH-sleutels op Hallo VM die u inricht voor vastleggen. In plaats daarvan wordt aangeraden verificatie op basis van een gebruiker instellen nadat u Hallo-cluster implementeren. Zie Hallo volgende sectie voor meer informatie.  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a>Passwordless SSH vertrouwen op Hallo cluster instellen
Op een op basis van CentOS HPC-cluster, er zijn twee methoden voor het instellen van een vertrouwensrelatie tussen de rekenknooppunten Hallo: verificatie op basis van de host en verificatie op basis van gebruiker. Verificatie op basis van een host bevindt zich buiten het bereik van dit artikel hello en in het algemeen moet worden uitgevoerd via een script extensie tijdens de implementatie. Verificatie op basis van een gebruiker is handig voor het instellen van een vertrouwensrelatie na de implementatie en vereist Hallo genereren en delen van SSH-sleutels tussen Hallo rekenknooppunten in Hallo-cluster. Deze methode staat bekend als passwordless SSH-aanmelding en is vereist bij het uitvoeren van MPI-taken.

Een voorbeeld van een script bijgedragen Hallo community is beschikbaar op [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable eenvoudig gebruikersverificatie op een op basis van CentOS HPC-cluster. Download en gebruik dit script met behulp van Hallo stappen te volgen. U kunt ook dit script wijzigen of een andere methode tooestablish passwordless SSH-verificatie tussen de clusterknooppunten compute hello gebruiken.

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

toorun hello script, moet u tooknow Hallo voorvoegsel voor uw subnet IP-adressen. Hallo voorvoegsel ophalen door het uitvoeren van de volgende opdracht op een van de clusterknooppunten Hallo Hallo. De uitvoer ziet er ongeveer als 10.1.3.5 en Hallo-voorvoegsel is Hallo/m 10.1.3 gedeelte.

    ifconfig eth0 | grep -w inet | awk '{print $2}'

Voer nu Hallo script met drie parameters: algemene gebruikersnaam op Hallo Hallo rekenknooppunten, Hallo gemeenschappelijk wachtwoord voor die gebruiker op Hallo van rekenknooppunten en Hallo subnetvoorvoegsel die is geretourneerd van de vorige opdracht Hallo.

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

Dit script Hallo te volgen:

* Maakt een map op Hallo hostknooppunt met SSH, de naam die is vereist voor passwordless aanmelding.
* Maakt een configuratiebestand in Hallo SSH directory zodat passwordless aanmelding tooallow aanmelding vanaf elk knooppunt in het Hallo-cluster.
* Bestanden met Hallo node names en knooppunt IP-adressen voor alle Hallo knooppunten in Hallo-cluster maakt. Deze bestanden blijven nadat het Hallo-script wordt uitgevoerd voor naslagdoeleinden.
* Maakt een persoonlijke en openbare sleutelpaar voor elk clusterknooppunt (inclusief Hallo hostknooppunt) en vermeldingen in Hallo authorized_keys bestand maakt.

> [!WARNING]
> Dit script uitvoert, kan een beveiligingsrisico met zich mee maken. Zorg ervoor dat Hallo openbare sleutelinformatie in ~/.ssh niet is gedistribueerd.
>
>

## <a name="configure-intel-mpi"></a>Intel MPI configureren
toorun MPI-toepassingen op Azure Linux RDMA, moet u tooconfigure bepaalde omgeving variabelen specifieke tooIntel MPI. Hier volgt een voorbeeld Bash script tooconfigure Hallo variabelen nodig toorun een toepassing. Hallo pad toompivars.sh Wijzig zo nodig voor de installatie van Intel MPI.

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

Hallo-indeling van het hostbestand Hallo is als volgt. Een regel voor elk knooppunt in het cluster toevoegen. Geef de privé IP-adressen van het virtuele netwerk Hallo eerder hebt gedefinieerd, niet de DNS-namen. Hallo-bestand bevat bijvoorbeeld voor twee hosts met IP-adressen 10.32.0.1 en 10.32.0.2 Hallo volgende:

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a>MPI worden uitgevoerd op een basic cluster met twee knooppunten
Als u dit nog niet hebt gedaan, eerst Hallo omgeving instellen voor Intel MPI.

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a>Voer een MPI-opdracht
Een MPI-opdracht uitvoeren op een van de Hallo compute knooppunten tooshow die MPI juist is geïnstalleerd en kan communiceren tussen ten minste twee rekenknooppunten. Hallo volgende **mpirun** opdracht wordt uitgevoerd Hallo **hostnaam** opdracht op twee knooppunten.

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
De uitvoer moet lijst Hallo-namen van alle Hallo knooppunten die u hebt doorgegeven als invoer voor `-hosts`. Bijvoorbeeld, een **mpirun** opdracht met twee knooppunten retourneert Hallo volgende uitvoer:

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a>Voer een benchmark MPI
Hallo volgende Intel MPI-opdracht wordt uitgevoerd een pingpong benchmark tooverify Hallo configuratie en verbinding toohello RDMA clusternetwerk.

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

Op een werkende-cluster met twee knooppunten ziet u uitvoer zoals Hallo volgende. Verwacht op Hallo RDMA Azure-netwerk, latentie op of onder 3 microseconden voor berichtgrootten up too512 bytes.

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a>Volgende stappen
* Implementeren en uw Linux MPI-toepassingen uitvoeren op uw Linux-cluster.
* Zie Hallo [Intel MPI-bibliotheek documentatie](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) voor hulp bij het Intel MPI.
* Probeer een [snelstartsjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate een Intel Lustre met behulp van een installatiekopie op basis van CentOS HPC-cluster. Zie voor meer informatie [Intel Cloud Edition implementeren voor Lustre in Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).
