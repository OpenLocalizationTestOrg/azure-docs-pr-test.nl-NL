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
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a><span data-ttu-id="aaf70-103">Een iothub met behulp van Azure CLI 2.0 Hallo maken</span><span class="sxs-lookup"><span data-stu-id="aaf70-103">Create an IoT hub using hello Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="aaf70-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="aaf70-104">Introduction</span></span>

<span data-ttu-id="aaf70-105">U kunt Azure CLI 2.0 (az.py) toocreate gebruiken en Azure IoT hubs programmatisch te beheren.</span><span class="sxs-lookup"><span data-stu-id="aaf70-105">You can use Azure CLI 2.0 (az.py) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="aaf70-106">Dit artikel laat zien hoe toouse hello Azure CLI 2.0 (az.py) toocreate een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="aaf70-106">This article shows you how toouse hello Azure CLI 2.0 (az.py) toocreate an IoT hub.</span></span>

<span data-ttu-id="aaf70-107">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="aaf70-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="aaf70-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI voor Hallo klassieke en resource management implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="aaf70-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="aaf70-109">Azure CLI 2.0 (az.py) - Hallo volgende generatie CLI voor Hallo resource management-implementatiemodel zoals beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="aaf70-109">Azure CLI 2.0 (az.py) - hello next generation CLI for hello resource management deployment model as described in this article.</span></span>

<span data-ttu-id="aaf70-110">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="aaf70-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="aaf70-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="aaf70-111">An active Azure account.</span></span> <span data-ttu-id="aaf70-112">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="aaf70-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="aaf70-113">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="aaf70-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="aaf70-114">Aanmelden en uw Azure-account instellen</span><span class="sxs-lookup"><span data-stu-id="aaf70-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="aaf70-115">Meld u aan tooyour Azure-account en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="aaf70-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="aaf70-116">Uitvoeren bij de opdrachtprompt Hallo Hallo [aanmelding opdracht][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="aaf70-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="aaf70-117">Volg Hallo instructies tooauthenticate met Hallo code en meld u aan tooyour Azure-account via een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="aaf70-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

2. <span data-ttu-id="aaf70-118">Aanmelden tooAzure verleent u tooall toegang tot Azure-accounts die zijn gekoppeld aan uw referenties in Media Player Hallo als u meerdere Azure-abonnementen hebt.</span><span class="sxs-lookup"><span data-stu-id="aaf70-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="aaf70-119">Gebruik de volgende Hallo [opdracht toolist hello Azure-accounts] [ lnk-az-account-command] beschikbaar voor u toouse:</span><span class="sxs-lookup"><span data-stu-id="aaf70-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="aaf70-120">Gebruik Hallo opdracht tooselect abonnement dat u wilt dat uw IoT-hub-opdrachten toocreate toouse toorun hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="aaf70-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="aaf70-121">U kunt Hallo abonnementsnaam of ID van uitvoer van de vorige opdracht Hallo Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="aaf70-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="aaf70-122">Een IoT Hub maken</span><span class="sxs-lookup"><span data-stu-id="aaf70-122">Create an IoT Hub</span></span>

<span data-ttu-id="aaf70-123">Gebruik hello Azure CLI toocreate een resourcegroep en voeg vervolgens een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="aaf70-123">Use hello Azure CLI toocreate a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="aaf70-124">Wanneer u een IoT-hub maakt, moet u deze in een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="aaf70-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="aaf70-125">Gebruik een bestaande resourcegroep of Voer de volgende Hallo [opdracht toocreate een resourcegroep][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="aaf70-125">Either use an existing resource group, or run hello following [command toocreate a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="aaf70-126">het vorige voorbeeld Hallo maakt Hallo resourcegroep in Hallo locatie VS-West.</span><span class="sxs-lookup"><span data-stu-id="aaf70-126">hello previous example creates hello resource group in hello West US location.</span></span> <span data-ttu-id="aaf70-127">U kunt een lijst met beschikbare locaties weergeven door de opdracht uit te voeren Hallo `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="aaf70-127">You can view a list of available locations by running hello command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="aaf70-128">Voer de volgende Hallo [opdracht toocreate een IoT-hub] [ lnk-az-iot-command] met behulp van een globaal unieke naam voor uw IoT-hub in de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="aaf70-128">Run hello following [command toocreate an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="aaf70-129">Hallo vorige opdracht maakt u een IoT-hub in Hallo S1 prijscategorie waarvoor u wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="aaf70-129">hello previous command creates an IoT hub in hello S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="aaf70-130">Zie voor meer informatie [prijzen van Azure IoT Hub][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="aaf70-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="aaf70-131">Verwijderen van een IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="aaf70-131">Remove an IoT Hub</span></span>

<span data-ttu-id="aaf70-132">U kunt ook hello Azure CLI gebruiken[verwijderen van een afzonderlijke resource][lnk-az-resource-command], zoals een IoT-hub of verwijder een resourcegroep en alle bijbehorende bronnen, met inbegrip van een IoT-hubs.</span><span class="sxs-lookup"><span data-stu-id="aaf70-132">You can use hello Azure CLI too[delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="aaf70-133">toodelete een IoT-hub Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="aaf70-133">toodelete an IoT hub, run hello following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="aaf70-134">toodelete een resourcegroep en alle bijbehorende bronnen, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="aaf70-134">toodelete a resource group and all its resources, run hello following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="aaf70-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aaf70-135">Next steps</span></span>
<span data-ttu-id="aaf70-136">toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aaf70-136">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="aaf70-137">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="aaf70-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="aaf70-138">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="aaf70-138">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="aaf70-139">[Met behulp van hello Azure portal toomanage IoT-Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="aaf70-139">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

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
