---
title: aaaHPC Pack voor Excel en SOA-cluster | Microsoft Docs
description: Aan de slag grootschalige workloads voor Excel- en SOA-uitgevoerd op een HPC Pack-cluster in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="434ec-103">Excel- en SOA-belastingen uitgevoerd op een HPC Pack-cluster in Azure aan de slag</span><span class="sxs-lookup"><span data-stu-id="434ec-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="434ec-104">Dit artikel laat zien hoe toodeploy een Microsoft HPC Pack 2012 R2-cluster op virtuele machines in Azure met behulp van een Azure quickstart-sjabloon of desgewenst een Azure PowerShell-script voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="434ec-104">This article shows you how toodeploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="434ec-105">Hallo-cluster maakt gebruik van virtuele machine in Azure Marketplace-installatiekopieën ontworpen toorun Microsoft Excel of service oriented architecture (SOA) werkbelastingen met HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="434ec-105">hello cluster uses Azure Marketplace VM images designed toorun Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="434ec-106">U kunt Hallo cluster toorun Excel HPC en SOA-services van een on-premises clientcomputer gebruiken.</span><span class="sxs-lookup"><span data-stu-id="434ec-106">You can use hello cluster toorun Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="434ec-107">Hallo Excel HPC-services bevatten Excel-werkmap offloading en de gebruiker gedefinieerde functies van Excel of de UDF's.</span><span class="sxs-lookup"><span data-stu-id="434ec-107">hello Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="434ec-108">In dit artikel is gebaseerd op de functies, sjablonen en scripts voor HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="434ec-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="434ec-109">Dit scenario is momenteel niet ondersteund in HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="434ec-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="434ec-110">Op een hoog niveau hello volgende diagram toont Hallo HPC Pack cluster dat u maakt.</span><span class="sxs-lookup"><span data-stu-id="434ec-110">At a high level, hello following diagram shows hello HPC Pack cluster you create.</span></span>

![HPC-cluster met knooppunten waarop Excel werkbelastingen worden uitgevoerd][scenario]

## <a name="prerequisites"></a><span data-ttu-id="434ec-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="434ec-112">Prerequisites</span></span>
* <span data-ttu-id="434ec-113">**Clientcomputer** -moet u een Windows-clientapparaten computer toosubmit voorbeeld Excel- en SOA-taken toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="434ec-113">**Client computer** - You need a Windows-based client computer toosubmit sample Excel and SOA jobs toohello cluster.</span></span> <span data-ttu-id="434ec-114">U moet ook een Windows computer toorun Hallo script voor implementatie van Azure PowerShell-cluster (als u deze implementatiemethode kiest).</span><span class="sxs-lookup"><span data-stu-id="434ec-114">You also need a Windows computer toorun hello Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="434ec-115">**Azure-abonnement** -als u geen Azure-abonnement hebt, kunt u een [gratis account](https://azure.microsoft.com/pricing/free-trial/) binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="434ec-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="434ec-116">**Quotum voor kernen** -moet u mogelijk tooincrease Hallo quotum van kernen, vooral als u verschillende clusterknooppunten met multicore VM-grootten implementeert.</span><span class="sxs-lookup"><span data-stu-id="434ec-116">**Cores quota** - You might need tooincrease hello quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="434ec-117">Als u een Azure quickstart-sjabloon gebruikt, is het Hallo kernen quotum in Resource Manager per Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="434ec-117">If you are using an Azure quickstart template, hello cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="434ec-118">In dat geval moet u mogelijk tooincrease Hallo quotum in een specifieke regio.</span><span class="sxs-lookup"><span data-stu-id="434ec-118">In that case, you might need tooincrease hello quota in a specific region.</span></span> <span data-ttu-id="434ec-119">Zie [Azure-abonnement limieten, quota's en beperkingen](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="434ec-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="434ec-120">een quotum tooincrease [opent u een ondersteuningsaanvraag online klant](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) zonder kosten.</span><span class="sxs-lookup"><span data-stu-id="434ec-120">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="434ec-121">**Microsoft Office-licentie** - als het implementeren van compute knooppunten met de installatiekopie van een virtuele machine Marketplace HPC Pack 2012 R2 met Microsoft Excel, een 30-daagse evaluatieversie van Microsoft Excel Professional Plus 2013 is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="434ec-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="434ec-122">Nadat de evaluatieperiode hello moet u tooprovide een geldige Microsoft Office-licentie tooactivate Excel toocontinue toorun werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="434ec-122">After hello evaluation period, you need tooprovide a valid Microsoft Office license tooactivate Excel toocontinue toorun workloads.</span></span> <span data-ttu-id="434ec-123">Zie [Excel-activering](#excel-activation) verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="434ec-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="434ec-124">Step 1.</span><span class="sxs-lookup"><span data-stu-id="434ec-124">Step 1.</span></span> <span data-ttu-id="434ec-125">Een HPC Pack cluster in Azure instellen</span><span class="sxs-lookup"><span data-stu-id="434ec-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="434ec-126">Laten we zien twee opties tooset Hallo HPC Pack 2012 R2-cluster: eerste, met behulp van een sjabloon van de Azure quickstart en hello Azure-portal; en de tweede pagina, met behulp van een Azure PowerShell-script voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="434ec-126">We show two options tooset up hello HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and hello Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="434ec-127">Optie 1.</span><span class="sxs-lookup"><span data-stu-id="434ec-127">Option 1.</span></span> <span data-ttu-id="434ec-128">Een Quick Start-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="434ec-128">Use a quickstart template</span></span>
<span data-ttu-id="434ec-129">Gebruik een sjabloon Azure quickstart tooquickly een cluster HPC Pack in hello Azure-portal implementeren.</span><span class="sxs-lookup"><span data-stu-id="434ec-129">Use an Azure quickstart template tooquickly deploy an HPC Pack cluster in hello Azure portal.</span></span> <span data-ttu-id="434ec-130">Als u Hallo-sjabloon in Hallo-portal opent, krijgt u een eenvoudige gebruikersinterface waar u Hallo-instellingen voor uw cluster opgeven.</span><span class="sxs-lookup"><span data-stu-id="434ec-130">When you open hello template in hello portal, you get a simple UI where you enter hello settings for your cluster.</span></span> <span data-ttu-id="434ec-131">Hier volgen de stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="434ec-131">Here are hello steps.</span></span> 

> [!TIP]
> <span data-ttu-id="434ec-132">Als u wilt, gebruikt u een [Azure Marketplace sjabloon](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) die wordt een soortgelijke cluster specifiek voor werkbelastingen van Excel.</span><span class="sxs-lookup"><span data-stu-id="434ec-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="434ec-133">Hallo stappen verschillen enigszins van de volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="434ec-133">hello steps differ slightly from hello following.</span></span>
> 
> 

1. <span data-ttu-id="434ec-134">Ga naar Hallo [sjabloonpagina HPC-Cluster maken op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="434ec-134">Visit hello [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="434ec-135">Als u wilt, kunt u informatie over het Hallo-sjabloon en Hallo broncode controleren.</span><span class="sxs-lookup"><span data-stu-id="434ec-135">If you want, review information about hello template and hello source code.</span></span>
2. <span data-ttu-id="434ec-136">Klik op **implementeren tooAzure** toostart een implementatie met Hallo-sjabloon in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="434ec-136">Click **Deploy tooAzure** toostart a deployment with hello template in hello Azure portal.</span></span>
   
   ![Sjabloon tooAzure implementeren][github]
3. <span data-ttu-id="434ec-138">Volg deze stappen tooenter Hallo parameters voor Hallo HPC cluster sjabloon in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="434ec-138">In hello portal, follow these steps tooenter hello parameters for hello HPC cluster template.</span></span>
   
   <span data-ttu-id="434ec-139">a.</span><span class="sxs-lookup"><span data-stu-id="434ec-139">a.</span></span> <span data-ttu-id="434ec-140">Op Hallo **Parameters** pagina Typ of wijzig de waarden voor de sjabloonparameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="434ec-140">On hello **Parameters** page, enter or modify values for hello template parameters.</span></span> <span data-ttu-id="434ec-141">(Klik op Hallo pictogram volgende tooeach-instelling voor help-informatie). Voorbeeldwaarden weergegeven in het volgende scherm Hallo.</span><span class="sxs-lookup"><span data-stu-id="434ec-141">(Click hello icon next tooeach setting for help information.) Sample values are shown in hello following screen.</span></span> <span data-ttu-id="434ec-142">In dit voorbeeld wordt een cluster met de naam *hpc01* in Hallo *hpc.local* domein die bestaan uit een hoofdknooppunt en 2 rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="434ec-142">This example creates a cluster named *hpc01* in hello *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="434ec-143">Hallo rekenknooppunten worden gemaakt van een installatiekopie van een HPC Pack VM met Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="434ec-143">hello compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Geef parameters][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="434ec-145">virtuele machine automatisch wordt gemaakt van Hallo Hallo-hoofdknooppunt [nieuwste Marketplace-installatiekopie](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) van HPC Pack 2012 R2 op Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="434ec-145">hello head node VM is created automatically from hello [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="434ec-146">Momenteel is Hallo-installatiekopie gebaseerd op HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="434ec-146">Currently hello image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="434ec-147">COMPUTE knooppunt virtuele machines worden gemaakt van de meest recente image Hallo van Hallo geselecteerd compute-knooppunt producten.</span><span class="sxs-lookup"><span data-stu-id="434ec-147">Compute node VMs are created from hello latest image of hello selected compute node family.</span></span> <span data-ttu-id="434ec-148">Selecteer Hallo **ComputeNodeWithExcel** optie voor Hallo nieuwste HPC Pack compute knooppunt afbeelding met een evaluatieversie van Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="434ec-148">Select hello **ComputeNodeWithExcel** option for hello latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="434ec-149">toodeploy een cluster voor algemene SOA-sessies of Excel UDF-offloading, kies Hallo **ComputeNode** optie (zonder Excel geïnstalleerd).</span><span class="sxs-lookup"><span data-stu-id="434ec-149">toodeploy a cluster for general SOA sessions or for Excel UDF offloading, choose hello **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="434ec-150">b.</span><span class="sxs-lookup"><span data-stu-id="434ec-150">b.</span></span> <span data-ttu-id="434ec-151">Kies Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="434ec-151">Choose hello subscription.</span></span>
   
   <span data-ttu-id="434ec-152">c.</span><span class="sxs-lookup"><span data-stu-id="434ec-152">c.</span></span> <span data-ttu-id="434ec-153">Maak een resourcegroep voor Hallo-cluster, zoals *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="434ec-153">Create a resource group for hello cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="434ec-154">d.</span><span class="sxs-lookup"><span data-stu-id="434ec-154">d.</span></span> <span data-ttu-id="434ec-155">Kies een locatie voor de resourcegroep hello, zoals VS-midden.</span><span class="sxs-lookup"><span data-stu-id="434ec-155">Choose a location for hello resource group, such as Central US.</span></span>
   
   <span data-ttu-id="434ec-156">e.</span><span class="sxs-lookup"><span data-stu-id="434ec-156">e.</span></span> <span data-ttu-id="434ec-157">Op Hallo **juridische voorwaarden** pagina, bekijkt hello voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="434ec-157">On hello **Legal terms** page, review hello terms.</span></span> <span data-ttu-id="434ec-158">Als u akkoord gaat, klikt u op **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="434ec-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="434ec-159">Vervolgens, wanneer u klaar bent met waarden voor de sjabloon Hallo Hallo instellen, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="434ec-159">Then, when you are finished setting hello values for hello template, click **Create**.</span></span>
4. <span data-ttu-id="434ec-160">Wanneer Hallo-implementatie is voltooid (het duurt meestal ongeveer 30 minuten), Hallo cluster certificaatbestand exporteren van hoofdknooppunt Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="434ec-160">When hello deployment completes (it typically takes around 30 minutes), export hello cluster certificate file from hello cluster head node.</span></span> <span data-ttu-id="434ec-161">In een latere stap, moet u deze openbaar certificaat op Hallo computer tooprovide Hallo serverzijde clientverificatie voor beveiligde HTTP-binding importeren.</span><span class="sxs-lookup"><span data-stu-id="434ec-161">In a later step, you import this public certificate on hello client computer tooprovide hello server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="434ec-162">a.</span><span class="sxs-lookup"><span data-stu-id="434ec-162">a.</span></span> <span data-ttu-id="434ec-163">Ga in hello Azure-portal, toohello dashboard, selecteer Hallo hoofdknooppunt, en klik op **Connect** bovenaan Hallo Hallo pagina tooconnect met extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="434ec-163">In hello Azure portal, go toohello dashboard, select hello head node, and click **Connect** at hello top of hello page tooconnect using Remote Desktop.</span></span>
   
    <!-- ![Connect toohello head node][connect] -->
   
   <span data-ttu-id="434ec-164">b.</span><span class="sxs-lookup"><span data-stu-id="434ec-164">b.</span></span> <span data-ttu-id="434ec-165">Standaardprocedures in Certificate Manager tooexport Hallo hoofdknooppunt certificaat (te vinden onder Cert: \LocalMachine\My) zonder Hallo persoonlijke sleutel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="434ec-165">Use standard procedures in Certificate Manager tooexport hello head node certificate (located under Cert:\LocalMachine\My) without hello private key.</span></span> <span data-ttu-id="434ec-166">In dit voorbeeld exporteren *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="434ec-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Hallo-certificaat exporteren][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="434ec-168">Optie 2.</span><span class="sxs-lookup"><span data-stu-id="434ec-168">Option 2.</span></span> <span data-ttu-id="434ec-169">Hallo HPC Pack IaaS implementatiescript gebruiken</span><span class="sxs-lookup"><span data-stu-id="434ec-169">Use hello HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="434ec-170">Hallo HPC Pack IaaS-implementatiescript biedt een andere manier veelzijdige toodeploy een HPC Pack-cluster.</span><span class="sxs-lookup"><span data-stu-id="434ec-170">hello HPC Pack IaaS deployment script provides another versatile way toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="434ec-171">Wordt gemaakt van een cluster in het klassieke implementatiemodel hello, terwijl het Hallo-sjabloon gebruikt hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="434ec-171">It creates a cluster in hello classic deployment model, whereas hello template uses hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="434ec-172">Hallo-script is ook compatibel met een abonnement in Azure globale Hallo of service van Azure voor China.</span><span class="sxs-lookup"><span data-stu-id="434ec-172">Also, hello script is compatible with a subscription in either hello Azure Global or Azure China service.</span></span>

<span data-ttu-id="434ec-173">**Aanvullende vereisten**</span><span class="sxs-lookup"><span data-stu-id="434ec-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="434ec-174">**Azure PowerShell** - [installeren en configureren van Azure PowerShell](/powershell/azure/overview) (versie 0.8.10 of hoger) op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="434ec-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="434ec-175">**HPC Pack IaaS-implementatiescript** - downloaden en uitpakken Hallo meest recente versie van script Hallo van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="434ec-175">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="434ec-176">Hallo-versie van script Hallo controleren door te voeren `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="434ec-176">Check hello version of hello script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="434ec-177">In dit artikel is gebaseerd op versie 4.5.0 of hoger van Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="434ec-177">This article is based on version 4.5.0 or later of hello script.</span></span>

<span data-ttu-id="434ec-178">**Hallo-configuratiebestand maken**</span><span class="sxs-lookup"><span data-stu-id="434ec-178">**Create hello configuration file**</span></span>

 <span data-ttu-id="434ec-179">Hallo HPC Pack IaaS-implementatiescript maakt gebruik van een XML-configuratiebestand als invoer die Hallo-infrastructuur van Hallo HPC-cluster beschrijft.</span><span class="sxs-lookup"><span data-stu-id="434ec-179">hello HPC Pack IaaS deployment script uses an XML configuration file as input that describes hello infrastructure of hello HPC cluster.</span></span> <span data-ttu-id="434ec-180">een cluster die bestaan uit een hoofdknooppunt en 18 rekenknooppunten gemaakt op basis van Hallo compute knooppunt installatiekopie, zoals Microsoft Excel toodeploy vervangen door waarden voor uw omgeving in Hallo voorbeeldconfiguratiebestand te volgen.</span><span class="sxs-lookup"><span data-stu-id="434ec-180">toodeploy a cluster consisting of a head node and 18 compute nodes created from hello compute node image that includes Microsoft Excel, substitute values for your environment into hello following sample configuration file.</span></span> <span data-ttu-id="434ec-181">Zie voor meer informatie over het Hallo-configuratiebestand Hallo Manual.rtf bestand in map voor Hallo-script en [een HPC-cluster maken met Hallo HPC Pack IaaS-implementatiescript](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="434ec-181">For more information about hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="434ec-182">**Opmerkingen over Hallo-configuratiebestand**</span><span class="sxs-lookup"><span data-stu-id="434ec-182">**Notes about hello configuration file**</span></span>

* <span data-ttu-id="434ec-183">Hallo **VMName** van hoofdknooppunt Hallo **moet** zijn dezelfde als Hallo Hallo **ServiceName**, of de SOA-taken mislukken toorun.</span><span class="sxs-lookup"><span data-stu-id="434ec-183">hello **VMName** of hello head node **MUST** be hello same as hello **ServiceName**, or SOA jobs fail toorun.</span></span>
* <span data-ttu-id="434ec-184">Zorg ervoor dat u opgeeft **EnableWebPortal** zodat hello hoofdknooppunt certificaat wordt gegenereerd en geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="434ec-184">Make sure you specify **EnableWebPortal** so that hello head node certificate is generated and exported.</span></span>
* <span data-ttu-id="434ec-185">Hallo-bestand geeft een PowerShell-script na configuratie PostConfig.ps1 die wordt uitgevoerd op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="434ec-185">hello file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on hello head node.</span></span> <span data-ttu-id="434ec-186">Hallo volgende voorbeeldscript hello Azure storage-verbindingsreeks configureert, Hallo knooppunt berekeningsfunctie verwijdert uit het hoofdknooppunt Hallo en alle knooppunten online brengt wanneer ze zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="434ec-186">hello following sample script configures hello Azure storage connection string, removes hello compute node role from hello head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

<span data-ttu-id="434ec-187">**Hallo-script uitvoeren**</span><span class="sxs-lookup"><span data-stu-id="434ec-187">**Run hello script**</span></span>

1. <span data-ttu-id="434ec-188">Open PowerShell-console op de clientcomputer Hallo Hallo als beheerder.</span><span class="sxs-lookup"><span data-stu-id="434ec-188">Open hello PowerShell console on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="434ec-189">Wijzig de directory toohello script-map (E:\IaaSClusterScript in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="434ec-189">Change directory toohello script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="434ec-190">toodeploy hello HPC Pack cluster, Hallo volgende opdracht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="434ec-190">toodeploy hello HPC Pack cluster, run hello following command.</span></span> <span data-ttu-id="434ec-191">In dit voorbeeld wordt ervan uitgegaan dat configuratiebestand Hallo bevindt zich in E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="434ec-191">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="434ec-192">Hallo HPC Pack implementatiescript kan enige tijd worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="434ec-192">hello HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="434ec-193">Een ding Hallo script doet tooexport en Hallo cluster certificaat downloaden en opslaan in de map documenten Hallo van de huidige gebruiker op Hallo-clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="434ec-193">One thing hello script does is tooexport and download hello cluster certificate and save it in hello current user’s Documents folder on hello client computer.</span></span> <span data-ttu-id="434ec-194">Hallo script genereert een bericht vergelijkbaar toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="434ec-194">hello script generates a message similar toohello following.</span></span> <span data-ttu-id="434ec-195">In de volgende stap moet u Hallo-certificaat in de juiste certificaatarchief Hallo importeren.</span><span class="sxs-lookup"><span data-stu-id="434ec-195">In a following step, you import hello certificate in hello appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="434ec-196">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="434ec-196">Step 2.</span></span> <span data-ttu-id="434ec-197">Offload Excel-werkmappen en UDF's uitvoert vanuit een on-premises client</span><span class="sxs-lookup"><span data-stu-id="434ec-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="434ec-198">Excel-activering</span><span class="sxs-lookup"><span data-stu-id="434ec-198">Excel activation</span></span>
<span data-ttu-id="434ec-199">Wanneer u Hallo ComputeNodeWithExcel VM-installatiekopie voor productieworkloads, moet u een geldige Microsoft Office license key tooactivate Excel op rekenknooppunten hello tooprovide.</span><span class="sxs-lookup"><span data-stu-id="434ec-199">When using hello ComputeNodeWithExcel VM image for production workloads, you need tooprovide a valid Microsoft Office license key tooactivate Excel on hello compute nodes.</span></span> <span data-ttu-id="434ec-200">Anders Hallo evaluatie-versie van Excel verloopt na 30 dagen en uitvoeren van Excel-werkmappen mislukt met de Hallo COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="434ec-200">Otherwise, hello evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with hello COMException (0x800AC472).</span></span> 

<span data-ttu-id="434ec-201">U kunt Excel opnieuw 30 dagen van evaluatietijd rearm: Meld u aan het hoofdknooppunt toohello en clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` op alle Excel rekenknooppunten via HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="434ec-201">You can rearm Excel for another 30 days of evaluation time: Log on toohello head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="434ec-202">U kunt maximaal twee keer rearm.</span><span class="sxs-lookup"><span data-stu-id="434ec-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="434ec-203">Daarna moet u een geldige sleutel van de Office-licentie opgeven.</span><span class="sxs-lookup"><span data-stu-id="434ec-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="434ec-204">Hallo Office Professional Plus 2013 is geïnstalleerd op Hallo VM-installatiekopie is een volume-editie met een Generic Volume License Key (GVLK).</span><span class="sxs-lookup"><span data-stu-id="434ec-204">hello Office Professional Plus 2013 installed on hello VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="434ec-205">Kan worden geactiveerd via Key Management Service (KMS) / Active Directory gebaseerde activering (AD BA) of Multiple Activation Key (MAK).</span><span class="sxs-lookup"><span data-stu-id="434ec-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="434ec-206">toouse AD-KMS-BA, een bestaande KMS-server gebruiken of een nieuwe met behulp van Microsoft Office 2013 Volume License Pack Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="434ec-206">toouse KMS/AD-BA, use an existing KMS server or set up a new one by using hello Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="434ec-207">(Als u wilt instellen Hallo-server op Hallo hoofdknooppunt.) Vervolgens activeren Hallo KMS-hostsleutel via Hallo Internet of telefonisch.</span><span class="sxs-lookup"><span data-stu-id="434ec-207">(If you want to, set up hello server on hello head node.) Then, activate hello KMS host key via hello Internet or telephone.</span></span> <span data-ttu-id="434ec-208">Vervolgens clusrun `ospp.vbs` tooset Hallo KMS-server en de poort en het activeren van Office op alle rekenknooppunten voor Hallo Excel.</span><span class="sxs-lookup"><span data-stu-id="434ec-208">Then clusrun `ospp.vbs` tooset hello KMS server and port and activate Office on all hello Excel compute nodes.</span></span> 

    * <span data-ttu-id="434ec-209">toouse MAK, eerste clusrun `ospp.vbs` tooinput Hallo sleutel en vervolgens alle Hallo Excel rekenknooppunten via Hallo Internet of telefonisch te activeren.</span><span class="sxs-lookup"><span data-stu-id="434ec-209">toouse MAK, first clusrun `ospp.vbs` tooinput hello key and then activate all hello Excel compute nodes via hello Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="434ec-210">Retail-productcodes voor Office Professional Plus 2013 kunnen niet worden gebruikt met deze VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="434ec-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="434ec-211">Als u geldige sleutels en installatiemedia voor Office of Microsoft Excel-versies dan deze versie van de volume Office Professional Plus 2013 hebt, kunt u ze in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="434ec-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="434ec-212">Eerst verwijderen van dit volume-editie en Hallo-editie die u hebt installeren.</span><span class="sxs-lookup"><span data-stu-id="434ec-212">First uninstall this volume edition and install hello edition that you have.</span></span> <span data-ttu-id="434ec-213">Hallo opnieuw geïnstalleerd Excel rekenknooppunt worden vastgelegd als een aangepaste VM-installatiekopie toouse in een implementatie op grote schaal.</span><span class="sxs-lookup"><span data-stu-id="434ec-213">hello reinstalled Excel compute node can be captured as a customized VM image toouse in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="434ec-214">Offload Excel-werkmappen</span><span class="sxs-lookup"><span data-stu-id="434ec-214">Offload Excel workbooks</span></span>
<span data-ttu-id="434ec-215">Volg deze stappen toooffload een Excel-werkmap in zodat deze wordt uitgevoerd op Hallo HPC Pack cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="434ec-215">Follow these steps toooffload an Excel workbook so that it runs on hello HPC Pack cluster in Azure.</span></span> <span data-ttu-id="434ec-216">toodo, moet u Excel 2010 of 2013 is al geïnstalleerd op de clientcomputer Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="434ec-216">toodo this, you must have Excel 2010 or 2013 already installed on hello client computer.</span></span>

1. <span data-ttu-id="434ec-217">Gebruik een van de opties Hallo in stap 1 toodeploy een cluster HPC Pack Hello Excel compute installatiekopie van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="434ec-217">Use one of hello options in Step 1 toodeploy an HPC Pack cluster with hello Excel compute node image.</span></span> <span data-ttu-id="434ec-218">Hallo cluster-certificaatbestand (.cer) en cluster-gebruikersnaam en wachtwoord ophalen.</span><span class="sxs-lookup"><span data-stu-id="434ec-218">Obtain hello cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="434ec-219">Klik op de clientcomputer Hallo Hallo cluster certificaat onder Cert: \CurrentUser\Root te importeren.</span><span class="sxs-lookup"><span data-stu-id="434ec-219">On hello client computer, import hello cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="434ec-220">Zorg ervoor dat Excel is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="434ec-220">Make sure Excel is installed.</span></span> <span data-ttu-id="434ec-221">Maak een Excel.exe.config-bestand met de volgende inhoud in Hallo Hallo dezelfde map als Excel.exe op Hallo-clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="434ec-221">Create an Excel.exe.config file with hello following contents in hello same folder as Excel.exe on hello client computer.</span></span> <span data-ttu-id="434ec-222">Deze stap zorgt ervoor dat Hallo HPC Pack 2012 R2 Excel COM-invoegtoepassing is geladen.</span><span class="sxs-lookup"><span data-stu-id="434ec-222">This step ensures that hello HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="434ec-223">Hallo client toosubmit taken toohello HPC Pack cluster ingesteld.</span><span class="sxs-lookup"><span data-stu-id="434ec-223">Set up hello client toosubmit jobs toohello HPC Pack cluster.</span></span> <span data-ttu-id="434ec-224">Een mogelijkheid is toodownload Hallo volledige [HPC Pack 2012 R2 Update 3 installatie](http://www.microsoft.com/download/details.aspx?id=49922) en Hallo HPC Pack client installeren.</span><span class="sxs-lookup"><span data-stu-id="434ec-224">One option is toodownload hello full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install hello HPC Pack client.</span></span> <span data-ttu-id="434ec-225">U kunt ook downloaden en installeren van Hallo [HPC Pack 2012 R2 Update 3 client-hulpprogramma's](https://www.microsoft.com/download/details.aspx?id=49923) en Hallo juiste Visual C++ 2010 redistributable voor uw computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="434ec-225">Alternatively, download and install hello [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and hello appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="434ec-226">In dit voorbeeld gebruiken we een voorbeeld-Excel-werkmap met de naam ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="434ec-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="434ec-227">U kunt dit downloaden [hier](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="434ec-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="434ec-228">Hallo Excel-werkmap tooa werkmap zoals D:\Excel\Run kopiëren.</span><span class="sxs-lookup"><span data-stu-id="434ec-228">Copy hello Excel workbook tooa working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="434ec-229">Hallo Excel-werkmap opent.</span><span class="sxs-lookup"><span data-stu-id="434ec-229">Open hello Excel workbook.</span></span> <span data-ttu-id="434ec-230">Op Hallo **ontwikkelen** lint, klikt u op **COM-invoegtoepassingen** en Bevestig dat Hallo HPC Pack Excel COM-invoegtoepassing is geladen.</span><span class="sxs-lookup"><span data-stu-id="434ec-230">On hello **Develop** ribbon, click **COM Add-Ins** and confirm that hello HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Excel-invoegtoepassing voor HPC Pack][addin]
8. <span data-ttu-id="434ec-232">Bewerken Hallo VBA-macro HPCControlMacros in Excel door het wijzigen van Hallo toegelicht regels, zoals weergegeven in het volgende script Hallo.</span><span class="sxs-lookup"><span data-stu-id="434ec-232">Edit hello VBA macro HPCControlMacros in Excel by changing hello commented lines as shown in hello following script.</span></span> <span data-ttu-id="434ec-233">Vervang de juiste waarden voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="434ec-233">Substitute appropriate values for your environment.</span></span>
   
   ![Excel-macro voor HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. <span data-ttu-id="434ec-235">Hallo Excel-werkmap tooan uploaden directory zoals D:\Excel\Upload kopiëren.</span><span class="sxs-lookup"><span data-stu-id="434ec-235">Copy hello Excel workbook tooan upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="434ec-236">Deze map is opgegeven in Hallo HPC_DependsFiles constante in Hallo VBA-macro.</span><span class="sxs-lookup"><span data-stu-id="434ec-236">This directory is specified in hello HPC_DependsFiles constant in hello VBA macro.</span></span>
10. <span data-ttu-id="434ec-237">toorun hello werkmap op Hallo-cluster in Azure, klikt u op Hallo **Cluster** knop op Hallo werkblad.</span><span class="sxs-lookup"><span data-stu-id="434ec-237">toorun hello workbook on hello cluster in Azure, click hello **Cluster** button on hello worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="434ec-238">Excel UDF's uitvoeren</span><span class="sxs-lookup"><span data-stu-id="434ec-238">Run Excel UDFs</span></span>
<span data-ttu-id="434ec-239">toorun Excel UDF's, volg Hallo vorige stappen 1-3 tooset van Hallo-clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="434ec-239">toorun Excel UDFs, follow hello preceding steps 1 – 3 tooset up hello client computer.</span></span> <span data-ttu-id="434ec-240">Voor Excel UDF's hoeft u geen toohave Hallo Excel toepassing is geïnstalleerd op de rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="434ec-240">For Excel UDFs, you don't need toohave hello Excel application installed on compute nodes.</span></span> <span data-ttu-id="434ec-241">Dus bij het maken van uw cluster rekenknooppunten, kunt u berekenen de installatiekopie van een normale compute-knooppunt in plaats van Hallo knooppunt van de installatiekopie met Excel.</span><span class="sxs-lookup"><span data-stu-id="434ec-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of hello compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="434ec-242">Er is een 34 tekenlimiet in Hallo Excel 2010 en 2013 cluster connector dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="434ec-242">There is a 34 character limit in hello Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="434ec-243">U dit dialoogvenster vak toospecify Hallo cluster die Hallo UDF's uitvoert.</span><span class="sxs-lookup"><span data-stu-id="434ec-243">You use this dialog box toospecify hello cluster that runs hello UDFs.</span></span> <span data-ttu-id="434ec-244">Als de volledige clusternaam Hallo langer (bijvoorbeeld hpcexcelhn01.southeastasia.cloudapp.azure.com), past niet in het dialoogvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="434ec-244">If hello full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in hello dialog box.</span></span> <span data-ttu-id="434ec-245">Hallo tijdelijke oplossing is tooset een variabele van alle computers, zoals *CCP_IAASHN* met Hallo Hallo lang clusternaam waarde.</span><span class="sxs-lookup"><span data-stu-id="434ec-245">hello workaround is tooset a machine-wide variable such as *CCP_IAASHN* with hello value of hello long cluster name.</span></span> <span data-ttu-id="434ec-246">Voer de *% CCP_IAASHN %* in het dialoogvenster Hallo als Hallo hoofdknooppunt clusternaam.</span><span class="sxs-lookup"><span data-stu-id="434ec-246">Then, enter *%CCP_IAASHN%* in hello dialog box as hello cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="434ec-247">Hallo-cluster is geïmplementeerd, Ga verder met nadat Hallo toorun stappen te volgen een ingebouwde voorbeeld Excel UDF.</span><span class="sxs-lookup"><span data-stu-id="434ec-247">After hello cluster is successfully deployed, continue with hello following steps toorun a sample built-in Excel UDF.</span></span> <span data-ttu-id="434ec-248">Zie voor aangepaste Excel UDF's, deze [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild Hallo XLL's en deze implementeren op Hallo IaaS-cluster.</span><span class="sxs-lookup"><span data-stu-id="434ec-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLLs and deploy them on hello IaaS cluster.</span></span>

1. <span data-ttu-id="434ec-249">Open een nieuwe Excel-werkmap.</span><span class="sxs-lookup"><span data-stu-id="434ec-249">Open a new Excel workbook.</span></span> <span data-ttu-id="434ec-250">Op Hallo **ontwikkelen** lint, klikt u op **-invoegtoepassingen**. Klik vervolgens in het dialoogvenster Hallo op **Bladeren**, toohello %CCP_HOME%Bin\XLL32 map te navigeren en selecteert u Hallo voorbeeld ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="434ec-250">On hello **Develop** ribbon, click **Add-Ins**. Then, in hello dialog box, click **Browse**, navigate toohello %CCP_HOME%Bin\XLL32 folder, and select hello sample ClusterUDF32.xll.</span></span> <span data-ttu-id="434ec-251">Als hello ClusterUDF32 niet op de clientcomputer hello bestaat, kunt u deze vanuit Hallo %CCP_HOME%Bin\XLL32 map op het hoofdknooppunt Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="434ec-251">If hello ClusterUDF32 doesn't exist on hello client machine, copy it from hello %CCP_HOME%Bin\XLL32 folder on hello head node.</span></span>
   
   ![Hallo UDF selecteren][udf]
2. <span data-ttu-id="434ec-253">Klik op **bestand** > **opties** > **geavanceerde**.</span><span class="sxs-lookup"><span data-stu-id="434ec-253">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="434ec-254">Onder **formules**, Controleer **toestaan gebruiker gedefinieerde XLL functies toorun een rekencluster**.</span><span class="sxs-lookup"><span data-stu-id="434ec-254">Under **Formulas**, check **Allow user-defined XLL functions toorun a compute cluster**.</span></span> <span data-ttu-id="434ec-255">Klik vervolgens op **opties** en voer de volledige clusternaam Hallo in **hoofdknooppunt clusternaam**.</span><span class="sxs-lookup"><span data-stu-id="434ec-255">Then click **Options** and enter hello full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="434ec-256">(Als zijn aangegeven eerder deze invoervak is beperkt too34 tekens, zodat een lange clusternaam niet past.</span><span class="sxs-lookup"><span data-stu-id="434ec-256">(As noted previously this input box is limited too34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="434ec-257">U kunt hier een variabele voor alle computers voor een lange clusternaam.)</span><span class="sxs-lookup"><span data-stu-id="434ec-257">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Hallo UDF configureren][options]
3. <span data-ttu-id="434ec-259">toorun hello UDF berekening op Hallo-cluster, klik op Hallo cel met de waarde =XllGetComputerNameC() en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="434ec-259">toorun hello UDF calculation on hello cluster, click hello cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="434ec-260">Hallo-functie haalt gewoon Hallo-naam van het Hallo-rekenknooppunt op welke Hallo UDF wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="434ec-260">hello function simply retrieves hello name of hello compute node on which hello UDF runs.</span></span> <span data-ttu-id="434ec-261">Voor Hallo voor het eerst uitvoert, wordt een dialoogvenster referenties gevraagd voor Hallo gebruikersnaam en wachtwoord tooconnect toohello IaaS-cluster.</span><span class="sxs-lookup"><span data-stu-id="434ec-261">For hello first run, a credentials dialog box prompts for hello username and password tooconnect toohello IaaS cluster.</span></span>
   
   ![UDF uitvoeren][run]
   
   <span data-ttu-id="434ec-263">Wanneer er veel cellen toocalculate, druk op Alt-Shift-Ctrl + F9 toorun Hallo berekening op alle cellen.</span><span class="sxs-lookup"><span data-stu-id="434ec-263">When there are many cells toocalculate, press Alt-Shift-Ctrl + F9 toorun hello calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="434ec-264">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="434ec-264">Step 3.</span></span> <span data-ttu-id="434ec-265">Een SOA-werkbelasting uitvoeren vanuit een on-premises client</span><span class="sxs-lookup"><span data-stu-id="434ec-265">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="434ec-266">toorun algemene SOA-toepassingen op Hallo HPC Pack IaaS cluster gebruik een van de methoden Hallo eerst in stap 1 toodeploy Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="434ec-266">toorun general SOA applications on hello HPC Pack IaaS cluster, first use one of hello methods in Step 1 toodeploy hello cluster.</span></span> <span data-ttu-id="434ec-267">Geef de installatiekopie van een algemene compute-knooppunt in dit geval omdat u geen Excel nodig op Hallo rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="434ec-267">Specify a generic compute node image in this case, because you do not need Excel on hello compute nodes.</span></span> <span data-ttu-id="434ec-268">Volg deze stappen.</span><span class="sxs-lookup"><span data-stu-id="434ec-268">Then follow these steps.</span></span>

1. <span data-ttu-id="434ec-269">Bij het ophalen van Hallo cluster certificaat, moet u het importeren op de clientcomputer Hallo onder Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="434ec-269">After retrieving hello cluster certificate, import it on hello client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="434ec-270">Hallo installeren [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) en [HPC Pack 2012 R2 Update 3 client-hulpprogramma's](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="434ec-270">Install hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="434ec-271">Deze hulpprogramma's kunnen u toodevelop en SOA-clienttoepassingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="434ec-271">These tools enable you toodevelop and run SOA client applications.</span></span>
3. <span data-ttu-id="434ec-272">Hallo HelloWorldR2 downloaden [voorbeeldcode](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="434ec-272">Download hello HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="434ec-273">Open Hallo HelloWorldR2.sln in Visual Studio 2010 of 2012.</span><span class="sxs-lookup"><span data-stu-id="434ec-273">Open hello HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="434ec-274">(Dit voorbeeld is niet compatibel met latere versies van Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="434ec-274">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="434ec-275">Hallo EchoService project eerst bouwen.</span><span class="sxs-lookup"><span data-stu-id="434ec-275">Build hello EchoService project first.</span></span> <span data-ttu-id="434ec-276">Vervolgens implementeert Hallo service toohello IaaS-cluster in Hallo dezelfde manier als tooan lokale cluster.</span><span class="sxs-lookup"><span data-stu-id="434ec-276">Then, deploy hello service toohello IaaS cluster in hello same way you deploy tooan on-premises cluster.</span></span> <span data-ttu-id="434ec-277">Zie voor gedetailleerde stappen Hallo Readme.doc in HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="434ec-277">For detailed steps, see hello Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="434ec-278">Wijzig en Hallo HellWorldR2 en andere projecten bouwen, zoals beschreven in de volgende sectie toogenerate Hallo SOA-clienttoepassingen die worden uitgevoerd op een cluster Azure IaaS Hallo.</span><span class="sxs-lookup"><span data-stu-id="434ec-278">Modify and build hello HellWorldR2 and other projects as described in hello following section toogenerate hello SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="434ec-279">Http-binding gebruiken met Azure storage-wachtrij</span><span class="sxs-lookup"><span data-stu-id="434ec-279">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="434ec-280">toouse Http-binding met een Azure storage-wachtrij worden enkele wijzigingen aanbrengen toohello voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="434ec-280">toouse Http binding with an Azure storage queue, make a few changes toohello sample code.</span></span>

* <span data-ttu-id="434ec-281">De clusternaam Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="434ec-281">Update hello cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="434ec-282">Eventueel Hallo standaard TransportScheme in SessionStartInfo gebruiken of stel expliciet tooHttp.</span><span class="sxs-lookup"><span data-stu-id="434ec-282">Optionally, use hello default TransportScheme in SessionStartInfo or explicitly set it tooHttp.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="434ec-283">Standaard-binding voor Hallo BrokerClient gebruiken.</span><span class="sxs-lookup"><span data-stu-id="434ec-283">Use default binding for hello BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="434ec-284">Of expliciet met Hallo basicHttpBinding ingesteld.</span><span class="sxs-lookup"><span data-stu-id="434ec-284">Or set explicitly using hello basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="434ec-285">Eventueel Hallo UseAzureQueue vlag tootrue in SessionStartInfo instellen.</span><span class="sxs-lookup"><span data-stu-id="434ec-285">Optionally, set hello UseAzureQueue flag tootrue in SessionStartInfo.</span></span> <span data-ttu-id="434ec-286">Als dat niet is ingesteld, wordt deze ingesteld tootrue standaard wanneer clusternaam hello Azure domeinachtervoegsels en Hallo TransportScheme Http is.</span><span class="sxs-lookup"><span data-stu-id="434ec-286">If not set, it will be set tootrue by default when hello cluster name has Azure domain suffixes and hello TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="434ec-287">Gebruik Http-binding zonder Azure storage-wachtrij</span><span class="sxs-lookup"><span data-stu-id="434ec-287">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="434ec-288">zonder een Azure storage-wachtrij, expliciet set Hallo UseAzureQueue vlag toofalse in Hallo SessionStartInfo toouse Http-binding.</span><span class="sxs-lookup"><span data-stu-id="434ec-288">toouse Http binding without an Azure storage queue, explicitly set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="434ec-289">Gebruik NetTcp-binding</span><span class="sxs-lookup"><span data-stu-id="434ec-289">Use NetTcp binding</span></span>
<span data-ttu-id="434ec-290">toouse NetTcp binding, Hallo-configuratie is vergelijkbaar tooconnecting tooan on-premises-cluster.</span><span class="sxs-lookup"><span data-stu-id="434ec-290">toouse NetTcp binding, hello configuration is similar tooconnecting tooan on-premises cluster.</span></span> <span data-ttu-id="434ec-291">U moet enkele eindpunten op Hallo hoofdknooppunt VM tooopen.</span><span class="sxs-lookup"><span data-stu-id="434ec-291">You need tooopen a few endpoints on hello head node VM.</span></span> <span data-ttu-id="434ec-292">Als u Hallo HPC Pack IaaS implementatie script toocreate Hallo cluster gebruikt, bijvoorbeeld hello set Hallo eindpunten in Azure-portal als volgt.</span><span class="sxs-lookup"><span data-stu-id="434ec-292">If you used hello HPC Pack IaaS deployment script toocreate hello cluster, for example, set hello endpoints in hello Azure portal as follows.</span></span>

1. <span data-ttu-id="434ec-293">Hallo VM stoppen.</span><span class="sxs-lookup"><span data-stu-id="434ec-293">Stop hello VM.</span></span>
2. <span data-ttu-id="434ec-294">Voeg Hallo TCP-poorten 9090, 9087, 9091, 9094 voor Hallo-sessie Broker, respectievelijk worker en Data services Broker</span><span class="sxs-lookup"><span data-stu-id="434ec-294">Add hello TCP ports 9090, 9087, 9091, 9094 for hello Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Eindpunten configureren][endpoint-new-portal]
3. <span data-ttu-id="434ec-296">Hallo VM start.</span><span class="sxs-lookup"><span data-stu-id="434ec-296">Start hello VM.</span></span>

<span data-ttu-id="434ec-297">Hallo SOA-clienttoepassing vereist geen wijzigingen behalve Hallo head toohello IaaS cluster volledige naam te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="434ec-297">hello SOA client application requires no changes except altering hello head name toohello IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="434ec-298">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="434ec-298">Next steps</span></span>
* <span data-ttu-id="434ec-299">Zie [deze resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) voor meer informatie over het uitvoeren van Excel-werkbelastingen met HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="434ec-299">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="434ec-300">Zie [SOA-Services beheren in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) voor meer informatie over het implementeren en beheren van SOA-services met HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="434ec-300">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
