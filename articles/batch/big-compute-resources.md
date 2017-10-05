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
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="90a0d-103">Grote in Azure Compute: technische bronnen voor batchverwerking en high performance computing</span><span class="sxs-lookup"><span data-stu-id="90a0d-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="90a0d-104">Dit is een handleiding voor technische bronnen voor hulp bij het uitvoeren van uw grootschalige parallelle, batchverwerking en high performance computing (HPC) werkbelastingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="90a0d-104">This is a guide to technical resources to help you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="90a0d-105">Breid uw bestaande batch of HPC-workloads in de Azure-cloud of nieuwe Big Compute-oplossingen met een bereik van Azure-services bouwen.</span><span class="sxs-lookup"><span data-stu-id="90a0d-105">Extend your existing batch or HPC workloads to the Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="90a0d-106">Opties voor oplossingen</span><span class="sxs-lookup"><span data-stu-id="90a0d-106">Solutions options</span></span>
<span data-ttu-id="90a0d-107">Lees meer over Big Compute-opties in Azure en kies de juiste aanpak voor uw werkbelasting en zakelijke behoeften.</span><span class="sxs-lookup"><span data-stu-id="90a0d-107">Learn about Big Compute options in Azure, and choose the right approach for your workload and business need.</span></span>

* [<span data-ttu-id="90a0d-108">Batch en HPC-oplossingen</span><span class="sxs-lookup"><span data-stu-id="90a0d-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="90a0d-109">-Video: Big Compute in de cloud met Azure- en HPC</span><span class="sxs-lookup"><span data-stu-id="90a0d-109">Video: Big Compute in the cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="90a0d-110">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="90a0d-110">Azure Batch</span></span>
<span data-ttu-id="90a0d-111">[Batch](https://azure.microsoft.com/services/batch/) is een platformservice die het eenvoudiger om te schakelen voor de cloud uw Linux- en Windows-toepassingen en taken worden uitgevoerd zonder instellen en beheren van een cluster en taak scheduler maakt.</span><span class="sxs-lookup"><span data-stu-id="90a0d-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy to cloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="90a0d-112">Gebruik de SDK om toepassingen integreren met Azure Batch via diverse talen, fase gegevens naar Azure, en taak uitvoering pijplijnen bouwen.</span><span class="sxs-lookup"><span data-stu-id="90a0d-112">Use the SDK to integrate client applications with Azure Batch through various languages, stage data to Azure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="90a0d-113">Documentatie</span><span class="sxs-lookup"><span data-stu-id="90a0d-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="90a0d-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), en [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="90a0d-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="90a0d-115">[Batch management .NET-bibliotheek](https://msdn.microsoft.com/library/mt463120.aspx) verwijzing</span><span class="sxs-lookup"><span data-stu-id="90a0d-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="90a0d-116">Zelfstudie: Aan de slag met [Azure Batch-bibliotheek voor .NET](batch-dotnet-get-started.md) en [Batch Python-client](batch-python-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="90a0d-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="90a0d-117">Batch-forum</span><span class="sxs-lookup"><span data-stu-id="90a0d-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="90a0d-118">Batch-video 's</span><span class="sxs-lookup"><span data-stu-id="90a0d-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="90a0d-119">HPC-clusteroplossingen</span><span class="sxs-lookup"><span data-stu-id="90a0d-119">HPC cluster solutions</span></span>
<span data-ttu-id="90a0d-120">Implementeer of uw bestaande Windows of Linux HPC-cluster uitbreiden naar Azure uw berekenings-intensieve werkbelastingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="90a0d-120">Deploy or extend your existing Windows or Linux HPC cluster to Azure to run your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="90a0d-121">Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="90a0d-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="90a0d-122">HPC Pack is oplossing van Microsoft gratis HPC gebouwd op Microsoft Azure en Windows Server-technologieën, kan worden uitgevoerd van Windows en Linux HPC werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="90a0d-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="90a0d-123">HPC Pack 2016 downloaden</span><span class="sxs-lookup"><span data-stu-id="90a0d-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="90a0d-124">HPC Pack 2012 R2 Update 3 downloaden</span><span class="sxs-lookup"><span data-stu-id="90a0d-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="90a0d-125">Documentatie</span><span class="sxs-lookup"><span data-stu-id="90a0d-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="90a0d-126">Opties voor het cluster in Azure HPC Pack: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) en [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="90a0d-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="90a0d-127">Burst naar Azure worker-exemplaren met HPC Pack</span><span class="sxs-lookup"><span data-stu-id="90a0d-127">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="90a0d-128">Azure batch met HPC Pack burst</span><span class="sxs-lookup"><span data-stu-id="90a0d-128">Burst to Azure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="90a0d-129">Windows HPC-forums</span><span class="sxs-lookup"><span data-stu-id="90a0d-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="90a0d-130">Linux- en OSS-clusteroplossingen</span><span class="sxs-lookup"><span data-stu-id="90a0d-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="90a0d-131">Gebruik deze Azure-sjablonen voor het implementeren van Linux-HPC-clusters.</span><span class="sxs-lookup"><span data-stu-id="90a0d-131">Use these Azure templates to deploy Linux HPC clusters.</span></span>

* <span data-ttu-id="90a0d-132">[Een cluster SLURM ronddraaien](https://azure.microsoft.com/documentation/templates/slurm/) en [blogbericht](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="90a0d-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="90a0d-133">Een cluster koppel draaien</span><span class="sxs-lookup"><span data-stu-id="90a0d-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="90a0d-134">Raster sjablonen met PBS Professional te berekenen</span><span class="sxs-lookup"><span data-stu-id="90a0d-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="90a0d-135">HPC-opslag</span><span class="sxs-lookup"><span data-stu-id="90a0d-135">HPC storage</span></span>
* [<span data-ttu-id="90a0d-136">Parallelle bestandssystemen voor HPC-opslag in Azure</span><span class="sxs-lookup"><span data-stu-id="90a0d-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="90a0d-137">Intel Cloud Edition voor Lustre Software - evaluatie</span><span class="sxs-lookup"><span data-stu-id="90a0d-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="90a0d-138">BeeGFS op CentOS 7.2 sjabloon</span><span class="sxs-lookup"><span data-stu-id="90a0d-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="90a0d-139">Microsoft MPI</span><span class="sxs-lookup"><span data-stu-id="90a0d-139">Microsoft MPI</span></span>
<span data-ttu-id="90a0d-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is een Microsoft-implementatie van de standaard bericht doorgeven Interface voor het ontwikkelen en uitvoeren van parallelle toepassingen op het Windows-platform.</span><span class="sxs-lookup"><span data-stu-id="90a0d-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of the Message Passing Interface standard for developing and running parallel applications on the Windows platform.</span></span>

* [<span data-ttu-id="90a0d-141">MS MPI downloaden</span><span class="sxs-lookup"><span data-stu-id="90a0d-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="90a0d-142">MS MPI-verwijzing</span><span class="sxs-lookup"><span data-stu-id="90a0d-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="90a0d-143">MPI-forum</span><span class="sxs-lookup"><span data-stu-id="90a0d-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="90a0d-144">Rekenintensieve instanties</span><span class="sxs-lookup"><span data-stu-id="90a0d-144">Compute-intensive instances</span></span>
<span data-ttu-id="90a0d-145">Azure biedt een [bereik van VM-grootten](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), waaronder [rekenintensieve H-serie](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) exemplaren kunnen verbinding maken met een back-end RDMA-netwerk, uw Linux- en Windows HPC-workloads uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="90a0d-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting to a back-end RDMA network, to run your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="90a0d-146">Instellen van een cluster Linux RDMA MPI-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="90a0d-146">Set up a Linux RDMA cluster to run MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="90a0d-147">Instellen van een cluster met Windows RDMA met Microsoft HPC Pack MPI-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="90a0d-147">Set up a Windows RDMA cluster with Microsoft HPC Pack to run MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="90a0d-148">Bekijk voor GPU-intensieve werkbelastingen, [NC en NV grootten](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span><span class="sxs-lookup"><span data-stu-id="90a0d-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="90a0d-149">Voorbeelden en demo 's</span><span class="sxs-lookup"><span data-stu-id="90a0d-149">Samples and demos</span></span>
* [<span data-ttu-id="90a0d-150">Azure Batch C# en Python-codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="90a0d-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="90a0d-151">[Batch-scheepswerf](https://azure.github.io/batch-shipyard/) toolkit voor een gemakkelijke implementatie van batch-stijl Dockerized werkbelastingen naar Azure Batch</span><span class="sxs-lookup"><span data-stu-id="90a0d-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads to Azure Batch</span></span>
* <span data-ttu-id="90a0d-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R-pakket gebouwd op Azure Batch</span><span class="sxs-lookup"><span data-stu-id="90a0d-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="90a0d-153">Uitprobeert SUSE Linux Enterprise Server voor HPC</span><span class="sxs-lookup"><span data-stu-id="90a0d-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="90a0d-154">Gerelateerde Azure Services</span><span class="sxs-lookup"><span data-stu-id="90a0d-154">Related Azure services</span></span>
* [<span data-ttu-id="90a0d-155">Data Factory</span><span class="sxs-lookup"><span data-stu-id="90a0d-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* [<span data-ttu-id="90a0d-156">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="90a0d-156">Machine Learning</span></span>](https://azure.microsoft.com/documentation/services/machine-learning/)
* [<span data-ttu-id="90a0d-157">HDInsight</span><span class="sxs-lookup"><span data-stu-id="90a0d-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="90a0d-158">Virtuele machines</span><span class="sxs-lookup"><span data-stu-id="90a0d-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="90a0d-159">Virtuele-Machineschaalsets</span><span class="sxs-lookup"><span data-stu-id="90a0d-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="90a0d-160">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="90a0d-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="90a0d-161">App Service</span><span class="sxs-lookup"><span data-stu-id="90a0d-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="90a0d-162">Media Services</span><span class="sxs-lookup"><span data-stu-id="90a0d-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="90a0d-163">Functies</span><span class="sxs-lookup"><span data-stu-id="90a0d-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="90a0d-164">Architectuurblauwdrukken</span><span class="sxs-lookup"><span data-stu-id="90a0d-164">Architecture blueprints</span></span>
* <span data-ttu-id="90a0d-165">[HPC en gegevens orchestration met behulp van Azure Batch- en Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) en [artikel](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="90a0d-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="90a0d-166">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="90a0d-166">Industry solutions</span></span>
* [<span data-ttu-id="90a0d-167">Bank- en investering markten</span><span class="sxs-lookup"><span data-stu-id="90a0d-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="90a0d-168">Technische simulaties</span><span class="sxs-lookup"><span data-stu-id="90a0d-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="90a0d-169">Verhalen van klanten</span><span class="sxs-lookup"><span data-stu-id="90a0d-169">Customer stories</span></span>
* [<span data-ttu-id="90a0d-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="90a0d-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="90a0d-171">d3View</span><span class="sxs-lookup"><span data-stu-id="90a0d-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="90a0d-172">Ludwig Institute of kanker Research</span><span class="sxs-lookup"><span data-stu-id="90a0d-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="90a0d-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="90a0d-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="90a0d-174">Milliman</span><span class="sxs-lookup"><span data-stu-id="90a0d-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="90a0d-175">Mitsubishi UFJ effecten International</span><span class="sxs-lookup"><span data-stu-id="90a0d-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="90a0d-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="90a0d-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="90a0d-177">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="90a0d-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="90a0d-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="90a0d-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="90a0d-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="90a0d-179">Next steps</span></span>
* <span data-ttu-id="90a0d-180">Bezoek het [teamblog voor Microsoft HPC en Batch](http://blogs.technet.com/b/windowshpc/) en het [Azure-blog](https://azure.microsoft.com/blog/tag/hpc/) voor de meest recente aankondigingen.</span><span class="sxs-lookup"><span data-stu-id="90a0d-180">For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="90a0d-181">Zie ook [wat is er nieuw in Batch](https://azure.microsoft.com/updates/?service=batch) of zich abonneert op de [RSS-feed](https://azure.microsoft.com/updates/feed/?service=batch).</span><span class="sxs-lookup"><span data-stu-id="90a0d-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe to the [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

