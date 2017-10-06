---
title: aaaUse een Azure App Service-omgeving
description: Hoe toocreate, publiceren en schalen van apps in een Azure App Service-omgeving
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 30c89e384efc07c560254856c0ca7d4eb4b1f010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-app-service-environment"></a>Gebruik van een App Service-omgeving #

## <a name="overview"></a>Overzicht ##

Azure App Service-omgeving is een implementatie van Azure App Service in een subnet in virtuele Azure-netwerk van een klant. Deze bestaat uit:

- **FrontPage-ends**: Hallo-front-ends zijn waar HTTP/HTTPS wordt beëindigd in een App Service-omgeving (as-omgeving).
- **Werknemers**: Hallo werknemers zijn Hallo resources die uw apps te hosten.
- **Database**: Hallo-database bevat informatie die Hallo-omgeving bepaalt.
- **Opslag**: Hallo opslag is gebruikte toohost Hallo klant gepubliceerde apps.

> [!NOTE]
> Er zijn twee versies van App Service-omgeving: ASEv1 en ASEv2. U moet in ASEv1, Hallo resources beheren voordat u ze kunt gebruiken. toolearn hoe tooconfigure en ASEv1 beheren, Zie [configureren van een App Service-omgeving v1][ConfigureASEv1]. Hallo rest van dit artikel is gericht op ASEv2.
>
>

U kunt een as-omgeving (ASEv1 en ASEv2) implementeren met een externe of interne VIP voor toegang tot Apps. Hallo-implementatie met een externe VIP wordt gewoonlijk aangeduid met een externe as-omgeving. Hallo interne versie heet Hallo ILB as-omgeving omdat deze gebruikmaakt van een interne load balancer (ILB). toolearn meer informatie over Hallo ILB as-omgeving, Zie [maken en gebruiken een ILB-as-omgeving][MakeILBASE].

## <a name="create-a-web-app-in-an-ase"></a>Een web-app maken in een as-omgeving ##

toocreate een web-app in een as-omgeving, u dezelfde verwerken hello gebruiken als wanneer u dit hebt gemaakt normaal, maar met een paar kleine verschillen. Wanneer u een nieuwe App Service-abonnement maken:

- In plaats van een geografische locatie kiezen in welke toodeploy uw app, kiest u een as-omgeving als uw locatie.
- Alle App Service-abonnementen gemaakt in een as-omgeving moeten zich in een geïsoleerd prijscategorie.

Als u een as-omgeving hebt, kunt u door de instructies te volgen Hallo in [maken van een App Service-omgeving][MakeExternalASE].

toocreate een web-app in een as-omgeving:

1. Selecteer **nieuwe** > **Web en mobiel** > **Web-App**.

2. Voer een naam voor Hallo web-app. Als u al een App Service-abonnement in een as-omgeving hebt geselecteerd, geeft Hallo-domeinnaam voor Hallo app domeinnaam Hallo Hallo as-omgeving.

    ![Web-app-naam selecteren][1]

3. Selecteer een abonnement.

4. Geef een naam voor een nieuwe resourcegroep of selecteer **gebruik bestaande** en selecteer een optie uit de vervolgkeuzelijst Hallo.

5. Selecteer een bestaand App Service-abonnement in uw as-omgeving of een nieuwe maken met de volgende stappen:

    a. Selecteer **maken van nieuwe**.

    b. Geef de naam Hallo voor uw App Service-abonnement.

    c. Selecteer uw as-omgeving in Hallo **locatie** vervolgkeuzelijst.

    d. Selecteer een **geïsoleerd** prijscategorie. Selecteer **Selecteer**.

    e. Selecteer **OK**.
    
    ![Geïsoleerde Prijscategorieën][2]

6. Selecteer **Maken**.

## <a name="how-scale-works"></a>Hoe werkt schalen ##

Elke App Service-app wordt uitgevoerd in een App Service-plan. Hallo container model is omgevingen Houd App Service-abonnementen en App Service-abonnementen Houd apps. Wanneer u een app schalen, u schalen Hallo App Service-abonnement en dus alle Hallo apps schalen in Hallo hetzelfde abonnement.

In ASEv2, wanneer u een App Service-abonnement schalen wordt Hallo nodig infrastructuur automatisch toegevoegd. Er is een vertraging tooscale operations tijdens het Hallo-infrastructuur is toegevoegd. Hallo nodig infrastructuur moet ASEv1, worden toegevoegd voordat u kunt maken of uitbreiden van uw App Service-abonnement. 

In Hallo multitenant-App Service, schalen is meestal onmiddellijke omdat een groep die direct beschikbaar toosupport deze. Er is geen dergelijke buffer in een as-omgeving, en bronnen worden toegewezen na nodig.

U kunt too100 exemplaren opschalen in een as-omgeving. De instanties van 100 kunnen alles in één enkele App Service-abonnement of verdeeld over meerdere App Service-abonnementen.

## <a name="ip-addresses"></a>IP-adressen ##

App Service biedt Hallo mogelijkheid tooallocate een toegewezen IP-adres tooan app. Deze mogelijkheid is beschikbaar nadat u een SSL op IP-basis geconfigureerd zoals beschreven in [binden van een bestaande aangepaste SSL-certificaat tooAzure web-apps][ConfigureSSL]. In een as-omgeving is er echter een opmerkelijke uitzondering. U kunt geen extra IP toevoegen adressen toobe gebruikt voor een op IP gebaseerd SSL in een ILB-as-omgeving.

ASEv1 moet u tooallocate Hallo IP-adressen als resources voordat u ze kunt gebruiken. In ASEv2 gebruikt u deze van uw app net als in Hallo multitenant-App Service. Er is altijd één spare adres in ASEv2 too30 IP-adressen. Telkens wanneer is u een gebruikt, een andere toegevoegd, zodat een adres altijd direct beschikbaar voor gebruik is. Een vertraging is tijd die nodig tooallocate een ander IP-adres, waardoor het toevoegen van IP-adressen in snel achter elkaar.

## <a name="front-end-scaling"></a>Front-schaling ##

In ASEv2, wanneer u uw App Service-abonnementen worden uitgebreid werknemers automatisch toegevoegd toosupport ze. Elke as-omgeving met twee front-ends gemaakt. Bovendien schalen Hallo-front-ends automatisch uit met een snelheid van één front-end voor elke 15 exemplaren in uw App Service-abonnementen. Bijvoorbeeld, als u 15 exemplaren hebt, hebt u drie front-ends. Als u exemplaren too30 schalen, hebt u vier FrontPage-ends, enzovoort.

Dit aantal front-ends moet hetgeen ruim voldoende is voor de meeste scenario's. Echter, kunt u uitschalen sneller. U kunt Hallo verhouding tooas laag als een front-end voor elke vijf exemplaren wijzigen. Er is een kosten voor het wijzigen van Hallo verhouding. Zie voor meer informatie [prijzen voor Azure App Service][Pricing].

Front-resources zijn Hallo HTTP/HTTPS-eindpunt voor Hallo as-omgeving. Geheugengebruik per front-end is met de front-standaardconfiguratie hello, consistent ongeveer 60 procent. Klant-werkbelastingen uitvoeren niet op een front-end. Hallo is belangrijke factor voor een front-end met opzicht tooscale Hallo CPU, dit is vooral als gevolg van HTTPS-verkeer.

## <a name="app-access"></a>App-toegang ##

In een externe as-omgeving verschilt Hallo-domein dat wordt gebruikt bij het maken van apps van Hallo multitenant-App Service. Het bevat Hallo-naam van Hallo as-omgeving. Voor meer informatie over het toocreate een externe as-omgeving, Zie [maken van een App Service-omgeving][MakeExternalASE]. Hallo-domeinnaam in een externe as-omgeving ziet eruit als *.&lt; asename&gt;. p.azurewebsites.net*. Bijvoorbeeld, als de naam van uw as-omgeving _externe-as-omgeving_ en hosten van een app aangeroepen _contoso_ in die as-omgeving, u bereikt dit op Hallo volgende URL's:

- Contoso.external ase.p.azurewebsites.net
- Contoso.SCM.external ase.p.azurewebsites.net

Hallo URL contoso.scm.external-ase.p.azurewebsites.net is gebruikte tooaccess hello Kudu-console of voor de publicatie van uw app met behulp van web implementeren. Zie voor informatie over Hallo Kudu-console, [Kudu-console voor Azure App Service][Kudu]. Hallo Kudu-console biedt u een webgebruikersinterface voor foutopsporing, het uploaden van bestanden, bestanden en nog veel meer bewerken.

In een ILB as-omgeving bepaalt u Hallo domein tijdens de implementatie. Voor meer informatie over hoe toocreate een ILB as-omgeving, Zie [maken en gebruiken een ILB-as-omgeving][MakeILBASE]. Als u de domeinnaam Hallo opgeven _ilb ase.info_, Hallo apps in die as-omgeving dat domein gebruiken tijdens het maken van de app. Voor het Hallo-app met de naam _contoso_, Hallo-URL's zijn:

- Contoso.ILB ase.info
- Contoso.SCM.ILB ase.info

## <a name="publishing"></a>Publiceren ##

Net als bij Hallo multitenant-App Service, in een as-omgeving kunt u publiceren met:

- Web-implementatie.
- FTP.
- Continue integratie.
- Slepen en neerzetten in Hallo Kudu-console.
- Een IDE, zoals Visual Studio, Eclipse of IntelliJ IDEA.

Met een externe as-omgeving Hallo deze publicatieopties die alle moeten omgaan dezelfde. Zie voor meer informatie [-implementatie in Azure App Service][AppDeploy]. 

Hallo belangrijk verschil met het publiceren is ten opzichte van tooan ILB as-omgeving. Met een ILB as-omgeving zijn Hallo publishing eindpunten alle alleen beschikbaar via Hallo ILB. Hallo ILB is op een privé IP-adres in Hallo as-omgeving subnet in het virtuele netwerk Hallo. Als u geen netwerk toegang toohello ILB hebt, kunt u alle apps op die as-omgeving niet publiceren. Zoals vermeld in [maken en gebruiken een ILB-as-omgeving][MakeILBASE], moet u tooconfigure DNS voor Hallo apps in Hallo-systeem. Dat betekent onder meer Hallo SCM-eindpunt. Als ze zijn niet correct gedefinieerd, kunt u niet publiceren. Uw IDE moet ook toohave netwerk toegang toohello ILB in volgorde toopublish rechtstreeks tooit.

Internetgebaseerde CI systemen, zoals GitHub en Visual Studio Team Services, werkt niet met een ILB-as-omgeving omdat publishing Hallo-eindpunt niet toegankelijk Internet is. In plaats daarvan moet u een CI-besturingssysteem dat gebruikmaakt van een pull-model, zoals Dropbox toouse.

Hallo publishing eindpunten voor apps in een ILB-as-omgeving gebruik Hallo domein dat Hallo die ILB as-omgeving is gemaakt met. Kunt u deze bekijken in het publicatieprofiel Hallo-app en op de portalblade van Hallo app (in **overzicht** > **Essentials** en ook in **eigenschappen**). 

## <a name="pricing"></a>Prijzen ##

Hallo prijzen SKU aangeroepen **geïsoleerd** is gemaakt voor gebruik met ASEv2. Alle App Service-abonnementen die worden gehost in ASEv2 in Hallo geïsoleerd SKU prijzen. Geïsoleerde App Service plan tarieven kunnen verschillen per regio. 

Bovendien toohello prijs voor uw App Service-plannen, wordt er een vast tarief voor de as-omgeving zelf. Hallo vast tarief verandert niet met Hallo grootte van uw as-omgeving en betaalt voor de infrastructuur Hallo as-omgeving op een standaard frequentie van 1 aanvullende schalen front-voor elke 15 exemplaren van de App Service-plan.  

Als Hallo standaardfrequentie schaal van 1-front-end voor elke 15 exemplaren van de App Service-plan niet snel genoeg is, kunt u Hallo verhouding die front-ends worden toegevoegd of grootte van de front-ends van Hallo Hallo aanpassen.  Wanneer u Hallo verhouding of grootte aanpast, betaalt u voor de front-kernen Hallo die niet standaard zou worden toegevoegd.  

Bijvoorbeeld, als u Hallo scale verhouding too10 aanpast, een front-end toegevoegd voor elke 10 exemplaren in uw App Service-abonnementen. Hallo platte vergoeding geldt voor een snelheid van de schaal van één front-end voor elke 15 exemplaren. Met een ratio van de schaal van 10 betaalt u een vast bedrag voor Hallo derde front-end dat is toegevoegd voor Hallo 10 exemplaren van de App Service-abonnement. U hoeft niet toopay voor wanneer u 15 exemplaren bereikt omdat deze automatisch is toegevoegd.

Als u een Hallo grootte van Hallo front-ends too2 kernen aangepast maar Hallo verhouding niet wijzigen en betaalt u voor Hallo extra kernen.  Een as-omgeving wordt gemaakt met 2 front-ends, dus ook onder Hallo automatisch vergroten/verkleinen drempelwaarde die u voor 2 extra kernen betalen zou als u Hallo grootte too2 core front-ends verhoogd.

Zie voor meer informatie [prijzen voor Azure App Service][Pricing].

## <a name="delete-an-ase"></a>Verwijderen van een as-omgeving ##

toodelete een as-omgeving: 

1. Gebruik **verwijderen** bovenaan Hallo Hallo **App Service-omgeving** blade. 

2. Voer Hallo-naam van uw as-omgeving tooconfirm dat u wilt dat toodelete deze. Wanneer u een as-omgeving verwijdert, verwijdert u alle Hallo inhoud binnen deze ook. 

    ![Verwijderen van een as-omgeving][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


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
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
