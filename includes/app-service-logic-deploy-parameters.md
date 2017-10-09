Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd. Hallo-sjabloon bevat een sectie met de naam van de Parameters die alle Hallo parameterwaarden bevat.
U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren. Definieer parameters niet voor waarden die altijd blijft dezelfde Hallo. De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo implementeren van resources die zijn. 

Bij het definiëren van parameters gebruiken Hallo **allowedValues** veld toospecify die de waarden van een gebruiker kunt opgeven tijdens de implementatie. Gebruik Hallo **defaultValue** tooassign veld een waarde toohello parameter, als geen waarde is opgegeven tijdens de implementatie.

Er wordt elke parameter in de sjabloon Hallo beschreven.

### <a name="logicappname"></a>logicAppName
Hallo-naam van Hallo logic app toocreate.

    "logicAppName": {
        "type": "string"
    }