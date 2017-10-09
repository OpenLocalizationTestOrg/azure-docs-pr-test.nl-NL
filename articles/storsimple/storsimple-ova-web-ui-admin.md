---
title: aaaStorSimple virtuele matrix web UI beheer | Microsoft Docs
description: Hierin wordt beschreven hoe tooperform basic Apparaatbeheer via Hallo virtuele StorSimple-matrix webgebruikersinterface taken.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="70dfe-103">Uw virtuele StorSimple-matrix, Hallo Webgebruikersinterface tooadminister gebruiken</span><span class="sxs-lookup"><span data-stu-id="70dfe-103">Use hello Web UI tooadminister your StorSimple Virtual Array</span></span>
![Processtroom](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="70dfe-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="70dfe-105">Overview</span></span>
<span data-ttu-id="70dfe-106">Hallo-zelfstudies in dit artikel toohello Microsoft Azure StorSimple virtuele matrix (ook wel bekend als Hallo StorSimple on-premises virtuele apparaat) actieve maart 2016 algemene beschikbaarheid (GA) versie van toepassing.</span><span class="sxs-lookup"><span data-stu-id="70dfe-106">hello tutorials in this article apply toohello Microsoft Azure StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="70dfe-107">In dit artikel worden enkele Hallo complexe werkstromen en beheertaken uitvoeren die kunnen worden uitgevoerd op Hallo virtuele StorSimple-matrix beschreven.</span><span class="sxs-lookup"><span data-stu-id="70dfe-107">This article describes some of hello complex workflows and management tasks that can be performed on hello StorSimple Virtual Array.</span></span> <span data-ttu-id="70dfe-108">U kunt beheren Hallo virtuele StorSimple-matrix met Hallo StorSimple Manager-service UI (waarnaar wordt verwezen tooas Hallo portal UI) en Hallo lokale webgebruikersinterface voor Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="70dfe-108">You can manage hello StorSimple Virtual Array using hello StorSimple Manager service UI (referred tooas hello portal UI) and hello local web UI for hello device.</span></span> <span data-ttu-id="70dfe-109">In dit artikel is gericht op Hallo taken u kunt uitvoeren met behulp van Hallo webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="70dfe-109">This article focuses on hello tasks that you can perform using hello web UI.</span></span>

<span data-ttu-id="70dfe-110">In dit artikel bevat Hallo volgende zelfstudies:</span><span class="sxs-lookup"><span data-stu-id="70dfe-110">This article includes hello following tutorials:</span></span>

* <span data-ttu-id="70dfe-111">Hallo-service gegevens coderingssleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="70dfe-111">Get hello service data encryption key</span></span>
* <span data-ttu-id="70dfe-112">Web UI setup fouten oplossen</span><span class="sxs-lookup"><span data-stu-id="70dfe-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="70dfe-113">Genereren van een logboek-pakket</span><span class="sxs-lookup"><span data-stu-id="70dfe-113">Generate a log package</span></span>
* <span data-ttu-id="70dfe-114">Afsluiten of opnieuw opstarten van uw apparaat</span><span class="sxs-lookup"><span data-stu-id="70dfe-114">Shut down or restart your device</span></span>

## <a name="get-hello-service-data-encryption-key"></a><span data-ttu-id="70dfe-115">Hallo-service gegevens coderingssleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="70dfe-115">Get hello service data encryption key</span></span>
<span data-ttu-id="70dfe-116">Een service voor de gegevensversleutelingssleutel wordt gegenereerd wanneer u uw eerste apparaat bij Hallo StorSimple Manager-service registreren.</span><span class="sxs-lookup"><span data-stu-id="70dfe-116">A service data encryption key is generated when you register your first device with hello StorSimple Manager service.</span></span> <span data-ttu-id="70dfe-117">Deze sleutel is vereist met Hallo service registratie sleutel tooregister extra apparaten Hello StorSimple Manager-service.</span><span class="sxs-lookup"><span data-stu-id="70dfe-117">This key is then required with hello service registration key tooregister additional devices with hello StorSimple Manager service.</span></span>

<span data-ttu-id="70dfe-118">Als u de coderingssleutel voor uw service-gegevens hebt foutief worden geplaatst en tooretrieve moet, voeren Hallo volgende stappen in Hallo lokale webgebruikersinterface van Hallo apparaat geregistreerd bij uw service.</span><span class="sxs-lookup"><span data-stu-id="70dfe-118">If you have misplaced your service data encryption key and need tooretrieve it, perform hello following steps in hello local web UI of hello device registered with your service.</span></span>

#### <a name="tooget-hello-service-data-encryption-key"></a><span data-ttu-id="70dfe-119">gegevensversleutelingssleutel van tooget Hallo-service</span><span class="sxs-lookup"><span data-stu-id="70dfe-119">tooget hello service data encryption key</span></span>
1. <span data-ttu-id="70dfe-120">Verbinding maken met toohello lokale webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="70dfe-120">Connect toohello local web UI.</span></span> <span data-ttu-id="70dfe-121">Ga te**configuratie** > **Cloudinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="70dfe-121">Go too**Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="70dfe-122">Klik onder aan de pagina Hallo Hallo op **Get service gegevensversleutelingssleutel**.</span><span class="sxs-lookup"><span data-stu-id="70dfe-122">At hello bottom of hello page, click **Get service data encryption key**.</span></span> <span data-ttu-id="70dfe-123">Een sleutel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="70dfe-123">A key will appear.</span></span> <span data-ttu-id="70dfe-124">Kopieer en sla deze sleutel.</span><span class="sxs-lookup"><span data-stu-id="70dfe-124">Copy and save this key.</span></span>
   
    ![ophalen van de gegevensversleutelingssleutel van service 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="70dfe-126">Web UI setup fouten oplossen</span><span class="sxs-lookup"><span data-stu-id="70dfe-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="70dfe-127">In sommige gevallen wanneer u Hallo apparaat via Hallo lokale webgebruikersinterface, configureert kunt u tegenkomen fouten.</span><span class="sxs-lookup"><span data-stu-id="70dfe-127">In some instances when you configure hello device through hello local web UI, you might run into errors.</span></span> <span data-ttu-id="70dfe-128">toodiagnose en dergelijke fouten oplossen, kunt u Hallo diagnostische tests uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="70dfe-128">toodiagnose and troubleshoot such errors, you can run hello diagnostics tests.</span></span>

#### <a name="toorun-hello-diagnostic-tests"></a><span data-ttu-id="70dfe-129">toorun hello diagnostische tests</span><span class="sxs-lookup"><span data-stu-id="70dfe-129">toorun hello diagnostic tests</span></span>
1. <span data-ttu-id="70dfe-130">Ga te in Hallo lokale webgebruikersinterface,**probleemoplossing** > **diagnostische tests**.</span><span class="sxs-lookup"><span data-stu-id="70dfe-130">In hello local web UI, go too**Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![diagnose 1 uitvoeren](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="70dfe-132">Klik onder aan de pagina Hallo Hallo op **diagnostische Tests uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="70dfe-132">At hello bottom of hello page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="70dfe-133">Er wordt nu een mogelijke problemen met uw netwerk, apparaat, webproxy, tijd of instellingen voor cloud tests toodiagnose.</span><span class="sxs-lookup"><span data-stu-id="70dfe-133">This will initiate tests toodiagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="70dfe-134">U wordt gewaarschuwd dat apparaat Hallo tests wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="70dfe-134">You will be notified that hello device is running tests.</span></span>
3. <span data-ttu-id="70dfe-135">Nadat de tests Hallo hebt voltooid, worden Hallo resultaten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="70dfe-135">After hello tests have completed, hello results will be displayed.</span></span> <span data-ttu-id="70dfe-136">Hallo volgende voorbeeld ziet u de resultaten Hallo van diagnostische tests.</span><span class="sxs-lookup"><span data-stu-id="70dfe-136">hello following example shows hello results of diagnostic tests.</span></span> <span data-ttu-id="70dfe-137">Houd er rekening mee dat Hallo web proxy-instellingen zijn niet geconfigureerd op dit apparaat en Hallo proxy WebTest is daarom niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="70dfe-137">Note that hello web proxy settings were not configured on this device, and therefore, hello web proxy test was not run.</span></span> <span data-ttu-id="70dfe-138">Alle andere tests voor de netwerkinstellingen, DNS-server, Hallo- en tijdinstellingen is gelukt.</span><span class="sxs-lookup"><span data-stu-id="70dfe-138">All hello other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![de diagnostische gegevens van 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="70dfe-140">Genereren van een logboek-pakket</span><span class="sxs-lookup"><span data-stu-id="70dfe-140">Generate a log package</span></span>
<span data-ttu-id="70dfe-141">Een pakket logboek bestaat uit alle Hallo relevante logboeken die Microsoft Support helpen kunnen bij het oplossen van problemen met apparaten.</span><span class="sxs-lookup"><span data-stu-id="70dfe-141">A log package is comprised of all hello relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="70dfe-142">In deze release, kan een pakket logboek via Hallo lokale webgebruikersinterface worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="70dfe-142">In this release, a log package can be generated via hello local web UI.</span></span>

#### <a name="toogenerate-hello-log-package"></a><span data-ttu-id="70dfe-143">toogenerate hello logboek-pakket</span><span class="sxs-lookup"><span data-stu-id="70dfe-143">toogenerate hello log package</span></span>
1. <span data-ttu-id="70dfe-144">Ga te in Hallo lokale webgebruikersinterface,**probleemoplossing** > **systeemlogboeken**.</span><span class="sxs-lookup"><span data-stu-id="70dfe-144">In hello local web UI, go too**Troubleshooting** > **System logs**.</span></span>
   
    ![logboek pakket, 1 genereren](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="70dfe-146">Klik onder aan de pagina Hallo Hallo op **maken logboek pakket**.</span><span class="sxs-lookup"><span data-stu-id="70dfe-146">At hello bottom of hello page, click **Create log package**.</span></span> <span data-ttu-id="70dfe-147">Een pakket van Hallo systeemlogboeken wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70dfe-147">A package of hello system logs will be created.</span></span> <span data-ttu-id="70dfe-148">Dit duurt enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="70dfe-148">This will take a couple of minutes.</span></span>
   
    ![logboek pakket 2 genereren](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="70dfe-150">U ontvangt een melding nadat Hallo-pakket is gemaakt en Hallo pagina wordt bijgewerkt tooindicate Hallo tijd en datum waarop het Hallo-pakket is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70dfe-150">You will be notified after hello package is successfully created, and hello page will be updated tooindicate hello time and date when hello package was created.</span></span>
   
    ![logboek pakket, 3 genereren](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="70dfe-152">Klik op **logboek downloadpakket**.</span><span class="sxs-lookup"><span data-stu-id="70dfe-152">Click **Download log package**.</span></span> <span data-ttu-id="70dfe-153">Een ZIP-pakket worden gedownload op uw systeem.</span><span class="sxs-lookup"><span data-stu-id="70dfe-153">A zipped package will be downloaded on your system.</span></span>
   
    ![logboek pakket 4 genereren](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="70dfe-155">U kunt pak Hallo logboek gedownloade pakket en Hallo Systeemlogboekbestanden weergeven.</span><span class="sxs-lookup"><span data-stu-id="70dfe-155">You can unzip hello downloaded log package and view hello system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="70dfe-156">Afsluiten en opnieuw opstarten van uw apparaat</span><span class="sxs-lookup"><span data-stu-id="70dfe-156">Shut down and restart your device</span></span>
<span data-ttu-id="70dfe-157">U kunt afsluiten of opnieuw opstarten van uw virtuele apparaat via Hallo lokale web UI.</span><span class="sxs-lookup"><span data-stu-id="70dfe-157">You can shut down or restart your virtual device using hello local web UI.</span></span> <span data-ttu-id="70dfe-158">We raden aan dat voordat u opnieuw opstarten, Hallo volumes of shares offline op Hallo host nemen en vervolgens Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="70dfe-158">We recommend that before you restart, take hello volumes or shares offline on hello host and then hello device.</span></span> <span data-ttu-id="70dfe-159">Hierdoor minimaliseert u iedere mogelijkheid van beschadigde gegevens.</span><span class="sxs-lookup"><span data-stu-id="70dfe-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="tooshut-down-your-virtual-device"></a><span data-ttu-id="70dfe-160">tooshut omlaag uw virtuele apparaat</span><span class="sxs-lookup"><span data-stu-id="70dfe-160">tooshut down your virtual device</span></span>
1. <span data-ttu-id="70dfe-161">Ga te in Hallo lokale webgebruikersinterface,**onderhoud** > **energie-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="70dfe-161">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="70dfe-162">Klik onder aan de pagina Hallo Hallo op **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="70dfe-162">At hello bottom of hello page, click **Shutdown**.</span></span>
   
    ![Afsluitgebeurtenis apparaat 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="70dfe-164">Er wordt een waarschuwing weergegeven waarin staat dat afsluiten van Hallo-apparaat een i/o die zijn uitgevoerd, wat resulteert in een uitvaltijd wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="70dfe-164">A warning will appear stating that a shutdown of hello device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="70dfe-165">Klik op het vinkje Hallo</span><span class="sxs-lookup"><span data-stu-id="70dfe-165">Click hello check icon</span></span> ![vinkje](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="70dfe-167">.</span><span class="sxs-lookup"><span data-stu-id="70dfe-167">.</span></span>
   
    ![Waarschuwing voor apparaat afsluiten](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="70dfe-169">U wordt gewaarschuwd dat het Hallo afsluiten is gestart.</span><span class="sxs-lookup"><span data-stu-id="70dfe-169">You will be notified that hello shutdown has been initiated.</span></span>
   
    ![apparaat afsluiten is gestart](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="70dfe-171">Hallo-apparaat wordt nu afgesloten.</span><span class="sxs-lookup"><span data-stu-id="70dfe-171">hello device will now shut down.</span></span> <span data-ttu-id="70dfe-172">Als u toostart op uw apparaat wilt, moet u toodo die via Hallo Hyper-V-beheer.</span><span class="sxs-lookup"><span data-stu-id="70dfe-172">If you want toostart your device, you will need toodo that through hello Hyper-V Manager.</span></span>

#### <a name="toorestart-your-virtual-device"></a><span data-ttu-id="70dfe-173">toorestart uw virtuele apparaat</span><span class="sxs-lookup"><span data-stu-id="70dfe-173">toorestart your virtual device</span></span>
1. <span data-ttu-id="70dfe-174">Ga te in Hallo lokale webgebruikersinterface,**onderhoud** > **energie-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="70dfe-174">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="70dfe-175">Klik onder aan de pagina Hallo Hallo op **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="70dfe-175">At hello bottom of hello page, click **Restart**.</span></span>
   
    ![herstart van het apparaat](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="70dfe-177">Er wordt een waarschuwing weergegeven waarin staat dat opnieuw te starten Hallo-apparaat een IOs die zijn uitgevoerd, wat resulteert in een uitvaltijd wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="70dfe-177">A warning will appear stating that restarting hello device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="70dfe-178">Klik op het vinkje Hallo</span><span class="sxs-lookup"><span data-stu-id="70dfe-178">Click hello check icon</span></span> ![vinkje](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="70dfe-180">.</span><span class="sxs-lookup"><span data-stu-id="70dfe-180">.</span></span>
   
    ![opnieuw opstarten van waarschuwing](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="70dfe-182">U wordt gewaarschuwd dat Hallo opnieuw is gestart.</span><span class="sxs-lookup"><span data-stu-id="70dfe-182">You will be notified that hello restart has been initiated.</span></span>
   
    ![opnieuw opstarten geïnitieerd](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="70dfe-184">Tijdens het Hallo opnieuw moet worden uitgevoerd, verliest u Hallo verbinding toohello gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="70dfe-184">While hello restart is in progress, you will lose hello connection toohello UI.</span></span> <span data-ttu-id="70dfe-185">U kunt Hallo opnieuw opstarten controleren door het Hallo-gebruikersinterface periodiek vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="70dfe-185">You can monitor hello restart by refreshing hello UI periodically.</span></span> <span data-ttu-id="70dfe-186">U kunt ook Hallo Apparaatstatus opnieuw opstarten via Hallo Hyper-V Manager bewaken.</span><span class="sxs-lookup"><span data-stu-id="70dfe-186">Alternatively, you can monitor hello device restart status through hello Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70dfe-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70dfe-187">Next steps</span></span>
<span data-ttu-id="70dfe-188">Meer informatie over hoe te[gebruik Hallo StorSimple Manager service toomanage uw apparaat](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="70dfe-188">Learn how too[use hello StorSimple Manager service toomanage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

