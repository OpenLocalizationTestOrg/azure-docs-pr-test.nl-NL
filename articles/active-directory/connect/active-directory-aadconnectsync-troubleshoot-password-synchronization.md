---
title: aaaTroubleshoot Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie | Microsoft Docs
description: In dit artikel bevat informatie over het tootroubleshoot wachtwoord synchronisatieproblemen.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="d7b62-103">Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie oplossen</span><span class="sxs-lookup"><span data-stu-id="d7b62-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="d7b62-104">In dit onderwerp bevat stappen voor hoe tootroubleshoot met synchronisatie van wachtwoorden problemen.</span><span class="sxs-lookup"><span data-stu-id="d7b62-104">This topic provides steps for how tootroubleshoot issues with password synchronization.</span></span> <span data-ttu-id="d7b62-105">Als wachtwoorden zijn niet zoals verwacht wordt gesynchroniseerd, kan het zijn voor een subset van gebruikers of voor alle gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d7b62-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="d7b62-106">Voor Azure Active Directory (Azure AD) implementatie verbinden met versie 1.1.524.0 of hoger, er is nu een diagnostische cmdlet waarmee u tootroubleshoot wachtwoord synchronisatieproblemen kunt:</span><span class="sxs-lookup"><span data-stu-id="d7b62-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use tootroubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="d7b62-107">Als er een probleem waarbij geen wachtwoorden worden gesynchroniseerd, raadpleegt u toohello [geen wachtwoorden worden gesynchroniseerd: problemen oplossen met behulp van de diagnostische cmdlet Hallo](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) sectie.</span><span class="sxs-lookup"><span data-stu-id="d7b62-107">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="d7b62-108">Als u een probleem met de afzonderlijke objecten hebt, raadpleegt u toohello [één object worden wachtwoorden niet gesynchroniseerd: problemen oplossen met behulp van de diagnostische cmdlet Hallo](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) sectie.</span><span class="sxs-lookup"><span data-stu-id="d7b62-108">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="d7b62-109">Voor oudere versies van Azure AD Connect-implementatie:</span><span class="sxs-lookup"><span data-stu-id="d7b62-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="d7b62-110">Als er een probleem waarbij geen wachtwoorden worden gesynchroniseerd, raadpleegt u toohello [geen wachtwoorden worden gesynchroniseerd: handmatige stappen voor probleemoplossing](#no-passwords-are-synchronized-manual-troubleshooting-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="d7b62-110">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="d7b62-111">Als u een probleem met de afzonderlijke objecten hebt, raadpleegt u toohello [één object worden wachtwoorden niet gesynchroniseerd: handmatige stappen voor probleemoplossing](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="d7b62-111">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="d7b62-112">Er is geen wachtwoorden worden gesynchroniseerd: problemen oplossen met behulp van de diagnostische cmdlet Hallo</span><span class="sxs-lookup"><span data-stu-id="d7b62-112">No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="d7b62-113">U kunt Hallo `Invoke-ADSyncDiagnostics` cmdlet toofigure uit waarom geen wachtwoorden worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="d7b62-113">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toofigure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="d7b62-114">Hallo `Invoke-ADSyncDiagnostics` cmdlet is alleen beschikbaar voor Azure AD Connect versie 1.1.524.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d7b62-114">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="d7b62-115">Hallo diagnostics cmdlet uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d7b62-115">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="d7b62-116">tootroubleshoot problemen waar geen wachtwoorden worden gesynchroniseerd:</span><span class="sxs-lookup"><span data-stu-id="d7b62-116">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="d7b62-117">Open een nieuw Windows PowerShell-sessie op de server van uw Azure AD Connect met Hallo **als Administrator uitvoeren** optie.</span><span class="sxs-lookup"><span data-stu-id="d7b62-117">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="d7b62-118">Voer `Set-ExecutionPolicy RemoteSigned` of `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="d7b62-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="d7b62-119">Voer `Import-Module ADSyncDiagnostics` uit.</span><span class="sxs-lookup"><span data-stu-id="d7b62-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="d7b62-120">Voer `Invoke-ADSyncDiagnostics -PasswordSync` uit.</span><span class="sxs-lookup"><span data-stu-id="d7b62-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="d7b62-121">Resultaten van de cmdlet Hallo Hallo begrijpen</span><span class="sxs-lookup"><span data-stu-id="d7b62-121">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="d7b62-122">Hallo diagnostische cmdlet voert controles Hallo:</span><span class="sxs-lookup"><span data-stu-id="d7b62-122">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="d7b62-123">Valideert dat Hallo wachtwoordfunctie voor synchronisatie is ingeschakeld voor uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="d7b62-123">Validates that hello password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="d7b62-124">Valideert dat hello Azure AD Connect server niet in de faseringsmodus is.</span><span class="sxs-lookup"><span data-stu-id="d7b62-124">Validates that hello Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="d7b62-125">Voor elk bestaand on-premises Active Directory-connector (die overeenkomt met de bestaande Active Directory-forest tooan):</span><span class="sxs-lookup"><span data-stu-id="d7b62-125">For each existing on-premises Active Directory connector (which corresponds tooan existing Active Directory forest):</span></span>

   * <span data-ttu-id="d7b62-126">Valideert dat Hallo wachtwoordfunctie voor synchronisatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d7b62-126">Validates that hello password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="d7b62-127">Hiermee zoekt u wachtwoord synchronisatie heartbeat gebeurtenissen in Hallo Windows toepassing gebeurtenislogboeken.</span><span class="sxs-lookup"><span data-stu-id="d7b62-127">Searches for password synchronization heartbeat events in hello Windows Application Event logs.</span></span>

   * <span data-ttu-id="d7b62-128">Voor elk Active Directory-domein onder Hallo lokale Active Directory-connector:</span><span class="sxs-lookup"><span data-stu-id="d7b62-128">For each Active Directory domain under hello on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="d7b62-129">Valideert dat Hallo domein kan worden bereikt vanaf hello Azure AD Connect-server.</span><span class="sxs-lookup"><span data-stu-id="d7b62-129">Validates that hello domain is reachable from hello Azure AD Connect server.</span></span>

      * <span data-ttu-id="d7b62-130">Valideert dat Hallo Active Directory Domain Services (AD DS)-accounts die worden gebruikt door Hallo lokale Active Directory-connector heeft Hallo juiste gebruikersnaam, wachtwoord en machtigingen die vereist zijn voor Wachtwoordsynchronisatie.</span><span class="sxs-lookup"><span data-stu-id="d7b62-130">Validates that hello Active Directory Domain Services (AD DS) accounts used by hello on-premises Active Directory connector has hello correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="d7b62-131">Hallo volgende diagram illustreert Hallo resultaten van het Hallo-cmdlet voor een lokale Active Directory-topologie van één domein:</span><span class="sxs-lookup"><span data-stu-id="d7b62-131">hello following diagram illustrates hello results of hello cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Diagnostische uitvoer voor Wachtwoordsynchronisatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="d7b62-133">Hallo rest van deze sectie beschrijft specifieke resultaten die zijn geretourneerd door de cmdlet Hallo en bijbehorende problemen.</span><span class="sxs-lookup"><span data-stu-id="d7b62-133">hello rest of this section describes specific results that are returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="d7b62-134">De synchronisatiefunctie wachtwoord is niet ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="d7b62-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="d7b62-135">Als u dit nog niet hebt Wachtwoordsynchronisatie met behulp van hello Azure AD Connect-wizard ingeschakeld, wordt de Hallo volgende fout geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d7b62-135">If you haven't enabled password synchronization by using hello Azure AD Connect wizard, hello following error is returned:</span></span>

![Wachtwoordsynchronisatie is niet ingeschakeld](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="d7b62-137">Azure AD Connect-server is in de faseringsmodus</span><span class="sxs-lookup"><span data-stu-id="d7b62-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="d7b62-138">Wachtwoordsynchronisatie is tijdelijk uitgeschakeld als hello Azure AD Connect-server in de faseringsmodus is, en hello volgende fout is geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d7b62-138">If hello Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and hello following error is returned:</span></span>

![Azure AD Connect-server is in de faseringsmodus](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="d7b62-140">Er zijn geen wachtwoord synchronisatie heartbeat-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="d7b62-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="d7b62-141">Elke lokale Active Directory-connector heeft een eigen synchronisatiekanaal wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d7b62-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="d7b62-142">Wanneer Hallo wachtwoord synchronisatiekanaal tot stand is gebracht en er wachtwoord wijzigingen toobe gesynchroniseerd zijn, wordt elke 30 minuten onder Hallo Windows-toepassingslogboek gegenereerd in een heartbeat-gebeurtenis (EventId 654).</span><span class="sxs-lookup"><span data-stu-id="d7b62-142">When hello password synchronization channel is established and there aren't any password changes toobe synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under hello Windows Application Event Log.</span></span> <span data-ttu-id="d7b62-143">Voor elke lokale Active Directory-connector Hallo cmdlet wordt gezocht naar overeenkomende heartbeat-gebeurtenissen in Hallo afgelopen drie uur.</span><span class="sxs-lookup"><span data-stu-id="d7b62-143">For each on-premises Active Directory connector, hello cmdlet searches for corresponding heartbeat events in hello past three hours.</span></span> <span data-ttu-id="d7b62-144">Als er geen heartbeat-gebeurtenis wordt gevonden, hello volgende fout is geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d7b62-144">If no heartbeat event is found, hello following error is returned:</span></span>

![Er is geen wachtwoord synchronisatie hartslag gebeurtenis](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="d7b62-146">AD DS-account heeft geen juiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="d7b62-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="d7b62-147">Als Hallo AD DS-account dat wordt gebruikt door Hallo on-premises Active Directory-connector toosynchronize wachtwoord-hashes heeft geen juiste machtigingen Hallo is Hallo volgende fout geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d7b62-147">If hello AD DS account that's used by hello on-premises Active Directory connector toosynchronize password hashes does not have hello appropriate permissions, hello following error is returned:</span></span>

![Onjuiste referenties](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="d7b62-149">Onjuiste gebruikersnaam van de AD DS-account of wachtwoord</span><span class="sxs-lookup"><span data-stu-id="d7b62-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="d7b62-150">Als hello AD DS-account gebruikt door hello lokale Active Directory-connector toosynchronize wachtwoord-hashes heeft een onjuiste gebruikersnaam of wachtwoord, hello volgende fout is geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d7b62-150">If hello AD DS account used by hello on-premises Active Directory connector toosynchronize password hashes has an incorrect username or password, hello following error is returned:</span></span>

![Onjuiste referenties](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="d7b62-152">Wachtwoorden niet kan één object worden gesynchroniseerd: problemen oplossen met behulp van de diagnostische cmdlet Hallo</span><span class="sxs-lookup"><span data-stu-id="d7b62-152">One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="d7b62-153">U kunt Hallo `Invoke-ADSyncDiagnostics` cmdlet toodetermine waarom één object wachtwoorden niet wordt gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="d7b62-153">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="d7b62-154">Hallo `Invoke-ADSyncDiagnostics` cmdlet is alleen beschikbaar voor Azure AD Connect versie 1.1.524.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d7b62-154">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="d7b62-155">Hallo diagnostics cmdlet uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d7b62-155">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="d7b62-156">tootroubleshoot problemen waar geen wachtwoorden worden gesynchroniseerd:</span><span class="sxs-lookup"><span data-stu-id="d7b62-156">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="d7b62-157">Open een nieuw Windows PowerShell-sessie op de server van uw Azure AD Connect met Hallo **als Administrator uitvoeren** optie.</span><span class="sxs-lookup"><span data-stu-id="d7b62-157">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="d7b62-158">Voer `Set-ExecutionPolicy RemoteSigned` of `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="d7b62-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="d7b62-159">Voer `Import-Module ADSyncDiagnostics` uit.</span><span class="sxs-lookup"><span data-stu-id="d7b62-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="d7b62-160">Voer Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d7b62-160">Run hello following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="d7b62-161">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d7b62-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="d7b62-162">Resultaten van de cmdlet Hallo Hallo begrijpen</span><span class="sxs-lookup"><span data-stu-id="d7b62-162">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="d7b62-163">Hallo diagnostische cmdlet voert controles Hallo:</span><span class="sxs-lookup"><span data-stu-id="d7b62-163">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="d7b62-164">Hallo-status van Active Directory-object in de adresruimte van Hallo Active Directory-connector, Metaverse en Azure Hallo onderzoekt AD connectorgebied overgebracht.</span><span class="sxs-lookup"><span data-stu-id="d7b62-164">Examines hello state of hello Active Directory object in hello Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="d7b62-165">Controleert of er synchronisatieregels Wachtwoordsynchronisatie is ingeschakeld en toohello Active Directory-object worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="d7b62-165">Validates that there are synchronization rules with password synchronization enabled and applied toohello Active Directory object.</span></span>

* <span data-ttu-id="d7b62-166">Pogingen tooretrieve en weergave Hallo resultaten van Hallo laatste poging toosynchronize Hallo wachtwoord voor Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="d7b62-166">Attempts tooretrieve and display hello results of hello last attempt toosynchronize hello password for hello object.</span></span>

<span data-ttu-id="d7b62-167">Hallo volgende diagram illustreert Hallo resultaten van de cmdlet Hallo wanneer u problemen met Wachtwoordsynchronisatie voor één object:</span><span class="sxs-lookup"><span data-stu-id="d7b62-167">hello following diagram illustrates hello results of hello cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Diagnostische uitvoer voor Wachtwoordsynchronisatie - enkel object](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="d7b62-169">Hallo rest van deze sectie beschrijft specifieke resultaten geretourneerd door de cmdlet Hallo en bijbehorende problemen.</span><span class="sxs-lookup"><span data-stu-id="d7b62-169">hello rest of this section describes specific results returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a><span data-ttu-id="d7b62-170">Hallo Active Directory-object is niet de geëxporteerde tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="d7b62-170">hello Active Directory object isn't exported tooAzure AD</span></span>
<span data-ttu-id="d7b62-171">Wachtwoordsynchronisatie voor deze lokale Active Directory-account is mislukt omdat er geen bijbehorende object in hello Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="d7b62-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in hello Azure AD tenant.</span></span> <span data-ttu-id="d7b62-172">Hallo volgende fout is geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d7b62-172">hello following error is returned:</span></span>

![Azure AD-object ontbreekt.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="d7b62-174">Gebruiker heeft een tijdelijk wachtwoord</span><span class="sxs-lookup"><span data-stu-id="d7b62-174">User has a temporary password</span></span>
<span data-ttu-id="d7b62-175">Azure AD Connect ondersteunt momenteel geen tijdelijke wachtwoorden synchroniseren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7b62-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="d7b62-176">Een wachtwoord wordt beschouwd als toobe tijdelijke als hello **wachtwoord bij volgende aanmelding wijzigen** optie is ingesteld op Hallo on-premises Active Directory-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d7b62-176">A password is considered toobe temporary if hello **Change password at next logon** option is set on hello on-premises Active Directory user.</span></span> <span data-ttu-id="d7b62-177">Hallo volgende fout is geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d7b62-177">hello following error is returned:</span></span>

![Tijdelijke wachtwoord wordt niet geëxporteerd.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a><span data-ttu-id="d7b62-179">Resultaten van de laatste poging toosynchronize wachtwoord niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="d7b62-179">Results of last attempt toosynchronize password aren't available</span></span>
<span data-ttu-id="d7b62-180">Azure AD Connect slaat standaard Hallo resultaten van synchronisatiepogingen van wachtwoord voor de zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="d7b62-180">By default, Azure AD Connect stores hello results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="d7b62-181">Als er geen resultaten beschikbaar voor Active Directory-object Hallo geselecteerd zijn, wordt Hallo volgende waarschuwing geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="d7b62-181">If there are no results available for hello selected Active Directory object, hello following warning is returned:</span></span>

![Diagnostische uitvoer voor één object - geen wachtwoordgeschiedenis voor synchronisatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="d7b62-183">Er is geen wachtwoorden worden gesynchroniseerd: handmatige stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="d7b62-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="d7b62-184">Volg deze stappen toodetermine waarom geen wachtwoorden worden gesynchroniseerd:</span><span class="sxs-lookup"><span data-stu-id="d7b62-184">Follow these steps toodetermine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="d7b62-185">Hallo-Connect-server in [faseringsmodus](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="d7b62-185">Is hello Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="d7b62-186">Een server in de faseringsmodus wachtwoorden niet wordt gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="d7b62-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="d7b62-187">Hallo-script uitvoeren in Hallo [Hallo status van wachtwoord synchronisatie-instellingen ophalen](#get-the-status-of-password-sync-settings) sectie.</span><span class="sxs-lookup"><span data-stu-id="d7b62-187">Run hello script in hello [Get hello status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="d7b62-188">Dit biedt u een overzicht van de configuratie van Hallo wachtwoord synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="d7b62-188">It gives you an overview of hello password sync configuration.</span></span>  

    ![PowerShell-scriptuitvoer van de synchronisatie-instellingen voor wachtwoord](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="d7b62-190">Hallo Connect-installatiewizard als Hallo-functie niet is ingeschakeld in Azure AD of als het Hallo-synchronisatiestatus kanaal niet is ingeschakeld, worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d7b62-190">If hello feature is not enabled in Azure AD or if hello sync channel status is not enabled, run hello Connect installation wizard.</span></span> <span data-ttu-id="d7b62-191">Selecteer **aanpassen Synchronisatieopties**, en Wachtwoordsynchronisatie te deselecteren. Deze wijziging worden Hallo functie tijdelijk uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d7b62-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables hello feature.</span></span> <span data-ttu-id="d7b62-192">Vervolgens voert u de wizard Hallo opnieuw en Wachtwoordsynchronisatie opnieuw in te schakelen. Hallo-script uitvoeren opnieuw tooverify die Hallo configuratie juist is.</span><span class="sxs-lookup"><span data-stu-id="d7b62-192">Then run hello wizard again and re-enable password sync. Run hello script again tooverify that hello configuration is correct.</span></span>

4. <span data-ttu-id="d7b62-193">Kijk in het Hallo-gebeurtenislogboek op fouten.</span><span class="sxs-lookup"><span data-stu-id="d7b62-193">Look in hello event log for errors.</span></span> <span data-ttu-id="d7b62-194">Zoek naar Hallo gebeurtenissen die op een probleem duiden op te volgen:</span><span class="sxs-lookup"><span data-stu-id="d7b62-194">Look for hello following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="d7b62-195">Bron: 'Adreslijstsynchronisatie' ID: 0, 611, 652, 655 als u deze gebeurtenissen, ziet u hebt een verbindingsprobleem.</span><span class="sxs-lookup"><span data-stu-id="d7b62-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="d7b62-196">Hallo-bericht van gebeurtenislogboek beschreven forest waar u problemen ondervindt.</span><span class="sxs-lookup"><span data-stu-id="d7b62-196">hello event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="d7b62-197">Zie voor meer informatie [verbindingsprobleem](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="d7b62-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="d7b62-198">Als er geen heartbeat of niets anders gewerkt, uitvoeren [activeren van een volledige synchronisatie van wachtwoorden voor alle](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="d7b62-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="d7b62-199">Hallo script slechts eenmaal worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d7b62-199">Run hello script only once.</span></span>

6. <span data-ttu-id="d7b62-200">Zie Hallo [oplossen van één object dat wachtwoorden niet synchroniseert](#one-object-is-not-synchronizing-passwords) sectie.</span><span class="sxs-lookup"><span data-stu-id="d7b62-200">See hello [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="d7b62-201">Verbindingsproblemen</span><span class="sxs-lookup"><span data-stu-id="d7b62-201">Connectivity problems</span></span>

<span data-ttu-id="d7b62-202">Hebt u verbinding met Azure AD?</span><span class="sxs-lookup"><span data-stu-id="d7b62-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="d7b62-203">Hallo-account vereist machtigingen tooread Hallo wachtwoord-hashes in alle domeinen?</span><span class="sxs-lookup"><span data-stu-id="d7b62-203">Does hello account have required permissions tooread hello password hashes in all domains?</span></span> <span data-ttu-id="d7b62-204">Als u verbinding maken met behulp van snelle instellingen hebt geïnstalleerd, kunnen Hallo machtigingen moeten al zijn juist.</span><span class="sxs-lookup"><span data-stu-id="d7b62-204">If you installed Connect by using Express settings, hello permissions should already be correct.</span></span> 

<span data-ttu-id="d7b62-205">Als u aangepaste installatie gebruikt, Hallo machtigingen handmatig instellen door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="d7b62-205">If you used custom installation, set hello permissions manually by doing hello following:</span></span>
    
1. <span data-ttu-id="d7b62-206">toofind hello account dat wordt gebruikt door Hallo Active Directory-connector start **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-206">toofind hello account used by hello Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="d7b62-207">Ga te**Connectors**, en zoek vervolgens naar Hallo lokale Active Directory-forest die u wilt oplossen.</span><span class="sxs-lookup"><span data-stu-id="d7b62-207">Go too**Connectors**, and then search for hello on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="d7b62-208">Selecteer Hallo-connector en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-208">Select hello connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="d7b62-209">Ga te**tooActive Directory-Forest verbinding**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-209">Go too**Connect tooActive Directory Forest**.</span></span>  
    
    ![Account dat wordt gebruikt door Active Directory-connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="d7b62-211">Houd er rekening mee Hallo gebruikersnaam en het Hallo-domein waar Hallo account zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="d7b62-211">Note hello username and hello domain where hello account is located.</span></span>
    
5. <span data-ttu-id="d7b62-212">Start **Active Directory: gebruikers en Computers**, en controleer vervolgens of Hallo-account die u eerder hebt gevonden Hallo Volg machtigingen zijn ingesteld in de hoofdmap Hallo van alle domeinen in uw forest heeft:</span><span class="sxs-lookup"><span data-stu-id="d7b62-212">Start **Active Directory Users and Computers**, and then verify that hello account you found earlier has hello follow permissions set at hello root of all domains in your forest:</span></span>
    * <span data-ttu-id="d7b62-213">Directorywijzigingen repliceren</span><span class="sxs-lookup"><span data-stu-id="d7b62-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="d7b62-214">Alle repliceren Directory gewijzigd</span><span class="sxs-lookup"><span data-stu-id="d7b62-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="d7b62-215">Hallo-domeincontrollers kunnen worden bereikt door Azure AD Connect zijn?</span><span class="sxs-lookup"><span data-stu-id="d7b62-215">Are hello domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="d7b62-216">Als het Hallo-Connect-server kan geen verbinding met het maken van domeincontrollers tooall, configureert u **voorkeur domeincontroller alleen gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-216">If hello Connect server cannot connect tooall domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![-Domeincontroller die wordt gebruikt door Active Directory-connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="d7b62-218">Ga terug te**Synchronization Service Manager** en **mappartitie configureren**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-218">Go back too**Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="d7b62-219">Selecteer uw domein in **mappartities selecteren**, selecteer Hallo **alleen gebruiken voorkeur domeincontrollers** selectievakje en klik vervolgens op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-219">Select your domain in **Select directory partitions**, select hello **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="d7b62-220">Voer in lijst Hallo Hallo-domeincontrollers die verbinding voor Wachtwoordsynchronisatie gebruiken moet. Hallo dezelfde lijst wordt gebruikt voor het importeren en exporteren ook.</span><span class="sxs-lookup"><span data-stu-id="d7b62-220">In hello list, enter hello domain controllers that Connect should use for password sync. hello same list is used for import and export as well.</span></span> <span data-ttu-id="d7b62-221">Voer deze stappen uit voor alle domeinen.</span><span class="sxs-lookup"><span data-stu-id="d7b62-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="d7b62-222">Als Hallo script wordt aangegeven dat er geen heartbeat, Hallo-script uitvoeren [activeren van een volledige synchronisatie van wachtwoorden voor alle](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="d7b62-222">If hello script shows that there is no heartbeat, run hello script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="d7b62-223">Wachtwoorden niet kan één object worden gesynchroniseerd: handmatige stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="d7b62-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="d7b62-224">U kunt eenvoudig wachtwoord synchronisatieproblemen aan de hand van de status van een object Hallo oplossen.</span><span class="sxs-lookup"><span data-stu-id="d7b62-224">You can easily troubleshoot password synchronization issues by reviewing hello status of an object.</span></span>

1. <span data-ttu-id="d7b62-225">In **Active Directory: gebruikers en Computers**, zoeken naar Hallo gebruiker en controleer vervolgens dat Hallo **gebruiker moet wachtwoord bij volgende aanmelding wijzigen** selectievakje is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d7b62-225">In **Active Directory Users and Computers**, search for hello user, and then verify that hello **User must change password at next logon** check box is cleared.</span></span>  

    ![Active Directory-productief wachtwoorden](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="d7b62-227">Hallo selectievakje is ingeschakeld, vraagt u Hallo gebruiker toosign in als Hallo wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d7b62-227">If hello check box is selected, ask hello user toosign in and change hello password.</span></span> <span data-ttu-id="d7b62-228">Tijdelijke wachtwoorden zijn niet gesynchroniseerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7b62-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="d7b62-229">Hallo wachtwoord ziet er juist in Active Directory, volg Hallo-gebruiker in Hallo synchronisatie-engine.</span><span class="sxs-lookup"><span data-stu-id="d7b62-229">If hello password looks correct in Active Directory, follow hello user in hello sync engine.</span></span> <span data-ttu-id="d7b62-230">Volgende Hallo gebruiker van de lokale Active Directory tooAzure AD, kunt u zien of er een beschrijvend foutbericht op Hallo-object is.</span><span class="sxs-lookup"><span data-stu-id="d7b62-230">By following hello user from on-premises Active Directory tooAzure AD, you can see whether there is a descriptive error on hello object.</span></span>

    <span data-ttu-id="d7b62-231">a.</span><span class="sxs-lookup"><span data-stu-id="d7b62-231">a.</span></span> <span data-ttu-id="d7b62-232">Hallo Start [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="d7b62-232">Start hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="d7b62-233">b.</span><span class="sxs-lookup"><span data-stu-id="d7b62-233">b.</span></span> <span data-ttu-id="d7b62-234">Klik op **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-234">Click **Connectors**.</span></span>

    <span data-ttu-id="d7b62-235">c.</span><span class="sxs-lookup"><span data-stu-id="d7b62-235">c.</span></span> <span data-ttu-id="d7b62-236">Selecteer Hallo **Active Directory-Connector** waar Hallo gebruiker zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="d7b62-236">Select hello **Active Directory Connector** where hello user is located.</span></span>

    <span data-ttu-id="d7b62-237">d.</span><span class="sxs-lookup"><span data-stu-id="d7b62-237">d.</span></span> <span data-ttu-id="d7b62-238">Selecteer **Connectorgebied zoeken**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="d7b62-239">e.</span><span class="sxs-lookup"><span data-stu-id="d7b62-239">e.</span></span> <span data-ttu-id="d7b62-240">In Hallo **bereik** de optie **DN-naam of het anker**, en voer de volledige DN Hallo van Hallo-gebruiker die u wilt oplossen.</span><span class="sxs-lookup"><span data-stu-id="d7b62-240">In hello **Scope** box, select **DN or Anchor**, and then enter hello full DN of hello user you are troubleshooting.</span></span>

    ![Zoeken naar de gebruiker in de connectorruimte met de DN-naam](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="d7b62-242">f.</span><span class="sxs-lookup"><span data-stu-id="d7b62-242">f.</span></span> <span data-ttu-id="d7b62-243">Hallo gebruiker die u zoekt, en klik vervolgens op Zoeken **eigenschappen** toosee alle kenmerken Hallo.</span><span class="sxs-lookup"><span data-stu-id="d7b62-243">Locate hello user you are looking for, and then click **Properties** toosee all hello attributes.</span></span> <span data-ttu-id="d7b62-244">Als het Hallo-gebruiker zich niet in de zoekresultaten hello, controleert u of uw [filterregels](active-directory-aadconnectsync-configure-filtering.md) en zorg ervoor dat u uitvoert [toepassen en controleer of de wijzigingen](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) voor Hallo gebruiker tooappear in verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="d7b62-244">If hello user is not in hello search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for hello user tooappear in Connect.</span></span>

    <span data-ttu-id="d7b62-245">g.</span><span class="sxs-lookup"><span data-stu-id="d7b62-245">g.</span></span> <span data-ttu-id="d7b62-246">Klik op toosee Hallo wachtwoord sync details van Hallo-object voor Hallo afgelopen week **logboek**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-246">toosee hello password sync details of hello object for hello past week, click **Log**.</span></span>  

    ![Object-logboekgegevens](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="d7b62-248">Als Hallo object logboek leeg is, is Azure AD Connect kan niet tooread Hallo wachtwoord-hash van Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7b62-248">If hello object log is empty, Azure AD Connect has been unable tooread hello password hash from Active Directory.</span></span> <span data-ttu-id="d7b62-249">Gaat u uw verder met [Connectiviteitsfouten](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="d7b62-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="d7b62-250">Als er een andere waarde dan **geslaagd**, raadpleegt u de tabel toohello in [wachtwoord sync logboek](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="d7b62-250">If you see any other value than **success**, refer toohello table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="d7b62-251">h.</span><span class="sxs-lookup"><span data-stu-id="d7b62-251">h.</span></span> <span data-ttu-id="d7b62-252">Selecteer Hallo **afkomst** tabblad en zorg ervoor dat ten minste één synchronisatieregel in Hallo **PasswordSync** kolom is **True**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-252">Select hello **lineage** tab, and make sure that at least one sync rule in hello **PasswordSync** column is **True**.</span></span> <span data-ttu-id="d7b62-253">In de standaardconfiguratie Hallo Hallo-naam van de synchronisatieregel Hallo is **In uit Active Directory - gebruiker AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-253">In hello default configuration, hello name of hello sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Informatie over een gebruiker Lineage](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="d7b62-255">ik.</span><span class="sxs-lookup"><span data-stu-id="d7b62-255">i.</span></span> <span data-ttu-id="d7b62-256">Klik op **eigenschappen Metaverse-Object** toodisplay een lijst met gebruikerskenmerken.</span><span class="sxs-lookup"><span data-stu-id="d7b62-256">Click **Metaverse Object Properties** toodisplay a list of user attributes.</span></span>  

    ![Metaverse-informatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="d7b62-258">Controleer of er geen **cloudFiltered** kenmerk aanwezig.</span><span class="sxs-lookup"><span data-stu-id="d7b62-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="d7b62-259">Zorg ervoor dat Hallo Domeinkenmerken (domainFQDN en domainNetBios) Hallo verwachte waarden hebben.</span><span class="sxs-lookup"><span data-stu-id="d7b62-259">Make sure that hello domain attributes (domainFQDN and domainNetBios) have hello expected values.</span></span>

    <span data-ttu-id="d7b62-260">j.</span><span class="sxs-lookup"><span data-stu-id="d7b62-260">j.</span></span> <span data-ttu-id="d7b62-261">Klik op Hallo **Connectors** tabblad. Zorg ervoor dat u connectors tooboth ziet op lokale Active Directory en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7b62-261">Click hello **Connectors** tab. Make sure that you see connectors tooboth on-premises Active Directory and Azure AD.</span></span>

    ![Metaverse-informatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="d7b62-263">k.</span><span class="sxs-lookup"><span data-stu-id="d7b62-263">k.</span></span> <span data-ttu-id="d7b62-264">Selecteer Hallo rij voor Azure AD, klikt u op **eigenschappen**, en klik vervolgens op Hallo **afkomst** tabblad Hallo connector space-object moet een uitgaande regel in Hallo **PasswordSync** kolomset te**True**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-264">Select hello row that represents Azure AD, click **Properties**, and then click hello **Lineage** tab. hello connector space object should have an outbound rule in hello **PasswordSync** column set too**True**.</span></span> <span data-ttu-id="d7b62-265">In de standaardconfiguratie Hallo Hallo-naam van de synchronisatieregel Hallo is **uit tooAAD - gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-265">In hello default configuration, hello name of hello sync rule is **Out tooAAD - User Join**.</span></span>  

    ![Dialoogvenster voor eigenschappen van het Object ruimte connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="d7b62-267">Wachtwoord sync-logboek</span><span class="sxs-lookup"><span data-stu-id="d7b62-267">Password sync log</span></span>
<span data-ttu-id="d7b62-268">de kolom status Hallo kan Hallo volgende waarden hebben:</span><span class="sxs-lookup"><span data-stu-id="d7b62-268">hello status column can have hello following values:</span></span>

| <span data-ttu-id="d7b62-269">Status</span><span class="sxs-lookup"><span data-stu-id="d7b62-269">Status</span></span> | <span data-ttu-id="d7b62-270">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d7b62-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d7b62-271">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="d7b62-271">Success</span></span> |<span data-ttu-id="d7b62-272">Wachtwoord is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="d7b62-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="d7b62-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="d7b62-273">FilteredByTarget</span></span> |<span data-ttu-id="d7b62-274">Wachtwoord wordt ingesteld, te**gebruiker moet wachtwoord bij volgende aanmelding wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="d7b62-274">Password is set too**User must change password at next logon**.</span></span> <span data-ttu-id="d7b62-275">Wachtwoord is niet gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="d7b62-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="d7b62-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="d7b62-276">NoTargetConnection</span></span> |<span data-ttu-id="d7b62-277">Er is geen object in Hallo metaverse of in de ruimte van hello Azure AD-connector.</span><span class="sxs-lookup"><span data-stu-id="d7b62-277">No object in hello metaverse or in hello Azure AD connector space.</span></span> |
| <span data-ttu-id="d7b62-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="d7b62-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="d7b62-279">Er is geen object gevonden in Hallo lokale Active Directory-connectorruimte.</span><span class="sxs-lookup"><span data-stu-id="d7b62-279">No object found in hello on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="d7b62-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="d7b62-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="d7b62-281">Hallo-object in hello Azure AD-connectorruimte is nog niet geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="d7b62-281">hello object in hello Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="d7b62-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="d7b62-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="d7b62-283">Logboekvermelding is gemaakt voordat de build 1.0.9125.0 en wordt weergegeven in de oude status.</span><span class="sxs-lookup"><span data-stu-id="d7b62-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="d7b62-284">Fout</span><span class="sxs-lookup"><span data-stu-id="d7b62-284">Error</span></span> |<span data-ttu-id="d7b62-285">Service heeft een onbekende fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="d7b62-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="d7b62-286">Onbekend</span><span class="sxs-lookup"><span data-stu-id="d7b62-286">Unknown</span></span> |<span data-ttu-id="d7b62-287">Er is een fout opgetreden tijdens een poging tooprocess een batch wachtwoord-hashes.</span><span class="sxs-lookup"><span data-stu-id="d7b62-287">An error occurred while trying tooprocess a batch of password hashes.</span></span>  |
| <span data-ttu-id="d7b62-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="d7b62-288">MissingAttribute</span></span> |<span data-ttu-id="d7b62-289">Specifieke kenmerken die vereist zijn door Azure AD Domain Services (bijvoorbeeld, Kerberos-hash) zijn niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="d7b62-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="d7b62-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="d7b62-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="d7b62-291">Specifieke kenmerken die vereist zijn door Azure AD Domain Services (bijvoorbeeld, Kerberos-hash) was eerder niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="d7b62-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="d7b62-292">Een poging tooresynchronize Hallo gebruiker wachtwoord-hash wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d7b62-292">An attempt tooresynchronize hello user's password hash is made.</span></span> |

## <a name="scripts-toohelp-troubleshooting"></a><span data-ttu-id="d7b62-293">Scripts toohelp probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="d7b62-293">Scripts toohelp troubleshooting</span></span>

### <a name="get-hello-status-of-password-sync-settings"></a><span data-ttu-id="d7b62-294">Hallo-status van wachtwoord synchronisatie-instellingen ophalen</span><span class="sxs-lookup"><span data-stu-id="d7b62-294">Get hello status of password sync settings</span></span>
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="d7b62-295">Activeren van een volledige synchronisatie van alle wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="d7b62-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="d7b62-296">Dit script wordt slechts één keer uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d7b62-296">Run this script only once.</span></span> <span data-ttu-id="d7b62-297">Als u toorun deze meer dan één keer moet, is iets anders Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="d7b62-297">If you need toorun it more than once, something else is hello problem.</span></span> <span data-ttu-id="d7b62-298">tootroubleshoot hello probleem contact op met Microsoft ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="d7b62-298">tootroubleshoot hello problem, contact Microsoft support.</span></span>

<span data-ttu-id="d7b62-299">U kunt een volledige synchronisatie van alle wachtwoorden activeren met behulp van Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="d7b62-299">You can trigger a full sync of all passwords by using hello following script:</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a><span data-ttu-id="d7b62-300">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d7b62-300">Next steps</span></span>
* [<span data-ttu-id="d7b62-301">Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie implementeren</span><span class="sxs-lookup"><span data-stu-id="d7b62-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="d7b62-302">Azure AD Connect-synchronisatie: Synchronisatie-opties voor aanpassen</span><span class="sxs-lookup"><span data-stu-id="d7b62-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="d7b62-303">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7b62-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
