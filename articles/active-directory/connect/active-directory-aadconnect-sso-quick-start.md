---
title: 'Azure AD Connect: Naadloze eenmalige aanmelding - snel aan de slag | Microsoft Docs'
description: Dit artikel wordt beschreven hoe tooget gestart met Azure Active Directory naadloze eenmalige aanmelding.
services: active-directory
keywords: Wat is Azure AD Connect, installeer Active Directory onderdelen vereist voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="783cf-104">Azure Active Directory naadloze eenmalige aanmelding: snel starten</span><span class="sxs-lookup"><span data-stu-id="783cf-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-toodeploy-seamless-sso"></a><span data-ttu-id="783cf-105">Hoe toodeploy naadloze eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="783cf-105">How toodeploy Seamless SSO</span></span>

<span data-ttu-id="783cf-106">Azure Active Directory naadloze eenmalige aanmelding (Azure AD naadloze SSO) gebruikers wanneer ze zijn in het bedrijfsnetwerk van hun bedrijfscomputers verbonden tooyour automatisch afgemeld.</span><span class="sxs-lookup"><span data-stu-id="783cf-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected tooyour corporate network.</span></span> <span data-ttu-id="783cf-107">Dit biedt uw gebruikers eenvoudig toegang tooyour cloud-gebaseerde toepassingen zonder extra on-premises onderdelen.</span><span class="sxs-lookup"><span data-stu-id="783cf-107">It provides your users easy access tooyour cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="783cf-108">Hallo naadloze SSO-functie is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="783cf-108">hello Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="783cf-109">Wanneer u toofollow toodeploy naadloze eenmalige aanmelding, moet deze stappen:</span><span class="sxs-lookup"><span data-stu-id="783cf-109">toodeploy Seamless SSO, you need toofollow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="783cf-110">Stap 1: Controle van vereisten</span><span class="sxs-lookup"><span data-stu-id="783cf-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="783cf-111">Zorg ervoor dat Hallo volgende vereisten wordt voldaan:</span><span class="sxs-lookup"><span data-stu-id="783cf-111">Ensure that hello following prerequisites are in place:</span></span>

1. <span data-ttu-id="783cf-112">Instellen van uw Azure AD Connect-server: als u [Pass through-verificatie](active-directory-aadconnect-pass-through-authentication.md) als uw contactmethode aanmelden is geen verdere actie vereist.</span><span class="sxs-lookup"><span data-stu-id="783cf-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="783cf-113">Als u [synchronisatie van wachtwoordhash](active-directory-aadconnectsync-implement-password-synchronization.md) als uw contactmethode aanmelden en als er een firewall tussen Azure AD Connect en Azure AD, zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="783cf-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="783cf-114">U gebruikt versies 1.1.484.0 of hoger van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="783cf-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="783cf-115">Azure AD Connect kan communiceren met `*.msappproxy.net` URL's en meer dan poort 443.</span><span class="sxs-lookup"><span data-stu-id="783cf-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="783cf-116">Deze vereiste geldt alleen wanneer u Hallo-functie, niet voor de werkelijke gebruikersaanmeldingen inschakelt.</span><span class="sxs-lookup"><span data-stu-id="783cf-116">This prerequisite is applicable only when you enable hello feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="783cf-117">Azure AD Connect kunt aanbrengen direct IP-verbindingen toohello [Azure datacentrum IP-adresbereiken](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="783cf-117">Azure AD Connect can make direct IP connections toohello [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="783cf-118">Deze vereiste geldt opnieuw, alleen wanneer u Hallo functie inschakelt.</span><span class="sxs-lookup"><span data-stu-id="783cf-118">Again, this prerequisite is applicable only when you enable hello feature.</span></span>
2. <span data-ttu-id="783cf-119">U moet domeinbeheerder-referenties voor elk AD-forest dat u tooAzure AD synchroniseren (met behulp van Azure AD Connect) en gebruikers voor wie u wilt dat tooenable naadloze eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="783cf-119">You need Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span>

## <a name="step-2-enable-hello-feature"></a><span data-ttu-id="783cf-120">Stap 2: Hallo-functie inschakelen</span><span class="sxs-lookup"><span data-stu-id="783cf-120">Step 2: Enable hello feature</span></span>

<span data-ttu-id="783cf-121">Naadloze eenmalige aanmelding kan worden ingeschakeld met [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="783cf-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="783cf-122">Als u een nieuwe installatie van Azure AD Connect uitvoert, kiest u Hallo [aangepaste installatiepad](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="783cf-122">If you are doing a fresh installation of Azure AD Connect, choose hello [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="783cf-123">Controleer op Hallo ' gebruiker ' aanmeldingspagina, Hallo 'Inschakelen voor eenmalige aanmelding' optie.</span><span class="sxs-lookup"><span data-stu-id="783cf-123">At hello "User sign-in" page, check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - gebruiker aanmelden](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="783cf-125">Als u al een installatie van Azure AD Connect, kiest u 'Gebruiker aanmelden pagina wijzigen' op Azure AD Connect en klik op 'Volgende'.</span><span class="sxs-lookup"><span data-stu-id="783cf-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="783cf-126">Controleer vervolgens Hallo 'Inschakelen voor eenmalige aanmelding' optie.</span><span class="sxs-lookup"><span data-stu-id="783cf-126">Then check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - wijziging gebruiker aanmelden](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="783cf-128">Hallo wizard vervolgen, totdat u toohello 'Inschakelen voor eenmalige aanmelding' pagina.</span><span class="sxs-lookup"><span data-stu-id="783cf-128">Continue through hello wizard until you get toohello "Enable single sign on" page.</span></span> <span data-ttu-id="783cf-129">Referenties van de domeinbeheerder voor elk AD-forest dat u tooAzure AD gesynchroniseerd (met behulp van Azure AD Connect) en gebruikers voor wie u wilt dat tooenable naadloze eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="783cf-129">Provide Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span> 

<span data-ttu-id="783cf-130">Naadloze eenmalige aanmelding is na voltooiing van de wizard hello wordt ingeschakeld op uw tenant.</span><span class="sxs-lookup"><span data-stu-id="783cf-130">After completion of hello wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="783cf-131">Hallo domeinbeheerder-referenties niet zijn opgeslagen in Azure AD Connect of in Azure AD, maar alleen gebruikte tooenable Hallo functie zijn.</span><span class="sxs-lookup"><span data-stu-id="783cf-131">hello Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used tooenable hello feature.</span></span>

<span data-ttu-id="783cf-132">Volg deze instructies tooverify naadloze eenmalige aanmelding correct ingeschakeld:</span><span class="sxs-lookup"><span data-stu-id="783cf-132">Follow these instructions tooverify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="783cf-133">Meld u aan toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met Hallo hoofdbeheerder referenties voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="783cf-133">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with hello Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="783cf-134">Selecteer **Azure Active Directory** op de linkernavigatiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="783cf-134">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="783cf-135">Selecteer **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="783cf-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="783cf-136">Controleer of deze Hallo **naadloze eenmalige aanmelding** functie wordt weergegeven als **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="783cf-136">Verify that hello **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Azure-portal - blade van Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a><span data-ttu-id="783cf-138">Stap 3: Implementeer Hallo-functie</span><span class="sxs-lookup"><span data-stu-id="783cf-138">Step 3: Roll out hello feature</span></span>

<span data-ttu-id="783cf-139">tooroll hello functie tooyour gebruikers, moet u tooadd twee Azure AD-URL's (https://autologon.microsoftazuread-sso.com en https://aadg.windows.net.nsatc.net) toousers de Intranet-beveiligingszone-instellingen via Groepsbeleid in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="783cf-139">tooroll out hello feature tooyour users, you need tooadd two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) toousers' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="783cf-140">Hallo alleen werk voor Internet Explorer en Google Chrome instructies te volgen in Windows (indien deze reeks URL's van vertrouwde site met Internet Explorer deelt).</span><span class="sxs-lookup"><span data-stu-id="783cf-140">hello following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="783cf-141">Lees de volgende sectie Hallo voor instructies tooset Mozilla Firefox en Google Chrome op Mac.</span><span class="sxs-lookup"><span data-stu-id="783cf-141">Read hello next section for instructions tooset up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a><span data-ttu-id="783cf-142">Waarom moet u gebruikers toomodify Intranet-beveiligingszone-instellingen?</span><span class="sxs-lookup"><span data-stu-id="783cf-142">Why do you need toomodify users' Intranet zone settings?</span></span>

<span data-ttu-id="783cf-143">Standaard berekend Hallo browser automatisch Hallo in de juiste zone (Internet of een Intranet) van een URL.</span><span class="sxs-lookup"><span data-stu-id="783cf-143">By default, hello browser automatically calculates hello right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="783cf-144">Http://contoso/ is bijvoorbeeld toegewezen toohello intranetzone terwijl http://intranet.contoso.com/ toegewezen toohello internetzone (omdat het Hallo-URL bevat een periode).</span><span class="sxs-lookup"><span data-stu-id="783cf-144">For example, http://contoso/ is mapped toohello Intranet zone, whereas http://intranet.contoso.com/ is mapped toohello Internet zone (because hello URL contains a period).</span></span> <span data-ttu-id="783cf-145">Browsers verzenden geen Kerberos-tickets tooa cloudeindpunt - zoals Hallo twee Azure AD-URL's -, tenzij de URL van de browser toohello intranetzone is expliciet zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="783cf-145">Browsers don't send Kerberos tickets tooa cloud endpoint - like hello two Azure AD URLs - unless its URL is explicitly added toohello browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="783cf-146">Gedetailleerde stappen</span><span class="sxs-lookup"><span data-stu-id="783cf-146">Detailed steps</span></span>

1. <span data-ttu-id="783cf-147">Open het Hallo Group Policy Management-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="783cf-147">Open hello Group Policy Management tool.</span></span>
2. <span data-ttu-id="783cf-148">Hallo Groepsbeleid die toegepaste toosome of alle gebruikers bewerken.</span><span class="sxs-lookup"><span data-stu-id="783cf-148">Edit hello Group Policy that is applied toosome or all your users.</span></span> <span data-ttu-id="783cf-149">In dit voorbeeld gebruiken we Hallo **standaarddomeinbeleid**.</span><span class="sxs-lookup"><span data-stu-id="783cf-149">In this example, we use hello **Default Domain Policy**.</span></span>
3. <span data-ttu-id="783cf-150">Navigeer te**Configuration\Administrative Templates\Windows Explorer\Onderdeel Internet Control Panel\Security op de gebruikerspagina** en selecteer **tooZone lijst van zonetoewijzingen Site**.</span><span class="sxs-lookup"><span data-stu-id="783cf-150">Navigate too**User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site tooZone Assignment List**.</span></span>
<span data-ttu-id="783cf-151">![Eenmalige aanmelding](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="783cf-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="783cf-152">Hallo-beleid inschakelen en Voer Hallo waarden (Azure AD URL's waarin de Kerberos-tickets worden doorgestuurd) te volgen en gegevens (*1* intranetzone geeft) in het dialoogvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="783cf-152">Enable hello policy, and enter hello following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in hello dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="783cf-153">Als u toodisallow sommige gebruikers met een naadloze eenmalige aanmelding - bijvoorbeeld, wilt als deze gebruikers op gedeelde kiosken aanmelden zich - stelt Hallo voorafgaand aan waarden te*4*.</span><span class="sxs-lookup"><span data-stu-id="783cf-153">If you want toodisallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set hello preceding values too*4*.</span></span> <span data-ttu-id="783cf-154">Deze actie hello Azure AD-URL's toohello beperkte Zone worden toegevoegd en alle Hallo tijd voor naadloze eenmalige aanmelding mislukt.</span><span class="sxs-lookup"><span data-stu-id="783cf-154">This action adds hello Azure AD URLs toohello Restricted Zone, and fails Seamless SSO all hello time.</span></span>

5. <span data-ttu-id="783cf-155">Klik op **OK** en **OK** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="783cf-155">Click **OK** and **OK** again.</span></span>

![Eenmalige aanmelding](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="783cf-157">Browser-overwegingen</span><span class="sxs-lookup"><span data-stu-id="783cf-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="783cf-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="783cf-158">Mozilla Firefox</span></span>

<span data-ttu-id="783cf-159">Mozilla Firefox niet automatisch Kerberos-verificatie.</span><span class="sxs-lookup"><span data-stu-id="783cf-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="783cf-160">Elke gebruiker heeft toomanually hello Azure AD-URL's tootheir Firefox instellingen met behulp van de volgende stappen uit Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="783cf-160">Each user has toomanually add hello Azure AD URLs tootheir Firefox settings using hello following steps:</span></span>
1. <span data-ttu-id="783cf-161">Firefox uitvoeren en voer `about:config` in de adresbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="783cf-161">Run Firefox and enter `about:config` in hello address bar.</span></span> <span data-ttu-id="783cf-162">Meldingen die u ziet worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="783cf-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="783cf-163">Zoeken naar Hallo **network.negotiate-auth.trusted-URI's** voorkeur.</span><span class="sxs-lookup"><span data-stu-id="783cf-163">Search for hello **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="783cf-164">Deze voorkeur geeft een lijst met vertrouwde sites van Firefox voor Kerberos-verificatie.</span><span class="sxs-lookup"><span data-stu-id="783cf-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="783cf-165">Met de rechtermuisknop en selecteer 'Wijzigen'.</span><span class="sxs-lookup"><span data-stu-id="783cf-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="783cf-166">Voer "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in het Hallo-veld.</span><span class="sxs-lookup"><span data-stu-id="783cf-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in hello field.</span></span>
5. <span data-ttu-id="783cf-167">Klik op 'OK' en Hallo browser openen.</span><span class="sxs-lookup"><span data-stu-id="783cf-167">Click "OK" and reopen hello browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="783cf-168">Safari op Mac OS</span><span class="sxs-lookup"><span data-stu-id="783cf-168">Safari on Mac OS</span></span>

<span data-ttu-id="783cf-169">Zorg ervoor dat Hallo-machine met Mac OS gekoppelde tooAD.</span><span class="sxs-lookup"><span data-stu-id="783cf-169">Ensure that hello machine running Mac OS is joined tooAD.</span></span> <span data-ttu-id="783cf-170">Zie de instructies voor het toodo die [hier](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="783cf-170">See instructions on how toodo that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="783cf-171">Google Chrome op Mac OS</span><span class="sxs-lookup"><span data-stu-id="783cf-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="783cf-172">Raadpleeg te voor Google Chrome op Mac OS en andere niet-Windows-platforms,[in dit artikel](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) voor meer informatie over hoe toowhitelist hello Azure AD-URL's voor geïntegreerde verificatie.</span><span class="sxs-lookup"><span data-stu-id="783cf-172">For Google Chrome on Mac OS and other non-Windows platforms, refer too[this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how toowhitelist hello Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="783cf-173">Het gebruik van Active Directory-groepsbeleid van derden is extensies tooroll hello Azure AD-URL's tooFirefox en Google Chrome op Mac-gebruikers buiten het bereik van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="783cf-173">Using third-party Active Directory Group Policy extensions tooroll out hello Azure AD URLs tooFirefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="783cf-174">Bekende beperkingen</span><span class="sxs-lookup"><span data-stu-id="783cf-174">Known limitations</span></span>

<span data-ttu-id="783cf-175">Naadloze eenmalige aanmelding werkt niet in de privémodus Browse Firefox en rand browsers.</span><span class="sxs-lookup"><span data-stu-id="783cf-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="783cf-176">Deze ook werkt niet op Internet Explorer als Hallo browser wordt uitgevoerd in de modus voor uitgebreide beveiliging.</span><span class="sxs-lookup"><span data-stu-id="783cf-176">It also doesn't work on Internet Explorer if hello browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="783cf-177">We onlangs teruggedraaid ondersteuning voor rand tooinvestigate klanten gemelde problemen.</span><span class="sxs-lookup"><span data-stu-id="783cf-177">We recently rolled back support for Edge tooinvestigate customer-reported issues.</span></span>

## <a name="step-4-test-hello-feature"></a><span data-ttu-id="783cf-178">Stap 4: Hallo functie testen</span><span class="sxs-lookup"><span data-stu-id="783cf-178">Step 4: Test hello feature</span></span>

<span data-ttu-id="783cf-179">tootest Hallo-functie voor een specifieke gebruiker controleren of _alle_ Hallo volgende voorwaarden wordt voldaan:</span><span class="sxs-lookup"><span data-stu-id="783cf-179">tootest hello feature for a specific user, ensure that _all_ hello following conditions are in place:</span></span>
  - <span data-ttu-id="783cf-180">Hallo-gebruiker zich aanmeldt op een zakelijke apparaat.</span><span class="sxs-lookup"><span data-stu-id="783cf-180">hello user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="783cf-181">Hallo-apparaat is eerder samengevoegde tooyour Active Directory (AD)-domein.</span><span class="sxs-lookup"><span data-stu-id="783cf-181">hello device has been previously joined tooyour Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="783cf-182">Hallo-apparaat heeft een directe verbinding tooyour domeincontroller (DC), op Hallo bekabelde of draadloze bedrijfsnetwerk of via een externe verbinding, zoals een VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="783cf-182">hello device has a direct connection tooyour Domain Controller (DC), either on hello corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="783cf-183">U hebt [uitgerold Hallo functie](##step-3-roll-out-the-feature) toothis-gebruiker met behulp van Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="783cf-183">You have [rolled out hello feature](##step-3-roll-out-the-feature) toothis user using Group Policy.</span></span>

<span data-ttu-id="783cf-184">tootest hello scenario waarbij Hallo gebruiker alleen Hallo gebruikersnaam, maar niet Hallo wachtwoord invoert:</span><span class="sxs-lookup"><span data-stu-id="783cf-184">tootest hello scenario where hello user enters only hello username, but not hello password:</span></span>
- <span data-ttu-id="783cf-185">Meld u aan bij *https://myapps.microsoft.com/* in een nieuwe persoonlijke browsersessie.</span><span class="sxs-lookup"><span data-stu-id="783cf-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="783cf-186">tootest hello scenario waarbij Hallo gebruiker geen tooenter Hallo gebruikersnaam of het Hallo-wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="783cf-186">tootest hello scenario where hello user doesn't have tooenter hello username or hello password:</span></span> 
- <span data-ttu-id="783cf-187">Meld u aan bij *https://myapps.microsoft.com/contoso.onmicrosoft.com* in een nieuwe persoonlijke browsersessie.</span><span class="sxs-lookup"><span data-stu-id="783cf-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="783cf-188">Vervang '*contoso*"met de naam van uw tenant.</span><span class="sxs-lookup"><span data-stu-id="783cf-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="783cf-189">Of meld u aan bij *https://myapps.microsoft.com/contoso.com* in een nieuwe persoonlijke browsersessie.</span><span class="sxs-lookup"><span data-stu-id="783cf-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="783cf-190">Vervang '*contoso.com*' met een geverifieerd domein (niet een federatieve domein) in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="783cf-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="783cf-191">Stap 5: Sleutels rollover</span><span class="sxs-lookup"><span data-stu-id="783cf-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="783cf-192">Azure AD Connect maakt in stap 2 computeraccounts (voor Azure AD) in alle Hallo AD-forests waarop naadloze eenmalige aanmelding is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="783cf-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all hello AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="783cf-193">Meer informatie over meer in detail [hier](active-directory-aadconnect-sso-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="783cf-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="783cf-194">Het wordt aanbevolen dat u vaak Hallo Kerberos-sleutels voor ontsleuteling van deze computeraccounts overschakelen voor betere beveiliging.</span><span class="sxs-lookup"><span data-stu-id="783cf-194">For improved security, it is recommended that  you frequently roll over hello Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="783cf-195">U hoeft niet toodo deze stap _onmiddellijk_ nadat u Hallo-functie hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="783cf-195">You don't need toodo this step _immediately_ after you have enabled hello feature.</span></span> <span data-ttu-id="783cf-196">Hallo Kerberos ontsleutelingssleutels bevatten overschakelen met ten minste elke 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="783cf-196">Roll over hello Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="783cf-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="783cf-197">Next steps</span></span>

- <span data-ttu-id="783cf-198">[**Technische diepgaand** ](active-directory-aadconnect-sso-how-it-works.md) -begrijpen hoe deze functie werkt.</span><span class="sxs-lookup"><span data-stu-id="783cf-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="783cf-199">[**Veelgestelde vragen** ](active-directory-aadconnect-sso-faq.md) -toofrequently vragen worden beantwoord.</span><span class="sxs-lookup"><span data-stu-id="783cf-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="783cf-200">[**Problemen met** ](active-directory-aadconnect-troubleshoot-sso.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="783cf-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="783cf-201">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.</span><span class="sxs-lookup"><span data-stu-id="783cf-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
