---
title: gebeurtenissen voor Azure Event raster aaaCustom | Microsoft Docs
description: Gebruik Azure gebeurtenis raster toopublish een onderwerp en toothat gebeurtenis abonneren.
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a>Aangepaste gebeurtenissen maken en routeren met behulp van Azure Event Grid

Azure Event raster is een gebeurtenisservice voor Hallo cloud. In dit artikel gebruiken hello Azure CLI toocreate een eigen onderwerp, toohello onderwerp abonneren en Hallo gebeurtenis tooview Hallo resultaat activeren. Normaal gesproken verzendt u gebeurtenissen tooan eindpunt dat toohello gebeurtenis, zoals een webhook of een Azure-functie reageert. Toosimplify dit artikel, u Hallo gebeurtenissen tooa URL die alleen Hallo-berichten verzamelt verzenden. U maakt deze URL met behulp van een open source-hulpprogramma van derden, met de naam [RequestBin](https://requestb.in/).

>[!NOTE]
>**RequestBin** is een open source-hulpprogramma dat niet is bedoeld voor gebruik met een hoge doorvoer. Hallo-gebruik van Hallo hulpprogramma hier is puur demonstrative. Als u meer dan een gebeurtenis op een tijdstip pushen, ziet u mogelijk niet alle gebeurtenissen in Hallo-hulpprogramma.

Wanneer u klaar bent, ziet u dat Hallo gebeurtenisgegevens tooan eindpunt is verzonden.

![Gebeurtenisgegevens](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, in dit artikel is vereist dat u altijd de meest recente versie Hallo van Azure CLI (2.0.14 of hoger). toofind hello versie, voer `az --version`. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Event Grid-onderwerpen zijn Azure-resources en moeten in een Azure-resourcegroep worden geplaatst. Hallo-resourcegroep is een logische verzameling in welke Azure resources worden geïmplementeerd en beheerd.

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *gridResourceGroup* in Hallo *westus2* locatie.

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a>Een aangepast onderwerp maken

Een onderwerp biedt een door de gebruiker gedefinieerd eindpunt waarop u de gebeurtenissen kunt posten. Hallo maakt volgende voorbeeld Hallo onderwerp in de resourcegroep. Vervang `<topic_name>` door een unieke naam voor het onderwerp. Hallo onderwerp de naam moet uniek zijn omdat deze wordt vertegenwoordigd door een DNS-vermelding. Voor de preview-versie Hallo gebeurtenis raster ondersteunt **westus2** en **westcentralus** locaties.

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a>Het eindpunt van een bericht maken

Voordat u zich abonneert toohello onderwerp, gaan we maken Hallo-eindpunt voor de gebeurtenis het Hallo-bericht. In plaats van schrijven van code toorespond toohello gebeurtenis, maken we een eindpunt dat Hallo-berichten worden verzameld zodat u ze kunt weergeven. RequestBin is een open-source hulpprogramma van derden waarmee u een eindpunt toocreate en aanvragen weergeven die tooit worden verzonden. Ga te[RequestBin](https://requestb.in/), en klik op **maken van een RequestBin**.  Kopieer de URL van Hallo-opslaglocatie, omdat u deze nodig hebt wanneer u zich abonneert toohello onderwerp.

## <a name="subscribe-tooa-topic"></a>Abonneren tooa onderwerp

U zich hebt geabonneerd tooa onderwerp tootell gebeurtenis raster welke gebeurtenissen u wilt dat tootrack. Hallo volgende voorbeeld is geabonneerd toohello onderwerp hebt gemaakt Hallo-URL van RequestBin als Hallo-eindpunt voor gebeurtenismelding doorgegeven. Vervang `<event_subscription_name>` met een unieke naam voor uw abonnement en `<URL_from_RequestBin>` Hallo waarde uit de voorgaande sectie Hallo. Als u zich abonneert, kunt u een eindpunt opgeeft, verwerkt gebeurtenis raster Hallo routering van gebeurtenissen toothat eindpunt. Voor `<topic_name>`, gebruik Hallo-waarde die u eerder hebt gemaakt. 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a>Een gebeurtenis tooyour onderwerp verzenden

Nu gaan we een gebeurtenis toosee activeren hoe gebeurtenis raster Hallo-bericht tooyour eindpunt distribueert. Eerst laten we Hallo-URL ophalen en de sleutel voor Hallo onderwerp. Gebruik opnieuw de onderwerpnaam voor `<topic_name>`.

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

toosimplify in dit artikel we een voorbeeld gebeurtenis gegevens toosend toohello onderwerp hebt ingesteld. Een toepassing of service van Azure wilt verzenden doorgaans Hallo gebeurtenisgegevens. Hallo volgt opgehaald Hallo gebeurtenisgegevens:

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

Als u `echo "$body"` ziet u de volledige gebeurtenis Hallo. Hallo `data` Hallo JSON-element is Hallo nettolading van de gebeurtenis. Elke juist opgemaakte JSON kan in dit veld worden ingevoerd. U kunt ook het veld onderwerp hello gebruiken voor geavanceerde routering en filteren.

CURL is een hulpprogramma waarmee HTTP-aanvragen worden uitgevoerd. In dit artikel gebruiken we CURL toosend Hallo gebeurtenis tooour onderwerp. 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

U hebt Hallo-gebeurtenis geactiveerd en gebeurtenis raster Hallo-bericht toohello eindpunt die u geconfigureerd wanneer u zich abonneert verzonden. Blader toohello RequestBin-URL die u eerder hebt gemaakt. Of klik in het geopende RequestBin-browservenster op Vernieuwen. U ziet Hallo-gebeurtenis die u zojuist hebt verzonden. 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a>Resources opschonen
Als u van plan toocontinue werken met deze gebeurtenis bent, gaat u als Hallo-resources die zijn gemaakt in dit artikel niet opruimen. Als u niet van plan toocontinue bent, gebruikt u Hallo opdracht toodelete Hallo-resources die u hebt gemaakt in dit artikel te volgen.

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

Als u weet hoe toocreate onderwerpen en abonnementen, meer informatie over welke gebeurtenis raster kunt u doen:

- [Over Event Grid](overview.md)
- [Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md) (Wijzigingen in virtuele machines bewaken met Azure Event Grid en Logic Apps)
