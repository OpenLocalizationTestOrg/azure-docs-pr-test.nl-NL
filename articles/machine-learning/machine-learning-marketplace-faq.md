---
title: (afgeschaft) Veelgestelde vragen over - publiceren en gebruiken van Machine Learning-apps in Azure Marketplace | Microsoft Docs
description: (afgeschaft) Veelgestelde vragen over Machine Learning-apps publiceren in Azure Marketplace
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a4631dfeb2f817b3a3c612a8f6af48398e4f2ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a>(afgeschaft) Publiceren en gebruiken van Machine Learning-apps in Azure Marketplace: veelgestelde vragen

> [!NOTE]
> DataMarket en Data Services worden gesteld en bestaande abonnementen wordt buiten gebruik worden gesteld en geannuleerd vanaf 3/31/2017. Als gevolg hiervan wordt in dit artikel afgeschaft. 
> 
> Als alternatief kunt u uw Machine Learning-experimenten te publiceren de [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) ten behoeve van de community van de wetenschappelijke gegevens. Zie voor meer informatie [Share en het detecteren van bronnen in de Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).


## <a name="questions-about-consuming-from-marketplace"></a>Vragen over het gebruiken van Marketplace
**1. Waarom krijg ik het volgende foutbericht weergegeven wanneer ik invoer hebt ingevoerd voor de webservice:**

**De aanvraag heeft een back-end time-out- of back-end-fout. Het team onderzoekt het probleem. We kunnen onze excuses voor het ongemak. (500)**

De parameters mogelijk niet overeen met de vereiste indeling voor de specifieke webservice. Raadpleeg de bijbehorende documentatie-koppeling om de juiste notatie voor de invoerparameters en de beperkingen van deze webservice te vinden.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. Als het kopiëren van de API-koppeling voor de webservice die op de pagina 'Verkennen deze gegevensset' en plak deze in een ander browservenster wat referenties moet ik gebruiken voor toegang tot de resultaten en hoe kan ik ze zien?**

U moet uw Marketplace-account gebruiken als de gebruikersnaam en de primaire toegangssleutel als het wachtwoord. Primaire sleutel vindt u op de **verkennen van deze gegevensset** pagina onder de beschrijving van de webservice (Klik op de **weergeven** knop). Het resultaat wordt mogelijk weergegeven in de browser of mogelijk worden gedownload, afhankelijk van welke browser die u gebruikt.

**3. Waarom krijg ik het volgende foutbericht weergegeven wanneer ik de invoer hebt ingevoerd voor de webservice op de pagina 'Verkennen deze gegevensset':** 

**Een onverwachte fout opgetreden tijdens het verwerken van uw aanvraag. Probeer het opnieuw.**

Een of meer invoerparameters van uw web-service kunnen hebben overschrijdt de maximale lengte wanneer de web-service op marketplace worden verbruikt **verkennen van deze gegevensset** pagina. De services kunnen worden aangeroepen met een meer invoerlengte via HTTP POST-methoden. Zie voor voorbeelden [steekproef oplossingen met R op Machine Learning en gepubliceerd naar Marketplace](machine-learning-r-csharp-web-service-examples.md).

**4. Waarom kan ik niet zien in de 'API EXPLORER' tabblad int het archief in de klassieke Azure Portal niets?** 

Dit is een bekend probleem met de klassieke Azure Portal Marketplace. Dit probleem oplossen door werkt het team. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>Vragen over het publiceren van Azure Machine Learning op Marketplace
**1. Waarom zijn mijn transacties logo's of afbeeldingen niet vernieuwen voor Mijn webservice?** 

Logo's en afbeeldingen in cache zijn opgeslagen in de portal voor publiceren en het duurt maximaal 10 dagen voor de nieuwe logo of de afbeelding om bij te werken op de portal.

**2. Waarom is het tabblad 'Details' van Mijn webservice op Marketplace een foutbericht weergegeven?**

Er is een bekend probleem in de Marketplace bij het verbinden met Azure Machine Learning voor service-informatie. Dit probleem oplossen door werkt het team.

**3. Waarom de voorbeeldcode R in de Azure Machine Learning-webservices werkt niet voor het verbruik van de web-services Marketplace?**

De verificatiesystemen zijn verschillend bij het verbinden met Azure Machine Learning-webservices rechtstreeks vergeleken met de verbinding te maken met deze webservices via de Marketplace. De services in Marketplace OData-services zijn en ze kunnen worden aangeroepen met de methoden GET of POST. 

**4. Waarom zijn de koppelingen voor ondersteuning van mijn web-service biedt voor sommige mijn aanbiedingen niet correct bijgewerkt?**

De koppelingen ondersteuning zijn globaal per uitgever, niet per aanbieding. 

**5. Hoe kan ik een webservice met invoer batchmodus publiceren in de Marketplace?**

De invoermodus batch wordt momenteel niet ondersteund in de Marketplace-webservices.

**6. Wie moet ik contact opnemen voor hulp als ik vragen hebt over een uitgever is of als er problemen tijdens de publicatie?**

Neem contact op met het team van Azure Marketplace via < mailto:datamarketbd@microsoft.com > voor meer informatie.

