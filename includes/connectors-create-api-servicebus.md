### <a name="prerequisites"></a>Vereisten
U moet hebben een [Service Bus](https://azure.microsoft.com/services/service-bus/) account.  

Voordat u uw Azure Service Bus-account in een logische app gebruiken kunt, geeft u toestemming Hallo logic app tooconnect tooyour service bus-account. U kunt dit eenvoudig vanuit gelukkig doen in uw logische app op Hallo Azure-portal.  

Hier volgen Hallo stappen tooauthorize uw logische app tooconnect tooyour Service Bus-account:  

1. selecteert u een verbinding tooService Bus, in Hallo logic app-ontwerper toocreate **beheerde API's van Microsoft weergeven** in de vervolgkeuzelijst Hallo. Voer vervolgens **service bus** in het zoekvak Hallo. Selecteer Hallo trigger of de actie die u wilt toouse.  
    ![Afbeelding voor de service Bus 1](./media/connectors-create-api-servicebus/servicebus-1.png)  
2. Als u alle verbindingen tooService Bus voordat u dit nog niet hebt gemaakt, moet na vragen aan gebruiker tooprovide uw Service Bus-referenties. Deze referenties worden gebruikt tooauthorize uw logische app tooconnect tooand toegang tot de gegevens van uw Service Bus-account. Hallo Service Bus-connector moet een verbindingstekenreeks Hallo voor Hallo Service Bus-naamruimte. Vereist ook **beheren** machtigingen. Een goede manier tooknow als de verbindingsreeks voor de naamruimte hello is of een specifieke entiteit is als het Hallo bevat `EntityPath` parameter. Als dit het geval is, is het niet de juiste verbindingsreeks Hallo voor een logische app.  
    ![Service Bus-verbindingsreeks](./media/connectors-create-api-servicebus/connectionstring.png)
3. Nadat u de verbindingsreeks Hallo voor Hallo naamruimte hebt ontvangen, kunt u deze kunt gebruiken voor Hallo API-verbinding in Logic Apps.  
    ![Afbeelding voor de service Bus 2](./media/connectors-create-api-servicebus/servicebus-2.png)  
4. U ziet het Hallo-verbinding is gemaakt en u bent nu gratis tooproceed Hello, andere in uw logische app stappen.  
    ![Afbeelding voor de service Bus 3](./media/connectors-create-api-servicebus/servicebus-3.png)   

