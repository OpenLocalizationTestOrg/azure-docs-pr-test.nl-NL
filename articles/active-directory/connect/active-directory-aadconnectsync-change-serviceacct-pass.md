---
title: 'Azure AD Connect-synchronisatie: het Azure AD Connect-synchronisatie-serviceaccount wijzigen | Microsoft Docs'
description: Dit document onderwerp beschrijft de versleutelingssleutel en hoe deze Breek deze af nadat het wachtwoord is gewijzigd.
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
ms.openlocfilehash: bf6234d0810f870909957ee1c1e33c225a4922b9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="e0a6d-104">Het wijzigen van het wachtwoord voor de Azure AD Connect sync-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="e0a6d-104">Changing the Azure AD Connect sync service account password</span></span>
<span data-ttu-id="e0a6d-105">Als u het wachtwoord voor de Azure AD Connect sync-serviceaccount wijzigen, zich de Synchronization Service niet kunnen starten correct totdat u hebt de versleutelingssleutel afgebroken en het wachtwoord voor de Azure AD Connect sync-serviceaccount opnieuw geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-105">If you change the  Azure AD Connect sync service account password, the Synchronization Service will not be able start correctly until you have abandoned the encryption key and reinitialized the Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="e0a6d-106">Azure AD Connect als onderdeel van de Synchronisatieservices maakt gebruik van een coderingssleutel voor het opslaan van de wachtwoorden van de AD DS en Azure AD-serviceaccounts.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-106">Azure AD Connect, as part of the Synchronization Services uses an encryption key to store the passwords of the AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="e0a6d-107">Deze accounts worden versleuteld voordat ze worden opgeslagen in de database.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-107">These accounts are encrypted before they are stored in the database.</span></span> 

<span data-ttu-id="e0a6d-108">De versleutelingssleutel die wordt gebruikt, is beveiligd met [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0a6d-108">The encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="e0a6d-109">DPAPI beveiligt de versleuteling sleutel met behulp van de **wachtwoord van de Azure AD Connect sync-serviceaccount**.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-109">DPAPI protects the encryption key using the **password of the Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="e0a6d-110">Als u wilt wijzigen van het wachtwoord van serviceaccount kunt u de procedures in [opgegeven van de versleutelingssleutel van de Azure AD Connect-synchronisatie](#abandoning-the-azure-ad-connect-sync-encryption-key) om dit te bereiken.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-110">If you need to change the service account password you can use the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) to accomplish this.</span></span>  <span data-ttu-id="e0a6d-111">Deze procedures moeten ook worden gebruikt als u moet de versleutelingssleutel voor een bepaalde reden afbreken.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-111">These procedures should also be used if you need to abandon the encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-the-password"></a><span data-ttu-id="e0a6d-112">Problemen die ontstaan bij het wijzigen van het wachtwoord</span><span class="sxs-lookup"><span data-stu-id="e0a6d-112">Issues that arise from changing the password</span></span>
<span data-ttu-id="e0a6d-113">Er zijn twee dingen die worden uitgevoerd moeten wanneer u het wachtwoord van serviceaccount wijzigt.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-113">There are two things that need to be done when you change the service account password.</span></span>

<span data-ttu-id="e0a6d-114">Eerst moet u het wachtwoord onder Windows Service Control Manager wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-114">First, you need to change the password under the Windows Service Control Manager.</span></span>  <span data-ttu-id="e0a6d-115">Totdat dit probleem opgelost is ziet u volgende fouten:</span><span class="sxs-lookup"><span data-stu-id="e0a6d-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="e0a6d-116">Als u de synchronisatie-Service starten in Windows Service Control Manager probeert, ontvangt u de fout '**Windows kan de Microsoft Azure AD Sync-service niet starten op de lokale Computer**'.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-116">If you try to start the Synchronization Service in Windows Service Control Manager, you receive the error "**Windows could not start the Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="e0a6d-117">**Fout 1069: De service is niet gestart vanwege een aanmeldingsfout.** "</span><span class="sxs-lookup"><span data-stu-id="e0a6d-117">**Error 1069: The service did not start due to a logon failure.**"</span></span>
- <span data-ttu-id="e0a6d-118">Onder Windows Logboeken, het logboek voor systeemgebeurtenissen bevat een fout opgetreden bij **gebeurtenis-ID 7038** en het bericht '**de ADSync-service kan niet worden aangemeld bij het huidige ingestelde wachtwoord vanwege de volgende fout is: de gebruikersnaam of wachtwoord is onjuist.**'</span><span class="sxs-lookup"><span data-stu-id="e0a6d-118">Under Windows Event Viewer, the system event log contains an error with **Event ID 7038** and message “**The ADSync service was unable to log on as with the currently configured password due to the following error: The user name or password is incorrect.**"</span></span>

<span data-ttu-id="e0a6d-119">Ten tweede onder bepaalde omstandigheden, kunnen als het wachtwoord wordt bijgewerkt, de synchronisatieservice niet meer ophalen de versleutelingssleutel via DPAPI.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-119">Second, under specific conditions, if the password is updated, the Synchronization Service can no longer retrieve the encryption key via DPAPI.</span></span> <span data-ttu-id="e0a6d-120">Zonder de versleutelingssleutel decoderen de synchronisatieservice niet van de wachtwoorden vereist voor het synchroniseren van on-premises AD en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-120">Without the encryption key, the Synchronization Service cannot decrypt the passwords required to synchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="e0a6d-121">U ziet bijvoorbeeld fouten:</span><span class="sxs-lookup"><span data-stu-id="e0a6d-121">You will see errors such as:</span></span>

- <span data-ttu-id="e0a6d-122">Onder Windows Service Control Manager als u probeert te starten van de synchronisatieservice en de versleutelingssleutel, kan niet worden opgehaald mislukt met fout "** Windows kan de Microsoft Azure AD-synchronisatie niet starten op de lokale Computer.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-122">Under Windows Service Control Manager, if you try to start the Synchronization Service and it cannot retrieve the encryption key, it fails with error “**Windows could not start the Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="e0a6d-123">Bekijk het gebeurtenislogboek van systeem voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-123">For more information, review the System Event log.</span></span> <span data-ttu-id="e0a6d-124">Als dit een niet-Microsoft-service, neem contact op met de leverancier van de service en Raadpleeg servicespecifieke foutcode **-21451857952 ***. "</span><span class="sxs-lookup"><span data-stu-id="e0a6d-124">If this is a non-Microsoft service, contact the service vendor, and refer to service-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="e0a6d-125">Onder Windows Logboeken, het logboek voor toepassingsgebeurtenissen bevat een fout opgetreden bij **gebeurtenis-ID 6028** en foutbericht *'**de versleutelingssleutel van de server kan niet worden geopend.* *'*</span><span class="sxs-lookup"><span data-stu-id="e0a6d-125">Under Windows Event Viewer, the application event log contains an error with **Event ID 6028** and error message *“**The server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="e0a6d-126">Volg de procedures in om ervoor te zorgen dat er geen deze fouten, [opgegeven van de versleutelingssleutel van de Azure AD Connect-synchronisatie](#abandoning-the-azure-ad-connect-sync-encryption-key) wanneer het wachtwoord wijzigt.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-126">To ensure that you do not receive these errors, follow the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing the password.</span></span>
 
## <a name="abandoning-the-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="e0a6d-127">De versleutelingssleutel van de Azure AD Connect-synchronisatie wordt afgebroken</span><span class="sxs-lookup"><span data-stu-id="e0a6d-127">Abandoning the Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="e0a6d-128">De volgende procedures zijn alleen van toepassing op Azure AD Connect build 1.1.443.0 of ouder.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-128">The following procedures only apply to Azure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="e0a6d-129">Gebruik de volgende procedures om de versleutelingssleutel af te breken.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-129">Use the following procedures to abandon the encryption key.</span></span>

### <a name="what-to-do-if-you-need-to-abandon-the-encryption-key"></a><span data-ttu-id="e0a6d-130">Wat te doen als u wilt afbreken van de versleutelingssleutel</span><span class="sxs-lookup"><span data-stu-id="e0a6d-130">What to do if you need to abandon the encryption key</span></span>

<span data-ttu-id="e0a6d-131">Als u afbreken van de versleutelingssleutel wilt, gebruikt u de volgende procedures om dit te bereiken.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-131">If you need to abandon the encryption key, use the following procedures to accomplish this.</span></span>

1. [<span data-ttu-id="e0a6d-132">De bestaande versleutelingssleutel afbreken</span><span class="sxs-lookup"><span data-stu-id="e0a6d-132">Abandon the existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="e0a6d-133">Geef het wachtwoord voor de AD DS-account</span><span class="sxs-lookup"><span data-stu-id="e0a6d-133">Provide the password of the AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="e0a6d-134">Initialiseren van het wachtwoord van het Azure AD sync-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="e0a6d-134">Reinitialize the password of the Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="e0a6d-135">De synchronisatieservice starten</span><span class="sxs-lookup"><span data-stu-id="e0a6d-135">Start the Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-the-existing-encryption-key"></a><span data-ttu-id="e0a6d-136">De bestaande versleutelingssleutel afbreken</span><span class="sxs-lookup"><span data-stu-id="e0a6d-136">Abandon the existing encryption key</span></span>
<span data-ttu-id="e0a6d-137">De bestaande versleutelingssleutel afbreken zodat deze nieuwe versleutelingssleutel kan worden gemaakt:</span><span class="sxs-lookup"><span data-stu-id="e0a6d-137">Abandon the existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="e0a6d-138">Meld u aan bij uw Azure AD Connect-Server als beheerder.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-138">Log in to your Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="e0a6d-139">Start een nieuwe PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="e0a6d-140">Navigeer naar de map:`$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="e0a6d-140">Navigate to folder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="e0a6d-141">Voer de opdracht:`./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="e0a6d-141">Run the command: `./miiskmu.exe /a`</span></span>

![Azure AD Connect Sync Encryption Key-hulpprogramma](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-the-password-of-the-ad-ds-account"></a><span data-ttu-id="e0a6d-143">Geef het wachtwoord voor de AD DS-account</span><span class="sxs-lookup"><span data-stu-id="e0a6d-143">Provide the password of the AD DS account</span></span>
<span data-ttu-id="e0a6d-144">Als de bestaande wachtwoorden worden opgeslagen in de database kunnen niet meer worden ontsleuteld, moet u de Synchronization Service voorzien van het wachtwoord van de AD DS-account.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-144">As the existing passwords stored inside the database can no longer be decrypted, you need to provide the Synchronization Service with the password of the AD DS account.</span></span> <span data-ttu-id="e0a6d-145">De synchronisatieservice versleutelt de met de nieuwe versleutelingssleutel wachtwoorden:</span><span class="sxs-lookup"><span data-stu-id="e0a6d-145">The Synchronization Service encrypts the passwords using the new encryption key:</span></span>

1. <span data-ttu-id="e0a6d-146">Synchronization Service Manager (START → Synchronization-Service) starten.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-146">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="e0a6d-147">![Sync-Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="e0a6d-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="e0a6d-148">Ga naar de **Connectors** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-148">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="e0a6d-149">Selecteer de **AD-Connector** die overeenkomt met uw on-premises AD.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-149">Select the **AD Connector** that corresponds to your on-premises AD.</span></span> <span data-ttu-id="e0a6d-150">Als u meer dan één AD-connector hebt, herhaalt u de volgende stappen uit voor elk van deze.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-150">If you have more than one AD connector, repeat the following steps for each of them.</span></span>
4. <span data-ttu-id="e0a6d-151">Onder **acties**, selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="e0a6d-152">Selecteer in het pop-updialoogvenster **verbinding maken met Active Directory-Forest**:</span><span class="sxs-lookup"><span data-stu-id="e0a6d-152">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>
6. <span data-ttu-id="e0a6d-153">Geef het wachtwoord van de AD DS-account in de **wachtwoord** textbox.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-153">Enter the password of the AD DS account in the **Password** textbox.</span></span> <span data-ttu-id="e0a6d-154">Als u het wachtwoord niet weet, moet u deze instellen op een bekende waarde voordat u deze stap uitvoert.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-154">If you do not know its password, you must set it to a known value before performing this step.</span></span>
7. <span data-ttu-id="e0a6d-155">Klik op **OK** naar het nieuwe wachtwoord opslaan en sluiten van een pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-155">Click **OK** to save the new password and close the pop-up dialog.</span></span>
<span data-ttu-id="e0a6d-156">![Azure AD Connect Sync Encryption Key-hulpprogramma](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="e0a6d-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-the-password-of-the-azure-ad-sync-account"></a><span data-ttu-id="e0a6d-157">Initialiseren van het wachtwoord van het Azure AD sync-serviceaccount</span><span class="sxs-lookup"><span data-stu-id="e0a6d-157">Reinitialize the password of the Azure AD sync account</span></span>
<span data-ttu-id="e0a6d-158">U kan niet rechtstreeks Geef het wachtwoord van de Azure AD-serviceaccount voor de synchronisatieservice.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-158">You cannot directly provide the password of the Azure AD service account to the Synchronization Service.</span></span> <span data-ttu-id="e0a6d-159">In plaats daarvan moet u de cmdlet gebruiken **toevoegen ADSyncAADServiceAccount** opnieuw initialiseren van het Azure AD-serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-159">Instead, you need to use the cmdlet **Add-ADSyncAADServiceAccount** to reinitialize the Azure AD service account.</span></span> <span data-ttu-id="e0a6d-160">De cmdlet het accountwachtwoord opnieuw instellen en is beschikbaar voor de synchronisatieservice:</span><span class="sxs-lookup"><span data-stu-id="e0a6d-160">The cmdlet resets the account password and makes it available to the Synchronization Service:</span></span>

1. <span data-ttu-id="e0a6d-161">Start een nieuwe PowerShell-sessie op de Azure AD Connect-server.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-161">Start a new PowerShell session on the Azure AD Connect server.</span></span>
2. <span data-ttu-id="e0a6d-162">Voer cmdlet `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="e0a6d-163">Geef de globale beheerder Azure AD-referenties voor uw Azure AD-tenant in het pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-163">In the pop-up dialog, provide the Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="e0a6d-164">![Azure AD Connect Sync Encryption Key-hulpprogramma](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="e0a6d-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="e0a6d-165">Als dat lukt, ziet u de PowerShell-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-165">If it is successful, you will see the PowerShell command prompt.</span></span>

#### <a name="start-the-synchronization-service"></a><span data-ttu-id="e0a6d-166">De synchronisatieservice starten</span><span class="sxs-lookup"><span data-stu-id="e0a6d-166">Start the Synchronization Service</span></span>
<span data-ttu-id="e0a6d-167">Nu dat de synchronisatieservice toegang tot de versleutelingssleutel en de wachtwoorden die nodig is heeft, kunt u de service opnieuw in de Windows Service Control Manager:</span><span class="sxs-lookup"><span data-stu-id="e0a6d-167">Now that the Synchronization Service has access to the encryption key and all the passwords it needs, you can restart the service in the Windows Service Control Manager:</span></span>


1. <span data-ttu-id="e0a6d-168">Ga naar Windows Service Control Manager (START → Services).</span><span class="sxs-lookup"><span data-stu-id="e0a6d-168">Go to Windows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="e0a6d-169">Selecteer **Microsoft Azure AD Sync** en klik op opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="e0a6d-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0a6d-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0a6d-170">Next steps</span></span>
<span data-ttu-id="e0a6d-171">**Overzichtsonderwerpen**</span><span class="sxs-lookup"><span data-stu-id="e0a6d-171">**Overview topics**</span></span>

* [<span data-ttu-id="e0a6d-172">Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="e0a6d-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="e0a6d-173">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0a6d-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
