---
title: aaaCreate en beheren van een Azure virtuele Machine met behulp van C# | Microsoft Docs
description: Gebruik toodeploy C# en Azure Resource Manager een virtuele machine en de ondersteunende bronnen.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 8beeabde731bbaa25e68d2b9c5abbf71acbe377f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="2107a-103">Maken en beheren van Windows-machines in Azure met C#</span><span class="sxs-lookup"><span data-stu-id="2107a-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="2107a-104">Een [Azure virtuele Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) moet meerdere ondersteunende Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="2107a-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="2107a-105">In dit artikel bevat informatie over het maken, beheren en het verwijderen van de VM-netwerkbronnen met C#.</span><span class="sxs-lookup"><span data-stu-id="2107a-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="2107a-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="2107a-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2107a-107">Een Visual Studio-project maken</span><span class="sxs-lookup"><span data-stu-id="2107a-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="2107a-108">Hallo-pakket installeren</span><span class="sxs-lookup"><span data-stu-id="2107a-108">Install hello package</span></span>
> * <span data-ttu-id="2107a-109">Referenties maken</span><span class="sxs-lookup"><span data-stu-id="2107a-109">Create credentials</span></span>
> * <span data-ttu-id="2107a-110">Resources maken</span><span class="sxs-lookup"><span data-stu-id="2107a-110">Create resources</span></span>
> * <span data-ttu-id="2107a-111">Beheertaken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2107a-111">Perform management tasks</span></span>
> * <span data-ttu-id="2107a-112">Resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="2107a-112">Delete resources</span></span>
> * <span data-ttu-id="2107a-113">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2107a-113">Run hello application</span></span>

<span data-ttu-id="2107a-114">Het duurt ongeveer 20 minuten toodo deze stappen.</span><span class="sxs-lookup"><span data-stu-id="2107a-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="2107a-115">Een Visual Studio-project maken</span><span class="sxs-lookup"><span data-stu-id="2107a-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="2107a-116">Als u nog niet gedaan hebt, installeert u [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="2107a-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="2107a-117">Selecteer **.NET-ontwikkeling voor bureaubladen** op Hallo van werkbelastingen pagina en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="2107a-117">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="2107a-118">In Hallo samenvatting, kunt u zien dat **.NET Framework 4 4.6 ontwikkelingsprogramma's** automatisch voor u is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="2107a-118">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="2107a-119">Als u Visual Studio al hebt geïnstalleerd, kunt u Hallo .NET werkbelasting met behulp van Visual Studio starten Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2107a-119">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="2107a-120">Klik in Visual Studio **bestand** > **nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="2107a-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="2107a-121">In **sjablonen** > **Visual C#**, selecteer **Console-App (.NET Framework)**, voer *myDotnetProject* voor Hallo-naam van Hallo-project, selecteer Hallo-locatie van het Hallo-project en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2107a-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-package"></a><span data-ttu-id="2107a-122">Hallo-pakket installeren</span><span class="sxs-lookup"><span data-stu-id="2107a-122">Install hello package</span></span>

<span data-ttu-id="2107a-123">NuGet-pakketten zijn Hallo gemakkelijkste manier tooinstall Hallo tapewisselaars moet u toofinish deze stappen.</span><span class="sxs-lookup"><span data-stu-id="2107a-123">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="2107a-124">tooget hello bibliotheken die u nodig hebt in Visual Studio, voer deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2107a-124">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="2107a-125">Klik op **extra** > **Nuget Package Manager**, en klik vervolgens op **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="2107a-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="2107a-126">Typ deze opdracht in Hallo-console:</span><span class="sxs-lookup"><span data-stu-id="2107a-126">Type this command in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="2107a-127">Referenties maken</span><span class="sxs-lookup"><span data-stu-id="2107a-127">Create credentials</span></span>

<span data-ttu-id="2107a-128">Voordat u deze stap, zorg ervoor dat u toegang tot tooan hebt [Active Directory-service-principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2107a-128">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="2107a-129">U moet ook Hallo toepassings-ID en verificatiesleutel Hallo Hallo tenant-ID die u nodig hebt in een later stadium vastleggen.</span><span class="sxs-lookup"><span data-stu-id="2107a-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="2107a-130">Hallo-bestand met autorisatieregels maken</span><span class="sxs-lookup"><span data-stu-id="2107a-130">Create hello authorization file</span></span>

1. <span data-ttu-id="2107a-131">Klik in Solution Explorer met de rechtermuisknop op *myDotnetProject* > **toevoegen** > **Nieuw Item**, en selecteer vervolgens **tekstbestand** in *Visual C# Items*.</span><span class="sxs-lookup"><span data-stu-id="2107a-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="2107a-132">Bestand met de Hallo *azureauth.properties*, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2107a-132">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="2107a-133">Deze eigenschappen van autorisatie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2107a-133">Add these authorization properties:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="2107a-134">Vervang  **&lt;abonnement-id&gt;**  met uw abonnements-id  **&lt;toepassing-id&gt;**  Hello Active Directory-toepassing ID en  **&lt;verificatiesleutel&gt;**  sleutel van de toepassing hello, en  **&lt;tenant-id&gt;**  hello tenant ID.</span><span class="sxs-lookup"><span data-stu-id="2107a-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="2107a-135">Hallo azureauth.properties bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="2107a-135">Save hello azureauth.properties file.</span></span> 
4. <span data-ttu-id="2107a-136">Stelt de omgevingsvariabele in Windows met de naam AZURE_AUTH_LOCATION met Hallo volledig pad tooauthorization-bestand dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2107a-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created.</span></span> <span data-ttu-id="2107a-137">Bijvoorbeeld de volgende PowerShell-opdracht Hallo kan worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="2107a-137">For example, hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a><span data-ttu-id="2107a-138">Hallo-management-client maken</span><span class="sxs-lookup"><span data-stu-id="2107a-138">Create hello management client</span></span>

1. <span data-ttu-id="2107a-139">Open het bestand Program.cs Hallo voor Hallo-project dat u hebt gemaakt en voeg vervolgens deze using-instructies toohello bestaande instructies boven aan het Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="2107a-139">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="2107a-140">toocreate hello Beheerclient, voeg deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="2107a-140">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="2107a-141">Resources maken</span><span class="sxs-lookup"><span data-stu-id="2107a-141">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="2107a-142">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="2107a-142">Create hello resource group</span></span>

<span data-ttu-id="2107a-143">Alle resources moeten zijn opgenomen in een [resourcegroep](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2107a-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="2107a-144">toospecify waarden voor toepassing hello en Hallo resourcegroep maken, deze code toohello Main-methode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2107a-144">toospecify values for hello application and create hello resource group, add this code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="2107a-145">Hallo beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="2107a-145">Create hello availability set</span></span>

<span data-ttu-id="2107a-146">[Beschikbaarheidssets](tutorial-availability-sets.md) eenvoudiger voor u toomaintain Hallo virtuele machines die worden gebruikt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="2107a-146">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="2107a-147">toocreate hello beschikbaarheid ingesteld, wordt deze code toohello Main-methode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2107a-147">toocreate hello availability set, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="2107a-148">Hallo openbare IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="2107a-148">Create hello public IP address</span></span>

<span data-ttu-id="2107a-149">Een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) benodigde toocommunicate met Hallo virtuele machine is.</span><span class="sxs-lookup"><span data-stu-id="2107a-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="2107a-150">toocreate Hallo openbaar IP-adres voor de virtuele machine van Hallo, voeg deze code toohello Main-methode:</span><span class="sxs-lookup"><span data-stu-id="2107a-150">toocreate hello public IP address for hello virtual machine, add this code toohello Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="2107a-151">Hallo virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="2107a-151">Create hello virtual network</span></span>

<span data-ttu-id="2107a-152">Een virtuele machine moet worden in een subnet van een [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2107a-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="2107a-153">Voeg deze code toohello Main-methode toocreate een subnet en een virtueel netwerk:</span><span class="sxs-lookup"><span data-stu-id="2107a-153">toocreate a subnet and a virtual network, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="2107a-154">Hallo-netwerkinterface maken</span><span class="sxs-lookup"><span data-stu-id="2107a-154">Create hello network interface</span></span>

<span data-ttu-id="2107a-155">Een virtuele machine moet een network interface-toocommunicate op Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="2107a-155">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="2107a-156">toocreate een netwerkinterface, voeg deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="2107a-156">toocreate a network interface, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating network interface...");
var networkInterface = azure.NetworkInterfaces.Define("myNIC")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetwork(network)
    .WithSubnet("mySubnet")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithExistingPrimaryPublicIPAddress(publicIPAddress)
    .Create();
 ```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="2107a-157">Hallo virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="2107a-157">Create hello virtual machine</span></span>

<span data-ttu-id="2107a-158">Nu dat u alle Hallo ondersteunende resources hebt gemaakt, kunt u een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2107a-158">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="2107a-159">toocreate Hallo van virtuele machine, voeg deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="2107a-159">toocreate hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual machine...");
azure.VirtualMachines.Define(vmName)
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("azureuser")
    .WithAdminPassword("Azure12345678")
    .WithComputerName(vmName)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

> [!NOTE]
> <span data-ttu-id="2107a-160">Deze zelfstudie maakt een virtuele machine met een versie van Windows Server-besturingssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="2107a-160">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="2107a-161">Zie toolearn meer informatie over het selecteren van de andere afbeeldingen [navigeren door en selecteren van installatiekopieën van virtuele machine van Azure met Windows PowerShell en Azure CLI Hallo](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2107a-161">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="2107a-162">Als u een bestaande schijf in plaats van een marketplace-installatiekopie toouse wilt, kunt u deze code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2107a-162">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span>

```
var managedDisk = azure.Disks.Define("myosdisk")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd")
    .WithSizeInGB(128)
    .WithSku(DiskSkuTypes.PremiumLRS)
    .Create();

azure.VirtualMachines.Define("myVM")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

## <a name="perform-management-tasks"></a><span data-ttu-id="2107a-163">Beheertaken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2107a-163">Perform management tasks</span></span>

<span data-ttu-id="2107a-164">Tijdens het Hallo-levensduur van een virtuele machine kunt u beheertaken toorun zoals starten, stoppen of een virtuele machine wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2107a-164">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="2107a-165">U kunt bovendien toocreate code tooautomate herhalende of complexe taken.</span><span class="sxs-lookup"><span data-stu-id="2107a-165">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="2107a-166">Wanneer u toodo iets met Hallo VM nodig, moet u tooget een exemplaar van het:</span><span class="sxs-lookup"><span data-stu-id="2107a-166">When you need toodo anything with hello VM, you need tooget an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="2107a-167">Informatie ophalen over Hallo VM</span><span class="sxs-lookup"><span data-stu-id="2107a-167">Get information about hello VM</span></span>

<span data-ttu-id="2107a-168">tooget informatie over de virtuele machine Hallo, voeg deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="2107a-168">tooget information about hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Getting information about hello virtual machine...");
Console.WriteLine("hardwareProfile");
Console.WriteLine("   vmSize: " + vm.Size);
Console.WriteLine("storageProfile");
Console.WriteLine("  imageReference");
Console.WriteLine("    publisher: " + vm.StorageProfile.ImageReference.Publisher);
Console.WriteLine("    offer: " + vm.StorageProfile.ImageReference.Offer);
Console.WriteLine("    sku: " + vm.StorageProfile.ImageReference.Sku);
Console.WriteLine("    version: " + vm.StorageProfile.ImageReference.Version);
Console.WriteLine("  osDisk");
Console.WriteLine("    osType: " + vm.StorageProfile.OsDisk.OsType);
Console.WriteLine("    name: " + vm.StorageProfile.OsDisk.Name);
Console.WriteLine("    createOption: " + vm.StorageProfile.OsDisk.CreateOption);
Console.WriteLine("    caching: " + vm.StorageProfile.OsDisk.Caching);
Console.WriteLine("osProfile");
Console.WriteLine("  computerName: " + vm.OSProfile.ComputerName);
Console.WriteLine("  adminUsername: " + vm.OSProfile.AdminUsername);
Console.WriteLine("  provisionVMAgent: " + vm.OSProfile.WindowsConfiguration.ProvisionVMAgent.Value);
Console.WriteLine("  enableAutomaticUpdates: " + vm.OSProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
Console.WriteLine("networkProfile");
foreach (string nicId in vm.NetworkInterfaceIds)
{
    Console.WriteLine("  networkInterface id: " + nicId);
}
Console.WriteLine("vmAgent");
Console.WriteLine("  vmAgentVersion" + vm.InstanceView.VmAgent.VmAgentVersion);
Console.WriteLine("    statuses");
foreach (InstanceViewStatus stat in vm.InstanceView.VmAgent.Statuses)
{
    Console.WriteLine("    code: " + stat.Code);
    Console.WriteLine("    level: " + stat.Level);
    Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
    Console.WriteLine("    message: " + stat.Message);
    Console.WriteLine("    time: " + stat.Time);
}
Console.WriteLine("disks");
foreach (DiskInstanceView disk in vm.InstanceView.Disks)
{
    Console.WriteLine("  name: " + disk.Name);
    Console.WriteLine("  statuses");
    foreach (InstanceViewStatus stat in disk.Statuses)
    {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    time: " + stat.Time);
    }
}
Console.WriteLine("VM general status");
Console.WriteLine("  provisioningStatus: " + vm.ProvisioningState);
Console.WriteLine("  id: " + vm.Id);
Console.WriteLine("  name: " + vm.Name);
Console.WriteLine("  type: " + vm.Type);
Console.WriteLine("  location: " + vm.Region);
Console.WriteLine("VM instance status");
foreach (InstanceViewStatus stat in vm.InstanceView.Statuses)
{
    Console.WriteLine("  code: " + stat.Code);
    Console.WriteLine("  level: " + stat.Level);
    Console.WriteLine("  displayStatus: " + stat.DisplayStatus);
}
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="stop-hello-vm"></a><span data-ttu-id="2107a-169">Hallo VM stoppen</span><span class="sxs-lookup"><span data-stu-id="2107a-169">Stop hello VM</span></span>

<span data-ttu-id="2107a-170">Stoppen van een virtuele machine en alle bijbehorende instellingen behouden, maar blijven toobe in rekening gebracht voor of u kunt een virtuele machine stoppen en deze ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2107a-170">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="2107a-171">Wanneer een virtuele machine in de toewijzing is opgeheven, zijn alle resources die zijn gekoppeld ook toewijzing ongedaan is gemaakt en facturering eindigt voor.</span><span class="sxs-lookup"><span data-stu-id="2107a-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="2107a-172">toostop hello virtuele machine zonder toewijzing, voeg deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="2107a-172">toostop hello virtual machine without deallocating it, add this code toohello Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

<span data-ttu-id="2107a-173">Als u toodeallocate Hallo virtuele machine wilt, Hallo uitgeschakeld aanroep toothis code wijzigen:</span><span class="sxs-lookup"><span data-stu-id="2107a-173">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="2107a-174">Hallo VM starten</span><span class="sxs-lookup"><span data-stu-id="2107a-174">Start hello VM</span></span>

<span data-ttu-id="2107a-175">toostart Hallo van virtuele machine, voeg deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="2107a-175">toostart hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="2107a-176">Hallo VM vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="2107a-176">Resize hello VM</span></span>

<span data-ttu-id="2107a-177">Veel aspecten van de implementatie moeten worden beschouwd bij het kiezen van een grootte voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2107a-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="2107a-178">Zie voor meer informatie [VM-grootten](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="2107a-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="2107a-179">toochange grootte van Hallo virtuele machine, voeg deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="2107a-179">toochange size of hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="2107a-180">Toevoegen van een data schijf toohello VM</span><span class="sxs-lookup"><span data-stu-id="2107a-180">Add a data disk toohello VM</span></span>

<span data-ttu-id="2107a-181">tooadd een gegevens schijf toohello virtuele machine, deze code toohello Main-methode tooadd een gegevensschijf dat is 2 GB groot en han een LUN van 0 en een cache in type ReadWrite toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2107a-181">tooadd a data disk toohello virtual machine, add this code toohello Main method tooadd a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="2107a-182">Resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="2107a-182">Delete resources</span></span>

<span data-ttu-id="2107a-183">Omdat u in rekening voor resources die worden gebruikt in Azure gebracht, maar het is altijd raadzaam toodelete bronnen die niet langer nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="2107a-183">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="2107a-184">Als u toodelete Hallo virtuele machines wilt en alle Hallo bronnen ondersteunen, alle toodo hebt is Hallo-resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2107a-184">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

<span data-ttu-id="2107a-185">toodelete hello resource groep, voegt u deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="2107a-185">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="2107a-186">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2107a-186">Run hello application</span></span>

<span data-ttu-id="2107a-187">Het moet over vijf minuten duren voordat deze toorun console toepassing volledig van toofinish start.</span><span class="sxs-lookup"><span data-stu-id="2107a-187">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="2107a-188">toorun Hallo-consoletoepassing, klikt u op **Start**.</span><span class="sxs-lookup"><span data-stu-id="2107a-188">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="2107a-189">Voordat u op **Enter** toostart verwijderen resources, u kan een paar minuten duren tooverify Hallo maken van Hallo resources in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2107a-189">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="2107a-190">Klik op Hallo implementatie toosee statusinformatie over Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="2107a-190">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2107a-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2107a-191">Next steps</span></span>
* <span data-ttu-id="2107a-192">Profiteren van het gebruik van een sjabloon toocreate een virtuele machine met behulp van informatie in Hallo [implementeren van een virtuele Machine van Azure met C# en Resource Manager-sjabloon](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2107a-192">Take advantage of using a template toocreate a virtual machine by using hello information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="2107a-193">Meer informatie over het gebruik van Hallo [Azure-bibliotheken voor .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="2107a-193">Learn more about using hello [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

