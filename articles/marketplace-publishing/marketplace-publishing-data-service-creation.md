---
title: aaaGuide toocreating een gegevensservice voor Hallo Marketplace | Microsoft Docs
description: Gedetailleerde instructies waarmee toocreate, certificeren en implementeren van een Service voor gegevens aanschaffen op Hallo Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a>Gegevens Service Publishing Guide voor hello Azure Marketplace
> [!IMPORTANT]
> **Op dit moment wordt niet langer zijn voorbereiden op alle nieuwe gegevensservice uitgevers. Nieuwe dataservices wordt niet goedgekeurd voor de aanbieding.** Als u een SaaS-business-toepassing hebt wilt toopublish op AppSource vindt u meer informatie [hier](https://appsource.microsoft.com/partners). Als u beschikt over een IaaS-toepassingen of developer-service dat u zou zoals toopublish op Azure Marketplace vindt u meer informatie [hier](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Na het voltooien van Hallo-stap 1, [-Account maken en registratie](marketplace-publishing-accounts-creation-registration.md), wordt u geholpen bij Hallo [algemene niet-technische](marketplace-publishing-pre-requisites.md) en [technische vereisten](marketplace-publishing-data-service-creation-prerequisites.md) van een gegevensservice aanbieding voor Azure Marketplace. Nu we u stapsgewijs door de stappen begeleidt voor het maken van een gegevensservice aanbieding op Hallo Hallo [Publishing Portal] [ link-pubportal] voor hello Azure Marketplace.

## <a name="1----login-toohello-publishing-portal"></a>1.    Aanmelding toohello Publishing Portal.
Ga te[https://publish.windowsazure.com](https://publish.windowsazure.com.)

**Gebruik voor de eerste keer aanmelden tooPublishing Portal Hallo hetzelfde account waaraan uw bedrijf verkoper profiel is geregistreerd in het Developer Center.**  (Later kunt u toevoegen elke werknemer van uw bedrijf als een co-beheerder in Hallo Publishing Portal).

Klik op Hallo **publiceren van een Data Services** tegel als dit de eerste aanmelding Hallo bij Hallo publishing portal.

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a>2.    Kies **Data Services** in het navigatiemenu Hallo op Hallo linkerkant.
  ![tekenen](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a>3.    Een nieuwe Data-Service maken
Vul Hallo titel in voor uw nieuwe gegevens Service bieden en klik op '+' op de juiste Hallo.

  ![tekenen](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a>4.    Data-Service controleren Hallo submenu onder Hallo nieuw gemaakt in het navigatiemenu Hallo.
Klik op Hallo **scenario** tabblad en Bekijk alle benodigde stappen nodig toopublish goed Hallo gegevensservice op Hallo Azure Marketplace.

> [!TIP]
> U kunt altijd klikt u op Hallo koppelingen in Hallo 'Overzicht' pagina of tabbladen op Hallo gegevensservice aanbieding submenu aan de linkerkant hello gebruiken.
> 
> 

## <a name="5----create-a-new-plan"></a>5.    Maak een nieuw Plan.
### <a name="offers-plans-transactions"></a>Biedt, plannen, transacties.
Elke aanbieding moet meerdere abonnementen kan hebben, maar ten minste één (1) abonnement. Wanneer eindgebruikers zich tooyour aanbieding abonneert abonneren ze voor een van de aanbieding van het Hallo-Plan. Elk plan definieert hoe eindgebruikers zal worden kunnen toouse uw service.

Momenteel Azure Marketplace ondersteunen alleen maandelijkse abonnement transactie op basis van model voor Data Services, dat wil zeggen eindgebruikers maandelijkse kosten op basis van toohello prijs van de specifieke plan Hallo ze tooand geabonneerd betaalt worden elke maand aantal kunnen tooconsume de transactie is gedefinieerd door Hallo plan.

Elke transactie gewoonlijk gedefinieerd als het aantal records dat wordt geretourneerd met de Service van uw gegevens gebaseerd op Hallo query toohello Service verzonden. Hallo standaardwaarde is 100. Het aantal transacties geretourneerd tooeach query worden aantal records gedeeld door 100 en toohello dichtstbijzijnde gehele getal afgerond.

Het is Azure Marketplace Service laag verantwoordelijkheid toomonitor (meter) aantal transacties verbruikt door elke query.

> [!IMPORTANT]
> Eindgebruikers Hallo transactie tijdens Hallo maand bereikt wordt niet door kan gaan toouse Hallo service tot einde van de maandelijkse cyclus van abonnement geblokkeerd.
> 
> Hallo abonnement of een van de abonnementen Hallo kunt (maar niet moet) omvatten onbeperkt aantal transacties.
> 
> 

### <a name="create-a-plan"></a>Een schema maken.
1. Klik op **'+'** volgende toohello 'een nieuwe planning toevoegen'.
2. Kies een van de opties Hallo: **onbeperkt** of **beperkt** gebruik voor dit abonnement.  Als beperkt aantal transactie Hallo plan Hallo geeft toegestaan tooconsume in een maand.
   
    ![tekenen](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    Publiceren van de Portal wordt ook gevraagd 'Id', die worden gebruikt toocommunicate toohello eindgebruikers naam van het Hallo-plan in de gebruikersinterface Hallo Hallo en ook gebruikt door Hallo marktplaats Service tooidentify Hallo Plan. Als u wilt, kunt u Hallo 'Plan-id' wijzigen.
   
   > [!NOTE]
   > Hallo 'Id plannen' moet uniek zijn binnen het Hallo-bereik van elke aanbieding. Omdat veel andere id's worden gebruikt in Hallo Publishing Portal van plan bent id wordt vergrendeld nadat hello eerste publishing tooproduction en u niet meer kunnen toochange worden deze id.
   > 
   > 
3. Klik op tooaccept uw keuze.
4. Wordt u gevraagd enkele aanvullende vragen met betrekking tot de zojuist gemaakte planning.
   
    ![tekenen](media/marketplace-publishing-data-service-creation/step-5.2.png)

| Vraag | Significante veelvoud |
| --- | --- |
| **Dit Plan is vrij en beschikbaar wereldwijd?** |U kunt een volledig vrij van-gratis-plan maken. Als de Hallo alleen voor deze aanbieding plannen – betekent dit dat u 'Gratis bieden' in hello Marketplace publiceren wilt. Als deze alleen gebruikt voor een (van enkele wordt) Plan, Hallo dit biedt u een optie toooffer eindgebruikers toolearn-meer informatie over uw service met een relatief klein aantal transacties per maand.  Als antwoord Hallo 'Ja' is, wordt geen verdere vragen worden gevraagd. |

> [!NOTE]
> Eindgebruikers kunnen altijd toohello betaalde abonnementen bijwerken.
> 
> 

| Vraag | Significante veelvoud |
| --- | --- |
| **Gratis proefversie beschikbaar is?** |U kunt kiezen tussen 'Nee proefversie' helemaal of geven een optie toouse uw Plan 'Één maand'. Uitgevers zoals toouse deze optie tooprovide eindgebruikers Hallo mogelijkheid toounderstand Hallo voordelen van Hallo gratis gedurende één maand bieden. |

> [!IMPORTANT]
> Eindgebruikers wordt alleen kunnen toopurchase een gratis proefversie worden als ze betaalmiddel bijvoorbeeld creditcard-of enterprise-overeenkomst hebt vastgesteld.
> 
> Na één maand van de gratis proefversie hello wordt Azure Marketplace gestart opladen klanten Hallo prijs op Hallo datum van Hallo-abonnement, tenzij Hallo klant geïnitieerd Hallo abonnement annuleren. Er is geen speciale melding worden toohello eindgebruikers geleverd.
> 
> 

| Vraag | Significante veelvoud |
| --- | --- |
| **Dit abonnement is vereist om een code promotie toopurchase?** |Uitgevers hebben een optie toolimit toegang tootheir Service-plannen door op te geven van een speciale code, 'A Promocode' toospecific klanten. Alleen eindgebruikers waarvoor deze Promocode worden kunnen toosubscribe toohello Plan. Als u 'Nee' kiest, wordt u gaat ermee akkoord dat iedereen van Hallo regio waar Hallo bieden beschikbaar is (Zie [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) voor meer informatie) worden kunnen toosubscribe toothis plan. Er is geen verdere vragen gevraagd. |
| **Dit plan van iemand die niet beschikt over een geldige promotiecode ook verbergen?** |Als 'Ja' is de Hallo antwoord toohello vorige vraag heeft Hallo Publisher een optie toocompletely verwijderen van dit abonnement wordt weergegeven in de gebruikersinterface van Hallo Marketplace Hallo. Dit houdt in dat klanten niet zichtbaar voor dit abonnement in de detailpagina Hallo-aanbieding. Eindgebruikers ontvangen een toopurchase promocode, moeten kunnen toosubscribe tooit met behulp van deze promocode. |

## <a name="6----create-your-marketplace-marketing-content"></a>6.    Uw Marketplace marketing inhoud maken
Voor hoe tooprovide informatie vereist **Marketing, prijs, ondersteuning en categorieën** tabbladen gaat u naar [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) die algemene tooall artefacten die zijn gepubliceerd in Hallo is Azure Marketplace.  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a>7.    Verbinding maken met uw aanbieding tooyour Service (SQL Azure op basis van of op basis van Web-Service).
Klik op Hallo **Data Services** vervolgmenu.

Op het bovenste gedeelte van de Hallo van Hallo pagina wordt u gevraagd tooprovide Hallo aanbieding **Namespace**.  

  ![tekenen](media/marketplace-publishing-data-service-creation/step-7.png)

Hallo hieronder vraag definieert hoe Hallo Publisher tooexpose nieuw gemaakte aanbieding tooAzure Marketplace verloopt. (Zie voor meer informatie Hallo [Data Services technische vereisten Guide](marketplace-publishing-data-service-creation-prerequisites.md)).

  ![tekenen](media/marketplace-publishing-data-service-creation/step-7.2.png)

**Hallo publiceren Database op basis van service**

Klik op **Database**. Hallo na pagina wordt weergegeven:

  ![tekenen](media/marketplace-publishing-data-service-creation/step-7.3.png)

toocreate een CSDL-toewijzing voor Hallo gegevensset op basis van Hallo SQL Azure DB:

  ![tekenen](media/marketplace-publishing-data-service-creation/step-7.4.png)

En vervolgens voor elke tabel

  ![tekenen](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![tekenen](media/marketplace-publishing-data-service-creation/step-7.6.png)

Als webservice

  ![tekenen](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> Lees [toewijzing van een bestaande web-service tooOData via CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) voor gedetailleerde instructies en voorbeelden voor het maken van een CSDL-webservice.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Nu dat u uw aanbieding Data-Service hebt gemaakt, zorg ervoor dat u volledige Hallo-instructies in Hallo [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) voordat u verder gaan te[testen van uw Data-Service in de Faseringsmodus](marketplace-publishing-data-service-test-in-staging.md).

## <a name="see-also"></a>Zie ook
* [Aan de slag: Hoe toopublish een aanbieding toohello Azure Marketplace](marketplace-publishing-getting-started.md)
* Als u geïnteresseerd bent in kennis Hallo algehele proces voor OData-toewijzing en het doel, Lees dit artikel [gegevens Service OData-toewijzing](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definities, structuren en instructies.
* Als u geïnteresseerd in learning en de specifieke kennis Hallo-knooppunten en de bijbehorende parameters bent, Lees dit artikel [Service OData toewijzing gegevensknooppunten](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) voor definities en uitleg, voorbeelden en gebruik case-context.
* Als u geïnteresseerd bent in de voorbeelden controleren, Lees dit artikel [gegevens Service OData toewijzing voorbeelden](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee voorbeeldcode en begrijpen codesyntaxis en in het contextmenu.

[link-pubportal]:https://publish.windowsazure.com
