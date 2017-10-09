tooenable aanmelden op uw toepassing, moet u toocreate een aanmeldingspagina beleid. Dit beleid wordt Hallo ervaringen die consumenten doorlopen tijdens het aanmelden en het Hallo-inhoud van de tokens die toepassing hello ontvangt op geslaagde aanmeldingen beschreven.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Hallo beleidsregels sectie van de instellingen en selecteer **registreren of aanmelden beleid** en klik op **+ toevoegen**.

![Beleid voor registreren of aanmelden selecteren en op de knop Toevoegen klikken](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

Voer een beleid **naam** voor uw toepassing tooreference. Geef bijvoorbeeld `SiUpIn` op.

Selecteer **Id-providers** en schakel **Registreren met e-mailadres** in. U kunt er ook voor kiezen om sociale id-providers te selecteren als dit al is geconfigureerd. Klik op **OK**.

![E-aanmelding als een id-provider en klik op de knop OK Hallo](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

Selecteer **Registratiekenmerken**. Kenmerken kiezen gewenste toocollect van Hallo consumer tijdens de registratie. Schakel bijvoorbeeld **Land/regio**, **Weergavenaam** en **Postcode** in. Klik op **OK**.

![Selecteer enkele kenmerken en klik op OK Hallo](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

Selecteer **Toepassingsclaims**. Kies claims opvragen in Hallo autorisatie tokens wilt verzonden back tooyour toepassing na een geslaagde aanmelding of aanmelden ervaring. Selecteer bijvoorbeeld **Weergavenaam**, **Id-provider**, **Postcode**, **Gebruiker is nieuw** en **Object-id van gebruiker**.

![Selecteer enkele toepassingsclaims en klik op de knop OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

Klik op **maken** tooadd Hallo beleid. Hallo-beleid wordt vermeld als **B2C_1_SiUpIn**. Hallo **B2C_1_** voorvoegsel is de naam van de toegevoegde toohello.

Hallo beleid openen door te selecteren **B2C_1_SiUpIn**. Hallo-instellingen die zijn opgegeven in de tabel Hallo controleren en klik vervolgens op **nu uitvoeren**.

![Selecteer het beleid en voer dit uit](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| Instelling      | Waarde  |
| ------------ | ------ |
| **Toepassingen** | Contoso B2C-app |
| **Antwoord-URL selecteren** | `https://localhost:44316/` |

Een nieuw browsertabblad wordt geopend en u kunt controleren of Hallo registreren of aanmelden consumer ervaring zoals geconfigureerd.

> [!NOTE]
> Het tooa minuut voor het maken van beleid in beslag en updates van kracht tootake.
>