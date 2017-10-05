---
title: Updates installeren op een virtuele Microsoft Azure StorSimple-matrix | Microsoft Docs
description: Beschrijft hoe u de virtuele StorSimple-matrix-webgebruikersinterface toepassen van updates via de portal en de hotfix-methode
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 9997a97b-9382-43ed-b56e-61369335c987
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c2d081604c0ca01f47c3ff2aab7477859d280963
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array---azure-portal"></a><span data-ttu-id="cd533-103">Updates installeren op uw StorSimple virtuele matrix - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="cd533-103">Install Updates on your StorSimple Virtual Array - Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="cd533-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="cd533-104">Overview</span></span>

<span data-ttu-id="cd533-105">In dit artikel beschrijft de stappen die nodig zijn om updates te installeren op uw virtuele StorSimple-matrix via de lokale webgebruikersinterface en via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cd533-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="cd533-106">U moet toepassen van software-updates of hotfixes voor uw virtuele StorSimple-matrix up-to-date te houden.</span><span class="sxs-lookup"><span data-stu-id="cd533-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="cd533-107">Houd er rekening mee dat voor het installeren van een update of hotfix uw apparaat opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="cd533-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="cd533-108">Gezien het feit dat het virtuele StorSimple-matrix een apparaat met één knooppunt is, een i/o uitgevoerd wordt onderbroken en uw apparaat ervaringen uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="cd533-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="cd533-109">Voordat u een update hebt toegepast, wordt u aangeraden dat u rekening houden met de volumes of shares offline op de host eerst en klik vervolgens op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="cd533-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="cd533-110">Dit verkleint dat beschadigde gegevens.</span><span class="sxs-lookup"><span data-stu-id="cd533-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd533-111">Als u Update 0.1 of GA softwareversies uitvoert, moet u de hotfix-methode via de lokale webgebruikersinterface voor het installeren van update 0.3.</span><span class="sxs-lookup"><span data-stu-id="cd533-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="cd533-112">Als u Update 0.2 uitvoert, raden wij aan dat u de updates via de klassieke Azure portal installeert.</span><span class="sxs-lookup"><span data-stu-id="cd533-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="cd533-113">Gebruik de lokale webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="cd533-113">Use the local web UI</span></span>

<span data-ttu-id="cd533-114">Er zijn twee stappen wanneer u de lokale-webgebruikersinterface:</span><span class="sxs-lookup"><span data-stu-id="cd533-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="cd533-115">Download de update of hotfix</span><span class="sxs-lookup"><span data-stu-id="cd533-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="cd533-116">Installeer de update of de hotfix</span><span class="sxs-lookup"><span data-stu-id="cd533-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="cd533-117">Download de update of hotfix</span><span class="sxs-lookup"><span data-stu-id="cd533-117">Download the update or the hotfix</span></span>

<span data-ttu-id="cd533-118">Voer de volgende stappen uit om de software-update te downloaden uit de Microsoft Update-catalogus.</span><span class="sxs-lookup"><span data-stu-id="cd533-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="cd533-119">De update of de hotfix te downloaden</span><span class="sxs-lookup"><span data-stu-id="cd533-119">To download the update or the hotfix</span></span>

1. <span data-ttu-id="cd533-120">Start Internet Explorer en blader naar [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cd533-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="cd533-121">Als dit de eerste keer is dat u de Microsoft Update-catalogus op deze computer gebruikt, klikt u op **Installeren** wanneer u wordt gevraagd of u de invoegtoepassing voor de Microsoft Update-catalogus wilt installeren.</span><span class="sxs-lookup"><span data-stu-id="cd533-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="cd533-122">Voer in het zoekvak van Microsoft Update-catalogus, het aantal Knowledge Base (KB) van de hotfix die u wilt downloaden.</span><span class="sxs-lookup"><span data-stu-id="cd533-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="cd533-123">Voer **3182061** voor Update 0.3 en klik vervolgens op **Search**.</span><span class="sxs-lookup"><span data-stu-id="cd533-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="cd533-124">De hotfix-wordt weergegeven, bijvoorbeeld **StorSimple virtuele matrix Update 0.3**.</span><span class="sxs-lookup"><span data-stu-id="cd533-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Catalogus doorzoeken](./media/storsimple-virtual-array-install-update/download1.png)

4. <span data-ttu-id="cd533-126">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="cd533-126">Click **Add**.</span></span> <span data-ttu-id="cd533-127">De update wordt toegevoegd aan het mandje.</span><span class="sxs-lookup"><span data-stu-id="cd533-127">The update is added to the basket.</span></span>

5. <span data-ttu-id="cd533-128">Klik op **Mandje weergeven**.</span><span class="sxs-lookup"><span data-stu-id="cd533-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="cd533-129">Klik op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="cd533-129">Click **Download**.</span></span> <span data-ttu-id="cd533-130">Typ of **blader naar** een lokale locatie waar u de downloads wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="cd533-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="cd533-131">De updates worden naar de opgegeven locatie gedownload en in een submap met dezelfde naam als de update geplaatst.</span><span class="sxs-lookup"><span data-stu-id="cd533-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="cd533-132">De map kan ook worden gekopieerd naar een netwerkshare die bereikbaar is vanaf het apparaat.</span><span class="sxs-lookup"><span data-stu-id="cd533-132">The folder can also be copied to a network share that is reachable from the device.</span></span>

7. <span data-ttu-id="cd533-133">De gekopieerde map opent, ziet u een zelfstandige pakket voor Microsoft Update-bestand `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="cd533-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="cd533-134">Dit bestand wordt gebruikt voor het installeren van de update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="cd533-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="cd533-135">Installeer de update of de hotfix</span><span class="sxs-lookup"><span data-stu-id="cd533-135">Install the update or the hotfix</span></span>

<span data-ttu-id="cd533-136">Controleer of dat u de update hebt of de hotfix gedownload lokaal op de host of toegankelijk via een netwerkshare voor de installatie van de update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="cd533-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="cd533-137">Gebruik deze methode updates installeren op een apparaat met GA of 0,1 softwareversies bijwerken.</span><span class="sxs-lookup"><span data-stu-id="cd533-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="cd533-138">Deze procedure duurt minder dan 2 minuten.</span><span class="sxs-lookup"><span data-stu-id="cd533-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="cd533-139">Voer de volgende stappen uit voor het installeren van de update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="cd533-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="cd533-140">De update of de hotfix te installeren</span><span class="sxs-lookup"><span data-stu-id="cd533-140">To install the update or the hotfix</span></span>

1. <span data-ttu-id="cd533-141">Ga in de lokale webgebruikersinterface naar **onderhoud** > **Software-Update**.</span><span class="sxs-lookup"><span data-stu-id="cd533-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="cd533-143">In **Update bestandspad**, geef de bestandsnaam voor de update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="cd533-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="cd533-144">U kunt ook bladeren naar het installatiebestand update of hotfix als geplaatst op een netwerkshare.</span><span class="sxs-lookup"><span data-stu-id="cd533-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="cd533-145">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="cd533-145">Click **Apply**.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="cd533-147">Een waarschuwing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cd533-147">A warning is displayed.</span></span> <span data-ttu-id="cd533-148">Gegeven dit is een apparaat met één knooppunt, nadat de update is toegepast, het apparaat opnieuw wordt opgestart en er uitvaltijd is.</span><span class="sxs-lookup"><span data-stu-id="cd533-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="cd533-149">Klik op het vinkje.</span><span class="sxs-lookup"><span data-stu-id="cd533-149">Click the check icon.</span></span>
   
   ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="cd533-151">De update wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="cd533-151">The update starts.</span></span> <span data-ttu-id="cd533-152">Nadat het apparaat is bijgewerkt, opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="cd533-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="cd533-153">De lokale gebruikersinterface is niet toegankelijk in deze duur.</span><span class="sxs-lookup"><span data-stu-id="cd533-153">The local UI is not accessible in this duration.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="cd533-155">Nadat het opnieuw opstarten voltooid is, gaat u naar de **aanmelden** pagina.</span><span class="sxs-lookup"><span data-stu-id="cd533-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="cd533-156">Om te controleren of software van het apparaat is bijgewerkt, in de lokale webgebruikersinterface, gaat u naar **onderhoud** > **Software-Update**.</span><span class="sxs-lookup"><span data-stu-id="cd533-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="cd533-157">De weergegeven software-versie moet **10.0.0.0.0.10288.0** voor Update 0.3.</span><span class="sxs-lookup"><span data-stu-id="cd533-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cd533-158">We rapport de softwareversies in een iets andere manier in de lokale webgebruikersinterface en de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd533-158">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="cd533-159">Bijvoorbeeld: de lokale webgebruikersinterface rapporten **10.0.0.0.0.10288** en de Azure portal rapporten **10.0.10288.0** voor dezelfde versie.</span><span class="sxs-lookup"><span data-stu-id="cd533-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure portal reports **10.0.10288.0** for the same version.</span></span>
   
    ![apparaat bijwerken](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-the-azure-portal"></a><span data-ttu-id="cd533-161">Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="cd533-161">Use the Azure portal</span></span>

<span data-ttu-id="cd533-162">Als u Update 0.2 uitvoert, wordt u aangeraden updates via de Azure portal te installeren.</span><span class="sxs-lookup"><span data-stu-id="cd533-162">If running Update 0.2, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="cd533-163">De portal procedure moet de gebruiker om te scannen, downloaden en installeer vervolgens de updates.</span><span class="sxs-lookup"><span data-stu-id="cd533-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="cd533-164">Deze procedure duurt ongeveer 7 minuten is voltooid.</span><span class="sxs-lookup"><span data-stu-id="cd533-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="cd533-165">Voer de volgende stappen uit voor het installeren van de update of hotfix.</span><span class="sxs-lookup"><span data-stu-id="cd533-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal.md)]

<span data-ttu-id="cd533-166">Nadat de installatie is voltooid (zoals aangegeven door de status van de taak op 100%), gaat u naar uw StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="cd533-166">After the installation is complete (as indicated by job status at 100 %), go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="cd533-167">Selecteer **apparaten** en selecteer en klik op het apparaat dat u wilt bijwerken in de lijst met apparaten die zijn verbonden met deze service.</span><span class="sxs-lookup"><span data-stu-id="cd533-167">Select **Devices** and then select and click the device you want to update from the list of devices connected to this service.</span></span> <span data-ttu-id="cd533-168">In de **instellingen** blade, gaat u naar **beheren** sectie en selecteer **apparaatupdates**.</span><span class="sxs-lookup"><span data-stu-id="cd533-168">In the **Settings** blade, go to **Manage** section and select **Device updates**.</span></span> <span data-ttu-id="cd533-169">De weergegeven software-versie moet **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="cd533-169">The displayed software version should be **10.0.10288.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cd533-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cd533-170">Next steps</span></span>

<span data-ttu-id="cd533-171">Meer informatie over [beheer van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="cd533-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

