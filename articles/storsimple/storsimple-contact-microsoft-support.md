---
title: Meld u ondersteuningsticket voor StorSimple 8000 serie | Microsoft Docs
description: Informatie over het maken van een verzoek om ondersteuning en ondersteuningssessie starten op uw StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cecc2566b432e897b5eff0c12e66598f0518ed80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="9cccf-103">Neem contact op met Microsoft ondersteuning voor uw StorSimple</span><span class="sxs-lookup"><span data-stu-id="9cccf-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="9cccf-104">Als u problemen ondervindt met uw Microsoft Azure StorSimple-oplossing, kunt u een serviceaanvraag voor technische ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="9cccf-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="9cccf-105">In een online-sessie met de ondersteuningstechnicus moet u mogelijk ook een support-sessie starten op uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9cccf-105">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="9cccf-106">Dit artikel begeleidt u bij:</span><span class="sxs-lookup"><span data-stu-id="9cccf-106">This article walks you through:</span></span>

* <span data-ttu-id="9cccf-107">Het maken van een aanvraag voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="9cccf-107">How to create a support request.</span></span>
* <span data-ttu-id="9cccf-108">Het starten van een ondersteuningssessie in de Windows PowerShell-interface van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="9cccf-108">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="9cccf-109">Controleer de [StorSimple 8000 Series ondersteuning Sla's en informatie](https://msdn.microsoft.com/library/mt433077.aspx) voordat u een ondersteuningsaanvraag maken.</span><span class="sxs-lookup"><span data-stu-id="9cccf-109">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="9cccf-110">Een ondersteuningsaanvraag maken</span><span class="sxs-lookup"><span data-stu-id="9cccf-110">Create a support request</span></span>
<span data-ttu-id="9cccf-111">Voer de volgende stappen uit om een ondersteuningsaanvraag te maken:</span><span class="sxs-lookup"><span data-stu-id="9cccf-111">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="9cccf-112">Om een ondersteuningsaanvraag te maken</span><span class="sxs-lookup"><span data-stu-id="9cccf-112">To create a support request</span></span>
1. <span data-ttu-id="9cccf-113">In de [klassieke Azure-portal](https://manage.windowsazure.com/), klik op de accountnaam van uw in de rechterbovenhoek en klik vervolgens op **contact opnemen met Microsoft ondersteuning**.</span><span class="sxs-lookup"><span data-stu-id="9cccf-113">In the [Azure classic portal](https://manage.windowsazure.com/), in the upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![Neem contact op met MS ondersteuning via ManagementPortal](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="9cccf-115">U wordt omgeleid naar de nieuwe Azure portal (portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9cccf-115">You will be redirected to the new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="9cccf-116">Klik op de **nieuw ondersteuningsverzoek** tegel.</span><span class="sxs-lookup"><span data-stu-id="9cccf-116">Click the **New support request** tile.</span></span>
   
    ![Neem contact op met MS ondersteuning via de nieuwe portal](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="9cccf-118">Aan de rechterkant van het scherm de **nieuw ondersteuningsverzoek** deelvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9cccf-118">On the right side of the screen, the **New support request** pane appears.</span></span> 
   
    ![Nieuw deelvenster voor ondersteuning aanvragen](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="9cccf-120">In de **basisbeginselen** dialoogvenster Vervolledig de volgende:</span><span class="sxs-lookup"><span data-stu-id="9cccf-120">In the **Basics** dialog box, complete the following:</span></span>                                
   
   1. <span data-ttu-id="9cccf-121">Van de **probleemtype** vervolgkeuzelijst, selecteer **technische**.</span><span class="sxs-lookup"><span data-stu-id="9cccf-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="9cccf-122">Selecteer een **abonnement** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="9cccf-122">Select a **Subscription** from the drop-down list.</span></span>
   3. <span data-ttu-id="9cccf-123">Van de **Service** vervolgkeuzelijst, selecteer **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="9cccf-123">From the **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="9cccf-124">Selecteer een **ondersteuningsplan** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="9cccf-124">Select a **Support plan** from the drop-down list.</span></span> <span data-ttu-id="9cccf-125">U moet een betaald ondersteuningsplan om in te schakelen met technische ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="9cccf-125">You need a paid support plan to enable Technical Support.</span></span>
4. <span data-ttu-id="9cccf-126">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9cccf-126">Click **Next**.</span></span> <span data-ttu-id="9cccf-127">De **probleem** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9cccf-127">The **Problem** dialog box appears.</span></span>
   
    ![Nieuw deelvenster voor ondersteuning aanvragen](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="9cccf-129">In de **probleem** dialoogvenster Vervolledig de volgende:</span><span class="sxs-lookup"><span data-stu-id="9cccf-129">In the **Problem** dialog box, complete the following:</span></span>
   
   1. <span data-ttu-id="9cccf-130">Selecteer een **ernst** niveau uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="9cccf-130">Select a **Severity** level from the drop-down list.</span></span>
   2. <span data-ttu-id="9cccf-131">Selecteer een **probleemtype** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="9cccf-131">Select a **Problem type** from the drop-down list.</span></span>
   3. <span data-ttu-id="9cccf-132">Selecteer een **categorie** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="9cccf-132">Select a **Category** from the drop-down list.</span></span> 
   4. <span data-ttu-id="9cccf-133">In de **Details** vak een korte beschrijving van het probleem.</span><span class="sxs-lookup"><span data-stu-id="9cccf-133">In the **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="9cccf-134">In de **tijdsbestek** vak, geven de datum, tijd en tijdzone die overeenkomt met het meest recente exemplaar van het probleem.</span><span class="sxs-lookup"><span data-stu-id="9cccf-134">In the **Time frame** box, indicate the date, time, and time zone that corresponds to the most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="9cccf-135">Onder **uploaden bestand**, klikt u op het pictogram van de map om te bladeren naar het ondersteuningspakket.</span><span class="sxs-lookup"><span data-stu-id="9cccf-135">Under **File upload**, click the folder icon to browse to your support package.</span></span>
   7. <span data-ttu-id="9cccf-136">Selecteer de **diagnostische gegevens delen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="9cccf-136">Select the **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="9cccf-137">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9cccf-137">Click **Next**.</span></span> <span data-ttu-id="9cccf-138">De **contactgegevens** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9cccf-138">The **Contact information** dialog box appears.</span></span>
   
    ![Nieuw deelvenster voor ondersteuning aanvragen](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="9cccf-140">Voer uw contactgegevens en selecteer een contactmethode (telefoon of e-mail).</span><span class="sxs-lookup"><span data-stu-id="9cccf-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="9cccf-141">Selecteer de **contact op met wijzigingen opslaan voor toekomstige ondersteuningsaanvragen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="9cccf-141">Select the **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="9cccf-142">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9cccf-142">Click **Create**.</span></span>

<span data-ttu-id="9cccf-143">Nadat u uw aanvraag hebt verzonden, een ondersteuningstechnicus neemt contact met u zo snel mogelijk om door te gaan met uw aanvraag.</span><span class="sxs-lookup"><span data-stu-id="9cccf-143">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="9cccf-144">Een support-sessie te starten in Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="9cccf-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="9cccf-145">Voor het oplossen van problemen die u met de StorSimple-apparaat ondervindt mogelijk, moet u het Microsoft Support team benaderen.</span><span class="sxs-lookup"><span data-stu-id="9cccf-145">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="9cccf-146">Microsoft Support moet mogelijk gebruik van een ondersteuningssessie aan te melden op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="9cccf-146">Microsoft Support may need to use a support session to log on to your device.</span></span> 

<span data-ttu-id="9cccf-147">Voer de volgende stappen uit om een ondersteuningssessie te starten:</span><span class="sxs-lookup"><span data-stu-id="9cccf-147">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="9cccf-148">Ondersteuningssessie starten</span><span class="sxs-lookup"><span data-stu-id="9cccf-148">To start a support session</span></span>
1. <span data-ttu-id="9cccf-149">Toegang tot het apparaat via de seriële console of via een Telnet-sessie vanaf een externe computer.</span><span class="sxs-lookup"><span data-stu-id="9cccf-149">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="9cccf-150">Volg hiervoor de stappen in [PuTTY gebruiken om verbinding maken met de seriële console van het apparaat](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="9cccf-150">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="9cccf-151">In de sessie die wordt geopend, drukt u op de **Enter** sleutel om op te halen vanaf de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="9cccf-151">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="9cccf-152">Selecteer in het menu van de seriële console optie 1, **aanmelden met volledige toegang**.</span><span class="sxs-lookup"><span data-stu-id="9cccf-152">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="9cccf-153">Typ het volgende wachtwoord bij de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="9cccf-153">At the prompt, type the following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="9cccf-154">Typ de volgende opdracht bij de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="9cccf-154">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="9cccf-155">U krijgt een gecodeerde tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9cccf-155">An encrypted string will be presented to you.</span></span> <span data-ttu-id="9cccf-156">Kopieer deze tekenreeks in een teksteditor zoals Kladblok.</span><span class="sxs-lookup"><span data-stu-id="9cccf-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="9cccf-157">Bewaar deze tekenreeks en deze in een e-mailbericht verzenden naar Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="9cccf-157">Save this string and send it in an email message to Microsoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9cccf-158">U kunt ondersteuning toegang uitschakelen door het uitvoeren van `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="9cccf-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="9cccf-159">Het StorSimple-apparaat wordt ook geprobeerd om uit te schakelen ondersteuning toegang tot 8 uur nadat de sessie is gestart.</span><span class="sxs-lookup"><span data-stu-id="9cccf-159">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="9cccf-160">Het is een best practice om te wijzigen van de referenties van uw StorSimple-apparaat na het initiëren van een ondersteuningssessie voor.</span><span class="sxs-lookup"><span data-stu-id="9cccf-160">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

