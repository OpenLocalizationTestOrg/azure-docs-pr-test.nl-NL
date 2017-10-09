[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister uw mobiele of native-toepassing hello-instellingen gebruiken in de tabel Hallo opgegeven.

![Voorbeeld van registratie-instellingen voor nieuwe mobiele of native toepassing](./media/active-directory-b2c-register-mobile-native-app/b2c-new-mobile-native-app-settings.png)

| Instelling      | Voorbeeldwaarde  | Beschrijving                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Naam** | Contoso B2C-app | Voer een **naam** voor Hallo-toepassing die uw toepassing tooconsumers beschrijft. |
| **Systeemeigen client** | Ja | Selecteer **Ja** voor een mobiele of native toepassing. |
| **Aangepaste omleidings-URI** | `com.onmicrosoft.contoso.appname://redirect/path` | Voer een omleidings-URI met een aangepast schema in. Zorg ervoor dat u een [goede omleidings-URI](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-native-application-redirect-uri) kiest en geen speciale tekens zoals onderstrepingstekens gebruikt. |

Klik op **maken** tooregister uw toepassing.

Uw zojuist geregistreerde toepassing wordt weergegeven in de lijst met toepassingen Hallo voor Hallo B2C-tenant. Selecteer uw app mobiele of systeemeigen in Hallo-lijst. deelvenster met de eigenschap van de toepassing Hello wordt weergegeven.

![Toepassingseigenschappen](./media/active-directory-b2c-register-mobile-native-app/b2c-mobile-native-app-properties.png)

Noteer Hallo globaal unieke **toepassing de Client-ID**. U Hallo-ID gebruiken in uw toepassingscode.

Als de native toepassing een web-API aanroept die is beveiligd door Azure AD B2C, voert u deze stappen uit:
   1. Maken van een toepassingsgeheim door te gaan toohello **sleutels** blade en te klikken op Hallo **sleutel genereren** knop. Noteer Hallo **App-sleutel** waarde. Hallo-waarde worden gebruikt als Hallo toepassingsgeheim in de code van uw toepassing.
   2. Klik op **API-toegang**, klik op **Toevoegen** en selecteer uw web-API en bereiken (machtigingen).

> [!NOTE]
> Een **toepassingsgeheim** is een belangrijke beveiligingsreferentie en moet op de juiste wijze worden beveiligd.
> 
