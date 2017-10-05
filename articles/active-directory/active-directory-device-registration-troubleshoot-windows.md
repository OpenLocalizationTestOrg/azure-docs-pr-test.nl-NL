---
title: Het oplossen van de automatische registratie van Azure AD-domein aangesloten computers voor Windows 10 en Windows Server 2016 | Microsoft Docs
description: Het oplossen van de automatische registratie van Azure AD-domein lid zijn van computers voor Windows 10 en Windows Server 2016.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="c4d10-103">Het oplossen van automatische registratie van domein computers toegevoegd aan Azure AD. – Windows 10 en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c4d10-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="c4d10-104">In dit onderwerp is van toepassing op de volgende clients:</span><span class="sxs-lookup"><span data-stu-id="c4d10-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="c4d10-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="c4d10-105">Windows 10</span></span>
-   <span data-ttu-id="c4d10-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c4d10-106">Windows Server 2016</span></span>

<span data-ttu-id="c4d10-107">Zie voor andere Windows-clients [probleemoplossing automatische registratie van domein aangesloten computers naar Azure AD voor Windows downlevel-clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="c4d10-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="c4d10-108">Dit onderwerp wordt ervan uitgegaan dat u hebt geconfigureerd automatische registratie van apparaten domein vermelde in dat wordt beschreven in [automatische registratie van Windows-domein-apparaten met Azure Active Directory configureren](active-directory-device-registration-get-started.md) ter ondersteuning van de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="c4d10-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span></span>

- [<span data-ttu-id="c4d10-109">Voorwaardelijke toegang op basis van apparaten</span><span class="sxs-lookup"><span data-stu-id="c4d10-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="c4d10-110">Enterprise-instellingen voor roaming</span><span class="sxs-lookup"><span data-stu-id="c4d10-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="c4d10-111">Windows Hello voor Bedrijven</span><span class="sxs-lookup"><span data-stu-id="c4d10-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="c4d10-112">Dit document bevat richtlijnen voor probleemoplossing over de mogelijke problemen kunt oplossen.</span><span class="sxs-lookup"><span data-stu-id="c4d10-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 

<span data-ttu-id="c4d10-113">De registratie wordt ondersteund in de Windows Update 10 November 2015 en hoger.</span><span class="sxs-lookup"><span data-stu-id="c4d10-113">The registration is supported in the Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="c4d10-114">U wordt aangeraden de Update Verjaardag gebruiken voor het inschakelen van de bovenstaande scenario's.</span><span class="sxs-lookup"><span data-stu-id="c4d10-114">We recommend using the Anniversary Update for enabling the scenarios above.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="c4d10-115">Stap 1: De registratiestatus ophalen</span><span class="sxs-lookup"><span data-stu-id="c4d10-115">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="c4d10-116">**De registratiestatus ophalen:**</span><span class="sxs-lookup"><span data-stu-id="c4d10-116">**To retrieve the registration status:**</span></span>

1. <span data-ttu-id="c4d10-117">Open de opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c4d10-117">Open the command prompt as an administrator.</span></span>

2. <span data-ttu-id="c4d10-118">Type **dsregcmd/status**</span><span class="sxs-lookup"><span data-stu-id="c4d10-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="c4d10-119">+----------------------------------------------------------------------+
   | Apparaatstatus |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="c4d10-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="c4d10-120">EnterpriseJoined: Geen apparaat-id: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 vingerafdruk: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto-Provider TpmProtected: Ja KeySignTest:: moet worden uitgevoerd met verhoogde bevoegdheden te testen.</span><span class="sxs-lookup"><span data-stu-id="c4d10-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="c4d10-121">IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: Ja DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="c4d10-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="c4d10-122">+----------------------------------------------------------------------+
   | Gebruikersstatus |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="c4d10-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="c4d10-123">WamDefaultAuthority: organisaties WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd) AzureAdPrt: Ja</span><span class="sxs-lookup"><span data-stu-id="c4d10-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="c4d10-124">Stap 2: De registratiestatus van de</span><span class="sxs-lookup"><span data-stu-id="c4d10-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="c4d10-125">Bekijk de volgende velden en zorg ervoor dat ze de verwachte waarden hebben:</span><span class="sxs-lookup"><span data-stu-id="c4d10-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="c4d10-126">AzureAdJoined: Ja</span><span class="sxs-lookup"><span data-stu-id="c4d10-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="c4d10-127">Dit veld geeft aan of het apparaat is geregistreerd bij Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4d10-127">This field shows whether the device is registered with Azure AD.</span></span> <span data-ttu-id="c4d10-128">Als de waarde wordt weergegeven als 'Nee', worden de registratie is niet voltooid.</span><span class="sxs-lookup"><span data-stu-id="c4d10-128">If the value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="c4d10-129">**Mogelijke oorzaken:**</span><span class="sxs-lookup"><span data-stu-id="c4d10-129">**Possible causes:**</span></span>

- <span data-ttu-id="c4d10-130">Verificatie van de computer voor de registratie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="c4d10-130">Authentication of the computer for registration failed.</span></span>

- <span data-ttu-id="c4d10-131">Er is een HTTP-proxy in de organisatie die door de computer kan niet worden gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="c4d10-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="c4d10-132">De computer kan niet aangemeld bij Azure AD voor de verificatie of Azure DRS voor registratie</span><span class="sxs-lookup"><span data-stu-id="c4d10-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="c4d10-133">De computer mogelijk niet op het interne netwerk van de organisatie of VPN-met direct zicht regel met een on-premises AD-domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="c4d10-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="c4d10-134">Als de computer een TPM heeft, wordt in een verkeerde status.</span><span class="sxs-lookup"><span data-stu-id="c4d10-134">If the computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="c4d10-135">Er is mogelijk een onjuiste configuratie van services eerder hebt genoteerd in het document dat moet u opnieuw te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="c4d10-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="c4d10-136">Algemene voorbeelden zijn:</span><span class="sxs-lookup"><span data-stu-id="c4d10-136">Common examples are:</span></span>

    - <span data-ttu-id="c4d10-137">De federatieserver is geen WS-Trust-eindpunten die zijn ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="c4d10-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="c4d10-138">De federatieserver mogelijk niet toegestaan voor binnenkomende verificatie vanaf computers in uw netwerk met behulp van geïntegreerde Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="c4d10-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="c4d10-139">Er is geen object van het Service Connection Point die verwijst naar de domeinnaam van uw geverifieerde in Azure AD in de AD-forest waar de computer deel uitmaakt</span><span class="sxs-lookup"><span data-stu-id="c4d10-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="c4d10-140">DomainJoined: Ja</span><span class="sxs-lookup"><span data-stu-id="c4d10-140">DomainJoined : YES</span></span>  

<span data-ttu-id="c4d10-141">Dit veld wordt aangegeven of het apparaat is verbonden met een lokale Active Directory of niet.</span><span class="sxs-lookup"><span data-stu-id="c4d10-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="c4d10-142">Als de waarde wordt weergegeven als **Nee**, het apparaat niet automatisch kan registreren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4d10-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="c4d10-143">Controleer eerst het apparaat lid wordt aan de lokale Active Directory, voordat u deze kunt registreren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4d10-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="c4d10-144">Als u de computer lid te worden naar Azure AD rechtstreeks zoekt, gaat u naar meer informatie over de mogelijkheden van Azure Active Directory Join.</span><span class="sxs-lookup"><span data-stu-id="c4d10-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="c4d10-145">WorkplaceJoined: Nee</span><span class="sxs-lookup"><span data-stu-id="c4d10-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="c4d10-146">Dit veld geeft aan of het apparaat is geregistreerd met Azure AD, maar als een persoonlijk apparaat (gemarkeerd als 'Workplace Joined').</span><span class="sxs-lookup"><span data-stu-id="c4d10-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="c4d10-147">Als deze waarde moet worden weergegeven als 'Nee' voor een domeincomputer geregistreerd in Azure AD, maar als deze wordt weergegeven als Ja betekent dit dat een account voor werk of school voordat de computer die ooit is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c4d10-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span></span> <span data-ttu-id="c4d10-148">In dit geval wordt het account genegeerd als de verjaardag Update versie van Windows 10 (1607 wanneer de WinVer uitgevoerd opdracht in het venster 'Uitvoeren' of een opdrachtprompt).</span><span class="sxs-lookup"><span data-stu-id="c4d10-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="c4d10-149">WamDefaultSet: Ja en AzureADPrt: Ja</span><span class="sxs-lookup"><span data-stu-id="c4d10-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="c4d10-150">Deze velden weergeven dat de gebruiker heeft geverifieerd naar Azure AD bij het aanmelden bij het apparaat.</span><span class="sxs-lookup"><span data-stu-id="c4d10-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span></span> <span data-ttu-id="c4d10-151">Als u 'Nee' weergeven ze dat de volgende oorzaken hebben:</span><span class="sxs-lookup"><span data-stu-id="c4d10-151">If they show ‘NO’ the following are possible causes:</span></span>

- <span data-ttu-id="c4d10-152">Ongeldige opslagsleutel (BEURS) in de TPM die zijn gekoppeld aan het apparaat na inschrijving (Controleer de KeySignTest tijdens de uitvoering van verhoogde).</span><span class="sxs-lookup"><span data-stu-id="c4d10-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="c4d10-153">Alternatieve aanmeldings-ID</span><span class="sxs-lookup"><span data-stu-id="c4d10-153">Alternate Login ID</span></span>

- <span data-ttu-id="c4d10-154">HTTP-Proxy is niet gevonden</span><span class="sxs-lookup"><span data-stu-id="c4d10-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4d10-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4d10-155">Next steps</span></span>

<span data-ttu-id="c4d10-156">Zie voor meer informatie de [automatische apparaatregistratie Veelgestelde vragen](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="c4d10-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 