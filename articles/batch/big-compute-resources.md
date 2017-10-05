---
title: Bronnen voor batch- en HPC in de Azure-cloud | Microsoft Docs
description: Een lijst met technische bronnen voor hulp bij het uitvoeren van uw grootschalige parallelle, batchverwerking en high performance computing (HPC)-workloads in Azure.
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: 18be9f503b57117a7e8f5f0a4e9c93614cc7755b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a>Grote in Azure Compute: technische bronnen voor batchverwerking en high performance computing
Dit is een handleiding voor technische bronnen voor hulp bij het uitvoeren van uw grootschalige parallelle, batchverwerking en high performance computing (HPC) werkbelastingen in Azure. Breid uw bestaande batch of HPC-workloads in de Azure-cloud of nieuwe Big Compute-oplossingen met een bereik van Azure-services bouwen.

## <a name="solutions-options"></a>Opties voor oplossingen
Lees meer over Big Compute-opties in Azure en kies de juiste aanpak voor uw werkbelasting en zakelijke behoeften.

* [Batch en HPC-oplossingen](batch-hpc-solutions.md)
* [-Video: Big Compute in de cloud met Azure- en HPC](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a>Azure Batch
[Batch](https://azure.microsoft.com/services/batch/) is een platformservice die het eenvoudiger om te schakelen voor de cloud uw Linux- en Windows-toepassingen en taken worden uitgevoerd zonder instellen en beheren van een cluster en taak scheduler maakt. Gebruik de SDK om toepassingen integreren met Azure Batch via diverse talen, fase gegevens naar Azure, en taak uitvoering pijplijnen bouwen.

* [Documentatie](https://azure.microsoft.com/documentation/services/batch/)
* [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), en [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API-referentiemateriaal
* [Batch management .NET-bibliotheek](https://msdn.microsoft.com/library/mt463120.aspx) verwijzing
* Zelfstudie: Aan de slag met [Azure Batch-bibliotheek voor .NET](batch-dotnet-get-started.md) en [Batch Python-client](batch-python-tutorial.md)
* [Batch-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [Batch-video 's](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a>HPC-clusteroplossingen
Implementeer of uw bestaande Windows of Linux HPC-cluster uitbreiden naar Azure uw berekenings-intensieve werkbelastingen uitvoeren.  

### <a name="microsoft-hpc-pack"></a>Microsoft HPC Pack
HPC Pack is oplossing van Microsoft gratis HPC gebouwd op Microsoft Azure en Windows Server-technologieën, kan worden uitgevoerd van Windows en Linux HPC werkbelastingen.  

* [HPC Pack 2016 downloaden](https://www.microsoft.com/download/details.aspx?id=54507)
* [HPC Pack 2012 R2 Update 3 downloaden](https://www.microsoft.com/download/details.aspx?id=49922)
* [Documentatie](https://technet.microsoft.com/library/jj899572.aspx)
* Opties voor het cluster in Azure HPC Pack: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) en [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 
* [Burst naar Azure worker-exemplaren met HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)
* [Azure batch met HPC Pack burst](https://technet.microsoft.com/library/mt612877.aspx)
* [Windows HPC-forums](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a>Linux- en OSS-clusteroplossingen
Gebruik deze Azure-sjablonen voor het implementeren van Linux-HPC-clusters.

* [Een cluster SLURM ronddraaien](https://azure.microsoft.com/documentation/templates/slurm/) en [blogbericht](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)
* [Een cluster koppel draaien](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [Raster sjablonen met PBS Professional te berekenen](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a>HPC-opslag
* [Parallelle bestandssystemen voor HPC-opslag in Azure](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [Intel Cloud Edition voor Lustre Software - evaluatie](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [BeeGFS op CentOS 7.2 sjabloon](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a>Microsoft MPI
[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is een Microsoft-implementatie van de standaard bericht doorgeven Interface voor het ontwikkelen en uitvoeren van parallelle toepassingen op het Windows-platform.

* [MS MPI downloaden](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [MS MPI-verwijzing](https://msdn.microsoft.com/library/dn473458.aspx)
* [MPI-forum](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a>Rekenintensieve instanties
Azure biedt een [bereik van VM-grootten](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), waaronder [rekenintensieve H-serie](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) exemplaren kunnen verbinding maken met een back-end RDMA-netwerk, uw Linux- en Windows HPC-workloads uitvoeren. 

* [Instellen van een cluster Linux RDMA MPI-toepassingen uitvoeren](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Instellen van een cluster met Windows RDMA met Microsoft HPC Pack MPI-toepassingen uitvoeren](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Bekijk voor GPU-intensieve werkbelastingen, [NC en NV grootten](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).

## <a name="samples-and-demos"></a>Voorbeelden en demo 's
* [Azure Batch C# en Python-codevoorbeelden](https://github.com/Azure/azure-batch-samples)
* [Batch-scheepswerf](https://azure.github.io/batch-shipyard/) toolkit voor een gemakkelijke implementatie van batch-stijl Dockerized werkbelastingen naar Azure Batch
* [doAzureParallel](http://www.github.com/Azure/doAzureParallel) R-pakket gebouwd op Azure Batch
* [Uitprobeert SUSE Linux Enterprise Server voor HPC](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a>Gerelateerde Azure Services
* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)
* [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Virtuele machines](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Virtuele-Machineschaalsets](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [Cloud Services](https://azure.microsoft.com/documentation/services/cloud-services/)
* [App Service](https://azure.microsoft.com/documentation/services/app-service/)
* [Media Services](https://azure.microsoft.com/documentation/services/media-services/)
* [Functies](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a>Architectuurblauwdrukken
* [HPC en gegevens orchestration met behulp van Azure Batch- en Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) en [artikel](../data-factory/data-factory-data-processing-using-batch.md)

## <a name="industry-solutions"></a>Oplossingen
* [Bank- en investering markten](https://finance.azure.com/)
* [Technische simulaties](https://simulation.azure.com/) 

## <a name="customer-stories"></a>Verhalen van klanten
* [ANEO](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [d3View](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [Ludwig Institute of kanker Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [Microsoft Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [Milliman](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [Mitsubishi UFJ effecten International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [Schlumberger](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [UberCloud](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a>Volgende stappen
* Bezoek het [teamblog voor Microsoft HPC en Batch](http://blogs.technet.com/b/windowshpc/) en het [Azure-blog](https://azure.microsoft.com/blog/tag/hpc/) voor de meest recente aankondigingen.
* Zie ook [wat is er nieuw in Batch](https://azure.microsoft.com/updates/?service=batch) of zich abonneert op de [RSS-feed](https://azure.microsoft.com/updates/feed/?service=batch).

