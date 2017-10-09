---
title: een Azure IoT hub met aaaCreate Hallo resourceprovider REST-API | Microsoft Docs
description: Hoe Hallo toouse resource provider REST-API toocreate een IoT-Hub.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 98d240ccce47dec13a255bce28943b40f5354ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a><span data-ttu-id="04dc0-103">Een iothub met Hallo resourceprovider REST-API (.NET) maken</span><span class="sxs-lookup"><span data-stu-id="04dc0-103">Create an IoT hub using hello resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="04dc0-104">U kunt Hallo [resourceprovider IoT Hub REST-API] [ lnk-rest-api] toocreate en Azure IoT hubs programmatisch te beheren.</span><span class="sxs-lookup"><span data-stu-id="04dc0-104">You can use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="04dc0-105">Deze zelfstudie leert u hoe toouse Hallo IoT Hub resource provider REST-API toocreate een IoT-hub vanuit een C#-programma.</span><span class="sxs-lookup"><span data-stu-id="04dc0-105">This tutorial shows you how toouse hello IoT Hub resource provider REST API toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="04dc0-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="04dc0-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="04dc0-107">In dit artikel bevat informatie over met behulp van hello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="04dc0-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="04dc0-108">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="04dc0-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="04dc0-109">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="04dc0-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="04dc0-110">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="04dc0-110">An active Azure account.</span></span> <br/><span data-ttu-id="04dc0-111">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="04dc0-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="04dc0-112">[Azure PowerShell 1.0] [ lnk-powershell-install] of hoger.</span><span class="sxs-lookup"><span data-stu-id="04dc0-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="04dc0-113">Visual Studio-project voorbereiden</span><span class="sxs-lookup"><span data-stu-id="04dc0-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="04dc0-114">Maak in Visual Studio een Visual C# Classic Windows Desktop-project met Hallo **Console-App (.NET Framework)** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="04dc0-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="04dc0-115">Naam Hallo project **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="04dc0-115">Name hello project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="04dc0-116">Klik in Solution Explorer met de rechtermuisknop op uw project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="04dc0-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="04dc0-117">Controleer in NuGet Package Manager **Include prerelease**, en op Hallo **Bladeren** pagina zoeken naar **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="04dc0-117">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="04dc0-118">Selecteer Hallo pakket, klikt u op **installeren**in **wijzigingen** klikt u op **OK**, klikt u vervolgens op **ik ga akkoord** tooaccept Hallo licenties.</span><span class="sxs-lookup"><span data-stu-id="04dc0-118">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="04dc0-119">Zoekt u in NuGet Package Manager **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="04dc0-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="04dc0-120">Klik op **installeren**in **wijzigingen** klikt u op **OK**, klikt u vervolgens op **ik ga akkoord** tooaccept Hallo licentie.</span><span class="sxs-lookup"><span data-stu-id="04dc0-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="04dc0-121">Vervang in Program.cs Hallo bestaande **met** instructies met Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="04dc0-121">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```

6. <span data-ttu-id="04dc0-122">Toevoegen in Program.cs Hallo statische variabelen Vervang Hallo tijdelijke aanduiding voor waarden te volgen.</span><span class="sxs-lookup"><span data-stu-id="04dc0-122">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="04dc0-123">U hebt een genoteerd **ApplicationId**, **SubscriptionId**, **TenantId**, en **wachtwoord** eerder in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="04dc0-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="04dc0-124">**De naam van resourcegroep** Hallo-naam van resourcegroep Hallo u gebruiken wanneer u Hallo iothub maken.</span><span class="sxs-lookup"><span data-stu-id="04dc0-124">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="04dc0-125">U kunt een reeds bestaande of een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="04dc0-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="04dc0-126">**Naam van de IoT Hub** heet Hallo Hallo IoT-Hub die u, zoals maakt **MyIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="04dc0-126">**IoT Hub name** is hello name of hello IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="04dc0-127">Hallo-naam van uw IoT-hub moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="04dc0-127">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="04dc0-128">**Implementatienaam** is een naam voor de implementatie van hello, zoals **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="04dc0-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";

    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```
[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a><span data-ttu-id="04dc0-129">Hallo resource provider REST-API toocreate een IoT-hub gebruiken</span><span class="sxs-lookup"><span data-stu-id="04dc0-129">Use hello resource provider REST API toocreate an IoT hub</span></span>

<span data-ttu-id="04dc0-130">Gebruik Hallo [resourceprovider IoT Hub REST-API] [ lnk-rest-api] toocreate een IoT-hub in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="04dc0-130">Use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="04dc0-131">U kunt ook Hallo resource provider REST-API toomake wijzigingen tooan bestaande IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="04dc0-131">You can also use hello resource provider REST API toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="04dc0-132">Hallo methode tooProgram.cs volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="04dc0-132">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="04dc0-133">Hallo na code toohello toevoegen **CreateIoTHub** methode.</span><span class="sxs-lookup"><span data-stu-id="04dc0-133">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="04dc0-134">Deze code maakt een **HttpClient** object met Hallo-verificatietoken in Hallo headers:</span><span class="sxs-lookup"><span data-stu-id="04dc0-134">This code creates an **HttpClient** object with hello authentication token in hello headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="04dc0-135">Hallo na code toohello toevoegen **CreateIoTHub** methode.</span><span class="sxs-lookup"><span data-stu-id="04dc0-135">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="04dc0-136">Deze code beschrijft Hallo IoT hub toocreate en genereert een JSON-weergave.</span><span class="sxs-lookup"><span data-stu-id="04dc0-136">This code describes hello IoT hub toocreate and generates a JSON representation.</span></span> <span data-ttu-id="04dc0-137">Zie voor de huidige lijst Hallo van locaties die ondersteuning bieden voor IoT Hub [Azure Status][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="04dc0-137">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

    ```csharp
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };

    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. <span data-ttu-id="04dc0-138">Hallo na code toohello toevoegen **CreateIoTHub** methode.</span><span class="sxs-lookup"><span data-stu-id="04dc0-138">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="04dc0-139">Deze code verzendt Hallo REST aanvraag tooAzure.</span><span class="sxs-lookup"><span data-stu-id="04dc0-139">This code submits hello REST request tooAzure.</span></span> <span data-ttu-id="04dc0-140">Hallo code vervolgens antwoord Hallo controleert en haalt status van de toomonitor Hallo van Hallo implementatie taak kunt u Hallo-URL:</span><span class="sxs-lookup"><span data-stu-id="04dc0-140">hello code then checks hello response and retrieves hello URL you can use toomonitor hello state of hello deployment task:</span></span>

    ```csharp
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;

    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }

    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. <span data-ttu-id="04dc0-141">Toevoegen van de volgende code toohello einde van Hallo Hallo **CreateIoTHub** methode.</span><span class="sxs-lookup"><span data-stu-id="04dc0-141">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="04dc0-142">Deze code gebruikt Hallo **asyncStatusUri** adres in de vorige stap toowait voor Hallo implementatie toocomplete Hallo opgehaald:</span><span class="sxs-lookup"><span data-stu-id="04dc0-142">This code uses hello **asyncStatusUri** address retrieved in hello previous step toowait for hello deployment toocomplete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="04dc0-143">Toevoegen van de volgende code toohello einde van Hallo Hallo **CreateIoTHub** methode.</span><span class="sxs-lookup"><span data-stu-id="04dc0-143">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="04dc0-144">Deze code haalt Hallo sleutels Hallo iothub die u hebt gemaakt en worden ze toohello console afgedrukt:</span><span class="sxs-lookup"><span data-stu-id="04dc0-144">This code retrieves hello keys of hello IoT hub you created and prints them toohello console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="04dc0-145">Volledige en Voer Hallo-toepassing</span><span class="sxs-lookup"><span data-stu-id="04dc0-145">Complete and run hello application</span></span>

<span data-ttu-id="04dc0-146">U kunt nu de toepassing hello voltooien door de aanroepende Hallo **CreateIoTHub** methode voordat u bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="04dc0-146">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="04dc0-147">Toevoegen van de volgende code toohello einde van Hallo Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="04dc0-147">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="04dc0-148">Klik op **bouwen** en vervolgens **oplossing bouwen**.</span><span class="sxs-lookup"><span data-stu-id="04dc0-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="04dc0-149">Eventuele fouten te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="04dc0-149">Correct any errors.</span></span>

3. <span data-ttu-id="04dc0-150">Klik op **Debug** en vervolgens **foutopsporing starten** toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="04dc0-150">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="04dc0-151">Het kan enkele minuten duren voordat Hallo implementatie toorun.</span><span class="sxs-lookup"><span data-stu-id="04dc0-151">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="04dc0-152">tooverify die uw toepassing toegevoegd Hallo nieuwe iothub, gaat u naar Hallo [Azure-portal] [ lnk-azure-portal] en uw lijst met resources weergeven.</span><span class="sxs-lookup"><span data-stu-id="04dc0-152">tooverify that your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="04dc0-153">Ook gebruiken Hallo **Get-AzureRmResource** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="04dc0-153">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="04dc0-154">Deze voorbeeldtoepassing voegt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="04dc0-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="04dc0-155">Wanneer u klaar bent, kunt u Hallo IoT-hub via Hallo verwijderen [Azure-portal] [ lnk-azure-portal] of met behulp van Hallo **verwijderen AzureRmResource** PowerShell-cmdlet als u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="04dc0-155">When you are finished, you can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04dc0-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="04dc0-156">Next steps</span></span>
<span data-ttu-id="04dc0-157">Nu u een iothub met Hallo resourceprovider REST-API hebt geïmplementeerd, kunt u verder tooexplore:</span><span class="sxs-lookup"><span data-stu-id="04dc0-157">Now you have deployed an IoT hub using hello resource provider REST API, you may want tooexplore further:</span></span>

* <span data-ttu-id="04dc0-158">Meer informatie over de mogelijkheden van Hallo Hallo [resourceprovider IoT Hub REST-API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="04dc0-158">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="04dc0-159">Lees [overzicht van Azure Resource Manager] [ lnk-azure-rm-overview] toolearn meer over Hallo-mogelijkheden van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="04dc0-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="04dc0-160">toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="04dc0-160">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="04dc0-161">[Inleiding tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="04dc0-161">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="04dc0-162">[Azure IoT SDK 's][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="04dc0-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="04dc0-163">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="04dc0-163">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="04dc0-164">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="04dc0-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
