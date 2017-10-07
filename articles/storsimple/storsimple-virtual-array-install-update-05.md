---
title: aaaInstall Update 0,5 op de virtuele StorSimple-matrix | Microsoft Docs
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
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="efd49-103">Update 0,5 installeren op uw virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="efd49-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="efd49-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="efd49-104">Overview</span></span>

<span data-ttu-id="efd49-105">In dit artikel beschrijft Hallo stappen vereist tooinstall Update 0,5 op uw virtuele StorSimple-matrix via Hallo lokale webgebruikersinterface en via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="efd49-105">This article describes hello steps required tooinstall Update 0.5 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="efd49-106">U moet het software-updates of hotfixes tookeep tooapply uw virtuele StorSimple-matrix up-to-date.</span><span class="sxs-lookup"><span data-stu-id="efd49-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="efd49-107">Voordat u een update hebt toegepast, wordt aangeraden dat u rekening houden met Hallo volumes of shares op Hallo eerst hosten en vervolgens Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="efd49-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="efd49-108">Dit verkleint dat beschadigde gegevens.</span><span class="sxs-lookup"><span data-stu-id="efd49-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="efd49-109">Nadat het Hallo-volumes of shares die offline is, u moet ook rekening houden met een handmatige back-up van het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="efd49-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="efd49-110">Update 0,5 te overeenkomt met**10.0.10290.0** softwareversie van de op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="efd49-110">Update 0.5 corresponds too**10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="efd49-111">Voor informatie over wat is er nieuw in deze update gaat te[Release-opmerkingen voor Update 0,5](storsimple-virtual-array-update-05-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="efd49-111">For information on what is new in this update, go too[Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="efd49-112">Als u Update 0.2 uitvoert of hoger, we raden installeren u Hallo updates via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="efd49-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="efd49-113">Als u Update 0.1 of GA softwareversies uitvoert, moet u Hallo hotfix methode via Hallo lokale web UI tooinstall Update 0,5 gebruiken.</span><span class="sxs-lookup"><span data-stu-id="efd49-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.5.</span></span>
>
> - <span data-ttu-id="efd49-114">Houd er rekening mee dat voor het installeren van een update of hotfix uw apparaat opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="efd49-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="efd49-115">Aangezien Hallo virtuele StorSimple-matrix is een apparaat met één knooppunt, een i/o uitgevoerd wordt onderbroken en uw apparaat uitval optreedt.</span><span class="sxs-lookup"><span data-stu-id="efd49-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="efd49-116">Gebruik hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="efd49-116">Use hello Azure portal</span></span>

<span data-ttu-id="efd49-117">Als Update 0,2 en hoger, raden wij aan dat u updates via hello Azure-portal installeert.</span><span class="sxs-lookup"><span data-stu-id="efd49-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="efd49-118">Hallo portal procedure vereist Hallo gebruiker tooscan, downloaden en installeer vervolgens Hallo-updates.</span><span class="sxs-lookup"><span data-stu-id="efd49-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="efd49-119">Deze procedure duurt ongeveer 7 minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="efd49-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="efd49-120">Uitvoeren van de volgende Hallo stappen tooinstall Hallo update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="efd49-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="efd49-121">Na het Hallo is installatie voltooid, gaat u tooyour StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="efd49-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="efd49-122">Selecteer **apparaten** en selecteer en klikt u op Hallo-apparaat die u zojuist hebt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="efd49-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="efd49-123">Ga te**instellingen > beheren > apparaatupdates**.</span><span class="sxs-lookup"><span data-stu-id="efd49-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="efd49-124">de softwareversie weergegeven Hallo moet **10.0.10290.0**.</span><span class="sxs-lookup"><span data-stu-id="efd49-124">hello displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="efd49-125">Gebruik Hallo lokale webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="efd49-125">Use hello local web UI</span></span>

<span data-ttu-id="efd49-126">Er zijn twee stappen wanneer u Hallo lokale-webgebruikersinterface:</span><span class="sxs-lookup"><span data-stu-id="efd49-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="efd49-127">Hallo update of hotfix Hallo downloaden</span><span class="sxs-lookup"><span data-stu-id="efd49-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="efd49-128">Hallo update of hotfix Hallo installeren</span><span class="sxs-lookup"><span data-stu-id="efd49-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="efd49-129">Hallo update of hotfix Hallo downloaden</span><span class="sxs-lookup"><span data-stu-id="efd49-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="efd49-130">Volgende stappen toodownload Hallo software-update vanaf Microsoft Update-catalogus Hallo Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="efd49-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="efd49-131">toodownload hello update of Hallo hotfix</span><span class="sxs-lookup"><span data-stu-id="efd49-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="efd49-132">Start Internet Explorer en navigeer te[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="efd49-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="efd49-133">Als dit de eerste keer dat u Microsoft Update-catalogus Hallo op deze computer is, klikt u op **installeren** wanneer na vragen aan gebruiker tooinstall Hallo-invoegtoepassing voor Microsoft Update-catalogus.</span><span class="sxs-lookup"><span data-stu-id="efd49-133">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="efd49-134">In het zoekvak Hallo Hallo Microsoft Update-catalogus, invoeren Hallo-Knowledge Base (KB) van de hotfix Hallo gewenste toodownload.</span><span class="sxs-lookup"><span data-stu-id="efd49-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="efd49-135">Voer **4021576** voor Update 0,5 en klik vervolgens op **Search**.</span><span class="sxs-lookup"><span data-stu-id="efd49-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="efd49-136">Hallo hotfix wordt weergegeven, bijvoorbeeld **StorSimple virtuele matrix Update 0,5**.</span><span class="sxs-lookup"><span data-stu-id="efd49-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![Catalogus doorzoeken](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="efd49-138">Klik op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="efd49-138">Click **Download**.</span></span> 

5. <span data-ttu-id="efd49-139">U ziet nu twee bestanden toodownload, een *MSU* en een *cab* bestand.</span><span class="sxs-lookup"><span data-stu-id="efd49-139">You should see two files toodownload, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="efd49-140">Elk van deze map bestanden tooa downloaden.</span><span class="sxs-lookup"><span data-stu-id="efd49-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="efd49-141">Hallo-map kan ook worden gekopieerde tooa netwerkshare zijn die bereikbaar is vanaf het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="efd49-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="efd49-142">Open Hallo map waar Hallo bestanden zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="efd49-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="efd49-143">![Bestanden in Hallo-pakket](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="efd49-143">![Files in hello package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="efd49-144">U ziet:</span><span class="sxs-lookup"><span data-stu-id="efd49-144">You see:</span></span>
    -  <span data-ttu-id="efd49-145">Een pakketbestand van Microsoft Update zelfstandige `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="efd49-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="efd49-146">Dit bestand is software gebruikte tooupdate Hallo-apparaten.</span><span class="sxs-lookup"><span data-stu-id="efd49-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="efd49-147">Een pakketbestand Geneva Monitoring Agent `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="efd49-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="efd49-148">Dit bestand is gebruikte tooupdate Hallo controle en diagnostische gegevens (MDS)-service-agent.</span><span class="sxs-lookup"><span data-stu-id="efd49-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="efd49-149">Dubbelklik op Hallo cab-bestand.</span><span class="sxs-lookup"><span data-stu-id="efd49-149">Double-click hello cab file.</span></span> <span data-ttu-id="efd49-150">Een .msi wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="efd49-150">A .msi is displayed.</span></span> <span data-ttu-id="efd49-151">Selecteer Hallo-bestand met de rechtermuisknop en vervolgens **extraheren** Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="efd49-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="efd49-152">U gebruikt Hallo _.msi_ bestand tooupdate Hallo agent.</span><span class="sxs-lookup"><span data-stu-id="efd49-152">You will use hello _.msi_ file tooupdate hello agent.</span></span>

        ![Update van Clientagent MDS-bestand uitpakken](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="efd49-154">Hallo update of hotfix Hallo installeren</span><span class="sxs-lookup"><span data-stu-id="efd49-154">Install hello update or hello hotfix</span></span>

<span data-ttu-id="efd49-155">Installatie van eerdere toohello update of hotfix, Controleer of dat u Hallo update of hotfix Hallo gedownload lokaal op de host of toegankelijk via een netwerkshare.</span><span class="sxs-lookup"><span data-stu-id="efd49-155">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="efd49-156">Gebruik deze methode tooinstall updates op een apparaat met GA of 0,1 softwareversies bijwerken.</span><span class="sxs-lookup"><span data-stu-id="efd49-156">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="efd49-157">Deze procedure duurt minder dan twee minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="efd49-157">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="efd49-158">Uitvoeren van de volgende Hallo stappen tooinstall Hallo update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="efd49-158">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="efd49-159">tooinstall Hallo update of hotfix Hallo</span><span class="sxs-lookup"><span data-stu-id="efd49-159">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="efd49-160">Ga te in Hallo lokale webgebruikersinterface,**onderhoud** > **Software-Update**.</span><span class="sxs-lookup"><span data-stu-id="efd49-160">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="efd49-162">In **Update bestandspad**, typ de bestandsnaam Hallo voor Hallo update of hotfix Hallo.</span><span class="sxs-lookup"><span data-stu-id="efd49-162">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="efd49-163">U kunt ook toohello update of hotfix installatiebestand Bladeren als geplaatst op een netwerkshare.</span><span class="sxs-lookup"><span data-stu-id="efd49-163">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="efd49-164">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="efd49-164">Click **Apply**.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="efd49-166">Een waarschuwing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="efd49-166">A warning is displayed.</span></span> <span data-ttu-id="efd49-167">Gegeven dit is een apparaat met één knooppunt, nadat het Hallo-update is toegepast, Hallo-apparaat opnieuw wordt opgestart en er is uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="efd49-167">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="efd49-168">Klik op het vinkje Hallo.</span><span class="sxs-lookup"><span data-stu-id="efd49-168">Click hello check icon.</span></span>
   
   ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="efd49-170">Hallo-update is gestart.</span><span class="sxs-lookup"><span data-stu-id="efd49-170">hello update starts.</span></span> <span data-ttu-id="efd49-171">Nadat het Hallo-apparaat is bijgewerkt, opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="efd49-171">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="efd49-172">Hallo is lokale UI niet toegankelijk in deze duur.</span><span class="sxs-lookup"><span data-stu-id="efd49-172">hello local UI is not accessible in this duration.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="efd49-174">Nadat Hallo opnieuw opstarten voltooid is, gaat u toohello **aanmelden** pagina.</span><span class="sxs-lookup"><span data-stu-id="efd49-174">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="efd49-175">tooverify die software Hallo-apparaat is bijgewerkt in lokale Hallo-web-gebruikersinterface te gaan**onderhoud** > **Software-Update**.</span><span class="sxs-lookup"><span data-stu-id="efd49-175">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="efd49-176">de softwareversie weergegeven Hallo moet **10.0.0.0.0.10290.0** voor Update 0,5.</span><span class="sxs-lookup"><span data-stu-id="efd49-176">hello displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="efd49-177">We Hallo softwareversies rapport in een iets andere manier in Hallo lokale webgebruikersinterface en hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="efd49-177">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="efd49-178">Bijvoorbeeld Hallo lokale web UI rapporten **10.0.0.0.0.10290** en Azure portal rapporten Hallo **10.0.10290.0** voor Hallo dezelfde versie.</span><span class="sxs-lookup"><span data-stu-id="efd49-178">For example, hello local web UI reports **10.0.0.0.0.10290** and hello Azure portal reports **10.0.10290.0** for hello same version.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="efd49-180">de volgende stap Hallo is tooupdate Hallo MDS-agent.</span><span class="sxs-lookup"><span data-stu-id="efd49-180">hello next step is tooupdate hello MDS agent.</span></span> <span data-ttu-id="efd49-181">In Hallo **Software-Update** pagina, gaat u toohello **Update bestandspad** en blader toohello `GenevaMonitoringAgentPackageInstaller.msi` bestand.</span><span class="sxs-lookup"><span data-stu-id="efd49-181">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="efd49-182">Herhaal stappen 2 tot 4.</span><span class="sxs-lookup"><span data-stu-id="efd49-182">Repeat steps 2-4.</span></span> <span data-ttu-id="efd49-183">Nadat Hallo virtuele matrix opnieuw is opgestart, meldt u zich in Hallo lokale webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="efd49-183">After hello virtual array restarts, sign into hello local web UI.</span></span>

<span data-ttu-id="efd49-184">Hallo-update is nu voltooid.</span><span class="sxs-lookup"><span data-stu-id="efd49-184">hello update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efd49-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="efd49-185">Next steps</span></span>

<span data-ttu-id="efd49-186">Meer informatie over [beheer van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="efd49-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

