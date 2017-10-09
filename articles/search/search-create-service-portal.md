---
title: een Azure Search-service in de portal Hallo aaaCreate | Microsoft Docs
description: Een Azure Search-service in de portal Hallo inrichten.
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a>Maken van een Azure Search-service in Hallo-portal

Dit artikel wordt uitgelegd hoe toocreate of het inrichten een Azure Search-service in Hallo-portal. Zie voor instructies PowerShell [Azure Search beheren met PowerShell](search-manage-powershell.md).

## <a name="subscribe-free-or-paid"></a>Abonneren (gratis of betaalde)

[Een gratis Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) en gebruik gratis tegoed tootry uit betaalde Azure-services. Nadat het tegoed is gebruikt, Hallo account houden en toouse gratis Azure-services, zoals Websites worden voortgezet. Uw creditcard is nooit in rekening gebracht tenzij u expliciet de instellingen wijzigen en vraag toobe in rekening gebracht.

U kunt ook [voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Een MSDN-abonnement ontvangt u elke maand tegoeden die kunt u voor betaalde Azure-services. 

## <a name="find-azure-search"></a>Zoeken naar Azure Search
1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Klik op Hallo plus -teken ('+') in de linkerbovenhoek Hallo.
3. Selecteer **Web en mobiel** > **Azure Search**.

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a>Naam Hallo-service en de URL-eindpunt

Naam van een service maakt deel uit van Hallo URL-eindpunt op basis waarvan de API-aanroepen zijn uitgegeven. Typ de servicenaam van uw in Hallo **URL** veld. 

Vereisten voor service-naam:
   * 2 en 60 tekens lang zijn
   * kleine letters, getallen of streepjes ('-')
   * Er is geen streepje ('-') als Hallo eerst 2 tekens of laatste teken
   * Er zijn geen twee opeenvolgende streepjes ('--')

## <a name="select-a-subscription"></a>Een abonnement selecteren
Als u meer dan één abonnement hebt, kiest u dat ook gegevens of file storage-services heeft. Azure Search kunt automatische detectie Azure Table- en Blob-opslag, SQL-Database en Azure Cosmos DB voor indexeren *indexeerfuncties*, maar alleen voor services in Hallo hetzelfde abonnement.

## <a name="select-a-resource-group"></a>Een resourcegroep selecteren
Een resourcegroep is een verzameling Azure-services en bronnen die samen worden gebruikt. Bijvoorbeeld, als u van Azure Search tooindex een SQL-database gebruikmaakt, klikt u vervolgens beide services moeten deel uitmaken van Hallo dezelfde resourcegroep.

> [!TIP]
> Verwijderen van een resourcegroep verwijderd Hallo services binnen deze ook. Voor prototype projecten met behulp van meerdere services, zodat ze allemaal Hallo gemakkelijker dezelfde resourcegroep opschoning nadat het Hallo-project is voltooid. 

## <a name="select-a-hosting-location"></a>Selecteer een hosting-locatie 
Als een Azure-service kan de Azure Search in datacenters Hallo wereld worden gehost. Houd er rekening mee dat [prijzen kunnen verschillen](https://azure.microsoft.com/pricing/details/search/) per Geografie.

## <a name="select-a-pricing-tier-sku"></a>Selecteer een prijscategorie (SKU)
[Azure Search momenteel wordt aangeboden in meerdere Prijscategorieën](https://azure.microsoft.com/pricing/details/search/): gratis, basis of standaard. Elke laag heeft zijn eigen [capaciteit en limieten](search-limits-quotas-capacity.md). Zie [Kies een prijscategorie laag of SKU](search-sku-tier.md) voor hulp.

In dit overzicht hebben we Hallo standaardcategorie gekozen voor onze service.

## <a name="create-your-service"></a>Uw service maken

Houd er rekening mee toopin uw dashboard service toohello voor eenvoudige toegang wanneer u zich aanmeldt.

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a>Schalen van uw service
Het kan enkele minuten toocreate een service (15 minuten of langer, afhankelijk van het Hallo-laag) duren. Nadat de service is geconfigureerd, kunt u de schaal het toomeet uw behoeften. Omdat u de standaardcategorie Hallo voor uw Azure Search-service kiest, kunt u uw service schalen in twee dimensies: replica's en partities. Had u Hallo basisstaffel gekozen, kunt u alleen toevoegen replica's. Als u de gratis service Hallo ingericht, is scale niet beschikbaar.

***Partities*** toestaan uw service toostore en zoek via meer documenten.

***Replica's*** een hogere belasting van zoekopdrachten voor uw service toohandle toestaan.

> [!Important]
> Een service moet hebben [2 replica's voor alleen-lezen-SLA en 3 replica's voor lezen/schrijven SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

1. Ga tooyour search-service-blade in hello Azure-portal.
2. Selecteer in het deelvenster navigatie aan de linkerkant Hallo **instellingen** > **Scale**.
3. Hallo slidebar tooadd replica's of partities gebruiken.

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> Elke laag zijn verschillende [limieten](search-limits-quotas-capacity.md) van totaal aantal Search-eenheden die zijn toegestaan in een enkele service hello (replica's * partities totaal aantal Search-eenheden =).

## <a name="when-tooadd-a-second-service"></a>Wanneer een tweede service tooadd

Een grote meerderheid van klanten gebruik slechts één service ingericht op een laag die Hallo biedt [rechtermuisknop saldo van resources](search-sku-tier.md). Een service kunt hosten meerdere indexen, onderwerp toohello [Hallo laag die u selecteert deze limieten](search-capacity-planning.md), met elke geïsoleerd van een andere index. In Azure Search aanvragen kunnen slechts worden gerichte tooone index, minimaliseert de kans op Hallo van per ongeluk of opzettelijk gegevens ophalen van andere in Hallo dezelfde indexen service.

Hoewel de meeste klanten slechts één service gebruikt, is het mogelijk dat service redundantie nodig als operationele vereisten Hallo volgende opnemen:

+ Herstel na noodgevallen (onderbreking datacentrum). Azure Search biedt geen chatberichten failover in Hallo-gebeurtenis van een storing. Zie voor aanbevelingen en richtlijnen [Service-beheer](search-manage.md).
+ Uw onderzoek van multi-tenancymodus modellering heeft vastgesteld dat extra services Hallo optimaal ontwerp. Zie voor meer informatie [ontwerp voor multi-tenancy](search-modeling-multitenant-saas-applications.md).
+ Voor globaal geïmplementeerde toepassingen mogelijk u een exemplaar van Azure Search in meerdere regio's toominimize latentie van de internationale verkeer van uw toepassing.

> [!NOTE]
> In Azure Search kan niet u werkbelastingen voor indexering en opvragen; scheiden Zo maakt u meerdere services voor gescheiden werkbelastingen nooit. Een index is altijd opgevraagd op Hallo service waarin het is gemaakt (u kunt geen een index in een service maken of kopiëren tooanother).
>

Een tweede service is niet vereist voor hoge beschikbaarheid. Hoge beschikbaarheid voor query's wordt bereikt wanneer u 2 of meer replica's in dezelfde service Hallo. Replica-updates zijn sequentiële, ten minste één operationeel is wanneer een service-update is geïmplementeerd. Zie voor meer informatie over bedrijfstijd [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

## <a name="next-steps"></a>Volgende stappen
Na het inrichten van een Azure Search-service, bent u klaar te[een index definiëren](search-what-is-an-index.md) zodat u kunt uploaden en uw gegevens te zoeken.

Hallo-service van code of het script tooaccess Hallo-URL opgeven (*servicenaam*. search.windows.net) en een sleutel. Beheersleutels bieden volledige toegang. querysleutels verlenen alleen-lezen toegang. Zie [hoe toouse Azure zoeken in .NET](search-howto-dotnet-sdk.md) tooget gestart.

Zie [bouwen en query uitvoeren op uw eerste index](search-get-started-portal.md) voor een snelle zelfstudie op basis van de portal.

