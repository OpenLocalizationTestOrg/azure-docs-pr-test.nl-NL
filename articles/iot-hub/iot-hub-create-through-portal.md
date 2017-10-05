---
title: De Azure portal gebruiken voor het maken van een IoT Hub | Microsoft Docs
description: "Informatie over het maken, beheren en verwijderen van Azure IoT hubs via de Azure-portal. Bevat informatie over Prijscategorieën, schaalbaarheid, beveiliging en configuratie-berichten."
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
ms.openlocfilehash: bca7eea5f44bbed3b784b56edaac235161b43e5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-portal"></a><span data-ttu-id="6d750-104">Een iothub met de Azure portal maken</span><span class="sxs-lookup"><span data-stu-id="6d750-104">Create an IoT hub using the Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="6d750-105">Dit artikel wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="6d750-105">This article describes:</span></span>

* <span data-ttu-id="6d750-106">Hoe de IoT Hub-service niet vinden in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6d750-106">How to find the IoT Hub service in the Azure portal.</span></span>
* <span data-ttu-id="6d750-107">Het maken en beheren van IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="6d750-107">How to create and manage IoT hubs.</span></span>

## <a name="where-to-find-the-iot-hub-service"></a><span data-ttu-id="6d750-108">Waar vind ik de IoT Hub-service</span><span class="sxs-lookup"><span data-stu-id="6d750-108">Where to find the IoT Hub service</span></span>

<span data-ttu-id="6d750-109">U vindt de IoT Hub-service in de volgende locaties in de portal:</span><span class="sxs-lookup"><span data-stu-id="6d750-109">You can find the IoT Hub service in the following locations in the portal:</span></span>

* <span data-ttu-id="6d750-110">Kies **+ nieuw**, en kies vervolgens **Internet der dingen**.</span><span class="sxs-lookup"><span data-stu-id="6d750-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="6d750-111">Kies in de Marketplace **Internet der dingen**.</span><span class="sxs-lookup"><span data-stu-id="6d750-111">In the Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="6d750-112">Een IoT Hub maken</span><span class="sxs-lookup"><span data-stu-id="6d750-112">Create an IoT hub</span></span>

<span data-ttu-id="6d750-113">U kunt een iothub met behulp van de volgende manieren maken:</span><span class="sxs-lookup"><span data-stu-id="6d750-113">You can create an IoT hub using the following methods:</span></span>

* <span data-ttu-id="6d750-114">De **+ nieuw** optie opent u de blade die wordt weergegeven in de volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="6d750-114">The **+ New** option opens the blade shown in the following screen shot.</span></span> <span data-ttu-id="6d750-115">De stappen voor het maken van de IoT-hub via deze methode en via de marketplace zijn identiek.</span><span class="sxs-lookup"><span data-stu-id="6d750-115">The steps for creating the IoT hub through this method and through the marketplace are identical.</span></span>
* <span data-ttu-id="6d750-116">Kies in de Marketplace **maken** om de blade wordt weergegeven in de volgende schermopname te openen.</span><span class="sxs-lookup"><span data-stu-id="6d750-116">In the Marketplace, choose **Create** to open the blade shown in the following screen shot.</span></span>

<span data-ttu-id="6d750-117">De volgende secties worden de verschillende stappen voor het maken van een IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="6d750-117">The following sections describe the several steps to create an IoT hub:</span></span>

### <a name="choose-the-name-of-the-iot-hub"></a><span data-ttu-id="6d750-118">Kies de naam van de IoT-hub</span><span class="sxs-lookup"><span data-stu-id="6d750-118">Choose the name of the IoT hub</span></span>

<span data-ttu-id="6d750-119">U moet de IoT-hub naam voor het maken van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6d750-119">To create an IoT hub, you must name the IoT hub.</span></span> <span data-ttu-id="6d750-120">Deze naam moet uniek zijn in alle IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="6d750-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-the-pricing-tier"></a><span data-ttu-id="6d750-121">Kies de prijscategorie</span><span class="sxs-lookup"><span data-stu-id="6d750-121">Choose the pricing tier</span></span>

<span data-ttu-id="6d750-122">U kunt kiezen uit vier lagen: **vrije**, **Standard 1** en **standaard 2**, en **Standard-S3**.</span><span class="sxs-lookup"><span data-stu-id="6d750-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="6d750-123">De gratis categorie kan alleen 500 apparaten zijn verbonden met de iothub en maximaal 8000 berichten per dag.</span><span class="sxs-lookup"><span data-stu-id="6d750-123">The free tier allows only 500 devices to be connected to the IoT hub and up to 8,000 messages per day.</span></span>

<span data-ttu-id="6d750-124">**Standard-S1**: Gebruik de editie S1 voor IoT-oplossingen met een groot aantal apparaten dat elke kleine hoeveelheden gegevens genereren.</span><span class="sxs-lookup"><span data-stu-id="6d750-124">**Standard S1**: Use the S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="6d750-125">Met elke eenheid van de S1-versie kunt u in totaal maximaal 400.000 berichten per dag verzenden voor alle verbonden apparaten.</span><span class="sxs-lookup"><span data-stu-id="6d750-125">Each unit of the S1 edition allows up to 400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="6d750-126">**Standard S2**: S2 versie gebruiken voor de IoT-oplossingen waarin apparaten grote hoeveelheden gegevens worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="6d750-126">**Standard S2**: Use the S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="6d750-127">Elke eenheid van de editie S2 kunt 6 miljoen berichten per dag tussen alle verbonden apparaten.</span><span class="sxs-lookup"><span data-stu-id="6d750-127">Each unit of the S2 edition allows up to 6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="6d750-128">**Standard-S3**: S3 versie gebruiken voor de IoT-oplossingen die grote hoeveelheden gegevens genereren.</span><span class="sxs-lookup"><span data-stu-id="6d750-128">**Standard S3**: Use the S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="6d750-129">Elke eenheid van de editie S3 kunt 300 miljoen berichten per dag tussen alle verbonden apparaten.</span><span class="sxs-lookup"><span data-stu-id="6d750-129">Each unit of the S3 edition allows up to 300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="6d750-130">IoT Hub staat slechts één gratis hub per Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6d750-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="6d750-131">IoT hub-eenheden</span><span class="sxs-lookup"><span data-stu-id="6d750-131">IoT hub units</span></span>

<span data-ttu-id="6d750-132">Het aantal berichten dat is toegestaan per eenheid per dag, is afhankelijk van uw hub prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="6d750-132">The number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="6d750-133">Als u iothub ter ondersteuning van inkomende berichten 700.000, kiest u bijvoorbeeld twee S1 laag eenheden.</span><span class="sxs-lookup"><span data-stu-id="6d750-133">For example, if you want the IoT hub to support ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-to-cloud-partitions-and-resource-group"></a><span data-ttu-id="6d750-134">Apparaat cloud partities en resourcegroep</span><span class="sxs-lookup"><span data-stu-id="6d750-134">Device to cloud partitions and resource group</span></span>

<span data-ttu-id="6d750-135">U kunt het aantal partities voor een IoT-hub kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6d750-135">You can change the number of partitions for an IoT hub.</span></span> <span data-ttu-id="6d750-136">Het aantal partities is 4, u kunt een ander nummer kiezen uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="6d750-136">The default number of partitions is 4, you can choose a different number from the drop-down list.</span></span>

<span data-ttu-id="6d750-137">U hoeft niet expliciet een lege resourcegroep te maken.</span><span class="sxs-lookup"><span data-stu-id="6d750-137">You do not need to explicitly create an empty resource group.</span></span> <span data-ttu-id="6d750-138">Wanneer u een resource maakt, kunt u kiest u een nieuwe maken of een bestaande resourcegroep gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6d750-138">When you create a resource, you can choose either to create a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="6d750-139">Abonnement kiezen</span><span class="sxs-lookup"><span data-stu-id="6d750-139">Choose subscription</span></span>

<span data-ttu-id="6d750-140">Azure IoT Hub worden automatisch de Azure-abonnementen die aan het gebruikersaccount is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="6d750-140">Azure IoT Hub automatically lists the Azure subscriptions the user account is linked to.</span></span> <span data-ttu-id="6d750-141">U kunt de Azure-abonnement om te koppelen van de iothub.</span><span class="sxs-lookup"><span data-stu-id="6d750-141">You can choose the Azure subscription to associate the IoT hub to.</span></span>

### <a name="choose-the-location"></a><span data-ttu-id="6d750-142">Kies de locatie</span><span class="sxs-lookup"><span data-stu-id="6d750-142">Choose the location</span></span>

<span data-ttu-id="6d750-143">De optie locatie bevat een lijst van de regio's waar IoT Hub beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="6d750-143">The location option provides a list of the regions where IoT Hub is available.</span></span>

### <a name="create-the-iot-hub"></a><span data-ttu-id="6d750-144">De IoT-hub maken</span><span class="sxs-lookup"><span data-stu-id="6d750-144">Create the IoT hub</span></span>

<span data-ttu-id="6d750-145">Wanneer alle voorgaande stappen voltooid zijn, kunt u de IoT-hub kunt maken.</span><span class="sxs-lookup"><span data-stu-id="6d750-145">When all previous steps are complete, you can create the IoT hub.</span></span> <span data-ttu-id="6d750-146">Klik op **maken** starten van de back-end-proces voor het maken en implementeren van de iothub met de opties die u hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="6d750-146">Click **Create** to start the back-end process to create and deploy the IoT hub with the options you chose.</span></span>

<span data-ttu-id="6d750-147">Het kan even duren voor het maken van de IoT-hub, omdat het duurt voor de back-end-implementatie uit te voeren op de juiste locatie-servers.</span><span class="sxs-lookup"><span data-stu-id="6d750-147">It can take a few minutes to create the IoT hub as it takes time for the back-end deployment to run on the appropriate location servers.</span></span>

## <a name="change-the-settings-of-the-iot-hub"></a><span data-ttu-id="6d750-148">Wijzig de instellingen van de IoT-hub</span><span class="sxs-lookup"><span data-stu-id="6d750-148">Change the settings of the IoT hub</span></span>

<span data-ttu-id="6d750-149">U kunt de instellingen van een bestaande IoT-hub wijzigen nadat deze is gemaakt op de blade IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6d750-149">You can change the settings of an existing IoT hub after it is created from the IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="6d750-150">**Gedeeld toegangsbeleid**: dit beleid bepaalt de machtigingen voor apparaten en services om te verbinden met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6d750-150">**Shared access policies**: These policies define the permissions for devices and services to connect to IoT Hub.</span></span> <span data-ttu-id="6d750-151">U kunt dit beleid openen door te klikken op **gedeeld toegangsbeleid** onder **algemene**.</span><span class="sxs-lookup"><span data-stu-id="6d750-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="6d750-152">In deze blade kunt u bestaande beleidsregels wijzigen of toevoegen van een nieuw beleid.</span><span class="sxs-lookup"><span data-stu-id="6d750-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="6d750-153">Een beleid maken</span><span class="sxs-lookup"><span data-stu-id="6d750-153">Create a policy</span></span>

* <span data-ttu-id="6d750-154">Klik op **toevoegen** om een blade te openen.</span><span class="sxs-lookup"><span data-stu-id="6d750-154">Click **Add** to open a blade.</span></span> <span data-ttu-id="6d750-155">Hier kunt u de naam van het nieuwe beleid en de machtigingen die u koppelen aan dit beleid, wilt zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="6d750-155">Here you can enter the new policy name and the permissions that you want to associate with this policy, as shown in the following figure:</span></span>

    <span data-ttu-id="6d750-156">Er zijn enkele machtigingen die gekoppeld aan deze gedeelde beleidsregels worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="6d750-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="6d750-157">De **register gelezen** en **register schrijven** beleid verlenen van rechten voor lezen en schrijven in het identiteitsregister.</span><span class="sxs-lookup"><span data-stu-id="6d750-157">The **Registry read** and **Registry write** policies grant read and write access rights to the identity registry.</span></span> <span data-ttu-id="6d750-158">Automatisch kiezen van de optie schrijven, kiest de optie voor lezen.</span><span class="sxs-lookup"><span data-stu-id="6d750-158">Choosing the write option automatically chooses the read option.</span></span>

    <span data-ttu-id="6d750-159">De **Service verbinding** beleid verleent service-eindpunten, zoals toegang tot **ontvangen van apparaat-naar-cloud**.</span><span class="sxs-lookup"><span data-stu-id="6d750-159">The **Service connect** policy grants permission to access service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="6d750-160">De **apparaat verbinding kan maken** beleid verleent machtigingen voor het verzenden en ontvangen van berichten met behulp van de IoT Hub apparaat-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="6d750-160">The **Device connect** policy grants permissions for sending and receiving messages using the IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="6d750-161">Klik op **maken** deze nieuwe beleid aan de bestaande lijst toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6d750-161">Click **Create** to add this newly created policy to the existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="6d750-162">Eindpunten</span><span class="sxs-lookup"><span data-stu-id="6d750-162">Endpoints</span></span>

<span data-ttu-id="6d750-163">Klik op **eindpunten** om weer te geven een lijst met eindpunten voor de IoT-hub die u wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6d750-163">Click **Endpoints** to display a list of endpoints for the IoT hub that you are modifying.</span></span> <span data-ttu-id="6d750-164">Er zijn twee soorten eindpunten: eindpunten die zijn ingebouwd in de IoT-hub en eindpunten die u toevoegt aan de IoT-hub na het maken ervan.</span><span class="sxs-lookup"><span data-stu-id="6d750-164">There are two types of endpoints: endpoints that are built into the IoT hub, and endpoints that you add to the IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="6d750-165">Ingebouwde eindpunten</span><span class="sxs-lookup"><span data-stu-id="6d750-165">Built-in endpoints</span></span>

<span data-ttu-id="6d750-166">Er zijn twee ingebouwde eindpunten: **Cloud naar apparaat feedback** en **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="6d750-166">There are two built-in endpoints: **Cloud to device feedback** and **Events**.</span></span>

* <span data-ttu-id="6d750-167">**Cloud naar apparaat feedback** instellingen: deze instelling heeft twee subsettings: **Cloud naar apparaat TTL** (time-to-live) en **bewaartijd** (in uren) voor de berichten.</span><span class="sxs-lookup"><span data-stu-id="6d750-167">**Cloud to device feedback** settings: This setting has two subsettings: **Cloud to Device TTL** (time-to-live) and **Retention time** (in hours) for the messages.</span></span> <span data-ttu-id="6d750-168">Wanneer uw eerste een iothub maakt, zijn deze instellingen voor beide de standaardwaarde van één uur.</span><span class="sxs-lookup"><span data-stu-id="6d750-168">When your first create an IoT hub, both these settings have the default value of one hour.</span></span> <span data-ttu-id="6d750-169">Deze instellingen aanpassen, gebruikt u de schuifregelaars of typ de waarden.</span><span class="sxs-lookup"><span data-stu-id="6d750-169">To adjust these settings, use the sliders or type the values.</span></span>
* <span data-ttu-id="6d750-170">**Gebeurtenissen** instellingen: deze instelling heeft verschillende subsettings, waarvan sommige alleen-lezen zijn.</span><span class="sxs-lookup"><span data-stu-id="6d750-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="6d750-171">De volgende lijst beschrijft deze instellingen:</span><span class="sxs-lookup"><span data-stu-id="6d750-171">The following list describes these settings:</span></span>

  * <span data-ttu-id="6d750-172">**Partities**: een standaardwaarde is ingesteld wanneer de IoT-hub is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6d750-172">**Partitions**: A default value is set when the IoT hub is created.</span></span> <span data-ttu-id="6d750-173">U kunt het aantal partities via deze instelling wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6d750-173">You can change the number of partitions through this setting.</span></span>

  * <span data-ttu-id="6d750-174">**Event Hub-compatibele naam en een eindpunt**: wanneer de IoT-hub is gemaakt, wordt een Event Hub gemaakt intern mogelijk moet u toegang tot onder bepaalde omstandigheden.</span><span class="sxs-lookup"><span data-stu-id="6d750-174">**Event Hub-compatible name and endpoint**: When the IoT hub is created, an Event Hub is created internally that you may need access to under certain circumstances.</span></span> <span data-ttu-id="6d750-175">De waarden van de Event Hub-compatibele eindpunt en kan niet worden aangepast, maar u kunt deze kopiëren door te klikken op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="6d750-175">You cannot customize the Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="6d750-176">**Bewaartijd**: standaard ingesteld op één dag, maar u kunt wijzigen met behulp van de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="6d750-176">**Retention Time**: Set to one day by default but you can change it using the drop-down list.</span></span> <span data-ttu-id="6d750-177">Deze waarde is in dagen voor de apparaat-naar-cloud-instelling.</span><span class="sxs-lookup"><span data-stu-id="6d750-177">This value is in days for the device-to-cloud setting.</span></span>

  * <span data-ttu-id="6d750-178">**Consumergroepen**: consumergroepen inschakelen meerdere lezers om berichten te lezen onafhankelijk van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6d750-178">**Consumer Groups**: Consumer groups enable multiple readers to read messages independently from the IoT hub.</span></span> <span data-ttu-id="6d750-179">Elke iothub is gemaakt met een standaard consumergroep.</span><span class="sxs-lookup"><span data-stu-id="6d750-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="6d750-180">U kunt echter toevoegen of verwijderen van consumergroepen naar uw IoT-hubs met deze instelling.</span><span class="sxs-lookup"><span data-stu-id="6d750-180">However, you can add or delete consumer groups to your IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6d750-181">De standaardgroep consumer kan niet worden bewerkt of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6d750-181">The default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="6d750-182">Aangepaste eindpunten</span><span class="sxs-lookup"><span data-stu-id="6d750-182">Custom endpoints</span></span>

<span data-ttu-id="6d750-183">U kunt aangepaste eindpunten toevoegen op uw IoT-hub met behulp van de portal.</span><span class="sxs-lookup"><span data-stu-id="6d750-183">You can add custom endpoints on your IoT hub using the portal.</span></span> <span data-ttu-id="6d750-184">Van de **eindpunten** blade, klikt u op **toevoegen** boven openen de **eindpunt toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="6d750-184">From the **Endpoints** blade, click **Add** at the top to open the **Add endpoint** blade.</span></span> <span data-ttu-id="6d750-185">Voer de vereiste gegevens en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d750-185">Enter the required information, then click **OK**.</span></span> <span data-ttu-id="6d750-186">Uw aangepaste eindpunt wordt nu weergegeven in het hoofdvenster **eindpunten** blade.</span><span class="sxs-lookup"><span data-stu-id="6d750-186">Your custom endpoint is now listed in the main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="6d750-187">Meer informatie over aangepaste eindpunten in [referentie - IoT-hubeindpunten][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="6d750-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="6d750-188">Routes</span><span class="sxs-lookup"><span data-stu-id="6d750-188">Routes</span></span>

<span data-ttu-id="6d750-189">Klik op **Routes** beheren hoe IoT Hub verzendt uw apparaat-naar-cloud-berichten.</span><span class="sxs-lookup"><span data-stu-id="6d750-189">Click **Routes** to manage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="6d750-190">U kunt routes toevoegen aan uw IoT-hub door te klikken op **toevoegen** boven aan de **Routes*** blade, voert u de vereiste gegevens en op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d750-190">You can add routes to your IoT hub by clicking **Add** at the top of the **Routes*** blade, entering the required information, and clicking **OK**.</span></span> <span data-ttu-id="6d750-191">De route wordt vervolgens weergegeven in het hoofdvenster **Routes** blade.</span><span class="sxs-lookup"><span data-stu-id="6d750-191">Your route is then listed in the main **Routes** blade.</span></span> <span data-ttu-id="6d750-192">U kunt een route bewerken door erop te klikken in de lijst met routes.</span><span class="sxs-lookup"><span data-stu-id="6d750-192">You can edit a route by clicking it in the list of routes.</span></span> <span data-ttu-id="6d750-193">Om een route, klikt u in de lijst met routes op en stel de **ingeschakeld** in-of uitschakelen op **uit**.</span><span class="sxs-lookup"><span data-stu-id="6d750-193">To enable a route, click it in the list of routes and set the **Enabled** toggle to **Off**.</span></span> <span data-ttu-id="6d750-194">Klik op om de wijziging, **OK** onderaan de blade.</span><span class="sxs-lookup"><span data-stu-id="6d750-194">To save the change, click **OK** at the bottom of the blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="6d750-195">Prijzen en schaal</span><span class="sxs-lookup"><span data-stu-id="6d750-195">Pricing and scale</span></span>

<span data-ttu-id="6d750-196">De prijs van een iothub kan worden gewijzigd via de **prijzen** instellingen met de volgende uitzonderingen:</span><span class="sxs-lookup"><span data-stu-id="6d750-196">The pricing of an existing IoT hub can be changed through the **Pricing** settings, with the following exceptions:</span></span>

* <span data-ttu-id="6d750-197">In de huidige implementatie een iothub met een gratis SKU lagen niet wijzigen in een van de betaalde SKU's, of vice versa.</span><span class="sxs-lookup"><span data-stu-id="6d750-197">In the current implementation, an IoT hub with a free SKU cannot change tiers to one of the paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="6d750-198">Er kan alleen worden één laag gratis IoT-hub in de Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6d750-198">There can only be one free tier IoT hub in the Azure subscription.</span></span>

![][12]

<span data-ttu-id="6d750-199">U kunt verplaatsen van een hogere naar lagere lagen alleen wanneer het aantal berichten die dag het quotum voor de onderste laag overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="6d750-199">You can move from a higher to lower tier only when the number of messages sent that day do exceed the quota for the lower tier.</span></span> <span data-ttu-id="6d750-200">Bijvoorbeeld, als het aantal berichten per dag 400.000 overschrijdt, kan klikt u vervolgens de laag voor de iothub worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6d750-200">For example, if the number of messages per day exceeds 400,000, then the tier for the IoT hub can be changed.</span></span> <span data-ttu-id="6d750-201">Echter, als u naar de laag S1 wijzigt vervolgens de IoT-hub is beperkt voor die dag.</span><span class="sxs-lookup"><span data-stu-id="6d750-201">However, if you change to the S1 tier then the IoT hub is throttled for that day.</span></span>

## <a name="delete-the-iot-hub"></a><span data-ttu-id="6d750-202">Verwijderen van de IoT-hub</span><span class="sxs-lookup"><span data-stu-id="6d750-202">Delete the IoT hub</span></span>

<span data-ttu-id="6d750-203">U kunt bladeren naar de IoT-hub die u verwijderen wilt door te klikken op **Bladeren**, en vervolgens de juiste hub verwijderen te kiezen.</span><span class="sxs-lookup"><span data-stu-id="6d750-203">You can browse to the IoT hub you want to delete by clicking **Browse**, and then choosing the appropriate hub to delete.</span></span> <span data-ttu-id="6d750-204">Als u wilt verwijderen van de IoT-hub, klikt u op de **verwijderen** knop onder de naam van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6d750-204">To delete the IoT hub, click the **Delete** button below the IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d750-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d750-205">Next steps</span></span>

<span data-ttu-id="6d750-206">Volg deze koppelingen voor meer informatie over het beheren van Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="6d750-206">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="6d750-207">[Bulksgewijs IoT-apparaten beheren][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="6d750-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="6d750-208">[IoT Hub metrische gegevens][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="6d750-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="6d750-209">[Bewerkingen controleren][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="6d750-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="6d750-210">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="6d750-210">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6d750-211">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="6d750-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="6d750-212">[Een apparaat simuleren met IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6d750-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="6d750-213">[Beveiligen van uw IoT-oplossing bouwen up][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="6d750-213">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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
