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
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="c288c-103">Azure Active Directory B2C: Maken en gebruiken van aangepaste kenmerken in een aangepast profiel beleid bewerken</span><span class="sxs-lookup"><span data-stu-id="c288c-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="c288c-104">In dit artikel wordt een aangepast kenmerk in uw Azure AD B2C-directory maken en gebruiken dit nieuwe kenmerk als een aangepaste claim in Hallo profiel bewerken gebruiker reis.</span><span class="sxs-lookup"><span data-stu-id="c288c-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in hello profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c288c-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c288c-105">Prerequisites</span></span>

<span data-ttu-id="c288c-106">Volledige Hallo stappen voor het artikel Hallo [aan de slag met beleid voor aangepaste](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c288c-106">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="c288c-107">Gebruik aangepaste kenmerken toocollect informatie over uw klanten in Azure Active Directory B2C gebruik van aangepast beleid</span><span class="sxs-lookup"><span data-stu-id="c288c-107">Use custom attributes toocollect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="c288c-108">Uw Azure Active Directory (Azure AD) B2C-directory wordt geleverd met een ingebouwde set kenmerken: naam, achternaam, plaats, postcode, userPrincipalName gezien, enzovoort.  U moet vaak toocreate uw eigen kenmerken.</span><span class="sxs-lookup"><span data-stu-id="c288c-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need toocreate your own attributes.</span></span>  <span data-ttu-id="c288c-109">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c288c-109">For example:</span></span>
* <span data-ttu-id="c288c-110">Een toepassing klantgerichte moet toopersist een kenmerk zoals 'LoyaltyNumber'.</span><span class="sxs-lookup"><span data-stu-id="c288c-110">A customer-facing application needs toopersist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="c288c-111">Een id-provider heeft een unieke gebruikers-id die moet worden opgeslagen zoals 'uniqueUserGUID'.'</span><span class="sxs-lookup"><span data-stu-id="c288c-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="c288c-112">Een aangepaste gebruiker reis moet toopersist Hallo status van de gebruiker zoals 'migrationStatus'.</span><span class="sxs-lookup"><span data-stu-id="c288c-112">A custom user journey needs toopersist hello state of user such as "migrationStatus."</span></span>

<span data-ttu-id="c288c-113">Met Azure AD B2C, kunt u Hallo set kenmerken die zijn opgeslagen voor elk gebruikersaccount uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="c288c-113">With Azure AD B2C, you can extend hello set of attributes stored on each user account.</span></span> <span data-ttu-id="c288c-114">U kunt ook lezen en schrijven van deze kenmerken met behulp van Hallo [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c288c-114">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="c288c-115">Extensie-eigenschappen uitbreiden Hallo-schema van Hallo gebruikersobjecten in Hallo directory.</span><span class="sxs-lookup"><span data-stu-id="c288c-115">Extension properties extend hello schema of hello user objects in hello directory.</span></span>  <span data-ttu-id="c288c-116">Hallo voorwaarden uitbreidingseigenschap, aangepast kenmerk en aangepaste claim Raadpleeg toohello hetzelfde is in de context van dit artikel en Hallo Hallo naargelang Hallo context (toepassing, object, beleid verschilt).</span><span class="sxs-lookup"><span data-stu-id="c288c-116">hello terms extension property, custom attribute and custom claim refer toohello same thing in hello context of this article and hello name varies depending on hello context (application, object, policy).</span></span>

<span data-ttu-id="c288c-117">Extensie-eigenschappen kunnen alleen worden geregistreerd voor een toepassingsobject ondanks dat ze de gegevens voor een gebruiker kunnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="c288c-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="c288c-118">Hallo-eigenschap is aangesloten toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="c288c-118">hello property is attached toohello application.</span></span> <span data-ttu-id="c288c-119">object voor de toepassing Hello moet verleend schrijftoegang tooregister een eigenschap extension.</span><span class="sxs-lookup"><span data-stu-id="c288c-119">hello Application object must be granted write access tooregister an extension property.</span></span> <span data-ttu-id="c288c-120">100 uitbreidingseigenschappen (voor alle typen en alle toepassingen) kunnen tooany enkel object worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="c288c-120">100 Extension properties (across ALL types and ALL applications) can be written tooany single object.</span></span> <span data-ttu-id="c288c-121">Extensie-eigenschappen toohello directory doeltype worden toegevoegd en wordt onmiddellijk beschikbaar in hello Azure AD B2C-directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="c288c-121">Extension properties are added toohello target directory type and becomes immediately accessible in hello Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="c288c-122">Als de toepassing hello wordt verwijderd, worden deze eigenschappen uitbreiding samen met gegevens in die voor alle gebruikers worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c288c-122">If hello application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="c288c-123">Als een eigenschap extension is verwijderd door de toepassing hello, wordt deze verwijderd op Hallo directory-objecten zijn gericht en Hallo waarden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c288c-123">If an extension property is deleted by hello Application, it is removed on hello target directory objects, and hello values deleted.</span></span>

<span data-ttu-id="c288c-124">Eigenschappen van de extensie bestaan alleen in de context van een geregistreerde toepassing hello tenant Hallo.</span><span class="sxs-lookup"><span data-stu-id="c288c-124">Extension properties exist only in hello context of a registered  Application in hello tenant.</span></span> <span data-ttu-id="c288c-125">Hallo-object-id van de toepassing moet zijn opgenomen in Hallo TechnicalProfile die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c288c-125">hello object id of that Application must be included in hello TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="c288c-126">Hello Azure AD B2C-directory bevat meestal een Web-App met de naam `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="c288c-126">hello Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="c288c-127">Deze toepassing wordt voornamelijk gebruikt door ingebouwde Hallo b2c-beleid voor de aangepaste claims Hallo gemaakt via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c288c-127">This application is primarily used by hello b2c built-in  policies for hello custom claims created via hello Azure portal.</span></span>  <span data-ttu-id="c288c-128">Deze toepassing tooregister-extensies gebruiken voor aangepaste beleidsregels b2c wordt alleen aanbevolen voor gevorderde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c288c-128">Using this application tooregister extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="c288c-129">Instructies hiervoor vindt u in Hallo sectie van de volgende stappen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c288c-129">Instructions for this are included in hello Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a><span data-ttu-id="c288c-130">Maken van een nieuwe toepassing toostore Hallo extensie-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="c288c-130">Creating a new application toostore hello extension properties</span></span>

1. <span data-ttu-id="c288c-131">Open een browsersessie en navigeer van toohello [Azure Portal](https://portal.azure.com) en meld u aan met beheerdersreferenties Hallo B2C-Directory die u wenst dat tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c288c-131">Open a browsing session and navigate toohello [Azure porta](https://portal.azure.com) and sign in with administrative credentials of hello B2C Directory you wish tooconfigure.</span></span>
1. <span data-ttu-id="c288c-132">Klik op **Azure Active Directory** Hallo linkernavigatievenster menu.</span><span class="sxs-lookup"><span data-stu-id="c288c-132">Click **Azure Active Directory** on hello left navigation menu.</span></span> <span data-ttu-id="c288c-133">Mogelijk moet u deze door te selecteren meer bedient toofind >.</span><span class="sxs-lookup"><span data-stu-id="c288c-133">You may need toofind it by selecting More services>.</span></span>
1. <span data-ttu-id="c288c-134">Selecteer **App registraties** en klik op **nieuwe toepassing registreren**</span><span class="sxs-lookup"><span data-stu-id="c288c-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="c288c-135">Bieden Hallo volgende vermeldingen aanbevolen:</span><span class="sxs-lookup"><span data-stu-id="c288c-135">Provide hello following recommended entries:</span></span>
  * <span data-ttu-id="c288c-136">Geef een naam voor de webtoepassing Hallo: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="c288c-136">Specify a name for hello web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="c288c-137">Toepassingstype: Web-app/API</span><span class="sxs-lookup"><span data-stu-id="c288c-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="c288c-138">Eenmalige aanmelding URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="c288c-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="c288c-139">Selecteer ** maken.</span><span class="sxs-lookup"><span data-stu-id="c288c-139">Select **Create.</span></span> <span data-ttu-id="c288c-140">Met succes is voltooid wordt weergegeven in Hallo **meldingen**</span><span class="sxs-lookup"><span data-stu-id="c288c-140">Successful completion appears in hello **notifications**</span></span>
1. <span data-ttu-id="c288c-141">Selecteer de webtoepassing Hallo nieuw gemaakt: **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="c288c-141">Select hello newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="c288c-142">Selecteer instellingen: **machtigingen vereist**</span><span class="sxs-lookup"><span data-stu-id="c288c-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="c288c-143">Selecteer API **Windows Active Directory**</span><span class="sxs-lookup"><span data-stu-id="c288c-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="c288c-144">Zet een vinkje in Toepassingsmachtigingen: **lezen en schrijven directorygegevens**, en **opslaan**</span><span class="sxs-lookup"><span data-stu-id="c288c-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="c288c-145">Kies **machtigingen verlenen** en bevestig **Ja**.</span><span class="sxs-lookup"><span data-stu-id="c288c-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="c288c-146">Tooyour Klembord kopiëren en opslaan van de volgende id's uit WebApp-GraphAPI-DirectoryExtensions Hallo > Instellingen > Eigenschappen ></span><span class="sxs-lookup"><span data-stu-id="c288c-146">Copy tooyour clipboard and save hello following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="c288c-147">**Toepassings-ID** .</span><span class="sxs-lookup"><span data-stu-id="c288c-147">**Application ID** .</span></span> <span data-ttu-id="c288c-148">Voorbeeld:`103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="c288c-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="c288c-149">**Object-ID**.</span><span class="sxs-lookup"><span data-stu-id="c288c-149">**Object ID**.</span></span> <span data-ttu-id="c288c-150">Voorbeeld:`80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="c288c-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a><span data-ttu-id="c288c-151">Uw aangepaste beleid tooadd hello ApplicationObjectId wijzigen</span><span class="sxs-lookup"><span data-stu-id="c288c-151">Modifying your custom policy tooadd hello ApplicationObjectId</span></span>

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
><span data-ttu-id="c288c-152">Hallo <TechnicalProfile Id="AAD-Common"> is waarnaar wordt verwezen tooas 'algemene' omdat de elementen zijn opgenomen in en opnieuw worden gebruikt in alle hello Azure Active Directory TechnicalProfiles met Hallo element:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="c288c-152">hello <TechnicalProfile Id="AAD-Common"> is referred tooas "common" because its elements are included in and reused in all hello Azure Active Directory TechnicalProfiles by using hello element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="c288c-153">Wanneer hello TechnicalProfile voor Hallo eerste toohello nieuwe extensie tijdeigenschap schrijft, kunnen een eenmalige fout optreden.</span><span class="sxs-lookup"><span data-stu-id="c288c-153">When hello TechnicalProfile writes for hello first time toohello newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="c288c-154">Hallo-extensie de eigenschap wordt gemaakt van Hallo eerste keer dat deze wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c288c-154">hello extension property is created hello first time it is used.</span></span>  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="c288c-155">Met behulp van de nieuwe uitbreidingseigenschap Hallo / aangepast kenmerk in een reis gebruiker</span><span class="sxs-lookup"><span data-stu-id="c288c-155">Using hello new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="c288c-156">Open Hallo Party(RP) Relying-bestand met een beschrijving van uw beleid bewerken traject van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c288c-156">Open hello Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="c288c-157">Als u uit start, wordt aangeraden toodownload uw al geconfigureerde versie van Hallo RP PolicyEdit bestand rechtstreeks vanuit hello Azure B2C aangepast beleid-sectie in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c288c-157">If you are starting out, it may be advisable toodownload your already configured version of hello RP-PolicyEdit file directly from hello Azure B2C Custom Policy section in hello Azure portal.</span></span>  <span data-ttu-id="c288c-158">Het XML-bestand ook openen vanuit de opslagmap van uw.</span><span class="sxs-lookup"><span data-stu-id="c288c-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="c288c-159">Toevoegen van een aangepaste claim `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="c288c-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="c288c-160">Door op te nemen Hallo aangepaste claim in Hallo `<RelyingParty>` element, het is doorgegeven als een parameter toohello UserJourney TechnicalProfiles en opgenomen in het token voor de toepassing hello Hallo.</span><span class="sxs-lookup"><span data-stu-id="c288c-160">By including hello custom claim in hello `<RelyingParty>` element, it is passed as a parameter toohello UserJourney TechnicalProfiles and included in hello token for hello application.</span></span>
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
3. <span data-ttu-id="c288c-161">Een claim definitie toohello-extensiebestand beleid toevoegen `TrustFrameworkExtensions.xml` binnen Hallo `<ClaimsSchema>` element zoals wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c288c-161">Add a claim definition toohello Extension policy file  `TrustFrameworkExtensions.xml` inside hello `<ClaimsSchema>` element as shown.</span></span>
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
4. <span data-ttu-id="c288c-162">Hallo toevoegen dezelfde definitie toohello Base beleidsbestand claim `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="c288c-162">Add hello same claim definition toohello Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="c288c-163">Toevoegen van een `ClaimType` definitie in zowel Hallo base en Hallo extensiebestand is normaal gesproken niet nodig, maar omdat Hallo volgende stappen Hallo extension_loyaltyId tooTechnicalProfiles in Base Hallo-bestand toevoegen wordt, Hallo beleid validator Hallo uploaden weigert van Hallo base-bestand zonder deze.</span><span class="sxs-lookup"><span data-stu-id="c288c-163">Adding a `ClaimType` definition in both hello base and hello extensions file is normally not necessary, however since hello next steps will add hello extension_loyaltyId tooTechnicalProfiles in hello Base file, hello policy validator will reject hello upload of hello base file without it.</span></span>
><span data-ttu-id="c288c-164">Het wellicht handig tootrace Hallo uitvoering van Hallo gebruiker reis met de naam 'ProfileEdit' in hello TrustFrameworkBase.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="c288c-164">It may be useful tootrace hello execution of hello user journey named "ProfileEdit" in hello TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="c288c-165">Zoeken naar Hallo gebruiker reis Hallo dezelfde naam in uw editor en zien dat Orchestration stap 5 Hallo TechnicalProfileReferenceID roept = 'SelfAsserted ProfileUpdate'.</span><span class="sxs-lookup"><span data-stu-id="c288c-165">Search for hello user journey of hello same name in your editor and observe that Orchestration Step 5 invokes hello TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="c288c-166">Zoeken en deze toofamiliarize TechnicalProfile zelf controleren met Hallo-stroom.</span><span class="sxs-lookup"><span data-stu-id="c288c-166">Search and inspect this TechnicalProfile toofamiliarize yourself with hello flow.</span></span>
5. <span data-ttu-id="c288c-167">LoyaltyId toevoegen als de invoer en uitvoer claim in Hallo TechnicalProfile 'SelfAsserted ProfileUpdate'</span><span class="sxs-lookup"><span data-stu-id="c288c-167">Add loyaltyId as input and output claim in hello TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
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
6. <span data-ttu-id="c288c-168">Claim in TechnicalProfile 'AAD-UserWriteProfileUsingObjectId' toopersist Hallo waarde van de claim Hallo in Hallo-extensie de eigenschap voor de huidige gebruiker in de map Hallo Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c288c-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello value of hello claim in hello extension property, for hello current user in hello directory.</span></span>
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
7. <span data-ttu-id="c288c-169">Claim in TechnicalProfile 'AAD-UserReadUsingObjectId' tooread Hallo waarde van het Hallo-extensie-kenmerk toevoegen telkens wanneer een gebruiker zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="c288c-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello value of hello extension attribute every time a user logs in.</span></span> <span data-ttu-id="c288c-170">Tot nu toe Hallo TechnicalProfiles zijn gewijzigd in de stroom Hallo van alleen lokale accounts.</span><span class="sxs-lookup"><span data-stu-id="c288c-170">Thus far hello TechnicalProfiles have been changed in hello flow of local accounts only.</span></span>  <span data-ttu-id="c288c-171">Als u nieuwe Hallo-kenmerk in Hallo stroom van een account sociale/federatieve, moet een andere set TechnicalProfiles toobe gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c288c-171">If hello new attribute is desired in hello flow of a social/federated account, a different set of TechnicalProfiles needs toobe changed.</span></span> <span data-ttu-id="c288c-172">Zie de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="c288c-172">See Next Steps.</span></span>

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
><span data-ttu-id="c288c-173">Hallo IncludeTechnicalProfile element voegt alle Hallo elementen van AAD-gemeenschappelijke toothis TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="c288c-173">hello IncludeTechnicalProfile element adds all hello elements of AAD-Common toothis TechnicalProfile.</span></span>

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="c288c-174">Hallo aangepast beleid met 'Nu uitvoeren' testen</span><span class="sxs-lookup"><span data-stu-id="c288c-174">Test hello custom policy using "Run Now"</span></span>
1. <span data-ttu-id="c288c-175">Open Hallo **Azure AD B2C-Blade** en te navigeren**identiteit ervaring Framework > aangepast beleid**.</span><span class="sxs-lookup"><span data-stu-id="c288c-175">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="c288c-176">Selecteer Hallo aangepaste beleid dat u hebt geüpload en klikt u op Hallo **nu uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="c288c-176">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
1. <span data-ttu-id="c288c-177">U moet kunnen toosign met behulp van een e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="c288c-177">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="c288c-178">Hallo-id-token teruggestuurd tooyour toepassing hello nieuwe extensie eigenschap bevat als een aangepaste claim voorafgegaan door extension_loyaltyId.</span><span class="sxs-lookup"><span data-stu-id="c288c-178">hello  id token sent back tooyour application includes hello new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="c288c-179">Zie het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c288c-179">See example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c288c-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c288c-180">Next steps</span></span>

<span data-ttu-id="c288c-181">Hallo nieuwe claim toohello stromen voor sociale account aanmeldingen toevoegen door te wijzigen van Hallo TechnicalProfiles vermeld.</span><span class="sxs-lookup"><span data-stu-id="c288c-181">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed.</span></span> <span data-ttu-id="c288c-182">Deze twee TechnicalProfiles worden gebruikt door sociale/federatieve account aanmeldingen toowrite en gebruikersgegevens Hallo Hallo alternativeSecurityId zo locator van het gebruikersobject Hallo Hallo met lezen.</span><span class="sxs-lookup"><span data-stu-id="c288c-182">These two TechnicalProfiles are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator of hello user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="c288c-183">Met behulp van dezelfde uitbreidingskenmerken tussen ingebouwde en aangepaste beleidsregels Hallo.</span><span class="sxs-lookup"><span data-stu-id="c288c-183">Using hello same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="c288c-184">Wanneer u uitbreidingskenmerken (aka aangepaste kenmerken) via de portal Hallo-ervaring toevoegt, deze kenmerken worden geregistreerd met Hallo ** b2c-uitbreidingen-app die in elke b2c-tenant voorkomt.</span><span class="sxs-lookup"><span data-stu-id="c288c-184">When you add extension attributes (aka custom attributes) via hello portal experience, those attributes are registered using hello **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="c288c-185">toouse deze extensie kenmerken in het aangepaste beleid:</span><span class="sxs-lookup"><span data-stu-id="c288c-185">toouse these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="c288c-186">In uw b2c-tenant in portal.azure.com te navigeren**Azure Active Directory** en selecteer **App registraties**</span><span class="sxs-lookup"><span data-stu-id="c288c-186">Within your b2c tenant in portal.azure.com, navigate too**Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="c288c-187">Zoek uw **b2c-uitbreidingen-app** en dit selecteren</span><span class="sxs-lookup"><span data-stu-id="c288c-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="c288c-188">Onder 'Essentials' record Hallo **toepassings-ID** en Hallo **Object-ID**</span><span class="sxs-lookup"><span data-stu-id="c288c-188">Under 'Essentials' record hello **Application ID** and hello **Object ID**</span></span>
4. <span data-ttu-id="c288c-189">Opnemen in uw AAD-gemeenschappelijke technische profiel metagegevens zoals als volgt:</span><span class="sxs-lookup"><span data-stu-id="c288c-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

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

<span data-ttu-id="c288c-190">tookeep consistentie met portal Hallo-ervaring, maken deze kenmerken met Hallo portal UI *voordat* u deze gebruiken in uw eigen beleid.</span><span class="sxs-lookup"><span data-stu-id="c288c-190">tookeep consistency with hello portal experience, create these attributes using hello portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="c288c-191">Wanneer u een kenmerk 'ActivationStatus' in hello portal maakt, moet u als volgt tooit verwijzen:</span><span class="sxs-lookup"><span data-stu-id="c288c-191">When you create an attribute "ActivationStatus" in hello portal, you must refer tooit as follows:</span></span>

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a><span data-ttu-id="c288c-192">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="c288c-192">Reference</span></span>

* <span data-ttu-id="c288c-193">Een **technische profiel (TP)** is een elementtype dat kan worden beschouwd als een *functie* die definieert de naam van een eindpunt, de metagegevens, het protocol en details Hallo uitwisseling van claims die Hallo identiteit Ervaring Framework moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c288c-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details hello exchange of claims that hello Identity Experience Framework should perform.</span></span>  <span data-ttu-id="c288c-194">Wanneer dit *functie* wordt aangeroepen in een stap orchestration of vanaf een andere TechnicalProfile, Hallo InputClaims en OutputClaims zijn beschikbaar als parameters door Hallo aanroeper.</span><span class="sxs-lookup"><span data-stu-id="c288c-194">When this *function* is called in an orchestration step or from another TechnicalProfile, hello InputClaims and OutputClaims are provided as parameters by hello caller.</span></span>


* <span data-ttu-id="c288c-195">Voor volledige behandeling op extensie-eigenschappen, Zie Hallo artikel [DIRECTORY-SCHEMA-UITBREIDINGEN | GRAPH API-CONCEPTEN](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="c288c-195">For full treatment on extension properties, see hello article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="c288c-196">Extensie kenmerken in Graph API zijn benoemde Hallo conventie `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="c288c-196">Extension attributes in Graph API are named using hello convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="c288c-197">Aangepast beleid verwijzen tooextensions kenmerken als extension_attributename, dus als weggelaten Hallo ApplicationObjectId in Hallo XML</span><span class="sxs-lookup"><span data-stu-id="c288c-197">Custom policies refer tooextensions attributes as extension_attributename, thus omitting hello ApplicationObjectId in hello XML</span></span>
