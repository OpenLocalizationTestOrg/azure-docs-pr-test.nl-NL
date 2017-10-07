---
title: aaaCreate een externe Azure App Service-omgeving
description: Legt uit hoe toocreate een App Service-omgeving, terwijl u een app of een zelfstandige maken
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 94dd0222-b960-469c-85da-7fcb98654241
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: f8619534ddd889ea65063733ac6ec11b206e799c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-external-app-service-environment"></a>Een externe App Service-omgeving maken #

Azure App Service-omgeving is een implementatie van Azure App Service in een subnet in een Azure-netwerk (VNet). Er zijn twee manieren toodeploy een App Service-omgeving (as-omgeving):

- Een VIP-adres op een externe IP-adres, vaak aangeduid als een externe as-omgeving.
- Met de Hallo VIP op een interne IP-adres, vaak genoemd, een ILB-as-omgeving omdat Hallo interne eindpunt, een interne load balancer (ILB is).

Dit artikel ziet u hoe toocreate een externe as-omgeving. Zie voor een overzicht van Hallo as-omgeving [een inleiding toohello App Service-omgeving][Intro]. Voor informatie over hoe toocreate een ILB as-omgeving, Zie [maken en gebruiken een ILB-as-omgeving][MakeILBASE].

## <a name="before-you-create-your-ase"></a>Voordat u uw as-omgeving maken ##

Nadat u uw as-omgeving hebt gemaakt, kunt u de volgende Hallo niet wijzigen:

- Locatie
- Abonnement
- Resourcegroep
- VNet gebruikt
- Subnet dat wordt gebruikt
- De subnetgrootte van het

> [!NOTE]
> Als u een VNet kiest en geef een subnet, zorg ervoor dat deze groot genoeg tooaccommodate toekomstige groei. Een grootte van het is raadzaam `/25` met 128 adressen.
>

## <a name="three-ways-toocreate-an-ase"></a>Drie manieren toocreate een as-omgeving ##

Er zijn drie manieren toocreate een as-omgeving:

- **Tijdens het maken van een App Service-plan**. Deze methode maakt Hallo as-omgeving en Hallo App Service-abonnement in één stap.
- **Als een zelfstandige actie**. Deze methode maakt u een zelfstandige as-omgeving, die een as-omgeving helemaal leeg is. Deze methode is een meer geavanceerde proces toocreate een as-omgeving. U gebruikt deze toocreate een as-omgeving met een ILB.
- **Van een Azure Resource Manager-sjabloon**. Deze methode is bedoeld voor ervaren gebruikers. Zie voor meer informatie [een as-omgeving te maken van een sjabloon][MakeASEfromTemplate].

Een externe as-omgeving heeft een openbare VIP, wat betekent dat alle HTTP/HTTPS-verkeer toohello apps in Hallo as-omgeving komt binnen via internet toegankelijke IP-adres. Een as met een ILB-omgeving heeft een IP-adres uit Hallo subnet dat wordt gebruikt door Hallo as-omgeving. Hallo apps die worden gehost in een ILB-as-omgeving zijn niet beschikbaar gesteld rechtstreeks toohello internet.

## <a name="create-an-ase-and-an-app-service-plan-together"></a>Samen een as-omgeving en een App Service-abonnement maken ##

Hallo App Service-abonnement is een container van apps. Wanneer u een app in App Service maakt, kunt u kiezen of maken van een App Service-abonnement. Hallo container model omgevingen Houd App Service-abonnementen en App Service-abonnementen Houd apps.

een as-omgeving bij het maken van een App Service-plan toocreate:

1. In Hallo [Azure-portal](https://portal.azure.com/), selecteer **nieuw** > **Web en mobiel** > **Web-App**.

    ![Web-Apps maken][1]

2. Selecteer uw abonnement. Hallo-app en Hallo as-omgeving worden gemaakt in Hallo dezelfde abonnementen.

3. Selecteer of maak een resourcegroep. Met resourcegroepen kunt u Azure gerelateerde resources beheren als één eenheid. Resourcegroepen zijn ook nuttig wanneer u regels voor toegangsbeheer op basis van rollen tot stand voor uw apps brengen. Zie voor meer informatie, Hallo [overzicht van Azure Resource Manager][ARMOverview].

4. Selecteer Hallo App Service-abonnement en selecteer vervolgens **nieuw**.

    ![Nieuwe App Service-abonnement][2]

5. In Hallo **locatie** vervolgkeuzelijst, selecteer Hallo-regio waar u toocreate Hallo as-omgeving. Als u een bestaande as-omgeving selecteert, wordt een nieuwe as-omgeving is niet gemaakt. Hallo App Service-abonnement wordt gemaakt in Hallo as-omgeving die u hebt geselecteerd. 

6. Selecteer **prijscategorie**, en kies een van de Hallo **geïsoleerd** prijzen SKU's. Als u ervoor kiest een **geïsoleerd** SKU-kaart en een locatie die niet een as-omgeving, een nieuwe as-omgeving wordt gemaakt op die locatie. toostart hello proces toocreate een as-omgeving, selecteer **Selecteer**. Hallo **geïsoleerd** SKU is alleen beschikbaar in combinatie met een as-omgeving. U ook niet gebruiken andere prijscategorie SKU in een as-omgeving anders dan **geïsoleerd**.

    ![Het selecteren van een prijscategorie][3]

7. Geef de naam Hallo voor uw as-omgeving. Deze naam wordt gebruikt in de adresseerbare naam Hallo voor uw apps. Als de naam Hallo Hallo as-omgeving _appsvcenvdemo_, Hallo domeinnaam is *. appsvcenvdemo.p.azurewebsites.net*. Als u een app met de naam maakt *mytestapp*, adresseerbare op mytestapp.appsvcenvdemo.p.azurewebsites.net is. U kunt witruimte niet gebruiken in Hallo naam. Als u hoofdletters gebruikt, is domeinnaam Hallo Hallo totale kleine versie met die naam.

    ![Naam van een nieuwe App Service-abonnement][4]

8. Geef de details van Azure virtuele netwerken. Selecteer een **maken van nieuwe** of **Selecteer een bestaande**. Hallo optie tooselect bestaand VNet is alleen beschikbaar als u een VNet in de geselecteerde regio Hallo hebben. Als u selecteert **nieuw**, voer een naam voor Hallo VNet. Een nieuwe Resource Manager VNet met deze naam wordt gemaakt. Hallo-adresruimte wordt `192.168.250.0/23` in Hallo geselecteerde regio. Als u selecteert **bestaande selecteren**, moet u:

    a. Selecteer Hallo VNet-Adresblok, hebt u meer dan één.

    b. Voer de subnetnaam van een nieuwe.

    c. Selecteer Hallo grootte van Hallo subnet. *Houd er rekening mee tooselect een groot genoeg tooaccommodate grootte toekomstige groei van uw as-omgeving.* Het is raadzaam `/25`, waardoor 128 adressen heeft en een maximale grootte as-omgeving kan verwerken. Wordt niet aanbevolen `/28`, bijvoorbeeld omdat alleen 16 adressen beschikbaar zijn. Infrastructuur ten minste vijf adressen worden gebruikt. In een `/28` subnet, bent u links met een maximale schaling van 11 exemplaren.

    d. Selecteer Hallo subnet IP-bereik.

9. Selecteer **maken** toocreate Hallo as-omgeving. Dit proces maakt ook Hallo App Service-abonnement en Hallo-app. Hallo as-omgeving, de App Service-abonnement en de app zijn allemaal onder Hallo hetzelfde abonnement en Hallo ook in dezelfde resourcegroep. Als uw as-omgeving een afzonderlijke resourcegroep moet of als u een ILB-as-omgeving moet, voert u Hallo stappen toocreate een as-omgeving op zichzelf.

## <a name="create-an-ase-by-itself"></a>Zelf een as-omgeving maken ##

Als u een zelfstandige as-omgeving maakt, heeft niets in deze. Maandelijkse kosten met zich mee voor Hallo infrastructuur nog steeds leidt ertoe dat een leeg as-omgeving. Volg deze stappen toocreate een as-omgeving met een ILB of toocreate een as-omgeving in een eigen resourcegroep bevinden. Nadat u uw as-omgeving hebt gemaakt, kunt u apps in deze met behulp van de normale proces Hallo. Selecteer uw nieuwe as-omgeving als Hallo locatie.

1. Zoeken hello Azure Marketplace voor **App Service-omgeving**, of selecteer **nieuw** > **Web Mobile** > **App Service Omgeving**. 

2. Voer Hallo-naam van uw as-omgeving. Deze naam wordt gebruikt voor het Hallo-apps die zijn gemaakt in Hallo as-omgeving. Als de naam van de Hallo *mynewdemoase*, Hallo subdomeinnaam *. mynewdemoase.p.azurewebsites.net*. Als u een app met de naam maakt *mytestapp*, adresseerbare op mytestapp.mynewdemoase.p.azurewebsites.net is. U kunt witruimte niet gebruiken in Hallo naam. Als u hoofdletters gebruikt, is domeinnaam Hallo Hallo totale kleine versie van Hallo-naam. Als u een ILB, wordt de naam van uw as-omgeving wordt niet gebruikt in een subdomein maar in plaats daarvan expliciet is opgegeven tijdens het maken van de as-omgeving.

    ![Naamgeving van de as-omgeving][5]

3. Selecteer uw abonnement. Dit abonnement is ook Hallo waarmee alle apps in Hallo as-omgeving. U kunt geen uw as-omgeving plaatsen in een VNet dat in een ander abonnement.

4. Selecteer of geef een nieuwe resourcegroep. Hallo resourcegroep gebruikt voor uw as-omgeving moet dezelfde versie die wordt gebruikt voor uw VNet Hallo. Als u een bestaande VNet selecteert, Hallo resourcegroep selecteren voor uw as-omgeving is bijgewerkte tooreflect die uw VNet. *U kunt een as-omgeving maken met een resourcegroep die verschilt van de resourcegroep voor Hallo VNet als u een Resource Manager-sjabloon gebruikt.* toocreate een as-omgeving van een sjabloon, Zie [maken van een App Service-omgeving van een sjabloon][MakeASEfromTemplate].

    ![Resourcegroep selecteren][6]

5. Selecteer uw VNet en locatie. U kunt een nieuw VNet maken of een bestaande VNet selecteren: 

    * Als u een nieuw VNet selecteert, kunt u een naam en locatie opgeven. Hallo heeft nieuwe VNet Hallo adresbereik 192.168.250.0/23 en een subnet met de naam default. Hallo-subnet wordt gedefinieerd als 192.168.250.0/24. U kunt alleen een Resource Manager VNet selecteren. Hallo **VIP Type** selectie bepaalt als uw as-omgeving rechtstreeks toegankelijk zijn vanuit Hallo internet (extern) of als een ILB wordt gebruikt. Zie toolearn meer informatie over deze opties [maken en gebruiken van een interne load balancer met een App Service-omgeving][MakeILBASE]. 

      * Als u selecteert **externe** voor Hallo **VIP Type**, kunt u hoeveel extern IP-adressen Hallo-systeem is gemaakt met voor SSL op basis van IP-doeleinden. 
    
      * Als u selecteert **intern** voor Hallo **VIP Type**, moet u Hallo-domein dat gebruikmaakt van uw as-omgeving. U kunt een as-omgeving implementeren in een VNet die gebruikmaakt van openbare of particuliere adresbereiken. een VNet met een openbare-adresbereik toouse, moet u toocreate hello VNet tevoren. 
    
    * Als u een bestaande VNet selecteert, wordt een nieuw subnet wordt gemaakt wanneer Hallo as-omgeving wordt gemaakt. *U kunt een vooraf gemaakte subnet niet gebruiken in Hallo-portal. Als u een Resource Manager-sjabloon gebruikt, kunt u een as-omgeving met een bestaande subnet.* toocreate een as-omgeving van een sjabloon, Zie [maken van een App Service-omgeving van een sjabloon][MakeASEfromTemplate].

## <a name="app-service-environment-v1"></a>App Service-omgeving v1 ##

U kunt nog steeds exemplaren van de eerste versie Hallo van App Service-omgeving (ASEv1) maken. toostart die verwerken, zoeken Hallo Marketplace voor **App Service-omgeving v1**. U Hallo as-omgeving maken in Hallo dezelfde manier waarop u Hallo zelfstandige as-omgeving. Wanneer dit voltooid, wordt uw ASEv1 heeft twee front-ends en twee werknemers. Met ASEv1, moet u Hallo-front-ends en werknemers beheren. Ze zijn niet automatisch toegevoegd wanneer u uw App Service-abonnementen maakt. Hallo-front-ends fungeren als Hallo HTTP/HTTPS-eindpunten en verkeer toohello werknemers verzenden. Hallo werknemers zijn Hallo-functies die voor het hosten van uw apps. Nadat u uw as-omgeving hebt gemaakt, kunt u Hallo hoeveelheid front-ends en werknemers aanpassen. 

toolearn meer informatie over ASEv1, Zie [inleiding toohello App Service-omgeving v1][ASEv1Intro]. Zie voor meer informatie over het schalen, beheren en controleren van ASEv1, [hoe tooconfigure een App-serviceomgeving][ConfigureASEv1].

<!--Image references-->
[1]: ./media/how_to_create_an_external_app_service_environment/createexternalase-create.png
[2]: ./media/how_to_create_an_external_app_service_environment/createexternalase-aspcreate.png
[3]: ./media/how_to_create_an_external_app_service_environment/createexternalase-pricing.png
[4]: ./media/how_to_create_an_external_app_service_environment/createexternalase-embeddedcreate.png
[5]: ./media/how_to_create_an_external_app_service_environment/createexternalase-standalonecreate.png
[6]: ./media/how_to_create_an_external_app_service_environment/createexternalase-network.png



<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
