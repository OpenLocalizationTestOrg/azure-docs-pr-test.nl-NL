---
title: aaaSet up en gebruikt Machine Learning aanbevelingen API Hallo | Microsoft Docs
description: Microsoft aanbevelingen API gebouwd met veelgestelde vragen over Azure Machine Learning
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>Veelgestelde vragen over Recommendations-API voor Machine Learning instellen en gebruiken
**Wat is aanbevelingen?**

> [!NOTE]
> U moet beginnen met Hallo cognitieve aanbevelingen API-Service in plaats van deze versie. Hallo aanbevelingen cognitieve Service vervangt deze service en alle nieuwe functies in Hallo er zal worden ontwikkeld. Heeft nieuwe mogelijkheden, zoals batchverwerking ondersteuning, beter API Explorer, een schonere API surface, consistente aanmelding/facturering ervaring, enzovoort.
> Meer informatie over [migreren toohello nieuwe cognitieve Service](http://aka.ms/recomigrate)
> 
> 

Voor organisaties en bedrijven die afhankelijk van aanbevelingen toocross-verkopen en Upsell-producten en services tootheir klanten zijn, bevat de aanbevelingen in Azure Machine Learning een aanbevelingen selfservice-engine. Er is een implementatie van samenwerking filteren die gebruikmaakt van de matrix factoriseren als de core-algoritme. Ontwikkelaars hebben toegang tot aanbevelingen met behulp van REST-API's. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**Wat kan ik doen met aanbevelingen**

AANBEVELINGEN neemt als invoer een item of een verzameling items en geeft een lijst met relevante aanbevelingen. Bijvoorbeeld: een klant van een online winkel klikt op een product. Hallo online detailhandel product verzendt als invoer tooRECOMMENDATIONS, in een lijst van producten opgehaald en besluit welke van deze producten toohello klant wordt weergegeven. U kunt wilt toouse aanbevelingen toooptimize uw online winkel of zelfs tooinform uw binnen verkoop afdeling of aanroep center.

**Zijn er beperkingen gebruik?**

Aanbevelingen heeft Hallo na gebruik beperkingen:

* Maximumaantal modellen per abonnement: 10
* Maximum aantal items dat een catalogus kan bevatten: 100.000
* maximum aantal gebruik punten die blijven Hallo is ~ 5,000,000. Hallo oudste worden verwijderd als nieuwe wordt geüpload of gerapporteerd.
* Maximale grootte van gegevens die kunnen worden verzonden via e-mail (bijvoorbeeld importeren catalogusgegevens, gebruiksgegevens importeren) is 200 MB
* Het aantal transacties per seconde (TPS) voor een model-build van aanbevelingen die niet actief is ~ 2 TPS. Een build voor het model van aanbevelingen die actief is, kunt too20 TPS houdt.

## <a name="purchase-and-billing"></a>Kopen en facturering
**Hoeveel kost aanbevelingen periode Hallo starten?**

Aanbevelingen is een service op basis van abonnement. Opladen is gebaseerd op het volume van transacties per maand. U kunt controleren Hallo [bieden pagina](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace voor informatie over prijzen.

**Zijn er kosten in verband met de aanbevelingen die bijhouden en opslaan van Gebruikersactiviteit voor mij?**

Niet op Hallo moment.

**Heeft aanbevelingen voor een gratis proefversie**

Er is een gratis spoor die beperkte too10, 000 transacties per maand.

**Wanneer wordt ik gefactureerd voor aanbevelingen?**

Een betaald abonnement is geen abonnement waarvoor maandelijks een vast bedrag is. Wanneer u een betaald abonnement aanschaft, er zijn direct in rekening gebracht voor Hallo eerst gebruik van de maand. U Hallo hoeveelheid die is gekoppeld aan Hallo aanbieding op de pagina Hallo-abonnement (plus btw) in rekening worden gebracht. Deze maandelijkse kosten wordt gemaakt van elke maand op Hallo dezelfde datum als uw oorspronkelijke aankoop kalender totdat u Hallo abonnement annuleren. 

**Hoe voer ik een upgrade tooa hogere tier-service?**

U kunt kopen of bijwerken van uw abonnement op Hallo [bieden pagina](https://datamarket.azure.com/dataset/amla/recommendations) pagina op Microsoft Azure Marketplace.

Wanneer u een abonnement upgrade:

* Transacties die op uw oude abonnement nog niet tooyour nieuw abonnement toegevoegd. 
* U betaalt volledige prijs voor het nieuwe abonnement hello, hoewel u hebt niet-gebruikte transacties op uw oude abonnement.

Proces tooupgrade een abonnement:

* Nevigate toohello [bieden pagina](https://datamarket.azure.com/dataset/amla/recommendations).
* Meld u toohello Marketplace als u al bent niet aangemeld.
* Klik in het rechterdeelvenster Hallo worden alle Hallo beschikbare abonnementen weergegeven. Klik op het keuzerondje Hallo voor Hallo plan gewenste tooupgrade aan.
* Als u wilt dat tooupgrade, klikt u op **OK**. Als u niet dat tooupgrade wilt, klikt u op **annuleren**.

**Belangrijke** zorgvuldig lezen Hallo dialoogvenster voordat u bijwerkt, omdat er gevolgen voor facturering en het gebruik.

**Wanneer wordt mijn abonnement tooRecommendations eindigen?**

Uw abonnement wordt beëindigd als u deze annuleren. Als u toocancel wilt uw abonnementen, Zie Hallo instructies te volgen.

**Hoe annuleer ik mijn abonnement aanbevelingen**

toocancel uw abonnement, gebruik hello te volgen stappen. Als uw huidige abonnement een betaald abonnement, wordt uw abonnement actief blijft tot einde van de huidige periode facturering Hallo Hallo. Als u moet de annulering toobe effectieve onmiddellijk hello, contact met ons op [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

**Opmerking** geen restitutie krijgt als u voordat Hallo einde van een factureringsperiode of voor niet-gebruikte transacties in een factureringsperiode annuleert.

* Navigeer toohello [bieden pagina](https://datamarket.azure.com/dataset/amla/recommendations).
* Meld u toohello Marketplace als u al bent niet aangemeld.
* Klik op **annuleren** toohello rechts van de naam van de dataset Hallo en status. U kunt dit abonnement totdat het Hallo-einde van de huidige financieel periode of de Transactielimiet van uw Hallo is bereikt (indien dit eerder gebeurt eerst).

Als u uw abonnement dat wilt onmiddellijk zodat u een nieuw abonnement kunt aanschaffen bestand een ticket op toocancel [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

## <a name="getting-started-with-recommendations"></a>Aan de slag met aanbevelingen
**Is de aanbevelingen voor mij?** 

Aanbevelingen in Machine Learning is bedoeld voor organisaties en bedrijven die afhankelijk van aanbevelingen toocross verkopen en Upsell producten of services tootheir klanten zijn. Als u beschikt over een website klantgerichte, een verkoopmedewerkers, een inwendige verkoopmedewerkers of een aanroep center, en als u een catalogus van meer dan een paar dozijn producten of services aanbiedt, uw bedrijfsresultaten kunnen profiteren van aanbevelingen. 

Experimenteren met aanbevelingen is ontworpen toobe redelijk eenvoudig. Hallo huidige API-versie vereist basic programmeren. Als u hulp nodig hebt, contact met de Hallo leverancier die ontwikkeld van uw website. Als er een interne IT-afdeling of een interne ontwikkelaar, moeten ze kunnen tooget aanbevelingen toowork voor u zijn. 

**Wat zijn de vereisten voor het instellen van aanbevelingen Hallo?**

Aanbevelingen vereist dat u een logboek van de gebruiker te zien krijgt als deze zich verhoudt tooyour catalogus. Als u dergelijke logboek hebt en u een klant gerichte website hebt, kunnen aanbevelingen gebruikersactiviteit verzamelen voor u. 

Aanbevelingen moet ook een catalogus met producten en services. Als u geen Hallo catalogus hebt, kunnen aanbevelingen Hallo werkelijke klant gebruiksgegevens gebruiken en een catalogus distill. Een impliciete catalogus bevat items die niet zijn gemeld als onderdeel van de gebruikerstransacties.

**Hoe stel ik aanbevelingen voor Hallo eerst?**

Na [geabonneerde](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, moet u Hallo API-documentatie in Hallo [aanbevelingen in Azure Machine Learning - introductiehandleiding](machine-learning-recommendation-api-quick-start-guide.md) tooset Hallo-service.

**Waar vind ik API-documentatie** 

Hallo API-documentatie is [aanbevelingen voor Azure Machine Learning-introductiehandleiding](machine-learning-recommendation-api-quick-start-guide.md).

**Wat opties doen er tooupload catalogus en gebruik gegevens tooRecommendations?**

Hebt u twee opties voor het uploaden van uw data catalog en het gebruik: U kunt Hallo gegevens exporteren uit uw CRM-systeem of andere logboeken en tooRecommendations te uploaden of u labels tooyour website die u activiteiten van gebruikers bijhouden wilt kunt toevoegen. Als u de laatste Hallo-methode gebruikt, wordt de Hallo gegevens worden opgeslagen in Azure.

## <a name="maintenance-and-support"></a>Onderhoud en ondersteuning
**Hoe groot mag mijn gegevensset zijn?**

Elke set gegevens kan bevatten too100, 000 catalogusitems en too2048 MB van gebruiksgegevens.
Bovendien kan een abonnement bevatten van gegevensverzamelingen too10 (modellen).

**Waar vind ik technische ondersteuning voor aanbevelingen**

Technische ondersteuning is beschikbaar op Hallo [ondersteuning van Microsoft Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.

**Waar vind ik Hallo gebruiksvoorwaarden**

[Microsoft Azure Machine Learning-aanbevelingen API servicevoorwaarden](https://datamarket.azure.com/dataset/amla/recommendations#terms).

