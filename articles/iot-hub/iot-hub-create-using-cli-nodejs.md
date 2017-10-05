---
title: Maken van een iothub met Azure CLI (azure.js) | Microsoft Docs
description: Het maken van een Azure-IoT-hub met behulp van de platformoverschrijdende Azure CLI (azure.js).
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
ms.openlocfilehash: 5e37c6c5e8625ce446ab203f19f9a8b2f1cd5a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli"></a><span data-ttu-id="61344-103">Een iothub met de Azure CLI maken</span><span class="sxs-lookup"><span data-stu-id="61344-103">Create an IoT hub using the Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="61344-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="61344-104">Introduction</span></span>

<span data-ttu-id="61344-105">U kunt Azure CLI (azure.js) maken en beheren van Azure IoT hubs programmatisch gebruiken.</span><span class="sxs-lookup"><span data-stu-id="61344-105">You can use Azure CLI (azure.js) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="61344-106">In dit artikel leest u hoe de Azure CLI (azure.js) gebruiken om te maken van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="61344-106">This article shows you how to use the Azure CLI (azure.js) to create an IoT hub.</span></span>

<span data-ttu-id="61344-107">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="61344-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="61344-108">Azure CLI (azure.js) – de CLI voor het klassieke en resource management-implementatiemodel zoals beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="61344-108">Azure CLI (azure.js) – the CLI for the classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="61344-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) : de volgende generatie CLI voor de resource management-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="61344-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - the next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="61344-110">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="61344-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="61344-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="61344-111">An active Azure account.</span></span> <span data-ttu-id="61344-112">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="61344-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="61344-113">[Azure CLI 0.10.4] [ lnk-CLI-install] of hoger.</span><span class="sxs-lookup"><span data-stu-id="61344-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="61344-114">Als u de Azure CLI geïnstalleerd hebt, kunt u de huidige versie bij de opdrachtprompt met de volgende opdracht valideren:</span><span class="sxs-lookup"><span data-stu-id="61344-114">If you already have the Azure CLI installed, you can validate the current version at the command prompt with the following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="61344-115">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="61344-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="61344-116">De Azure CLI moet zich in de modus Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="61344-116">The Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="61344-117">Uw Azure-account en -abonnement instellen</span><span class="sxs-lookup"><span data-stu-id="61344-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="61344-118">Bij de opdrachtprompt, aanmelding door de volgende opdracht te typen:</span><span class="sxs-lookup"><span data-stu-id="61344-118">At the command prompt, login by typing the following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="61344-119">De voorgestelde webbrowser en code voor verificatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="61344-119">Use the suggested web browser and code to authenticate.</span></span>
1. <span data-ttu-id="61344-120">Als u meerdere Azure-abonnementen hebt, verleent verbinding maken met Azure u toegang tot alle de Azure-abonnementen die zijn gekoppeld aan uw referenties.</span><span class="sxs-lookup"><span data-stu-id="61344-120">If you have multiple Azure subscriptions, connecting to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="61344-121">U kunt zien die de Azure-abonnementen en bepalen welke is de standaard, met de opdracht:</span><span class="sxs-lookup"><span data-stu-id="61344-121">You can view the Azure subscriptions, and identify which one is the default, using the command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="61344-122">De context van het abonnement waaronder u wilt uitvoeren van de rest van het gebruik van de opdrachten instellen:</span><span class="sxs-lookup"><span data-stu-id="61344-122">To set the subscription context under which you want to run the rest of the commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="61344-123">Als u een resourcegroep niet hebt, kunt u een met de naam **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="61344-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="61344-124">Het artikel [de Azure CLI gebruiken voor het beheren van Azure-resources en resourcegroepen] [ lnk-CLI-arm] vindt u meer informatie over het gebruik van de Azure CLI voor het beheren van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="61344-124">The article [Use the Azure CLI to manage Azure resources and resource groups][lnk-CLI-arm] provides more information about how to use the Azure CLI to manage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="61344-125">Een IoT Hub maken</span><span class="sxs-lookup"><span data-stu-id="61344-125">Create an IoT Hub</span></span>

<span data-ttu-id="61344-126">Vereiste parameters:</span><span class="sxs-lookup"><span data-stu-id="61344-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="61344-127">**resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="61344-127">**resource-group**.</span></span> <span data-ttu-id="61344-128">De naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="61344-128">The resource group name.</span></span> <span data-ttu-id="61344-129">De indeling is niet hoofdlettergevoelig alfanumerieke, onderstrepingstekens en liggende streepjes, 1-64-lengte.</span><span class="sxs-lookup"><span data-stu-id="61344-129">The format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="61344-130">**Naam**.</span><span class="sxs-lookup"><span data-stu-id="61344-130">**name**.</span></span> <span data-ttu-id="61344-131">De naam van de iothub worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="61344-131">The name of the IoT hub to be created.</span></span> <span data-ttu-id="61344-132">De indeling is niet hoofdlettergevoelig alfanumerieke, onderstrepingstekens en liggende streepjes, de lengte 3-50.</span><span class="sxs-lookup"><span data-stu-id="61344-132">The format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="61344-133">**locatie**.</span><span class="sxs-lookup"><span data-stu-id="61344-133">**location**.</span></span> <span data-ttu-id="61344-134">De locatie (azure-regio/datacenter) voor het inrichten van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="61344-134">The location (azure region/datacenter) to provision the IoT hub.</span></span>
* <span data-ttu-id="61344-135">**SKU-naam**.</span><span class="sxs-lookup"><span data-stu-id="61344-135">**sku-name**.</span></span> <span data-ttu-id="61344-136">De naam van de sku, een van: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="61344-136">The name of the sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="61344-137">Raadpleeg de pagina met prijzen voor IoT Hub voor de laatste volledige lijst.</span><span class="sxs-lookup"><span data-stu-id="61344-137">For the latest full list, refer to the pricing page for IoT Hub.</span></span>
* <span data-ttu-id="61344-138">**eenheden**.</span><span class="sxs-lookup"><span data-stu-id="61344-138">**units**.</span></span> <span data-ttu-id="61344-139">Het aantal ingerichte eenheden.</span><span class="sxs-lookup"><span data-stu-id="61344-139">The number of provisioned units.</span></span> <span data-ttu-id="61344-140">-Bereik: F1 [1-1]: S1, S2 [1-200]: [1-10] S3.</span><span class="sxs-lookup"><span data-stu-id="61344-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="61344-141">IoT Hub-eenheden zijn gebaseerd op het totale aantal berichten en het aantal apparaten dat u verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="61344-141">IoT Hub units are based on your total message count and the number of devices you want to connect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="61344-142">Overzicht van de parameters die zijn gemaakt, kunt u de opdracht help in de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="61344-142">To see all the parameters available for creation, you can use the help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="61344-143">Snel voorbeeld: een IoT-Hub maken aangeroepen **exampleIoTHubName** in de resourcegroep **exampleResourceGroup**, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="61344-143">Quick example: To create an IoT Hub called **exampleIoTHubName** in the resource group **exampleResourceGroup**, run the following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="61344-144">Deze opdracht Azure CLI maakt een standaard IoT-Hub van S1, waarvoor u wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="61344-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="61344-145">U kunt de IoT-hub verwijderen **exampleIoTHubName** met volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="61344-145">You can delete the IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="61344-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="61344-146">Next steps</span></span>

<span data-ttu-id="61344-147">Zie het volgende artikel voor meer informatie over het ontwikkelen voor IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="61344-147">To learn more about developing for IoT Hub, see the following article:</span></span>

* <span data-ttu-id="61344-148">[IoT SDK 's][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="61344-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="61344-149">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="61344-149">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="61344-150">[IoT Hub beheren met behulp van de Azure-portal][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="61344-150">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
