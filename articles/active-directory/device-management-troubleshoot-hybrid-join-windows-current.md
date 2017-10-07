---
title: aaaTroubleshooting hybride Azure Active Directory die lid zijn van apparaten met Windows 10 en Windows Server 2016 | Microsoft Docs
description: Apparaten met Windows 10 en Windows Server 2016 probleemoplossing hybride Azure Active Directory worden toegevoegd.
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="e692b-103">Het oplossen van hybride Azure Active Directory die lid zijn van Windows 10 en Windows Server 2016-apparaten</span><span class="sxs-lookup"><span data-stu-id="e692b-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="e692b-104">In dit onderwerp is van toepassing toohello volgende clients:</span><span class="sxs-lookup"><span data-stu-id="e692b-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="e692b-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="e692b-105">Windows 10</span></span>
-   <span data-ttu-id="e692b-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e692b-106">Windows Server 2016</span></span>

<span data-ttu-id="e692b-107">Zie voor andere Windows-clients [probleemoplossing hybride Azure Active Directory die lid zijn van de downlevel-apparaten](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="e692b-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="e692b-108">Dit onderwerp wordt ervan uitgegaan dat u hebt [geconfigureerde hybride Azure Active Directory die lid zijn van de apparaten](device-management-hybrid-azuread-joined-devices-setup.md) toosupport Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="e692b-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="e692b-109">Voorwaardelijke toegang op basis van apparaten</span><span class="sxs-lookup"><span data-stu-id="e692b-109">Device-based conditional access</span></span>

- [<span data-ttu-id="e692b-110">Enterprise-instellingen voor roaming</span><span class="sxs-lookup"><span data-stu-id="e692b-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="e692b-111">Windows Hello voor Bedrijven</span><span class="sxs-lookup"><span data-stu-id="e692b-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="e692b-112">Dit document bevat richtlijnen voor probleemoplossing over hoe tooresolve mogelijke problemen.</span><span class="sxs-lookup"><span data-stu-id="e692b-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 


<span data-ttu-id="e692b-113">Voor Windows 10 en Windows Server 2016 hybride Azure Active Directory join ondersteunt Hallo Windows 10 November 2015 Update en hoger.</span><span class="sxs-lookup"><span data-stu-id="e692b-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports hello Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="e692b-114">U kunt het beste Hallo Verjaardag update gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e692b-114">We recommend using hello Anniversary update.</span></span>

## <a name="step-1-retrieve-hello-join-status"></a><span data-ttu-id="e692b-115">Stap 1: Hallo join status ophalen</span><span class="sxs-lookup"><span data-stu-id="e692b-115">Step 1: Retrieve hello join status</span></span> 

<span data-ttu-id="e692b-116">**tooretrieve hello join-status:**</span><span class="sxs-lookup"><span data-stu-id="e692b-116">**tooretrieve hello join status:**</span></span>

1. <span data-ttu-id="e692b-117">Open Hallo opdrachtprompt als beheerder</span><span class="sxs-lookup"><span data-stu-id="e692b-117">Open hello command prompt as an administrator</span></span>

2. <span data-ttu-id="e692b-118">Type **dsregcmd/status**</span><span class="sxs-lookup"><span data-stu-id="e692b-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="e692b-119">+----------------------------------------------------------------------+
   | Apparaatstatus |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="e692b-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="e692b-120">EnterpriseJoined: Geen apparaat-id: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 vingerafdruk: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto-Provider TpmProtected: Ja KeySignTest:: moet uitvoeren met verhoogde bevoegdheden voor tootest.</span><span class="sxs-lookup"><span data-stu-id="e692b-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="e692b-121">IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: Ja DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="e692b-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="e692b-122">+----------------------------------------------------------------------+
   | Gebruikersstatus |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="e692b-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="e692b-123">WamDefaultAuthority: organisaties WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd) AzureAdPrt: Ja</span><span class="sxs-lookup"><span data-stu-id="e692b-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-hello-join-status"></a><span data-ttu-id="e692b-124">Stap 2: De Hallo join-status</span><span class="sxs-lookup"><span data-stu-id="e692b-124">Step 2: Evaluate hello join status</span></span> 

<span data-ttu-id="e692b-125">Bekijk Hallo velden te volgen en zorg ervoor dat ze Hallo verwachte waarden hebben:</span><span class="sxs-lookup"><span data-stu-id="e692b-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="e692b-126">AzureAdJoined: Ja</span><span class="sxs-lookup"><span data-stu-id="e692b-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="e692b-127">Dit veld geeft aan of het Hallo-apparaat is verbonden met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e692b-127">This field indicates whether hello device is joined with Azure AD.</span></span> <span data-ttu-id="e692b-128">Als de waarde Hallo **Nee**, Hallo join tooAzure AD is nog niet voltooid.</span><span class="sxs-lookup"><span data-stu-id="e692b-128">If hello value is **NO**, hello join tooAzure AD has not completed yet.</span></span> 

<span data-ttu-id="e692b-129">**Mogelijke oorzaken:**</span><span class="sxs-lookup"><span data-stu-id="e692b-129">**Possible causes:**</span></span>

- <span data-ttu-id="e692b-130">Verificatie van de computer Hallo voor een join is mislukt.</span><span class="sxs-lookup"><span data-stu-id="e692b-130">Authentication of hello computer for a join failed.</span></span>

- <span data-ttu-id="e692b-131">Er is een HTTP-proxy in Hallo organisatie die niet kan worden gedetecteerd door Hallo-computer</span><span class="sxs-lookup"><span data-stu-id="e692b-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="e692b-132">Hallo-computer kan niet bereiken tooauthenticate Azure AD of Azure DRS voor registratie</span><span class="sxs-lookup"><span data-stu-id="e692b-132">hello computer cannot reach Azure AD tooauthenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="e692b-133">Hallo computer mogelijk niet op het interne netwerk van de organisatie van de Hallo of VPN met rechtstreeks tooan lokale AD-domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="e692b-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="e692b-134">Als het Hallo-computer heeft een TPM, kan het zijn in orde.</span><span class="sxs-lookup"><span data-stu-id="e692b-134">If hello computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="e692b-135">Er zijn mogelijk een onjuiste configuratie van Hallo services eerder hebt genoteerd in Hallo-document dat u tooverify opnieuw moet.</span><span class="sxs-lookup"><span data-stu-id="e692b-135">There might be a misconfiguration in hello services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="e692b-136">Algemene voorbeelden zijn:</span><span class="sxs-lookup"><span data-stu-id="e692b-136">Common examples are:</span></span>

    - <span data-ttu-id="e692b-137">De federatieserver is geen WS-Trust-eindpunten die zijn ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="e692b-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="e692b-138">De federatieserver kan geen binnenkomende verificatie vanaf computers in uw netwerk met behulp van geïntegreerde Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="e692b-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="e692b-139">Er is geen Service Connection Point-object dat tooyour geverifieerde domeinnaam op in Azure AD in Hallo AD-forest waar Hallo computer behoort beheerpunten bij</span><span class="sxs-lookup"><span data-stu-id="e692b-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="e692b-140">DomainJoined: Ja</span><span class="sxs-lookup"><span data-stu-id="e692b-140">DomainJoined : YES</span></span>  

<span data-ttu-id="e692b-141">Dit veld geeft aan of het Hallo-apparaat is lid van tooan op lokale Active Directory of niet.</span><span class="sxs-lookup"><span data-stu-id="e692b-141">This field indicates whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="e692b-142">Als de waarde Hallo **Nee**, Hallo-apparaat een hybride Azure AD join kan niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e692b-142">If hello value is **NO**, hello device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="e692b-143">WorkplaceJoined: Nee</span><span class="sxs-lookup"><span data-stu-id="e692b-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="e692b-144">Dit veld wordt aangegeven of het Hallo-apparaat is geregistreerd bij Azure AD als een persoonlijk apparaat (gemarkeerd als *Workplace Joined*).</span><span class="sxs-lookup"><span data-stu-id="e692b-144">This field indicates whether hello device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="e692b-145">Deze waarde moet **Nee** voor een domein computer die ook hybride Azure AD die lid zijn.</span><span class="sxs-lookup"><span data-stu-id="e692b-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="e692b-146">Als de waarde Hallo **Ja**, een account voor werk of school voorafgaande toohello voltooiing Hallo hybride Azure AD join is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e692b-146">If hello value is **YES**, a work or school account was added prior toohello completion of hello hybrid Azure AD join.</span></span> <span data-ttu-id="e692b-147">Hallo-account wordt in dit geval genegeerd wanneer Hallo Verjaardag Update versie van Windows 10 (1607).</span><span class="sxs-lookup"><span data-stu-id="e692b-147">In this case, hello account is ignored when using hello Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="e692b-148">WamDefaultSet: Ja en AzureADPrt: Ja</span><span class="sxs-lookup"><span data-stu-id="e692b-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="e692b-149">Deze velden wordt aangegeven of de gebruiker Hallo tooAzure AD heeft geverifieerd bij de aanmelding toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="e692b-149">These fields indicate whether hello user has successfully authenticated tooAzure AD when signing in toohello device.</span></span> <span data-ttu-id="e692b-150">Als de waarden Hallo **Nee**, kan worden voldaan:</span><span class="sxs-lookup"><span data-stu-id="e692b-150">If hello values are **NO**, it could be due:</span></span>

- <span data-ttu-id="e692b-151">Ongeldige opslagsleutel (BEURS) in de TPM die zijn gekoppeld aan Hallo apparaat na inschrijving (selectievakje hello KeySignTest tijdens de uitvoering van verhoogde).</span><span class="sxs-lookup"><span data-stu-id="e692b-151">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="e692b-152">Alternatieve aanmeldings-ID</span><span class="sxs-lookup"><span data-stu-id="e692b-152">Alternate Login ID</span></span>

- <span data-ttu-id="e692b-153">HTTP-Proxy is niet gevonden</span><span class="sxs-lookup"><span data-stu-id="e692b-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="e692b-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e692b-154">Next steps</span></span>

<span data-ttu-id="e692b-155">Bekijk voor vragen Hallo [Apparaatbeheer Veelgestelde vragen](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="e692b-155">For questions, see hello [device management FAQ](device-management-faq.md)</span></span> 
