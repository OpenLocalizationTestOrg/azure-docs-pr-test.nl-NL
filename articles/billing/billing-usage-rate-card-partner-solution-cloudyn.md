---
title: aaaMicrosoft Azure gebruiks- en RateCard API's inschakelen Cloudyn tooProvide ITFM voor klanten | Microsoft Docs
description: "Biedt een unieke perspectief van Microsoft Azure Billing partner Cloudyn, op hun ervaringen hello Azure Billing-API's integreren in hun product.  Dit is vooral nuttig voor Azure en Cloudyn klanten die zijn geïnteresseerd zijn in gebruik/probeert Cloudyn voor Azure-Services."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: f1397397-7e92-4c20-9862-ab6b93afefb7
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: e221ac8b8feebb725a1cc669c8143ab829621a8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-tooprovide-itfm-for-customers"></a>Microsoft Azure gebruiks- en RateCard API's inschakelen Cloudyn tooProvide ITFM voor klanten
Gebruik van Microsoft Azure-bronnen en RateCard APIs is voor een persoonlijke preview Hallo nieuwe Cloudyn, een Microsoft-partner voor ontwikkeling en een toonaangevende leverancier van de cloud beheermogelijkheden, gekozen.  Hallo gebruik API biedt toegang tot tooestimated Azure-verbruiksgegevens voor een abonnement. Hallo RateCard API biedt volledige informatie over de prijzen van alle Azure-services, voor niet - Enterprise Agreement EA klanten. Deze API's bieden een basis voor volledige informatie voor invoer in IT financiële Management (ITFM)-hulpprogramma's zoals die worden verstrekt door Cloudyn samen geïntegreerd.

## <a name="introduction"></a>Inleiding
Hallo zogenaamde 'vermenigvuldiging' van gegevens van Hallo gebruik API met gegevens van Hallo RateCard API (gebruik [eenheden] [$unit] prijs = gedetailleerde informatie over het gebruik en de kosten) Hallo meest gedetailleerd, nauwkeurige en betrouwbare factureringsgegevens beschikbaar voor Azure vandaag maakt.

![Overzicht van ITFM][1]

Deze API's gebruiken bevat belangrijke informatie over het gebruik en kosten, waardoor het Cloudyn tooanalyze klantaccounts in een eenvoudige, programmatische manier en tooperform diverse ITFM taken zijn klanten van klanten.

## <a name="integrating-cloudyn-with-hello-ratecard-and-usage-apis"></a>Integratie van Cloudyn Hello RateCard en gebruik van API 's
Hallo RateCard API zijn verschillende invoerparameters--zoals regio info, valuta en landinstellingen-- maar Hallo belangrijkste een OfferDurableID waarin hello Azure aanbieden Hallo klant wordt gebruikt (betalen naar gebruik, verouderde 6 en 12 maanden streven is vereist plan, MSDN biedt, MPN aanbiedingen, aanbiedingen en andere). Hallo OfferDurableID vindt u in Hallo [Azure gebruiks- en facturering portal](https://account.windowsazure.com/Subscriptions), onder Hallo 'Bieden ID' voor Hallo opgegeven abonnement.

Bij de registratie voor [Cloudyn voor Azure](https://www.cloudyn.com/microsoft-azure/) services, klanten hun OfferDurableID-code, waarmee Cloudyn toopull hun relevante informatie over de prijzen via Hallo RateCard API kunnen toevoegen.  Informatie over verschillende soorten aanbiedingen Hallo vindt u een Hallo [Details van Microsoft Azure-aanbieding](https://azure.microsoft.com/support/legal/offer-details/) pagina.

![Overzicht van Cloudyn ITFM-Engine][2]

Cloudyn maakt gebruik van die beide Hallo gebruik en RateCard APIs, in aanvulling toohello Azure prestaties API, toocreate extra verificatielagen visualisatie, analytics, waarschuwingen, kosten beheer en uitvoerbare aanbevelingen, biedt Azure klanten een betrouwbare rapportage, Enterprise cloud ITFM hulpprogramma.

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a>Gebruiksvoorbeelden Cloudyn ITFM ingeschakeld door gebruik en RateCard API-integratie
Algemene Cloudyn ITFM gebruiksvoorbeelden ingeschakeld door gebruik en RateCard APIs omvatten:

* **Kosten Analysis** -cloud kunt toobe tooany systeemeigen dimensie (provider, service, account, regio, enzovoort) te identificeren onderverdeeld kosten. Hello Azure-gebruik en RateCard APIs vergemakkelijken dit een eenvoudige taak door Hallo meest gedetailleerd uitsplitsing van gebruiks- en -gegevens per account, die vervolgens gegroepeerd en gefilterd op Cloudyn en toohello-gebruiker in de vorm van een afbeelding of in tabelvorm weergegeven.

![Kosten van het cirkeldiagram analyse][3]

* **Toewijzing 360 kosten** -schakelt Financiën en IT-managers toouncover Hallo werkelijke kosten uitsplitsing, stuurprogramma's en trends van hun cloudimplementatie. Verder kunt u managers tooeasily koppelen implementatie uitgaven met meer bedrijfseenheden, afdelingen en regio's bieden een ongekende inzicht in de cloud kosten en om verrekening enterprise en showbacks te vergemakkelijken. Hello Azure-gebruik en RateCard APIs fungeren als invoer tooCloudyn kosten toewijzing-engine is een aanvulling op Hallo API's door methoden en zakelijke logica voor het toewijzen van niet-gecodeerde of untaggable resources te definiëren.

![Kosten toewijzing 360-grafiek][4]

* **Rendabele Sizing** -juiste formaat van aanbevelingen voor onderbenutte virtuele machines, zodat de kosten van de klant Hallo op te groot of te weinig ingerichte computers. Dit gebeurt door virtuele machines CPU en RAM-geheugen metrische gegevens (via prestaties API), in uren van de runtime (via de API van gebruik) en de kosten (via RateCard API). Cloudyn juiste formaat aanbevelingen op basis van onderbenutte RAM of CPU-resources (prestaties) en berekent de geschatte besparingen vermenigvuldigd Hallo prijs delta (RateCard) tussen VM's Hallo door Hallo werkelijk tijd-verbruik (gebruik) Hallo onderbenutte machine.

![Rendabel schaling][5]

* **Aanbevelingen voor het overdragen van cloud** -financiële advies bevat op cloud overdragen. Het huidige kosten van cloudresources die zijn geïmplementeerd op de primaire cloud leveranciers van een gebruiker moet worden gecontroleerd en vergelijkt deze met een toohello kosten van de implementatie van een equivalent in Azure. Vervolgens wordt gedetailleerd, per resource, financiële gebaseerde aanbevelingen tooAzure overdragen. Na het evalueren van gelijkwaardige Hallo-implementatie vereist in Azure (op basis van voorkeuren voor prestaties metrische gegevens en de gebruiker) gebruikt Cloudyn hello RateCard API tooevaluate Hallo implementatiekosten Hallo equivalent op Azure.
* **Prestatierapporten** -ingeschakeld door de prestaties van de Azure API, deze rapporten bieden een matrix van functies van CPU-en RAM-geheugen toooptimization aanbevelingen. Hieronder staat een exemplaar gebruik rapport voorbeeld, exemplaar uitsplitsing aangeboden door het gemiddelde CPU-gebruik.

![Prestatierapporten][6]

* **Categoriemanager** -een krachtige functie in Cloudyn die ook volgorde toounorganized cloudresources. Het biedt gebruikers Hallo vrijheid toocreate hun eigen unieke categorieën (tags) voor het effectieve meten en rapportage die in overeenstemming met de bedrijfsvoering is. Verder kan kunnen gebruikers eenvoudig reguleren en categoriseren inconsistente tagging (dat wil zeggen typefouten en andere verschillen) en niet-gecodeerde bronnen voor toekenning van een nauwkeurige kostenberekening automatisch detecteren.

![Categorie Manager][7]

## <a name="video"></a>Video
Hier volgt een korte video die laat zien hoe een Azure-klant Cloudyn kunt gebruiken voor Azure en hello Azure Billing-API's, toogain inzicht in de Azure-verbruik-gegevens.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Start een gratis [Cloudyn voor Azure](https://www.cloudyn.com/microsoft-azure/) proefversie toosee hoe kunt u kosten transparantie met aangepaste rapportage en analyse voor de implementatie van uw Microsoft Azure-cloud.
* Zie [inzicht in uw Microsoft Azure-brongebruik](billing-usage-rate-card-overview.md) voor een overzicht van hello Azure brongebruik en RateCard APIs.
* Bekijk Hallo [Azure Billing REST API-verwijzing](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) voor meer informatie over beide API's die deel uitmaken van Hallo set API's die worden geleverd door hello Azure Resource Manager.
* Als u toodive in de voorbeeldcode Hallo wilt, Bekijk onze Microsoft Azure Billing API codevoorbeelden op [Azure codevoorbeelden](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>Meer informatie
* toolearn meer informatie over de aanbiedingen van Microsoft Azure Enterprise Agreement (EA), gaat u naar [Azure voor Hallo Enterprise-licentieverlening](https://azure.microsoft.com/pricing/enterprise-agreement/)
* Zie Hallo [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) artikel toolearn meer over hello Azure Resource Manager.
* Voor meer informatie over Hallo-suite met hulpprogramma's te besteden aan de benodigde toohelp krijgt u inzicht hebben in de cloud, raadpleegt u te Gartner artikel [markt-handleiding voor IT financiële Management (ITFM)-hulpprogramma's voor](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
