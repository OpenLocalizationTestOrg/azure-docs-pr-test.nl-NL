---
title: Updates installeren op de virtuele StorSimple-matrix | Microsoft Docs
description: Beschrijft hoe u de virtuele StorSimple-matrix-webgebruikersinterface toepassen van updates via de Azure portal en de hotfix-methode
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
ms.openlocfilehash: 3fb246b1515e7a637e6cff6499bf324c3f80dd45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-04-on-your-storsimple-virtual-array"></a><span data-ttu-id="ce5bb-103">Update 0,4 installeren op uw virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="ce5bb-103">Install Update 0.4 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="ce5bb-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ce5bb-104">Overview</span></span>

<span data-ttu-id="ce5bb-105">In dit artikel beschrijft de stappen voor het installeren van Update 0,4 op uw virtuele StorSimple-matrix via de lokale webgebruikersinterface en via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-105">This article describes the steps required to install Update 0.4 on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="ce5bb-106">U moet toepassen van software-updates of hotfixes voor uw virtuele StorSimple-matrix up-to-date te houden.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="ce5bb-107">Houd er rekening mee dat voor het installeren van een update of hotfix uw apparaat opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="ce5bb-108">Gezien het feit dat het virtuele StorSimple-matrix een apparaat met één knooppunt is, een i/o uitgevoerd wordt onderbroken en uw apparaat ervaringen uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="ce5bb-109">Voordat u een update hebt toegepast, wordt u aangeraden dat u rekening houden met de volumes of shares offline op de host eerst en klik vervolgens op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="ce5bb-110">Dit verkleint dat beschadigde gegevens.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce5bb-111">Als u Update 0.1 of GA softwareversies uitvoert, moet u de hotfix-methode via de lokale webgebruikersinterface voor het installeren van update 0.3.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="ce5bb-112">Als u Update 0.2 uitvoert of hoger, we raden installeren u de updates via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-112">If you are running Update 0.2 or later, we recommend that you install the updates via the Azure portal.</span></span>
 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="ce5bb-113">Gebruik de lokale webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="ce5bb-113">Use the local web UI</span></span>

<span data-ttu-id="ce5bb-114">Er zijn twee stappen wanneer u de lokale-webgebruikersinterface:</span><span class="sxs-lookup"><span data-stu-id="ce5bb-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="ce5bb-115">Download de update of hotfix</span><span class="sxs-lookup"><span data-stu-id="ce5bb-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="ce5bb-116">Installeer de update of de hotfix</span><span class="sxs-lookup"><span data-stu-id="ce5bb-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="ce5bb-117">Download de update of hotfix</span><span class="sxs-lookup"><span data-stu-id="ce5bb-117">Download the update or the hotfix</span></span>

<span data-ttu-id="ce5bb-118">Voer de volgende stappen uit om de software-update te downloaden uit de Microsoft Update-catalogus.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="ce5bb-119">De update of de hotfix te downloaden</span><span class="sxs-lookup"><span data-stu-id="ce5bb-119">To download the update or the hotfix</span></span>

1. <span data-ttu-id="ce5bb-120">Start Internet Explorer en blader naar [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ce5bb-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="ce5bb-121">Als dit de eerste keer is dat u de Microsoft Update-catalogus op deze computer gebruikt, klikt u op **Installeren** wanneer u wordt gevraagd of u de invoegtoepassing voor de Microsoft Update-catalogus wilt installeren.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="ce5bb-122">Voer in het zoekvak van Microsoft Update-catalogus, het aantal Knowledge Base (KB) van de hotfix die u wilt downloaden.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="ce5bb-123">Voer **3216577** voor Update 0,4 en klik vervolgens op **Search**.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-123">Enter **3216577** for Update 0.4, and then click **Search**.</span></span>
   
    <span data-ttu-id="ce5bb-124">De hotfix-wordt weergegeven, bijvoorbeeld **StorSimple virtuele matrix Update 0,4**.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.4**.</span></span>
   
    ![Catalogus doorzoeken](./media/storsimple-virtual-array-install-update-04/download1.png)

4. <span data-ttu-id="ce5bb-126">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-126">Click **Add**.</span></span> <span data-ttu-id="ce5bb-127">De update wordt toegevoegd aan het mandje.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-127">The update is added to the basket.</span></span>

5. <span data-ttu-id="ce5bb-128">Klik op **Mandje weergeven**.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="ce5bb-129">Klik op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-129">Click **Download**.</span></span> <span data-ttu-id="ce5bb-130">Typ of **blader naar** een lokale locatie waar u de downloads wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="ce5bb-131">De updates worden naar de opgegeven locatie gedownload en in een submap met dezelfde naam als de update geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="ce5bb-132">De map kan ook worden gekopieerd naar een netwerkshare die bereikbaar is vanaf het apparaat.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-132">The folder can also be copied to a network share that is reachable from the device.</span></span>

7. <span data-ttu-id="ce5bb-133">De gekopieerde map opent, ziet u een zelfstandige pakket voor Microsoft Update-bestand `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="ce5bb-134">Dit bestand wordt gebruikt voor het installeren van de update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="ce5bb-135">Installeer de update of de hotfix</span><span class="sxs-lookup"><span data-stu-id="ce5bb-135">Install the update or the hotfix</span></span>

<span data-ttu-id="ce5bb-136">Controleer of dat u de update hebt of de hotfix gedownload lokaal op de host of toegankelijk via een netwerkshare voor de installatie van de update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="ce5bb-137">Gebruik deze methode updates installeren op een apparaat met GA of 0,1 softwareversies bijwerken.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="ce5bb-138">Deze procedure duurt minder dan 2 minuten.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="ce5bb-139">Voer de volgende stappen uit voor het installeren van de update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="ce5bb-140">De update of de hotfix te installeren</span><span class="sxs-lookup"><span data-stu-id="ce5bb-140">To install the update or the hotfix</span></span>

1. <span data-ttu-id="ce5bb-141">Ga in de lokale webgebruikersinterface naar **onderhoud** > **Software-Update**.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="ce5bb-143">In **Update bestandspad**, geef de bestandsnaam voor de update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="ce5bb-144">U kunt ook bladeren naar het installatiebestand update of hotfix als geplaatst op een netwerkshare.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="ce5bb-145">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-145">Click **Apply**.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="ce5bb-147">Een waarschuwing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-147">A warning is displayed.</span></span> <span data-ttu-id="ce5bb-148">Gegeven dit is een apparaat met één knooppunt, nadat de update is toegepast, het apparaat opnieuw wordt opgestart en er uitvaltijd is.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="ce5bb-149">Klik op het vinkje.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-149">Click the check icon.</span></span>
   
   ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="ce5bb-151">De update wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-151">The update starts.</span></span> <span data-ttu-id="ce5bb-152">Nadat het apparaat is bijgewerkt, opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="ce5bb-153">De lokale gebruikersinterface is niet toegankelijk in deze duur.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-153">The local UI is not accessible in this duration.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="ce5bb-155">Nadat het opnieuw opstarten voltooid is, gaat u naar de **aanmelden** pagina.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="ce5bb-156">Om te controleren of software van het apparaat is bijgewerkt, in de lokale webgebruikersinterface, gaat u naar **onderhoud** > **Software-Update**.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="ce5bb-157">De weergegeven software-versie moet **10.0.0.0.0.10289.0** voor Update 0,4.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-157">The displayed software version should be **10.0.0.0.0.10289.0** for Update 0.4.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ce5bb-158">We rapport de softwareversies in een iets andere manier in de lokale webgebruikersinterface en de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-158">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="ce5bb-159">Bijvoorbeeld: de lokale webgebruikersinterface rapporten **10.0.0.0.0.10289** en de Azure portal rapporten **10.0.10289.0** voor dezelfde versie.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-159">For example, the local web UI reports **10.0.0.0.0.10289** and the Azure portal reports **10.0.10289.0** for the same version.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-the-azure-portal"></a><span data-ttu-id="ce5bb-161">Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="ce5bb-161">Use the Azure portal</span></span>

<span data-ttu-id="ce5bb-162">Als Update 0,2 en hoger, raden wij aan dat u updates via de Azure portal installeert.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-162">If running Update 0.2 and later, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="ce5bb-163">De portal procedure moet de gebruiker om te scannen, downloaden en installeer vervolgens de updates.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="ce5bb-164">Deze procedure duurt ongeveer 7 minuten is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="ce5bb-165">Voer de volgende stappen uit voor het installeren van de update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="ce5bb-166">Nadat de installatie is voltooid (zoals aangegeven door de status van de taak op 100%), gaat u naar uw StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-166">After the installation is complete (as indicated by job status at 100 %), go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="ce5bb-167">Selecteer **apparaten** en selecteer en klik op het apparaat dat u wilt bijwerken in de lijst met apparaten die zijn verbonden met deze service.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-167">Select **Devices** and then select and click the device you want to update from the list of devices connected to this service.</span></span> <span data-ttu-id="ce5bb-168">In de **instellingen** blade, gaat u naar **beheren** sectie en selecteer **apparaatupdates**.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-168">In the **Settings** blade, go to **Manage** section and select **Device updates**.</span></span> <span data-ttu-id="ce5bb-169">De weergegeven software-versie moet **10.0.10289.0**.</span><span class="sxs-lookup"><span data-stu-id="ce5bb-169">The displayed software version should be **10.0.10289.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ce5bb-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ce5bb-170">Next steps</span></span>

<span data-ttu-id="ce5bb-171">Meer informatie over [beheer van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="ce5bb-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

