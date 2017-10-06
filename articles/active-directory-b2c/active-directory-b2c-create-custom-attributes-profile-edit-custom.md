---
title: 'Azure Active Directory B2C: Uw eigen kenmerken toocustom beleid toevoegen en gebruiken in het profiel bewerken | Microsoft Docs'
description: Een stapsgewijze uitleg over het gebruik van extensie-eigenschappen, aangepaste kenmerken, en in de gebruikersinterface Hallo
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a>Azure Active Directory B2C: Maken en gebruiken van aangepaste kenmerken in een aangepast profiel beleid bewerken

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

In dit artikel wordt een aangepast kenmerk in uw Azure AD B2C-directory maken en gebruiken dit nieuwe kenmerk als een aangepaste claim in Hallo profiel bewerken gebruiker reis.

## <a name="prerequisites"></a>Vereisten

Volledige Hallo stappen voor het artikel Hallo [aan de slag met beleid voor aangepaste](active-directory-b2c-get-started-custom.md).

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a>Gebruik aangepaste kenmerken toocollect informatie over uw klanten in Azure Active Directory B2C gebruik van aangepast beleid
Uw Azure Active Directory (Azure AD) B2C-directory wordt geleverd met een ingebouwde set kenmerken: naam, achternaam, plaats, postcode, userPrincipalName gezien, enzovoort.  U moet vaak toocreate uw eigen kenmerken.  Bijvoorbeeld:
* Een toepassing klantgerichte moet toopersist een kenmerk zoals 'LoyaltyNumber'.
* Een id-provider heeft een unieke gebruikers-id die moet worden opgeslagen zoals 'uniqueUserGUID'.'
* Een aangepaste gebruiker reis moet toopersist Hallo status van de gebruiker zoals 'migrationStatus'.

Met Azure AD B2C, kunt u Hallo set kenmerken die zijn opgeslagen voor elk gebruikersaccount uitbreiden. U kunt ook lezen en schrijven van deze kenmerken met behulp van Hallo [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).

Extensie-eigenschappen uitbreiden Hallo-schema van Hallo gebruikersobjecten in Hallo directory.  Hallo voorwaarden uitbreidingseigenschap, aangepast kenmerk en aangepaste claim Raadpleeg toohello hetzelfde is in de context van dit artikel en Hallo Hallo naargelang Hallo context (toepassing, object, beleid verschilt).

Extensie-eigenschappen kunnen alleen worden geregistreerd voor een toepassingsobject ondanks dat ze de gegevens voor een gebruiker kunnen bevatten. Hallo-eigenschap is aangesloten toohello toepassing. object voor de toepassing Hello moet verleend schrijftoegang tooregister een eigenschap extension. 100 uitbreidingseigenschappen (voor alle typen en alle toepassingen) kunnen tooany enkel object worden geschreven. Extensie-eigenschappen toohello directory doeltype worden toegevoegd en wordt onmiddellijk beschikbaar in hello Azure AD B2C-directory-tenant.
Als de toepassing hello wordt verwijderd, worden deze eigenschappen uitbreiding samen met gegevens in die voor alle gebruikers worden ook verwijderd. Als een eigenschap extension is verwijderd door de toepassing hello, wordt deze verwijderd op Hallo directory-objecten zijn gericht en Hallo waarden verwijderd.

Eigenschappen van de extensie bestaan alleen in de context van een geregistreerde toepassing hello tenant Hallo. Hallo-object-id van de toepassing moet zijn opgenomen in Hallo TechnicalProfile die worden gebruikt.

>[!NOTE]
>Hello Azure AD B2C-directory bevat meestal een Web-App met de naam `b2c-extensions-app`.  Deze toepassing wordt voornamelijk gebruikt door ingebouwde Hallo b2c-beleid voor de aangepaste claims Hallo gemaakt via hello Azure-portal.  Deze toepassing tooregister-extensies gebruiken voor aangepaste beleidsregels b2c wordt alleen aanbevolen voor gevorderde gebruikers.  Instructies hiervoor vindt u in Hallo sectie van de volgende stappen in dit artikel.


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a>Maken van een nieuwe toepassing toostore Hallo extensie-eigenschappen

1. Open een browsersessie en navigeer van toohello [Azure Portal](https://portal.azure.com) en meld u aan met beheerdersreferenties Hallo B2C-Directory die u wenst dat tooconfigure.
1. Klik op **Azure Active Directory** Hallo linkernavigatievenster menu. Mogelijk moet u deze door te selecteren meer bedient toofind >.
1. Selecteer **App registraties** en klik op **nieuwe toepassing registreren**
1. Bieden Hallo volgende vermeldingen aanbevolen:
  * Geef een naam voor de webtoepassing Hallo: **WebApp-GraphAPI-DirectoryExtensions**
  * Toepassingstype: Web-app/API
  * Eenmalige aanmelding URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions
1. Selecteer ** maken. Met succes is voltooid wordt weergegeven in Hallo **meldingen**
1. Selecteer de webtoepassing Hallo nieuw gemaakt: **WebApp-GraphAPI-DirectoryExtensions**
1. Selecteer instellingen: **machtigingen vereist**
1. Selecteer API **Windows Active Directory**
1. Zet een vinkje in Toepassingsmachtigingen: **lezen en schrijven directorygegevens**, en **opslaan**
1. Kies **machtigingen verlenen** en bevestig **Ja**.
1. Tooyour Klembord kopiëren en opslaan van de volgende id's uit WebApp-GraphAPI-DirectoryExtensions Hallo > Instellingen > Eigenschappen >
*  **Toepassings-ID** . Voorbeeld:`103ee0e6-f92d-4183-b576-8c3739027780`
* **Object-ID**. Voorbeeld:`80d8296a-da0a-49ee-b6ab-fd232aa45201`



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a>Uw aangepaste beleid tooadd hello ApplicationObjectId wijzigen

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
>Hallo <TechnicalProfile Id="AAD-Common"> is waarnaar wordt verwezen tooas 'algemene' omdat de elementen zijn opgenomen in en opnieuw worden gebruikt in alle hello Azure Active Directory TechnicalProfiles met Hallo element:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`

>[!NOTE]
>Wanneer hello TechnicalProfile voor Hallo eerste toohello nieuwe extensie tijdeigenschap schrijft, kunnen een eenmalige fout optreden.  Hallo-extensie de eigenschap wordt gemaakt van Hallo eerste keer dat deze wordt gebruikt.  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a>Met behulp van de nieuwe uitbreidingseigenschap Hallo / aangepast kenmerk in een reis gebruiker


1. Open Hallo Party(RP) Relying-bestand met een beschrijving van uw beleid bewerken traject van de gebruiker.  Als u uit start, wordt aangeraden toodownload uw al geconfigureerde versie van Hallo RP PolicyEdit bestand rechtstreeks vanuit hello Azure B2C aangepast beleid-sectie in hello Azure-portal.  Het XML-bestand ook openen vanuit de opslagmap van uw.
2. Toevoegen van een aangepaste claim `loyaltyId`.  Door op te nemen Hallo aangepaste claim in Hallo `<RelyingParty>` element, het is doorgegeven als een parameter toohello UserJourney TechnicalProfiles en opgenomen in het token voor de toepassing hello Hallo.
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. Een claim definitie toohello-extensiebestand beleid toevoegen `TrustFrameworkExtensions.xml` binnen Hallo `<ClaimsSchema>` element zoals wordt weergegeven.
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. Hallo toevoegen dezelfde definitie toohello Base beleidsbestand claim `TrustFrameworkBase.xml`.  
>Toevoegen van een `ClaimType` definitie in zowel Hallo base en Hallo extensiebestand is normaal gesproken niet nodig, maar omdat Hallo volgende stappen Hallo extension_loyaltyId tooTechnicalProfiles in Base Hallo-bestand toevoegen wordt, Hallo beleid validator Hallo uploaden weigert van Hallo base-bestand zonder deze.
>Het wellicht handig tootrace Hallo uitvoering van Hallo gebruiker reis met de naam 'ProfileEdit' in hello TrustFrameworkBase.xml-bestand.  Zoeken naar Hallo gebruiker reis Hallo dezelfde naam in uw editor en zien dat Orchestration stap 5 Hallo TechnicalProfileReferenceID roept = 'SelfAsserted ProfileUpdate'.  Zoeken en deze toofamiliarize TechnicalProfile zelf controleren met Hallo-stroom.
5. LoyaltyId toevoegen als de invoer en uitvoer claim in Hallo TechnicalProfile 'SelfAsserted ProfileUpdate'
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. Claim in TechnicalProfile 'AAD-UserWriteProfileUsingObjectId' toopersist Hallo waarde van de claim Hallo in Hallo-extensie de eigenschap voor de huidige gebruiker in de map Hallo Hallo toevoegen.
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. Claim in TechnicalProfile 'AAD-UserReadUsingObjectId' tooread Hallo waarde van het Hallo-extensie-kenmerk toevoegen telkens wanneer een gebruiker zich aanmeldt. Tot nu toe Hallo TechnicalProfiles zijn gewijzigd in de stroom Hallo van alleen lokale accounts.  Als u nieuwe Hallo-kenmerk in Hallo stroom van een account sociale/federatieve, moet een andere set TechnicalProfiles toobe gewijzigd. Zie de volgende stappen.

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
>Hallo IncludeTechnicalProfile element voegt alle Hallo elementen van AAD-gemeenschappelijke toothis TechnicalProfile.

## <a name="test-hello-custom-policy-using-run-now"></a>Hallo aangepast beleid met 'Nu uitvoeren' testen
1. Open Hallo **Azure AD B2C-Blade** en te navigeren**identiteit ervaring Framework > aangepast beleid**.
1. Selecteer Hallo aangepaste beleid dat u hebt geüpload en klikt u op Hallo **nu uitvoeren** knop.
1. U moet kunnen toosign met behulp van een e-mailadres.

Hallo-id-token teruggestuurd tooyour toepassing hello nieuwe extensie eigenschap bevat als een aangepaste claim voorafgegaan door extension_loyaltyId. Zie het voorbeeld.

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Volgende stappen

Hallo nieuwe claim toohello stromen voor sociale account aanmeldingen toevoegen door te wijzigen van Hallo TechnicalProfiles vermeld. Deze twee TechnicalProfiles worden gebruikt door sociale/federatieve account aanmeldingen toowrite en gebruikersgegevens Hallo Hallo alternativeSecurityId zo locator van het gebruikersobject Hallo Hallo met lezen.
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

Met behulp van dezelfde uitbreidingskenmerken tussen ingebouwde en aangepaste beleidsregels Hallo.
Wanneer u uitbreidingskenmerken (aka aangepaste kenmerken) via de portal Hallo-ervaring toevoegt, deze kenmerken worden geregistreerd met Hallo ** b2c-uitbreidingen-app die in elke b2c-tenant voorkomt.  toouse deze extensie kenmerken in het aangepaste beleid:
1. In uw b2c-tenant in portal.azure.com te navigeren**Azure Active Directory** en selecteer **App registraties**
2. Zoek uw **b2c-uitbreidingen-app** en dit selecteren
3. Onder 'Essentials' record Hallo **toepassings-ID** en Hallo **Object-ID**
4. Opnemen in uw AAD-gemeenschappelijke technische profiel metagegevens zoals als volgt:

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

tookeep consistentie met portal Hallo-ervaring, maken deze kenmerken met Hallo portal UI *voordat* u deze gebruiken in uw eigen beleid.  Wanneer u een kenmerk 'ActivationStatus' in hello portal maakt, moet u als volgt tooit verwijzen:

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a>Naslaginformatie

* Een **technische profiel (TP)** is een elementtype dat kan worden beschouwd als een *functie* die definieert de naam van een eindpunt, de metagegevens, het protocol en details Hallo uitwisseling van claims die Hallo identiteit Ervaring Framework moet worden uitgevoerd.  Wanneer dit *functie* wordt aangeroepen in een stap orchestration of vanaf een andere TechnicalProfile, Hallo InputClaims en OutputClaims zijn beschikbaar als parameters door Hallo aanroeper.


* Voor volledige behandeling op extensie-eigenschappen, Zie Hallo artikel [DIRECTORY-SCHEMA-UITBREIDINGEN | GRAPH API-CONCEPTEN](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)

>[!NOTE]
>Extensie kenmerken in Graph API zijn benoemde Hallo conventie `extension_ApplicationObjectID_attributename`. Aangepast beleid verwijzen tooextensions kenmerken als extension_attributename, dus als weggelaten Hallo ApplicationObjectId in Hallo XML
