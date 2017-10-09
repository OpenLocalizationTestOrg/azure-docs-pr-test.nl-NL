tooenable aanmelden op uw toepassing, moet u toocreate een registratiebeleid. Dit beleid wordt Hallo ervaringen die consumenten doorlopen die tijdens de registratie en het Hallo-inhoud van de tokens die toepassing hello ontvangt op geslaagde aanmelding-ups beschreven.

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

Klik op **Registratiebeleid**.

Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.

Hallo **naam** bepaalt Hallo registratiebeleid naam die wordt gebruikt door uw toepassing. Voer bijvoorbeeld **SiUp** in.

Klik op **Id-providers** en selecteer **Registreren met e-mailadres**. U kunt er ook voor kiezen om sociale id-providers te selecteren als dit al is geconfigureerd. Klik op **OK**.

Klik op **Registratiekenmerken**. Hier u kenmerken kiezen dat u wilt dat toocollect van Hallo consumer tijdens de registratie. Selecteer bijvoorbeeld **Land/regio**, **Weergavenaam** en **Postcode**. Klik op **OK**.

Klik op **Toepassingsclaims**. Hier kiest u claims die u opvragen in Hallo tokens wilt back tooyour toepassing na een geslaagde aanmelding ervaring verzonden. Selecteer bijvoorbeeld **Weergavenaam**, **Id-provider**, **Postcode**, **Gebruiker is nieuw** en **Object-id van gebruiker**.

Klik op **Create**. Hallo-beleid hebt gemaakt, wordt weergegeven als **B2C_1_SiUp** (Hallo **B2C\_1\_**  fragment wordt automatisch toegevoegd) in Hallo **aanmelding beleid** blade.

Hallo beleid openen door te klikken op **B2C_1_SiUp**.

Selecteer **Contoso B2C-app** in Hallo **toepassingen** vervolgkeuzelijst en `https://localhost:44321/` in Hallo **antwoord-URL / omleidings-URI** vervolgkeuzelijst.

Klik op **Nu uitvoeren**. Een nieuw browsertabblad geopend en u kunt uitvoeren via Hallo consumer ervaring zich registreert voor uw toepassing.

> [!NOTE]
> Het tooa minuut voor het maken van beleid in beslag en updates van kracht tootake.
>