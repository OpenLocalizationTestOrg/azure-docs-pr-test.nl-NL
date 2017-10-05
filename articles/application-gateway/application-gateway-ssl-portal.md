---
title: Configureren van SSL-offload - Azure Application Gateway - Azure-Portal | Microsoft Docs
description: Deze pagina vindt u instructies voor het maken van een toepassingsgateway met SSL-offload met behulp van de portal
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a>Een toepassingsgateway voor SSL-offload configureren met behulp van de portal

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure Application Gateway kan zodanig worden geconfigureerd dat de Secure Sockets Layer-sessie (SSL) wordt beëindigd bij de gateway om kostbare SSL-ontsleutelingstaken te voorkomen die worden uitgevoerd in de webfarm. Met SSL-offload worden ook het instellen van de front-endserver en het beheer van de webtoepassing eenvoudiger.

## <a name="scenario"></a>Scenario

Het volgende scenario gaat het bij het configureren van SSL-offload op een bestaande toepassingsgateway. Het scenario wordt ervan uitgegaan dat u de stappen voor het al hebt gevolgd [een toepassingsgateway maken](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Voordat u begint

Er is een certificaat voor SSL-offload met een application gateway configureert, vereist. Dit certificaat wordt geladen in de toepassingsgateway en gebruikt voor het versleutelen en ontsleutelen van het verkeer dat wordt verzonden via SSL. Het certificaat moet zich in de indeling Personal Information Exchange (pfx). Deze bestandsindeling kunt u de persoonlijke sleutel exporteerbaar die voor de toepassingsgateway vereist is om uit te voeren voor de versleuteling en ontsleuteling van verkeer.

## <a name="add-an-https-listener"></a>Toevoegen van een HTTPS-listener

De HTTPS-listener wordt gezocht naar verkeer op basis van de configuratie en helpt bij het verkeer naar de back-endpools sturen.

### <a name="step-1"></a>Stap 1

Navigeer naar de Azure-portal en selecteer een bestaande application gateway

### <a name="step-2"></a>Stap 2

Listeners en klik op de knop toevoegen om het toevoegen van een listener.

![overzichtsblade van App-gateway][1]

### <a name="step-3"></a>Stap 3

Vul de vereiste informatie voor de listener en upload het pfx-certificaat, als u klaar Klik op OK.

**Naam** -deze waarde is een beschrijvende naam van de listener.

**Frontend-IP configuratie** -deze waarde is de frontend-IP-configuratie die wordt gebruikt voor de listener.

**Frontend-poort (naam/poort)** : een beschrijvende naam voor de poort op de front-end van de toepassingsgateway gebruikt en de werkelijke poort gebruikt.

**Protocol** -een schakeloptie om te bepalen als https of http voor de front-endserver gebruikt.

**Certificaat (naam en wachtwoord)** - als SSL-offload wordt gebruikt, is een pfx-certificaat vereist voor deze instelling en een beschrijvende naam en wachtwoord zijn vereist.

![listener-blade toevoegen][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a>Een regel maken en deze koppelen aan de listener

De listener is gemaakt. Is het tijd om een regel voor het afhandelen van het verkeer van de listener te maken. Regels definiëren hoe verkeer wordt doorgestuurd naar de back-end-adresgroepen op basis van meerdere configuratie-instellingen, inclusief of sessie cookies gebaseerde affiniteit wordt gebruikt, protocol, poort en statuscontroles.

### <a name="step-1"></a>Stap 1

Klik op de **regels** van de toepassingsgateway, en klik vervolgens op toevoegen.

![blade App gateway-regels][3]

### <a name="step-2"></a>Stap 2

Op de **basic regel toevoegen** blade, typ de beschrijvende naam voor de regel en kies de listener is gemaakt in de vorige stap. Kies de juiste back-endpool en HTTP-instelling en klikt u op **OK**

![venster van de instellingen voor HTTPS][4]

De instellingen zijn nu opgeslagen op de toepassingsgateway. Het opslaan verwerken voor deze instellingen kunnen even duren voordat ze beschikbaar zijn voor weergeven via de portal of PowerShell. Wanneer de toepassingsgateway opgeslagen verwerkt de versleuteling en ontsleuteling van verkeer. Al het verkeer tussen de toepassingsgateway en de back-end-webservers wordt verwerkt via http. Alle communicatie naar de client als gestart via https wordt geretourneerd naar de client die is versleuteld.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het configureren van een aangepaste health test met Azure Application Gateway, [maken van een aangepaste health test](application-gateway-create-gateway-portal.md).

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
