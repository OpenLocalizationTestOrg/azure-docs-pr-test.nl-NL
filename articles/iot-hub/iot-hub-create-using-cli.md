---
title: aaaCreate een IoT Hub met Azure CLI (az.py) | Microsoft Docs
description: Hoe een Azure IoT hub met toocreate Hallo platformoverschrijdende Azure CLI 2.0 (az.py).
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a>Een iothub met behulp van Azure CLI 2.0 Hallo maken

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Inleiding

U kunt Azure CLI 2.0 (az.py) toocreate gebruiken en Azure IoT hubs programmatisch te beheren. Dit artikel laat zien hoe toouse hello Azure CLI 2.0 (az.py) toocreate een IoT-hub.

U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

* [Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI voor Hallo klassieke en resource management implementatiemodellen.
* Azure CLI 2.0 (az.py) - Hallo volgende generatie CLI voor Hallo resource management-implementatiemodel zoals beschreven in dit artikel.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.
* [Azure CLI 2.0][lnk-CLI-install].

## <a name="sign-in-and-set-your-azure-account"></a>Aanmelden en uw Azure-account instellen

Meld u aan tooyour Azure-account en uw abonnement te selecteren.

1. Uitvoeren bij de opdrachtprompt Hallo Hallo [aanmelding opdracht][lnk-login-command]:
    
    ```azurecli
    az login
    ```

    Volg Hallo instructies tooauthenticate met Hallo code en meld u aan tooyour Azure-account via een webbrowser.

2. Aanmelden tooAzure verleent u tooall toegang tot Azure-accounts die zijn gekoppeld aan uw referenties in Media Player Hallo als u meerdere Azure-abonnementen hebt. Gebruik de volgende Hallo [opdracht toolist hello Azure-accounts] [ lnk-az-account-command] beschikbaar voor u toouse:
    
    ```azurecli
    az account list 
    ```

    Gebruik Hallo opdracht tooselect abonnement dat u wilt dat uw IoT-hub-opdrachten toocreate toouse toorun hello te volgen. U kunt Hallo abonnementsnaam of ID van uitvoer van de vorige opdracht Hallo Hallo gebruiken:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a>Een IoT Hub maken

Gebruik hello Azure CLI toocreate een resourcegroep en voeg vervolgens een IoT-hub.

1. Wanneer u een IoT-hub maakt, moet u deze in een resourcegroep maken. Gebruik een bestaande resourcegroep of Voer de volgende Hallo [opdracht toocreate een resourcegroep][lnk-az-resource-command]:
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > het vorige voorbeeld Hallo maakt Hallo resourcegroep in Hallo locatie VS-West. U kunt een lijst met beschikbare locaties weergeven door de opdracht uit te voeren Hallo `az account list-locations -o table`.
    >
    >

2. Voer de volgende Hallo [opdracht toocreate een IoT-hub] [ lnk-az-iot-command] met behulp van een globaal unieke naam voor uw IoT-hub in de resourcegroep:
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> Hallo vorige opdracht maakt u een IoT-hub in Hallo S1 prijscategorie waarvoor u wordt gefactureerd. Zie voor meer informatie [prijzen van Azure IoT Hub][lnk-iot-pricing].
>
>

## <a name="remove-an-iot-hub"></a>Verwijderen van een IoT-Hub

U kunt ook hello Azure CLI gebruiken[verwijderen van een afzonderlijke resource][lnk-az-resource-command], zoals een IoT-hub of verwijder een resourcegroep en alle bijbehorende bronnen, met inbegrip van een IoT-hubs.

toodelete een IoT-hub Hallo volgende opdracht uitvoeren:

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

toodelete een resourcegroep en alle bijbehorende bronnen, Voer Hallo volgende opdracht:

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo artikelen te volgen:

* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Met behulp van hello Azure portal toomanage IoT-Hub][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
