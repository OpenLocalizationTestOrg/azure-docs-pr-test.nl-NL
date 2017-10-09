---
title: aaaUnderstanding hello Azure Active Directory Application Manifest | Microsoft Docs
description: Gedetailleerde dekking van hello Azure Active Directory application manifest, die staat voor configuratie van de identiteit van een toepassing in een Azure AD-tenant, en gebruikte toofacilitate OAuth-autorisatie en toestemming ervaring.
services: active-directory
documentationcenter: 
author: sureshja
manager: mbaldwin
editor: 
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: sureshja
ms.custom: aaddev
ms.reviewer: elisol
ms.openlocfilehash: 096c9d5501edbfc08731fea670cee559d4442ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-azure-active-directory-application-manifest"></a>Understanding hello Azure Active Directory-toepassingsmanifest
Toepassingen die kunnen worden geïntegreerd met Azure Active Directory (AD) moeten zijn geregistreerd bij Azure AD-tenant, de configuratie van een permanente identiteit voor de toepassing hello bieden. Deze configuratie wordt geraadpleegd tijdens runtime, scenario's waarmee een toepassing toooutsource en broker-verificatie/autorisatie via Azure AD inschakelen. Zie voor meer informatie over hello Azure AD-toepassingsmodel Hallo [toevoegen, bijwerken en verwijderen van een toepassing] [ ADD-UPD-RMV-APP] artikel.

## <a name="updating-an-applications-identity-configuration"></a>Configuratie van de identiteit van de toepassing bijwerken
Er zijn daadwerkelijk meerdere opties beschikbaar voor het Hallo-eigenschappen van de configuratie van de identiteit van een toepassing, die in functies en graden van problemen verschillen, waaronder de volgende Hallo bijwerken:

* Hallo  **[Azure portal] [ AZURE-PORTAL] online gebruikersinterface** kunt u tooupdate Hallo meest algemene eigenschappen van een toepassing. Dit Hallo snelste en minimaal fout foutgevoelige manier bijwerken van de eigenschappen van uw toepassing, maar niet het geval u volledige toegang tooall eigenschappen, zoals de volgende twee methoden Hallo geven.
* Meer geavanceerde scenario's waar u tooupdate-eigenschappen die niet worden weergegeven in de klassieke Azure-portal Hallo nodig hebt, kunt u Hallo **toepassingsmanifest**. Dit is de focus Hallo van dit artikel en wordt besproken in meer detail starten in de volgende sectie Hallo.
* Het kan ook te**schrijven van een toepassing die gebruikmaakt van Hallo [Graph API] [ GRAPH-API]**  tooupdate uw toepassing waarvoor de meeste inspanning Hallo. Kan dit een aantrekkelijke optie echter als u beheersoftware ontwikkelt of de toepassingseigenschappen tooupdate regelmatig op automatische wijze moet.

## <a name="using-hello-application-manifest-tooupdate-an-applications-identity-configuration"></a>Configuratie van de identiteit van een toepassing met behulp van Hallo application manifest tooupdate
Via Hallo [Azure-portal][AZURE-PORTAL], kunt u de configuratie van de identiteit van uw toepassing bijwerken Hallo toepassingsmanifest met Hallo inline manifest editor door te beheren. U kunt ook downloaden en het toepassingsmanifest Hallo als een JSON-bestand uploaden. Er is geen werkelijke bestand wordt opgeslagen in Hallo-directory. Hallo toepassingsmanifest is slechts een HTTP GET-bewerking op Hallo Azure AD Graph API Toepassingsentiteit en hello uploaden is een PATCH voor HTTP-bewerking op Hallo Toepassingsentiteit.

Als gevolg hiervan, in volgorde toounderstand Hallo indeling en eigenschappen van het toepassingsmanifest hello, moet u tooreference Hallo Graph API [Toepassingsentiteit] [ APPLICATION-ENTITY] documentatie. Voorbeelden van updates die kunnen worden uitgevoerd, hoewel het uploaden van het toepassingsmanifest zijn:

* **-Machtigingsbereiken (oauth2Permissions) declareren** die worden weergegeven door uw web-API. Zie Hallo 'Exposing Web-API's tooOther toepassingen' onderwerp in [toepassingen integreren met Azure Active Directory] [ INTEGRATING-APPLICATIONS-AAD] voor informatie over het implementeren van gebruikersimitaties met Hallo oauth2Permissions overgedragen machtigingen bereik. Zoals eerder vermeld, toepassingseigenschappen entiteit zijn gedocumenteerd in Hallo Graph API [entiteit en het complexType] [ APPLICATION-ENTITY] verwijzingsartikel, met inbegrip van Hallo oauth2Permissions eigenschap hebben die een verzameling van het type [OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION].
* **Toepassingsrollen (appRoles) die worden weergegeven door uw app declareren**. Hallo appRoles-eigenschap van de entiteit van de toepassing is een verzameling van het type [AppRole][APPLICATION-ENTITY-APP-ROLE]. Zie Hallo [op rollen gebaseerde toegangsbeheer in de cloud-toepassingen die gebruikmaken van Azure AD] [ RBAC-CLOUD-APPS-AZUREAD] artikel voor een voorbeeldimplementatie.
* **Bekende client toepassingen (knownClientApplications) declareren**, waarmee u toestemming van toologically tie Hallo Hallo opgegeven client toepassing(en) toohello resource of web-API.
* **Azure AD tooissue groepslidmaatschappen claim aanvragen** voor Hallo aangemelde gebruiker (groupMembershipClaims).  Dit kan ook worden de geconfigureerde tooissue claims over van de gebruiker Hallo directory rollen lidmaatschappen. Zie Hallo [autorisatie in de Cloud-toepassingen met behulp van AD-groepen] [ AAD-GROUPS-FOR-AUTHORIZATION] artikel voor een voorbeeldimplementatie.
* **Toestaan dat uw toepassing toosupport OAuth 2.0 impliciete grant** stromen (oauth2AllowImplicitFlow). Dit type grant-stroom wordt gebruikt met ingesloten JavaScript-webpagina's of toepassingen van één pagina (SPA). Zie voor meer informatie over Hallo impliciete authorization grant [Understanding Hallo OAuth2 impliciete stroom in Azure Active Directory verlenen][IMPLICIT-GRANT].
* **Gebruik van X509 inschakelen certificaten als de geheime sleutel Hallo** (keyCredentials). Zie Hallo [in Office 365-service en -daemon apps bouwen] [ O365-SERVICE-DAEMON-APPS] en [Developer's guide tooauth met Azure Resource Manager-API] [ DEV-GUIDE-TO-AUTH-WITH-ARM] de artikelen voor voorbeelden van de implementatie.
* **Voeg een nieuwe App ID URI** voor uw toepassing (identifierURIs[]). App ID URI's gebruikt toouniquely identificeren van een toepassing binnen de Azure AD-tenant (of op meerdere Azure AD-tenants voor scenario's met meerdere tenants wanneer gekwalificeerd via geverifieerde aangepaste domeinnaam). Ze worden gebruikt bij het aanvragen van machtigingen tooa resource toepassing of het ophalen van een toegangstoken voor de toepassing van een resource. Tijdens het bijwerken van dit element wordt hello dezelfde update uitgevoerd toohello bijbehorende service-principal van servicePrincipalNames [] verzameling, die zich in een van de toepassing hello thuis-tenant.

Hallo toepassingsmanifest biedt ook een goede manier tootrack Hallo status van de registratie van uw toepassing. Omdat het is beschikbaar in JSON-indeling, kan bestandsweergave Hallo in uw broncodebeheer, samen met de broncode van uw toepassing worden gecontroleerd.

## <a name="step-by-step-example"></a>Stap door stap voorbeeld
Nu kunt doorlopen Hallo stappen vereist tooupdate van uw toepassing identiteit configuratie via Hallo-toepassingsmanifest. We van een van de voorgaande voorbeelden hello wordt markering die laat zien hoe toodeclare een machtiging voor het nieuwe scope op een resource-toepassing:

1. Meld u aan toohello [Azure-portal][AZURE-PORTAL].
2. Nadat u hebt geverifieerd, kiest u uw Azure AD-tenant van Hallo rechtsboven Hallo pagina te selecteren.
3. Selecteer **Azure Active Directory** extensie van Hallo links van het navigatievenster en klik op **App registraties**.
4. Hallo-toepassing u wilt tooupdate in Hallo lijst en klik op zoeken.
5. Klik op de pagina toepassing hello **Manifest** tooopen Hallo inline manifest editor. 
6. Hallo-manifest met behulp van deze editor kunt u direct bewerken. Opmerking die manifest Hallo volgt Hallo-schema voor Hallo [Toepassingsentiteit] [ APPLICATION-ENTITY] zoals eerder gezegd: bijvoorbeeld 'Employees.Read.All' ervan uitgaande dat we willen een nieuwe machtiging tooimplement/zichtbaar aangeroepen op de resource-toepassing (API), zou u een nieuwe/seconde element toohello oauth2Permissions verzameling, gewoon ie toevoegen:
   
        "oauth2Permissions": [
        {
        "adminConsentDescription": "Allow hello application tooaccess MyWebApplication on behalf of hello signed-in user.",
        "adminConsentDisplayName": "Access MyWebApplication",
        "id": "aade5b35-ea3e-481c-b38d-cba4c78682a0",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application tooaccess MyWebApplication on your behalf.",
        "userConsentDisplayName": "Access MyWebApplication",
        "value": "user_impersonation"
        },
        {
        "adminConsentDescription": "Allow hello application toohave read-only access tooall Employee data.",
        "adminConsentDisplayName": "Read-only access tooEmployee records",
        "id": "2b351394-d7a7-4a84-841e-08a6a17e4cb8",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application toohave read-only access tooyour Employee data.",
        "userConsentDisplayName": "Read-only access tooyour Employee records",
        "value": "Employees.Read.All"
        }
        ],
   
    Hallo-item moet uniek en daarom moet u een nieuwe globaal unieke ID (GUID) voor Hallo genereren `"id"` eigenschap. In dit geval omdat we opgegeven `"type": "User"`, deze machtiging mag instemming tooby alle accounts die zijn geverifieerd door hello Azure AD-tenant in welke Hallo resource/API-toepassing is geregistreerd. Deze verleent Hallo client toepassing machtiging tooaccess deze namens het Hallo-account. Hallo beschrijving en de weergave tekenreeksen met de naam worden gebruikt tijdens toestemming en weergegeven in de hello Azure-portal.
6. Wanneer u klaar bent Hallo manifest bijwerken, klikt u op **opslaan** toosave Hallo manifest.  
   
Nu dat hello manifest wordt opgeslagen, kunt u een geregistreerde client geven toepassing toohello nieuwe toegangsmachtiging we die hierboven staan vermeld. U kunt nu hello Azure portal-Webgebruikersinterface in plaats van het manifest Hallo clienttoepassing bewerken:  

1. Ga eerst toohello **instellingen** blade Hallo client toepassing toowhich gewenst tooadd toegang toohello nieuwe API, klikt u op **Required Permissions** en kies **selecteert u een API** .
2. U wordt vervolgens gepresenteerd Hallo lijst met geregistreerde resource toepassingen (API's) in Hallo-tenant. Klik op Hallo resource toepassing tooselect of Hallo typenaam van Hallo toepassing hello zoekvak. Wanneer u de toepassing hello hebt gevonden, klikt u op **Selecteer**.  
3. Hiermee gaat u toohello **Selecteer machtigingen** pagina Hallo lijst met machtigingen voor een toepassing en overgedragen machtigingen beschikbaar zijn voor de resource-toepassing hello worden weergegeven. Selecteer nieuwe machtiging in volgorde tooadd Hallo deze toohello client gevraagde van lijst met machtigingen. Deze nieuwe machtiging worden opgeslagen in de configuratie van het Hallo-clienttoepassing van identiteit, in Hallo 'requiredResourceAccess' verzamelingseigenschap.


Dat is alles. Uw toepassingen wordt nu uitgevoerd met de nieuwe configuratie voor identiteit.

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over de relatie tussen de toepassing en Service-Principal objecten van een toepassing hello [toepassing en service-principal objecten in Azure AD][AAD-APP-OBJECTS].
* Zie Hallo [verklarende woordenlijst voor Azure AD-ontwikkelaar] [ AAD-DEVELOPER-GLOSSARY] voor definities van Hallo core Azure Active Directory (AD)-concepten voor ontwikkelaars.

Gebruik Hallo opmerkingen sectie hieronder tooprovide feedback en help ons verfijnen en onze content vorm.

<!--article references -->
[AAD-APP-OBJECTS]: active-directory-application-objects.md
[AAD-DEVELOPER-GLOSSARY]: active-directory-dev-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]: active-directory-integrating-applications.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]: active-directory-dev-understanding-oauth2-implicit-grant.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/

