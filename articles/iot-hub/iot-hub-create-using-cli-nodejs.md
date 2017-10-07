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
# <a name="create-an-iot-hub-using-hello-azure-cli"></a><span data-ttu-id="b5ab8-103">Een iothub met behulp van Azure CLI Hallo maken</span><span class="sxs-lookup"><span data-stu-id="b5ab8-103">Create an IoT hub using hello Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="b5ab8-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="b5ab8-104">Introduction</span></span>

<span data-ttu-id="b5ab8-105">U kunt Azure CLI (azure.js) toocreate gebruiken en Azure IoT hubs programmatisch te beheren.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-105">You can use Azure CLI (azure.js) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="b5ab8-106">Dit artikel laat zien hoe toouse hello Azure CLI (azure.js) toocreate een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-106">This article shows you how toouse hello Azure CLI (azure.js) toocreate an IoT hub.</span></span>

<span data-ttu-id="b5ab8-107">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="b5ab8-108">Azure CLI (azure.js) – Hallo CLI voor klassieke Hallo en resource management implementatiemodellen zoals beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-108">Azure CLI (azure.js) – hello CLI for hello classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="b5ab8-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) -Hallo volgende generatie CLI voor Hallo resource management-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - hello next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="b5ab8-110">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b5ab8-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-111">An active Azure account.</span></span> <span data-ttu-id="b5ab8-112">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="b5ab8-113">[Azure CLI 0.10.4] [ lnk-CLI-install] of hoger.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="b5ab8-114">Als u al hello Azure CLI is geïnstalleerd, kunt u de huidige versie Hallo achter de opdrachtprompt Hallo valideren Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-114">If you already have hello Azure CLI installed, you can validate hello current version at hello command prompt with hello following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="b5ab8-115">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b5ab8-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b5ab8-116">Hello Azure CLI moet zich in de modus Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-116">hello Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="b5ab8-117">Uw Azure-account en -abonnement instellen</span><span class="sxs-lookup"><span data-stu-id="b5ab8-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="b5ab8-118">Bij de opdrachtprompt Hallo Hallo aanmelding door in te voeren opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-118">At hello command prompt, login by typing hello following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="b5ab8-119">Hallo voorgestelde webbrowser en code tooauthenticate gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-119">Use hello suggested web browser and code tooauthenticate.</span></span>
1. <span data-ttu-id="b5ab8-120">Als u meerdere Azure-abonnementen hebt, verbinding maken met tooAzure biedt u toegang tooall hello Azure-abonnementen die zijn gekoppeld aan uw referenties.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-120">If you have multiple Azure subscriptions, connecting tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="b5ab8-121">U kunt bekijken hello Azure-abonnementen en bepalen welke Hallo standaard met Hallo-opdracht is:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-121">You can view hello Azure subscriptions, and identify which one is hello default, using hello command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="b5ab8-122">tooset hello abonnementscontext waarin u wilt dat toorun Hallo rest van Hallo-opdrachten gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-122">tooset hello subscription context under which you want toorun hello rest of hello commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="b5ab8-123">Als u een resourcegroep niet hebt, kunt u een met de naam **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="b5ab8-124">Hallo artikel [hello Azure CLI toomanage Azure gebruiken resources en resourcegroepen] [ lnk-CLI-arm] vindt u meer informatie over hoe toouse hello Azure CLI toomanage Azure resources.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-124">hello article [Use hello Azure CLI toomanage Azure resources and resource groups][lnk-CLI-arm] provides more information about how toouse hello Azure CLI toomanage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="b5ab8-125">Een IoT Hub maken</span><span class="sxs-lookup"><span data-stu-id="b5ab8-125">Create an IoT Hub</span></span>

<span data-ttu-id="b5ab8-126">Vereiste parameters:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="b5ab8-127">**resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-127">**resource-group**.</span></span> <span data-ttu-id="b5ab8-128">Hallo Resourcegroepnaam.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-128">hello resource group name.</span></span> <span data-ttu-id="b5ab8-129">Hallo-indeling is niet hoofdlettergevoelig alfanumerieke, onderstrepingstekens en liggende streepjes, 1-64-lengte.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-129">hello format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="b5ab8-130">**Naam**.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-130">**name**.</span></span> <span data-ttu-id="b5ab8-131">Hallo-naam van Hallo IoT hub toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-131">hello name of hello IoT hub toobe created.</span></span> <span data-ttu-id="b5ab8-132">Hallo-indeling is niet hoofdlettergevoelig alfanumerieke, onderstrepingstekens en liggende streepjes, de lengte 3-50.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-132">hello format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="b5ab8-133">**locatie**.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-133">**location**.</span></span> <span data-ttu-id="b5ab8-134">Hallo locatie (azure-regio/datacenter) tooprovision Hallo IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-134">hello location (azure region/datacenter) tooprovision hello IoT hub.</span></span>
* <span data-ttu-id="b5ab8-135">**SKU-naam**.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-135">**sku-name**.</span></span> <span data-ttu-id="b5ab8-136">Hallo-naam van het Hallo-sku, een van: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="b5ab8-136">hello name of hello sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="b5ab8-137">Raadpleeg voor laatste volledige lijst hello, toohello pagina met prijzen voor IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-137">For hello latest full list, refer toohello pricing page for IoT Hub.</span></span>
* <span data-ttu-id="b5ab8-138">**eenheden**.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-138">**units**.</span></span> <span data-ttu-id="b5ab8-139">Hallo aantal ingerichte eenheden.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-139">hello number of provisioned units.</span></span> <span data-ttu-id="b5ab8-140">-Bereik: F1 [1-1]: S1, S2 [1-200]: [1-10] S3.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="b5ab8-141">IoT Hub-eenheden zijn gebaseerd op uw totale aantal en de Hallo aantal apparaten dat u wilt dat tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-141">IoT Hub units are based on your total message count and hello number of devices you want tooconnect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="b5ab8-142">toosee alle Hallo parameters weer die beschikbaar zijn voor het maken, kunt u opdracht Hallo-help in de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-142">toosee all hello parameters available for creation, you can use hello help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="b5ab8-143">Snel voorbeeld: toocreate aangeroepen voor een IoT-Hub **exampleIoTHubName** in de resourcegroep Hallo **exampleResourceGroup**, voert hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-143">Quick example: toocreate an IoT Hub called **exampleIoTHubName** in hello resource group **exampleResourceGroup**, run hello following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="b5ab8-144">Deze opdracht Azure CLI maakt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="b5ab8-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="b5ab8-145">U kunt verwijderen Hallo IoT-hub **exampleIoTHubName** met volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-145">You can delete hello IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="b5ab8-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b5ab8-146">Next steps</span></span>

<span data-ttu-id="b5ab8-147">toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo volgende artikel:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-147">toolearn more about developing for IoT Hub, see hello following article:</span></span>

* <span data-ttu-id="b5ab8-148">[IoT SDK 's][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="b5ab8-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="b5ab8-149">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="b5ab8-149">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b5ab8-150">[Met behulp van hello Azure portal toomanage IoT-Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="b5ab8-150">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
