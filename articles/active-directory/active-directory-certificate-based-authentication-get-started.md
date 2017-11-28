---
title: Active Directory-verificatie op basis van certificaat - aaaAzure aan de slag | Microsoft Docs
description: Meer informatie over hoe tooconfigure op certificaten gebaseerde verificatie in uw omgeving
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="c011b-103">Aan de slag met verificatie op basis van certificaten in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c011b-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="c011b-104">Verificatie op basis van certificaten kunt u toobe geverifieerd door Azure Active Directory met een clientcertificaat op een Windows-, Android of iOS-apparaat verbinding te maken met uw Exchange online-account in:</span><span class="sxs-lookup"><span data-stu-id="c011b-104">Certificate-based authentication enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="c011b-105">Mobiele Office-toepassingen zoals Microsoft Outlook en Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="c011b-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="c011b-106">Exchange ActiveSync (EAS)-clients</span><span class="sxs-lookup"><span data-stu-id="c011b-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="c011b-107">Configuratie van deze functie wordt voorkomen dat Hallo nodig tooenter een gebruikersnaam en wachtwoord combinatie in bepaalde e-mail en Microsoft Office-toepassingen op uw mobiele apparaat.</span><span class="sxs-lookup"><span data-stu-id="c011b-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="c011b-108">Dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="c011b-108">This topic:</span></span>

- <span data-ttu-id="c011b-109">Biedt u Hello stappen tooconfigure gebruikmaken van verificatie op basis van certificaten voor gebruikers van tenants in Office 365 Enterprise, Business, Education en US Government-plannen.</span><span class="sxs-lookup"><span data-stu-id="c011b-109">Provides you with hello steps tooconfigure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="c011b-110">Deze functie is beschikbaar in preview in Office 365 China US Government verdediging en US Government Federal plannen.</span><span class="sxs-lookup"><span data-stu-id="c011b-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="c011b-111">Wordt ervan uitgegaan dat er al een [openbare-sleutelinfrastructuur (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) en [AD FS](connect/active-directory-aadconnectfed-whatis.md) geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c011b-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="c011b-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c011b-112">Requirements</span></span>

<span data-ttu-id="c011b-113">tooconfigure certificaten gebaseerde verificatie Hallo volgende moet worden voldaan:</span><span class="sxs-lookup"><span data-stu-id="c011b-113">tooconfigure certificate-based authentication, hello following must be true:</span></span>  

- <span data-ttu-id="c011b-114">Certificaat gebaseerde verificatie (CBA) wordt alleen ondersteund voor een federatieve omgeving voor browser- of systeemeigen clients met moderne authenticatie (ADAL).</span><span class="sxs-lookup"><span data-stu-id="c011b-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="c011b-115">Hallo een uitzondering is Exchange Active Sync (EAS) voor EXO die kan worden gebruikt voor zowel federatieve als beheerde accounts.</span><span class="sxs-lookup"><span data-stu-id="c011b-115">hello one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="c011b-116">Hallo basiscertificeringsinstantie en tussenliggende certificeringsinstanties moeten worden geconfigureerd in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c011b-116">hello root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="c011b-117">Elke CA moet een certificaatintrekkingslijst (CRL) die kan worden verwezen via de URL van een internetverbinding hebben.</span><span class="sxs-lookup"><span data-stu-id="c011b-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="c011b-118">U moet ten minste één certificeringsinstantie geconfigureerd in Azure Active Directory hebben.</span><span class="sxs-lookup"><span data-stu-id="c011b-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="c011b-119">Stappen vindt u verwante in Hallo [Hallo certificeringsinstanties configureren](#step-2-configure-the-certificate-authorities) sectie.</span><span class="sxs-lookup"><span data-stu-id="c011b-119">You can find related steps in hello [Configure hello certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="c011b-120">Voor Exchange ActiveSync-clients, moet clientcertificaat Hallo Hallo gebruikers routeerbaar e-mail adres Exchange online in beide Hallo Principal-naam of het Hallo RFC822 naamwaarde van Hallo alternatieve naam voor onderwerp veld hebben.</span><span class="sxs-lookup"><span data-stu-id="c011b-120">For Exchange ActiveSync clients, hello client certificate must have hello user’s routable email address in Exchange online in either hello Principal Name or hello RFC822 Name value of hello Subject Alternative Name field.</span></span> <span data-ttu-id="c011b-121">Azure Active Directory maps Hallo RFC822 toohello proxyadres kenmerk value in Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="c011b-121">Azure Active Directory maps hello RFC822 value toohello Proxy Address attribute in hello directory.</span></span>  

- <span data-ttu-id="c011b-122">Het clientapparaat moet hebben toegang tooat minimaal één certificeringsinstantie die certificaten uitgeeft.</span><span class="sxs-lookup"><span data-stu-id="c011b-122">Your client device must have access tooat least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="c011b-123">Een clientcertificaat voor clientverificatie zijn uitgegeven tooyour client.</span><span class="sxs-lookup"><span data-stu-id="c011b-123">A client certificate for client authentication must have been issued tooyour client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="c011b-124">Stap 1: Selecteer uw apparaatplatform</span><span class="sxs-lookup"><span data-stu-id="c011b-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="c011b-125">Als een eerste stap voor u belangrijk vindt u het platform Hallo apparaat tooreview Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="c011b-125">As a first step, for hello device platform you care about, you need tooreview hello following:</span></span>

- <span data-ttu-id="c011b-126">ondersteuning voor mobiele Office-toepassingen Hallo</span><span class="sxs-lookup"><span data-stu-id="c011b-126">hello Office mobile applications support</span></span> 
- <span data-ttu-id="c011b-127">Hallo specifieke implementatie-vereisten</span><span class="sxs-lookup"><span data-stu-id="c011b-127">hello specific implementation requirements</span></span>  

<span data-ttu-id="c011b-128">Hallo verwante informatie bestaat voor Hallo volgende apparaatplatforms:</span><span class="sxs-lookup"><span data-stu-id="c011b-128">hello related information exists for hello following device platforms:</span></span>

- [<span data-ttu-id="c011b-129">Android</span><span class="sxs-lookup"><span data-stu-id="c011b-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="c011b-130">iOS</span><span class="sxs-lookup"><span data-stu-id="c011b-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a><span data-ttu-id="c011b-131">Stap 2: Hallo certificeringsinstanties configureren</span><span class="sxs-lookup"><span data-stu-id="c011b-131">Step 2: Configure hello certificate authorities</span></span> 

<span data-ttu-id="c011b-132">tooconfigure uw certificeringsinstanties in Azure Active Directory, voor elke certificeringsinstantie uploaden hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="c011b-132">tooconfigure your certificate authorities in Azure Active Directory, for each certificate authority, upload hello following:</span></span> 

* <span data-ttu-id="c011b-133">Hallo openbare deel van het Hallo-certificaat *.cer* indeling</span><span class="sxs-lookup"><span data-stu-id="c011b-133">hello public portion of hello certificate, in *.cer* format</span></span> 
* <span data-ttu-id="c011b-134">Hallo URL's voor Internetgericht waar hello certificaatintrekkingslijsten (CRL's) zich bevinden</span><span class="sxs-lookup"><span data-stu-id="c011b-134">hello Internet facing URLs where hello Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="c011b-135">Hallo-schema voor een certificeringsinstantie ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="c011b-135">hello schema for a certificate authority looks as follows:</span></span> 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

<span data-ttu-id="c011b-136">Hallo-configuratie, kunt u Hallo [Azure Active Directory PowerShell versie 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="c011b-136">For hello configuration, you can use hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="c011b-137">Windows PowerShell starten met administratorbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="c011b-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="c011b-138">Hello Azure AD-module installeren.</span><span class="sxs-lookup"><span data-stu-id="c011b-138">Install hello Azure AD module.</span></span> <span data-ttu-id="c011b-139">U moet versie tooinstall [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) of hoger.</span><span class="sxs-lookup"><span data-stu-id="c011b-139">You need tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="c011b-140">Als een eerste stap in de configuratie moet u tooestablish een verbinding met uw tenant.</span><span class="sxs-lookup"><span data-stu-id="c011b-140">As a first configuration step, you need tooestablish a connection with your tenant.</span></span> <span data-ttu-id="c011b-141">Zodra een verbinding tooyour tenant bestaat, kunt u bekijken, toevoegen, verwijderen en wijzigen Hallo vertrouwde certificeringsinstanties die zijn gedefinieerd in uw directory.</span><span class="sxs-lookup"><span data-stu-id="c011b-141">As soon as a connection tooyour tenant exists, you can review, add, delete and modify hello trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="c011b-142">Verbinding maken</span><span class="sxs-lookup"><span data-stu-id="c011b-142">Connect</span></span>

<span data-ttu-id="c011b-143">een verbinding met uw tenant, gebruik Hallo tooestablish [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c011b-143">tooestablish a connection with your tenant, use hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="c011b-144">Ophalen</span><span class="sxs-lookup"><span data-stu-id="c011b-144">Retrieve</span></span> 

<span data-ttu-id="c011b-145">tooretrieve hello vertrouwde certificeringsinstanties die zijn gedefinieerd in uw directory gebruiken Hallo [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c011b-145">tooretrieve hello trusted certificate authorities that are defined in your directory, use hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="c011b-146">Toevoegen</span><span class="sxs-lookup"><span data-stu-id="c011b-146">Add</span></span>

<span data-ttu-id="c011b-147">toocreate een vertrouwde certificeringsinstantie gebruiken Hallo [nieuw AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet en set Hallo **crlDistributionPoint** kenmerk tooa juiste waarde:</span><span class="sxs-lookup"><span data-stu-id="c011b-147">toocreate a trusted certificate authority, use hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set hello **crlDistributionPoint** attribute tooa correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="c011b-148">Verwijderen</span><span class="sxs-lookup"><span data-stu-id="c011b-148">Remove</span></span>

<span data-ttu-id="c011b-149">tooremove een vertrouwde certificeringsinstantie gebruiken Hallo [verwijderen AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c011b-149">tooremove a trusted certificate authority, use hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="c011b-150">Modfiy</span><span class="sxs-lookup"><span data-stu-id="c011b-150">Modfiy</span></span>

<span data-ttu-id="c011b-151">toomodify een vertrouwde certificeringsinstantie gebruiken Hallo [Set AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c011b-151">toomodify a trusted certificate authority, use hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="c011b-152">Stap 3: Configureer intrekken</span><span class="sxs-lookup"><span data-stu-id="c011b-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="c011b-153">een clientcertificaat, Azure Active Directory toorevoke haalt Hallo certificaat certificaatintrekkingslijst (CRL) Hallo URL's als onderdeel van de informatie over certificeringsinstantie geüpload en opgeslagen in het cachegeheugen.</span><span class="sxs-lookup"><span data-stu-id="c011b-153">toorevoke a client certificate, Azure Active Directory fetches hello certificate revocation list (CRL) from hello URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="c011b-154">Hallo publiceren laatste tijdstempel (**ingangsdatum** eigenschap) in Hallo CRL wordt gebruikt tooensure Hallo CRL is nog geldig.</span><span class="sxs-lookup"><span data-stu-id="c011b-154">hello last publish timestamp (**Effective Date** property) in hello CRL is used tooensure hello CRL is still valid.</span></span> <span data-ttu-id="c011b-155">Hallo CRL is periodiek waarnaar wordt verwezen toorevoke toegang toocertificates die deel van het Hallo-lijst uitmaken.</span><span class="sxs-lookup"><span data-stu-id="c011b-155">hello CRL is periodically referenced toorevoke access toocertificates that are a part of hello list.</span></span>

<span data-ttu-id="c011b-156">Als een meer instant intrekking is vereist (bijvoorbeeld als een gebruiker verliest een apparaat), kunt ongeldig Hallo verificatietoken van Hallo gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c011b-156">If a more instant revocation is required (for example, if a user loses a device), hello authorization token of hello user can be invalidated.</span></span> <span data-ttu-id="c011b-157">tooinvalidate hello autorisatie token, stel Hallo **StsRefreshTokenValidFrom** veld voor deze bepaalde gebruiker met behulp van Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c011b-157">tooinvalidate hello authorization token, set hello **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="c011b-158">U moet bijwerken Hallo **StsRefreshTokenValidFrom** veld voor elke gebruiker die u wilt dat toorevoke toegang voor.</span><span class="sxs-lookup"><span data-stu-id="c011b-158">You must update hello **StsRefreshTokenValidFrom** field for each user you want toorevoke access for.</span></span>

<span data-ttu-id="c011b-159">tooensure die Hallo intrekken zich blijft voordoen, moet u Hallo instellen **ingangsdatum** van Hallo CRL tooa datum na Hallo-waarde ingesteld door **StsRefreshTokenValidFrom** en zorg dat de betreffende Hallo-certificaat Hallo CRL.</span><span class="sxs-lookup"><span data-stu-id="c011b-159">tooensure that hello revocation persists, you must set hello **Effective Date** of hello CRL tooa date after hello value set by **StsRefreshTokenValidFrom** and ensure hello certificate in question is in hello CRL.</span></span>

<span data-ttu-id="c011b-160">volgende stappen overzicht Hallo proces voor het bijwerken en het Hallo-verificatietoken ongeldig te maken door de instelling Hallo Hallo **StsRefreshTokenValidFrom** veld.</span><span class="sxs-lookup"><span data-stu-id="c011b-160">hello following steps outline hello process for updating and invalidating hello authorization token by setting hello **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="c011b-161">**tooconfigure intrekken:**</span><span class="sxs-lookup"><span data-stu-id="c011b-161">**tooconfigure revocation:**</span></span> 

1. <span data-ttu-id="c011b-162">Verbinding maken met de beheerservice referenties toohello MSOL:</span><span class="sxs-lookup"><span data-stu-id="c011b-162">Connect with admin credentials toohello MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="c011b-163">Hallo huidige StsRefreshTokensValidFrom waarde ophalen voor een gebruiker:</span><span class="sxs-lookup"><span data-stu-id="c011b-163">Retrieve hello current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="c011b-164">Een nieuwe StsRefreshTokensValidFrom-waarde voor Hallo gebruiker gelijk toohello Huidig timestamp configureren:</span><span class="sxs-lookup"><span data-stu-id="c011b-164">Configure a new StsRefreshTokensValidFrom value for hello user equal toohello current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="c011b-165">Hallo datum die u instelt, moet zich in toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="c011b-165">hello date you set must be in hello future.</span></span> <span data-ttu-id="c011b-166">Als Hallo datum niet in toekomstige hello is, Hallo **StsRefreshTokensValidFrom** eigenschap is niet ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c011b-166">If hello date is not in hello future, hello **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="c011b-167">Als Hallo datum in toekomstige, Hallo **StsRefreshTokensValidFrom** toohello huidige tijd (geen Hallo datum aangegeven door de opdracht Set-MsolUser) is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c011b-167">If hello date is in hello future, **StsRefreshTokensValidFrom** is set toohello current time (not hello date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="c011b-168">Stap 4: De configuratie van de testen</span><span class="sxs-lookup"><span data-stu-id="c011b-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="c011b-169">Testen van uw certificaat</span><span class="sxs-lookup"><span data-stu-id="c011b-169">Testing your certificate</span></span>

<span data-ttu-id="c011b-170">Als een eerste configuratietest, moet u toosign in te proberen[Outlook Web Access](https://outlook.office365.com) of [SharePoint Online](https://microsoft.sharepoint.com) met behulp van uw **browser op het apparaat**.</span><span class="sxs-lookup"><span data-stu-id="c011b-170">As a first configuration test, you should try toosign in too[Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="c011b-171">Als het aanmelden geslaagd is, weet u dat:</span><span class="sxs-lookup"><span data-stu-id="c011b-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="c011b-172">Hallo gebruikerscertificaat is ingericht tooyour testapparaat</span><span class="sxs-lookup"><span data-stu-id="c011b-172">hello user certificate has been provisioned tooyour test device</span></span>
- <span data-ttu-id="c011b-173">AD FS is juist geconfigureerd</span><span class="sxs-lookup"><span data-stu-id="c011b-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="c011b-174">Mobiele Office-toepassingen testen</span><span class="sxs-lookup"><span data-stu-id="c011b-174">Testing Office mobile applications</span></span>

<span data-ttu-id="c011b-175">**tootest verificatie op basis van certificaten op uw mobiele Office-toepassing:**</span><span class="sxs-lookup"><span data-stu-id="c011b-175">**tootest certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="c011b-176">Installeer een mobiele Office-toepassing (zoals OneDrive) op uw testapparaat.</span><span class="sxs-lookup"><span data-stu-id="c011b-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="c011b-177">Hallo toepassing starten.</span><span class="sxs-lookup"><span data-stu-id="c011b-177">Launch hello application.</span></span> 
4. <span data-ttu-id="c011b-178">Voer uw gebruikersnaam en selecteer vervolgens Hallo gebruikerscertificaat gewenste toouse.</span><span class="sxs-lookup"><span data-stu-id="c011b-178">Enter your user name, and then select hello user certificate you want toouse.</span></span> 

<span data-ttu-id="c011b-179">U moet worden aangemeld.</span><span class="sxs-lookup"><span data-stu-id="c011b-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="c011b-180">Exchange ActiveSync clienttoepassingen testen</span><span class="sxs-lookup"><span data-stu-id="c011b-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="c011b-181">tooaccess Exchange ActiveSync (EAS) via certificaat gebaseerde verificatie, een EAS-profiel met Hallo clientcertificaat moet beschikbaar toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="c011b-181">tooaccess Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing hello client certificate must be available toohello application.</span></span> 

<span data-ttu-id="c011b-182">Hallo EAS-profiel moet Hallo volgende informatie bevatten:</span><span class="sxs-lookup"><span data-stu-id="c011b-182">hello EAS profile must contain hello following information:</span></span>

- <span data-ttu-id="c011b-183">Hallo gebruiker certificaat toobe gebruikt voor verificatie</span><span class="sxs-lookup"><span data-stu-id="c011b-183">hello user certificate toobe used for authentication</span></span> 

- <span data-ttu-id="c011b-184">Hallo EAS-eindpunt (bijvoorbeeld outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="c011b-184">hello EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="c011b-185">EAS-profiel kan worden geconfigureerd en worden geplaatst op Hallo apparaat via Hallo-gebruik van beheer van mobiele apparaten (MDM) zoals Intune, of door het plaatsen van Hallo certificaat handmatig in Hallo EAS-profiel op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c011b-185">An EAS profile can be configured and placed on hello device through hello utilization of Mobile device management (MDM) such as Intune or by manually placing hello certificate in hello EAS profile on hello device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="c011b-186">Testen van toepassingen voor EAS-client op Android</span><span class="sxs-lookup"><span data-stu-id="c011b-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="c011b-187">**verificatie van tootest:**</span><span class="sxs-lookup"><span data-stu-id="c011b-187">**tootest certificate authentication:**</span></span>  

1. <span data-ttu-id="c011b-188">EAS-profiel configureren in Hallo-toepassing die voldoet aan de bovenstaande Hallo-vereisten.</span><span class="sxs-lookup"><span data-stu-id="c011b-188">Configure an EAS profile in hello application that satisfies hello requirements above.</span></span>  
2. <span data-ttu-id="c011b-189">Open de toepassing hello en controleer of dat e-mail wordt gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="c011b-189">Open hello application, and verify that mail is synchronizing.</span></span> 

