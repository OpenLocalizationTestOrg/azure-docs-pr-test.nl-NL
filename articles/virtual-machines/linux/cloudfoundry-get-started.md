---
title: aaaGetting gestart met Cloud Foundry op Microsoft Azure | Microsoft Docs
description: OSS of belangrijke Cloud Foundry uitvoeren in Microsoft Azure
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a>Cloud Foundry op Azure

Cloud Foundry is een open source platform-as-a-service (PaaS) voor het bouwen, te implementeren en gebruiken van 12-factor-toepassingen die in verschillende talen en frameworks ontwikkeld. Dit document beschrijft Hallo-opties die u hebt voor het uitvoeren van de Cloud Foundry op Azure en hoe u kunt aan de slag.

## <a name="cloud-foundry-offerings"></a>De offerings Foundry cloud

Er zijn twee soorten Cloud Foundry beschikbaar toorun op Azure: open source Cloud Foundry (OSS CF) en belangrijke Cloud Foundry (PCF). OSS CF is een volledig [open source](https://github.com/cloudfoundry) versie van Cloud Foundry beheerd door Hallo Cloud Foundry Foundation. Belangrijke Cloud Foundry is een enterprise-distributie van Cloud Foundry van belangrijke Software, Inc. Kijken we enkele Hallo verschillen tussen de twee Hallo-oplossingen.

### <a name="open-source-cloud-foundry"></a>Open-source Cloud Foundry

U kunt OSS Cloud Foundry in Azure implementeren door eerst een directeur BOSH implementeren en het implementeren van Cloud Foundry, met behulp van Hallo [-instructies op GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md). toolearn meer over het gebruik van OSS-CF Zie Hallo [documentatie](https://docs.cloudfoundry.org/) geleverd door Hallo Cloud Foundry Foundation.

Microsoft biedt ondersteuning voor het best-effort voor OSS CF via Hallo community kanalen te volgen:

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a>bosh-azure-KPI-kanaal op [Cloud Foundry Slack](https://slack.cloudfoundry.org/)
- [CF bosh mailinglijst](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- Problemen met GitHub hello [KPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) en [service broker](https://github.com/Azure/meta-azure-service-broker/issues)

>[!NOTE]
> Hallo-niveau van ondersteuning voor uw Azure-resources, zoals Hallo virtuele machines waarop u Cloud-Foundry uitvoert is gebaseerd op de ondersteuning van Azure-overeenkomst. Communityondersteuning best effort is alleen van toepassing toohello Cloud Foundry-specifieke onderdelen.

### <a name="pivotal-cloud-foundry"></a>Belangrijke Cloud Foundry

Belangrijke Cloud Foundry Hallo bevat dezelfde kernplatform als Hallo OSS-distributiepunt, samen met een reeks bedrijfseigen beheerhulpprogramma's en enterprise-ondersteuning. toorun PCF op Azure, moet u een licentie van Pivotal verkrijgen. Hallo PCF aanbieding van hello Azure marketplace omvat proeflicentie is 90 dagen.

Hallo's bevatten [belangrijke Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), een webtoepassing die vereenvoudigt de implementatie en beheer van een basis Cloud Foundry en [belangrijke Apps Manager](https://docs.pivotal.io/pivotalcf/console/), een webtoepassing voor het beheren van gebruikers en toepassingen.

Bovendien toohello ondersteuningskanalen voor OSS CF hierboven vermeld, kunt een licentie PCF u toocontact Pivotal voor ondersteuning. Microsoft Pivotal ondersteuning werkstromen waarmee u toocontact beide partijen voor hulp hebben ingeschakeld en en hebben uw vraag op de juiste wijze worden doorgestuurd, afhankelijk van waar Hallo probleem wordt veroorzaakt.

## <a name="azure-service-broker"></a>Azure Service Broker

Cloud Foundry moedigt Hallo ['twaalf factor app'](https://12factor.net/) methodologie die bijdraagt aan een schone scheiding van toepassingsprocessen staatloze en stateful services back-ups. [Service beleggingsmakelaars](https://docs.cloudfoundry.org/services/api.html) bieden een consistente manier tooprovision en ondersteunende services tooapplications binden. Hallo [Azure service broker](https://github.com/Azure/meta-azure-service-broker) staan enkele Hallo belangrijke Azure-services via dit kanaal, met inbegrip van Azure storage en Azure SQL.

Als u van belangrijke Cloud Foundry gebruikmaakt, Hallo service broker is ook [beschikbaar als een tegel](https://docs.pivotal.io/azure-sb/installing.html) van Hallo centrale netwerk.

## <a name="related-resources"></a>Gerelateerde resources

### <a name="visual-studio-team-services-plugin"></a>Visual Studio Team Services-invoegtoepassing

Cloud Foundry is uitermate geschikt tooagile software development, waaronder Hallo gebruik van doorlopende integratie (CI) en continue levering (CD). Als u Visual Studio Team Services (VSTS) toomanage projecten en wilt tooset van een Cloud Foundry targeting CI/CD-pijplijn, kunt u Hallo [VSTS Cloud Foundry-opbouwextensie](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension). Hallo-invoegtoepassing kunt u eenvoudige tooconfigure en implementaties tooCloud Foundry, automatiseren of uitgevoerd in Azure of een andere omgeving.

## <a name="next-steps"></a>Volgende stappen

- [Belangrijke Cloud Foundry implementeren vanuit Azure Marketplace Hallo](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [Een app tooCloud Foundry in Azure implementeren](./cloudfoundry-deploy-your-first-app.md)
