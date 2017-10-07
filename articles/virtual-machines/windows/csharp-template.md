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
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a>Een Azure-virtuele Machine met C# en Resource Manager-sjabloon implementeren
Dit artikel ziet u hoe toodeploy met C# om een Azure Resource Manager-sjabloon. Hallo-sjabloon die u maakt implementeert een enkele virtuele machine met Windows Server in een nieuw virtueel netwerk met één subnet.

Zie voor een gedetailleerde beschrijving van de bron van de virtuele machine Hallo [virtuele machines in een Azure Resource Manager-sjabloon](template-description.md). Zie voor meer informatie over alle Hallo resources in een sjabloon [overzicht van Azure Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Het duurt ongeveer 10 minuten toodo deze stappen.

## <a name="create-a-visual-studio-project"></a>Een Visual Studio-project maken

In deze stap maakt ervoor u zorgen dat Visual Studio is geïnstalleerd en u een console-toepassing gebruikt toodeploy Hallo sjabloon maken.

1. Als u nog niet gedaan hebt, installeert u [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Selecteer **.NET-ontwikkeling voor bureaubladen** op Hallo van werkbelastingen pagina en klik vervolgens op **installeren**. In Hallo samenvatting, kunt u zien dat **.NET Framework 4 4.6 ontwikkelingsprogramma's** automatisch voor u is geselecteerd. Als u Visual Studio al hebt geïnstalleerd, kunt u Hallo .NET werkbelasting met behulp van Visual Studio starten Hallo toevoegen.
2. Klik in Visual Studio **bestand** > **nieuw** > **Project**.
3. In **sjablonen** > **Visual C#**, selecteer **Console-App (.NET Framework)**, voer *myDotnetProject* voor Hallo-naam van Hallo-project, selecteer Hallo-locatie van het Hallo-project en klik vervolgens op **OK**.

## <a name="install-hello-packages"></a>Hello-pakketten installeren

NuGet-pakketten zijn Hallo gemakkelijkste manier tooinstall Hallo tapewisselaars moet u toofinish deze stappen. tooget hello bibliotheken die u nodig hebt in Visual Studio, voer deze stappen uit:

1. Klik op **extra** > **Nuget Package Manager**, en klik vervolgens op **Package Manager Console**.
2. Typ deze opdrachten in het Hallo-console:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a>Hallo-bestanden maken

In deze stap maakt u een sjabloonbestand die Hallo resources implementeert en een parameterbestand dat parameter waarden toohello sjabloon. U wordt ook een bestand met autorisatieregels die gebruikte tooperform Azure Resource Manager-bewerkingen.

### <a name="create-hello-template-file"></a>Hallo een sjabloon maken

1. Klik in Solution Explorer met de rechtermuisknop op *myDotnetProject* > **toevoegen** > **Nieuw Item**, en selecteer vervolgens **tekstbestand** in *Visual C# Items*. Bestand met de Hallo *CreateVMTemplate.json*, en klik vervolgens op **toevoegen**.
2. Voeg deze JSON-code toohello-bestand dat u hebt gemaakt:

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

3. Hallo CreateVMTemplate.json bestand opslaan.

### <a name="create-hello-parameters-file"></a>Hallo parameterbestand maken

toospecify waarden voor Hallo Resourceparameters die zijn gedefinieerd in de sjabloon hello, dat u een parameterbestand met Hallo waarden maken.

1. Klik in Solution Explorer met de rechtermuisknop op *myDotnetProject* > **toevoegen** > **Nieuw Item**, en selecteer vervolgens **tekstbestand** in *Visual C# Items*. Bestand met de Hallo *Parameters.json*, en klik vervolgens op **toevoegen**.
2. Voeg deze JSON-code toohello-bestand dat u hebt gemaakt:

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

4. Hallo Parameters.json bestand opslaan.

### <a name="create-hello-authorization-file"></a>Hallo-bestand met autorisatieregels maken

Voordat u een sjabloon implementeren kunt, zorg ervoor dat u toegang tot tooan hebt [Active Directory-service-principal](../../resource-group-authenticate-service-principal.md). Van de service-principal hello, moet u een token voor het verifiëren van aanvragen tooAzure Resource Manager verkrijgen. U moet ook Hallo toepassings-ID en verificatiesleutel Hallo Hallo tenant-ID die u nodig hebt in-bestand met autorisatieregels Hallo vastleggen.

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
4. Instellen van een omgevingsvariabele in Windows met de naam AZURE_AUTH_LOCATION met Hallo volledig pad tooauthorization-bestand dat u hebt gemaakt, bijvoorbeeld Hallo volgende PowerShell-opdracht kan worden gebruikt:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a>Hallo-management-client maken

1. Open het bestand Program.cs Hallo voor Hallo-project dat u hebt gemaakt en voeg vervolgens deze using-instructies toohello bestaande instructies boven aan het Hallo-bestand:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
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

## <a name="create-a-resource-group"></a>Een resourcegroep maken

toospecify waarden voor de toepassing hello, voeg code toohello Main-methode toe:

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a>Een opslagaccount maken

Hallo-sjabloon en de parameters worden van een opslagaccount in Azure geïmplementeerd. In deze stap maakt u Hallo-account maakt en Hallo bestanden uploaden. 

toocreate Hallo account, voeg deze code toohello Main-methode toe:

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

## <a name="deploy-hello-template"></a>Hallo-sjabloon implementeren

Implementeer Hallo sjabloon en parameters van Hallo storage-account dat is gemaakt. 

toodeploy hello sjabloon, voeg deze code toohello Main-methode toe:

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

## <a name="delete-hello-resources"></a>Hallo-resources verwijderen

Omdat u in rekening voor resources die worden gebruikt in Azure gebracht, maar het is altijd raadzaam toodelete bronnen die niet langer nodig zijn. U hoeft niet toodelete elke resource afzonderlijk van een resourcegroep. Verwijder Hallo resourcegroep en alle bijbehorende resources worden automatisch verwijderd. 

toodelete hello resource groep, voegt u deze code toohello Main-methode toe:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

Het moet over vijf minuten duren voordat deze toorun console toepassing volledig van toofinish start. 

1. toorun Hallo-consoletoepassing, klikt u op **Start**.

2. Voordat u op **Enter** toostart verwijderen resources, u kan een paar minuten duren tooverify Hallo maken van Hallo resources in hello Azure-portal. Klik op Hallo implementatie toosee statusinformatie over Hallo-implementatie.

## <a name="next-steps"></a>Volgende stappen
* Als er problemen met de Hallo-implementatie zijn, een volgende stap toolook op zou zijn [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](../../resource-manager-common-deployment-errors.md).
* Meer informatie over hoe toodeploy een virtuele machine en de ondersteunende resources aan de hand van [implementeren van een Azure virtuele Machine met behulp van C#](csharp.md).
