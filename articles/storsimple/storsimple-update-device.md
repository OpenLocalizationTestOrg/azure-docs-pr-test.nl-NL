---
title: aaaUpdate uw StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe toouse hello StorSimple functie tooinstall reguliere en onderhoud modus updates en hotfixes bijwerken.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="fe23f-103">Uw StorSimple 8000-serie-apparaat bijwerken</span><span class="sxs-lookup"><span data-stu-id="fe23f-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="fe23f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="fe23f-104">Overview</span></span>
<span data-ttu-id="fe23f-105">Hallo StorSimple updates functies kunt u de tooeasily uw StorSimple-apparaat up-to-date houden.</span><span class="sxs-lookup"><span data-stu-id="fe23f-105">hello StorSimple updates features allow you tooeasily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="fe23f-106">Afhankelijk van het type update hello, kunt u updates toohello apparaat via Hallo klassieke Azure-portal of via Windows PowerShell-interface Hallo toepassen.</span><span class="sxs-lookup"><span data-stu-id="fe23f-106">Depending on hello update type, you can apply updates toohello device via hello Azure classic portal or via hello Windows PowerShell interface.</span></span> <span data-ttu-id="fe23f-107">Deze zelfstudie wordt de update-typen Hallo beschreven en hoe tooinstall hiervan.</span><span class="sxs-lookup"><span data-stu-id="fe23f-107">This tutorial describes hello update types and how tooinstall each of them.</span></span>

<span data-ttu-id="fe23f-108">U kunt twee soorten apparaatupdates toepassen:</span><span class="sxs-lookup"><span data-stu-id="fe23f-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="fe23f-109">Reguliere (of de normale modus) updates</span><span class="sxs-lookup"><span data-stu-id="fe23f-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="fe23f-110">Onderhoud modus updates</span><span class="sxs-lookup"><span data-stu-id="fe23f-110">Maintenance mode updates</span></span>

<span data-ttu-id="fe23f-111">U kunt ook regelmatige updates via de klassieke Azure-portal Hallo of Windows PowerShell; installeren echter, moet u Windows PowerShell tooinstall onderhoud modus updates.</span><span class="sxs-lookup"><span data-stu-id="fe23f-111">You can install regular updates via hello Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell tooinstall Maintenance mode updates.</span></span> 

<span data-ttu-id="fe23f-112">Elk updatetype wordt afzonderlijk hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="fe23f-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="fe23f-113">Regelmatig updates</span><span class="sxs-lookup"><span data-stu-id="fe23f-113">Regular updates</span></span>
<span data-ttu-id="fe23f-114">Regelmatig updates zijn ononderbroken updates die kunnen worden geïnstalleerd wanneer het Hallo-apparaat is in de normale modus.</span><span class="sxs-lookup"><span data-stu-id="fe23f-114">Regular updates are non-disruptive updates that can be installed when hello device is in Normal mode.</span></span> <span data-ttu-id="fe23f-115">Deze updates worden toegepast via Hallo Microsoft Update-website tooeach apparaat controller.</span><span class="sxs-lookup"><span data-stu-id="fe23f-115">These updates are applied through hello Microsoft Update website tooeach device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fe23f-116">Een failover van de domeincontroller kan optreden tijdens het updateproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="fe23f-116">A controller failover may occur during hello update process.</span></span> <span data-ttu-id="fe23f-117">Dit wordt echter niet gewijzigd beschikbaarheid van het systeem of de bewerking.</span><span class="sxs-lookup"><span data-stu-id="fe23f-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="fe23f-118">Zie voor informatie over hoe tooinstall regelmatige updates via Hallo klassieke Azure-portal, [installeren regelmatig updates via de klassieke Azure-portal Hallo](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="fe23f-118">For details on how tooinstall regular updates via hello Azure classic portal, see [Install regular updates via hello Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="fe23f-119">U kunt ook regelmatige updates via Windows PowerShell voor StorSimple installeren.</span><span class="sxs-lookup"><span data-stu-id="fe23f-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="fe23f-120">Zie voor meer informatie [regelmatig updates via Windows PowerShell voor StorSimple installeren](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="fe23f-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="fe23f-121">Onderhoud modus updates</span><span class="sxs-lookup"><span data-stu-id="fe23f-121">Maintenance mode updates</span></span>
<span data-ttu-id="fe23f-122">Onderhoud modus updates zijn verstoren updates zoals upgrades van de schijf.</span><span class="sxs-lookup"><span data-stu-id="fe23f-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="fe23f-123">Deze updates vereisen Hallo apparaat toobe in onderhoudsmodus geplaatst.</span><span class="sxs-lookup"><span data-stu-id="fe23f-123">These updates require hello device toobe put into Maintenance mode.</span></span> <span data-ttu-id="fe23f-124">Zie voor meer informatie [stap 2: Voer onderhoudsmodus](#step2).</span><span class="sxs-lookup"><span data-stu-id="fe23f-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="fe23f-125">U kunt hello Azure classic portal tooinstall onderhoud modus updates niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fe23f-125">You cannot use hello Azure classic portal tooinstall Maintenance mode updates.</span></span> <span data-ttu-id="fe23f-126">In plaats daarvan moet u Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="fe23f-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="fe23f-127">Zie voor informatie over de manier waarop de onderhoudsmodus tooinstall wordt bijgewerkt, [installeren onderhoud modus updates via Windows PowerShell voor StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="fe23f-127">For details on how tooinstall Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe23f-128">Onderhoudsmodus updates moet afzonderlijk tooeach domeincontroller toegepast.</span><span class="sxs-lookup"><span data-stu-id="fe23f-128">Maintenance mode updates must be applied separately tooeach controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a><span data-ttu-id="fe23f-129">Regelmatig updates via Hallo klassieke Azure-portal installeren</span><span class="sxs-lookup"><span data-stu-id="fe23f-129">Install regular updates via hello Azure classic portal</span></span>
<span data-ttu-id="fe23f-130">U kunt hello Azure classic portal tooapply updates tooyour StorSimple-apparaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fe23f-130">You can use hello Azure classic portal tooapply updates tooyour StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="fe23f-131">Installeer regelmatig updates via Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="fe23f-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="fe23f-132">U kunt ook Windows PowerShell voor StorSimple tooapply regular (normale modus)-updates.</span><span class="sxs-lookup"><span data-stu-id="fe23f-132">Alternatively, you can use Windows PowerShell for StorSimple tooapply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe23f-133">Hoewel u regelmatig updates met Windows PowerShell voor StorSimple installeren kunt, wordt aangeraden dat u regelmatig updates via Hallo klassieke Azure-portal installeert.</span><span class="sxs-lookup"><span data-stu-id="fe23f-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through hello Azure classic portal.</span></span> <span data-ttu-id="fe23f-134">Vanaf Update 1, zijn eerste controles uitgevoerd voorafgaande tooinstalling updates van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="fe23f-134">Beginning with Update 1, pre-checks will be performed prior tooinstalling updates from hello portal.</span></span> <span data-ttu-id="fe23f-135">Deze controles vooraf wordt hebben voorrang op fouten en zorg ervoor dat een soepeler ervaring.</span><span class="sxs-lookup"><span data-stu-id="fe23f-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="fe23f-136">Onderhoud modus updates via Windows PowerShell voor StorSimple installeren</span><span class="sxs-lookup"><span data-stu-id="fe23f-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="fe23f-137">U Windows PowerShell voor StorSimple tooapply onderhoud modus updates tooyour StorSimple-apparaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fe23f-137">You use Windows PowerShell for StorSimple tooapply Maintenance mode updates tooyour StorSimple device.</span></span> <span data-ttu-id="fe23f-138">Alle i/o-aanvragen zijn in deze modus onderbroken.</span><span class="sxs-lookup"><span data-stu-id="fe23f-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="fe23f-139">Services zoals niet-vluchtige RAM-geheugen (NVRAM) of de clusteringservice Hallo zijn ook gestopt.</span><span class="sxs-lookup"><span data-stu-id="fe23f-139">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="fe23f-140">Beide domeincontrollers worden opgestart wanneer u in of uit deze modus.</span><span class="sxs-lookup"><span data-stu-id="fe23f-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="fe23f-141">Wanneer u deze modus afsluit, worden alle Hallo-services wordt hervat en moeten in orde.</span><span class="sxs-lookup"><span data-stu-id="fe23f-141">When you exit this mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="fe23f-142">(Dit kan enkele minuten duren.)</span><span class="sxs-lookup"><span data-stu-id="fe23f-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="fe23f-143">Als u tooapply onderhoud modus updates nodig hebt, ontvangt u een waarschuwing via Hallo klassieke Azure-portal of er updates die moeten worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="fe23f-143">If you need tooapply Maintenance mode updates, you will receive an alert through hello Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="fe23f-144">Deze waarschuwing bevat instructies voor het gebruik van Windows PowerShell voor StorSimple tooinstall Hallo-updates.</span><span class="sxs-lookup"><span data-stu-id="fe23f-144">This alert will include instructions for using Windows PowerShell for StorSimple tooinstall hello updates.</span></span> <span data-ttu-id="fe23f-145">Nadat u uw apparaat bijwerkt, Hallo gebruik dezelfde procedure toochange Hallo apparaat tooRegular modus.</span><span class="sxs-lookup"><span data-stu-id="fe23f-145">After you update your device, use hello same procedure toochange hello device tooRegular mode.</span></span> <span data-ttu-id="fe23f-146">Zie voor stapsgewijze instructies [stap 4: afsluiten onderhoudsmodus](#step4).</span><span class="sxs-lookup"><span data-stu-id="fe23f-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="fe23f-147">Controleer of beide apparaatcontrollers zijn in orde door Hallo controleren voordat u de onderhoudsmodus invoert, **hardwarestatus** op Hallo **onderhoud** pagina in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fe23f-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="fe23f-148">Hallo-controller is niet in orde, contact op met Microsoft Support voor de volgende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="fe23f-148">If hello controller is not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="fe23f-149">Ga voor meer informatie tooContact Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="fe23f-149">For more information, go tooContact Microsoft Support.</span></span> 
> * <span data-ttu-id="fe23f-150">Wanneer u in de onderhoudsmodus bevindt bent, moet u tooapply Hallo update eerst op een domeincontroller en klik vervolgens op Hallo andere domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="fe23f-150">When you are in Maintenance mode, you need tooapply hello update first on one controller and then on hello other controller.</span></span>
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a><span data-ttu-id="fe23f-151">Stap 1: Verbinding maken met de seriële console toohello<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="fe23f-151">Step 1: Connect toohello serial console <a name="step1"></span></span>
<span data-ttu-id="fe23f-152">Eerst gebruik van een toepassing, zoals PuTTY tooaccess Hallo seriële console.</span><span class="sxs-lookup"><span data-stu-id="fe23f-152">First, use an application such as PuTTY tooaccess hello serial console.</span></span> <span data-ttu-id="fe23f-153">Hallo volgende procedure wordt uitgelegd hoe toouse PuTTY tooconnect toohello seriële console.</span><span class="sxs-lookup"><span data-stu-id="fe23f-153">hello following procedure explains how toouse PuTTY tooconnect toohello serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="fe23f-154">Stap 2: Geef de onderhoudsmodus<a name="step2"></span><span class="sxs-lookup"><span data-stu-id="fe23f-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="fe23f-155">Nadat u toohello console verbinding maakt, bepalen of er updates tooinstall en onderhoud modus tooinstall Voer ze.</span><span class="sxs-lookup"><span data-stu-id="fe23f-155">After you connect toohello console, determine whether there are updates tooinstall, and enter Maintenance mode tooinstall them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="fe23f-156">Stap 3: Uw updates installeren<a name="step3"></span><span class="sxs-lookup"><span data-stu-id="fe23f-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="fe23f-157">Vervolgens installeert u de updates.</span><span class="sxs-lookup"><span data-stu-id="fe23f-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="fe23f-158">Stap 4: Afsluiten onderhoudsmodus<a name="step4"></span><span class="sxs-lookup"><span data-stu-id="fe23f-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="fe23f-159">Onderhoudsmodus ten slotte af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="fe23f-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="fe23f-160">Installeren van hotfixes via Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="fe23f-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="fe23f-161">In tegenstelling tot de updates voor Microsoft Azure StorSimple zijn-hotfixes geïnstalleerd vanuit een gedeelde map.</span><span class="sxs-lookup"><span data-stu-id="fe23f-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="fe23f-162">Net als bij updates, zijn er twee soorten hotfixes:</span><span class="sxs-lookup"><span data-stu-id="fe23f-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="fe23f-163">Reguliere hotfixes</span><span class="sxs-lookup"><span data-stu-id="fe23f-163">Regular hotfixes</span></span> 
* <span data-ttu-id="fe23f-164">Onderhoud modus hotfixes</span><span class="sxs-lookup"><span data-stu-id="fe23f-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="fe23f-165">Hallo volgende procedures wordt uitgelegd hoe toouse Windows PowerShell voor StorSimple tooinstall reguliere en hotfixes voor onderhoud-modus.</span><span class="sxs-lookup"><span data-stu-id="fe23f-165">hello following procedures explain how toouse Windows PowerShell for StorSimple tooinstall regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a><span data-ttu-id="fe23f-166">Wat gebeurt er tooupdates als u een fabriek voeren opnieuw instellen van Hallo apparaat?</span><span class="sxs-lookup"><span data-stu-id="fe23f-166">What happens tooupdates if you perform a factory reset of hello device?</span></span>
<span data-ttu-id="fe23f-167">Als een apparaat opnieuw instellen van toofactory instellingen, zijn alle Hallo updates gaan verloren.</span><span class="sxs-lookup"><span data-stu-id="fe23f-167">If a device is reset toofactory settings, then all hello updates are lost.</span></span> <span data-ttu-id="fe23f-168">Nadat de Hallo fabrieksinstellingen apparaat is geregistreerd en geconfigureerd, moet u updates van de toomanually installeren via de klassieke Azure-portal Hallo en/of Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="fe23f-168">After hello factory-reset device is registered and configured, you will need toomanually install updates through hello Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="fe23f-169">Zie voor meer informatie over de fabrieksinstellingen [Hallo apparaat toofactory standaardinstellingen herstellen](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="fe23f-169">For more information about factory reset, see [Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe23f-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fe23f-170">Next steps</span></span>
* <span data-ttu-id="fe23f-171">Meer informatie over [met Windows PowerShell voor StorSimple tooadminister uw StorSimple-apparaat](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="fe23f-171">Learn more about [using Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="fe23f-172">Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="fe23f-172">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

