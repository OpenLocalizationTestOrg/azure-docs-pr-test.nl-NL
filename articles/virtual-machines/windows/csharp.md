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
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a>Maken en beheren van Windows-machines in Azure met C# #

Een [Azure virtuele Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) moet meerdere ondersteunende Azure-resources. In dit artikel bevat informatie over het maken, beheren en het verwijderen van de VM-netwerkbronnen met C#. Procedures voor:

> [!div class="checklist"]
> * Een Visual Studio-project maken
> * Hallo-pakket installeren
> * Referenties maken
> * Resources maken
> * Beheertaken uitvoeren
> * Resources verwijderen
> * Hallo-toepassing uitvoeren

Het duurt ongeveer 20 minuten toodo deze stappen.

## <a name="create-a-visual-studio-project"></a>Een Visual Studio-project maken

1. Als u nog niet gedaan hebt, installeert u [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Selecteer **.NET-ontwikkeling voor bureaubladen** op Hallo van werkbelastingen pagina en klik vervolgens op **installeren**. In Hallo samenvatting, kunt u zien dat **.NET Framework 4 4.6 ontwikkelingsprogramma's** automatisch voor u is geselecteerd. Als u Visual Studio al hebt geïnstalleerd, kunt u Hallo .NET werkbelasting met behulp van Visual Studio starten Hallo toevoegen.
2. Klik in Visual Studio **bestand** > **nieuw** > **Project**.
3. In **sjablonen** > **Visual C#**, selecteer **Console-App (.NET Framework)**, voer *myDotnetProject* voor Hallo-naam van Hallo-project, selecteer Hallo-locatie van het Hallo-project en klik vervolgens op **OK**.

## <a name="install-hello-package"></a>Hallo-pakket installeren

NuGet-pakketten zijn Hallo gemakkelijkste manier tooinstall Hallo tapewisselaars moet u toofinish deze stappen. tooget hello bibliotheken die u nodig hebt in Visual Studio, voer deze stappen uit:

1. Klik op **extra** > **Nuget Package Manager**, en klik vervolgens op **Package Manager Console**.
2. Typ deze opdracht in Hallo-console:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a>Referenties maken

Voordat u deze stap, zorg ervoor dat u toegang tot tooan hebt [Active Directory-service-principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md). U moet ook Hallo toepassings-ID en verificatiesleutel Hallo Hallo tenant-ID die u nodig hebt in een later stadium vastleggen.

### <a name="create-hello-authorization-file"></a>Hallo-bestand met autorisatieregels maken

1. Klik in Solution Explorer met de rechtermuisknop op *myDotnetProject* > **toevoegen** > **Nieuw Item**, en selecteer vervolgens **tekstbestand** in *Visual C# Items*. Bestand met de Hallo *azureauth.properties*, en klik vervolgens op **toevoegen**.
2. Deze eigenschappen van autorisatie toevoegen:

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

    Vervang  **&lt;abonnement-id&gt;**  met uw abonnements-id  **&lt;toepassing-id&gt;**  Hello Active Directory-toepassing ID en  **&lt;verificatiesleutel&gt;**  sleutel van de toepassing hello, en  **&lt;tenant-id&gt;**  hello tenant ID.

3. Hallo azureauth.properties bestand opslaan. 
4. Stelt de omgevingsvariabele in Windows met de naam AZURE_AUTH_LOCATION met Hallo volledig pad tooauthorization-bestand dat u hebt gemaakt. Bijvoorbeeld de volgende PowerShell-opdracht Hallo kan worden gebruikt:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a>Hallo-management-client maken

1. Open het bestand Program.cs Hallo voor Hallo-project dat u hebt gemaakt en voeg vervolgens deze using-instructies toohello bestaande instructies boven aan het Hallo-bestand:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. toocreate hello Beheerclient, voeg deze code toohello Main-methode toe:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a>Resources maken

### <a name="create-hello-resource-group"></a>Hallo resourcegroep maken

Alle resources moeten zijn opgenomen in een [resourcegroep](../../azure-resource-manager/resource-group-overview.md).

toospecify waarden voor toepassing hello en Hallo resourcegroep maken, deze code toohello Main-methode toevoegen:

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a>Hallo beschikbaarheidsset maken

[Beschikbaarheidssets](tutorial-availability-sets.md) eenvoudiger voor u toomaintain Hallo virtuele machines die worden gebruikt door uw toepassing.

toocreate hello beschikbaarheid ingesteld, wordt deze code toohello Main-methode toevoegen:

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a>Hallo openbare IP-adres maken

Een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) benodigde toocommunicate met Hallo virtuele machine is.

toocreate Hallo openbaar IP-adres voor de virtuele machine van Hallo, voeg deze code toohello Main-methode:
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a>Hallo virtueel netwerk maken

Een virtuele machine moet worden in een subnet van een [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).

Voeg deze code toohello Main-methode toocreate een subnet en een virtueel netwerk:

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a>Hallo-netwerkinterface maken

Een virtuele machine moet een network interface-toocommunicate op Hallo virtueel netwerk.

toocreate een netwerkinterface, voeg deze code toohello Main-methode toe:

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

### <a name="create-hello-virtual-machine"></a>Hallo virtuele machine maken

Nu dat u alle Hallo ondersteunende resources hebt gemaakt, kunt u een virtuele machine.

toocreate Hallo van virtuele machine, voeg deze code toohello Main-methode toe:

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
> Deze zelfstudie maakt een virtuele machine met een versie van Windows Server-besturingssysteem Hallo. Zie toolearn meer informatie over het selecteren van de andere afbeeldingen [navigeren door en selecteren van installatiekopieën van virtuele machine van Azure met Windows PowerShell en Azure CLI Hallo](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Als u een bestaande schijf in plaats van een marketplace-installatiekopie toouse wilt, kunt u deze code gebruiken:

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

## <a name="perform-management-tasks"></a>Beheertaken uitvoeren

Tijdens het Hallo-levensduur van een virtuele machine kunt u beheertaken toorun zoals starten, stoppen of een virtuele machine wordt verwijderd. U kunt bovendien toocreate code tooautomate herhalende of complexe taken.

Wanneer u toodo iets met Hallo VM nodig, moet u tooget een exemplaar van het:

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a>Informatie ophalen over Hallo VM

tooget informatie over de virtuele machine Hallo, voeg deze code toohello Main-methode toe:

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

### <a name="stop-hello-vm"></a>Hallo VM stoppen

Stoppen van een virtuele machine en alle bijbehorende instellingen behouden, maar blijven toobe in rekening gebracht voor of u kunt een virtuele machine stoppen en deze ongedaan gemaakt. Wanneer een virtuele machine in de toewijzing is opgeheven, zijn alle resources die zijn gekoppeld ook toewijzing ongedaan is gemaakt en facturering eindigt voor.

toostop hello virtuele machine zonder toewijzing, voeg deze code toohello Main-methode toe:

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

Als u toodeallocate Hallo virtuele machine wilt, Hallo uitgeschakeld aanroep toothis code wijzigen:

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a>Hallo VM starten

toostart Hallo van virtuele machine, voeg deze code toohello Main-methode toe:

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a>Hallo VM vergroten of verkleinen

Veel aspecten van de implementatie moeten worden beschouwd bij het kiezen van een grootte voor de virtuele machine. Zie voor meer informatie [VM-grootten](sizes.md).  

toochange grootte van Hallo virtuele machine, voeg deze code toohello Main-methode toe:

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Toevoegen van een data schijf toohello VM

tooadd een gegevens schijf toohello virtuele machine, deze code toohello Main-methode tooadd een gegevensschijf dat is 2 GB groot en han een LUN van 0 en een cache in type ReadWrite toevoegen:

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a>Resources verwijderen

Omdat u in rekening voor resources die worden gebruikt in Azure gebracht, maar het is altijd raadzaam toodelete bronnen die niet langer nodig zijn. Als u toodelete Hallo virtuele machines wilt en alle Hallo bronnen ondersteunen, alle toodo hebt is Hallo-resourcegroep verwijderen.

toodelete hello resource groep, voegt u deze code toohello Main-methode toe:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

Het moet over vijf minuten duren voordat deze toorun console toepassing volledig van toofinish start. 

1. toorun Hallo-consoletoepassing, klikt u op **Start**.

2. Voordat u op **Enter** toostart verwijderen resources, u kan een paar minuten duren tooverify Hallo maken van Hallo resources in hello Azure-portal. Klik op Hallo implementatie toosee statusinformatie over Hallo-implementatie.

## <a name="next-steps"></a>Volgende stappen
* Profiteren van het gebruik van een sjabloon toocreate een virtuele machine met behulp van informatie in Hallo [implementeren van een virtuele Machine van Azure met C# en Resource Manager-sjabloon](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Meer informatie over het gebruik van Hallo [Azure-bibliotheken voor .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).

