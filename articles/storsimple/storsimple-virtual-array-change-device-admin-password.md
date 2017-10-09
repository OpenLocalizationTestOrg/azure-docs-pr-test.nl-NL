---
title: beheerderswachtwoord voor aaaChange virtuele matrix StorSimple-apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe toouse ofwel hello Azure portal of virtuele StorSimple-matrix web UI toochange Hallo beheerderswachtwoord apparaat.
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
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="71ebd-103">Hallo virtuele StorSimple-matrix apparaat beheerderswachtwoord via StorSimple Apparaatbeheer wijzigen</span><span class="sxs-lookup"><span data-stu-id="71ebd-103">Change hello StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="71ebd-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="71ebd-104">Overview</span></span>

<span data-ttu-id="71ebd-105">Wanneer u Hallo Windows PowerShell-interface tooaccess Hallo virtuele StorSimple-matrix, bent u vereiste tooenter het beheerderswachtwoord voor een apparaat.</span><span class="sxs-lookup"><span data-stu-id="71ebd-105">When you use hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="71ebd-106">Wanneer Hallo StorSimple-apparaat eerst is ingericht en is gestart, is het standaardwachtwoord Hallo *Wachtwoord1*.</span><span class="sxs-lookup"><span data-stu-id="71ebd-106">When hello StorSimple device is first provisioned and started, hello default password is *Password1*.</span></span> <span data-ttu-id="71ebd-107">Voor beveiliging van uw gegevens Hallo Hallo standaardwachtwoord verloopt Hallo eerste keer is dat u zich aanmelden en u vereiste toochange zijn dit wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="71ebd-107">For hello security of your data, hello default password expires hello first time that you sign in and you are required toochange this password.</span></span>

<span data-ttu-id="71ebd-108">U kunt ook beide Hallo lokale web UI of hello Azure portal toochange Hallo wachtwoord apparaatbeheerder op elk gewenst moment nadat Hallo-apparaat is geïmplementeerd in uw productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="71ebd-108">You can also use either hello local web UI or hello Azure portal toochange hello device administrator password at any time after hello device is deployed in your production environment.</span></span> <span data-ttu-id="71ebd-109">Elk van deze procedures wordt beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="71ebd-109">Each of these procedures is described in this article.</span></span>

 ![Blade voor apparaten](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a><span data-ttu-id="71ebd-111">Hello Azure portal toochange Hallo wachtwoord gebruiken</span><span class="sxs-lookup"><span data-stu-id="71ebd-111">Use hello Azure portal toochange hello password</span></span>

<span data-ttu-id="71ebd-112">Volgende stappen toochange Hallo beheerderswachtwoord apparaat via de Azure-portal Hallo Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="71ebd-112">Perform hello following steps toochange hello device administrator password through hello Azure portal.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a><span data-ttu-id="71ebd-113">toochange hello beheerderswachtwoord apparaat via hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="71ebd-113">toochange hello device administrator password via hello Azure portal</span></span>

1. <span data-ttu-id="71ebd-114">Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **Management** sectie, klikt u op **apparaten**.</span><span class="sxs-lookup"><span data-stu-id="71ebd-114">On hello service landing page, select your service, double-click hello service name, and then within hello **Management** section, click **Devices**.</span></span> <span data-ttu-id="71ebd-115">Hiermee opent u Hallo **apparaten** blade met een lijst met alle apparaten in uw virtuele StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="71ebd-115">This opens hello **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="71ebd-116">In Hallo **apparaten** blade, dubbelklikt u op Hallo-apparaat dat een wijziging van wachtwoord vereist.</span><span class="sxs-lookup"><span data-stu-id="71ebd-116">In hello **Devices** blade, double-click hello device that requires a change of password.</span></span>

3. <span data-ttu-id="71ebd-117">In Hallo **instellingen** blade voor uw apparaat, klikt u op **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="71ebd-117">In hello **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="71ebd-118">In Hallo **beveiligingsinstellingen** blade Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="71ebd-118">In hello **Security Settings** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="71ebd-119">Schuif omlaag toohello **apparaat beheerderswachtwoord** sectie.</span><span class="sxs-lookup"><span data-stu-id="71ebd-119">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="71ebd-120">Geef een administrator-wachtwoord van 8 too15 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="71ebd-120">Provide an administrator password that contains from 8 too15 characters.</span></span>
   2. <span data-ttu-id="71ebd-121">Hallo wachtwoord bevestigen.</span><span class="sxs-lookup"><span data-stu-id="71ebd-121">Confirm hello password.</span></span>
   3. <span data-ttu-id="71ebd-122">Klik op **opslaan** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="71ebd-122">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="71ebd-123">Hallo beheerder het wachtwoord van het apparaat is nu bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="71ebd-123">hello device administrator password is now updated.</span></span> <span data-ttu-id="71ebd-124">U kunt dit apparaat gewijzigde wachtwoord tooaccess Hallo lokaal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71ebd-124">You can use this modified password tooaccess hello device locally.</span></span>

![Blade Security-instellingen](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a><span data-ttu-id="71ebd-126">Hallo lokale web UI toochange Hallo wachtwoord gebruiken</span><span class="sxs-lookup"><span data-stu-id="71ebd-126">Use hello local web UI toochange hello password</span></span>

<span data-ttu-id="71ebd-127">Volgende stappen toochange Hallo beheerderswachtwoord apparaat via Hallo lokale webgebruikersinterface Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="71ebd-127">Perform hello following steps toochange hello device administrator password through hello local web UI.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a><span data-ttu-id="71ebd-128">toochange hello beheerderswachtwoord apparaat via Hallo lokale webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="71ebd-128">toochange hello device administrator password via hello local web UI</span></span>

1. <span data-ttu-id="71ebd-129">Klik in Hallo lokale web UI op **onderhoud** > **wachtwoordwijziging** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="71ebd-129">In hello local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![Wachtwoord1 wijzigen](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="71ebd-131">Voer Hallo **huidige wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="71ebd-131">Enter hello **Current password**.</span></span>
3. <span data-ttu-id="71ebd-132">Geef een **nieuw wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="71ebd-132">Provide a **New Password**.</span></span> <span data-ttu-id="71ebd-133">Hallo-wachtwoord moet ten minste 8 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="71ebd-133">hello password must be at least 8 characters long.</span></span> <span data-ttu-id="71ebd-134">Deze moet 3 van 4 van Hallo volgende bevatten: hoofdletters, kleine letters, numerieke en speciale tekens.</span><span class="sxs-lookup"><span data-stu-id="71ebd-134">It must contain 3 of 4 of hello following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="71ebd-135">Denk eraan dat uw wachtwoord mag niet Hallo hetzelfde als de laatste 24 wachtwoorden Hallo.</span><span class="sxs-lookup"><span data-stu-id="71ebd-135">Note that your password cannot be hello same as hello last 24 passwords.</span></span>
4. <span data-ttu-id="71ebd-136">Hallo wachtwoord tooconfirm opnieuw het.</span><span class="sxs-lookup"><span data-stu-id="71ebd-136">Reenter hello password tooconfirm it.</span></span>
   
    ![Wachtwoord2 wijzigen](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="71ebd-138">Klik onder aan de pagina Hallo Hallo op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="71ebd-138">At hello bottom of hello page, click **Apply**.</span></span> <span data-ttu-id="71ebd-139">het nieuwe wachtwoord Hallo nu wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="71ebd-139">hello new password is now applied.</span></span> <span data-ttu-id="71ebd-140">Als het Hallo-wachtwoordwijziging niet is geslaagd, ziet u Hallo volgende fout:</span><span class="sxs-lookup"><span data-stu-id="71ebd-140">If hello password change is not successful, you see hello following error:</span></span>
   
    ![Fout bij het](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="71ebd-142">Nadat het Hallo-wachtwoord is bijgewerkt, wordt u gewaarschuwd.</span><span class="sxs-lookup"><span data-stu-id="71ebd-142">After hello password is successfully updated, you are notified.</span></span> <span data-ttu-id="71ebd-143">Vervolgens kunt u dit apparaat gewijzigde wachtwoord tooaccess Hallo lokaal.</span><span class="sxs-lookup"><span data-stu-id="71ebd-143">You can then use this modified password tooaccess hello device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="71ebd-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="71ebd-144">Next steps</span></span>
<span data-ttu-id="71ebd-145">Meer informatie over hoe te[beheren van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="71ebd-145">Learn how too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

