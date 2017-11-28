---
title: aaaUse hello toocreate met Azure portal een IoT Hub | Microsoft Docs
description: "Hoe toocreate, beheren en verwijderen van Azure IoT hubs via hello Azure-portal. Bevat informatie over Prijscategorieën, schaalbaarheid, beveiliging en configuratie-berichten."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a><span data-ttu-id="f0ef8-104">Een iothub met hello Azure-portal maken</span><span class="sxs-lookup"><span data-stu-id="f0ef8-104">Create an IoT hub using hello Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="f0ef8-105">Dit artikel wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="f0ef8-105">This article describes:</span></span>

* <span data-ttu-id="f0ef8-106">Hoe Hallo toofind service IoT Hub in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-106">How toofind hello IoT Hub service in hello Azure portal.</span></span>
* <span data-ttu-id="f0ef8-107">Hoe toocreate en beheren van IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-107">How toocreate and manage IoT hubs.</span></span>

## <a name="where-toofind-hello-iot-hub-service"></a><span data-ttu-id="f0ef8-108">Waar toofind Hallo service IoT Hub</span><span class="sxs-lookup"><span data-stu-id="f0ef8-108">Where toofind hello IoT Hub service</span></span>

<span data-ttu-id="f0ef8-109">U vindt Hallo service IoT Hub in de volgende locaties in de portal Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="f0ef8-109">You can find hello IoT Hub service in hello following locations in hello portal:</span></span>

* <span data-ttu-id="f0ef8-110">Kies **+ nieuw**, en kies vervolgens **Internet der dingen**.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="f0ef8-111">Kies in Hallo Marketplace, **Internet der dingen**.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-111">In hello Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="f0ef8-112">Een IoT Hub maken</span><span class="sxs-lookup"><span data-stu-id="f0ef8-112">Create an IoT hub</span></span>

<span data-ttu-id="f0ef8-113">U kunt een iothub met behulp van de volgende methoden Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="f0ef8-113">You can create an IoT hub using hello following methods:</span></span>

* <span data-ttu-id="f0ef8-114">Hallo **+ nieuw** optie wordt weergegeven in de volgende schermopname Hallo Hallo-blade geopend.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-114">hello **+ New** option opens hello blade shown in hello following screen shot.</span></span> <span data-ttu-id="f0ef8-115">Hallo-stappen voor het maken van IoT-hub Hallo via deze methode en Hallo marketplace zijn identiek.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-115">hello steps for creating hello IoT hub through this method and through hello marketplace are identical.</span></span>
* <span data-ttu-id="f0ef8-116">Kies in Hallo Marketplace, **maken** tooopen Hallo blade wordt weergegeven in de volgende schermopname Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-116">In hello Marketplace, choose **Create** tooopen hello blade shown in hello following screen shot.</span></span>

<span data-ttu-id="f0ef8-117">Hallo volgende secties beschrijven Hallo verschillende stappen toocreate een IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="f0ef8-117">hello following sections describe hello several steps toocreate an IoT hub:</span></span>

### <a name="choose-hello-name-of-hello-iot-hub"></a><span data-ttu-id="f0ef8-118">Kies de naam Hallo van Hallo iothub</span><span class="sxs-lookup"><span data-stu-id="f0ef8-118">Choose hello name of hello IoT hub</span></span>

<span data-ttu-id="f0ef8-119">een IoT-hub toocreate, moet u een naam Hallo IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-119">toocreate an IoT hub, you must name hello IoT hub.</span></span> <span data-ttu-id="f0ef8-120">Deze naam moet uniek zijn in alle IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a><span data-ttu-id="f0ef8-121">Hallo prijscategorie kiezen</span><span class="sxs-lookup"><span data-stu-id="f0ef8-121">Choose hello pricing tier</span></span>

<span data-ttu-id="f0ef8-122">U kunt kiezen uit vier lagen: **vrije**, **Standard 1** en **standaard 2**, en **Standard-S3**.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="f0ef8-123">gratis laag Hallo kan alleen 500 apparaten toobe toohello IoT-hub verbonden en up too8, 000 berichten per dag.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-123">hello free tier allows only 500 devices toobe connected toohello IoT hub and up too8,000 messages per day.</span></span>

<span data-ttu-id="f0ef8-124">**Standard-S1**: gebruik Hallo S1 edition voor IoT-oplossingen met een groot aantal apparaten dat elke kleine hoeveelheden gegevens genereren.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-124">**Standard S1**: Use hello S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="f0ef8-125">Elke eenheid van Hallo S1 edition kunt up too400, 000 berichten per dag op alle verbonden apparaten.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-125">Each unit of hello S1 edition allows up too400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="f0ef8-126">**Standard S2**: gebruik Hallo S2 edition voor op waarin apparaten grote hoeveelheden gegevens genereren IoT-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-126">**Standard S2**: Use hello S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="f0ef8-127">Elke eenheid van Hallo S2 edition kunt up too6 miljoen berichten per dag tussen alle verbonden apparaten.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-127">Each unit of hello S2 edition allows up too6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="f0ef8-128">**Standard-S3**: gebruik Hallo S3 edition voor IoT-oplossingen die grote hoeveelheden gegevens genereren.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-128">**Standard S3**: Use hello S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="f0ef8-129">Elke eenheid van Hallo S3 edition kunt up too300 miljoen berichten per dag tussen alle verbonden apparaten.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-129">Each unit of hello S3 edition allows up too300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="f0ef8-130">IoT Hub staat slechts één gratis hub per Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="f0ef8-131">IoT hub-eenheden</span><span class="sxs-lookup"><span data-stu-id="f0ef8-131">IoT hub units</span></span>

<span data-ttu-id="f0ef8-132">Hallo aantal berichten dat is toegestaan per eenheid per dag, is afhankelijk van uw hub prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-132">hello number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="f0ef8-133">Als u Hallo IoT hub toosupport instroom van 700.000 berichten, kiest u bijvoorbeeld twee S1 laag eenheden.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-133">For example, if you want hello IoT hub toosupport ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-toocloud-partitions-and-resource-group"></a><span data-ttu-id="f0ef8-134">Apparaat toocloud partities en resourcegroep</span><span class="sxs-lookup"><span data-stu-id="f0ef8-134">Device toocloud partitions and resource group</span></span>

<span data-ttu-id="f0ef8-135">U kunt het aantal partities voor een IoT-hub Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-135">You can change hello number of partitions for an IoT hub.</span></span> <span data-ttu-id="f0ef8-136">Hallo standaardaantal partities is 4, u kunt een ander nummer kiezen uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-136">hello default number of partitions is 4, you can choose a different number from hello drop-down list.</span></span>

<span data-ttu-id="f0ef8-137">U hoeft geen tooexplicitly een lege resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-137">You do not need tooexplicitly create an empty resource group.</span></span> <span data-ttu-id="f0ef8-138">Wanneer u een resource maakt, kunt u beide toocreate een nieuwe kiezen of een bestaande resourcegroep gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-138">When you create a resource, you can choose either toocreate a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="f0ef8-139">Abonnement kiezen</span><span class="sxs-lookup"><span data-stu-id="f0ef8-139">Choose subscription</span></span>

<span data-ttu-id="f0ef8-140">Azure IoT Hub automatisch een lijst met hello Azure-abonnementen Hallo-gebruikersaccount is gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-140">Azure IoT Hub automatically lists hello Azure subscriptions hello user account is linked to.</span></span> <span data-ttu-id="f0ef8-141">U kunt hello Azure-abonnement tooassociate Hallo iothub.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-141">You can choose hello Azure subscription tooassociate hello IoT hub to.</span></span>

### <a name="choose-hello-location"></a><span data-ttu-id="f0ef8-142">Hallo locatie kiezen</span><span class="sxs-lookup"><span data-stu-id="f0ef8-142">Choose hello location</span></span>

<span data-ttu-id="f0ef8-143">Hallo locatie optie biedt een lijst met Hallo regio's waar IoT Hub beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-143">hello location option provides a list of hello regions where IoT Hub is available.</span></span>

### <a name="create-hello-iot-hub"></a><span data-ttu-id="f0ef8-144">Hallo iothub maken</span><span class="sxs-lookup"><span data-stu-id="f0ef8-144">Create hello IoT hub</span></span>

<span data-ttu-id="f0ef8-145">Wanneer alle voorgaande stappen voltooid zijn, kunt u Hallo IoT-hub kunt maken.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-145">When all previous steps are complete, you can create hello IoT hub.</span></span> <span data-ttu-id="f0ef8-146">Klik op **maken** toostart Hallo back-endproces toocreate en implementeren van Hallo iothub met Hallo-opties die u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-146">Click **Create** toostart hello back-end process toocreate and deploy hello IoT hub with hello options you chose.</span></span>

<span data-ttu-id="f0ef8-147">Het kan enkele minuten toocreate Hallo IoT-hub duren als het duurt voor Hallo back-end-implementatie toorun op Hallo juiste Locationservers.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-147">It can take a few minutes toocreate hello IoT hub as it takes time for hello back-end deployment toorun on hello appropriate location servers.</span></span>

## <a name="change-hello-settings-of-hello-iot-hub"></a><span data-ttu-id="f0ef8-148">Hallo-instellingen van Hallo iothub wijzigen</span><span class="sxs-lookup"><span data-stu-id="f0ef8-148">Change hello settings of hello IoT hub</span></span>

<span data-ttu-id="f0ef8-149">U kunt Hallo-instellingen van een bestaande IoT-hub wijzigen nadat deze is gemaakt van Hallo blade IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-149">You can change hello settings of an existing IoT hub after it is created from hello IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="f0ef8-150">**Gedeeld toegangsbeleid**: dit beleid definiëren Hallo machtigingen voor apparaten en services tooconnect tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-150">**Shared access policies**: These policies define hello permissions for devices and services tooconnect tooIoT Hub.</span></span> <span data-ttu-id="f0ef8-151">U kunt dit beleid openen door te klikken op **gedeeld toegangsbeleid** onder **algemene**.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="f0ef8-152">In deze blade kunt u bestaande beleidsregels wijzigen of toevoegen van een nieuw beleid.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="f0ef8-153">Een beleid maken</span><span class="sxs-lookup"><span data-stu-id="f0ef8-153">Create a policy</span></span>

* <span data-ttu-id="f0ef8-154">Klik op **toevoegen** tooopen een blade.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-154">Click **Add** tooopen a blade.</span></span> <span data-ttu-id="f0ef8-155">Hier kunt u nieuwe beleidsnaam Hallo en dat het gewenste tooassociate aan dit beleid, zoals wordt weergegeven in de volgende Hallo Hallo machtigingen afbeelding:</span><span class="sxs-lookup"><span data-stu-id="f0ef8-155">Here you can enter hello new policy name and hello permissions that you want tooassociate with this policy, as shown in hello following figure:</span></span>

    <span data-ttu-id="f0ef8-156">Er zijn enkele machtigingen die gekoppeld aan deze gedeelde beleidsregels worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="f0ef8-157">Hallo **register gelezen** en **register schrijven** beleid verlenen lees- en schrijftoegang rechten toohello id-register.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-157">hello **Registry read** and **Registry write** policies grant read and write access rights toohello identity registry.</span></span> <span data-ttu-id="f0ef8-158">Optie Hallo schrijven automatisch kiest Hallo optie lezen.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-158">Choosing hello write option automatically chooses hello read option.</span></span>

    <span data-ttu-id="f0ef8-159">Hallo **Service verbinding** beleid verleent machtiging tooaccess service-eindpunten zoals **ontvangen van apparaat-naar-cloud**.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-159">hello **Service connect** policy grants permission tooaccess service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="f0ef8-160">Hallo **apparaat verbinding kan maken** beleid verleent machtigingen voor het verzenden en ontvangen van berichten met behulp van Hallo IoT Hub apparaat-side '-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-160">hello **Device connect** policy grants permissions for sending and receiving messages using hello IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="f0ef8-161">Klik op **maken** tooadd dit nieuw beleid toohello bestaande lijst gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-161">Click **Create** tooadd this newly created policy toohello existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="f0ef8-162">Eindpunten</span><span class="sxs-lookup"><span data-stu-id="f0ef8-162">Endpoints</span></span>

<span data-ttu-id="f0ef8-163">Klik op **eindpunten** toodisplay een lijst met eindpunten voor Hallo IoT-hub die u wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-163">Click **Endpoints** toodisplay a list of endpoints for hello IoT hub that you are modifying.</span></span> <span data-ttu-id="f0ef8-164">Er zijn twee soorten eindpunten: eindpunten die zijn ingebouwd in Hallo IoT-hub en eindpunten u toohello IoT-hub toevoegen na het maken ervan.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-164">There are two types of endpoints: endpoints that are built into hello IoT hub, and endpoints that you add toohello IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="f0ef8-165">Ingebouwde eindpunten</span><span class="sxs-lookup"><span data-stu-id="f0ef8-165">Built-in endpoints</span></span>

<span data-ttu-id="f0ef8-166">Er zijn twee ingebouwde eindpunten: **toodevice feedback Cloud** en **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-166">There are two built-in endpoints: **Cloud toodevice feedback** and **Events**.</span></span>

* <span data-ttu-id="f0ef8-167">**Cloud toodevice feedback** instellingen: deze instelling heeft twee subsettings: **tooDevice TTL Cloud** (time-to-live) en **bewaartijd** (in uren) voor Hallo-berichten.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-167">**Cloud toodevice feedback** settings: This setting has two subsettings: **Cloud tooDevice TTL** (time-to-live) and **Retention time** (in hours) for hello messages.</span></span> <span data-ttu-id="f0ef8-168">Wanneer uw eerste een iothub maakt, hebben beide deze instellingen standaardwaarde Hallo van één uur.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-168">When your first create an IoT hub, both these settings have hello default value of one hour.</span></span> <span data-ttu-id="f0ef8-169">tooadjust deze instellingen Hallo schuifregelaars gebruiken of typ Hallo waarden.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-169">tooadjust these settings, use hello sliders or type hello values.</span></span>
* <span data-ttu-id="f0ef8-170">**Gebeurtenissen** instellingen: deze instelling heeft verschillende subsettings, waarvan sommige alleen-lezen zijn.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="f0ef8-171">Hallo volgende lijst beschrijft deze instellingen:</span><span class="sxs-lookup"><span data-stu-id="f0ef8-171">hello following list describes these settings:</span></span>

  * <span data-ttu-id="f0ef8-172">**Partities**: een standaardwaarde is ingesteld wanneer Hallo IoT-hub is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-172">**Partitions**: A default value is set when hello IoT hub is created.</span></span> <span data-ttu-id="f0ef8-173">U kunt Hallo aantal partities via deze instelling wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-173">You can change hello number of partitions through this setting.</span></span>

  * <span data-ttu-id="f0ef8-174">**Event Hub-compatibele naam en een eindpunt**: wanneer Hallo IoT-hub is gemaakt, een Event Hub intern wordt gemaakt dat u mogelijk moet toegang hebben tot toounder bepaalde omstandigheden.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-174">**Event Hub-compatible name and endpoint**: When hello IoT hub is created, an Event Hub is created internally that you may need access toounder certain circumstances.</span></span> <span data-ttu-id="f0ef8-175">Hallo Event Hub-compatibele naam en het eindpunt waarden kan niet worden aangepast, maar u kunt deze kopiëren door te klikken op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-175">You cannot customize hello Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="f0ef8-176">**Bewaartijd**: tooone dag standaard ingesteld, maar u kunt met behulp van de vervolgkeuzelijst Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-176">**Retention Time**: Set tooone day by default but you can change it using hello drop-down list.</span></span> <span data-ttu-id="f0ef8-177">Deze waarde is in dagen voor het Hallo-apparaat-naar-cloud-instelling.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-177">This value is in days for hello device-to-cloud setting.</span></span>

  * <span data-ttu-id="f0ef8-178">**Consumergroepen**: consumergroepen meerdere lezers tooread berichten onafhankelijk van de IoT-hub Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-178">**Consumer Groups**: Consumer groups enable multiple readers tooread messages independently from hello IoT hub.</span></span> <span data-ttu-id="f0ef8-179">Elke iothub is gemaakt met een standaard consumergroep.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="f0ef8-180">U kunt echter toevoegen of verwijderen van de consument groepen tooyour IoT hubs die gebruikmaken van deze instelling.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-180">However, you can add or delete consumer groups tooyour IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f0ef8-181">Hallo standaard consumergroep kan niet worden bewerkt of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-181">hello default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="f0ef8-182">Aangepaste eindpunten</span><span class="sxs-lookup"><span data-stu-id="f0ef8-182">Custom endpoints</span></span>

<span data-ttu-id="f0ef8-183">U kunt aangepaste eindpunten toevoegen op uw IoT-hub met Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-183">You can add custom endpoints on your IoT hub using hello portal.</span></span> <span data-ttu-id="f0ef8-184">Van Hallo **eindpunten** blade, klikt u op **toevoegen** op Hallo bovenste tooopen hello **eindpunt toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-184">From hello **Endpoints** blade, click **Add** at hello top tooopen hello **Add endpoint** blade.</span></span> <span data-ttu-id="f0ef8-185">Geef informatie op Hallo vereist en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-185">Enter hello required information, then click **OK**.</span></span> <span data-ttu-id="f0ef8-186">Uw aangepaste eindpunt wordt nu weergegeven in de belangrijkste Hallo **eindpunten** blade.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-186">Your custom endpoint is now listed in hello main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="f0ef8-187">Meer informatie over aangepaste eindpunten in [referentie - IoT-hubeindpunten][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="f0ef8-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="f0ef8-188">Routes</span><span class="sxs-lookup"><span data-stu-id="f0ef8-188">Routes</span></span>

<span data-ttu-id="f0ef8-189">Klik op **Routes** toomanage hoe IoT Hub verzendt uw apparaat-naar-cloud-berichten.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-189">Click **Routes** toomanage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="f0ef8-190">U kunt routes tooyour IoT-hub toevoegen door te klikken op **toevoegen** bovenaan Hallo Hallo **Routes*** blade Hallo vereist gegevens invoeren en op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-190">You can add routes tooyour IoT hub by clicking **Add** at hello top of hello **Routes*** blade, entering hello required information, and clicking **OK**.</span></span> <span data-ttu-id="f0ef8-191">Uw route wordt vervolgens weergegeven in de belangrijkste Hallo **Routes** blade.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-191">Your route is then listed in hello main **Routes** blade.</span></span> <span data-ttu-id="f0ef8-192">U kunt een route door erop te klikken in de lijst met routes Hallo bewerken.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-192">You can edit a route by clicking it in hello list of routes.</span></span> <span data-ttu-id="f0ef8-193">een route tooenable klikt u in de lijst met routes Hallo op en stel Hallo **ingeschakeld** te schakelen**uit**.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-193">tooenable a route, click it in hello list of routes and set hello **Enabled** toggle too**Off**.</span></span> <span data-ttu-id="f0ef8-194">toosave hello wijzigen, klikt u op **OK** Hallo Hallo blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-194">toosave hello change, click **OK** at hello bottom of hello blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="f0ef8-195">Prijzen en schaal</span><span class="sxs-lookup"><span data-stu-id="f0ef8-195">Pricing and scale</span></span>

<span data-ttu-id="f0ef8-196">Hallo prijzen van een iothub kan worden gewijzigd via Hallo **prijzen** instellingen Hello volgende uitzonderingen:</span><span class="sxs-lookup"><span data-stu-id="f0ef8-196">hello pricing of an existing IoT hub can be changed through hello **Pricing** settings, with hello following exceptions:</span></span>

* <span data-ttu-id="f0ef8-197">In de huidige implementatie hello, een iothub met een gratis SKU lagen tooone Hallo betaald SKU's, niet wijzigen of vice versa.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-197">In hello current implementation, an IoT hub with a free SKU cannot change tiers tooone of hello paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="f0ef8-198">Er kan alleen worden één laag gratis IoT-hub in hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-198">There can only be one free tier IoT hub in hello Azure subscription.</span></span>

![][12]

<span data-ttu-id="f0ef8-199">U kunt verplaatsen van een hogere toolower categorie alleen wanneer het aantal berichten die dag Hallo Hallo quotum voor de onderste laag Hallo overschrijden.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-199">You can move from a higher toolower tier only when hello number of messages sent that day do exceed hello quota for hello lower tier.</span></span> <span data-ttu-id="f0ef8-200">Hallo bijvoorbeeld laag voor Hallo IoT hub kan worden gewijzigd op als het aantal berichten per dag Hallo 400.000 overschrijdt, vervolgens.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-200">For example, if hello number of messages per day exceeds 400,000, then hello tier for hello IoT hub can be changed.</span></span> <span data-ttu-id="f0ef8-201">Echter, als u toohello S1 laag wijzigt vervolgens Hallo IoT-hub is beperkt voor die dag.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-201">However, if you change toohello S1 tier then hello IoT hub is throttled for that day.</span></span>

## <a name="delete-hello-iot-hub"></a><span data-ttu-id="f0ef8-202">Hallo IoT-hub verwijderen</span><span class="sxs-lookup"><span data-stu-id="f0ef8-202">Delete hello IoT hub</span></span>

<span data-ttu-id="f0ef8-203">U kunt toohello IoT-hub gewenste toodelete door te klikken op Bladeren **Bladeren**, en vervolgens te kiezen Hallo juiste hub toodelete.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-203">You can browse toohello IoT hub you want toodelete by clicking **Browse**, and then choosing hello appropriate hub toodelete.</span></span> <span data-ttu-id="f0ef8-204">toodelete Hallo IoT-hub, klikt u op Hallo **verwijderen** knop onder naam Hallo IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="f0ef8-204">toodelete hello IoT hub, click hello **Delete** button below hello IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0ef8-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f0ef8-205">Next steps</span></span>

<span data-ttu-id="f0ef8-206">Volg deze koppelingen toolearn meer over het beheren van Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="f0ef8-206">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="f0ef8-207">[Bulksgewijs IoT-apparaten beheren][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="f0ef8-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="f0ef8-208">[IoT Hub metrische gegevens][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="f0ef8-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="f0ef8-209">[Bewerkingen controleren][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="f0ef8-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="f0ef8-210">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="f0ef8-210">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="f0ef8-211">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="f0ef8-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="f0ef8-212">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="f0ef8-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="f0ef8-213">[Uw IoT-oplossing van Hallo gemalen beveiligen][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="f0ef8-213">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
