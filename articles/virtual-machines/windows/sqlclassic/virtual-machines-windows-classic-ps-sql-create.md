---
title: aaaCreate een SQL Server-Machine in Azure PowerShell (klassiek) | Microsoft Docs
description: "Bevat de stappen en PowerShell-scripts voor het maken van een virtuele machine in Azure met SQL Server-installatiekopieën voor virtuele machine-galerie. In dit onderwerp maakt gebruik van de klassieke implementatiemodus Hallo."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="661f8-104">Een SQL Server-machine met Azure PowerShell (klassiek) inrichten</span><span class="sxs-lookup"><span data-stu-id="661f8-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="661f8-105">In dit artikel bevat stappen voor hoe toocreate een SQL Server virtuele machine in Azure met behulp van PowerShell-cmdlets Hallo.</span><span class="sxs-lookup"><span data-stu-id="661f8-105">This article provides steps for how toocreate a SQL Server virtual machine in Azure by using hello PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="661f8-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="661f8-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="661f8-107">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="661f8-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="661f8-108">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="661f8-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="661f8-109">Zie voor Hallo Resource Manager-versie van dit onderwerp [een met Azure PowerShell-Resource Manager van SQL Server-machine inrichten](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="661f8-109">For hello Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="661f8-110">PowerShell installeren en configureren:</span><span class="sxs-lookup"><span data-stu-id="661f8-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="661f8-111">Als u geen Azure-account hebt, gaat u naar [Azure, gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="661f8-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="661f8-112">[Download en installeer de nieuwste Azure PowerShell-opdrachten Hallo](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="661f8-112">[Download and install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="661f8-113">Start Windows PowerShell en tooyour Azure-abonnement verbinden met de Hallo **Add-AzureAccount** opdracht.</span><span class="sxs-lookup"><span data-stu-id="661f8-113">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="661f8-114">Het doel-Azure-regio bepalen</span><span class="sxs-lookup"><span data-stu-id="661f8-114">Determine your target Azure region</span></span>

<span data-ttu-id="661f8-115">Uw virtuele Machine van SQL Server zal worden gehost in een cloudservice die een specifieke Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="661f8-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="661f8-116">Hallo volgende stappen kunt u toodetermine uw regio, de storage-account en de cloudservice, die wordt gebruikt voor de rest van de zelfstudie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="661f8-116">hello following steps help you toodetermine your region, storage account, and cloud service that will be used for hello rest of hello tutorial.</span></span>

1. <span data-ttu-id="661f8-117">Hallo datacenter dat u wilt dat toouse toohost uw SQL Server VM bepalen.</span><span class="sxs-lookup"><span data-stu-id="661f8-117">Determine hello data center that you want toouse toohost your SQL Server VM.</span></span> <span data-ttu-id="661f8-118">Hallo volgende PowerShell-opdracht geeft een lijst van beschikbare regionamen.</span><span class="sxs-lookup"><span data-stu-id="661f8-118">hello following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="661f8-119">Zodra u de gewenste locatie hebt geïdentificeerd, instellen van een variabele met de naam **$dcLocation** toothat regio.</span><span class="sxs-lookup"><span data-stu-id="661f8-119">Once you've identified your preferred location, set a variable named **$dcLocation** toothat region.</span></span> <span data-ttu-id="661f8-120">Bijvoorbeeld, Hallo opdracht sets Hallo regio te volgen 'VS-Oost':</span><span class="sxs-lookup"><span data-stu-id="661f8-120">For example, hello following command sets hello region too"East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="661f8-121">Uw abonnement en storage-account instellen</span><span class="sxs-lookup"><span data-stu-id="661f8-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="661f8-122">Hello Azure-abonnement u voor de nieuwe virtuele machine Hallo gebruiken wilt bepalen.</span><span class="sxs-lookup"><span data-stu-id="661f8-122">Determine hello Azure subscription you will use for hello new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="661f8-123">Toewijzen van uw Azure-abonnement doel toohello **$subscr** variabele.</span><span class="sxs-lookup"><span data-stu-id="661f8-123">Assign your target Azure subscription toohello **$subscr** variable.</span></span> <span data-ttu-id="661f8-124">Dit wordt ingesteld als uw huidige Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="661f8-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="661f8-125">Vervolgens kunt u controleren op bestaande opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="661f8-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="661f8-126">Hallo geeft volgende script alle opslagaccounts die zijn opgenomen in uw gekozen regio:</span><span class="sxs-lookup"><span data-stu-id="661f8-126">hello following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="661f8-127">Als u een nieuw opslagaccount vereist, moet u eerst een opslagaccountnaam alle kleine maken met de opdracht zoals in het volgende voorbeeld Hallo Hallo nieuw AzureStorageAccount:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="661f8-127">If you require a new storage account, first create an all-lower-case storage account name with hello New-AzureStorageAccount command as in hello following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="661f8-128">Hallo doel storage account name toohello toewijzen **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="661f8-128">Assign hello target storage account name toohello **$staccount**.</span></span> <span data-ttu-id="661f8-129">Gebruik vervolgens **Set-AzureSubscription** tooset Hallo abonnement en de huidige opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="661f8-129">Then use **Set-AzureSubscription** tooset hello subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="661f8-130">Selecteer de installatiekopie van een SQL Server-virtuele machine</span><span class="sxs-lookup"><span data-stu-id="661f8-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="661f8-131">Ontdek Hallo lijst met beschikbare virtuele machines van SQL Server-installatiekopieën uit Hallo galerie.</span><span class="sxs-lookup"><span data-stu-id="661f8-131">Find out hello list of available SQL Server virtual machines images from hello gallery.</span></span> <span data-ttu-id="661f8-132">Deze installatiekopieën alle hebben een **ImageFamily** eigenschap die met 'SQL begint'.</span><span class="sxs-lookup"><span data-stu-id="661f8-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="661f8-133">Hallo volgende query geeft Hallo installatiekopie familie beschikbaar tooyou die SQL Server vooraf geïnstalleerd hebben.</span><span class="sxs-lookup"><span data-stu-id="661f8-133">hello following query displays hello image family available tooyou that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="661f8-134">Wanneer u Hallo virtuele machine installatiekopie familie gevonden, kan dit worden veroorzaakt door meerdere gepubliceerde afbeeldingen in deze familie.</span><span class="sxs-lookup"><span data-stu-id="661f8-134">When you find hello  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="661f8-135">Gebruik Hallo volgende script toofind Hallo nieuwste gepubliceerde naam virtuele machine-installatiekopie voor de geselecteerde installatiekopie-familie (zoals **RTM Enterprise van SQL Server 2016 op Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="661f8-135">Use hello following script toofind hello latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a><span data-ttu-id="661f8-136">Hallo virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="661f8-136">Create hello virtual machine</span></span>

<span data-ttu-id="661f8-137">Maak ten slotte Hallo virtuele machine met PowerShell:</span><span class="sxs-lookup"><span data-stu-id="661f8-137">Finally, create hello virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="661f8-138">Maak een cloud service toohost Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="661f8-138">Create a cloud service toohost hello new VM.</span></span> <span data-ttu-id="661f8-139">Houd er rekening mee dat het is ook mogelijk toouse een bestaande cloudservice in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="661f8-139">Note that it is also possible toouse an existing cloud service instead.</span></span> <span data-ttu-id="661f8-140">Maak een nieuwe variabele **$svcname** met korte naam van de cloudservice Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="661f8-140">Create a new variable **$svcname** with hello short name of hello cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="661f8-141">Naam van de virtuele machine Hallo en een grootte opgeven.</span><span class="sxs-lookup"><span data-stu-id="661f8-141">Specify hello virtual machine name and a size.</span></span> <span data-ttu-id="661f8-142">Zie voor meer informatie over de grootte van virtuele machines, [grootten van virtuele machines voor Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="661f8-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="661f8-143">Hallo lokale administrator-account en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="661f8-143">Specify hello local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="661f8-144">Hallo na script toocreate Hallo virtuele machine worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="661f8-144">Run hello following script toocreate hello virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="661f8-145">Zie voor aanvullende uitleg en configuratieopties Hallo **bouwen van uw opdrachtset** in sectie [toocreate gebruik Azure PowerShell en vooraf configureren van virtuele Machines op basis van Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="661f8-145">For additional explanation and configuration options, see hello **Build your command set** section in [Use Azure PowerShell toocreate and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="661f8-146">Voorbeeld van de PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="661f8-146">Example PowerShell script</span></span>

<span data-ttu-id="661f8-147">Hallo volgende script toont een voorbeeld van een volledige-script maakt een **RTM Enterprise van SQL Server 2016 op Windows Server 2012 R2** virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="661f8-147">hello following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="661f8-148">Als u dit script gebruikt, moet u de initiële Hallo-variabelen op basis van de vorige stappen in dit onderwerp Hallo aanpassen.</span><span class="sxs-lookup"><span data-stu-id="661f8-148">If you use this script, you must customize hello initial variables based on hello previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="661f8-149">Verbinding maken met extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="661f8-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="661f8-150">Hallo RDP-bestanden op Hallo van de huidige gebruiker document map toolaunch deze toocomplete-setup van virtuele machines maken:</span><span class="sxs-lookup"><span data-stu-id="661f8-150">Create hello RDP files in hello current user's document folder toolaunch these virtual machines toocomplete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="661f8-151">Start in de map documenten van Hallo Hallo RDP-bestand.</span><span class="sxs-lookup"><span data-stu-id="661f8-151">In hello documents directory, launch hello RDP file.</span></span> <span data-ttu-id="661f8-152">Verbinding maken met de Hallo beheerdersgebruikersnaam en wachtwoord die eerder is verkregen (bijvoorbeeld, als uw gebruikersnaam VMAdmin, '\VMAdmin' opgeven als de gebruiker Hallo en Hallo wachtwoord opgeven).</span><span class="sxs-lookup"><span data-stu-id="661f8-152">Connect with hello administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as hello user and provide hello password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a><span data-ttu-id="661f8-153">Configuratie voltooid Hallo Hallo Machine van SQL Server voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="661f8-153">Complete hello configuration of hello SQL Server Machine for remote access</span></span>

<span data-ttu-id="661f8-154">Na aanmelding toohello machine via Extern bureaublad configureren van SQL Server op basis van de instructies in Hallo [stappen voor het configureren van SQL-serververbindingen in een Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="661f8-154">After logging on toohello machine with remote desktop, configure SQL Server based on hello instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="661f8-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="661f8-155">Next steps</span></span>

<span data-ttu-id="661f8-156">U vindt aanvullende instructies voor het inrichten van virtuele machines met PowerShell in Hallo [documentatie virtual machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="661f8-156">You can find additional instructions for provisioning virtual machines with PowerShell in hello [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="661f8-157">In veel gevallen is de volgende stap Hallo toomigrate uw databases toothis nieuwe virtuele machine voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="661f8-157">In many cases, hello next step is toomigrate your databases toothis new SQL Server VM.</span></span> <span data-ttu-id="661f8-158">Zie voor instructies voor het migreren van database [migreren van een Database tooSQL Server op een Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="661f8-158">For database migration guidance, see [Migrating a Database tooSQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="661f8-159">Als u ook geïnteresseerd bent in met behulp van hello Azure portal toocreate virtuele Machines van SQL, raadpleegt u [inrichten van een virtuele Machine van SQL Server op Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="661f8-159">If you're also interested in using hello Azure portal toocreate SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="661f8-160">Houd er rekening mee dat Hallo-zelfstudie dat helpt die u bij het Hallo-portal maakt virtuele machines met Hallo aanbevolen Resource Manager-model, in plaats van klassieke Hallo-model in dit onderwerp PowerShell gebruikt.</span><span class="sxs-lookup"><span data-stu-id="661f8-160">Note that hello tutorial that walks you through hello portal creates VMs using hello recommended Resource Manager model, rather than hello classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="661f8-161">Bovendien toothese resources, wordt aangeraden te controleren [andere onderwerpen gerelateerde toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="661f8-161">In addition toothese resources, we recommend that you review [other topics related toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
