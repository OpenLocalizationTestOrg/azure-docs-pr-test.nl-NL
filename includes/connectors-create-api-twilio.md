### <a name="prerequisites"></a>Vereisten
* Een Twilio-account
* Een geverifieerde Twilio-telefoonnummer dat SMS-berichten kunt ontvangen
* Een geverifieerde Twilio-telefoonnummer dat SMS kan verzenden

> [!NOTE]
> Als u van een Twilio-proefaccount gebruikmaakt, kunt u alleen verzenden SMS te**geverifieerd** telefoonnummers.  
> 
> 

Voordat u uw Twilio-account in een logische app gebruiken kunt, moet u autoriseren hello Logic app tooconnect tooyour Twilio-account. U kunt dit eenvoudig vanuit gelukkig doen in uw logische app op Hallo Azure-Portal. 

Hier volgen Hallo stappen tooauthorize uw logische app tooconnect tooyour Twilio-account:

1. selecteert u een verbinding tooTwilio, in Hallo Logic app-ontwerper toocreate **beheerde API's van Microsoft weergeven** in Hallo vervolgkeuzelijst Geef vervolgens *Twilio* in het zoekvak Hallo. Hallo trigger of actie je toouse selecteren:  
   ![](./media/connectors-create-api-twilio/twilio-0.png)
2. Als u alle verbindingen tooTwilio voordat u dit nog niet hebt gemaakt, krijgt u na vragen aan gebruiker tooprovide uw Twilio-referenties. Deze referenties worden gebruikte tooauthorize uw logische app tooconnect naar en toegang tot gegevens van uw Twilio-account:  
   ![](./media/connectors-create-api-twilio/twilio-1.png)  
3. U moet Hallo **Twilio-account-id** en **Twilio-toegangstoken** vanuit Hallo dashboard in Twilio, dus aanmelden tooyour Twilio-account nu toograb deze twee soorten informatie:  
   ![](./media/connectors-create-api-twilio/twilio-2.png)  
4. Twilio en Logic apps gebruiken verschillende namen tooidentify deze twee soorten informatie. Hier ziet u hoe u moet toe te wijzen toohello Logic apps dialoogvenster:![](./media/connectors-create-api-twilio/twilio-3.png)  
5. Selecteer Hallo **verbinding maken** knop:  
   ![](./media/connectors-create-api-twilio/twilio-4.png)
6. U ziet het Hallo-verbinding is gemaakt en u bent nu gratis tooproceed Hello, andere in uw logische app stappen:  
   ![](./media/connectors-create-api-twilio/twilio-5.png)

