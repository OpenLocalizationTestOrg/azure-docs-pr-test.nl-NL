---
title: aaaTroubleshooting hello automatische registratie van Azure AD-domein voor Windows 10 en Windows Server 2016 computers die lid zijn | Microsoft Docs
description: Het oplossen van problemen Hallo automatische registratie van Azure AD-domein lid zijn van computers voor Windows 10 en Windows Server 2016.
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
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="4e505-103">Automatische registratie van domein het oplossen van problemen die lid zijn van computers tooAzure AD – Windows 10 en Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="4e505-103">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="4e505-104">In dit onderwerp is van toepassing toohello volgende clients:</span><span class="sxs-lookup"><span data-stu-id="4e505-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="4e505-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="4e505-105">Windows 10</span></span>
-   <span data-ttu-id="4e505-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="4e505-106">Windows Server 2016</span></span>

<span data-ttu-id="4e505-107">Zie voor andere Windows-clients [computers tooAzure AD probleemoplossing automatische registratie van domein worden toegevoegd voor Windows downlevel-clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="4e505-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="4e505-108">Dit onderwerp wordt ervan uitgegaan dat u hebt geconfigureerd automatische registratie van apparaten domein vermelde in dat wordt beschreven in [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="4e505-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello following scenarios:</span></span>

- [<span data-ttu-id="4e505-109">Voorwaardelijke toegang op basis van apparaten</span><span class="sxs-lookup"><span data-stu-id="4e505-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="4e505-110">Enterprise-instellingen voor roaming</span><span class="sxs-lookup"><span data-stu-id="4e505-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="4e505-111">Windows Hello voor Bedrijven</span><span class="sxs-lookup"><span data-stu-id="4e505-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="4e505-112">Dit document bevat richtlijnen voor probleemoplossing over hoe tooresolve mogelijke problemen.</span><span class="sxs-lookup"><span data-stu-id="4e505-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 

<span data-ttu-id="4e505-113">Hallo wordt registratie ondersteund in Windows hello Update 10 November 2015 en hoger.</span><span class="sxs-lookup"><span data-stu-id="4e505-113">hello registration is supported in hello Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="4e505-114">U kunt het beste Hallo Verjaardag Update gebruikt voor het inschakelen van de bovenstaande Hallo scenario's.</span><span class="sxs-lookup"><span data-stu-id="4e505-114">We recommend using hello Anniversary Update for enabling hello scenarios above.</span></span>

## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="4e505-115">Stap 1: De registratiestatus Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="4e505-115">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="4e505-116">**tooretrieve hello registratiestatus:**</span><span class="sxs-lookup"><span data-stu-id="4e505-116">**tooretrieve hello registration status:**</span></span>

1. <span data-ttu-id="4e505-117">Open Hallo-opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="4e505-117">Open hello command prompt as an administrator.</span></span>

2. <span data-ttu-id="4e505-118">Type **dsregcmd/status**</span><span class="sxs-lookup"><span data-stu-id="4e505-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="4e505-119">+----------------------------------------------------------------------+
   | Apparaatstatus |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="4e505-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="4e505-120">EnterpriseJoined: Geen apparaat-id: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 vingerafdruk: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto-Provider TpmProtected: Ja KeySignTest:: moet uitvoeren met verhoogde bevoegdheden voor tootest.</span><span class="sxs-lookup"><span data-stu-id="4e505-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="4e505-121">IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: Ja DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="4e505-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="4e505-122">+----------------------------------------------------------------------+
   | Gebruikersstatus |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="4e505-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="4e505-123">WamDefaultAuthority: organisaties WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd) AzureAdPrt: Ja</span><span class="sxs-lookup"><span data-stu-id="4e505-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="4e505-124">Stap 2: De registratiestatus Hallo</span><span class="sxs-lookup"><span data-stu-id="4e505-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="4e505-125">Bekijk Hallo velden te volgen en zorg ervoor dat ze Hallo verwachte waarden hebben:</span><span class="sxs-lookup"><span data-stu-id="4e505-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="4e505-126">AzureAdJoined: Ja</span><span class="sxs-lookup"><span data-stu-id="4e505-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="4e505-127">Dit veld bevat of Hallo-apparaat is geregistreerd bij Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e505-127">This field shows whether hello device is registered with Azure AD.</span></span> <span data-ttu-id="4e505-128">Als Hallo waarde wordt weergegeven als 'Nee', worden de registratie is niet voltooid.</span><span class="sxs-lookup"><span data-stu-id="4e505-128">If hello value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="4e505-129">**Mogelijke oorzaken:**</span><span class="sxs-lookup"><span data-stu-id="4e505-129">**Possible causes:**</span></span>

- <span data-ttu-id="4e505-130">Verificatie van de computer Hallo voor registratie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="4e505-130">Authentication of hello computer for registration failed.</span></span>

- <span data-ttu-id="4e505-131">Er is een HTTP-proxy in Hallo organisatie die niet kan worden gedetecteerd door Hallo-computer</span><span class="sxs-lookup"><span data-stu-id="4e505-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="4e505-132">Hallo-computer kan Azure AD voor de verificatie of Azure DRS voor registratie niet bereiken</span><span class="sxs-lookup"><span data-stu-id="4e505-132">hello computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="4e505-133">Hallo computer mogelijk niet op het interne netwerk van de organisatie van de Hallo of VPN met rechtstreeks tooan lokale AD-domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="4e505-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="4e505-134">Als Hallo computer een TPM heeft, wordt in een verkeerde status.</span><span class="sxs-lookup"><span data-stu-id="4e505-134">If hello computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="4e505-135">Er is mogelijk een onjuiste configuratie van services eerder hebt genoteerd in Hallo-document dat u tooverify opnieuw moet.</span><span class="sxs-lookup"><span data-stu-id="4e505-135">There may be a misconfiguration in services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="4e505-136">Algemene voorbeelden zijn:</span><span class="sxs-lookup"><span data-stu-id="4e505-136">Common examples are:</span></span>

    - <span data-ttu-id="4e505-137">De federatieserver is geen WS-Trust-eindpunten die zijn ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="4e505-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="4e505-138">De federatieserver mogelijk niet toegestaan voor binnenkomende verificatie vanaf computers in uw netwerk met behulp van geïntegreerde Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="4e505-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="4e505-139">Er is geen Service Connection Point-object dat tooyour geverifieerde domeinnaam op in Azure AD in Hallo AD-forest waar Hallo computer behoort beheerpunten bij</span><span class="sxs-lookup"><span data-stu-id="4e505-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="4e505-140">DomainJoined: Ja</span><span class="sxs-lookup"><span data-stu-id="4e505-140">DomainJoined : YES</span></span>  

<span data-ttu-id="4e505-141">Dit veld wordt aangegeven of Hallo apparaat lid tooan op lokale Active Directory of niet.</span><span class="sxs-lookup"><span data-stu-id="4e505-141">This field shows whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="4e505-142">Als het Hallo-waarde wordt weergegeven als **Nee**, Hallo apparaat niet automatisch kan registreren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e505-142">If hello value shows as **NO**, hello device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="4e505-143">Controleer eerst die Hallo apparaat joins toohello op lokale Active Directory voordat u deze kunt registreren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e505-143">Check first that hello device joins toohello on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="4e505-144">Als u om lid te worden Hallo computer tooAzure AD rechtstreeks op zoek bent, gaat u tooLearn over de mogelijkheden van Azure Active Directory Join.</span><span class="sxs-lookup"><span data-stu-id="4e505-144">If you are looking for joining hello computer tooAzure AD directly, please go tooLearn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="4e505-145">WorkplaceJoined: Nee</span><span class="sxs-lookup"><span data-stu-id="4e505-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="4e505-146">Dit veld bevat of Hallo-apparaat is geregistreerd met Azure AD, maar als een persoonlijk apparaat (gemarkeerd als 'Workplace Joined').</span><span class="sxs-lookup"><span data-stu-id="4e505-146">This field shows whether hello device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="4e505-147">Als deze waarde moet worden weergegeven als 'Nee' voor een computer verbonden met het domein is geregistreerd in Azure AD, maar als deze wordt weergegeven als Ja betekent dit dat is een account voor werk of school toegevoegde voorafgaande toohello computer voltooien registratie.</span><span class="sxs-lookup"><span data-stu-id="4e505-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior toohello computer completing registration.</span></span> <span data-ttu-id="4e505-148">In dit geval worden Hallo-account genegeerd als Hallo Verjaardag Update versie van Windows 10 (1607 wanneer de opdracht WinVer Hallo uitgevoerd in de Hallo venster 'Uitvoeren' of een opdrachtpromptvenster).</span><span class="sxs-lookup"><span data-stu-id="4e505-148">In this case hello account will be ignored if using hello Anniversary Update version of Windows 10 (1607 when running hello WinVer command in hello ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="4e505-149">WamDefaultSet: Ja en AzureADPrt: Ja</span><span class="sxs-lookup"><span data-stu-id="4e505-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="4e505-150">Deze velden weergeven dat die Hallo-gebruiker is geverifieerd tooAzure AD bij de ondertekening van toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="4e505-150">These fields show that hello user has successfully authenticated tooAzure AD upon signing in toohello device.</span></span> <span data-ttu-id="4e505-151">Als ze weergeven volgen 'NO' hello mogelijke oorzaken:</span><span class="sxs-lookup"><span data-stu-id="4e505-151">If they show ‘NO’ hello following are possible causes:</span></span>

- <span data-ttu-id="4e505-152">Ongeldige opslagsleutel (BEURS) in de TPM die zijn gekoppeld aan Hallo apparaat na inschrijving (selectievakje hello KeySignTest tijdens de uitvoering van verhoogde).</span><span class="sxs-lookup"><span data-stu-id="4e505-152">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="4e505-153">Alternatieve aanmeldings-ID</span><span class="sxs-lookup"><span data-stu-id="4e505-153">Alternate Login ID</span></span>

- <span data-ttu-id="4e505-154">HTTP-Proxy is niet gevonden</span><span class="sxs-lookup"><span data-stu-id="4e505-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e505-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4e505-155">Next steps</span></span>

<span data-ttu-id="4e505-156">Zie voor meer informatie, Hallo [automatische apparaatregistratie Veelgestelde vragen](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="4e505-156">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
