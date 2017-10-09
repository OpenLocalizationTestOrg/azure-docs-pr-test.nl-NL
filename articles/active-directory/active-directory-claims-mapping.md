---
title: Claims toewijzen in Azure Active Directory (openbare preview) | Microsoft Docs
description: Deze pagina beschrijft Azure Active Directory-claims toewijzen.
services: active-directory
author: billmath
manager: femila
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: ff07b9954d5c2ce71ab0ffd0db49fde15f323586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a>Claims toewijzen in Azure Active Directory (openbare preview)

>[!NOTE]
>Deze functie vervangt en vervangt Hallo [claims aanpassing](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) die worden aangeboden via de portal Hallo vandaag. Als u claims op basis van Hallo portal aanpast bovendien toohello grafiek/PowerShell-methode uiteengezet in dit document op Hallo dezelfde toepassing, tokens die zijn uitgegeven voor die toepassing hello configuratie in Hallo portal wordt genegeerd.
Configuraties die worden aangebracht via Hallo methoden uiteengezet in dit document worden niet doorgevoerd in Hallo-portal.

Deze functie wordt gebruikt door de tenant admins toocustomize Hallo claims verzonden in tokens voor een bepaalde toepassing in de tenant. U kunt beleid voor het toewijzen van claims gebruiken:

- Selecteer welke claims worden opgenomen in de tokens.
- Claimtypen die al bestaan niet maken.
- Kies of wijzig Hallo-bron van gegevens in specifieke claims worden verzonden.

>[!NOTE]
>Deze mogelijkheid is momenteel in de openbare preview. Toorevert worden voorbereid op of verwijder eventuele wijzigingen. Hallo-functie is beschikbaar in een abonnement voor Azure Active Directory (Azure AD) tijdens de openbare preview. Wanneer het Hallo-functie in het algemeen beschikbaar wordt, mogelijk bepaalde aspecten van de functie Hallo echter een Azure Active Directory premium-abonnement nodig.

## <a name="claims-mapping-policy-type"></a>Claims beleidstype toewijzing
In Azure AD een **beleid** object vertegenwoordigt een reeks regels afgedwongen op afzonderlijke toepassingen of op alle toepassingen in een organisatie. Elk type beleid heeft een unieke structuur, met een set eigenschappen die zijn vervolgens toegepast tooobjects toowhich die ze worden toegewezen.

Claims van een toewijzing van beleid is een soort **beleid** -object dat wordt gewijzigd Hallo claims in tokens die zijn uitgegeven voor specifieke toepassingen worden verzonden.

## <a name="claim-sets"></a>Claimsets
Er zijn bepaalde sets van claims die definiëren hoe en wanneer ze worden gebruikt in tokens.

### <a name="core-claim-set"></a>Claim kernset
Claims in Hallo core claimtype set aanwezig zijn in elke token, ongeacht het beleid. Deze claims worden ook beschouwd als beperkt en kunnen niet worden gewijzigd.

### <a name="basic-claim-set"></a>Basic claimset
Hallo basic claimset bevat Hallo claims die worden gegenereerd door de standaardwaarde voor tokens (in aanvulling toohello claim kernset). Deze claims worden weggelaten of gewijzigd via Hallo claims koppelen van beleidsregels.

### <a name="restricted-claim-set"></a>Beperkte claimset
Beperkte claims worden niet gewijzigd met behulp van beleid. Hallo-gegevensbron kan niet worden gewijzigd en er is geen transformatie wordt toegepast als deze claims worden gegenereerd.

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a>Tabel 1: JSON Web Token (JWT) beperkt claimset
|Claimtype (naam)|
| ----- |
|_claim_names|
|_claim_sources|
|access_token|
|Account_type|
|ACR|
|Actor|
|actortoken|
|AIO|
|altsecid|
|AMR|
|app_chain|
|app_displayname|
|app_res|
|appctx|
|appctxsender|
|AppID|
|appidacr|
|Verklaring|
|at_hash|
|AUD|
|auth_data|
|auth_time|
|authorization_code|
|azp|
|azpacr|
|c_hash|
|ca_enf|
|CC|
|cert_token_use|
|client_id|
|cloud_graph_host_name|
|cloud_instance_name|
|CNF|
|code|
|besturingselementen|
|credential_keys|
|aanvraag voor Certificaatondertekening|
|csr_type|
|apparaat-id|
|dns_names|
|domain_dns_name|
|domain_netbios_name|
|e_exp|
|E-mail|
|Eindpunt|
|enfpolids|
|EXP|
|expires_on|
|grant_type|
|Grafiek|
|group_sids|
|groepen|
|hasgroups|
|hash_alg|
|home_oid|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/AuthenticationInstant|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/AuthenticationMethod|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/Expiration|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/EXPIRED|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/EmailAddress|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/name|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/NameIdentifier|
|IAT|
|identityprovider|
|IDP|
|in_corp|
|Exemplaar|
|IpAddr|
|isbrowserhostedapp|
|ISS|
|jwk|
|key_id|
|key_type|
|mam_compliance_url|
|mam_enrollment_url|
|mam_terms_of_use_url|
|mdm_compliance_url|
|mdm_enrollment_url|
|mdm_terms_of_use_url|
|NameID|
|NBF|
|netbios_name|
|nonce|
|OID|
|on_prem_id|
|onprem_sam_account_name|
|onprem_sid|
|openid2_id|
|wachtwoord|
|platf|
|polids|
|pop_jwk|
|preferred_username|
|previous_refresh_token|
|primary_sid|
|PUID|
|pwd_exp|
|pwd_url|
|redirect_uri|
|refresh_token|
|refreshtoken|
|request_nonce|
|Resource|
|Rol|
|rolls|
|Bereik|
|SCP|
|beveiligings-id|
|Handtekening|
|signin_state|
|src1|
|src2|
|Sub|
|tbid|
|tenant_display_name|
|tenant_region_scope|
|thumbnail_photo|
|TID|
|tokenAutologonEnabled|
|trustedfordelegation|
|unique_name|
|UPN|
|user_setting_sync_url|
|gebruikersnaam|
|uti|
|ver|
|verified_primary_email|
|verified_secondary_email|
|wids|
|win_ver|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a>Tabel 2: Security Assertion Markup Language (SAML) beperkt claimset
|Claimtype (URI)|
| ----- |
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/Expiration|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/EXPIRED|
|http://schemas.Microsoft.com/Identity/claims/accesstoken|
|http://schemas.Microsoft.com/Identity/claims/openid2_id|
|http://schemas.Microsoft.com/Identity/claims/identityprovider|
|http://schemas.Microsoft.com/Identity/claims/objectidentifier|
|http://schemas.Microsoft.com/Identity/claims/PUID|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/NameIdentifier [MR1] |
|http://schemas.Microsoft.com/Identity/claims/tenantid|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/AuthenticationInstant|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/AuthenticationMethod|
|http://schemas.Microsoft.com/AccessControlService/2010/07/claims/identityprovider|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/Groups|
|http://schemas.Microsoft.com/claims/groups.Link|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/Role|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/wids|
|http://schemas.Microsoft.com/2014/09/devicecontext/claims/iscompliant|
|http://schemas.Microsoft.com/2014/02/devicecontext/claims/isknown|
|http://schemas.Microsoft.com/2012/01/devicecontext/claims/ismanaged|
|http://schemas.Microsoft.com/2014/03/psso|
|http://schemas.Microsoft.com/claims/authnmethodsreferences|
|http://schemas.xmlsoap.org/ws/2009/09/Identity/claims/actor|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/samlissuername|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/confirmationkey|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowsaccountname|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/primarygroupsid|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/primarysid|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/authorizationdecision|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/Authentication|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/SID|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/denyonlyprimarygroupsid|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/denyonlyprimarysid|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/denyonlysid|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/denyonlywindowsdevicegroup|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowsdeviceclaim|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowsdevicegroup|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowsfqbnversion|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowssubauthority|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/windowsuserclaim|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/x500distinguishedname|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/UPN|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/GroupSID|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/SPN|
|http://schemas.Microsoft.com/ws/2008/06/Identity/claims/ispersistent|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/claims/privatepersonalidentifier|
|http://schemas.Microsoft.com/Identity/claims/scope|

## <a name="claims-mapping-policy-properties"></a>Claims toewijzing van eigenschappen van beleid
Hallo-eigenschappen van een toewijzing van beleid toocontrol welke claims worden verzonden en waar Hallo gegevens afkomstig is uit de claimprovider gebruiken. Als er geen beleid is ingesteld, Hallo systeem geeft tokens met Hallo claim kernset Hallo basic claim set en optionele claims die toepassing hello tooreceive heeft gekozen.

### <a name="include-basic-claim-set"></a>Basic claimset opnemen

**Tekenreeks:** IncludeBasicClaimSet

**Gegevenstype:** Booleaans (True of False)

**Overzicht:** deze eigenschap bepaalt of Hallo basic claimset is opgenomen in de tokens die worden beïnvloed door dit beleid. 

- Als de set tooTrue, alle claims in Hallo basic claimset in Hallo beleid van invloed op tokens worden gegenereerd. 
- Als er geen set tooFalse, claims in Hallo basic claimset zijn Hallo-tokens, tenzij ze zijn afzonderlijk toegevoegd in Hallo claims schema-eigenschap van Hallo dezelfde beleid.

>[!NOTE] 
>Claims in Hallo core claimtype set aanwezig zijn in elke token, ongeacht wat deze eigenschap is ingesteld op. 

### <a name="claims-schema"></a>Claims schema

**Tekenreeks:** ClaimsSchema

**Gegevenstype:** JSON-blob met een of meer claim schema vermeldingen

**Overzicht:** deze eigenschap wordt gedefinieerd welke claims aanwezig zijn in Hallo beleid van invloed op Hallo-tokens, Daarnaast toohello basic als de Hallo core claim set.
Bepaalde informatie is vereist voor elke claim schema vermelding gedefinieerd voor deze eigenschap. U moet opgeven waar Hallo gegevens vandaan (**waarde** of **paar van de bron-ID**), en die Hallo claimgegevens wordt verzonden als (**Type Claim**).

### <a name="claim-schema-entry-elements"></a>Claim-vermelding schema-elementen

**Waarde:** Hallo waarde element definieert een statische waarde als Hallo gegevens toobe in Hallo claim verzonden.

**De combinatie van de bron-ID:** Hallo bron en ID-elementen definiëren waar Hallo-gegevens in Hallo claim afkomstig is uit. 

Hallo bronelement moet worden ingesteld als tooone van Hallo volgende: 


- 'gebruiker': Hallo-gegevens in Hallo claim is een eigenschap van het gebruikersobject Hallo. 
- 'application': Hallo-gegevens in Hallo claim is een eigenschap op Hallo toepassing (client) service-principal. 
- 'resource': Hallo-gegevens in Hallo claim is een eigenschap op Hallo resource service-principal.
- 'doelgroep': Hallo-gegevens in Hallo claim is een eigenschap op Hallo service-principal die is Hallo doelgroep van Hallo-token (ofwel Hallo client- of service-principal).
- 'bedrijf': Hallo-gegevens in Hallo claim is een eigenschap op Hallo resource tenant bedrijfs-object.
- 'transformatie': Hallo-gegevens in Hallo claim afkomstig is van claimtransformatie (Zie de sectie 'claimtransformatie' hello verderop in dit artikel). 

Als Hallo bron transformatie, Hallo **TransformationID** element moet worden opgenomen in deze claimdefinitie.

Hallo-ID-element identificeert waarvan de eigenschap op Hallo-bron biedt Hallo-waarde voor Hallo claim. Hallo bevat volgende tabel Hallo waarden geldig zijn voor elke waarde van de bron-id.

#### <a name="table-3-valid-id-values-per-source"></a>Tabel 3: Geldige id-waarden per bron
|Bron|Id|Beschrijving|
|-----|-----|-----|
|Gebruiker|Achternaam|Familienaam|
|Gebruiker|Voornaam|Voornaam|
|Gebruiker|weergavenaam|Weergavenaam|
|Gebruiker|object-id|Object-id|
|Gebruiker|E-mail|E-mailadres|
|Gebruiker|userPrincipalName|Principalnaam van gebruiker|
|Gebruiker|Afdeling|Afdeling|
|Gebruiker|onpremisessamaccountname|Op de lokale Sam-accountnaam|
|Gebruiker|NetBIOS-naam|NetBios-naam|
|Gebruiker|DNS-domeinnaam|DNS-domeinnaam|
|Gebruiker|onpremisesecurityidentifier|on-premises beveiligings-id|
|Gebruiker|bedrijfsnaam|Naam van organisatie|
|Gebruiker|streetAddress|Straat|
|Gebruiker|Postcode|Postcode|
|Gebruiker|preferredlanguange|Voorkeurstaal|
|Gebruiker|onpremisesuserprincipalname|lokale UPN|
|Gebruiker|mailnickname|E-mail bijnaam|
|Gebruiker|extensionattribute1|Kenmerk toestelnummer 1|
|Gebruiker|extensionattribute2|Kenmerk toestelnummer 2|
|Gebruiker|extensionattribute3|Kenmerk toestelnummer 3|
|Gebruiker|extensionattribute4|Kenmerk toestelnummer 4|
|Gebruiker|extensionattribute5|Kenmerk toestelnummer 5|
|Gebruiker|extensionattribute6|Kenmerk toestelnummer 6|
|Gebruiker|extensionattribute7|Kenmerk toestelnummer 7|
|Gebruiker|extensionattribute8|Kenmerk toestelnummer 8|
|Gebruiker|extensionattribute9|Kenmerk toestelnummer 9|
|Gebruiker|extensionattribute10|Kenmerk toestelnummer 10|
|Gebruiker|extensionattribute11|Kenmerk toestelnummer 11|
|Gebruiker|extensionattribute12|Kenmerk toestelnummer 12|
|Gebruiker|extensionattribute13|Kenmerk toestelnummer 13|
|Gebruiker|extensionattribute14|Kenmerk toestelnummer 14|
|Gebruiker|extensionattribute15|Kenmerk toestelnummer 15|
|Gebruiker|othermail|Andere Mail|
|Gebruiker|Land|Land|
|Gebruiker|city|Plaats|
|Gebruiker|state|Status|
|Gebruiker|functie|Functie|
|Gebruiker|Werknemer-id|Werknemer-ID|
|Gebruiker|facsimiletelephonenumber|Faxbericht telefoonnummer|
|toepassing, resource, doelgroep|weergavenaam|Weergavenaam|
|toepassing, resource, doelgroep|objecten|Object-id|
|toepassing, resource, doelgroep|tags|Service-Principal label|
|Bedrijf|tenantcountry|Land van tenant|

**TransformationID:** hello TransformationID element moet worden opgegeven als hello bronelement te is ingesteld 'transformatie'.

- Dit element moet overeenkomen met een ID-element Hallo van Hallo transformatie vermelding in Hallo **ClaimsTransformation** eigenschap die definieert hoe Hallo-gegevens voor deze claim wordt gegenereerd.

**Claimtype:** hello **JwtClaimType** en **SamlClaimType** elementen definiëren die claim claim schema post verwijst.

- Hallo JwtClaimType moet Hallo-naam van Hallo claim toobe verzonden in JWTs bevatten.
- Hallo SamlClaimType moet Hallo URI Hallo claim verzonden in SAML-tokens toobe bevatten.

>[!NOTE]
>Namen en URI's van claims in Hallo beperkt claim set kan niet worden gebruikt voor Hallo claim type elementen. Zie Hallo 'Uitzonderingen en beperkingen' sectie verderop in dit artikel voor meer informatie.

### <a name="claims-transformation"></a>Claimtransformatie

**Tekenreeks:** ClaimsTransformation

**Gegevenstype:** JSON-blob met een of meer vermeldingen voor transformatie 

**Overzicht:** gebruiken deze eigenschap tooapply algemene transformaties toosource gegevens, toogenerate Hallo uitvoergegevens voor claims in opgegeven Hallo Claims Schema.

**-ID:** gebruik Hallo ID-element tooreference dit item transformatie in Hallo TransformationID Claims Schema-item. Deze waarde moet uniek zijn voor elk item transformatie binnen dit beleid.

**TransformationMethod:** hello TransformationMethod element identificeert welke bewerking is uitgevoerd toogenerate Hallo gegevens voor Hallo claim.

Op basis van Hallo methode die is gekozen, wordt een reeks invoer en uitvoer verwacht. Deze worden gedefinieerd met behulp van Hallo **InputClaims**, **invoerparameters** en **OutputClaims** elementen.

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a>Tabel 4: Transformatie methoden en verwachte invoer en uitvoer
|TransformationMethod|Verwachte invoer|Verwachte uitvoer|Beschrijving|
|-----|-----|-----|-----|
|Koppelen|tekenreeks1, tekenreeks2, scheidingselement|outputClaim|Joins invoer tekenreeksen met behulp van een scheidingsteken ertussen. Bijvoorbeeld: tekenreeks1: 'foo@bar.com', tekenreeks2: sandbox '-', scheidingsteken: '. ' resulteert in outputClaim: 'foo@bar.com.sandbox'|
|ExtractMailPrefix|E-mail|outputClaim|Extraheert Hallo lokale gedeelte van een e-mailadres. Bijvoorbeeld: e-mail: 'foo@bar.com' resulteert in outputClaim: "foo". Wanneer dit niet het @ is aanmelding aanwezig is, wordt Hallo bestaande invoerreeks geretourneerd als is.|

**InputClaims:** een InputClaims element toopass Hallo gegevens uit een claim schema vermelding tooa transformatie gebruiken. Deze twee kenmerken heeft: **ClaimTypeReferenceId** en **TransformationClaimType**.

- **ClaimTypeReferenceId** wordt samengevoegd met de ID-element van Hallo claim schema vermelding toofind Hallo juiste invoerclaim wordt aangeduid. 
- **TransformationClaimType** gebruikte toogive is een unieke naam toothis-invoer. Deze naam moet overeenkomen met een van de invoerwaarden Hallo verwacht voor Hallo transformatie-methode.

**Invoerparameters:** een invoerparameters element toopass een constante waarde tooa transformatie gebruiken. Deze twee kenmerken heeft: **waarde** en **ID**.

- **Waarde** Hallo werkelijke constante waarde toobe wordt doorgegeven.
- **ID** gebruikte toogive is een unieke naam toothis-invoer. Deze naam moet overeenkomen met een van de invoerwaarden Hallo verwacht voor Hallo transformatie-methode.

**OutputClaims:** een OutputClaims element toohold Hallo gegevens die worden gegenereerd door een transformatie gebruiken en deze tooa claim schema vermelding koppelen. Deze twee kenmerken heeft: **ClaimTypeReferenceId** en **TransformationClaimType**.

- **ClaimTypeReferenceId** met Hallo Hallo claim schema vermelding toofind Hallo juiste uitvoer claim-ID is gekoppeld.
- **TransformationClaimType** gebruikte toogive is een unieke naam toothis uitvoer. Deze naam moet overeenkomen met een van de uitvoer voor transformatiemethode Hallo Hallo verwacht.

### <a name="exceptions-and-restrictions"></a>Uitzonderingen en beperkingen

**SAML NameID en UPN:** Hallo kenmerken van waaruit u Hallo NameID en UPN waarden bron en Hallo claims transformaties die zijn toegestaan, zijn beperkt.

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a>Tabel 5: Kenmerken die zijn toegestaan als een gegevensbron voor SAML-NameID
|Bron|Id|Beschrijving|
|-----|-----|-----|
|Gebruiker|E-mail|E-mailadres|
|Gebruiker|userPrincipalName|Principalnaam van gebruiker|
|Gebruiker|onpremisessamaccountname|Op de lokale Sam-accountnaam|
|Gebruiker|Werknemer-id|Werknemer-ID|
|Gebruiker|extensionattribute1|Kenmerk toestelnummer 1|
|Gebruiker|extensionattribute2|Kenmerk toestelnummer 2|
|Gebruiker|extensionattribute3|Kenmerk toestelnummer 3|
|Gebruiker|extensionattribute4|Kenmerk toestelnummer 4|
|Gebruiker|extensionattribute5|Kenmerk toestelnummer 5|
|Gebruiker|extensionattribute6|Kenmerk toestelnummer 6|
|Gebruiker|extensionattribute7|Kenmerk toestelnummer 7|
|Gebruiker|extensionattribute8|Kenmerk toestelnummer 8|
|Gebruiker|extensionattribute9|Kenmerk toestelnummer 9|
|Gebruiker|extensionattribute10|Kenmerk toestelnummer 10|
|Gebruiker|extensionattribute11|Kenmerk toestelnummer 11|
|Gebruiker|extensionattribute12|Kenmerk toestelnummer 12|
|Gebruiker|extensionattribute13|Kenmerk toestelnummer 13|
|Gebruiker|extensionattribute14|Kenmerk toestelnummer 14|
|Gebruiker|extensionattribute15|Kenmerk toestelnummer 15|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a>Tabel 6: Transformatie methoden zijn toegestaan voor SAML-NameID
|TransformationMethod|Beperkingen|
| ----- | ----- |
|ExtractMailPrefix|Geen|
|Koppelen|Hallo-achtervoegsel wordt toegevoegd, moet een geverifieerde domein voor Hallo resource tenant.|

### <a name="custom-signing-key"></a>Aangepaste ondertekeningssleutel
Een aangepaste handtekeningsleutel moet toohello service principal-object voor een toewijzing van beleid tootake effect claims worden toegewezen. Alle tokens uitgegeven hebben zijn beïnvloed door het Hallo-beleid zijn ondertekend met deze sleutel. Toepassingen moet geconfigureerde tooaccept tokens die zijn ondertekend met deze sleutel. Dit zorgt ervoor dat tokens zijn gewijzigd door de maker van Hallo Hallo bevestiging claims toewijzing van beleid. Deze beschermt toepassingen tegen toewijzing van beleid dat is gemaakt door schadelijke actoren claims.

### <a name="cross-tenant-scenarios"></a>Cross-tenantscenario 's
Claims beleidsregels koppelen tooguest gebruikers niet van toepassing. Als een gastgebruiker tooaccess probeert een toepassing met een van de claimprovider toewijzing beleid dat is toegewezen tooits service-principal, Hallo standaardtoken is uitgegeven (Hallo beleid heeft geen effect).

## <a name="claims-mapping-policy-assignment"></a>Claims beleidstoewijzing toewijzing
Claims toewijzing beleid kan alleen worden toegewezen tooservice SPN-objecten.

### <a name="example-claims-mapping-policies"></a>Voorbeeld van claims toewijzing van beleid

In Azure AD zijn veel scenario's mogelijk als u claims die worden verzonden in tokens voor een specifieke service-principals kunt aanpassen. In deze sectie doorlopen we enkele algemene scenario's kunt u leren hoe toouse Hallo toewijzing beleidstype claims.

#### <a name="prerequisites"></a>Vereisten
In de Hallo volgen voorbeelden, u maken, bijwerken, koppelen en beleidsregels voor service-principals verwijderen. Als u nieuwe tooAzure AD bent, raden wij aan dat u meer informatie over hoe tooget een Azure AD-tenant voordat u doorgaat met deze voorbeelden. 

tooget gestart, Hallo stappen te volgen:


1. Meest recente Hallo downloaden [public preview-versie van Azure AD PowerShell-Module](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).
2.  Hallo Connect opdracht toosign in tooyour Azure AD-admin-account uitgevoerd. Deze opdracht uitvoeren telkens wanneer starten u een nieuwe sessie.
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  toosee alle beleidsregels die zijn gemaakt in uw organisatie, Voer Hallo na de opdracht. Het is raadzaam dat u deze opdracht nadat de meeste bewerkingen in Hallo uitvoeren volgende scenario's, toocheck die uw beleid worden gemaakt als verwacht.
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a>Voorbeeld: Maken en toewijzen van een beleid tooomit Hallo basic claims van uitgegeven tokens tooa service-principal.
In dit voorbeeld maakt u een beleid dat Hallo basic claimset uit uitgegeven tokens toolinked verwijdert service-principals.


1. Maak een van de claimprovider toewijzing van beleid. Dit beleid, gekoppelde toospecific service-principals, verwijdert Hallo basic claimset van tokens.
    1. toocreate hello beleid, voer deze opdracht uit: 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. toosee uw nieuw beleid en tooget Hallo beleid ObjectId, Voer Hallo volgende opdracht:
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Hallo beleid tooyour service-principal toewijzen. U moet ook tooget Hallo ObjectId van uw service-principal. 
    1.  toosee service-principals van uw organisatie, kunt u Microsoft Graph query. Of aanmelden in Azure AD Graph Explorer tooyour Azure AD-account.
    2.  Wanneer u hebt Hallo ObjectId van uw service-principal, voert Hallo zijn na de opdracht:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a>Voorbeeld: Maken en toewijzen van een beleid tooinclude Hallo werknemer-id en TenantCountry als tooa service-principal die claims in tokens worden uitgegeven.
In dit voorbeeld maakt u een beleid dat wordt toegevoegd Hallo werknemer-id en TenantCountry tootokens uitgegeven toolinked service-principals. Hallo werknemer-id wordt verzonden als Hallo naam claimtype in SAML-tokens en JWTs. Hallo TenantCountry wordt verzonden als Hallo land claimtype in SAML-tokens en JWTs. In dit voorbeeld gaan we tooinclude Hallo basic claims ingesteld in het Hallo-tokens.

1. Maak een van de claimprovider toewijzing van beleid. Dit beleid, gekoppelde toospecific service-principals, wordt Hallo werknemer-id en TenantCountry claims tootokens toegevoegd.
    1. toocreate hello beleid, voer deze opdracht uit:  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee uw nieuw beleid en tooget Hallo beleid ObjectId, Voer Hallo volgende opdracht:
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  Hallo beleid tooyour service-principal toewijzen. U moet ook tooget Hallo ObjectId van uw service-principal. 
    1.  toosee service-principals van uw organisatie, kunt u Microsoft Graph query. Of aanmelden in Azure AD Graph Explorer tooyour Azure AD-account.
    2.  Wanneer u hebt Hallo ObjectId van uw service-principal, voert Hallo zijn na de opdracht:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a>Voorbeeld: Maken en toewijzen van een beleid dat gebruikmaakt van een claimtransformatie in uitgegeven tokens tooa service-principal.
In dit voorbeeld maakt u een beleid dat u een aangepaste claim 'JoinedData' tooJWTs uitgegeven toolinked service-principals verzendt. Deze claim bevat een waarde die is gemaakt door Hallo-gegevens die zijn opgeslagen in Hallo extensionattribute1 kenmerk van het gebruikersobject Hallo met '.sandbox'. In dit voorbeeld uitsluiten we Hallo basic claims ingesteld in het Hallo-tokens.


1. Maak een van de claimprovider toewijzing van beleid. Dit beleid, gekoppelde toospecific service-principals, wordt Hallo werknemer-id en TenantCountry claims tootokens toegevoegd.
    1. toocreate hello beleid, voer deze opdracht uit: 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee uw nieuw beleid en tooget Hallo beleid ObjectId, Voer Hallo volgende opdracht: 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Hallo beleid tooyour service-principal toewijzen. U moet ook tooget Hallo ObjectId van uw service-principal. 
    1.  toosee service-principals van uw organisatie, kunt u Microsoft Graph query. Of aanmelden in Azure AD Graph Explorer tooyour Azure AD-account.
    2.  Wanneer u hebt Hallo ObjectId van uw service-principal, voert Hallo zijn na de opdracht: 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
