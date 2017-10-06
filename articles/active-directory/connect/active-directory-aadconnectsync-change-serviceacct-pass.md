---
title: 'Azure AD Connect-synchronisatie: hello Azure AD Connect-synchronisatie-serviceaccount wijzigen | Microsoft Docs'
description: Dit document onderwerp beschrijft de versleutelingssleutel Hallo en hoe tooabandon na het Hallo-wachtwoord is gewijzigd.
services: active-directory
keywords: Azure AD sync-serviceaccount, wachtwoord
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="5b96c-104">Wachtwoord wijzigen hello Azure AD Connect sync-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="5b96c-104">Changing hello Azure AD Connect sync service account password</span></span>
<span data-ttu-id="5b96c-105">Als u een wachtwoord hello Azure AD Connect sync-serviceaccount wijzigt, zich Hallo Synchronization Service niet kunnen starten correct totdat u hebt verlaten Hallo versleutelingssleutel en opnieuw geïnitialiseerd wachtwoord hello Azure AD Connect sync-serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="5b96c-105">If you change hello  Azure AD Connect sync service account password, hello Synchronization Service will not be able start correctly until you have abandoned hello encryption key and reinitialized hello Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="5b96c-106">Azure AD Connect als onderdeel van Hallo Synchronisatieservices maakt gebruik van een versleuteling sleutel toostore Hallo wachtwoorden van Hallo AD DS en Azure AD-serviceaccounts.</span><span class="sxs-lookup"><span data-stu-id="5b96c-106">Azure AD Connect, as part of hello Synchronization Services uses an encryption key toostore hello passwords of hello AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="5b96c-107">Deze accounts worden versleuteld voordat ze worden opgeslagen in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="5b96c-107">These accounts are encrypted before they are stored in hello database.</span></span> 

<span data-ttu-id="5b96c-108">Hallo versleutelingssleutel die wordt gebruikt is beveiligd met [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b96c-108">hello encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="5b96c-109">DPAPI beveiligt Hallo-versleutelingssleutel met Hallo **wachtwoord van hello Azure AD Connect sync-serviceaccount**.</span><span class="sxs-lookup"><span data-stu-id="5b96c-109">DPAPI protects hello encryption key using hello **password of hello Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="5b96c-110">Als u het wachtwoord van serviceaccount Hallo toochange nodig kunt u Hallo procedures in [Abandoning hello Azure AD Connect-synchronisatie versleutelingssleutel](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish dit.</span><span class="sxs-lookup"><span data-stu-id="5b96c-110">If you need toochange hello service account password you can use hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish this.</span></span>  <span data-ttu-id="5b96c-111">Deze procedures moeten ook worden gebruikt als u tooabandon Hallo versleutelingssleutel nodig om welke reden.</span><span class="sxs-lookup"><span data-stu-id="5b96c-111">These procedures should also be used if you need tooabandon hello encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-hello-password"></a><span data-ttu-id="5b96c-112">Problemen die voortkomen uit Hallo wachtwoord wijzigen</span><span class="sxs-lookup"><span data-stu-id="5b96c-112">Issues that arise from changing hello password</span></span>
<span data-ttu-id="5b96c-113">Er zijn twee dingen nodig toobe uitgevoerd als u het wachtwoord Hallo-serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="5b96c-113">There are two things that need toobe done when you change hello service account password.</span></span>

<span data-ttu-id="5b96c-114">U moet eerst toochange Hallo wachtwoord onder Hallo Windows Service Control Manager.</span><span class="sxs-lookup"><span data-stu-id="5b96c-114">First, you need toochange hello password under hello Windows Service Control Manager.</span></span>  <span data-ttu-id="5b96c-115">Totdat dit probleem opgelost is ziet u volgende fouten:</span><span class="sxs-lookup"><span data-stu-id="5b96c-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="5b96c-116">Als u toostart Hallo Synchronization Service in Windows Service Control Manager probeert, ontvangt u fout Hallo '**Windows kan Hallo Microsoft Azure AD Sync-service niet starten op de lokale Computer**'.</span><span class="sxs-lookup"><span data-stu-id="5b96c-116">If you try toostart hello Synchronization Service in Windows Service Control Manager, you receive hello error "**Windows could not start hello Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="5b96c-117">**Fout 1069: Hallo-service is niet gestart vanwege tooa aanmelding mislukt.** "</span><span class="sxs-lookup"><span data-stu-id="5b96c-117">**Error 1069: hello service did not start due tooa logon failure.**"</span></span>
- <span data-ttu-id="5b96c-118">Onder de functie Logboeken van Windows hello logboek met systeemgebeurtenissen bevat een fout opgetreden bij **gebeurtenis-ID 7038** en het bericht '**Hallo-service ADSync is kan niet toolog op net als bij Hallo momenteel zodanig geconfigureerd dat wachtwoorden vanwege de volgende toohello fout: Hallo-gebruikersnaam of wachtwoord is onjuist.** "</span><span class="sxs-lookup"><span data-stu-id="5b96c-118">Under Windows Event Viewer, hello system event log contains an error with **Event ID 7038** and message “**hello ADSync service was unable toolog on as with hello currently configured password due toohello following error: hello user name or password is incorrect.**"</span></span>

<span data-ttu-id="5b96c-119">Ten tweede onder bepaalde omstandigheden, kan als Hallo wachtwoord wordt bijgewerkt, Hallo Synchronization Service niet langer ophalen Hallo versleutelingssleutel via DPAPI.</span><span class="sxs-lookup"><span data-stu-id="5b96c-119">Second, under specific conditions, if hello password is updated, hello Synchronization Service can no longer retrieve hello encryption key via DPAPI.</span></span> <span data-ttu-id="5b96c-120">Zonder de versleutelingssleutel hello, Hallo die Synchronization-Service niet Hallo wachtwoorden vereist toosynchronize naar/van ontsleutelen kan on-premises AD en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b96c-120">Without hello encryption key, hello Synchronization Service cannot decrypt hello passwords required toosynchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="5b96c-121">U ziet bijvoorbeeld fouten:</span><span class="sxs-lookup"><span data-stu-id="5b96c-121">You will see errors such as:</span></span>

- <span data-ttu-id="5b96c-122">Onder Windows Service Control Manager als u toostart Hallo-synchronisatieservice probeert en de versleutelingssleutel hello, kan niet worden opgehaald mislukt met fout "** Windows kan Microsoft Azure AD Sync Hallo niet starten op de lokale Computer.</span><span class="sxs-lookup"><span data-stu-id="5b96c-122">Under Windows Service Control Manager, if you try toostart hello Synchronization Service and it cannot retrieve hello encryption key, it fails with error “**Windows could not start hello Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="5b96c-123">Bekijk Hallo System-gebeurtenislogboek voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5b96c-123">For more information, review hello System Event log.</span></span> <span data-ttu-id="5b96c-124">Als dit een niet-Microsoft-service, neem contact op met de leverancier van de Hallo en tooservice-specifieke foutcode Raadpleeg **-21451857952 ***. "</span><span class="sxs-lookup"><span data-stu-id="5b96c-124">If this is a non-Microsoft service, contact hello service vendor, and refer tooservice-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="5b96c-125">Onder de functie Logboeken van Windows hello toepassingslogboek bevat een fout opgetreden bij **gebeurtenis-ID 6028** en foutbericht *'**versleutelingssleutel Hallo-server kan niet worden geopend.* *'*</span><span class="sxs-lookup"><span data-stu-id="5b96c-125">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6028** and error message *“**hello server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="5b96c-126">tooensure dat er geen deze fouten, volgt u de procedures Hallo in [Abandoning hello Azure AD Connect-synchronisatie versleutelingssleutel](#abandoning-the-azure-ad-connect-sync-encryption-key) wanneer Hallo wachtwoord wijzigt.</span><span class="sxs-lookup"><span data-stu-id="5b96c-126">tooensure that you do not receive these errors, follow hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing hello password.</span></span>
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="5b96c-127">Versleutelingssleutel van de Hallo-Azure AD Connect-synchronisatie wordt afgebroken</span><span class="sxs-lookup"><span data-stu-id="5b96c-127">Abandoning hello Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="5b96c-128">Hallo volgende procedures gelden alleen tooAzure AD Connect build 1.1.443.0 of ouder.</span><span class="sxs-lookup"><span data-stu-id="5b96c-128">hello following procedures only apply tooAzure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="5b96c-129">Gebruik hello procedures tooabandon Hallo versleutelingssleutel te volgen.</span><span class="sxs-lookup"><span data-stu-id="5b96c-129">Use hello following procedures tooabandon hello encryption key.</span></span>

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a><span data-ttu-id="5b96c-130">Welke toodo als u tooabandon Hallo versleutelingssleutel nodig</span><span class="sxs-lookup"><span data-stu-id="5b96c-130">What toodo if you need tooabandon hello encryption key</span></span>

<span data-ttu-id="5b96c-131">Als u tooabandon Hallo versleutelingssleutel nodig hebt, gebruik Hallo tooaccomplish procedures te volgen deze.</span><span class="sxs-lookup"><span data-stu-id="5b96c-131">If you need tooabandon hello encryption key, use hello following procedures tooaccomplish this.</span></span>

1. [<span data-ttu-id="5b96c-132">Bestaande versleutelingssleutel Hallo afbreken</span><span class="sxs-lookup"><span data-stu-id="5b96c-132">Abandon hello existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="5b96c-133">Hallo wachtwoord Hallo AD DS-account opgeven</span><span class="sxs-lookup"><span data-stu-id="5b96c-133">Provide hello password of hello AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="5b96c-134">Hallo-wachtwoord van hello Azure AD sync-account opnieuw initialiseren</span><span class="sxs-lookup"><span data-stu-id="5b96c-134">Reinitialize hello password of hello Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="5b96c-135">Hallo Synchronization Service starten</span><span class="sxs-lookup"><span data-stu-id="5b96c-135">Start hello Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a><span data-ttu-id="5b96c-136">Bestaande versleutelingssleutel Hallo afbreken</span><span class="sxs-lookup"><span data-stu-id="5b96c-136">Abandon hello existing encryption key</span></span>
<span data-ttu-id="5b96c-137">Bestaande versleutelingssleutel Hallo afbreken zodat deze nieuwe versleutelingssleutel kan worden gemaakt:</span><span class="sxs-lookup"><span data-stu-id="5b96c-137">Abandon hello existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="5b96c-138">Aanmelden tooyour Azure AD Connect-Server als beheerder.</span><span class="sxs-lookup"><span data-stu-id="5b96c-138">Log in tooyour Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="5b96c-139">Start een nieuwe PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="5b96c-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="5b96c-140">Navigeer toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="5b96c-140">Navigate toofolder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="5b96c-141">Hallo-opdracht uitvoeren:`./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="5b96c-141">Run hello command: `./miiskmu.exe /a`</span></span>

![Azure AD Connect Sync Encryption Key-hulpprogramma](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a><span data-ttu-id="5b96c-143">Hallo wachtwoord Hallo AD DS-account opgeven</span><span class="sxs-lookup"><span data-stu-id="5b96c-143">Provide hello password of hello AD DS account</span></span>
<span data-ttu-id="5b96c-144">Zoals Hallo bestaande wachtwoorden worden opgeslagen in het Hallo-database kunnen niet meer worden ontsleuteld, moet je tooprovide Hallo synchronisatieservice met wachtwoord op Hallo van Hallo AD DS-account.</span><span class="sxs-lookup"><span data-stu-id="5b96c-144">As hello existing passwords stored inside hello database can no longer be decrypted, you need tooprovide hello Synchronization Service with hello password of hello AD DS account.</span></span> <span data-ttu-id="5b96c-145">Hallo-synchronisatieservice versleutelt Hallo wachtwoorden met nieuwe coderingssleutel Hallo:</span><span class="sxs-lookup"><span data-stu-id="5b96c-145">hello Synchronization Service encrypts hello passwords using hello new encryption key:</span></span>

1. <span data-ttu-id="5b96c-146">Hallo Synchronization Service Manager (START → Synchronization Service) starten.</span><span class="sxs-lookup"><span data-stu-id="5b96c-146">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="5b96c-147">![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="5b96c-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="5b96c-148">Ga toohello **Connectors** tabblad.</span><span class="sxs-lookup"><span data-stu-id="5b96c-148">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="5b96c-149">Selecteer Hallo **AD-Connector** die overeenkomt met tooyour on-premises AD dat.</span><span class="sxs-lookup"><span data-stu-id="5b96c-149">Select hello **AD Connector** that corresponds tooyour on-premises AD.</span></span> <span data-ttu-id="5b96c-150">Als u meer dan één AD-connector hebt, herhaalt u Hallo volgende stappen uit voor elk van deze.</span><span class="sxs-lookup"><span data-stu-id="5b96c-150">If you have more than one AD connector, repeat hello following steps for each of them.</span></span>
4. <span data-ttu-id="5b96c-151">Onder **acties**, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="5b96c-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="5b96c-152">Selecteer in het pop-upvenster hello, **tooActive Directory-Forest verbinding**:</span><span class="sxs-lookup"><span data-stu-id="5b96c-152">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>
6. <span data-ttu-id="5b96c-153">Voer wachtwoord op Hallo van Hallo AD DS-account in Hallo **wachtwoord** textbox.</span><span class="sxs-lookup"><span data-stu-id="5b96c-153">Enter hello password of hello AD DS account in hello **Password** textbox.</span></span> <span data-ttu-id="5b96c-154">Als u het wachtwoord niet weet, moet u dit tooa bekende waarde voordat u deze stap uitvoert instellen.</span><span class="sxs-lookup"><span data-stu-id="5b96c-154">If you do not know its password, you must set it tooa known value before performing this step.</span></span>
7. <span data-ttu-id="5b96c-155">Klik op **OK** toosave Hallo nieuw wachtwoord en sluiten Hallo pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="5b96c-155">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>
<span data-ttu-id="5b96c-156">![Azure AD Connect Sync Encryption Key-hulpprogramma](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="5b96c-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a><span data-ttu-id="5b96c-157">Hallo-wachtwoord van hello Azure AD sync-account opnieuw initialiseren</span><span class="sxs-lookup"><span data-stu-id="5b96c-157">Reinitialize hello password of hello Azure AD sync account</span></span>
<span data-ttu-id="5b96c-158">U kan niet rechtstreeks wachtwoord op Hallo van hello Azure AD-service-account toohello Synchronization Service opgeven.</span><span class="sxs-lookup"><span data-stu-id="5b96c-158">You cannot directly provide hello password of hello Azure AD service account toohello Synchronization Service.</span></span> <span data-ttu-id="5b96c-159">In plaats daarvan moet u toouse Hallo cmdlet **toevoegen ADSyncAADServiceAccount** tooreinitialize hello Azure AD-serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="5b96c-159">Instead, you need toouse hello cmdlet **Add-ADSyncAADServiceAccount** tooreinitialize hello Azure AD service account.</span></span> <span data-ttu-id="5b96c-160">Hallo cmdlet Hallo accountwachtwoord opnieuw instellen en maakt het beschikbaar toohello Synchronization Service:</span><span class="sxs-lookup"><span data-stu-id="5b96c-160">hello cmdlet resets hello account password and makes it available toohello Synchronization Service:</span></span>

1. <span data-ttu-id="5b96c-161">Start een nieuwe PowerShell-sessie op Hallo Azure AD Connect-server.</span><span class="sxs-lookup"><span data-stu-id="5b96c-161">Start a new PowerShell session on hello Azure AD Connect server.</span></span>
2. <span data-ttu-id="5b96c-162">Voer cmdlet `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="5b96c-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="5b96c-163">In het pop-upvenster hello, referenties hello Azure AD globale beheerder voor uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="5b96c-163">In hello pop-up dialog, provide hello Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="5b96c-164">![Azure AD Connect Sync Encryption Key-hulpprogramma](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="5b96c-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="5b96c-165">Als dat lukt, ziet u Hallo PowerShell-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="5b96c-165">If it is successful, you will see hello PowerShell command prompt.</span></span>

#### <a name="start-hello-synchronization-service"></a><span data-ttu-id="5b96c-166">Hallo Synchronization Service starten</span><span class="sxs-lookup"><span data-stu-id="5b96c-166">Start hello Synchronization Service</span></span>
<span data-ttu-id="5b96c-167">Nu Hallo Synchronization Service heeft toegang toohello versleutelingssleutel en alle Hallo wachtwoorden nodig is, kunt u Hallo-service opnieuw starten in Hallo Windows Service Control Manager:</span><span class="sxs-lookup"><span data-stu-id="5b96c-167">Now that hello Synchronization Service has access toohello encryption key and all hello passwords it needs, you can restart hello service in hello Windows Service Control Manager:</span></span>


1. <span data-ttu-id="5b96c-168">Ga tooWindows Service Control Manager (START → Services).</span><span class="sxs-lookup"><span data-stu-id="5b96c-168">Go tooWindows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="5b96c-169">Selecteer **Microsoft Azure AD Sync** en klik op opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="5b96c-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b96c-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5b96c-170">Next steps</span></span>
<span data-ttu-id="5b96c-171">**Overzichtsonderwerpen**</span><span class="sxs-lookup"><span data-stu-id="5b96c-171">**Overview topics**</span></span>

* [<span data-ttu-id="5b96c-172">Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="5b96c-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="5b96c-173">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b96c-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
