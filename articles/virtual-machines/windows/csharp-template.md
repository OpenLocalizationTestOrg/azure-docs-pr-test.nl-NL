---
title: aaaDeploy een VM die gebruikmaakt van C# en Resource Manager-sjabloon | Microsoft Docs
description: Informatie over toohow toouse C# en een Resource Manager-sjabloon toodeploy een Azure VM.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: davidmu
ms.openlocfilehash: 91d470228cfeed72336b488ffef4dfbb25bc3a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="fbbdc-103">Een Azure-virtuele Machine met C# en Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="fbbdc-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="fbbdc-104">Dit artikel ziet u hoe toodeploy met C# om een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-104">This article shows you how toodeploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="fbbdc-105">Hallo-sjabloon die u maakt implementeert een enkele virtuele machine met Windows Server in een nieuw virtueel netwerk met één subnet.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="fbbdc-106">Zie voor een gedetailleerde beschrijving van de bron van de virtuele machine Hallo [virtuele machines in een Azure Resource Manager-sjabloon](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="fbbdc-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="fbbdc-107">Zie voor meer informatie over alle Hallo resources in een sjabloon [overzicht van Azure Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="fbbdc-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="fbbdc-108">Het duurt ongeveer 10 minuten toodo deze stappen.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-108">It takes about 10 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="fbbdc-109">Een Visual Studio-project maken</span><span class="sxs-lookup"><span data-stu-id="fbbdc-109">Create a Visual Studio project</span></span>

<span data-ttu-id="fbbdc-110">In deze stap maakt ervoor u zorgen dat Visual Studio is geïnstalleerd en u een console-toepassing gebruikt toodeploy Hallo sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-110">In this step, you make sure that Visual Studio is installed and you create a console application used toodeploy hello template.</span></span>

1. <span data-ttu-id="fbbdc-111">Als u nog niet gedaan hebt, installeert u [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="fbbdc-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="fbbdc-112">Selecteer **.NET-ontwikkeling voor bureaubladen** op Hallo van werkbelastingen pagina en klik vervolgens op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-112">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="fbbdc-113">In Hallo samenvatting, kunt u zien dat **.NET Framework 4 4.6 ontwikkelingsprogramma's** automatisch voor u is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-113">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="fbbdc-114">Als u Visual Studio al hebt geïnstalleerd, kunt u Hallo .NET werkbelasting met behulp van Visual Studio starten Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-114">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="fbbdc-115">Klik in Visual Studio **bestand** > **nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="fbbdc-116">In **sjablonen** > **Visual C#**, selecteer **Console-App (.NET Framework)**, voer *myDotnetProject* voor Hallo-naam van Hallo-project, selecteer Hallo-locatie van het Hallo-project en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-packages"></a><span data-ttu-id="fbbdc-117">Hello-pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="fbbdc-117">Install hello packages</span></span>

<span data-ttu-id="fbbdc-118">NuGet-pakketten zijn Hallo gemakkelijkste manier tooinstall Hallo tapewisselaars moet u toofinish deze stappen.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-118">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="fbbdc-119">tooget hello bibliotheken die u nodig hebt in Visual Studio, voer deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-119">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="fbbdc-120">Klik op **extra** > **Nuget Package Manager**, en klik vervolgens op **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="fbbdc-121">Typ deze opdrachten in het Hallo-console:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-121">Type these commands in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a><span data-ttu-id="fbbdc-122">Hallo-bestanden maken</span><span class="sxs-lookup"><span data-stu-id="fbbdc-122">Create hello files</span></span>

<span data-ttu-id="fbbdc-123">In deze stap maakt u een sjabloonbestand die Hallo resources implementeert en een parameterbestand dat parameter waarden toohello sjabloon.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-123">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="fbbdc-124">U wordt ook een bestand met autorisatieregels die gebruikte tooperform Azure Resource Manager-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-124">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

### <a name="create-hello-template-file"></a><span data-ttu-id="fbbdc-125">Hallo een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="fbbdc-125">Create hello template file</span></span>

1. <span data-ttu-id="fbbdc-126">Klik in Solution Explorer met de rechtermuisknop op *myDotnetProject* > **toevoegen** > **Nieuw Item**, en selecteer vervolgens **tekstbestand** in *Visual C# Items*.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="fbbdc-127">Bestand met de Hallo *CreateVMTemplate.json*, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-127">Name hello file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="fbbdc-128">Voeg deze JSON-code toohello-bestand dat u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-128">Add this JSON code toohello file that you created:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

3. <span data-ttu-id="fbbdc-129">Hallo CreateVMTemplate.json bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-129">Save hello CreateVMTemplate.json file.</span></span>

### <a name="create-hello-parameters-file"></a><span data-ttu-id="fbbdc-130">Hallo parameterbestand maken</span><span class="sxs-lookup"><span data-stu-id="fbbdc-130">Create hello parameters file</span></span>

<span data-ttu-id="fbbdc-131">toospecify waarden voor Hallo Resourceparameters die zijn gedefinieerd in de sjabloon hello, dat u een parameterbestand met Hallo waarden maken.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-131">toospecify values for hello resource parameters that are defined in hello template, you create a parameters file that contains hello values.</span></span>

1. <span data-ttu-id="fbbdc-132">Klik in Solution Explorer met de rechtermuisknop op *myDotnetProject* > **toevoegen** > **Nieuw Item**, en selecteer vervolgens **tekstbestand** in *Visual C# Items*.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="fbbdc-133">Bestand met de Hallo *Parameters.json*, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-133">Name hello file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="fbbdc-134">Voeg deze JSON-code toohello-bestand dat u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-134">Add this JSON code toohello file that you created:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

4. <span data-ttu-id="fbbdc-135">Hallo Parameters.json bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-135">Save hello Parameters.json file.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="fbbdc-136">Hallo-bestand met autorisatieregels maken</span><span class="sxs-lookup"><span data-stu-id="fbbdc-136">Create hello authorization file</span></span>

<span data-ttu-id="fbbdc-137">Voordat u een sjabloon implementeren kunt, zorg ervoor dat u toegang tot tooan hebt [Active Directory-service-principal](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="fbbdc-137">Before you can deploy a template, make sure that you have access tooan [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="fbbdc-138">Van de service-principal hello, moet u een token voor het verifiëren van aanvragen tooAzure Resource Manager verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-138">From hello service principal, you acquire a token for authenticating requests tooAzure Resource Manager.</span></span> <span data-ttu-id="fbbdc-139">U moet ook Hallo toepassings-ID en verificatiesleutel Hallo Hallo tenant-ID die u nodig hebt in-bestand met autorisatieregels Hallo vastleggen.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-139">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in hello authorization file.</span></span>

1. <span data-ttu-id="fbbdc-140">Klik in Solution Explorer met de rechtermuisknop op *myDotnetProject* > **toevoegen** > **Nieuw Item**, en selecteer vervolgens **tekstbestand** in *Visual C# Items*.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="fbbdc-141">Bestand met de Hallo *azureauth.properties*, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-141">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="fbbdc-142">Deze eigenschappen van autorisatie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-142">Add these authorization properties:</span></span>

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

    <span data-ttu-id="fbbdc-143">Vervang  **&lt;abonnement-id&gt;**  met uw abonnements-id  **&lt;toepassing-id&gt;**  Hello Active Directory-toepassing ID en  **&lt;verificatiesleutel&gt;**  sleutel van de toepassing hello, en  **&lt;tenant-id&gt;**  hello tenant ID.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="fbbdc-144">Hallo azureauth.properties bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-144">Save hello azureauth.properties file.</span></span>
4. <span data-ttu-id="fbbdc-145">Instellen van een omgevingsvariabele in Windows met de naam AZURE_AUTH_LOCATION met Hallo volledig pad tooauthorization-bestand dat u hebt gemaakt, bijvoorbeeld Hallo volgende PowerShell-opdracht kan worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created, for example hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a><span data-ttu-id="fbbdc-146">Hallo-management-client maken</span><span class="sxs-lookup"><span data-stu-id="fbbdc-146">Create hello management client</span></span>

1. <span data-ttu-id="fbbdc-147">Open het bestand Program.cs Hallo voor Hallo-project dat u hebt gemaakt en voeg vervolgens deze using-instructies toohello bestaande instructies boven aan het Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-147">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="fbbdc-148">toocreate hello Beheerclient, voeg deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-148">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="fbbdc-149">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="fbbdc-149">Create a resource group</span></span>

<span data-ttu-id="fbbdc-150">toospecify waarden voor de toepassing hello, voeg code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-150">toospecify values for hello application, add code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="fbbdc-151">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="fbbdc-151">Create a storage account</span></span>

<span data-ttu-id="fbbdc-152">Hallo-sjabloon en de parameters worden van een opslagaccount in Azure geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-152">hello template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="fbbdc-153">In deze stap maakt u Hallo-account maakt en Hallo bestanden uploaden.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-153">In this step, you create hello account and upload hello files.</span></span> 

<span data-ttu-id="fbbdc-154">toocreate Hallo account, voeg deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-154">toocreate hello account, add this code toohello Main method:</span></span>

```
string storageAccountName = SdkContext.RandomResourceName("st", 10);

Console.WriteLine("Creating storage account...");
var storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USWest)
    .WithExistingResourceGroup(resourceGroup)
    .Create();

var storageKeys = storage.GetKeys();
string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=" + storage.Name
    + ";AccountKey=" + storageKeys[0].Value
    + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
var serviceClient = account.CreateCloudBlobClient();

Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("templates");
container.CreateIfNotExistsAsync().Wait();
var containerPermissions = new BlobContainerPermissions()
    { PublicAccess = BlobContainerPublicAccessType.Container };
container.SetPermissionsAsync(containerPermissions).Wait();

Console.WriteLine("Uploading template file...");
var templateblob = container.GetBlockBlobReference("CreateVMTemplate.json");
templateblob.UploadFromFile("..\\..\\CreateVMTemplate.json");

Console.WriteLine("Uploading parameters file...");
var paramblob = container.GetBlockBlobReference("Parameters.json");
paramblob.UploadFromFile("..\\..\\Parameters.json");
```

## <a name="deploy-hello-template"></a><span data-ttu-id="fbbdc-155">Hallo-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="fbbdc-155">Deploy hello template</span></span>

<span data-ttu-id="fbbdc-156">Implementeer Hallo sjabloon en parameters van Hallo storage-account dat is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-156">Deploy hello template and parameters from hello storage account that was created.</span></span> 

<span data-ttu-id="fbbdc-157">toodeploy hello sjabloon, voeg deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-157">toodeploy hello template, add this code toohello Main method:</span></span>

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter toodelete hello resource group...");
Console.ReadLine();
```

## <a name="delete-hello-resources"></a><span data-ttu-id="fbbdc-158">Hallo-resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="fbbdc-158">Delete hello resources</span></span>

<span data-ttu-id="fbbdc-159">Omdat u in rekening voor resources die worden gebruikt in Azure gebracht, maar het is altijd raadzaam toodelete bronnen die niet langer nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-159">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="fbbdc-160">U hoeft niet toodelete elke resource afzonderlijk van een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-160">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="fbbdc-161">Verwijder Hallo resourcegroep en alle bijbehorende resources worden automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-161">Delete hello resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="fbbdc-162">toodelete hello resource groep, voegt u deze code toohello Main-methode toe:</span><span class="sxs-lookup"><span data-stu-id="fbbdc-162">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="fbbdc-163">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="fbbdc-163">Run hello application</span></span>

<span data-ttu-id="fbbdc-164">Het moet over vijf minuten duren voordat deze toorun console toepassing volledig van toofinish start.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-164">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="fbbdc-165">toorun Hallo-consoletoepassing, klikt u op **Start**.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-165">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="fbbdc-166">Voordat u op **Enter** toostart verwijderen resources, u kan een paar minuten duren tooverify Hallo maken van Hallo resources in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-166">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="fbbdc-167">Klik op Hallo implementatie toosee statusinformatie over Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="fbbdc-167">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbbdc-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fbbdc-168">Next steps</span></span>
* <span data-ttu-id="fbbdc-169">Als er problemen met de Hallo-implementatie zijn, een volgende stap toolook op zou zijn [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="fbbdc-169">If there were issues with hello deployment, a next step would be toolook at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="fbbdc-170">Meer informatie over hoe toodeploy een virtuele machine en de ondersteunende resources aan de hand van [implementeren van een Azure virtuele Machine met behulp van C#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="fbbdc-170">Learn how toodeploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
