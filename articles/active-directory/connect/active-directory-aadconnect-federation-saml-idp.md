---
title: 'Azure AD Connect: Gebruik een SAML-identiteitsprovider 2.0 voor eenmalige aanmelding in | Microsoft Docs'
description: In dit onderwerp wordt beschreven hoe een compatibele Idp SAML 2.0 voor eenmalige aanmelding op.
services: active-directory
author: billmath
manager: femila
ms.custom: it-pro
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f9653dc44fb284a9b3c1988f623c33f27ae148cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#  <a name="use-a-saml-20-identity-provider-idp-for-single-sign-on"></a>Gebruik van SAML 2.0-identiteitsprovider (IdP) voor eenmalige aanmelding in

Dit onderwerp bevat informatie over het gebruik van een SAML 2.0 compatibel SP Lite-profiel op basis van id-Provider zoals hello Security Token Service (STS) voorkeur / id-provider. Dit is handig wanneer u hebt al een map van de gebruiker en het wachtwoord voor het opslaan van lokale die kunnen worden geopend met behulp van SAML 2.0. Deze bestaande map van de gebruiker kan worden gebruikt voor eenmalige aanmelding tooOffice 365 en andere Azure AD-beveiligde bronnen. Hallo SAML 2.0 SP-Lite profiel is gebaseerd op Hallo alom gebruikt Security Assertion Markup Language (SAML) federatieve identiteit standaard tooprovide een eenmalige aanmelding en het kenmerk exchange framework.

>[!NOTE]
>Voor een lijst van 3e partij Idps die zijn getest voor gebruik met Azure AD raadpleegt Hallo [Azure AD-federatiecompatibiliteitslijst](active-directory-aadconnect-federation-compatibility.md)

Microsoft ondersteunt deze ervaring aanmelding als Hallo integratie van een Microsoft-cloudservice, zoals Office 365, met uw correct geconfigureerde SAML 2.0 profiel op basis van IdP. SAML 2.0 identiteitsproviders zijn producten van derden en daarom Microsoft biedt geen ondersteuning voor Hallo-implementatie, configuratie, met betrekking tot deze aanbevolen procedures voor het oplossen van problemen. Eenmaal correct is geconfigureerd, Hallo-integratie met Hallo SAML 2.0-id-provider voor de juiste configuratie kan worden getest met behulp van Hallo Microsoft connectiviteit Analyzer Tool die wordt hieronder in detail beschreven. Vraag Hallo organisatie die deze heeft geleverd voor meer informatie over uw SAML 2.0 SP-Lite profiel op basis van id-provider.

>[!IMPORTANT]
>Alleen een beperkte set clients zijn beschikbaar in dit scenario aanmelding met identiteitsproviders SAML 2.0, wordt dit omvat:

>- Web-gebaseerde clients zoals Outlook Web Access en SharePoint Online
- E-rich clients die gebruikmaken van basisverificatie en een ondersteunde Exchange toegangsmethode zoals IMAP, pop-server, ActiveSync, MAPI, enzovoort (hello uitgebreid clientprotocol eindpunt is vereist toobe geïmplementeerd), waaronder:
    - Microsoft Outlook 2010/Outlook 2013/Outlook 2016, Apple iPhone (verschillende iOS-versies)
    - Verschillende Google Android-apparaten
    - Windows Phone 7, Windows Phone 7,8 en Windows Phone 8.0
    - E-mailclient van Windows 8 en Windows 8.1-e-mailclient
    - E-mailclient van Windows 10

Alle andere clients zijn niet beschikbaar in dit scenario aanmelding met de id-Provider van SAML 2.0. Hallo Lync 2010 bureaubladclient is bijvoorbeeld niet kunnen toologin Hallo brengen met het SAML 2.0-identiteitsprovider geconfigureerd voor eenmalige aanmelding.

## <a name="azure-ad-saml-20-protocol-requirements"></a>Vereisten voor Azure AD-SAML 2.0-protocol
Dit onderwerp bevat gedetailleerde vereisten op het Hallo-protocol en berichtindeling dat uw SAML 2.0-id-provider toofederate met Azure AD tooenable aanmelding tooone of meer Microsoft-cloudservices (zoals Office 365 implementeren moet). Hallo SAML 2.0 relying party (SP-STS) voor een Microsoft-cloudservice in dit scenario gebruikt is Azure AD.

Het is raadzaam dat u uw SAML 2.0 identiteit provider Uitvoerberichten als vergelijkbaar toohello opgegeven voorbeeld traceringen mogelijk worden voor zorgen. Gebruik kenmerkwaarden van Hallo levert ook Azure AD-metagegevens, waar mogelijk. Wanneer u tevreden met uw Uitvoerberichten bent, kunt u testen met Microsoft connectiviteit Analyzer Hallo zoals hieronder wordt beschreven.

metagegevens Hello Azure AD kan worden gedownload vanaf deze URL: [https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml).
Voor klanten in China met behulp van hello China-specifieke exemplaar van Office 365, Hallo na federation-eindpunt moet worden gebruikt: [https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml).

## <a name="saml-protocol-requirements"></a>Vereisten voor SAML-protocol
In deze sectie worden hoe Hallo aanvraag en -antwoord berichtenparen worden samenstellen in volgorde toohelp u tooformat uw berichten correct.

Azure AD kan worden geconfigureerd toowork met de id-providers die Hallo SAML 2.0 SP Lite profiel met een aantal specifieke vereisten gebruiken, zoals hieronder weergegeven. Hallo voorbeeld SAML-aanvraag en antwoord-berichten samen met automatische en handmatige testen kunt u tooachieve interoperabiliteit met Azure AD werken.

## <a name="signature-block-requirements"></a>Vereisten voor het blokkeren van handtekeningen
Knooppunt bericht Hallo-handtekening bevat binnen Hallo SAML-reactie die informatie over Hallo digitale handtekening voor het Hallo-bericht zelf. Hallo handtekeningblok heeft Hallo volgens de vereisten:

1. Hallo verklaring knooppunt zelf moet zijn ondertekend
2.  Hallo RSA sha1-algoritme moet als Hallo DigestMethod worden gebruikt. Andere algoritmen digitale handtekening worden niet geaccepteerd.
   `<ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>`
3.  Hallo XML-document kan zich ook aanmelden. 
4.  Hallo transformatie-algoritme moet overeenkomen met de Hallo-waarden in Hallo voorbeeld te volgen:`<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`
9.  Hallo SignatureMethod algoritme moet overeenkomen met de Hallo voorbeeld te volgen:`<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`

## <a name="supported-bindings"></a>Ondersteunde bindingen
Bindingen zijn Hallo transport communicatieparameters die vereist zijn gerelateerd. Hallo volgens de vereisten van toepassing toohello bindingen

1. HTTPS is vereist Hallo transport.
2.  Azure AD is HTTP POST-token te verzenden tijdens de aanmelding vereist
3.  Azure AD gebruikt HTTP POST voor Hallo verificatie aanvraag toohello id-provider en -OMLEIDING voor Hallo afmelden bericht toohello id-provider.

## <a name="required-attributes"></a>Vereiste kenmerken
Deze tabel bevat de vereisten voor specifieke kenmerken in het SAML 2.0 Hallo-bericht.
 
|Kenmerk|Beschrijving|
| ----- | ----- |
|NameID|Hallo-waarde van deze verklaring moet Hallo hetzelfde als van hello Azure AD-gebruiker onveranderbare id genoemd. Het kan zijn van too64 alfanumerieke tekens. Veilige niet HTML-tekens moeten worden gecodeerd, bijvoorbeeld een teken '+' wordt weergegeven als '.2B'.|
|IDPEmail|Hallo UPN (User Principal Name) wordt vermeld in Hallo SAML antwoord als een element met Hallo naam IDPEmail is van de gebruiker Hallo UserPrincipalName (UPN) in Azure AD/Office 365. Hallo UPN is in de e-mailadres. De waarde van de UPN in Windows Office 365 (Azure Active Directory).|
|certificaatverlener|Dit is vereiste toobe een URI van de identiteitsprovider Hallo. U moet niet opnieuw gebruiken Hallo verlener van hello voorbeeld-berichten. Als er meerdere domeinen van het hoogste niveau in uw Azure AD-tenants Hallo verlener moet overeenkomen met opgegeven Hallo URI-instelling die per domein geconfigureerd.|

>[!IMPORTANT]
>Azure AD momenteel ondersteunt Hallo NameID indeling URI hierna om SAML 2.0:urn:oasis:names:tc:SAML:2.0:nameid-indeling: permanente.

## <a name="sample-saml-request-and-response-messages"></a>Voorbeeld SAML-aanvraag en antwoord-berichten
Een combinatie van de bericht-aanvraag en antwoord wordt voor Hallo aanmelding bericht exchange weergegeven.
Dit is een voorbeeld-aanvraagbericht dat is verzonden vanaf de Azure AD tooa voorbeeld SAML 2.0 id-provider. Hallo voorbeeld SAML 2.0-id-provider is dat Active Directory Federation Services (AD FS) geconfigureerd toouse SAML-P-protocol. Interoperabiliteit testen is ook voltooid met een andere id-providers van SAML 2.0.

    `<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_7171b0b2-19f2-4ba2-8f94-24b5e56b7f1e" IssueInstant="2014-01-30T16:18:35Z" Version="2.0" AssertionConsumerServiceIndex="0" >
    <saml:Issuer>urn:federation:MicrosoftOnline</saml:Issuer>
    <samlp:NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
    </samlp:AuthnRequest>`

Dit is een voorbeeld van een antwoordbericht dat wordt verzonden door Hallo voorbeeld SAML 2.0 compatibele id-provider tooAzure AD / Office 365.

    `<samlp:Response ID="_592c022f-e85e-4d23-b55b-9141c95cd2a5" Version="2.0" IssueInstant="2014-01-31T15:36:31.357Z" Destination="https://login.microsoftonline.com/login.srf" Consent="urn:oasis:names:tc:SAML:2.0:consent:unspecified" InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
    </samlp:Status>
    <Assertion ID="_7e3c1bcd-f180-4f78-83e1-7680920793aa" IssueInstant="2014-01-31T15:36:31.279Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
        <ds:Reference URI="#_7e3c1bcd-f180-4f78-83e1-7680920793aa">
          <ds:Transforms>
            <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
            <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
          </ds:Transforms>
          <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
          <ds:DigestValue>CBn/5YqbheaJP425c0pHva9PhNY=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
      <ds:SignatureValue>TciWMyHW2ZODrh/2xrvp5ggmcHBFEd9vrp6DYXp+hZWJzmXMmzwmwS8KNRJKy8H7XqBsdELA1Msqi8I3TmWdnoIRfM/ZAyUppo8suMu6Zw+boE32hoQRnX9EWN/f0vH6zA/YKTzrjca6JQ8gAV1ErwvRWDpyMcwdYCiWALv9ScbkAcebOE1s1JctZ5RBXggdZWrYi72X+I4i6WgyZcIGai/rZ4v2otoWAEHS0y1yh1qT7NDPpl/McDaTGkNU6C+8VfjD78DrUXEcAfKvPgKlKrOMZnD1lCGsViimGY+LSuIdY45MLmyaa5UT4KWph6dA==</ds:SignatureValue>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <ds:X509Data>
          <ds:X509Certificate>MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyhBREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDTE1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9ybWVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/+3ZWxd9T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEMb2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvyJOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBySx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==</ds:X509Certificate>
        </ds:X509Data>
      </KeyInfo>
    </ds:Signature>
    <Subject>
      <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">ABCDEG1234567890</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" NotOnOrAfter="2014-01-31T15:41:31.357Z" Recipient="https://login.microsoftonline.com/login.srf" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2014-01-31T15:36:31.263Z" NotOnOrAfter="2014-01-31T16:36:31.263Z">
      <AudienceRestriction>
        <Audience>urn:federation:MicrosoftOnline</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="IDPEmail">
        <AttributeValue>administrator@contoso.com</AttributeValue>
      </Attribute>
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2014-01-31T15:36:30.200Z" SessionIndex="_7e3c1bcd-f180-4f78-83e1-7680920793aa">
      <AuthnContext>
        <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
    </Assertion>
    </samlp:Response>`

## <a name="configure-your-saml-20-compliant-identity-provider"></a>SAML 2.0 compatibele id-provider configureren
Dit onderwerp bevat richtlijnen over hoe tooconfigure uw toofederate SAML 2.0-id-provider met Azure AD tooenable één aanmelding toegang tooone of meer Microsoft cloud-services (zoals Office 365) met behulp van Hallo SAML 2.0-protocol. Hallo is SAML 2.0 relying party voor een Microsoft-cloudservice in dit scenario gebruikt Azure AD.

## <a name="add-azure-ad-metadata"></a>Azure AD-metagegevens toevoegen
Id-provider SAML 2.0 moet tooadhere tooinformation over de relying party hello Azure AD. Azure AD publiceert metagegevens op https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml.

Het is raadzaam om metagegevens van de meest recente Azure AD Hallo altijd te importeren bij het configureren van SAML 2.0 id-provider. Houd er rekening mee dat Azure AD niet metagegevens uit het Hallo-id-provider gelezen.

## <a name="add-azure-ad-as-a-relying-party"></a>Azure AD als een relying party toevoegen
U hebt tooenable communicatie tussen uw identiteitsprovider die SAML 2.0 en Azure AD. Deze configuratie zijn afhankelijk van uw specifieke id-provider en raadpleegt u toodocumentation voor. Stelt u doorgaans Hallo relying party-ID toohello zelfde als id van de entiteit Hallo van hello Azure AD-metagegevens.

>[!NOTE]
>Controleer of Hallo klok op de server SAML 2.0 provider gesynchroniseerde tooan nauwkeurige bron. Een onjuiste kloktijd kan leiden tot federatieve aanmeldingen toofail.

## <a name="install-windows-powershell-for-sign-on-with-saml-20-identity-provider"></a>Installeer Windows PowerShell voor aanmelding met SAML 2.0-id-provider
Nadat u hebt uw SAML 2.0-id-provider voor gebruik met aanmelding van Azure AD geconfigureerd, is de volgende stap Hallo toodownload en installatie hello Azure Active Directory-Module voor Windows PowerShell. Eenmaal geïnstalleerd, gebruikt u deze cmdlets tooconfigure uw Azure AD-domeinen als federatieve domeinen.

Hello Azure Active Directory-Module voor Windows PowerShell is een download voor het beheren van gegevens van uw organisatie in Azure AD. Deze module installeert een set cmdlets tooWindows PowerShell; u voert deze cmdlets tooset van eenmalige aanmelding toegang tooAzure AD en op zijn beurt tooall Hallo cloudservices u bent geabonneerd. Zie voor instructies over hoe toodownload en installeer cmdlets Hallo [http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)

## <a name="set-up-a-trust-between-your-saml-identity-provider-and-azure-ad"></a>Stel een vertrouwensrelatie tussen de SAML-identiteitsprovider en Azure AD
Voordat u federation configureert op een Azure AD-domein, moet een aangepast domein geconfigureerd hebben. Hallo standaarddomein dat wordt geleverd door Microsoft, kunnen niet worden gefedereerd. Hallo standaarddomein van Microsoft eindigt op "onmicrosoft.com".
U wordt een reeks cmdlets worden uitgevoerd in Hallo Windows PowerShell-opdrachtregelinterface tooadd of domeinen voor eenmalige aanmelding te converteren.

Elk Azure Active Directory-domein dat u wilt met behulp van de identiteitsprovider SAML 2.0 toofederate moet een van de worden toegevoegd als een enkel domein voor eenmalige aanmelding of geconverteerde toobe één domein aanmelding van een standaard domein. Het toevoegen of omzetten van een domein stelt een vertrouwensrelatie tussen uw identiteitsprovider die SAML 2.0 en Azure AD.

Hallo begeleidt volgende procedure u bij het converteren van een bestaand domein standaard tooa federatieve domein met behulp van SAML 2.0 SP-Lite. Houd er rekening mee dat het domein een storing die van invloed is op gebruikers too2 uur nadat u deze stap kan optreden.

## <a name="configuring-a-domain-in-your-azure-ad-directory-for-federation"></a>Configureren van een domein in uw Azure AD-Directory voor Federatie


1. Verbinding maken met Azure AD-Directory als tenantbeheerder tooyour: verbinding maken met MsolService.
2.  Configureer de gewenste Office 365 toouse domeinfederatie met SAML 2.0:`$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol` 

3.  U kunt ondertekenen certificaat base64-gecodeerde tekenreeks uit het bestand van de metagegevens IDP Hallo verkrijgen. Een voorbeeld van deze locatie is opgegeven, maar kan verschillen enigszins verschillen op basis van uw implementatie.

    `<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"> <KeyDescriptor use="signing"> <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#"> <X509Data> <X509Certificate>MIIC5jCCAc6gAwIBAgIQLnaxUPzay6ZJsC8HVv/QfTANBgkqhkiG9w0BAQsFADAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwHhcNMTMxMTA0MTgxMzMyWhcNMTQxMTA0MTgxMzMyWjAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCwMdVLTr5YTSRp+ccbSpuuFeXMfABD9mVCi2wtkRwC30TIyPdORz642MkurdxdPCWjwgJ0HW6TvXwcO9afH3OC5V//wEGDoNcI8PV4enCzTYFe/h//w51uqyv48Fbb3lEXs+aVl8155OAj2sO9IX64OJWKey82GQWK3g7LfhWWpp17j5bKpSd9DBH5pvrV+Q1ESU3mx71TEOvikHGCZYitEPywNeVMLRKrevdWI3FAhFjcCSO6nWDiMqCqiTDYOURXIcHVYTSof1YotkJ4tG6mP5Kpjzd4VQvnR7Pjb47nhIYG6iZ3mR1F85Ns9+hBWukQWNN2hcD/uGdPXhpdMVpBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAK7h7jF7wPzhZ1dPl4e+XMAr8I7TNbhgEU3+oxKyW/IioQbvZVw1mYVCbGq9Rsw4KE06eSMybqHln3w5EeBbLS0MEkApqHY+p68iRpguqa+W7UHKXXQVgPMCpqxMFKonX6VlSQOR64FgpBme2uG+LJ8reTgypEKspQIN0WvtPWmiq4zAwBp08hAacgv868c0MM4WbOYU0rzMIR6Q+ceGVRImlCwZ5b7XKp4mJZ9hlaRjeuyVrDuzBkzROSurX1OXoci08yJvhbtiBJLf3uPOJHrhjKRwIt2TnzS9ElgFZlJiDIA26Athe73n43CT0af2IG6yC7e6sK4L3NEXJrwwUZk=</X509Certificate> </X509Data> </KeyInfo> </KeyDescriptor>` 

Zie voor meer informatie over 'Set MsolDomainAuthentication': [http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx).

>[!NOTE]
>Gebruik moet worden uitgevoerd ' $ecpUrl 'https://WS2012R2-0.contoso.com/PAOS' = ' alleen als u een uitbreiding ECP ingesteld voor de id-provider. Exchange Online-clients, met uitzondering van Outlook Web Application (OWA) zijn afhankelijk van een bericht op basis van actieve eindpunt. Als uw SAML 2.0 STS een actieve eindpunt vergelijkbare-tooShibboleth ECP uitvoering van een actieve eindpunt implementeert is het mogelijk dat het mogelijk dat deze toointeract rich clients Hello Exchange Online-service.

Als federation is geconfigureerd kunt u back te 'niet-gefedereerde' (of 'beheerde'), overschakelen, maar deze wijziging toocomplete van tootwo uren in beslag en nieuwe willekeurige wachtwoorden voor cloud toewijzen op basis van gebruiker aanmelden tooeach is vereist. Schakelen tussen back te 'beheerde' mogelijk vereist zijn in sommige scenario's tooreset een fout in uw instellingen. Zie voor meer informatie over domein-conversie: [http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx).

## <a name="provision-user-principals-tooazure-ad--office-365"></a>Gebruiker principals tooAzure AD inrichten / Office 365
Voordat u uw gebruikers tooOffice 365 kunt verifiëren, moet u Azure AD inrichten met gebruiker principals die overeenkomen met toohello assertion in Hallo SAML 2.0 claim. Als deze gebruiker principals zijn niet van tevoren tooAzure AD bekend kunnen niet vervolgens zij worden gebruikt voor federatieve aanmelding. Azure AD Connect of Windows PowerShell kan gebruikte tooprovision gebruiker principals zijn.

Azure AD Connect kan worden gebruikt tooprovision principals tooyour domeinen in uw Azure AD-Directory Hallo on-premises Active Directory. Voor meer informatie gedetailleerde, Zie [uw on-premises adreslijsten integreren met Azure Active Directory](active-directory-aadconnect.md).

Windows PowerShell kan ook worden de gebruikte tooautomate toevoegen van nieuwe gebruikers tooAzure AD en toosynchronize verandert van Hallo on-premises adreslijst. toouse hello, moet u Hallo downloaden van Windows PowerShell-cmdlets [Azure Active Directory-Modules](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0).

Deze procedure laat zien hoe een enkele gebruiker tooAzure AD tooadd.


1. Verbinding maken met Azure AD-Directory als tenantbeheerder tooyour: verbinding maken met MsolService.
2.  Maak een nieuwe gebruiker-principal:` New-MsolUser
        -UserPrincipalName elwoodf1@contoso.com
        -ImmutableId ABCDEFG1234567890
        -DisplayName "Elwood Folk"
        -FirstName Elwood 
        -LastName Folk 
        -AlternateEmailAddresses "Elwood.Folk@contoso.com" 
        -LicenseAssignment "samlp2test:ENTERPRISEPACK" 
        -UsageLocation "US" ` 

Voor meer informatie over 'New-MsolUser' uitchecken, [http://technet.microsoft.com/library/dn194096.aspx](http://technet.microsoft.com/library/dn194096.aspx)

>[!NOTE]
>Hallo 'UserPrinciplName', waarde moet overeenkomen met de Hallo-waarde die u in uw claim SAML 2.0 en Hallo 'onveranderbare id genoemd"waarde moet overeenkomen met de Hallo verzonden in de verklaring"NameID"voor 'IDPEmail' verzendt.

## <a name="verify-single-sign-on-with-your-saml-20-idp"></a>Controleer of eenmalige aanmelding met uw SAML 2.0 IDP
Als Hallo beheerder voordat u controleren en beheren van eenmalige aanmelding (ook wel identiteitsfederatie genoemd), Hallo informatie bekijken en Hallo stappen uitvoeren in Hallo artikelen tooset van eenmalige aanmelding met SAML 2.0 SP-Lite gebaseerde id-provider te volgen:


1.  U hebt doorgenomen Hallo vereisten voor Azure AD SAML 2.0-Protocol
2.  U hebt geconfigureerd SAML 2.0 id-provider
3.  Windows PowerShell installeren voor eenmalige aanmelding met SAML 2.0-id-provider
4.  Stel een vertrouwensrelatie tussen identiteitsprovider die SAML 2.0 en Azure AD
5.  Een gebruiker principal tooAzure Active Directory (Office 365) van bekende test ingericht via Windows PowerShell of Azure AD Connect.
6.  Configureren met behulp van directory-synchronisatie [Azure AD Connect](active-directory-aadconnect.md).

Na het instellen van eenmalige aanmelding met je SAML 2.0 SP-Lite op basis van identiteit Provider, moet u controleren of deze correct werkt.

>[!NOTE]
>Als u een domein, in plaats van toevoegen van een geconverteerd, kan het too24 uren tooset van eenmalige aanmelding duren.
Voordat u eenmalige aanmelding verifiëren, moet u de installatie van Active Directory-synchronisatie voltooid, Synchroniseer uw mappen en de gesynchroniseerde gebruikers activeren.

### <a name="use-hello-tool-tooverify-that-single-sign-on-has-been-set-up-correctly"></a>Gebruik Hallo hulpprogramma tooverify die eenmalige aanmelding is correct zijn ingesteld
tooverify dat eenmalige aanmelding heeft is ingesteld, kunt u hello te volgen procedure tooconfirm dat u kunt toosign in toohello cloudservice met uw bedrijfsreferenties zijn uitvoeren.

Microsoft heeft gegeven die een hulpprogramma waarmee u tootest uw SAML 2.0 kunt op basis van de identiteitsprovider. Testen voordat u Hallo hulpprogramma, moet u hebben geconfigureerd een toofederate Azure AD-tenant met id-provider.

>[!NOTE]
>Hallo connectiviteit Analyzer vereist Internet Explorer 10 of hoger.



1. Download Hallo connectiviteit Analyzer, [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client).
2.  Klik op Nu installeren toobegin downloaden en installeren van Hallo-hulpprogramma.
3.  Selecteer 'Ik kan geen instellen Federatie met Office 365, Azure of andere services die gebruikmaken van Azure Active Directory'.
4.  Hallo tool wordt gedownload en uitgevoerd, ziet u Hallo connectiviteit Diagnostics-venster. Hallo-hulpprogramma wordt u stapsgewijs uw federation-verbinding testen.
5.  Hallo connectiviteit Analyzer wordt uw IDP SAML 2.0 voor u toologon openen, voert Hallo-referenties in voor het Hallo-UPN die u wilt testen: ![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)
6.  Testen op Hallo Federation aanmelden venster die u moet een accountnaam en wachtwoord invoeren voor hello Azure AD-tenant die is geconfigureerd toobe gefedereerd met SAML 2.0 id-provider. Hallo hulpprogramma probeert toosign in met behulp van deze referenties en gedetailleerde resultaten van tests die worden uitgevoerd tijdens het Hallo aanmeldingspoging wordt geleverd als uitvoer.
![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)
7. Dit venster ziet u een mislukte resultaat van de testen. Klik op gedetailleerde resultaten wordt informatie weergeven over Hallo resultaten voor elke test die werd uitgevoerd, controleren. U kunt ook Hallo resultaten toodisk opslaan in de volgorde tooshare ze.
 
>[!NOTE]
>Hallo connectiviteit analyzer test ook Active Federation met Hallo WS *-protocollen op basis en ECP/PAOS. Als u deze niet gebruikt kunt u de volgende fout Hallo kunt negeren: testen Hallo Active stroom aanmelden met behulp van de identiteitsprovider Active federation-eindpunt.

### <a name="manually-verify-that-single-sign-on-has-been-set-up-correctly"></a>Handmatig te verifiëren dat eenmalige aanmelding is ingesteld correct
Handmatige verificatie biedt extra stappen die u kunt ondernemen tooensure die uw identiteit SAML 2.0 Provider goed in veel scenario's werkt.
tooverify die eenmalige aanmelding heeft correct is ingesteld, voert u Hallo volgende stappen:


1. Aanmelden tooyour cloudservice met dezelfde naam die u voor uw zakelijke referenties gebruikt aanmelden Hallo op een computer lid van een domein.
2.  Klik in het vak Hallo-wachtwoord. Als eenmalige aanmelding is ingesteld, Hallo wachtwoordvak grijs worden weergegeven wordt en ziet u Hallo volgende bericht: "u bent nu vereist toosign in op <your company>."
3.  Klik op Hallo aanmeldt bij <your company> koppeling. Als u kunnen toosign in, is klikt u vervolgens eenmalige aanmelding ingesteld.

## <a name="next-steps"></a>Volgende stappen


- [Active Directory Federation Services-beheer en aanpassingen met Azure AD Connect](active-directory-aadconnect-federation-management.md)
- [Compatibiliteitslijst voor Azure AD-federatie](active-directory-aadconnect-federation-compatibility.md)
- [Azure AD Connect aangepaste installatie](active-directory-aadconnect-get-started-custom.md)
