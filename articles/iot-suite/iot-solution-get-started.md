---
title: 'MyDriving Azure IoT-voorbeeld: snel aan de slag | Microsoft Docs'
description: Aan de slag met een app die is een uitgebreide demonstratie van het tooarchitect een IoT-systeem met Microsoft Azure, met inbegrip van de Stream Analytics, Machine Learning en Event Hubs.
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
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="598ba-103">MyDriving IoT-systeem: snel starten</span><span class="sxs-lookup"><span data-stu-id="598ba-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="598ba-104">MyDriving is een systeem dat laat Hallo ontwerpen en implementeren van een typische zien [Internet der dingen](iot-suite-overview.md) (IoT)-oplossing die worden verzameld van telemetrie vanaf apparaten, die gegevens in de cloud Hallo verwerkt en van toepassing is machine learning tooprovide een adaptieve antwoord.</span><span class="sxs-lookup"><span data-stu-id="598ba-104">MyDriving is a system that demonstrates hello design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in hello cloud, and applies machine learning tooprovide an adaptive response.</span></span> <span data-ttu-id="598ba-105">Hallo-demonstratie registreert gegevens over uw reizen auto op basis van gegevens uit uw mobiele telefoon en een netwerkadapter die u gegevens van uw auto controlesysteem verzamelt.</span><span class="sxs-lookup"><span data-stu-id="598ba-105">hello demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="598ba-106">Deze gegevens tooprovide feedback wordt gebruikt op uw aangedreven stijl in vergelijking tooother gebruikers.</span><span class="sxs-lookup"><span data-stu-id="598ba-106">It uses this data tooprovide feedback on your driving style in comparison tooother users.</span></span>

<span data-ttu-id="598ba-107">Hallo werkelijke doel van MyDriving is tooget die u gestart bij het maken van uw eigen IoT-oplossing.</span><span class="sxs-lookup"><span data-stu-id="598ba-107">hello real purpose of MyDriving is tooget you started in creating your own IoT solution.</span></span> <span data-ttu-id="598ba-108">Maar vóór Hiermee kunt u beginnen met Hallo MyDriving app zelf--als lid van ons team van de gebruiker test.</span><span class="sxs-lookup"><span data-stu-id="598ba-108">But before that, let’s get you going with hello MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="598ba-109">Dit biedt u een ervaring van Hallo-app en Hallo systeem erachter als een consument voordat u dieper Hallo-architectuur.</span><span class="sxs-lookup"><span data-stu-id="598ba-109">This gives you an experience of hello app and hello system behind it as a consumer, before you delve into hello architecture.</span></span> <span data-ttu-id="598ba-110">Deze ook vindt u tooHockeyApp, een cool manier om Hallo alfa en beta distributies van uw apps tootest gebruikers te beheren.</span><span class="sxs-lookup"><span data-stu-id="598ba-110">It also introduces you tooHockeyApp, a cool way of managing hello alpha and beta distributions of your apps tootest users.</span></span>

## <a name="use-hello-mobile-experience"></a><span data-ttu-id="598ba-111">Hallo mobiele ervaring gebruiken</span><span class="sxs-lookup"><span data-stu-id="598ba-111">Use hello mobile experience</span></span>
<span data-ttu-id="598ba-112">U kunt Hallo MyDriving app gebruiken als u een Android, iOS of Windows 10-apparaat hebt.</span><span class="sxs-lookup"><span data-stu-id="598ba-112">You can use hello MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="598ba-113">Android en Windows 10 Mobile-installatie</span><span class="sxs-lookup"><span data-stu-id="598ba-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="598ba-114">Op uw apparaat:</span><span class="sxs-lookup"><span data-stu-id="598ba-114">On your device:</span></span>

1. <span data-ttu-id="598ba-115">Ontwikkeling van apps toestaan:</span><span class="sxs-lookup"><span data-stu-id="598ba-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="598ba-116">Android: In **instellingen** > **beveiliging**, toestaan dat apps uit **onbekende bronnen**.</span><span class="sxs-lookup"><span data-stu-id="598ba-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="598ba-117">Windows 10: In **instellingen** > **Updates** > **voor ontwikkelaars**stelt **ontwikkelaarsmodus**.</span><span class="sxs-lookup"><span data-stu-id="598ba-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="598ba-118">Deelnemen aan ons testteam beta door met registreert of aanmeldt, [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="598ba-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="598ba-119">HockeyApp maakt het eenvoudig toodistribute prereleases van uw app tootest-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="598ba-119">HockeyApp makes it easy toodistribute early releases of your app tootest users.</span></span>
   
   <span data-ttu-id="598ba-120">Als u Windows 10, gebruikt u Hallo Edge-browser.</span><span class="sxs-lookup"><span data-stu-id="598ba-120">If you’re using Windows 10, use hello Edge browser.</span></span>
   
   <span data-ttu-id="598ba-121">Als u een deelnemer Build 2016, meld u aan met Hallo hetzelfde Microsoft-account e-mailbericht dat u voor Hallo conferentie, met behulp van een Microsoft-knoppen Hallo geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="598ba-121">If you were a Build 2016 attendee, sign in with hello same Microsoft account email that you registered for hello conference, by using one of hello Microsoft buttons.</span></span> <span data-ttu-id="598ba-122">U bent al aangemeld met HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="598ba-122">You’re already signed up with HockeyApp.</span></span>
   
   ![HockeyApp aanmeldingsscherm](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="598ba-124">Download en installeer Hallo app vanaf hier:</span><span class="sxs-lookup"><span data-stu-id="598ba-124">Download and install hello app from here:</span></span>
   
   * [<span data-ttu-id="598ba-125">Android</span><span class="sxs-lookup"><span data-stu-id="598ba-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="598ba-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="598ba-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="598ba-127">Er zijn twee items.</span><span class="sxs-lookup"><span data-stu-id="598ba-127">There are two items.</span></span> <span data-ttu-id="598ba-128">Installeren van certificaat in Hallo **vertrouwde personen**.</span><span class="sxs-lookup"><span data-stu-id="598ba-128">Install hello certificate in **Trusted People**.</span></span> <span data-ttu-id="598ba-129">Hallo-app installeren.</span><span class="sxs-lookup"><span data-stu-id="598ba-129">Then install hello app.</span></span>

<span data-ttu-id="598ba-130">*Hallo-app starten op Windows 10 Mobile problemen?*</span><span class="sxs-lookup"><span data-stu-id="598ba-130">*Any issues starting hello app on Windows 10 Mobile?*</span></span> <span data-ttu-id="598ba-131">Uw telefoon is mogelijk een update of twee achter.</span><span class="sxs-lookup"><span data-stu-id="598ba-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="598ba-132">Zorg ervoor dat u de nieuwste updates Hallo heeft of installeert:</span><span class="sxs-lookup"><span data-stu-id="598ba-132">Make sure you've got hello latest updates, or install:</span></span>

* [<span data-ttu-id="598ba-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="598ba-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="598ba-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="598ba-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="598ba-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="598ba-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="598ba-136">iOS-installatie</span><span class="sxs-lookup"><span data-stu-id="598ba-136">iOS installation</span></span>
<span data-ttu-id="598ba-137">Als u Build 2016 hebt gevolgd, moet u Hallo-app downloaden als lid van ons testteam op HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="598ba-137">If you attended Build 2016, download hello app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="598ba-138">Op uw iOS-apparaat, meld u aan te[HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="598ba-138">On your iOS device, sign in too[HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="598ba-139">Gebruik een van de Microsoft-aanmelden-knoppen Hallo en meld u aan met dezelfde e-mail van de Microsoft-account dat u bij Hallo conferentie geregistreerd Hallo.</span><span class="sxs-lookup"><span data-stu-id="598ba-139">Use one of hello Microsoft sign-in buttons, and sign in with hello same Microsoft account email that you registered with hello conference.</span></span> <span data-ttu-id="598ba-140">(Gebruik niet Hallo e-mailadres en wachtwoord velden).</span><span class="sxs-lookup"><span data-stu-id="598ba-140">(Don’t use hello email and password fields.)</span></span>
   
   ![HockeyApp aanmeldingsscherm](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="598ba-142">In Hallo HockeyApp dashboard MyDriving Selecteer en download het.</span><span class="sxs-lookup"><span data-stu-id="598ba-142">In hello HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="598ba-143">Autoriseren hello bètaversie van HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="598ba-143">Authorize hello beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="598ba-144">a.</span><span class="sxs-lookup"><span data-stu-id="598ba-144">a.</span></span> <span data-ttu-id="598ba-145">Ga te**instellingen** > **algemene** > **profielen en beheer van apparaten.**</span><span class="sxs-lookup"><span data-stu-id="598ba-145">Go too**Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="598ba-146">b.</span><span class="sxs-lookup"><span data-stu-id="598ba-146">b.</span></span> <span data-ttu-id="598ba-147">Hallo vertrouwen **bits Stadium GmbH** certificaat.</span><span class="sxs-lookup"><span data-stu-id="598ba-147">Trust hello **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="598ba-148">Als u niet de Build 2016 aandacht, kunt u app bouwen en implementeren Hallo zelf:</span><span class="sxs-lookup"><span data-stu-id="598ba-148">If you didn’t attend Build 2016, you can build and deploy hello app yourself:</span></span>

1. <span data-ttu-id="598ba-149">Hallo code downloaden [vanuit GitHub].</span><span class="sxs-lookup"><span data-stu-id="598ba-149">Download hello code [from GitHub].</span></span>
2. <span data-ttu-id="598ba-150">Bouwen en implementeren met [met Xamarin].</span><span class="sxs-lookup"><span data-stu-id="598ba-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="598ba-151">Meer informatie vinden in Hallo [MyDriving handleiding](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="598ba-151">Find more details in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="598ba-152">Ophalen van een OBD-adapter (optioneel)</span><span class="sxs-lookup"><span data-stu-id="598ba-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="598ba-153">Dit is Hallo onderdeel waarmee dit een echte Internet der dingen-systeem!</span><span class="sxs-lookup"><span data-stu-id="598ba-153">This is hello part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="598ba-154">Hallo app zonder, kunt u maar meer plezier met Hallo echt een ding is, en ze niet duur.</span><span class="sxs-lookup"><span data-stu-id="598ba-154">You can use hello app without one, but it’s more fun with hello real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="598ba-155">Ingebouwde diagnostische gegevens (OBD) is de functie Hallo auto die Hallo garage gebruikt tootune van uw auto en onderzoeken van oneven geluiden en waarschuwing lichten.</span><span class="sxs-lookup"><span data-stu-id="598ba-155">On-board diagnostics (OBD) is hello feature of your car that hello garage uses tootune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="598ba-156">Tenzij uw auto van goede antiquity, vindt u een socket ergens in Hallo stuurcabine, doorgaans achter een flap onder Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="598ba-156">Unless your car is of great antiquity, you’ll find a socket somewhere in hello cabin, typically behind a flap under hello dashboard.</span></span> <span data-ttu-id="598ba-157">U kunt met de juiste connector hello, metrische gegevens van Hallo motorprestaties ophalen en bepaalde wijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="598ba-157">With hello right connector, you can get metrics of hello engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="598ba-158">Een OBD-connector kan worden gekocht goedkoop Hallo gangbare locaties.</span><span class="sxs-lookup"><span data-stu-id="598ba-158">An OBD connector can be purchased cheaply from hello usual places.</span></span> <span data-ttu-id="598ba-159">Deze verbinding maakt met behulp van de Bluetooth- of Wi-Fi tooan-app op uw telefoon.</span><span class="sxs-lookup"><span data-stu-id="598ba-159">It connects by using Bluetooth or Wi-Fi tooan app on your phone.</span></span>

<span data-ttu-id="598ba-160">In dit geval gaan we tooconnect uw auto toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="598ba-160">In this case, we’re going tooconnect your car toohello cloud.</span></span> <span data-ttu-id="598ba-161">Hallo rechtstreekse verbinding tussen Hallo OBD tooyour telefoonnummer is, maar onze app werkt als een relay.</span><span class="sxs-lookup"><span data-stu-id="598ba-161">hello direct connection from hello OBD is tooyour phone, but our app works as a relay.</span></span> <span data-ttu-id="598ba-162">Telemetrie van uw auto wordt verzonden, rechte toohello MyDriving IoT hub, waar deze zich toolog verwerkt uw reizen weg en uw aangedreven stijl te beoordelen.</span><span class="sxs-lookup"><span data-stu-id="598ba-162">Your car's telemetry is sent straight toohello MyDriving IoT hub, where it's processed toolog your road trips and assess your driving style.</span></span>

<span data-ttu-id="598ba-163">een apparaat OBD-tooconnect:</span><span class="sxs-lookup"><span data-stu-id="598ba-163">tooconnect an OBD device:</span></span>

1. <span data-ttu-id="598ba-164">Controleer of uw auto een OBD-socket.</span><span class="sxs-lookup"><span data-stu-id="598ba-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="598ba-165">Vraag een OBD-adapter:</span><span class="sxs-lookup"><span data-stu-id="598ba-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="598ba-166">Als u een Android- en Windows phone, moet u een adapter OBD II Bluetooth-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="598ba-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="598ba-167">We hebben gebruikt [BAFX producten 34t5 Bluetooth OBDII Scan Tool].</span><span class="sxs-lookup"><span data-stu-id="598ba-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="598ba-168">Als u een iOS-telefoon, moet u een Wi-Fi-functionaliteit OBD-adapter.</span><span class="sxs-lookup"><span data-stu-id="598ba-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="598ba-169">We hebben gebruikt [onderzoekprogramma OBDLink MX Wi-Fi: OBD-Adapter/diagnose Scanner].</span><span class="sxs-lookup"><span data-stu-id="598ba-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="598ba-170">Volg Hallo-instructies die worden geleverd met uw OBD-adapter tooconnect het tooyour telefoon.</span><span class="sxs-lookup"><span data-stu-id="598ba-170">Follow hello instructions that come with your OBD adapter tooconnect it tooyour phone.</span></span> <span data-ttu-id="598ba-171">Houd er rekening mee Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="598ba-171">Keep hello following in mind:</span></span>
   
   * <span data-ttu-id="598ba-172">Een Bluetooth-adapter moet worden gekoppeld aan het Hallo-telefoon, op Hallo **instellingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="598ba-172">A Bluetooth adapter must be paired with hello phone, on hello **Settings** page.</span></span>
   * <span data-ttu-id="598ba-173">Een Wi-Fi-adapter moet een adres Hallo bereik 192.168.xxx.xxx hebben.</span><span class="sxs-lookup"><span data-stu-id="598ba-173">A Wi-Fi adapter must have an address in hello range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="598ba-174">Als u verschillende auto's hebt, krijgt u een afzonderlijke adapter voor elke (maximaal drie).</span><span class="sxs-lookup"><span data-stu-id="598ba-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="598ba-175">Als u geen een OBD-adapter, stuurt Hallo app nog steeds locatie en gegevens van de snelheid van van Hallo telefoon GPS ontvanger toohello terug wordt gevraagd of u een OBD toosimulate wilt beëindigen.</span><span class="sxs-lookup"><span data-stu-id="598ba-175">If you don’t have an OBD adapter, hello app will still send location and speed data from hello phone's GPS receiver toohello back end and will ask if you want toosimulate an OBD.</span></span>

<span data-ttu-id="598ba-176">U vindt hier meer over hoe Hallo app gebruikmaakt van gegevens uit de Hallo OBD-adapter en opties voor het maken van uw eigen apparaat OBD in sectie 2.1 'IoT-apparaten,' in hello [MyDriving handleiding](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="598ba-176">You can find out more about how hello app uses data from hello OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-hello-app"></a><span data-ttu-id="598ba-177">Hallo-app gebruiken</span><span class="sxs-lookup"><span data-stu-id="598ba-177">Use hello app</span></span>
<span data-ttu-id="598ba-178">Hallo-app te starten.</span><span class="sxs-lookup"><span data-stu-id="598ba-178">Start hello app.</span></span> <span data-ttu-id="598ba-179">Er is een initiële Quick Start-toowalk u stapsgewijs hoe het werkt.</span><span class="sxs-lookup"><span data-stu-id="598ba-179">There’s an initial Quickstart toowalk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="598ba-180">Uw reizen bijhouden</span><span class="sxs-lookup"><span data-stu-id="598ba-180">Track your trips</span></span>
<span data-ttu-id="598ba-181">Tik op Hallo record knop (big rode cirkel onderaan Hallo welkomstscherm) toostart reis en tik nogmaals op tooend.</span><span class="sxs-lookup"><span data-stu-id="598ba-181">Tap hello record button (big red circle at hello bottom of hello screen) toostart a trip, and tap again tooend.</span></span>

![Afbeelding van knop voor Hallo-record voor reis bijhouden](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="598ba-183">Telkens wanneer die u een reis start als er geen OBD-apparaat, u gevraagd als u wilt dat toouse Hallo simulator.</span><span class="sxs-lookup"><span data-stu-id="598ba-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want toouse hello simulator.</span></span>

<span data-ttu-id="598ba-184">Hallo na een reis Tik Hallo stop-knop, en u een samenvatting worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="598ba-184">At hello end of a trip, tap hello stop button, and you get a summary.</span></span>

![Voorbeeld van een reis samenvatting](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="598ba-186">Bekijk uw reizen</span><span class="sxs-lookup"><span data-stu-id="598ba-186">Review your trips</span></span>
![Voorbeeld van een eerdere reis](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="598ba-188">Uw profiel bekijken</span><span class="sxs-lookup"><span data-stu-id="598ba-188">Review your profile</span></span>
![Voorbeeld van een groot-stijl-profiel](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="598ba-190">Stuur ons uw feedback test</span><span class="sxs-lookup"><span data-stu-id="598ba-190">Send us your test feedback</span></span>
<span data-ttu-id="598ba-191">Omdat we MyDriving toohelp aan de slag met uw eigen IoT-systemen gemaakt, willen we zeker toohear van u over hoe goed werkt.</span><span class="sxs-lookup"><span data-stu-id="598ba-191">Because we created MyDriving toohelp jumpstart your own IoT systems, we certainly want toohear from you about how well it works.</span></span> <span data-ttu-id="598ba-192">Laat ons weten als:</span><span class="sxs-lookup"><span data-stu-id="598ba-192">Let us know if:</span></span>

* <span data-ttu-id="598ba-193">U ondervindt problemen of uitdagingen.</span><span class="sxs-lookup"><span data-stu-id="598ba-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="598ba-194">Er is een extensiepunt waaruit zou geschikte tooyour scenario.</span><span class="sxs-lookup"><span data-stu-id="598ba-194">There is an extension point that would make it more suitable tooyour scenario.</span></span>
* <span data-ttu-id="598ba-195">U vindt een efficiëntere manier tooaccomplish bepaalde behoeften.</span><span class="sxs-lookup"><span data-stu-id="598ba-195">You find a more efficient way tooaccomplish certain needs.</span></span>
* <span data-ttu-id="598ba-196">U hebt andere suggesties voor het verbeteren van MyDriving of deze documentatie.</span><span class="sxs-lookup"><span data-stu-id="598ba-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="598ba-197">Binnen Hallo MyDriving app zelf, kunt u Hallo ingebouwde HockeyApp feedback mechanisme: iOS en Android, net verleent op uw telefoon een schud of gebruik Hallo **Feedback** menuopdracht.</span><span class="sxs-lookup"><span data-stu-id="598ba-197">Within hello MyDriving app itself, you can use hello built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use hello **Feedback** menu command.</span></span> <span data-ttu-id="598ba-198">Dit wordt automatisch een schermopname koppelen zodat we weet wat u bent bespreken.</span><span class="sxs-lookup"><span data-stu-id="598ba-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="598ba-199">En als er vervelend crashes, HockeyApp verzamelt Hallo crash logboeken tootell ons informatie hierover.</span><span class="sxs-lookup"><span data-stu-id="598ba-199">And if there are any unfortunate crashes, HockeyApp collects hello crash logs tootell us about them.</span></span> <span data-ttu-id="598ba-200">U kunt ook feedback via Hallo [HockeyApp-portal].</span><span class="sxs-lookup"><span data-stu-id="598ba-200">You can also give feedback through hello [HockeyApp portal].</span></span>

<span data-ttu-id="598ba-201">U kunt ook het bestand een [probleem op GitHub], of laat een opmerking hieronder (en-us edition).</span><span class="sxs-lookup"><span data-stu-id="598ba-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="598ba-202">We hopen toohearing van u!</span><span class="sxs-lookup"><span data-stu-id="598ba-202">We look forward toohearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="598ba-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="598ba-203">Next steps</span></span>
* <span data-ttu-id="598ba-204">Hallo verkennen [MyDriving handleiding](http://aka.ms/mydrivingdocs) toounderstand hoe we hebt ontwikkeld en gebouwd Hallo gehele MyDriving-systeem.</span><span class="sxs-lookup"><span data-stu-id="598ba-204">Explore hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) toounderstand how we’ve designed and built hello entire MyDriving system.</span></span>
* <span data-ttu-id="598ba-205">[Maken en implementeren van een systeem van uw eigen](iot-solution-build-system.md) met behulp van de Azure Resource Manager-scripts.</span><span class="sxs-lookup"><span data-stu-id="598ba-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="598ba-206">Hallo [MyDriving handleiding](http://aka.ms/mydrivingdocs) helpt u ook bij gebieden waarin u Hallo meeste aanpassingen zult.</span><span class="sxs-lookup"><span data-stu-id="598ba-206">hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make hello most customizations.</span></span>

[vanuit GitHub]: https://github.com/Azure-Samples/MyDriving
[met Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX producten 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[onderzoekprogramma OBDLink MX Wi-Fi: OBD-Adapter/diagnose Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp-portal]: https://rink.hockeyapp.org
[probleem op GitHub]: https://github.com/Azure-Samples/MyDriving/issues
