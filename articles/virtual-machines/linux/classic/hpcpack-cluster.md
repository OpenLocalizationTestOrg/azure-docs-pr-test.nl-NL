---
title: aaaLinux compute virtuele machines in een cluster HPC Pack | Microsoft Docs
description: Meer informatie over hoe toocreate en gebruik een Pack HPC-cluster in Azure voor Linux van de high performance computing (HPC)-workloads
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Aan de slag met Linux-rekenknooppunten in een HPC Pack-cluster in Azure
Instellen van een [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure met een hoofdknooppunt met Windows Server en meerdere rekenknooppunten met een ondersteunde Linux-distributie. Verken opties toomove gegevens tussen Hallo Linux-knooppunten en Hallo Windows-hoofdknooppunt van het Hallo-cluster. Meer informatie over hoe toosubmit Linux HPC cluster toohello taken.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Op een hoog niveau hello volgende diagram toont Hallo HPC Pack cluster u maken en bewerken.

![HPC Pack cluster met Linux-knooppunten][scenario]

Voor andere opties toorun Linux HPC werkbelastingen in Azure, Zie [technische bronnen voor batchverwerking en high performance computing](../../../batch/big-compute-resources.md).

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a>Een HPC Pack cluster met Linux-rekenknooppunten implementeren
Dit artikel ziet u twee opties toodeploy een HPC Pack-cluster in Azure met Linux-rekenknooppunten. Beide methoden gebruiken een Marketplace-installatiekopie van Windows Server met HPC Pack toocreate Hallo hoofdknooppunt. 

* **Azure Resource Manager-sjabloon** -een sjabloon uit Azure Marketplace hello of een snelstartsjabloon van Hallo-community, tooautomate maken van Hallo-cluster in Hallo Resource Manager-implementatiemodel. Bijvoorbeeld, Hallo [HPC Pack cluster voor Linux-werkbelastingen](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) sjabloon in hello Azure Marketplace maakt een complete HPC Pack clusterinfrastructuur voor Linux HPC werkbelastingen.
* **PowerShell-script** -gebruik Hallo [Microsoft HPC Pack IaaS-implementatiescript](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**nieuw HpcIaaSCluster.ps1**) tooautomate een volledige Clusterimplementatie Hallo klassieke implementatiemodel. Deze Azure PowerShell-script maakt gebruik van een installatiekopie van een HPC Pack VM in hello Azure Marketplace voor snelle implementatie en biedt een uitgebreide set configuratie parameters toodeploy Linux-rekenknooppunten.

Zie voor meer informatie over opties voor de implementatie van HPC Pack cluster in Azure [toocreate opties en beheren van een cluster high performance computing (HPC) in Azure met Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="prerequisites"></a>Vereisten
* **Azure-abonnement** -kunt u een abonnement in beide hello Azure globale of Azure China-service. Als u geen account hebt, kunt u een [gratis account](https://azure.microsoft.com/pricing/free-trial/) binnen een paar minuten.
* **Quotum voor kernen** -moet u mogelijk tooincrease Hallo quotum van kernen, met name als u verschillende clusterknooppunten met multicore VM-grootten toodeploy kiezen. tooincrease een quotum, opent u een ondersteuningsaanvraag online klant zonder kosten.
* **Linux-distributies** -momenteel HPC Pack Hallo volgende Linux-distributies rekenknooppunten ondersteunt. U kunt Marketplace-versies van deze verdelingen gebruiken indien beschikbaar, of geef uw eigen.
  
  * **Op basis van centOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC
  * **Red Hat Enterprise Linux**: 6.7, 6,8, 7.2
  * **SUSE Linux Enterprise Server**: SLES 12 SLES 12 (Premium) SLES 12 SP1, SLES 12 SP1 (Premium) SLES 12 voor HPC SLES 12 voor HPC (Premium)
  * **Ubuntu Server**: 14.04 TNS, 16.04 TNS
    
    > [!TIP]
    > toouse hello Azure RDMA-netwerk met een van de RDMA-compatibele Hallo VM-grootten, Geef een SUSE Linux Enterprise Server 12 HPC of op basis van CentOS HPC-installatiekopie uit hello Azure Marketplace. Zie voor meer informatie [hoge prestaties compute-VM-grootten](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

Aanvullende vereisten toodeploy Hallo-cluster met behulp van Hallo HPC Pack IaaS-implementatiescript:

* **Clientcomputer** -u moet een implementatiescript van Windows-clientapparaten computer toorun Hallo cluster.
* **Azure PowerShell** - [installeren en configureren van Azure PowerShell](/powershell/azure/overview) (versie 0.8.10 of hoger) op de clientcomputer.
* **HPC Pack IaaS-implementatiescript** - downloaden en uitpakken Hallo meest recente versie van script Hallo van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). U kunt Hallo-versie van script Hallo controleren door te voeren `.\New-HPCIaaSCluster.ps1 –Version`. In dit artikel is gebaseerd op versie 4.4.1 of hoger van Hallo-script.

### <a name="deployment-option-1-use-a-resource-manager-template"></a>Implementatieoptie 1. Een Resource Manager-sjabloon gebruiken
1. Ga toohello [HPC Pack cluster voor Linux-werkbelastingen](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) sjabloon in Azure Marketplace Hallo en klik op **implementeren**.
2. In Azure-portal hello, Hallo informatie bekijken en klik op **maken**.
   
    ![Maken van de portal][portal]
3. Op Hallo **basisbeginselen** blade een naam voor het Hallo-cluster, die ook de namen van hoofdknooppunt Hallo VM. U kunt een bestaande resourcegroep kiezen of een groep voor de implementatie van Hallo maken in een locatie die beschikbaar tooyou. Hallo locatie is van invloed op Hallo beschikbaarheid van bepaalde VM-grootten en andere Azure-services (Zie [producten die beschikbaar zijn in elke regio](https://azure.microsoft.com/regions/services/)).
4. Op Hallo **Head knooppunt instellingen** blade voor een eerste implementatie, kunt u in het algemeen Hallo standaardinstellingen accepteren. 
   
   > [!NOTE]
   > Hallo **post-configuratiescript URL** is een optionele instelling toospecify openbaar beschikbare Windows PowerShell-script dat u toorun op Hallo hoofdknooppunt VM wilt nadat deze wordt uitgevoerd. 
   > 
   > 
5. Op Hallo **Compute knooppunt instellingen** blade selecteren van een naamgevingspatroon uit voor het Hallo-knooppunten, Hallo aantal en grootte van Hallo knooppunten en Linux-distributie toodeploy Hallo.
6. Op Hallo **infrastructuurinstellingen** blade Voer namen voor Hallo virtueel netwerk en Active Directory domain, domein en VM-beheerdersreferenties en naamgevingspatroon uit een voor Hallo storage-accounts.
   
   > [!NOTE]
   > HPC Pack Hallo Active Directory-domein tooauthenticate cluster gebruikers gebruikt. 
   > 
   > 
7. Nadat de validatietests Hallo uitgevoerd en u de gebruiksvoorwaarden Hallo bekijken, klikt u op **aankoop**.

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a>Implementatieoptie 2. Hallo IaaS-implementatiescript gebruiken
Hieronder vindt u aanvullende vereisten toodeploy Hallo cluster met behulp van Hallo HPC Pack IaaS-implementatiescript:

* **Clientcomputer** -u moet een implementatiescript van Windows-clientapparaten computer toorun Hallo cluster.
* **Azure PowerShell** - [installeren en configureren van Azure PowerShell](/powershell/azure/overview) (versie 0.8.10 of hoger) op de clientcomputer.
* **HPC Pack IaaS-implementatiescript** - downloaden en uitpakken Hallo meest recente versie van script Hallo van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). U kunt Hallo-versie van script Hallo controleren door te voeren `.\New-HPCIaaSCluster.ps1 –Version`. In dit artikel is gebaseerd op versie 4.4.1 of hoger van Hallo-script.

**XML-configuratiebestand**

een XML-configuratiebestand Hallo HPC Pack IaaS-implementatiescript gebruikt als invoer toodescribe Hallo HPC-cluster. Hallo geeft volgende voorbeeldconfiguratiebestand een kort cluster die bestaan uit een hoofdknooppunt HPC Pack en twee grootte A7 CentOS 7.0 Linux-rekenknooppunten. 

Hallo-bestand aanpassen nodig zijn voor uw omgeving en de configuratie van het gewenste cluster en sla het bestand met een naam, zoals HPCDemoConfig.xml. U moet bijvoorbeeld toosupply de abonnementsnaam van uw en een unieke opslagaccountnaam en de naam van cloud-service. U kunt bovendien toochoose een andere Linux installatiekopie Hallo rekenknooppunten ondersteund. Zie voor meer informatie over het Hallo-elementen in het configuratiebestand Hallo Hallo Manual.rtf bestand in map voor Hallo-script en [een HPC-cluster maken met Hallo HPC Pack IaaS-implementatiescript](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

**toorun hello HPC Pack IaaS-implementatiescript**

1. Open Windows PowerShell op de clientcomputer Hallo als beheerder.
2. Wijziging toohello uit de map waar het Hallo-script is geïnstalleerd (E:\IaaSClusterScript in dit voorbeeld).
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. Hallo na de opdracht toodeploy Hallo HPC Pack cluster worden uitgevoerd. In dit voorbeeld wordt ervan uitgegaan dat configuratiebestand Hallo bevindt zich in E:\HPCDemoConfig.xml
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    a. Omdat Hallo **AdminPassword** is niet opgegeven in Hallo voorafgaand aan de opdracht, bent u na vragen aan gebruiker tooenter Hallo wachtwoord voor gebruiker *MyAdminName*.
   
    b. Hallo-script wordt gestart toovalidate Hallo-configuratiebestand. Tooseveral minuten, afhankelijk van de netwerkverbinding Hallo kan duren.
   
    ![Validatie][validate]
   
    c. Nadat de validaties doorgeven, bevat Hallo script Hallo cluster resources toocreate. Voer *Y* toocontinue.
   
    ![Resources][resources]
   
    d. Hallo script start toodeploy Hallo HPC Pack cluster en Hallo-configuratie zonder verdere handmatige stappen is voltooid. Hallo-script kunt uitvoeren voor enkele minuten.
   
    ![Implementeren][deploy]
   
   > [!NOTE]
   > In dit voorbeeld Hallo script genereert een logboekbestand automatisch sinds Hallo **- LogFile** parameter is niet opgegeven. Hallo-Logboeken in realtime niet worden geschreven, maar worden verzameld achter Hallo Hallo validatie en Hallo-implementatie. Als Hallo PowerShell-proces is gestopt tijdens het Hallo-script wordt uitgevoerd, is enkele logboeken gaan verloren.
   > 
   > 

## <a name="connect-toohello-head-node"></a>Verbinding maken met het hoofdknooppunt toohello
Nadat u Hallo HPC Pack cluster in Azure worden geïmplementeerd [verbinding maken met extern bureaublad](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello hoofdknooppunt VM gebruik Hallo domeinreferenties die u hebt opgegeven tijdens de implementatie Hallo-cluster (bijvoorbeeld *hpc\\ clusteradmin*). U beheren Hallo cluster vanaf het hoofdknooppunt Hallo.

Start op het hoofdknooppunt Hallo HPC Cluster Manager toocheck Hallo status van Hallo HPC Pack cluster. U kunt beheren en bewaken van Linux-rekenknooppunten hello dezelfde manier werken met Windows rekenknooppunten. Zie bijvoorbeeld Hallo Linux-knooppunten die worden vermeld in **bronbeheer** (deze knooppunten worden geïmplementeerd met Hallo **LinuxNode** sjabloon).

![Knooppunt Management][management]

U ziet ook Hallo Linux-knooppunten in Hallo **Heatmap** weergeven.

![Heatmap][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a>Hoe toomove gegevens in een cluster met Linux-knooppunten
U hebt verschillende opties toomove gegevens tussen Linux-knooppunten en Hallo Windows-hoofdknooppunt van het Hallo-cluster. Hier volgen drie algemene methoden in de volgende secties Hallo uitvoeriger beschreven:

* **Azure File** -gegarandeerd dat een beheerde SMB-share toostore bestandsgegevens in Azure-opslag-bestanden. Knooppunten voor Windows en Linux-knooppunten een Azure-bestandsshare kunnen koppelen als een station of een map op Hallo dezelfde tijd, zelfs als ze zijn geïmplementeerd in verschillende virtuele netwerken.
* **Hoofdknooppunt SMB-share** -koppelt een standaard gedeelde Windows-map van het hoofdknooppunt Hallo op Linux-knooppunten.
* **HEAD knooppunt NFS-server** -biedt een oplossing voor het delen van bestanden voor een gemengde omgeving van Windows en Linux.

### <a name="azure-file-storage"></a>Azure File storage
Hallo [Azure File](https://azure.microsoft.com/services/storage/files/) -service geeft bestandsshares met behulp van Hallo standaard SMB 2.1-protocol. Azure virtuele machines en cloudservices kunnen bestandsgegevens delen tussen toepassingsonderdelen via gekoppelde shares en on-premises toepassingen hebben toegang tot bestandsgegevens in een share via Hallo File storage-API. 

Zie voor gedetailleerde stappen toocreate een Azure-bestand delen en koppel deze aan Hallo hoofdknooppunt [aan de slag met Azure File storage in Windows](../../../storage/files/storage-how-to-use-files-windows.md). toomount hello Azure-bestandsshare op Hallo van Linux-knooppunten, Zie [hoe toouse Azure File storage met Linux](../../../storage/files/storage-how-to-use-files-linux.md). Zie tooset persistent maken verbindingen [Persisting verbindingen tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).

In Hallo voorbeeld te volgen, maakt u een Azure-bestandsshare op een opslagaccount. Hallo toomount delen op Hallo hoofdknooppunt, open een opdrachtprompt en voert u Hallo volgende opdrachten:

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

In dit voorbeeld allvhdsje is de naam van uw opslagaccount, storageaccountkey is de sleutel van uw opslagaccount en rdma is hello Azure File-sharenaam. Hello Azure-bestandsshare is gekoppeld als Z: op Hallo hoofdknooppunt.

toomount hello Azure-bestandsshare op Linux-knooppunten, voer een **clusrun** opdracht op Hallo hoofdknooppunt. **[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  is een nuttig HPC Pack hulpprogramma toocarry administratieve taken op meerdere knooppunten. (Zie ook [Clusrun voor Linux-knooppunten](#Clusrun-for-Linux-nodes) in dit artikel.)

Open een Windows PowerShell-venster en Voer Hallo volgende opdrachten:

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

de eerste opdracht Hallo maakt een map met de naam /rdma op alle knooppunten in Hallo LinuxNodes groep. de tweede opdracht Hallo koppelt hello Azure File share allvhdsjw.file.core.windows.net/rdma op Hallo /rdma map met dir en de bestandsnaam modus bits set too777. In de tweede opdracht Hallo allvhdsje is de naam van uw opslagaccount en storageaccountkey is sleutel van uw opslagaccount.

> [!NOTE]
> Hallo '\`' symbool in de tweede opdracht Hallo is een escapeteken voor PowerShell. "\`, 'betekent dat Hallo', ' (door komma's teken) maakt deel uit van Hallo-opdracht.
> 
> 

### <a name="head-node-share"></a>Hoofdknooppunt share
U kunt ook een gedeelde map van het hoofdknooppunt Hallo op Linux-knooppunten koppelen. Een share bevat Hallo eenvoudigste manier waarop tooshare bestanden, maar Hallo hoofdknooppunt en alle Linux-knooppunten moeten worden geïmplementeerd in Hallo hetzelfde virtuele netwerk. Hier volgen de stappen Hallo.

1. Maak een map op het hoofdknooppunt Hallo en tooEveryone delen met de machtiging lezen/schrijven. Bijvoorbeeld D:\OpenFOAM delen op Hallo hoofdknooppunt als \\CentOS7RDMA HN\OpenFOAM. Hier volgt CentOS7RDMA HN Hallo hostname van Hallo hoofdknooppunt.
   
    ![Machtigingen voor de bestandsshare][fileshareperms]
   
    ![Delen van bestanden][filesharing]
2. Open een Windows PowerShell-venster en Voer Hallo volgende opdrachten uit:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

de eerste opdracht Hallo maakt een map met de naam /openfoam op alle knooppunten in Hallo LinuxNodes groep. de tweede opdracht Hallo koppelt Hallo gedeelde map //CentOS7RDMA-HN/OpenFOAM op Hallo-map met dir en de bestandsnaam modus bits set too777. Hallo moet gebruikersnaam en wachtwoord in Hallo-opdracht Hallo gebruikersnaam en wachtwoord van een gebruiker van het cluster op Hallo hoofdknooppunt. (Zie [toevoegen of verwijderen cluster gebruikers](https://technet.microsoft.com/library/ff919330.aspx).)

> [!NOTE]
> Hallo '\`' symbool in de tweede opdracht Hallo is een escapeteken voor PowerShell. "\`, 'betekent dat Hallo', ' (door komma's teken) maakt deel uit van Hallo-opdracht.
> 
> 

### <a name="nfs-server"></a>NFS-server
Hallo NFS-service kunt u tooshare en migreren van bestanden tussen computers met besturingssystemen Hallo Windows Server 2012 met behulp van SMB-protocol Hallo en met Hallo NFS-protocol op basis van Linux-computers. Hallo NFS-server en alle andere knooppunten hebben geïmplementeerd in Hallo toobe hetzelfde virtuele netwerk. Dit biedt betere compatibiliteit met Linux-knooppunten vergeleken met een SMB-share. Bijvoorbeeld: het bestandskoppelingen ondersteunt.

1. tooinstall en stelt u de NFS-server stappen Hallo in [Server voor Network File System-eerste Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).
   
    Maak bijvoorbeeld een NFS-share met de naam nfs Hello volgende eigenschappen:
   
    ![NFS-autorisatie][nfsauth]
   
    ![NFS-sharemachtigingen][nfsshare]
   
    ![NFS-NTFS-machtigingen][nfsperm]
   
    ![Eigenschappen van de NFS-beheer][nfsmanage]
2. Open een Windows PowerShell-venster en Voer Hallo volgende opdrachten uit:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   de eerste opdracht Hallo maakt een map met de naam /nfsshared op alle knooppunten in Hallo LinuxNodes groep. Hallo tweede opdracht koppelingen Hallo NFS delen CentOS7RDMA HN: / nfs op Hallo map. Hier CentOS7RDMA HN:-nfs Hallo extern pad van de NFS-share is.

## <a name="how-toosubmit-jobs"></a>Hoe toosubmit taken
Er zijn verschillende manieren toosubmit taken toohello HPC Pack cluster:

* HPC Cluster Manager of HPC Job Manager GUI
* HPC-webportal
* REST API

Verzending van de taak toohello cluster in Azure via HPC Pack GUI-hulpprogramma's en Hallo HPC-webportal Hallo zijn dezelfde als voor Windows-rekenknooppunten. Zie [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) en [hoe toosubmit taken uit een on-premises clientcomputer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

toosubmit-taken via Hallo REST-API te verwijzen[maken en verzenden van taken op met de REST-API in Microsoft HPC Pack Hallo](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx). toosubmit taken van een Linux-client ook verwijzen toohello Python voorbeeld in Hallo [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).

## <a name="clusrun-for-linux-nodes"></a>Clusrun voor Linux-knooppunten
HPC Pack Hallo [clusrun](https://technet.microsoft.com/library/cc947685.aspx) hulpprogramma kan worden gebruikt tooexecute opdrachten op Linux-knooppunten via een opdrachtprompt of HPC Cluster Manager. Hier volgen enkele eenvoudige voorbeelden.

* Huidige gebruikersnamen op alle knooppunten in cluster Hallo weergeven.
  
    ```command
    clusrun whoami
    ```
* Hallo installeren **gdb** foutopsporingsprogramma met **yum** op alle knooppunten in Hallo linuxnodes groeperen en Hallo knooppunten na 10 minuten opnieuw opstarten.
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* Een weergave van elk getal van 1 tot en met 10 voor één seconde op elk knooppunt van Linux in Hallo cluster shell-script maken, uitvoeren en de uitvoer van Hallo knooppunten onmiddellijk weergeven.
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> Mogelijk moet u toouse bepaalde escape-tekens in **clusrun** opdrachten. Zoals u in dit voorbeeld, gebruik ^ in een opdrachtprompt tooescape Hallo ' > ' symbool.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Probeer schaalt Hallo cluster tooa groter aantal knooppunten of het uitvoeren van een Linux-werkbelasting op Hallo-cluster. Zie voor een voorbeeld [NAMD uitvoeren met Microsoft HPC Pack op Linux-rekenknooppunten in Azure](hpcpack-cluster-namd.md).
* Probeer een cluster met [RDMA-functionaliteit, rekenintensieve VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI-belastingen. Zie voor een voorbeeld [OpenFOAM uitvoeren met Microsoft HPC Pack op een Linux RDMA-cluster in Azure](hpcpack-cluster-openfoam.md).
* Als u geïnteresseerd bent in het werken met Linux-knooppunten in een on-premises HPC Pack-cluster, raadpleegt u Hallo [TechNet richtlijnen](https://technet.microsoft.com/library/mt595803.aspx).

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
