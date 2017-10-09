---
title: een klassieke webservice aaaRetrain | Microsoft Docs
description: Meer informatie over hoe tooprogrammatically opnieuw trainen model en update Hallo web service toouse Hallo nieuw model is getraind in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a>Een klassieke webservice opnieuw trainen
Hallo voorspellende u geïmplementeerde webservice is Hallo standaard score-eindpunt. Standaardeindpunten worden gesynchroniseerd met Hallo oorspronkelijke trainings- en experimenten score berekenen en daarom hello getrainde model voor het standaardeindpunt Hallo kan niet worden vervangen. tooretrain hello web-service, moet u een nieuwe webservice van de endpoint-toohello toevoegen. 

## <a name="prerequisites"></a>Vereisten
U moet een trainingsexperiment en een Voorspellend experiment hebt ingesteld zoals wordt weergegeven in [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> Hallo Voorspellend experiment moet worden geïmplementeerd als een klassiek machine learning-webservice. 
> 
> 

Zie voor meer informatie over webservices implementeren [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="add-a-new-endpoint"></a>Een nieuw eindpunt toevoegen
Hallo voorspellende webservice die u hebt geïmplementeerd bevat een standaardexemplaar score-eindpunt dat is gesynchroniseerd met de oorspronkelijke training Hallo en scoreprofiel experimenten getrainde model. tooupdate toowith een nieuw getraind model van uw web-service moet u een nieuw score-eindpunt. 

een nieuw scoreprofiel eindpunt op Hallo voorspellende webservice die kan worden bijgewerkt met het getrainde model Hallo toocreate:

> [!NOTE]
> Zorg ervoor dat u toevoegt Hallo eindpunt toohello voorspellende webservice niet Hallo Training Web Service. Als u correct zowel een trainings- en een Voorspellend webservice hebt geïmplementeerd, ziet u twee afzonderlijke webservices die worden vermeld. Hallo voorspellende webservice moet eindigen met '[voorspellende exp.]'.
> 
> 

Er zijn drie manieren waarop u een nieuwe webservice van de eindpunt-tooa kunt toevoegen:

1. Programmatisch
2. Hallo webservices voor Microsoft Azure portal gebruiken
3. Hallo klassieke Azure-portal gebruiken

### <a name="programmatically-add-an-endpoint"></a>Programmatisch een eindpunt toevoegen
U kunt scoreprofiel Hallo voorbeeldcode in dit om eindpunten toevoegen [github-opslagplaats](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a>Hallo webservices voor Microsoft Azure portal tooadd een eindpunt gebruiken
1. Klik op Web-Services op Hallo linkernavigatievenster kolom in Machine Learning Studio.
2. Aan de onderkant van de Hallo van Hallo web servicedashboard, klikt u op **beheren eindpunten preview**.
3. Klik op **Add**.
4. Typ een naam en beschrijving voor het nieuwe eindpunt Hallo. Selecteer het logboekregistratieniveau Hallo en of voorbeeldgegevens is ingeschakeld. Zie voor meer informatie over logboekregistratie [logboekregistratie inschakelen voor Machine Learning-webservices](machine-learning-web-services-logging.md).

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a>Gebruik hello Azure classic portal tooadd een eindpunt
1. Meld u aan toohello [klassieke Azure portal](https://manage.windowsazure.com).
2. Klik in het linkermenu hello, **Machine Learning**.
3. Onder de naam, uw werkruimte op en klik op **webservices**.
4. Klik onder de naam, **telling Model [voorspellende exp].** .
5. Klik onder aan de pagina Hallo Hallo op **eindpunt toevoegen**. Zie voor meer informatie over het toevoegen van eindpunten [eindpunten maken](machine-learning-create-endpoint.md). 

## <a name="update-hello-added-endpoints-trained-model"></a>Update Hallo Trained Model-eindpunt toegevoegd
toocomplete hello retraining proces, moet u bijwerken Hallo getrainde model van het nieuwe eindpunt Hallo die u hebt toegevoegd.

* Als u nieuwe Hallo-eindpunt met de klassieke Azure portal Hallo hebt toegevoegd, kunt u op de naam van de Hallo nieuw eindpunt in Hallo-portal en vervolgens Hallo **UpdateResource** tooget Hallo URL moet u tooupdate Hallo eindpunt model koppelen.
* Als u met behulp van de voorbeeldcode Hallo Hallo-eindpunt toegevoegd, dit omvat de locatie van Hallo help-URL is geïdentificeerd door Hallo *HelpLocationURL* waarde in het Hallo-uitvoer.

tooretrieve hello pad URL:

1. Kopieer en plak Hallo-URL in uw browser.
2. Klik op Hallo Update Resource koppeling.
3. Hallo POST-URL van de PATCH-aanvraag Hallo kopiëren. Bijvoorbeeld:
   
     URL VAN DE PATCH: HTTPS://MANAGEMENT.AZUREML.NET/WORKSPACES/00BF70534500B34REBFA1843D6/WEBSERVICES/AF3ER32AD393852F9B30AC9A35B/ENDPOINTS/NEWENDPOINT2

U kunt nu Hallo getrainde model tooupdate Hallo score-eindpunt dat u eerder hebt gemaakt.

Hallo volgende voorbeeldcode laat zien u hoe toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, en URL PATCH tooupdate Hallo-eindpunt.

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

Hallo *apiKey* en Hallo *endpointUrl* voor Hallo aanroep kan worden verkregen van endpoint-dashboard.

waarde van Hallo Hallo *naam* parameter in *Resources* moeten identieke Hallo resourcenaam Hallo opgeslagen getrainde Model Hallo Voorspellend experiment. tooget hello resourcenaam:

1. Meld u aan toohello [klassieke Azure portal](https://manage.windowsazure.com).
2. Klik in het linkermenu hello, **Machine Learning**.
3. Onder de naam, uw werkruimte op en klik op **webservices**.
4. Klik onder de naam, **telling Model [voorspellende exp].** .
5. Klik op de nieuwe eindpunt Hallo die u hebt toegevoegd.
6. Klik op Hallo eindpunt dashboard **Update Resource**.
7. Op Hallo Update Resource API-documentatie pagina voor de webservice Hallo vindt u Hallo **resourcenaam** onder **bij te werken bronnen**.

Als uw SAS-token is verstreken voordat u klaar bent met het eindpunt van de Hallo bijwerken, moet u een GET met Hallo taak-Id tooobtain-token van een nieuwe uitvoeren.

Wanneer Hallo code met succes is uitgevoerd, nieuw Hallo-eindpunt moet zich eerst Hallo retrained objectmodel gebruiken in ongeveer 30 seconden.

## <a name="summary"></a>Samenvatting
Met behulp van Hallo Retraining API's, kunt u Hallo getraind model van een Voorspellend webservice scenario's zoals inschakelen bijwerken:

* Periodieke model retraining met nieuwe gegevens.
* Distributie van een model toocustomers met Hallo doel van zodat ze opnieuw trainen Hallo-model met hun eigen gegevens.

## <a name="next-steps"></a>Volgende stappen
[Het oplossen van problemen Hallo retraining van een klassieke Azure Machine Learning-webservice](machine-learning-troubleshooting-retraining-models.md)

