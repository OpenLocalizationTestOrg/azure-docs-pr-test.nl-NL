---
title: 'Azure Active Directory: Identity Protection playbook | Microsoft Docs'
description: Meer informatie over hoe Azure AD Identity Protection kunt u de mogelijkheid van een aanvaller misbruik maakt van een verdachte identiteit of het apparaat en voor het beveiligen van een identiteit of een apparaat dat eerder is verdacht of bekend is dat inbreuk wordt gepleegd beperken.
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
ms.openlocfilehash: 2ecd07faed785fa6aa179ac1cca35a70d965e1dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="298b8-104">Playbook voor Azure Active Directory: Identity Protection</span><span class="sxs-lookup"><span data-stu-id="298b8-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="298b8-105">Deze playbook helpt u bij:</span><span class="sxs-lookup"><span data-stu-id="298b8-105">This playbook helps you to:</span></span>

* <span data-ttu-id="298b8-106">Gegevens in de omgeving Identity Protection door simulating risicogebeurtenissen en beveiligingsproblemen vullen</span><span class="sxs-lookup"><span data-stu-id="298b8-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="298b8-107">Beleid voor voorwaardelijke toegang op basis van risico's instellen en de gevolgen van het beleid testen</span><span class="sxs-lookup"><span data-stu-id="298b8-107">Set up risk-based conditional access policies and test the impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="298b8-108">Risico's te simuleren</span><span class="sxs-lookup"><span data-stu-id="298b8-108">Simulating Risk Events</span></span>
<span data-ttu-id="298b8-109">Deze sectie bevat stappen voor het simuleren van de volgende typen van de risico-gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="298b8-109">This section provides you with steps for simulating the following risk event types:</span></span>

* <span data-ttu-id="298b8-110">Aanmeldingen vanaf anonieme IP-adressen (eenvoudig)</span><span class="sxs-lookup"><span data-stu-id="298b8-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="298b8-111">Aanmeldingen vanaf onbekende locaties (gemiddeld)</span><span class="sxs-lookup"><span data-stu-id="298b8-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="298b8-112">Onmogelijke reis naar ongewone locaties (moeilijk)</span><span class="sxs-lookup"><span data-stu-id="298b8-112">Impossible travel to atypical locations (difficult)</span></span>

<span data-ttu-id="298b8-113">Andere risicogebeurtenissen kunnen niet op een veilige manier worden gesimuleerd.</span><span class="sxs-lookup"><span data-stu-id="298b8-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="298b8-114">Aanmeldingen vanaf anonieme IP-adressen</span><span class="sxs-lookup"><span data-stu-id="298b8-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="298b8-115">Dit type risico gebeurtenis identificeert gebruikers die zich heeft aangemeld vanaf een IP-adres dat is geïdentificeerd als een anonieme proxy IP-adres.</span><span class="sxs-lookup"><span data-stu-id="298b8-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="298b8-116">Deze proxy's worden gebruikt door mensen die u wilt verbergen, IP-adres van het apparaat en kan worden gebruikt voor kwade bedoelingen.</span><span class="sxs-lookup"><span data-stu-id="298b8-116">These proxies are used by people who want to hide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="298b8-117">**De volgende stappen uitvoeren om te simuleren een aanmeldingspagina van een anoniem IP,**:</span><span class="sxs-lookup"><span data-stu-id="298b8-117">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span></span>

1. <span data-ttu-id="298b8-118">Download de [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="298b8-118">Download the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="298b8-119">Met de Tor-Browser, Ga naar [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="298b8-119">Using the Tor Browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="298b8-120">Voer de referenties van het account moet worden weergegeven de **aanmeldingen vanaf anonieme IP-adressen** rapport.</span><span class="sxs-lookup"><span data-stu-id="298b8-120">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="298b8-121">De aanmeldingspagina wordt weergegeven op het dashboard Identity Protection binnen 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="298b8-121">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="298b8-122">Aanmeldingen vanaf onbekende locaties</span><span class="sxs-lookup"><span data-stu-id="298b8-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="298b8-123">Het risico van onbekende locaties is een van realtime-in-evaluatiemechanisme dat uit het verleden aanmelden locaties overweegt (IP, breedtegraad / lengtegraad en ASN) om te bepalen van de nieuwe / onbekende locaties.</span><span class="sxs-lookup"><span data-stu-id="298b8-123">The unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="298b8-124">Het systeem slaat vorige IP-adressen, de breedtegraad / lengtegraad en ASN's van een gebruiker en wordt deze aan het vertrouwde locaties worden beschouwd.</span><span class="sxs-lookup"><span data-stu-id="298b8-124">The system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these to be familiar locations.</span></span> <span data-ttu-id="298b8-125">Een locatie aanmelden wordt beschouwd als niet bekend als de locatie aanmelden komt niet overeen met een van de bestaande vertrouwde locaties.</span><span class="sxs-lookup"><span data-stu-id="298b8-125">A sign-in location is considered unfamiliar if the sign-in location does not match any of the existing familiar locations.</span></span>

<span data-ttu-id="298b8-126">Beveiliging van Azure Active Directory-identiteit:</span><span class="sxs-lookup"><span data-stu-id="298b8-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="298b8-127">heeft een initiële learning periode van 14 dagen aan waarover biedt het geen nieuwe locaties als onbekende locaties vlag.</span><span class="sxs-lookup"><span data-stu-id="298b8-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="298b8-128">aanmeldingen vanaf bekende apparaten en de locaties die geografisch zich dicht bij een bestaande vertrouwde locatie negeert.</span><span class="sxs-lookup"><span data-stu-id="298b8-128">ignores sign-ins from familiar devices and locations that are geographically close to an existing familiar location.</span></span>

<span data-ttu-id="298b8-129">Om te simuleren onbekende locaties, die u moet zich aanmelden via een locatie en het apparaat dat het account is niet aangemeld uit voordat u.</span><span class="sxs-lookup"><span data-stu-id="298b8-129">To simulate unfamiliar locations, you have to sign in from a location and device that the account has not signed in from before.</span></span> 

<span data-ttu-id="298b8-130">**De volgende stappen uitvoeren om te simuleren een aanmelden vanaf een onbekend locatie,**:</span><span class="sxs-lookup"><span data-stu-id="298b8-130">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span></span>

1. <span data-ttu-id="298b8-131">Kies een account met ten minste een geschiedenis van de aanmeldingspagina 14 dagen.</span><span class="sxs-lookup"><span data-stu-id="298b8-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="298b8-132">Doen:</span><span class="sxs-lookup"><span data-stu-id="298b8-132">Do either:</span></span>
   
   <span data-ttu-id="298b8-133">a.</span><span class="sxs-lookup"><span data-stu-id="298b8-133">a.</span></span> <span data-ttu-id="298b8-134">Tijdens het gebruik van een VPN, gaat u naar [https://myapps.microsoft.com](https://myapps.microsoft.com) en voer de referenties van het account dat u wilt de risicogebeurtenis voor simuleren.</span><span class="sxs-lookup"><span data-stu-id="298b8-134">While using a VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of the account you want to simulate the risk event for.</span></span>
   
   <span data-ttu-id="298b8-135">b.</span><span class="sxs-lookup"><span data-stu-id="298b8-135">b.</span></span> <span data-ttu-id="298b8-136">Vraag een koppelen in een andere locatie kunnen aanmelden met de accountreferenties (niet aanbevolen).</span><span class="sxs-lookup"><span data-stu-id="298b8-136">Ask an associate in a different location to sign in using the account’s credentials (not recommended).</span></span>

<span data-ttu-id="298b8-137">De aanmeldingspagina wordt weergegeven op het dashboard Identity Protection binnen 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="298b8-137">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-to-atypical-location"></a><span data-ttu-id="298b8-138">Onmogelijke reis naar ongewone locatie</span><span class="sxs-lookup"><span data-stu-id="298b8-138">Impossible travel to atypical location</span></span>
<span data-ttu-id="298b8-139">Het is moeilijk om de voorwaarde onmogelijke reis simuleren omdat de algoritme machine learning gebruikt voor wieden uit ONWAAR-positieven zoals onmogelijke reis vanaf vertrouwde apparaten of aanmeldingen vanaf VPN's die worden gebruikt door andere gebruikers in de map.</span><span class="sxs-lookup"><span data-stu-id="298b8-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span></span> <span data-ttu-id="298b8-140">Daarnaast vereist het algoritme een geschiedenis aanmelden van 3 tot en met 14 dagen voor de gebruiker voordat u begint deze risico's te genereren.</span><span class="sxs-lookup"><span data-stu-id="298b8-140">Additionally, the algorithm requires a sign-in history of 3 to 14 days for the user before it begins generating risk events.</span></span>

<span data-ttu-id="298b8-141">**De volgende stappen uitvoeren om te simuleren van een onmogelijke reis naar ongewone locatie,**:</span><span class="sxs-lookup"><span data-stu-id="298b8-141">**To simulate an impossible travel to atypical location, perform the following steps**:</span></span>

1. <span data-ttu-id="298b8-142">Navigeer met uw standaardbrowser naar [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="298b8-142">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="298b8-143">Voer de referenties van het account dat u wilt genereren van een onmogelijke reis risicogebeurtenis voor.</span><span class="sxs-lookup"><span data-stu-id="298b8-143">Enter the credentials of the account you want to generate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="298b8-144">Uw gebruikersagent wijzigen.</span><span class="sxs-lookup"><span data-stu-id="298b8-144">Change your user agent.</span></span> <span data-ttu-id="298b8-145">U kunt gebruikersagent in Internet Explorer van hulpprogramma's voor ontwikkelaars wijzigen of uw gebruikersagent in Firefox of Chrome met de invoegtoepassing van een gebruikersagent schakelbaar wijzigen.</span><span class="sxs-lookup"><span data-stu-id="298b8-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="298b8-146">Wijzig het IP-adres.</span><span class="sxs-lookup"><span data-stu-id="298b8-146">Change your IP address.</span></span> <span data-ttu-id="298b8-147">U kunt uw IP-adres wijzigen met behulp van een VPN, een invoegtoepassing Tor, of van een nieuwe machine in Azure in een ander datacenter draait.</span><span class="sxs-lookup"><span data-stu-id="298b8-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="298b8-148">Aanmelden bij [https://myapps.microsoft.com](https://myapps.microsoft.com) met dezelfde referenties als voordat en binnen een paar minuten na de vorige aanmelden.</span><span class="sxs-lookup"><span data-stu-id="298b8-148">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span></span>

<span data-ttu-id="298b8-149">De aanmeldingspagina wordt weergegeven in het dashboard Identity Protection binnen 2-4 uur.</span><span class="sxs-lookup"><span data-stu-id="298b8-149">The sign-in will show up in the Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="298b8-150">Vanwege de complexe machine learning-modellen die zijn betrokken, is er een kans dat deze wordt niet ophalen opgepikt.</span><span class="sxs-lookup"><span data-stu-id="298b8-150">Because of the complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="298b8-151">Mogelijk wilt deze stappen over meerdere Azure AD-accounts worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="298b8-151">You might want to replicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="298b8-152">Beveiligingsproblemen simuleren</span><span class="sxs-lookup"><span data-stu-id="298b8-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="298b8-153">Zwakke plekken zijn zwakke punten in een Azure AD-omgeving die door een onjuiste acteur kan worden misbruikt.</span><span class="sxs-lookup"><span data-stu-id="298b8-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="298b8-154">Momenteel worden 3 typen zwakke plekken die opgehaald in Azure AD Identity Protection die gebruikmaken van andere functies van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="298b8-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="298b8-155">Deze beveiligingslekken wordt weergegeven op het dashboard Identity Protection automatisch zodra deze functies zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="298b8-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="298b8-156">Azure AD [multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="298b8-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="298b8-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="298b8-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="298b8-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="298b8-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="298b8-159">Gebruiker risico op inbreuk</span><span class="sxs-lookup"><span data-stu-id="298b8-159">User compromise risk</span></span>
<span data-ttu-id="298b8-160">**De volgende stappen uitvoeren om het risico op inbreuk gebruiker testen,**:</span><span class="sxs-lookup"><span data-stu-id="298b8-160">**To test User compromise risk, perform the following steps**:</span></span>

1. <span data-ttu-id="298b8-161">Aanmelden bij [https://portal.azure.com](https://portal.azure.com) met referenties van de globale beheerder voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="298b8-161">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="298b8-162">Navigeer naar **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="298b8-162">Navigate to **Identity Protection**.</span></span> 
3. <span data-ttu-id="298b8-163">Op de hoofdblade **Azure AD Identity Protection** blade, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="298b8-163">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="298b8-164">Op de **instellingen voor de Gebruikersportal** blade onder **beveiligingsregels**, klikt u op **gebruiker inbreuk risico**.</span><span class="sxs-lookup"><span data-stu-id="298b8-164">On the **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="298b8-165">Op de **aanmelden risico** blade inschakelen **inschakelen regel** uit en klik vervolgens op **opslaan** instellingen.</span><span class="sxs-lookup"><span data-stu-id="298b8-165">On the **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="298b8-166">Voor een bepaald gebruikersaccount simuleren een onbekende locaties of anonieme IP-risicogebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="298b8-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="298b8-167">Hiermee wordt het risiconiveau van de gebruiker voor die gebruiker bevoegdheden **gemiddeld**.</span><span class="sxs-lookup"><span data-stu-id="298b8-167">This will elevate the user risk level for that user to **Medium**.</span></span>
7. <span data-ttu-id="298b8-168">Wacht een paar minuten en controleer vervolgens dat gebruikersniveau voor de gebruiker is **gemiddeld**.</span><span class="sxs-lookup"><span data-stu-id="298b8-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="298b8-169">Ga naar de **instellingen voor de Gebruikersportal** blade.</span><span class="sxs-lookup"><span data-stu-id="298b8-169">Go to the **Portal Settings** blade.</span></span>
9. <span data-ttu-id="298b8-170">Op de **gebruiker inbreuk risico** blade onder **inschakelen regel**, selecteer **op** .</span><span class="sxs-lookup"><span data-stu-id="298b8-170">On the **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="298b8-171">Selecteer een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="298b8-171">Select one of the following options:</span></span>
    
    <span data-ttu-id="298b8-172">a.</span><span class="sxs-lookup"><span data-stu-id="298b8-172">a.</span></span> <span data-ttu-id="298b8-173">Om te blokkeren, selecteer **gemiddeld** onder **blok aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="298b8-173">To block, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="298b8-174">b.</span><span class="sxs-lookup"><span data-stu-id="298b8-174">b.</span></span> <span data-ttu-id="298b8-175">Afdwingen van beveiligd wachtwoord wijzigen **gemiddeld** onder **meervoudige authenticatie**.</span><span class="sxs-lookup"><span data-stu-id="298b8-175">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="298b8-176">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="298b8-176">Click **Save**.</span></span>
12. <span data-ttu-id="298b8-177">U kunt nu voorwaardelijke toegang op basis van risico's wanneer u zich aanmeldt bij het gebruik van een gebruiker met een verhoogde risiconiveau testen.</span><span class="sxs-lookup"><span data-stu-id="298b8-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="298b8-178">Als het risico van de gebruiker normaal, afhankelijk van de configuratie van uw beleid voor het aanmelden is worden geblokkeerd of u gedwongen om uw wachtwoord te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="298b8-178">If the user risk is Medium, depending on the configuration of your policy, your sign-in is be either blocked or you are forced to change your password.</span></span> 
    <br><br><span data-ttu-id="298b8-179">
    ![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
    </span><span class="sxs-lookup"><span data-stu-id="298b8-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="298b8-180">Aanmelden risico</span><span class="sxs-lookup"><span data-stu-id="298b8-180">Sign-in risk</span></span>
<span data-ttu-id="298b8-181">**Test een teken in de risico's door de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="298b8-181">**To test a sign in risk, perform the following steps:**</span></span>

1. <span data-ttu-id="298b8-182">Aanmelden bij [https://portal.azure.com ](https://portal.azure.com) met referenties van de globale beheerder voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="298b8-182">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="298b8-183">Navigeer naar **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="298b8-183">Navigate to **Identity Protection**.</span></span>
3. <span data-ttu-id="298b8-184">Op de hoofdblade **Azure AD Identity Protection** blade, klikt u op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="298b8-184">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="298b8-185">Op de **instellingen voor de Gebruikersportal** blade onder **beveiligingsregels**, klikt u op **aanmelden risico**.</span><span class="sxs-lookup"><span data-stu-id="298b8-185">On the **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="298b8-186">Op de ** aanmelden risico ** blade Selecteer **op** onder **inschakelen regel**.</span><span class="sxs-lookup"><span data-stu-id="298b8-186">On the **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="298b8-187">Selecteer een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="298b8-187">Select one of the following options:</span></span>
   
   <span data-ttu-id="298b8-188">a.</span><span class="sxs-lookup"><span data-stu-id="298b8-188">a.</span></span> <span data-ttu-id="298b8-189">Als u wilt blokkeren, selecteer **gemiddeld** onder **blok aanmelden**</span><span class="sxs-lookup"><span data-stu-id="298b8-189">To block, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="298b8-190">b.</span><span class="sxs-lookup"><span data-stu-id="298b8-190">b.</span></span> <span data-ttu-id="298b8-191">Afdwingen van beveiligd wachtwoord wijzigen **gemiddeld** onder **meervoudige authenticatie**.</span><span class="sxs-lookup"><span data-stu-id="298b8-191">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="298b8-192">Selecteer om te blokkeren, gemiddeld onder blok aanmelden.</span><span class="sxs-lookup"><span data-stu-id="298b8-192">To block, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="298b8-193">Afdwingen van multi-factor authentication-server **gemiddeld** onder **meervoudige authenticatie**.</span><span class="sxs-lookup"><span data-stu-id="298b8-193">To enforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="298b8-194">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="298b8-194">Click on **Save**.</span></span>
10. <span data-ttu-id="298b8-195">U kunt nu voorwaardelijke toegang op basis van risico's testen door simuleren onbekende locaties of anoniem IP gebeurtenissen risico omdat ze beide **gemiddeld** bestaat de kans dat gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="298b8-195">You can now test risk-based conditional access by simulating the unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="298b8-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="298b8-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="298b8-197">Zie ook</span><span class="sxs-lookup"><span data-stu-id="298b8-197">See also</span></span>
* [<span data-ttu-id="298b8-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="298b8-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

