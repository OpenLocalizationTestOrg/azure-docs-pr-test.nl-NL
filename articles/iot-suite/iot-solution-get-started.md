---
title: 'MyDriving Azure IoT-voorbeeld: snel aan de slag | Microsoft Docs'
description: Aan de slag met een app die is een uitgebreide demonstratie van het bouwen van een IoT-systeem met Microsoft Azure, met inbegrip van de Stream Analytics, Machine Learning en Event Hubs.
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 031b492df1f186087e7b91102cbb44f552999293
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="5f534-103">MyDriving IoT-systeem: snel starten</span><span class="sxs-lookup"><span data-stu-id="5f534-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="5f534-104">MyDriving is een systeem dat laat zien van het ontwerp en de implementatie van een typische [Internet der dingen](iot-suite-overview.md) (IoT)-oplossing die worden verzameld van telemetrie vanaf apparaten, verwerkt die gegevens in de cloud en machine learning voor het bieden van toepassing is een adaptieve antwoord.</span><span class="sxs-lookup"><span data-stu-id="5f534-104">MyDriving is a system that demonstrates the design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in the cloud, and applies machine learning to provide an adaptive response.</span></span> <span data-ttu-id="5f534-105">Demonstratie van de gegevens over uw reizen auto geregistreerd met behulp van gegevens uit uw mobiele telefoon en een netwerkadapter die u gegevens van uw auto controlesysteem verzamelt.</span><span class="sxs-lookup"><span data-stu-id="5f534-105">The demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="5f534-106">Deze gegevens maakt gebruik van deze feedback wilt geven over uw aangedreven style in vergelijking met andere gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5f534-106">It uses this data to provide feedback on your driving style in comparison to other users.</span></span>

<span data-ttu-id="5f534-107">Het werkelijke doel van MyDriving is weer om u bij het maken van uw eigen IoT-oplossing is gestart.</span><span class="sxs-lookup"><span data-stu-id="5f534-107">The real purpose of MyDriving is to get you started in creating your own IoT solution.</span></span> <span data-ttu-id="5f534-108">Maar voordat dat we u doorgaat met de MyDriving-app--als lid van ons team van de gebruiker test.</span><span class="sxs-lookup"><span data-stu-id="5f534-108">But before that, let’s get you going with the MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="5f534-109">Dit biedt u een ervaring van de app en het systeem erachter als een consument voordat u de architectuur dieper.</span><span class="sxs-lookup"><span data-stu-id="5f534-109">This gives you an experience of the app and the system behind it as a consumer, before you delve into the architecture.</span></span> <span data-ttu-id="5f534-110">Ook vindt u naar HockeyApp, een cool manier om de alfa en beta-distributies van uw apps te beheren voor het testen van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5f534-110">It also introduces you to HockeyApp, a cool way of managing the alpha and beta distributions of your apps to test users.</span></span>

## <a name="use-the-mobile-experience"></a><span data-ttu-id="5f534-111">Gebruik de mobiele-ervaring</span><span class="sxs-lookup"><span data-stu-id="5f534-111">Use the mobile experience</span></span>
<span data-ttu-id="5f534-112">Als u een Android, iOS of Windows 10-apparaat hebt, kunt u de MyDriving-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f534-112">You can use the MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="5f534-113">Android en Windows 10 Mobile-installatie</span><span class="sxs-lookup"><span data-stu-id="5f534-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="5f534-114">Op uw apparaat:</span><span class="sxs-lookup"><span data-stu-id="5f534-114">On your device:</span></span>

1. <span data-ttu-id="5f534-115">Ontwikkeling van apps toestaan:</span><span class="sxs-lookup"><span data-stu-id="5f534-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="5f534-116">Android: In **instellingen** > **beveiliging**, toestaan dat apps uit **onbekende bronnen**.</span><span class="sxs-lookup"><span data-stu-id="5f534-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="5f534-117">Windows 10: In **instellingen** > **Updates** > **voor ontwikkelaars**stelt **ontwikkelaarsmodus**.</span><span class="sxs-lookup"><span data-stu-id="5f534-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="5f534-118">Deelnemen aan ons testteam beta door met registreert of aanmeldt, [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="5f534-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="5f534-119">HockeyApp kunt gemakkelijk eerdere releases van uw app testen gebruikers distribueren.</span><span class="sxs-lookup"><span data-stu-id="5f534-119">HockeyApp makes it easy to distribute early releases of your app to test users.</span></span>
   
   <span data-ttu-id="5f534-120">Als u Windows 10, gebruikt u de browser Edge.</span><span class="sxs-lookup"><span data-stu-id="5f534-120">If you’re using Windows 10, use the Edge browser.</span></span>
   
   <span data-ttu-id="5f534-121">Als u een deelnemer Build 2016, aanmelden met het hetzelfde Microsoft-account e-mailbericht dat u geregistreerd voor de Conferentie via een van de Microsoft-knoppen.</span><span class="sxs-lookup"><span data-stu-id="5f534-121">If you were a Build 2016 attendee, sign in with the same Microsoft account email that you registered for the conference, by using one of the Microsoft buttons.</span></span> <span data-ttu-id="5f534-122">U bent al aangemeld met HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="5f534-122">You’re already signed up with HockeyApp.</span></span>
   
   ![HockeyApp aanmeldingsscherm](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="5f534-124">Download en installeer de app vanaf deze locatie:</span><span class="sxs-lookup"><span data-stu-id="5f534-124">Download and install the app from here:</span></span>
   
   * [<span data-ttu-id="5f534-125">Android</span><span class="sxs-lookup"><span data-stu-id="5f534-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="5f534-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="5f534-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="5f534-127">Er zijn twee items.</span><span class="sxs-lookup"><span data-stu-id="5f534-127">There are two items.</span></span> <span data-ttu-id="5f534-128">Installeer het certificaat in **vertrouwde personen**.</span><span class="sxs-lookup"><span data-stu-id="5f534-128">Install the certificate in **Trusted People**.</span></span> <span data-ttu-id="5f534-129">Installeer de app.</span><span class="sxs-lookup"><span data-stu-id="5f534-129">Then install the app.</span></span>

<span data-ttu-id="5f534-130">*Problemen bij het starten van de app op Windows 10 Mobile?*</span><span class="sxs-lookup"><span data-stu-id="5f534-130">*Any issues starting the app on Windows 10 Mobile?*</span></span> <span data-ttu-id="5f534-131">Uw telefoon is mogelijk een update of twee achter.</span><span class="sxs-lookup"><span data-stu-id="5f534-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="5f534-132">Zorg ervoor dat u de meest recente updates beschikt of installeren:</span><span class="sxs-lookup"><span data-stu-id="5f534-132">Make sure you've got the latest updates, or install:</span></span>

* [<span data-ttu-id="5f534-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="5f534-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="5f534-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="5f534-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="5f534-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="5f534-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="5f534-136">iOS-installatie</span><span class="sxs-lookup"><span data-stu-id="5f534-136">iOS installation</span></span>
<span data-ttu-id="5f534-137">Als u Build 2016 hebt gevolgd, moet u de app downloaden als lid van ons testteam op HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="5f534-137">If you attended Build 2016, download the app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="5f534-138">Op uw iOS-apparaat, moet u zich aanmelden bij [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="5f534-138">On your iOS device, sign in to [HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="5f534-139">Gebruik een van de Microsoft-aanmelden-knoppen en meld u aan met het hetzelfde Microsoft-account e-mailbericht dat u bij de Conferentie geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="5f534-139">Use one of the Microsoft sign-in buttons, and sign in with the same Microsoft account email that you registered with the conference.</span></span> <span data-ttu-id="5f534-140">(Gebruik niet de velden e-mailadres en wachtwoord).</span><span class="sxs-lookup"><span data-stu-id="5f534-140">(Don’t use the email and password fields.)</span></span>
   
   ![HockeyApp aanmeldingsscherm](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="5f534-142">In het dashboard HockeyApp MyDriving Selecteer en download het.</span><span class="sxs-lookup"><span data-stu-id="5f534-142">In the HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="5f534-143">De bètaversie van HockeyApp toestaan:</span><span class="sxs-lookup"><span data-stu-id="5f534-143">Authorize the beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="5f534-144">a.</span><span class="sxs-lookup"><span data-stu-id="5f534-144">a.</span></span> <span data-ttu-id="5f534-145">Ga naar **instellingen** > **algemene** > **profielen en beheer van apparaten.**</span><span class="sxs-lookup"><span data-stu-id="5f534-145">Go to **Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="5f534-146">b.</span><span class="sxs-lookup"><span data-stu-id="5f534-146">b.</span></span> <span data-ttu-id="5f534-147">Vertrouwt de **bits Stadium GmbH** certificaat.</span><span class="sxs-lookup"><span data-stu-id="5f534-147">Trust the **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="5f534-148">Als u hebt niet de Build 2016 letten, kunt u bouwen en implementeren van de app:</span><span class="sxs-lookup"><span data-stu-id="5f534-148">If you didn’t attend Build 2016, you can build and deploy the app yourself:</span></span>

1. <span data-ttu-id="5f534-149">De code downloaden [vanuit GitHub].</span><span class="sxs-lookup"><span data-stu-id="5f534-149">Download the code [from GitHub].</span></span>
2. <span data-ttu-id="5f534-150">Bouwen en implementeren met [met Xamarin].</span><span class="sxs-lookup"><span data-stu-id="5f534-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="5f534-151">Meer informatie in de [MyDriving handleiding](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="5f534-151">Find more details in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="5f534-152">Ophalen van een OBD-adapter (optioneel)</span><span class="sxs-lookup"><span data-stu-id="5f534-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="5f534-153">Dit is het onderdeel dat dit een echte Internet der dingen-systeem is!</span><span class="sxs-lookup"><span data-stu-id="5f534-153">This is the part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="5f534-154">Kunt u de app zonder een, maar meer plezier met de echte is, en ze niet duur.</span><span class="sxs-lookup"><span data-stu-id="5f534-154">You can use the app without one, but it’s more fun with the real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="5f534-155">Ingebouwde diagnostische gegevens (OBD) is de functie van uw auto die de garage gebruikt voor het optimaliseren van uw auto en onderzoeken van oneven geluiden en waarschuwing lichten.</span><span class="sxs-lookup"><span data-stu-id="5f534-155">On-board diagnostics (OBD) is the feature of your car that the garage uses to tune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="5f534-156">Tenzij uw auto van goede antiquity, vindt u een socket ergens in de stuurcabine, doorgaans achter een flap onder het dashboard.</span><span class="sxs-lookup"><span data-stu-id="5f534-156">Unless your car is of great antiquity, you’ll find a socket somewhere in the cabin, typically behind a flap under the dashboard.</span></span> <span data-ttu-id="5f534-157">U kunt met de juiste connector metrische gegevens van de prestaties van de engine van ophalen en bepaalde wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="5f534-157">With the right connector, you can get metrics of the engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="5f534-158">Een connector OBD kan goedkoop worden gekocht vanuit de gebruikelijke plaatsen.</span><span class="sxs-lookup"><span data-stu-id="5f534-158">An OBD connector can be purchased cheaply from the usual places.</span></span> <span data-ttu-id="5f534-159">Deze verbinding maakt met behulp van de Bluetooth- of Wi-Fi met een app op uw telefoon.</span><span class="sxs-lookup"><span data-stu-id="5f534-159">It connects by using Bluetooth or Wi-Fi to an app on your phone.</span></span>

<span data-ttu-id="5f534-160">In dit geval gaan we uw auto verbinding te maken met de cloud.</span><span class="sxs-lookup"><span data-stu-id="5f534-160">In this case, we’re going to connect your car to the cloud.</span></span> <span data-ttu-id="5f534-161">De rechtstreekse verbinding tussen de OBD is naar uw telefoon, maar de app werkt als een relay.</span><span class="sxs-lookup"><span data-stu-id="5f534-161">The direct connection from the OBD is to your phone, but our app works as a relay.</span></span> <span data-ttu-id="5f534-162">Telemetrie van uw auto wordt verzonden door naar de MyDriving IoT-hub, waar deze wordt verwerkt uw reizen weg aanmelden en uw aangedreven stijl te beoordelen.</span><span class="sxs-lookup"><span data-stu-id="5f534-162">Your car's telemetry is sent straight to the MyDriving IoT hub, where it's processed to log your road trips and assess your driving style.</span></span>

<span data-ttu-id="5f534-163">Sluit een OBD-apparaat:</span><span class="sxs-lookup"><span data-stu-id="5f534-163">To connect an OBD device:</span></span>

1. <span data-ttu-id="5f534-164">Controleer of uw auto een OBD-socket.</span><span class="sxs-lookup"><span data-stu-id="5f534-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="5f534-165">Vraag een OBD-adapter:</span><span class="sxs-lookup"><span data-stu-id="5f534-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="5f534-166">Als u een Android- en Windows phone, moet u een adapter OBD II Bluetooth-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="5f534-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="5f534-167">We hebben gebruikt [BAFX producten 34t5 Bluetooth OBDII Scan Tool].</span><span class="sxs-lookup"><span data-stu-id="5f534-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="5f534-168">Als u een iOS-telefoon, moet u een Wi-Fi-functionaliteit OBD-adapter.</span><span class="sxs-lookup"><span data-stu-id="5f534-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="5f534-169">We hebben gebruikt [onderzoekprogramma OBDLink MX Wi-Fi: OBD-Adapter/diagnose Scanner].</span><span class="sxs-lookup"><span data-stu-id="5f534-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="5f534-170">Volg de instructies die worden geleverd met uw OBD-netwerkadapter aansluiten op uw telefoon.</span><span class="sxs-lookup"><span data-stu-id="5f534-170">Follow the instructions that come with your OBD adapter to connect it to your phone.</span></span> <span data-ttu-id="5f534-171">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="5f534-171">Keep the following in mind:</span></span>
   
   * <span data-ttu-id="5f534-172">Een Bluetooth-adapter moet worden gekoppeld aan de telefoon op de **instellingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="5f534-172">A Bluetooth adapter must be paired with the phone, on the **Settings** page.</span></span>
   * <span data-ttu-id="5f534-173">Een Wi-Fi-adapter moet een adres in het bereik 192.168.xxx.xxx hebben.</span><span class="sxs-lookup"><span data-stu-id="5f534-173">A Wi-Fi adapter must have an address in the range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="5f534-174">Als u verschillende auto's hebt, krijgt u een afzonderlijke adapter voor elke (maximaal drie).</span><span class="sxs-lookup"><span data-stu-id="5f534-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="5f534-175">Als u een adapter OBD geen hebt, wordt de app wordt nog steeds locatie en de snelheid van gegevens van de telefoon GPS-ontvanger verzonden naar de back-end en wordt u gevraagd of u wilt een OBD simuleren.</span><span class="sxs-lookup"><span data-stu-id="5f534-175">If you don’t have an OBD adapter, the app will still send location and speed data from the phone's GPS receiver to the back end and will ask if you want to simulate an OBD.</span></span>

<span data-ttu-id="5f534-176">U kunt meer informatie over hoe de app gebruikmaakt van gegevens van de adapter OBD- en opties voor het maken van uw eigen apparaat OBD in sectie 2.1 'IoT-apparaten,' de [MyDriving handleiding](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="5f534-176">You can find out more about how the app uses data from the OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-the-app"></a><span data-ttu-id="5f534-177">De app gebruiken</span><span class="sxs-lookup"><span data-stu-id="5f534-177">Use the app</span></span>
<span data-ttu-id="5f534-178">De app te starten.</span><span class="sxs-lookup"><span data-stu-id="5f534-178">Start the app.</span></span> <span data-ttu-id="5f534-179">Er is een initiële Quick Start u stapsgewijs door het hoe het werkt.</span><span class="sxs-lookup"><span data-stu-id="5f534-179">There’s an initial Quickstart to walk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="5f534-180">Uw reizen bijhouden</span><span class="sxs-lookup"><span data-stu-id="5f534-180">Track your trips</span></span>
<span data-ttu-id="5f534-181">Tik op de knop opnemen (big rode cirkel aan de onderkant van het scherm) voor het starten van een reis en tik nogmaals op om te beëindigen.</span><span class="sxs-lookup"><span data-stu-id="5f534-181">Tap the record button (big red circle at the bottom of the screen) to start a trip, and tap again to end.</span></span>

![Afbeelding van de knop opnemen voor reis bijhouden](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="5f534-183">Telkens wanneer die u een reis start als er geen OBD-apparaat, worden u gevraagd als u wilt gebruiken de simulator.</span><span class="sxs-lookup"><span data-stu-id="5f534-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want to use the simulator.</span></span>

<span data-ttu-id="5f534-184">Aan het einde van een reis, tikt u op de knop stoppen, en u een samenvatting.</span><span class="sxs-lookup"><span data-stu-id="5f534-184">At the end of a trip, tap the stop button, and you get a summary.</span></span>

![Voorbeeld van een reis samenvatting](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="5f534-186">Bekijk uw reizen</span><span class="sxs-lookup"><span data-stu-id="5f534-186">Review your trips</span></span>
![Voorbeeld van een eerdere reis](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="5f534-188">Uw profiel bekijken</span><span class="sxs-lookup"><span data-stu-id="5f534-188">Review your profile</span></span>
![Voorbeeld van een groot-stijl-profiel](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="5f534-190">Stuur ons uw feedback test</span><span class="sxs-lookup"><span data-stu-id="5f534-190">Send us your test feedback</span></span>
<span data-ttu-id="5f534-191">Omdat we MyDriving om te helpen aan de slag met uw eigen IoT-systemen gemaakt, willen we zeker graag van u over hoe goed werkt.</span><span class="sxs-lookup"><span data-stu-id="5f534-191">Because we created MyDriving to help jumpstart your own IoT systems, we certainly want to hear from you about how well it works.</span></span> <span data-ttu-id="5f534-192">Laat ons weten als:</span><span class="sxs-lookup"><span data-stu-id="5f534-192">Let us know if:</span></span>

* <span data-ttu-id="5f534-193">U ondervindt problemen of uitdagingen.</span><span class="sxs-lookup"><span data-stu-id="5f534-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="5f534-194">Er is een extensiepunt zou om het meest geschikt is voor uw scenario.</span><span class="sxs-lookup"><span data-stu-id="5f534-194">There is an extension point that would make it more suitable to your scenario.</span></span>
* <span data-ttu-id="5f534-195">U vindt een efficiëntere manier voor het uitvoeren van bepaalde behoeften.</span><span class="sxs-lookup"><span data-stu-id="5f534-195">You find a more efficient way to accomplish certain needs.</span></span>
* <span data-ttu-id="5f534-196">U hebt andere suggesties voor het verbeteren van MyDriving of deze documentatie.</span><span class="sxs-lookup"><span data-stu-id="5f534-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="5f534-197">In de app MyDriving zelf, kunt u de ingebouwde HockeyApp feedback mechanisme: iOS en Android, net verleent op uw telefoon een schud of gebruik de **Feedback** menuopdracht.</span><span class="sxs-lookup"><span data-stu-id="5f534-197">Within the MyDriving app itself, you can use the built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use the **Feedback** menu command.</span></span> <span data-ttu-id="5f534-198">Dit wordt automatisch een schermopname koppelen zodat we weet wat u bent bespreken.</span><span class="sxs-lookup"><span data-stu-id="5f534-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="5f534-199">En als er vervelend crashes, HockeyApp de Vertel ons meer over deze crash logboeken verzamelt.</span><span class="sxs-lookup"><span data-stu-id="5f534-199">And if there are any unfortunate crashes, HockeyApp collects the crash logs to tell us about them.</span></span> <span data-ttu-id="5f534-200">U kunt ook feedback via de [HockeyApp-portal].</span><span class="sxs-lookup"><span data-stu-id="5f534-200">You can also give feedback through the [HockeyApp portal].</span></span>

<span data-ttu-id="5f534-201">U kunt ook het bestand een [probleem op GitHub], of laat een opmerking hieronder (en-us edition).</span><span class="sxs-lookup"><span data-stu-id="5f534-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="5f534-202">We hopen graag van u!</span><span class="sxs-lookup"><span data-stu-id="5f534-202">We look forward to hearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f534-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f534-203">Next steps</span></span>
* <span data-ttu-id="5f534-204">Verken de [MyDriving handleiding](http://aka.ms/mydrivingdocs) om te begrijpen hoe we hebt ontwikkeld en gebouwd van de gehele MyDriving-systeem.</span><span class="sxs-lookup"><span data-stu-id="5f534-204">Explore the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) to understand how we’ve designed and built the entire MyDriving system.</span></span>
* <span data-ttu-id="5f534-205">[Maken en implementeren van een systeem van uw eigen](iot-solution-build-system.md) met behulp van de Azure Resource Manager-scripts.</span><span class="sxs-lookup"><span data-stu-id="5f534-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="5f534-206">De [MyDriving handleiding](http://aka.ms/mydrivingdocs) helpt u ook bij gebieden waar u de meeste aanpassingen maakt.</span><span class="sxs-lookup"><span data-stu-id="5f534-206">The [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make the most customizations.</span></span>

<span data-ttu-id="5f534-207">[vanuit GitHub]: https://github.com/Azure-Samples/MyDriving</span><span class="sxs-lookup"><span data-stu-id="5f534-207">[from GitHub]: https://github.com/Azure-Samples/MyDriving</span></span>
<span data-ttu-id="5f534-208">[met Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/</span><span class="sxs-lookup"><span data-stu-id="5f534-208">[using Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/</span></span>
<span data-ttu-id="5f534-209">[BAFX producten 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS</span><span class="sxs-lookup"><span data-stu-id="5f534-209">[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS</span></span>
<span data-ttu-id="5f534-210">[onderzoekprogramma OBDLink MX Wi-Fi: OBD-Adapter/diagnose Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP</span><span class="sxs-lookup"><span data-stu-id="5f534-210">[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP</span></span>
<span data-ttu-id="5f534-211">[HockeyApp-portal]: https://rink.hockeyapp.org</span><span class="sxs-lookup"><span data-stu-id="5f534-211">[HockeyApp portal]: https://rink.hockeyapp.org</span></span>
<span data-ttu-id="5f534-212">[probleem op GitHub]: https://github.com/Azure-Samples/MyDriving/issues</span><span class="sxs-lookup"><span data-stu-id="5f534-212">[issue on GitHub]: https://github.com/Azure-Samples/MyDriving/issues</span></span>
