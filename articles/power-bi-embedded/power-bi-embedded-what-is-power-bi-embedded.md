---
title: aaaWhat is Microsoft Power BI Embedded?
description: Power BI Embedded kunt u toointegrate Power BI-rapporten in uw web- of mobiele toepassingen zodat u niet toobuild aangepaste oplossingen hoeft.
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 03649b72-b7d7-40ca-b077-12356d72d4f3
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/20/2017
ms.author: asaxton
ms.openlocfilehash: 0353938b6cdd9bb58b123b250f45f76b8cc7abe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>Wat is Microsoft Power BI Embedded?
Met **Power BI Embedded**, kunt u Power BI-rapporten integreren in uw web- of mobiele toepassingen.

![](media/powerbi-embedded-whats-is/what-is.png)

Power BI Embedded is een **Azure service** waarmee ISV's en de ervaring van app-ontwikkelaars toosurface Power BI-gegevens binnen hun toepassingen. Als een ontwikkelaar u toepassingen hebt gemaakt en deze toepassingen hebben hun eigen gebruikers en een afzonderlijke reeks functies. Deze apps kunnen ook een aantal ingebouwde gegevenselementen zoals grafieken en rapporten die kunnen nu worden aangestuurd door Microsoft Power BI Embedded toohave gebeuren. U hoeft niet een Power BI-account toouse uw app. U kunt doorgaan toosign in tooyour toepassing net als voorheen kunt en bekijken en communiceren met de Hallo reporting Power BI-ervaring zonder aanvullende licenties.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Licenties voor Microsoft Power BI Embedded
In Hallo **Microsoft Power BI Embedded** gebruiksmodel, voor Power BI niet Hallo verantwoordelijkheid van de eindgebruiker Hallo is-licentieverlening.  In plaats daarvan **sessies** zijn aangeschaft door de ontwikkelaar Hallo van Hallo app verbruikt Hallo visuele elementen en toohello-abonnement dat eigenaar is van deze resources in rekening worden gebracht. Als u meer informatie vindt u op Hallo [pagina met prijzen](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Microsoft Power BI Embedded conceptuele model

![](media/powerbi-embedded-whats-is/model.png)

Net als elke andere service in Azure-resources voor Power BI Embedded zijn ingericht via Hallo [Azure Resource Manager-API's](https://msdn.microsoft.com/library/mt712306.aspx). In dit geval Hallo resource die u inricht is een **Power BI-Werkruimteverzameling**.

## <a name="workspace-collection"></a>Werkruimteverzameling
Een **Werkruimteverzameling** is Hallo op het hoogste niveau Azure container voor bronnen met 0 of meer **werkruimten**.  Een **werkruimte** **verzameling** heeft alle hello Azure standaardeigenschappen, evenals Hallo volgende:

* **Toegangssleutels** – sleutels die worden gebruikt bij het aanroepen van veilig Hallo Power BI-API's (beschreven in een volgende sectie).
* **Gebruikers** : Azure Active Directory (AAD)-gebruikers met administrator-rechten toomanage Hallo Power BI-Werkruimteverzameling via hello Azure-portal of Azure Resource Manager-API.
* **Regio** : als onderdeel van het inrichten van een **Werkruimteverzameling**, kunt u een regio toobe ingericht in. Zie voor meer informatie [Azure-gebieden](https://azure.microsoft.com/regions/).

## <a name="workspace"></a>Werkruimte
Een **werkruimte** is een container van Power BI-inhoud, die kan bestaan uit gegevenssets en rapporten. Een **werkruimte** is leeg wanneer het eerst hebt gemaakt. U gaat ontwerpen inhoud met behulp van Power BI Desktop en u hebt Hallo PBIX programmatisch implementeren in de werkruimte op basis van Hallo [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx). U kunt ook programmatisch maken uw gegevensset en maak vervolgens rapporten in uw toepassing in plaats van Power BI Desktop.

## <a name="using-workspace-collections-and-workspaces"></a>Met behulp van de werkruimte verzamelingen en werkruimten
**Werkruimte verzamelingen** en **werkruimten** zijn containers voor inhoud die worden gebruikt en georganiseerd in welke manier best past bij de Hallo ontwerp van Hallo-toepassing die u wilt maken. Er zijn veel verschillende manieren dat u inhoud Hallo ervan kan rangschikken. U kunt ervoor kiezen tooput alle inhoud in een werkruimte en vervolgens later gebruik app-tokens toofurther onderverdelen Hallo inhoud onder uw klanten. U kunt ook tooput al uw klanten in afzonderlijke werkruimten zodat er een scheiding tussen deze twee. Of u kunt ervoor kiezen tooorganize gebruikers per regio in plaats van door de klant. Dit flexibele ontwerp kunt u toochoose Hallo aanbevolen manier tooorganize inhoud.

## <a name="cached-datasets"></a>In de cache gegevenssets
In de cache gegevenssets kan worden gebruikt.  Echter, u gegevens in de cache niet vernieuwen zodra deze is geladen in **Microsoft Power BI Embedded**. Een gegevensset in de cache betekent dat u in Power BI Desktop Hallo gegevens hebt geïmporteerd in plaats van DirectQuery.

## <a name="authentication-and-authorization-with-app-tokens"></a>Verificatie en autorisatie met app-tokens
**Microsoft Power BI Embedded** past omleiding tooyour toepassing tooperform alle Hallo nodig gebruikersverificatie en autorisatie. Er is geen expliciete vereiste dat uw eindgebruikers klanten van Azure Active Directory (Azure AD zijn).  Uw toepassing uitgedrukt in plaats daarvan te**Microsoft Power BI Embedded** autorisatie toorender een Power BI-rapport met behulp van **verificatietokens toepassing (App-Tokens)**.  Deze **App-Tokens** zo nodig wanneer uw app wil toorender een rapport worden gemaakt.

![](media/powerbi-embedded-whats-is/app-tokens.png)

**Verificatietokens toepassing (App-Tokens)** zijn gebruikte tooauthenticate tegen **Microsoft Power BI Embedded**.  Er zijn drie soorten **App-Tokens**:

1. Inrichting van Tokens - die worden gebruikt bij het inrichten van een nieuwe **werkruimte** in een **Werkruimteverzameling**
2. Ontwikkeling van Tokens - gebruikt bij het maken rechtstreeks toohello roept **Power BI REST-API's**
3. Een rapport in Hallo ingesloten insluiten Tokens - gebruikt bij het maken van aanroepen toorender iframe

Deze tokens worden gebruikt voor Hallo verschillende fasen van de interacties met **Microsoft Power BI Embedded**.  Hallo tokens zijn zo ontworpen dat u machtigingen in uw app tooPower BI delegeren kunt. Zie voor meer informatie [App Token stromen](power-bi-embedded-app-token-flow.md).

## <a name="create-or-edit-reports-within-your-application"></a>Maken of bewerken van rapporten in uw toepassing

U kunt nu bewerken rapporten bestaan of het maken van nieuwe rapporten rechtstreeks in uw toepassing zonder toouse Power BI Desktop. Dit is vereist dat een gegevensset bestaat in uw werkruimte.

## <a name="see-also"></a>Zie ook

[Algemene scenario's voor Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Aan de slag met Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Aan de slag met het voorbeeld](power-bi-embedded-get-started-sample.md)  
[Een rapport insluiten](power-bi-embedded-embed-report.md)  
[Verifiëren en autoriseren in Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Voorbeeld van ingesloten JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI-CSharp Git-opslagplaats](https://github.com/Microsoft/PowerBI-CSharp)  
[Power BI-knooppunt Git-opslagplaats](https://github.com/Microsoft/PowerBI-Node)  
Nog vragen? [Probeer Hallo Power BI-Community](http://community.powerbi.com/)
