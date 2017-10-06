---
title: aaaHow tooCreate een App Service-omgeving v1
description: Beschrijving van de stroom maken voor een app service-omgeving v1
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a>Hoe tooCreate een App Service-omgeving v1 

> [!NOTE]
> In dit artikel gaat over het Hallo v1 App Service-omgeving. Er is een nieuwere versie van App Service-omgeving die eenvoudiger toouse en wordt uitgevoerd op krachtiger infrastructuur Hallo. meer informatie over de nieuwe versie Hallo met Hallo beginnen toolearn [inleiding toohello App Service-omgeving](../app-service/app-service-environment/intro.md).
> 

### <a name="overview"></a>Overzicht
Hallo as-omgeving (App Service omgeving) is de optie voor een Premium-service van Azure App Service, die zorgt voor een verbeterde functie die is niet beschikbaar in Hallo multitenant stempels. Hallo as-omgeving functie implementeert in wezen hello Azure App Service in virtueel netwerk van een klant. toogain een beter inzicht in Hallo mogelijkheden die worden aangeboden door App Service-omgevingen lezen Hallo [wat is er een App-serviceomgeving] [ WhatisASE] documentatie.

### <a name="before-you-create-your-ase"></a>Voordat u uw as-omgeving maken
Het is belangrijk toobe op de hoogte van Hallo dingen die u niet wijzigen. Deze aspecten die u over uw as-omgeving niet wijzigen nadat deze is gemaakt, zijn:

* Locatie
* Abonnement
* Resourcegroep
* VNet gebruikt
* Subnet dat wordt gebruikt 
* De subnetgrootte van het

Wanneer een VNet verzamelen en een subnet, op te geven kunt controleren of deze is groot genoeg tooaccomodate een eventuele toekomstige groei. 

### <a name="creating-an-app-service-environment-v1"></a>Maken van een App Service-omgeving v1
toocreate een App Service-omgeving v1 moet u toosearch hello Azure Marketplace voor ***App Service-omgeving v1***, of door te gaan via nieuw -> Web en mobiel -> App Service-omgeving. een ASEv1 toocreate:

1. Geef de naam op Hallo van uw as-omgeving. Hallo-naam die is opgegeven voor Hallo as-omgeving wordt gebruikt voor het Hallo-apps die zijn gemaakt in Hallo as-omgeving. Hallo subdomeinnaam zou zijn als de naam van de as-omgeving Hallo appsvcenvdemo. *appsvcenvdemo.p.azurewebsites.net*. Als u een app met de naam dus gemaakt *mytestapp* en vervolgens het normaal zou op adresseerbare zijn *mytestapp.appsvcenvdemo.p.azurewebsites.net*. U kunt witruimte niet gebruiken in Hallo-naam van uw as-omgeving. Als u hoofdletters in de naam van de Hallo gebruikt, worden de domeinnaam Hallo Hallo totale kleine versie met die naam. Als u een ILB gebruikt vervolgens de naam van uw as-omgeving wordt niet gebruikt in een subdomein maar in plaats daarvan expliciet is opgegeven tijdens het maken van de as-omgeving
   
    ![][1]
2. Selecteer uw abonnement. Hallo abonnement dat u gebruikt voor uw as-omgeving is ook Hallo een die alle apps in die as-omgeving met worden gemaakt. U kunt uw as-omgeving in een VNet dat in een ander abonnement plaatsen
3. Selecteer of geef een nieuwe resourcegroep. Hallo resourcegroep gebruikt voor uw as-omgeving moet dezelfde dat wordt gebruikt voor uw VNet Hallo. Als u een bestaande VNet selecteert en Hallo resourcegroep selecteren voor uw as-omgeving bijgewerkte tooreflect worden die uw VNet.
   
    ![][2]
4. Controleer uw selecties virtueel netwerk en de locatie. U kunt kiezen toocreate een nieuw VNet of Selecteer een bestaande VNet. Als u een nieuw VNet daarna kunt u een naam en locatie opgeven. Hallo nieuwe VNet hebben Hallo adresbereik 192.168.250.0/23 en een subnet met de naam **standaard** die is gedefinieerd als 192.168.250.0/24. U kunt ook gewoon een reeds bestaande klassiek of Resource Manager VNet selecteren. Hallo VIP selectie bepaalt als uw as-omgeving rechtstreeks toegankelijk zijn vanuit Hallo internet (extern) of als er een interne Load Balancer (ILB) gebruikt. meer informatie hierover lezen toolearn [met behulp van een interne Load Balancer met een App-serviceomgeving][ILBASE]. Als u een VIP-type van externe selecteert kunt vervolgens u hoeveel extern IP-adressen Hallo-systeem is gemaakt met voor IPSSL doeleinden. Als u interne selecteren moet u toospecify Hallo subdomein die door uw as-omgeving wordt gebruikt. ASEs kan worden geïmplementeerd in virtuele netwerken die gebruikmaken van *beide* openbare-adresbereiken, *of* RFC1918 adresruimten (dat wil zeggen particuliere adressen). In de volgorde toouse een virtueel netwerk met een openbare-adresbereik moet u toocreate hello VNet tevoren. Wanneer u een bestaande VNet selecteert moet u een nieuw subnet toocreate tijdens het maken van de as-omgeving. **U kunt een vooraf gemaakte subnet niet gebruiken in Hallo-portal. Als u uw as-omgeving met een resource manager-sjabloon maakt, kunt u een as-omgeving met een bestaande subnet.** toocreate een as-omgeving van een sjabloon Hallo informatie hier gebruiken [maken van een App-serviceomgeving uit sjabloon] [ ILBAseTemplate] en hier [een ILB-App Service-omgeving te maken van sjabloon] [ASEfromTemplate].

### <a name="details"></a>Details
Een as-omgeving wordt gemaakt met 2-Front-Ends en twee 2 werkers beschikken. Hallo-Front-Ends fungeren als Hallo HTTP/HTTPS-eindpunten en verkeer verzenden toohello werknemers die Hallo-functies die als host fungeren van uw apps. U kunt Hallo hoeveelheid na het maken van de as-omgeving aanpassen en zelfs instellen regels voor automatisch schalen op deze resourcegroepen. Ga voor meer informatie over het handmatig schalen beheren en controleren van een App Service-omgeving naar: [hoe tooconfigure een App-serviceomgeving][ASEConfig] 

Alleen Hallo een as-omgeving kan bestaan in Hallo subnet dat wordt gebruikt door Hallo as-omgeving. Hallo-subnet kan niet worden gebruikt voor iets anders dan Hallo as-omgeving

### <a name="after-app-service-environment-v1-creation"></a>Na het maken van App Service-omgeving v1
U kunt na het maken van de as-omgeving aanpassen:

* Aantal van de Front-Ends (minimum: 2)
* Aantal werknemers (minimum: 2)
* Het aantal IP-adressen beschikbaar voor IP-SSL
* COMPUTE resource tekengrootten in Hallo-Front-Ends of werknemers (front-end minimumgrootte is P2)

Er zijn meer details omtrent handmatige schaal, management en hier bewaking van App Service-omgevingen: [hoe tooconfigure een App-serviceomgeving][ASEConfig] 

Voor informatie over automatisch schalen is er een handleiding hier: [hoe tooconfigure automatisch schalen voor een App-serviceomgeving][ASEAutoscale]

Er zijn extra afhankelijkheden die niet beschikbaar voor aanpassing zoals Hallo-database en opslag. Deze zijn verwerkt door Azure en worden geleverd met Hallo-systeem. Hallo system opslag ondersteunt up too500 GB voor de hele App Service-omgeving Hallo en Hallo-database wordt aangepast door Azure indien nodig door Hallo schaal van Hallo-systeem.

## <a name="getting-started"></a>Aan de slag
Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).

tooget de slag met App Service-omgeving v1, Zie [inleiding toohello App Service-omgeving v1][WhatisASE]

Zie voor meer informatie over hello Azure App Service-platform, [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
