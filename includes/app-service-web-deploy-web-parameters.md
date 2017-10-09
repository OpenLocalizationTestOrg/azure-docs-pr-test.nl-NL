Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd. Hallo-sjabloon bevat een sectie met de naam van de Parameters die alle Hallo parameterwaarden bevat.
U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren. Definieer parameters niet voor waarden die altijd blijft dezelfde Hallo. De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo resources die zijn geïmplementeerd. 

Bij het definiëren van parameters gebruiken Hallo **allowedValues** veld toospecify die de waarden van een gebruiker kunt opgeven tijdens de implementatie. Gebruik Hallo **defaultValue** tooassign veld een waarde toohello parameter, als geen waarde is opgegeven tijdens de implementatie.

Er wordt elke parameter in de sjabloon Hallo beschreven.

### <a name="sitename"></a>Sitenaam
Hallo-naam van Hallo web-app die u wenst dat toocreate.

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a>hostingPlanName
Hallo-naam van het Hallo-App Service plan toouse voor het hosten van Hallo web-app.

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a>SKU
Hallo prijscategorie voor Hallo hosting-plan.

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

Hallo sjabloon definieert Hallo-waarden die zijn toegestaan voor deze parameter en een standaardwaarde (S1) wordt toegewezen als er geen waarde is opgegeven.

### <a name="workersize"></a>workerSize
Hallo exemplaargrootte van Hallo die als host fungeert voor plan (klein, Gemiddeld of grote).

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

Hallo sjabloon definieert Hallo-waarden die zijn toegestaan voor deze parameter (0, 1 of 2), en wijst een standaardwaarde (0) als er geen waarde is opgegeven. Hallo-waarden komen overeen toosmall, middelgrote en grote.

