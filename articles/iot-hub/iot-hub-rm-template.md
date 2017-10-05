---
title: Maken van een Azure-IoT-Hub met een sjabloon (.NET) | Microsoft Docs
description: Het gebruik van een Azure Resource Manager-sjabloon maken van een IoT Hub met C#-programma.
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
ms.openlocfilehash: 0f197a28e0c51b06d0b47a03c29fe1fde0c6b78d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="6f82f-103">Een iothub met Azure Resource Manager-sjabloon (.NET) maken</span><span class="sxs-lookup"><span data-stu-id="6f82f-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="6f82f-104">Azure Resource Manager kunt u maken en beheren van Azure IoT hubs via een programma.</span><span class="sxs-lookup"><span data-stu-id="6f82f-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="6f82f-105">Deze zelfstudie ziet u het gebruik van een Azure Resource Manager-sjabloon voor een iothub maken vanuit een C#-programma.</span><span class="sxs-lookup"><span data-stu-id="6f82f-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="6f82f-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6f82f-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="6f82f-107">In dit artikel wordt behandeld met het Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6f82f-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="6f82f-108">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="6f82f-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="6f82f-109">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6f82f-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="6f82f-110">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="6f82f-110">An active Azure account.</span></span> <br/><span data-ttu-id="6f82f-111">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="6f82f-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="6f82f-112">Een [Azure Storage-account] [ lnk-storage-account] waarin u uw Azure Resource Manager sjabloonbestanden kunt opslaan.</span><span class="sxs-lookup"><span data-stu-id="6f82f-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="6f82f-113">[Azure PowerShell 1.0] [ lnk-powershell-install] of hoger.</span><span class="sxs-lookup"><span data-stu-id="6f82f-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="6f82f-114">Visual Studio-project voorbereiden</span><span class="sxs-lookup"><span data-stu-id="6f82f-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="6f82f-115">In Visual Studio maakt een Visual C# Classic Windows Desktop-project met de **Console-App (.NET Framework)** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="6f82f-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="6f82f-116">Noem het project **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-116">Name the project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="6f82f-117">Klik in Solution Explorer met de rechtermuisknop op uw project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="6f82f-118">Controleer in NuGet Package Manager **Include prerelease**, en klik op de **Bladeren** pagina zoeken naar **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-118">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="6f82f-119">Selecteer het pakket, klikt u op **installeren**in **wijzigingen** klikt u op **OK**, klikt u vervolgens op **ik ga akkoord** te accepteren van de licenties.</span><span class="sxs-lookup"><span data-stu-id="6f82f-119">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="6f82f-120">Zoekt u in NuGet Package Manager **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="6f82f-121">Klik op **installeren**in **wijzigingen** klikt u op **OK**, klikt u vervolgens op **ik ga akkoord** de licentievoorwaarden accepteren.</span><span class="sxs-lookup"><span data-stu-id="6f82f-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="6f82f-122">Vervang in Program.cs de bestaande **met** instructies met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="6f82f-122">In Program.cs, replace the existing **using** statements with the following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="6f82f-123">Voeg de volgende statische variabelen Vervang de tijdelijke aanduiding voor waarden in Program.cs.</span><span class="sxs-lookup"><span data-stu-id="6f82f-123">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="6f82f-124">U hebt een genoteerd **ApplicationId**, **SubscriptionId**, **TenantId**, en **wachtwoord** eerder in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6f82f-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="6f82f-125">**De naam van uw Azure Storage** is de naam van de Azure Storage-account waar u uw Azure Resource Manager-sjabloonbestanden opslaat.</span><span class="sxs-lookup"><span data-stu-id="6f82f-125">**Your Azure Storage account name** is the name of the Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="6f82f-126">**De naam van resourcegroep** is de naam van de resourcegroep die u bij het maken van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6f82f-126">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="6f82f-127">De naam mag een vooraf bestaande of nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="6f82f-127">The name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="6f82f-128">**Implementatienaam** is een naam voor de implementatie, zoals **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

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

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="6f82f-129">Een sjabloon voor het maken van een IoT-hub te verzenden</span><span class="sxs-lookup"><span data-stu-id="6f82f-129">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="6f82f-130">Gebruik een JSON-sjabloon en de parameter-bestand te maken van een IoT-hub in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="6f82f-130">Use a JSON template and parameter file to create an IoT hub in your resource group.</span></span> <span data-ttu-id="6f82f-131">U kunt ook een Azure Resource Manager-sjabloon gebruiken om een bestaande IoT-hub te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6f82f-131">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="6f82f-132">Klik in Solution Explorer met de rechtermuisknop op uw project, klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="6f82f-133">Toevoegen van een JSON-bestand aangeroepen **template.json** aan uw project.</span><span class="sxs-lookup"><span data-stu-id="6f82f-133">Add a JSON file called **template.json** to your project.</span></span>

2. <span data-ttu-id="6f82f-134">Toevoegen van een standaard iothub en de **VS-Oost** regio, vervang de inhoud van **template.json** met de volgende resourcedefinitie.</span><span class="sxs-lookup"><span data-stu-id="6f82f-134">To add a standard IoT hub to the **East US** region, replace the contents of **template.json** with the following resource definition.</span></span> <span data-ttu-id="6f82f-135">Zie voor de huidige lijst met regio's die ondersteuning bieden voor IoT Hub [Azure Status][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="6f82f-135">For the current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

3. <span data-ttu-id="6f82f-136">Klik in Solution Explorer met de rechtermuisknop op uw project, klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="6f82f-137">Toevoegen van een JSON-bestand aangeroepen **parameters.json** aan uw project.</span><span class="sxs-lookup"><span data-stu-id="6f82f-137">Add a JSON file called **parameters.json** to your project.</span></span>

4. <span data-ttu-id="6f82f-138">Vervang de inhoud van **parameters.json** met de volgende parameterinformatie die een naam voor de nieuwe iothub, zoals ingesteld **{uw initialen} mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-138">Replace the contents of **parameters.json** with the following parameter information that sets a name for the new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="6f82f-139">De naam van de IoT-hub moet wereldwijd uniek zodat deze uw naam of initialen bevatten:</span><span class="sxs-lookup"><span data-stu-id="6f82f-139">The IoT hub name must be globally unique so it should include your name or initials:</span></span>

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

5. <span data-ttu-id="6f82f-140">In **Server Explorer**maakt verbinding met uw Azure-abonnement en maak een zogenaamd in uw Azure Storage-account **sjablonen**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-140">In **Server Explorer**, connect to your Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="6f82f-141">In de **eigenschappen** deelvenster, stelt u de **openbare leestoegang** machtigingen voor de **sjablonen** container **Blob**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-141">In the **Properties** panel, set the **Public Read Access** permissions for the **templates** container to **Blob**.</span></span>

6. <span data-ttu-id="6f82f-142">In **Server Explorer**, met de rechtermuisknop op de **sjablonen** container en klik vervolgens op **weergave Blob-Container**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-142">In **Server Explorer**, right-click on the **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="6f82f-143">Klik op de **Blob uploaden** knop, selecteert u de twee bestanden **parameters.json** en **templates.json**, en klik vervolgens op **Open** voor het uploaden van de JSON-bestanden toe aan de **sjablonen** container.</span><span class="sxs-lookup"><span data-stu-id="6f82f-143">Click the **Upload Blob** button, select the two files, **parameters.json** and **templates.json**, and then click **Open** to upload the JSON files to the **templates** container.</span></span> <span data-ttu-id="6f82f-144">De URL's van de blobs die met de JSON-gegevens zijn:</span><span class="sxs-lookup"><span data-stu-id="6f82f-144">The URLs of the blobs containing the JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="6f82f-145">Voeg de volgende methode toe aan Program.cs:</span><span class="sxs-lookup"><span data-stu-id="6f82f-145">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="6f82f-146">Voeg de volgende code naar de **CreateIoTHub** methode voor het verzenden van de sjabloon en de parameter-bestanden in de Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="6f82f-146">Add the following code to the **CreateIoTHub** method to submit the template and parameter files to the Azure Resource Manager:</span></span>

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

9. <span data-ttu-id="6f82f-147">Voeg de volgende code naar de **CreateIoTHub** methode die de status en de sleutels voor de nieuwe iothub worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="6f82f-147">Add the following code to the **CreateIoTHub** method that displays the status and the keys for the new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed to create iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="6f82f-148">Voltooid en voer de toepassing</span><span class="sxs-lookup"><span data-stu-id="6f82f-148">Complete and run the application</span></span>

<span data-ttu-id="6f82f-149">U kunt de toepassing nu voltooien door het aanroepen van de **CreateIoTHub** methode voordat u bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6f82f-149">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="6f82f-150">Voeg de volgende code toe aan het einde van de **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="6f82f-150">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="6f82f-151">Klik op **bouwen** en vervolgens **oplossing bouwen**.</span><span class="sxs-lookup"><span data-stu-id="6f82f-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="6f82f-152">Eventuele fouten te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="6f82f-152">Correct any errors.</span></span>

3. <span data-ttu-id="6f82f-153">Klik op **Debug** en vervolgens **foutopsporing starten** de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="6f82f-153">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="6f82f-154">Duurt enkele minuten voor de implementatie om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="6f82f-154">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="6f82f-155">Als u wilt controleren of uw toepassing de nieuwe iothub toegevoegd, gaat u naar de [Azure-portal] [ lnk-azure-portal] en uw lijst met resources weergeven.</span><span class="sxs-lookup"><span data-stu-id="6f82f-155">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="6f82f-156">U kunt ook de **Get-AzureRmResource** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6f82f-156">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="6f82f-157">Deze voorbeeldtoepassing voegt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="6f82f-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="6f82f-158">U kunt de IoT-hub via verwijderen de [Azure-portal] [ lnk-azure-portal] of met behulp van de **verwijderen AzureRmResource** PowerShell-cmdlet als u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="6f82f-158">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f82f-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6f82f-159">Next steps</span></span>
<span data-ttu-id="6f82f-160">Nu u een iothub met een Azure Resource Manager-sjabloon met een C#-programma hebt geïmplementeerd, kunt u verder verkennen:</span><span class="sxs-lookup"><span data-stu-id="6f82f-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want to explore further:</span></span>

* <span data-ttu-id="6f82f-161">Meer informatie over de mogelijkheden van de [resourceprovider IoT Hub REST-API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="6f82f-161">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="6f82f-162">Lees [overzicht van Azure Resource Manager] [ lnk-azure-rm-overview] voor meer informatie over de mogelijkheden van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6f82f-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="6f82f-163">Zie de volgende artikelen voor meer informatie over het ontwikkelen voor IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="6f82f-163">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="6f82f-164">[Inleiding tot C-SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="6f82f-164">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="6f82f-165">[Azure IoT SDK 's][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="6f82f-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="6f82f-166">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="6f82f-166">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6f82f-167">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6f82f-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
