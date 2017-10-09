---
title: aaaConfigure CHAP voor StorSimple 8000 series apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe tooconfigure Challenge Handshake Authentication Protocol (CHAP) Hallo op een StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="3b05b-103">CHAP configureren voor uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="3b05b-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="3b05b-104">Deze zelfstudie wordt uitgelegd hoe tooconfigure CHAP voor uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="3b05b-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="3b05b-105">Hallo-procedure in dit artikel wordt beschreven geldt tooStorSimple 8000 reeks apparaten.</span><span class="sxs-lookup"><span data-stu-id="3b05b-105">hello procedure detailed in this article applies tooStorSimple 8000 series devices.</span></span>

<span data-ttu-id="3b05b-106">CHAP staat voor Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="3b05b-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="3b05b-107">Het is een verificatieschema dat wordt gebruikt door servers toovalidate Hallo identiteit van externe clients.</span><span class="sxs-lookup"><span data-stu-id="3b05b-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="3b05b-108">Hallo-verificatie is gebaseerd op een gedeelde wachtwoord of geheim.</span><span class="sxs-lookup"><span data-stu-id="3b05b-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="3b05b-109">CHAP mag een manier (Unidirectioneel) of onderlinge (bidirectioneel).</span><span class="sxs-lookup"><span data-stu-id="3b05b-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="3b05b-110">Een manier CHAP is wanneer er wordt een initiator Hallo doel geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="3b05b-110">One way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="3b05b-111">In de wederzijdse of reverse-CHAP Hallo doel verifieert Hallo initiator en Hallo initiator verifieert vervolgens Hallo doel.</span><span class="sxs-lookup"><span data-stu-id="3b05b-111">In mutual or reverse CHAP, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="3b05b-112">Initiator verificatie kan worden geïmplementeerd zonder verificatie doel.</span><span class="sxs-lookup"><span data-stu-id="3b05b-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="3b05b-113">Doel-verificatie kan echter alleen als de verificatie van de initiator is ook geïmplementeerd worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3b05b-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="3b05b-114">Als een best practice is het raadzaam dat u CHAP tooenhance iSCSI-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="3b05b-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="3b05b-115">Houd er rekening mee dat IPSEC wordt momenteel niet ondersteund op het StorSimple-apparaten.</span><span class="sxs-lookup"><span data-stu-id="3b05b-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="3b05b-116">Hallo CHAP-instellingen op Hallo StorSimple-apparaat kunnen worden geconfigureerd in de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="3b05b-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="3b05b-117">Unidirectioneel of eenrichtings-verificatie</span><span class="sxs-lookup"><span data-stu-id="3b05b-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="3b05b-118">Bidirectionele of wederzijdse of reverse-verificatie</span><span class="sxs-lookup"><span data-stu-id="3b05b-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="3b05b-119">Hallo-portal voor het Hallo-apparaat en Hallo server iSCSI-initiatorsoftware moet in elk van deze gevallen toobe geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3b05b-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="3b05b-120">Hallo gedetailleerde stappen voor deze configuratie worden beschreven in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b05b-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="3b05b-121">Unidirectioneel of eenrichtings-verificatie</span><span class="sxs-lookup"><span data-stu-id="3b05b-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="3b05b-122">In één richting verificatie verifieert Hallo doel Hallo initiator.</span><span class="sxs-lookup"><span data-stu-id="3b05b-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="3b05b-123">Deze verificatie vereist dat u Hallo CHAP-initiator instellingen op Hallo StorSimple-apparaat en Hallo iSCSI-initiatorsoftware op Hallo host configureren.</span><span class="sxs-lookup"><span data-stu-id="3b05b-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="3b05b-124">Hallo gedetailleerde procedures voor uw StorSimple-apparaat en Windows-host worden nu beschreven.</span><span class="sxs-lookup"><span data-stu-id="3b05b-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="3b05b-125">tooconfigure uw apparaat voor eenzijdige verificatie</span><span class="sxs-lookup"><span data-stu-id="3b05b-125">tooconfigure your device for one-way authentication</span></span>

1. <span data-ttu-id="3b05b-126">Ga in hello Azure-portal, tooyour Apparaatbeheer StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="3b05b-126">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="3b05b-127">Klik op **apparaten** en selecteer een apparaat dat u wenst dat tooconfigure CHAP voor.</span><span class="sxs-lookup"><span data-stu-id="3b05b-127">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="3b05b-128">Ga te**apparaatinstellingen > beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-128">Go too**Device settings > Security**.</span></span> <span data-ttu-id="3b05b-129">In Hallo **beveiligingsinstellingen** blade, klikt u op **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-129">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP-Initiator](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="3b05b-131">In Hallo **CHAP** blade en in Hallo **CHAP-Initiator** sectie:</span><span class="sxs-lookup"><span data-stu-id="3b05b-131">In hello **CHAP** blade, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="3b05b-132">Geef een gebruikersnaam op voor uw CHAP-initiator.</span><span class="sxs-lookup"><span data-stu-id="3b05b-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="3b05b-133">Een wachtwoord opgeven voor CHAP-initiator.</span><span class="sxs-lookup"><span data-stu-id="3b05b-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="3b05b-134">Hallo CHAP-gebruikersnaam moet minder dan 233 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="3b05b-134">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="3b05b-135">Hallo CHAP-wachtwoord moet tussen 12 en 16 tekens.</span><span class="sxs-lookup"><span data-stu-id="3b05b-135">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="3b05b-136">Een langer gebruikersnaam of wachtwoord resulteert in een verificatiefout opgetreden op Hallo Windows-host.</span><span class="sxs-lookup"><span data-stu-id="3b05b-136">A longer user name or password results in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="3b05b-137">Hallo wachtwoord bevestigen.</span><span class="sxs-lookup"><span data-stu-id="3b05b-137">Confirm hello password.</span></span>

       ![CHAP-Initiator](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="3b05b-139">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-139">Click **Save**.</span></span> <span data-ttu-id="3b05b-140">Er wordt een bevestigingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3b05b-140">A confirmation message is displayed.</span></span> <span data-ttu-id="3b05b-141">Klik op **OK** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="3b05b-141">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="3b05b-142">eenzijdige verificatie tooconfigure op Hallo van Windows server host</span><span class="sxs-lookup"><span data-stu-id="3b05b-142">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="3b05b-143">Start Hallo iSCSI-Initiator op hostserver uit Windows hello.</span><span class="sxs-lookup"><span data-stu-id="3b05b-143">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="3b05b-144">In Hallo **eigenschappen iSCSI-Initiator** venster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="3b05b-144">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="3b05b-145">Klik op Hallo **detectie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3b05b-145">Click hello **Discovery** tab.</span></span>
      
       ![Eigenschappen iSCSI-initiator](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="3b05b-147">Klik op **Portal detecteren**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="3b05b-148">In Hallo **doelportaal detecteren** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="3b05b-148">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="3b05b-149">Hallo IP-adres van uw apparaat opgeven.</span><span class="sxs-lookup"><span data-stu-id="3b05b-149">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="3b05b-150">Klik op **geavanceerde**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-150">Click **Advanced**.</span></span>
      
       ![Doelportaal detecteren](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="3b05b-152">In Hallo **geavanceerde instellingen** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="3b05b-152">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="3b05b-153">Selecteer Hallo **inschakelen CHAP aanmelden** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="3b05b-153">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="3b05b-154">In Hallo **naam** veld, levering Hallo-gebruikersnaam die u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b05b-154">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="3b05b-155">In Hallo **geheim van het doel** veld, geef Hallo wachtwoord dat u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b05b-155">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="3b05b-156">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-156">Click **OK**.</span></span>
      
       ![Geavanceerde instellingen algemeen](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="3b05b-158">Op Hallo **doelen** tabblad Hallo **eigenschappen iSCSI-Initiator** venster Hallo Apparaatstatus moet worden weergegeven als **verbonden**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-158">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="3b05b-159">Als u een 1200 StorSimple-apparaat gebruikt, is elk volume gekoppeld als een iSCSI-doel.</span><span class="sxs-lookup"><span data-stu-id="3b05b-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="3b05b-160">Stap 3 en 4 moet daarom toobe herhaald voor elk volume.</span><span class="sxs-lookup"><span data-stu-id="3b05b-160">Hence, steps 3-4 will need toobe repeated for each volume.</span></span>
   
    ![Volumes die zijn gekoppeld als afzonderlijke doelen](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="3b05b-162">Als u de naam van de iSCSI-Hallo wijzigt, worden de nieuwe naam hello wordt gebruikt voor nieuwe iSCSI-sessies.</span><span class="sxs-lookup"><span data-stu-id="3b05b-162">If you change hello iSCSI name, hello new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="3b05b-163">Nieuwe instellingen worden niet gebruikt voor bestaande sessies totdat u afmelden en aanmelden opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3b05b-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="3b05b-164">Ga te voor meer informatie over het configureren van CHAP op de hostserver voor Windows hello[aanvullende overwegingen](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="3b05b-164">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="3b05b-165">Bidirectionele of wederzijdse verificatie</span><span class="sxs-lookup"><span data-stu-id="3b05b-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="3b05b-166">Hallo doel verifieert Hallo initiator in twee richtingen-verificatie en Hallo initiator verifieert vervolgens Hallo doel.</span><span class="sxs-lookup"><span data-stu-id="3b05b-166">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="3b05b-167">Deze procedure vereist Hallo tooconfigure Hallo CHAP initiator gebruikersinstellingen, omgekeerde CHAP-instellingen op Hallo-apparaat en iSCSI-initiatorsoftware op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="3b05b-167">This procedure requires hello user tooconfigure hello CHAP initiator settings, reverse CHAP settings on hello device, and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="3b05b-168">Hallo volgende procedures beschrijven Hallo stappen tooconfigure wederzijdse verificatie op Hallo-apparaat en op Hallo Windows-host.</span><span class="sxs-lookup"><span data-stu-id="3b05b-168">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="3b05b-169">tooconfigure uw apparaat voor wederzijdse verificatie</span><span class="sxs-lookup"><span data-stu-id="3b05b-169">tooconfigure your device for mutual authentication</span></span>

1. <span data-ttu-id="3b05b-170">Ga in hello Azure-portal, tooyour Apparaatbeheer StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="3b05b-170">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="3b05b-171">Klik op **apparaten** en selecteer een apparaat dat u wenst dat tooconfigure CHAP voor.</span><span class="sxs-lookup"><span data-stu-id="3b05b-171">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="3b05b-172">Ga te**apparaatinstellingen > beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-172">Go too**Device settings > Security**.</span></span> <span data-ttu-id="3b05b-173">In Hallo **beveiligingsinstellingen** blade, klikt u op **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-173">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP-doel](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="3b05b-175">Schuif naar beneden op deze pagina en in Hallo **CHAP Target** sectie:</span><span class="sxs-lookup"><span data-stu-id="3b05b-175">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="3b05b-176">Geef een **omgekeerde CHAP-gebruikersnaam** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="3b05b-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="3b05b-177">Geef een **omgekeerde CHAP-wachtwoord** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="3b05b-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="3b05b-178">Hallo wachtwoord bevestigen.</span><span class="sxs-lookup"><span data-stu-id="3b05b-178">Confirm hello password.</span></span>
3. <span data-ttu-id="3b05b-179">In Hallo **CHAP-Initiator** sectie:</span><span class="sxs-lookup"><span data-stu-id="3b05b-179">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="3b05b-180">Geef een **gebruikersnaam** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="3b05b-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="3b05b-181">Geef een **wachtwoord** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="3b05b-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="3b05b-182">Hallo wachtwoord bevestigen.</span><span class="sxs-lookup"><span data-stu-id="3b05b-182">Confirm hello password.</span></span>

       ![CHAP-Initiator](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="3b05b-184">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-184">Click **Save**.</span></span> <span data-ttu-id="3b05b-185">Er wordt een bevestigingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3b05b-185">A confirmation message is displayed.</span></span> <span data-ttu-id="3b05b-186">Klik op **OK** toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="3b05b-186">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="3b05b-187">tooconfigure bidirectionele verificatie op Hallo van Windows server host</span><span class="sxs-lookup"><span data-stu-id="3b05b-187">tooconfigure bidirectional authentication on hello Windows host server</span></span>

1. <span data-ttu-id="3b05b-188">Start Hallo iSCSI-Initiator op hostserver uit Windows hello.</span><span class="sxs-lookup"><span data-stu-id="3b05b-188">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="3b05b-189">In Hallo **eigenschappen iSCSI-Initiator** venster, klikt u op Hallo **configuratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3b05b-189">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="3b05b-190">Klik op **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="3b05b-191">In Hallo **iSCSI-Initiator wederzijdse CHAP Secret** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="3b05b-191">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="3b05b-192">Type Hallo **omgekeerde CHAP-wachtwoord** die u hebt geconfigureerd in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3b05b-192">Type hello **Reverse CHAP Password** that you configured in hello Azure portal.</span></span>
   2. <span data-ttu-id="3b05b-193">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-193">Click **OK**.</span></span>
      
       ![iSCSI-initiator wederzijdse CHAP-geheim](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="3b05b-195">Klik op Hallo **doelen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="3b05b-195">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="3b05b-196">Klik op Hallo **Connect** knop.</span><span class="sxs-lookup"><span data-stu-id="3b05b-196">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="3b05b-197">In Hallo **verbinding tooTarget** in het dialoogvenster, klikt u op **Geavanceerd**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-197">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="3b05b-198">In Hallo **geavanceerde eigenschappen** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="3b05b-198">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="3b05b-199">Selecteer Hallo **inschakelen CHAP aanmelden** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="3b05b-199">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="3b05b-200">In Hallo **naam** veld, levering Hallo-gebruikersnaam die u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b05b-200">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="3b05b-201">In Hallo **geheim van het doel** veld, geef Hallo wachtwoord dat u hebt opgegeven voor Hallo CHAP-Initiator in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b05b-201">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="3b05b-202">Selecteer Hallo **wederzijdse verificatie uitvoeren** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="3b05b-202">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Geavanceerde instellingen voor wederzijdse verificatie](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="3b05b-204">Klik op **OK** toocomplete Hallo CHAP-configuratie</span><span class="sxs-lookup"><span data-stu-id="3b05b-204">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="3b05b-205">Ga te voor meer informatie over het configureren van CHAP op de hostserver voor Windows hello[aanvullende overwegingen](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="3b05b-205">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="3b05b-206">Aanvullende overwegingen</span><span class="sxs-lookup"><span data-stu-id="3b05b-206">Additional considerations</span></span>

<span data-ttu-id="3b05b-207">Hallo **snelle verbinding** functie biedt geen ondersteuning voor verbindingen waarvoor CHAP ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3b05b-207">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="3b05b-208">Wanneer CHAP is ingeschakeld, zorg ervoor dat u Hallo **Connect** knop die beschikbaar is op Hallo **doelen** tabblad tooconnect tooa doel.</span><span class="sxs-lookup"><span data-stu-id="3b05b-208">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Verbinding maken met tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="3b05b-210">In Hallo **verbinding tooTarget** dialoogvenster dat wordt aangeboden, selecteer Hallo **deze verbinding toohello lijst met favoriete doelen toevoegen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="3b05b-210">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="3b05b-211">Deze selectie zorgt ervoor dat elke keer Hallo computer opnieuw is opgestart, wordt geprobeerd toorestore Hallo verbinding toohello iSCSI-favoriete doelen.</span><span class="sxs-lookup"><span data-stu-id="3b05b-211">This selection ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="3b05b-212">Fouten tijdens het configureren van</span><span class="sxs-lookup"><span data-stu-id="3b05b-212">Errors during configuration</span></span>

<span data-ttu-id="3b05b-213">Als de CHAP-configuratie onjuist is, moet u waarschijnlijk toosee zijn een **verificatiefout** foutbericht.</span><span class="sxs-lookup"><span data-stu-id="3b05b-213">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="3b05b-214">Verificatie van CHAP-configuratie</span><span class="sxs-lookup"><span data-stu-id="3b05b-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="3b05b-215">U kunt controleren dat CHAP wordt gebruikt door Hallo volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3b05b-215">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="3b05b-216">tooverify uw CHAP-configuratie</span><span class="sxs-lookup"><span data-stu-id="3b05b-216">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="3b05b-217">Klik op **favoriete doelen**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="3b05b-218">Selecteer Hallo doel waarvoor verificatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3b05b-218">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="3b05b-219">Klik op **Details**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-219">Click **Details**.</span></span>
   
    ![iSCSI-initiator eigenschappen favoriete doelen](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="3b05b-221">In Hallo **favoriete Doeldetails** in het dialoogvenster vermelding van de opmerking Hallo in Hallo **verificatie** veld.</span><span class="sxs-lookup"><span data-stu-id="3b05b-221">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="3b05b-222">Als is Hallo-configuratie voltooid is, moet spreken **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="3b05b-222">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Details van de favoriet doel](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="3b05b-224">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b05b-224">Next steps</span></span>

* <span data-ttu-id="3b05b-225">Meer informatie over [StorSimple security](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="3b05b-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="3b05b-226">Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="3b05b-226">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

