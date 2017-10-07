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
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a>Aan de slag met verificatie op basis van certificaten in Azure Active Directory

Verificatie op basis van certificaten kunt u toobe geverifieerd door Azure Active Directory met een clientcertificaat op een Windows-, Android of iOS-apparaat verbinding te maken met uw Exchange online-account in: 

- Mobiele Office-toepassingen zoals Microsoft Outlook en Microsoft Word   

- Exchange ActiveSync (EAS)-clients 

Configuratie van deze functie wordt voorkomen dat Hallo nodig tooenter een gebruikersnaam en wachtwoord combinatie in bepaalde e-mail en Microsoft Office-toepassingen op uw mobiele apparaat. 

Dit onderwerp:

- Biedt u Hello stappen tooconfigure gebruikmaken van verificatie op basis van certificaten voor gebruikers van tenants in Office 365 Enterprise, Business, Education en US Government-plannen. Deze functie is beschikbaar in preview in Office 365 China US Government verdediging en US Government Federal plannen. 

- Wordt ervan uitgegaan dat er al een [openbare-sleutelinfrastructuur (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) en [AD FS](connect/active-directory-aadconnectfed-whatis.md) geconfigureerd.    


## <a name="requirements"></a>Vereisten

tooconfigure certificaten gebaseerde verificatie Hallo volgende moet worden voldaan:  

- Certificaat gebaseerde verificatie (CBA) wordt alleen ondersteund voor een federatieve omgeving voor browser- of systeemeigen clients met moderne authenticatie (ADAL). Hallo een uitzondering is Exchange Active Sync (EAS) voor EXO die kan worden gebruikt voor zowel federatieve als beheerde accounts. 

- Hallo basiscertificeringsinstantie en tussenliggende certificeringsinstanties moeten worden geconfigureerd in Azure Active Directory.  

- Elke CA moet een certificaatintrekkingslijst (CRL) die kan worden verwezen via de URL van een internetverbinding hebben.  

- U moet ten minste één certificeringsinstantie geconfigureerd in Azure Active Directory hebben. Stappen vindt u verwante in Hallo [Hallo certificeringsinstanties configureren](#step-2-configure-the-certificate-authorities) sectie.  

- Voor Exchange ActiveSync-clients, moet clientcertificaat Hallo Hallo gebruikers routeerbaar e-mail adres Exchange online in beide Hallo Principal-naam of het Hallo RFC822 naamwaarde van Hallo alternatieve naam voor onderwerp veld hebben. Azure Active Directory maps Hallo RFC822 toohello proxyadres kenmerk value in Hallo-directory.  

- Het clientapparaat moet hebben toegang tooat minimaal één certificeringsinstantie die certificaten uitgeeft.  

- Een clientcertificaat voor clientverificatie zijn uitgegeven tooyour client.  




## <a name="step-1-select-your-device-platform"></a>Stap 1: Selecteer uw apparaatplatform

Als een eerste stap voor u belangrijk vindt u het platform Hallo apparaat tooreview Hallo volgende nodig:

- ondersteuning voor mobiele Office-toepassingen Hallo 
- Hallo specifieke implementatie-vereisten  

Hallo verwante informatie bestaat voor Hallo volgende apparaatplatforms:

- [Android](active-directory-certificate-based-authentication-android.md)
- [iOS](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a>Stap 2: Hallo certificeringsinstanties configureren 

tooconfigure uw certificeringsinstanties in Azure Active Directory, voor elke certificeringsinstantie uploaden hello te volgen: 

* Hallo openbare deel van het Hallo-certificaat *.cer* indeling 
* Hallo URL's voor Internetgericht waar hello certificaatintrekkingslijsten (CRL's) zich bevinden

Hallo-schema voor een certificeringsinstantie ziet er als volgt uit: 

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

Hallo-configuratie, kunt u Hallo [Azure Active Directory PowerShell versie 2](/powershell/azure/install-adv2?view=azureadps-2.0):  

1. Windows PowerShell starten met administratorbevoegdheden. 
2. Hello Azure AD-module installeren. U moet versie tooinstall [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) of hoger.  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

Als een eerste stap in de configuratie moet u tooestablish een verbinding met uw tenant. Zodra een verbinding tooyour tenant bestaat, kunt u bekijken, toevoegen, verwijderen en wijzigen Hallo vertrouwde certificeringsinstanties die zijn gedefinieerd in uw directory. 

### <a name="connect"></a>Verbinding maken

een verbinding met uw tenant, gebruik Hallo tooestablish [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:

    Connect-AzureAD 


### <a name="retrieve"></a>Ophalen 

tooretrieve hello vertrouwde certificeringsinstanties die zijn gedefinieerd in uw directory gebruiken Hallo [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet. 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a>Toevoegen

toocreate een vertrouwde certificeringsinstantie gebruiken Hallo [nieuw AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet en set Hallo **crlDistributionPoint** kenmerk tooa juiste waarde: 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a>Verwijderen

tooremove een vertrouwde certificeringsinstantie gebruiken Hallo [verwijderen AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a>Modfiy

toomodify een vertrouwde certificeringsinstantie gebruiken Hallo [Set AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a>Stap 3: Configureer intrekken

een clientcertificaat, Azure Active Directory toorevoke haalt Hallo certificaat certificaatintrekkingslijst (CRL) Hallo URL's als onderdeel van de informatie over certificeringsinstantie geüpload en opgeslagen in het cachegeheugen. Hallo publiceren laatste tijdstempel (**ingangsdatum** eigenschap) in Hallo CRL wordt gebruikt tooensure Hallo CRL is nog geldig. Hallo CRL is periodiek waarnaar wordt verwezen toorevoke toegang toocertificates die deel van het Hallo-lijst uitmaken.

Als een meer instant intrekking is vereist (bijvoorbeeld als een gebruiker verliest een apparaat), kunt ongeldig Hallo verificatietoken van Hallo gebruiker worden gemaakt. tooinvalidate hello autorisatie token, stel Hallo **StsRefreshTokenValidFrom** veld voor deze bepaalde gebruiker met behulp van Windows PowerShell. U moet bijwerken Hallo **StsRefreshTokenValidFrom** veld voor elke gebruiker die u wilt dat toorevoke toegang voor.

tooensure die Hallo intrekken zich blijft voordoen, moet u Hallo instellen **ingangsdatum** van Hallo CRL tooa datum na Hallo-waarde ingesteld door **StsRefreshTokenValidFrom** en zorg dat de betreffende Hallo-certificaat Hallo CRL.

volgende stappen overzicht Hallo proces voor het bijwerken en het Hallo-verificatietoken ongeldig te maken door de instelling Hallo Hallo **StsRefreshTokenValidFrom** veld. 

**tooconfigure intrekken:** 

1. Verbinding maken met de beheerservice referenties toohello MSOL: 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. Hallo huidige StsRefreshTokensValidFrom waarde ophalen voor een gebruiker: 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. Een nieuwe StsRefreshTokensValidFrom-waarde voor Hallo gebruiker gelijk toohello Huidig timestamp configureren: 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

Hallo datum die u instelt, moet zich in toekomstige Hallo. Als Hallo datum niet in toekomstige hello is, Hallo **StsRefreshTokensValidFrom** eigenschap is niet ingesteld. Als Hallo datum in toekomstige, Hallo **StsRefreshTokensValidFrom** toohello huidige tijd (geen Hallo datum aangegeven door de opdracht Set-MsolUser) is ingesteld. 


## <a name="step-4-test-your-configuration"></a>Stap 4: De configuratie van de testen

### <a name="testing-your-certificate"></a>Testen van uw certificaat

Als een eerste configuratietest, moet u toosign in te proberen[Outlook Web Access](https://outlook.office365.com) of [SharePoint Online](https://microsoft.sharepoint.com) met behulp van uw **browser op het apparaat**.

Als het aanmelden geslaagd is, weet u dat:

- Hallo gebruikerscertificaat is ingericht tooyour testapparaat
- AD FS is juist geconfigureerd  


### <a name="testing-office-mobile-applications"></a>Mobiele Office-toepassingen testen

**tootest verificatie op basis van certificaten op uw mobiele Office-toepassing:** 

1. Installeer een mobiele Office-toepassing (zoals OneDrive) op uw testapparaat.
3. Hallo toepassing starten. 
4. Voer uw gebruikersnaam en selecteer vervolgens Hallo gebruikerscertificaat gewenste toouse. 

U moet worden aangemeld. 

### <a name="testing-exchange-activesync-client-applications"></a>Exchange ActiveSync clienttoepassingen testen

tooaccess Exchange ActiveSync (EAS) via certificaat gebaseerde verificatie, een EAS-profiel met Hallo clientcertificaat moet beschikbaar toohello toepassing. 

Hallo EAS-profiel moet Hallo volgende informatie bevatten:

- Hallo gebruiker certificaat toobe gebruikt voor verificatie 

- Hallo EAS-eindpunt (bijvoorbeeld outlook.office365.com)

EAS-profiel kan worden geconfigureerd en worden geplaatst op Hallo apparaat via Hallo-gebruik van beheer van mobiele apparaten (MDM) zoals Intune, of door het plaatsen van Hallo certificaat handmatig in Hallo EAS-profiel op Hallo-apparaat.  

### <a name="testing-eas-client-applications-on-android"></a>Testen van toepassingen voor EAS-client op Android

**verificatie van tootest:**  

1. EAS-profiel configureren in Hallo-toepassing die voldoet aan de bovenstaande Hallo-vereisten.  
2. Open de toepassing hello en controleer of dat e-mail wordt gesynchroniseerd. 

