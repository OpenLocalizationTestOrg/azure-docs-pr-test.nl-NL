---
title: Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie oplossen | Microsoft Docs
description: In dit artikel bevat informatie over het oplossen van problemen met synchronisatie van wachtwoorden.
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
ms.openlocfilehash: 33fa6a8867764975a57b8727e7705529d1d7506a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="decbe-103">Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie oplossen</span><span class="sxs-lookup"><span data-stu-id="decbe-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="decbe-104">Dit onderwerp bevat stappen voor het oplossen van problemen met synchronisatie van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="decbe-104">This topic provides steps for how to troubleshoot issues with password synchronization.</span></span> <span data-ttu-id="decbe-105">Als wachtwoorden zijn niet zoals verwacht wordt gesynchroniseerd, kan het zijn voor een subset van gebruikers of voor alle gebruikers.</span><span class="sxs-lookup"><span data-stu-id="decbe-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="decbe-106">Voor Azure Active Directory (Azure AD) implementatie verbinden met versie 1.1.524.0 of hoger, er is nu een diagnostische cmdlet kunt u problemen met synchronisatie wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="decbe-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use to troubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="decbe-107">Als er een probleem waarbij geen wachtwoorden worden gesynchroniseerd, raadpleegt u de [geen wachtwoorden worden gesynchroniseerd: oplossen met behulp van de diagnostische cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) sectie.</span><span class="sxs-lookup"><span data-stu-id="decbe-107">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="decbe-108">Als u een probleem met de afzonderlijke objecten hebt, raadpleegt u de [één object worden wachtwoorden niet gesynchroniseerd: oplossen met behulp van de diagnostische cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) sectie.</span><span class="sxs-lookup"><span data-stu-id="decbe-108">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="decbe-109">Voor oudere versies van Azure AD Connect-implementatie:</span><span class="sxs-lookup"><span data-stu-id="decbe-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="decbe-110">Als er een probleem waarbij geen wachtwoorden worden gesynchroniseerd, raadpleegt u de [geen wachtwoorden worden gesynchroniseerd: handmatige stappen voor probleemoplossing](#no-passwords-are-synchronized-manual-troubleshooting-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="decbe-110">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="decbe-111">Als u een probleem met de afzonderlijke objecten hebt, raadpleegt u de [één object worden wachtwoorden niet gesynchroniseerd: handmatige stappen voor probleemoplossing](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="decbe-111">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="decbe-112">Er is geen wachtwoorden worden gesynchroniseerd: oplossen met behulp van de diagnostische cmdlet</span><span class="sxs-lookup"><span data-stu-id="decbe-112">No passwords are synchronized: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="decbe-113">U kunt de `Invoke-ADSyncDiagnostics` cmdlet om te achterhalen waarom geen wachtwoorden worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="decbe-113">You can use the `Invoke-ADSyncDiagnostics` cmdlet to figure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="decbe-114">De `Invoke-ADSyncDiagnostics` cmdlet is alleen beschikbaar voor Azure AD Connect versie 1.1.524.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="decbe-114">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="decbe-115">Voer de cmdlet diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="decbe-115">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="decbe-116">Oplossen van problemen waarbij geen wachtwoorden worden gesynchroniseerd met:</span><span class="sxs-lookup"><span data-stu-id="decbe-116">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="decbe-117">Open een nieuw Windows PowerShell-sessie op uw Azure AD Connect-server met de **als Administrator uitvoeren** optie.</span><span class="sxs-lookup"><span data-stu-id="decbe-117">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="decbe-118">Voer `Set-ExecutionPolicy RemoteSigned` of `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="decbe-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="decbe-119">Voer `Import-Module ADSyncDiagnostics` uit.</span><span class="sxs-lookup"><span data-stu-id="decbe-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="decbe-120">Voer `Invoke-ADSyncDiagnostics -PasswordSync` uit.</span><span class="sxs-lookup"><span data-stu-id="decbe-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="decbe-121">Inzicht in de resultaten van de cmdlet</span><span class="sxs-lookup"><span data-stu-id="decbe-121">Understand the results of the cmdlet</span></span>
<span data-ttu-id="decbe-122">De diagnostische cmdlet voert de volgende controles:</span><span class="sxs-lookup"><span data-stu-id="decbe-122">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="decbe-123">Hiermee valideert u of de functie wachtwoord synchronisatie is ingeschakeld voor uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="decbe-123">Validates that the password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="decbe-124">Valideert de Azure AD Connect-server is niet in de faseringsmodus.</span><span class="sxs-lookup"><span data-stu-id="decbe-124">Validates that the Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="decbe-125">Voor elk bestaand on-premises Active Directory-connector (die overeenkomt met een bestaand Active Directory-forest):</span><span class="sxs-lookup"><span data-stu-id="decbe-125">For each existing on-premises Active Directory connector (which corresponds to an existing Active Directory forest):</span></span>

   * <span data-ttu-id="decbe-126">Hiermee valideert u of de functie wachtwoord synchronisatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="decbe-126">Validates that the password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="decbe-127">Hiermee zoekt u naar wachtwoord synchronisatie heartbeat gebeurtenissen in de gebeurtenislogboeken van Windows-toepassing.</span><span class="sxs-lookup"><span data-stu-id="decbe-127">Searches for password synchronization heartbeat events in the Windows Application Event logs.</span></span>

   * <span data-ttu-id="decbe-128">Voor elk Active Directory-domein onder de lokale Active Directory-connector:</span><span class="sxs-lookup"><span data-stu-id="decbe-128">For each Active Directory domain under the on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="decbe-129">Wordt gecontroleerd of het domein bereikbaar is vanaf de Azure AD Connect-server.</span><span class="sxs-lookup"><span data-stu-id="decbe-129">Validates that the domain is reachable from the Azure AD Connect server.</span></span>

      * <span data-ttu-id="decbe-130">Hiermee valideert u of de Active Directory Domain Services (AD DS)-accounts die worden gebruikt door de lokale Active Directory-connector heeft de juiste gebruikersnaam, wachtwoord en machtigingen die vereist zijn voor Wachtwoordsynchronisatie.</span><span class="sxs-lookup"><span data-stu-id="decbe-130">Validates that the Active Directory Domain Services (AD DS) accounts used by the on-premises Active Directory connector has the correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="decbe-131">Het volgende diagram illustreert de resultaten van de cmdlet voor een lokale Active Directory-topologie van één domein:</span><span class="sxs-lookup"><span data-stu-id="decbe-131">The following diagram illustrates the results of the cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Diagnostische uitvoer voor Wachtwoordsynchronisatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="decbe-133">De rest van deze sectie beschrijft specifieke resultaten die zijn geretourneerd door de cmdlet en de bijbehorende problemen.</span><span class="sxs-lookup"><span data-stu-id="decbe-133">The rest of this section describes specific results that are returned by the cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="decbe-134">De synchronisatiefunctie wachtwoord is niet ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="decbe-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="decbe-135">Als u dit nog niet hebt Wachtwoordsynchronisatie met behulp van de Azure AD Connect-wizard ingeschakeld, wordt de volgende fout geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="decbe-135">If you haven't enabled password synchronization by using the Azure AD Connect wizard, the following error is returned:</span></span>

![Wachtwoordsynchronisatie is niet ingeschakeld](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="decbe-137">Azure AD Connect-server is in de faseringsmodus</span><span class="sxs-lookup"><span data-stu-id="decbe-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="decbe-138">Als de Azure AD Connect-server zich in de faseringsmodus, Wachtwoordsynchronisatie is tijdelijk uitgeschakeld en de volgende fout is geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="decbe-138">If the Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and the following error is returned:</span></span>

![Azure AD Connect-server is in de faseringsmodus](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="decbe-140">Er zijn geen wachtwoord synchronisatie heartbeat-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="decbe-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="decbe-141">Elke lokale Active Directory-connector heeft een eigen synchronisatiekanaal wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="decbe-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="decbe-142">Wanneer het wachtwoord synchronisatiekanaal tot stand is gebracht en er zijn geen wachtwoordwijzigingen kunnen worden gesynchroniseerd, wordt elke 30 minuten onder het gebeurtenislogboek van Windows-toepassing in een heartbeat-gebeurtenis (EventId 654) gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="decbe-142">When the password synchronization channel is established and there aren't any password changes to be synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under the Windows Application Event Log.</span></span> <span data-ttu-id="decbe-143">Voor elke lokale Active Directory-connector zoekt u de cmdlet heartbeat er overeenkomende gebeurtenissen in de afgelopen drie uur.</span><span class="sxs-lookup"><span data-stu-id="decbe-143">For each on-premises Active Directory connector, the cmdlet searches for corresponding heartbeat events in the past three hours.</span></span> <span data-ttu-id="decbe-144">Als er geen heartbeat-gebeurtenis wordt gevonden, wordt de volgende fout geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="decbe-144">If no heartbeat event is found, the following error is returned:</span></span>

![Er is geen wachtwoord synchronisatie hartslag gebeurtenis](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="decbe-146">AD DS-account heeft geen juiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="decbe-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="decbe-147">Als de AD DS-account dat wordt gebruikt door de lokale Active Directory-connector synchroniseren wachtwoord-hashes geen de juiste machtigingen heeft, wordt de volgende fout geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="decbe-147">If the AD DS account that's used by the on-premises Active Directory connector to synchronize password hashes does not have the appropriate permissions, the following error is returned:</span></span>

![Onjuiste referenties](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="decbe-149">Onjuiste gebruikersnaam van de AD DS-account of wachtwoord</span><span class="sxs-lookup"><span data-stu-id="decbe-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="decbe-150">Als de AD DS-account gebruikt door de lokale Active Directory-connector voor het synchroniseren van de wachtwoord-hashes een onjuiste gebruikersnaam of wachtwoord heeft, wordt de volgende fout geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="decbe-150">If the AD DS account used by the on-premises Active Directory connector to synchronize password hashes has an incorrect username or password, the following error is returned:</span></span>

![Onjuiste referenties](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="decbe-152">Wachtwoorden niet kan één object worden gesynchroniseerd: oplossen met behulp van de diagnostische cmdlet</span><span class="sxs-lookup"><span data-stu-id="decbe-152">One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="decbe-153">U kunt de `Invoke-ADSyncDiagnostics` cmdlet om te bepalen waarom één object wachtwoorden niet wordt gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="decbe-153">You can use the `Invoke-ADSyncDiagnostics` cmdlet to determine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="decbe-154">De `Invoke-ADSyncDiagnostics` cmdlet is alleen beschikbaar voor Azure AD Connect versie 1.1.524.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="decbe-154">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="decbe-155">Voer de cmdlet diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="decbe-155">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="decbe-156">Oplossen van problemen waarbij geen wachtwoorden worden gesynchroniseerd met:</span><span class="sxs-lookup"><span data-stu-id="decbe-156">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="decbe-157">Open een nieuw Windows PowerShell-sessie op uw Azure AD Connect-server met de **als Administrator uitvoeren** optie.</span><span class="sxs-lookup"><span data-stu-id="decbe-157">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="decbe-158">Voer `Set-ExecutionPolicy RemoteSigned` of `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="decbe-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="decbe-159">Voer `Import-Module ADSyncDiagnostics` uit.</span><span class="sxs-lookup"><span data-stu-id="decbe-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="decbe-160">Voer de volgende cmdlet uit:</span><span class="sxs-lookup"><span data-stu-id="decbe-160">Run the following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="decbe-161">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="decbe-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="decbe-162">Inzicht in de resultaten van de cmdlet</span><span class="sxs-lookup"><span data-stu-id="decbe-162">Understand the results of the cmdlet</span></span>
<span data-ttu-id="decbe-163">De diagnostische cmdlet voert de volgende controles:</span><span class="sxs-lookup"><span data-stu-id="decbe-163">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="decbe-164">Controleert de status van het Active Directory-object in de Active Directory-connectorruimte, Metaverse en Azure AD-connectorruimte.</span><span class="sxs-lookup"><span data-stu-id="decbe-164">Examines the state of the Active Directory object in the Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="decbe-165">Controleert of er synchronisatieregels Wachtwoordsynchronisatie is ingeschakeld en toegepast op de Active Directory-object.</span><span class="sxs-lookup"><span data-stu-id="decbe-165">Validates that there are synchronization rules with password synchronization enabled and applied to the Active Directory object.</span></span>

* <span data-ttu-id="decbe-166">Probeert op te halen en de resultaten van de laatste poging tot het synchroniseren van het wachtwoord voor het object weer te geven.</span><span class="sxs-lookup"><span data-stu-id="decbe-166">Attempts to retrieve and display the results of the last attempt to synchronize the password for the object.</span></span>

<span data-ttu-id="decbe-167">Het volgende diagram illustreert de resultaten van de cmdlet bij het oplossen van Wachtwoordsynchronisatie voor één object:</span><span class="sxs-lookup"><span data-stu-id="decbe-167">The following diagram illustrates the results of the cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Diagnostische uitvoer voor Wachtwoordsynchronisatie - enkel object](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="decbe-169">De rest van deze sectie beschrijft specifieke resultaten geretourneerd door de cmdlet en de bijbehorende problemen.</span><span class="sxs-lookup"><span data-stu-id="decbe-169">The rest of this section describes specific results returned by the cmdlet and corresponding issues.</span></span>

#### <a name="the-active-directory-object-isnt-exported-to-azure-ad"></a><span data-ttu-id="decbe-170">Het Active Directory-object is niet geëxporteerd naar Azure AD</span><span class="sxs-lookup"><span data-stu-id="decbe-170">The Active Directory object isn't exported to Azure AD</span></span>
<span data-ttu-id="decbe-171">Wachtwoordsynchronisatie voor deze lokale Active Directory-account is mislukt omdat er geen bijbehorende object in de Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="decbe-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in the Azure AD tenant.</span></span> <span data-ttu-id="decbe-172">De volgende fout is geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="decbe-172">The following error is returned:</span></span>

![Azure AD-object ontbreekt.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="decbe-174">Gebruiker heeft een tijdelijk wachtwoord</span><span class="sxs-lookup"><span data-stu-id="decbe-174">User has a temporary password</span></span>
<span data-ttu-id="decbe-175">Azure AD Connect ondersteunt momenteel geen tijdelijke wachtwoorden synchroniseren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="decbe-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="decbe-176">Een wachtwoord wordt beschouwd als tijdelijke als de **wachtwoord bij volgende aanmelding wijzigen** optie is ingesteld op de on-premises Active Directory-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="decbe-176">A password is considered to be temporary if the **Change password at next logon** option is set on the on-premises Active Directory user.</span></span> <span data-ttu-id="decbe-177">De volgende fout is geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="decbe-177">The following error is returned:</span></span>

![Tijdelijke wachtwoord wordt niet geëxporteerd.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-to-synchronize-password-arent-available"></a><span data-ttu-id="decbe-179">Resultaten van de laatste poging om te synchroniseren van wachtwoord niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="decbe-179">Results of last attempt to synchronize password aren't available</span></span>
<span data-ttu-id="decbe-180">Azure AD Connect, slaat de resultaten van synchronisatiepogingen van wachtwoord voor de zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="decbe-180">By default, Azure AD Connect stores the results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="decbe-181">Als er geen resultaten beschikbaar voor het geselecteerde object in de Active Directory zijn, wordt de volgende waarschuwing geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="decbe-181">If there are no results available for the selected Active Directory object, the following warning is returned:</span></span>

![Diagnostische uitvoer voor één object - geen wachtwoordgeschiedenis voor synchronisatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="decbe-183">Er is geen wachtwoorden worden gesynchroniseerd: handmatige stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="decbe-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="decbe-184">Volg deze stappen om te bepalen waarom er geen wachtwoorden worden gesynchroniseerd:</span><span class="sxs-lookup"><span data-stu-id="decbe-184">Follow these steps to determine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="decbe-185">De server verbinden in [faseringsmodus](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="decbe-185">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="decbe-186">Een server in de faseringsmodus wachtwoorden niet wordt gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="decbe-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="decbe-187">Het script uitvoeren in de [ophalen van de status van synchronisatie-instellingen voor wachtwoord](#get-the-status-of-password-sync-settings) sectie.</span><span class="sxs-lookup"><span data-stu-id="decbe-187">Run the script in the [Get the status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="decbe-188">Dit biedt u een overzicht van de configuratie van de wachtwoord-synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="decbe-188">It gives you an overview of the password sync configuration.</span></span>  

    ![PowerShell-scriptuitvoer van de synchronisatie-instellingen voor wachtwoord](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="decbe-190">Als de functie is niet ingeschakeld in Azure AD of als de synchronisatiestatus van het kanaal niet is ingeschakeld, moet u de wizard voor Connect-installatie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="decbe-190">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, run the Connect installation wizard.</span></span> <span data-ttu-id="decbe-191">Selecteer **aanpassen Synchronisatieopties**, en Wachtwoordsynchronisatie te deselecteren. Deze wijziging wordt de functie tijdelijk uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="decbe-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables the feature.</span></span> <span data-ttu-id="decbe-192">Vervolgens voert u de wizard opnieuw en Wachtwoordsynchronisatie opnieuw in te schakelen. Voer het script opnieuw uit om te controleren of de configuratie juist is.</span><span class="sxs-lookup"><span data-stu-id="decbe-192">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span></span>

4. <span data-ttu-id="decbe-193">Kijk in het gebeurtenislogboek voor fouten.</span><span class="sxs-lookup"><span data-stu-id="decbe-193">Look in the event log for errors.</span></span> <span data-ttu-id="decbe-194">Zoek naar de volgende reeks gebeurtenissen die op een probleem opgetreden wijzen:</span><span class="sxs-lookup"><span data-stu-id="decbe-194">Look for the following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="decbe-195">Bron: 'Adreslijstsynchronisatie' ID: 0, 611, 652, 655 als u deze gebeurtenissen, ziet u hebt een verbindingsprobleem.</span><span class="sxs-lookup"><span data-stu-id="decbe-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="decbe-196">Het bericht van gebeurtenislogboek beschreven forest waar u problemen ondervindt.</span><span class="sxs-lookup"><span data-stu-id="decbe-196">The event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="decbe-197">Zie voor meer informatie [verbindingsprobleem](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="decbe-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="decbe-198">Als er geen heartbeat of niets anders gewerkt, uitvoeren [activeren van een volledige synchronisatie van wachtwoorden voor alle](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="decbe-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="decbe-199">Voer het script slechts één keer.</span><span class="sxs-lookup"><span data-stu-id="decbe-199">Run the script only once.</span></span>

6. <span data-ttu-id="decbe-200">Zie de [oplossen van één object dat wachtwoorden niet synchroniseert](#one-object-is-not-synchronizing-passwords) sectie.</span><span class="sxs-lookup"><span data-stu-id="decbe-200">See the [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="decbe-201">Verbindingsproblemen</span><span class="sxs-lookup"><span data-stu-id="decbe-201">Connectivity problems</span></span>

<span data-ttu-id="decbe-202">Hebt u verbinding met Azure AD?</span><span class="sxs-lookup"><span data-stu-id="decbe-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="decbe-203">Heeft het account vereist machtigingen om te lezen van de wachtwoord-hashes in alle domeinen?</span><span class="sxs-lookup"><span data-stu-id="decbe-203">Does the account have required permissions to read the password hashes in all domains?</span></span> <span data-ttu-id="decbe-204">Als u verbinding maken met behulp van snelle instellingen hebt geïnstalleerd, kunnen de machtigingen moeten al zijn juist.</span><span class="sxs-lookup"><span data-stu-id="decbe-204">If you installed Connect by using Express settings, the permissions should already be correct.</span></span> 

<span data-ttu-id="decbe-205">Als u aangepaste installatie gebruikt, de machtigingen handmatig instellen door de volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="decbe-205">If you used custom installation, set the permissions manually by doing the following:</span></span>
    
1. <span data-ttu-id="decbe-206">Ga voor het account dat wordt gebruikt door de Active Directory-connector start **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="decbe-206">To find the account used by the Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="decbe-207">Ga naar **Connectors**, en zoek vervolgens naar de lokale Active Directory-forest die u wilt oplossen.</span><span class="sxs-lookup"><span data-stu-id="decbe-207">Go to **Connectors**, and then search for the on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="decbe-208">Selecteer de connector en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="decbe-208">Select the connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="decbe-209">Ga naar **verbinding maken met Active Directory-Forest**.</span><span class="sxs-lookup"><span data-stu-id="decbe-209">Go to **Connect to Active Directory Forest**.</span></span>  
    
    ![Account dat wordt gebruikt door Active Directory-connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="decbe-211">Noteer de gebruikersnaam en het domein waar het account zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="decbe-211">Note the username and the domain where the account is located.</span></span>
    
5. <span data-ttu-id="decbe-212">Start **Active Directory: gebruikers en Computers**, en controleer vervolgens of het account dat u eerder hebt gevonden heeft de volgende machtigingen zijn ingesteld in de hoofdmap van alle domeinen in uw forest:</span><span class="sxs-lookup"><span data-stu-id="decbe-212">Start **Active Directory Users and Computers**, and then verify that the account you found earlier has the follow permissions set at the root of all domains in your forest:</span></span>
    * <span data-ttu-id="decbe-213">Directorywijzigingen repliceren</span><span class="sxs-lookup"><span data-stu-id="decbe-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="decbe-214">Alle repliceren Directory gewijzigd</span><span class="sxs-lookup"><span data-stu-id="decbe-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="decbe-215">De domeincontrollers bereikbaar zijn voor Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="decbe-215">Are the domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="decbe-216">Als de Connect-server kan geen verbinding met alle domeincontrollers, configureert u **voorkeur domeincontroller alleen gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="decbe-216">If the Connect server cannot connect to all domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![-Domeincontroller die wordt gebruikt door Active Directory-connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="decbe-218">Ga terug naar **Synchronization Service Manager** en **mappartitie configureren**.</span><span class="sxs-lookup"><span data-stu-id="decbe-218">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="decbe-219">Selecteer uw domein in **mappartities selecteren**, selecteer de **alleen gebruiken voorkeur domeincontrollers** selectievakje en klik vervolgens op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="decbe-219">Select your domain in **Select directory partitions**, select the **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="decbe-220">Voer de domeincontrollers die verbinding maken voor Wachtwoordsynchronisatie moet worden gebruikt in de lijst. Dezelfde lijst wordt gebruikt voor importeren en exporteren ook.</span><span class="sxs-lookup"><span data-stu-id="decbe-220">In the list, enter the domain controllers that Connect should use for password sync. The same list is used for import and export as well.</span></span> <span data-ttu-id="decbe-221">Voer deze stappen uit voor alle domeinen.</span><span class="sxs-lookup"><span data-stu-id="decbe-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="decbe-222">Als het script wordt aangegeven dat er geen heartbeat, voert u het script in [activeren van een volledige synchronisatie van wachtwoorden voor alle](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="decbe-222">If the script shows that there is no heartbeat, run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="decbe-223">Wachtwoorden niet kan één object worden gesynchroniseerd: handmatige stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="decbe-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="decbe-224">U kunt eenvoudig wachtwoord synchronisatieproblemen oplossen aan de hand van de status van een object.</span><span class="sxs-lookup"><span data-stu-id="decbe-224">You can easily troubleshoot password synchronization issues by reviewing the status of an object.</span></span>

1. <span data-ttu-id="decbe-225">In **Active Directory: gebruikers en Computers**, zoeken naar de gebruiker en controleer vervolgens of de **gebruiker moet wachtwoord bij volgende aanmelding wijzigen** selectievakje is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="decbe-225">In **Active Directory Users and Computers**, search for the user, and then verify that the **User must change password at next logon** check box is cleared.</span></span>  

    ![Active Directory-productief wachtwoorden](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="decbe-227">Als het selectievakje is ingeschakeld, vraagt de gebruiker aanmelden en het wachtwoord te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="decbe-227">If the check box is selected, ask the user to sign in and change the password.</span></span> <span data-ttu-id="decbe-228">Tijdelijke wachtwoorden zijn niet gesynchroniseerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="decbe-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="decbe-229">Als het wachtwoord in Active Directory juist zoekt, volgt u de gebruiker in de synchronisatie-engine.</span><span class="sxs-lookup"><span data-stu-id="decbe-229">If the password looks correct in Active Directory, follow the user in the sync engine.</span></span> <span data-ttu-id="decbe-230">Door de gebruiker van de lokale Active Directory naar Azure AD te volgen, kunt u zien of er een beschrijvend foutbericht op het object is.</span><span class="sxs-lookup"><span data-stu-id="decbe-230">By following the user from on-premises Active Directory to Azure AD, you can see whether there is a descriptive error on the object.</span></span>

    <span data-ttu-id="decbe-231">a.</span><span class="sxs-lookup"><span data-stu-id="decbe-231">a.</span></span> <span data-ttu-id="decbe-232">Start de [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="decbe-232">Start the [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="decbe-233">b.</span><span class="sxs-lookup"><span data-stu-id="decbe-233">b.</span></span> <span data-ttu-id="decbe-234">Klik op **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="decbe-234">Click **Connectors**.</span></span>

    <span data-ttu-id="decbe-235">c.</span><span class="sxs-lookup"><span data-stu-id="decbe-235">c.</span></span> <span data-ttu-id="decbe-236">Selecteer de **Active Directory-Connector** waarin de gebruiker zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="decbe-236">Select the **Active Directory Connector** where the user is located.</span></span>

    <span data-ttu-id="decbe-237">d.</span><span class="sxs-lookup"><span data-stu-id="decbe-237">d.</span></span> <span data-ttu-id="decbe-238">Selecteer **Connectorgebied zoeken**.</span><span class="sxs-lookup"><span data-stu-id="decbe-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="decbe-239">e.</span><span class="sxs-lookup"><span data-stu-id="decbe-239">e.</span></span> <span data-ttu-id="decbe-240">In de **bereik** de optie **DN-naam of het anker**, en voer de volledige DN-naam van de gebruiker die u wilt oplossen.</span><span class="sxs-lookup"><span data-stu-id="decbe-240">In the **Scope** box, select **DN or Anchor**, and then enter the full DN of the user you are troubleshooting.</span></span>

    ![Zoeken naar de gebruiker in de connectorruimte met de DN-naam](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="decbe-242">f.</span><span class="sxs-lookup"><span data-stu-id="decbe-242">f.</span></span> <span data-ttu-id="decbe-243">Zoek de gebruiker die u zoekt, en klik vervolgens op **eigenschappen** voor een overzicht van alle kenmerken.</span><span class="sxs-lookup"><span data-stu-id="decbe-243">Locate the user you are looking for, and then click **Properties** to see all the attributes.</span></span> <span data-ttu-id="decbe-244">Als de gebruiker zich niet in de zoekresultaten, controleert u of uw [filterregels](active-directory-aadconnectsync-configure-filtering.md) en zorg ervoor dat u uitvoert [toepassen en controleer of de wijzigingen](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) voor de gebruiker worden weergegeven in het Connect.</span><span class="sxs-lookup"><span data-stu-id="decbe-244">If the user is not in the search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span></span>

    <span data-ttu-id="decbe-245">g.</span><span class="sxs-lookup"><span data-stu-id="decbe-245">g.</span></span> <span data-ttu-id="decbe-246">Het wachtwoord synchronisatie van het object voor de afgelopen week, klik op details **logboek**.</span><span class="sxs-lookup"><span data-stu-id="decbe-246">To see the password sync details of the object for the past week, click **Log**.</span></span>  

    ![Object-logboekgegevens](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="decbe-248">Of het object logboek leeg is, is Azure AD Connect kan niet lezen van de wachtwoord-hash uit Active Directory.</span><span class="sxs-lookup"><span data-stu-id="decbe-248">If the object log is empty, Azure AD Connect has been unable to read the password hash from Active Directory.</span></span> <span data-ttu-id="decbe-249">Gaat u uw verder met [Connectiviteitsfouten](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="decbe-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="decbe-250">Als er een andere waarde dan **geslaagd**, Zie de tabel in [wachtwoord sync logboek](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="decbe-250">If you see any other value than **success**, refer to the table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="decbe-251">h.</span><span class="sxs-lookup"><span data-stu-id="decbe-251">h.</span></span> <span data-ttu-id="decbe-252">Selecteer de **afkomst** tabblad en zorg ervoor dat ten minste één synchronisatieregel in de **PasswordSync** kolom is **True**.</span><span class="sxs-lookup"><span data-stu-id="decbe-252">Select the **lineage** tab, and make sure that at least one sync rule in the **PasswordSync** column is **True**.</span></span> <span data-ttu-id="decbe-253">In de standaardconfiguratie wordt de naam van de synchronisatieregel is **In uit Active Directory - gebruiker AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="decbe-253">In the default configuration, the name of the sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Informatie over een gebruiker Lineage](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="decbe-255">ik.</span><span class="sxs-lookup"><span data-stu-id="decbe-255">i.</span></span> <span data-ttu-id="decbe-256">Klik op **eigenschappen Metaverse-Object** om een lijst met gebruikerskenmerken weer te geven.</span><span class="sxs-lookup"><span data-stu-id="decbe-256">Click **Metaverse Object Properties** to display a list of user attributes.</span></span>  

    ![Metaverse-informatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="decbe-258">Controleer of er geen **cloudFiltered** kenmerk aanwezig.</span><span class="sxs-lookup"><span data-stu-id="decbe-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="decbe-259">Zorg ervoor dat de domeinkenmerken (domainFQDN en domainNetBios) de verwachte waarden.</span><span class="sxs-lookup"><span data-stu-id="decbe-259">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span></span>

    <span data-ttu-id="decbe-260">j.</span><span class="sxs-lookup"><span data-stu-id="decbe-260">j.</span></span> <span data-ttu-id="decbe-261">Klik op de **Connectors** tabblad. Zorg ervoor dat u zowel op de lokale Active Directory en Azure AD connectors ziet.</span><span class="sxs-lookup"><span data-stu-id="decbe-261">Click the **Connectors** tab. Make sure that you see connectors to both on-premises Active Directory and Azure AD.</span></span>

    ![Metaverse-informatie](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="decbe-263">k.</span><span class="sxs-lookup"><span data-stu-id="decbe-263">k.</span></span> <span data-ttu-id="decbe-264">Selecteer de rij die vertegenwoordigt Azure AD, klikt u op **eigenschappen**, en klik vervolgens op de **afkomst** tabblad. De connector space-object moet een uitgaande regel de **PasswordSync** kolom ingesteld op **True**.</span><span class="sxs-lookup"><span data-stu-id="decbe-264">Select the row that represents Azure AD, click **Properties**, and then click the **Lineage** tab. The connector space object should have an outbound rule in the **PasswordSync** column set to **True**.</span></span> <span data-ttu-id="decbe-265">In de standaardconfiguratie wordt de naam van de synchronisatieregel is **buiten het AAD - gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="decbe-265">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span></span>  

    ![Dialoogvenster voor eigenschappen van het Object ruimte connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="decbe-267">Wachtwoord sync-logboek</span><span class="sxs-lookup"><span data-stu-id="decbe-267">Password sync log</span></span>
<span data-ttu-id="decbe-268">De statuskolom kan de volgende waarden hebben:</span><span class="sxs-lookup"><span data-stu-id="decbe-268">The status column can have the following values:</span></span>

| <span data-ttu-id="decbe-269">Status</span><span class="sxs-lookup"><span data-stu-id="decbe-269">Status</span></span> | <span data-ttu-id="decbe-270">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="decbe-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="decbe-271">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="decbe-271">Success</span></span> |<span data-ttu-id="decbe-272">Wachtwoord is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="decbe-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="decbe-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="decbe-273">FilteredByTarget</span></span> |<span data-ttu-id="decbe-274">Wachtwoord is ingesteld op **gebruiker moet wachtwoord bij volgende aanmelding wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="decbe-274">Password is set to **User must change password at next logon**.</span></span> <span data-ttu-id="decbe-275">Wachtwoord is niet gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="decbe-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="decbe-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="decbe-276">NoTargetConnection</span></span> |<span data-ttu-id="decbe-277">Er is geen object in de metaverse of in de ruimte van Azure AD-connector.</span><span class="sxs-lookup"><span data-stu-id="decbe-277">No object in the metaverse or in the Azure AD connector space.</span></span> |
| <span data-ttu-id="decbe-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="decbe-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="decbe-279">Er is geen object gevonden in de ruimte op de lokale Active Directory-connector.</span><span class="sxs-lookup"><span data-stu-id="decbe-279">No object found in the on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="decbe-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="decbe-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="decbe-281">Het object in de ruimte van Azure AD-connector is nog niet geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="decbe-281">The object in the Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="decbe-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="decbe-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="decbe-283">Logboekvermelding is gemaakt voordat de build 1.0.9125.0 en wordt weergegeven in de oude status.</span><span class="sxs-lookup"><span data-stu-id="decbe-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="decbe-284">Fout</span><span class="sxs-lookup"><span data-stu-id="decbe-284">Error</span></span> |<span data-ttu-id="decbe-285">Service heeft een onbekende fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="decbe-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="decbe-286">Onbekend</span><span class="sxs-lookup"><span data-stu-id="decbe-286">Unknown</span></span> |<span data-ttu-id="decbe-287">Er is een fout opgetreden tijdens het verwerken van een batch wachtwoord-hashes.</span><span class="sxs-lookup"><span data-stu-id="decbe-287">An error occurred while trying to process a batch of password hashes.</span></span>  |
| <span data-ttu-id="decbe-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="decbe-288">MissingAttribute</span></span> |<span data-ttu-id="decbe-289">Specifieke kenmerken die vereist zijn door Azure AD Domain Services (bijvoorbeeld, Kerberos-hash) zijn niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="decbe-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="decbe-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="decbe-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="decbe-291">Specifieke kenmerken die vereist zijn door Azure AD Domain Services (bijvoorbeeld, Kerberos-hash) was eerder niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="decbe-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="decbe-292">Een poging de wachtwoord-hash van de gebruiker opnieuw synchroniseren is gedaan.</span><span class="sxs-lookup"><span data-stu-id="decbe-292">An attempt to resynchronize the user's password hash is made.</span></span> |

## <a name="scripts-to-help-troubleshooting"></a><span data-ttu-id="decbe-293">Scripts bij het oplossen</span><span class="sxs-lookup"><span data-stu-id="decbe-293">Scripts to help troubleshooting</span></span>

### <a name="get-the-status-of-password-sync-settings"></a><span data-ttu-id="decbe-294">De status van wachtwoord synchronisatie-instellingen ophalen</span><span class="sxs-lookup"><span data-stu-id="decbe-294">Get the status of password sync settings</span></span>
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
        Write-Warning "More than one Azure AD Connectors found. Please update the script to use the appropriate Connector."
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

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="decbe-295">Activeren van een volledige synchronisatie van alle wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="decbe-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="decbe-296">Dit script wordt slechts één keer uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="decbe-296">Run this script only once.</span></span> <span data-ttu-id="decbe-297">Als u meer dan één keer uitgevoerd wilt, is iets anders het probleem.</span><span class="sxs-lookup"><span data-stu-id="decbe-297">If you need to run it more than once, something else is the problem.</span></span> <span data-ttu-id="decbe-298">U kunt het probleem oplossen door contact op met Microsoft ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="decbe-298">To troubleshoot the problem, contact Microsoft support.</span></span>

<span data-ttu-id="decbe-299">U kunt een volledige synchronisatie van alle wachtwoorden activeren met behulp van het volgende script:</span><span class="sxs-lookup"><span data-stu-id="decbe-299">You can trigger a full sync of all passwords by using the following script:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="decbe-300">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="decbe-300">Next steps</span></span>
* [<span data-ttu-id="decbe-301">Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie implementeren</span><span class="sxs-lookup"><span data-stu-id="decbe-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="decbe-302">Azure AD Connect-synchronisatie: Synchronisatie-opties voor aanpassen</span><span class="sxs-lookup"><span data-stu-id="decbe-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="decbe-303">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="decbe-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
