---
title: Gebruik van Microsoft Azure en RateCard API's inschakelen Cloudyn ITFM om klanten te bieden | Microsoft Docs
description: "Biedt een unieke perspectief van Microsoft Azure Billing partner Cloudyn, op hun ervaringen van de Azure Billing API's integreren in hun product.  Dit is vooral nuttig voor Azure en Cloudyn klanten die zijn geïnteresseerd zijn in gebruik/probeert Cloudyn voor Azure-Services."
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
ms.openlocfilehash: fac0ee2e9cbc87c8b3d04675551bba61f7a532b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-to-provide-itfm-for-customers"></a>Microsoft Azure-gebruik en RateCard API's inschakelen Cloudyn ITFM om klanten te bieden
Cloudyn, een Microsoft-partner voor ontwikkeling en een toonaangevende leverancier van de beheermogelijkheden voor cloud hebt gekozen voor een persoonlijke voorbeeld van de nieuwe Microsoft Azure-brongebruik en RateCard APIs.  De informatie over het gebruik API biedt toegang tot gegevens van de geschatte Azure-verbruik voor een abonnement. De API RateCard biedt volledige informatie over de prijzen van alle Azure-services, voor niet - Enterprise Agreement EA klanten. Deze API's bieden een basis voor volledige informatie voor invoer in IT financiële Management (ITFM)-hulpprogramma's zoals die worden verstrekt door Cloudyn samen geïntegreerd.

## <a name="introduction"></a>Inleiding
De zogenaamde 'vermeerdering' van de gegevens van de API voor gebruik met gegevens van de API RateCard (gebruik [eenheden] [$unit] prijs = gedetailleerde informatie over het gebruik en de kosten van) de meest gedetailleerd, nauwkeurige en betrouwbare factureringsgegevens beschikbaar voor Azure vandaag maakt.

![Overzicht van ITFM][1]

Deze API's gebruiken bevat belangrijke informatie over het gebruik en kosten, zodat Cloudyn klantaccounts analyseren in een eenvoudige, programmatische manier en voor het uitvoeren van verschillende ITFM taken voor de klanten van klanten.

## <a name="integrating-cloudyn-with-the-ratecard-and-usage-apis"></a>Cloudyn integreren met de RateCard en het gebruik van API 's
De API RateCard verschillende invoerparameters--zoals regio info, valuta en landinstellingen--vereist, maar het belangrijkste instrument is OfferDurableID waarin de Azure-aanbieding van de klant wordt gebruikt (betalen naar gebruik, verouderde 6 en 12 maanden streven plannen, MSDN-aanbiedingen, MPN aanbiedingen, aanbiedingen en andere). De OfferDurableID vindt u in de [Azure gebruiks- en facturering portal](https://account.windowsazure.com/Subscriptions), onder het 'bieden ID' voor het opgegeven abonnement.

Bij de registratie voor [Cloudyn voor Azure](https://www.cloudyn.com/microsoft-azure/) services, klanten hun OfferDurableID-code, waarmee Cloudyn voor het ophalen van de relevante informatie over de prijzen via de API RateCard kunnen toevoegen.  Informatie over de verschillende soorten aanbiedingen vindt u een de [Details van Microsoft Azure-aanbieding](https://azure.microsoft.com/support/legal/offer-details/) pagina.

![Overzicht van Cloudyn ITFM-Engine][2]

Cloudyn gebruikt de informatie over het gebruik en RateCard APIs, naast de API van de prestaties van Azure voor het maken van extra verificatielagen visualisatie, analytics, waarschuwingen, rapportage, kostenbeheer en uitvoerbare aanbevelingen biedt Azure klanten een betrouwbare enterprise cloud ITFM hulpprogramma.

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a>Gebruiksvoorbeelden Cloudyn ITFM ingeschakeld door gebruik en RateCard API-integratie
Algemene Cloudyn ITFM gebruiksvoorbeelden ingeschakeld door gebruik en RateCard APIs omvatten:

* **Kosten Analysis** -cloud kunt kosten worden verdeeld in de native identificerende dimensies (provider, service, account, regio, enzovoort). Het gebruik van Azure en RateCard APIs dit aan de hand van de meest gedetailleerd uitsplitsing van het gebruik van een eenvoudige taak maken en kostengegevens per account, die vervolgens gegroepeerd en gefilterd op Cloudyn en gepresenteerd aan de gebruiker, in de vorm van een afbeelding of in tabelvorm.

![Kosten van het cirkeldiagram analyse][3]

* **Toewijzing 360 kosten** -kunt u financiën en IT-beheerders om de verdeling van de werkelijke kosten, stuurprogramma's en trends van hun cloudimplementatie. Kunt u meer beheerders gemakkelijk implementatie uitgaven koppelen aan meer bieden ongekende inzicht in de cloud kosten en de enterprise verrekening en showbacks bedrijfseenheden, afdelingen en regio's. Het gebruik van Azure en RateCard APIs fungeren als invoer voor de Cloudyn kosten toewijzing-engine is een aanvulling op de API's door methoden en zakelijke logica voor het toewijzen van niet-gecodeerde of untaggable resources te definiëren.

![Kosten toewijzing 360-grafiek][4]

* **Rendabele Sizing** -juiste formaat van aanbevelingen voor onderbenutte virtuele machines, verkleint u de kosten van de klant op te groot of te weinig ingerichte computers. Dit gebeurt door virtuele machines CPU en RAM-geheugen metrische gegevens (via prestaties API), in uren van de runtime (via de API van gebruik) en de kosten (via RateCard API). Cloudyn juiste formaat aanbevelingen op basis van onderbenutte RAM of CPU-resources (prestaties), en geschatte besparingen berekend vermenigvuldigd met de prijs delta (RateCard) tussen de virtuele machines door de werkelijke tijd-gebruik (gebruik) van de onderbenutte machine.

![Rendabel schaling][5]

* **Aanbevelingen voor het overdragen van cloud** -financiële advies bevat op cloud overdragen. Het huidige kosten van cloudresources die zijn geïmplementeerd op de primaire cloud leveranciers van een gebruiker moet worden gecontroleerd en vergelijkt deze met de kosten van de implementatie van een equivalent in Azure. Vervolgens wordt gedetailleerd, per resource, financiële gebaseerde overdragen aanbevelingen naar Azure. Na het evalueren van de equivalente implementatie vereist op Azure (op basis van voorkeuren voor prestaties metrische gegevens en de gebruiker) gebruikt Cloudyn de RateCard-API voor het evalueren van de kosten van de equivalente implementatie op Azure.
* **Prestatierapporten** -ingeschakeld door de prestaties van de Azure API, deze rapporten bieden een matrix van functies van CPU-en RAM-geheugen optimalisatie aanbevelingen. Hieronder staat een exemplaar gebruik rapport voorbeeld, exemplaar uitsplitsing aangeboden door het gemiddelde CPU-gebruik.

![Prestatierapporten][6]

* **Categoriemanager** -een krachtige functie in Cloudyn die volgorde naar ongeordende cloudresources brengt. Deze biedt gebruikers de vrijheid om hun eigen unieke categorieën (tags) maken voor het effectieve meten en rapportage die in overeenstemming met de bedrijfsvoering. Verder kan kunnen gebruikers eenvoudig reguleren en categoriseren inconsistente tagging (dat wil zeggen typefouten en andere verschillen) en niet-gecodeerde bronnen voor toekenning van een nauwkeurige kostenberekening automatisch detecteren.

![Categorie Manager][7]

## <a name="video"></a>Video
Hier volgt een korte video die hoe een Azure-klant Cloudyn voor Azure en de Azure Billing-API's toont, kunt gebruiken voor het verkrijgen van inzicht in de Azure-verbruik-gegevens.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Start een gratis [Cloudyn voor Azure](https://www.cloudyn.com/microsoft-azure/) evaluatieversie om te zien hoe u kunt verkrijgen kosten transparantie met aangepaste rapportage en analyse voor de implementatie van uw Microsoft Azure-cloud.
* Zie [inzicht in uw Microsoft Azure-brongebruik](billing-usage-rate-card-overview.md) voor een overzicht van het gebruik van Azure-bronnen en RateCard APIs.
* Bekijk de [Azure Billing REST API-verwijzing](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) voor meer informatie over beide API's die deel uitmaken van de reeks API's die zijn opgegeven door de Azure Resource Manager.
* Als u meteen rechts in de voorbeeldcode wilt, Bekijk onze Microsoft Azure Billing API codevoorbeelden op [Azure codevoorbeelden](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>Meer informatie
* Voor meer informatie over de aanbiedingen van Microsoft Azure Enterprise Agreement (EA), gaat u naar [Azure licentieverlening voor de onderneming](https://azure.microsoft.com/pricing/enterprise-agreement/)
* Zie de [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) artikel voor meer informatie over de Azure Resource Manager.
* Voor meer informatie over de suite met hulpprogramma's die nodig zijn om u te helpen bij het krijgen van een goed begrip van de cloud te besteden aan, raadpleegt u Gartner artikel [markt-handleiding voor IT financiële Management (ITFM)-hulpprogramma's voor](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
