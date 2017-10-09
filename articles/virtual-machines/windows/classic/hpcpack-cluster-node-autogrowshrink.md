---
title: aaaAutoscale HPC Pack clusterknooppunten | Microsoft Docs
description: Automatisch vergroten of verkleinen Hallo aantal HPC Pack cluster-rekenknooppunten in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a><span data-ttu-id="314b0-103">Automatisch vergroten of verkleinen Hallo HPC Pack clusterbronnen in Azure op basis van toohello clusterbelasting</span><span class="sxs-lookup"><span data-stu-id="314b0-103">Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload</span></span>
<span data-ttu-id="314b0-104">Als u Azure 'burst' knooppunten in het cluster HPC Pack implementeert, of u een cluster HPC Pack in Azure VM's maakt, kunt u een manier om automatisch vergroten of verkleinen Hallo clusterbronnen zoals knooppunten of kernen volgens Hallo werkbelasting op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="314b0-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink hello cluster resources such as nodes or cores according to hello workload on hello cluster.</span></span> <span data-ttu-id="314b0-105">Hallo-clusterbronnen schaling op deze manier kunt u toouse uw Azure-resources efficiënter en hun kosten te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="314b0-105">Scaling hello cluster resources in this way allows you toouse your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="314b0-106">Dit artikel ziet u twee manieren waarop HPC Pack tooautoscale rekenresources biedt:</span><span class="sxs-lookup"><span data-stu-id="314b0-106">This article shows you two ways that HPC Pack provides tooautoscale compute resources:</span></span>

* <span data-ttu-id="314b0-107">Hallo HPC Pack cluster eigenschap **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="314b0-107">hello HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="314b0-108">Hallo **AzureAutoGrowShrink.ps1** HPC PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="314b0-108">hello **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="314b0-109">Momenteel kunt u alleen automatisch vergroten of verkleinen van HPC Pack rekenknooppunten waarop een Windows-serverbesturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="314b0-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-hello-autogrowshrink-cluster-property"></a><span data-ttu-id="314b0-110">Hallo AutoGrowShrink cluster eigenschap instellen</span><span class="sxs-lookup"><span data-stu-id="314b0-110">Set hello AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="314b0-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="314b0-111">Prerequisites</span></span>

* <span data-ttu-id="314b0-112">**HPC Pack 2012 R2 Update 2 of hoger cluster** -hoofdknooppunt Hallo-cluster kan worden geïmplementeerd on-premises of in een Azure VM.</span><span class="sxs-lookup"><span data-stu-id="314b0-112">**HPC Pack 2012 R2 Update 2 or later cluster** - hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="314b0-113">Zie [een hybride-cluster met HPC Pack instellen](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget gestart met het hoofdknooppunt van een lokale en Azure 'burst' knooppunten.</span><span class="sxs-lookup"><span data-stu-id="314b0-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="314b0-114">Zie Hallo [HPC Pack IaaS-implementatiescript](hpcpack-cluster-powershell-script.md) tooquickly een HPC Pack cluster in Azure VM's implementeren.</span><span class="sxs-lookup"><span data-stu-id="314b0-114">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="314b0-115">**Voor een cluster met een hoofdknooppunt in Azure (Resource Manager-implementatiemodel)** - vanaf HPC Pack 2016, certificaatverificatie in een Azure Active Directory-toepassing wordt gebruikt voor het automatisch groeiende en comprimeren cluster virtuele machines geïmplementeerd met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="314b0-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="314b0-116">Een certificaat als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="314b0-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="314b0-117">Na implementatie van het cluster, verbinding maken met extern bureaublad tooone hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="314b0-117">After cluster deployment, connect by Remote Desktop tooone head node.</span></span>

  2. <span data-ttu-id="314b0-118">Hallo-certificaat (PFX-indeling met persoonlijke sleutel) tooeach hoofdknooppunt uploaden en installeer tooCert:\LocalMachine\My en Cert: \LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="314b0-118">Upload hello certificate (PFX format with private key) tooeach head node and install tooCert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="314b0-119">Open Azure PowerShell als beheerder en Voer Hallo opdrachten op één hoofdknooppunt volgen:</span><span class="sxs-lookup"><span data-stu-id="314b0-119">Start Azure PowerShell as an administrator and run hello following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="314b0-120">Als uw account meer dan één Azure Active Directory-tenant of Azure-abonnement is, kunt u de volgende Hallo uitvoeren opdracht tooselect Hallo juiste tenant en -abonnement:</span><span class="sxs-lookup"><span data-stu-id="314b0-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run hello following command tooselect hello correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="314b0-121">Na de opdracht tooview Hallo geselecteerde Hallo momenteel uitvoeren tenant en -abonnement:</span><span class="sxs-lookup"><span data-stu-id="314b0-121">Run hello following command tooview hello currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="314b0-122">Hallo na script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="314b0-122">Run hello following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="314b0-123">waar</span><span class="sxs-lookup"><span data-stu-id="314b0-123">where</span></span>

    <span data-ttu-id="314b0-124">**DisplayName** -weergavenaam van de Azure Active-toepassing.</span><span class="sxs-lookup"><span data-stu-id="314b0-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="314b0-125">Als de toepassing hello niet bestaat, wordt deze gemaakt in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="314b0-125">If hello application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="314b0-126">**Startpagina** -startpagina Hallo van Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="314b0-126">**HomePage** - hello home page of hello application.</span></span> <span data-ttu-id="314b0-127">U kunt een dummy-URL, zoals in het voorgaande voorbeeld Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="314b0-127">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="314b0-128">**IdentifierUri** -id van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="314b0-128">**IdentifierUri** - Identifier of hello application.</span></span> <span data-ttu-id="314b0-129">U kunt een dummy-URL, zoals in het voorgaande voorbeeld Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="314b0-129">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="314b0-130">**CertificateThumbprint** -vingerafdruk van certificaat Hallo dat u op Hallo hoofdknooppunt in stap 1 hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="314b0-130">**CertificateThumbprint** - Thumbprint of hello certificate you installed on hello head node in Step 1.</span></span>

    <span data-ttu-id="314b0-131">**TenantId** -Tenant-ID van uw Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="314b0-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="314b0-132">U kunt Hallo Tenant-ID ophalen van hello Azure Active Directory-beheerportal **eigenschappen** pagina.</span><span class="sxs-lookup"><span data-stu-id="314b0-132">You can get hello Tenant ID from hello Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="314b0-133">Voor meer informatie over **ConfigARMAutoGrowShrinkCert.ps1**, voert `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="314b0-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="314b0-134">**Voor een cluster met een hoofdknooppunt in Azure (klassieke implementatiemodel)** : als u Hallo HPC Pack IaaS implementatie script toocreate Hallo-cluster in Hallo klassieke implementatiemodel inschakelen Hallo gebruiken **AutoGrowShrink** cluster de eigenschap door Hallo AutoGrowShrink optie in het configuratiebestand Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="314b0-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use hello HPC Pack IaaS deployment script toocreate hello cluster in hello classic deployment model, enable hello **AutoGrowShrink** cluster property by setting hello AutoGrowShrink option in hello cluster configuration file.</span></span> <span data-ttu-id="314b0-135">Zie voor meer informatie, Hallo documentatie bij Hallo [script downloaden](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="314b0-135">For details, see hello documentation accompanying hello [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="314b0-136">U kunt ook inschakelen Hallo **AutoGrowShrink** cluster eigenschap nadat u Hallo-cluster implementeren met behulp van HPC PowerShell-opdrachten in Hallo volgende sectie beschreven.</span><span class="sxs-lookup"><span data-stu-id="314b0-136">Alternatively, enable hello **AutoGrowShrink** cluster property after you deploy hello cluster by using HPC PowerShell commands described in hello following section.</span></span> <span data-ttu-id="314b0-137">tooprepare voor deze eerste volledige Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="314b0-137">tooprepare for this, first complete hello following steps:</span></span>

  1. <span data-ttu-id="314b0-138">Een Azure-beheercertificaat configureren op het hoofdknooppunt hello en in hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="314b0-138">Configure an Azure management certificate on hello head node and in hello Azure subscription.</span></span> <span data-ttu-id="314b0-139">U kunt voor een testimplementatie Hallo standaard Microsoft HPC Azure zelf-ondertekend certificaat gebruiken dat HPC Pack wordt geïnstalleerd op het hoofdknooppunt Hallo en vervolgens uploaden dat certificaat tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="314b0-139">For a test deployment, you can use hello Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on hello head node, and then upload that certificate tooyour Azure subscription.</span></span> <span data-ttu-id="314b0-140">Zie voor opties en stappen Hallo [TechNet-bibliotheek richtlijnen](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="314b0-140">For options and steps, see hello [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="314b0-141">Voer **regedit** op het hoofdknooppunt hello, gaat u tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo en voeg een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="314b0-141">Run **regedit** on hello head node, go tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="314b0-142">Waardenaam hello te ingesteld 'Vingerafdruk' en waarde gegevens toohello vingerafdruk van certificaat Hallo in stap 1.</span><span class="sxs-lookup"><span data-stu-id="314b0-142">Set hello Value name too“ThumbPrint”, and Value data toohello thumbprint of hello certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a><span data-ttu-id="314b0-143">HPC PowerShell-opdrachten tooset hello AutoGrowShrink-eigenschap</span><span class="sxs-lookup"><span data-stu-id="314b0-143">HPC PowerShell commands tooset hello AutoGrowShrink property</span></span>
<span data-ttu-id="314b0-144">Hieronder vindt u voorbeeld HPC PowerShell-opdrachten tooset **AutoGrowShrink** en tootune het gedrag met extra parameters.</span><span class="sxs-lookup"><span data-stu-id="314b0-144">Following are sample HPC PowerShell commands tooset **AutoGrowShrink** and tootune its behavior with additional parameters.</span></span> <span data-ttu-id="314b0-145">Zie [AutoGrowShrink parameters](#AutoGrowShrink-parameters) verderop in dit artikel voor Hallo volledige lijst met instellingen.</span><span class="sxs-lookup"><span data-stu-id="314b0-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for hello complete list of settings.</span></span>

<span data-ttu-id="314b0-146">toorun deze opdrachten, HPC PowerShell Hallo hoofdknooppunt van cluster start als beheerder.</span><span class="sxs-lookup"><span data-stu-id="314b0-146">toorun these commands, start HPC PowerShell on hello cluster head node as an administrator.</span></span>

<span data-ttu-id="314b0-147">**tooenable hello AutoGrowShrink eigenschap**</span><span class="sxs-lookup"><span data-stu-id="314b0-147">**tooenable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="314b0-148">**toodisable hello AutoGrowShrink eigenschap**</span><span class="sxs-lookup"><span data-stu-id="314b0-148">**toodisable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="314b0-149">**toochange hello toenemen interval in minuten**</span><span class="sxs-lookup"><span data-stu-id="314b0-149">**toochange hello grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="314b0-150">**Hallo toochange verkleinen interval in minuten**</span><span class="sxs-lookup"><span data-stu-id="314b0-150">**toochange hello shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="314b0-151">**tooview hello huidige configuratie van AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="314b0-151">**tooview hello current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="314b0-152">**tooexclude knooppuntgroepen van AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="314b0-152">**tooexclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="314b0-153">Deze parameter wordt ondersteund vanaf HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="314b0-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="314b0-154">AutoGrowShrink parameters</span><span class="sxs-lookup"><span data-stu-id="314b0-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="314b0-155">Hallo volgen AutoGrowShrink parameters die u aanpassen kunt met behulp van Hallo **Set HpcClusterProperty** opdracht.</span><span class="sxs-lookup"><span data-stu-id="314b0-155">hello following are AutoGrowShrink parameters that you can modify by using hello **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="314b0-156">**EnableGrowShrink** - tooenable Switch- of uitschakelen van Hallo **AutoGrowShrink** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="314b0-156">**EnableGrowShrink** - Switch tooenable or disable hello **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="314b0-157">**ParamSweepTasksPerCore** -aantal parametrische taken toogrow één kern.</span><span class="sxs-lookup"><span data-stu-id="314b0-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks toogrow one core.</span></span> <span data-ttu-id="314b0-158">Hallo standaardwaarde is één kern toogrow per taak.</span><span class="sxs-lookup"><span data-stu-id="314b0-158">hello default is toogrow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="314b0-159">HPC Pack QFE KB3134307 wijzigingen **ParamSweepTasksPerCore** te**TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="314b0-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** too**TasksPerResourceUnit**.</span></span> <span data-ttu-id="314b0-160">Dit is gebaseerd op Hallo taak brontype en kan dit knooppunt, socket of core.</span><span class="sxs-lookup"><span data-stu-id="314b0-160">It is based on hello job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="314b0-161">**GrowThreshold** -drempelwaarde van taken in de wachtrij tootrigger automatische groei.</span><span class="sxs-lookup"><span data-stu-id="314b0-161">**GrowThreshold** - Threshold of queued tasks tootrigger automatic growth.</span></span> <span data-ttu-id="314b0-162">Hallo standaardwaarde is 1, wat dat betekent als er 1 of meer taken in Hallo in de wachtrij staat, worden automatisch vergroot knooppunten.</span><span class="sxs-lookup"><span data-stu-id="314b0-162">hello default is 1, which means that if there are 1 or more tasks in hello queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="314b0-163">**GrowInterval** -Interval in minuten tootrigger automatische groei.</span><span class="sxs-lookup"><span data-stu-id="314b0-163">**GrowInterval** - Interval in minutes tootrigger automatic growth.</span></span> <span data-ttu-id="314b0-164">Hallo interval is standaard 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="314b0-164">hello default interval is 5 minutes.</span></span>
* <span data-ttu-id="314b0-165">**ShrinkInterval** -Interval in minuten tootrigger automatische verkleinen.</span><span class="sxs-lookup"><span data-stu-id="314b0-165">**ShrinkInterval** - Interval in minutes tootrigger automatic shrinking.</span></span> <span data-ttu-id="314b0-166">Hallo-interval is standaard 5 minuten. |</span><span class="sxs-lookup"><span data-stu-id="314b0-166">hello default interval is 5 minutes.|</span></span>
* <span data-ttu-id="314b0-167">**ShrinkIdleTimes** -aantal continue controles tooshrink tooindicate Hallo knooppunten niet actief zijn.</span><span class="sxs-lookup"><span data-stu-id="314b0-167">**ShrinkIdleTimes** - Number of continuous checks tooshrink tooindicate hello nodes are idle.</span></span> <span data-ttu-id="314b0-168">Hallo standaardinstelling is 3 maal.</span><span class="sxs-lookup"><span data-stu-id="314b0-168">hello default is 3 times.</span></span> <span data-ttu-id="314b0-169">Bijvoorbeeld, als hello **ShrinkInterval** is 5 minuten, HPC Pack controleert of Hallo knooppunt niet actief is om de 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="314b0-169">For example, if hello **ShrinkInterval** is 5 minutes, HPC Pack checks whether hello node is idle every 5 minutes.</span></span> <span data-ttu-id="314b0-170">Als Hallo knooppunten zich in niet-actieve status Hallo nadat 3 continue gecontroleerd (15 minuten), verkleint HPC Pack dat knooppunt.</span><span class="sxs-lookup"><span data-stu-id="314b0-170">If hello nodes are in hello idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="314b0-171">**ExtraNodesGrowRatio** -extra percentage van de knooppunten toogrow voor Message Passing Interface (MPI)-taken.</span><span class="sxs-lookup"><span data-stu-id="314b0-171">**ExtraNodesGrowRatio** - Additional percentage of nodes toogrow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="314b0-172">Hallo-standaardwaarde is 1, wat betekent dat HPC Pack knooppunten 1% voor MPI-taken groeit.</span><span class="sxs-lookup"><span data-stu-id="314b0-172">hello default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="314b0-173">**GrowByMin** -tooindicate Switch of Hallo autogrow beleid is gebaseerd op Hallo minimale resources die vereist zijn voor Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="314b0-173">**GrowByMin** - Switch tooindicate whether hello autogrow policy is based on hello minimum resources required for hello job.</span></span> <span data-ttu-id="314b0-174">Hallo standaardwaarde is ONWAAR, wat betekent dat HPC Pack knooppunten voor taken die zijn gebaseerd op Hallo maximale resources die vereist zijn voor Hallo taken groeit.</span><span class="sxs-lookup"><span data-stu-id="314b0-174">hello default is false, which means that HPC Pack grows nodes for jobs based on hello maximum resources required for hello jobs.</span></span>
* <span data-ttu-id="314b0-175">**SoaJobGrowThreshold** -drempelwaarde van binnenkomende SOA-aanvragen tootrigger Hallo automatische proces groeien.</span><span class="sxs-lookup"><span data-stu-id="314b0-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests tootrigger hello automatic grow process.</span></span> <span data-ttu-id="314b0-176">de standaardwaarde Hallo is 50000.</span><span class="sxs-lookup"><span data-stu-id="314b0-176">hello default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="314b0-177">Deze parameter wordt ondersteund vanaf HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="314b0-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="314b0-178">**SoaRequestsPerCore** -het aantal inkomende SOA aanvragen toogrow één kern.</span><span class="sxs-lookup"><span data-stu-id="314b0-178">**SoaRequestsPerCore** -Number of incoming SOA requests toogrow one core.</span></span> <span data-ttu-id="314b0-179">de standaardwaarde Hallo is 20000.</span><span class="sxs-lookup"><span data-stu-id="314b0-179">hello default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="314b0-180">Deze parameter wordt ondersteund vanaf HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="314b0-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="314b0-181">**ExcludeNodeGroups** – knooppunten in Hallo opgegeven knooppuntgroepen niet automatisch vergroten of verkleinen.</span><span class="sxs-lookup"><span data-stu-id="314b0-181">**ExcludeNodeGroups** – Nodes in hello specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="314b0-182">Deze parameter wordt ondersteund vanaf HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="314b0-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="314b0-183">MPI-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="314b0-183">MPI example</span></span>
<span data-ttu-id="314b0-184">Standaard HPC Pack 1% groeit extra knooppunten voor MPI-jobs (**ExtraNodesGrowRatio** too1 is ingesteld).</span><span class="sxs-lookup"><span data-stu-id="314b0-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set too1).</span></span> <span data-ttu-id="314b0-185">Hallo reden is dat MPI kan meerdere knooppunten zijn vereist, en Hallo taak kan alleen worden uitgevoerd als alle knooppunten klaar bent.</span><span class="sxs-lookup"><span data-stu-id="314b0-185">hello reason is that MPI may require multiple nodes, and hello job can only run when all nodes are ready.</span></span> <span data-ttu-id="314b0-186">Wanneer Azure knooppunten is gestart, soms één knooppunt mogelijk meer tijd toostart dan andere andere knooppunten van niet-actieve tijdens het wachten op dat knooppunt tooget gereed toobe veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="314b0-186">When Azure starts nodes, occasionally one node might need more time toostart than others, causing other nodes toobe idle while waiting for that node tooget ready.</span></span> <span data-ttu-id="314b0-187">Extra knooppunten groeiende HPC Pack vermindert de wachttijd voor deze resource en bespaart u mogelijk kosten.</span><span class="sxs-lookup"><span data-stu-id="314b0-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="314b0-188">percentage van de tooincrease Hallo van extra knooppunten voor MPI-taken (bijvoorbeeld too10%), een vergelijkbaar met opdracht uitvoeren</span><span class="sxs-lookup"><span data-stu-id="314b0-188">tooincrease hello percentage of extra nodes for MPI jobs (for example, too10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="314b0-189">SOA-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="314b0-189">SOA example</span></span>
<span data-ttu-id="314b0-190">Standaard **SoaJobGrowThreshold** too50000 is ingesteld en **SoaRequestsPerCore** too200000 is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="314b0-190">By default, **SoaJobGrowThreshold** is set too50000 and **SoaRequestsPerCore** is set too200000.</span></span> <span data-ttu-id="314b0-191">Als u één SOA-taak met 70000 aanvragen indient, er is een taak die in de wachtrij en inkomende aanvragen zijn 70000.</span><span class="sxs-lookup"><span data-stu-id="314b0-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="314b0-192">In dit geval HPC Pack 1 core groeit voor Hallo taak in de wachtrij en (70000 50000) voor binnenkomende aanvragen groeit / 20000 = 1 core daarom in totaal 2 kernen voor deze taak SOA groeit.</span><span class="sxs-lookup"><span data-stu-id="314b0-192">In this case HPC Pack grows 1 core for hello queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-hello-azureautogrowshrinkps1-script"></a><span data-ttu-id="314b0-193">Hallo AzureAutoGrowShrink.ps1 script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="314b0-193">Run hello AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="314b0-194">Vereisten</span><span class="sxs-lookup"><span data-stu-id="314b0-194">Prerequisites</span></span>

* <span data-ttu-id="314b0-195">**HPC Pack 2012 R2 Update 1 of hoger cluster** - hello **AzureAutoGrowShrink.ps1** script in Hallo % CCP_HOME % bin-map is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="314b0-195">**HPC Pack 2012 R2 Update 1 or later cluster** - hello **AzureAutoGrowShrink.ps1** script is installed in hello %CCP_HOME%bin folder.</span></span> <span data-ttu-id="314b0-196">hoofdknooppunt Hallo-cluster kan worden geïmplementeerd on-premises of in een Azure VM.</span><span class="sxs-lookup"><span data-stu-id="314b0-196">hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="314b0-197">Zie [een hybride-cluster met HPC Pack instellen](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget gestart met het hoofdknooppunt van een lokale en Azure 'burst' knooppunten.</span><span class="sxs-lookup"><span data-stu-id="314b0-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="314b0-198">Zie Hallo [HPC Pack IaaS-implementatiescript](hpcpack-cluster-powershell-script.md) tooquickly een HPC Pack cluster in Azure VM's implementeren of gebruik een [snelstartsjabloon met de Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="314b0-198">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="314b0-199">**Azure PowerShell 1.4.0** -Hallo script momenteel is afhankelijk van deze specifieke versie van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="314b0-199">**Azure PowerShell 1.4.0** - hello script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="314b0-200">**Voor een cluster met Azure burst knooppunten** -Hallo-script uitvoeren op een clientcomputer waarop HPC Pack is geïnstalleerd of op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="314b0-200">**For a cluster with Azure burst nodes** - Run hello script on a client computer where HPC Pack is installed, or on hello head node.</span></span> <span data-ttu-id="314b0-201">Als dit wordt uitgevoerd op een clientcomputer, zorg ervoor dat u ingesteld Hallo variabele $env: CCP_SCHEDULER toopoint toohello hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="314b0-201">If running on a client computer, ensure that you set hello variable $env:CCP_SCHEDULER toopoint toohello head node.</span></span> <span data-ttu-id="314b0-202">Hello Azure 'burst' knooppunten toohello cluster moeten worden toegevoegd, maar kunnen ze zich in Hallo status niet geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="314b0-202">hello Azure “burst” nodes must be added toohello cluster, but they may be in hello Not-Deployed state.</span></span>
* <span data-ttu-id="314b0-203">**Voor een cluster dat is geïmplementeerd in Azure Virtual machines (Resource Manager-implementatiemodel)** -voor een cluster van Azure VM's geïmplementeerd in de Resource Manager-implementatiemodel Hallo Hallo script ondersteunt twee methoden voor verificatie op Azure: aanmelden tooyour Azure-account toorun hello script telkens (door het uitvoeren van `Login-AzureRmAccount`, of een service-principal tooauthenticate configureren met een certificaat.</span><span class="sxs-lookup"><span data-stu-id="314b0-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in hello Resource Manager deployment model, hello script supports two methods for Azure authentication: sign in tooyour Azure account toorun hello script every time (by running `Login-AzureRmAccount`, or configure a service principal tooauthenticate with a certificate.</span></span> <span data-ttu-id="314b0-204">HPC Pack Hallo script biedt **ConfigARMAutoGrowShrinkCert.ps** toocreate een service-principal met certificaat.</span><span class="sxs-lookup"><span data-stu-id="314b0-204">HPC Pack provides hello script **ConfigARMAutoGrowShrinkCert.ps** toocreate a service principal with certificate.</span></span> <span data-ttu-id="314b0-205">Hallo script maakt een toepassing Azure Active Directory (Azure AD) en een service-principal en wijst Hallo Inzender rol toohello service-principal.</span><span class="sxs-lookup"><span data-stu-id="314b0-205">hello script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns hello Contributor role toohello service principal.</span></span> <span data-ttu-id="314b0-206">toorun Hallo script, start u Azure PowerShell als administrator en Voer Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="314b0-206">toorun hello script, start Azure PowerShell  as administrator and run hello following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="314b0-207">Voor meer informatie over **ConfigARMAutoGrowShrinkCert.ps1**, voert `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span><span class="sxs-lookup"><span data-stu-id="314b0-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="314b0-208">**Voor een cluster dat is geïmplementeerd in Azure Virtual machines (klassieke implementatiemodel)** -Hallo-script uitvoeren op Hallo hoofdknooppunt VM, omdat deze afhankelijk Hallo **Start HpcIaaSNode.ps1** en **Stop-HpcIaaSNode.ps1**scripts die zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="314b0-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run hello script on hello head node VM, because it depends on hello **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="314b0-209">Deze scripts Bovendien vereisen een Azure-beheercertificaat of bestand publicatie-instellingen (Zie [rekenknooppunten beheren in een Pack HPC-cluster in Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="314b0-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="314b0-210">Zorg ervoor dat alle Hallo compute knooppunt u moet virtuele machines toohello cluster al zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="314b0-210">Make sure all hello compute node VMs you need are already added toohello cluster.</span></span> <span data-ttu-id="314b0-211">Ze mogelijk Hallo status gestopt.</span><span class="sxs-lookup"><span data-stu-id="314b0-211">They may be in hello Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="314b0-212">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="314b0-212">Syntax</span></span>
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="314b0-213">Parameters</span><span class="sxs-lookup"><span data-stu-id="314b0-213">Parameters</span></span>
* <span data-ttu-id="314b0-214">**NodeTemplates** -namen van Hallo knooppunt sjablonen toodefine Hallo bereik voor Hallo knooppunten toogrow en te verkleinen.</span><span class="sxs-lookup"><span data-stu-id="314b0-214">**NodeTemplates** - Names of hello node templates toodefine hello scope for hello nodes toogrow and shrink.</span></span> <span data-ttu-id="314b0-215">Als niet wordt opgegeven (Hallo standaardwaarde is @()), alle knooppunten in Hallo **AzureNodes** knooppunt groep zijn wanneer het in bereik **NodeType** heeft een waarde van AzureNodes en alle knooppunten in Hallo **ComputeNodes** knooppunt groep zijn wanneer het in bereik **NodeType** een waarde heeft van ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="314b0-215">If not specified (hello default value is @()), all nodes in hello **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in hello **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="314b0-216">**JobTemplates** -namen van Hallo sjablonen toodefine Hallo bereik voor Hallo knooppunten toogrow taak.</span><span class="sxs-lookup"><span data-stu-id="314b0-216">**JobTemplates** - Names of hello job templates toodefine hello scope for hello nodes toogrow.</span></span>
* <span data-ttu-id="314b0-217">**NodeType** - type knooppunt toogrow Hallo en verkleinen.</span><span class="sxs-lookup"><span data-stu-id="314b0-217">**NodeType** - hello type of node toogrow and shrink.</span></span> <span data-ttu-id="314b0-218">Ondersteunde waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="314b0-218">Supported values are:</span></span>

  * <span data-ttu-id="314b0-219">**AzureNodes** : voor Azure PaaS (burst) knooppunten in een on-premises of Azure IaaS-cluster.</span><span class="sxs-lookup"><span data-stu-id="314b0-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="314b0-220">**ComputeNodes** : voor het rekenknooppunt VM's alleen in een Azure IaaS-cluster.</span><span class="sxs-lookup"><span data-stu-id="314b0-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="314b0-221">**NumOfQueuedJobsPerNodeToGrow** -aantal taken in de wachtrij is vereist toogrow één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="314b0-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required toogrow one node.</span></span>
* <span data-ttu-id="314b0-222">**NumOfQueuedJobsToGrowThreshold** -Hallo drempelwaarde voor aantal wachtrijtaken toostart Hallo proces groeien.</span><span class="sxs-lookup"><span data-stu-id="314b0-222">**NumOfQueuedJobsToGrowThreshold** - hello threshold number of queued jobs toostart hello grow process.</span></span>
* <span data-ttu-id="314b0-223">**NumOfActiveQueuedTasksPerNodeToGrow** -Hallo aantal actieve taken in de wachtrij is vereist toogrow één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="314b0-223">**NumOfActiveQueuedTasksPerNodeToGrow** - hello number of active queued tasks required toogrow one node.</span></span> <span data-ttu-id="314b0-224">Als **NumOfQueuedJobsPerNodeToGrow** wordt opgegeven met een waarde groter dan 0, worden deze parameter wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="314b0-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="314b0-225">**NumOfActiveQueuedTasksToGrowThreshold** -Hallo drempelwaarde voor aantal actieve taken in de wachtrij toostart Hallo proces groeien.</span><span class="sxs-lookup"><span data-stu-id="314b0-225">**NumOfActiveQueuedTasksToGrowThreshold** - hello threshold number of active queued tasks toostart hello grow process.</span></span>
* <span data-ttu-id="314b0-226">**NumOfInitialNodesToGrow** - hello minimum aantal knooppunten toogrow initiële als alle Hallo knooppunten in het bereik zijn **niet geïmplementeerd** of **gestopt (Deallocated)**.</span><span class="sxs-lookup"><span data-stu-id="314b0-226">**NumOfInitialNodesToGrow** - hello initial minimum number of nodes toogrow if all hello nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="314b0-227">**GrowCheckIntervalMins** -hello-interval in minuten tussen toogrow controleert.</span><span class="sxs-lookup"><span data-stu-id="314b0-227">**GrowCheckIntervalMins** - hello interval in minutes between checks toogrow.</span></span>
* <span data-ttu-id="314b0-228">**ShrinkCheckIntervalMins** -hello-interval in minuten tussen tooshrink controleert.</span><span class="sxs-lookup"><span data-stu-id="314b0-228">**ShrinkCheckIntervalMins** - hello interval in minutes between checks tooshrink.</span></span>
* <span data-ttu-id="314b0-229">**ShrinkCheckIdleTimes** -Hallo continue verkleinen controles (gescheiden door **ShrinkCheckIntervalMins**) tooindicate Hallo knooppunten niet actief zijn.</span><span class="sxs-lookup"><span data-stu-id="314b0-229">**ShrinkCheckIdleTimes** - hello number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) tooindicate hello nodes are idle.</span></span>
* <span data-ttu-id="314b0-230">**UseLastConfigurations** -Hallo vorige configuraties in Hallo argument bestand opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="314b0-230">**UseLastConfigurations** - hello previous configurations saved in hello argument file.</span></span>
* <span data-ttu-id="314b0-231">**ArgFile**- naam van Hallo argument bestand dat wordt gebruikt toosave Hallo en Hallo configuraties toorun Hallo updatescript.</span><span class="sxs-lookup"><span data-stu-id="314b0-231">**ArgFile**- hello name of hello argument file used toosave and update hello configurations toorun hello script.</span></span>
* <span data-ttu-id="314b0-232">**LogFilePrefix** -naam van het voorvoegsel van het logboekbestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="314b0-232">**LogFilePrefix** - hello prefix name of hello log file.</span></span> <span data-ttu-id="314b0-233">U kunt een pad opgeven.</span><span class="sxs-lookup"><span data-stu-id="314b0-233">You can specify a path.</span></span> <span data-ttu-id="314b0-234">Hallo-logboek is standaard de huidige werkmap toohello geschreven.</span><span class="sxs-lookup"><span data-stu-id="314b0-234">By default hello log is written toohello current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="314b0-235">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="314b0-235">Example 1</span></span>
<span data-ttu-id="314b0-236">Hallo configureert volgende voorbeeld hello Azure burst knooppunten die zijn geïmplementeerd met de standaardsjabloon AzureNode toogrow en automatisch verkleinen.</span><span class="sxs-lookup"><span data-stu-id="314b0-236">hello following example configures hello Azure burst nodes deployed with the Default AzureNode Template toogrow and shrink automatically.</span></span> <span data-ttu-id="314b0-237">Als alle knooppunten in eerste instantie in Hallo **niet geïmplementeerd** staat, ten minste 3 knooppunten worden gestart.</span><span class="sxs-lookup"><span data-stu-id="314b0-237">If all the nodes are initially in hello **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="314b0-238">Als het aantal taken in de wachtrij Hallo groter is dan 8, Hallo script knooppunten begint, totdat hun aantal Hallo ratio van opdrachten in de wachtrij overschrijdt **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="314b0-238">If hello number of queued jobs exceeds 8, hello script starts nodes until their number exceeds hello ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="314b0-239">Als een knooppunt toobe 3 opeenvolgende niet-actieve tijd inactief gevonden wordt, wordt het gestopt.</span><span class="sxs-lookup"><span data-stu-id="314b0-239">If a node is found toobe idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="314b0-240">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="314b0-240">Example 2</span></span>
<span data-ttu-id="314b0-241">Hallo configureert volgende voorbeeld hello Azure compute knooppunt virtuele machines die zijn geïmplementeerd met Hallo standaardsjabloon ComputeNode toogrow en automatisch verkleinen.</span><span class="sxs-lookup"><span data-stu-id="314b0-241">hello following example configures hello Azure compute node VMs deployed with hello Default ComputeNode Template toogrow and shrink automatically.</span></span>
<span data-ttu-id="314b0-242">Hallo-taken die zijn geconfigureerd door de taak standaardsjabloon Hallo definiëren Hallo bereik van de werkbelasting op Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="314b0-242">hello jobs configured by hello Default job template define hello scope of the workload on hello cluster.</span></span> <span data-ttu-id="314b0-243">Als alle knooppunten van het Hallo in eerste instantie zijn gestopt, worden ten minste 5 knooppunten gestart.</span><span class="sxs-lookup"><span data-stu-id="314b0-243">If all hello nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="314b0-244">Als het aantal actieve taken in de wachtrij Hallo groter is dan 15, Hallo script knooppunten begint, totdat hun aantal Hallo ratio van actieve taken in de wachtrij te overschrijdt**NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="314b0-244">If hello number of active queued tasks exceeds 15, hello script starts nodes until their number exceeds hello ratio of active queued tasks too**NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="314b0-245">Als een knooppunt toobe 10 opeenvolgende niet-actieve tijd inactief gevonden wordt, wordt het gestopt.</span><span class="sxs-lookup"><span data-stu-id="314b0-245">If a node is found toobe idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
