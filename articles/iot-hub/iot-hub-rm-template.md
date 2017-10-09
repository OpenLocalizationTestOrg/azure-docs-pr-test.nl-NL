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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a>Een iothub met Azure Resource Manager-sjabloon (.NET) maken

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

U kunt Azure Resource Manager toocreate gebruiken en Azure IoT hubs programmatisch te beheren. Deze zelfstudie leert u hoe toouse een Azure Resource Manager-sjabloon toocreate een IoT-hub vanuit een C#-programma.

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md).  In dit artikel bevat informatie over met behulp van hello Azure Resource Manager-implementatiemodel.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Visual Studio 2015 of Visual Studio 2017.
* Een actief Azure-account. <br/>Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.
* Een [Azure Storage-account] [ lnk-storage-account] waarin u uw Azure Resource Manager sjabloonbestanden kunt opslaan.
* [Azure PowerShell 1.0] [ lnk-powershell-install] of hoger.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Visual Studio-project voorbereiden

1. Maak in Visual Studio een Visual C# Classic Windows Desktop-project met Hallo **Console-App (.NET Framework)** projectsjabloon. Naam Hallo project **CreateIoTHub**.

2. Klik in Solution Explorer met de rechtermuisknop op uw project en klik vervolgens op **NuGet-pakketten beheren**.

3. Controleer in NuGet Package Manager **Include prerelease**, en op Hallo **Bladeren** pagina zoeken naar **Microsoft.Azure.Management.ResourceManager**. Selecteer Hallo pakket, klikt u op **installeren**in **wijzigingen** klikt u op **OK**, klikt u vervolgens op **ik ga akkoord** tooaccept Hallo licenties.

4. Zoekt u in NuGet Package Manager **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Klik op **installeren**in **wijzigingen** klikt u op **OK**, klikt u vervolgens op **ik ga akkoord** tooaccept Hallo licentie.

5. Vervang in Program.cs Hallo bestaande **met** instructies met Hallo code te volgen:

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. Toevoegen in Program.cs Hallo statische variabelen Vervang Hallo tijdelijke aanduiding voor waarden te volgen. U hebt een genoteerd **ApplicationId**, **SubscriptionId**, **TenantId**, en **wachtwoord** eerder in deze zelfstudie. **De naam van uw Azure Storage** heet Hallo hello Azure Storage-account waar u uw Azure Resource Manager-sjabloonbestanden opslaat. **De naam van resourcegroep** Hallo-naam van resourcegroep Hallo u gebruiken wanneer u Hallo iothub maken. Hallo-naam mag een vooraf bestaande of nieuwe resourcegroep. **Implementatienaam** is een naam voor de implementatie van hello, zoals **Deployment_01**.

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

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Een sjabloon toocreate een IoT-hub te verzenden

Gebruik een JSON-sjabloon en de parameter bestand toocreate een IoT-hub in de resourcegroep. U kunt ook een Azure Resource Manager sjabloon toomake wijzigingen tooan iothub gebruiken.

1. Klik in Solution Explorer met de rechtermuisknop op uw project, klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item**. Toevoegen van een JSON-bestand aangeroepen **template.json** tooyour project.

2. een standaard IoT hub toohello tooadd **VS-Oost** vervangen Hallo inhoud van de regio **template.json** Hello resourcedefinitie te volgen. Zie voor Hallo huidige lijst met regio's die ondersteuning bieden voor IoT Hub [Azure Status][lnk-status]:

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

3. Klik in Solution Explorer met de rechtermuisknop op uw project, klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item**. Toevoegen van een JSON-bestand aangeroepen **parameters.json** tooyour project.

4. Vervang de inhoud Hallo van **parameters.json** Hello parameterinformatie die een naam voor de nieuwe IoT-hub hello, zoals ingesteld na **{uw initialen} mynewiothub**. naam van IoT-hub Hallo moet wereldwijd uniek zodat deze uw naam of initialen bevatten:

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

5. In **Server Explorer**verbinding tooyour Azure-abonnement en in uw Azure Storage-account maken een zogenaamd **sjablonen**. In Hallo **eigenschappen** Configuratiescherm, set Hallo **openbare leestoegang** machtigingen voor Hallo **sjablonen** container te**Blob**.

6. In **Server Explorer**, met de rechtermuisknop op Hallo **sjablonen** container en klik vervolgens op **weergave Blob-Container**. Klik op Hallo **Blob uploaden** knop, selecteert u Hallo twee bestanden: **parameters.json** en **templates.json**, en klik vervolgens op **Open** tooupload hello JSON bestanden toohello **sjablonen** container. Hallo-URL's van Hallo blobs met Hallo JSON-gegevens zijn:

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. Hallo methode tooProgram.cs volgende toevoegen:

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. Hallo na code toohello toevoegen **CreateIoTHub** methode toosubmit Hallo sjabloon en de parameterbestanden bestanden toohello Azure Resource Manager:

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

9. Hallo na code toohello toevoegen **CreateIoTHub** methode die Hallo status en Hallo sleutels voor Hallo nieuwe iothub worden weergegeven:

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a>Volledige en Voer Hallo-toepassing

U kunt nu de toepassing hello voltooien door de aanroepende Hallo **CreateIoTHub** methode voordat u bouwen en uitvoeren.

1. Toevoegen van de volgende code toohello einde van Hallo Hallo **Main** methode:

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. Klik op **bouwen** en vervolgens **oplossing bouwen**. Eventuele fouten te corrigeren.

3. Klik op **Debug** en vervolgens **foutopsporing starten** toorun Hallo-toepassing. Het kan enkele minuten duren voordat Hallo implementatie toorun.

4. uw toepassing toegevoegd tooverify nieuwe iothub, gaat u naar Hallo Hallo [Azure-portal] [ lnk-azure-portal] en uw lijst met resources weergeven. Ook gebruiken Hallo **Get-AzureRmResource** PowerShell-cmdlet.

> [!NOTE]
> Deze voorbeeldtoepassing voegt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd. U kunt IoT-hub via Hallo Hallo verwijderen [Azure-portal] [ lnk-azure-portal] of met behulp van Hallo **verwijderen AzureRmResource** PowerShell-cmdlet als u klaar bent.

## <a name="next-steps"></a>Volgende stappen
Nu u een iothub met een Azure Resource Manager-sjabloon met een C#-programma hebt geïmplementeerd, kunt u verder tooexplore:

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
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
