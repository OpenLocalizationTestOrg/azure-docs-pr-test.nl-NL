---
title: aaaIoT DevKit toocloud - verbinding maken met IoT DevKit AZ3166 tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en toosend gegevens toohello Azure-cloudplatform van IoT DevKit AZ3166 tooAzure IoT Hub voor deze verbinding in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="a2945-103">Verbinding maken met IoT DevKit AZ3166 tooAzure IoT-Hub in de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="a2945-103">Connect IoT DevKit AZ3166 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="a2945-104">Hallo [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) kan worden gebruikt toodevelop en prototype Internet der dingen (IoT) oplossingen gebruik van Microsoft Azure-services.</span><span class="sxs-lookup"><span data-stu-id="a2945-104">hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used toodevelop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="a2945-105">Het bevat een compatibel mededelingenbord Arduino met uitgebreide randapparatuur en sensoren, een open source mededelingenbord pakket en een groeiende [projecten catalogus](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span><span class="sxs-lookup"><span data-stu-id="a2945-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="a2945-106">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="a2945-106">What you do</span></span>
<span data-ttu-id="a2945-107">Verbinding maken met [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub maken, de temperatuur en vochtigheid gegevens verzamelen Hallo van sensoren en Hallo gegevens tooIoT hub te verzenden.</span><span class="sxs-lookup"><span data-stu-id="a2945-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub that you create, collect hello temperature and humidity data from sensors and send hello data tooIoT hub.</span></span>

<span data-ttu-id="a2945-108">Heb je nog een DevKit?</span><span class="sxs-lookup"><span data-stu-id="a2945-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="a2945-109">Ophalen van een nieuwe [hier](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="a2945-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="a2945-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="a2945-110">What you learn</span></span>

* <span data-ttu-id="a2945-111">Hoe tooconnect IoT DevKit tooWireless toegang wijst u en uw ontwikkelingsomgeving voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="a2945-111">How tooconnect IoT DevKit tooWireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="a2945-112">Hoe toocreate een IoT-hub en een apparaat registreren voor MXChip IoT DevKit.</span><span class="sxs-lookup"><span data-stu-id="a2945-112">How toocreate an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="a2945-113">Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeld van toepassing op MXChip IoT DevKit.</span><span class="sxs-lookup"><span data-stu-id="a2945-113">How toocollect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="a2945-114">Hoe Hallo toosend sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a2945-114">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a2945-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="a2945-115">What you need</span></span>

* <span data-ttu-id="a2945-116">Een MXChip IoT DevKit moederbord met een micro USB-kabel.</span><span class="sxs-lookup"><span data-stu-id="a2945-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="a2945-117">Nu downloaden</span><span class="sxs-lookup"><span data-stu-id="a2945-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="a2945-118">Een computer met Windows 10- of Mac OS 10.10 +</span><span class="sxs-lookup"><span data-stu-id="a2945-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="a2945-119">Een actief Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="a2945-119">An active Azure subscription</span></span>
  * <span data-ttu-id="a2945-120">Activeren van een [gratis 30-daagse evaluatieversie Microsoft Azure-account](https://azureinfo.microsoft.com/us-freetrial.html)</span><span class="sxs-lookup"><span data-stu-id="a2945-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="a2945-121">Bereid uw hardware</span><span class="sxs-lookup"><span data-stu-id="a2945-121">Prepare your hardware</span></span>

<span data-ttu-id="a2945-122">Hallo hardware tooyour computer aansluiten.</span><span class="sxs-lookup"><span data-stu-id="a2945-122">Hook up hello hardware tooyour computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="a2945-123">U moet hardware</span><span class="sxs-lookup"><span data-stu-id="a2945-123">Hardware you need</span></span>

* <span data-ttu-id="a2945-124">DevKit mededelingenbord</span><span class="sxs-lookup"><span data-stu-id="a2945-124">DevKit board</span></span>
* <span data-ttu-id="a2945-125">Micro USB-kabel</span><span class="sxs-lookup"><span data-stu-id="a2945-125">Micro USB cable</span></span>

![ophalen van-slag-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a><span data-ttu-id="a2945-127">Verbind DevKit tooyour computer</span><span class="sxs-lookup"><span data-stu-id="a2945-127">Connect DevKit tooyour computer</span></span>

1. <span data-ttu-id="a2945-128">Verbinding maken met USB-end tooyour PC</span><span class="sxs-lookup"><span data-stu-id="a2945-128">Connect USB end tooyour PC</span></span>
2. <span data-ttu-id="a2945-129">Verbinding maken met Micro USB end toohello DevKit</span><span class="sxs-lookup"><span data-stu-id="a2945-129">Connect Micro USB end toohello DevKit</span></span>
3. <span data-ttu-id="a2945-130">Hallo groen LED volgende toopower bevestigt verbinding</span><span class="sxs-lookup"><span data-stu-id="a2945-130">hello green LED next toopower confirms connection</span></span>

![ophalen van-slag-verbinding](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="a2945-132">Wi-Fi configureren</span><span class="sxs-lookup"><span data-stu-id="a2945-132">Configure WiFi</span></span>

<span data-ttu-id="a2945-133">IoT-projecten zijn afhankelijk van verbinding met Internet.</span><span class="sxs-lookup"><span data-stu-id="a2945-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="a2945-134">Gebruik Hallo instructies tooconfigure hello DevKit tooconnect tooWiFi te volgen.</span><span class="sxs-lookup"><span data-stu-id="a2945-134">Use hello following instructions tooconfigure hello DevKit tooconnect tooWiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="a2945-135">Azië modus</span><span class="sxs-lookup"><span data-stu-id="a2945-135">Enter AP Mode</span></span>

<span data-ttu-id="a2945-136">Houd B, en vervolgens push en release Hallo herstelknop vervolgens release knop B. Uw DevKit opgeven voor het configureren van Wi-Fi AP-modus.</span><span class="sxs-lookup"><span data-stu-id="a2945-136">Hold down button B, then push and release hello reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="a2945-137">welkomstscherm worden weergegeven Hallo Service ingesteld Identifier(SSID) Hallo DevKit evenals Hallo portal IP-adres:</span><span class="sxs-lookup"><span data-stu-id="a2945-137">hello screen will display hello Service Set Identifier(SSID) of hello DevKit as well as hello configuration portal IP address:</span></span>

![ophalen van-slag-Wi-Fi-Azië](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a><span data-ttu-id="a2945-139">Verbinding maken met tooDevKit Azië</span><span class="sxs-lookup"><span data-stu-id="a2945-139">Connect tooDevKit AP</span></span>

<span data-ttu-id="a2945-140">Nu een andere Wi-Fi ingeschakeld apparaat (PC of mobiele telefoon) tooconnect toohello DevKit SSID (gemarkeerd in de bovenstaande Hallo) gebruiken, Hallo wachtwoord leeg laten.</span><span class="sxs-lookup"><span data-stu-id="a2945-140">Now, use another WiFi enabled device (PC or mobile phone) tooconnect toohello DevKit SSID (highlighted in hello screenshot above), leave hello password empty.</span></span>

![ophalen van-slag-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="a2945-142">Wi-Fi voor DevKit configureren</span><span class="sxs-lookup"><span data-stu-id="a2945-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="a2945-143">Open Hallo IP-adres weergegeven op het Hallo DevKit scherm op uw PC of mobiele telefoon browser Hallo Wi-Fi-netwerk Hallo DevKit tooconnect te gewenste selecteren, en typ Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a2945-143">Open hello IP address shown on hello DevKit screen on your PC or mobile phone browser, select hello WiFi network you want hello DevKit tooconnect to, then type hello password.</span></span> <span data-ttu-id="a2945-144">Klik op **Connect** toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a2945-144">Click **Connect** toocomplete:</span></span>

![ophalen van-slag-Wi-Fi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="a2945-146">Zodra het Hallo-verbinding is geslaagd, wordt in een paar seconden Hallo DevKit opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a2945-146">Once hello connection succeeds, hello DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="a2945-147">Als de is voltooid, ziet u Hallo Wi-Fi-naam en IP-adres op het welkomstscherm:</span><span class="sxs-lookup"><span data-stu-id="a2945-147">If succeeded, you will see hello WiFi name and IP address on hello screen:</span></span>

![ophalen van-slag-Wi-Fi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="a2945-149">Hallo IP-adres weergegeven in Hallo photo mogelijk niet overeen met de Hallo werkelijke IP toegewezen en weergegeven op het welkomstscherm DevKit.</span><span class="sxs-lookup"><span data-stu-id="a2945-149">hello IP address displayed in hello photo may not match hello actual IP assigned and displayed on hello DevKit screen.</span></span> <span data-ttu-id="a2945-150">Dit is normaal als Wi-Fi maakt gebruik van DHCP-toodynamically IP-adressen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="a2945-150">This is normal as WiFi uses DHCP toodynamically assign IPs.</span></span>

<span data-ttu-id="a2945-151">Nadat Wi-Fi is geconfigureerd, worden uw referenties persistent op Hallo-apparaat voor die verbinding, zelfs als losgekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a2945-151">After WiFi is configured, your credentials will be persisted on hello device for that connection, even if unplugged.</span></span> <span data-ttu-id="a2945-152">Bijvoorbeeld, als u Hallo DevKit geconfigureerd voor Wi-Fi thuis en vervolgens Hallo DevKit toohello office duurde, moet u tooreconfigure AP-modus (vanaf stap **Voer Azië modus**) tooconnect hello DevKit tooyour office Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a2945-152">For example, if you configured hello DevKit for WiFi in your home and then took hello DevKit toohello office, you will need tooreconfigure AP mode (starting at step **Enter AP Mode**) tooconnect hello DevKit tooyour office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="a2945-153">Aan de slag met DevKit</span><span class="sxs-lookup"><span data-stu-id="a2945-153">Start using DevKit</span></span>

<span data-ttu-id="a2945-154">Hallo standaard app uitgevoerd op DevKit wordt Hallo meest recente versie van de firmware Hallo controleren en sommige diagnose sensorgegevens weergeven voor u.</span><span class="sxs-lookup"><span data-stu-id="a2945-154">hello default app running on DevKit will check hello latest version of hello firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-toohello-latest-firmware"></a><span data-ttu-id="a2945-155">De meest recente firmware toohello bijwerken</span><span class="sxs-lookup"><span data-stu-id="a2945-155">Upgrade toohello latest firmware</span></span>

<span data-ttu-id="a2945-156">U wordt gevraagd op het welkomstscherm die zowel huidige en de meest recente firmwareversie Hallo als er een upgrade nodig.</span><span class="sxs-lookup"><span data-stu-id="a2945-156">You will be prompted on hello screen both hello current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="a2945-157">Ga als volgt [firmware bijwerken](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) tooupgrade helpen deze.</span><span class="sxs-lookup"><span data-stu-id="a2945-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade it.</span></span>

![ophalen van-slag-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="a2945-159">Dit is een eenmalige moeite, wanneer u begint met het ontwikkelen van op Hallo DevKit en uw app te uploaden, moet u de meest recente firmware Hallo worden geleverd met uw app.</span><span class="sxs-lookup"><span data-stu-id="a2945-159">This is a one-time effort, once you start developing on hello DevKit and upload your app, you will have hello latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="a2945-160">Verschillende sensoren testen</span><span class="sxs-lookup"><span data-stu-id="a2945-160">Test various sensors</span></span>

<span data-ttu-id="a2945-161">Druk op de knop B tootest sensoren, blijven indrukken en loslaten Hallo B knop toocycle via elke sensor.</span><span class="sxs-lookup"><span data-stu-id="a2945-161">Press button B tootest sensors, continue pressing and releasing hello B button toocycle through each sensor.</span></span>

![ophalen van-slag-sensoren](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="a2945-163">Ontwikkelingsomgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="a2945-163">Prepare development environment</span></span>

<span data-ttu-id="a2945-164">Nu gaat u tijd tooset van Hallo ontwikkelomgeving: hulpprogramma's en pakketten voor u toobuild bedwelmen IoT-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a2945-164">Now it's time tooset up hello development environment: tools and packages for you toobuild stunning IoT applications.</span></span> <span data-ttu-id="a2945-165">U kunt Windows of Mac OS-versie op basis van het besturingssysteem tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2945-165">You can choose Windows or macOS version according tooyour operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="a2945-166">Windows</span><span class="sxs-lookup"><span data-stu-id="a2945-166">Windows</span></span>

<span data-ttu-id="a2945-167">We raden u toouse Hallo installatie pakket tooprepare Hallo-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="a2945-167">We encourage you toouse hello installation package tooprepare hello development environment.</span></span> <span data-ttu-id="a2945-168">Als u problemen ondervindt, kunt u Hallo [handmatige stappen](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget doen.</span><span class="sxs-lookup"><span data-stu-id="a2945-168">If you encounter any issues, you can follow hello [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="a2945-169">Meest recente pakket te downloaden</span><span class="sxs-lookup"><span data-stu-id="a2945-169">Download latest package</span></span>

<span data-ttu-id="a2945-170">Hallo `.zip` bestand downloaden bevat alle benodigde hulpprogramma's en pakketten die zijn vereist voor de ontwikkeling van DevKit.</span><span class="sxs-lookup"><span data-stu-id="a2945-170">hello `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="a2945-171">Downloaden</span><span class="sxs-lookup"><span data-stu-id="a2945-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="a2945-172">Hallo `.zip` bestand bevat Hallo volgende hulpprogramma's en pakketten.</span><span class="sxs-lookup"><span data-stu-id="a2945-172">hello `.zip` file contains hello following tools and packages.</span></span> <span data-ttu-id="a2945-173">Als u al een aantal onderdelen geïnstalleerd hebt, Hallo script detecteert en ze overslaan.</span><span class="sxs-lookup"><span data-stu-id="a2945-173">If you already have some components installed, hello script will detect and skip them.</span></span>
> * <span data-ttu-id="a2945-174">Node.js en Yarn: Runtime voor het installatiescript Hallo en geautomatiseerde taken</span><span class="sxs-lookup"><span data-stu-id="a2945-174">Node.js and Yarn: Runtime for hello setup script and automated tasks</span></span>
> * <span data-ttu-id="a2945-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -platformoverschrijdende opdrachtregel ervaring voor het beheren van Azure-resources, Hallo MSI afhankelijke Python en pip bevat.</span><span class="sxs-lookup"><span data-stu-id="a2945-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, hello MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="a2945-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code-editor voor DevKit-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="a2945-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="a2945-177">[Visual Studio Code-uitbreiding voor Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Arduino kunt ontwikkelen in VS-Code</span><span class="sxs-lookup"><span data-stu-id="a2945-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="a2945-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): Hallo-extensie voor Arduino is afhankelijk van dit hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="a2945-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="a2945-179">DevKit mededelingenbord pakket: Hulpprogramma ketens, bibliotheken en projecten voor Hallo DevKit</span><span class="sxs-lookup"><span data-stu-id="a2945-179">DevKit Board Package: Tool chains, libraries and projects for hello DevKit</span></span>
> * <span data-ttu-id="a2945-180">ST koppeling hulpprogramma: Essentiële hulpprogramma's en stuurprogramma 's</span><span class="sxs-lookup"><span data-stu-id="a2945-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="a2945-181">Voer het script voor installatie</span><span class="sxs-lookup"><span data-stu-id="a2945-181">Run installation script</span></span>

<span data-ttu-id="a2945-182">Zoek in Windows Verkenner, Hallo `.zip` en pak deze uit, Ga naar `install.cmd`, klik met de rechtermuisknop en selecteer **'Als administrator uitvoeren'** toostart.</span><span class="sxs-lookup"><span data-stu-id="a2945-182">In Windows File Explorer, locate hello `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** toostart.</span></span>

![ophalen van-slag-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="a2945-184">Tijdens de installatie ziet u Hallo voortgang van elk hulpprogramma of het pakket.</span><span class="sxs-lookup"><span data-stu-id="a2945-184">During installation, you will see hello progress of each tool or package.</span></span>

![ophalen van-slag-installatie](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a><span data-ttu-id="a2945-186">Stuurprogramma's tooinstall bevestigen</span><span class="sxs-lookup"><span data-stu-id="a2945-186">Confirm tooinstall drivers</span></span>

<span data-ttu-id="a2945-187">Hallo VS-Code voor de extensie Arduino afhankelijk van Hallo Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="a2945-187">hello VS Code for Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="a2945-188">Als dit Hallo eerst die u Hallo Arduino IDE installeert, kunt u zich na vragen aan gebruiker tooinstall relevante stuurprogramma's:</span><span class="sxs-lookup"><span data-stu-id="a2945-188">If this is hello first time you are installing hello Arduino IDE, you will be prompted tooinstall relevant drivers:</span></span>

![ophalen van-slag-stuurprogramma](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="a2945-190">Het duurt ongeveer 10 minuten toofinish installatie, afhankelijk van uw Internet-snelheid.</span><span class="sxs-lookup"><span data-stu-id="a2945-190">It should take around 10 minutes toofinish installation depending on your Internet speed.</span></span> <span data-ttu-id="a2945-191">Zodra het Hallo-installatie is voltooid, ziet u Visual Studio Code en Arduino IDE snelkoppelingen op het bureaublad.</span><span class="sxs-lookup"><span data-stu-id="a2945-191">Once hello installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="a2945-192">Van tijd tot tijd, wanneer u Code tegenover start, wordt u gevraagd met een fout die Arduino IDE of verwante mededelingenbord pakket niet vinden.</span><span class="sxs-lookup"><span data-stu-id="a2945-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="a2945-193">toosolve deze sluiten VS-Code Arduino IDE eenmaal starten en VS-Code moet Arduino IDE pad correct vinden.</span><span class="sxs-lookup"><span data-stu-id="a2945-193">toosolve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="a2945-194">Mac OS (Preview)</span><span class="sxs-lookup"><span data-stu-id="a2945-194">macOS (Preview)</span></span>

<span data-ttu-id="a2945-195">Volg deze stappen tooprepare-ontwikkelomgeving op Mac OS.</span><span class="sxs-lookup"><span data-stu-id="a2945-195">Follow these steps tooprepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="a2945-196">Azure CLI 2.0 installeren</span><span class="sxs-lookup"><span data-stu-id="a2945-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="a2945-197">Ga als volgt Hallo [officiële handleiding](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="a2945-197">Follow hello [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span></span>

<span data-ttu-id="a2945-198">Azure CLI 2.0 installeren met een `curl` opdracht:</span><span class="sxs-lookup"><span data-stu-id="a2945-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="a2945-199">En start de opdrachtshell voor wijzigingen tootake effect:</span><span class="sxs-lookup"><span data-stu-id="a2945-199">And restart your command shell for changes tootake effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="a2945-200">Arduino IDE installeren</span><span class="sxs-lookup"><span data-stu-id="a2945-200">Install Arduino IDE</span></span>

<span data-ttu-id="a2945-201">Hallo Visual Studio Code Arduino-extensie is afhankelijk van Hallo Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="a2945-201">hello Visual Studio Code Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="a2945-202">Download en installeer Hallo [Arduino IDE voor Mac OS](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="a2945-202">Download and install hello [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="a2945-203">Visual Studio Code installeren</span><span class="sxs-lookup"><span data-stu-id="a2945-203">Install Visual Studio Code</span></span>

<span data-ttu-id="a2945-204">Download en installeer [Visual Studio Code voor Mac OS](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="a2945-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="a2945-205">Dit is de primaire ontwikkelprogramma Hallo voor het bouwen van DevKit IoT-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a2945-205">This will be hello primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="a2945-206">Meest recente pakket te downloaden</span><span class="sxs-lookup"><span data-stu-id="a2945-206">Download latest package</span></span>

1. <span data-ttu-id="a2945-207">Installeer Node.js.</span><span class="sxs-lookup"><span data-stu-id="a2945-207">Install Node.js.</span></span> <span data-ttu-id="a2945-208">U kunt de Pakketbeheer populaire Mac OS [Homebrew](https://brew.sh/) of [vooraf gemaakte installatieprogramma](https://nodejs.org/en/download/) tooinstall deze.</span><span class="sxs-lookup"><span data-stu-id="a2945-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) tooinstall it.</span></span>

2. <span data-ttu-id="a2945-209">Download `.zip` -bestand met taak-scripts die zijn vereist voor de ontwikkeling van DevKit in VS-Code.</span><span class="sxs-lookup"><span data-stu-id="a2945-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="a2945-210">Downloaden</span><span class="sxs-lookup"><span data-stu-id="a2945-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="a2945-211">Zoek Hallo `.zip` en pak het bestand.</span><span class="sxs-lookup"><span data-stu-id="a2945-211">Locate hello `.zip` and extract it.</span></span> <span data-ttu-id="a2945-212">Start vervolgens **Terminal** app en Voer Hallo opdrachten tooconfigure te volgen:</span><span class="sxs-lookup"><span data-stu-id="a2945-212">Then launch **Terminal** app and run hello following commands tooconfigure:</span></span>

   <span data-ttu-id="a2945-213">Verplaats de uitgepakte map tooyour Mac OS gebruikersmap:</span><span class="sxs-lookup"><span data-stu-id="a2945-213">Move extracted folder tooyour macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="a2945-214">Installeer `npm` pakketten:</span><span class="sxs-lookup"><span data-stu-id="a2945-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="a2945-215">VS-Code-uitbreiding voor Arduino installeren</span><span class="sxs-lookup"><span data-stu-id="a2945-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="a2945-216">Visual Studio Code kunt u tooinstall Marketplace extensies rechtstreeks in Hallo hulpprogramma, klikt u op Hallo extensies pictogram in Hallo linkermenu deelvenster en zoek vervolgens `Arduino` tooinstall:</span><span class="sxs-lookup"><span data-stu-id="a2945-216">Visual Studio Code allows you tooinstall Marketplace extensions directly in hello tool, simply click hello extensions icon in hello left menu pane and then search `Arduino` tooinstall:</span></span>

![installatie-extensies](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="a2945-218">DevKit mededelingenbord pakket installeren</span><span class="sxs-lookup"><span data-stu-id="a2945-218">Install DevKit board package</span></span>

<span data-ttu-id="a2945-219">U moet tooadd hello DevKit mededelingenbord met Hallo mededelingenbord Manager in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a2945-219">You will need tooadd hello DevKit board using hello Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="a2945-220">Gebruik `Cmd+Shift+P` tooinvoke palet en het type opdracht **Arduino** vervolgens zoeken en te selecteren **Arduino: mededelingenbord Manager**.</span><span class="sxs-lookup"><span data-stu-id="a2945-220">Use `Cmd+Shift+P` tooinvoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="a2945-221">Klik op **extra URL's** op Hallo rechtsonder.</span><span class="sxs-lookup"><span data-stu-id="a2945-221">Click **'Additional URLs'** at hello bottom right.</span></span>
   <span data-ttu-id="a2945-222">![installatie van extra URL](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="a2945-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="a2945-223">In Hallo `settings.json` bestand, een regel toegevoegd aan de onderkant Hallo van `USER SETTINGS` deelvenster en op te slaan.</span><span class="sxs-lookup"><span data-stu-id="a2945-223">In hello `settings.json` file, add a line at hello bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installatie-instellingen-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="a2945-225">Nu zoeken in Hallo mededelingenbord Manager 'az3166' en installeer de meest recente versie Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2945-225">Now in hello Board Manager search for 'az3166' and install hello latest version.</span></span>
   <span data-ttu-id="a2945-226">![installatie az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="a2945-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="a2945-227">U hebt nu alle benodigde Hallo-hulpprogramma's en pakketten die zijn geïnstalleerd voor Mac OS.</span><span class="sxs-lookup"><span data-stu-id="a2945-227">You now have all hello necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="a2945-228">Open projectmap</span><span class="sxs-lookup"><span data-stu-id="a2945-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="a2945-229">VS Code starten</span><span class="sxs-lookup"><span data-stu-id="a2945-229">Launch VS Code</span></span>

<span data-ttu-id="a2945-230">Zorg ervoor dat uw DevKit niet is verbonden.</span><span class="sxs-lookup"><span data-stu-id="a2945-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="a2945-231">VS Code eerst start en Hallo DevKit tooyour computer verbinden.</span><span class="sxs-lookup"><span data-stu-id="a2945-231">Launch VS Code first and connect hello DevKit tooyour computer.</span></span> <span data-ttu-id="a2945-232">VS-Code wordt automatisch vinden en pop-up van een introductiepagina:</span><span class="sxs-lookup"><span data-stu-id="a2945-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![Mini solution vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="a2945-234">Van tijd tot tijd, wanneer u Code tegenover start, wordt u gevraagd met fout die Arduino IDE of verwante mededelingenbord pakket niet vinden.</span><span class="sxs-lookup"><span data-stu-id="a2945-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="a2945-235">toosolve deze sluiten VS-Code Arduino IDE opnieuw starten en VS-Code moet Arduino IDE pad correct vinden.</span><span class="sxs-lookup"><span data-stu-id="a2945-235">toosolve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="a2945-236">Voorbeelden van Arduino-map openen</span><span class="sxs-lookup"><span data-stu-id="a2945-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="a2945-237">Switch te**'Arduino voorbeelden'** tabblad, te navigeren`Examples for MXCHIP AZ3166 > AzureIoT` en klik op `GetStarted`.</span><span class="sxs-lookup"><span data-stu-id="a2945-237">Switch too**'Arduino Examples'** tab, navigate too`Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![Mini solution-voorbeelden](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="a2945-239">Als u per ongeluk tooclose Hallo deelvenster tooreload ervan gebruik `Ctrl+Shift+P` (Mac OS: `Cmd+Shift+P`) tooinvoke palet en het type opdracht **Arduino** toofind en selecteer **Arduino: voorbeelden**.</span><span class="sxs-lookup"><span data-stu-id="a2945-239">If you happen tooclose hello pane, tooreload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** toofind and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="a2945-240">Azure-services inrichten</span><span class="sxs-lookup"><span data-stu-id="a2945-240">Provision Azure services</span></span>

<span data-ttu-id="a2945-241">Voer in Hallo oplossingsvenster uw taak via `Ctrl+P` (Mac OS: `Cmd+P`) door 'cloud inrichten van de taak' in te voeren:</span><span class="sxs-lookup"><span data-stu-id="a2945-241">In hello solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="a2945-242">VS Code terminal dat een interactieve opdrachtregel leidt u door de inrichting Hallo vereist in hello Azure-services:</span><span class="sxs-lookup"><span data-stu-id="a2945-242">In hello VS Code terminal, an interactive command line will guide you through provisioning hello required Azure services:</span></span>

![Mini-solution-cloud-inrichten](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="a2945-244">Maken en uploaden Arduino schema</span><span class="sxs-lookup"><span data-stu-id="a2945-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="a2945-245">Installeren van vereiste bibliotheek</span><span class="sxs-lookup"><span data-stu-id="a2945-245">Install required library</span></span>

1. <span data-ttu-id="a2945-246">Druk op `F1` of `Ctrl+Shift+P` (Mac OS: `Cmd+Shift+P`) tooinvoke palet en het type opdracht **Arduino** vervolgens zoeken en te selecteren **Arduino: Library Manager**.</span><span class="sxs-lookup"><span data-stu-id="a2945-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="a2945-247">Zoeken naar `ArduinoJson` bibliotheek en klik op **installeren**</span><span class="sxs-lookup"><span data-stu-id="a2945-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-hello-device-code"></a><span data-ttu-id="a2945-248">Maken en uploaden Hallo apparaatcode</span><span class="sxs-lookup"><span data-stu-id="a2945-248">Build and upload hello device code</span></span>

<span data-ttu-id="a2945-249">Gebruik `Ctrl+P` (Mac OS: `Cmd+P`) toorun 'taak apparaat-upload'.</span><span class="sxs-lookup"><span data-stu-id="a2945-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'task device-upload'.</span></span> <span data-ttu-id="a2945-250">Hallo terminal vraagt tooenter configuratiemodus.</span><span class="sxs-lookup"><span data-stu-id="a2945-250">hello terminal will prompt you tooenter configuration mode.</span></span> <span data-ttu-id="a2945-251">knop A toodo dus houd vervolgens push en release Hallo knop herstellen.</span><span class="sxs-lookup"><span data-stu-id="a2945-251">toodo so, hold down button A, then push and release hello reset button.</span></span> <span data-ttu-id="a2945-252">welkomstscherm weergegeven 'Configuration'.</span><span class="sxs-lookup"><span data-stu-id="a2945-252">hello screen will display 'Configuration'.</span></span> <span data-ttu-id="a2945-253">Dit is tooset Hallo-verbindingsreeks die wordt opgehaald uit de stap 'taak cloud-provision'.</span><span class="sxs-lookup"><span data-stu-id="a2945-253">This is tooset hello connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="a2945-254">Vervolgens wordt gestart wordt gecontroleerd en Hallo Arduino schema uploaden:</span><span class="sxs-lookup"><span data-stu-id="a2945-254">Then it will start verifying and uploading hello Arduino sketch:</span></span>

![Mini-solution-apparaat-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="a2945-256">Hallo DevKit wordt opnieuw opgestart en start Hallo code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a2945-256">hello DevKit will reboot and start running hello code.</span></span>

## <a name="test-hello-project"></a><span data-ttu-id="a2945-257">Hallo testproject</span><span class="sxs-lookup"><span data-stu-id="a2945-257">Test hello project</span></span>

<span data-ttu-id="a2945-258">Klik op Hallo power plug-pictogram op Hallo statusbalk tooopen Hallo seriële Monitor in VS-Code.</span><span class="sxs-lookup"><span data-stu-id="a2945-258">In VS Code, click hello power plug icon on hello status bar tooopen hello Serial Monitor.</span></span>

<span data-ttu-id="a2945-259">Hallo-voorbeeldtoepassing wordt correct uitgevoerd wanneer er Hallo resultaten te volgen:</span><span class="sxs-lookup"><span data-stu-id="a2945-259">hello sample application is running successfully when you see hello following results:</span></span>

* <span data-ttu-id="a2945-260">Hallo Hallo seriële Monitor geeft dezelfde informatie als Hallo inhoud in Hallo schermafbeelding hieronder.</span><span class="sxs-lookup"><span data-stu-id="a2945-260">hello Serial Monitor displays hello same information as hello content in hello screenshot below.</span></span>
* <span data-ttu-id="a2945-261">Hallo LED MXChip IoT DevKit knippert.</span><span class="sxs-lookup"><span data-stu-id="a2945-261">hello LED on MXChip IoT DevKit is blinking.</span></span>

![Uiteindelijke uitvoer in VS-Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="a2945-263">Problemen en feedback</span><span class="sxs-lookup"><span data-stu-id="a2945-263">Problems and feedback</span></span>

<span data-ttu-id="a2945-264">U vindt [Veelgestelde vragen over](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) als u problemen ondervindt of toous van Hallo kanalen onderstaande bereiken.</span><span class="sxs-lookup"><span data-stu-id="a2945-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out toous from hello channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2945-265">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2945-265">Next steps</span></span>

<span data-ttu-id="a2945-266">De verbinding van een MXChip IoT DevKit tooyour IoT-Hub gemaakt en verzonden hello vastgelegd sensor gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a2945-266">You have successfully connected an MXChip IoT DevKit tooyour IoT Hub, and sent hello captured sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="a2945-267">toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:</span><span class="sxs-lookup"><span data-stu-id="a2945-267">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="a2945-268">Berichten op cloudapparaten beheren met iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="a2945-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="a2945-269">IoT Hub berichten tooAzure gegevensopslag opslaan</span><span class="sxs-lookup"><span data-stu-id="a2945-269">Save IoT Hub messages tooAzure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="a2945-270">Gebruik Power BI toovisualize realtime-sensorgegevens uit Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a2945-270">Use Power BI toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="a2945-271">Gebruik Azure Web Apps toovisualize realtime-sensorgegevens uit Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a2945-271">Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="a2945-272">Weer voor de prognose met Hallo sensorgegevens uit uw IoT-hub in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a2945-272">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="a2945-273">Apparaatbeheer met iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="a2945-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="a2945-274">Externe bewaking en meldingen met Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a2945-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)