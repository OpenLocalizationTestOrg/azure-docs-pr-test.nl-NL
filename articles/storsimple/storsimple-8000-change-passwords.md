---
title: aaaChange uw StorSimple-wachtwoorden | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Hallo StorSimple Apparaatbeheer service toochange uw administrator-wachtwoord StorSimple Snapshot Manager en het apparaat.
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="a65cc-103">Hallo Apparaatbeheer StorSimple-service toochange uw StorSimple-wachtwoorden gebruiken</span><span class="sxs-lookup"><span data-stu-id="a65cc-103">Use hello StorSimple Device Manager service toochange your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="a65cc-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="a65cc-104">Overview</span></span>
<span data-ttu-id="a65cc-105">Azure-portal Hallo **apparaatinstellingen** optie bevat alle parameters van de Hallo apparaat die u kunt opnieuw configureren op een StorSimple-apparaat dat wordt beheerd door een StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="a65cc-105">hello Azure portal **Device settings** option contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="a65cc-106">Deze zelfstudie wordt uitgelegd hoe u kunt Hallo **beveiliging** onder de optie **apparaatinstellingen** toochange de apparaatbeheerder van uw of het wachtwoord voor StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="a65cc-106">This tutorial explains how you can use hello **Security** option under **Device settings** toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="a65cc-107">Wachtwoord apparaatbeheerder Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="a65cc-107">Change hello device administrator password</span></span>
<span data-ttu-id="a65cc-108">Wanneer u Windows PowerShell-interface tooaccess hello StorSimple-apparaat gebruikt, bent u vereiste tooenter het beheerderswachtwoord voor een apparaat.</span><span class="sxs-lookup"><span data-stu-id="a65cc-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="a65cc-109">Wanneer Hallo eerste StorSimple-apparaat is geregistreerd bij een service, is het standaardwachtwoord Hallo voor deze interface *Wachtwoord1*.</span><span class="sxs-lookup"><span data-stu-id="a65cc-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="a65cc-110">Voor Hallo beveiliging van uw gegevens, zijn de vereiste toochange dit wachtwoord op Hallo einde van het registratieproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="a65cc-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="a65cc-111">U kunt niet afsluiten van het registratieproces Hallo zonder dat u dit wachtwoord wijzigt.</span><span class="sxs-lookup"><span data-stu-id="a65cc-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="a65cc-112">Zie voor meer informatie [stap 3: apparaat configureren en registreren Hallo via Windows PowerShell voor StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="a65cc-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="a65cc-113">Hallo-wachtwoord dat eerst via de Windows PowerShell-interface Hallo is ingesteld tijdens de registratie kan later worden gewijzigd via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a65cc-113">hello password that was first set through hello Windows PowerShell interface during registration can be changed later via hello Azure portal.</span></span> <span data-ttu-id="a65cc-114">Hallo te volgen stappen toochange Hallo wachtwoord apparaatbeheerder uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a65cc-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="a65cc-115">wachtwoord apparaatbeheerder hello toochange</span><span class="sxs-lookup"><span data-stu-id="a65cc-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="a65cc-116">Ga tooyour Apparaatbeheer StorSimple-service en klik op **apparaten**.</span><span class="sxs-lookup"><span data-stu-id="a65cc-116">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="a65cc-117">Selecteer uit Hallo in tabelvorm aanbieding van apparaten, en op Hallo apparaat waarvan het wachtwoord u van plan bent toochange.</span><span class="sxs-lookup"><span data-stu-id="a65cc-117">From hello tabular listing of devices, select and click hello device whose password you intend toochange.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="a65cc-118">In Hallo **instellingen** blade te gaan**apparaatinstellingen > beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="a65cc-118">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="a65cc-119">In Hallo **beveiligingsinstellingen** blade, klikt u op **wachtwoord** toochange Hallo apparaat administrator-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a65cc-119">In hello **Security settings** blade, click **Password** toochange hello device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="a65cc-120">In Hallo **wachtwoord** blade bieden een administrator-wachtwoord van 8 too15 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="a65cc-120">In hello **Password** blade, provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="a65cc-121">Hallo-wachtwoord moet een combinatie van 3 of meer van hoofdletters, kleine letters, numerieke en speciale tekens.</span><span class="sxs-lookup"><span data-stu-id="a65cc-121">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="a65cc-122">Hallo wachtwoord bevestigen.</span><span class="sxs-lookup"><span data-stu-id="a65cc-122">Confirm hello password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="a65cc-123">Klik op **opslaan** wanneer u om bevestiging gevraagd, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="a65cc-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="a65cc-124">wachtwoord apparaatbeheerder Hallo moet nu worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="a65cc-124">hello device administrator password should now be updated.</span></span> <span data-ttu-id="a65cc-125">U kunt deze gewijzigde wachtwoord tooaccess Hallo Windows PowerShell-interface gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a65cc-125">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="set-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="a65cc-126">Hallo StorSimple Snapshot Manager-wachtwoord instellen</span><span class="sxs-lookup"><span data-stu-id="a65cc-126">Set hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="a65cc-127">StorSimple Snapshot Manager-software bevindt zich op uw Windows-host en kan beheerders toomanage back-ups van uw StorSimple-apparaat in Hallo vorm van lokale en cloudmomentopnamen.</span><span class="sxs-lookup"><span data-stu-id="a65cc-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="a65cc-128">Wanneer u een apparaat in StorSimple Snapshot Manager configureert, wordt u gevraagd tooprovide Hallo apparaat IP-adres en het wachtwoord tooauthenticate uw opslagapparaat.</span><span class="sxs-lookup"><span data-stu-id="a65cc-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span>

<span data-ttu-id="a65cc-129">U kunt instellen of wijzigen van Hallo wachtwoord voor StorSimple Snapshot Manager via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a65cc-129">You can set or change hello password for StorSimple Snapshot Manager via hello Azure portal.</span></span> <span data-ttu-id="a65cc-130">Volgende stappen tooset Hallo uitvoeren of Hallo StorSimple Snapshot Manager wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a65cc-130">Perform hello following steps tooset or change hello StorSimple Snapshot Manager password.</span></span>

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="a65cc-131">tooset hello StorSimple Snapshot Manager-wachtwoord</span><span class="sxs-lookup"><span data-stu-id="a65cc-131">tooset hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="a65cc-132">Ga tooyour Apparaatbeheer StorSimple-service en klik op **apparaten**.</span><span class="sxs-lookup"><span data-stu-id="a65cc-132">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="a65cc-133">Selecteer uit Hallo in tabelvorm aanbieding van apparaten, en klik op Hallo apparaat waarvan wachtwoord StorSimple Snapshot Manager u van plan bent tooset of wijzigt.</span><span class="sxs-lookup"><span data-stu-id="a65cc-133">From hello tabular listing of devices, select and click hello device whose StorSimple Snapshot Manager password you intend tooset or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="a65cc-134">In Hallo **instellingen** blade te gaan**apparaatinstellingen > beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="a65cc-134">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="a65cc-135">In Hallo **beveiligingsinstellingen** blade, klikt u op **wachtwoord** tooset of wijzig Hallo wachtwoord StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="a65cc-135">In hello **Security settings** blade, click **Password** tooset or change hello StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="a65cc-136">In Hallo **wachtwoord** blade, voer een wachtwoord 14 of 15 tekens.</span><span class="sxs-lookup"><span data-stu-id="a65cc-136">In hello **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="a65cc-137">Zorg ervoor dat wachtwoord Hallo een combinatie van 3 of meer van hoofdletters, kleine letters, numerieke en speciale tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="a65cc-137">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="a65cc-138">Hallo wachtwoord bevestigen.</span><span class="sxs-lookup"><span data-stu-id="a65cc-138">Confirm hello password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="a65cc-139">Klik op **opslaan** wanneer u om bevestiging gevraagd, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="a65cc-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="a65cc-140">wachtwoord voor StorSimple Snapshot Manager Hallo moet nu worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="a65cc-140">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a65cc-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a65cc-141">Next steps</span></span>
* <span data-ttu-id="a65cc-142">Meer informatie over [StorSimple security](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="a65cc-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="a65cc-143">Meer informatie over [wijzigen van de configuratie van uw apparaat](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="a65cc-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="a65cc-144">Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a65cc-144">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

