---
title: aaaConfigure CHAP voor StorSimple 8000 series apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe tooconfigure Challenge Handshake Authentication Protocol (CHAP) Hallo op een StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="6e9e5-103">CHAP configureren voor uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="6e9e5-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="6e9e5-104">Deze zelfstudie wordt uitgelegd hoe tooconfigure CHAP voor uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="6e9e5-105">Hallo-procedure in dit artikel wordt beschreven geldt tooStorSimple 8000-serie, evenals 1200 StorSimple-apparaten.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-105">hello procedure detailed in this article applies tooStorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="6e9e5-106">CHAP staat voor Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="6e9e5-107">Het is een verificatieschema dat wordt gebruikt door servers toovalidate Hallo identiteit van externe clients.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="6e9e5-108">Hallo-verificatie is gebaseerd op een gedeelde wachtwoord of geheim.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="6e9e5-109">CHAP mag eenzijdige (Unidirectioneel) of onderlinge (bidirectioneel).</span><span class="sxs-lookup"><span data-stu-id="6e9e5-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="6e9e5-110">Eenzijdige CHAP is wanneer er wordt een initiator Hallo doel geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-110">One-way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="6e9e5-111">Wederzijdse of reverse-CHAP Hallo daarentegen is vereist dat Hallo doel Hallo initiator verifiëren en vervolgens Hallo initiator Hallo doel te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-111">Mutual or reverse CHAP, on hello other hand, requires that hello target authenticate hello initiator and then hello initiator authenticate hello target.</span></span> <span data-ttu-id="6e9e5-112">Initiator verificatie kan worden geïmplementeerd zonder verificatie doel.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="6e9e5-113">Doel-verificatie kan echter alleen als de verificatie van de initiator is ook geïmplementeerd worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="6e9e5-114">Als een best practice is het raadzaam dat u CHAP tooenhance iSCSI-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="6e9e5-115">Houd er rekening mee dat IPSEC wordt momenteel niet ondersteund op het StorSimple-apparaten.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="6e9e5-116">Hallo CHAP-instellingen op Hallo StorSimple-apparaat kunnen worden geconfigureerd in de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="6e9e5-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="6e9e5-117">Unidirectioneel of eenrichtings-verificatie</span><span class="sxs-lookup"><span data-stu-id="6e9e5-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="6e9e5-118">Bidirectionele of wederzijdse of reverse-verificatie</span><span class="sxs-lookup"><span data-stu-id="6e9e5-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="6e9e5-119">Hallo-portal voor het Hallo-apparaat en Hallo server iSCSI-initiatorsoftware moet in elk van deze gevallen toobe geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="6e9e5-120">Hallo gedetailleerde stappen voor deze configuratie worden beschreven in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="6e9e5-121">Unidirectioneel of eenrichtings-verificatie</span><span class="sxs-lookup"><span data-stu-id="6e9e5-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="6e9e5-122">In één richting verificatie verifieert Hallo doel Hallo initiator.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="6e9e5-123">Deze verificatie vereist dat u Hallo CHAP-initiator instellingen op Hallo StorSimple-apparaat en Hallo iSCSI-initiatorsoftware op Hallo host configureren.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="6e9e5-124">Hallo gedetailleerde procedures voor uw StorSimple-apparaat en Windows-host worden nu beschreven.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="6e9e5-125">tooconfigure uw apparaat voor eenzijdige verificatie</span><span class="sxs-lookup"><span data-stu-id="6e9e5-125">tooconfigure your device for one-way authentication</span></span>
1. <span data-ttu-id="6e9e5-126">In de klassieke Azure-portal op Hallo Hallo **apparaten** pagina, klikt u op Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-126">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![CHAP-Initiator](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="6e9e5-128">Schuif naar beneden op deze pagina en in Hallo **CHAP-Initiator** sectie:</span><span class="sxs-lookup"><span data-stu-id="6e9e5-128">Scroll down on this page, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="6e9e5-129">Geef een gebruikersnaam op voor uw CHAP-initiator.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="6e9e5-130">Een wachtwoord opgeven voor CHAP-initiator.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="6e9e5-131">Hallo CHAP-gebruikersnaam moet minder dan 233 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-131">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="6e9e5-132">Hallo CHAP-wachtwoord moet tussen 12 en 16 tekens.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-132">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="6e9e5-133">Een langer gebruikersnaam of wachtwoord leidt tot een verificatiefout opgetreden op Hallo Windows-host.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-133">A longer user name or password will result in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="6e9e5-134">Hallo wachtwoord bevestigen.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-134">Confirm hello password.</span></span>
3. <span data-ttu-id="6e9e5-135">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-135">Click **Save**.</span></span> <span data-ttu-id="6e9e5-136">Een bevestigingsbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="6e9e5-137">Klik op **OK** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-137">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="6e9e5-138">eenzijdige verificatie tooconfigure op Hallo van Windows server host</span><span class="sxs-lookup"><span data-stu-id="6e9e5-138">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="6e9e5-139">Start Hallo iSCSI-Initiator op hostserver uit Windows hello.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-139">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="6e9e5-140">In Hallo **eigenschappen iSCSI-Initiator** venster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="6e9e5-140">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="6e9e5-141">Klik op Hallo **detectie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-141">Click hello **Discovery** tab.</span></span>
      
       ![Eigenschappen iSCSI-initiator](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="6e9e5-143">Klik op **Portal detecteren**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="6e9e5-144">In Hallo **doelportaal detecteren** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="6e9e5-144">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="6e9e5-145">Hallo IP-adres van uw apparaat opgeven.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-145">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="6e9e5-146">Klik op **geavanceerde**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-146">Click **Advanced**.</span></span>
      
       ![Doelportaal detecteren](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="6e9e5-148">In Hallo **geavanceerde instellingen** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="6e9e5-148">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="6e9e5-149">Selecteer Hallo **inschakelen CHAP aanmelden** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-149">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="6e9e5-150">In Hallo **naam** veld, levering Hallo-gebruikersnaam die u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-150">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="6e9e5-151">In Hallo **geheim van het doel** veld, geef Hallo wachtwoord dat u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-151">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="6e9e5-152">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-152">Click **OK**.</span></span>
      
       ![Geavanceerde instellingen algemeen](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="6e9e5-154">Op Hallo **doelen** tabblad Hallo **eigenschappen iSCSI-Initiator** venster Hallo Apparaatstatus moet worden weergegeven als **verbonden**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-154">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="6e9e5-155">Als u een 1200 StorSimple-apparaat gebruikt, zal klikt u vervolgens elk volume worden gekoppeld als een iSCSI-doel zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="6e9e5-156">Stap 3 en 4 moet daarom toobe herhaald voor elk volume.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-156">Hence, steps  3-4 will need toobe repeated for each volume.</span></span>
   
    ![Volumes die zijn gekoppeld als afzonderlijke doelen](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="6e9e5-158">Als u de naam van de iSCSI-Hallo wijzigt, wordt de nieuwe naam hello worden gebruikt voor nieuwe iSCSI-sessies.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-158">If you change hello iSCSI name, hello new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="6e9e5-159">Nieuwe instellingen worden niet gebruikt voor bestaande sessies totdat u afmelden en aanmelden opnieuw.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="6e9e5-160">Ga te voor meer informatie over het configureren van CHAP op de hostserver voor Windows hello[aanvullende overwegingen](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="6e9e5-160">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="6e9e5-161">Bidirectionele of wederzijdse verificatie</span><span class="sxs-lookup"><span data-stu-id="6e9e5-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="6e9e5-162">Hallo doel verifieert Hallo initiator in twee richtingen-verificatie en Hallo initiator verifieert vervolgens Hallo doel.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-162">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="6e9e5-163">Hiervoor moet Hallo tooconfigure Hallo CHAP initiator gebruikersinstellingen, evenals Hallo omgekeerde CHAP-instellingen op Hallo apparaat- en iSCSI-initiatorsoftware op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-163">This requires hello user tooconfigure hello CHAP initiator settings, as well as hello reverse CHAP settings on hello device and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="6e9e5-164">Hallo volgende procedures beschrijven Hallo stappen tooconfigure wederzijdse verificatie op Hallo-apparaat en op Hallo Windows-host.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-164">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="6e9e5-165">tooconfigure uw apparaat voor wederzijdse verificatie</span><span class="sxs-lookup"><span data-stu-id="6e9e5-165">tooconfigure your device for mutual authentication</span></span>
1. <span data-ttu-id="6e9e5-166">In de klassieke Azure-portal op Hallo Hallo **apparaten** pagina, klikt u op Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-166">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![CHAP-doel](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="6e9e5-168">Schuif naar beneden op deze pagina en in Hallo **CHAP Target** sectie:</span><span class="sxs-lookup"><span data-stu-id="6e9e5-168">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="6e9e5-169">Geef een **omgekeerde CHAP-gebruikersnaam** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="6e9e5-170">Geef een **omgekeerde CHAP-wachtwoord** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="6e9e5-171">Hallo wachtwoord bevestigen.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-171">Confirm hello password.</span></span>
3. <span data-ttu-id="6e9e5-172">In Hallo **CHAP-Initiator** sectie:</span><span class="sxs-lookup"><span data-stu-id="6e9e5-172">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="6e9e5-173">Geef een **gebruikersnaam** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="6e9e5-174">Geef een **wachtwoord** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="6e9e5-175">Hallo wachtwoord bevestigen.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-175">Confirm hello password.</span></span>
4. <span data-ttu-id="6e9e5-176">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-176">Click **Save**.</span></span> <span data-ttu-id="6e9e5-177">Een bevestigingsbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="6e9e5-178">Klik op **OK** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-178">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="6e9e5-179">tooconfigure bidirectionele verificatie op Hallo van Windows server host</span><span class="sxs-lookup"><span data-stu-id="6e9e5-179">tooconfigure bidirectional authentication on hello Windows host server</span></span>
1. <span data-ttu-id="6e9e5-180">Start Hallo iSCSI-Initiator op hostserver uit Windows hello.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-180">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="6e9e5-181">In Hallo **eigenschappen iSCSI-Initiator** venster, klikt u op Hallo **configuratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-181">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="6e9e5-182">Klik op **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="6e9e5-183">In Hallo **iSCSI-Initiator wederzijdse CHAP Secret** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="6e9e5-183">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="6e9e5-184">Type Hallo **omgekeerde CHAP-wachtwoord** die u in de klassieke Azure-portal Hallo geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-184">Type hello **Reverse CHAP Password** that you configured in hello Azure classic portal.</span></span>
   2. <span data-ttu-id="6e9e5-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-185">Click **OK**.</span></span>
      
       ![iSCSI-initiator wederzijdse CHAP-geheim](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="6e9e5-187">Klik op Hallo **doelen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-187">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="6e9e5-188">Klik op Hallo **Connect** knop.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-188">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="6e9e5-189">In Hallo **verbinding tooTarget** in het dialoogvenster, klikt u op **Geavanceerd**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-189">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="6e9e5-190">In Hallo **geavanceerde eigenschappen** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="6e9e5-190">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="6e9e5-191">Selecteer Hallo **inschakelen CHAP aanmelden** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-191">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="6e9e5-192">In Hallo **naam** veld, levering Hallo-gebruikersnaam die u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-192">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="6e9e5-193">In Hallo **geheim van het doel** veld, geef Hallo wachtwoord dat u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-193">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="6e9e5-194">Selecteer Hallo **wederzijdse verificatie uitvoeren** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-194">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Geavanceerde instellingen voor wederzijdse verificatie](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="6e9e5-196">Klik op **OK** toocomplete Hallo CHAP-configuratie</span><span class="sxs-lookup"><span data-stu-id="6e9e5-196">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="6e9e5-197">Ga te voor meer informatie over het configureren van CHAP op de hostserver voor Windows hello[aanvullende overwegingen](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="6e9e5-197">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="6e9e5-198">Aanvullende overwegingen</span><span class="sxs-lookup"><span data-stu-id="6e9e5-198">Additional considerations</span></span>
<span data-ttu-id="6e9e5-199">Hallo **snelle verbinding** functie biedt geen ondersteuning voor verbindingen waarvoor CHAP ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-199">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="6e9e5-200">Wanneer CHAP is ingeschakeld, zorg ervoor dat u Hallo **Connect** knop die beschikbaar is op Hallo **doelen** tabblad tooconnect tooa doel.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-200">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Verbinding maken met tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="6e9e5-202">In Hallo **verbinding tooTarget** dialoogvenster dat wordt aangeboden, selecteer Hallo **deze verbinding toohello lijst met favoriete doelen toevoegen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-202">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="6e9e5-203">Dit zorgt ervoor dat elke keer Hallo computer opnieuw is opgestart, wordt geprobeerd toorestore Hallo verbinding toohello iSCSI-favoriete doelen.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-203">This ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="6e9e5-204">Fouten tijdens het configureren van</span><span class="sxs-lookup"><span data-stu-id="6e9e5-204">Errors during configuration</span></span>
<span data-ttu-id="6e9e5-205">Als de CHAP-configuratie onjuist is, moet u waarschijnlijk toosee zijn een **verificatiefout** foutbericht.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-205">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="6e9e5-206">Verificatie van CHAP-configuratie</span><span class="sxs-lookup"><span data-stu-id="6e9e5-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="6e9e5-207">U kunt controleren dat CHAP wordt gebruikt door Hallo volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-207">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="6e9e5-208">tooverify uw CHAP-configuratie</span><span class="sxs-lookup"><span data-stu-id="6e9e5-208">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="6e9e5-209">Klik op **favoriete doelen**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="6e9e5-210">Selecteer Hallo doel waarvoor verificatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-210">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="6e9e5-211">Klik op **Details**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-211">Click **Details**.</span></span>
   
    ![iSCSI-initiator eigenschappen favoriete doelen](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="6e9e5-213">In Hallo **favoriete Doeldetails** in het dialoogvenster vermelding van de opmerking Hallo in Hallo **verificatie** veld.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-213">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="6e9e5-214">Als is Hallo-configuratie voltooid is, moet spreken **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="6e9e5-214">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Details van de favoriet doel](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="6e9e5-216">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e9e5-216">Next steps</span></span>
* <span data-ttu-id="6e9e5-217">Meer informatie over [StorSimple security](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="6e9e5-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="6e9e5-218">Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6e9e5-218">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

