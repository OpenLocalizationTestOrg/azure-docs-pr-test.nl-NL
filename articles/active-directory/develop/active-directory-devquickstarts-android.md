---
title: aaaAzure AD Android aan de slag | Microsoft Docs
description: Hoe beveiligd toobuild een Android-toepassing die met Azure AD voor aanmelden en Azure AD-aanroepen integreert API's met behulp van OAuth.
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a>Azure AD integreren met een Android-app
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Hallo Preview-versie van onze nieuwe [ontwikkelaarsportal](https://identity.microsoft.com/Docs/Android), die helpt u bij leren werken met Azure AD in een paar minuten. Hallo-portal voor ontwikkelaars begeleidt u door Hallo van een app registreren en Azure AD integreren in uw code. Wanneer u klaar bent, hebt u een eenvoudige toepassing die gebruikers in uw tenant en een back-end die kunnen tokens accepteren en gevalideerd kan worden geverifieerd.
>
>

Als u een bureaubladtoepassing ontwikkelt, kunt Azure Active Directory (Azure AD) u eenvoudig en snel voor tooauthenticate u uw gebruikers via hun lokale Active Directory-accounts. Uw toepassing toosecurely ook kunt gebruiken van een web-API die zijn beveiligd door Azure AD, zoals Office 365-API's Hallo of hello Azure API.

Azure AD levert voor Android-clients die tooaccess beveiligde bronnen nodig Hallo Active Directory Authentication Library (ADAL). Hallo enig doel van ADAL toomake is het eenvoudig voor uw app tooget-toegangstokens. hoe eenvoudig het is, gaan we gaat verder met een takenlijst Android-toepassing die toodemonstrate:

* Krijgt toegang tot tokens voor een taak lijst-API aanroept met behulp van Hallo [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* De takenlijst van een gebruiker opgehaald.
* Tekenen van gebruikers.

tooget gestart, moet u een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren. Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a>Stap 1: Download en Hallo Node.js REST-API TODO voorbeeldserver wordt uitgevoerd
Hallo Node.js REST-API TODO voorbeeld geschreven specifiek toowork tegen onze huidige voorbeeld voor het bouwen van een één-tenant taak REST-API voor Azure AD. Dit is een vereiste voor Hallo snel starten.

Voor informatie over hoe tooset dit, Zie onze bestaande voorbeelden in [Microsoft Azure Active Directory-voorbeeld REST API-Service voor Node.js](active-directory-devquickstarts-webapi-nodejs.md).


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>Stap 2: Uw web-API registreren bij uw Azure AD-tenant
Active Directory ondersteunt twee soorten toepassingen toe te voegen:

- Web-API's die worden geboden door services toousers
- Toepassingen (die worden uitgevoerd op Hallo web of op een apparaat) die toegang hebben tot de web-API 's

U bent Hallo web-API die u lokaal worden uitgevoerd voor het testen van dit voorbeeld wordt geregistreerd in deze stap. Deze web-API is normaal gesproken een REST-service die aanbieding functionaliteit die u wilt een app-tooaccess is. Azure AD kunt een willekeurig eindpunt beschermen.

We ervan uit dat u bent u registreert Hallo TODO waarnaar wordt verwezen eerder REST-API. Maar dit werkt voor alle web-API die u wilt dat Azure Active Directory toohelp beveiligen.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op de bovenste balk hello, uw account. In Hallo **Directory** Kies waar u tooregister hello Azure AD-tenant van uw toepassing.
3. Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.
4. Klik op **App registraties**, en selecteer vervolgens **toevoegen**.
5. Een beschrijvende naam voor de toepassing hello (bijvoorbeeld **TodoListService**), selecteer **webtoepassing en/of Web-API**, en klik op **volgende**.
6. Voer voor Hallo aanmeldings-URL, Hallo basis-URL voor Hallo-voorbeeld. Dit is standaard `https://localhost:8080`.
7. Klik op **OK** toocomplete Hallo registratie.
8. Terwijl u nog steeds in hello Azure-portal, Ga tooyour toepassingspagina, Hallo toepassing id-waarde vinden en kopiëren. U hebt dit later nodig bij het configureren van uw toepassing.
9. Van Hallo **instellingen** -> **eigenschappen** pagina, Hallo app ID URI bijwerken - Voer `https://<your_tenant_name>/TodoListService`. Vervang `<your_tenant_name>` met Hallo-naam van uw Azure AD-tenant.

## <a name="step-3-register-hello-sample-android-native-client-application"></a>Stap 3: De voorbeeldtoepassing Android Native Client Hallo registreren
In dit voorbeeld moet u uw webtoepassing registreren. Hiermee kunt uw toepassing toocommunicate met Hallo zojuist hebt geregistreerd web-API. Azure AD weigert tooeven toestaan uw toepassing tooask voor aanmelden, tenzij deze is geregistreerd. Die uitmaakt deel van Hallo beveiliging van Hallo-model.

We ervan uit dat u bent u registreert Hallo voorbeeldtoepassing eerder verwezen. Maar deze procedure werkt voor elke app die u ontwikkelt.

> [!NOTE]
> U vraagt zich misschien af waarom u een toepassing en een web-API wilt opslaan in een tenant. Als u mogelijk hebt geraden, kunt u een app die toegang heeft tot een externe API die is geregistreerd in Azure AD van een andere tenant. Als u dat doet, uw klanten zich tooconsent toohello gebruik van Hallo API in de toepassing hello gevraagd. Active Directory Authentication Library voor iOS zorgt voor deze toestemming voor u. Als we geavanceerdere functies, verkennen, ziet u dat dit een belangrijk onderdeel van Hallo werk nodig tooaccess Hallo suite van Microsoft APIs van Azure en Office, evenals andere serviceprovider is. Op dit moment omdat u zowel uw web-API en uw toepassing onder Hallo geregistreerd dezelfde tenant, ziet u niet de prompts om toestemming. Dit is meestal Hallo geval als u een toepassing alleen voor uw eigen bedrijf toouse ontwikkelt.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op de bovenste balk hello, uw account. In Hallo **Directory** Kies waar u tooregister hello Azure AD-tenant van uw toepassing.
3. Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.
4. Klik op **App registraties**, en selecteer vervolgens **toevoegen**.
5. Een beschrijvende naam voor de toepassing hello (bijvoorbeeld **TodoListClient Android**), selecteer **systeemeigen clienttoepassing**, en klik op **volgende**.
6. Omleidings-URI voor hello, voert u `http://TodoListClient`. Klik op **Voltooien**.
7. Hallo toepassing pagina Hallo toepassing id-waarde vinden en kopiëren. U hebt dit later nodig bij het configureren van uw toepassing.
8. Van Hallo **instellingen** pagina **Required Permissions** en selecteer **toevoegen**.  Zoek en selecteer TodoListService, Hallo toevoegen **toegang TodoListService** machtiging onder **gedelegeerde machtigingen**, en klik op **gedaan**.

toobuild met Maven, kunt u pom.xml op het hoogste niveau hello gebruiken:

1. Deze opslagplaats klonen naar een map van uw keuze:

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Volg de stappen Hallo in Hallo [tooset vereisten van uw omgeving Maven voor Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).
3. Hallo-emulator met de SDK-19 instellen.
4. Ga toohello hoofdmap waar u Hallo-opslagplaats.
5. Deze opdracht uitvoeren:`mvn clean install`
6. Hallo directory toohello Quick Start voorbeeld wijzigen:`cd samples\hello`
7. Deze opdracht uitvoeren:`mvn android:deploy android:run`

   U ziet Hallo app wordt gestart.
8. Voer test gebruiker referenties tootry.

Naast Hallo AAR pakket worden JAR-pakketten verzonden.

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a>Stap 4: Android ADAL Hallo downloaden en deze tooyour Eclipse werkruimte toevoegen
We hebt gemaakt dat u toohave meerdere opties toouse ADAL in uw Android-project:

* U kunt Hallo source code tooimport deze bibliotheek in Eclipse en koppeling tooyour-toepassing.
* Als u Android Studio, kunt u Hallo AAR pakket indeling en verwijzing Hallo binaire bestanden.

### <a name="option-1-source-zip"></a>Optie 1: Bron Zip
toodownload een kopie van de broncode hello, klikt u op **ZIP downloaden** aan de rechterkant Hallo van Hallo pagina. U kunt [downloaden vanuit GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).

### <a name="option-2-source-via-git"></a>Optie 2: Bron via Git
tooget hello broncode Hallo SDK via Git, typt u:

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>Optie 3: Binaire bestanden via Gradle
U kunt Hallo binaire bestanden ophalen uit Hallo Maven centrale opslagplaats. Hallo AAR pakket kan als volgt worden opgenomen in uw project in Android Studio:

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a>Optie 4: AAR via Maven
Als u Hallo M2Eclipse invoegtoepassing gebruikt, kunt u Hallo afhankelijkheid opgeven in het bestand pom.xml:

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a>Optie 5: JAR-pakket in de map libs Hallo
U kunt ophalen Hallo JAR-bestand uit Hallo Maven opslagplaats en zet het neer in Hallo **bibliotheken** map in uw project. U moet toocopy Hallo vereiste resources tooyour project, omdat Hallo JAR pakketten niet opnemen.

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a>Stap 5: Verwijzingen tooAndroid ADAL tooyour project toevoegen
1. Voeg een verwijzing tooyour-project en dit opgeven als een Android-bibliotheek. Als u niet zeker hoe toodo, krijgt u meer informatie over het Hallo [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).
2. Hallo project afhankelijkheid voor foutopsporing in de instellingen van uw project toevoegen.
3. Bijwerken van uw project AndroidManifest.xml bestand tooinclude:

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. Een exemplaar van AuthenticationContext op uw belangrijkste activiteit maken. Hallo-details van deze aanroep zijn buiten bereik Hallo van dit onderwerp, maar u kunt een goede start door te kijken Hallo [Android Native Client voorbeeld](https://github.com/AzureADSamples/NativeClient-Android). In Hallo voorbeeld te volgen, SharedPreferences Hallo standaardcache is en instantie in de vorm van Hallo `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Kopieer deze code blok toohandle Hallo einde van AuthenticationActivity nadat Hallo gebruiker referenties invoert en een autorisatiecode ontvangt:

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. tooask voor een token een retouraanroep definiëren:

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. Ten slotte vragen voor een token met behulp van terugbellen:

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

Hier volgt een uitleg van Hallo parameters:

* *resource* is vereist en u probeert tooaccess Hallo-resource.
* *clientid* is vereist en afkomstig zijn van Azure AD.
* *RedirectUri* is niet vereist toobe hello acquireToken aanroep voorzien. U kunt instellen deze als de pakketnaam van uw.
* *PromptBehavior* helpt tooask voor referenties tooskip Hallo cache en cookie.
* *callback* wordt aangeroepen nadat de autorisatiecode Hallo worden uitgewisseld voor een token. Heeft een object van het AuthenticationResult waarvoor toegangstoken, datum verlopen en ID token-informatie.
* *acquireTokenSilent* is optioneel. U kunt deze aanroepen toohandle opslaan in cache en token vernieuwen. Het bevat ook Hallo synchronisatieversie. De cmdlet accepteert *userId* als parameter.

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

Met behulp van dit scenario hebt u wat u moet toosuccessfully integreren met Azure Active Directory. Voor meer voorbeelden van deze werken, gaat u naar Hallo AzureADSamples / opslagplaats op GitHub.

## <a name="important-information"></a>Belangrijke informatie
### <a name="customization"></a>Aanpassing
Uw toepassingsresources kunnen project bibliotheekresources overschrijven. Dit gebeurt wanneer uw app wordt samengesteld. Daarom kunt u verificatie activiteit indeling Hallo zoals die u wilt aanpassen. Ervoor tookeep Hallo-id van Hallo besturingselementen die ADAL (webweergave) gebruikt.

### <a name="broker"></a>Broker
Hallo Microsoft Intune-bedrijfsportal-app biedt Hallo broker onderdeel. Hallo-account wordt gemaakt in AccountManager. Hallo-accounttype is 'com.microsoft.workaccount'. AccountManager kan slechts één SSO-account. Maakt een SSO-cookie voor Hallo gebruiker na het voltooien van Hallo apparaat uitdaging voor een Hallo apps.

ADAL hello broker account wordt gebruikt als een gebruikersaccount op deze verificator wordt gemaakt en u ervoor geen tooskip kiest deze. U kunt doorgaan Hallo broker gebruiker met:

   `AuthenticationSettings.Instance.setSkipBroker(true);`

Een speciale RedirectUri tooregister moet u voor het gebruik van de broker. RedirectUri is Hallo notatie `msauth://packagename/Base64UrlencodedSignature`. U kunt uw RedirectUri ophalen voor uw app met behulp van Hallo script brokerRedirectPrint.ps1 of Hallo API-aanroep mContext.getBrokerRedirectUri. Hallo-handtekening is gerelateerde tooyour ondertekenen van certificaten.

Hallo huidige broker model is voor één gebruiker. AuthenticationContext biedt Hallo API methode tooget Hallo broker gebruiker.

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

Uw app-manifest hebt Hallo machtigingen toouse AccountManager accounts te volgen. Zie voor meer informatie, Hallo [AccountManager informatie over Android-site Hallo](http://developer.android.com/reference/android/accounts/AccountManager.html).

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>Instantie-URL en AD FS
Active Directory Federation Services (AD FS) is niet herkend als productie STS, zodat u tooturn van exemplaar van detectie moet en geef ' false ' op Hallo AuthenticationContext constructor.

Hallo-instantie URL moet een STS-exemplaar en een [tenantnaam](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).

### <a name="querying-cache-items"></a>Opvragen van cache-items
ADAL biedt een standaardcache in SharedPreferences met enkele eenvoudige cache queryfuncties. U kunt de huidige cache Hallo krijgen van AuthenticationContext met behulp van:

    ITokenCacheStore cache = mContext.getCache();

U kunt ook uw cache-implementatie opgeven als u wilt dat toocustomize deze.

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>Waarschuwing
ADAL biedt een optie toospecify vragen gedrag. PromptBehavior.Auto wordt Hallo gebruikersinterface weergegeven als het vernieuwingstoken Hallo ongeldig is en gebruikersreferenties vereist zijn. PromptBehavior.Always wordt Hallo cache gebruik overslaan en altijd weergeven Hallo gebruikersinterface.

### <a name="silent-token-request-from-cache-and-refresh"></a>Achtergrond tokenaanvraag uit de cache en vernieuwen
Een achtergrond tokenaanvraag gebruikt geen Hallo pop-UI en vereist geen een activiteit. Het resultaat een token uit cache Hallo indien beschikbaar. Als het Hallo-token is verlopen, deze methode toorefresh probeert deze. Als het Hallo-vernieuwingstoken is verlopen of is mislukt, wordt AuthenticationException.

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

U kunt een synchronisatie met deze methode aanroepen. U kunt instellen null toocallback of acquireTokenSilentSync gebruiken.

### <a name="diagnostics"></a>Diagnostiek
Hallo primaire bronnen met informatie voor het oplossen van problemen zijn:

* Uitzonderingen
* Logboeken
* Netwerktracering

Houd er rekening mee dat correlatie-id's centrale toohello diagnostics in Hallo-bibliotheek zijn. U kunt de correlatie-id's op basis van per aanvraag instellen als u wilt dat toocorrelate een ADAL aanvragen met andere bewerkingen zijn in uw code. Als u een correlatie-ID niet instelt, wordt de ADAL een willekeurige token genereren. Alle berichten logboekbestanden en netwerk aanroepen wordt vervolgens wordt voorzien van Hallo correlatie-ID. Hallo zelfgegenereerd ID wijzigingen bij elke aanvraag.

#### <a name="exceptions"></a>Uitzonderingen
Uitzonderingen worden eerst diagnostische Hallo. We proberen tooprovide handig foutberichten worden weergegeven. Als u een die niet handig vinden, Controleer het bestand een probleem en laat ons weten. Apparaatgegevens zoals model en SDK getal bevatten.

#### <a name="logs"></a>Logboeken
U kunt Hallo bibliotheek toogenerate configureren waarmee u toohelp kunt logboekberichten vaststellen van problemen. U kunt logboekregistratie configureren doordat Hallo volgende aanroepen tooconfigure een retouraanroep dat ADAL toohand uit elk logboekbericht gebruiken zoals deze wordt gegenereerd.

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

Berichten kunnen worden geschreven worden tooa aangepaste logboekbestand, zoals wordt weergegeven in de volgende code Hallo. Er is geen standaardmethode voor het ophalen van Logboeken vanaf een apparaat. Er zijn bepaalde services waarmee u kunnen met deze. U kunt ook uw eigen zoals verzenden Hallo tooa bestandsserver tot.

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

Dit zijn de registratieniveaus Hallo:
* Fout (uitzonderingen)
* Waarschuwen (waarschuwing)
* Info (doelen)
* Uitgebreid (meer informatie)

U instellen Hallo logboekniveau als volgt:

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 Alle berichten in het logboek worden toevoeging tooany aangepaste logboek retouraanroepen toologcat, verzonden.
U kunt als volgt een logboekbestand tooa van logcat krijgen:

    adb logcat > "C:\logmsg\logfile.txt"

 Zie voor meer informatie over adb opdrachten Hallo [logcat informatie over Android-site Hallo](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).

#### <a name="network-traces"></a>Netwerktracering
U kunt verschillende hulpprogramma's voor toocapture Hallo HTTP-verkeer dat ADAL genereert.  Dit is vooral handig als u bekend met de Hallo OAuth-protocol bent of als u tooprovide diagnostische gegevens tooMicrosoft of andere ondersteuningskanalen nodig hebt.

Fiddler is Hallo-hulpmiddel voor het traceren van eenvoudigste HTTP. Gebruik Hallo volgende koppelingen tooset het toocorrectly record ADAL-netwerkverkeer. Voor een tracering hulpprogramma zoals Fiddler of Jeroen toobe nuttig, moet u deze configureren toorecord ongecodeerd SSL-verkeer.  

> [!NOTE]
> Traceringen gegenereerd op deze manier kunnen zeer vertrouwelijke informatie zoals toegangstokens, gebruikersnamen en wachtwoorden bevatten. Als u van productie-accounts gebruikmaakt, deze traceringen niet delen met derden. Als u een toosomeone tracering in de volgorde tooget ondersteuning toosupply moet, reproduceren Hallo probleem met behulp van een tijdelijke rekening met gebruikersnamen en wachtwoorden dat wel delen.

* Van Hallo Telerik website: [instelling Up Fiddler voor Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* Vanuit GitHub: [Fiddler regels configureren voor ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)

### <a name="dialog-mode"></a>Dialoogvenster modus
Hallo acquireToken methode zonder activiteit ondersteunt een dialoogvenster.

### <a name="encryption"></a>Versleuteling
ADAL versleutelt Hallo tokens en opslaan in SharedPreferences standaard. U kunt zoeken op Hallo StorageHelper klasse toosee Hallo details. Android Keystore android geïntroduceerd voor 4.3 (API 18) veilige opslag van persoonlijke sleutels. ADAL gebruikt voor API 18 en hoger. Als u wilt dat toouse ADAL voor lagere SDK-versies, moet u een geheime sleutel op AuthenticationSettings.INSTANCE.setSecretKey tooprovide.

### <a name="oauth2-bearer-challenge"></a>OAuth2 bearer uitdaging
Hallo AuthenticationParameters klasse biedt functionaliteit tooget authorization_uri van Hallo OAuth2 bearer uitdaging.

### <a name="session-cookies-in-webview"></a>Sessiecookies in webweergave
Android webweergave wist niet sessiecookies nadat Hallo app is gesloten. U kunt die verwerkt met behulp van deze voorbeeldcode:

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

Zie voor meer informatie over cookies Hallo [CookieSyncManager informatie over Android-site Hallo](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).

### <a name="resource-overrides"></a>Resource-onderdrukkingen
Hallo ADAL-bibliotheek bevat Engelse tekenreeksen voor de ProgressDialog berichten. Uw toepassing moet ze als u gelokaliseerde tekenreeksen wilt overschrijven.

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>Dialoogvenster NTLM
ADAL-versie 1.1.0 ondersteunt een NTLM-dialoogvenster dat wordt verwerkt via Hallo onReceivedHttpAuthRequest gebeurtenis uit WebViewClient. U kunt Hallo indeling en tekenreeksen voor dialoogvenster Hallo aanpassen.

### <a name="cross-app-sso"></a>Cross-app eenmalige aanmelding
Meer informatie over [hoe tooenable SSO cross-app voor Android met behulp van ADAL](active-directory-sso-android.md).  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
