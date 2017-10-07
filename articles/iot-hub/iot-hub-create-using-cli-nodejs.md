---
title: aaaCreate een iothub met Azure CLI (azure.js) | Microsoft Docs
description: Hoe een Azure IoT hub met toocreate Hallo platformoverschrijdende CLI van Azure (azure.js).
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a>Een iothub met behulp van Azure CLI Hallo maken

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Inleiding

U kunt Azure CLI (azure.js) toocreate gebruiken en Azure IoT hubs programmatisch te beheren. Dit artikel laat zien hoe toouse hello Azure CLI (azure.js) toocreate een IoT-hub.

U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

* Azure CLI (azure.js) – Hallo CLI voor klassieke Hallo en resource management implementatiemodellen zoals beschreven in dit artikel.
* [Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -Hallo volgende generatie CLI voor Hallo resource management-implementatiemodel.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.
* [Azure CLI 0.10.4] [ lnk-CLI-install] of hoger. Als u al hello Azure CLI is geïnstalleerd, kunt u de huidige versie Hallo achter de opdrachtprompt Hallo valideren Hello volgende opdracht:

```azurecli
azure --version
```

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md). Hello Azure CLI moet zich in de modus Azure Resource Manager:
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a>Uw Azure-account en -abonnement instellen

1. Bij de opdrachtprompt Hallo Hallo aanmelding door in te voeren opdracht te volgen:

   ```azurecli
    azure login
   ```

   Hallo voorgestelde webbrowser en code tooauthenticate gebruiken.
1. Als u meerdere Azure-abonnementen hebt, verbinding maken met tooAzure biedt u toegang tooall hello Azure-abonnementen die zijn gekoppeld aan uw referenties. U kunt bekijken hello Azure-abonnementen en bepalen welke Hallo standaard met Hallo-opdracht is:

   ```azurecli
    azure account list
   ```

   tooset hello abonnementscontext waarin u wilt dat toorun Hallo rest van Hallo-opdrachten gebruiken:

   ```azurecli
    azure account set <subscription name>
   ```

1. Als u een resourcegroep niet hebt, kunt u een met de naam **exampleResourceGroup**:

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> Hallo artikel [hello Azure CLI toomanage Azure gebruiken resources en resourcegroepen] [ lnk-CLI-arm] vindt u meer informatie over hoe toouse hello Azure CLI toomanage Azure resources.

## <a name="create-an-iot-hub"></a>Een IoT Hub maken

Vereiste parameters:

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* **resourcegroep**. Hallo Resourcegroepnaam. Hallo-indeling is niet hoofdlettergevoelig alfanumerieke, onderstrepingstekens en liggende streepjes, 1-64-lengte.
* **Naam**. Hallo-naam van Hallo IoT hub toobe gemaakt. Hallo-indeling is niet hoofdlettergevoelig alfanumerieke, onderstrepingstekens en liggende streepjes, de lengte 3-50.
* **locatie**. Hallo locatie (azure-regio/datacenter) tooprovision Hallo IoT-hub.
* **SKU-naam**. Hallo-naam van het Hallo-sku, een van: [F1, S1, S2, S3]. Raadpleeg voor laatste volledige lijst hello, toohello pagina met prijzen voor IoT Hub.
* **eenheden**. Hallo aantal ingerichte eenheden. -Bereik: F1 [1-1]: S1, S2 [1-200]: [1-10] S3. IoT Hub-eenheden zijn gebaseerd op uw totale aantal en de Hallo aantal apparaten dat u wilt dat tooconnect.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

toosee alle Hallo parameters weer die beschikbaar zijn voor het maken, kunt u opdracht Hallo-help in de opdrachtprompt:

```azurecli
azure iothub create -h
```

Snel voorbeeld: toocreate aangeroepen voor een IoT-Hub **exampleIoTHubName** in de resourcegroep Hallo **exampleResourceGroup**, voert hello volgende opdracht:

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> Deze opdracht Azure CLI maakt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd. U kunt verwijderen Hallo IoT-hub **exampleIoTHubName** met volgende opdracht:
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo volgende artikel:

* [IoT SDK 's][lnk-sdks]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Met behulp van hello Azure portal toomanage IoT-Hub][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
