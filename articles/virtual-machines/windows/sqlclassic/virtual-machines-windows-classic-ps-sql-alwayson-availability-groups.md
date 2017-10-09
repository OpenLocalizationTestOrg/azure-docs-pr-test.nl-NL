---
title: aaaConfigure hello AlwaysOn-beschikbaarheidsgroep op een virtuele machine in Azure met behulp van PowerShell | Microsoft Docs
description: Deze zelfstudie maakt gebruik van bronnen die zijn gemaakt met het klassieke implementatiemodel Hallo. U kunt PowerShell toocreate een AlwaysOn-beschikbaarheidsgroep gebruikt in Azure.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="b0445-104">Hallo-AlwaysOn-beschikbaarheidsgroep configureren op een virtuele machine in Azure met PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0445-104">Configure hello Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0445-105">Klassieke: UI</span><span class="sxs-lookup"><span data-stu-id="b0445-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="b0445-106">[Klassieke: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="b0445-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="b0445-107">Voordat u begint, kunt u overwegen of u kunt deze taak in Azure resource manager-model voltooien.</span><span class="sxs-lookup"><span data-stu-id="b0445-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="b0445-108">U wordt aangeraden Azure resource manager-model voor nieuwe implementaties.</span><span class="sxs-lookup"><span data-stu-id="b0445-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="b0445-109">Zie [op virtuele machines in Azure SQL Server altijd op beschikbaarheidsgroepen](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b0445-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0445-110">U wordt aangeraden de meeste nieuwe implementaties Hallo Resource Manager-model gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b0445-110">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b0445-111">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b0445-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b0445-112">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0445-112">This article covers using hello classic deployment model.</span></span>

<span data-ttu-id="b0445-113">Azure virtuele machines (VM's) kunt database beheerders toolower Hallo kosten van een SQL Server-systeem voor hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="b0445-113">Azure virtual machines (VMs) can help database administrators toolower hello cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="b0445-114">Deze zelfstudie leert u hoe tooimplement een beschikbaarheid van groep met behulp van SQL Server Always On end-to-end binnen een Azure-omgeving.</span><span class="sxs-lookup"><span data-stu-id="b0445-114">This tutorial shows you how tooimplement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="b0445-115">Uw oplossing SQL Server Always On in Azure wordt aan het einde van de Hallo Hallo zelfstudie bestaan uit Hallo volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="b0445-115">At hello end of hello tutorial, your SQL Server Always On solution in Azure will consist of hello following elements:</span></span>

* <span data-ttu-id="b0445-116">Een virtueel netwerk met meerdere subnetten, met inbegrip van een front-end- en een back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="b0445-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="b0445-117">Een domeincontroller met een Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="b0445-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="b0445-118">Twee SQL Server-VM's die geïmplementeerd toohello back-end-subnet en gekoppelde toohello Active Directory-domein zijn.</span><span class="sxs-lookup"><span data-stu-id="b0445-118">Two SQL Server VMs that are deployed toohello back-end subnet and joined toohello Active Directory domain.</span></span>
* <span data-ttu-id="b0445-119">Drie knooppunten Windows failovercluster met Hallo Knooppuntmeerderheid quorummodel.</span><span class="sxs-lookup"><span data-stu-id="b0445-119">A three-node Windows failover cluster with hello Node Majority quorum model.</span></span>
* <span data-ttu-id="b0445-120">Een beschikbaarheidsgroep met twee replica's voor synchrone doorvoer van een beschikbaarheidsdatabase.</span><span class="sxs-lookup"><span data-stu-id="b0445-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="b0445-121">Dit scenario is een goede keuze voor de eenvoud op Azure, niet voor de kosteneffectiviteit of andere factoren.</span><span class="sxs-lookup"><span data-stu-id="b0445-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="b0445-122">Bijvoorbeeld, kunt u met behulp van de domeincontroller Hallo als Hallo bestandssharewitness van quorum in een failovercluster met twee knooppunten Hallo aantal virtuele machines voor een groep twee replica beschikbaarheid toosave minimaliseren op rekenuren in Azure.</span><span class="sxs-lookup"><span data-stu-id="b0445-122">For example, you can minimize hello number of VMs for a two-replica availability group toosave on compute hours in Azure by using hello domain controller as hello quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="b0445-123">Deze methode wordt Hallo-aantal VM's met één van Hallo hierboven configuratie verlaagd.</span><span class="sxs-lookup"><span data-stu-id="b0445-123">This method reduces hello VM count by one from hello above configuration.</span></span>

<span data-ttu-id="b0445-124">Deze zelfstudie is bedoeld tooshow u stappen die vereist tooset up Hallo zijn Hallo oplossing hierboven beschreven zonder bespreekt Hallo details van elke stap.</span><span class="sxs-lookup"><span data-stu-id="b0445-124">This tutorial is intended tooshow you hello steps that are required tooset up hello described solution above, without elaborating on hello details of each step.</span></span> <span data-ttu-id="b0445-125">Daarom stap in plaats van mits Hallo GUI-configuratiestappen, deze PowerShell-scripts tootake gebruikt u snel tot en met elke.</span><span class="sxs-lookup"><span data-stu-id="b0445-125">Therefore, instead of providing hello GUI configuration steps, it uses PowerShell scripting tootake you quickly through each step.</span></span> <span data-ttu-id="b0445-126">Deze zelfstudie wordt ervan uitgegaan dat de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="b0445-126">This tutorial assumes hello following:</span></span>

* <span data-ttu-id="b0445-127">U hebt al een Azure-account met Hallo virtuele machine abonnement.</span><span class="sxs-lookup"><span data-stu-id="b0445-127">You already have an Azure account with hello virtual machine subscription.</span></span>
* <span data-ttu-id="b0445-128">U hebt geïnstalleerd Hallo [Azure PowerShell-cmdlets](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b0445-128">You've installed hello [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="b0445-129">U hebt al een goed begrip van AlwaysOn-beschikbaarheidsgroepen voor oplossingen on-premises.</span><span class="sxs-lookup"><span data-stu-id="b0445-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="b0445-130">Zie voor meer informatie [altijd op beschikbaarheidsgroepen (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0445-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a><span data-ttu-id="b0445-131">Verbinding maken met tooyour Azure-abonnement en Hallo virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="b0445-131">Connect tooyour Azure subscription and create hello virtual network</span></span>
1. <span data-ttu-id="b0445-132">In een PowerShell-venster op de lokale computer hello Azure-module importeren, Hallo publiceren instellingen bestand tooyour machine downloaden en verbinding maken met de PowerShell-sessie tooyour Azure-abonnement via Hallo gedownload publicatie-instellingen te importeren.</span><span class="sxs-lookup"><span data-stu-id="b0445-132">In a PowerShell window on your local computer, import hello Azure module, download hello publishing settings file tooyour machine, and connect your PowerShell session tooyour Azure subscription by importing hello downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="b0445-133">Hallo **Get-AzurePublishSettingsFile** opdracht genereert u een beheercertificaat met Azure automatisch en downloadt u tooyour machine.</span><span class="sxs-lookup"><span data-stu-id="b0445-133">hello **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it tooyour machine.</span></span> <span data-ttu-id="b0445-134">Een browser wordt automatisch geopend en u bent na vragen aan gebruiker tooenter Hallo Microsoft-accountreferenties voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b0445-134">A browser is automatically opened, and you're prompted tooenter hello Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="b0445-135">Hallo gedownload **.publishsettings** bestand bevat alle Hallo gegevens die u nodig toomanage uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b0445-135">hello downloaded **.publishsettings** file contains all hello information that you need toomanage your Azure subscription.</span></span> <span data-ttu-id="b0445-136">Na het opslaan van deze lokale map tooa importeren met Hallo **importeren AzurePublishSettingsFile** opdracht.</span><span class="sxs-lookup"><span data-stu-id="b0445-136">After saving this file tooa local directory, import it by using hello **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b0445-137">Hallo .publishsettings-bestand bevat uw referenties (ongecodeerde) die gebruikt tooadminister zijn uw Azure-abonnementen en services.</span><span class="sxs-lookup"><span data-stu-id="b0445-137">hello .publishsettings file contains your credentials (unencoded) that are used tooadminister your Azure subscriptions and services.</span></span> <span data-ttu-id="b0445-138">Hallo aanbevolen beveiligingsprocedure voor dit bestand is toostore deze tijdelijk buiten uw adreslijsten bron (bijvoorbeeld in Hallo Libraries\Documents map), en vervolgens verwijdert nadat Hallo importeren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b0445-138">hello security best practice for this file is toostore it temporarily outside your source directories (for example, in hello Libraries\Documents folder), and then delete it after hello import has finished.</span></span> <span data-ttu-id="b0445-139">Een kwaadwillende gebruiker die u toegang tot toohello .publishsettings-bestand krijgt kunt bewerken, maken en verwijderen van uw Azure-services.</span><span class="sxs-lookup"><span data-stu-id="b0445-139">A malicious user who gains access toohello .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="b0445-140">Definieer een reeks variabelen die u toocreate uw cloud IT-infrastructuur gebruiken wilt.</span><span class="sxs-lookup"><span data-stu-id="b0445-140">Define a series of variables that you'll use toocreate your cloud IT infrastructure.</span></span>

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    <span data-ttu-id="b0445-141">Betalen aandacht toohello tooensure die uw opdrachten later slaagt te volgen:</span><span class="sxs-lookup"><span data-stu-id="b0445-141">Pay attention toohello following tooensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="b0445-142">Variabelen **$storageAccountName** en **$dcServiceName** moeten uniek zijn omdat ze gebruikt tooidentify uw cloud-opslagaccount en cloud-server, respectievelijk op Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="b0445-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used tooidentify your cloud storage account and cloud server, respectively, on hello Internet.</span></span>
   * <span data-ttu-id="b0445-143">Hallo namen die u voor variabelen opgeeft **$affinityGroupName** en **$virtualNetworkName** zijn geconfigureerd in het configuratiebestand voor Hallo virtueel netwerk die u later gaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b0445-143">hello names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in hello virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="b0445-144">**$sqlImageName** geeft de naam bijgewerkt Hallo van Hallo VM-installatiekopie waarin SQL Server 2012 Service Pack 1 Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="b0445-144">**$sqlImageName** specifies hello updated name of hello VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="b0445-145">Ter vereenvoudiging **Contoso! 000** is Hallo hetzelfde wachtwoord dat wordt gebruikt in de hele zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0445-145">For simplicity, **Contoso!000** is hello same password that's used throughout hello entire tutorial.</span></span>

3. <span data-ttu-id="b0445-146">Maak een affiniteitsgroep.</span><span class="sxs-lookup"><span data-stu-id="b0445-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="b0445-147">Een virtueel netwerk maken door een configuratiebestand te importeren.</span><span class="sxs-lookup"><span data-stu-id="b0445-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="b0445-148">Hallo-configuratiebestand bevat Hallo XML-document te volgen.</span><span class="sxs-lookup"><span data-stu-id="b0445-148">hello configuration file contains hello following XML document.</span></span> <span data-ttu-id="b0445-149">Kort samengevat: Hiermee wordt een virtueel netwerk met de naam **ContosoNET** in Hallo affiniteitsgroep aangeroepen **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="b0445-149">In brief, it specifies a virtual network called **ContosoNET** in hello affinity group called **ContosoAG**.</span></span> <span data-ttu-id="b0445-150">Het Hallo-adresruimte is **10.10.0.0/16** en heeft twee subnetten **10.10.1.0/24** en **10.10.2.0/24**, die zijn Hallo front-subnet en back-subnet, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="b0445-150">It has hello address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are hello front subnet and back subnet, respectively.</span></span> <span data-ttu-id="b0445-151">Hallo front-subnet is waarin u de clienttoepassingen, zoals Microsoft SharePoint kunt plaatsen.</span><span class="sxs-lookup"><span data-stu-id="b0445-151">hello front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="b0445-152">Hallo back-subnet is plaats voegt u Hallo SQL Server-VM's.</span><span class="sxs-lookup"><span data-stu-id="b0445-152">hello back subnet is where you'll place hello SQL Server VMs.</span></span> <span data-ttu-id="b0445-153">Als u Hallo wijzigt **$affinityGroupName** en **$virtualNetworkName** variabelen eerder, moet u ook wijzigen Hallo namen onderstaande overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="b0445-153">If you change hello **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change hello corresponding names below.</span></span>

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. <span data-ttu-id="b0445-154">Maak een opslagaccount die is gekoppeld aan een affiniteitsgroep Hallo gemaakt en stel dit in als de huidige opslagaccount Hallo in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="b0445-154">Create a storage account that's associated with hello affinity group that you created, and set it as hello current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="b0445-155">Hallo domeincontrollerserver maken in Hallo nieuwe cloud service- en beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="b0445-155">Create hello domain controller server in hello new cloud service and availability set.</span></span>

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    <span data-ttu-id="b0445-156">Deze opdrachten piped Hallo volgende dingen:</span><span class="sxs-lookup"><span data-stu-id="b0445-156">These piped commands do hello following things:</span></span>

   * <span data-ttu-id="b0445-157">**Nieuwe AzureVMConfig** maakt u een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="b0445-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="b0445-158">**Voeg AzureProvisioningConfig** biedt Hallo parameters voor de configuratie van een zelfstandige Windows-server.</span><span class="sxs-lookup"><span data-stu-id="b0445-158">**Add-AzureProvisioningConfig** gives hello configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="b0445-159">**Voeg AzureDataDisk** Hallo gegevensschijf die u gebruiken gaat voor het opslaan van Active Directory-gegevens met caching optie set tooNone hello wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b0445-159">**Add-AzureDataDisk** adds hello data disk that you'll use for storing Active Directory data, with hello caching option set tooNone.</span></span>
   * <span data-ttu-id="b0445-160">**Nieuwe AzureVM** maakt een nieuwe cloudservice en maakt u nieuwe virtuele machine van Azure in een nieuwe cloudservice Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0445-160">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span>

7. <span data-ttu-id="b0445-161">Wachten op Hallo nieuwe VM toobe volledig is ingericht en Hallo extern bureaublad bestand tooyour-werkmap downloaden.</span><span class="sxs-lookup"><span data-stu-id="b0445-161">Wait for hello new VM toobe fully provisioned, and download hello remote desktop file tooyour working directory.</span></span> <span data-ttu-id="b0445-162">Omdat hello nieuwe virtuele machine in Azure een tooprovision lang, Hallo `while` lus blijft toopoll Hallo van nieuwe virtuele machine totdat deze klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="b0445-162">Because hello new Azure VM takes a long time tooprovision, hello `while` loop continues toopoll hello new VM until it's ready for use.</span></span>

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

<span data-ttu-id="b0445-163">Hallo domain controller-server is nu is ingericht.</span><span class="sxs-lookup"><span data-stu-id="b0445-163">hello domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="b0445-164">Vervolgens configureert u Hallo Active Directory-domein op deze domeincontrollerserver.</span><span class="sxs-lookup"><span data-stu-id="b0445-164">Next, you'll configure hello Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="b0445-165">Laat Hallo PowerShell-venster geopend op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="b0445-165">Leave hello PowerShell window open on your local computer.</span></span> <span data-ttu-id="b0445-166">U gaat deze gebruiken opnieuw hoger toocreate Hallo twee SQL Server-VM's.</span><span class="sxs-lookup"><span data-stu-id="b0445-166">You'll use it again later toocreate hello two SQL Server VMs.</span></span>

## <a name="configure-hello-domain-controller"></a><span data-ttu-id="b0445-167">Hallo-domeincontroller configureren</span><span class="sxs-lookup"><span data-stu-id="b0445-167">Configure hello domain controller</span></span>
1. <span data-ttu-id="b0445-168">Verbinding maken met toohello domeincontrollerserver beschadigt door Hallo extern bureaublad-bestand.</span><span class="sxs-lookup"><span data-stu-id="b0445-168">Connect toohello domain controller server by launching hello remote desktop file.</span></span> <span data-ttu-id="b0445-169">Gebruik de gebruikersnaam AzureAdmin en het wachtwoord van beheerder Hallo-machine **Contoso! 000**, die u hebt opgegeven tijdens het maken van Hallo van nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b0445-169">Use hello machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created hello new VM.</span></span>
2. <span data-ttu-id="b0445-170">Open een PowerShell-venster in de beheerdersmodus.</span><span class="sxs-lookup"><span data-stu-id="b0445-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="b0445-171">Voer de volgende Hallo **DCPROMO. EXE** opdracht tooset up Hallo **corp.contoso.com** domein met de gegevensmappen Hallo op station M.</span><span class="sxs-lookup"><span data-stu-id="b0445-171">Run hello following **DCPROMO.EXE** command tooset up hello **corp.contoso.com** domain, with hello data directories on drive M.</span></span>

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    <span data-ttu-id="b0445-172">Nadat het Hallo-opdracht is voltooid, wordt Hallo VM automatisch opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="b0445-172">After hello command finishes, hello VM restarts automatically.</span></span>

4. <span data-ttu-id="b0445-173">Verbinding maken toohello domeincontrollerserver opnieuw beschadigt door Hallo extern bureaublad-bestand.</span><span class="sxs-lookup"><span data-stu-id="b0445-173">Connect toohello domain controller server again by launching hello remote desktop file.</span></span> <span data-ttu-id="b0445-174">Deze tijd, meld u aan als **CORP\Administrator**.</span><span class="sxs-lookup"><span data-stu-id="b0445-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="b0445-175">Open een PowerShell-venster in de beheerdersmodus en Hallo Active Directory PowerShell-module importeren met behulp van Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b0445-175">Open a PowerShell window in administrator mode, and import hello Active Directory PowerShell module by using hello following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="b0445-176">Voer Hallo opdrachten tooadd drie gebruikers toohello domein te volgen.</span><span class="sxs-lookup"><span data-stu-id="b0445-176">Run hello following commands tooadd three users toohello domain.</span></span>

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    <span data-ttu-id="b0445-177">**CORP\Install** gebruikte tooconfigure is alles verwante toohello SQL Server-service-exemplaren, Hallo failover-cluster en Hallo-beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="b0445-177">**CORP\Install** is used tooconfigure everything related toohello SQL Server service instances, hello failover cluster, and hello availability group.</span></span> <span data-ttu-id="b0445-178">**CORP\SQLSvc1** en **CORP\SQLSvc2** worden gebruikt als Hallo SQL Server-serviceaccounts voor Hallo twee SQL Server-VM's.</span><span class="sxs-lookup"><span data-stu-id="b0445-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as hello SQL Server service accounts for hello two SQL Server VMs.</span></span>
7. <span data-ttu-id="b0445-179">Hallo volgende, voert deze opdrachten toogive **CORP\Install** Hallo machtigingen toocreate computerobjecten in Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="b0445-179">Next, run hello following commands toogive **CORP\Install** hello permissions toocreate computer objects in hello domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="b0445-180">Hallo hierboven opgegeven GUID is Hallo GUID voor objecttype Hallo-computer.</span><span class="sxs-lookup"><span data-stu-id="b0445-180">hello GUID specified above is hello GUID for hello computer object type.</span></span> <span data-ttu-id="b0445-181">Hallo **CORP\Install** account moet Hallo **alle eigenschappen lezen** en **Computerobjecten maken** machtiging toocreate Hallo Active Direct objecten voor Hallo failover cluster.</span><span class="sxs-lookup"><span data-stu-id="b0445-181">hello **CORP\Install** account needs hello **Read All Properties** and **Create Computer Objects** permission toocreate hello Active Direct objects for hello failover cluster.</span></span> <span data-ttu-id="b0445-182">Hallo **alle eigenschappen lezen** machtiging is al toegewezen tooCORP\Install standaard, dus u toogrant hoeft het expliciet.</span><span class="sxs-lookup"><span data-stu-id="b0445-182">hello **Read All Properties** permission is already given tooCORP\Install by default, so you don't need toogrant it explicitly.</span></span> <span data-ttu-id="b0445-183">Zie voor meer informatie over de machtigingen die zijn vereist toocreate Hallo failover-cluster, [stapsgewijze handleiding voor Failover-Cluster: Accounts configureren in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0445-183">For more information on permissions that are needed toocreate hello failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="b0445-184">Nu dat u klaar bent met het configureren van Active Directory en gebruikersobjecten hello, hebt u twee SQL Server-virtuele machines maken en toothis domein kan toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b0445-184">Now that you've finished configuring Active Directory and hello user objects, you'll create two SQL Server VMs and join them toothis domain.</span></span>

## <a name="create-hello-sql-server-vms"></a><span data-ttu-id="b0445-185">Hallo SQL Server-VM's maken</span><span class="sxs-lookup"><span data-stu-id="b0445-185">Create hello SQL Server VMs</span></span>
1. <span data-ttu-id="b0445-186">Blijven toouse Hallo PowerShell-venster is geopend op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="b0445-186">Continue toouse hello PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="b0445-187">Definieer Hallo aanvullende variabelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b0445-187">Define hello following additional variables:</span></span>

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    <span data-ttu-id="b0445-188">IP-adres Hallo **10.10.0.4** is doorgaans toegewezen toohello eerste VM die u in Hallo maakt **10.10.0.0/16** subnet van uw virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="b0445-188">hello IP address **10.10.0.4** is typically assigned toohello first VM that you create in hello **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="b0445-189">U moet controleren of het Hallo-adres van de domain controller-server door het uitvoeren van **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="b0445-189">You should verify that this is hello address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="b0445-190">Voer Hallo doorgesluisd opdrachten toocreate Hallo eerst na VM in het Hallo-failovercluster, met de naam **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="b0445-190">Run hello following piped commands toocreate hello first VM in hello failover cluster, named **ContosoQuorum**:</span></span>

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    <span data-ttu-id="b0445-191">Let op Hallo volgende met betrekking tot de bovenstaande Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="b0445-191">Note hello following regarding hello command above:</span></span>

   * <span data-ttu-id="b0445-192">**Nieuwe AzureVMConfig** maakt u een VM-configuratie met de naam van de gewenste beschikbaarheidsset Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0445-192">**New-AzureVMConfig** creates a VM configuration with hello desired availability set name.</span></span> <span data-ttu-id="b0445-193">Hallo latere virtuele machines wordt gemaakt met Hallo dezelfde beschikbaarheidsset zodat ze bent gekoppeld toohello dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="b0445-193">hello subsequent VMs will be created with hello same availability set name so that they're joined toohello same availability set.</span></span>
   * <span data-ttu-id="b0445-194">**Voeg AzureProvisioningConfig** joins Hallo VM toohello Active Directory-domein dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b0445-194">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="b0445-195">**Set-AzureSubnet** plaatsen Hallo VM in Hallo back-subnet.</span><span class="sxs-lookup"><span data-stu-id="b0445-195">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="b0445-196">**Nieuwe AzureVM** maakt een nieuwe cloudservice en maakt u nieuwe virtuele machine van Azure in een nieuwe cloudservice Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0445-196">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span> <span data-ttu-id="b0445-197">Hallo **DnsSettings** parameter die Hallo DNS-server geeft u voor het Hallo-servers in een nieuwe cloudservice Hallo Hallo IP-adres **10.10.0.4**.</span><span class="sxs-lookup"><span data-stu-id="b0445-197">hello **DnsSettings** parameter specifies that hello DNS server for hello servers in hello new cloud service has hello IP address **10.10.0.4**.</span></span> <span data-ttu-id="b0445-198">Dit is Hallo IP-adres van Hallo domeincontrollerserver.</span><span class="sxs-lookup"><span data-stu-id="b0445-198">This is hello IP address of hello domain controller server.</span></span> <span data-ttu-id="b0445-199">Deze parameter is vereist tooenable Hallo nieuwe virtuele machines in Hallo cloud service toojoin toohello Active Directory-domein is.</span><span class="sxs-lookup"><span data-stu-id="b0445-199">This parameter is needed tooenable hello new VMs in hello cloud service toojoin toohello Active Directory domain successfully.</span></span> <span data-ttu-id="b0445-200">Deze parameter niet opgeeft, moet u handmatig instellen Hallo IPv4-instellingen in uw VM toouse Hallo domain controller-server als het primaire DNS-server Hallo nadat Hallo VM is ingericht en meldt u zich Hallo VM toohello Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="b0445-200">Without this parameter, you must manually set hello IPv4 settings in your VM toouse hello domain controller server as hello primary DNS server after hello VM is provisioned, and then join hello VM toohello Active Directory domain.</span></span>
3. <span data-ttu-id="b0445-201">Voer Hallo na doorgesluisd opdrachten toocreate Hallo SQL Server-VM's met de naam **ContosoSQL1** en **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="b0445-201">Run hello following piped commands toocreate hello SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    <span data-ttu-id="b0445-202">Let op Hallo volgende met betrekking tot de bovenstaande Hallo-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="b0445-202">Note hello following regarding hello commands above:</span></span>

   * <span data-ttu-id="b0445-203">**Nieuwe AzureVMConfig** gebruikt dezelfde naam van de beschikbaarheidsset als domeincontrollerserver Hallo Hallo en maakt gebruik van SQL Server 2012 Service Pack 1 Enterprise Edition-installatiekopie in de galerie met virtuele machines Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0445-203">**New-AzureVMConfig** uses hello same availability set name as hello domain controller server, and uses hello SQL Server 2012 Service Pack 1 Enterprise Edition image in hello virtual machine gallery.</span></span> <span data-ttu-id="b0445-204">Hallo operationele systeem tooread-schijfcache alleen (geen schrijfcache) wordt ook ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b0445-204">It also sets hello operating system disk tooread-caching only (no write caching).</span></span> <span data-ttu-id="b0445-205">U wordt aangeraden Hallo database bestanden tooa afzonderlijke gegevensschijf u koppelen toohello VM, en deze configureren met niet lezen of schrijfcache te migreren.</span><span class="sxs-lookup"><span data-stu-id="b0445-205">We recommend that you migrate hello database files tooa separate data disk that you attach toohello VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="b0445-206">De volgende beste Hallo is echter tooremove schrijfcache op Hallo besturingssysteemschijf omdat u niet verwijderen lezen cachegebruik op schijf Hallo-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="b0445-206">However, hello next best thing is tooremove write caching on hello operating system disk because you can't remove read caching on hello operating system disk.</span></span>
   * <span data-ttu-id="b0445-207">**Voeg AzureProvisioningConfig** joins Hallo VM toohello Active Directory-domein dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b0445-207">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="b0445-208">**Set-AzureSubnet** plaatsen Hallo VM in Hallo back-subnet.</span><span class="sxs-lookup"><span data-stu-id="b0445-208">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="b0445-209">**Voeg AzureEndpoint** toegang eindpunten toegevoegd zodat clienttoepassingen toegang deze services-exemplaren van SQL Server op Hallo Internet tot.</span><span class="sxs-lookup"><span data-stu-id="b0445-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on hello Internet.</span></span> <span data-ttu-id="b0445-210">Er zijn verschillende poorten opgegeven tooContosoSQL1 en ContosoSQL2.</span><span class="sxs-lookup"><span data-stu-id="b0445-210">Different ports are given tooContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="b0445-211">**Nieuwe AzureVM** maakt nieuwe SQL Server VM Hallo in Hallo dezelfde cloudservice als ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="b0445-211">**New-AzureVM** creates hello new SQL Server VM in hello same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="b0445-212">U moet Hallo VMs plaatsen in dezelfde cloudservice als u deze wilt toobe in Hallo Hallo dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="b0445-212">You must place hello VMs in hello same cloud service if you want them toobe in hello same availability set.</span></span>
4. <span data-ttu-id="b0445-213">Wacht voor elke VM toobe volledig is ingericht en voor elke VM toodownload werkmap tooyour extern bureaublad-bestand.</span><span class="sxs-lookup"><span data-stu-id="b0445-213">Wait for each VM toobe fully provisioned and for each VM toodownload its remote desktop file tooyour working directory.</span></span> <span data-ttu-id="b0445-214">Hallo `for` lus Hallo doorlopen met drie nieuwe virtuele machines en voert Hallo-opdrachten binnen het hoogste niveau accolades Hallo voor elk van deze.</span><span class="sxs-lookup"><span data-stu-id="b0445-214">hello `for` loop cycles through hello three new VMs and executes hello commands inside hello top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    <span data-ttu-id="b0445-215">Hallo SQL Server-VM's nu zijn ingericht en wordt uitgevoerd, maar ze zijn geïnstalleerd met SQL Server met de standaardopties.</span><span class="sxs-lookup"><span data-stu-id="b0445-215">hello SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-hello-failover-cluster-vms"></a><span data-ttu-id="b0445-216">Hallo failover-cluster virtuele machines te initialiseren</span><span class="sxs-lookup"><span data-stu-id="b0445-216">Initialize hello failover cluster VMs</span></span>
<span data-ttu-id="b0445-217">In deze sectie moet u toomodify Hallo drie servers die u in Hallo failover-cluster en Hallo SQL Server-installatie gebruiken gaat.</span><span class="sxs-lookup"><span data-stu-id="b0445-217">In this section, you need toomodify hello three servers that you'll use in hello failover cluster and hello SQL Server installation.</span></span> <span data-ttu-id="b0445-218">Specifiek:</span><span class="sxs-lookup"><span data-stu-id="b0445-218">Specifically:</span></span>

* <span data-ttu-id="b0445-219">Alle servers: U moet tooinstall hello **Failoverclustering** functie.</span><span class="sxs-lookup"><span data-stu-id="b0445-219">All servers: You need tooinstall hello **Failover Clustering** feature.</span></span>
* <span data-ttu-id="b0445-220">Alle servers: U moet tooadd **CORP\Install** als Hallo machine **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="b0445-220">All servers: You need tooadd **CORP\Install** as hello machine **administrator**.</span></span>
* <span data-ttu-id="b0445-221">ContosoSQL1 en alleen ContosoSQL2: U moet tooadd **CORP\Install** als een **sysadmin** rol in de standaarddatabase Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0445-221">ContosoSQL1 and ContosoSQL2 only: You need tooadd **CORP\Install** as a **sysadmin** role in hello default database.</span></span>
* <span data-ttu-id="b0445-222">ContosoSQL1 en alleen ContosoSQL2: U moet tooadd **NT AUTHORITY\System** als iemand zich aanmeldt met Hallo volgende machtigingen:</span><span class="sxs-lookup"><span data-stu-id="b0445-222">ContosoSQL1 and ContosoSQL2 only: You need tooadd **NT AUTHORITY\System** as a sign-in with hello following permissions:</span></span>

  * <span data-ttu-id="b0445-223">Wijzigen van een beschikbaarheidsgroep</span><span class="sxs-lookup"><span data-stu-id="b0445-223">Alter any availability group</span></span>
  * <span data-ttu-id="b0445-224">Verbinding maken met SQL</span><span class="sxs-lookup"><span data-stu-id="b0445-224">Connect SQL</span></span>
  * <span data-ttu-id="b0445-225">Status van de server weergeven</span><span class="sxs-lookup"><span data-stu-id="b0445-225">View server state</span></span>
* <span data-ttu-id="b0445-226">ContosoSQL1 en ContosoSQL2 alleen: Hallo **TCP** protocol is al ingeschakeld op Hallo van SQL Server-VM.</span><span class="sxs-lookup"><span data-stu-id="b0445-226">ContosoSQL1 and ContosoSQL2 only: hello **TCP** protocol is already enabled on hello SQL Server VM.</span></span> <span data-ttu-id="b0445-227">U moet echter nog steeds tooopen Hallo firewall voor externe toegang van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b0445-227">However, you still need tooopen hello firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="b0445-228">U bent nu klaar toostart.</span><span class="sxs-lookup"><span data-stu-id="b0445-228">Now, you're ready toostart.</span></span> <span data-ttu-id="b0445-229">Beginnen met **ContosoQuorum**, volgt u onderstaande Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="b0445-229">Beginning with **ContosoQuorum**, follow hello steps below:</span></span>

1. <span data-ttu-id="b0445-230">Verbinding te maken met**ContosoQuorum** door Hallo extern bureaublad-bestanden.</span><span class="sxs-lookup"><span data-stu-id="b0445-230">Connect too**ContosoQuorum** by launching hello remote desktop files.</span></span> <span data-ttu-id="b0445-231">Gebruik Hallo machine beheerder gebruikersnaam **AzureAdmin** en het wachtwoord **Contoso! 000**, die u hebt opgegeven tijdens het maken van virtuele machines Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0445-231">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="b0445-232">Controleer of dat Hallo computers hebt toegevoegd te**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b0445-232">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="b0445-233">Wachten op Hallo SQL Server-installatie toofinish actieve Hallo automatische initialisatietaken voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="b0445-233">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="b0445-234">Open een PowerShell-venster in de beheerdersmodus.</span><span class="sxs-lookup"><span data-stu-id="b0445-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="b0445-235">Hallo Windows Failover Clustering installeren.</span><span class="sxs-lookup"><span data-stu-id="b0445-235">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="b0445-236">Voeg **CORP\Install** als een lokale beheerder.</span><span class="sxs-lookup"><span data-stu-id="b0445-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="b0445-237">Afmelden bij ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="b0445-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="b0445-238">U bent nu klaar met deze server.</span><span class="sxs-lookup"><span data-stu-id="b0445-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="b0445-239">Vervolgens initialiseren **ContosoSQL1** en **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="b0445-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="b0445-240">Volgende stappen uit hello, die identiek voor beide VM's van SQL Server zijn.</span><span class="sxs-lookup"><span data-stu-id="b0445-240">Follow hello steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="b0445-241">Verbinding met het maken van VM's toohello twee SQL Server door Hallo extern bureaublad-bestanden.</span><span class="sxs-lookup"><span data-stu-id="b0445-241">Connect toohello two SQL Server VMs by launching hello remote desktop files.</span></span> <span data-ttu-id="b0445-242">Gebruik Hallo machine beheerder gebruikersnaam **AzureAdmin** en het wachtwoord **Contoso! 000**, die u hebt opgegeven tijdens het maken van virtuele machines Hallo.</span><span class="sxs-lookup"><span data-stu-id="b0445-242">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="b0445-243">Controleer of dat Hallo computers hebt toegevoegd te**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b0445-243">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="b0445-244">Wachten op Hallo SQL Server-installatie toofinish actieve Hallo automatische initialisatietaken voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="b0445-244">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="b0445-245">Open een PowerShell-venster in de beheerdersmodus.</span><span class="sxs-lookup"><span data-stu-id="b0445-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="b0445-246">Hallo Windows Failover Clustering installeren.</span><span class="sxs-lookup"><span data-stu-id="b0445-246">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="b0445-247">Voeg **CORP\Install** als een lokale beheerder.</span><span class="sxs-lookup"><span data-stu-id="b0445-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="b0445-248">Hallo PowerShell-Provider voor SQL Server worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="b0445-248">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="b0445-249">Voeg **CORP\Install** als Hallo sysadmin-rol voor Hallo standaard SQL Server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b0445-249">Add **CORP\Install** as hello sysadmin role for hello default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="b0445-250">Voeg **NT AUTHORITY\System** als iemand zich aanmeldt met Hallo drie machtigingen die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="b0445-250">Add **NT AUTHORITY\System** as a sign-in with hello three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="b0445-251">Hallo firewall voor externe toegang van SQL Server openen.</span><span class="sxs-lookup"><span data-stu-id="b0445-251">Open hello firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="b0445-252">Afmelden bij beide virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b0445-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="b0445-253">Ten slotte, bent u klaar tooconfigure Hallo-beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="b0445-253">Finally, you're ready tooconfigure hello availability group.</span></span> <span data-ttu-id="b0445-254">U Hallo PowerShell-Provider voor SQL Server tooperform werkt met alle Hallo **ContosoSQL1**.</span><span class="sxs-lookup"><span data-stu-id="b0445-254">You'll use hello SQL Server PowerShell Provider tooperform all of hello work on **ContosoSQL1**.</span></span>

## <a name="configure-hello-availability-group"></a><span data-ttu-id="b0445-255">Hallo-beschikbaarheidsgroep configureren</span><span class="sxs-lookup"><span data-stu-id="b0445-255">Configure hello availability group</span></span>
1. <span data-ttu-id="b0445-256">Verbinding te maken met**ContosoSQL1** opnieuw door het Hallo-bestanden voor extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="b0445-256">Connect too**ContosoSQL1** again by launching hello remote desktop files.</span></span> <span data-ttu-id="b0445-257">In plaats van via Hallo machineaccount aanmeldt, moet u zich aanmelden via **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="b0445-257">Instead of signing in by using hello machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="b0445-258">Open een PowerShell-venster in de beheerdersmodus.</span><span class="sxs-lookup"><span data-stu-id="b0445-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="b0445-259">Definieer Hallo variabelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b0445-259">Define hello following variables:</span></span>

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. <span data-ttu-id="b0445-260">Hallo PowerShell-Provider voor SQL Server worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="b0445-260">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="b0445-261">Hallo SQL Server-serviceaccount voor ContosoSQL1 tooCORP\SQLSvc1 wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b0445-261">Change hello SQL Server service account for ContosoSQL1 tooCORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="b0445-262">Hallo SQL Server-serviceaccount voor ContosoSQL2 tooCORP\SQLSvc2 wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b0445-262">Change hello SQL Server service account for ContosoSQL2 tooCORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="b0445-263">Download **CreateAzureFailoverCluster.ps1** van [failovercluster maken voor AlwaysOn-beschikbaarheidsgroepen in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello lokale werkmap.</span><span class="sxs-lookup"><span data-stu-id="b0445-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello local working directory.</span></span> <span data-ttu-id="b0445-264">U gebruikt dit script toohelp maken van een functionele failover-cluster.</span><span class="sxs-lookup"><span data-stu-id="b0445-264">You'll use this script toohelp you create a functional failover cluster.</span></span> <span data-ttu-id="b0445-265">Netwerk voor belangrijke informatie over hoe Windows Failover Clustering met hello Azure samenwerkt, Zie [hoge beschikbaarheid en herstel na noodgevallen voor SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0445-265">For important information on how Windows Failover Clustering interacts with hello Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="b0445-266">Wijzig tooyour werkmap en Hallo failover-cluster maken met een script Hallo gedownload.</span><span class="sxs-lookup"><span data-stu-id="b0445-266">Change tooyour working directory and create hello failover cluster with hello downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="b0445-267">Schakel AlwaysOn-beschikbaarheidsgroepen voor Hallo standaard SQL Server-exemplaren op **ContosoSQL1** en **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="b0445-267">Enable Always On availability groups for hello default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. <span data-ttu-id="b0445-268">Maak een back-map en machtigingen voor Hallo SQL Server-serviceaccounts.</span><span class="sxs-lookup"><span data-stu-id="b0445-268">Create a backup directory and grant permissions for hello SQL Server service accounts.</span></span> <span data-ttu-id="b0445-269">U gebruikt deze beschikbaarheidsdatabase directory tooprepare Hallo op Hallo secundaire replica.</span><span class="sxs-lookup"><span data-stu-id="b0445-269">You'll use this directory tooprepare hello availability database on hello secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="b0445-270">Een database maakt op **ContosoSQL1** aangeroepen **MyDB1**, Neem zowel een volledige back-up als een logboekback-up en herstel deze op **ContosoSQL2** Hello **WITH NORECOVERY** optie.</span><span class="sxs-lookup"><span data-stu-id="b0445-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with hello **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="b0445-271">Hallo beschikbaarheid groep eindpunten maken op Hallo VM's van SQL Server en de juiste machtigingen Hallo op Hallo-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="b0445-271">Create hello availability group endpoints on hello SQL Server VMs and set hello proper permissions on hello endpoints.</span></span>

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. <span data-ttu-id="b0445-272">Hallo beschikbaarheidsreplica's maken.</span><span class="sxs-lookup"><span data-stu-id="b0445-272">Create hello availability replicas.</span></span>

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. <span data-ttu-id="b0445-273">Maak ten slotte Hallo beschikbaarheidsgroep en join Hallo secundaire replica toohello-beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="b0445-273">Finally, create hello availability group and join hello secondary replica toohello availability group.</span></span>

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a><span data-ttu-id="b0445-274">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b0445-274">Next steps</span></span>
<span data-ttu-id="b0445-275">U hebt nu geïmplementeerd SQL Server Always On door het maken van een beschikbaarheidsgroep in Azure.</span><span class="sxs-lookup"><span data-stu-id="b0445-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="b0445-276">Zie een listener voor deze beschikbaarheidsgroep tooconfigure [een ILB-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="b0445-276">tooconfigure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="b0445-277">Zie voor meer informatie over het gebruik van SQL Server in Azure, [SQL Server op virtuele machines in Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b0445-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
