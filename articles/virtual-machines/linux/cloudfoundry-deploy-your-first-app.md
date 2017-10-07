---
title: aaaDeploy uw eerste app tooCloud Foundry op Microsoft Azure | Microsoft Docs
description: Een toepassing tooCloud Foundry in Azure implementeren
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a>Implementeren van uw eerste app tooCloud Foundry op Microsoft Azure

[Foundry cloud](http://cloudfoundry.org) is een platform voor populaire open-source beschikbaar op Microsoft Azure. In dit artikel wordt gedemonstreerd hoe toodeploy en beheren van een toepassing in de Cloud Foundry in een Azure-omgeving.

## <a name="create-a-cloud-foundry-environment"></a>Een Cloud Foundry-omgeving maken

Er zijn verschillende opties voor het maken van een Cloud Foundry-omgeving op Azure:

- Gebruik Hallo [belangrijke Cloud Foundry aanbieding] [ pcf-azuremarketplace] in hello Azure Marketplace toocreate een standaard omgeving die PCF Ops Manager en hello Azure Service Broker. U vindt [volledige instructies] [ pcf-azuremarketplace-pivotaldocs] bieden voor het implementeren van Hallo marketplace in Hallo belangrijke documentatie.
- Maakt een aangepaste omgeving door [belangrijke Cloud Foundry handmatig implementeren][pcf-custom].
- [Hallo open source Cloud Foundry pakketten rechtstreeks implementeren] [ oss-cf-bosh] door het instellen van een [BOSH](http://bosh.io) directeur, een virtuele machine die Hallo-implementatie van Hallo Cloud Foundry-omgeving coördineert.

> [!IMPORTANT] 
> Als u PCF vanuit Azure Marketplace hello implementeert, noteer Hallo SYSTEMDOMAINURL en Hallo beheerdersreferenties vereist tooaccess Hallo belangrijke Apps Manager, die beide worden beschreven in de Implementatiehandleiding voor Hallo marketplace. Ze zijn benodigde toocomplete in deze zelfstudie. Voor implementaties van marketplace wordt Hallo SYSTEMDOMAINURL Hallo formulier https://system. *IP-adres*. cf.pcfazure.com.

## <a name="connect-toohello-cloud-controller"></a>Verbinding maken met toohello Cloud-Controller

Hallo Cloud-Controller is Hallo primaire ingang punt tooa Cloud Foundry-omgeving voor het implementeren en beheren van toepassingen. Hallo core Cloud Controller API (CCAPI) is een REST-API, maar is toegankelijk via verschillende hulpprogramma's. In dit geval er interactief mee werken via Hallo [Cloud Foundry CLI][cf-cli]. U kunt Hallo CLI installeren op Linux-, Mac OS- of Windows, maar als u liever niet tooinstall helemaal deze beschikbaar is geïnstalleerd in Hallo [Azure Cloud Shell][cloudshell-docs].

toevoegen van toolog, `api` toohello SYSTEMDOMAINURL die u hebt verkregen via Hallo marketplace-implementatie. Aangezien Hallo standaardimplementatie gebruikmaakt van een zelfondertekend certificaat, moet u ook opnemen Hallo `skip-ssl-validation` overschakelen.

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

U bent na vragen aan gebruiker toolog in toohello Cloud-Controller. Hallo beheerder accountreferenties die u hebt aangeschaft van Hallo marketplace implementatiestappen gebruikt.

Cloud Foundry biedt *organisaties* en *spaties* als naamruimten tooisolate Hallo teams en omgevingen binnen een gedeelde implementatie. Hallo PCF marketplace implementatie bevat standaard Hallo *system* org en een set spaties gemaakt toocontain basisonderdelen Hallo zoals Hallo automatisch schalen service en hello Azure service broker. Kies nu Hallo *system* ruimte.


## <a name="create-an-org-and-space"></a>Een organisatie en de ruimte maken

Als u typt `cf apps`, ziet u een set systeemtoepassingen die zijn geïmplementeerd in de ruimte die op Hallo binnen Hallo system org. 

U dient te houden met Hallo *system* org gereserveerd voor systeemtoepassingen, dus maak een organisatie en de ruimte toohouse onze voorbeeldtoepassing.

```bash
cf create-org myorg
cf create-space dev -o myorg
```

Hallo doel opdracht tooswitch toohello nieuwe org en ruimte gebruiken:

```bash
cf target -o testorg -s dev
```

Nu, wanneer u een toepassing implementeert, deze automatisch is gemaakt in de nieuwe org Hallo en ruimte. tooconfirm die er zijn momenteel geen apps in Hallo nieuwe org per ruimte, typ `cf apps` opnieuw.

> [!NOTE] 
> Zie voor meer informatie over organisaties en spaties en hoe ze kunnen worden gebruikt voor op rollen gebaseerde toegangsbeheer (RBAC) Hallo [Cloud Foundry documentatie][cf-orgs-spaces-docs].

## <a name="deploy-an-application"></a>Een app implementeren

We gebruiken een voorbeeldtoepassing Cloud Foundry Hallo Spring Cloud, die is geschreven in Java en op basis van Hallo aangeroepen [Spring Framework](http://spring.io) en [Spring Boot](http://projects.spring.io/spring-boot/).

### <a name="clone-hello-hello-spring-cloud-repository"></a>Hallo Hallo Spring Cloud opslagplaats klonen

Hallo Hallo Spring Cloud voorbeeldtoepassing is beschikbaar op GitHub. Kloon tooyour omgeving en naar de nieuwe map Hallo wijzigen:

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a>Hallo-toepassing bouwen

Build Hallo app met behulp [Apache Maven](http://maven.apache.org).

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a>Implementeer de toepassing hello met cf push

U kunt de meeste toepassingen tooCloud Foundry implementeren met behulp van Hallo `push` opdracht:

```bash
cf push
```

Wanneer u *push* een toepassing, Cloud Foundry detecteert Hallo type toepassing (in dit geval een Java-app) en de afhankelijkheden ervan (in dit geval Hallo Spring framework) identificeert. Vervolgens pakketten alles toorun uw code vereist in de container installatiekopie van een zelfstandige, ook wel een *droplet*. Ten slotte Cloud Foundry planningen Hallo van toepassing op een van de beschikbare machines Hallo in uw omgeving en maakt u een URL waarop u bereiken kan, die beschikbaar is in het Hallo-uitvoer van Hallo-opdracht.

![Uitvoer van cf push-opdracht][cf-push-output]

toosee Hallo Hallo-spring-cloud-toepassing open Hallo opgegeven URL in uw browser:

![Standaardgebruikersinterface voor Hallo Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> meer informatie over wat er tijdens gebeurt toolearn `cf push`, Zie [hoe toepassingen worden voorbereid] [ cf-push-docs] in Hallo Cloud Foundry-documentatie.

## <a name="view-application-logs"></a>Logboeken van de toepassing bekijken

U kunt Hallo Cloud Foundry CLI tooview Logboeken kunt gebruiken voor een toepassing met de naam:

```bash
cf logs hello-spring-cloud
```

Standaard Hallo opdracht gebruikt Logboeken *tail*, waarmee nieuwe logboeken wordt weergegeven als ze zijn geschreven. Hallo Hallo-spring-cloud-app in de browser Hallo toosee nieuwe logboeken worden weergegeven, worden vernieuwd.

tooview logboeken die al zijn geschreven, voeg Hallo `recent` switch:

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a>Hallo-toepassing schalen

Standaard `cf push` slechts één exemplaar van uw toepassing maakt. tooensure hoge beschikbaarheid en inschakelen scale-out voor een hogere doorvoer, wilt u in het algemeen toorun meer dan één exemplaar van uw toepassingen. Kunt u eenvoudig uitschalen reeds geïmplementeerde toepassingen met behulp van Hallo `scale` opdracht:

```bash
cf scale -i 2 hello-spring-cloud
```

Actieve Hallo `cf app` opdracht bij de toepassing hello toont Cloud Foundry maken van een ander exemplaar van de toepassing hello. Eenmaal Hallo toepassing is gestart, worden de taakverdeling verkeer tooit Cloud Foundry automatisch gestart.


## <a name="next-steps"></a>Volgende stappen

- [Lees Hallo Cloud Foundry-documentatie][cloudfoundry-docs]
- [Hallo Visual Studio Team Services-invoegtoepassing voor Cloud Foundry instellen][vsts-plugin]
- [Hallo Microsoft Log Analytics pijp configureren voor Cloud Foundry][loganalytics-nozzle]

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png