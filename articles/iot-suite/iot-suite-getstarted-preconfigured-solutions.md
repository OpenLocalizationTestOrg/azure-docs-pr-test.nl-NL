---
title: aaaGet de slag met vooraf geconfigureerde oplossingen | Microsoft Docs
description: Volg deze zelfstudie toolearn hoe toodeploy een Azure IoT Suite vooraf geconfigureerde oplossing.
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
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a><span data-ttu-id="d28af-103">Aan de slag met Hallo vooraf geconfigureerde oplossingen</span><span class="sxs-lookup"><span data-stu-id="d28af-103">Get started with hello preconfigured solutions</span></span>

<span data-ttu-id="d28af-104">Azure IoT Suite [vooraf geconfigureerde oplossingen] [ lnk-preconfigured-solutions] combineren meerdere Azure IoT services toodeliver end-to-end-oplossingen die algemene IoT-bedrijfsscenario's implementeren.</span><span class="sxs-lookup"><span data-stu-id="d28af-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="d28af-105">Hallo *externe controle* vooraf geconfigureerde oplossing voor uw apparaten tooand monitors verbonden.</span><span class="sxs-lookup"><span data-stu-id="d28af-105">hello *remote monitoring* preconfigured solution connects tooand monitors your devices.</span></span> <span data-ttu-id="d28af-106">Hallo oplossing tooanalyze Hallo stroom van gegevens van uw apparaten en tooimprove bedrijfsresultaten kunt u door het maken van processen automatisch toothat gegevensstroom reageren.</span><span class="sxs-lookup"><span data-stu-id="d28af-106">You can use hello solution tooanalyze hello stream of data from your devices and tooimprove business outcomes by making processes respond automatically toothat stream of data.</span></span>

<span data-ttu-id="d28af-107">Deze zelfstudie leert u hoe tooprovision Hallo externe controle vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="d28af-107">This tutorial shows you how tooprovision hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="d28af-108">Ook wordt u begeleid Hallo basisfuncties van Hallo vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="d28af-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="d28af-109">U veel van deze functies kunt openen vanaf Hallo oplossing *dashboard* die als onderdeel van Hallo vooraf geconfigureerde oplossing implementeert:</span><span class="sxs-lookup"><span data-stu-id="d28af-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Vooraf geconfigureerd oplossingsdashboard voor externe controle][img-dashboard]

<span data-ttu-id="d28af-111">toocomplete in deze zelfstudie, moet u een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d28af-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d28af-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="d28af-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d28af-113">Zie [Gratis proefversie van Azure][lnk_free_trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d28af-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="d28af-114">Overzicht van scenario's</span><span class="sxs-lookup"><span data-stu-id="d28af-114">Scenario overview</span></span>

<span data-ttu-id="d28af-115">Wanneer u Hallo vooraf geconfigureerde oplossing voor externe controle implementeert, is deze vooraf ingevuld met resources waarmee u toostep via een algemeen scenario voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="d28af-115">When you deploy hello remote monitoring preconfigured solution, it is prepopulated with resources that enable you toostep through a common remote monitoring scenario.</span></span> <span data-ttu-id="d28af-116">In dit scenario zijn verschillende apparaten verbonden toohello oplossing onverwachte temperatuur waarden rapportage.</span><span class="sxs-lookup"><span data-stu-id="d28af-116">In this scenario, several devices connected toohello solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="d28af-117">Hallo volgende secties ziet u hoe aan:</span><span class="sxs-lookup"><span data-stu-id="d28af-117">hello following sections show you how to:</span></span>

* <span data-ttu-id="d28af-118">Onverwachte temperatuur waarden verzenden Hallo-apparaten kan identificeren.</span><span class="sxs-lookup"><span data-stu-id="d28af-118">Identify hello devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="d28af-119">Configureren van deze apparaten toosend meer gedetailleerde telemetrie.</span><span class="sxs-lookup"><span data-stu-id="d28af-119">Configure these devices toosend more detailed telemetry.</span></span>
* <span data-ttu-id="d28af-120">Hallo probleem oplossen door het bijwerken van de firmware Hallo op deze apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-120">Fix hello problem by updating hello firmware on these devices.</span></span>
* <span data-ttu-id="d28af-121">Controleer of dat uw actie Hallo probleem is opgelost.</span><span class="sxs-lookup"><span data-stu-id="d28af-121">Verify that your action has resolved hello issue.</span></span>

<span data-ttu-id="d28af-122">Een belangrijke functie van dit scenario is dat u al deze acties extern vanuit Hallo oplossing dashboard uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="d28af-122">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="d28af-123">U hoeft geen fysieke toegang toohello apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-123">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="d28af-124">Dashboard van oplossing Hallo weergeven</span><span class="sxs-lookup"><span data-stu-id="d28af-124">View hello solution dashboard</span></span>

<span data-ttu-id="d28af-125">Hallo oplossing dashboard kunt u toomanage Hallo geïmplementeerd oplossing.</span><span class="sxs-lookup"><span data-stu-id="d28af-125">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="d28af-126">U kunt er bijvoorbeeld telemetrie weergeven, apparaten toevoegen en regels configureren.</span><span class="sxs-lookup"><span data-stu-id="d28af-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="d28af-127">Wanneer Hallo inrichten is voltooid en Hallo tegel voor uw vooraf geconfigureerde oplossing geeft **gereed**, kies **starten** tooopen uw externe controle portal van de oplossing in een nieuw tabblad.</span><span class="sxs-lookup"><span data-stu-id="d28af-127">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Hallo vooraf geconfigureerde oplossing starten][img-launch-solution]

1. <span data-ttu-id="d28af-129">Standaard ziet u de oplossingsportal Hallo Hallo *dashboard*.</span><span class="sxs-lookup"><span data-stu-id="d28af-129">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="d28af-130">U kunt tooother gebieden van de portal van de oplossing Hallo Hallo menu aan de linkerkant Hallo van Hallo pagina met navigeren.</span><span class="sxs-lookup"><span data-stu-id="d28af-130">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Vooraf geconfigureerd oplossingsdashboard voor externe controle][img-menu]

<span data-ttu-id="d28af-132">Hallo dashboard toont de Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="d28af-132">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="d28af-133">Een kaart die wordt weergegeven Hallo-locatie van elk apparaat verbonden toohello oplossing.</span><span class="sxs-lookup"><span data-stu-id="d28af-133">A map that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="d28af-134">Wanneer u Hallo oplossing voor het eerst uitvoert, moet u er 25 gesimuleerde apparaten zijn.</span><span class="sxs-lookup"><span data-stu-id="d28af-134">When you first run hello solution, there are 25 simulated devices.</span></span> <span data-ttu-id="d28af-135">Hallo gesimuleerde apparaten worden geïmplementeerd als Azure WebJobs en Hallo oplossing gebruikt Hallo Bing kaarten-API tooplot informatie op Hallo-kaart.</span><span class="sxs-lookup"><span data-stu-id="d28af-135">hello simulated devices are implemented as Azure WebJobs, and hello solution uses hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="d28af-136">Zie Hallo [Veelgestelde vragen over] [ lnk-faq] toolearn hoe toomake kaart dynamische Hallo.</span><span class="sxs-lookup"><span data-stu-id="d28af-136">See hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="d28af-137">Een deelvenster **Telemetriegeschiedenis** dat de vochtigheids- en temperatuurtelemetrie van een geselecteerd apparaat in bijna realtime tekent en statistische gegevens weergeeft, zoals de maximale, minimale en gemiddelde vochtigheid.</span><span class="sxs-lookup"><span data-stu-id="d28af-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="d28af-138">Een deelvenster **Geschiedenis van waarschuwingen** dat recente waarschuwingsgebeurtenissen toont wanneer voor een telemetriewaarde een drempelwaarde wordt overschreden.</span><span class="sxs-lookup"><span data-stu-id="d28af-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="d28af-139">U kunt uw eigen alarmen definiëren in toevoeging toohello voorbeelden is gemaakt door Hallo vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="d28af-139">You can define your own alarms in addition toohello examples created by hello preconfigured solution.</span></span>
* <span data-ttu-id="d28af-140">Een deelvenster **Taken** dat informatie weergeeft over geplande taken.</span><span class="sxs-lookup"><span data-stu-id="d28af-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="d28af-141">U kunt uw eigen taken plannen op de pagina **Beheertaken**.</span><span class="sxs-lookup"><span data-stu-id="d28af-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="d28af-142">Waarschuwingen weergeven</span><span class="sxs-lookup"><span data-stu-id="d28af-142">View alarms</span></span>

<span data-ttu-id="d28af-143">Hallo alarm geschiedenis deelvenster ziet u dat de melden van vijf apparaten hoger dan de verwachte telemetrie waarden.</span><span class="sxs-lookup"><span data-stu-id="d28af-143">hello alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Geschiedenis van TODO-waarschuwingen op Hallo oplossing dashboard][img-alarms]

> [!NOTE]
> <span data-ttu-id="d28af-145">Deze waarschuwingen worden gegenereerd door een regel die is opgenomen in Hallo vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="d28af-145">These alarms are generated by a rule that is included in hello preconfigured solution.</span></span> <span data-ttu-id="d28af-146">Deze regel genereert een waarschuwing wanneer Hallo temperatuur waarde die is verzonden door een apparaat hoger is dan 60.</span><span class="sxs-lookup"><span data-stu-id="d28af-146">This rule generates an alert when hello temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="d28af-147">U kunt uw eigen regels en acties definiëren door te kiezen [regels](#add-a-rule) en [acties](#add-an-action) in het menu links van Hallo.</span><span class="sxs-lookup"><span data-stu-id="d28af-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in hello left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="d28af-148">Apparaten weergeven</span><span class="sxs-lookup"><span data-stu-id="d28af-148">View devices</span></span>

<span data-ttu-id="d28af-149">Hallo *apparaten* lijst bevat alle Hallo geregistreerde apparaten in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="d28af-149">hello *devices* list shows all hello registered devices in hello solution.</span></span> <span data-ttu-id="d28af-150">Vanaf Hallo lijst met apparaten kunt u bekijken en bewerken van metagegevens van apparaten, toevoegen of verwijderen van apparaten en methoden niet aanroepen voor apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-150">From hello device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="d28af-151">U kunt filteren en sorteren Hallo lijst met apparaten in de lijst met Hallo-apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-151">You can filter and sort hello list of devices in hello device list.</span></span> <span data-ttu-id="d28af-152">U kunt ook weergegeven in de lijst met apparaten Hallo Hallo-kolommen aanpassen.</span><span class="sxs-lookup"><span data-stu-id="d28af-152">You can also customize hello columns shown in hello device list.</span></span>

1. <span data-ttu-id="d28af-153">Kies **apparaten** tooshow Hallo lijst met apparaten voor deze oplossing.</span><span class="sxs-lookup"><span data-stu-id="d28af-153">Choose **Devices** tooshow hello device list for this solution.</span></span>

   ![Lijst met apparaten van weergave-Hallo in de oplossingsportal Hallo][img-devicelist]

1. <span data-ttu-id="d28af-155">lijst met apparaten Hallo toont in eerste instantie 25 gesimuleerde apparaten die zijn gemaakt door Hallo inrichtingsproces.</span><span class="sxs-lookup"><span data-stu-id="d28af-155">hello device list initially shows 25 simulated devices created by hello provisioning process.</span></span> <span data-ttu-id="d28af-156">U kunt extra gesimuleerde en fysieke apparaten toohello oplossing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d28af-156">You can add additional simulated and physical devices toohello solution.</span></span>

1. <span data-ttu-id="d28af-157">tooview hello details van een apparaat, kies een apparaat in de lijst met Hallo-apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-157">tooview hello details of a device, choose a device in hello device list.</span></span>

   ![Hallo Apparaatdetails in de oplossingsportal Hallo weergeven][img-devicedetails]

<span data-ttu-id="d28af-159">Hallo **Apparaatdetails** deelvenster bevat zes secties:</span><span class="sxs-lookup"><span data-stu-id="d28af-159">hello **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="d28af-160">Een verzameling van koppelingen die u toocustomize Hallo pictogram van het apparaat inschakelen, Hallo apparaat uitschakelt, een regel kunt toevoegen, een methode aangeroepen of een opdracht verzenden.</span><span class="sxs-lookup"><span data-stu-id="d28af-160">A collection of links that enable you toocustomize hello device icon, disable hello device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="d28af-161">Zie [Cloud-to-device communications guidance][lnk-c2d-guidance] (Richtlijnen voor communicatie tussen cloud en apparaat) voor een vergelijking van opdrachten (berichten van apparaat naar cloud) en methoden (directe methoden).</span><span class="sxs-lookup"><span data-stu-id="d28af-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="d28af-162">Hallo **apparaat Twin - Tags** sectie kunt u tooedit labelwaarden voor Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="d28af-162">hello **Device Twin - Tags** section enables you tooedit tag values for hello device.</span></span> <span data-ttu-id="d28af-163">U kunt tagwaarden worden weergegeven in de lijst met apparaten Hallo en tag waarden toofilter Hallo apparatenlijst gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d28af-163">You can display tag values in hello device list and use tag values toofilter hello device list.</span></span>
* <span data-ttu-id="d28af-164">Hallo **apparaat Twin - eigenschappen gewenst** sectie kunt u tooset eigenschap waarden toobe verzonden toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="d28af-164">hello **Device Twin - Desired Properties** section enables you tooset property values toobe sent toohello device.</span></span>
* <span data-ttu-id="d28af-165">Hallo **apparaat Twin - eigenschappen gerapporteerd** sectie toont de waarden van Hallo apparaat verzonden.</span><span class="sxs-lookup"><span data-stu-id="d28af-165">hello **Device Twin - Reported Properties** section shows property values sent from hello device.</span></span>
* <span data-ttu-id="d28af-166">Hallo **apparaateigenschappen** sectie wordt informatie weergegeven uit Hallo identiteitsregister zoals Hallo apparaat-id- en verificatiesleutels.</span><span class="sxs-lookup"><span data-stu-id="d28af-166">hello **Device Properties** section shows information from hello identity registry such as hello device id and authentication keys.</span></span>
* <span data-ttu-id="d28af-167">Hallo **recente taken** sectie bevat informatie over alle taken die dit apparaat onlangs zijn gericht.</span><span class="sxs-lookup"><span data-stu-id="d28af-167">hello **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-hello-device-list"></a><span data-ttu-id="d28af-168">Lijst met apparaten Hallo filteren</span><span class="sxs-lookup"><span data-stu-id="d28af-168">Filter hello device list</span></span>

<span data-ttu-id="d28af-169">Alleen de apparaten die onverwachte temperatuur waarden verzendt, kunt u een filter toodisplay gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d28af-169">You can use a filter toodisplay only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="d28af-170">Hallo vooraf geconfigureerde oplossing voor externe controle omvat Hallo **slecht apparaten** tooshow apparaten met een gemiddelde temperatuur-waarde die groter zijn dan 60 filteren.</span><span class="sxs-lookup"><span data-stu-id="d28af-170">hello remote monitoring preconfigured solution includes hello **Unhealthy devices** filter tooshow devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="d28af-171">U kunt ook [uw eigen filters maken](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="d28af-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="d28af-172">Kies **opgeslagen filter openen** toodisplay een lijst met beschikbare filters.</span><span class="sxs-lookup"><span data-stu-id="d28af-172">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="d28af-173">Kies vervolgens **slecht apparaten** tooapply Hallo filter:</span><span class="sxs-lookup"><span data-stu-id="d28af-173">Then choose **Unhealthy devices** tooapply hello filter:</span></span>

    ![Hallo-lijst met filters weergeven][img-unhealthy-filter]

1. <span data-ttu-id="d28af-175">lijst met apparaten Hallo wordt nu alleen apparaten met een gemiddelde temperatuur-waarde groter dan 60.</span><span class="sxs-lookup"><span data-stu-id="d28af-175">hello device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Weergave Hallo gefilterde lijst met apparaten niet in orde apparaten weergegeven][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="d28af-177">Gewenste eigenschappen bijwerken</span><span class="sxs-lookup"><span data-stu-id="d28af-177">Update desired properties</span></span>

<span data-ttu-id="d28af-178">U hebt nu een set apparaten geïdentificeerd die mogelijk moeten worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="d28af-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="d28af-179">Echter, u besluit Hallo gegevensfrequentie van 15 seconden is niet voldoende voor een duidelijke diagnose van Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="d28af-179">However, you decide that hello data frequency of 15 seconds is not sufficient for a clear diagnosis of hello issue.</span></span> <span data-ttu-id="d28af-180">Het wijzigen van Hallo telemetrie frequentie toofive seconden tooprovide diagnosticeren u met meer gegevenspunten toobetter Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="d28af-180">Changing hello telemetry frequency toofive seconds tooprovide you with more data points toobetter diagnose hello issue.</span></span> <span data-ttu-id="d28af-181">U kunt deze configuratie wijzigen tooyour externe apparaten uit de oplossingsportal Hallo push.</span><span class="sxs-lookup"><span data-stu-id="d28af-181">You can push this configuration change tooyour remote devices from hello solution portal.</span></span> <span data-ttu-id="d28af-182">U kunt slechts één keer evalueren Hallo impact, en vervolgens reageren op resultaten Hallo Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d28af-182">You can make hello change once, evaluate hello impact, and then act on hello results.</span></span>

<span data-ttu-id="d28af-183">Volg deze stappen toorun een taak die wijzigingen Hallo **TelemetryInterval** gewenst eigenschap voor Hallo van invloed op apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-183">Follow these steps toorun a job that changes hello **TelemetryInterval** desired property for hello affected devices.</span></span> <span data-ttu-id="d28af-184">Wanneer apparaten Hallo Hallo nieuwe ontvangt **TelemetryInterval** eigenschapswaarde, dat ze hun configuratie toosend telemetrie om de vijf seconden in plaats van elke 15 seconden wijzigen:</span><span class="sxs-lookup"><span data-stu-id="d28af-184">When hello devices receive hello new **TelemetryInterval** property value, they change their configuration toosend telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="d28af-185">Terwijl u Hallo lijst met apparaten die niet in orde worden weergegeven in de lijst met apparaten hello, kies **Taakplanner**, klikt u vervolgens **bewerken apparaat Twin**.</span><span class="sxs-lookup"><span data-stu-id="d28af-185">While you are showing hello list of unhealthy devices in hello device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="d28af-186">Hallo taak aanroepen **interval voor wijzigen van telemetrie**.</span><span class="sxs-lookup"><span data-stu-id="d28af-186">Call hello job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="d28af-187">Wijzig de waarde Hallo Hallo **gewenste eigenschap** naam **gewenste. Config.TelemetryInterval** toofive seconden.</span><span class="sxs-lookup"><span data-stu-id="d28af-187">Change hello value of hello **Desired Property** name **desired.Config.TelemetryInterval** toofive seconds.</span></span>

1. <span data-ttu-id="d28af-188">Kies **Planning**.</span><span class="sxs-lookup"><span data-stu-id="d28af-188">Choose **Schedule**.</span></span>

    ![Hallo TelemetryInterval eigenschap toofive seconden wijzigen][img-change-interval]

1. <span data-ttu-id="d28af-190">U kunt Hallo voortgang van de taak Hallo op Hallo **Management taken** pagina in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d28af-190">You can monitor hello progress of hello job on hello **Management Jobs** page in hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d28af-191">Als u toochange een gewenste eigenschapwaarde voor een afzonderlijk apparaat wilt, gebruikt u Hallo **gewenste eigenschappen** sectie in Hallo **Apparaatdetails** deelvenster in plaats van een taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d28af-191">If you want toochange a desired property value for an individual device, use hello **Desired Properties** section in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="d28af-192">Deze taak wordt Hallo-waarde van Hallo **TelemetryInterval** eigenschap in Hallo apparaat twin gewenst voor alle apparaten die zijn geselecteerd door Hallo filter Hallo.</span><span class="sxs-lookup"><span data-stu-id="d28af-192">This job sets hello value of hello **TelemetryInterval** desired property in hello device twin for all hello devices selected by hello filter.</span></span> <span data-ttu-id="d28af-193">Hallo apparaten deze waarde wordt opgehaald uit Hallo apparaat twin en hun gedrag bij te werken.</span><span class="sxs-lookup"><span data-stu-id="d28af-193">hello devices retrieve this value from hello device twin and update their behavior.</span></span> <span data-ttu-id="d28af-194">Als u een apparaat worden opgehaald en verwerkt een gewenste eigenschap van een apparaat-twin, wordt Hallo overeenkomende gemelde waarde eigenschap.</span><span class="sxs-lookup"><span data-stu-id="d28af-194">When a device retrieves and processes a desired property from a device twin, it sets hello corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="d28af-195">Aanroepmethodes</span><span class="sxs-lookup"><span data-stu-id="d28af-195">Invoke methods</span></span>

<span data-ttu-id="d28af-196">Tijdens het Hallo-taak wordt uitgevoerd, ziet u in de lijst Hallo met slechte apparaten dat al deze apparaten oude (minder dan versie 1.6) firmware hebben versies.</span><span class="sxs-lookup"><span data-stu-id="d28af-196">While hello job runs, you notice in hello list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Weergave Hallo firmwareversie voor Hallo slecht apparaten gerapporteerd][img-old-firmware]

<span data-ttu-id="d28af-198">Deze firmwareversie is mogelijk de hoofdoorzaak Hallo Hallo onverwachte temperatuur waarden omdat u weet dat andere apparaten in orde onlangs bijgewerkt tooversion 2.0 zijn.</span><span class="sxs-lookup"><span data-stu-id="d28af-198">This firmware version may be hello root cause of hello unexpected temperature values because you know that other healthy devices were recently updated tooversion 2.0.</span></span> <span data-ttu-id="d28af-199">U kunt ingebouwde Hallo **oude firmware apparaten** filteren tooidentify alle apparaten met oude firmware-versies.</span><span class="sxs-lookup"><span data-stu-id="d28af-199">You can use hello built-in **Old firmware devices** filter tooidentify any devices with old firmware versions.</span></span> <span data-ttu-id="d28af-200">Vanuit de portal Hallo kunt u alle Hallo apparaten nog steeds met oude firmwareversies vervolgens extern bijwerken:</span><span class="sxs-lookup"><span data-stu-id="d28af-200">From hello portal, you can then remotely update all hello devices still running old firmware versions:</span></span>

1. <span data-ttu-id="d28af-201">Kies **opgeslagen filter openen** toodisplay een lijst met beschikbare filters.</span><span class="sxs-lookup"><span data-stu-id="d28af-201">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="d28af-202">Kies vervolgens **oude firmware apparaten** tooapply Hallo filter:</span><span class="sxs-lookup"><span data-stu-id="d28af-202">Then choose **Old firmware devices** tooapply hello filter:</span></span>

    ![Hallo-lijst met filters weergeven][img-old-filter]

1. <span data-ttu-id="d28af-204">lijst met apparaten Hello wordt nu alleen apparaten met oude firmware-versies.</span><span class="sxs-lookup"><span data-stu-id="d28af-204">hello device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="d28af-205">Deze lijst bevat Hallo vijf apparaten die worden geïdentificeerd door Hallo **slecht apparaten** filteren en drie extra apparaten:</span><span class="sxs-lookup"><span data-stu-id="d28af-205">This list includes hello five devices identified by hello **Unhealthy devices** filter and three additional devices:</span></span>

    ![Weergave Hallo gefilterde lijst met apparaten oude apparaten weergegeven][img-filtered-old-list]

1. <span data-ttu-id="d28af-207">Kies **Job Scheduler** en vervolgens **Aanroepmethode**.</span><span class="sxs-lookup"><span data-stu-id="d28af-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="d28af-208">Stel **taaknaam** te**Firmware-update tooversion 2.0**.</span><span class="sxs-lookup"><span data-stu-id="d28af-208">Set **Job Name** too**Firmware update tooversion 2.0**.</span></span>

1. <span data-ttu-id="d28af-209">Kies **InitiateFirmwareUpdate** als Hallo **methode**.</span><span class="sxs-lookup"><span data-stu-id="d28af-209">Choose **InitiateFirmwareUpdate** as hello **Method**.</span></span>

1. <span data-ttu-id="d28af-210">Set Hallo **FwPackageUri** parameter te**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="d28af-210">Set hello **FwPackageUri** parameter too**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="d28af-211">Kies **Planning**.</span><span class="sxs-lookup"><span data-stu-id="d28af-211">Choose **Schedule**.</span></span> <span data-ttu-id="d28af-212">Hallo standaard is nu voor Hallo taak toorun.</span><span class="sxs-lookup"><span data-stu-id="d28af-212">hello default is for hello job toorun now.</span></span>

    ![Taak tooupdate Hallo firmware van apparaten Hallo geselecteerd maken][img-method-update]

> [!NOTE]
> <span data-ttu-id="d28af-214">Als u tooinvoke een methode op een bepaald apparaat wilt, kies **methoden** in Hallo **Apparaatdetails** deelvenster in plaats van een taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d28af-214">If you want tooinvoke a method on an individual device, choose **Methods** in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="d28af-215">Deze taak wordt aangeroepen Hallo **InitiateFirmwareUpdate** directe methode op alle Hallo apparaten ingeschakeld door het Hallo-filter.</span><span class="sxs-lookup"><span data-stu-id="d28af-215">This job invokes hello **InitiateFirmwareUpdate** direct method on all hello devices selected by hello filter.</span></span> <span data-ttu-id="d28af-216">Apparaten onmiddellijk tooIoT Hub reageren en start vervolgens asynchroon Hallo firmware updateproces.</span><span class="sxs-lookup"><span data-stu-id="d28af-216">Devices respond immediately tooIoT Hub and then initiate hello firmware update process asynchronously.</span></span> <span data-ttu-id="d28af-217">Hallo-apparaten bieden statusinformatie over Hallo firmware updateproces via gemelde eigenschapswaarden, zoals wordt weergegeven in de volgende schermafbeeldingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="d28af-217">hello devices provide status information about hello firmware update process through reported property values, as shown in hello following screenshots.</span></span> <span data-ttu-id="d28af-218">Kies Hallo **vernieuwen** pictogram tooupdate Hallo informatie in de apparaat- en lijsten Hallo:</span><span class="sxs-lookup"><span data-stu-id="d28af-218">Choose hello **Refresh** icon tooupdate hello information in hello device and job lists:</span></span>

<span data-ttu-id="d28af-219">![Takenlijst Hallo lijst firmware-update wordt uitgevoerd met][img-update-1]
![lijst met apparaten weer met de status van de firmware-update][img-update-2]
![taak lijst met Hallo firmware-update een lijst voltooid][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="d28af-219">![Job list showing hello firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing hello firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="d28af-220">U kunt taken toorun plannen tijdens een onderhoudsvenster aangewezen in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="d28af-220">In a production environment, you can schedule jobs toorun during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="d28af-221">Samenvatting van scenario</span><span class="sxs-lookup"><span data-stu-id="d28af-221">Scenario review</span></span>

<span data-ttu-id="d28af-222">In dit scenario kunt u een mogelijk probleem met enkele van uw externe apparaten met behulp van de geschiedenis van waarschuwingen Hallo op Hallo dashboard en een filter geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="d28af-222">In this scenario, you identified a potential issue with some of your remote devices using hello alarm history on hello dashboard and a filter.</span></span> <span data-ttu-id="d28af-223">U vervolgens gebruikte Hallo-filter en een taak tooremotely configureren Hallo apparaten tooprovide toohelp voor meer informatie Hallo probleem opsporen.</span><span class="sxs-lookup"><span data-stu-id="d28af-223">You then used hello filter and a job tooremotely configure hello devices tooprovide more information toohelp diagnose hello issue.</span></span> <span data-ttu-id="d28af-224">Ten slotte, gebruikt u een filter en een taak tooschedule onderhoud op Hallo van invloed op apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-224">Finally, you used a filter and a job tooschedule maintenance on hello affected devices.</span></span> <span data-ttu-id="d28af-225">Als u toohello dashboard terugkeert, kunt u controleren dat er niet langer zijn alle alarmen afkomstig zijn van apparaten in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="d28af-225">If you return toohello dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="d28af-226">U kunt een filter tooverify die Hallo firmware op alle Hallo-apparaten in uw oplossing up-to-date is en of er niet meer slecht apparaten:</span><span class="sxs-lookup"><span data-stu-id="d28af-226">You can use a filter tooverify that hello firmware is up-to-date on all hello devices in your solution and that there are no more unhealthy devices:</span></span>

![Filter dat laat zien dat alle apparaten bijgewerkte firmware hebben][img-updated]

![Filter dat laat zien dat alle apparaten in orde zijn][img-healthy]

## <a name="other-features"></a><span data-ttu-id="d28af-229">Andere functies</span><span class="sxs-lookup"><span data-stu-id="d28af-229">Other features</span></span>

<span data-ttu-id="d28af-230">Hallo volgende secties worden enkele aanvullende functies van Hallo vooraf geconfigureerde oplossing voor externe controle die niet als onderdeel van het vorige scenario Hallo zijn beschreven.</span><span class="sxs-lookup"><span data-stu-id="d28af-230">hello following sections describe some additional features of hello remote monitoring preconfigured solution that are not described as part of hello previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="d28af-231">Kolommen aanpassen</span><span class="sxs-lookup"><span data-stu-id="d28af-231">Customize columns</span></span>

<span data-ttu-id="d28af-232">U kunt aanpassen Hallo informatie wordt weergegeven in de lijst met apparaten Hallo door te kiezen **kolom editor**.</span><span class="sxs-lookup"><span data-stu-id="d28af-232">You can customize hello information shown in hello device list by choosing **Column editor**.</span></span> <span data-ttu-id="d28af-233">U kunt kolommen die gerapporteerde eigenschaps- en tagwaarden weergeven, toevoegen en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d28af-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="d28af-234">U kunt ook de volgorde en namen van de kolommen wijzigen:</span><span class="sxs-lookup"><span data-stu-id="d28af-234">You can also reorder and rename columns:</span></span>

   ![Lijst met kolommen editor bewaartermijn Hallo apparaat][img-columneditor]

### <a name="customize-hello-device-icon"></a><span data-ttu-id="d28af-236">Pictogram Hallo aanpassen</span><span class="sxs-lookup"><span data-stu-id="d28af-236">Customize hello device icon</span></span>

<span data-ttu-id="d28af-237">U kunt aanpassen Hallo apparaat pictogram weergegeven in de lijst met apparaten op Hallo van Hallo **Apparaatdetails** paneel als volgt:</span><span class="sxs-lookup"><span data-stu-id="d28af-237">You can customize hello device icon displayed in hello device list from hello **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="d28af-238">Kies Hallo pen pictogram tooopen hello **bewerken installatiekopie** Configuratiescherm voor een apparaat:</span><span class="sxs-lookup"><span data-stu-id="d28af-238">Choose hello pencil icon tooopen hello **Edit image** panel for a device:</span></span>

   ![De afbeeldingseditor van het apparaat openen][img-startimageedit]

1. <span data-ttu-id="d28af-240">Een nieuwe installatiekopie uploaden of gebruik een van de bestaande installatiekopieën Hallo en kies vervolgens **opslaan**:</span><span class="sxs-lookup"><span data-stu-id="d28af-240">Either upload a new image or use one of hello existing images and then choose **Save**:</span></span>

   ![De afbeelding van het apparaat bewerken in de afbeeldingseditor][img-imageedit]

1. <span data-ttu-id="d28af-242">Hallo nu geselecteerde afbeelding wordt weergegeven in Hallo **pictogram** kolom voor Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="d28af-242">hello image you selected now displays in hello **Icon** column for hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="d28af-243">Hallo-installatiekopie is opgeslagen in blob storage.</span><span class="sxs-lookup"><span data-stu-id="d28af-243">hello image is stored in blob storage.</span></span> <span data-ttu-id="d28af-244">Een tag op in Hallo apparaat twin bevat een koppeling toohello installatiekopie in de blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="d28af-244">A tag in hello device twin contains a link toohello image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="d28af-245">Een apparaat toevoegen</span><span class="sxs-lookup"><span data-stu-id="d28af-245">Add a device</span></span>

<span data-ttu-id="d28af-246">Wanneer u Hallo vooraf geconfigureerde oplossing implementeert, worden automatisch 25 voorbeeld-apparaten die u in de lijst met Hallo apparaten zien kunt inrichten.</span><span class="sxs-lookup"><span data-stu-id="d28af-246">When you deploy hello preconfigured solution, you automatically provision 25 sample devices that you can see in hello device list.</span></span> <span data-ttu-id="d28af-247">Deze apparaten zijn *gesimuleerde apparaten* uitgevoerd in een Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="d28af-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="d28af-248">Gesimuleerde apparaten eenvoudiger voor u tooexperiment met Hallo vooraf geconfigureerde oplossing zonder Hallo nodig toodeploy echte apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-248">Simulated devices make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical devices.</span></span> <span data-ttu-id="d28af-249">Als u dat een echte toohello oplossing tooconnect wilt, raadpleegt u Hallo [verbinding maken met uw vooraf geconfigureerde oplossing voor externe controle apparaat toohello] [ lnk-connect-rm] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d28af-249">If you do want tooconnect a real device toohello solution, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="d28af-250">Hallo volgende stappen ziet u hoe tooadd een gesimuleerd apparaat toohello-oplossing:</span><span class="sxs-lookup"><span data-stu-id="d28af-250">hello following steps show you how tooadd a simulated device toohello solution:</span></span>

1. <span data-ttu-id="d28af-251">Navigeer terug toohello lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-251">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="d28af-252">tooadd een apparaat, kies **+ een apparaat toevoegen** in Hallo linkerbenedenhoek.</span><span class="sxs-lookup"><span data-stu-id="d28af-252">tooadd a device, choose **+ Add A Device** in hello bottom left corner.</span></span>

   ![Een apparaat toohello vooraf geconfigureerde oplossing toevoegen][img-adddevice]

1. <span data-ttu-id="d28af-254">Kies **nieuwe toevoegen** op Hallo **gesimuleerd apparaat** tegel.</span><span class="sxs-lookup"><span data-stu-id="d28af-254">Choose **Add New** on hello **Simulated Device** tile.</span></span>

   ![Nieuwe apparaatgegevens in het dashboard instellen][img-addnew]

   <span data-ttu-id="d28af-256">In aanvulling toocreating een nieuw gesimuleerd apparaat, kunt u ook toevoegen een fysiek apparaat als u ervoor toocreate kiest een **aangepast apparaat**.</span><span class="sxs-lookup"><span data-stu-id="d28af-256">In addition toocreating a new simulated device, you can also add a physical device if you choose toocreate a **Custom Device**.</span></span> <span data-ttu-id="d28af-257">toolearn meer informatie over het verbinden van fysieke apparaten toohello-oplossing, Zie [verbinding maken met uw apparaat toohello IoT Suite vooraf geconfigureerde oplossing voor externe controle][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="d28af-257">toolearn more about connecting physical devices toohello solution, see [Connect your device toohello IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="d28af-258">Selecteer **Laat mij mijn eigen apparaat-id definiëren** en voer de unieke id van een apparaatnaam in, zoals **mijnapparaat_01**.</span><span class="sxs-lookup"><span data-stu-id="d28af-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="d28af-259">Kies **Maken**.</span><span class="sxs-lookup"><span data-stu-id="d28af-259">Choose **Create**.</span></span>

   ![Een nieuw apparaat opslaan][img-definedevice]

1. <span data-ttu-id="d28af-261">In stap 3 van **een gesimuleerd apparaat toevoegen**, kies **gedaan** tooreturn toohello lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-261">In step 3 of **Add a simulated device**, choose **Done** tooreturn toohello device list.</span></span>

1. <span data-ttu-id="d28af-262">U kunt uw apparaat weergeven **uitgevoerd** in de lijst met Hallo-apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-262">You can view your device **Running** in hello device list.</span></span>

    ![Nieuw apparaat weergeven in de apparatenlijst][img-runningnew]

1. <span data-ttu-id="d28af-264">U kunt ook weergeven Hallo gesimuleerde telemetrie van het nieuwe apparaat op Hallo dashboard:</span><span class="sxs-lookup"><span data-stu-id="d28af-264">You can also view hello simulated telemetry from your new device on hello dashboard:</span></span>

    ![Telemetrie voor nieuw apparaat weergeven][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="d28af-266">Een apparaat uitschakelen en verwijderen</span><span class="sxs-lookup"><span data-stu-id="d28af-266">Disable and delete a device</span></span>

<span data-ttu-id="d28af-267">U kunt een apparaat uitschakelen en nadat het is uitgeschakeld kunt u het verwijderen:</span><span class="sxs-lookup"><span data-stu-id="d28af-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Een apparaat uitschakelen en verwijderen][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="d28af-269">Een regel toevoegen</span><span class="sxs-lookup"><span data-stu-id="d28af-269">Add a rule</span></span>

<span data-ttu-id="d28af-270">Er zijn geen regels voor het nieuwe apparaat Hallo die u zojuist hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d28af-270">There are no rules for hello new device you just added.</span></span> <span data-ttu-id="d28af-271">In deze sectie voegt u een regel die een waarschuwing activeert wanneer de temperatuur Hallo gemeld door Hallo nieuwe apparaat 47 graden overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="d28af-271">In this section, you add a rule that triggers an alarm when hello temperature reported by hello new device exceeds 47 degrees.</span></span> <span data-ttu-id="d28af-272">Voordat u begint, zoals u ziet dat Hallo telemetriegeschiedenis voor nieuwe apparaat Hallo op Hallo dashboard toont Hallo apparaat temperatuur nooit meer dan 45 graden.</span><span class="sxs-lookup"><span data-stu-id="d28af-272">Before you start, notice that hello telemetry history for hello new device on hello dashboard shows hello device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="d28af-273">Navigeer terug toohello lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-273">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="d28af-274">tooadd een regel voor Hallo-apparaat, selecteert u het nieuwe apparaat in Hallo **lijst met apparaten**, en kies vervolgens **regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d28af-274">tooadd a rule for hello device, select your new device in hello **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="d28af-275">Een regel maken die gebruikmaakt van **temperatuur** als Hallo gegevensveld gebruikt en **AlarmTemp** zoals Hallo uitvoer wanneer Hallo temperatuur 47 graden overschrijdt:</span><span class="sxs-lookup"><span data-stu-id="d28af-275">Create a rule that uses **Temperature** as hello data field and uses **AlarmTemp** as hello output when hello temperature exceeds 47 degrees:</span></span>

    ![Een apparaatregel toevoegen][img-adddevicerule]

1. <span data-ttu-id="d28af-277">kiest u uw wijzigingen toosave **regels opslaan en weergeven**.</span><span class="sxs-lookup"><span data-stu-id="d28af-277">toosave your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="d28af-278">Kies **opdrachten** in Hallo deelvenster Apparaatdetails voor het nieuwe apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="d28af-278">Choose **Commands** in hello device details pane for hello new device.</span></span>

    ![Een apparaatregel toevoegen][img-adddevicerule2]

1. <span data-ttu-id="d28af-280">Selecteer **ChangeSetPointTemp** van Hallo Opdrachtlijst en stel **SetPointTemp** too45.</span><span class="sxs-lookup"><span data-stu-id="d28af-280">Select **ChangeSetPointTemp** from hello command list and set **SetPointTemp** too45.</span></span> <span data-ttu-id="d28af-281">Kies vervolgens **Opdracht verzenden**:</span><span class="sxs-lookup"><span data-stu-id="d28af-281">Then choose **Send Command**:</span></span>

    ![Een apparaatregel toevoegen][img-adddevicerule3]

1. <span data-ttu-id="d28af-283">Navigeer terug toohello dashboard.</span><span class="sxs-lookup"><span data-stu-id="d28af-283">Navigate back toohello dashboard.</span></span> <span data-ttu-id="d28af-284">Na korte tijd, ziet u een nieuwe vermelding in Hallo **geschiedenis van waarschuwingen** deelvenster wanneer Hallo temperatuur gemeld door het nieuwe apparaat Hallo-47 graden overschrijdt:</span><span class="sxs-lookup"><span data-stu-id="d28af-284">After a short time, you will see a new entry in hello **Alarm History** pane when hello temperature reported by your new device exceeds hello 47-degree threshold:</span></span>

    ![Een apparaatregel toevoegen][img-adddevicerule4]

1. <span data-ttu-id="d28af-286">U kunt bekijken en bewerken van alle regels op Hallo **regels** pagina van Hallo dashboard:</span><span class="sxs-lookup"><span data-stu-id="d28af-286">You can review and edit all your rules on hello **Rules** page of hello dashboard:</span></span>

    ![Lijst met apparaatregels][img-rules]

1. <span data-ttu-id="d28af-288">U kunt bekijken en bewerken van alle Hallo-acties die kunnen worden uitgevoerd in reactie tooa regel op Hallo **acties** pagina van Hallo dashboard:</span><span class="sxs-lookup"><span data-stu-id="d28af-288">You can review and edit all hello actions that can be taken in response tooa rule on hello **Actions** page of hello dashboard:</span></span>

    ![Lijst met apparaatacties][img-actions]

> [!NOTE]
> <span data-ttu-id="d28af-290">Het is mogelijk toodefine acties die een e-mailbericht kunnen verzenden of SMS in antwoord tooa regel of integreren met een line-of-business-systeem via een [logische App][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="d28af-290">It is possible toodefine actions that can send an email message or SMS in response tooa rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="d28af-291">Zie voor meer informatie, Hallo [tooyour van logische App verbinding maken met Azure IoT Suite Remote Monitoring vooraf geconfigureerde oplossing][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="d28af-291">For more information, see hello [Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="d28af-292">Filters beheren</span><span class="sxs-lookup"><span data-stu-id="d28af-292">Manage filters</span></span>

<span data-ttu-id="d28af-293">In de lijst met apparaten van hello, kunt u maken, opslaan en laden van filters toodisplay een aangepaste lijst met apparaten verbonden tooyour hub.</span><span class="sxs-lookup"><span data-stu-id="d28af-293">In hello device list, you can create, save, and reload filters toodisplay a customized list of devices connected tooyour hub.</span></span> <span data-ttu-id="d28af-294">een filter toocreate:</span><span class="sxs-lookup"><span data-stu-id="d28af-294">toocreate a filter:</span></span>

1. <span data-ttu-id="d28af-295">Kies Hallo bewerken filterpictogram boven Hallo-lijst van apparaten:</span><span class="sxs-lookup"><span data-stu-id="d28af-295">Choose hello edit filter icon above hello list of devices:</span></span>

    ![Open Hallo filter-editor][img-editfiltericon]

1. <span data-ttu-id="d28af-297">In Hallo **Filter editor**, Hallo velden, operators en waarden toofilter Hallo apparatenlijst toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d28af-297">In hello **Filter editor**, add hello fields, operators, and values toofilter hello device list.</span></span> <span data-ttu-id="d28af-298">U kunt meerdere componenten toorefine uw filter toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d28af-298">You can add multiple clauses toorefine your filter.</span></span> <span data-ttu-id="d28af-299">Kies **Filter** tooapply Hallo filter:</span><span class="sxs-lookup"><span data-stu-id="d28af-299">Choose **Filter** tooapply hello filter:</span></span>

    ![Een filter maken][img-filtereditor]

1. <span data-ttu-id="d28af-301">In dit voorbeeld wordt Hallo lijst gefilterd op fabrikant en het modelnummer:</span><span class="sxs-lookup"><span data-stu-id="d28af-301">In this example, hello list is filtered by manufacturer and model number:</span></span>

    ![Gefilterde lijst][img-filterelist]

1. <span data-ttu-id="d28af-303">toosave uw filter met de naam van een aangepaste kiezen Hallo **opslaan als** pictogram:</span><span class="sxs-lookup"><span data-stu-id="d28af-303">toosave your filter with a custom name, choose hello **Save as** icon:</span></span>

    ![Een filter opslaan][img-savefilter]

1. <span data-ttu-id="d28af-305">tooreapply een filter dat u eerder hebt opgeslagen, kies Hallo **opgeslagen filter openen** pictogram:</span><span class="sxs-lookup"><span data-stu-id="d28af-305">tooreapply a filter you saved previously, choose hello **Open saved filter** icon:</span></span>

    ![Een filter openen][img-openfilter]

<span data-ttu-id="d28af-307">U kunt filters maken op basis van apparaat-id, apparaatstatus gewenste eigenschappen, gerapporteerde eigenschappen en tags.</span><span class="sxs-lookup"><span data-stu-id="d28af-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="d28af-308">U uw eigen aangepaste labels tooa apparaat toevoegen in Hallo **labels** sectie Hallo **Apparaatdetails** deelvenster of een taak tooupdate labels worden uitgevoerd op meerdere apparaten.</span><span class="sxs-lookup"><span data-stu-id="d28af-308">You add your own custom tags tooa device in hello **Tags** section of hello **Device Details** panel, or run a job tooupdate tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="d28af-309">In Hallo **Filter editor**, kunt u Hallo **weergave Geavanceerd** tooedit Hallo querytekst rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="d28af-309">In hello **Filter editor**, you can use hello **Advanced view** tooedit hello query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="d28af-310">Opdrachten</span><span class="sxs-lookup"><span data-stu-id="d28af-310">Commands</span></span>

<span data-ttu-id="d28af-311">Van Hallo **Apparaatdetails** Configuratiescherm kunt u opdrachten toohello apparaat verzenden.</span><span class="sxs-lookup"><span data-stu-id="d28af-311">From hello **Device Details** panel, you can send commands toohello device.</span></span> <span data-ttu-id="d28af-312">Wanneer een apparaat eerst wordt gestart, stuurt informatie over het Hallo-opdrachten dat het toohello-oplossing ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="d28af-312">When a device first starts, it sends information about hello commands it supports toohello solution.</span></span> <span data-ttu-id="d28af-313">Zie voor een beschrijving van Hallo verschillen tussen opdrachten en -methoden [Azure IoT Hub cloud-naar-apparaat opties][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="d28af-313">For a discussion of hello differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="d28af-314">Kies **opdrachten** in Hallo **Apparaatdetails** Configuratiescherm voor het geselecteerde apparaat Hallo:</span><span class="sxs-lookup"><span data-stu-id="d28af-314">Choose **Commands** in hello **Device Details** panel for hello selected device:</span></span>

   ![Apparaatopdrachten in het dashboard][img-devicecommands]

1. <span data-ttu-id="d28af-316">Selecteer **PingDevice** uit Hallo Opdrachtlijst.</span><span class="sxs-lookup"><span data-stu-id="d28af-316">Select **PingDevice** from hello command list.</span></span>

1. <span data-ttu-id="d28af-317">Kies **Opdracht verzenden**.</span><span class="sxs-lookup"><span data-stu-id="d28af-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="d28af-318">U kunt de status van de Hallo Hallo-opdracht in de opdrachtgeschiedenis Hallo kunt zien.</span><span class="sxs-lookup"><span data-stu-id="d28af-318">You can see hello status of hello command in hello command history.</span></span>

   ![Opdrachtstatus in het dashboard][img-pingcommand]

<span data-ttu-id="d28af-320">Hallo oplossing houdt Hallo status van elke opdracht die worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="d28af-320">hello solution tracks hello status of each command it sends.</span></span> <span data-ttu-id="d28af-321">In eerste instantie Hallo resultaat is **in behandeling**.</span><span class="sxs-lookup"><span data-stu-id="d28af-321">Initially hello result is **Pending**.</span></span> <span data-ttu-id="d28af-322">Wanneer Hallo apparaat meldt dat het Hallo-opdracht heeft uitgevoerd, Hallo resultaat te ingesteld**geslaagd**.</span><span class="sxs-lookup"><span data-stu-id="d28af-322">When hello device reports that it has executed hello command, hello result is set too**Success**.</span></span>

## <a name="behind-hello-scenes"></a><span data-ttu-id="d28af-323">Achter de schermen Hallo</span><span class="sxs-lookup"><span data-stu-id="d28af-323">Behind hello scenes</span></span>

<span data-ttu-id="d28af-324">Wanneer u een vooraf geconfigureerde oplossing implementeert, maakt Hallo implementatieproces meerdere resources in hello Azure-abonnement u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d28af-324">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="d28af-325">U kunt deze resources weergeven in hello Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="d28af-325">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="d28af-326">Hallo-implementatieproces maakt een **resourcegroep** met een naam op basis van Hallo-naam die u voor uw vooraf geconfigureerde oplossing kiest:</span><span class="sxs-lookup"><span data-stu-id="d28af-326">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Vooraf geconfigureerde oplossing in hello Azure-portal][img-portal]

<span data-ttu-id="d28af-328">U kunt instellingen Hallo van elke resource weergeven door deze te selecteren in lijst van resources in de resourcegroep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d28af-328">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="d28af-329">U kunt ook de broncode Hallo voor Hallo vooraf geconfigureerde oplossing weergeven.</span><span class="sxs-lookup"><span data-stu-id="d28af-329">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="d28af-330">Hallo voor externe controle van de broncode van de vooraf geconfigureerde oplossing is in Hallo [azure-iot-remote-monitoring] [ lnk-rmgithub] GitHub-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="d28af-330">hello remote monitoring preconfigured solution source code is in hello [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="d28af-331">Hallo **DeviceAdministration** map bevat de broncode Hallo voor Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="d28af-331">hello **DeviceAdministration** folder contains hello source code for hello dashboard.</span></span>
* <span data-ttu-id="d28af-332">Hallo **Simulator** map bevat de broncode Hallo voor Hallo gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="d28af-332">hello **Simulator** folder contains hello source code for hello simulated device.</span></span>
* <span data-ttu-id="d28af-333">Hallo **EventProcessor** map bevat de broncode Hallo voor Hallo back-endproces dat Hallo binnenkomende telemetrie verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d28af-333">hello **EventProcessor** folder contains hello source code for hello back-end process that handles hello incoming telemetry.</span></span>

<span data-ttu-id="d28af-334">Wanneer u klaar bent, kunt u Hallo vooraf geconfigureerde oplossing verwijderen uit uw Azure-abonnement op Hallo [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="d28af-334">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="d28af-335">Deze site kunt u alle resources die zijn ingericht toen u Hallo vooraf geconfigureerde oplossing maakte Hallo tooeasily-verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d28af-335">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="d28af-336">tooensure u Alles verwijderen gerelateerde toohello vooraf geconfigureerde oplossing, te verwijderen op Hallo [azureiotsuite.com] [ lnk-azureiotsuite] site en het Hallo-resourcegroep in Hallo portal niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d28af-336">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site and do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d28af-337">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d28af-337">Next Steps</span></span>

<span data-ttu-id="d28af-338">Nu dat u een werkende vooraf geconfigureerde oplossing hebt geïmplementeerd, kunt u blijven aan de slag met IoT Suite door te lezen Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d28af-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="d28af-339">[Walkthrough over de vooraf geconfigureerde oplossing voor externe bewaking][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="d28af-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="d28af-340">[Verbinding maken met uw apparaat toohello vooraf geconfigureerde oplossing voor externe controle][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="d28af-340">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="d28af-341">[Machtigingen op Hallo azureiotsuite.com site][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="d28af-341">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

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