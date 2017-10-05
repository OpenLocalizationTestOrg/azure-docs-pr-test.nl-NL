---
title: Toepassingen integreren met Azure Active Directory | Microsoft Docs
description: Meer informatie over het toevoegen, bijwerken of verwijderen van een toepassing in Azure Active Directory (Azure AD).
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: mbaldwin
ms.assetid: ae637be5-0b71-4b1e-b1fe-b83df3eb4845
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: lenalepa
ms.custom: aaddev
ms.reviewer: luleon
ms.openlocfilehash: 3be341bcb897a1481f145825429a1a94dfaae3b0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="integrating-applications-with-azure-active-directory"></a>Toepassingen integreren met Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Enterprise-ontwikkelaars en providers van software-as-a-service (SaaS) kunnen commerciële cloudservices of bedrijfstoepassingen ontwikkelen die kunnen worden geïntegreerd met Azure Active Directory (Azure AD) om beveiligde aanmelding en autorisatie te bieden voor hun services. Voor het integreren van een toepassing of service met Azure AD, moet een ontwikkelaar de details over de toepassing eerst registreren bij Azure AD via de klassieke Azure portal.

In dit artikel laat zien hoe toevoegen, bijwerken of verwijderen van een toepassing in Azure AD. U vindt u informatie over de verschillende typen toepassingen die kunnen worden geïntegreerd met Azure AD, het configureren van uw toepassingen voor toegang tot andere resources, zoals web-API's en meer.

Zie voor meer informatie over de twee Azure AD-objecten die een geregistreerde toepassing en de relatie tussen deze twee vertegenwoordigen, [toepassingsobjecten en Service-Principal objecten](active-directory-application-objects.md); voor meer informatie over de huisstijlrichtlijnen moet u bij het ontwikkelen van toepassingen met Azure Active Directory, Zie [huisstijl richtlijnen voor geïntegreerde Apps](active-directory-branding-guidelines.md).

## <a name="adding-an-application"></a>Een toepassing toevoegen
Alle toepassingen die gebruikmaken van de mogelijkheden van Azure AD wil moet eerst worden geregistreerd in een Azure AD-tenant. Het registratieproces omvat het Azure AD-gegevens over uw toepassing, zoals de URL waar is gevonden, de URL om te antwoorden verzenden nadat een gebruiker is geverifieerd, geeft de URI die de app, enzovoort identificeert.

Als u een webtoepassing die u zojuist hebt moet ondersteuning bieden voor aanmelding voor gebruikers in Azure AD maakt, kunt u gewoon de onderstaande instructies volgen. Als uw toepassing moet referenties of de machtigingen voor toegang tot een web-API of toestaan dat gebruikers van andere Azure AD-tenants toegang tot dit moet, raadpleeg dan [bijwerken van een toepassing](#updating-an-application) sectie om door te gaan met het configureren van uw toepassing.

### <a name="to-register-a-new-application-in-the-azure-portal"></a>Een nieuwe toepassing registreren in de Azure-portal
1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Uw account selecteren in de rechterbovenhoek van de pagina kiest u uw Azure AD-tenant.
3. Kies in het navigatiedeelvenster links **meer Services**, klikt u op **App registraties**, en klik op **toevoegen**.
4. Volg de aanwijzingen op het scherm en maak een nieuwe toepassing. Als u specifieke voorbeelden voor webtoepassingen of systeemeigen toepassingen wilt, Bekijk onze [snelstartgidsen](active-directory-developers-guide.md).
  * Voor webtoepassingen, geeft u de **aanmeldings-URL**, dit is de basis-URL van uw app, waarbij kunnen gebruikers zich aanmelden bijvoorbeeld `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: The **App ID URI** is a unique identifier for your application. The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Voor systeemeigen toepassingen bieden een **omleidings-URI**, dat gebruikmaakt van Azure AD token antwoorden retourneren. Voer een waarde in die specifiek is voor uw toepassing, bijvoorbeeld `http://MyFirstAADApp`.
5. Zodra u inschrijving hebt voltooid, wijst Azure AD van uw toepassing een unieke client-id, de toepassing-ID. Uw toepassing is toegevoegd en gaat u naar de pagina Quick Start voor uw toepassing. Afhankelijk van of uw toepassing een web- of systeemeigen toepassing is, ziet u de verschillende opties voor het toevoegen van aanvullende mogelijkheden voor uw toepassing. Wanneer uw toepassing is toegevoegd, kunt u beginnen uw toepassing bijwerkt zodat gebruikers aanmelden, toegang tot web-API's in andere toepassingen of multitenant-toepassing (die andere organisaties toegang tot uw toepassing kan) configureren.

> [!NOTE]
> De registratie van de nieuwe toepassing wordt standaard geconfigureerd, zodat gebruikers van uw directory aan te melden bij uw toepassing.
> 
> 

## <a name="updating-an-application"></a>Bijwerken van een toepassing
Als uw toepassing met Azure AD is geregistreerd, moet deze mogelijk worden bijgewerkt om te voorzien van toegang tot web-API's, beschikbaar gesteld in andere organisaties en meer. Deze sectie beschrijft de verschillende manieren waarop in die u wellicht voor het configureren van uw toepassing verder. Eerst begint we met een overzicht van het Framework toestemming geven, dit is belangrijk te weten als u resource/API-toepassingen die worden gebruikt door clienttoepassingen gebouwd door ontwikkelaars in uw organisatie of een andere organisatie bouwt.

Voor meer informatie over de manier waarop verificatie in Azure AD, gaat u [verificatie scenario's voor Azure AD](active-directory-authentication-scenarios.md).

### <a name="overview-of-the-consent-framework"></a>Overzicht van het framework toestemming
Azure AD toestemming framework kunt eenvoudig ontwikkelen van multitenant-web- en systeemeigen clienttoepassingen die toegang moeten krijgen tot de web-API's die zijn beveiligd door een Azure AD-tenant, verschilt van de waar de clienttoepassing is geregistreerd. Deze web-API's omvatten de Microsoft Graph-API (voor toegang tot Azure Active Directory, Intune en services in Office 365) en andere Microsoft-services-API's, naast uw eigen web-API's. Het framework is gebaseerd op een gebruiker of beheerder toestemming verlenen tot een toepassing waarin u wordt gevraagd om te worden geregistreerd in de directory, waarbij toegang tot Active directory-gegevens.

Bijvoorbeeld, als een client-toepassing moet lezen agenda-informatie over de gebruiker van Office 365, die gebruiker moet toe te staan de clienttoepassing. Nadat u toestemming is opgegeven, is de clienttoepassing worden kunnen de Microsoft Graph-API aanroepen namens de gebruiker en het gebruik van de agenda-informatie, indien nodig. De [Microsoft Graph API](https://graph.microsoft.io) biedt toegang tot gegevens in Office 365 (zoals agenda's en berichten van Exchange, sites en lijsten van SharePoint, documenten van OneDrive, OneNote-notitieblokken, taken van de Planner, werkmappen van Excel, enz.) en de gebruikers en groepen van Azure AD en andere gegevensobjecten van meer Microsoft-cloudservices. 

Het framework toestemming is gebouwd op OAuth 2.0 en de verschillende stromen, zoals code verlenen en client autorisatiereferenties verlenen, met behulp van openbare of vertrouwelijke clients. Met behulp van OAuth 2.0, maakt Azure AD het mogelijk te veel verschillende soorten clienttoepassingen, zoals in een telefoon, tablet, server of een webtoepassing is opgebouwd en toegang krijgen tot de vereiste resources.

Zie voor meer informatie over het framework toestemming gedetailleerde [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx), [verificatie scenario's voor Azure AD](active-directory-authentication-scenarios.md), en Zie voor meer informatie over het verkrijgen van toegang tot Office 365 via Microsoft Graph [App verificatie met Microsoft Graph](https://graph.microsoft.io/docs/authorization/auth_overview).

#### <a name="example-of-the-consent-experience"></a>Voorbeeld van de toestemming-ervaring
De volgende stappen ziet u hoe de toestemming ondervinden werkt voor de ontwikkelaar van toepassingen en de gebruiker.

1. Stel de machtigingen die vereist zijn voor uw toepassing met behulp van de menu's in de sectie machtigingen vereist op de configuratiepagina van uw webtoepassing client in de Azure portal.
   
    ![Machtigingen voor andere toepassingen](./media/active-directory-integrating-applications/requiredpermissions.png)
2. U kunt uw toepassing worden machtigingen zijn bijgewerkt, de toepassing wordt uitgevoerd en een gebruiker is gebruikt voor het eerst. Als de toepassing niet al verkregen een toegang of het vernieuwen van tokens, de toepassing moet gaat u naar Azure AD autorisatie eindpunt verkrijgen van een autorisatiecode die kan worden gebruikt voor het verkrijgen van een nieuwe toegang en vernieuw token.
3. Als de gebruiker niet al is geverifieerd, wordt hen gevraagd aan te melden bij Azure AD.
   
    ![Gebruiker of beheerder aanmelden bij Azure AD](./media/active-directory-integrating-applications/usersignin.png)
4. Nadat de gebruiker is aangemeld, wordt Azure AD bepalen of de gebruiker moet een pagina toestemming worden weergegeven. Deze beslissing is gebaseerd op of de gebruiker (of de beheerder van hun organisatie) is al verleend de toepassing toestemming. Toestemming heeft geen toestemming gekregen, Azure AD wordt de gebruiker om toestemming gevraagd als de vereiste machtigingen die deze functie moet worden weergegeven. De reeks machtigingen die wordt weergegeven in het dialoogvenster toestemming zijn hetzelfde als wat u in de gedelegeerde machtigingen in de Azure portal is geselecteerd.
   
    ![Toestemming gebruikerservaring](./media/active-directory-integrating-applications/consent.png)
5. Nadat de gebruiker toestemming verleent, wordt een autorisatiecode wordt geretourneerd naar uw toepassing, kan worden ingewisseld verkrijgen van een toegangstoken en vernieuwen van tokens. Zie voor meer informatie over deze stroom, de [webtoepassing voor web-API-sectie](active-directory-authentication-scenarios.md#web-application-to-web-api) in sectie [verificatie scenario's voor Azure AD](active-directory-authentication-scenarios.md).

6. Als beheerder, kunt u ook akkoord gedelegeerde machtigingen van een toepassing namens de gebruikers in uw tenant. Hiermee wordt voorkomen dat het dialoogvenster toestemming wordt weergegeven voor elke gebruiker in de tenant. U kunt dit doen vanuit de [Azure-portal](https://portal.azure.com) vanaf de toepassingspagina. Van de **instellingen** blade voor uw toepassing, klikt u op **Required Permissions** en klik op de **machtiging verlenen** knop. 

    ![Machtigingen voor expliciete admin toestemming verlenen](./media/active-directory-integrating-applications/grantpermissions.png)
    
> [!NOTE]
> Verlenen expliciete toestemming geven met behulp van de **machtiging verlenen** knop is momenteel vereist zijn voor één pagina toepassingen (SPA) met behulp van ADAL.js, zoals het toegangstoken is aangevraagd zonder een instemmingsprompt, mislukken als toestemming is niet verleend.   

### <a name="configuring-a-client-application-to-access-web-apis"></a>Een clienttoepassing toegang krijgt tot de web-API's configureren
Om een web/vertrouwelijk clienttoepassing kunnen deelnemen aan een machtiging grant-stroom die verificatie vereist (en verkrijgen van een toegangstoken), moet deze beveiligde referenties maken. De standaardmethode voor verificatie wordt ondersteund door de Azure-portal is de Client-ID + symmetrische sleutel. Deze sectie wordt uitgelegd hoe de configuratiestappen die vereist de geheime sleutel van de client om referenties te verstrekken.

Bovendien voordat een client kan toegang tot een web-API die worden weergegeven door een resource-toepassing (ie: Microsoft Graph API), het framework toestemming zorgt voor de client verkrijgt de machtiging grant vereist, op basis van de machtigingen die zijn aangevraagd. Standaard kunt alle toepassingen machtigingen van Azure Active Directory (Graph API) en Azure Service Management API met de Azure AD-'aanmelding bij het inschakelen en lezen gebruikersprofiel' machtiging zijn standaard al geselecteerd. Als u de clienttoepassing wordt geregistreerd in een Office 365 Azure AD-tenant, web-API's en machtigingen voor SharePoint en Exchange Online worden ook beschikbaar voor selectie. U kunt kiezen uit [twee soorten machtigingen](active-directory-dev-glossary.md#permissions) in de vervolgkeuzemenu's naast de gewenste web-API:

* Toepassingsmachtigingen: Uw clienttoepassing moet toegang tot de web-API als zelf (geen gebruikerscontext). Dit type machtiging beheerder toestemming nodig en is ook niet beschikbaar voor systeemeigen clienttoepassingen.
* Gedelegeerde machtigingen: Uw clienttoepassing moet toegang tot de web-API als de gebruiker is aangemeld, maar met de toegang beperkt door de geselecteerde machtiging. Dit type machtigingen kan worden verleend door een gebruiker, tenzij de machtiging is geconfigureerd als het vereisen van instemming met de beheerder. 

> [!NOTE]
> Een gedelegeerde machtigingen toe te voegen aan een toepassing verleent automatisch geen toestemming aan de gebruikers in de tenant, zoals in de klassieke Azure Portal. De gebruikers moeten nog steeds handmatig toestemming voor de toegevoegde gedelegeerde machtigingen tijdens runtime, tenzij de beheerder klikt op de **machtiging verlenen** knop van de **Required Permissions** sectie van de toepassingspagina in de Azure portal. 

#### <a name="to-add-credentials-or-permissions-to-access-web-apis"></a>Referenties of machtigingen voor toegang tot web-API's toe te voegen
1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Uw account selecteren in de rechterbovenhoek van de pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de toepassing die u wilt configureren. Dit wordt gaat u naar de pagina Quick Start van de toepassing, evenals de blade instellingen voor de toepassing geopend.
4. Klik op de sectie 'Sleutels' op de blade instellingen als u een geheime sleutel voor de referenties van de webtoepassing.  
   
   * Een beschrijving voor uw sleutel toevoegen en selecteer een 1 of 2 jaar duur. 
   * De meest rechtse kolom bevat de waarde van de sleutel, nadat u de wijzigingen in de configuratie hebt opgeslagen. Moet u keert u terug naar deze sectie en kopieer het nadat u opslaan raakt, zodat u deze voor gebruik in uw clienttoepassing tijdens de verificatie tijdens runtime.
5. Klik op de sectie 'Required Permissions' uit de blade instellingen als u machtigingen voor toegang tot bronnen API's van de client. 
   
   * Klik eerst op de knop "Toevoegen".
   * Klik op "Selecteer een API' om te selecteren van het type bronnen die u verzamelen wilt uit.
   * Blader door de lijst met beschikbare API's of gebruik het zoekvak te selecteren in de beschikbare resource toepassingen in uw directory waarin een web-API. Klik op de resource die u geïnteresseerd bent in en klik vervolgens op **Selecteer**.
   * Zodra u hebt geselecteerd, kunt u in de **Selecteer machtigingen** menu, waarin u de ' toepassing ' en 'Overgedragen machtigingen' voor uw toepassing selecteren kunt.
   
6. Wanneer u klaar bent, klikt u op de **gedaan** knop.

> [!NOTE]
> Te klikken op de **gedaan** knop stelt ook automatisch de machtigingen voor uw toepassing in uw directory op basis van de machtigingen voor andere toepassingen die u hebt geconfigureerd.  U kunt deze Toepassingsmachtigingen weergeven door te kijken naar de toepassing **instellingen** blade.
> 
> 

### <a name="configuring-a-resource-application-to-expose-web-apis"></a>Configureren van de toepassing van een resource te kunnen stellen van web-API 's
U kunt een web-API ontwikkelen en beschikbaar is voor clienttoepassingen maken bij het blootstellen van toegang [scopes](active-directory-dev-glossary.md#scopes) en [rollen](active-directory-dev-glossary.md#roles). Een juist geconfigureerde web-API wordt uitgevoerd net als de andere Microsoft-website API's, waaronder de Graph API en de Office 365-API's beschikbaar zijn. Toegangsbereiken en rollen worden weergegeven via uw [van toepassingsmanifest](active-directory-dev-glossary.md#application-manifest), dit is een JSON-bestand met de configuratie van de identiteit van uw toepassing.  

De volgende sectie wordt beschreven hoe u toegangsbereiken, door het wijzigen van de resource toepassingsmanifest blootstellen.

#### <a name="adding-access-scopes-to-your-resource-application"></a>Toegangsbereiken toe te voegen aan uw toepassing resource
1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Uw account selecteren in de rechterbovenhoek van de pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de toepassing die u wilt configureren. Dit wordt gaat u naar de pagina Quick Start van de toepassing, evenals de blade instellingen voor de toepassing geopend.
4. Klik op **Manifest** vanaf de toepassingspagina om het manifest inline-editor te openen. 
5. Knooppunt "oauth2Permissions" vervangen door de volgende JSON-fragment. Dit fragment is een voorbeeld van het blootstellen van een scope bekend als 'gebruikersimitaties', waarmee een resource-eigenaar een clienttoepassing een soort gedelegeerde toegang geven tot een resource. Zorg ervoor dat u de tekst en waarden voor uw eigen toepassing wijzigen:
   
        "oauth2Permissions": [
        {
            "adminConsentDescription": "Allow the application full access to the Todo List service on behalf of the signed-in     user",
            "adminConsentDisplayName": "Have full access to the Todo List service",
            "id": "b69ee3c9-c40d-4f2a-ac80-961cd1534e40",
            "isEnabled": true,
            "type": "User",
            "userConsentDescription": "Allow the application full access to the todo service on your behalf",
            "userConsentDisplayName": "Have full access to the todo service",
            "value": "user_impersonation"
            }
        ],
   
    De id-waarde moet een nieuwe gegenereerde GUID die u met behulp van maakt een [GUID generatie hulpprogramma](https://msdn.microsoft.com/library/ms241442%28v=vs.80%29.aspx) of via een programma. Hiermee geeft u een unieke id voor de machtiging die wordt blootgelegd door de web-API. Nadat de client op de juiste wijze geconfigureerd is om aan te vragen toegang tot uw web-API en de web-API-aanroepen, wordt er een OAuth 2.0 JWT-token met de claim bereik (scp) is ingesteld op de bovenstaande waarde die in dit geval user_impersonation opleveren.
   
   > [!NOTE]
   > Extra scopes later zo nodig kan worden blootgesteld. U kunt uw web-API kan meerdere scopes die zijn gekoppeld met tal van verschillende functies worden blootgesteld. U kunt nu toegang tot de web-API beheren met behulp van de claim bereik (scp) in de ontvangen OAuth 2.0 JWT-token.
   > 
   > 
6. Klik op **opslaan** om op te slaan van het manifest. Uw web-API is nu geconfigureerd voor gebruik door andere toepassingen in uw directory.

#### <a name="to-verify-the-web-api-is-exposed-to-other-applications-in-your-directory"></a>Om te controleren of het web wordt API blootgesteld aan andere toepassingen in uw directory
1. Klik op het bovenste menu **App registraties**, selecteer de gewenste clienttoepassing die u wilt configureren, toegang tot de web-API en navigeer naar de blade instellingen.
2. Van de **Required Permissions** sectie, selecteert u de web-API die u zojuist hebt een machtiging voor beschikbaar gesteld. Selecteer de nieuwe machtiging in de vervolgkeuzelijst gedelegeerde machtigingen.

![Takenlijst machtigingen worden weergegeven.](./media/active-directory-integrating-applications/todolistpermissions.png)

#### <a name="more-on-the-application-manifest"></a>Meer informatie over het toepassingsmanifest
Het toepassingsmanifest wordt daadwerkelijk fungeert als een mechanisme voor het bijwerken van de toepassing-entiteit waarmee alle kenmerken van een Azure AD-toepassing identiteit configuratie, met inbegrip van de API-toegangsbereiken besproken zijn gedefinieerd. Zie voor meer informatie over de entiteit van de toepassing de [Graph API-toepassing entiteit documentatie](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity). In dit vindt u volledige naslaginformatie over de toepassing entiteitsleden gebruikt om machtigingen voor uw API te geven:  

* het lid appRoles die een verzameling van [AppRole](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type) entiteiten die kunnen worden gebruikt voor het definiëren van de **Toepassingsmachtigingen** voor een web-API  
* het lid oauth2Permissions die een verzameling van [OAuth2Permission](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type) entiteiten die kunnen worden gebruikt voor het definiëren van de **gedelegeerde machtigingen** voor een web-API

Voor meer informatie over application manifest concepten over het algemeen Raadpleeg [inzicht in de Azure Active Directory-toepassingsmanifest](active-directory-application-manifest.md).

### <a name="accessing-the-azure-ad-graph-and-office-365-via-microsoft-graph-apis"></a>Toegang tot de Azure AD Graph en Office 365 via Microsoft Graph API 's  
Zoals eerder gezegd blootstellen/hebt u toegang tot API's op uw eigen toepassingen resource, kunt u ook uw clienttoepassing toegang krijgt tot de API's die worden weergegeven door de Microsoft-bronnen bijwerken.  De Microsoft Graph API wel 'Microsoft Graph' in de lijst met machtigingen voor andere toepassingen genoemd, beschikbaar is of alle toepassingen die zijn geregistreerd bij Azure AD. Als u de clienttoepassing in een Azure AD-tenant die is ingericht door Office 365 registreert, u kunt ook toegang tot alle machtigingen die worden weergegeven door de Microsoft Graph-API aan verschillende resources voor Office 365.

Zie voor een volledige bespreking van de toegangsbereiken beschikbaar is gemaakt door Microsoft Graph API, de [-machtigingsbereiken | Microsoft Graph API concepten](https://graph.microsoft.io/docs/authorization/permission_scopes) artikel.

> [!NOTE]
> Vanwege een beperking, kunnen native client-toepassingen alleen aanroepen in de Azure AD Graph API als ze de machtiging 'Toegang tot de directory van uw organisatie' gebruiken.  Deze beperking geldt niet voor webtoepassingen.
> 
> 

### <a name="configuring-multi-tenant-applications"></a>Multitenant-toepassingen configureren
Wanneer u een toepassing naar Azure AD toevoegt, kunt u uw toepassing kan alleen worden geopend door gebruikers in uw organisatie. U kunt ook uw toepassing worden geopend door gebruikers in externe organisaties. Deze twee toepassingstypen worden één tenant en multitenant-toepassingen genoemd. U kunt de configuratie van een toepassing voor één tenant zodat het een multitenant-toepassing in deze sectie wordt beschreven hieronder wijzigen.

Het is belangrijk te weten de verschillen tussen een één tenant en multitenant-toepassing:  

* Een toepassing voor één tenant is bedoeld voor gebruik in een organisatie. Ze zijn doorgaans een line-of-business (LoB)-toepassing geschreven door de ontwikkelaar van een onderneming. Een toepassing voor één tenant moet alleen worden geopend door gebruikers in een bepaalde map en als gevolg hiervan wordt alleen moet worden ingericht in één directory.
* Een multitenant-toepassing is bedoeld voor gebruik in veel organisaties. Een software-as-a-service (SaaS)-webtoepassing die meestal geschreven door een onafhankelijke softwareleverancier (ISV) zijn. Multitenant-toepassingen moeten worden ingericht in elke map waar ze worden gebruikt, waarvoor een gebruiker of beheerder toestemming voor deze ondersteund via de Azure AD toestemming framework registreren. Houd er rekening mee dat alle systeemeigen clienttoepassingen multitenant standaard zijn als ze zijn geïnstalleerd op de resource-eigenaar apparaat. Zie het overzicht van de bovenstaande sectie toestemming Framework voor meer informatie over het framework toestemming.

#### <a name="enabling-external-users-to-grant-your-application-access-to-their-resources"></a>Inschakelen van externe gebruikers op uw App toegang verlenen tot hun bronnen
Als u een toepassing die u beschikbaar wilt maken voor uw klanten of partners buiten uw organisatie schrijft, moet u de definitie van de toepassing in de Azure portal bijwerken.

> [!NOTE]
> Als u meerdere tenants inschakelt, moet u ervoor zorgen dat uw toepassing App ID URI in een geverifieerd domein behoort. Bovendien moet de retour-URL beginnen met https://. Zie voor meer informatie [toepassingsobjecten en Service-Principal objecten](active-directory-application-objects.md).
> 
> 

Toegang tot uw app voor externe gebruikers inschakelen: 

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Uw account selecteren in de rechterbovenhoek van de pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de toepassing die u wilt configureren. Dit wordt gaat u naar de pagina Quick Start van de toepassing, evenals de blade instellingen voor de toepassing geopend.
4. Klik op de blade instellingen **eigenschappen** en spiegelen de **Multi-verpachte** overschakelen naar **Ja**.

Zodra u de bovenstaande wijziging hebt aangebracht, zich gebruikers en beheerders van andere organisaties naar uw App toegang verlenen tot de directory en andere gegevens.

#### <a name="triggering-the-azure-ad-consent-framework-at-runtime"></a>Activering van het Azure AD toestemming framework tijdens runtime
Voor het gebruik van het framework toestemming moeten multitenant-clienttoepassingen aanvragen autorisatie met behulp van OAuth 2.0. [Codevoorbeelden](https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multi-tenant) om weer te geven hoe een webtoepassing, systeemeigen toepassing of server/daemon toepassing aanvragen autorisatiecodes en toegangstokens aanroepen van web-API's beschikbaar zijn.

Een registratie ervaring voor gebruikers kan ook worden geboden door uw webtoepassing. Als u een registratie-ervaring bieden, verwacht wordt dat de gebruiker wordt klikt u op een knop aanmelden bij dat de browser van de Azure AD-OAuth2.0 omleiding eindpunt of een eindpunt met OpenID Connect gebruikersgegevens machtigen. Deze eindpunten toe dat de toepassing voor informatie over de nieuwe gebruiker door de id_token te bekijken. Na de aanmelding fase de gebruiker krijgt een instemmingsprompt lijkt op de hierboven weergegeven in het overzicht van de sectie Framework toestemming geeft.

U kunt ook kan uw webtoepassing bieden ook een werkwijze die beheerders kunnen de 'Mijn bedrijf aanmelden'. Deze ervaring zou ook de gebruiker omgeleid naar de Azure AD-OAuth 2.0 autoriseren eindpunt. In dit geval echter het doorgeven van een prompt = admin_consent parameter naar het geautoriseerde eindpunt om af te dwingen de toestemming ervaring van de beheerder, waar de beheerder toestemming namens hun organisatie verleent. Alleen een gebruiker die verifieert met een account dat bij de rol globale beheerder hoort krijgt toestemming; anderen wordt er een foutbericht. Op geslaagde toestemming het antwoord bevat admin_consent = true. Wanneer een toegangstoken wisselt, ontvangt u ook een id_token die informatie over de organisatie bevatten en de beheerder die aangemeld voor uw toepassing.

### <a name="enabling-oauth-20-implicit-grant-for-single-page-applications"></a>Inschakelen van OAuth verlenen 2.0 impliciete voor toepassingen met één pagina
Één pagina van de toepassing (kuuroorden) worden doorgaans met een JavaScript-zware front-end die wordt uitgevoerd in de browser, die weer van de toepassing web-API aanroept end om uit te voeren van de bedrijfslogica voor gestructureerde. Voor kuuroorden gehost in Azure AD, kunt u OAuth 2.0 impliciete Grant gebruiken voor het verifiëren van de gebruiker met Azure AD en verkrijgen van een token dat u beveiligde gesprekken van JavaScript-client van de toepassing aan de back-end-web-API kunt. Nadat de gebruiker heeft toestemming verleend, kan dit dezelfde authenticatieprotocol aanroepen tussen de client en andere web API-resources die zijn geconfigureerd voor de toepassing beveiligen-tokens verkrijgen worden gebruikt. Zie voor meer informatie over de impliciete authorization grant en kunt u bepalen of deze geschikt voor uw toepassingsscenario is, [inzicht in de impliciete OAuth2 stroom in Azure Active Directory verlenen ](active-directory-dev-understanding-oauth2-implicit-grant.md).

Impliciete Grant OAuth 2.0 is standaard uitgeschakeld voor toepassingen. U kunt de impliciete OAuth 2.0-Grant voor uw toepassing inschakelen door in te stellen de `oauth2AllowImplicitFlow` waarde in de [toepassingsmanifest](active-directory-application-manifest.md), dit is een JSON-bestand met de configuratie van de identiteit van uw toepassing.

#### <a name="to-enable-oauth-20-implicit-grant"></a>Impliciete OAuth 2.0-grant inschakelen
1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Uw account selecteren in de rechterbovenhoek van de pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de toepassing die u wilt configureren. Dit wordt gaat u naar de pagina Quick Start van de toepassing, evenals de blade instellingen voor de toepassing geopend.
4. Klik op de toepassingspagina **Manifest** om het manifest inline-editor te openen.
   Zoek en stel de waarde 'oauth2AllowImplicitFlow' op 'true'. Standaard is het 'false'.
   
    `"oauth2AllowImplicitFlow": true,`
5. Sla het bijgewerkte manifest. Wanneer opgeslagen, wordt uw web-API is nu geconfigureerd voor het gebruik van OAuth 2.0 impliciete Grant om gebruikers te verifiëren.


## <a name="removing-an-application"></a>Een toepassing verwijderen
Deze sectie wordt beschreven hoe een toepassing verwijderen van uw Azure AD-tenant.

### <a name="removing-an-application-authored-by-your-organization"></a>Verwijderen van een toepassing die is geschreven door uw organisatie
Dit zijn de toepassingen die worden weergegeven onder het filter 'Toepassingen mijn bedrijf eigenaar' op de hoofdpagina van 'Toepassingen' voor uw Azure AD-tenant. Dit zijn toepassingen die u handmatig via de klassieke Azure portal of via een programma via PowerShell of de Graph API geregistreerd in technische voorwaarden. Meer specifiek, worden ze weergegeven door een toepassing en Service-Principal object in uw tenant. Zie [toepassingsobjecten en Service-Principal objecten](active-directory-application-objects.md) voor meer informatie.

#### <a name="to-remove-a-single-tenant-application-from-your-directory"></a>Een toepassing voor één tenant verwijderen uit uw directory
1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Uw account selecteren in de rechterbovenhoek van de pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de toepassing die u wilt configureren. Dit wordt gaat u naar de pagina Quick Start van de toepassing, evenals de blade instellingen voor de toepassing geopend.
4. Klik op de toepassingspagina **verwijderen**.
5. Klik op **Ja** in het bevestigingsbericht.

#### <a name="to-remove-a-multi-tenant-application-from-your-directory"></a>Een multitenant-toepassing verwijderen uit de map
1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Uw account selecteren in de rechterbovenhoek van de pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de toepassing die u wilt configureren. Dit wordt gaat u naar de pagina Quick Start van de toepassing, evenals de blade instellingen voor de toepassing geopend.
4. Kies in de blade instellingen **eigenschappen** en spiegelen de **Multi-verpachte** overschakelen naar **Nee**. Hiermee zet u de toepassing kan één tenant, maar de toepassing blijven bestaan in een organisatie die al wil deze.
5. Klik op de **verwijderen** knop van de toepassingspagina.
6. Klik op **Ja** in het bevestigingsbericht.

### <a name="removing-a-multi-tenant-application-authorized-by-another-organization"></a>Verwijderen van een multitenant-toepassing geautoriseerd door een andere organisatie
Dit zijn een subset van de toepassingen die worden weergegeven onder het filter 'Toepassingen mijn bedrijf gebruikt' op de pagina belangrijkste 'toepassingen' voor uw Azure AD-tenant, specifiek voor de waarden die niet worden vermeld in de lijst 'Toepassingen mijn bedrijf eigenaar'. Dit zijn multitenant-toepassingen die zijn geregistreerd tijdens het proces toestemming in technische voorwaarden. Meer specifiek, worden ze weergegeven door alleen een Service-Principal-object in uw tenant. Zie [toepassingsobjecten en Service-Principal objecten](active-directory-application-objects.md) voor meer informatie.

Om het verwijderen van de toepassing van een multitenant-toegang tot uw directory (na heeft toestemming verleend), moet de company administrator om de toegang via de Azure portal een Azure-abonnement hebben. U kunt ook de company administrator kunt gebruiken de [Azure AD PowerShell-Cmdlets](http://go.microsoft.com/fwlink/?LinkId=294151) om toegang te verwijderen.

## <a name="next-steps"></a>Volgende stappen
* Zie de [huisstijl richtlijnen voor geïntegreerde Apps](active-directory-branding-guidelines.md) voor tips over visual richtlijnen voor uw app.
* Zie voor meer informatie over de relatie tussen de toepassing en Service-Principal objecten van een toepassing, [toepassingsobjecten en Service-Principal objecten](active-directory-application-objects.md).
* Zie voor meer informatie over de rol van de app-manifest wordt afgespeeld, [inzicht in de Azure Active Directory-toepassingsmanifest](active-directory-application-manifest.md)
* Zie de [verklarende woordenlijst voor Azure AD-ontwikkelaar](active-directory-dev-glossary.md) voor definities van de concepten voor ontwikkelaars van core Azure Active Directory (AD).
* Ga naar de [ontwikkelaarshandleiding Active Directory](active-directory-developers-guide.md) voor een overzicht van alle developer verwante inhoud.

