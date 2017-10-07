---
title: een API aaaImport in Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooimport een API en bewerkingen in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a>Hoe tooimport Hallo definitie van een API met bewerkingen in Azure API Management
Nieuwe API's kunnen worden gemaakt in API Management en Hallo bewerkingen handmatig toegevoegd of Hallo API kan samen met de Hallo-bewerkingen in één stap worden geïmporteerd.

API's en hun bewerkingen kunnen worden geïmporteerd met behulp van de volgende indelingen Hallo.

* WADL
* Swagger

Deze handleiding bevat een nieuwe API maken en importeren van bewerkingen in één stap. Zie voor informatie over het handmatig maken van een API en het toevoegen van bewerkingen, [hoe toocreate API's] [ How toocreate APIs] en [hoe tooadd operations tooan API] [ How tooadd operations tooan API].

## <a name="import-api"> </a>Een API importeren
API's zijn gemaakt en geconfigureerd in de publicatieportal Hallo. tooaccess publisher en klik op Hallo **publicatieportal** in hello Azure-Portal voor uw API Management-service. Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.

![Publicatieportal][api-management-management-console]

Klik op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **importeren API**.

![API importeren][api-management-import-apis]

Hallo **Import API** venster bestaat uit drie tabbladen die overeenkomen met toohello drie manieren tooprovide Hallo API-specificatie.

* **Van Klembord** kunt u toopaste Hallo API-specificatie in aangewezen Hallo-tekstvak.
* **Uit bestand** kunt u toobrowse tooand Selecteer Hallo-bestand met de Hallo API-specificatie.
* **Van URL** kunt u toosupply Hallo URL toohello-specificatie voor Hallo API.

![Indeling van de API importeren][api-management-import-api-clipboard]

Gebruik na het opgeven van Hallo API-specificatie Hallo keuzerondjes op Hallo rechts tooindicate Hallo specificatie indeling. Hallo volgende indelingen worden ondersteund.

* WADL
* Swagger

Geef vervolgens een **achtervoegsel URL Web-API**. Dit is de toegevoegde toohello basis-URL voor uw API management-service. Hallo basis-URL is gebruikelijk voor alle API's die worden gehost op elk exemplaar van API Management-service. API Management API's onderscheidt door hun achtervoegsel en daarom Hallo achtervoegsel moet uniek zijn voor elke API in een specifiek exemplaar van API management-service.

Nadat alle waarden zijn ingevoerd, klikt u op **opslaan** toocreate Hallo API en Hallo operations gekoppeld. 

> [!NOTE]
> Zie voor een zelfstudie over het importeren van de basisrekenmachine API in Swagger-indeling, [uw eerste API beheren in Azure API Management](api-management-get-started.md).
> 
> 

## <a name="export-api"></a> Exporteren van een API
In aanvulling tooimporting nieuwe API's, kunt u Hallo definities van uw API's van de publicatieportal Hallo exporteren. toodo hiervoor, klikt u op **exporteren API** van Hallo **tabblad Samenvatting** van uw **API**.

![API exporteren][api-management-export-api]

API's kunnen worden geëxporteerd met WADL of Swagger. Selecteer de gewenste indeling hello, klikt u op **opslaan**, en Hallo locatie kiezen in welke toosave Hallo-bestand.

![API-indeling voor exporteren][api-management-export-api-format]

## <a name="next-steps"> </a>Volgende stappen
Nadat een API is gemaakt en Hallo-bewerkingen die zijn geïmporteerd, die u kunt bekijken en configureren van eventuele aanvullende instellingen Hallo API tooa Product toevoegen en publiceren zodat deze beschikbaar voor ontwikkelaars. Zie voor meer informatie Hallo handleidingen te volgen.

* [Hoe tooconfigure API-instellingen][How tooconfigure API settings]
* [Hoe toocreate en een product publiceren][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
