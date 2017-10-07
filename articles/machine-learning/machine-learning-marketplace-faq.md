---
title: Veelgestelde vragen over - aaa(deprecated) publiceren en gebruiken van Machine Learning-apps in Azure Marketplace | Microsoft Docs
description: (afgeschaft) Veelgestelde vragen over Machine Learning-apps publiceren in hello Azure Marketplace
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
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a>(afgeschaft) Publiceren en gebruiken van Machine Learning-apps in Azure Marketplace Hallo: veelgestelde vragen

> [!NOTE]
> DataMarket en Data Services worden gesteld en bestaande abonnementen wordt buiten gebruik worden gesteld en geannuleerd vanaf 3/31/2017. Als gevolg hiervan wordt in dit artikel afgeschaft. 
> 
> Als alternatief kunt u uw Machine Learning-experimenten toohello kunt publiceren [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) voor Hallo voordeel van het Hallo gegevens wetenschappelijke community. Zie voor meer informatie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).


## <a name="questions-about-consuming-from-marketplace"></a>Vragen over het gebruiken van Marketplace
**1. Waarom krijg ik het volgende foutbericht wordt weergegeven nadat ik invoer voor de webservice Hallo Hallo:**

**Hallo-aanvraag heeft een back-end time-out- of back-end-fout. Hallo-team onderzoekt Hallo probleem zijn. We kunnen onze excuses voor het ongemak Hallo. (500)**

De parameters voldoet mogelijk niet de vereiste indeling toohello voor specifieke Hallo-webservice. Raadpleeg toohello bijbehorende documentatie toofind Hallo juiste indeling voor de koppeling voor de invoerparameters en Hallo beperkingen van deze webservice.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. Als ik kopieer Hallo API-koppeling voor Hallo-webservice die ik Zie op de pagina 'Verkennen deze gegevensset' Hallo en plak deze in een ander browservenster, welke referenties moet ik tooaccess Hallo resultaten gebruiken en hoe kan ik zien?**

U moet uw Marketplace-account gebruiken als Hallo gebruikersnaam en het Hallo primaire sleutel als Hallo wachtwoord. Hallo primaire sleutel vindt u op Hallo **verkennen van deze gegevensset** pagina onder Hallo beschrijving van de webservice hello (Klik op Hallo **weergeven** knop). Hallo resultaat wordt mogelijk weergegeven in de browser Hallo of wordt mogelijk beschikbaar te downloaden, afhankelijk van welke browser die u gebruikt.

**3. Waarom krijg ik Hallo volgende foutbericht wordt weergegeven nadat ik Hallo invoer voor Hallo-webservice op Hallo 'Verkennen deze gegevensset' pagina:** 

**Een onverwachte fout opgetreden tijdens het verwerken van uw aanvraag. Probeer het opnieuw.**

Een of meer invoerparameters van uw web-service is overschreden Hallo lengtelimiet wanneer verbruikt Hallo-webservice op Hallo marketplace **verkennen van deze gegevensset** pagina. Hallo-services kunnen worden aangeroepen met een meer invoerlengte via HTTP POST-methoden. Zie voor voorbeelden [steekproef oplossingen met R op Machine Learning en gepubliceerde tooMarketplace](machine-learning-r-csharp-web-service-examples.md).

**4. Waarom kan ik niet zien in Hallo 'API EXPLORER' tabblad int Hallo Store in de klassieke Azure-Portal Hallo niets?** 

Dit is een bekend probleem met hello Azure Classic Portal Marketplace. Hallo-team werkt tooresolve dit probleem. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>Vragen over het publiceren van Azure Machine Learning op Marketplace
**1. Waarom zijn mijn transacties logo's of afbeeldingen niet vernieuwen voor Mijn webservice?** 

Logo's en afbeeldingen in cache zijn opgeslagen in de portal voor het publiceren van Hallo en het too10 dagen voor nieuwe logo Hallo of afbeelding tooupdate op Hallo portal kan duren.

**2. Waarom is Hallo ' ' detailtabblad van mijn web-service op een foutbericht weergegeven Marketplace?**

Er is een bekend probleem in de Marketplace bij het verbinden van Machine Learning tooAzure voor service-informatie. Hallo-team werkt tooresolve dit probleem.

**3. Waarom Hallo R voorbeeldcode in hello Azure Machine Learning-webservices werkt niet voor in beslag neemt Hallo-webservices in de Marketplace?**

Hallo verificatiesystemen zijn verschillend vergelijking rechtstreeks verbinding maken met Machine Learning-webservices tooAzure tooconnecting toothese webservices via Hallo Marketplace. Hallo-services in Marketplace OData-services zijn en ze kunnen worden aangeroepen met de methoden GET of POST. 

**4. Waarom zijn Hallo ondersteuning koppelingen van Mijn webservice biedt voor sommige mijn aanbiedingen niet correct bijgewerkt?**

Hallo ondersteuning koppelingen zijn globale per uitgever, niet per aanbieding. 

**5. Hoe kan ik een webservice met invoer batchmodus publiceren in de Marketplace?**

Hallo batch invoermodus is momenteel niet ondersteund in de Marketplace-webservices.

**6. Wie moet ik contact opnemen met help tooget als ik vragen hebt over een uitgever is, of als er problemen tijdens de publicatie?**

Neem contact op met de Hallo Azure Marketplace-team via < mailto:datamarketbd@microsoft.com > voor meer informatie.

