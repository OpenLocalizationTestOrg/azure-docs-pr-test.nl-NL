---
title: aaaConnect een apparaat met C op mbed | Microsoft Docs
description: Hierin wordt beschreven hoe tooconnect een apparaat toohello Azure IoT Suite vooraf geconfigureerde oplossing voor externe controle met behulp van een toepassing die is geschreven in C uitvoering op een apparaat mbed.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="4a844-103">Verbinding maken met uw apparaat toohello vooraf geconfigureerde oplossing (mbed) voor externe controle</span><span class="sxs-lookup"><span data-stu-id="4a844-103">Connect your device toohello remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="4a844-104">Overzicht van scenario's</span><span class="sxs-lookup"><span data-stu-id="4a844-104">Scenario overview</span></span>
<span data-ttu-id="4a844-105">In dit scenario die u maakt een apparaat dat verzendt telemetrie toohello externe controle te volgen Hallo [vooraf geconfigureerde oplossing][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="4a844-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="4a844-106">Externe temperatuur</span><span class="sxs-lookup"><span data-stu-id="4a844-106">External temperature</span></span>
* <span data-ttu-id="4a844-107">Interne temperatuur</span><span class="sxs-lookup"><span data-stu-id="4a844-107">Internal temperature</span></span>
* <span data-ttu-id="4a844-108">Vochtigheid</span><span class="sxs-lookup"><span data-stu-id="4a844-108">Humidity</span></span>

<span data-ttu-id="4a844-109">Eenvoud, Hallo-code op Hallo apparaat genereert voorbeeldwaarden, maar we raden u tooextend Hallo voorbeeld door de echte sensoren tooyour apparaat verbinding te maken en verzenden van telemetrie echte.</span><span class="sxs-lookup"><span data-stu-id="4a844-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="4a844-110">Hallo-apparaat is ook kunnen toorespond toomethods aangeroepen vanuit het dashboard van de oplossing Hallo en eigenschapswaarden ingesteld in het dashboard van de oplossing Hallo gewenst.</span><span class="sxs-lookup"><span data-stu-id="4a844-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="4a844-111">toocomplete in deze zelfstudie, moet u een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="4a844-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="4a844-112">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="4a844-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4a844-113">Zie [Gratis proefversie van Azure][lnk-free-trial] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4a844-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="4a844-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="4a844-114">Before you start</span></span>
<span data-ttu-id="4a844-115">Voordat u code voor het apparaat gaat schrijven, moet u de vooraf geconfigureerde oplossing voor externe controle inrichten en een nieuw aangepast apparaat in die oplossing inrichten.</span><span class="sxs-lookup"><span data-stu-id="4a844-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="4a844-116">De vooraf geconfigureerde oplossing voor externe controle inrichten</span><span class="sxs-lookup"><span data-stu-id="4a844-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="4a844-117">Hallo-apparaat in deze zelfstudie hebt u verzendt gegevens tooan exemplaar van Hallo [externe controle] [ lnk-remote-monitoring] vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="4a844-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="4a844-118">Als u al vooraf geconfigureerde oplossing in uw Azure-account voor externe controle Hallo nog niet hebt ingericht, gebruikt u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4a844-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="4a844-119">Op Hallo <https://www.azureiotsuite.com/> pagina, klikt u op  **+**  toocreate een oplossing.</span><span class="sxs-lookup"><span data-stu-id="4a844-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="4a844-120">Klik op **Selecteer** op Hallo **externe controle** toocreate van uw oplossing het deelvenster.</span><span class="sxs-lookup"><span data-stu-id="4a844-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="4a844-121">Op Hallo **maken oplossing voor externe controle** pagina, voert u een **oplossingsnaam** van uw keuze, selecteer Hallo **regio** u wilt toodeploy naar en selecteer hello Azure abonnement toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="4a844-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="4a844-122">Klik vervolgens op **Oplossing maken**.</span><span class="sxs-lookup"><span data-stu-id="4a844-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="4a844-123">Wacht totdat het Hallo inrichtingsproces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4a844-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="4a844-124">Hallo vooraf geconfigureerde oplossingen gebruiken factureerbare Azure-services.</span><span class="sxs-lookup"><span data-stu-id="4a844-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="4a844-125">Zorg ervoor dat tooremove Hallo vooraf geconfigureerde oplossing van uw abonnement wanneer u klaar bent met het tooavoid eventuele onnodige kosten.</span><span class="sxs-lookup"><span data-stu-id="4a844-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="4a844-126">U kunt een vooraf geconfigureerde oplossing volledig verwijderen uit uw abonnement via Hallo <https://www.azureiotsuite.com/> pagina.</span><span class="sxs-lookup"><span data-stu-id="4a844-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="4a844-127">Wanneer Hallo proces voor het Hallo-oplossing voor externe controle inrichten is voltooid, klikt u op **starten** tooopen Hallo dashboard van de oplossing in uw browser.</span><span class="sxs-lookup"><span data-stu-id="4a844-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Dashboard van de oplossing][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="4a844-129">Uw apparaat bij Hallo oplossing voor externe controle inrichten</span><span class="sxs-lookup"><span data-stu-id="4a844-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="4a844-130">Als u al een apparaat in uw oplossing hebt ingericht, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="4a844-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="4a844-131">Bij het maken van de client-toepassing hello moet u tooknow Hallo apparaat referenties.</span><span class="sxs-lookup"><span data-stu-id="4a844-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="4a844-132">Voor een apparaat tooconnect toohello vooraf geconfigureerde oplossing, deze moet zelfidentificatie tooIoT Hub met geldige referenties.</span><span class="sxs-lookup"><span data-stu-id="4a844-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="4a844-133">U kunt Hallo apparaat referenties ophalen uit Hallo oplossing dashboard.</span><span class="sxs-lookup"><span data-stu-id="4a844-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="4a844-134">Hallo apparaat referenties in uw clienttoepassing verderop in deze zelfstudie te nemen.</span><span class="sxs-lookup"><span data-stu-id="4a844-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="4a844-135">de oplossing voor externe controle van een apparaat-tooyour tooadd, volledige hello te volgen stappen in Hallo oplossing dashboard:</span><span class="sxs-lookup"><span data-stu-id="4a844-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="4a844-136">In Hallo linkerbenedenhoek van Hallo dashboard, klikt u op **een apparaat toevoegt**.</span><span class="sxs-lookup"><span data-stu-id="4a844-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Een apparaat toevoegen][1]
2. <span data-ttu-id="4a844-138">In Hallo **aangepast apparaat** -scherm, klikt u op **nieuwe toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4a844-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Een aangepast apparaat toevoegen][2]
3. <span data-ttu-id="4a844-140">Kies **Laat mij mijn eigen apparaat-id definiëren**.</span><span class="sxs-lookup"><span data-stu-id="4a844-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="4a844-141">Voer een apparaat-ID zoals **mydevice**, klikt u op **cheque-ID** tooverify die naam niet al in gebruik en klik vervolgens op **maken** tooprovision Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="4a844-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Apparaat-id toevoegen][3]
4. <span data-ttu-id="4a844-143">Een opmerking Hallo-apparaat referenties (apparaat-ID, hostnaam van de IoT-Hub en apparaatsleutel) maken.</span><span class="sxs-lookup"><span data-stu-id="4a844-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="4a844-144">De clienttoepassing moet deze waarden tooconnect toohello oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="4a844-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="4a844-145">Klik vervolgens op **Gereed**.</span><span class="sxs-lookup"><span data-stu-id="4a844-145">Then click **Done**.</span></span>
   
    ![Apparaatreferenties weergeven][4]
5. <span data-ttu-id="4a844-147">Selecteer uw apparaat in de lijst met apparaten in het dashboard van de oplossing Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a844-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="4a844-148">Klik op Hallo **Apparaatdetails** -scherm, klikt u op **apparaat inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="4a844-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="4a844-149">Hallo-status van uw apparaat is nu **met**.</span><span class="sxs-lookup"><span data-stu-id="4a844-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="4a844-150">Hallo-oplossing voor externe controle kan nu telemetrie van uw apparaat wordt ontvangen en methoden niet aanroepen voor het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4a844-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a><span data-ttu-id="4a844-151">Bouwen en uitvoeren van Voorbeeldoplossing Hallo C</span><span class="sxs-lookup"><span data-stu-id="4a844-151">Build and run hello C sample solution</span></span>

<span data-ttu-id="4a844-152">Hallo volgende instructies beschrijven Hallo stappen voor het verbinden van een [mbed ingeschakeld Freescale FRDM-K64F] [ lnk-mbed-home] apparaat toohello oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="4a844-152">hello following instructions describe hello steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device toohello remote monitoring solution.</span></span>

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a><span data-ttu-id="4a844-153">Verbinding maken met de Hallo mbed apparaat tooyour netwerk- en computer</span><span class="sxs-lookup"><span data-stu-id="4a844-153">Connect hello mbed device tooyour network and desktop machine</span></span>

1. <span data-ttu-id="4a844-154">Hallo mbed apparaat tooyour netwerk met behulp van een Ethernet-kabel verbinden.</span><span class="sxs-lookup"><span data-stu-id="4a844-154">Connect hello mbed device tooyour network using an Ethernet cable.</span></span> <span data-ttu-id="4a844-155">Deze stap is nodig omdat de voorbeeldtoepassing Hallo hiervoor is internettoegang vereist.</span><span class="sxs-lookup"><span data-stu-id="4a844-155">This step is necessary because hello sample application requires internet access.</span></span>

1. <span data-ttu-id="4a844-156">Zie [aan de slag met mbed] [ lnk-mbed-getstarted] tooconnect uw mbed apparaat tooyour bureaublad PC.</span><span class="sxs-lookup"><span data-stu-id="4a844-156">See [Getting Started with mbed][lnk-mbed-getstarted] tooconnect your mbed device tooyour desktop PC.</span></span>

1. <span data-ttu-id="4a844-157">Als uw PC kan Windows wordt uitgevoerd, Zie [configuratie PC] [ lnk-mbed-pcconnect] tooconfigure seriële poort toegang tooyour mbed apparaat.</span><span class="sxs-lookup"><span data-stu-id="4a844-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] tooconfigure serial port access tooyour mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a><span data-ttu-id="4a844-158">Maken van een project mbed en voorbeeldcode Hallo importeren</span><span class="sxs-lookup"><span data-stu-id="4a844-158">Create an mbed project and import hello sample code</span></span>

<span data-ttu-id="4a844-159">Volg deze stappen tooadd sommige voorbeeldproject code tooan mbed.</span><span class="sxs-lookup"><span data-stu-id="4a844-159">Follow these steps tooadd some sample code tooan mbed project.</span></span> <span data-ttu-id="4a844-160">U Hallo externe controle starter project importeren en wijzig vervolgens Hallo project toouse hello MQTT protocol in plaats van Hallo AMQP-protocol.</span><span class="sxs-lookup"><span data-stu-id="4a844-160">You import hello remote monitoring starter project and then change hello project toouse hello MQTT protocol instead of hello AMQP protocol.</span></span> <span data-ttu-id="4a844-161">Op dit moment moet u toouse hello MQTT protocol toouse Hallo beheerfuncties voor apparaten van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4a844-161">Currently, you need toouse hello MQTT protocol toouse hello device management features of IoT Hub.</span></span>

1. <span data-ttu-id="4a844-162">Ga in uw webbrowser toohello mbed.org [developer site](https://developer.mbed.org/).</span><span class="sxs-lookup"><span data-stu-id="4a844-162">In your web browser, go toohello mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="4a844-163">Als u dit nog niet hebt aangemeld, ziet u een optie toocreate een account (het is gratis).</span><span class="sxs-lookup"><span data-stu-id="4a844-163">If you haven't signed up, you see an option toocreate an account (it's free).</span></span> <span data-ttu-id="4a844-164">Anders kunt u aanmelden met referenties van uw account.</span><span class="sxs-lookup"><span data-stu-id="4a844-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="4a844-165">Klik vervolgens op **Compiler** in Hallo rechterbovenhoek van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="4a844-165">Then click **Compiler** in hello upper right-hand corner of hello page.</span></span> <span data-ttu-id="4a844-166">Deze actie biedt u toohello *werkruimte* interface.</span><span class="sxs-lookup"><span data-stu-id="4a844-166">This action brings you toohello *Workspace* interface.</span></span>

1. <span data-ttu-id="4a844-167">Zorg ervoor dat Hallo hardwareplatform dat u gebruikt in Hallo rechterbovenhoek van Hallo-venster wordt weergegeven of klik op Hallo-pictogram in Hallo rechterhoek tooselect uw hardwareplatform.</span><span class="sxs-lookup"><span data-stu-id="4a844-167">Make sure hello hardware platform you're using appears in hello upper right-hand corner of hello window, or click hello icon in hello right-hand corner tooselect your hardware platform.</span></span>

1. <span data-ttu-id="4a844-168">Klik op **importeren** in het hoofdmenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a844-168">Click **Import** on hello main menu.</span></span> <span data-ttu-id="4a844-169">Klik vervolgens op **Klik hier tooimport van URL**.</span><span class="sxs-lookup"><span data-stu-id="4a844-169">Then click **Click here tooimport from URL**.</span></span>
   
    ![Start importeren toombed werkruimte][6]

1. <span data-ttu-id="4a844-171">Voer in het pop-upvenster hello, Hallo-koppeling voor Hallo voorbeeld code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ en klik vervolgens op **importeren**.</span><span class="sxs-lookup"><span data-stu-id="4a844-171">In hello pop-up window, enter hello link for hello sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Voorbeeld code toombed werkruimte importeren][7]

1. <span data-ttu-id="4a844-173">U kunt zien in Hallo mbed compiler venster dat dit project importeren ook verschillende bibliotheken invoer.</span><span class="sxs-lookup"><span data-stu-id="4a844-173">You can see in hello mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="4a844-174">Sommige worden geleverd en beheerd door hello Azure IoT-team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), terwijl andere derden beschikbare bibliotheken in Hallo mbed bibliotheken catalogus.</span><span class="sxs-lookup"><span data-stu-id="4a844-174">Some are provided and maintained by hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in hello mbed libraries catalog.</span></span>
   
    ![Weergave mbed project][8]

1. <span data-ttu-id="4a844-176">In Hallo **programma werkruimte**, klik met de rechtermuisknop Hallo **iothub\_amqp\_transport** bibliotheek, klikt u op **verwijderen**, en klik vervolgens op **OK** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="4a844-176">In hello **Program Workspace**, right-click hello **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="4a844-177">In Hallo **programma werkruimte**, klik met de rechtermuisknop Hallo **azure\_amqp\_c** bibliotheek, klikt u op **verwijderen**, en klik vervolgens op **OK**  tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="4a844-177">In hello **Program Workspace**, right-click hello **azure\_amqp\_c** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="4a844-178">Met de rechtermuisknop op Hallo **remote_monitoring** -project in Hallo **programma werkruimte**, selecteer **bibliotheek importeren**, selecteer daarna **van URL**.</span><span class="sxs-lookup"><span data-stu-id="4a844-178">Right-click hello **remote_monitoring** project in hello **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Starten van de werkruimte bibliotheek import-toombed][6]

1. <span data-ttu-id="4a844-180">Voer in het pop-upvenster hello, Hallo-koppeling voor Hallo MQTT transport bibliotheek https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport / klikt u vervolgens op **importeren**.</span><span class="sxs-lookup"><span data-stu-id="4a844-180">In hello pop-up window, enter hello link for hello MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![De werkruimte toombed bibliotheek importeren][12]

1. <span data-ttu-id="4a844-182">Herhaal Hallo vorige stap tooadd hello MQTT-bibliotheek van https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="4a844-182">Repeat hello previous step tooadd hello MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="4a844-183">Uw werkruimte is nu ziet eruit als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="4a844-183">Your workspace now looks like hello following:</span></span>

    ![Mbed-werkruimte weergeven][13]

1. <span data-ttu-id="4a844-185">Open Hallo externe\_monitoring\remote_monitoring.c bestands- en vervang Hallo bestaande `#include` instructies met Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="4a844-185">Open hello remote\_monitoring\remote_monitoring.c file and replace hello existing `#include` statements with hello following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. <span data-ttu-id="4a844-186">Verwijderen van alle Hallo resterende code in externe Hallo\_monitoring\remote\_monitoring.c-bestand.</span><span class="sxs-lookup"><span data-stu-id="4a844-186">Delete all hello remaining code in hello remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="4a844-187">Bouwen en uitvoeren van Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="4a844-187">Build and run hello sample</span></span>

<span data-ttu-id="4a844-188">Toevoegen van code tooinvoke Hallo **externe\_bewaking\_uitvoeren** werken en vervolgens toepassing bouwen en uitvoeren Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="4a844-188">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="4a844-189">Toevoegen een **belangrijkste** functie met de volgende code achter Hallo Hallo externe\_monitoring.c bestand tooinvoke hello **externe\_bewaking\_uitvoeren** functie:</span><span class="sxs-lookup"><span data-stu-id="4a844-189">Add a **main** function with following code at hello end of hello remote\_monitoring.c file tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="4a844-190">Klik op **compileren** toobuild Hallo programma.</span><span class="sxs-lookup"><span data-stu-id="4a844-190">Click **Compile** toobuild hello program.</span></span> <span data-ttu-id="4a844-191">U kunt veilig negeren van waarschuwingen, maar als Hallo build fouten genereert corrigeren voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="4a844-191">You can safely ignore any warnings, but if hello build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="4a844-192">Als Hallo build geslaagd is, wordt Hallo mbed compiler website genereert u een .bin-bestand met de naam van uw project Hallo en downloadt u de lokale computer tooyour.</span><span class="sxs-lookup"><span data-stu-id="4a844-192">If hello build is successful, hello mbed compiler website generates a .bin file with hello name of your project and downloads it tooyour local machine.</span></span> <span data-ttu-id="4a844-193">Hallo .bin-bestand toohello apparaat kopiëren.</span><span class="sxs-lookup"><span data-stu-id="4a844-193">Copy hello .bin file toohello device.</span></span> <span data-ttu-id="4a844-194">Hallo .bin-bestand toohello apparaat opslaan Hallo apparaat toorestart veroorzaakt en opgenomen in het .bin-bestand Hallo Hallo-programma uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4a844-194">Saving hello .bin file toohello device causes hello device toorestart and run hello program contained in hello .bin file.</span></span> <span data-ttu-id="4a844-195">U kunt handmatig opnieuw opstarten Hallo programma op elk gewenst moment Hallo opnieuw instellen door knop te drukken op Hallo mbed apparaat.</span><span class="sxs-lookup"><span data-stu-id="4a844-195">You can manually restart hello program at any time by pressing hello reset button on hello mbed device.</span></span>

1. <span data-ttu-id="4a844-196">Verbinding maken met behulp van een SSH-client-toepassing, zoals PuTTY toohello-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4a844-196">Connect toohello device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="4a844-197">U kunt de seriële poort Hallo die uw apparaat wordt gebruikt door het controleren van Windows-Apparaatbeheer bepalen.</span><span class="sxs-lookup"><span data-stu-id="4a844-197">You can determine hello serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="4a844-198">Klik in de PuTTY, op Hallo **seriële** verbindingstype.</span><span class="sxs-lookup"><span data-stu-id="4a844-198">In PuTTY, click hello **Serial** connection type.</span></span> <span data-ttu-id="4a844-199">Hallo-apparaat is doorgaans verbinding maakt met 9600 baud, dus voer 9600 in Hallo **snelheid** vak.</span><span class="sxs-lookup"><span data-stu-id="4a844-199">hello device typically connects at 9600 baud, so enter 9600 in hello **Speed** box.</span></span> <span data-ttu-id="4a844-200">Klik vervolgens op **Open**.</span><span class="sxs-lookup"><span data-stu-id="4a844-200">Then click **Open**.</span></span>

1. <span data-ttu-id="4a844-201">Hallo-programma wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4a844-201">hello program starts executing.</span></span> <span data-ttu-id="4a844-202">Mogelijk hebt u tooreset Hallo Mededelingenbord (druk op CTRL + Break of druk op Hallo mededelingenbord herstelknop) als Hallo programma niet automatisch wordt gestart wanneer u verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="4a844-202">You may have tooreset hello board (press CTRL+Break or press hello board's reset button) if hello program does not start automatically when you connect.</span></span>
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
