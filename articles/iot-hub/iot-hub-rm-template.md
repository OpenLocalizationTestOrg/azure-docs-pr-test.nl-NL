---
title: aaaCreate een Azure-IoT-Hub met een sjabloon (.NET) | Microsoft Docs
description: Hoe toouse een Azure Resource Manager-sjabloon toocreate een IoT Hub met C#-programma.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6140deff3553701f994502fd4a60178f874e27cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="2042c-103">Een iothub met Azure Resource Manager-sjabloon (.NET) maken</span><span class="sxs-lookup"><span data-stu-id="2042c-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="2042c-104">U kunt Azure Resource Manager toocreate gebruiken en Azure IoT hubs programmatisch te beheren.</span><span class="sxs-lookup"><span data-stu-id="2042c-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="2042c-105">Deze zelfstudie leert u hoe toouse een Azure Resource Manager-sjabloon toocreate een IoT-hub vanuit een C#-programma.</span><span class="sxs-lookup"><span data-stu-id="2042c-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="2042c-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2042c-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="2042c-107">In dit artikel bevat informatie over met behulp van hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2042c-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="2042c-108">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="2042c-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="2042c-109">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2042c-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="2042c-110">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="2042c-110">An active Azure account.</span></span> <br/><span data-ttu-id="2042c-111">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="2042c-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="2042c-112">Een [Azure Storage-account] [ lnk-storage-account] waarin u uw Azure Resource Manager sjabloonbestanden kunt opslaan.</span><span class="sxs-lookup"><span data-stu-id="2042c-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="2042c-113">[Azure PowerShell 1.0] [ lnk-powershell-install] of hoger.</span><span class="sxs-lookup"><span data-stu-id="2042c-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="2042c-114">Visual Studio-project voorbereiden</span><span class="sxs-lookup"><span data-stu-id="2042c-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="2042c-115">Maak in Visual Studio een Visual C# Classic Windows Desktop-project met Hallo **Console-App (.NET Framework)** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="2042c-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="2042c-116">Naam Hallo project **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="2042c-116">Name hello project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="2042c-117">Klik in Solution Explorer met de rechtermuisknop op uw project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="2042c-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="2042c-118">Controleer in NuGet Package Manager **Include prerelease**, en op Hallo **Bladeren** pagina zoeken naar **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="2042c-118">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="2042c-119">Selecteer Hallo pakket, klikt u op **installeren**in **wijzigingen** klikt u op **OK**, klikt u vervolgens op **ik ga akkoord** tooaccept Hallo licenties.</span><span class="sxs-lookup"><span data-stu-id="2042c-119">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="2042c-120">Zoekt u in NuGet Package Manager **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="2042c-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="2042c-121">Klik op **installeren**in **wijzigingen** klikt u op **OK**, klikt u vervolgens op **ik ga akkoord** tooaccept Hallo licentie.</span><span class="sxs-lookup"><span data-stu-id="2042c-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="2042c-122">Vervang in Program.cs Hallo bestaande **met** instructies met Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="2042c-122">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="2042c-123">Toevoegen in Program.cs Hallo statische variabelen Vervang Hallo tijdelijke aanduiding voor waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="2042c-123">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="2042c-124">U hebt een genoteerd **ApplicationId**, **SubscriptionId**, **TenantId**, en **wachtwoord** eerder in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2042c-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="2042c-125">**De naam van uw Azure Storage** heet Hallo hello Azure Storage-account waar u uw Azure Resource Manager-sjabloonbestanden opslaat.</span><span class="sxs-lookup"><span data-stu-id="2042c-125">**Your Azure Storage account name** is hello name of hello Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="2042c-126">**De naam van resourcegroep** Hallo-naam van resourcegroep Hallo u gebruiken wanneer u Hallo iothub maken.</span><span class="sxs-lookup"><span data-stu-id="2042c-126">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="2042c-127">Hallo-naam mag een vooraf bestaande of nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2042c-127">hello name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="2042c-128">**Implementatienaam** is een naam voor de implementatie van hello, zoals **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="2042c-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="2042c-129">Een sjabloon toocreate een IoT-hub te verzenden</span><span class="sxs-lookup"><span data-stu-id="2042c-129">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="2042c-130">Gebruik een JSON-sjabloon en de parameter bestand toocreate een IoT-hub in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2042c-130">Use a JSON template and parameter file toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="2042c-131">U kunt ook een Azure Resource Manager sjabloon toomake wijzigingen tooan iothub gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2042c-131">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="2042c-132">Klik in Solution Explorer met de rechtermuisknop op uw project, klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="2042c-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="2042c-133">Toevoegen van een JSON-bestand aangeroepen **template.json** tooyour project.</span><span class="sxs-lookup"><span data-stu-id="2042c-133">Add a JSON file called **template.json** tooyour project.</span></span>

2. <span data-ttu-id="2042c-134">een standaard IoT hub toohello tooadd **VS-Oost** vervangen Hallo inhoud van de regio **template.json** Hello resourcedefinitie te volgen.</span><span class="sxs-lookup"><span data-stu-id="2042c-134">tooadd a standard IoT hub toohello **East US** region, replace hello contents of **template.json** with hello following resource definition.</span></span> <span data-ttu-id="2042c-135">Zie voor Hallo huidige lijst met regio's die ondersteuning bieden voor IoT Hub [Azure Status][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="2042c-135">For hello current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

3. <span data-ttu-id="2042c-136">Klik in Solution Explorer met de rechtermuisknop op uw project, klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="2042c-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="2042c-137">Toevoegen van een JSON-bestand aangeroepen **parameters.json** tooyour project.</span><span class="sxs-lookup"><span data-stu-id="2042c-137">Add a JSON file called **parameters.json** tooyour project.</span></span>

4. <span data-ttu-id="2042c-138">Vervang de inhoud Hallo van **parameters.json** Hello parameterinformatie die een naam voor de nieuwe IoT-hub hello, zoals ingesteld na **{uw initialen} mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="2042c-138">Replace hello contents of **parameters.json** with hello following parameter information that sets a name for hello new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="2042c-139">naam van IoT-hub Hallo moet wereldwijd uniek zodat deze uw naam of initialen bevatten:</span><span class="sxs-lookup"><span data-stu-id="2042c-139">hello IoT hub name must be globally unique so it should include your name or initials:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

5. <span data-ttu-id="2042c-140">In **Server Explorer**verbinding tooyour Azure-abonnement en in uw Azure Storage-account maken een zogenaamd **sjablonen**.</span><span class="sxs-lookup"><span data-stu-id="2042c-140">In **Server Explorer**, connect tooyour Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="2042c-141">In Hallo **eigenschappen** Configuratiescherm, set Hallo **openbare leestoegang** machtigingen voor Hallo **sjablonen** container te**Blob**.</span><span class="sxs-lookup"><span data-stu-id="2042c-141">In hello **Properties** panel, set hello **Public Read Access** permissions for hello **templates** container too**Blob**.</span></span>

6. <span data-ttu-id="2042c-142">In **Server Explorer**, met de rechtermuisknop op Hallo **sjablonen** container en klik vervolgens op **weergave Blob-Container**.</span><span class="sxs-lookup"><span data-stu-id="2042c-142">In **Server Explorer**, right-click on hello **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="2042c-143">Klik op Hallo **Blob uploaden** knop, selecteert u Hallo twee bestanden: **parameters.json** en **templates.json**, en klik vervolgens op **Open** tooupload hello JSON bestanden toohello **sjablonen** container.</span><span class="sxs-lookup"><span data-stu-id="2042c-143">Click hello **Upload Blob** button, select hello two files, **parameters.json** and **templates.json**, and then click **Open** tooupload hello JSON files toohello **templates** container.</span></span> <span data-ttu-id="2042c-144">Hallo-URL's van Hallo blobs met Hallo JSON-gegevens zijn:</span><span class="sxs-lookup"><span data-stu-id="2042c-144">hello URLs of hello blobs containing hello JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="2042c-145">Hallo methode tooProgram.cs volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2042c-145">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="2042c-146">Hallo na code toohello toevoegen **CreateIoTHub** methode toosubmit Hallo sjabloon en de parameterbestanden bestanden toohello Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="2042c-146">Add hello following code toohello **CreateIoTHub** method toosubmit hello template and parameter files toohello Azure Resource Manager:</span></span>

    ```csharp
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```

9. <span data-ttu-id="2042c-147">Hallo na code toohello toevoegen **CreateIoTHub** methode die Hallo status en Hallo sleutels voor Hallo nieuwe iothub worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="2042c-147">Add hello following code toohello **CreateIoTHub** method that displays hello status and hello keys for hello new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="2042c-148">Volledige en Voer Hallo-toepassing</span><span class="sxs-lookup"><span data-stu-id="2042c-148">Complete and run hello application</span></span>

<span data-ttu-id="2042c-149">U kunt nu de toepassing hello voltooien door de aanroepende Hallo **CreateIoTHub** methode voordat u bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2042c-149">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="2042c-150">Toevoegen van de volgende code toohello einde van Hallo Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="2042c-150">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="2042c-151">Klik op **bouwen** en vervolgens **oplossing bouwen**.</span><span class="sxs-lookup"><span data-stu-id="2042c-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="2042c-152">Eventuele fouten te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="2042c-152">Correct any errors.</span></span>

3. <span data-ttu-id="2042c-153">Klik op **Debug** en vervolgens **foutopsporing starten** toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2042c-153">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="2042c-154">Het kan enkele minuten duren voordat Hallo implementatie toorun.</span><span class="sxs-lookup"><span data-stu-id="2042c-154">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="2042c-155">uw toepassing toegevoegd tooverify nieuwe iothub, gaat u naar Hallo Hallo [Azure-portal] [ lnk-azure-portal] en uw lijst met resources weergeven.</span><span class="sxs-lookup"><span data-stu-id="2042c-155">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="2042c-156">Ook gebruiken Hallo **Get-AzureRmResource** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2042c-156">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="2042c-157">Deze voorbeeldtoepassing voegt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="2042c-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="2042c-158">U kunt IoT-hub via Hallo Hallo verwijderen [Azure-portal] [ lnk-azure-portal] of met behulp van Hallo **verwijderen AzureRmResource** PowerShell-cmdlet als u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="2042c-158">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2042c-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2042c-159">Next steps</span></span>
<span data-ttu-id="2042c-160">Nu u een iothub met een Azure Resource Manager-sjabloon met een C#-programma hebt geïmplementeerd, kunt u verder tooexplore:</span><span class="sxs-lookup"><span data-stu-id="2042c-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want tooexplore further:</span></span>

* <span data-ttu-id="2042c-161">Meer informatie over de mogelijkheden van Hallo Hallo [resourceprovider IoT Hub REST-API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="2042c-161">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="2042c-162">Lees [overzicht van Azure Resource Manager] [ lnk-azure-rm-overview] toolearn meer over Hallo-mogelijkheden van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2042c-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="2042c-163">toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2042c-163">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="2042c-164">[Inleiding tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="2042c-164">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="2042c-165">[Azure IoT SDK 's][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="2042c-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="2042c-166">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="2042c-166">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="2042c-167">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="2042c-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
