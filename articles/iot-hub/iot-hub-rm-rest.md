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
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a>Een iothub met Hallo resourceprovider REST-API (.NET) maken

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

U kunt Hallo [resourceprovider IoT Hub REST-API] [ lnk-rest-api] toocreate en Azure IoT hubs programmatisch te beheren. Deze zelfstudie leert u hoe toouse Hallo IoT Hub resource provider REST-API toocreate een IoT-hub vanuit een C#-programma.

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md).  In dit artikel bevat informatie over met behulp van hello Azure Resource Manager-implementatiemodel.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Visual Studio 2015 of Visual Studio 2017.
* Een actief Azure-account. <br/>Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.
* [Azure PowerShell 1.0] [ lnk-powershell-install] of hoger.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Visual Studio-project voorbereiden

1. Maak in Visual Studio een Visual C# Classic Windows Desktop-project met Hallo **Console-App (.NET Framework)** projectsjabloon. Naam Hallo project **CreateIoTHubREST**.

2. Klik in Solution Explorer met de rechtermuisknop op uw project en klik vervolgens op **NuGet-pakketten beheren**.

3. Controleer in NuGet Package Manager **Include prerelease**, en op Hallo **Bladeren** pagina zoeken naar **Microsoft.Azure.Management.ResourceManager**. Selecteer Hallo pakket, klikt u op **installeren**in **wijzigingen** klikt u op **OK**, klikt u vervolgens op **ik ga akkoord** tooaccept Hallo licenties.

4. Zoekt u in NuGet Package Manager **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Klik op **installeren**in **wijzigingen** klikt u op **OK**, klikt u vervolgens op **ik ga akkoord** tooaccept Hallo licentie.

5. Vervang in Program.cs Hallo bestaande **met** instructies met Hallo code te volgen:

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

6. Toevoegen in Program.cs Hallo statische variabelen Vervang Hallo tijdelijke aanduiding voor waarden te volgen. U hebt een genoteerd **ApplicationId**, **SubscriptionId**, **TenantId**, en **wachtwoord** eerder in deze zelfstudie. **De naam van resourcegroep** Hallo-naam van resourcegroep Hallo u gebruiken wanneer u Hallo iothub maken. U kunt een reeds bestaande of een nieuwe resourcegroep. **Naam van de IoT Hub** heet Hallo Hallo IoT-Hub die u, zoals maakt **MyIoTHub**. Hallo-naam van uw IoT-hub moet wereldwijd uniek zijn. **Implementatienaam** is een naam voor de implementatie van hello, zoals **Deployment_01**.

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

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a>Hallo resource provider REST-API toocreate een IoT-hub gebruiken

Gebruik Hallo [resourceprovider IoT Hub REST-API] [ lnk-rest-api] toocreate een IoT-hub in de resourcegroep. U kunt ook Hallo resource provider REST-API toomake wijzigingen tooan bestaande IoT-hub.

1. Hallo methode tooProgram.cs volgende toevoegen:

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. Hallo na code toohello toevoegen **CreateIoTHub** methode. Deze code maakt een **HttpClient** object met Hallo-verificatietoken in Hallo headers:

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. Hallo na code toohello toevoegen **CreateIoTHub** methode. Deze code beschrijft Hallo IoT hub toocreate en genereert een JSON-weergave. Zie voor de huidige lijst Hallo van locaties die ondersteuning bieden voor IoT Hub [Azure Status][lnk-status]:

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

4. Hallo na code toohello toevoegen **CreateIoTHub** methode. Deze code verzendt Hallo REST aanvraag tooAzure. Hallo code vervolgens antwoord Hallo controleert en haalt status van de toomonitor Hallo van Hallo implementatie taak kunt u Hallo-URL:

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

5. Toevoegen van de volgende code toohello einde van Hallo Hallo **CreateIoTHub** methode. Deze code gebruikt Hallo **asyncStatusUri** adres in de vorige stap toowait voor Hallo implementatie toocomplete Hallo opgehaald:

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. Toevoegen van de volgende code toohello einde van Hallo Hallo **CreateIoTHub** methode. Deze code haalt Hallo sleutels Hallo iothub die u hebt gemaakt en worden ze toohello console afgedrukt:

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a>Volledige en Voer Hallo-toepassing

U kunt nu de toepassing hello voltooien door de aanroepende Hallo **CreateIoTHub** methode voordat u bouwen en uitvoeren.

1. Toevoegen van de volgende code toohello einde van Hallo Hallo **Main** methode:

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. Klik op **bouwen** en vervolgens **oplossing bouwen**. Eventuele fouten te corrigeren.

3. Klik op **Debug** en vervolgens **foutopsporing starten** toorun Hallo-toepassing. Het kan enkele minuten duren voordat Hallo implementatie toorun.

4. tooverify die uw toepassing toegevoegd Hallo nieuwe iothub, gaat u naar Hallo [Azure-portal] [ lnk-azure-portal] en uw lijst met resources weergeven. Ook gebruiken Hallo **Get-AzureRmResource** PowerShell-cmdlet.

> [!NOTE]
> Deze voorbeeldtoepassing voegt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd. Wanneer u klaar bent, kunt u Hallo IoT-hub via Hallo verwijderen [Azure-portal] [ lnk-azure-portal] of met behulp van Hallo **verwijderen AzureRmResource** PowerShell-cmdlet als u klaar bent.

## <a name="next-steps"></a>Volgende stappen
Nu u een iothub met Hallo resourceprovider REST-API hebt geïmplementeerd, kunt u verder tooexplore:

* Meer informatie over de mogelijkheden van Hallo Hallo [resourceprovider IoT Hub REST-API][lnk-rest-api].
* Lees [overzicht van Azure Resource Manager] [ lnk-azure-rm-overview] toolearn meer over Hallo-mogelijkheden van Azure Resource Manager.

toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo artikelen te volgen:

* [Inleiding tooC SDK][lnk-c-sdk]
* [Azure IoT SDK 's][lnk-sdks]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Een apparaat simuleren met Azure IoT rand][lnk-iotedge]

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
