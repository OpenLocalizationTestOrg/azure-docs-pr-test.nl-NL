---
title: Updates op de virtuele StorSimple-matrix aaaInstall | Microsoft Docs
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
ms.date: 02/07/2017
ms.author: alkohli
ms.openlocfilehash: 6165b305fb0d404b404cf3a11dd0ade2f2f13b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-04-on-your-storsimple-virtual-array"></a><span data-ttu-id="e9565-103">Update 0,4 installeren op uw virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="e9565-103">Install Update 0.4 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="e9565-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e9565-104">Overview</span></span>

<span data-ttu-id="e9565-105">In dit artikel beschrijft Hallo stappen vereist tooinstall Update 0,4 op uw virtuele StorSimple-matrix via Hallo lokale webgebruikersinterface en via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e9565-105">This article describes hello steps required tooinstall Update 0.4 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="e9565-106">U moet het software-updates of hotfixes tookeep tooapply uw virtuele StorSimple-matrix up-to-date.</span><span class="sxs-lookup"><span data-stu-id="e9565-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="e9565-107">Houd er rekening mee dat voor het installeren van een update of hotfix uw apparaat opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="e9565-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="e9565-108">Aangezien Hallo virtuele StorSimple-matrix is een apparaat met één knooppunt, een i/o uitgevoerd wordt onderbroken en uw apparaat uitval optreedt.</span><span class="sxs-lookup"><span data-stu-id="e9565-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="e9565-109">Voordat u een update hebt toegepast, wordt aangeraden dat u rekening houden met Hallo volumes of shares op Hallo eerst hosten en vervolgens Hallo apparaat.</span><span class="sxs-lookup"><span data-stu-id="e9565-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="e9565-110">Dit verkleint dat beschadigde gegevens.</span><span class="sxs-lookup"><span data-stu-id="e9565-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9565-111">Als u Update 0.1 of GA softwareversies uitvoert, moet u Hallo hotfix methode via Hallo lokale web UI tooinstall update 0.3.</span><span class="sxs-lookup"><span data-stu-id="e9565-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="e9565-112">Als u Update 0.2 uitvoert of hoger, we raden installeren u Hallo updates via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e9565-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span>
 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="e9565-113">Gebruik Hallo lokale webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="e9565-113">Use hello local web UI</span></span>

<span data-ttu-id="e9565-114">Er zijn twee stappen wanneer u Hallo lokale-webgebruikersinterface:</span><span class="sxs-lookup"><span data-stu-id="e9565-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="e9565-115">Hallo update of hotfix Hallo downloaden</span><span class="sxs-lookup"><span data-stu-id="e9565-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="e9565-116">Hallo update of hotfix Hallo installeren</span><span class="sxs-lookup"><span data-stu-id="e9565-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="e9565-117">Hallo update of hotfix Hallo downloaden</span><span class="sxs-lookup"><span data-stu-id="e9565-117">Download hello update or hello hotfix</span></span>

<span data-ttu-id="e9565-118">Volgende stappen toodownload Hallo software-update vanaf Microsoft Update-catalogus Hallo Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e9565-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="e9565-119">toodownload hello update of Hallo hotfix</span><span class="sxs-lookup"><span data-stu-id="e9565-119">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="e9565-120">Start Internet Explorer en navigeer te[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e9565-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="e9565-121">Als dit de eerste keer dat u Microsoft Update-catalogus Hallo op deze computer is, klikt u op **installeren** wanneer na vragen aan gebruiker tooinstall Hallo-invoegtoepassing voor Microsoft Update-catalogus.</span><span class="sxs-lookup"><span data-stu-id="e9565-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="e9565-122">In het zoekvak Hallo Hallo Microsoft Update-catalogus, invoeren Hallo-Knowledge Base (KB) van de hotfix Hallo gewenste toodownload.</span><span class="sxs-lookup"><span data-stu-id="e9565-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="e9565-123">Voer **3216577** voor Update 0,4 en klik vervolgens op **Search**.</span><span class="sxs-lookup"><span data-stu-id="e9565-123">Enter **3216577** for Update 0.4, and then click **Search**.</span></span>
   
    <span data-ttu-id="e9565-124">Hallo hotfix wordt weergegeven, bijvoorbeeld **StorSimple virtuele matrix Update 0,4**.</span><span class="sxs-lookup"><span data-stu-id="e9565-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.4**.</span></span>
   
    ![Catalogus doorzoeken](./media/storsimple-virtual-array-install-update-04/download1.png)

4. <span data-ttu-id="e9565-126">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="e9565-126">Click **Add**.</span></span> <span data-ttu-id="e9565-127">Hallo-update is toohello mandje toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e9565-127">hello update is added toohello basket.</span></span>

5. <span data-ttu-id="e9565-128">Klik op **Mandje weergeven**.</span><span class="sxs-lookup"><span data-stu-id="e9565-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="e9565-129">Klik op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="e9565-129">Click **Download**.</span></span> <span data-ttu-id="e9565-130">Opgeven of **Bladeren** tooa lokale locatie waar u Hallo tooappear downloadt.</span><span class="sxs-lookup"><span data-stu-id="e9565-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="e9565-131">Hallo-updates worden gedownload toohello opgegeven locatie en in een submap met dezelfde naam als de update Hallo Hallo geplaatst.</span><span class="sxs-lookup"><span data-stu-id="e9565-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="e9565-132">Hallo-map kan ook worden gekopieerde tooa netwerkshare zijn die bereikbaar is vanaf het Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="e9565-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

7. <span data-ttu-id="e9565-133">Open Hallo map gekopieerd, ziet u een zelfstandige pakket voor Microsoft Update-bestand `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="e9565-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="e9565-134">Dit bestand is gebruikte tooinstall Hallo update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="e9565-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="e9565-135">Hallo update of hotfix Hallo installeren</span><span class="sxs-lookup"><span data-stu-id="e9565-135">Install hello update or hello hotfix</span></span>

<span data-ttu-id="e9565-136">Installatie van eerdere toohello update of hotfix, Controleer of dat u Hallo update of hotfix Hallo gedownload lokaal op de host of toegankelijk via een netwerkshare.</span><span class="sxs-lookup"><span data-stu-id="e9565-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="e9565-137">Gebruik deze methode tooinstall updates op een apparaat met GA of 0,1 softwareversies bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e9565-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="e9565-138">Deze procedure duurt minder dan twee minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e9565-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="e9565-139">Uitvoeren van de volgende Hallo stappen tooinstall Hallo update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="e9565-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="e9565-140">tooinstall Hallo update of hotfix Hallo</span><span class="sxs-lookup"><span data-stu-id="e9565-140">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="e9565-141">Ga te in Hallo lokale webgebruikersinterface,**onderhoud** > **Software-Update**.</span><span class="sxs-lookup"><span data-stu-id="e9565-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="e9565-143">In **Update bestandspad**, typ de bestandsnaam Hallo voor Hallo update of hotfix Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9565-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="e9565-144">U kunt ook toohello update of hotfix installatiebestand Bladeren als geplaatst op een netwerkshare.</span><span class="sxs-lookup"><span data-stu-id="e9565-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="e9565-145">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="e9565-145">Click **Apply**.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="e9565-147">Een waarschuwing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e9565-147">A warning is displayed.</span></span> <span data-ttu-id="e9565-148">Gegeven dit is een apparaat met één knooppunt, nadat het Hallo-update is toegepast, Hallo-apparaat opnieuw wordt opgestart en er is uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="e9565-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="e9565-149">Klik op het vinkje Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9565-149">Click hello check icon.</span></span>
   
   ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="e9565-151">Hallo-update is gestart.</span><span class="sxs-lookup"><span data-stu-id="e9565-151">hello update starts.</span></span> <span data-ttu-id="e9565-152">Nadat het Hallo-apparaat is bijgewerkt, opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="e9565-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="e9565-153">Hallo is lokale UI niet toegankelijk in deze duur.</span><span class="sxs-lookup"><span data-stu-id="e9565-153">hello local UI is not accessible in this duration.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="e9565-155">Nadat Hallo opnieuw opstarten voltooid is, gaat u toohello **aanmelden** pagina.</span><span class="sxs-lookup"><span data-stu-id="e9565-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="e9565-156">tooverify die software Hallo-apparaat is bijgewerkt in lokale Hallo-web-gebruikersinterface te gaan**onderhoud** > **Software-Update**.</span><span class="sxs-lookup"><span data-stu-id="e9565-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="e9565-157">de softwareversie weergegeven Hallo moet **10.0.0.0.0.10289.0** voor Update 0,4.</span><span class="sxs-lookup"><span data-stu-id="e9565-157">hello displayed software version should be **10.0.0.0.0.10289.0** for Update 0.4.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e9565-158">We Hallo softwareversies rapport in een iets andere manier in Hallo lokale webgebruikersinterface en hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e9565-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="e9565-159">Bijvoorbeeld Hallo lokale web UI rapporten **10.0.0.0.0.10289** en Azure portal rapporten Hallo **10.0.10289.0** voor Hallo dezelfde versie.</span><span class="sxs-lookup"><span data-stu-id="e9565-159">For example, hello local web UI reports **10.0.0.0.0.10289** and hello Azure portal reports **10.0.10289.0** for hello same version.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a><span data-ttu-id="e9565-161">Gebruik hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e9565-161">Use hello Azure portal</span></span>

<span data-ttu-id="e9565-162">Als Update 0,2 en hoger, raden wij aan dat u updates via hello Azure-portal installeert.</span><span class="sxs-lookup"><span data-stu-id="e9565-162">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="e9565-163">Hallo portal procedure vereist Hallo gebruiker tooscan, downloaden en installeer vervolgens Hallo-updates.</span><span class="sxs-lookup"><span data-stu-id="e9565-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="e9565-164">Deze procedure duurt ongeveer 7 minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e9565-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="e9565-165">Uitvoeren van de volgende Hallo stappen tooinstall Hallo update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="e9565-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="e9565-166">Na het Hallo is installatie voltooid (zoals aangegeven door de status van de taak op 100%), Ga tooyour StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="e9565-166">After hello installation is complete (as indicated by job status at 100 %), go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="e9565-167">Selecteer **apparaten** en selecteer en klik op de gewenste tooupdate uit Hallo lijst met apparaten verbonden toothis service Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="e9565-167">Select **Devices** and then select and click hello device you want tooupdate from hello list of devices connected toothis service.</span></span> <span data-ttu-id="e9565-168">In Hallo **instellingen** blade te gaan**beheren** sectie en selecteer **apparaatupdates**.</span><span class="sxs-lookup"><span data-stu-id="e9565-168">In hello **Settings** blade, go too**Manage** section and select **Device updates**.</span></span> <span data-ttu-id="e9565-169">de softwareversie weergegeven Hallo moet **10.0.10289.0**.</span><span class="sxs-lookup"><span data-stu-id="e9565-169">hello displayed software version should be **10.0.10289.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e9565-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9565-170">Next steps</span></span>

<span data-ttu-id="e9565-171">Meer informatie over [beheer van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="e9565-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

