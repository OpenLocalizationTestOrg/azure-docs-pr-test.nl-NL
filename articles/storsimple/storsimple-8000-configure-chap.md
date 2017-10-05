---
title: CHAP configureren voor StorSimple 8000 series apparaat | Microsoft Docs
description: Beschrijft hoe de Challenge Handshake Authentication Protocol (CHAP) configureren op een StorSimple-apparaat.
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
ms.openlocfilehash: 61e0877187759d76b6f7efcef0a5ed8bec8500fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="693b8-103">CHAP configureren voor uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="693b8-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="693b8-104">Deze zelfstudie wordt uitgelegd hoe CHAP configureren voor uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="693b8-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="693b8-105">De procedure beschreven in dit artikel is van toepassing op StorSimple 8000 series apparaten.</span><span class="sxs-lookup"><span data-stu-id="693b8-105">The procedure detailed in this article applies to StorSimple 8000 series devices.</span></span>

<span data-ttu-id="693b8-106">CHAP staat voor Challenge Handshake Authentication Protocol.</span><span class="sxs-lookup"><span data-stu-id="693b8-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="693b8-107">Het is een verificatieschema dat wordt gebruikt door servers om de identiteit van externe clients te valideren.</span><span class="sxs-lookup"><span data-stu-id="693b8-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="693b8-108">De verificatie is gebaseerd op een gedeelde wachtwoord of geheim.</span><span class="sxs-lookup"><span data-stu-id="693b8-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="693b8-109">CHAP mag een manier (Unidirectioneel) of onderlinge (bidirectioneel).</span><span class="sxs-lookup"><span data-stu-id="693b8-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="693b8-110">Een manier CHAP is wanneer het doel een initiator verifieert.</span><span class="sxs-lookup"><span data-stu-id="693b8-110">One way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="693b8-111">Het doel verifieert de initiator in wederzijdse of omgekeerde CHAP, en vervolgens de initiator verifieert het doel.</span><span class="sxs-lookup"><span data-stu-id="693b8-111">In mutual or reverse CHAP, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="693b8-112">Initiator verificatie kan worden geïmplementeerd zonder verificatie doel.</span><span class="sxs-lookup"><span data-stu-id="693b8-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="693b8-113">Doel-verificatie kan echter alleen als de verificatie van de initiator is ook geïmplementeerd worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="693b8-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="693b8-114">Als een best practice is het raadzaam dat u CHAP om iSCSI-beveiliging te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="693b8-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="693b8-115">Houd er rekening mee dat IPSEC wordt momenteel niet ondersteund op het StorSimple-apparaten.</span><span class="sxs-lookup"><span data-stu-id="693b8-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="693b8-116">De CHAP-instellingen op het StorSimple-apparaat kunnen worden geconfigureerd op de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="693b8-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="693b8-117">Unidirectioneel of eenrichtings-verificatie</span><span class="sxs-lookup"><span data-stu-id="693b8-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="693b8-118">Bidirectionele of wederzijdse of reverse-verificatie</span><span class="sxs-lookup"><span data-stu-id="693b8-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="693b8-119">In alle gevallen moet de portal voor het apparaat en de server iSCSI-initiatorsoftware worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="693b8-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="693b8-120">De gedetailleerde stappen voor deze configuratie worden beschreven in de volgende zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="693b8-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="693b8-121">Unidirectioneel of eenrichtings-verificatie</span><span class="sxs-lookup"><span data-stu-id="693b8-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="693b8-122">In één richting verificatie verifieert het doel de initiator.</span><span class="sxs-lookup"><span data-stu-id="693b8-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="693b8-123">Deze verificatie vereist dat u de CHAP-initiator-instellingen op het StorSimple-apparaat en de iSCSI-initiatorsoftware op de host configureren.</span><span class="sxs-lookup"><span data-stu-id="693b8-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="693b8-124">De gedetailleerde procedures voor uw StorSimple-apparaat en de Windows-host worden nu beschreven.</span><span class="sxs-lookup"><span data-stu-id="693b8-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="693b8-125">Uw apparaat voor eenzijdige verificatie configureren</span><span class="sxs-lookup"><span data-stu-id="693b8-125">To configure your device for one-way authentication</span></span>

1. <span data-ttu-id="693b8-126">Ga in de Azure-portal naar uw StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="693b8-126">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="693b8-127">Klik op **apparaten** en selecteer een apparaat dat u wilt CHAP voor configureren.</span><span class="sxs-lookup"><span data-stu-id="693b8-127">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="693b8-128">Ga naar **apparaatinstellingen > beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="693b8-128">Go to **Device settings > Security**.</span></span> <span data-ttu-id="693b8-129">In de **beveiligingsinstellingen** blade, klikt u op **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="693b8-129">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP-Initiator](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="693b8-131">In de **CHAP** blade en in de **CHAP-Initiator** sectie:</span><span class="sxs-lookup"><span data-stu-id="693b8-131">In the **CHAP** blade, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="693b8-132">Geef een gebruikersnaam op voor uw CHAP-initiator.</span><span class="sxs-lookup"><span data-stu-id="693b8-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="693b8-133">Een wachtwoord opgeven voor CHAP-initiator.</span><span class="sxs-lookup"><span data-stu-id="693b8-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="693b8-134">De CHAP-gebruikersnaam moet minder dan 233 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="693b8-134">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="693b8-135">De CHAP-wachtwoord moet tussen 12 en 16 tekens.</span><span class="sxs-lookup"><span data-stu-id="693b8-135">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="693b8-136">Een langer gebruikersnaam of wachtwoord resulteert in een verificatiefout opgetreden op de Windows-host.</span><span class="sxs-lookup"><span data-stu-id="693b8-136">A longer user name or password results in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="693b8-137">Bevestig het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="693b8-137">Confirm the password.</span></span>

       ![CHAP-Initiator](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="693b8-139">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="693b8-139">Click **Save**.</span></span> <span data-ttu-id="693b8-140">Er wordt een bevestigingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="693b8-140">A confirmation message is displayed.</span></span> <span data-ttu-id="693b8-141">Klik op **OK** om de wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="693b8-141">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="693b8-142">Eenzijdige verificatie configureren op de host WindowsServer</span><span class="sxs-lookup"><span data-stu-id="693b8-142">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="693b8-143">Start de iSCSI-Initiator op de host WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="693b8-143">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="693b8-144">In de **eigenschappen iSCSI-Initiator** venster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="693b8-144">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="693b8-145">Klik op de **detectie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="693b8-145">Click the **Discovery** tab.</span></span>
      
       ![Eigenschappen iSCSI-initiator](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="693b8-147">Klik op **Portal detecteren**.</span><span class="sxs-lookup"><span data-stu-id="693b8-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="693b8-148">In de **doelportaal detecteren** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="693b8-148">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="693b8-149">Geef het IP-adres van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="693b8-149">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="693b8-150">Klik op **geavanceerde**.</span><span class="sxs-lookup"><span data-stu-id="693b8-150">Click **Advanced**.</span></span>
      
       ![Doelportaal detecteren](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="693b8-152">In de **geavanceerde instellingen** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="693b8-152">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="693b8-153">Selecteer de **inschakelen CHAP aanmelden** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="693b8-153">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="693b8-154">In de **naam** veld, geef de gebruikersnaam die u hebt opgegeven voor de CHAP-Initiator in de klassieke portal.</span><span class="sxs-lookup"><span data-stu-id="693b8-154">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="693b8-155">In de **geheim van het doel** veld, het wachtwoord die u hebt opgegeven voor de CHAP-Initiator in de klassieke portal opgeven.</span><span class="sxs-lookup"><span data-stu-id="693b8-155">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="693b8-156">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="693b8-156">Click **OK**.</span></span>
      
       ![Geavanceerde instellingen algemeen](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="693b8-158">Op de **doelen** tabblad van de **eigenschappen iSCSI-Initiator** venster status van het apparaat moet worden weergegeven als **verbonden**.</span><span class="sxs-lookup"><span data-stu-id="693b8-158">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="693b8-159">Als u een 1200 StorSimple-apparaat gebruikt, is elk volume gekoppeld als een iSCSI-doel.</span><span class="sxs-lookup"><span data-stu-id="693b8-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="693b8-160">Stap 3 en 4 moet daarom worden herhaald voor elk volume.</span><span class="sxs-lookup"><span data-stu-id="693b8-160">Hence, steps 3-4 will need to be repeated for each volume.</span></span>
   
    ![Volumes die zijn gekoppeld als afzonderlijke doelen](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="693b8-162">Als u de naam van de iSCSI-wijzigt, worden de nieuwe naam wordt gebruikt voor nieuwe iSCSI-sessies.</span><span class="sxs-lookup"><span data-stu-id="693b8-162">If you change the iSCSI name, the new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="693b8-163">Nieuwe instellingen worden niet gebruikt voor bestaande sessies totdat u afmelden en aanmelden opnieuw.</span><span class="sxs-lookup"><span data-stu-id="693b8-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="693b8-164">Voor meer informatie over het configureren van CHAP op de host WindowsServer, gaat u naar [aanvullende overwegingen](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="693b8-164">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="693b8-165">Bidirectionele of wederzijdse verificatie</span><span class="sxs-lookup"><span data-stu-id="693b8-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="693b8-166">Het doel verifieert de initiator in twee richtingen verificatie, en vervolgens de initiator verifieert het doel.</span><span class="sxs-lookup"><span data-stu-id="693b8-166">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="693b8-167">Deze procedure moet de gebruiker de CHAP-initiator configureren, omgekeerde CHAP-instellingen op het apparaat en iSCSI-initiatorsoftware is op de host.</span><span class="sxs-lookup"><span data-stu-id="693b8-167">This procedure requires the user to configure the CHAP initiator settings, reverse CHAP settings on the device, and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="693b8-168">De volgende procedures beschrijven de stappen voor het configureren van wederzijdse verificatie op het apparaat en op de Windows-host.</span><span class="sxs-lookup"><span data-stu-id="693b8-168">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="693b8-169">Om uw apparaat voor wederzijdse verificatie te configureren</span><span class="sxs-lookup"><span data-stu-id="693b8-169">To configure your device for mutual authentication</span></span>

1. <span data-ttu-id="693b8-170">Ga in de Azure-portal naar uw StorSimple-apparaat Manager-service.</span><span class="sxs-lookup"><span data-stu-id="693b8-170">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="693b8-171">Klik op **apparaten** en selecteer een apparaat dat u wilt CHAP voor configureren.</span><span class="sxs-lookup"><span data-stu-id="693b8-171">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="693b8-172">Ga naar **apparaatinstellingen > beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="693b8-172">Go to **Device settings > Security**.</span></span> <span data-ttu-id="693b8-173">In de **beveiligingsinstellingen** blade, klikt u op **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="693b8-173">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP-doel](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="693b8-175">Schuif naar beneden op deze pagina en in de **CHAP Target** sectie:</span><span class="sxs-lookup"><span data-stu-id="693b8-175">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="693b8-176">Geef een **omgekeerde CHAP-gebruikersnaam** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="693b8-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="693b8-177">Geef een **omgekeerde CHAP-wachtwoord** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="693b8-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="693b8-178">Bevestig het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="693b8-178">Confirm the password.</span></span>
3. <span data-ttu-id="693b8-179">In de **CHAP-Initiator** sectie:</span><span class="sxs-lookup"><span data-stu-id="693b8-179">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="693b8-180">Geef een **gebruikersnaam** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="693b8-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="693b8-181">Geef een **wachtwoord** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="693b8-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="693b8-182">Bevestig het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="693b8-182">Confirm the password.</span></span>

       ![CHAP-Initiator](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="693b8-184">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="693b8-184">Click **Save**.</span></span> <span data-ttu-id="693b8-185">Er wordt een bevestigingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="693b8-185">A confirmation message is displayed.</span></span> <span data-ttu-id="693b8-186">Klik op **OK** om de wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="693b8-186">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="693b8-187">Bidirectionele verificatie configureren op de host WindowsServer</span><span class="sxs-lookup"><span data-stu-id="693b8-187">To configure bidirectional authentication on the Windows host server</span></span>

1. <span data-ttu-id="693b8-188">Start de iSCSI-Initiator op de host WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="693b8-188">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="693b8-189">In de **eigenschappen iSCSI-Initiator** venster, klikt u op de **configuratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="693b8-189">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="693b8-190">Klik op **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="693b8-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="693b8-191">In de **iSCSI-Initiator wederzijdse CHAP Secret** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="693b8-191">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="693b8-192">Typ de **omgekeerde CHAP-wachtwoord** die u hebt geconfigureerd in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="693b8-192">Type the **Reverse CHAP Password** that you configured in the Azure portal.</span></span>
   2. <span data-ttu-id="693b8-193">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="693b8-193">Click **OK**.</span></span>
      
       ![iSCSI-initiator wederzijdse CHAP-geheim](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="693b8-195">Klik op de **doelen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="693b8-195">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="693b8-196">Klik op de **Connect** knop.</span><span class="sxs-lookup"><span data-stu-id="693b8-196">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="693b8-197">In de **verbinding naar doel** in het dialoogvenster, klikt u op **Geavanceerd**.</span><span class="sxs-lookup"><span data-stu-id="693b8-197">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="693b8-198">In de **geavanceerde eigenschappen** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="693b8-198">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="693b8-199">Selecteer de **inschakelen CHAP aanmelden** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="693b8-199">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="693b8-200">In de **naam** veld, geef de gebruikersnaam die u hebt opgegeven voor de CHAP-Initiator in de klassieke portal.</span><span class="sxs-lookup"><span data-stu-id="693b8-200">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="693b8-201">In de **geheim van het doel** veld, het wachtwoord die u hebt opgegeven voor de CHAP-Initiator in de klassieke portal opgeven.</span><span class="sxs-lookup"><span data-stu-id="693b8-201">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="693b8-202">Selecteer de **wederzijdse verificatie uitvoeren** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="693b8-202">Select the **Perform mutual authentication** check box.</span></span>
      
       ![Geavanceerde instellingen voor wederzijdse verificatie](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="693b8-204">Klik op **OK** de CHAP-configuratie voltooien</span><span class="sxs-lookup"><span data-stu-id="693b8-204">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="693b8-205">Voor meer informatie over het configureren van CHAP op de host WindowsServer, gaat u naar [aanvullende overwegingen](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="693b8-205">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="693b8-206">Aanvullende overwegingen</span><span class="sxs-lookup"><span data-stu-id="693b8-206">Additional considerations</span></span>

<span data-ttu-id="693b8-207">De **snelle verbinding** functie biedt geen ondersteuning voor verbindingen waarvoor CHAP ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="693b8-207">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="693b8-208">Wanneer CHAP is ingeschakeld, zorg ervoor dat u de **Connect** knop die beschikbaar is op de **doelen** tabblad verbinding maken met een doel.</span><span class="sxs-lookup"><span data-stu-id="693b8-208">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![Verbinding maken met doel](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="693b8-210">In de **verbinding maken met doel** in het dialoogvenster wordt weergegeven, selecteer de **deze verbinding toevoegen aan de lijst met favoriete doelen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="693b8-210">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="693b8-211">Deze selectie zorgt ervoor dat elke keer dat de computer opnieuw is opgestart, wordt geprobeerd de verbinding te herstellen met de favoriete iSCSI-doelen.</span><span class="sxs-lookup"><span data-stu-id="693b8-211">This selection ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="693b8-212">Fouten tijdens het configureren van</span><span class="sxs-lookup"><span data-stu-id="693b8-212">Errors during configuration</span></span>

<span data-ttu-id="693b8-213">Als de CHAP-configuratie onjuist is, wordt u ziet er waarschijnlijk een **verificatiefout** foutbericht.</span><span class="sxs-lookup"><span data-stu-id="693b8-213">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="693b8-214">Verificatie van CHAP-configuratie</span><span class="sxs-lookup"><span data-stu-id="693b8-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="693b8-215">U kunt controleren dat CHAP wordt gebruikt door de volgende stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="693b8-215">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="693b8-216">De CHAP-configuratie controleren</span><span class="sxs-lookup"><span data-stu-id="693b8-216">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="693b8-217">Klik op **favoriete doelen**.</span><span class="sxs-lookup"><span data-stu-id="693b8-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="693b8-218">Selecteer het doelobject op waarvoor verificatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="693b8-218">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="693b8-219">Klik op **Details**.</span><span class="sxs-lookup"><span data-stu-id="693b8-219">Click **Details**.</span></span>
   
    ![iSCSI-initiator eigenschappen favoriete doelen](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="693b8-221">In de **favoriete Doeldetails** dialoogvenster Noteer de vermelding in de **verificatie** veld.</span><span class="sxs-lookup"><span data-stu-id="693b8-221">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="693b8-222">Als wordt de configuratie voltooid is, moet spreken **CHAP**.</span><span class="sxs-lookup"><span data-stu-id="693b8-222">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![Details van de favoriet doel](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="693b8-224">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="693b8-224">Next steps</span></span>

* <span data-ttu-id="693b8-225">Meer informatie over [StorSimple security](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="693b8-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="693b8-226">Meer informatie over [de service Manager voor StorSimple-apparaat gebruiken voor het beheer van uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="693b8-226">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

