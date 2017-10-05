---
title: Uw StorSimple-apparaat bijwerken | Microsoft Docs
description: Wordt uitgelegd hoe u met de functie StorSimple update regular en onderhoud modus updates en hotfixes installeren.
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
ms.openlocfilehash: 8490110942741b049b6d44ac93697303cef40e8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="614a0-103">Uw StorSimple 8000-serie-apparaat bijwerken</span><span class="sxs-lookup"><span data-stu-id="614a0-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="614a0-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="614a0-104">Overview</span></span>
<span data-ttu-id="614a0-105">De StorSimple-updates-functies kunt u eenvoudig uw StorSimple-apparaat om up-to-date te houden.</span><span class="sxs-lookup"><span data-stu-id="614a0-105">The StorSimple updates features allow you to easily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="614a0-106">Afhankelijk van het updatetype kunt u updates toepassen op het apparaat via de klassieke Azure portal of via de Windows PowerShell-interface.</span><span class="sxs-lookup"><span data-stu-id="614a0-106">Depending on the update type, you can apply updates to the device via the Azure classic portal or via the Windows PowerShell interface.</span></span> <span data-ttu-id="614a0-107">Deze zelfstudie wordt de update-typen en het installeren van elk van deze beschreven.</span><span class="sxs-lookup"><span data-stu-id="614a0-107">This tutorial describes the update types and how to install each of them.</span></span>

<span data-ttu-id="614a0-108">U kunt twee soorten apparaatupdates toepassen:</span><span class="sxs-lookup"><span data-stu-id="614a0-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="614a0-109">Reguliere (of de normale modus) updates</span><span class="sxs-lookup"><span data-stu-id="614a0-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="614a0-110">Onderhoud modus updates</span><span class="sxs-lookup"><span data-stu-id="614a0-110">Maintenance mode updates</span></span>

<span data-ttu-id="614a0-111">U kunt ook regelmatige updates via de klassieke Azure-portal of de Windows PowerShell; installeren u moet Windows PowerShell echter gebruiken om onderhoud modus updates te installeren.</span><span class="sxs-lookup"><span data-stu-id="614a0-111">You can install regular updates via the Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell to install Maintenance mode updates.</span></span> 

<span data-ttu-id="614a0-112">Elk updatetype wordt afzonderlijk hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="614a0-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="614a0-113">Regelmatig updates</span><span class="sxs-lookup"><span data-stu-id="614a0-113">Regular updates</span></span>
<span data-ttu-id="614a0-114">Regelmatig updates zijn ononderbroken updates die kunnen worden geïnstalleerd wanneer het apparaat zich in de normale modus.</span><span class="sxs-lookup"><span data-stu-id="614a0-114">Regular updates are non-disruptive updates that can be installed when the device is in Normal mode.</span></span> <span data-ttu-id="614a0-115">Deze updates worden toegepast via de website Microsoft Update op elke domeincontroller apparaat.</span><span class="sxs-lookup"><span data-stu-id="614a0-115">These updates are applied through the Microsoft Update website to each device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="614a0-116">Een failover van de domeincontroller kan optreden tijdens het updateproces.</span><span class="sxs-lookup"><span data-stu-id="614a0-116">A controller failover may occur during the update process.</span></span> <span data-ttu-id="614a0-117">Dit wordt echter niet gewijzigd beschikbaarheid van het systeem of de bewerking.</span><span class="sxs-lookup"><span data-stu-id="614a0-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="614a0-118">Zie voor meer informatie over het installeren van regelmatige updates via de klassieke Azure portal [regelmatig updates via de klassieke Azure-portal installeren](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="614a0-118">For details on how to install regular updates via the Azure classic portal, see [Install regular updates via the Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="614a0-119">U kunt ook regelmatige updates via Windows PowerShell voor StorSimple installeren.</span><span class="sxs-lookup"><span data-stu-id="614a0-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="614a0-120">Zie voor meer informatie [regelmatig updates via Windows PowerShell voor StorSimple installeren](#install-regular-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="614a0-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="614a0-121">Onderhoud modus updates</span><span class="sxs-lookup"><span data-stu-id="614a0-121">Maintenance mode updates</span></span>
<span data-ttu-id="614a0-122">Onderhoud modus updates zijn verstoren updates zoals upgrades van de schijf.</span><span class="sxs-lookup"><span data-stu-id="614a0-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="614a0-123">Deze updates vereisen dat het apparaat in de onderhoudsmodus moet worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="614a0-123">These updates require the device to be put into Maintenance mode.</span></span> <span data-ttu-id="614a0-124">Zie voor meer informatie [stap 2: Voer onderhoudsmodus](#step2).</span><span class="sxs-lookup"><span data-stu-id="614a0-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="614a0-125">U kunt de klassieke Azure portal niet gebruiken om onderhoud modus updates te installeren.</span><span class="sxs-lookup"><span data-stu-id="614a0-125">You cannot use the Azure classic portal to install Maintenance mode updates.</span></span> <span data-ttu-id="614a0-126">In plaats daarvan moet u Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="614a0-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="614a0-127">Zie voor meer informatie over het installeren van updates voor onderhoud modus [installeren onderhoud modus updates via Windows PowerShell voor StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="614a0-127">For details on how to install Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="614a0-128">Onderhoud modus updates moeten afzonderlijk worden toegepast op elke domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="614a0-128">Maintenance mode updates must be applied separately to each controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-the-azure-classic-portal"></a><span data-ttu-id="614a0-129">Regelmatig updates via de klassieke Azure-portal installeren</span><span class="sxs-lookup"><span data-stu-id="614a0-129">Install regular updates via the Azure classic portal</span></span>
<span data-ttu-id="614a0-130">Updates toepassen op uw StorSimple-apparaat kunt u de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="614a0-130">You can use the Azure classic portal to apply updates to your StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="614a0-131">Installeer regelmatig updates via Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="614a0-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="614a0-132">U kunt ook Windows PowerShell voor StorSimple regular (normale modus)-updates toe te passen.</span><span class="sxs-lookup"><span data-stu-id="614a0-132">Alternatively, you can use Windows PowerShell for StorSimple to apply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="614a0-133">Hoewel u regelmatig updates met Windows PowerShell voor StorSimple installeren kunt, wordt aangeraden dat u regelmatig updates via de klassieke Azure portal installeert.</span><span class="sxs-lookup"><span data-stu-id="614a0-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through the Azure classic portal.</span></span> <span data-ttu-id="614a0-134">Vanaf Update 1, worden eerste controles uitgevoerd voordat u updates installeert vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="614a0-134">Beginning with Update 1, pre-checks will be performed prior to installing updates from the portal.</span></span> <span data-ttu-id="614a0-135">Deze controles vooraf wordt hebben voorrang op fouten en zorg ervoor dat een soepeler ervaring.</span><span class="sxs-lookup"><span data-stu-id="614a0-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="614a0-136">Onderhoud modus updates via Windows PowerShell voor StorSimple installeren</span><span class="sxs-lookup"><span data-stu-id="614a0-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="614a0-137">U kunt Windows PowerShell voor StorSimple gebruiken onderhoud modus updates toepassen op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="614a0-137">You use Windows PowerShell for StorSimple to apply Maintenance mode updates to your StorSimple device.</span></span> <span data-ttu-id="614a0-138">Alle i/o-aanvragen zijn in deze modus onderbroken.</span><span class="sxs-lookup"><span data-stu-id="614a0-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="614a0-139">Services zoals niet-vluchtige RAM-geheugen (NVRAM) of de clusteringservice ook worden gestopt.</span><span class="sxs-lookup"><span data-stu-id="614a0-139">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="614a0-140">Beide domeincontrollers worden opgestart wanneer u in of uit deze modus.</span><span class="sxs-lookup"><span data-stu-id="614a0-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="614a0-141">Wanneer u deze modus afsluit, worden alle services wordt hervat en moeten in orde.</span><span class="sxs-lookup"><span data-stu-id="614a0-141">When you exit this mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="614a0-142">(Dit kan enkele minuten duren.)</span><span class="sxs-lookup"><span data-stu-id="614a0-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="614a0-143">Als u onderhoud modus updates toe te passen wilt, ontvangt u een waarschuwing via de klassieke Azure portal dat er updates die moeten worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="614a0-143">If you need to apply Maintenance mode updates, you will receive an alert through the Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="614a0-144">Deze waarschuwing bevat instructies voor het gebruik van Windows PowerShell voor StorSimple om de updates te installeren.</span><span class="sxs-lookup"><span data-stu-id="614a0-144">This alert will include instructions for using Windows PowerShell for StorSimple to install the updates.</span></span> <span data-ttu-id="614a0-145">Nadat u uw apparaat bijwerkt, gebruikt u dezelfde procedure om te wijzigen van het apparaat naar de normale modus.</span><span class="sxs-lookup"><span data-stu-id="614a0-145">After you update your device, use the same procedure to change the device to Regular mode.</span></span> <span data-ttu-id="614a0-146">Zie voor stapsgewijze instructies [stap 4: afsluiten onderhoudsmodus](#step4).</span><span class="sxs-lookup"><span data-stu-id="614a0-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="614a0-147">Controleer of beide apparaatcontrollers zijn in orde door te controleren voordat u de onderhoudsmodus invoert, de **hardwarestatus** op de **onderhoud** pagina in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="614a0-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="614a0-148">Als de domeincontroller niet in orde is, moet u contact op met Microsoft Support voor de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="614a0-148">If the controller is not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="614a0-149">Ga voor meer informatie naar contact opnemen met Microsoft ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="614a0-149">For more information, go to Contact Microsoft Support.</span></span> 
> * <span data-ttu-id="614a0-150">Wanneer u in de onderhoudsmodus bevindt bent, moet u eerst de update toepassen op een domeincontroller en klik vervolgens op de andere controller.</span><span class="sxs-lookup"><span data-stu-id="614a0-150">When you are in Maintenance mode, you need to apply the update first on one controller and then on the other controller.</span></span>
> 
> 

### <a name="step-1-connect-to-the-serial-console-a-namestep1"></a><span data-ttu-id="614a0-151">Stap 1: Verbinding maken met de seriële console<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="614a0-151">Step 1: Connect to the serial console <a name="step1"></span></span>
<span data-ttu-id="614a0-152">Eerst een toepassing zoals PuTTY gebruiken voor toegang tot de seriële console.</span><span class="sxs-lookup"><span data-stu-id="614a0-152">First, use an application such as PuTTY to access the serial console.</span></span> <span data-ttu-id="614a0-153">De volgende procedure wordt uitgelegd hoe u met PuTTY verbinding maken met de seriële console.</span><span class="sxs-lookup"><span data-stu-id="614a0-153">The following procedure explains how to use PuTTY to connect to the serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="614a0-154">Stap 2: Geef de onderhoudsmodus<a name="step2"></span><span class="sxs-lookup"><span data-stu-id="614a0-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="614a0-155">Nadat u verbinding met de console, moet u bepalen of er updates voor het installeren en voer de onderhoudsmodus voor de installatie van deze zijn.</span><span class="sxs-lookup"><span data-stu-id="614a0-155">After you connect to the console, determine whether there are updates to install, and enter Maintenance mode to install them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="614a0-156">Stap 3: Uw updates installeren<a name="step3"></span><span class="sxs-lookup"><span data-stu-id="614a0-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="614a0-157">Vervolgens installeert u de updates.</span><span class="sxs-lookup"><span data-stu-id="614a0-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="614a0-158">Stap 4: Afsluiten onderhoudsmodus<a name="step4"></span><span class="sxs-lookup"><span data-stu-id="614a0-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="614a0-159">Onderhoudsmodus ten slotte af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="614a0-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="614a0-160">Installeren van hotfixes via Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="614a0-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="614a0-161">In tegenstelling tot de updates voor Microsoft Azure StorSimple zijn-hotfixes geïnstalleerd vanuit een gedeelde map.</span><span class="sxs-lookup"><span data-stu-id="614a0-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="614a0-162">Net als bij updates, zijn er twee soorten hotfixes:</span><span class="sxs-lookup"><span data-stu-id="614a0-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="614a0-163">Reguliere hotfixes</span><span class="sxs-lookup"><span data-stu-id="614a0-163">Regular hotfixes</span></span> 
* <span data-ttu-id="614a0-164">Onderhoud modus hotfixes</span><span class="sxs-lookup"><span data-stu-id="614a0-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="614a0-165">De volgende procedures wordt uitgelegd hoe u Windows PowerShell voor StorSimple gebruikt regular en onderhoud modus hotfixes installeren.</span><span class="sxs-lookup"><span data-stu-id="614a0-165">The following procedures explain how to use Windows PowerShell for StorSimple to install regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-to-updates-if-you-perform-a-factory-reset-of-the-device"></a><span data-ttu-id="614a0-166">Wat gebeurt er met updates als u de fabrieksinstellingen van het apparaat uitvoeren?</span><span class="sxs-lookup"><span data-stu-id="614a0-166">What happens to updates if you perform a factory reset of the device?</span></span>
<span data-ttu-id="614a0-167">Als een apparaat is standaardinstellingen herstellen, zijn alle updates gaan verloren.</span><span class="sxs-lookup"><span data-stu-id="614a0-167">If a device is reset to factory settings, then all the updates are lost.</span></span> <span data-ttu-id="614a0-168">Nadat het apparaat de fabrieksinstellingen is geregistreerd en geconfigureerd, moet u handmatig installeren van updates via de klassieke Azure-portal en/of de Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="614a0-168">After the factory-reset device is registered and configured, you will need to manually install updates through the Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="614a0-169">Zie voor meer informatie over de fabrieksinstellingen [opnieuw instellen van het apparaat fabrieksinstellingen](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="614a0-169">For more information about factory reset, see [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="614a0-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="614a0-170">Next steps</span></span>
* <span data-ttu-id="614a0-171">Meer informatie over [Windows PowerShell voor StorSimple gebruiken voor het beheer van uw StorSimple-apparaat](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="614a0-171">Learn more about [using Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="614a0-172">Meer informatie over [de StorSimple Manager-service gebruiken voor het beheer van uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="614a0-172">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

