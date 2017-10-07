---
title: aaaAzure container register webhooks | Microsoft Docs
description: Azure-container register webhooks.
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: Docker, Containers ACR
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>Met behulp van Azure Container register webhooks - Azure-portal

Een Azure container registry opgeslagen en beheerd persoonlijke Docker-container installatiekopieën, vergelijkbare toohello manier Docker Hub openbare Docker-installatiekopieën worden opgeslagen. U webhooks tootrigger gebeurtenissen wanneer bepaalde acties uitgevoerd in een van de Register-opslagplaatsen. Webhooks tooevents op Hallo register niveau kunnen reageren, of ze kunnen worden gericht op omlaag tooa specifieke opslagplaats label. 

Zie voor meer informatie over de achtergrond en concepten Hallo [overzicht](./container-registry-intro.md).

## <a name="prerequisites"></a>Vereisten 

- Azure-container beheerd register - een register beheerde container maken in uw Azure-abonnement. Bijvoorbeeld, gebruik hello Azure-portal of Azure CLI 2.0 Hallo. 
- Docker CLI - tooset van uw lokale computer als een Docker-host en toegang Hallo Docker CLI-opdrachten, Docker-Engine installeren. 

## <a name="create-webhook-azure-portal"></a>Maken van de webhook Azure-portal

1. Meld u bij toohello Azure-portal en navigeer toohello register waarin wordt gezocht toocreate webhooks. 

2. Selecteer in de Hallo container blade Hallo 'Webhooks' tabblad. 

3. Selecteer "Toevoegen" hello webhook blade werkbalk van. 

4. Volledige Hallo *Webhook maken* formulier Hello volgende informatie:

| Waarde | Beschrijving |
|---|---|
| Naam | gewenste toogive toohello webhook Hallo-naam. Kan alleen kleine letters en cijfers bevatten en tussen 5 tot 50 tekens bevatten. |
| Service-URI | Hallo URI waar Hallo webhook POST meldingen te verzenden. |
| Aangepaste headers | Headers gewenste toopass samen met de Hallo POST-aanvraag. Ze moet ' sleutel: waarde ' indeling. |
| Acties starten | Acties die Hallo webhook activeren. Momenteel webhooks kan worden geactiveerd door push en/of acties tooan installatiekopie verwijderen. |
| Status | Hallo-status voor Hallo webhook nadat deze gemaakt. Dit standaard ingeschakeld. |
| Bereik | Hallo-scope op welke Hallo webhook werkt. Hallo-scope is standaard voor alle gebeurtenissen in het Hallo-register. Het kan worden opgegeven voor een bibliotheek of een tag met de indeling Hallo ' opslagplaats: code '. |

Voorbeeld van de webhook formulier:

![DCOS GEBRUIKERSINTERFACE](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>Azure CLI-webhook maken

toocreate een webhook met Azure CLI, gebruik Hallo Hallo [az acr-webhook maken](/cli/azure/acr/webhook#create) opdracht.

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>Test webhook

### <a name="azure-portal"></a>Azure Portal

Eerdere toousing hello webhook voor container push installatiekopie en verwijderingsacties, kunnen worden getest met Hallo **Ping** knop. Wanneer gebruikt, stuurt Hallo Ping dat een toohello algemene post-aanvraag opgegeven eindpunt en logboeken Hallo antwoord. Dit is handig tooverify die Hallo webhook is correct zijn ingesteld.

1. Hallo-webhook u tootest wilt selecteren. 
2. Selecteer in de bovenste werkbalk Hallo Hallo 'Pingen' actie. 
3. Controleer Hallo-aanvraag en -antwoord.

### <a name="azure-cli"></a>Azure CLI

tootest een webhook ACR Hello Azure CLI gebruiken Hallo [az acr webhook ping](/cli/azure/acr/webhook#ping) opdracht.

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

toosee hello resultaten gebruiken Hallo [az acr webhook lijst-gebeurtenissen](/cli/azure/acr/webhook#list-events) opdracht. 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>Webhook verwijderen

### <a name="azure-portal"></a>Azure Portal

Elke webhook kan worden verwijderd door Hallo webhook en vervolgens Hallo verwijderen knop op Hallo Azure-portal te selecteren.

### <a name="azure-cli"></a>Azure CLI

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```