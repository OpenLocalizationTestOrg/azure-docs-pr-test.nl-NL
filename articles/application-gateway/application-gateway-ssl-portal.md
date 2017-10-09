---
title: aaaConfigure SSL-offload - Azure Application Gateway - Azure Portal | Microsoft Docs
description: Deze pagina vindt u instructies toocreate een toepassingsgateway met SSL-offload met behulp van Hallo-portal
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
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a>Een toepassingsgateway voor SSL-offload configureren met behulp van Hallo-portal

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure Application Gateway kan worden geconfigureerd tooterminate Hallo Secure Sockets Layer (SSL)-sessie op Hallo gateway tooavoid kostbare SSL ontsleuteling taken toohappen op Hallo-webfarm. SSL-offload vereenvoudigt ook Hallo front-end-server instellen en beheren van Hallo-webtoepassing.

## <a name="scenario"></a>Scenario

Hallo volgen scenario doorloopt configureren van SSL-offload op een bestaande toepassingsgateway. Hallo scenario wordt ervan uitgegaan dat u al stappen hebt gevolgd hello te[een toepassingsgateway maken](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Voordat u begint

tooconfigure SSL-offload met een application gateway, een certificaat is vereist. Dit certificaat is geladen in de toepassingsgateway Hallo en tooencrypt gebruikt en ontsleutelen van Hallo verkeer dat wordt verzonden via SSL. Hallo-certificaat moet toobe Personal Information Exchange (pfx)-indeling. Deze bestandsindeling kunt Hallo persoonlijke sleutel toobe geëxporteerd die vereist wordt door Hallo application gateway tooperform Hallo versleuteling en ontsleuteling van verkeer.

## <a name="add-an-https-listener"></a>Toevoegen van een HTTPS-listener

Hallo HTTPS-listener zoekt verkeer op basis van de configuratie en helpt route Hallo verkeer toohello back-endpools.

### <a name="step-1"></a>Stap 1

Gaat toohello Azure-portal en selecteert u een bestaande application gateway

### <a name="step-2"></a>Stap 2

Listeners en klik op de knop tooadd een listener voor Hallo toevoegen.

![overzichtsblade van App-gateway][1]

### <a name="step-3"></a>Stap 3

Vul het vereiste informatie voor de listener Hallo Hallo en uploaden Hallo pfx-certificaat, als u klaar klikt u op OK.

**Naam** -deze waarde is een beschrijvende naam van het Hallo-listener.

**Frontend-IP configuratie** -deze waarde is Hallo frontend-IP-configuratie die wordt gebruikt voor het Hallo-listener.

**Frontend-poort (naam/poort)** -een beschrijvende naam voor het Hallo-poort die wordt gebruikt op Hallo front-end van de toepassingsgateway Hallo en Hallo werkelijke poort die wordt gebruikt.

**Protocol** -een switch toodetermine als https of http wordt gebruikt voor het Hallo-front-end.

**Certificaat (naam en wachtwoord)** - als SSL-offload wordt gebruikt, is een pfx-certificaat vereist voor deze instelling en een beschrijvende naam en wachtwoord zijn vereist.

![listener-blade toevoegen][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a>Een regel maken en koppelen toohello listener

Hallo-listener is gemaakt. Het is tijd toocreate het verkeer van een regel toohandle Hallo van Hallo listener. Regels definiëren hoe verkeer wordt gerouteerd toohello back-endpools op basis van meerdere configuratie-instellingen, inclusief of sessie cookies gebaseerde affiniteit wordt gebruikt, protocol, poort en statuscontroles.

### <a name="step-1"></a>Stap 1

Klik op Hallo **regels** van toepassingsgateway hello, en klik vervolgens op toevoegen.

![blade App gateway-regels][3]

### <a name="step-2"></a>Stap 2

Op Hallo **basic regel toevoegen** blade Typ Hallo beschrijvende naam voor Hallo regel en kies Hallo-listener is gemaakt in de vorige stap Hallo. Kies Hallo juiste back-endpool en HTTP-instelling en klik op **OK**

![venster van de instellingen voor HTTPS][4]

Hallo-instellingen worden nu opgeslagen toohello toepassingsgateway. Hallo Sla-proces voor deze instellingen duurt even voordat ze beschikbaar tooview via Hallo portal of PowerShell. Toepassingsgateway eenmaal opgeslagen Hallo verwerkt Hallo versleuteling en ontsleuteling van verkeer. Al het verkeer tussen de toepassingsgateway Hallo en Hallo back-end-webservers wordt verwerkt via http. Alle communicatie back toohello client als gestart via https geretourneerd toohello client versleuteld.

## <a name="next-steps"></a>Volgende stappen

toolearn hoe tooconfigure een aangepaste health test met Azure Application Gateway, Zie [maken van een aangepaste health test](application-gateway-create-gateway-portal.md).

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
