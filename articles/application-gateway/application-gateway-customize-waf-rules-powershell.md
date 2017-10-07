---
title: web application firewall-regels in Azure Application Gateway - PowerShell aaaCustomize | Microsoft Docs
description: In dit artikel bevat informatie over hoe toocustomize web application firewall regels in Application Gateway met PowerShell.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: f320e687b0f621515255469dac8e375cdd900dda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a>Web application firewall-regels via PowerShell aanpassen

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

Hello Azure Application Gateway web application firewall (WAF) biedt beveiliging voor webtoepassingen. Deze beveiligingen worden geleverd door Hallo Open Web Application Security Project (OWASP) Core regel ingesteld (CRS). Sommige regels kunnen valse positieven veroorzaken en echte verkeer blokkeert. Daarom biedt Application Gateway Hallo mogelijkheid toocustomize regelgroepen en regels. Zie voor meer informatie over de specifieke regelgroepen Hallo en regels [lijst met web application firewall CRS regelgroepen en regels](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Groepen van de regel weergeven en regels

Hallo volgende codevoorbeelden ziet u hoe tooview regels en groepen die kunnen worden geconfigureerd op een gateway WAF-toepassing-regel.

### <a name="view-rule-groups"></a>Groepen van de regel weergeven

Hallo volgende voorbeeld ziet u hoe groepen met tooview regels:

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

Hallo na uitvoer is een afgekapte reactie van Hallo voorgaande voorbeeld:

```
OWASP (Ver. 3.0):

    REQUEST-910-IP-REPUTATION:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            910011     Rule 910011
            910012     Rule 910012
            ...        ...

    REQUEST-911-METHOD-ENFORCEMENT:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            911011     Rule 911011
            ...        ...

OWASP (Ver. 2.2.9):

    crs_20_protocol_violations:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            960911     Invalid HTTP Request Line
            981227     Apache Error: Invalid URI in Request.
            960000     Attempted multipart/form-data bypass
            ...        ...
```

## <a name="disable-rules"></a>Regels uitschakelen

Hallo volgende voorbeeld wordt uitgeschakeld regels `910018` en `910017` op een toepassingsgateway:

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Volgende stappen

Nadat u uw uitgeschakelde regels hebt geconfigureerd, leert u hoe tooview uw WAF-Logboeken. Zie voor meer informatie [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
