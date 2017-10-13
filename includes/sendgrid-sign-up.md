Azure-klanten kunnen iedere maand 25.000 gratis e-mails ontgrendelen. Deze 25.000 gratis maandelijkse e-mails geven u toegang tot geavanceerde rapportages en analyses en [alle API's][all APIs] (web, SMTP, gebeurtenis, parseren en meer). Voor informatie over extra diensten die door SendGrid worden aangeboden, gaat u naar de pagina met [SendGrid-oplossingen][SendGrid Solutions].

### <a name="to-sign-up-for-a-sendgrid-account"></a>Aanmelden voor een SendGrid-account
1. Meld u aan bij de [Azure-beheerportal][Azure Management Portal].
2. Klik in het menu aan de linkerkant op **Nieuw**.

    ![opdracht-balk-nieuw][command-bar-new]
3. Klik op **Invoegtoepassingen** en vervolgens op **SendGrid e-maillevering**.

    ![sendgrid-opslaan][sendgrid-store]
4. Vul het registratieformulier in en selecteer **Maken**.

    ![sendgrid-maken][sendgrid-create]
5. Voer een **naam** in om uw SendGrid-service in uw Azure-instellingen te herkennen. Namen moeten tussen de 1 en 100 tekens lang zijn en mogen alleen alfanumerieke tekens, streepjes, punten en onderstrepingstekens bevatten. De naam moet uniek zijn in uw lijst met geabonneerde Azure Store-items.
6. Voer uw **wachtwoord** in en bevestig dit.
7. Kies uw **abonnement**.
8. Maak een nieuwe **resourcegroep** of selecteer een bestaande.
9. Selecteer in het gedeelte **Prijscategorie** het SendGrid-abonnement waar u zich voor wilt aanmelden.

    ![sendgrid-prijzen][sendgrid-pricing]
10. Voer een **promotiecode** in als u er een hebt.
11. Voer uw **contactgegevens** in.
12. Lees en accepteer de **juridische bepalingen**.
13. Nadat u uw aankoop hebt bevestigd, verschijnt het pop-upbericht **Implementatie voltooid** en wordt uw account vermeld in het gedeelte **Alle resources**.

    ![alle-resources][all-resources]

    Nadat u uw aankoop hebt voltooid en op de knop **Beheren** hebt geklikt om de verificatieprocedure van het e-mailadres te starten, ontvangt u een e-mail van SendGrid waarin u wordt gevraagd uw account te verifiëren. Als u deze e-mail niet ontvangt of problemen ervaart bij het verifiëren van uw account, raadpleegt u deze veelgestelde vragen.

    ![beheren][manage]

    **U kunt maximaal 100 e-mailberichten per dag verzenden totdat u uw account hebt geverifieerd.**

    Als u uw abonnement wilt wijzigen of de SendGrid-contactinstellingen wilt bekijken, klikt u op de naam van uw SendGrid-service om het SendGrid Marketplace-dashboard te openen.

    ![instellingen][settings]

    Als u een e-mail met SendGrid wilt verzenden, moet u uw API-sleutel invoeren.

### <a name="to-find-your-sendgrid-api-key"></a>Uw SendGrid-API-sleutel vinden
1. Klik op **Beheren**.

    ![beheren][manage]
2. Selecteer op uw SendGrid-dashboard **Instellingen** en vervolgens **API-sleutels** in het menu aan de linkerkant.

    ![API-sleutels][api-keys]

3. Klik op de vervolgkeuzelijst **API-sleutel maken** en selecteer **Algemene API-sleutel**.

    ![algemene-api-sleutel][general-api-key]
4. Geef ten minste de **naam van de sleutel** op, verleen volledige toegang tot **Mail verzenden** en selecteer vervolgens **Opslaan**.

    ![toegang][access]
5. Uw API wordt op dit moment één keer weergegeven. Zorg ervoor dat u de API veilig opslaat.

### <a name="to-find-your-sendgrid-credentials"></a>Uw SendGrid-referenties vinden
1. Klik op het sleutelpictogram om uw **gebruikersnaam** te vinden.

    ![sleutel][key]
2. Het wachtwoord is door u gekozen tijdens de installatie. Als u wijzigingen wilt aanbrengen, selecteert u **Wachtwoord wijzigen** of **Wachtwoord opnieuw instellen**.

Als u uw instellingen voor de bezorging van e-mail wilt beheren, klikt u op de knop **Beheren**. Hiermee wordt een omleiding naar uw SendGrid-dashboard.

    ![manage][manage]

    For more information on sending email through SendGrid, visit the [Email API Overview][Email API Overview].

<!--images-->

[command-bar-new]: ./media/sendgrid-sign-up/new-addon.png
[sendgrid-store]: ./media/sendgrid-sign-up/sendgrid-store.png
[sendgrid-create]: ./media/sendgrid-sign-up/sendgrid-create.png
[sendgrid-pricing]: ./media/sendgrid-sign-up/sendgrid-pricing.png
[all-resources]: ./media/sendgrid-sign-up/all-resources.png
[manage]: ./media/sendgrid-sign-up/manage.png
[settings]: ./media/sendgrid-sign-up/settings.png
[api-keys]: ./media/sendgrid-sign-up/api-keys.png
[general-api-key]: ./media/sendgrid-sign-up/general-api-key.png
[access]: ./media/sendgrid-sign-up/access.png
[key]: ./media/sendgrid-sign-up/key.png

<!--Links-->

[SendGrid Solutions]: https://sendgrid.com/solutions
[Azure Management Portal]: https://manage.windowsazure.com
[SendGrid Getting Started]: http://sendgrid.com/docs
[SendGrid Provisioning Process]: https://support.sendgrid.com/hc/articles/200181628-Why-is-my-account-being-provisioned-
[all APIs]: https://sendgrid.com/docs/API_Reference/index.html
[Email API Overview]: https://sendgrid.com/docs/API_Reference/Web_API_v3/Mail/index.html
