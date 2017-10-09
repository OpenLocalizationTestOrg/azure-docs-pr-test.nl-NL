---
title: aaaIntegrating toepassingen met Azure Active Directory | Microsoft Docs
description: Informatie over hoe de tooadd, bijwerken of verwijderen van een toepassing in Azure Active Directory (Azure AD).
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
ms.openlocfilehash: c6bf1123bb3a4d78b55c1c55558e684fb844e687
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-applications-with-azure-active-directory"></a>Toepassingen integreren met Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Ontwikkelaars van ondernemingen en software-as-a-service (SaaS)-providers kunnen ontwikkelen commerciële cloudservices of line-of-business-toepassingen die kunnen worden geïntegreerd met Azure Active Directory (Azure AD) tooprovide veilig aanmelden en autorisatie voor hun Services. toointegrate een toepassing of service met Azure AD, moet een ontwikkelaar Hallo details over de toepassing eerst registreren bij Azure AD via Hallo klassieke Azure-portal.

Dit artikel ziet u hoe de tooadd, bijwerken of verwijderen van een toepassing in Azure AD. U vindt u informatie over de verschillende typen toepassingen die kunnen worden geïntegreerd met Azure AD, hoe Hallo tooconfigure uw toepassingen tooaccess andere resources, zoals web-API's en meer.

Zie toolearn meer informatie over Hallo twee Azure AD-objecten die een geregistreerde toepassing en het Hallo-relatie tussen deze twee, vertegenwoordigen [toepassingsobjecten en Service-Principal objecten](active-directory-application-objects.md); meer informatie over richtlijnen huisstijl Hallo toolearn u moet gebruiken bij het ontwikkelen van toepassingen met Azure Active Directory, raadpleegt u [huisstijl richtlijnen voor geïntegreerde Apps](active-directory-branding-guidelines.md).

## <a name="adding-an-application"></a>Een toepassing toevoegen
Alle toepassingen die toouse Hallo mogelijkheden van Azure AD wil moet eerst worden geregistreerd in een Azure AD-tenant. Het registratieproces omvat met Azure AD gedetailleerde informatie over uw toepassing, zoals Hallo URL op waar deze zich bevindt, URL toosend antwoorden Hallo nadat een gebruiker is geverifieerd, Hallo URI die Hallo app, enzovoort identificeert.

Als u een webtoepassing die u moet net toosupport aanmelden voor gebruikers in Azure AD maakt, kunt u eenvoudig hello onderstaande instructies volgen. Als uw toepassing moet referenties of machtigingen tooaccess tooa web-API of tooallow gebruikers van andere moet Azure AD tooaccess tenants, Zie [bijwerken van een toepassing](#updating-an-application) sectie toocontinue configureren van uw toepassing.

### <a name="tooregister-a-new-application-in-hello-azure-portal"></a>tooregister een nieuwe toepassing in hello Azure-portal
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD-tenant.
3. In Hallo links navigatiedeelvenster kiest **meer Services**, klikt u op **App registraties**, en klik op **toevoegen**.
4. Volg de aanwijzingen Hallo en maak een nieuwe toepassing. Als u specifieke voorbeelden voor webtoepassingen of systeemeigen toepassingen wilt, Bekijk onze [snelstartgidsen](active-directory-developers-guide.md).
  * Geef voor webtoepassingen, Hallo **aanmeldings-URL**, namelijk Hallo basis-URL van uw app, waar gebruikers bijvoorbeeld kunnen aanmelden `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Voor systeemeigen toepassingen bieden een **omleidings-URI**, welke Azure AD gebruikt tooreturn token antwoorden. Voer een waarde specifieke tooyour-toepassing. bijvoorbeeld`http://MyFirstAADApp`
5. Zodra u inschrijving hebt voltooid, wijst Azure AD van uw toepassing een unieke client-id en het Hallo-id van toepassing. Uw toepassing is toegevoegd en gaat u toohello snel starten-pagina voor uw toepassing. Afhankelijk van of uw toepassing een web- of systeemeigen toepassing is, worden er verschillende opties voor het tooadd aanvullende mogelijkheden tooyour toepassing. Wanneer uw toepassing is toegevoegd, kunt u beginnen met het bijwerken van uw toepassing tooenable gebruikers toosign in toegang tot web-API's in andere toepassingen of multitenant-toepassing (waarmee de tooaccess van andere organisaties uw toepassing) configureren.

> [!NOTE]
> Registratie van de toepassing hello nieuw gemaakt is standaard geconfigureerd tooallow gebruikers van uw directory toosign in tooyour toepassing.
> 
> 

## <a name="updating-an-application"></a>Bijwerken van een toepassing
Als uw toepassing met Azure AD is geregistreerd, kan het nodig zijn bijgewerkt toobe tooprovide access tooweb API's, beschikbaar gesteld in andere organisaties en meer. Deze sectie beschrijft de verschillende manieren waarop in die u tooconfigure uw toepassing verder wellicht. Eerst begint we met een overzicht van Hallo toestemming Framework, dit is belangrijk toounderstand als u bij het bouwen van resource/API-toepassingen die worden gebruikt door clienttoepassingen gebouwd door ontwikkelaars in uw organisatie of een andere organisatie.

Voor meer informatie over Hallo manier verificatie in Azure AD, gaat u [verificatie scenario's voor Azure AD](active-directory-authentication-scenarios.md).

### <a name="overview-of-hello-consent-framework"></a>Overzicht van Hallo toestemming framework
Azure AD toestemming framework maakt het eenvoudig toodevelop multitenant web en native clienttoepassingen die tooaccess moeten web-API's die zijn beveiligd door een Azure AD-tenant, verschilt van Hallo een waar de client-toepassing hello is geregistreerd. Deze web-API's Hallo Microsoft Graph API (tooaccess Azure Active Directory, Intune en services in Office 365) en andere Microsoft-services API's omvatten, maar daarnaast tooyour eigenaar van web-API's. Hallo-framework is gebaseerd op een gebruiker of beheerder waarbij toestemming tooan toepassing waarin u wordt gevraagd toobe geregistreerd in de directory, waarbij toegang tot Active directory-gegevens.

Als een client-toepassing tooread agenda-informatie over de gebruiker Hallo vanuit Office 365 moet, wordt die gebruiker vereist tooconsent toohello clienttoepassing worden. Nadat u toestemming is opgegeven, wordt Hallo-clienttoepassing kunnen toocall Hallo Microsoft Graph API namens de gebruiker Hallo worden en Hallo agenda-informatie gebruiken indien nodig. Hallo [Microsoft Graph API](https://graph.microsoft.io) biedt toegang tot toodata in Office 365 (zoals agenda's en berichten van Exchange, sites en lijsten van SharePoint, documenten van OneDrive, taken van de Planner werkmappen van OneNote-notitieblokken Excel-, enz.), evenals de gebruikers en groepen van Azure AD en andere gegevensobjecten van meer Microsoft-cloudservices. 

Hallo toestemming framework is gebouwd op OAuth 2.0 en de verschillende stromen, zoals de autorisatiecode verlenen en client referenties verlenen, met behulp van openbare of vertrouwelijke clients. Met behulp van OAuth 2.0, Azure AD maakt het mogelijk toobuild veel verschillende soorten clienttoepassingen, zoals zoals op een telefoon, tablet, server of een webtoepassing en toegang krijgen tot bronnen toohello vereist.

Zie voor meer informatie over Hallo toestemming framework, [OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx), [verificatie scenario's voor Azure AD](active-directory-authentication-scenarios.md), en voor informatie over het ophalen van geautoriseerde toegang tooOffice 365 via Microsoft Graph Zie [App verificatie met Microsoft Graph](https://graph.microsoft.io/docs/authorization/auth_overview).

#### <a name="example-of-hello-consent-experience"></a>Voorbeeld van Hallo toestemming ervaring
Hallo ziet volgende stappen u hoe Hallo toestemming experience werkt voor zowel de ontwikkelaar van de toepassing hello en de gebruiker.

1. Ingesteld op de configuratiepagina van uw web-client-toepassing in Azure-portal Hallo Hallo machtigingen die vereist zijn voor uw toepassing met behulp van menu's Hallo in Hallo sectie machtigingen vereist.
   
    ![Machtigingen tooother toepassingen](./media/active-directory-integrating-applications/requiredpermissions.png)
2. Houd rekening met dat uw toepassing worden machtigingen zijn bijgewerkt, Hallo toepassing wordt uitgevoerd en een gebruiker over toouse het voor Hallo eerst is. Als de toepassing hello niet al een toegang of vernieuwd token, Hallo toepassing verkregen moet toogo tooAzure van AD autorisatie eindpunt tooobtain een autorisatiecode die gebruikt tooacquire worden kan een nieuwe toegang en een vernieuwingstoken.
3. Als de gebruiker Hallo niet al is geverifieerd, wordt hen gevraagd toosign in tooAzure AD.
   
    ![Gebruiker of beheerder aanmelden tooAzure AD](./media/active-directory-integrating-applications/usersignin.png)
4. Nadat het Hallo-gebruiker is aangemeld, kan Azure AD wordt bepaald of Hallo gebruiker toobe weergegeven van een pagina toestemming moet. Deze beslissing is gebaseerd op welke Hallo gebruiker (of de beheerder van hun organisatie) is al toegekend Hallo toepassing toestemming. Toestemming heeft geen toestemming gekregen, Azure AD wordt Hallo gebruiker om toestemming gevraagd als Hallo vereist machtigingen toofunction moet worden weergegeven. Hallo reeks machtigingen die wordt weergegeven in het dialoogvenster voor Hallo toestemming zijn Hallo overeen met wat in Hallo gedelegeerde machtigingen in hello Azure-portal is geselecteerd.
   
    ![Toestemming gebruikerservaring](./media/active-directory-integrating-applications/consent.png)
5. Nadat de gebruiker Hallo toestemming verleent, wordt een autorisatiecode tooyour-toepassing die u kunt verzilverde tooacquire een toegangstoken en vernieuwen van token geretourneerd. Zie voor meer informatie over deze stroom Hallo [web-API tooweb toepassingsgedeelte](active-directory-authentication-scenarios.md#web-application-to-web-api) in sectie [verificatie scenario's voor Azure AD](active-directory-authentication-scenarios.md).

6. Als beheerder, kunt u ook gedelegeerde machtigingen van de toepassing tooan namens alle Hallo gebruikers toestemming in uw tenant. Dit wordt voorkomen dat Hallo toestemming dialoogvenster wordt weergegeven voor elke gebruiker in Hallo-tenant. U kunt dit doen vanuit Hallo [Azure-portal](https://portal.azure.com) vanaf de toepassingspagina. Van Hallo **instellingen** blade voor uw toepassing, klikt u op **Required Permissions** en klik op Hallo **machtiging verlenen** knop. 

    ![Machtigingen voor expliciete admin toestemming verlenen](./media/active-directory-integrating-applications/grantpermissions.png)
    
> [!NOTE]
> Expliciete verlenen met Hallo **machtiging verlenen** knop is momenteel vereist zijn voor één pagina toepassingen (SPA) met behulp van ADAL.js, zoals Hallo toegangstoken is aangevraagd zonder een instemmingsprompt, mislukken als toestemming niet is al toegekend.   

### <a name="configuring-a-client-application-tooaccess-web-apis"></a>Configureren van een client toepassing tooaccess-web-API 's
Om een web/vertrouwelijke client toepassing toobe kunnen tooparticipate in een machtiging grant-stroom die verificatie vereist is (en verkrijgen van een toegangstoken), moet deze beveiligde referenties maken. Hallo standaardmethode voor verificatie wordt ondersteund door hello Azure-portal is de Client-ID + symmetrische sleutel. Deze sectie wordt uitgelegd hoe Hallo configuratie stappen vereist tooprovide Hallo geheime sleutel van uw client-referenties.

Bovendien voordat een client kan toegang tot een web-API die worden weergegeven door een resource-toepassing (ie: Microsoft Graph API), Hallo toestemming framework waarborgt Hallo-client verkrijgt Hallo machtiging grant Hallo vereist, op basis van machtigingen die zijn aangevraagd. Standaard kunt alle toepassingen machtigingen van Azure Active Directory (Graph API) en Azure Service Management API met Azure AD Hallo 'aanmelding bij het inschakelen en lezen gebruikersprofiel' machtiging standaard al geselecteerd. Als u de clienttoepassing wordt geregistreerd in een Office 365 Azure AD-tenant, web-API's en machtigingen voor SharePoint en Exchange Online worden ook beschikbaar voor selectie. U kunt kiezen uit [twee soorten machtigingen](active-directory-dev-glossary.md#permissions) in Hallo vervolgkeuzelijsten volgende toohello gewenst web-API:

* Toepassingsmachtigingen: Uw clienttoepassing moet tooaccess Hallo web-API als zelf (geen gebruikerscontext). Dit type machtiging beheerder toestemming nodig en is ook niet beschikbaar voor systeemeigen clienttoepassingen.
* Gedelegeerde machtigingen: Uw clienttoepassing moet tooaccess Hallo web-API als Hallo aangemelde gebruiker, maar met de toegang beperkt door de machtiging Hallo geselecteerd. Dit type machtigingen kan worden verleend door een gebruiker tenzij Hallo machtiging is geconfigureerd als het vereisen van instemming met de beheerder. 

> [!NOTE]
> Een gedelegeerde machtigingen tooan toepassing toe te voegen verleent automatisch geen toestemming toohello gebruikers binnen Hallo-tenant, zoals in Hallo klassieke Azure-Portal. Hallo gebruikers moeten nog steeds handmatig toestemming geven voor Hallo toegevoegd machtigingen tijdens runtime overgedragen, tenzij Hallo beheerder klikt op Hallo **machtiging verlenen** knop van Hallo **Required Permissions** sectie van Hallo pagina van de toepassing in hello Azure-portal. 

#### <a name="tooadd-credentials-or-permissions-tooaccess-web-apis"></a>tooadd referenties of machtigingen tooaccess web-API 's
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu hello, **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de gewenste tooconfigure Hallo-toepassing. Dit zal duren voordat u de Quick Start-pagina van de toepassing van de toohello, evenals Hallo blade voor instellingen voor de toepassing hello geopend.
4. tooadd een geheime sleutel voor uw webtoepassing referenties, klikt u op Hallo 'Sleutels' sectie van de blade instellingen Hallo.  
   
   * Een beschrijving voor uw sleutel toevoegen en selecteer een 1 of 2 jaar duur. 
   * Hallo meest rechtse kolom bevat sleutelwaarde hello, nadat u de configuratiewijzigingen Hallo opgeslagen. Ervoor toocome weer worden toothis sectie en kopieer het nadat u raakt opslaan, zodat u deze voor gebruiken in uw clienttoepassing tijdens de verificatie tijdens runtime.
5. tooadd serverprincipal tooaccess resource API's van de client, klikt u op Hallo 'Required Permissions' sectie van de blade instellingen Hallo. 
   
   * Klik eerst Hallo "Toevoegen" knop.
   * Klik op 'Selecteer een API' tooselect Hallo type bronnen die u wilt toopick uit.
   * Blader door Hallo lijst met beschikbare API's of Hallo zoeken vak tooselect van Hallo beschikbare resource toepassingen in uw directory die een web-API gebruiken. Klik op Hallo resource u geïnteresseerd bent in en klik vervolgens op **Selecteer**.
   * Zodra u hebt geselecteerd, kunt u toohello **Selecteer machtigingen** menu waar u Hallo ' toepassing ' en 'Overgedragen machtigingen' voor uw toepassing selecteren kunt.
   
6. Wanneer u klaar bent, klikt u op Hallo **gedaan** knop.

> [!NOTE]
> Te klikken op Hallo **gedaan** knop worden ook automatisch Hallo machtigingen ingesteld voor uw toepassing in uw directory op basis van Hallo machtigingen tooother toepassingen die u hebt geconfigureerd.  U kunt deze Toepassingsmachtigingen weergeven door te kijken toepassing hello **instellingen** blade.
> 
> 

### <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Configureren van een resource toepassing tooexpose-web-API 's
U kunt een web-API ontwikkelen en toepassingen beschikbaar tooclient bij het blootstellen van toegang [scopes](active-directory-dev-glossary.md#scopes) en [rollen](active-directory-dev-glossary.md#roles). Een juist geconfigureerde web-API wordt beschikbaar gemaakt, net zoals andere Microsoft-web-API's, waaronder Hallo Graph API Hallo en Hallo Office 365-API's. Toegangsbereiken en rollen worden weergegeven via uw [van toepassingsmanifest](active-directory-dev-glossary.md#application-manifest), dit is een JSON-bestand met de configuratie van de identiteit van uw toepassing.  

Hallo volgende sectie leert u hoe tooexpose toegang scopes doordat Hallo resource application manifest.

#### <a name="adding-access-scopes-tooyour-resource-application"></a>Toegang scopes tooyour resource toepassing toe te voegen
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu hello, **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de gewenste tooconfigure Hallo-toepassing. Dit zal duren voordat u de Quick Start-pagina van de toepassing van de toohello, evenals Hallo blade voor instellingen voor de toepassing hello geopend.
4. Klik op **Manifest** van Hallo toepassing pagina tooopen Hallo inline manifest-editor. 
5. Knooppunt "oauth2Permissions" vervangen door Hallo volgende JSON-codefragment. Dit fragment is een voorbeeld van hoe tooexpose een scope bekend als 'gebruikersimitaties', waarmee een resource-eigenaar toogive een clienttoepassing een type toegang tooa resource overgedragen. Zorg ervoor dat u de tekst hello en waarden voor uw eigen toepassing wijzigt:
   
        "oauth2Permissions": [
        {
            "adminConsentDescription": "Allow hello application full access toohello Todo List service on behalf of hello signed-in     user",
            "adminConsentDisplayName": "Have full access toohello Todo List service",
            "id": "b69ee3c9-c40d-4f2a-ac80-961cd1534e40",
            "isEnabled": true,
            "type": "User",
            "userConsentDescription": "Allow hello application full access toohello todo service on your behalf",
            "userConsentDisplayName": "Have full access toohello todo service",
            "value": "user_impersonation"
            }
        ],
   
    Hallo id-waarde moet een nieuwe gegenereerde GUID die u met behulp van maakt een [GUID generatie hulpprogramma](https://msdn.microsoft.com/library/ms241442%28v=vs.80%29.aspx) of via een programma. Hiermee geeft u een unieke id voor het Hallo-machtiging die wordt blootgelegd door Hallo web-API. Zodra de client op de juiste wijze is geconfigureerd toorequest toegang tooyour web-API en aanroepen Hallo web-API, deze biedt een OAuth 2.0 JWT-token dat Hallo bereik (scp) set toohello claimwaarde bovenstaande dat in dit geval user_impersonation heeft.
   
   > [!NOTE]
   > Extra scopes later zo nodig kan worden blootgesteld. U kunt uw web-API kan meerdere scopes die zijn gekoppeld met tal van verschillende functies worden blootgesteld. U kunt nu toegang toohello web-API met behulp van Hallo-bereik (scp) claim in Hallo ontvangen OAuth 2.0 JWT-token beheren.
   > 
   > 
6. Klik op **opslaan** toosave Hallo manifest. Uw web-API is nu geconfigureerd toobe gebruikt door andere toepassingen in uw directory.

#### <a name="tooverify-hello-web-api-is-exposed-tooother-applications-in-your-directory"></a>tooverify Hallo-web-API is blootgestelde tooother toepassingen in uw directory
1. Klik op het bovenste menu Hallo **App registraties**, selecteer Hallo gewenst clienttoepassing die u wilt tooconfigure toegang toohello web-API en de blade instellingen toohello navigeren.
2. Van Hallo **Required Permissions** sectie, selecteert u Hallo web-API die u zojuist hebt een machtiging voor beschikbaar gesteld. Hallo gedelegeerde machtigingen vervolgkeuzelijst, selecteer Hallo nieuwe machtiging.

![Takenlijst machtigingen worden weergegeven.](./media/active-directory-integrating-applications/todolistpermissions.png)

#### <a name="more-on-hello-application-manifest"></a>Meer informatie over het Hallo-toepassingsmanifest
Hallo-toepassingsmanifest wordt daadwerkelijk fungeert als een mechanisme voor het bijwerken van entiteit Hallo toepassing waarin alle kenmerken van configuratie van een Azure AD-toepassing identiteit, Hallo API-toegangsbereiken besproken. Zie voor meer informatie over Hallo entiteit toepassing hello [Graph API-toepassing entiteit documentatie](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity). In dit vindt u volledige naslaginformatie over Hallo entiteit leden gebruikt toospecify Toepassingsmachtigingen voor uw API:  

* Hallo appRoles lid, een verzameling is van [AppRole](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type) entiteiten die gebruikt toodefine hello worden kunnen **Toepassingsmachtigingen** voor een web-API  
* Hallo oauth2Permissions lid, een verzameling is van [OAuth2Permission](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type) entiteiten die gebruikt toodefine hello worden kunnen **gedelegeerde machtigingen** voor een web-API

Voor meer informatie over application manifest concepten over het algemeen Raadpleeg te[Understanding hello Azure Active Directory-toepassingsmanifest](active-directory-application-manifest.md).

### <a name="accessing-hello-azure-ad-graph-and-office-365-via-microsoft-graph-apis"></a>Toegang tot Azure AD Graph Hallo en Office 365 via Microsoft Graph-API 's  
Als genoemde eerdere, Daarnaast tooexposing/toegang tot API's op uw eigen toepassingen resource, kunt u ook uw client-toepassing tooaccess API's die worden weergegeven door de Microsoft-bronnen bijwerken.  Hallo Microsoft Graph API die 'Microsoft Graph' in de lijst Hallo van machtigingen tooother toepassingen wordt genoemd, beschikbaar is of alle toepassingen die zijn geregistreerd bij Azure AD. Als u de clienttoepassing in een Azure AD-tenant die is ingericht door Office 365 registreert, u kunt ook toegang tot alle Hallo machtigingen die worden weergegeven door Hallo Microsoft Graph API toovarious Office 365-resources.

Zie voor een volledige bespreking van de toegangsbereiken beschikbaar is gemaakt door Microsoft Graph API, Hallo [-machtigingsbereiken | Microsoft Graph API concepten](https://graph.microsoft.io/docs/authorization/permission_scopes) artikel.

> [!NOTE]
> Vanwege de huidige beperking tooa, kunnen native client-toepassingen alleen aanroepen in Azure AD Graph API Hallo als ze Hallo 'Toegang tot de directory van uw organisatie' machtiging gebruiken.  Deze beperking geldt niet voor webtoepassingen.
> 
> 

### <a name="configuring-multi-tenant-applications"></a>Multitenant-toepassingen configureren
Wanneer u een toepassing tooAzure AD toevoegt, kunt u uw toepassing toobe alleen toegankelijk voor gebruikers in uw organisatie. U kunt ook uw toepassing toobe toegankelijk is voor gebruikers in externe organisaties. Deze twee toepassingstypen worden één tenant en multitenant-toepassingen genoemd. Hallo-configuratie van een toepassing één tenant toomake kunt u deze een multitenant-toepassing in deze sectie wordt beschreven hieronder.

Het is belangrijk toonote Hallo verschillen tussen een één tenant en multitenant-toepassing:  

* Een toepassing voor één tenant is bedoeld voor gebruik in een organisatie. Ze zijn doorgaans een line-of-business (LoB)-toepassing geschreven door de ontwikkelaar van een onderneming. Een toepassing voor één tenant moet alleen toobe waartoe gebruikers in een map en als gevolg hiervan, alleen moet toobe ingericht in één directory.
* Een multitenant-toepassing is bedoeld voor gebruik in veel organisaties. Een software-as-a-service (SaaS)-webtoepassing die meestal geschreven door een onafhankelijke softwareleverancier (ISV) zijn. Multitenant-toepassingen moeten toobe ingericht in elke map waar ze worden gebruikt, waarvoor een gebruiker of beheerder toestemming tooregister ze ondersteund via hello Azure AD toestemming framework. Houd er rekening mee dat alle systeemeigen clienttoepassingen multitenant standaard zijn als ze zijn geïnstalleerd op Hallo resource-eigenaar van apparaat. Zie Hallo overzicht van Hallo toestemming Framework sectie hierboven voor meer informatie over Hallo toestemming framework.

#### <a name="enabling-external-users-toogrant-your-application-access-tootheir-resources"></a>Inschakelen van externe gebruikers toogrant uw toepassing toegang tootheir resources
Als u een toepassing u wilt toomake beschikbaar tooyour klanten of partners buiten uw organisatie schrijft, moet u tooupdate Hallo definitie in hello Azure-portal.

> [!NOTE]
> Als u meerdere tenants inschakelt, moet u ervoor zorgen dat uw toepassing App ID URI in een geverifieerd domein behoort. Bovendien hello die retour-URL met https:// beginnen moet. Zie voor meer informatie [toepassingsobjecten en Service-Principal objecten](active-directory-application-objects.md).
> 
> 

tooenable access tooyour-app voor externe gebruikers: 

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu hello, **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de gewenste tooconfigure Hallo-toepassing. Dit zal duren voordat u de Quick Start-pagina van de toepassing van de toohello, evenals Hallo blade voor instellingen voor de toepassing hello geopend.
4. Blade Hallo-instellingen, klik op **eigenschappen** en spiegelen Hallo **Multi-verpachte** te schakelen**Ja**.

Nadat u hebt aangebracht Hallo wijzigen hierboven, gebruikers en beheerders van andere organisaties zijn kunnen toogrant uw toepassing toegang tootheir directory en andere gegevens.

#### <a name="triggering-hello-azure-ad-consent-framework-at-runtime"></a>Activering van hello Azure AD toestemming framework tijdens runtime
toouse hello toestemming framework multitenant clienttoepassingen moeten verificatie met OAuth 2.0 aanvragen. [Codevoorbeelden](https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multi-tenant) zijn beschikbaar tooshow u hoe een webtoepassing, de systeemeigen toepassing of de server/daemon toepassing aanvragen autorisatie codes en toegang tot toocall tokens web-API's.

Een registratie ervaring voor gebruikers kan ook worden geboden door uw webtoepassing. Als u een registratie-ervaring bieden, zouden dat die gebruiker hello wordt klikt u op een knop aanmelden bij dat omleiding Hallo browser toohello Azure AD OAuth2.0 eindpunt of een eindpunt met OpenID Connect gebruikersgegevens machtigen. Deze eindpunten toestaan Hallo toepassing tooget informatie over de nieuwe gebruiker Hallo door Hallo id_token te bekijken. Na registratie fase Hallo Hallo gebruiker krijgt een toestemming vragen vergelijkbare toohello melding hierboven in Hallo overzicht van Hallo toestemming Framework-sectie.

U kunt ook kan uw webtoepassing bieden ook een werkwijze die beheerders te 'Mijn bedrijf aanmelden'. Deze ervaring zou ook omleiden Hallo gebruiker toohello Azure AD OAuth 2.0 autoriseren eindpunt. In dit geval echter het doorgeven van een prompt = admin_consent parameter toohello autoriseren eindpunt tooforce Hallo beheerder toestemming ervaring, waarbij Hallo beheerder verleent toestemming namens hun organisatie. Alleen een gebruiker die verifieert met een account dat deel uitmaakt van de globale beheerdersrol toohello krijgt toestemming; anderen wordt er een foutbericht. Op geslaagde toestemming Hallo-antwoord bevat admin_consent = true. Wanneer een toegangstoken wisselt, ontvangt u ook een id_token die informatie over Hallo-organisatie bevatten en het Hallo-beheerder hebt aangemeld voor uw toepassing.

### <a name="enabling-oauth-20-implicit-grant-for-single-page-applications"></a>Inschakelen van OAuth verlenen 2.0 impliciete voor toepassingen met één pagina
Doorgaans structuur van één pagina van de toepassing (kuuroorden) met een JavaScript-zware front-end die in Hallo browser, die van de toepassing hello web-API-back-end tooperform de zakelijke logica roept wordt uitgevoerd. Voor kuuroorden gehost in Azure AD, u OAuth 2.0 impliciete Grant tooauthenticate Hallo gebruiker gebruiken met Azure AD en een token waarmee u kunt verkrijgen toosecure teruggebeld uit van de toepassing hello JavaScript client tooits end web-API. Nadat het Hallo-gebruiker heeft toestemming verleend, kan dit dezelfde verificatieprotocol gebruikte tooobtain tokens toosecure aanroepen tussen Hallo-client en andere bronnen web-API is geconfigureerd voor de toepassing hello zijn. Zie toolearn meer informatie over Hallo impliciete authorization grant en helpen u beslissen of deze geschikt is voor uw toepassingsscenario [Understanding Hallo OAuth2 impliciete stroom in Azure Active Directory verlenen ](active-directory-dev-understanding-oauth2-implicit-grant.md).

Impliciete Grant OAuth 2.0 is standaard uitgeschakeld voor toepassingen. Kunt u de impliciete OAuth 2.0-Grant inschakelen voor uw toepassing door de instelling Hallo `oauth2AllowImplicitFlow` waarde in de [toepassingsmanifest](active-directory-application-manifest.md), dit is een JSON-bestand met de configuratie van de identiteit van uw toepassing.

#### <a name="tooenable-oauth-20-implicit-grant"></a>de impliciete grant tooenable OAuth 2.0
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu hello, **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de gewenste tooconfigure Hallo-toepassing. Dit zal duren voordat u de Quick Start-pagina van de toepassing van de toohello, evenals Hallo blade voor instellingen voor de toepassing hello geopend.
4. Klik op de pagina toepassing hello **Manifest** tooopen Hallo inline manifest editor.
   Zoek en Hallo 'oauth2AllowImplicitFlow'-waarde te 'true' ingesteld. Standaard is het 'false'.
   
    `"oauth2AllowImplicitFlow": true,`
5. Hallo bijgewerkt manifest opslaan. Wanneer opgeslagen, worden de toouse impliciete OAuth 2.0-Grant tooauthenticate gebruikers uw web-API is nu geconfigureerd.


## <a name="removing-an-application"></a>Een toepassing verwijderen
Deze sectie beschrijft hoe tooremove van de toepassing in uw Azure AD-tenant.

### <a name="removing-an-application-authored-by-your-organization"></a>Verwijderen van een toepassing die is geschreven door uw organisatie
Dit zijn Hallo-toepassingen die worden weergegeven onder 'Toepassingen mijn bedrijf eigenaar' Hallo-filter op Hallo 'Toepassingen' hoofdpagina voor uw Azure AD-tenant. In technische termen, dit zijn toepassingen die u handmatig via Hallo klassieke Azure-portal of via een programma via PowerShell geregistreerd of Hallo Graph API. Meer specifiek, worden ze weergegeven door een toepassing en Service-Principal object in uw tenant. Zie [toepassingsobjecten en Service-Principal objecten](active-directory-application-objects.md) voor meer informatie.

#### <a name="tooremove-a-single-tenant-application-from-your-directory"></a>een toepassing voor één tenant van uw directory tooremove
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu hello, **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de gewenste tooconfigure Hallo-toepassing. Dit zal duren voordat u de Quick Start-pagina van de toepassing van de toohello, evenals Hallo blade voor instellingen voor de toepassing hello geopend.
4. Klik op de pagina toepassing hello **verwijderen**.
5. Klik op **Ja** in Hallo bevestigingsbericht.

#### <a name="tooremove-a-multi-tenant-application-from-your-directory"></a>een toepassing met meerdere tenants van uw directory tooremove
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD-tenant.
3. Kies in het bovenste menu hello, **Azure Active Directory**, klikt u op **App registraties**, en klik vervolgens op de gewenste tooconfigure Hallo-toepassing. Dit zal duren voordat u de Quick Start-pagina van de toepassing van de toohello, evenals Hallo blade voor instellingen voor de toepassing hello geopend.
4. Kies in de blade beleidinstellingen Hallo **eigenschappen** en spiegelen Hallo **Multi-verpachte** te schakelen**Nee**. Hiermee zet u uw toepassing toobe één tenant, maar de toepassing hello blijven bestaan in een organisatie die al tooit heeft ingestemd.
5. Klik op Hallo **verwijderen** knop van de pagina van de toepassing hello.
6. Klik op **Ja** in Hallo bevestigingsbericht.

### <a name="removing-a-multi-tenant-application-authorized-by-another-organization"></a>Verwijderen van een multitenant-toepassing geautoriseerd door een andere organisatie
Dit zijn een subset van Hallo-toepassingen die voor uw Azure AD-tenant, speciaal Hallo waarden die niet worden vermeld in de lijst met Hallo 'Toepassingen mijn bedrijf eigenaar' onder 'Toepassingen mijn bedrijf gebruikt' Hallo-filter op pagina van de belangrijkste 'toepassingen' Hallo worden weergegeven. Dit zijn multitenant-toepassingen die zijn geregistreerd tijdens Hallo toestemming in technische voorwaarden. Meer specifiek, worden ze weergegeven door alleen een Service-Principal-object in uw tenant. Zie [toepassingsobjecten en Service-Principal objecten](active-directory-application-objects.md) voor meer informatie.

In volgorde tooremove een multitenant-toepassing toegang tooyour directory (na heeft toestemming verleend), Hallo bedrijfsbeheerder moet beschikken over een Azure-abonnement tooremove via hello Azure-portal. Hallo bedrijfsbeheerder kan ook hello gebruiken [Azure AD PowerShell-Cmdlets](http://go.microsoft.com/fwlink/?LinkId=294151) tooremove toegang.

## <a name="next-steps"></a>Volgende stappen
* Zie Hallo [huisstijl richtlijnen voor geïntegreerde Apps](active-directory-branding-guidelines.md) voor tips over visual richtlijnen voor uw app.
* Zie voor meer informatie over de relatie tussen de toepassing en Service-Principal objecten van een toepassing hello [toepassingsobjecten en Service-Principal objecten](active-directory-application-objects.md).
* toolearn meer informatie over Hallo rol Hallo app manifest speelt, Zie [Understanding hello Azure Active Directory-toepassingsmanifest](active-directory-application-manifest.md)
* Zie Hallo [verklarende woordenlijst voor Azure AD-ontwikkelaar](active-directory-dev-glossary.md) voor definities van Hallo core Azure Active Directory (AD)-concepten voor ontwikkelaars.
* Ga naar Hallo [ontwikkelaarshandleiding Active Directory](active-directory-developers-guide.md) voor een overzicht van alle developer verwante inhoud.

