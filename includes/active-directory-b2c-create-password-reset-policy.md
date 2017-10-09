tooenable fijnmazig wachtwoord opnieuw instellen op uw toepassing, moet u een beleid voor wachtwoordherstel toocreate. Opmerking die Hallo tenant wide wachtwoordherstel optie opgegeven [hier](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md). Dit beleid beschrijft Hallo ervaringen die Hallo consumenten doorlopen tijdens het wachtwoord opnieuw instellen en het Hallo-inhoud van de tokens die toepassing hello ontvangt is gelukt.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Hallo beleidsregels sectie van de instellingen en selecteer **beleid voor wachtwoordherstel** en klik op **+ toevoegen**.

![Selecteer registreren of aanmelden beleid en klik op de knop toevoegen Hallo](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

Voer een beleid **naam** voor uw toepassing tooreference. Geef bijvoorbeeld `SSPR` op.

Selecteer **Id-providers** en schakel de optie **Het wachtwoord opnieuw instellen met e-mailadres** in. Klik op **OK**.

![Wachtwoord opnieuw instellen met behulp van e-mailadres als een id-provider en klik op de knop OK Hallo](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

Selecteer **Toepassingsclaims**. Kies de claims die u opvragen in Hallo autorisatie tokens wilt back tooyour toepassing verzonden nadat een geslaagde wachtwoordherstel ervaring. Selecteer bijvoorbeeld **Object-ID van gebruiker**.

![Selecteer enkele toepassingsclaims en klik op de knop OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

Klik op **maken** tooadd Hallo beleid. Hallo-beleid wordt vermeld als **B2C_1_SSPR**. Hallo **B2C_1_** voorvoegsel is de naam van de toegevoegde toohello.

Hallo beleid openen door te selecteren **B2C_1_SSPR**. Hallo-instellingen die zijn opgegeven in de tabel Hallo controleren en klik vervolgens op **nu uitvoeren**.

![Selecteer het beleid en voer dit uit](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| Instelling      | Waarde  |
| ------------ | ------ |
| **Toepassingen** | Contoso B2C-app |
| **Antwoord-URL selecteren** | `https://localhost:44316/` |

Een nieuw browsertabblad geopend en kunt u controleren of Hallo wachtwoordherstel consumer ervaring in uw toepassing.

> [!NOTE]
> Het tooa minuut voor het maken van beleid in beslag en updates van kracht tootake.
>
