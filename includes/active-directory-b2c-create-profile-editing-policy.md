tooenable profiel bewerken op uw toepassing, moet u toocreate een profiel te bewerken van beleid. Dit beleid beschrijft Hallo ervaringen die consumenten doorlopen tijdens profiel bewerken en het Hallo-inhoud van de tokens die de toepassing hello is gelukt ontvangt.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Hallo beleidsregels sectie van de instellingen en selecteer **profiel bewerken van beleid** en klik op **+ toevoegen**.

![Selecteer het profiel bewerken van beleid en klik op de knop toevoegen Hallo](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

Voer een beleid **naam** voor uw toepassing tooreference. Geef bijvoorbeeld `SiPe` op.

Selecteer **Id-providers** en schakel **Aanmelden met lokaal account** in. U kunt er ook voor kiezen om sociale id-providers te selecteren als dit al is geconfigureerd. Klik op **OK**.

![Lokale Account aanmelding als een id-provider en klik op de knop OK Hallo](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

Selecteer **Profielkenmerken**. Kies kenmerken Hallo consumer kunt bekijken en bewerken in het profiel. Schakel bijvoorbeeld **Land/regio**, **Weergavenaam** en **Postcode** in. Klik op **OK**.

![Selecteer enkele kenmerken en klik op OK Hallo](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

Selecteer **Toepassingsclaims**. Kies de claims die u opvragen in Hallo autorisatie tokens wilt verzonden back tooyour toepassing na een geslaagde profiel te bewerken. Selecteer bijvoorbeeld **Weergavenaam**, **Postcode**.

![Selecteer enkele toepassingsclaims en klik op de knop OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

Klik op **maken** tooadd Hallo beleid. Hallo-beleid wordt vermeld als **B2C_1_SiPe**. Hallo **B2C_1_** voorvoegsel is de naam van de toegevoegde toohello.

Hallo beleid openen door te selecteren **B2C_1_SiPe**. Hallo-instellingen die zijn opgegeven in de tabel Hallo controleren en klik vervolgens op **nu uitvoeren**.

![Selecteer het beleid en voer dit uit](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| Instelling      | Waarde  |
| ------------ | ------ |
| **Toepassingen** | Contoso B2C-app |
| **Antwoord-URL selecteren** | `https://localhost:44316/` |

Een nieuw browsertabblad geopend en kunt u controleren of Hallo profiel te bewerken consumer zoals geconfigureerd.

> [!NOTE]
> Het tooa minuut voor het maken van beleid in beslag en updates van kracht tootake.
>