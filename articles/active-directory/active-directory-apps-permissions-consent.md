---
title: Apps, machtigingen en toestemming in Azure Active Directory | Microsoft Docs
description: "Azure AD Connect integreert uw on-premises directory's met Azure Active Directory. Hiermee kunt u een algemene identiteit voor Office 365, Azure en SaaS toepassingen die zijn geïntegreerd met Azure AD tooprovide."
keywords: active directory inleiding tooAzure AD, apps, wat is Azure AD Connect installeren
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a>Apps, machtigingen en toestemming in Azure Active Directory
U kunt toepassingen tooyour directory toevoegen in Azure Active Directory.  Hallo-toepassingen kunnen variëren afhankelijk van de toepassing hello type.  tooview toepassingen in de klassieke portal hello, selecteer een map en kies de toepassingen.

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.

## <a name="types-of-apps"></a>App-typen

1. **Apps met één tenant** </br>
    - **Apps voor één tenant** -vaak tooas line-of-business (LOB)-apps. Dit is Hallo geval waar iemand binnen uw organisatie ontwikkelt van hun eigen app en wilt dat gebruikers in Hallo organisatie toobe kunnen toosign in toohello-app.
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - **Toepassingsproxy van apps** : wanneer u een on-premises toepassing met Azure AD-toepassingsproxy, weer een één-tenant-app in uw tenant (in aanvulling toohello App Proxy-service) is geregistreerd. Deze app vertegenwoordigt uw on-premises toepassing voor alle cloudinteracties (bijvoorbeeld verificatie). (App Proxy vereist Azure AD Basic of hoger.)


2. **Apps met meerdere tenants**
    - **Multitenant-apps die anderen met instemmen kunnen** - vergelijkbare te 'single-tenant-apps die uw organisatie ontwikkelt'. de belangrijkste verschil hello (naast het Hallo-logica in Hallo app zelf) is de gebruikers van andere tenants kunnen ook toestemming geven tooand toohello app aanmelden.</br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - **Apps met meerdere tenants die anderen ontwikkelen en waar Contoso toestemming voor kan geven**. (Kort gezegd ook 'toegestane apps'.) Dit is Hallo spiegelen zijde van 'multitenant apps in die uw organisatie ontwikkelt'. Wanneer een andere organisatie een multitenant-app ontwikkelt, kunnen gebruikers van uw organisatie toohello app toestemming en tooit aanmelden.
    - **Apps van Microsoft** - Apps die Microsoft-services vertegenwoordigen. Toestemming wordt aangedreven door Hallo feit dat u zich aanmeldt voor Hallo-service. Er is het soms speciale UX en logica voor bepaalde Microsoft-apps die vaak wordt gebruikt bij het opstellen van beleid rond toegang toohello app.</br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - **Vooraf geïntegreerde apps** -Apps die beschikbaar zijn in Azure AD App-galerie, die u kunt toevoegen Hallo tooyour directory tooprovide één eenmalige aanmelding (en in sommige gevallen, inrichting) toopopular SaaS-apps.
    - **Azure AD met eenmalige aanmelding** - 'Echte' eenmalige aanmelding voor apps die met Azure AD kunnen worden geïntegreerd via een ondersteund aanmeldingsprotocol zoals SAML 2.0 of OpenID Connect. Hallo wizard leidt u door het instelt.
    - **Eenmalige aanmelding wachtwoord**: Azure AD Hallo gebruikersreferenties voor Hallo app veilig opgeslagen en Hallo referenties zijn 'geïnjecteerd' in hello aanmelden formulier door Hallo Browseruitbreiding van de toegang tot Apps van Azure AD. Dit heet ook wel 'password vaulting'.

## <a name="permissions"></a>Machtigingen

Wanneer een app is geregistreerd, wordt Hallo gebruiker uitvoeren Hallo app-registratie (dat wil zeggen, Hallo developer) definieert welke machtigingen Hallo-app moet toegang tot en welke bronnen. (Hallo resources zijn, zelf, gedefinieerd als andere apps). Bijvoorbeeld zou iemand een e-mail reader-app bouwen vermeld dat de app Hallo 'Postvakken toegang als de gebruiker is aangemeld Hallo' toestemming in Hallo 'Office 365 Exchange Online' resource vereist:
    
![](media/active-directory-apps-permissions-consent/apps6.png)

Om een app (Hallo client) toorequest een bepaalde machtiging vanuit een andere app (Hallo resource) definieert Hallo ontwikkelaar van Hallo resource app Hallo machtigingen die aanwezig zijn. In ons voorbeeld Microsoft hello eigenaar van de 'Office 365 Exchange Online' hello resource app, gedefinieerd hebben een machtiging met de naam "Postvakken toegang als de gebruiker is aangemeld Hallo".

Bij het definiëren van machtigingen moet Hallo app-ontwikkelaar definiëren als Hallo-machtiging kunt wil of als hiervoor toestemming van de beheerder. Hierdoor kunnen ontwikkelaars tooallow gebruikers tooconsent op hun eigen tooapps alleen machtigingen voor lage gevoeligheid aangevraagd, maar tooconsent toomore gevoelige beheerdersmachtigingen nodig. Bijvoorbeeld, Hallo 'Azure Active Directory' resource app, is gedefinieerd, zodat gebruikers kunnen toestemming van tooapps, vraagt beperkte machtigingen voor alleen-lezen.  Er is echter toestemming van een beheerder nodig voor volledige lees- en schrijftoegang.

Omdat systeemeigen clients niet worden geverifieerd, kan een app die is gedefinieerd als systeemeigen client-app alleen overgedragen machtigingen aanvragen. Dit betekent dat er altijd een daadwerkelijke gebruiker betrokken moet zijn bij het ophalen van een token. Web-apps en web-API's (vertrouwelijke clients) moeten altijd worden geverifieerd door Azure AD bij het ophalen van een toegangstoken. Dit betekent dat ze hebben ook Hallo mogelijkheid app alleen-lezen machtigingen om te vragen. Als bijvoorbeeld een back-end-service moet tooauthenticate tooanother back-end-service. Toepassingen waarvoor machtigingen die zich beperken tot de app worden aangevraagd, moeten altijd worden goedgekeurd door een beheerder.

Samenvatting:



- Hallo-machtigingen die nodig zijn voor andere apps (bronnen) wordt aangegeven door een app (client).
- Een app (resource) wordt aangegeven welke machtigingen zijn blootgestelde tooother apps (clients).
- Een machtiging kan zich beperken tot één app of kan overgedragen zijn.
- Een overgedragen machtiging kan worden gemarkeerd als 'gebruikerstoestemming toegestaan' of 'beheerderstoestemming vereist'.
- Een app kan functioneren als een client (door op te geven dat het moet machtigingen tooa resource), als een bron (door op te geven welke machtigingen worden getoond), of als beide.

## <a name="controls"></a>Besturingselementen

Hallo Hieronder volgt een lijst met besturingselementen voor verschillende admin Hallo beschikbaar voor alle dit gedrag. Hallo beheerder besturingselementen kunnen worden geopend in de klassieke portal Hallo van configureren onder Hallo-directory.

![](media/active-directory-apps-permissions-consent/apps7.png)

In hello Azure portal onder **beheren**, **gebruikersinstellingen**.

![](media/active-directory-apps-permissions-consent/apps11.png)



- U kunt bepalen of gebruikers toestemming van tooapps geven kunnen:

Selecteer in de klassieke portal Hallo **gebruikers toepassingen machtigingen tooaccess kunnen geven hun gegevens.**
![](media/active-directory-apps-permissions-consent/apps8.png)

Selecteer in de Azure-portal hello, **gebruikers apps tooaccess kunnen toestaan hun gegevens**.
![](media/active-directory-apps-permissions-consent/apps12.png)



- Kunt u bepalen of gebruikers hun eigen LOB-apps voor één tenant kunnen registreren: In de klassieke portal Selecteer Hallo **gebruikers geïntegreerde toepassingen kunnen toevoegen.**
![](media/active-directory-apps-permissions-consent/apps9.png)

Selecteer in de Azure-portal hello, **gebruikers apps tooaccess kunnen toestaan hun gegevens**.
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
>Zelfs als u gebruikers tooregister één tenant LOB-apps toestaat, zijn er beperkingen met toowhat kunnen worden geregistreerd.  
>Dit geldt bijvoorbeeld voor ontwikkelaars die geen directorybeheerder zijn.
>
>- Gebruikers mogen van een app met één tenant geen app met meerdere tenants maken.
>- Bij het registreren van LOB-apps voor één tenant kunnen geen gebruikers app alleen-lezen machtigingen tooother apps vragen.
>- Bij het registreren van LOB-apps voor één tenant kunnen geen gebruikers gedelegeerde machtigingen tooother apps vragen als deze machtigingen admin toestemming vereist.
>- Gebruikers maken geen wijzigingen tooapps dat ze geen eigenaren van zijn.



- U bepaalt of gebruikers zelf vooraf geïntegreerde apps mogen toevoegen waarvoor eenmalige aanmelding met een wachtwoord wordt gebruikt ('password vaulting') ![](media/active-directory-apps-permissions-consent/apps10.png)



- U bepaalt onder welke omstandigheden toepassingen kunnen worden geopend (voorwaardelijke toegang). Let erop dat dit geldt voor zowel client-app toohello en toohello resource app. Ja, dat u een beleid voor voorwaardelijke toegang met de tekst dat die Hallo 'Office 365 Exchange Online' app alleen toegankelijk vanaf computers die voldoen aan het beleid.  Dit beleid wordt ook starten wanneer een gebruiker probeert een client-app die Online machtigingen tooExchange vraagt toouse.



- U hebt zichtbaarheid waarop apps zijn instemming tooand welke worden gebruikt.

1.  Wanneer een gebruiker hiermee akkoord tooan app gaat, wordt een ServicePrincipal-object gemaakt in Hallo-tenant. Maken van het ServicePrincipal is opgenomen in het Hallo-controlerapport.
2.  Gebruiker aanmelden activiteitsrapporten laat u weten welke app Hallo-gebruiker zich aanmeldt. 

## <a name="example"></a>Voorbeeld

Een voorbeeld: u gaat nu Hallo 'FabrikamMail voor Office 365' app, die u opgevallen dat gebruikers in uw tenant zich aanmeldt. FabrikamMail is een e-mail-app voor gebruik op Android-apparaten, gepubliceerd door Fabrikam, Inc. Hiermee worden onderverdeeld in Hallo ' multitenant apps andere ontwikkelen, Contoso met instemmen kunt '.

Als gebruikers tooconsent mogen, krijgen ze een toestemming vragen Hallo eerste keer dat ze zich aanmeldt:![](media/active-directory-apps-permissions-consent/apps14.png)

'Toegang tot uw postvakken' is hello gebruikersgerichte toestemming tekenreeks voor Hallo 'Postvakken toegang als de gebruiker is aangemeld Hallo' machtiging door 'Office 365 Exchange Online' (dat wil zeggen, Exchange) beschikbaar gesteld.

Hallo-machtigingen kunt u zien door het opzoeken van Hallo ServicePrincipal object voor Exchange (Hallo resource), dat is toegevoegd wanneer u zich registreerde voor Office 365. U kunt zien van Hallo ServicePrincipal-object van een 'exemplaar' Hallo-App in uw tenant, die wordt gebruikt voor het vastleggen van verschillende opties en configuraties.  U kunt dit zien met behulp van Hallo `Get-AzureADServicePrincipal` in PowerShell.

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

Toestemming wordt gestart wanneer 'Accepteren' Hallo-gebruiker. Eerst wordt een ServicePrincipal-object voor 'FabrikamMail voor Office 365' gemaakt in Hallo-tenant. Hallo ServicePrincipal ziet er ongeveer als volgt uit:

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

Tooan app ermee akkoord dat een Oauth2PermissionGrant koppeling maakt tussen Hallo volgende:
  
- Hallo-gebruikersobject
- Hallo van client-apps ServicePrincipalName (SPN)
- Hallo resource apps ServicePrincipalName (SPN)
- machtigingen in Hallo resource-app.  

In geval van FabrikamMail Hallo ziet deze er ongeveer als volgt:

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

(**ClientId** FabrikamMail van service principal-object-id (hello die u zojuist hebt gemaakt) **PrincipalId** Hallo gebruiker de object-ID (Hallo gebruiker die heeft ingestemd), is **ResourceId**is van de Exchange-service principal-object-ID, een bereik is Hallo toestemming in Exchange is wil).

Als gebruikers zijn niet toegestaan voor tooconsent, zien ze een scherm weergegeven dat dat de machtiging aangeeft is vereist.

