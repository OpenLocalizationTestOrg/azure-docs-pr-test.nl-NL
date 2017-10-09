---
title: uw Data-Service bieden voor Hallo Marketplace aaaTesting | Microsoft Docs
description: Begrijpen hoe tootest uw Data-Service bieden voor hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a>Testen van uw Data-Service-aanbieding in fasering
> [!IMPORTANT]
> **Op dit moment wordt niet langer zijn voorbereiden op alle nieuwe gegevensservice uitgevers. Nieuwe dataservices wordt niet goedgekeurd voor de aanbieding.** Als u een SaaS-business-toepassing hebt wilt toopublish op AppSource vindt u meer informatie [hier](https://appsource.microsoft.com/partners). Als u beschikt over een IaaS-toepassingen of developer-service dat u zou zoals toopublish op Azure Marketplace vindt u meer informatie [hier](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Na het voltooien van de eerste twee stappen Hallo van [maken van uw account Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) en [maken van uw gegevens Service bieden in Publishing Portal](marketplace-publishing-data-service-creation.md) u klaar bent om uw aanbieding in Hallo beschikbaar Azure Marketplace. In dit onderwerp wordt stapsgewijs Hallo eerst, tussenliggende, naam 'Staging' stap

Fasering manier uw aanbieding in een particulier 'sandbox"waar u kunt testen en de functionaliteit ervan controleren voordat u deze tooproduction implementeren. Hallo aanbieding wordt weergegeven in de faseringsmodus net zoals tooa klant die is geïmplementeerd.

## <a name="step-1-pushing-your-offer-toostaging"></a>Step 1. Uw aanbieding toostaging pushen
Uw aanbieding toostaging pushen kunt u tootest Hallo aanbieding daarna deze beschikbaar toofuture abonnees wordt.  U kunt zien hoe uw aanbieding wordt weergegeven en werken voor de tooyour gegevens te abonneren.  

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. Aanmelden bij Hallo [Publishing Portal](https://publish.windowsazure.com)
2. Selecteer **Data Services** in Hallo linkernavigatievenster venster
3. Selecteer de gewenste toopush toostaging aanbieding. Hallo boven scherm wordt weergegeven.
4. Klik op **tooStaging Push** knop.  
5. Als er problemen zijn met Hallo aanbieding die nodig toobe zijn voorafgaande toopushing toostaging voltooid, ziet u een lijst weergegeven.  Corrigeer deze items door te klikken op elk item in de lijst Hallo. Wanneer alle correcties zijn aangebracht, klikt u op **tooStaging Push** knop opnieuw.

Als er geen problemen met uw aanbieding zijn ziet u hieronder Hallo pop-upvenster.  

Als u niet bent planning/niet goedgekeurd toosurface uw aanbieding in Azure-Portal (momenteel heeft beperkte capaciteit), en vervolgens net sluiten Hallo pop-upvenster.

tootest uw gegevens in Azure Portal-Service (in aanvulling toohello DataMarket portal), moet u een Azure-abonnements-ID tootest met.  Dit abonnement-ID wordt geïdentificeerd Hallo-account dat wordt toegestaan tootest uw aanbieding.  

Knippen en plakken van uw abonnements-ID en klikt u op Hallo vinkje toocontinue.

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> Deze id Azure-abonnementen zijn alleen vereist voor het testen en fasering in Hallo [Azure Management Portal](https://manage.windowsazure.com). Ze zijn geen vereiste tootest in Azure Marketplace.
> 
> 

Hallo volgende scherm ziet u dat publicatie plaatsvindt door Hallo 'wordt uitgevoerd' weer te geven pictogram onderstaande geel gemarkeerd. Toostaging pushen duurt tussen 10 too15 minuten.  Als het duurt langer, moet u eerst uw browser (druk op F5 in Internet Explorer) vernieuwen.  Hallo zeldzame gevallen waarin uw aanbieding is nog steeds worden gepusht toostaging na een uur, klikt u op de koppeling toolet ons weten dat er een probleem Hallo contact is.

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

Wanneer Hallo Push tooStaging Hallo is voltooid 'wordt uitgevoerd' pictogram wordt gestopt met het verplaatsen van en Hallo status wordt bijgewerkt te 'gefaseerde'.  U bent nu klaar tootest uw aanbieding.  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a>Stap 2. Testen van uw voorbereide aanbieding in DataMarket
Klik op de koppeling Hallo na de tekst hello **' Zie uw service bieden op... '** welkomstscherm toodisplay die Hallo abonnee ziet wanneer uw aanbieding tooproduction gaat en wordt weergegeven in DataMarket.

  ![tekenen](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

Testen of Controleer of elk van Hallo 12 items gemarkeerd hierboven tooensure alle logo's, prijzen/transacties, tekst, afbeeldingen, documentatie en koppelingen correct zijn en werken goed.  Dit is een goed moment tooensure een testwaarden die u hebt ingevoerd bij het maken van uw aanbieding zijn vervangen door feitelijke waarden.

1. Aanbieding-logo
2. De aanbiedingsnaam van de
3. Publisher naam/link tooyour website van bedrijf
4. Categorieën voor uw aanbieding
5. Uw aanbieding ondersteuning koppeling tooassist abonnees
6. Contextafhankelijke beschrijving voor uw aanbieding
7. Plan factureringsgegevens van aanbieding
8. Koppeling tooimplementation code
9. Voorbeeld-installatiekopieën die aangeven gebruiken van gegevens van aanbieding
10. I/o-metagegevens voor elke service binnen Hallo aanbieding
11. De gebruiksvoorwaarden van aanbieding
12. Voorbeeld van gegevens Hallo-aanbieding

Controleer ten slotte Hallo service werkt via Hallo Datamarket door te klikken op Hallo 'Deze GEGEVENSSET VERKENNEN'.  Een nieuw venster wordt geopend in Hallo hulpprogramma noemen we 'Service Explorer' zodat u een voorbeeld Hallo resultaten van een query bij uw service bekijken kunt.  In dit venster kunt u Hallo parameters nodig en Hallo resultaten weergegeven van een query op uw service te zien.   Weergegeven is bovendien Hallo-URL voor uw Query.  

> [!NOTE]
> Worden ervoor tooreview Hallo tekstbeschrijving van weergegeven boven het Hallo Hallo-service.  En als uw aanbieding uit meer dan één service bestaat aanroepen, klikt u op de tabbladen Hallo op Hallo onder tooswitch toohello volgende service tooreview en testen.
> 
> 

## <a name="next-step"></a>Volgende stap
Als u problemen ondervindt en hebt u hulp nodig fouten op te lossen neemt contact op met [ondersteuning van Azure Publisher](http://go.microsoft.com/fwlink/?LinkId=272975).

Als u tevreden bent en gereed toopublish uw aanbieding Lees Hallo [goedkeuring aanvragen tooPush tooProduction](marketplace-publishing-push-to-production.md) documentatie.

## <a name="see-also"></a>Zie ook
* [Aan de slag: Hoe toopublish een aanbieding toohello Azure Marketplace](marketplace-publishing-getting-started.md)

