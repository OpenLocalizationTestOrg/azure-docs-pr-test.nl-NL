---
title: aaaCreate een pad op basis van een Azure-Portal - Azure Application Gateway - regel | Microsoft Docs
description: Meer informatie over hoe toocreate een regel op basis van het pad voor een toepassingsgateway met behulp van de portal Hallo
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a>Een regel op basis van het pad voor een toepassingsgateway maken met behulp van Hallo-portal

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

URL-pad gebaseerde routering, kunt u tooassociate routes op basis van de URL-pad Hallo van Http-aanvraag. Het wordt gecontroleerd of er een route tooa back-end-adresgroep geconfigureerd voor het Hallo-URL die wordt vermeld in Hallo Application Gateway is en verzendt Hallo netwerkverkeer toohello gedefinieerd back-end-pool. Vaak gebruikt voor het doorsturen van op basis van een URL is tooload van aanvragen verdelen over voor andere typen inhoud toodifferent back-end-servergroepen.

URL gebaseerde routering introduceert een nieuwe regel type tooapplication gateway. Toepassingsgateway heeft twee regeltypen: basic-en op basis van het pad. Hallo basic regeltype, biedt een round robin-service voor Hallo back-end voor groepen tijdens het pad gebaseerde regels bovendien tooround robin distributie, ook rekening wordt gehouden pad patroon van de aanvraag-URL Hallo daarbij de juiste back-endpool Hallo.

## <a name="scenario"></a>Scenario

Hallo doorloopt volgende scenario maken van een regel op basis van een pad in een bestaande toepassingsgateway.
Hallo scenario wordt ervan uitgegaan dat u al stappen hebt gevolgd hello te[een toepassingsgateway maken](application-gateway-create-gateway-portal.md).

![URL-route][scenario]

## <a name="createrule"></a>Hallo-pad op basis van een regel maken

Een regel op basis van het pad moet een eigen listener voordat Hallo regel maken die ervoor tooverify die u hebt een toouse beschikbaar listener worden.

### <a name="step-1"></a>Stap 1

Navigeer toohello [Azure-portal](http://portal.azure.com) en selecteer een bestaande toepassing. Klik op **regels**

![Overzicht van Application Gateway][1]

### <a name="step-2"></a>Stap 2

Klik op **op basis van het pad** tooadd knop een nieuwe regel op basis van het pad.

### <a name="step-3"></a>Stap 3

Hallo **toevoegen op basis van een pad regel** blade bevat twee secties. de eerste sectie Hallo is waar u Hallo listener, Hallo-naam van regel Hallo en Hallo pad standaardinstellingen gedefinieerd. Hallo zijn standaardinstellingen pad voor routes die niet onder Hallo aangepast op basis van een pad route vallen. tweede gedeelte van Hallo Hallo **toevoegen op basis van een pad regel** blade is waar u Hallo pad gebaseerde regels zelf definiëren.

**Basisinstellingen**

* **Naam** -deze waarde is een beschrijvende naam toohello regel die toegankelijk is in Hallo-portal.
* **Listener** -deze waarde is Hallo-listener die wordt gebruikt voor het Hallo-regel.
* **Standaard back-endpool** -deze instelling is Hallo-instelling die Hallo back-end toobe gebruikt voor de standaardregel Hallo definieert
* **Standaardinstellingen voor HTTP-** -deze instelling is Hallo-instelling die Hallo HTTP-instellingen toobe gebruikt voor de standaardregel Hallo definieert.

**Regels op basis van het pad**

* **Naam** -deze waarde is een beschrijvende naam op basis van toopath regel.
* **Paden** -deze instelling bepaalt Hallo pad Hallo regel zoekt doorsturen van verkeer
* **Back-Endpool** -deze instelling is Hallo-instelling die Hallo back-end toobe gebruikt voor het Hallo-regel definieert
* **HTTP-instelling** -deze instelling is Hallo-instelling die Hallo HTTP-instellingen toobe gebruikt voor het Hallo-regel definieert.

> [!IMPORTANT]
> Paden: lijst Hallo van pad patronen toomatch. Elk moet beginnen met / en Hallo enige plaats waar een '\*' is toegestaan Hallo einde. Voorbeelden van geldige zijn/xyz, /xyz* of xyz / *.  

![Een regel op basis van een pad blade met informatie is ingevuld toevoegen][2]

Toevoegen van een regel op basis van het pad tooan is bestaande application gateway een eenvoudig proces via Hallo-portal. Nadat een regel op basis van het pad is gemaakt, kan het bewerkte tooadd extra regels zijn. 

![Extra regels op basis van het pad toevoegen][3]

Deze stap configureert u een route op basis van het pad. Het is belangrijk toounderstand aanvragen niet opnieuw geschreven, zoals aanvragen worden geleverd in de toepassingsgateway inspecteert Hallo-aanvraag en basic op Hallo url patroon verzendt Hallo aanvraag toohello juiste back-end.

## <a name="next-steps"></a>Volgende stappen

hoe tooconfigure SSL-Offloading met Azure Application Gateway, Zie toolearn [SSL-Offload configureren](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
