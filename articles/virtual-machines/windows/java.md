---
title: aaaCreate en beheren van een Azure virtuele Machine met behulp van Java | Microsoft Docs
description: Gebruik toodeploy Java en Azure Resource Manager een virtuele machine en de ondersteunende bronnen.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 31ac8d59f92ecff887e64906940933dd6fd50815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="2e93d-103">Maken en beheren van Windows-machines in Azure met behulp van Java</span><span class="sxs-lookup"><span data-stu-id="2e93d-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="2e93d-104">Een [Azure virtuele Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) moet meerdere ondersteunende Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="2e93d-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="2e93d-105">In dit artikel bevat informatie over het maken, beheren en het verwijderen van de VM-netwerkbronnen met behulp van Java.</span><span class="sxs-lookup"><span data-stu-id="2e93d-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="2e93d-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="2e93d-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2e93d-107">Een Maven-project maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-107">Create a Maven project</span></span>
> * <span data-ttu-id="2e93d-108">Afhankelijkheden toevoegen</span><span class="sxs-lookup"><span data-stu-id="2e93d-108">Add dependencies</span></span>
> * <span data-ttu-id="2e93d-109">Referenties maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-109">Create credentials</span></span>
> * <span data-ttu-id="2e93d-110">Resources maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-110">Create resources</span></span>
> * <span data-ttu-id="2e93d-111">Beheertaken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2e93d-111">Perform management tasks</span></span>
> * <span data-ttu-id="2e93d-112">Resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="2e93d-112">Delete resources</span></span>
> * <span data-ttu-id="2e93d-113">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2e93d-113">Run hello application</span></span>

<span data-ttu-id="2e93d-114">Het duurt ongeveer 20 minuten toodo deze stappen.</span><span class="sxs-lookup"><span data-stu-id="2e93d-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="2e93d-115">Een Maven-project maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-115">Create a Maven project</span></span>

1. <span data-ttu-id="2e93d-116">Als u dit nog niet hebt gedaan, installeert u [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="2e93d-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="2e93d-117">Installeer [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="2e93d-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="2e93d-118">Maak een nieuwe map en het Hallo-project:</span><span class="sxs-lookup"><span data-stu-id="2e93d-118">Create a new folder and hello project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="2e93d-119">Afhankelijkheden toevoegen</span><span class="sxs-lookup"><span data-stu-id="2e93d-119">Add dependencies</span></span>

1. <span data-ttu-id="2e93d-120">Onder Hallo `testAzureApp` map, open Hallo `pom.xml` bestands- en configuratie van de build hello te toevoegen&lt;project&gt; tooenable Hallo bouwen van uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="2e93d-120">Under hello `testAzureApp` folder, open hello `pom.xml` file and add hello build configuration too&lt;project&gt; tooenable hello building of your application:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.App</mainClass>
            </configuration>
        </plugin>
      </plugins>
    </build>
    ```

2. <span data-ttu-id="2e93d-121">Hallo-afhankelijkheden die vereist tooaccess hello Azure-SDK voor Java zijn toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2e93d-121">Add hello dependencies that are needed tooaccess hello Azure Java SDK.</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-compute</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-resources</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-network</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.squareup.okio</groupId>
      <artifactId>okio</artifactId>
      <version>1.13.0</version>
    </dependency>
    <dependency> 
      <groupId>com.nimbusds</groupId>
      <artifactId>nimbus-jose-jwt</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>1.0.6.3</version>
    </dependency>
    <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>mail</artifactId>
      <version>1.4.5</version>
    </dependency>
    ```

3. <span data-ttu-id="2e93d-122">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="2e93d-122">Save hello file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="2e93d-123">Referenties maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-123">Create credentials</span></span>

<span data-ttu-id="2e93d-124">Voordat u deze stap, zorg ervoor dat u toegang tot tooan hebt [Active Directory-service-principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2e93d-124">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="2e93d-125">U moet ook Hallo toepassings-ID en verificatiesleutel Hallo Hallo tenant-ID die u nodig hebt in een later stadium vastleggen.</span><span class="sxs-lookup"><span data-stu-id="2e93d-125">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="2e93d-126">Hallo-bestand met autorisatieregels maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-126">Create hello authorization file</span></span>

1. <span data-ttu-id="2e93d-127">Maak een bestand met de naam `azureauth.properties` en deze tooit eigenschappen toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-127">Create a file named `azureauth.properties` and add these properties tooit:</span></span>

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

    <span data-ttu-id="2e93d-128">Vervang  **&lt;abonnement-id&gt;**  met uw abonnements-id  **&lt;toepassing-id&gt;**  Hello Active Directory-toepassing ID en  **&lt;verificatiesleutel&gt;**  sleutel van de toepassing hello, en  **&lt;tenant-id&gt;**  hello tenant ID.</span><span class="sxs-lookup"><span data-stu-id="2e93d-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

2. <span data-ttu-id="2e93d-129">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="2e93d-129">Save hello file.</span></span>
3. <span data-ttu-id="2e93d-130">Omgevingsvariabele AZURE_AUTH_LOCATION in uw shell met Hallo volledig pad toohello verificatiebestand ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2e93d-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with hello full path toohello authentication file.</span></span>

### <a name="create-hello-management-client"></a><span data-ttu-id="2e93d-131">Hallo-management-client maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-131">Create hello management client</span></span>

1. <span data-ttu-id="2e93d-132">Open Hallo `App.java` bestand onder `src\main\java\com\fabrikam` en zorg ervoor dat deze instructie package Hallo boven:</span><span class="sxs-lookup"><span data-stu-id="2e93d-132">Open hello `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at hello top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="2e93d-133">Voeg deze onder Hallo pakketinstructie importinstructies:</span><span class="sxs-lookup"><span data-stu-id="2e93d-133">Under hello package statement, add these import statements:</span></span>
   
    ```java
    import com.microsoft.azure.management.Azure;
    import com.microsoft.azure.management.compute.AvailabilitySet;
    import com.microsoft.azure.management.compute.AvailabilitySetSkuTypes;
    import com.microsoft.azure.management.compute.CachingTypes;
    import com.microsoft.azure.management.compute.InstanceViewStatus;
    import com.microsoft.azure.management.compute.DiskInstanceView;
    import com.microsoft.azure.management.compute.VirtualMachine;
    import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
    import com.microsoft.azure.management.network.PublicIPAddress;
    import com.microsoft.azure.management.network.Network;
    import com.microsoft.azure.management.network.NetworkInterface;
    import com.microsoft.azure.management.resources.ResourceGroup;
    import com.microsoft.azure.management.resources.fluentcore.arm.Region;
    import com.microsoft.azure.management.resources.fluentcore.model.Creatable;
    import com.microsoft.rest.LogLevel;
    import java.io.File;
    import java.util.Scanner;
    ```

2. <span data-ttu-id="2e93d-134">Active Directory-referenties voor toocreate Hallo is dat u toomake aanvragen, moet toevoegen deze code toohello-hoofdmethode Hallo App klasse:</span><span class="sxs-lookup"><span data-stu-id="2e93d-134">toocreate hello Active Directory credentials that you need toomake requests, add this code toohello main method of hello App class:</span></span>
   
    ```java
    try {    
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
            .withLogLevel(LogLevel.BASIC)
            .authenticate(credFile)
            .withDefaultSubscription();
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    ```

## <a name="create-resources"></a><span data-ttu-id="2e93d-135">Resources maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-135">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="2e93d-136">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-136">Create hello resource group</span></span>

<span data-ttu-id="2e93d-137">Alle resources moeten zijn opgenomen in een [resourcegroep](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e93d-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="2e93d-138">toospecify waarden voor toepassing hello en Hallo resourcegroep maken, deze code toohello try-blok op Hallo hoofdmethode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-138">toospecify values for hello application and create hello resource group, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="2e93d-139">Hallo beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-139">Create hello availability set</span></span>

<span data-ttu-id="2e93d-140">[Beschikbaarheidssets](tutorial-availability-sets.md) eenvoudiger voor u toomaintain Hallo virtuele machines die worden gebruikt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="2e93d-140">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="2e93d-141">toocreate hello beschikbaarheid instellen, deze code toohello try-blok op Hallo hoofdmethode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-141">toocreate hello availability set, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a><span data-ttu-id="2e93d-142">Hallo openbare IP-adres maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-142">Create hello public IP address</span></span>

<span data-ttu-id="2e93d-143">Een [openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) benodigde toocommunicate met Hallo virtuele machine is.</span><span class="sxs-lookup"><span data-stu-id="2e93d-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="2e93d-144">toocreate hello openbaar IP-adres voor de virtuele machine van hello, deze code toohello try-blok op Hallo hoofdmethode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-144">toocreate hello public IP address for hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="2e93d-145">Hallo virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-145">Create hello virtual network</span></span>

<span data-ttu-id="2e93d-146">Een virtuele machine moet worden in een subnet van een [virtueel netwerk](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e93d-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="2e93d-147">toocreate een subnet en een virtueel netwerk, moet u deze code toohello try-blok toevoegen in Hallo hoofdmethode:</span><span class="sxs-lookup"><span data-stu-id="2e93d-147">toocreate a subnet and a virtual network, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual network...");
Network network = azure.networks()
    .define("myVN")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withAddressSpace("10.0.0.0/16")
    .withSubnet("mySubnet","10.0.0.0/24")
    .create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="2e93d-148">Hallo-netwerkinterface maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-148">Create hello network interface</span></span>

<span data-ttu-id="2e93d-149">Een virtuele machine moet een network interface-toocommunicate op Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="2e93d-149">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="2e93d-150">een netwerkinterface toocreate deze code toohello try-blok op Hallo hoofdmethode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-150">toocreate a network interface, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating network interface...");
NetworkInterface networkInterface = azure.networkInterfaces()
    .define("myNIC")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetwork(network)
    .withSubnet("mySubnet")
    .withPrimaryPrivateIPAddressDynamic()
    .withExistingPrimaryPublicIPAddress(publicIPAddress)
    .create();
```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="2e93d-151">Hallo virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="2e93d-151">Create hello virtual machine</span></span>

<span data-ttu-id="2e93d-152">Nu dat u alle Hallo ondersteunende resources hebt gemaakt, kunt u een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2e93d-152">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="2e93d-153">toocreate Hallo van virtuele machine, deze code toohello try-blok op Hallo hoofdmethode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-153">toocreate hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual machine...");
VirtualMachine virtualMachine = azure.virtualMachines()
    .define("myVM")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("azureuser")
    .withAdminPassword("Azure12345678")
    .withComputerName("myVM")
    .withExistingAvailabilitySet(availabilitySet)
    .withSize("Standard_DS1")
    .create();
Scanner input = new Scanner(System.in);
System.out.println("Press enter tooget information about hello VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="2e93d-154">Deze zelfstudie maakt een virtuele machine met een versie van Windows Server-besturingssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e93d-154">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="2e93d-155">Zie toolearn meer informatie over het selecteren van de andere afbeeldingen [navigeren door en selecteren van installatiekopieën van virtuele machine van Azure met Windows PowerShell en Azure CLI Hallo](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e93d-155">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="2e93d-156">Als u een bestaande schijf in plaats van een marketplace-installatiekopie toouse wilt, kunt u deze code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2e93d-156">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span> 

```java
ManagedDisk managedDisk = azure.disks.define("myosdisk") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd") 
    .withSizeInGB(128) 
    .withSku(DiskSkuTypes.PremiumLRS) 
    .create(); 

azure.virtualMachines.define("myVM") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withExistingPrimaryNetworkInterface(networkInterface) 
    .withSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows) 
    .withExistingAvailabilitySet(availabilitySet) 
    .withSize(VirtualMachineSizeTypes.StandardDS1) 
    .create(); 
``` 

## <a name="perform-management-tasks"></a><span data-ttu-id="2e93d-157">Beheertaken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2e93d-157">Perform management tasks</span></span>

<span data-ttu-id="2e93d-158">Tijdens het Hallo-levensduur van een virtuele machine kunt u beheertaken toorun zoals starten, stoppen of een virtuele machine wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2e93d-158">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="2e93d-159">U kunt bovendien toocreate code tooautomate herhalende of complexe taken.</span><span class="sxs-lookup"><span data-stu-id="2e93d-159">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="2e93d-160">Wanneer u toodo iets met Hallo VM nodig, moet u tooget een exemplaar van deze.</span><span class="sxs-lookup"><span data-stu-id="2e93d-160">When you need toodo anything with hello VM, you need tooget an instance of it.</span></span> <span data-ttu-id="2e93d-161">Deze code toohello try-blok van de belangrijkste methode Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-161">Add this code toohello try block of hello main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="2e93d-162">Informatie ophalen over Hallo VM</span><span class="sxs-lookup"><span data-stu-id="2e93d-162">Get information about hello VM</span></span>

<span data-ttu-id="2e93d-163">informatie over de virtuele machine Hallo tooget deze code toohello try-blok op Hallo hoofdmethode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-163">tooget information about hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("hardwareProfile");
System.out.println("    vmSize: " + vm.size());
System.out.println("storageProfile");
System.out.println("  imageReference");
System.out.println("    publisher: " + vm.storageProfile().imageReference().publisher());
System.out.println("    offer: " + vm.storageProfile().imageReference().offer());
System.out.println("    sku: " + vm.storageProfile().imageReference().sku());
System.out.println("    version: " + vm.storageProfile().imageReference().version());
System.out.println("  osDisk");
System.out.println("    osType: " + vm.storageProfile().osDisk().osType());
System.out.println("    name: " + vm.storageProfile().osDisk().name());
System.out.println("    createOption: " + vm.storageProfile().osDisk().createOption());
System.out.println("    caching: " + vm.storageProfile().osDisk().caching());
System.out.println("osProfile");
System.out.println("    computerName: " + vm.osProfile().computerName());
System.out.println("    adminUserName: " + vm.osProfile().adminUsername());
System.out.println("    provisionVMAgent: " + vm.osProfile().windowsConfiguration().provisionVMAgent());
System.out.println("    enableAutomaticUpdates: " + vm.osProfile().windowsConfiguration().enableAutomaticUpdates());
System.out.println("networkProfile");
System.out.println("    networkInterface: " + vm.primaryNetworkInterfaceId());
System.out.println("vmAgent");
System.out.println("  vmAgentVersion: " + vm.instanceView().vmAgent().vmAgentVersion());
System.out.println("    statuses");
for(InstanceViewStatus status : vm.instanceView().vmAgent().statuses()) {
    System.out.println("    code: " + status.code());
    System.out.println("    displayStatus: " + status.displayStatus());
    System.out.println("    message: " + status.message());
    System.out.println("    time: " + status.time());
}
System.out.println("disks");
for(DiskInstanceView disk : vm.instanceView().disks()) {
    System.out.println("  name: " + disk.name());
    System.out.println("  statuses");
    for(InstanceViewStatus status : disk.statuses()) {
        System.out.println("    code: " + status.code());
        System.out.println("    displayStatus: " + status.displayStatus());
        System.out.println("    time: " + status.time());
    }
}
System.out.println("VM general status");
System.out.println("  provisioningStatus: " + vm.provisioningState());
System.out.println("  id: " + vm.id());
System.out.println("  name: " + vm.name());
System.out.println("  type: " + vm.type());
System.out.println("VM instance status");
for(InstanceViewStatus status : vm.instanceView().statuses()) {
    System.out.println("  code: " + status.code());
    System.out.println("  displayStatus: " + status.displayStatus());
}
System.out.println("Press enter toocontinue...");
input.nextLine();   
```

### <a name="stop-hello-vm"></a><span data-ttu-id="2e93d-164">Hallo VM stoppen</span><span class="sxs-lookup"><span data-stu-id="2e93d-164">Stop hello VM</span></span>

<span data-ttu-id="2e93d-165">Stoppen van een virtuele machine en alle bijbehorende instellingen behouden, maar blijven toobe in rekening gebracht voor of u kunt een virtuele machine stoppen en deze ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2e93d-165">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="2e93d-166">Wanneer een virtuele machine in de toewijzing is opgeheven, zijn alle resources die zijn gekoppeld ook toewijzing ongedaan is gemaakt en facturering eindigt voor.</span><span class="sxs-lookup"><span data-stu-id="2e93d-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="2e93d-167">toostop hello virtuele machine zonder toewijzing, wordt deze code toohello try-blok op Hallo hoofdmethode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-167">toostop hello virtual machine without deallocating it, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

<span data-ttu-id="2e93d-168">Als u toodeallocate Hallo virtuele machine wilt, Hallo uitgeschakeld aanroep toothis code wijzigen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-168">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="2e93d-169">Hallo VM starten</span><span class="sxs-lookup"><span data-stu-id="2e93d-169">Start hello VM</span></span>

<span data-ttu-id="2e93d-170">toostart Hallo van virtuele machine, deze code toohello try-blok op Hallo hoofdmethode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-170">toostart hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="2e93d-171">Hallo VM vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="2e93d-171">Resize hello VM</span></span>

<span data-ttu-id="2e93d-172">Veel aspecten van de implementatie moeten worden beschouwd bij het kiezen van een grootte voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2e93d-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="2e93d-173">Zie voor meer informatie [VM-grootten](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="2e93d-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="2e93d-174">toochange grootte van Hallo virtuele machine, wordt deze code toohello try-blok op Hallo hoofdmethode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-174">toochange size of hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="2e93d-175">Toevoegen van een data schijf toohello VM</span><span class="sxs-lookup"><span data-stu-id="2e93d-175">Add a data disk toohello VM</span></span>

<span data-ttu-id="2e93d-176">tooadd een gegevens schijf toohello virtuele machine die is 2 GB groot en heeft een LUN van 0 en een cache in type ReadWrite, deze code toohello try-blok op Hallo hoofdmethode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-176">tooadd a data disk toohello virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="2e93d-177">Resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="2e93d-177">Delete resources</span></span>

<span data-ttu-id="2e93d-178">Omdat u in rekening voor resources die worden gebruikt in Azure gebracht, maar het is altijd raadzaam toodelete bronnen die niet langer nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="2e93d-178">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="2e93d-179">Als u toodelete Hallo virtuele machines wilt en alle Hallo bronnen ondersteunen, alle toodo hebt is Hallo-resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2e93d-179">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="2e93d-180">toodelete hello resource groep, deze code toohello try-blok op Hallo hoofdmethode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2e93d-180">toodelete hello resource group, add this code toohello try block in hello main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="2e93d-181">Hallo App.java bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="2e93d-181">Save hello App.java file.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="2e93d-182">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2e93d-182">Run hello application</span></span>

<span data-ttu-id="2e93d-183">Het moet over vijf minuten duren voordat deze toorun console toepassing volledig van toofinish start.</span><span class="sxs-lookup"><span data-stu-id="2e93d-183">It should take about five minutes for this console application toorun completely from start toofinish.</span></span>

1. <span data-ttu-id="2e93d-184">toorun Hallo van toepassing, gebruikt u deze Maven-opdracht:</span><span class="sxs-lookup"><span data-stu-id="2e93d-184">toorun hello application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="2e93d-185">Voordat u op **Enter** toostart verwijderen resources, u kan een paar minuten duren tooverify Hallo maken van Hallo resources in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2e93d-185">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="2e93d-186">Klik op Hallo implementatie toosee statusinformatie over Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="2e93d-186">Click hello deployment status toosee information about hello deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2e93d-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e93d-187">Next steps</span></span>
* <span data-ttu-id="2e93d-188">Meer informatie over het gebruik van Hallo [Azure-beheerbibliotheken voor Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="2e93d-188">Learn more about using hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

