---
title: 'aaaAzure Active Directory: Identity Protection playbook | Microsoft Docs'
description: Meer informatie over hoe Azure AD Identity Protection kunt u toolimit Hallo mogelijkheid van een aanvaller tooexploit de identiteit van een verdachte of apparaat en toosecure een identiteit of een apparaat dat eerder verdachte of bekende toobe aangetast.
services: active-directory
keywords: beveiliging in Azure active directory-identiteit, cloud app discovery, het beheren van toepassingen, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="28876-104">Playbook voor Azure Active Directory: Identity Protection</span><span class="sxs-lookup"><span data-stu-id="28876-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="28876-105">Deze playbook helpt u bij:</span><span class="sxs-lookup"><span data-stu-id="28876-105">This playbook helps you to:</span></span>

* <span data-ttu-id="28876-106">Gegevens in Hallo Identity Protection omgeving door simulating risicogebeurtenissen en beveiligingsproblemen vullen</span><span class="sxs-lookup"><span data-stu-id="28876-106">Populate data in hello Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="28876-107">Instellen van beleidsregels voor voorwaardelijke toegang op basis van risico's en Hallo gevolgen van het beleid testen</span><span class="sxs-lookup"><span data-stu-id="28876-107">Set up risk-based conditional access policies and test hello impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="28876-108">Risico's te simuleren</span><span class="sxs-lookup"><span data-stu-id="28876-108">Simulating Risk Events</span></span>
<span data-ttu-id="28876-109">Deze sectie bevat met de stappen voor het simuleren Hallo gebeurtenistypen risico's te volgen:</span><span class="sxs-lookup"><span data-stu-id="28876-109">This section provides you with steps for simulating hello following risk event types:</span></span>

* <span data-ttu-id="28876-110">Aanmeldingen vanaf anonieme IP-adressen (eenvoudig)</span><span class="sxs-lookup"><span data-stu-id="28876-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="28876-111">Aanmeldingen vanaf onbekende locaties (gemiddeld)</span><span class="sxs-lookup"><span data-stu-id="28876-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="28876-112">Onmogelijke reis tooatypical locaties (moeilijk)</span><span class="sxs-lookup"><span data-stu-id="28876-112">Impossible travel tooatypical locations (difficult)</span></span>

<span data-ttu-id="28876-113">Andere risicogebeurtenissen kunnen niet op een veilige manier worden gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="28876-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="28876-114">Aanmeldingen vanaf anonieme IP-adressen</span><span class="sxs-lookup"><span data-stu-id="28876-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="28876-115">Dit type risico gebeurtenis identificeert gebruikers die zich heeft aangemeld vanaf een IP-adres dat is geïdentificeerd als een anonieme proxy IP-adres.</span><span class="sxs-lookup"><span data-stu-id="28876-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="28876-116">Deze proxy's worden gebruikt door mensen willen toohide van hun apparaat IP-adres en kan worden gebruikt voor kwade bedoelingen.</span><span class="sxs-lookup"><span data-stu-id="28876-116">These proxies are used by people who want toohide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="28876-117">**toosimulate een aanmeldingspagina van een anoniem IP uitvoeren Hallo stappen te volgen**:</span><span class="sxs-lookup"><span data-stu-id="28876-117">**toosimulate a sign-in from an anonymous IP, perform hello following steps**:</span></span>

1. <span data-ttu-id="28876-118">Hallo downloaden [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="28876-118">Download hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="28876-119">Hallo Tor Browser, navigeer te[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="28876-119">Using hello Tor Browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="28876-120">Geef referenties op Hallo van de gewenste tooappear in Hallo Hallo-account **aanmeldingen vanaf anonieme IP-adressen** rapport.</span><span class="sxs-lookup"><span data-stu-id="28876-120">Enter hello credentials of hello account you want tooappear in hello **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="28876-121">Hallo-aanmeldingspagina wordt weergegeven op Hallo Identity Protection-dashboard binnen 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="28876-121">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="28876-122">Aanmeldingen vanaf onbekende locaties</span><span class="sxs-lookup"><span data-stu-id="28876-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="28876-123">Hallo onbekende locaties risico is een realtime aanmelden evaluatiemechanisme dat uit het verleden aanmelden locaties overweegt (IP, breedtegraad / lengtegraad en ASN) toodetermine nieuwe / onbekende locaties.</span><span class="sxs-lookup"><span data-stu-id="28876-123">hello unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) toodetermine new / unfamiliar locations.</span></span> <span data-ttu-id="28876-124">Hallo opgeslagen vorige IP-adressen, de breedtegraad / lengtegraad en ASN's van een gebruiker en deze vertrouwde locaties toobe wordt beschouwd.</span><span class="sxs-lookup"><span data-stu-id="28876-124">hello system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these toobe familiar locations.</span></span> <span data-ttu-id="28876-125">Een locatie aanmelden wordt beschouwd als niet bekend als hello aanmelden locatie komt niet overeen met een van de bestaande vertrouwde locaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="28876-125">A sign-in location is considered unfamiliar if hello sign-in location does not match any of hello existing familiar locations.</span></span>

<span data-ttu-id="28876-126">Beveiliging van Azure Active Directory-identiteit:</span><span class="sxs-lookup"><span data-stu-id="28876-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="28876-127">heeft een initiële learning periode van 14 dagen aan waarover biedt het geen nieuwe locaties als onbekende locaties vlag.</span><span class="sxs-lookup"><span data-stu-id="28876-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="28876-128">aanmeldingen vanaf bekende apparaten en de locaties die geografisch sluiten tooan bestaande vertrouwde locatie worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="28876-128">ignores sign-ins from familiar devices and locations that are geographically close tooan existing familiar location.</span></span>

<span data-ttu-id="28876-129">Onbekende locaties toosimulate, hebt u toosign vanaf een locatie en het apparaat dat Hallo-account is niet aangemeld uit voordat in.</span><span class="sxs-lookup"><span data-stu-id="28876-129">toosimulate unfamiliar locations, you have toosign in from a location and device that hello account has not signed in from before.</span></span> 

<span data-ttu-id="28876-130">**toosimulate een aanmelden vanaf een onbekend locatie uitvoeren Hallo stappen te volgen**:</span><span class="sxs-lookup"><span data-stu-id="28876-130">**toosimulate a sign-in from an unfamiliar location, perform hello following steps**:</span></span>

1. <span data-ttu-id="28876-131">Kies een account met ten minste een geschiedenis van de aanmeldingspagina 14 dagen.</span><span class="sxs-lookup"><span data-stu-id="28876-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="28876-132">Doen:</span><span class="sxs-lookup"><span data-stu-id="28876-132">Do either:</span></span>
   
   <span data-ttu-id="28876-133">a.</span><span class="sxs-lookup"><span data-stu-id="28876-133">a.</span></span> <span data-ttu-id="28876-134">Tijdens het gebruik van een VPN te navigeren[https://myapps.microsoft.com](https://myapps.microsoft.com) en geef referenties op Hallo van de gewenste toosimulate Hallo risicogebeurtenis voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="28876-134">While using a VPN, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com) and enter hello credentials of hello account you want toosimulate hello risk event for.</span></span>
   
   <span data-ttu-id="28876-135">b.</span><span class="sxs-lookup"><span data-stu-id="28876-135">b.</span></span> <span data-ttu-id="28876-136">Vraag een koppelen in een andere locatie toosign aan met referenties van Hallo-account (niet aanbevolen).</span><span class="sxs-lookup"><span data-stu-id="28876-136">Ask an associate in a different location toosign in using hello account’s credentials (not recommended).</span></span>

<span data-ttu-id="28876-137">Hallo-aanmeldingspagina wordt weergegeven op Hallo Identity Protection-dashboard binnen 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="28876-137">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-tooatypical-location"></a><span data-ttu-id="28876-138">Onmogelijke reis tooatypical locatie</span><span class="sxs-lookup"><span data-stu-id="28876-138">Impossible travel tooatypical location</span></span>
<span data-ttu-id="28876-139">Hallo onmogelijke reis voorwaarde simuleren is moeilijk omdat Hallo-algoritme maakt gebruik van machine learning tooweed uit ONWAAR-positieven zoals onmogelijke reis vanaf vertrouwde apparaten of aanmeldingen van VPN-verbindingen die door andere gebruikers in de directory hello worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="28876-139">Simulating hello impossible travel condition is difficult because hello algorithm uses machine learning tooweed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in hello directory.</span></span> <span data-ttu-id="28876-140">Hallo-algoritme worden een geschiedenis aanmelden van 3 dagen van de too14 moet voor Hallo gebruiker voordat u begint deze risico's te genereren.</span><span class="sxs-lookup"><span data-stu-id="28876-140">Additionally, hello algorithm requires a sign-in history of 3 too14 days for hello user before it begins generating risk events.</span></span>

<span data-ttu-id="28876-141">**een locatie van de tooatypical onmogelijke reis toosimulate uitvoeren Hallo stappen te volgen**:</span><span class="sxs-lookup"><span data-stu-id="28876-141">**toosimulate an impossible travel tooatypical location, perform hello following steps**:</span></span>

1. <span data-ttu-id="28876-142">Met behulp van de standaardbrowser te navigeren[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="28876-142">Using your standard browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="28876-143">Geef referenties op Hallo van Hallo account toogenerate een gebeurtenis onmogelijke reis risico voor.</span><span class="sxs-lookup"><span data-stu-id="28876-143">Enter hello credentials of hello account you want toogenerate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="28876-144">Uw gebruikersagent wijzigen.</span><span class="sxs-lookup"><span data-stu-id="28876-144">Change your user agent.</span></span> <span data-ttu-id="28876-145">U kunt gebruikersagent in Internet Explorer van hulpprogramma's voor ontwikkelaars wijzigen of uw gebruikersagent in Firefox of Chrome met de invoegtoepassing van een gebruikersagent schakelbaar wijzigen.</span><span class="sxs-lookup"><span data-stu-id="28876-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="28876-146">Wijzig het IP-adres.</span><span class="sxs-lookup"><span data-stu-id="28876-146">Change your IP address.</span></span> <span data-ttu-id="28876-147">U kunt uw IP-adres wijzigen met behulp van een VPN, een invoegtoepassing Tor, of van een nieuwe machine in Azure in een ander datacenter draait.</span><span class="sxs-lookup"><span data-stu-id="28876-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="28876-148">Meld u aan te[https://myapps.microsoft.com](https://myapps.microsoft.com) met behulp van dezelfde referenties als voordat en binnen een paar minuten nadat de vorige aanmelden Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="28876-148">Sign-in too[https://myapps.microsoft.com](https://myapps.microsoft.com) using hello same credentials as before and within a few minutes after hello previous sign-in.</span></span>

<span data-ttu-id="28876-149">Hallo-aanmeldingspagina wordt weergegeven in Hallo Identity Protection-dashboard binnen 2-4 uur.</span><span class="sxs-lookup"><span data-stu-id="28876-149">hello sign-in will show up in hello Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="28876-150">Vanwege Hallo complexe machine learning-modellen die betrokken zijn, is er een kans dat deze wordt niet ophalen opgepikt.</span><span class="sxs-lookup"><span data-stu-id="28876-150">Because of hello complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="28876-151">Wilt u mogelijk tooreplicate deze stappen voor meerdere Azure AD-accounts.</span><span class="sxs-lookup"><span data-stu-id="28876-151">You might want tooreplicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="28876-152">Beveiligingsproblemen simuleren</span><span class="sxs-lookup"><span data-stu-id="28876-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="28876-153">Zwakke plekken zijn zwakke punten in een Azure AD-omgeving die door een onjuiste acteur kan worden misbruikt.</span><span class="sxs-lookup"><span data-stu-id="28876-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="28876-154">Momenteel worden 3 typen zwakke plekken die opgehaald in Azure AD Identity Protection die gebruikmaken van andere functies van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28876-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="28876-155">Deze beveiligingsproblemen op Hallo Identity Protection-dashboard automatisch weergegeven zodra deze functies zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="28876-155">These Vulnerabilities will be displayed on hello Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="28876-156">Azure AD [multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="28876-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="28876-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28876-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="28876-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="28876-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="28876-159">Gebruiker risico op inbreuk</span><span class="sxs-lookup"><span data-stu-id="28876-159">User compromise risk</span></span>
<span data-ttu-id="28876-160">**tootest gebruiker risico op inbreuk, voeren Hallo stappen te volgen**:</span><span class="sxs-lookup"><span data-stu-id="28876-160">**tootest User compromise risk, perform hello following steps**:</span></span>

1. <span data-ttu-id="28876-161">Meld u aan te[https://portal.azure.com](https://portal.azure.com) met referenties van de globale beheerder voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="28876-161">Sign-in too[https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="28876-162">Navigeer te**Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="28876-162">Navigate too**Identity Protection**.</span></span> 
3. <span data-ttu-id="28876-163">Op de belangrijkste Hallo **Azure AD Identity Protection** blade, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="28876-163">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="28876-164">Op Hallo **instellingen voor de Gebruikersportal** blade onder **beveiligingsregels**, klikt u op **gebruiker inbreuk risico**.</span><span class="sxs-lookup"><span data-stu-id="28876-164">On hello **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="28876-165">Op Hallo **aanmelden risico** blade inschakelen **inschakelen regel** uit en klik vervolgens op **opslaan** instellingen.</span><span class="sxs-lookup"><span data-stu-id="28876-165">On hello **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="28876-166">Voor een bepaald gebruikersaccount simuleren een onbekende locaties of anonieme IP-risicogebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="28876-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="28876-167">Dit wordt Hallo gebruiker risiconiveau voor die gebruiker te verhogen**gemiddeld**.</span><span class="sxs-lookup"><span data-stu-id="28876-167">This will elevate hello user risk level for that user too**Medium**.</span></span>
7. <span data-ttu-id="28876-168">Wacht een paar minuten en controleer vervolgens dat gebruikersniveau voor de gebruiker is **gemiddeld**.</span><span class="sxs-lookup"><span data-stu-id="28876-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="28876-169">Ga toohello **instellingen voor de Gebruikersportal** blade.</span><span class="sxs-lookup"><span data-stu-id="28876-169">Go toohello **Portal Settings** blade.</span></span>
9. <span data-ttu-id="28876-170">Op Hallo **gebruiker inbreuk risico** blade onder **inschakelen regel**, selecteer **op** .</span><span class="sxs-lookup"><span data-stu-id="28876-170">On hello **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="28876-171">Selecteer een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="28876-171">Select one of hello following options:</span></span>
    
    <span data-ttu-id="28876-172">a.</span><span class="sxs-lookup"><span data-stu-id="28876-172">a.</span></span> <span data-ttu-id="28876-173">tooblock, selecteer **gemiddeld** onder **blok aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="28876-173">tooblock, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="28876-174">b.</span><span class="sxs-lookup"><span data-stu-id="28876-174">b.</span></span> <span data-ttu-id="28876-175">tooenforce beveiligd wachtwoord wijzigen, selecteert **gemiddeld** onder **meervoudige authenticatie**.</span><span class="sxs-lookup"><span data-stu-id="28876-175">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="28876-176">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="28876-176">Click **Save**.</span></span>
12. <span data-ttu-id="28876-177">U kunt nu voorwaardelijke toegang op basis van risico's wanneer u zich aanmeldt bij het gebruik van een gebruiker met een verhoogde risiconiveau testen.</span><span class="sxs-lookup"><span data-stu-id="28876-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="28876-178">Hallo gebruiker risico gemiddeld, afhankelijk van de configuratie van de Hallo van uw beleid, de aanmeldingspagina is worden geblokkeerd of u toochange worden gedwongen uw wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="28876-178">If hello user risk is Medium, depending on hello configuration of your policy, your sign-in is be either blocked or you are forced toochange your password.</span></span> 
    <br><br><span data-ttu-id="28876-179">
    ![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
    </span><span class="sxs-lookup"><span data-stu-id="28876-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="28876-180">Aanmelden risico</span><span class="sxs-lookup"><span data-stu-id="28876-180">Sign-in risk</span></span>
<span data-ttu-id="28876-181">**tootest een teken in gevaar, Voer Hallo stappen te volgen:**</span><span class="sxs-lookup"><span data-stu-id="28876-181">**tootest a sign in risk, perform hello following steps:**</span></span>

1. <span data-ttu-id="28876-182">Meld u aan te[https://portal.azure.com ](https://portal.azure.com) met referenties van de globale beheerder voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="28876-182">Sign-in too[https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="28876-183">Navigeer te**Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="28876-183">Navigate too**Identity Protection**.</span></span>
3. <span data-ttu-id="28876-184">Op de belangrijkste Hallo **Azure AD Identity Protection** blade, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="28876-184">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="28876-185">Op Hallo **instellingen voor de Gebruikersportal** blade onder **beveiligingsregels**, klikt u op **aanmelden risico**.</span><span class="sxs-lookup"><span data-stu-id="28876-185">On hello **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="28876-186">Op Hallo ** aanmelden risico ** blade Selecteer **op** onder **inschakelen regel**.</span><span class="sxs-lookup"><span data-stu-id="28876-186">On hello **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="28876-187">Selecteer een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="28876-187">Select one of hello following options:</span></span>
   
   <span data-ttu-id="28876-188">a.</span><span class="sxs-lookup"><span data-stu-id="28876-188">a.</span></span> <span data-ttu-id="28876-189">tooblock, selecteer **gemiddeld** onder **blok aanmelden**</span><span class="sxs-lookup"><span data-stu-id="28876-189">tooblock, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="28876-190">b.</span><span class="sxs-lookup"><span data-stu-id="28876-190">b.</span></span> <span data-ttu-id="28876-191">tooenforce beveiligd wachtwoord wijzigen, selecteert **gemiddeld** onder **meervoudige authenticatie**.</span><span class="sxs-lookup"><span data-stu-id="28876-191">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="28876-192">tooblock, selecteer gemiddeld onder blok aanmelden.</span><span class="sxs-lookup"><span data-stu-id="28876-192">tooblock, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="28876-193">tooenforce multi-factor authentication-server, selecteer **gemiddeld** onder **meervoudige authenticatie**.</span><span class="sxs-lookup"><span data-stu-id="28876-193">tooenforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="28876-194">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="28876-194">Click on **Save**.</span></span>
10. <span data-ttu-id="28876-195">U kunt nu voorwaardelijke toegang op basis van risico testen door simuleren Hallo onbekende locaties of anoniem IP gebeurtenissen risico omdat ze beide **gemiddeld** bestaat de kans dat gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="28876-195">You can now test risk-based conditional access by simulating hello unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="28876-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="28876-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="28876-197">Zie ook</span><span class="sxs-lookup"><span data-stu-id="28876-197">See also</span></span>
* [<span data-ttu-id="28876-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="28876-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

