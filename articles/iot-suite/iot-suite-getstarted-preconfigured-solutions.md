---
title: Aan de slag met vooraf geconfigureerde oplossingen | Microsoft Docs
description: Volg deze zelfstudie voor meer informatie over het implementeren van een vooraf geconfigureerde Azure IoT Suite-oplossing.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 466825ab78a5ac9773d8beff69cca90ff9db6c01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-preconfigured-solutions"></a><span data-ttu-id="cb0b0-103">Aan de slag met vooraf geconfigureerde oplossingen</span><span class="sxs-lookup"><span data-stu-id="cb0b0-103">Get started with the preconfigured solutions</span></span>

<span data-ttu-id="cb0b0-104">[Vooraf geconfigureerde oplossingen][lnk-preconfigured-solutions] voor Azure IoT Suite zijn voorzien van meerdere Azure IoT-services om totaaloplossingen te leveren voor het implementeren van algemene IoT-bedrijfsscenario's.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="cb0b0-105">De vooraf geconfigureerde oplossing *externe controle* maakt verbinding met en controleert uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-105">The *remote monitoring* preconfigured solution connects to and monitors your devices.</span></span> <span data-ttu-id="cb0b0-106">U kunt deze oplossing gebruiken om de datastroom van uw apparaten te analyseren en de bedrijfsresultaten te verbeteren door processen automatisch te laten reageren op die datastroom.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-106">You can use the solution to analyze the stream of data from your devices and to improve business outcomes by making processes respond automatically to that stream of data.</span></span>

<span data-ttu-id="cb0b0-107">In deze zelfstudie leert u hoe de vooraf geconfigureerde oplossing voor externe controle inricht.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-107">This tutorial shows you how to provision the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="cb0b0-108">Hierbij maakt u ook kennis met de basisfuncties van de vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="cb0b0-109">U hebt toegang tot veel van deze functies via het *oplossingsdashboard* dat als onderdeel van de vooraf geconfigureerde oplossing wordt geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Vooraf geconfigureerd oplossingsdashboard voor externe controle][img-dashboard]

<span data-ttu-id="cb0b0-111">U hebt een actief Azure-abonnement nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="cb0b0-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cb0b0-113">Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="cb0b0-114">Overzicht van scenario's</span><span class="sxs-lookup"><span data-stu-id="cb0b0-114">Scenario overview</span></span>

<span data-ttu-id="cb0b0-115">Wanneer u de vooraf geconfigureerde oplossing voor externe bewaking implementeert, wordt deze vooraf ingevuld met de resources waarmee u een algemeen scenario voor externe controle kunt doorlopen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-115">When you deploy the remote monitoring preconfigured solution, it is prepopulated with resources that enable you to step through a common remote monitoring scenario.</span></span> <span data-ttu-id="cb0b0-116">In dit scenario melden verschillende apparaten die met de oplossing zijn verbonden, onverwachte temperatuurwaarden.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-116">In this scenario, several devices connected to the solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="cb0b0-117">De volgende gedeelten laten u zien hoe u:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-117">The following sections show you how to:</span></span>

* <span data-ttu-id="cb0b0-118">De apparaten die de onverwachte temperatuurwaarden melden, kunt identificeren.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-118">Identify the devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="cb0b0-119">Deze apparaten kunt configureren, zodat ze gedetailleerdere telemetrie verzenden.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-119">Configure these devices to send more detailed telemetry.</span></span>
* <span data-ttu-id="cb0b0-120">Het probleem kunt oplossen door de firmware op deze apparaten bij te werken.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-120">Fix the problem by updating the firmware on these devices.</span></span>
* <span data-ttu-id="cb0b0-121">Kunt controleren of uw actie het probleem heeft opgelost.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-121">Verify that your action has resolved the issue.</span></span>

<span data-ttu-id="cb0b0-122">Een belangrijke functie van dit scenario is dat u al deze acties extern kunt uitvoeren vanuit het dashboard van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-122">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="cb0b0-123">U hebt geen fysieke toegang tot de apparaten nodig.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-123">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="cb0b0-124">Het oplossingsdashboard bekijken</span><span class="sxs-lookup"><span data-stu-id="cb0b0-124">View the solution dashboard</span></span>

<span data-ttu-id="cb0b0-125">Vanaf het dashboard van de oplossing kunt u de geïmplementeerde oplossing beheren.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-125">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="cb0b0-126">U kunt er bijvoorbeeld telemetrie weergeven, apparaten toevoegen en regels configureren.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="cb0b0-127">Wanneer het inrichten is voltooid en voor de tegel voor uw vooraf geconfigureerde oplossing de status **Gereed** wordt weergegeven, kiest u **Starten** om uw oplossingsportal voor externe controle te openen op een nieuw tabblad.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-127">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![De vooraf geconfigureerde oplossing starten][img-launch-solution]

1. <span data-ttu-id="cb0b0-129">Standaard ziet u in de oplossingsportal het *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-129">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="cb0b0-130">U kunt navigeren naar andere gebieden van de portal van de oplossing met het menu aan de linkerkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-130">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Vooraf geconfigureerd oplossingsdashboard voor externe controle][img-menu]

<span data-ttu-id="cb0b0-132">Het dashboard bevat de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-132">The dashboard displays the following information:</span></span>

* <span data-ttu-id="cb0b0-133">Een kaart die de locatie aangeeft van elk apparaat dat met de oplossing is verbonden.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-133">A map that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="cb0b0-134">Wanneer u de oplossing voor het eerst uitvoert, zijn er 25 gesimuleerde apparaten.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-134">When you first run the solution, there are 25 simulated devices.</span></span> <span data-ttu-id="cb0b0-135">De gesimuleerde apparaten worden geïmplementeerd als Azure WebJobs en de oplossing gebruikt de API van Bing Kaarten om informatie op de kaart te tekenen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-135">The simulated devices are implemented as Azure WebJobs, and the solution uses the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="cb0b0-136">Zie de [Veelgestelde vragen][lnk-faq] voor meer informatie over hoe u de kaart dynamisch kunt maken.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-136">See the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="cb0b0-137">Een deelvenster **Telemetriegeschiedenis** dat de vochtigheids- en temperatuurtelemetrie van een geselecteerd apparaat in bijna realtime tekent en statistische gegevens weergeeft, zoals de maximale, minimale en gemiddelde vochtigheid.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="cb0b0-138">Een deelvenster **Geschiedenis van waarschuwingen** dat recente waarschuwingsgebeurtenissen toont wanneer voor een telemetriewaarde een drempelwaarde wordt overschreden.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="cb0b0-139">Naast de voorbeelden die met de vooraf geconfigureerde oplossing zijn gemaakt, kunt u ook uw eigen alarmen definiëren.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-139">You can define your own alarms in addition to the examples created by the preconfigured solution.</span></span>
* <span data-ttu-id="cb0b0-140">Een deelvenster **Taken** dat informatie weergeeft over geplande taken.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="cb0b0-141">U kunt uw eigen taken plannen op de pagina **Beheertaken**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="cb0b0-142">Waarschuwingen weergeven</span><span class="sxs-lookup"><span data-stu-id="cb0b0-142">View alarms</span></span>

<span data-ttu-id="cb0b0-143">Het deelvenster Waarschuwingsgeschiedenis laat u zien dat vijf apparaten telemetriewaarden melden die hoger zijn dan verwacht.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-143">The alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Waarschuwingsgeschiedenistaken op het dashboard van de oplossing][img-alarms]

> [!NOTE]
> <span data-ttu-id="cb0b0-145">Deze waarschuwingen worden gegenereerd door een regel die is opgenomen in de vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-145">These alarms are generated by a rule that is included in the preconfigured solution.</span></span> <span data-ttu-id="cb0b0-146">Deze regel genereert een waarschuwing als de temperatuurwaarde die door een apparaat is verzonden, groter is dan 60.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-146">This rule generates an alert when the temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="cb0b0-147">U kunt uw eigen regels en acties definiëren door [Regels](#add-a-rule) en [Acties](#add-an-action) te kiezen in het menu aan de linkerzijde.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in the left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="cb0b0-148">Apparaten weergeven</span><span class="sxs-lookup"><span data-stu-id="cb0b0-148">View devices</span></span>

<span data-ttu-id="cb0b0-149">De *Apparatenlijst* bevat alle geregistreerde apparaten in de oplossing.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-149">The *devices* list shows all the registered devices in the solution.</span></span> <span data-ttu-id="cb0b0-150">Uit de apparatenlijst kunt u metagegevens voor apparaten weergeven en bewerken, apparaten toevoegen of verwijderen en methoden aanroepen op apparaten.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-150">From the device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="cb0b0-151">U kunt de apparatenlijst filteren en sorteren.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-151">You can filter and sort the list of devices in the device list.</span></span> <span data-ttu-id="cb0b0-152">U kunt ook de weergave van de kolommen in de apparatenlijst aanpassen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-152">You can also customize the columns shown in the device list.</span></span>

1. <span data-ttu-id="cb0b0-153">Kies **Apparaten** om de apparatenlijst voor deze oplossing weer te geven.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-153">Choose **Devices** to show the device list for this solution.</span></span>

   ![De apparatenlijst weergeven in de portal van de oplossing][img-devicelist]

1. <span data-ttu-id="cb0b0-155">De apparatenlijst geeft eerst aan dat bij het inrichtingsproces 25 gesimuleerde apparaten zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-155">The device list initially shows 25 simulated devices created by the provisioning process.</span></span> <span data-ttu-id="cb0b0-156">U kunt extra gesimuleerde en fysieke apparaten aan de oplossing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-156">You can add additional simulated and physical devices to the solution.</span></span>

1. <span data-ttu-id="cb0b0-157">Kies in de lijst een apparaat om de details ervan weer te geven.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-157">To view the details of a device, choose a device in the device list.</span></span>

   ![De details van een apparaat weergeven in de portal van de oplossing][img-devicedetails]

<span data-ttu-id="cb0b0-159">Het deelvenster **Apparaatdetails** bevat zes gedeeltes:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-159">The **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="cb0b0-160">Een verzameling van koppelingen waarmee u het apparaatpictogram kunt aanpassen, het apparaat kunt uitschakelen, een regel kunt toevoegen, een methode kunt aanroepen of een opdracht kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-160">A collection of links that enable you to customize the device icon, disable the device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="cb0b0-161">Zie [Cloud-to-device communications guidance][lnk-c2d-guidance] (Richtlijnen voor communicatie tussen cloud en apparaat) voor een vergelijking van opdrachten (berichten van apparaat naar cloud) en methoden (directe methoden).</span><span class="sxs-lookup"><span data-stu-id="cb0b0-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="cb0b0-162">In het gedeelte **Apparaatdubbel - Tags** kunt u tagwaarden voor het apparaat bewerken.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-162">The **Device Twin - Tags** section enables you to edit tag values for the device.</span></span> <span data-ttu-id="cb0b0-163">U kunt tagwaarden in de apparatenlijst weergeven en tagwaarden gebruiken om de apparatenlijst te filteren.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-163">You can display tag values in the device list and use tag values to filter the device list.</span></span>
* <span data-ttu-id="cb0b0-164">In het gedeelte **Apparaatdubbel - Gewenste eigenschappen** kunt u eigenschapswaarden instellen die moeten worden verzonden naar het apparaat.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-164">The **Device Twin - Desired Properties** section enables you to set property values to be sent to the device.</span></span>
* <span data-ttu-id="cb0b0-165">Het gedeelte **Apparaatdubbel - Gerapporteerde eigenschappen** geeft eigenschapswaarden weer die vanaf het apparaat worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-165">The **Device Twin - Reported Properties** section shows property values sent from the device.</span></span>
* <span data-ttu-id="cb0b0-166">Het gedeelte **Apparaateigenschappen** geeft informatie weer vanuit het identiteitsregister, zoals het apparaat-id en de verificatiesleutels.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-166">The **Device Properties** section shows information from the identity registry such as the device id and authentication keys.</span></span>
* <span data-ttu-id="cb0b0-167">Het gedeelte **Recente taken** geeft informatie weer over taken die onlangs op dit apparaat zijn gericht.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-167">The **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-the-device-list"></a><span data-ttu-id="cb0b0-168">De apparatenlijst filteren</span><span class="sxs-lookup"><span data-stu-id="cb0b0-168">Filter the device list</span></span>

<span data-ttu-id="cb0b0-169">U kunt een filter gebruiken om alleen de apparaten weer te geven die onverwachte temperatuurwaarden verzenden.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-169">You can use a filter to display only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="cb0b0-170">De vooraf geconfigureerde oplossing voor externe bewaking bevat het filter **Beschadigde apparaten** om apparaten weer te geven met een gemiddelde temperatuurwaarde die groter is dan 60.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-170">The remote monitoring preconfigured solution includes the **Unhealthy devices** filter to show devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="cb0b0-171">U kunt ook [uw eigen filters maken](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="cb0b0-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="cb0b0-172">Kies **Opgeslagen filter openen** om een lijst met beschikbare filters weer te geven.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-172">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="cb0b0-173">Kies vervolgens **Beschadigde apparaten** om het filter toe te passen:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-173">Then choose **Unhealthy devices** to apply the filter:</span></span>

    ![De lijst met filters weergeven][img-unhealthy-filter]

1. <span data-ttu-id="cb0b0-175">De apparatenlijst geeft nu alleen apparaten weer met een gemiddelde temperatuurwaarde die groter is dan 60.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-175">The device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![De gefilterde apparatenlijst met beschadigde apparaten weergeven][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="cb0b0-177">Gewenste eigenschappen bijwerken</span><span class="sxs-lookup"><span data-stu-id="cb0b0-177">Update desired properties</span></span>

<span data-ttu-id="cb0b0-178">U hebt nu een set apparaten geïdentificeerd die mogelijk moeten worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="cb0b0-179">U besluit echter dat de gegevensfrequentie van 15 seconden niet voldoende is voor een duidelijke diagnose van het probleem.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-179">However, you decide that the data frequency of 15 seconds is not sufficient for a clear diagnosis of the issue.</span></span> <span data-ttu-id="cb0b0-180">Als u de telemetrische frequentie wijzigt in vijf seconden, hebt u meer gegevenspunten waarmee u het probleem beter kunt vaststellen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-180">Changing the telemetry frequency to five seconds to provide you with more data points to better diagnose the issue.</span></span> <span data-ttu-id="cb0b0-181">U kunt deze configuratiewijziging pushen naar uw externe apparaten vanuit de portal van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-181">You can push this configuration change to your remote devices from the solution portal.</span></span> <span data-ttu-id="cb0b0-182">U kunt de wijziging eenmaal doorvoeren, de impact controleren en vervolgens actie ondernemen op de resultaten.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-182">You can make the change once, evaluate the impact, and then act on the results.</span></span>

<span data-ttu-id="cb0b0-183">Volg deze stappen voor het uitvoeren van een taak die de gewenste eigenschap **TelemetryInterval** voor de betreffende apparaten wijzigt.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-183">Follow these steps to run a job that changes the **TelemetryInterval** desired property for the affected devices.</span></span> <span data-ttu-id="cb0b0-184">Wanneer de apparaten de nieuwe eigenschapswaarde **TelemetryInterval** ontvangen, wijzigen ze hun configuratie dusdanig dat er elke vijf seconden telemetrie wordt verzonden, in plaats van elke 15 seconden:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-184">When the devices receive the new **TelemetryInterval** property value, they change their configuration to send telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="cb0b0-185">Wanneer de lijst met beschadigde apparaten wordt weergegeven in de lijst met apparaten, kiest u **Taakplanner** en vervolgens **Apparaatdubbel bewerken**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-185">While you are showing the list of unhealthy devices in the device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="cb0b0-186">Roep de taak **Telemetrie-interval wijzigen** aan.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-186">Call the job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="cb0b0-187">Wijzig de waarde van de **Gewenste eigenschap** met de naam **desired.Config.TelemetryInterval** in vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-187">Change the value of the **Desired Property** name **desired.Config.TelemetryInterval** to five seconds.</span></span>

1. <span data-ttu-id="cb0b0-188">Kies **Planning**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-188">Choose **Schedule**.</span></span>

    ![De eigenschap TelemetryInterval in vijf seconden wijzigen][img-change-interval]

1. <span data-ttu-id="cb0b0-190">U kunt de voortgang bewaken van de taken op de pagina **Beheertaken** in de portal.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-190">You can monitor the progress of the job on the **Management Jobs** page in the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="cb0b0-191">Als u een gewenste eigenschapswaarde voor een afzonderlijk apparaat wilt wijzigen, gebruikt u het gedeelte **Gewenste eigenschappen** in het deelvenster **Apparaatdetails** in plaats van een taak.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-191">If you want to change a desired property value for an individual device, use the **Desired Properties** section in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="cb0b0-192">Deze taak stelt de waarde in van de gewenste eigenschap **TelemetryInterval** in het dubbele apparaat voor alle apparaten die door het filter zijn geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-192">This job sets the value of the **TelemetryInterval** desired property in the device twin for all the devices selected by the filter.</span></span> <span data-ttu-id="cb0b0-193">De apparaten halen deze waarde op van de dubbele apparaten en werken hun gedrag bij.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-193">The devices retrieve this value from the device twin and update their behavior.</span></span> <span data-ttu-id="cb0b0-194">Wanneer een apparaat een gewenste eigenschap ophaalt uit een dubbel apparaat, wordt de bijbehorende gerapporteerde eigenschapswaarde ingesteld.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-194">When a device retrieves and processes a desired property from a device twin, it sets the corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="cb0b0-195">Aanroepmethodes</span><span class="sxs-lookup"><span data-stu-id="cb0b0-195">Invoke methods</span></span>

<span data-ttu-id="cb0b0-196">Terwijl de taak wordt uitgevoerd, ziet u in de lijst met beschadigde apparaten dat al deze apparaten oude firmwareversies hebben (ouder dan versie 1.6).</span><span class="sxs-lookup"><span data-stu-id="cb0b0-196">While the job runs, you notice in the list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![De gemelde firmwareversie voor beschadigde apparaten weergeven][img-old-firmware]

<span data-ttu-id="cb0b0-198">Deze firmwareversie is mogelijk de basisoorzaak voor de onverwachte temperatuurwaarden als u weet dat andere apparaten die wel goed functioneren, onlangs zijn bijgewerkt naar versie 2.0.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-198">This firmware version may be the root cause of the unexpected temperature values because you know that other healthy devices were recently updated to version 2.0.</span></span> <span data-ttu-id="cb0b0-199">U kunt het ingebouwde filter **Apparaten met oude firmware** gebruiken om apparaten met oude firmwareversies te identificeren.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-199">You can use the built-in **Old firmware devices** filter to identify any devices with old firmware versions.</span></span> <span data-ttu-id="cb0b0-200">Via de portal kunt u vervolgens alle apparaten die nog een oude firmwareversie hebben, extern bijwerken:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-200">From the portal, you can then remotely update all the devices still running old firmware versions:</span></span>

1. <span data-ttu-id="cb0b0-201">Kies **Opgeslagen filter openen** om een lijst met beschikbare filters weer te geven.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-201">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="cb0b0-202">Kies vervolgens **Apparaten met oude firmwareversies** om het filter toe te passen:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-202">Then choose **Old firmware devices** to apply the filter:</span></span>

    ![De lijst met filters weergeven][img-old-filter]

1. <span data-ttu-id="cb0b0-204">In de lijst met apparaten worden nu alleen apparaten met oude firmwareversies weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-204">The device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="cb0b0-205">Deze lijst bevat de vijf apparaten die zijn geïdentificeerd door het filter **Beschadigde apparaten** en drie extra apparaten:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-205">This list includes the five devices identified by the **Unhealthy devices** filter and three additional devices:</span></span>

    ![De gefilterde apparatenlijst met oude apparaten weergeven][img-filtered-old-list]

1. <span data-ttu-id="cb0b0-207">Kies **Job Scheduler** en vervolgens **Aanroepmethode**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="cb0b0-208">Stel **Taaknaam** in op **Firmware bijwerken naar versie 2.0**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-208">Set **Job Name** to **Firmware update to version 2.0**.</span></span>

1. <span data-ttu-id="cb0b0-209">Kies **InitiateFirmwareUpdate** als de **Methode**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-209">Choose **InitiateFirmwareUpdate** as the **Method**.</span></span>

1. <span data-ttu-id="cb0b0-210">Stel de parameter **FwPackageUri** in op **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-210">Set the **FwPackageUri** parameter to **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="cb0b0-211">Kies **Planning**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-211">Choose **Schedule**.</span></span> <span data-ttu-id="cb0b0-212">De standaardwaarde voor de taak is nu uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-212">The default is for the job to run now.</span></span>

    ![Taak voor het bijwerken van de firmware van de geselecteerde apparaten maken][img-method-update]

> [!NOTE]
> <span data-ttu-id="cb0b0-214">Als u een aanroepmethode voor een bepaald apparaat wilt gebruiken, kiest u **Methoden** in het deelvenster **Apparaatdetails** in plaats van dat u de taak uitvoert.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-214">If you want to invoke a method on an individual device, choose **Methods** in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="cb0b0-215">Deze taak roept de directe methode **InitiateFirmwareUpdate** aan op alle apparaten die door het filter zijn geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-215">This job invokes the **InitiateFirmwareUpdate** direct method on all the devices selected by the filter.</span></span> <span data-ttu-id="cb0b0-216">Apparaten reageren onmiddellijk op IoT Hub en starten het updateproces voor de firmware asynchroon.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-216">Devices respond immediately to IoT Hub and then initiate the firmware update process asynchronously.</span></span> <span data-ttu-id="cb0b0-217">De apparaten bieden statusinformatie over het updateproces voor de firmware via gemelde eigenschapswaarden, zoals wordt weergegeven in de volgende schermafbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-217">The devices provide status information about the firmware update process through reported property values, as shown in the following screenshots.</span></span> <span data-ttu-id="cb0b0-218">Kies het pictogram **Vernieuwen** om de informatie in de apparaat- en takenlijsten bij te werken:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-218">Choose the **Refresh** icon to update the information in the device and job lists:</span></span>

<span data-ttu-id="cb0b0-219">![Taaklijst waarin de lijst met firmware die wordt bijgewerkt, wordt weergegeven][img-update-1]
![Apparatenlijst met de status van de firmware-update][img-update-2]
![Takenlijst met voltooide firmware-updates][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="cb0b0-219">![Job list showing the firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing the firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="cb0b0-220">U kunt taken volgens planning laten uitvoeren tijdens aangewezen onderhoudsperioden in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-220">In a production environment, you can schedule jobs to run during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="cb0b0-221">Samenvatting van scenario</span><span class="sxs-lookup"><span data-stu-id="cb0b0-221">Scenario review</span></span>

<span data-ttu-id="cb0b0-222">In dit scenario hebt u een mogelijk probleem met enkele van uw externe apparaten geïdentificeerd met behulp van de waarschuwingsgeschiedenis op het dashboard en een filter.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-222">In this scenario, you identified a potential issue with some of your remote devices using the alarm history on the dashboard and a filter.</span></span> <span data-ttu-id="cb0b0-223">Vervolgens hebt u het filter en een taak gebruikt om de apparaten extern te configureren om meer informatie te geven teneinde u te helpen bij het vaststellen van het probleem.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-223">You then used the filter and a job to remotely configure the devices to provide more information to help diagnose the issue.</span></span> <span data-ttu-id="cb0b0-224">Ten slotte hebt u een filter en een taak gebruikt om onderhoud op de beschadigde apparaten te plannen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-224">Finally, you used a filter and a job to schedule maintenance on the affected devices.</span></span> <span data-ttu-id="cb0b0-225">Als u naar het dashboard terugkeert, kunt u zien dat er geen waarschuwingen meer worden weergegeven voor apparaten in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-225">If you return to the dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="cb0b0-226">U kunt een filter gebruiken om te controleren of de firmware op alle apparaten in uw oplossing up-to-date is en er geen beschadigde apparaten meer zijn:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-226">You can use a filter to verify that the firmware is up-to-date on all the devices in your solution and that there are no more unhealthy devices:</span></span>

![Filter dat laat zien dat alle apparaten bijgewerkte firmware hebben][img-updated]

![Filter dat laat zien dat alle apparaten in orde zijn][img-healthy]

## <a name="other-features"></a><span data-ttu-id="cb0b0-229">Andere functies</span><span class="sxs-lookup"><span data-stu-id="cb0b0-229">Other features</span></span>

<span data-ttu-id="cb0b0-230">De volgende gedeelten beschrijven een aantal extra functies van de vooraf geconfigureerde oplossing voor externe controle die niet zijn beschreven als onderdeel van het voorgaande scenario.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-230">The following sections describe some additional features of the remote monitoring preconfigured solution that are not described as part of the previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="cb0b0-231">Kolommen aanpassen</span><span class="sxs-lookup"><span data-stu-id="cb0b0-231">Customize columns</span></span>

<span data-ttu-id="cb0b0-232">U kunt de informatie die in de apparatenlijst wordt weergegeven, aanpassen door **Kolomeditor** te kiezen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-232">You can customize the information shown in the device list by choosing **Column editor**.</span></span> <span data-ttu-id="cb0b0-233">U kunt kolommen die gerapporteerde eigenschaps- en tagwaarden weergeven, toevoegen en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="cb0b0-234">U kunt ook de volgorde en namen van de kolommen wijzigen:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-234">You can also reorder and rename columns:</span></span>

   ![Kolomeditor in de apparatenlijst][img-columneditor]

### <a name="customize-the-device-icon"></a><span data-ttu-id="cb0b0-236">Het apparaatpictogram aanpassen</span><span class="sxs-lookup"><span data-stu-id="cb0b0-236">Customize the device icon</span></span>

<span data-ttu-id="cb0b0-237">U kunt als volgt vanuit het deelvenster **Apparaatdetails** het apparaatpictogram aanpassen dat wordt weergegeven in de apparatenlijst:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-237">You can customize the device icon displayed in the device list from the **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="cb0b0-238">Kies het potloodpictogram om het deelvenster **Installatiekopie bewerken** voor een apparaat te openen:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-238">Choose the pencil icon to open the **Edit image** panel for a device:</span></span>

   ![De afbeeldingseditor van het apparaat openen][img-startimageedit]

1. <span data-ttu-id="cb0b0-240">Upload een nieuwe installatiekopie of gebruik een van de bestaande installatiekopieën en klik vervolgens op **Opslaan**:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-240">Either upload a new image or use one of the existing images and then choose **Save**:</span></span>

   ![De afbeelding van het apparaat bewerken in de afbeeldingseditor][img-imageedit]

1. <span data-ttu-id="cb0b0-242">De geselecteerde afbeelding wordt nu weergegeven in de kolom **Pictogram** voor het apparaat.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-242">The image you selected now displays in the **Icon** column for the device.</span></span>

> [!NOTE]
> <span data-ttu-id="cb0b0-243">De afbeelding wordt opgeslagen in Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-243">The image is stored in blob storage.</span></span> <span data-ttu-id="cb0b0-244">Een tag in de apparaatdubbel bevat een koppeling naar de afbeelding in Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-244">A tag in the device twin contains a link to the image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="cb0b0-245">Een apparaat toevoegen</span><span class="sxs-lookup"><span data-stu-id="cb0b0-245">Add a device</span></span>

<span data-ttu-id="cb0b0-246">Wanneer u de vooraf geconfigureerde oplossing implementeert, richt u automatisch de 25 proefapparaten in die u in de apparatenlijst ziet.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-246">When you deploy the preconfigured solution, you automatically provision 25 sample devices that you can see in the device list.</span></span> <span data-ttu-id="cb0b0-247">Deze apparaten zijn *gesimuleerde apparaten* uitgevoerd in een Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="cb0b0-248">Gesimuleerde apparaten maken het voor u gemakkelijk om te experimenteren met een vooraf geconfigureerde oplossing zonder echte, fysieke apparaten te moeten implementeren.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-248">Simulated devices make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical devices.</span></span> <span data-ttu-id="cb0b0-249">Raadpleeg de zelfstudie [Uw apparaat koppelen aan de vooraf geconfigureerde oplossing voor externe bewaking][lnk-connect-rm] als u een echt apparaat op de oplossing wilt aansluiten.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-249">If you do want to connect a real device to the solution, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="cb0b0-250">De volgende stappen laten zien hoe u een gesimuleerd apparaat toevoegt aan de oplossing:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-250">The following steps show you how to add a simulated device to the solution:</span></span>

1. <span data-ttu-id="cb0b0-251">Ga terug naar de lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-251">Navigate back to the device list.</span></span>

1. <span data-ttu-id="cb0b0-252">Kies linksonder **+ Een apparaat toevoegen** om een nieuw apparaat toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-252">To add a device, choose **+ Add A Device** in the bottom left corner.</span></span>

   ![Een apparaat toevoegen aan de vooraf geconfigureerde oplossing][img-adddevice]

1. <span data-ttu-id="cb0b0-254">Kies **Nieuwe toevoegen** op de tegel **Gesimuleerd apparaat**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-254">Choose **Add New** on the **Simulated Device** tile.</span></span>

   ![Nieuwe apparaatgegevens in het dashboard instellen][img-addnew]

   <span data-ttu-id="cb0b0-256">U kunt niet alleen een nieuw gesimuleerd apparaat maken, maar ook een fysiek apparaat toevoegen als u ervoor kiest om een **aangepast apparaat** te maken.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-256">In addition to creating a new simulated device, you can also add a physical device if you choose to create a **Custom Device**.</span></span> <span data-ttu-id="cb0b0-257">Zie [Uw apparaat aansluiten op de vooraf geconfigureerde IoT Suite-oplossing voor externe bewaking][lnk-connect-rm] voor meer informatie over het koppelen van fysieke apparaten aan de oplossing.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-257">To learn more about connecting physical devices to the solution, see [Connect your device to the IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="cb0b0-258">Selecteer **Laat mij mijn eigen apparaat-id definiëren** en voer de unieke id van een apparaatnaam in, zoals **mijnapparaat_01**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="cb0b0-259">Kies **Maken**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-259">Choose **Create**.</span></span>

   ![Een nieuw apparaat opslaan][img-definedevice]

1. <span data-ttu-id="cb0b0-261">Kies in stap 3 van **Een gesimuleerd apparaat toevoegen** de optie **Gereed** om terug te keren naar de apparatenlijst.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-261">In step 3 of **Add a simulated device**, choose **Done** to return to the device list.</span></span>

1. <span data-ttu-id="cb0b0-262">In de lijst met apparaten kunt u zien dat uw apparaat **wordt uitgevoerd**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-262">You can view your device **Running** in the device list.</span></span>

    ![Nieuw apparaat weergeven in de apparatenlijst][img-runningnew]

1. <span data-ttu-id="cb0b0-264">U kunt op het dashboard ook de gesimuleerde telemetrie van het nieuwe apparaat bekijken:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-264">You can also view the simulated telemetry from your new device on the dashboard:</span></span>

    ![Telemetrie voor nieuw apparaat weergeven][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="cb0b0-266">Een apparaat uitschakelen en verwijderen</span><span class="sxs-lookup"><span data-stu-id="cb0b0-266">Disable and delete a device</span></span>

<span data-ttu-id="cb0b0-267">U kunt een apparaat uitschakelen en nadat het is uitgeschakeld kunt u het verwijderen:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Een apparaat uitschakelen en verwijderen][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="cb0b0-269">Een regel toevoegen</span><span class="sxs-lookup"><span data-stu-id="cb0b0-269">Add a rule</span></span>

<span data-ttu-id="cb0b0-270">Er zijn geen regels voor het nieuwe apparaat dat u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-270">There are no rules for the new device you just added.</span></span> <span data-ttu-id="cb0b0-271">In deze sectie voegt u een regel toe die een waarschuwing activeert wanneer de door het nieuwe apparaat gemelde temperatuur 47 graden overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-271">In this section, you add a rule that triggers an alarm when the temperature reported by the new device exceeds 47 degrees.</span></span> <span data-ttu-id="cb0b0-272">Voordat u begint, kunt u al zien dat de telemetriegeschiedenis voor het nieuwe apparaat op het dashboard aantoont dat de temperatuur van het apparaat nooit meer dan 45 graden bedraagt.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-272">Before you start, notice that the telemetry history for the new device on the dashboard shows the device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="cb0b0-273">Ga terug naar de lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-273">Navigate back to the device list.</span></span>

1. <span data-ttu-id="cb0b0-274">Selecteer het nieuwe apparaat in de **apparatenlijst** en kies daarna **Regel toevoegen** om een regel voor het apparaat toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-274">To add a rule for the device, select your new device in the **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="cb0b0-275">Maak een regel die **Temperatuur** als gegevensveld gebruikt en **AlarmTemp** gebruikt als de uitvoer wanneer de temperatuur 47 graden overschrijdt:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-275">Create a rule that uses **Temperature** as the data field and uses **AlarmTemp** as the output when the temperature exceeds 47 degrees:</span></span>

    ![Een apparaatregel toevoegen][img-adddevicerule]

1. <span data-ttu-id="cb0b0-277">Kies **Regels opslaan en weergeven** om uw wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-277">To save your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="cb0b0-278">Kies **Opdrachten** in het deelvenster Apparaatdetails voor het nieuwe apparaat.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-278">Choose **Commands** in the device details pane for the new device.</span></span>

    ![Een apparaatregel toevoegen][img-adddevicerule2]

1. <span data-ttu-id="cb0b0-280">Selecteer **ChangeSetPointTemp** in de opdrachtlijst en stel **SetPointTemp** in op 45.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-280">Select **ChangeSetPointTemp** from the command list and set **SetPointTemp** to 45.</span></span> <span data-ttu-id="cb0b0-281">Kies vervolgens **Opdracht verzenden**:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-281">Then choose **Send Command**:</span></span>

    ![Een apparaatregel toevoegen][img-adddevicerule3]

1. <span data-ttu-id="cb0b0-283">Ga terug naar het dashboard.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-283">Navigate back to the dashboard.</span></span> <span data-ttu-id="cb0b0-284">Na korte tijd verschijnt in het deelvenster **Geschiedenis van waarschuwingen** een nieuwe vermelding wanneer de door het nieuwe apparaat gemelde temperatuur 47 graden overschrijdt:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-284">After a short time, you will see a new entry in the **Alarm History** pane when the temperature reported by your new device exceeds the 47-degree threshold:</span></span>

    ![Een apparaatregel toevoegen][img-adddevicerule4]

1. <span data-ttu-id="cb0b0-286">Op de pagina **Regels** van het dashboard kunt u al uw regels bekijken en bewerken:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-286">You can review and edit all your rules on the **Rules** page of the dashboard:</span></span>

    ![Lijst met apparaatregels][img-rules]

1. <span data-ttu-id="cb0b0-288">Op de pagina **Acties** van het dashboard kunt u alle acties die worden uitgevoerd in reactie op een regel bekijken en bewerken:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-288">You can review and edit all the actions that can be taken in response to a rule on the **Actions** page of the dashboard:</span></span>

    ![Lijst met apparaatacties][img-actions]

> [!NOTE]
> <span data-ttu-id="cb0b0-290">Het is mogelijk om acties te definiëren die een e-mailbericht of sms kunnen verzenden in antwoord op een regel of die met een Line-Of-Business-systeem kunnen worden geïntegreerd via een [logische app][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="cb0b0-290">It is possible to define actions that can send an email message or SMS in response to a rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="cb0b0-291">Zie [De logische app koppelen aan uw vooraf geconfigureerde oplossing Azure IoT Suite Remote Monitoring ][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="cb0b0-291">For more information, see the [Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="cb0b0-292">Filters beheren</span><span class="sxs-lookup"><span data-stu-id="cb0b0-292">Manage filters</span></span>

<span data-ttu-id="cb0b0-293">In de apparatenlijst kunt u filters maken, opslaan en opnieuw laden om een aangepaste lijst met apparaten die zijn verbonden met uw hub weer te geven.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-293">In the device list, you can create, save, and reload filters to display a customized list of devices connected to your hub.</span></span> <span data-ttu-id="cb0b0-294">Een filter maken:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-294">To create a filter:</span></span>

1. <span data-ttu-id="cb0b0-295">Kies het pictogram Filter bewerken boven de apparatenlijst:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-295">Choose the edit filter icon above the list of devices:</span></span>

    ![Open de filtereditor][img-editfiltericon]

1. <span data-ttu-id="cb0b0-297">Voeg in de **Filtereditor** de velden, operators en waarden toe om de apparatenlijst te filteren.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-297">In the **Filter editor**, add the fields, operators, and values to filter the device list.</span></span> <span data-ttu-id="cb0b0-298">U kunt meerdere clausules toevoegen om uw filter te verfijnen.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-298">You can add multiple clauses to refine your filter.</span></span> <span data-ttu-id="cb0b0-299">Kies **Filteren** om het filter toe te passen:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-299">Choose **Filter** to apply the filter:</span></span>

    ![Een filter maken][img-filtereditor]

1. <span data-ttu-id="cb0b0-301">In dit voorbeeld wordt de lijst gefilterd op fabrikant en modelnummer:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-301">In this example, the list is filtered by manufacturer and model number:</span></span>

    ![Gefilterde lijst][img-filterelist]

1. <span data-ttu-id="cb0b0-303">Als u uw filter met een aangepaste naam wilt opslaan, kiest u het pictogram **Opslaan als**:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-303">To save your filter with a custom name, choose the **Save as** icon:</span></span>

    ![Een filter opslaan][img-savefilter]

1. <span data-ttu-id="cb0b0-305">Als u een eerder opgeslagen filter opnieuw wilt toepassen, kiest u het pictogram **Opgeslagen filter openen**:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-305">To reapply a filter you saved previously, choose the **Open saved filter** icon:</span></span>

    ![Een filter openen][img-openfilter]

<span data-ttu-id="cb0b0-307">U kunt filters maken op basis van apparaat-id, apparaatstatus gewenste eigenschappen, gerapporteerde eigenschappen en tags.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="cb0b0-308">U kunt uw eigen aangepaste tags toevoegen aan een apparaat in het gedeelte **Tags** van het deelvenster **Apparaatdetails** of een taak voor het bijwerken van tags op meerdere apparaten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-308">You add your own custom tags to a device in the **Tags** section of the **Device Details** panel, or run a job to update tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="cb0b0-309">U kunt de **weergave Geavanceerd** in de **Filtereditor** gebruiken om de querytekst rechtstreeks te bewerken.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-309">In the **Filter editor**, you can use the **Advanced view** to edit the query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="cb0b0-310">Opdrachten</span><span class="sxs-lookup"><span data-stu-id="cb0b0-310">Commands</span></span>

<span data-ttu-id="cb0b0-311">Vanuit het deelvenster **Apparaatdetails** kunt u opdrachten naar het apparaat verzenden.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-311">From the **Device Details** panel, you can send commands to the device.</span></span> <span data-ttu-id="cb0b0-312">Wanneer een apparaat voor het eerst wordt gestart, stuurt het naar de oplossing informatie over de opdrachten die het apparaat ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-312">When a device first starts, it sends information about the commands it supports to the solution.</span></span> <span data-ttu-id="cb0b0-313">Zie [Opties van Azure IoT-Hub cloud-naar-apparaat][lnk-c2d-guidance] voor een beschrijving van de verschillen tussen opdrachten en methoden.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-313">For a discussion of the differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="cb0b0-314">Kies in het deelvenster **Apparaatdetails** de optie **Opdrachten** voor het geselecteerde apparaat:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-314">Choose **Commands** in the **Device Details** panel for the selected device:</span></span>

   ![Apparaatopdrachten in het dashboard][img-devicecommands]

1. <span data-ttu-id="cb0b0-316">Selecteer **PingDevice** in de lijst met opdrachten.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-316">Select **PingDevice** from the command list.</span></span>

1. <span data-ttu-id="cb0b0-317">Kies **Opdracht verzenden**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="cb0b0-318">U ziet de status van de opdracht in de opdrachtgeschiedenis.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-318">You can see the status of the command in the command history.</span></span>

   ![Opdrachtstatus in het dashboard][img-pingcommand]

<span data-ttu-id="cb0b0-320">De oplossing houdt de status van elke opdracht bij die met de oplossing wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-320">The solution tracks the status of each command it sends.</span></span> <span data-ttu-id="cb0b0-321">In eerste instantie is het resultaat **In behandeling**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-321">Initially the result is **Pending**.</span></span> <span data-ttu-id="cb0b0-322">Wanneer het apparaat meldt dat het de opdracht heeft uitgevoerd, wordt het resultaat ingesteld op **Geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-322">When the device reports that it has executed the command, the result is set to **Success**.</span></span>

## <a name="behind-the-scenes"></a><span data-ttu-id="cb0b0-323">Achter de schermen</span><span class="sxs-lookup"><span data-stu-id="cb0b0-323">Behind the scenes</span></span>

<span data-ttu-id="cb0b0-324">Wanneer u een vooraf geconfigureerde oplossing implementeert, maakt het implementatieproces meerdere resources in het door u geselecteerde Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-324">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="cb0b0-325">U kunt deze resources weergeven in Azure [Portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="cb0b0-325">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="cb0b0-326">Het implementatieproces maakt een **resourcegroep** met een naam die is gebaseerd op de naam die u voor uw vooraf geconfigureerde oplossing hebt gekozen:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-326">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Vooraf geconfigureerde oplossing in Azure Portal][img-portal]

<span data-ttu-id="cb0b0-328">U kunt de instellingen van elke resource weergeven door deze te selecteren in de lijst met resources in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-328">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="cb0b0-329">U kunt ook de broncode voor de vooraf geconfigureerde oplossing weergeven.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-329">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="cb0b0-330">De broncode van de vooraf geconfigureerde oplossing voor externe bewaking bevindt zich in de GitHub-opslagplaats [azure-iot-remote-monitoring][lnk-rmgithub]:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-330">The remote monitoring preconfigured solution source code is in the [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="cb0b0-331">De map **DeviceAdministration** bevat de broncode voor het dashboard.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-331">The **DeviceAdministration** folder contains the source code for the dashboard.</span></span>
* <span data-ttu-id="cb0b0-332">De map **Simulator** bevat de broncode voor het gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-332">The **Simulator** folder contains the source code for the simulated device.</span></span>
* <span data-ttu-id="cb0b0-333">De map **EventProcessor** bevat de broncode voor het back-endproces dat de binnenkomende telemetrie verwerkt.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-333">The **EventProcessor** folder contains the source code for the back-end process that handles the incoming telemetry.</span></span>

<span data-ttu-id="cb0b0-334">Wanneer u klaar bent, kunt u de vooraf geconfigureerde oplossing verwijderen uit uw Azure-abonnement op de site [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="cb0b0-334">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="cb0b0-335">Met de site kunt u gemakkelijk resources verwijderen die werden aangevoerd toen u de vooraf geconfigureerde oplossing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-335">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="cb0b0-336">Verwijder de resourcegroep niet uit de portal, maar verwijder de oplossing op de site [azureiotsuite.com][lnk-azureiotsuite]. Zo zorgt u ervoor dat alles met betrekking tot de vooraf geconfigureerde oplossing wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="cb0b0-336">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site and do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb0b0-337">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cb0b0-337">Next Steps</span></span>

<span data-ttu-id="cb0b0-338">Nu u een werkende vooraf geconfigureerde oplossing hebt geïmplementeerd, kunt u doorgaan met IoT Suite door de volgende artikels te lezen:</span><span class="sxs-lookup"><span data-stu-id="cb0b0-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="cb0b0-339">[Walkthrough over de vooraf geconfigureerde oplossing voor externe bewaking][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="cb0b0-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="cb0b0-340">[Uw apparaat koppelen aan de vooraf geconfigureerde oplossing voor externe bewaking][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="cb0b0-340">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="cb0b0-341">[Machtigingen op de site azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="cb0b0-341">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md