---
title: aaaOpenAPI metagegevens in Azure Functions | Microsoft Docs
description: Overzicht van ondersteuning voor Azure Functions OpenAPI
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a>Ondersteuning voor OpenAPI 2.0-metagegevens in de Azure-functies (preview)
OpenAPI 2.0 (voorheen Swagger) ondersteuning voor metagegevens in Azure Functions is een preview-functie waarmee u een 2.0 OpenAPI toowrite definitie binnen een functie-app kunt. Vervolgens kunt u dat bestand met behulp van de functie-app Hallo hosten.

[OpenAPI metagegevens](http://swagger.io/) kunt u een functie die als host voor een toobe REST-API fungeert wordt gebruikt door een groot aantal andere software. Deze software bevat de offerings Microsoft zoals PowerApps en Hallo [API Apps-functie van Azure App Service](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), hulpprogramma's voor ontwikkelaars van derden, zoals [Postman](https://www.getpostman.com/docs/importing_swagger), en [veel meer pakketten](http://swagger.io/tools/).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
>Het is raadzaam beginnen met Hallo [zelfstudie aan de slag](./functions-api-definition-getting-started.md) en vervolgens te retourneren toothis document toolearn meer informatie over specifieke functies.

## <a name="enable"></a>OpenAPI definitie ondersteuning inschakelen
U kunt alle OpenAPI-instellingen configureren op Hallo **API-definitie** pagina in de functie-app **platformfuncties**.

tooenable hello generatie van de definitie van een gehoste OpenAPI en een Quick Start-definitie ingesteld **API-definitie bron** te**functie (Preview)**. **Externe URL** Hiermee kunt u de functie toouse een OpenAPI definiëren die heeft die elders wordt gehost.

## <a name="generate-definition"></a>Genereren van een geraamte Swagger van metagegevens van de functie
Een sjabloon kunt u de definitie van de eerste OpenAPI vrienden. Hallo definitie sjabloon functie maakt een definitie van een sparse OpenAPI door alle Hallo metagegevens in Hallo function.json-bestand voor elk van de functies van uw HTTP-trigger. U moet toofill in meer informatie over de API van Hallo [OpenAPI specificatie](http://swagger.io/specification/), zoals sjablonen voor aanvraag en -antwoord.

Zie voor stapsgewijze instructies Hallo [zelfstudie aan de slag](./functions-api-definition-getting-started.md).

### <a name="templates"></a>Beschikbare sjablonen

|Naam| Beschrijving |
|:-----|:-----|
|De definitie van de gegenereerde|De definitie van een OpenAPI met maximale hoeveelheid gegevens die kan worden afgeleid van de bestaande metagegevens van de functie Hallo Hallo.|

### <a name="quickstart-details"></a>Opgenomen metagegevens in de definitie van de Hallo gegenereerd

Hallo na tabel vertegenwoordigt hello Azure portal-instellingen en de bijbehorende gegevens in function.json omdat deze toegewezen toohello gegenereerde Swagger basisproject.

|Swagger.JSON|Portal-gebruikersinterface|Function.JSON|
|:----|:-----|:-----|
|[Host](http://swagger.io/specification/#fixed-fields-15)|**App-instellingen werken** > **App Service-instellingen** > **overzicht** > **URL**|*Niet aanwezig*
|[Paden](http://swagger.io/specification/#paths-object-29)|**Integreren** > **geselecteerd HTTP-methoden**|Bindingen: Route
|[Pad-Item](http://swagger.io/specification/#path-item-object-32)|**Integreren** > **Routesjabloon**|Bindingen: methoden
|[Beveiliging](http://swagger.io/specification/#security-scheme-object-112)|**Sleutels**|*Niet aanwezig*|
|operationID *|**Route + toegestane termen**|Route + toegestane termen|

\*Hallo bewerkings-ID is alleen vereist voor integratie met PowerApps en stroom.
> [!NOTE]
> Hallo x-ms-overzicht extension biedt een weergavenaam in Logic Apps, PowerApps en stroom.
>
> toolearn meer, Zie [aanpassen van uw Swagger-definitie voor PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).

## <a name="CICD"></a>Gebruik CI/CD tooset een API-definitie

 API definitie die als host fungeert in Hallo portal voordat u uw API-definitie van broncodebeheer bron besturingselement toomodify inschakelt, moet u inschakelen. Volg deze instructies:

1. Te bladeren**API-definitie (preview)** in de functie app-instellingen.
  1. Stel **API-definitie bron** te**functie**.
  1. Klik op **genereren API-definitie sjabloon** en vervolgens **opslaan** toocreate de Sjabloondefinitie van een om later te wijzigen.
  1. Houd er rekening mee uw API-definitie URL en de sleutel.
1. [Continue integratie/doorlopende implementatie (CI/CD) ingesteld](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).
2. Wijzigen van swagger.json in broncodebeheer op \site\wwwroot\.azurefunctions\swagger\swagger.json.

Nu wijzigingen tooswagger.json in de opslagplaats worden gehost door de functie-app op Hallo API-definitie-URL en de sleutel die u hebt genoteerd in stap 1.c.

## <a name="next-steps"></a>Volgende stappen
* [Zelfstudie aan de slag](functions-api-definition-getting-started.md). Probeer onze toosee scenario de definitie van een OpenAPI in te grijpen.
* [Azure Functions GitHub-opslagplaats](https://github.com/Azure/Azure-Functions/). Uitchecken Hallo functies opslagplaats toogive ons feedback op Hallo API-definitie ondersteuning preview. Maak een GitHub-probleem voor elke toosee bijgewerkt gewenste.
* [Naslaginformatie over Azure Functions developer](functions-reference.md). Meer informatie over het coderen van functies en definiëren van triggers en bindingen.
