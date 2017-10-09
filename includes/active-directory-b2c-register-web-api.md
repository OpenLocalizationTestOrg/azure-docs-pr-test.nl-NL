[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister uw web-API, gebruik Hallo-instellingen die zijn opgegeven in de tabel Hallo.

![Voorbeeld van registratie-instellingen voor een nieuwe web-API](./media/active-directory-b2c-register-web-api/b2c-new-web-api-settings.png)

| Instelling      | Voorbeeldwaarde  | Beschrijving                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Naam** | Contoso B2C-API | Voer een **naam** voor Hallo-toepassing die uw API-tooconsumers beschrijft. | 
| **Web-app / web-API opnemen** | Ja | Selecteer **Ja** voor een web-API. |
| **Impliciete stroom toestaan** | Ja | Selecteer **Ja** als voor de toepassing wordt gebruikgemaakt van [Aanmelding via OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md) |
| **Antwoord-URL** | `https://localhost:44316/` | Antwoord-URL's zijn eindpunten waarop Azure AD B2C tokens retourneert die zijn aangevraagd voor de toepassing. Voer een [juiste](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **antwoord-URL**in. In dit voorbeeld is de web-API lokaal en luistert deze op poort 44316. |
| **App-id-URI** | api | Hallo App ID URI is Hallo-id die wordt gebruikt voor uw web-API. Hallo volledige id URI inclusief Hallo domein wordt voor u gegenereerd. |

Klik op **maken** tooregister uw toepassing.

Uw zojuist geregistreerde toepassing wordt weergegeven in de lijst met toepassingen Hallo voor Hallo B2C-tenant. Selecteer uw web-API in Hallo-lijst. Hallo-API's eigenschap deelvenster wordt weergegeven.

![Eigenschappen van de web-API](./media/active-directory-b2c-register-web-api/b2c-web-api-properties.png)

Noteer Hallo globaal unieke **toepassing de Client-ID**. U Hallo-ID gebruiken in uw toepassingscode.
