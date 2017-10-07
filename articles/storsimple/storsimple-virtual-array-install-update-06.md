---
title: aaaInstall Update 0,6 op de virtuele StorSimple-matrix | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Hallo virtuele StorSimple-matrix web UI tooapply updates met behulp van Azure portal en hotfix methode Hallo
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 2ccd1b5fc1957c35ebec35aa947d331b3ff05464
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a><span data-ttu-id="6fae9-103">Update 0,6 installeren op uw virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="6fae9-103">Install Update 0.6 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="6fae9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6fae9-104">Overview</span></span>

<span data-ttu-id="6fae9-105">In dit artikel beschrijft Hallo stappen vereist tooinstall Update 0,6 op uw virtuele StorSimple-matrix via Hallo lokale webgebruikersinterface en via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6fae9-105">This article describes hello steps required tooinstall Update 0.6 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="6fae9-106">U toepassen het software-updates of hotfixes tookeep Hallo uw StorSimple virtuele matrix up-to-date.</span><span class="sxs-lookup"><span data-stu-id="6fae9-106">You apply hello software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="6fae9-107">Voordat u een update hebt toegepast, wordt aangeraden dat u rekening houden met Hallo volumes of shares op Hallo eerst hosten en vervolgens Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="6fae9-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="6fae9-108">Dit verkleint dat beschadigde gegevens.</span><span class="sxs-lookup"><span data-stu-id="6fae9-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="6fae9-109">Nadat het Hallo-volumes of shares die offline is, u moet ook rekening houden met een handmatige back-up van het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6fae9-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="6fae9-110">Update 0,6 te overeenkomt met**10.0.10293.0** softwareversie van de op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="6fae9-110">Update 0.6 corresponds too**10.0.10293.0** software version on your device.</span></span> <span data-ttu-id="6fae9-111">Voor informatie over wat is er nieuw in deze update gaat te[Release-opmerkingen voor Update 0,6](storsimple-virtual-array-update-06-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="6fae9-111">For information on what is new in this update, go too[Release notes for Update 0.6](storsimple-virtual-array-update-06-release-notes.md).</span></span>
>
> - <span data-ttu-id="6fae9-112">Als u Update 0.2 uitvoert of hoger, we raden installeren u Hallo updates via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6fae9-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="6fae9-113">Als u Update 0.1 of GA softwareversies uitvoert, moet u Hallo hotfix methode via Hallo lokale web UI tooinstall Update 0,6 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6fae9-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.6.</span></span>
>
> - <span data-ttu-id="6fae9-114">Houd er rekening mee dat voor het installeren van een update of hotfix uw apparaat opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="6fae9-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="6fae9-115">Aangezien Hallo virtuele StorSimple-matrix is een apparaat met één knooppunt, een i/o uitgevoerd wordt onderbroken en uw apparaat uitval optreedt.</span><span class="sxs-lookup"><span data-stu-id="6fae9-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="6fae9-116">Gebruik hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6fae9-116">Use hello Azure portal</span></span>

<span data-ttu-id="6fae9-117">Als Update 0,2 en hoger, raden wij aan dat u updates via hello Azure-portal installeert.</span><span class="sxs-lookup"><span data-stu-id="6fae9-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="6fae9-118">Hallo portal procedure vereist Hallo gebruiker tooscan, downloaden en installeer vervolgens Hallo-updates.</span><span class="sxs-lookup"><span data-stu-id="6fae9-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="6fae9-119">Deze procedure duurt ongeveer 7 minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6fae9-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="6fae9-120">Uitvoeren van de volgende Hallo stappen tooinstall Hallo update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="6fae9-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="6fae9-121">Na het Hallo is installatie voltooid, gaat u tooyour StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="6fae9-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="6fae9-122">Selecteer **apparaten** en selecteer en klikt u op Hallo-apparaat die u zojuist hebt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="6fae9-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="6fae9-123">Ga te**instellingen > beheren > apparaatupdates**.</span><span class="sxs-lookup"><span data-stu-id="6fae9-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="6fae9-124">de softwareversie weergegeven Hallo moet **10.0.10293.0**.</span><span class="sxs-lookup"><span data-stu-id="6fae9-124">hello displayed software version should be **10.0.10293.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="6fae9-125">Gebruik Hallo lokale webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="6fae9-125">Use hello local web UI</span></span>

<span data-ttu-id="6fae9-126">Er zijn twee stappen wanneer u Hallo lokale-webgebruikersinterface:</span><span class="sxs-lookup"><span data-stu-id="6fae9-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="6fae9-127">Hallo update of hotfix Hallo downloaden</span><span class="sxs-lookup"><span data-stu-id="6fae9-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="6fae9-128">Hallo update of hotfix Hallo installeren</span><span class="sxs-lookup"><span data-stu-id="6fae9-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="6fae9-129">Hallo update of hotfix Hallo downloaden</span><span class="sxs-lookup"><span data-stu-id="6fae9-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="6fae9-130">Volgende stappen toodownload Hallo software-update vanaf Microsoft Update-catalogus Hallo Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6fae9-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="6fae9-131">toodownload hello update of Hallo hotfix</span><span class="sxs-lookup"><span data-stu-id="6fae9-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="6fae9-132">Start Internet Explorer en navigeer te[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6fae9-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="6fae9-133">Als u van Microsoft Update-catalogus Hallo voor Hallo eerst op deze computer gebruikmaakt, klikt u op **installeren** wanneer na vragen aan gebruiker tooinstall Hallo-invoegtoepassing voor Microsoft Update-catalogus.</span><span class="sxs-lookup"><span data-stu-id="6fae9-133">If you are using hello Microsoft Update Catalog for hello first time on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="6fae9-134">In het zoekvak Hallo Hallo Microsoft Update-catalogus, invoeren Hallo-Knowledge Base (KB) van de hotfix Hallo gewenste toodownload.</span><span class="sxs-lookup"><span data-stu-id="6fae9-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="6fae9-135">Voer **4023268** voor Update 0,6 en klik vervolgens op **Search**.</span><span class="sxs-lookup"><span data-stu-id="6fae9-135">Enter **4023268** for Update 0.6, and then click **Search**.</span></span>
   
    <span data-ttu-id="6fae9-136">Hallo hotfix wordt weergegeven, bijvoorbeeld **StorSimple virtuele matrix Update 0,6**.</span><span class="sxs-lookup"><span data-stu-id="6fae9-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.6**.</span></span>
   
    ![Catalogus doorzoeken](./media/storsimple-virtual-array-install-update-06/download1.png)

4. <span data-ttu-id="6fae9-138">Klik op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="6fae9-138">Click **Download**.</span></span>

5. <span data-ttu-id="6fae9-139">Hier ziet u vijf bestanden toodownload.</span><span class="sxs-lookup"><span data-stu-id="6fae9-139">You should see five files toodownload.</span></span> <span data-ttu-id="6fae9-140">Elk van deze map bestanden tooa downloaden.</span><span class="sxs-lookup"><span data-stu-id="6fae9-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="6fae9-141">Hallo-map kan ook worden gekopieerde tooa netwerkshare zijn die bereikbaar is vanaf het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6fae9-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="6fae9-142">Open Hallo map waar Hallo bestanden zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="6fae9-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="6fae9-143">![Bestanden in Hallo-pakket](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span><span class="sxs-lookup"><span data-stu-id="6fae9-143">![Files in hello package](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span></span>

    <span data-ttu-id="6fae9-144">U ziet:</span><span class="sxs-lookup"><span data-stu-id="6fae9-144">You see:</span></span>
    -  <span data-ttu-id="6fae9-145">Een pakketbestand van Microsoft Update zelfstandige `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="6fae9-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="6fae9-146">Dit bestand is software gebruikte tooupdate Hallo-apparaten.</span><span class="sxs-lookup"><span data-stu-id="6fae9-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="6fae9-147">Een pakketbestand Geneva Monitoring Agent `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="6fae9-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="6fae9-148">Dit bestand is gebruikte tooupdate Hallo controle en diagnostische gegevens (MDS)-service-agent.</span><span class="sxs-lookup"><span data-stu-id="6fae9-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="6fae9-149">Dubbelklik op Hallo cab-bestand.</span><span class="sxs-lookup"><span data-stu-id="6fae9-149">Double-click hello cab file.</span></span> <span data-ttu-id="6fae9-150">Een _.msi_ wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6fae9-150">A _.msi_ is displayed.</span></span> <span data-ttu-id="6fae9-151">Selecteer Hallo-bestand met de rechtermuisknop en vervolgens **extraheren** Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="6fae9-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="6fae9-152">Gebruik van Hallo _.msi_ bestand tooupdate Hallo agent.</span><span class="sxs-lookup"><span data-stu-id="6fae9-152">You use hello _.msi_ file tooupdate hello agent.</span></span>

        ![Update van Clientagent MDS-bestand uitpakken](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > <span data-ttu-id="6fae9-154">U hoeft geen tooupdate Hallo MDS agent als u het StorSimple Update 0,5 (0.0.10293.0) uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6fae9-154">You do not need tooupdate hello MDS agent if you are running StorSimple Update 0.5 (0.0.10293.0).</span></span>

    - <span data-ttu-id="6fae9-155">Drie bestanden met essentiële updates voor Windows-beveiliging, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, en `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="6fae9-155">Three files that contain critical Windows security updates, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span>


### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="6fae9-156">Hallo update of hotfix Hallo installeren</span><span class="sxs-lookup"><span data-stu-id="6fae9-156">Install hello update or hello hotfix</span></span>

<span data-ttu-id="6fae9-157">Installatie van eerdere toohello update of hotfix, Controleer of dat u Hallo update of hotfix Hallo gedownload lokaal op de host of toegankelijk via een netwerkshare.</span><span class="sxs-lookup"><span data-stu-id="6fae9-157">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="6fae9-158">Gebruik deze methode tooinstall updates op een apparaat met GA of 0,1 softwareversies bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6fae9-158">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="6fae9-159">Deze procedure duurt ongeveer 12 minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6fae9-159">This procedure takes approximately 12 minutes toocomplete.</span></span> <span data-ttu-id="6fae9-160">Uitvoeren van de volgende Hallo stappen tooinstall Hallo update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="6fae9-160">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="6fae9-161">tooinstall Hallo update of hotfix Hallo</span><span class="sxs-lookup"><span data-stu-id="6fae9-161">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="6fae9-162">Ga te in Hallo lokale webgebruikersinterface,**onderhoud** > **Software-Update**.</span><span class="sxs-lookup"><span data-stu-id="6fae9-162">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="6fae9-163">Noteer Hallo softwareversie die u uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6fae9-163">Make a note of hello software version that you are running.</span></span> <span data-ttu-id="6fae9-164">Als u werkt met **10.0.10290.0**, hoeft u geen tooupdate Hallo MDS-agent in stap 6.</span><span class="sxs-lookup"><span data-stu-id="6fae9-164">If you are running **10.0.10290.0**, you do not need tooupdate hello MDS agent in step 6.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="6fae9-166">In **Update bestandspad**, typ de bestandsnaam Hallo voor Hallo update of hotfix Hallo.</span><span class="sxs-lookup"><span data-stu-id="6fae9-166">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="6fae9-167">U kunt ook toohello update of hotfix installatiebestand Bladeren als geplaatst op een netwerkshare.</span><span class="sxs-lookup"><span data-stu-id="6fae9-167">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="6fae9-168">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="6fae9-168">Click **Apply**.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="6fae9-170">Een waarschuwing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6fae9-170">A warning is displayed.</span></span> <span data-ttu-id="6fae9-171">Gegeven Hallo is virtuele matrix een apparaat met één knooppunt, nadat het Hallo-update is toegepast, Hallo-apparaat opnieuw wordt opgestart en er is uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="6fae9-171">Given hello virtual array is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="6fae9-172">Klik op het vinkje Hallo.</span><span class="sxs-lookup"><span data-stu-id="6fae9-172">Click hello check icon.</span></span>
   
   ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="6fae9-174">Hallo-update is gestart.</span><span class="sxs-lookup"><span data-stu-id="6fae9-174">hello update starts.</span></span> <span data-ttu-id="6fae9-175">Nadat het Hallo-apparaat is bijgewerkt, opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="6fae9-175">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="6fae9-176">Hallo is lokale UI niet toegankelijk in deze duur.</span><span class="sxs-lookup"><span data-stu-id="6fae9-176">hello local UI is not accessible in this duration.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="6fae9-178">Nadat Hallo opnieuw opstarten voltooid is, gaat u toohello **aanmelden** pagina.</span><span class="sxs-lookup"><span data-stu-id="6fae9-178">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="6fae9-179">tooverify die software Hallo-apparaat is bijgewerkt in lokale Hallo-web-gebruikersinterface te gaan**onderhoud** > **Software-Update**.</span><span class="sxs-lookup"><span data-stu-id="6fae9-179">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="6fae9-180">de softwareversie weergegeven Hallo moet **10.0.0.0.0.10293** voor Update 0,6.</span><span class="sxs-lookup"><span data-stu-id="6fae9-180">hello displayed software version should be **10.0.0.0.0.10293** for Update 0.6.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6fae9-181">We Hallo softwareversies rapport in een iets andere manier in Hallo lokale webgebruikersinterface en hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6fae9-181">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="6fae9-182">Bijvoorbeeld Hallo lokale web UI rapporten **10.0.0.0.0.10293** en Azure portal rapporten Hallo **10.0.10293.0** voor Hallo dezelfde versie.</span><span class="sxs-lookup"><span data-stu-id="6fae9-182">For example, hello local web UI reports **10.0.0.0.0.10293** and hello Azure portal reports **10.0.10293.0** for hello same version.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. <span data-ttu-id="6fae9-184">Deze stap overslaan als u StorSimple virtuele matrix Update 0,5 uitvoerde (**10.0.10290.0**) voordat u deze update hebt toegepast.</span><span class="sxs-lookup"><span data-stu-id="6fae9-184">Skip this step if you were running StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) before you applied this update.</span></span> <span data-ttu-id="6fae9-185">U hebt een genoteerd Hallo softwareversie in stap 1 voordat u begint met tooupdate.</span><span class="sxs-lookup"><span data-stu-id="6fae9-185">You made a note of hello software version in step 1 before you began tooupdate.</span></span> <span data-ttu-id="6fae9-186">Als u Update 0,5 zijn uitgevoerd, is de MDS-agent al up-to-date.</span><span class="sxs-lookup"><span data-stu-id="6fae9-186">If you were running Update 0.5, your MDS agent is already up-to-date .</span></span>

    <span data-ttu-id="6fae9-187">Als u een software-versie voorafgaande tooUpdate 0,5 uitvoert, is de volgende stap Hallo voor u tooupdate Hallo MDS-agent.</span><span class="sxs-lookup"><span data-stu-id="6fae9-187">If you are running a software version prior tooUpdate 0.5, hello next step for you is tooupdate hello MDS agent.</span></span> <span data-ttu-id="6fae9-188">In Hallo **Software-Update** pagina, gaat u toohello **Update bestandspad** en blader toohello `GenevaMonitoringAgentPackageInstaller.msi` bestand.</span><span class="sxs-lookup"><span data-stu-id="6fae9-188">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="6fae9-189">Herhaal stappen 2 tot 4.</span><span class="sxs-lookup"><span data-stu-id="6fae9-189">Repeat steps 2-4.</span></span> <span data-ttu-id="6fae9-190">Nadat Hallo virtuele matrix opnieuw is opgestart, meldt u zich in Hallo lokale webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="6fae9-190">After hello virtual array restarts, sign into hello local web UI.</span></span>

7. <span data-ttu-id="6fae9-191">Herhaal stap 2-4 tooinstall Hallo Windows-beveiliging worden opgelost met behulp van bestanden `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, en `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="6fae9-191">Repeat step 2-4 tooinstall hello Windows security fixes using files `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span> <span data-ttu-id="6fae9-192">Hallo virtuele matrix wordt opnieuw opgestart na elke installatie en moet u toosign in Hallo lokale webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="6fae9-192">hello virtual array restarts after each install and you need toosign into hello local web UI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fae9-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6fae9-193">Next steps</span></span>

<span data-ttu-id="6fae9-194">Meer informatie over [beheer van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="6fae9-194">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

