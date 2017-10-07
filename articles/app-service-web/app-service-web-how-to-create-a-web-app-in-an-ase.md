---
title: een web-app in een App Service-omgeving v1 aaaCreate
description: Meer informatie over hoe toocreate web-apps en app-serviceabonnementen in een App Service-omgeving v1
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 983ba055-e9e4-495a-9342-fd3708dcc9ac
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 322ef344517c54247b102fb4920e35645986ef98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a>Een web-app maken in een App Service-omgeving v1

> [!NOTE]
> In dit artikel gaat over het Hallo v1 App Service-omgeving.  Er is een nieuwere versie van App Service-omgeving die eenvoudiger toouse en wordt uitgevoerd op krachtiger infrastructuur Hallo. meer informatie over de nieuwe versie Hallo met Hallo beginnen toolearn [inleiding toohello App Service-omgeving](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Overzicht
Deze zelfstudie laat zien hoe toocreate web-apps en App Service-plannen een [App Service-omgeving v1](app-service-app-service-environment-intro.md) (as-omgeving). 

> [!NOTE]
> Als u wilt dat toolearn hoe toocreate een web-app, maar toodo hoeft niet in een App Service-omgeving, Zie [een .NET-web-app maken](app-service-web-get-started-dotnet.md) of een Hallo-zelfstudies voor andere talen en frameworks gerelateerd.
> 
> 

## <a name="prerequisites"></a>Vereisten
Deze zelfstudie wordt ervan uitgegaan dat u een App Service-omgeving hebt gemaakt. Als u die nog niet hebt gedaan, Zie [maken van een App-serviceomgeving](app-service-web-how-to-create-an-app-service-environment.md). 

## <a name="create-a-web-app"></a>Een webtoepassing maken
1. In Hallo [Azure Portal](https://portal.azure.com/), klikt u op **Nieuw > Web + mobiel > Web-App**. 
   
    ![][1]
2. Selecteer uw abonnement.  
   
    Als u meerdere abonnementen hebt, worden op de hoogte dat toocreate een app in uw App Service-omgeving, moet u toouse Hallo hetzelfde abonnement die u hebt gebruikt bij het maken van Hallo-omgeving. 
3. Selecteer of maak een resourcegroep.
   
    *Resourcegroepen* inschakelen toomanage u Azure-resources als een eenheid gerelateerd en zijn handig bij het maken van *toegangsbeheer op basis van rollen* regels (RBAC) voor uw apps. Zie voor meer informatie [overzicht van Azure Resource Manager][ResourceGroups]. 
4. Selecteer of maak een App Service-abonnement.
   
    *App Service-plannen* beheerde sets met web-apps.  Wanneer u prijzen selecteert, is Hallo prijs normaal toegepaste toohello App Service-plan in plaats van afzonderlijke apps toohello. In een as-omgeving u voor Hallo compute betaalt toegewezen exemplaren toohello as-omgeving in plaats van de lijst met uw ASP.  tooscale up Hallo aantal exemplaren van een web-app u opschalen Hallo instanties van uw App Service-abonnement en dit van invloed op alle Hallo web-apps in het plan.  Sommige functies zoals site sleuven of VNET integratie hebben ook hoeveelheidsbeperkingen binnen Hallo plan.  Zie voor meer informatie [overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)
   
    Hallo-App Service-plannen kunt in uw as-omgeving u identificeren door te kijken Hallo locatie die wordt vermeld onder de naam van de Hallo-plan.  
   
    ![][5]
   
    Als u wilt dat toouse een App Service-abonnement dat al bestaat in uw App Service-omgeving, selecteert u plan. Als u een nieuw App Service-plan toocreate wilt, Zie Hallo gedeelte van deze zelfstudie te volgen [maken van een App Service-abonnement in een App-serviceomgeving](#createplan).
5. Hallo-naam voor uw web-app en klik vervolgens op **maken**. 
   
    Als uw as-omgeving gebruikmaakt van een externe VIP Hallo-URL van een app in een as-omgeving is: [*sitename*]. [ *naam van uw App Service-omgeving*]. p.azurewebsites.net in plaats van [*sitename*]. azurewebsites.net
   
    Als uw as-omgeving gebruikmaakt van een interne VIP vervolgens Hallo-URL van een app in dat as-omgeving is: [*sitename*]. [ *subdomein opgegeven tijdens het maken van de as-omgeving*]   
    Nadat u uw ASP tijdens het maken van de as-omgeving selecteren, ziet u Hallo subdomein bijwerken hieronder **naam**

## <a name="createplan"></a>Een App Service-abonnement maken
Wanneer u een App Service-abonnement in een App Service-omgeving maakt, zijn uw keuzes worker verschillend omdat er geen gedeelde werknemers zich in een as-omgeving.  Hallo-medewerkers hebt u toouse zijn Hallo waarden die zijn toegewezen toohello as-omgeving door Hallo beheerder.  Dit betekent dat toocreate een nieuw plan, moet u toohave meer werknemers toegewezen tooyour as-omgeving-werknemersgroep dan Hallo kunt u het totale aantal exemplaren voor alle uw plannen al uit de betreffende worker-groep.  Als u geen voldoende werknemers in uw as-omgeving worker-groep toocreate uw plan, moet u toowork met uw as-omgeving admin tooget die ze toegevoegd.

Een ander verschil met App Service-abonnementen die worden gehost door een App-serviceomgeving is Hallo gebrek aan selectie prijzen.  Wanneer u een App Service-omgeving hebt u betaalt voor de rekenresources die door Hallo systeem gebruikt en bevatten geen extra kosten voor Hallo plannen in deze omgeving.  Normaal gesproken wanneer u een App Service-abonnement maakt u een prijscategorie selecteren waarmee wordt bepaald van de facturering.  Een App Service-omgeving is in wezen een persoonlijke locatie waarin u inhoud kunt maken.  U betaalt voor Hallo-omgeving en niet toohost uw inhoud.

Hallo volgende instructies wordt aangegeven hoe toocreate een App Service plan tijdens het maken van een web-app, zoals wordt beschreven in de vorige sectie Hallo Hallo zelfstudie.

1. Klik op **nieuw** in Hallo plan selectie gebruikersinterface en geef een naam voor uw abonnement net zoals u dat gewend buiten een as-omgeving bent.
2. Selecteer Hallo as gewenste toouse van uw objectkiezer locatie-omgeving.
   
    Omdat een App Service-omgeving in wezen een locatie van de persoonlijke implementatie is, ziet u onder locatie. 
   
    ![][2]
   
    Hallo-App Service-abonnement maken UI updates na selectie van een as-omgeving in Hallo locatie kiezen.  Hallo locatie toont nu Hallo-naam van Hallo as-omgeving system en Hallo regio is in en prijzen plan objectkiezer Hallo is vervangen door een objectkiezer worker-groep.  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a>Een werknemersgroep selecteren
Normaal gesproken zijn in Azure App Service en buiten een App Service-omgeving, er 3 compute-grootten die beschikbaar met de Hallo selectie van een speciale prijs-plan zijn.  Op soortgelijke wijze voor een as-omgeving definiëren up too3 pools van werknemers en geef Hallo compute grootte die wordt gebruikt voor die worker-groep.  Wat dit betekent dat voor tenants Hallo as-omgeving is dat in plaats van een prijsstelling met compute-grootte voor uw App Service-abonnement selecteren, u wat heet een *werknemersgroep*.  

Hallo worker-groep selectie gebruikersinterface geeft Hallo compute omvang is gebruikt voor die werknemersgroep onder de naam van de Hallo.  Hallo beschikbare hoeveelheid verwijst toohow veel compute exemplaren zijn beschikbaar voor gebruik in die groep.  de totale groep Hallo kan daadwerkelijk meer exemplaren dan het aantal, maar deze waarde verwijst toosimply hoeveel zich niet in gebruik.  Als u tooadjust moet de uw App Service-omgeving tooadd meer compute resources Zie [configureren van uw App Service-omgeving](app-service-web-configure-an-app-service-environment.md).

![][4]

In dit voorbeeld ziet u slechts twee werknemersgroepen die beschikbaar is. Dat komt doordat Hallo as-omgeving administrator toegewezen alleen hosts in deze twee werknemersgroepen.  Hallo zou derde weergegeven wanneer er virtuele machines die zijn toegewezen in de App.  

## <a name="after-web-app-creation"></a>Na het maken van web-app
Er zijn enkele overwegingen voor het uitvoeren van de web-apps en het beheren van App Service-abonnementen in een as-omgeving die in aanmerking genomen toobe nodig.  

Zoals eerder opgemerkt, Hallo eigenaar van Hallo as-omgeving is verantwoordelijk voor het Hallo-grootte van het Hallo-systeem en als gevolg hiervan ze zijn ook verantwoordelijk voor het App Service-abonnementen om te garanderen dat er voldoende capaciteit toohost Hallo gewenst. Als er geen beschikbare werknemers, wordt u niet kunt toocreate worden uw App Service-abonnement.  Dit is ook true tooscaling van uw web-app.  Als u meer exemplaren nodig hebt u zou tooget uw App Service-omgeving admin tooadd meer werknemers.

Na het maken van uw web-app en App Service-abonnement is een goed idee tooscale het.  In een as-omgeving moet u altijd toohave ten minste 2 exemplaren van uw App Service plan tooprovide-fouttolerantie voor uw apps.  Schalen van een App Service is plan in een as-omgeving dezelfde als normale via App Service-abonnement UI Hallo Hallo.  Voor meer informatie over het schalen [hoe tooscale een web-app in een App-serviceomgeving](app-service-web-scale-a-web-app-in-an-app-service-environment.md)

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment
[ResourceGroups]: ../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
