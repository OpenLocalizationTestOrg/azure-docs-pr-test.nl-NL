---
title: aaaAzure AD Cordova aan de slag | Microsoft Docs
description: "Hoe toobuild een Cordova-toepassing die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-beveiligde API aanroept met behulp van OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a>Azure AD integreren met een Apache Cordova-app
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

U kunt Apache Cordova toodevelop HTML5/JavaScript-toepassingen die kunnen worden uitgevoerd op mobiele apparaten als volwaardig systeemeigen toepassingen gebruiken. U kunt met Azure Active Directory (Azure AD), bedrijfsniveau verificatie mogelijkheden tooyour Cordova toepassingen toevoegen.

Een invoegtoepassing Cordova verpakt Azure AD systeemeigen SDK's op iOS, Android, Windows Store en Windows Phone. Met behulp van dat invoegtoepassing, u door uw toepassing toosupport aanmelden met Windows Server Active Directory-accounts voor uw gebruikers verbeteren kunt krijgen toegang tooOffice 365 en Azure-API's, en zelfs beschermen aanroepen tooyour eigen aangepaste web-API.

In deze zelfstudie gebruiken we Hallo Apache Cordova-invoegtoepassing voor Active Directory Authentication Library (ADAL) tooimprove een eenvoudige app door toe te voegen Hallo volgende kenmerken:

* Verifiëren van een gebruiker met een paar regels code, en een token verkrijgen.
* Gebruik die tooquery token tooinvoke Hallo Graph API die map en Hallo resultaten weer te geven.  
* Gebruik Hallo ADAL tokencache toominimize verificatie wordt gevraagd om Hallo-gebruiker.

toomake deze verbeteringen, moet u:

1. U registreert een toepassing met Azure AD.
2. Code tooyour app toorequest-tokens toevoegen.
3. Voeg code toouse Hallo token query Hallo Graph API's en resultaten weer te geven.
4. Hallo Cordova-project voor implementatie te maken met alle Hallo platforms wilt tootarget, Hallo invoegtoepassing Cordova ADAL toevoegen en Hallo oplossing in emulators testen.

## <a name="prerequisites"></a>Vereisten
toocomplete deze zelfstudie hebt u nodig:

* Een Azure AD-tenant waarin u een account met app-ontwikkeling rechten hebben.
* Een ontwikkelingsomgeving die toouse Apache Cordova is geconfigureerd.  

Als u beide al hebt ingesteld, gaan rechtstreeks toostep 1.

Als u geen Azure AD-tenant, gebruikt u Hallo [instructies voor het tooget een](active-directory-howto-tenant.md).

Als u geen Apache Cordova instellen op uw computer, installeert u Hallo volgende:

* [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.js](https://nodejs.org/download/)
* [Cordova CLI](https://cordova.apache.org/) (kan gemakkelijk worden geïnstalleerd via NPM Pakketbeheer: `npm install -g cordova`)

Hallo voorgaande installaties moet werken voor Hallo PC en Hallo Mac.

Elk doelplatform heeft verschillende vereisten:

* toobuild en voer een app voor Windows-Tablet/PC of Windows Phone:
  * Installeer [Visual Studio 2013 voor Windows met Update 2 of hoger](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express of een andere versie) of [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).

* toobuild en voer een app voor iOS:

  * Installeer Xcode 6.x of hoger. Het downloaden van Hallo [Apple Developer site](http://developer.apple.com/downloads) of Hallo [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).
  * Installeer [ios-sim](https://www.npmjs.org/package/ios-sim). U kunt deze toostart iOS-apps in iOS-Simulator vanaf de opdrachtregel Hallo. (U kunt het eenvoudig installeren via Hallo terminal: `npm install -g ios-sim`.)
* toobuild en voer een app voor Android:

  * Installeer [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) of hoger. Zorg ervoor dat `JAVA_HOME` (omgevingsvariabele) correct is ingesteld op basis van toohello JDK installatiepad (bijvoorbeeld C:\Program Files\Java\jdk1.7.0_75).
  * Installeer [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) en voeg Hallo `<android-sdk-location>\tools` locatie (bijvoorbeeld C:\tools\Android\android-sdk\tools) tooyour `PATH` omgevingsvariabele.
  * Android SDK Manager openen (bijvoorbeeld via Hallo terminal: `android`) en te installeren:
    * *Android 5.0.1 (API 21)* platform SDK
    * *Android SDK-Build Tools* versie 19.1.0 of hoger
    * *Android-ondersteuning opslagplaats* (extra's)

  Hallo Android SDK biedt een standaardexemplaar van de emulator niet. Maken van een door het uitvoeren van `android avd` van Hallo terminal en vervolgens te klikken op **maken**, als u wilt dat toorun hello Android-app op een emulator. U wordt aangeraden een API-niveau van 19 of hoger. Zie voor meer informatie over de Android-emulator en het maken van opties Hallo [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) op Hallo Android-site.

## <a name="step-1-register-an-application-with-azure-ad"></a>Stap 1: Een toepassing registreren met Azure AD
Deze stap is optioneel. Deze zelfstudie bevat vooraf is ingericht waarden waarmee u toosee kunt Hallo voorbeeld in actie zonder eventuele inrichten in uw eigen tenant. We raden echter aan dat u deze stap uitvoeren en vertrouwd met Hallo proces, raken omdat deze vereist is wanneer u uw eigen toepassingen maken.

Azure AD geeft tokens tooonly bekend toepassingen. Voordat u Azure AD van uw app gebruiken kunt, moet u toocreate een vermelding voor het in uw tenant. een nieuwe toepassing in uw tenant tooregister:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op de bovenste balk hello, uw account. In Hallo **Directory** Kies waar u tooregister hello Azure AD-tenant van uw toepassing.
3. Klik op **meer Services** in Hallo linkerdeelvenster en selecteer vervolgens **Azure Active Directory**.
4. Klik op **App registraties**, en selecteer vervolgens **toevoegen**.
5. Volg de aanwijzingen Hallo en maak een **systeemeigen clienttoepassing**. (Hoewel de Cordova-apps zijn op basis van HTML, we creëren een native client-toepassing. Hallo **systeemeigen clienttoepassing** optie moet zijn geselecteerd, of de toepassing hello werken niet.)
  * **Naam** beschrijft de toousers van uw toepassing.
  * **Omleidings-URI** is Hallo URI die tooreturn tokens tooyour app wordt gebruikt. Voer **http://MyDirectorySearcherApp**.

Nadat u de registratie, wijst een unieke toepassingsnaam ID tooyour app in Azure AD toe. U moet deze waarde in de volgende secties Hallo. U vindt deze op het toepassingstabblad Hallo Hallo app een nieuw gemaakt.

toorun `DirSearchClient Sample`, Hallo nieuwe app machtiging tooquery hello Azure AD Graph API verlenen:

1. Van Hallo **instellingen** pagina **Required Permissions**, en selecteer vervolgens **toevoegen**.  
2. Voor Azure Active Directory-toepassing hello, selecteert u **Microsoft Graph** als Hallo API en voeg Hallo **toegang Hallo directory als de gebruiker is aangemeld Hallo** machtiging onder **gedelegeerde Machtigingen**.  Hierdoor kan uw toepassing tooquery Hallo Graph API voor gebruikers.

## <a name="step-2-clone-hello-sample-app-repository"></a>Stap 2: Hallo voorbeeld-app opslagplaats klonen
Van uw shell of vanaf de opdrachtregel typt u Hallo volgende opdracht:

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a>Stap 3: Hallo Cordova-app maken
Er zijn meerdere manieren toocreate Cordova-toepassingen. In deze zelfstudie gebruiken we Hallo Cordova-opdrachtregelinterface (CLI).

1. Van uw shell of vanaf de opdrachtregel typt u Hallo volgende opdracht:

        cordova create DirSearchClient

   Deze opdracht maakt Hallo mapstructuur en steigers voor Hallo Cordova-project.

2. Toohello nieuwe DirSearchClient map verplaatsen:

        cd .\DirSearchClient

3. Hallo-inhoud van Hallo starter project kopiëren in Hallo www submap met behulp van een bestand manager of de volgende opdracht in uw shell Hallo:

  * Windows:`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`
  * Mac:`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`

4. Hallo geaccepteerde invoegtoepassing toevoegen. Dit is nodig voor het aanroepen van Hallo Graph API.

        cordova plugin add cordova-plugin-whitelist

5. Alle Hallo-platforms die u toosupport wilt toevoegen. een voorbeeld van een werkende toohave, moet u tooexecute ten minste één van de volgende opdrachten Hallo. Houd er rekening mee dat u niet kunnen tooemulate iOS in Windows worden en emuleren van Windows op een Mac.

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. Hallo ADAL voor Cordova-invoegtoepassing tooyour project toevoegen:

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a>Stap 4: Code tooauthenticate gebruikers toevoegen en tokens verkrijgen bij Azure AD
Hallo-toepassing die u in deze zelfstudie ontwikkelt bieden een eenvoudige directory zoekfunctie. Hallo-gebruiker kan vervolgens Hallo alias van een gebruiker typt in Hallo directory en visualiseren enkele eenvoudige kenmerken. Hallo starter project bevat Hallo definitie van de algemene gebruikersinterface Hallo van Hallo-app (in www/index.html) en Hallo steigers die van de basis-Apps gebeurtenis kabels cycli, gebruikersinterface bindingen, en resultaten weergeven logica (in www/js/index.js). Hallo is alleen gegeven voor u uit de taak tooadd Hallo logica die identiteit taken implementeert.

Hallo eerste wat u moet toodo in uw code is introduceren Hallo protocol waarden die Azure AD wordt gebruikt voor het identificeren van uw app en Hallo resources die u zijn gericht. Deze waarden worden aanvragen voor beveiligingstokens gebruikte tooconstruct hello later op. Voeg Hallo codefragment bovenaan Hallo Hallo index.js bestand te volgen:

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

Hallo `redirectUri` en `clientId` waarden moeten overeenkomen met de Hallo-waarden met een beschrijving van uw app in Azure AD. U kunt vinden die uit Hallo **configureren** tabblad hello Azure-portal, zoals beschreven in stap 1 eerder in deze zelfstudie.

> [!NOTE]
> Als u hebt gekozen voor het registreren van een nieuwe app niet in uw eigen tenant, kunt u eenvoudig hello vooraf geconfigureerde waarden omdat plakken. U kunt zien Hallo voorbeeld wordt uitgevoerd, hoewel altijd moet u uw eigen vermelding maken voor uw apps die zijn bedoeld voor productie.

Vervolgens voegt u Hallo tokenaanvraag code. Invoegen na codefragment tussen Hallo Hallo `search` en `renderData` definities:

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
Door deze te splitsen in de twee belangrijkste delen behandeld die functie.
Dit voorbeeld is ontworpen toowork met een tenant zoals tegengestelde toobeing tooa name een gebonden. Hierbij Hallo '/ algemene' eindpunt waarmee Hallo gebruiker tooenter een account kunt verificatie tegelijk, en stuurt Hallo aanvraag toohello tenant waartoe deze behoort.

Deze eerste deel van de methode Hallo inspecteert Hallo ADAL cache toosee als een token is al opgeslagen. Zo ja, Hallo-methode maakt gebruik van Hallo tenants waar Hallo token vandaan komt voor het initialiseren van ADAL. Dit is noodzakelijk tooavoid omdat Hallo het gebruik van '/ algemene' altijd resulteert in het Hallo gebruiker tooenter gevraagd een nieuw account extra prompts.

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
Hallo secondegedeelte van Hallo methode voert de juiste tokenaanvraag Hallo. Hallo `acquireTokenSilentAsync` methode vraagt ADAL tooreturn een token voor Hallo opgegeven resource zonder dat u eventuele UX weergegeven Dat kan gebeuren als het Hallo-cache heeft al een geschikte toegangstoken opgeslagen, of als een vernieuwingstoken kan worden gebruikt u een nieuw toegangstoken tooget zonder een prompt weer te geven. Als dat lukt, we terugvallen op `acquireTokenAsync`--die Hallo gebruiker tooauthenticate zichtbaar wordt gevraagd.

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
Nu dat we Hallo-token hebben, kunnen we ten slotte Hallo Graph API aanroepen en Hallo zoekquery die we willen uitvoeren. Invoegen na de onderstaande Hallo codefragment Hallo `authenticate` definitie:

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
een eenvoudige UX Hallo startpunt bestanden opgegeven voor het invoeren van de alias van een gebruiker in het tekstvak. Deze methode maakt gebruik van die waarde tooconstruct een query, combineren met het toegangstoken Hallo tooMicrosoft grafiek om dit te verzenden en parseren Hallo resultaten. Hallo `renderData` methode, al aanwezig in Hallo startpunt bestand, zorgt voor het Hallo-resultaten te visualiseren.

## <a name="step-5-run-hello-app"></a>Stap 5: Hallo app uitvoeren
Uw app wordt tot slot gereed toorun. Het besturingssysteem is eenvoudig: wanneer Hallo-app wordt gestart, Voer Hallo alias van Hallo gebruiker toolook omhoog gewenste en klik vervolgens op Hallo knop. U wordt gevraagd om de verificatie. Bij de verificatie is geslaagd en zoekactie worden Hallo kenmerken van Hallo doorzocht gebruiker weergegeven.

Latere uitvoeringen Hallo zoekopdracht wordt uitgevoerd zonder een prompt weer te geven, dankzij toohello aanwezigheid van Hallo eerder hebt verkregen token in de cache.

Hallo concrete stappen voor het uitvoeren van de app hello, varieert per platform.

### <a name="windows-10"></a>Windows 10
   Tablet PC:`cordova run windows --archs=x64 -- --appx=uap`

   Mobile (vereist een Windows 10 Mobile-apparaat aansluit tooa PC):`cordova run windows --archs=arm -- --appx=uap --phone`

   > [!NOTE]
   > Tijdens het Hallo voor het eerst uitvoert, u mogelijk gevraagd toosign in voor een ontwikkelaarslicentie. Zie voor meer informatie [ontwikkelaarslicentie](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-81-tabletpc"></a>Windows 8.1 Tablet PC
   `cordova run windows`

   > [!NOTE]
   > Tijdens het Hallo voor het eerst uitvoert, u mogelijk gevraagd toosign in voor een ontwikkelaarslicentie. Zie voor meer informatie [ontwikkelaarslicentie](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-phone-81"></a>Windows Phone 8.1
   toorun op een verbonden apparaat:`cordova run windows --device -- --phone`

   toorun op Hallo standaardemulator:`cordova emulate windows -- --phone`

   Gebruik `cordova run windows --list -- --phone` toosee alle beschikbare doelen en `cordova run windows --target=<target_name> -- --phone` toorun Hallo toepassing op een specifiek apparaat of emulator (bijvoorbeeld `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).

### <a name="android"></a>Android
   toorun op een verbonden apparaat:`cordova run android --device`

   toorun op Hallo standaardemulator:`cordova emulate android`

   Zorg ervoor dat u hebt een exemplaar van de emulator gemaakt met behulp van AVD Manager, zoals eerder in de sectie 'Vereisten' hello beschreven.

   Gebruik `cordova run android --list` toosee alle beschikbare doelen en `cordova run android --target=<target_name>` toorun Hallo toepassing op een specifiek apparaat of emulator (bijvoorbeeld `cordova run android --target="Nexus4_emulator"`).

### <a name="ios"></a>iOS
   toorun op een verbonden apparaat:`cordova run ios --device`

   toorun op Hallo standaardemulator:`cordova emulate ios`

   > [!NOTE]
   > Controleer of er Hallo `ios-sim` toorun pakket is geïnstalleerd op het Hallo-emulator. Zie voor meer informatie, Hallo 'vereisten' sectie.

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a>Volgende stappen
Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) is beschikbaar in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).

U kunt nu verplaatsen op geavanceerde toomore (en meer interessante)-scenario's. U kunt tootry: [beveiligen van een Node.js-Web-API met Azure AD](active-directory-devquickstarts-webapi-nodejs.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
