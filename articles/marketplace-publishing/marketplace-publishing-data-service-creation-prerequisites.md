---
title: vereisten voor het maken van een Service voor Hallo Marketplace gegevens aaaTechnical | Microsoft Docs
description: Hallo-vereisten voor het maken van een gegevensservice toodeploy begrijpen en verkopen op Hallo Azure Marketplace
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: aaff609a-1cd1-4146-98f4-d04166b0fce0
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2bba4282473fed63c3fcab43043a97e179705844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-hello-azure-marketplace"></a>Technische vereisten voor het maken van een gegevensservice bieden voor hello Azure Marketplace
> [!IMPORTANT]
> **Op dit moment wordt niet langer zijn voorbereiden op alle nieuwe gegevensservice uitgevers. Nieuwe dataservices wordt niet goedgekeurd voor de aanbieding.** Als u een SaaS-business-toepassing hebt wilt toopublish op AppSource vindt u meer informatie [hier](https://appsource.microsoft.com/partners). Als u beschikt over een IaaS-toepassingen of developer-service dat u zou zoals toopublish op Azure Marketplace vindt u meer informatie [hier](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Hallo-proces zorgvuldig door voordat u begint lees en begrijp waar en waarom elke stap wordt uitgevoerd. Zo veel mogelijk, u moet uw bedrijfsgegevens en andere gegevens voorbereiden, vereiste hulpprogramma's downloaden en/of technische onderdelen maken voordat u begint met Hallo-proces voor het maken van aanbieding.

Moet u de volgende items gereed is voordat u begint met Hallo Hallo hebben:

## <a name="make-a-decision-on-what-technology-will-be-used-toopublish-your-data-service-offer"></a>Maken van een beslissing over welke technologie gebruikte toopublish worden uw aanbieding gegevensservice
Een uitgever kunt kiezen tussen meerdere technologieën bij het publiceren van Data-Service in Azure Marketplace. Hallo belangrijkste technologieën die worden ondersteund die hieronder worden beschreven. Ongeacht welke technologie gebruikte toopublish Hallo Data-Service is, Hallo eindgebruiker verbruikt Hallo gegevens via Hallo **OData-feed** die worden weergegeven door de Service voor Azure Marketplace. Gedetailleerde informatie over het OData-service die u kunt vinden op [http://www.odata.org/](http://www.odata.org/)

## <a name="sql-azure-database"></a>SQL Azure Database
Dataset gereed in SQL Azure met is de verantwoordelijkheid van de uitgever. U moet toosubscribe tooAzure, juiste grootte van de Database in te richten en uw gegevens uploaden naar SQL Azure DB. Uitgever is tevens verantwoordelijk tookeep stelt zijn/haar gegevens altijd up-to-date. Meer informatie over abonnementen tooAzure Services die u kunt vinden op [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)

Hallo-gegevens naar SQL Azure te verplaatsen, hello Azure Marketplace kan worden blootgesteld tabellen en weergaven. Hallo Publisher kunt opgeven welke tabellen/weergaven en de kolommen blootgestelde toohello door eindgebruikers zijn. Verdere Hallo inhoudsprovider kunt ook opgeven welke kolommen kunnen worden opgevraagd met Hallo eindgebruikers en welke alleen worden geretourneerd in Hallo nettolading. Hiermee geeft u een hoge mate van flexibiliteit over welke gegevens in Hallo-database moet worden weergegeven. Kolommen die kunnen worden opgevraagd moeten toobe ondersteund door een of meer database-indexen.

## <a name="rest-based-web-service"></a>Op basis van REST-webservice
Ondersteund protocol: **alleen HTTPS**

Bestaande op basis van REST-services kunnen worden blootgesteld via hello Azure Marketplace. Moet toobe kunnen toomap service tooa op basis van OData-service in Media Player Hallo Hallo dataset is altijd blootgestelde toohello eindgebruiker als een OData-feed, hello Azure Marketplace-service. toodo daarom Hallo op basis van REST-eindpunten tooexpose alle parameters als HTTP-parameters.

Hallo nettolading moet toobe in een formulier dat kan worden toegewezen aan een ATOM-antwoord. Daarom Hallo reactie van Hallo services moet toobe in XML-indeling en mogen slechts één herhalende element die Hallo nettolading waarden (zoals Recordset) bevat. Hello Azure Marketplace service zal hello, herhalende toohello vermelding knooppunt ATOM en Hallo nettolading waarden in de eigenschap knooppunten binnen Hallo vermelding knooppunt toewijzen.

Autorisatie-informatie (zoals API key, verificatie token, enz.) moet toobe opgegeven als een HTTP-parameter of in Hallo HTTP-header (sleutel-waardepaar) – basisverificatie wordt ook ondersteund. Een geldige sleutel moet toobe geleverd en worden alle aanvragen via Azure Marketplace gesteld via deze sleutel. Gebruiker bewaking en facturering gebeurt op Hallo Azure Marketplace-laag.

Fouten geretourneerd door het Hallo-service moeten toobe toegewezen in HTTP-statuscodes. Als Hallo-service retourneert een XML-bestand dat Hallo fout bevat gaat deze toobe toegewezen door tooHTTP statuscodes voor hello Azure Marketplace-service.

## <a name="soap-based-web-services"></a>Op basis van SOAP-webservices
Protocol: **alleen HTTPS**

Hallo-vereisten zijn dezelfde als in de sectie voor REST gebaseerde service Hallo Hallo. Hallo enige verschil is dat parameters kunnen ook worden opgegeven in een XML-hoofdtekst die worden verzonden van de uitgever van de toohello service met elk verzoek via Azure Marketplace. Dit betekent dat HTTP-parameters Hallo gebruiker heeft op de front-Hallo zijn wordt vertaald naar een XML-elementen van een XML-document dat wordt geboekt met Hallo aanvraag toohello inhoud van de provider-webservice.

## <a name="odata-based-web-services"></a>Op basis van OData-webservices
Protocol: **alleen HTTPS**

Gegevens kunnen worden weergegeven als een OData-service tooAzure Marketplace. Hallo-systeem is momenteel toopass Hallo-service via en Hallo hoofdmap van Hallo service vervangt door hello Azure Marketplace service hoofdmap – tooensure alle volgende aanroepen via Azure Marketplace gaat.

OData-services hoeft niet alleen toogo op basis van een database in Hallo back-end. OData biedt ondersteuning voor elk type opslag- of zakelijke logica toodrive Hallo-service.

## <a name="next-steps"></a>Volgende stappen
Nu dat u Hallo vereisten gecontroleerd en voltooid de benodigde taken hello, u kunt verder gaan met het maken van uw aanbieding gegevensservice als gedetailleerde in Hallo Hallo [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).

Of, indien gewenst tooreview Hallo algemene processen en Hallo respectieve artikelen voor elke Hallo fasen publiceren, gaat u naar Hallo artikel [aan de slag: hoe toopublish een aanbieding toohello Azure Marketplace](marketplace-publishing-getting-started.md).

[link-acct]:marketplace-publishing-accounts-creation-registration.md
