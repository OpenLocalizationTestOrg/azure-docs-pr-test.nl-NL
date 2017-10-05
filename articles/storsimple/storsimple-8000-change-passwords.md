---
title: Uw StorSimple-wachtwoorden wijzigen | Microsoft Docs
description: Beschrijft hoe de Apparaatbeheer StorSimple-service gebruiken om uw StorSimple Snapshot Manager en apparaat administrator-wachtwoord wijzigen.
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
ms.openlocfilehash: 7762f8499c67672f0a2ffed99e98baea4c940fa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-change-your-storsimple-passwords"></a><span data-ttu-id="ae489-103">De service StorSimple Apparaatbeheer gebruiken om uw StorSimple-wachtwoorden wijzigen</span><span class="sxs-lookup"><span data-stu-id="ae489-103">Use the StorSimple Device Manager service to change your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="ae489-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ae489-104">Overview</span></span>
<span data-ttu-id="ae489-105">De Azure-portal **apparaatinstellingen** optie bevat alle apparaatparameters die u kunt opnieuw configureren op een StorSimple-apparaat dat wordt beheerd door een StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="ae489-105">The Azure portal **Device settings** option contains all the device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="ae489-106">Deze zelfstudie wordt uitgelegd hoe u kunt de **beveiliging** onder de optie **apparaatinstellingen** om de apparaatbeheerder van uw of StorSimple Snapshot Manager-wachtwoord te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ae489-106">This tutorial explains how you can use the **Security** option under **Device settings** to change your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-the-device-administrator-password"></a><span data-ttu-id="ae489-107">Het beheerderswachtwoord voor het apparaat wijzigen</span><span class="sxs-lookup"><span data-stu-id="ae489-107">Change the device administrator password</span></span>
<span data-ttu-id="ae489-108">Wanneer u Windows PowerShell-interface gebruiken voor toegang tot het StorSimple-apparaat, hoeft u een apparaat administrator-wachtwoord moeten invoeren.</span><span class="sxs-lookup"><span data-stu-id="ae489-108">When you use Windows PowerShell interface to access the StorSimple device, you are required to enter a device administrator password.</span></span> <span data-ttu-id="ae489-109">Als de eerste StorSimple-apparaat is geregistreerd met een service, wordt het standaardwachtwoord voor deze interface is *Wachtwoord1*.</span><span class="sxs-lookup"><span data-stu-id="ae489-109">When the first StorSimple device is registered with a service, the default password for this interface is *Password1*.</span></span> <span data-ttu-id="ae489-110">Voor de beveiliging van uw gegevens moet u dit wachtwoord aan het einde van het registratieproces wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ae489-110">For the security of your data, you are required to change this password at the end of the registration process.</span></span> <span data-ttu-id="ae489-111">U kunt niet afsluiten van het registratieproces zonder dat u dit wachtwoord wijzigt.</span><span class="sxs-lookup"><span data-stu-id="ae489-111">You cannot exit from the registration process without changing this password.</span></span> <span data-ttu-id="ae489-112">Zie voor meer informatie [stap 3: configureren en registreren van het apparaat via Windows PowerShell voor StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="ae489-112">For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="ae489-113">Het wachtwoord dat u eerst via de Windows PowerShell-interface is ingesteld tijdens de registratie kan later worden gewijzigd via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ae489-113">The password that was first set through the Windows PowerShell interface during registration can be changed later via the Azure portal.</span></span> <span data-ttu-id="ae489-114">De volgende stappen uitvoeren om te wijzigen van het beheerderswachtwoord van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="ae489-114">Perform the following steps to change the device administrator password.</span></span>

#### <a name="to-change-the-device-administrator-password"></a><span data-ttu-id="ae489-115">Het beheerderswachtwoord van het apparaat wijzigen</span><span class="sxs-lookup"><span data-stu-id="ae489-115">To change the device administrator password</span></span>
1. <span data-ttu-id="ae489-116">Ga naar de StorSimple-apparaatbeheerservice en klik op **Apparaten**.</span><span class="sxs-lookup"><span data-stu-id="ae489-116">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="ae489-117">Selecteer in de lijst in tabelvorm van apparaten, en klik op het apparaat waarvan u wilt wijzigen wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ae489-117">From the tabular listing of devices, select and click the device whose password you intend to change.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="ae489-118">In de **instellingen** blade, gaat u naar **apparaatinstellingen > beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="ae489-118">In the **Settings** blade, go to **Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="ae489-119">In de **beveiligingsinstellingen** blade, klikt u op **wachtwoord** wijzigen van het beheerderswachtwoord van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="ae489-119">In the **Security settings** blade, click **Password** to change the device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="ae489-120">In de **wachtwoord** blade bieden een administrator-wachtwoord tussen 8 en 15 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="ae489-120">In the **Password** blade, provide an administrator password that contains from 8 to 15 characters.</span></span> <span data-ttu-id="ae489-121">Het wachtwoord moet een combinatie van 3 of meer van hoofdletters, kleine letters, numerieke en speciale tekens.</span><span class="sxs-lookup"><span data-stu-id="ae489-121">The password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="ae489-122">Bevestig het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ae489-122">Confirm the password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="ae489-123">Klik op **opslaan** wanneer u om bevestiging gevraagd, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="ae489-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="ae489-124">Het beheerderswachtwoord van het apparaat moet nu worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="ae489-124">The device administrator password should now be updated.</span></span> <span data-ttu-id="ae489-125">U kunt dit gewijzigde wachtwoord gebruiken voor toegang tot de Windows PowerShell-interface.</span><span class="sxs-lookup"><span data-stu-id="ae489-125">You can use this modified password to access the Windows PowerShell interface.</span></span>

## <a name="set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="ae489-126">Het wachtwoord voor StorSimple Snapshot Manager instellen</span><span class="sxs-lookup"><span data-stu-id="ae489-126">Set the StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="ae489-127">De StorSimple Snapshot Manager-software bevindt zich op uw Windows-host. Met deze software kunnen beheerders de back-ups van uw StorSimple-apparaat beheren. De back-ups zijn in feite momentopnamen die lokaal en in de cloud worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ae489-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators to manage backups of your StorSimple device in the form of local and cloud snapshots.</span></span>

<span data-ttu-id="ae489-128">Wanneer u een apparaat in StorSimple Snapshot Manager configureert, wordt u gevraagd de IP-adres en het wachtwoord voor verificatie van uw opslagapparaat opgeven.</span><span class="sxs-lookup"><span data-stu-id="ae489-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted to provide the device IP address and password to authenticate your storage device.</span></span>

<span data-ttu-id="ae489-129">U kunt instellen of het wachtwoord voor StorSimple Snapshot Manager wijzigen via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ae489-129">You can set or change the password for StorSimple Snapshot Manager via the Azure portal.</span></span> <span data-ttu-id="ae489-130">De volgende stappen wilt instellen of wijzigen van het wachtwoord voor StorSimple Snapshot Manager uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ae489-130">Perform the following steps to set or change the StorSimple Snapshot Manager password.</span></span>

#### <a name="to-set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="ae489-131">De StorSimple Snapshot Manager-wachtwoord instellen</span><span class="sxs-lookup"><span data-stu-id="ae489-131">To set the StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="ae489-132">Ga naar de StorSimple-apparaatbeheerservice en klik op **Apparaten**.</span><span class="sxs-lookup"><span data-stu-id="ae489-132">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="ae489-133">Selecteer in de lijst in tabelvorm van apparaten, en klik op het apparaat waarvan u wilt instellen of wijzigen van het wachtwoord StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="ae489-133">From the tabular listing of devices, select and click the device whose StorSimple Snapshot Manager password you intend to set or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="ae489-134">In de **instellingen** blade, gaat u naar **apparaatinstellingen > beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="ae489-134">In the **Settings** blade, go to **Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="ae489-135">In de **beveiligingsinstellingen** blade, klikt u op **wachtwoord** instellen of wijzigen van het StorSimple Snapshot Manager-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ae489-135">In the **Security settings** blade, click **Password** to set or change the StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="ae489-136">In de **wachtwoord** blade, voer een wachtwoord 14 of 15 tekens.</span><span class="sxs-lookup"><span data-stu-id="ae489-136">In the **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="ae489-137">Zorg ervoor dat het wachtwoord een combinatie van 3 of meer van hoofdletters, kleine letters, numerieke en speciale tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="ae489-137">Make sure that the password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="ae489-138">Bevestig het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ae489-138">Confirm the password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="ae489-139">Klik op **opslaan** wanneer u om bevestiging gevraagd, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="ae489-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="ae489-140">Het wachtwoord voor StorSimple Snapshot Manager moet nu worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="ae489-140">The StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae489-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ae489-141">Next steps</span></span>
* <span data-ttu-id="ae489-142">Meer informatie over [StorSimple security](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="ae489-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="ae489-143">Meer informatie over [wijzigen van de configuratie van uw apparaat](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="ae489-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="ae489-144">Meer informatie over [de service Manager voor StorSimple-apparaat gebruiken voor het beheer van uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ae489-144">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

