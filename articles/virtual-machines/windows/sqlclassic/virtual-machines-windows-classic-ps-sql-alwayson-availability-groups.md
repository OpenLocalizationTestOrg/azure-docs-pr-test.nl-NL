---
title: De AlwaysOn-beschikbaarheidsgroep configureren op een virtuele machine in Azure met behulp van PowerShell | Microsoft Docs
description: Deze zelfstudie maakt gebruik van bronnen die zijn gemaakt met het klassieke implementatiemodel. PowerShell kunt u een AlwaysOn-beschikbaarheidsgroep maken in Azure.
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
ms.openlocfilehash: b99cf767fb931d3f7fe14fcbe7990126244613ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="fa6a2-104">De AlwaysOn-beschikbaarheidsgroep configureren op een virtuele machine in Azure met PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa6a2-104">Configure the Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa6a2-105">Klassieke: UI</span><span class="sxs-lookup"><span data-stu-id="fa6a2-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="fa6a2-106">[Klassieke: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="fa6a2-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="fa6a2-107">Voordat u begint, kunt u overwegen of u kunt deze taak in Azure resource manager-model voltooien.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="fa6a2-108">U wordt aangeraden Azure resource manager-model voor nieuwe implementaties.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="fa6a2-109">Zie [op virtuele machines in Azure SQL Server altijd op beschikbaarheidsgroepen](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fa6a2-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa6a2-110">U wordt aangeraden de meeste nieuwe implementaties het Resource Manager-model gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-110">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="fa6a2-111">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fa6a2-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fa6a2-112">Dit artikel gaat over het gebruik van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-112">This article covers using the classic deployment model.</span></span>

<span data-ttu-id="fa6a2-113">Azure virtuele machines (VM's) kunt databasebeheerders verlagen de kosten van een SQL Server-systeem voor hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-113">Azure virtual machines (VMs) can help database administrators to lower the cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="fa6a2-114">Deze zelfstudie laat zien hoe u een beschikbaarheidsgroep implementeert met behulp van SQL Server Always On end-to-end binnen een Azure-omgeving.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-114">This tutorial shows you how to implement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="fa6a2-115">Uw oplossing SQL Server Always On in Azure wordt aan het einde van de zelfstudie bestaat uit de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-115">At the end of the tutorial, your SQL Server Always On solution in Azure will consist of the following elements:</span></span>

* <span data-ttu-id="fa6a2-116">Een virtueel netwerk met meerdere subnetten, met inbegrip van een front-end- en een back-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="fa6a2-117">Een domeincontroller met een Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="fa6a2-118">Twee SQL Server-VM's die zijn geïmplementeerd met het subnet voor back-end en toegevoegd aan het Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-118">Two SQL Server VMs that are deployed to the back-end subnet and joined to the Active Directory domain.</span></span>
* <span data-ttu-id="fa6a2-119">Een drie-knooppunt Windows failover-cluster met Knooppuntmeerderheid quorummodel.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-119">A three-node Windows failover cluster with the Node Majority quorum model.</span></span>
* <span data-ttu-id="fa6a2-120">Een beschikbaarheidsgroep met twee replica's voor synchrone doorvoer van een beschikbaarheidsdatabase.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="fa6a2-121">Dit scenario is een goede keuze voor de eenvoud op Azure, niet voor de kosteneffectiviteit of andere factoren.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="fa6a2-122">U kunt bijvoorbeeld het aantal virtuele machines voor een twee-replica van een beschikbaarheidsgroep op te slaan op rekenuren in Azure met behulp van de domeincontroller als de bestandssharewitness in quorum in een failovercluster met twee knooppunten minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-122">For example, you can minimize the number of VMs for a two-replica availability group to save on compute hours in Azure by using the domain controller as the quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="fa6a2-123">Deze methode wordt het aantal VM's met één van de bovenstaande configuratie verlaagd.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-123">This method reduces the VM count by one from the above configuration.</span></span>

<span data-ttu-id="fa6a2-124">Deze zelfstudie is bedoeld om u de stappen die nodig zijn voor het instellen van de beschreven oplossing hierboven, zonder de details van elke stap bespreekt weer te geven.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-124">This tutorial is intended to show you the steps that are required to set up the described solution above, without elaborating on the details of each step.</span></span> <span data-ttu-id="fa6a2-125">Daarom in plaats van het bieden van de GUI-configuratiestappen, gebruikt het PowerShell-scripts waarmee u snel via elke stap.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-125">Therefore, instead of providing the GUI configuration steps, it uses PowerShell scripting to take you quickly through each step.</span></span> <span data-ttu-id="fa6a2-126">Deze zelfstudie wordt ervan uitgegaan:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-126">This tutorial assumes the following:</span></span>

* <span data-ttu-id="fa6a2-127">U hebt al een Azure-account aan het abonnement van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-127">You already have an Azure account with the virtual machine subscription.</span></span>
* <span data-ttu-id="fa6a2-128">U hebt geïnstalleerd het [Azure PowerShell-cmdlets](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fa6a2-128">You've installed the [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="fa6a2-129">U hebt al een goed begrip van AlwaysOn-beschikbaarheidsgroepen voor oplossingen on-premises.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="fa6a2-130">Zie voor meer informatie [altijd op beschikbaarheidsgroepen (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa6a2-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-to-your-azure-subscription-and-create-the-virtual-network"></a><span data-ttu-id="fa6a2-131">Verbinding maken met uw Azure-abonnement en het virtuele netwerk maken</span><span class="sxs-lookup"><span data-stu-id="fa6a2-131">Connect to your Azure subscription and create the virtual network</span></span>
1. <span data-ttu-id="fa6a2-132">De Azure-module importeren in een PowerShell-venster op de lokale computer, downloaden van het bestand publicatie-instellingen naar uw computer en uw PowerShell-sessie verbinding met uw Azure-abonnement met het importeren van de gedownloade publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-132">In a PowerShell window on your local computer, import the Azure module, download the publishing settings file to your machine, and connect your PowerShell session to your Azure subscription by importing the downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="fa6a2-133">De **Get-AzurePublishSettingsFile** opdracht genereert u een beheercertificaat met Azure automatisch en downloadt u deze naar uw computer.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-133">The **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it to your machine.</span></span> <span data-ttu-id="fa6a2-134">Een browser wordt automatisch geopend en u wordt gevraagd de referenties van het Microsoft-account invoeren voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-134">A browser is automatically opened, and you're prompted to enter the Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="fa6a2-135">De gedownloade **.publishsettings** bestand bevat alle de informatie die u nodig voor het beheren van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-135">The downloaded **.publishsettings** file contains all the information that you need to manage your Azure subscription.</span></span> <span data-ttu-id="fa6a2-136">Na het opslaan van dit bestand naar een lokale map importeren met behulp van de **importeren AzurePublishSettingsFile** opdracht.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-136">After saving this file to a local directory, import it by using the **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fa6a2-137">Het .publishsettings-bestand bevat uw referenties (ongecodeerde) die worden gebruikt voor het beheren van uw Azure-abonnementen en services.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-137">The .publishsettings file contains your credentials (unencoded) that are used to administer your Azure subscriptions and services.</span></span> <span data-ttu-id="fa6a2-138">De aanbevolen beveiligingsprocedures voor dit bestand is tijdelijk buiten uw adreslijsten bron (bijvoorbeeld in de map Libraries\Documents) opslaan en vervolgens te verwijderen nadat het importeren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-138">The security best practice for this file is to store it temporarily outside your source directories (for example, in the Libraries\Documents folder), and then delete it after the import has finished.</span></span> <span data-ttu-id="fa6a2-139">Een kwaadwillende gebruiker die toegang tot de .publishsettings-bestand krijgt kunt bewerken, maken en verwijderen van uw Azure-services.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-139">A malicious user who gains access to the .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="fa6a2-140">Definieer een reeks variabelen die u gebruiken gaat voor het maken van uw cloud IT-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-140">Define a series of variables that you'll use to create your cloud IT infrastructure.</span></span>

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

    <span data-ttu-id="fa6a2-141">Let op het volgende om ervoor te zorgen dat uw opdrachten later slaagt:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-141">Pay attention to the following to ensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="fa6a2-142">Variabelen **$storageAccountName** en **$dcServiceName** moeten uniek zijn omdat deze worden gebruikt voor het identificeren van uw cloud-account en cloud opslagserver, respectievelijk op het Internet.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used to identify your cloud storage account and cloud server, respectively, on the Internet.</span></span>
   * <span data-ttu-id="fa6a2-143">De namen die u voor variabelen opgeeft **$affinityGroupName** en **$virtualNetworkName** zijn geconfigureerd in het configuratiebestand voor virtueel netwerk die u later gaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-143">The names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in the virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="fa6a2-144">**$sqlImageName** geeft de bijgewerkte naam van de VM-installatiekopie waarin SQL Server 2012 Service Pack 1 Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-144">**$sqlImageName** specifies the updated name of the VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="fa6a2-145">Voor het gemak, **Contoso! 000** is het wachtwoord dat wordt gebruikt in de hele zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-145">For simplicity, **Contoso!000** is the same password that's used throughout the entire tutorial.</span></span>

3. <span data-ttu-id="fa6a2-146">Maak een affiniteitsgroep.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="fa6a2-147">Een virtueel netwerk maken door een configuratiebestand te importeren.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="fa6a2-148">Het configuratiebestand bevat de volgende XML-document.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-148">The configuration file contains the following XML document.</span></span> <span data-ttu-id="fa6a2-149">Kort samengevat: Hiermee wordt een virtueel netwerk met de naam **ContosoNET** in de affiniteitsgroep aangeroepen **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-149">In brief, it specifies a virtual network called **ContosoNET** in the affinity group called **ContosoAG**.</span></span> <span data-ttu-id="fa6a2-150">Dit is de adresruimte **10.10.0.0/16** en heeft twee subnetten **10.10.1.0/24** en **10.10.2.0/24**, die de front-subnet en back-subnet, respectievelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-150">It has the address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are the front subnet and back subnet, respectively.</span></span> <span data-ttu-id="fa6a2-151">De front-subnet is waarin u de clienttoepassingen, zoals Microsoft SharePoint kunt plaatsen.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-151">The front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="fa6a2-152">Het back-subnet is plaats voegt u de VM's van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-152">The back subnet is where you'll place the SQL Server VMs.</span></span> <span data-ttu-id="fa6a2-153">Als u wijzigt de **$affinityGroupName** en **$virtualNetworkName** variabelen eerder, moet u ook de desbetreffende namen hieronder wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-153">If you change the **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change the corresponding names below.</span></span>

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

5. <span data-ttu-id="fa6a2-154">Maak een opslagaccount die is gekoppeld aan de affiniteitsgroep gemaakt en stel dit in als het huidige opslagaccount in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-154">Create a storage account that's associated with the affinity group that you created, and set it as the current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="fa6a2-155">Maak de domain controller-server in de nieuwe cloud-service en beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-155">Create the domain controller server in the new cloud service and availability set.</span></span>

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

    <span data-ttu-id="fa6a2-156">Deze piped opdrachten doen het volgende:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-156">These piped commands do the following things:</span></span>

   * <span data-ttu-id="fa6a2-157">**Nieuwe AzureVMConfig** maakt u een VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="fa6a2-158">**Voeg AzureProvisioningConfig** geeft de configuratieparameters van een zelfstandige Windows-server.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-158">**Add-AzureProvisioningConfig** gives the configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="fa6a2-159">**Voeg AzureDataDisk** voegt de gegevensschijf die u gebruiken gaat voor het opslaan van Active Directory-gegevens met de cache in optie is ingesteld op None.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-159">**Add-AzureDataDisk** adds the data disk that you'll use for storing Active Directory data, with the caching option set to None.</span></span>
   * <span data-ttu-id="fa6a2-160">**Nieuwe AzureVM** maakt een nieuwe cloudservice en maakt u de nieuwe Azure-virtuele machine in de nieuwe cloudservice.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-160">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span>

7. <span data-ttu-id="fa6a2-161">Wacht tot de nieuwe virtuele machine volledig is ingericht en download het externe bureaublad naar uw werkmap.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-161">Wait for the new VM to be fully provisioned, and download the remote desktop file to your working directory.</span></span> <span data-ttu-id="fa6a2-162">Omdat de nieuwe virtuele machine in Azure een lange tijd om in te richten duren, de `while` lus blijft voor het pollen van de nieuwe virtuele machine totdat deze klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-162">Because the new Azure VM takes a long time to provision, the `while` loop continues to poll the new VM until it's ready for use.</span></span>

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

<span data-ttu-id="fa6a2-163">De domain controller-server is nu is ingericht.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-163">The domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="fa6a2-164">Vervolgens configureert u het Active Directory-domein op deze domeincontrollerserver.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-164">Next, you'll configure the Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="fa6a2-165">Laat het PowerShell-venster geopend op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-165">Leave the PowerShell window open on your local computer.</span></span> <span data-ttu-id="fa6a2-166">U gaat deze later opnieuw gebruiken voor het maken van de twee SQL Server-VM's.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-166">You'll use it again later to create the two SQL Server VMs.</span></span>

## <a name="configure-the-domain-controller"></a><span data-ttu-id="fa6a2-167">De domeincontroller configureren</span><span class="sxs-lookup"><span data-stu-id="fa6a2-167">Configure the domain controller</span></span>
1. <span data-ttu-id="fa6a2-168">Verbinding maken met de domeincontrollerserver beschadigt door de extern bureaublad-bestand.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-168">Connect to the domain controller server by launching the remote desktop file.</span></span> <span data-ttu-id="fa6a2-169">Gebruik de gebruikersnaam AzureAdmin en het wachtwoord van de beheerder van de machine **Contoso! 000**, die u hebt opgegeven toen u de nieuwe virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-169">Use the machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created the new VM.</span></span>
2. <span data-ttu-id="fa6a2-170">Open een PowerShell-venster in de beheerdersmodus.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="fa6a2-171">Voer de volgende **DCPROMO. EXE** opdracht voor het instellen van de **corp.contoso.com** domein met de gegevensmappen op station M.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-171">Run the following **DCPROMO.EXE** command to set up the **corp.contoso.com** domain, with the data directories on drive M.</span></span>

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

    <span data-ttu-id="fa6a2-172">Nadat de opdracht is voltooid, wordt de virtuele machine automatisch opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-172">After the command finishes, the VM restarts automatically.</span></span>

4. <span data-ttu-id="fa6a2-173">Maakt verbinding met de domain controller-server opnieuw starten van de extern bureaublad-bestand.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-173">Connect to the domain controller server again by launching the remote desktop file.</span></span> <span data-ttu-id="fa6a2-174">Deze tijd, meld u aan als **CORP\Administrator**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="fa6a2-175">Open een PowerShell-venster in de beheerdersmodus en de Active Directory PowerShell-module importeren met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-175">Open a PowerShell window in administrator mode, and import the Active Directory PowerShell module by using the following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="fa6a2-176">Voer de volgende opdrachten drie gebruikers toevoegen aan het domein.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-176">Run the following commands to add three users to the domain.</span></span>

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

    <span data-ttu-id="fa6a2-177">**CORP\Install** wordt gebruikt voor het configureren van alles met betrekking tot de service-exemplaren van SQL Server, het failover-cluster en de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-177">**CORP\Install** is used to configure everything related to the SQL Server service instances, the failover cluster, and the availability group.</span></span> <span data-ttu-id="fa6a2-178">**CORP\SQLSvc1** en **CORP\SQLSvc2** worden gebruikt als de SQL Server-serviceaccounts voor de twee SQL Server-VM's.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as the SQL Server service accounts for the two SQL Server VMs.</span></span>
7. <span data-ttu-id="fa6a2-179">Voer vervolgens de volgende opdrachten om te geven **CORP\Install** de machtigingen voor het maken van computerobjecten in het domein.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-179">Next, run the following commands to give **CORP\Install** the permissions to create computer objects in the domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="fa6a2-180">De GUID die hierboven is opgegeven, is de GUID voor het objecttype van de computer.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-180">The GUID specified above is the GUID for the computer object type.</span></span> <span data-ttu-id="fa6a2-181">De **CORP\Install** account moet de **alle eigenschappen lezen** en **Computerobjecten maken** machtiging voor het maken van de actieve Direct objecten voor de failover-cluster.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-181">The **CORP\Install** account needs the **Read All Properties** and **Create Computer Objects** permission to create the Active Direct objects for the failover cluster.</span></span> <span data-ttu-id="fa6a2-182">De **alle eigenschappen lezen** machtiging is al toegewezen aan CORP\Install standaard, dus u hoeft niet expliciet verlenen.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-182">The **Read All Properties** permission is already given to CORP\Install by default, so you don't need to grant it explicitly.</span></span> <span data-ttu-id="fa6a2-183">Zie voor meer informatie over de machtigingen die nodig zijn voor het failovercluster maakt, [stapsgewijze handleiding voor Failover-Cluster: Accounts configureren in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa6a2-183">For more information on permissions that are needed to create the failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="fa6a2-184">Nu dat u klaar bent met het configureren van Active Directory en de gebruikersobjecten, u maakt twee SQL Server-VM's en voeg ze toe aan dit domein.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-184">Now that you've finished configuring Active Directory and the user objects, you'll create two SQL Server VMs and join them to this domain.</span></span>

## <a name="create-the-sql-server-vms"></a><span data-ttu-id="fa6a2-185">De VM's van SQL Server maken</span><span class="sxs-lookup"><span data-stu-id="fa6a2-185">Create the SQL Server VMs</span></span>
1. <span data-ttu-id="fa6a2-186">Blijven gebruiken van het PowerShell-venster is geopend op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-186">Continue to use the PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="fa6a2-187">De volgende aanvullende variabelen definiëren:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-187">Define the following additional variables:</span></span>

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

    <span data-ttu-id="fa6a2-188">Het IP-adres **10.10.0.4** is doorgaans toegewezen aan de eerste virtuele machine die u maakt in de **10.10.0.0/16** subnet van uw virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-188">The IP address **10.10.0.4** is typically assigned to the first VM that you create in the **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="fa6a2-189">U moet bevestigen dat dit het adres van uw domeincontrollerserver door te voeren **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-189">You should verify that this is the address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="fa6a2-190">Voer de volgende opdrachten voor het maken van de eerste virtuele machine in het failovercluster, met de naam doorgesluisd **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-190">Run the following piped commands to create the first VM in the failover cluster, named **ContosoQuorum**:</span></span>

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

    <span data-ttu-id="fa6a2-191">Houd rekening met het volgende met betrekking tot de bovenstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-191">Note the following regarding the command above:</span></span>

   * <span data-ttu-id="fa6a2-192">**Nieuwe AzureVMConfig** maakt u een VM-configuratie met de naam van de gewenste beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-192">**New-AzureVMConfig** creates a VM configuration with the desired availability set name.</span></span> <span data-ttu-id="fa6a2-193">De volgende virtuele machines wordt gemaakt met dezelfde naam van de beschikbaarheid zodat ze zijn gekoppeld aan dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-193">The subsequent VMs will be created with the same availability set name so that they're joined to the same availability set.</span></span>
   * <span data-ttu-id="fa6a2-194">**Voeg AzureProvisioningConfig** lid wordt van de virtuele machine aan Active Directory-domein dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-194">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="fa6a2-195">**Set-AzureSubnet** plaatst u de virtuele machine in het back-subnet.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-195">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="fa6a2-196">**Nieuwe AzureVM** maakt een nieuwe cloudservice en maakt u de nieuwe Azure-virtuele machine in de nieuwe cloudservice.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-196">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span> <span data-ttu-id="fa6a2-197">De **DnsSettings** parameter geeft u op dat de DNS-server voor de servers in de nieuwe cloudservice voor het IP-adres heeft **10.10.0.4**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-197">The **DnsSettings** parameter specifies that the DNS server for the servers in the new cloud service has the IP address **10.10.0.4**.</span></span> <span data-ttu-id="fa6a2-198">Dit is het IP-adres van de domain controller-server.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-198">This is the IP address of the domain controller server.</span></span> <span data-ttu-id="fa6a2-199">Deze parameter is vereist voor de nieuwe virtuele machines in de cloudservice om toe te voegen aan het Active Directory-domein is.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-199">This parameter is needed to enable the new VMs in the cloud service to join to the Active Directory domain successfully.</span></span> <span data-ttu-id="fa6a2-200">Deze parameter niet opgeeft, moet u handmatig de IPv4-instellingen instellen in uw VM voor gebruik van de domain controller-server als de primaire DNS-server nadat de virtuele machine is ingericht en vervolgens de virtuele machine toevoegen aan het Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-200">Without this parameter, you must manually set the IPv4 settings in your VM to use the domain controller server as the primary DNS server after the VM is provisioned, and then join the VM to the Active Directory domain.</span></span>
3. <span data-ttu-id="fa6a2-201">Voer de volgende opdrachten voor het maken van de SQL Server-VM's, met de naam doorgesluisd **ContosoSQL1** en **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-201">Run the following piped commands to create the SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

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

    <span data-ttu-id="fa6a2-202">Houd rekening met het volgende met betrekking tot de bovenstaande opdrachten:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-202">Note the following regarding the commands above:</span></span>

   * <span data-ttu-id="fa6a2-203">**Nieuwe AzureVMConfig** als de domain controller-server dezelfde naam van de beschikbaarheid, en de installatiekopie van het SQL Server 2012 Service Pack 1 Enterprise Edition gebruikt in de galerie met virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-203">**New-AzureVMConfig** uses the same availability set name as the domain controller server, and uses the SQL Server 2012 Service Pack 1 Enterprise Edition image in the virtual machine gallery.</span></span> <span data-ttu-id="fa6a2-204">Ook wordt de besturingssysteemschijf ingesteld op lees-caching alleen (geen schrijfcache).</span><span class="sxs-lookup"><span data-stu-id="fa6a2-204">It also sets the operating system disk to read-caching only (no write caching).</span></span> <span data-ttu-id="fa6a2-205">U wordt aangeraden de databasebestanden migreren naar een afzonderlijke schijf die u aan de virtuele machine koppelen en worden geconfigureerd met geen lees- of schrijfcache.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-205">We recommend that you migrate the database files to a separate data disk that you attach to the VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="fa6a2-206">Het volgende beste is echter verwijderen schrijfcache op de besturingssysteemschijf omdat de lees-caching op de schijf van het besturingssysteem kan niet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-206">However, the next best thing is to remove write caching on the operating system disk because you can't remove read caching on the operating system disk.</span></span>
   * <span data-ttu-id="fa6a2-207">**Voeg AzureProvisioningConfig** lid wordt van de virtuele machine aan Active Directory-domein dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-207">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="fa6a2-208">**Set-AzureSubnet** plaatst u de virtuele machine in het back-subnet.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-208">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="fa6a2-209">**Voeg AzureEndpoint** toegang eindpunten toegevoegd zodat clienttoepassingen toegang deze services-exemplaren van SQL Server op het Internet tot.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on the Internet.</span></span> <span data-ttu-id="fa6a2-210">Andere poorten worden besteed aan ContosoSQL1 en ContosoSQL2.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-210">Different ports are given to ContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="fa6a2-211">**Nieuwe AzureVM** maakt de nieuwe virtuele machine een SQL-Server in dezelfde cloudservice als ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-211">**New-AzureVM** creates the new SQL Server VM in the same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="fa6a2-212">Als u wilt dat ze zich in dezelfde beschikbaarheidsset, moet u de virtuele machines in dezelfde cloudservice plaatsen.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-212">You must place the VMs in the same cloud service if you want them to be in the same availability set.</span></span>
4. <span data-ttu-id="fa6a2-213">Wacht voor elke virtuele machine volledig is ingericht en voor elke virtuele machine de extern bureaublad-bestand te downloaden naar uw werkmap.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-213">Wait for each VM to be fully provisioned and for each VM to download its remote desktop file to your working directory.</span></span> <span data-ttu-id="fa6a2-214">De `for` lus doorlopen van de drie nieuwe virtuele machines en voert u de opdrachten binnen de site op het hoogste accolades voor elk van deze.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-214">The `for` loop cycles through the three new VMs and executes the commands inside the top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until the VM status is "ReadyRole"
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

    <span data-ttu-id="fa6a2-215">De SQL Server-VM's nu zijn ingericht en wordt uitgevoerd, maar ze zijn geïnstalleerd met SQL Server met de standaardopties.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-215">The SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-the-failover-cluster-vms"></a><span data-ttu-id="fa6a2-216">Initialiseren van het failover-cluster virtuele machines</span><span class="sxs-lookup"><span data-stu-id="fa6a2-216">Initialize the failover cluster VMs</span></span>
<span data-ttu-id="fa6a2-217">In deze sectie moet u de drie servers die u in het failovercluster en de installatie van SQL Server gebruiken gaat wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-217">In this section, you need to modify the three servers that you'll use in the failover cluster and the SQL Server installation.</span></span> <span data-ttu-id="fa6a2-218">Specifiek:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-218">Specifically:</span></span>

* <span data-ttu-id="fa6a2-219">Alle servers: U moet installeren de **Failoverclustering** functie.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-219">All servers: You need to install the **Failover Clustering** feature.</span></span>
* <span data-ttu-id="fa6a2-220">Alle servers: U moet toevoegen **CORP\Install** als de machine **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-220">All servers: You need to add **CORP\Install** as the machine **administrator**.</span></span>
* <span data-ttu-id="fa6a2-221">ContosoSQL1 en alleen ContosoSQL2: U moet toevoegen **CORP\Install** als een **sysadmin** rol in de standaarddatabase.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-221">ContosoSQL1 and ContosoSQL2 only: You need to add **CORP\Install** as a **sysadmin** role in the default database.</span></span>
* <span data-ttu-id="fa6a2-222">ContosoSQL1 en alleen ContosoSQL2: U moet toevoegen **NT AUTHORITY\System** als iemand zich aanmeldt met de volgende machtigingen:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-222">ContosoSQL1 and ContosoSQL2 only: You need to add **NT AUTHORITY\System** as a sign-in with the following permissions:</span></span>

  * <span data-ttu-id="fa6a2-223">Wijzigen van een beschikbaarheidsgroep</span><span class="sxs-lookup"><span data-stu-id="fa6a2-223">Alter any availability group</span></span>
  * <span data-ttu-id="fa6a2-224">Verbinding maken met SQL</span><span class="sxs-lookup"><span data-stu-id="fa6a2-224">Connect SQL</span></span>
  * <span data-ttu-id="fa6a2-225">Status van de server weergeven</span><span class="sxs-lookup"><span data-stu-id="fa6a2-225">View server state</span></span>
* <span data-ttu-id="fa6a2-226">ContosoSQL1 en alleen ContosoSQL2: de **TCP** protocol is al ingeschakeld op de virtuele machine van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-226">ContosoSQL1 and ContosoSQL2 only: The **TCP** protocol is already enabled on the SQL Server VM.</span></span> <span data-ttu-id="fa6a2-227">U moet nog steeds de firewall voor externe toegang van SQL Server te openen.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-227">However, you still need to open the firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="fa6a2-228">U bent nu klaar om te beginnen.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-228">Now, you're ready to start.</span></span> <span data-ttu-id="fa6a2-229">Beginnen met **ContosoQuorum**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-229">Beginning with **ContosoQuorum**, follow the steps below:</span></span>

1. <span data-ttu-id="fa6a2-230">Verbinding maken met **ContosoQuorum** door het starten van de extern bureaublad-bestanden.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-230">Connect to **ContosoQuorum** by launching the remote desktop files.</span></span> <span data-ttu-id="fa6a2-231">Gebruik de gebruikersnaam van de beheerder van de machine **AzureAdmin** en het wachtwoord **Contoso! 000**, die u hebt opgegeven tijdens het maken van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-231">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="fa6a2-232">Controleer of dat de computers met succes hebt toegevoegd aan **corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-232">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="fa6a2-233">Wacht tot de SQL Server-installatie te voltooien uitgevoerd van de van de geautomatiseerde initialisatietaken voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-233">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="fa6a2-234">Open een PowerShell-venster in de beheerdersmodus.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="fa6a2-235">Het onderdeel Windows Failover Clustering installeren.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-235">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="fa6a2-236">Voeg **CORP\Install** als een lokale beheerder.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="fa6a2-237">Afmelden bij ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="fa6a2-238">U bent nu klaar met deze server.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="fa6a2-239">Vervolgens initialiseren **ContosoSQL1** en **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="fa6a2-240">Volg de stappen hieronder, identiek voor beide VM's van SQL Server zijn.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-240">Follow the steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="fa6a2-241">Verbinding maken met de twee SQL Server-VM's met het starten van de extern bureaublad-bestanden.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-241">Connect to the two SQL Server VMs by launching the remote desktop files.</span></span> <span data-ttu-id="fa6a2-242">Gebruik de gebruikersnaam van de beheerder van de machine **AzureAdmin** en het wachtwoord **Contoso! 000**, die u hebt opgegeven tijdens het maken van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-242">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="fa6a2-243">Controleer of dat de computers met succes hebt toegevoegd aan **corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-243">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="fa6a2-244">Wacht tot de SQL Server-installatie te voltooien uitgevoerd van de van de geautomatiseerde initialisatietaken voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-244">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="fa6a2-245">Open een PowerShell-venster in de beheerdersmodus.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="fa6a2-246">Het onderdeel Windows Failover Clustering installeren.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-246">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="fa6a2-247">Voeg **CORP\Install** als een lokale beheerder.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="fa6a2-248">Importeer de PowerShell-Provider van de SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-248">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="fa6a2-249">Voeg **CORP\Install** als de rol sysadmin voor het standaardexemplaar van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-249">Add **CORP\Install** as the sysadmin role for the default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="fa6a2-250">Voeg **NT AUTHORITY\System** als iemand zich aanmeldt met de drie machtigingen die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-250">Add **NT AUTHORITY\System** as a sign-in with the three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="fa6a2-251">Open de firewall voor externe toegang van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-251">Open the firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="fa6a2-252">Afmelden bij beide virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="fa6a2-253">U kunt ten slotte de beschikbaarheidsgroep configureren.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-253">Finally, you're ready to configure the availability group.</span></span> <span data-ttu-id="fa6a2-254">U de SQL Server PowerShell-Provider voor het uitvoeren van al het werk op **ContosoSQL1**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-254">You'll use the SQL Server PowerShell Provider to perform all of the work on **ContosoSQL1**.</span></span>

## <a name="configure-the-availability-group"></a><span data-ttu-id="fa6a2-255">De beschikbaarheidsgroep configureren</span><span class="sxs-lookup"><span data-stu-id="fa6a2-255">Configure the availability group</span></span>
1. <span data-ttu-id="fa6a2-256">Verbinding maken met **ContosoSQL1** opnieuw door het starten van de extern bureaublad-bestanden.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-256">Connect to **ContosoSQL1** again by launching the remote desktop files.</span></span> <span data-ttu-id="fa6a2-257">In plaats van met de machineaccount aanmeldt, moet u zich aanmelden via **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-257">Instead of signing in by using the machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="fa6a2-258">Open een PowerShell-venster in de beheerdersmodus.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="fa6a2-259">Definieer de volgende variabelen:</span><span class="sxs-lookup"><span data-stu-id="fa6a2-259">Define the following variables:</span></span>

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
4. <span data-ttu-id="fa6a2-260">Importeer de PowerShell-Provider van de SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-260">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="fa6a2-261">De SQL Server-serviceaccount voor ContosoSQL1 om CORP\SQLSvc1 te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-261">Change the SQL Server service account for ContosoSQL1 to CORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="fa6a2-262">De SQL Server-serviceaccount voor ContosoSQL2 om CORP\SQLSvc2 te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-262">Change the SQL Server service account for ContosoSQL2 to CORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="fa6a2-263">Download **CreateAzureFailoverCluster.ps1** van [failovercluster maken voor AlwaysOn-beschikbaarheidsgroepen in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) naar de lokale werkmap.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) to the local working directory.</span></span> <span data-ttu-id="fa6a2-264">U hebt dit script gebruiken voor het maken van een functionele failover-cluster.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-264">You'll use this script to help you create a functional failover cluster.</span></span> <span data-ttu-id="fa6a2-265">Zie voor meer informatie over hoe Windows Failover Clustering met de Azure-netwerk samenwerkt [hoge beschikbaarheid en herstel na noodgevallen voor SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fa6a2-265">For important information on how Windows Failover Clustering interacts with the Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="fa6a2-266">Ga naar uw werkmap en het failovercluster maakt met het gedownloade script.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-266">Change to your working directory and create the failover cluster with the downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="fa6a2-267">Schakel AlwaysOn-beschikbaarheidsgroepen voor de standaard SQL Server-exemplaren op **ContosoSQL1** en **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-267">Enable Always On availability groups for the default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

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
10. <span data-ttu-id="fa6a2-268">Maak een back-map en machtigingen voor de SQL Server-serviceaccounts.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-268">Create a backup directory and grant permissions for the SQL Server service accounts.</span></span> <span data-ttu-id="fa6a2-269">U gebruikt deze map voor het voorbereiden van de beschikbaarheidsdatabase op de secundaire replica.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-269">You'll use this directory to prepare the availability database on the secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="fa6a2-270">Een database maakt op **ContosoSQL1** aangeroepen **MyDB1**, Neem zowel een volledige back-up als een logboekback-up en herstel deze op **ContosoSQL2** met de **WITH NORECOVERY**  optie.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with the **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="fa6a2-271">De beschikbaarheid van de groep eindpunten maken op de SQL Server-VM's en stel de juiste machtigingen op de eindpunten.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-271">Create the availability group endpoints on the SQL Server VMs and set the proper permissions on the endpoints.</span></span>

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
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct1]" -ServerInstance $server2
13. <span data-ttu-id="fa6a2-272">De beschikbaarheid van replica's maken.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-272">Create the availability replicas.</span></span>

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
14. <span data-ttu-id="fa6a2-273">Ten slotte de beschikbaarheidsgroep maken en de secundaire replica toevoegen aan de beschikbaarheidsgroep.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-273">Finally, create the availability group and join the secondary replica to the availability group.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fa6a2-274">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fa6a2-274">Next steps</span></span>
<span data-ttu-id="fa6a2-275">U hebt nu geïmplementeerd SQL Server Always On door het maken van een beschikbaarheidsgroep in Azure.</span><span class="sxs-lookup"><span data-stu-id="fa6a2-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="fa6a2-276">Zie voor het configureren van een listener voor deze beschikbaarheidsgroep [een ILB-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="fa6a2-276">To configure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="fa6a2-277">Zie voor meer informatie over het gebruik van SQL Server in Azure, [SQL Server op virtuele machines in Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fa6a2-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
