---
title: web application firewall-regels in Azure Application Gateway - Azure CLI 2.0 aaaCustomize | Microsoft Docs
description: In dit artikel bevat informatie over hoe toocustomize web application firewall regels Application Gateway met hello Azure CLI 2.0.
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
ms.openlocfilehash: b83ffb9f6a7e0d0c8c970885d2bcb3b63d32581c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a><span data-ttu-id="e85d7-103">Web application firewall-regels via hello Azure CLI 2.0 aanpassen</span><span class="sxs-lookup"><span data-stu-id="e85d7-103">Customize web application firewall rules through hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e85d7-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e85d7-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="e85d7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e85d7-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="e85d7-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e85d7-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="e85d7-107">Hello Azure Application Gateway web application firewall (WAF) biedt beveiliging voor webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="e85d7-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="e85d7-108">Deze beveiligingen worden geleverd door Hallo Open Web Application Security Project (OWASP) Core regel ingesteld (CRS).</span><span class="sxs-lookup"><span data-stu-id="e85d7-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="e85d7-109">Sommige regels kunnen valse positieven veroorzaken en echte verkeer blokkeert.</span><span class="sxs-lookup"><span data-stu-id="e85d7-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="e85d7-110">Daarom biedt Application Gateway Hallo mogelijkheid toocustomize regelgroepen en regels.</span><span class="sxs-lookup"><span data-stu-id="e85d7-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="e85d7-111">Zie voor meer informatie over de specifieke regelgroepen Hallo en regels [lijst van groepen met web application firewall CRS regels en voorschriften](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="e85d7-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="e85d7-112">Groepen van de regel weergeven en regels</span><span class="sxs-lookup"><span data-stu-id="e85d7-112">View rule groups and rules</span></span>

<span data-ttu-id="e85d7-113">Hallo volgende codevoorbeelden laten zien hoe tooview regels en de regels van de groepen die kunnen worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e85d7-113">hello following code examples show how tooview rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="e85d7-114">Groepen van de regel weergeven</span><span class="sxs-lookup"><span data-stu-id="e85d7-114">View rule groups</span></span>

<span data-ttu-id="e85d7-115">Hallo volgende voorbeeld ziet u hoe tooview regelgroepen Hallo:</span><span class="sxs-lookup"><span data-stu-id="e85d7-115">hello following example shows how tooview hello rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="e85d7-116">Hallo na uitvoer is een afgekapte reactie van Hallo voorgaande voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e85d7-116">hello following output is a truncated response from hello preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  },
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_2.2.9",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
   "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "crs_20_protocol_violations",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "2.2.9",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="e85d7-117">Regels weergeven in een regelgroep</span><span class="sxs-lookup"><span data-stu-id="e85d7-117">View rules in a rule group</span></span>

<span data-ttu-id="e85d7-118">Hallo volgende voorbeeld ziet u hoe tooview regels in een opgegeven regel-groep:</span><span class="sxs-lookup"><span data-stu-id="e85d7-118">hello following example shows how tooview rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="e85d7-119">Hallo na uitvoer is een afgekapte reactie van Hallo voorgaande voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e85d7-119">hello following output is a truncated response from hello preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": [
          {
            "description": "Rule 910011",
            "ruleId": 910011
          },
          ...
        ]
      }
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

## <a name="disable-rules"></a><span data-ttu-id="e85d7-120">Regels uitschakelen</span><span class="sxs-lookup"><span data-stu-id="e85d7-120">Disable rules</span></span>

<span data-ttu-id="e85d7-121">Hallo volgende voorbeeld wordt uitgeschakeld regels `910018` en `910017` op een toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="e85d7-121">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="e85d7-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e85d7-122">Next steps</span></span>

<span data-ttu-id="e85d7-123">Nadat u uw uitgeschakelde regels hebt geconfigureerd, leert u hoe tooview uw WAF-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="e85d7-123">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="e85d7-124">Zie voor meer informatie [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="e85d7-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
