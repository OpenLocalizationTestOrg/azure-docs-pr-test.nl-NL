---
title: aaaYou geen toegang vanaf nu Hallo van een apparaat met Windows Azure-portal | Microsoft Docs
description: Meer informatie over waar u kunt geen get er hier vandaan en wat u tooavoid die worden uitgevoerd in dit dialoogvenster kan controleren.
services: active-directory
keywords: voorwaardelijke toegang op basis van een apparaat, apparaatregistratie, apparaatregistratie inschakelen, apparaatregistratie en MDM
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="b66d5-104">U kunt daar niet komen vanaf deze locatie op een Windows-apparaat</span><span class="sxs-lookup"><span data-stu-id="b66d5-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="b66d5-105">Tijdens een poging om bijvoorbeeld het SharePoint Online-intranet van uw organisatie te openen, krijgt u een pagina te zien waarop staat dat *u geen toegang hebt*.</span><span class="sxs-lookup"><span data-stu-id="b66d5-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="b66d5-106">U ziet deze pagina omdat de beheerder een beleid voor voorwaardelijke toegang waardoor toegang tooyour organisatie resources onder bepaalde omstandigheden heeft geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b66d5-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access tooyour organization's resources under certain conditions.</span></span> <span data-ttu-id="b66d5-107">Het is mogelijk noodzakelijk toocontact helpdesk of uw beheerder tooget dit probleem is opgelost, maar er zijn een aantal dingen die u zelf eerst uitproberen kunt.</span><span class="sxs-lookup"><span data-stu-id="b66d5-107">While it might be necessary toocontact helpdesk or your administrator tooget this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="b66d5-108">Als u een **Windows** apparaat, moet u Hallo volgende controleren:</span><span class="sxs-lookup"><span data-stu-id="b66d5-108">If you are using a **Windows** device, you should check hello following:</span></span>

- <span data-ttu-id="b66d5-109">Gebruikt u een ondersteunde browser?</span><span class="sxs-lookup"><span data-stu-id="b66d5-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="b66d5-110">Voert u een ondersteunde versie van Windows uit op het apparaat?</span><span class="sxs-lookup"><span data-stu-id="b66d5-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="b66d5-111">Is het apparaat compatibel?</span><span class="sxs-lookup"><span data-stu-id="b66d5-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="b66d5-112">Ondersteunde browser</span><span class="sxs-lookup"><span data-stu-id="b66d5-112">Supported browser</span></span>

<span data-ttu-id="b66d5-113">Als de beheerder voorwaardelijk toegangsbeleid heeft geconfigureerd, hebt u alleen toegang tot de resources van uw organisatie vanaf een ondersteunde browser.</span><span class="sxs-lookup"><span data-stu-id="b66d5-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="b66d5-114">Op een Windows-apparaat worden alleen **Internet Explorer** en **Edge** ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b66d5-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="b66d5-115">U kunt eenvoudig bepalen of u geen toegang een resource vanwege niet-ondersteunde browser tooan tot door te kijken gedeelte van de Hallo details van de foutpagina Hallo:</span><span class="sxs-lookup"><span data-stu-id="b66d5-115">You can easily identify whether you can't access a resource due tooan unsupported browser by looking at hello details section of hello error page:</span></span>

<span data-ttu-id="b66d5-116">![Scenario](./media/active-directory-conditional-access-device-remediation/02.png "Berichten over ontoegankelijke toepassingen voor niet-ondersteunde browsers")</span><span class="sxs-lookup"><span data-stu-id="b66d5-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="b66d5-117">Hallo alleen herstel is toouse een browser die de toepassing hello ondersteuning voor uw apparaatplatform biedt.</span><span class="sxs-lookup"><span data-stu-id="b66d5-117">hello only remediation is toouse a browser that hello application supports for your device platform.</span></span> <span data-ttu-id="b66d5-118">Zie [Ondersteunde browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies) voor een volledige lijst met ondersteunde browsers.</span><span class="sxs-lookup"><span data-stu-id="b66d5-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="b66d5-119">Ondersteunde versies van Windows</span><span class="sxs-lookup"><span data-stu-id="b66d5-119">Supported versions of Windows</span></span>

<span data-ttu-id="b66d5-120">Hallo volgende moet worden voldaan over Hallo Windows-besturingssysteem op uw apparaat zijn:</span><span class="sxs-lookup"><span data-stu-id="b66d5-120">hello following must be true about hello Windows operating system on your device:</span></span> 

- <span data-ttu-id="b66d5-121">Als u een besturingssysteem voor Windows-bureaublad op uw apparaat uitvoert, moet deze toobe Windows 7 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b66d5-121">If you are running a Windows desktop operating system on your device, it needs toobe Windows 7 or later.</span></span>
- <span data-ttu-id="b66d5-122">Als u een Windows server-besturingssysteem op uw apparaat uitvoert, moet deze toobe Windows Server 2008 R2 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b66d5-122">If you are running a Windows server operating system on your device, it needs toobe Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="b66d5-123">Compatibel apparaat</span><span class="sxs-lookup"><span data-stu-id="b66d5-123">Compliant device</span></span>

<span data-ttu-id="b66d5-124">Mogelijk heeft de beheerder een beleid voor voorwaardelijke toegang kunnen resources alleen via compatibele apparaten toegang tooyour organisatie geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b66d5-124">Your administrator might have configured a conditional access policy that allows access tooyour organization's resources only from compliant devices.</span></span> <span data-ttu-id="b66d5-125">compatibel zijn, moet uw apparaat beide gekoppelde tooyour toobe on-premises Active Directory of die lid zijn van tooyour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b66d5-125">toobe compliant, your device must be either joined tooyour on-premises Active Directory or joined tooyour Azure Active Directory.</span></span>

<span data-ttu-id="b66d5-126">U kunt eenvoudig bepalen of u geen toegang tot een resource vanwege tooa-apparaat dat is niet compatibel met door te kijken gedeelte van de Hallo details van de foutpagina Hallo:</span><span class="sxs-lookup"><span data-stu-id="b66d5-126">You can easily identify whether you can't access a resource due tooa device that is not compliant by looking at hello details section of hello error page:</span></span>
 
<span data-ttu-id="b66d5-127">![Scenario](./media/active-directory-conditional-access-device-remediation/01.png "Berichten over ontoegankelijke toepassingen voor niet-geregistreerde apparaten")</span><span class="sxs-lookup"><span data-stu-id="b66d5-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="b66d5-128">Is uw apparaat lid tooan op lokale Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b66d5-128">Is your device joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="b66d5-129">**Als uw apparaat is toegevoegd tooan op lokale Active Directory in uw organisatie:**</span><span class="sxs-lookup"><span data-stu-id="b66d5-129">**If your device is joined tooan on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="b66d5-130">Zorg ervoor dat u zich aanmelden tooWindows met behulp van uw werkaccount (uw Active Directory-account).</span><span class="sxs-lookup"><span data-stu-id="b66d5-130">Make sure that you sign in tooWindows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="b66d5-131">Verbinding maken met bedrijfsnetwerk via een virtueel particulier netwerk (VPN) of DirectAccess tooyour.</span><span class="sxs-lookup"><span data-stu-id="b66d5-131">Connect tooyour corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="b66d5-132">Nadat u verbonden bent, drukt u op Hallo Windows-logotoets + L Hallo sleutel toolock uw Windows-sessie.</span><span class="sxs-lookup"><span data-stu-id="b66d5-132">After you are connected, press hello Windows logo key + hello L key toolock your Windows session.</span></span>
4. <span data-ttu-id="b66d5-133">Ontgrendel de Windows-sessie door de referenties voor uw werkaccount in te voeren.</span><span class="sxs-lookup"><span data-stu-id="b66d5-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="b66d5-134">Wacht een paar minuten en probeer het vervolgens opnieuw tooaccess Hallo toepassing of service.</span><span class="sxs-lookup"><span data-stu-id="b66d5-134">Wait for a minute, and then try again tooaccess hello application or service.</span></span>
6. <span data-ttu-id="b66d5-135">Als u dezelfde Hallo pagina, klikt u op Hallo **meer details** koppelen en vervolgens contact op met uw beheerder met Hallo details.</span><span class="sxs-lookup"><span data-stu-id="b66d5-135">If you see hello same page, click hello **More details** link, and then contact your administrator with hello details.</span></span>


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="b66d5-136">Is uw apparaat geen lid zijn van tooan op lokale Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b66d5-136">Is your device not joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="b66d5-137">Als uw apparaat niet is gekoppeld tooan on-premises Active Directory en Windows 10 wordt uitgevoerd, hebt u twee opties:</span><span class="sxs-lookup"><span data-stu-id="b66d5-137">If your device is not joined tooan on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="b66d5-138">Azure AD Join uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b66d5-138">Run Azure AD Join</span></span>
* <span data-ttu-id="b66d5-139">Toevoegen van uw werk of school account tooWindows</span><span class="sxs-lookup"><span data-stu-id="b66d5-139">Add your work or school account tooWindows</span></span>

<span data-ttu-id="b66d5-140">Zie [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md) (Windows 10-apparaten gebruiken op uw werkplek) voor informatie over de verschillen tussen deze opties.</span><span class="sxs-lookup"><span data-stu-id="b66d5-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="b66d5-141">Als het apparaat:</span><span class="sxs-lookup"><span data-stu-id="b66d5-141">If your device:</span></span>

- <span data-ttu-id="b66d5-142">Tooyour organisatie hoort, moet u Azure AD Join uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b66d5-142">Belongs tooyour organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="b66d5-143">Is een persoonlijk apparaat of een Windows phone, moet u toevoegen van uw werk of school account tooWindows</span><span class="sxs-lookup"><span data-stu-id="b66d5-143">Is a personal device or a Windows phone, you should add your work or school account tooWindows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="b66d5-144">Azure AD Join op Windows 10</span><span class="sxs-lookup"><span data-stu-id="b66d5-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="b66d5-145">Hallo stappen toojoin uw apparaat tooAzure AD zijn gekoppeld Hallo-versie van Windows 10 u erop worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b66d5-145">hello steps toojoin your device tooAzure AD are tied hello version of Windows 10 you are running on it.</span></span> <span data-ttu-id="b66d5-146">toodetermine hello versie van het besturingssysteem Windows 10 uitvoeren Hallo **winver** opdracht:</span><span class="sxs-lookup"><span data-stu-id="b66d5-146">toodetermine hello version of your Windows 10 operating system, run hello **winver** command:</span></span> 

![Windows-versie](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="b66d5-148">**Windows 10 Jubileumupdate (versie 1607)**</span><span class="sxs-lookup"><span data-stu-id="b66d5-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="b66d5-149">Open Hallo **instellingen** app.</span><span class="sxs-lookup"><span data-stu-id="b66d5-149">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="b66d5-150">Klik op **Accounts** > **Toegang via werk of school**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="b66d5-151">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-151">Click **Connect**.</span></span>
4. <span data-ttu-id="b66d5-152">Klik op **deelnemen aan dit apparaat tooAzure AD**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-152">Click **Join this device tooAzure AD**.</span></span>
5. <span data-ttu-id="b66d5-153">Tooyour organisatie verifiëren, bieden meervoudige verificatie als u wordt gevraagd en volg Hallo-stappen die worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b66d5-153">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
6. <span data-ttu-id="b66d5-154">Meld u af en meld u weer aan met uw werkaccount.</span><span class="sxs-lookup"><span data-stu-id="b66d5-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="b66d5-155">Probeer het opnieuw tooaccess Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b66d5-155">Try again tooaccess hello application.</span></span>

<span data-ttu-id="b66d5-156">**Windows 10-update van november 2015 (versie 1511):**</span><span class="sxs-lookup"><span data-stu-id="b66d5-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="b66d5-157">Open Hallo **instellingen** app.</span><span class="sxs-lookup"><span data-stu-id="b66d5-157">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="b66d5-158">Klik op **Systeem** > **Info**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="b66d5-159">Klik op **Lid worden van Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="b66d5-160">Tooyour organisatie verifiëren, bieden meervoudige verificatie als u wordt gevraagd en volg Hallo-stappen die worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b66d5-160">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="b66d5-161">Meld u af en meld u weer aan met uw werkaccount (uw Azure AD-account).</span><span class="sxs-lookup"><span data-stu-id="b66d5-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="b66d5-162">Probeer het opnieuw tooaccess Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b66d5-162">Try again tooaccess hello application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="b66d5-163">Workplace Join op Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="b66d5-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="b66d5-164">Als uw apparaat geen lid van een domein is- en Windows 8.1, toodo wordt uitgevoerd een werkplek koppelen en in Microsoft Intune inschrijven, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b66d5-164">If your device is not domain-joined and runs Windows 8.1, toodo a Workplace Join and enroll in Microsoft Intune, do hello following steps:</span></span>

1. <span data-ttu-id="b66d5-165">Open **Pc-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="b66d5-166">Klik op **Netwerk** > **Werkplek**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="b66d5-167">Klik op **Deelnemen**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-167">Click **Join**.</span></span>
4. <span data-ttu-id="b66d5-168">Tooyour organisatie verifiëren, bieden meervoudige verificatie als u wordt gevraagd en volg Hallo-stappen die worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b66d5-168">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="b66d5-169">Klik op **Inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="b66d5-170">Probeer het opnieuw tooaccess Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b66d5-170">Try again tooaccess hello application.</span></span>



#### <a name="add-your-work-or-school-account-toowindows"></a><span data-ttu-id="b66d5-171">Toevoegen van uw werk of school account tooWindows</span><span class="sxs-lookup"><span data-stu-id="b66d5-171">Add your work or school account tooWindows</span></span> 


<span data-ttu-id="b66d5-172">**Windows 10 Jubileumupdate (versie 1607)**</span><span class="sxs-lookup"><span data-stu-id="b66d5-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="b66d5-173">Open Hallo **instellingen** app.</span><span class="sxs-lookup"><span data-stu-id="b66d5-173">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="b66d5-174">Klik op **Accounts** > **Toegang via werk of school**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="b66d5-175">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-175">Click **Connect**.</span></span>
4. <span data-ttu-id="b66d5-176">Tooyour organisatie verifiëren, bieden meervoudige verificatie als u wordt gevraagd en volg Hallo-stappen die worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b66d5-176">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="b66d5-177">Probeer het opnieuw tooaccess Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b66d5-177">Try again tooaccess hello application.</span></span>


<span data-ttu-id="b66d5-178">**Windows 10-update van november 2015 (versie 1511):**</span><span class="sxs-lookup"><span data-stu-id="b66d5-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="b66d5-179">Open Hallo **instellingen** app.</span><span class="sxs-lookup"><span data-stu-id="b66d5-179">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="b66d5-180">Klik op **Accounts** > **Uw accounts**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="b66d5-181">Klik op **Werk- of schoolaccount toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b66d5-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="b66d5-182">Tooyour organisatie verifiëren, bieden meervoudige verificatie als u wordt gevraagd en volg Hallo-stappen die worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b66d5-182">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="b66d5-183">Probeer het opnieuw tooaccess Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b66d5-183">Try again tooaccess hello application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="b66d5-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b66d5-184">Next steps</span></span>
[<span data-ttu-id="b66d5-185">Voorwaardelijke toegang van Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b66d5-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

