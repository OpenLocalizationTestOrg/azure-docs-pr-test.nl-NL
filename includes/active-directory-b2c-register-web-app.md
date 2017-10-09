[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister uw webtoepassing, Hallo-instellingen gebruiken in de tabel Hallo opgegeven.

![Voorbeeld van registratie-instellingen voor een nieuwe web-app](./media/active-directory-b2c-register-web-app/b2c-new-app-settings.png)

| Instelling      | Voorbeeldwaarde  | Beschrijving                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Naam** | Contoso B2C-app | Voer een **naam** voor Hallo-toepassing die uw toepassing tooconsumers beschrijft. | 
| **Web-app / web-API opnemen** | Ja | Selecteer **Ja** voor een webtoepassing. |
| **Impliciete stroom toestaan** | Ja | Selecteer **Ja** als voor de toepassing wordt gebruikgemaakt van [Aanmelding via OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md) |
| **Antwoord-URL** | `https://localhost:44316` | Antwoord-URL's zijn eindpunten waarop Azure AD B2C tokens retourneert die zijn aangevraagd voor de toepassing. Voer een [juiste](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **antwoord-URL** in. In dit voorbeeld is de app lokaal en luistert deze op poort 44316. |

Klik op **maken** tooregister uw toepassing.

Uw zojuist geregistreerde toepassing wordt weergegeven in de lijst met toepassingen Hallo voor Hallo B2C-tenant. Selecteer uw web-app in Hallo-lijst. Hallo-webtoepassing eigenschap deelvenster wordt weergegeven.

![Eigenschappen van webtoepassing](./media/active-directory-b2c-register-web-app/b2c-web-app-properties.png)

Noteer Hallo globaal unieke **toepassing de Client-ID**. U Hallo-ID gebruiken in uw toepassingscode.
