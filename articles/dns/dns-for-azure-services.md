---
title: aaaUsing Azure DNS met andere Azure-services | Microsoft Docs
description: Begrijpen hoe toouse Azure DNS tooresolve naam voor andere Azure-services
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure dns
ms.assetid: e9b5eb94-7984-4640-9930-564bb9e82b78
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 09/21/2016
ms.author: gwallace
ms.openlocfilehash: 791f93d6aff2c638c08518e9f1e8ab89ac8de3f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-dns-works-with-other-azure-services"></a>De werking van Azure DNS met andere Azure-services

Azure DNS is een gehoste DNS-beheer en name resolution-service. Hiermee kunt u toocreate openbare DNS-namen voor Hallo andere toepassingen en services die u hebt geïmplementeerd in Azure. Maken van een naam voor een Azure-service in uw aangepaste domein is net zo eenvoudig als het toevoegen van een record van het juiste type Hallo voor uw service.

* Voor dynamisch toegewezen IP-adressen, moet u een DNS CNAME-record maps toohello DNS-naam die Azure gemaakt voor uw service. DNS-standaarden voorkomen dat u een CNAME-record gebruiken voor het toppunt van Hallo zone.
* Voor de statisch toegewezen IP-adressen, kunt u een DNS A-record met behulp van een naam, met inbegrip van een *Open domein* naam in het toppunt Hallo zone.

Hallo volgende tabel overzichten Hallo ondersteund recordtypen die kunnen worden gebruikt voor verschillende Azure-services. Als u in deze tabel zien kunt, ondersteunt Azure DNS alleen DNS-records voor internetgerichte netwerkbronnen. Azure DNS, kan niet worden gebruikt voor naamomzetting van interne, particuliere adressen.

| Azure-service | Netwerkinterface | Beschrijving |
| --- | --- | --- |
| Application Gateway |[Front-openbare IP-adres](dns-custom-domain.md#public-ip-address) |U kunt een DNS A of CNAME-record maken. |
| Load balancer |[Front-openbare IP-adres](dns-custom-domain.md#public-ip-address)  |U kunt een DNS A of CNAME-record maken. Load Balancer kan een IPv6-openbare IP-adres wordt dynamisch toegewezen hebben. Daarom moet u een CNAME-record voor een IPv6-adres maken. |
| Traffic Manager |Openbare naam |U kunt alleen een CNAME die toohello trafficmanager.net naam toegewezen tooyour Traffic Manager-profiel wijst maken. Zie voor meer informatie [hoe Traffic Manager werkt](../traffic-manager/traffic-manager-overview.md#traffic-manager-example). |
| Cloudservice |[Openbare IP-adres](dns-custom-domain.md#public-ip-address) |Voor de statisch toegewezen IP-adressen, kunt u een DNS A-record maken. Voor dynamisch toegewezen IP-adressen, moet u een CNAME-record dat is toegewezen toohello *cloudapp.net* naam. Deze regel geldt tooVMs gemaakt in de klassieke portal Hallo omdat ze zijn geïmplementeerd als een cloudservice. Zie voor meer informatie [een aangepaste domeinnaam configureren in Cloudservices](../cloud-services/cloud-services-custom-domain-name-portal.md). |
| App Service | [Extern IP-adres](dns-custom-domain.md#app-service-web-apps) |U kunt een DNS A-record maken voor het externe IP-adressen. Anders moet u een CNAME-record dat is toegewezen toohello azurewebsites.net naam maken. Zie voor meer informatie [toewijzen van een aangepast domein naam tooan Apps van Azure](../app-service-web/web-sites-custom-domain-name.md) |
| Resource Manager virtuele machines |[Openbare IP-adres](dns-custom-domain.md#public-ip-address) |Resource Manager virtuele machines kunnen openbare IP-adressen hebben. Een virtuele machine met een openbare IP-adres kan ook worden achter een load balancer. U kunt een DNS A of CNAME-record maken voor Hallo openbaar adres. Deze aangepaste naam kan worden gebruikt toobypass Hallo VIP op Hallo load balancer. |
| Klassieke VM's |[Openbare IP-adres](dns-custom-domain.md#public-ip-address) |Klassieke virtuele machines gemaakt met behulp van PowerShell of CLI kan worden geconfigureerd met een dynamisch of statisch (gereserveerd) virtueel adres. U kunt een DNS CNAME of een record respectievelijk maken. |
