---
title: Wijziging virtuele StorSimple-matrix apparaatwachtwoord admin | Microsoft Docs
description: Beschrijft hoe de Azure portal of het virtuele StorSimple-matrix webgebruikersinterface gebruiken om te wijzigen van het beheerderswachtwoord van het apparaat.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 260a23003d705e6598da8c51bb5a96f2539a0014
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="dd167-103">Wijzig het beheerderswachtwoord voor virtuele StorSimple-matrix apparaat via de StorSimple-Apparaatbeheer</span><span class="sxs-lookup"><span data-stu-id="dd167-103">Change the StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="dd167-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="dd167-104">Overview</span></span>

<span data-ttu-id="dd167-105">Wanneer u de Windows PowerShell-interface gebruiken voor toegang tot de virtuele StorSimple-matrix, hoeft u een apparaat administrator-wachtwoord moeten invoeren.</span><span class="sxs-lookup"><span data-stu-id="dd167-105">When you use the Windows PowerShell interface to access the StorSimple Virtual Array, you are required to enter a device administrator password.</span></span> <span data-ttu-id="dd167-106">Wanneer het StorSimple-apparaat eerst is ingericht en is gestart, is het standaardwachtwoord *Wachtwoord1*.</span><span class="sxs-lookup"><span data-stu-id="dd167-106">When the StorSimple device is first provisioned and started, the default password is *Password1*.</span></span> <span data-ttu-id="dd167-107">De standaardwachtwoord is verlopen, is de eerste keer dat u zich aanmelden als u dit wachtwoord wijzigen zijn vereist voor de beveiliging van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="dd167-107">For the security of your data, the default password expires the first time that you sign in and you are required to change this password.</span></span>

<span data-ttu-id="dd167-108">U kunt ook de lokale webgebruikersinterface of Azure portal gebruiken om te wijzigen van het beheerderswachtwoord van het apparaat op elk gewenst moment nadat het apparaat is geïmplementeerd in uw productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="dd167-108">You can also use either the local web UI or the Azure portal to change the device administrator password at any time after the device is deployed in your production environment.</span></span> <span data-ttu-id="dd167-109">Elk van deze procedures wordt beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="dd167-109">Each of these procedures is described in this article.</span></span>

 ![Blade voor apparaten](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-the-azure-portal-to-change-the-password"></a><span data-ttu-id="dd167-111">De Azure portal gebruiken om het wachtwoord te wijzigen</span><span class="sxs-lookup"><span data-stu-id="dd167-111">Use the Azure portal to change the password</span></span>

<span data-ttu-id="dd167-112">De volgende stappen uitvoeren om te wijzigen van het beheerderswachtwoord van het apparaat via de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dd167-112">Perform the following steps to change the device administrator password through the Azure portal.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-azure-portal"></a><span data-ttu-id="dd167-113">Het beheerderswachtwoord van het apparaat via de Azure-portal wijzigen</span><span class="sxs-lookup"><span data-stu-id="dd167-113">To change the device administrator password via the Azure portal</span></span>

1. <span data-ttu-id="dd167-114">Selecteer uw service op de startpagina van de service, dubbelklikt u op de servicenaam en klik vervolgens in de **Management** sectie, klikt u op **apparaten**.</span><span class="sxs-lookup"><span data-stu-id="dd167-114">On the service landing page, select your service, double-click the service name, and then within the **Management** section, click **Devices**.</span></span> <span data-ttu-id="dd167-115">Hiermee opent u de **apparaten** blade met een lijst met alle apparaten in uw virtuele StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="dd167-115">This opens the **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="dd167-116">In de **apparaten** blade, dubbelklik op het apparaat waarvoor u een wachtwoord is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="dd167-116">In the **Devices** blade, double-click the device that requires a change of password.</span></span>

3. <span data-ttu-id="dd167-117">In de **instellingen** blade voor uw apparaat, klikt u op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="dd167-117">In the **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="dd167-118">In de **beveiligingsinstellingen** blade het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="dd167-118">In the **Security Settings** blade, do the following:</span></span>
   
   1. <span data-ttu-id="dd167-119">Schuif omlaag naar de **apparaat beheerderswachtwoord** sectie.</span><span class="sxs-lookup"><span data-stu-id="dd167-119">Scroll down to the **Device Administrator Password** section.</span></span> <span data-ttu-id="dd167-120">Geef een administrator-wachtwoord tussen 8 en 15 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="dd167-120">Provide an administrator password that contains from 8 to 15 characters.</span></span>
   2. <span data-ttu-id="dd167-121">Bevestig het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="dd167-121">Confirm the password.</span></span>
   3. <span data-ttu-id="dd167-122">Klik op **opslaan** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="dd167-122">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="dd167-123">Het beheerderswachtwoord van het apparaat is nu bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="dd167-123">The device administrator password is now updated.</span></span> <span data-ttu-id="dd167-124">U kunt dit gewijzigde wachtwoord gebruiken voor toegang tot het apparaat lokaal.</span><span class="sxs-lookup"><span data-stu-id="dd167-124">You can use this modified password to access the device locally.</span></span>

![Blade Security-instellingen](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-the-local-web-ui-to-change-the-password"></a><span data-ttu-id="dd167-126">De lokale webgebruikersinterface gebruiken om het wachtwoord te wijzigen</span><span class="sxs-lookup"><span data-stu-id="dd167-126">Use the local web UI to change the password</span></span>

<span data-ttu-id="dd167-127">De volgende stappen uitvoeren om te wijzigen van het beheerderswachtwoord van het apparaat via de lokale webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="dd167-127">Perform the following steps to change the device administrator password through the local web UI.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-local-web-ui"></a><span data-ttu-id="dd167-128">Het beheerderswachtwoord van het apparaat via de lokale webgebruikersinterface wijzigen</span><span class="sxs-lookup"><span data-stu-id="dd167-128">To change the device administrator password via the local web UI</span></span>

1. <span data-ttu-id="dd167-129">Klik in de lokale webgebruikersinterface op **onderhoud** > **wachtwoordwijziging** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="dd167-129">In the local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![Wachtwoord1 wijzigen](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="dd167-131">Voer de **huidige wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="dd167-131">Enter the **Current password**.</span></span>
3. <span data-ttu-id="dd167-132">Geef een **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="dd167-132">Provide a **New Password**.</span></span> <span data-ttu-id="dd167-133">Het wachtwoord moet ten minste 8 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="dd167-133">The password must be at least 8 characters long.</span></span> <span data-ttu-id="dd167-134">Deze moet 3 van 4 van de volgende waarden bevatten: hoofdletters, kleine letters, numerieke en speciale tekens.</span><span class="sxs-lookup"><span data-stu-id="dd167-134">It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="dd167-135">Houd er rekening mee dat uw wachtwoord mag niet hetzelfde zijn als de laatste 24 wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="dd167-135">Note that your password cannot be the same as the last 24 passwords.</span></span>
4. <span data-ttu-id="dd167-136">Geef het wachtwoord ter bevestiging opnieuw.</span><span class="sxs-lookup"><span data-stu-id="dd167-136">Reenter the password to confirm it.</span></span>
   
    ![Wachtwoord2 wijzigen](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="dd167-138">Klik onder aan de pagina op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="dd167-138">At the bottom of the page, click **Apply**.</span></span> <span data-ttu-id="dd167-139">Het nieuwe wachtwoord is nu toegepast.</span><span class="sxs-lookup"><span data-stu-id="dd167-139">The new password is now applied.</span></span> <span data-ttu-id="dd167-140">Als het wijzigen van het wachtwoord is niet geslaagd, ziet u de volgende fout:</span><span class="sxs-lookup"><span data-stu-id="dd167-140">If the password change is not successful, you see the following error:</span></span>
   
    ![Fout bij het](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="dd167-142">Nadat het wachtwoord is bijgewerkt, wordt u gewaarschuwd.</span><span class="sxs-lookup"><span data-stu-id="dd167-142">After the password is successfully updated, you are notified.</span></span> <span data-ttu-id="dd167-143">U kunt vervolgens dit gewijzigde wachtwoord gebruiken voor toegang tot het apparaat lokaal.</span><span class="sxs-lookup"><span data-stu-id="dd167-143">You can then use this modified password to access the device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dd167-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dd167-144">Next steps</span></span>
<span data-ttu-id="dd167-145">Meer informatie over hoe [beheren van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="dd167-145">Learn how to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

