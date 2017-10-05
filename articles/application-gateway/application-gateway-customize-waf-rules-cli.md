---
title: Web application firewall-regels in Azure Application Gateway - Azure CLI 2.0 aanpassen | Microsoft Docs
description: In dit artikel bevat informatie over het aanpassen van web application firewall-regels in Application Gateway met de Azure CLI 2.0.
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
ms.openlocfilehash: 456be048dc2d82cd50d145b71f17a84a7189ea96
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-cli-20"></a><span data-ttu-id="01b9b-103">Web application firewall-regels via de Azure CLI 2.0 aanpassen</span><span class="sxs-lookup"><span data-stu-id="01b9b-103">Customize web application firewall rules through the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="01b9b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="01b9b-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="01b9b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01b9b-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="01b9b-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="01b9b-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="01b9b-107">De Azure Application Gateway web application firewall (WAF) biedt beveiliging voor webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="01b9b-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="01b9b-108">Deze beveiligingen worden geleverd door de toepassing van Open Web Project beveiliging (OWASP) Core regel ingesteld (CRS).</span><span class="sxs-lookup"><span data-stu-id="01b9b-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="01b9b-109">Sommige regels kunnen valse positieven veroorzaken en echte verkeer blokkeert.</span><span class="sxs-lookup"><span data-stu-id="01b9b-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="01b9b-110">Daarom biedt Application Gateway de mogelijkheid om aan te passen regelgroepen en regels.</span><span class="sxs-lookup"><span data-stu-id="01b9b-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="01b9b-111">Zie voor meer informatie over de specifieke regelgroepen en regels [lijst van groepen met web application firewall CRS regels en voorschriften](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="01b9b-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="01b9b-112">Groepen van de regel weergeven en regels</span><span class="sxs-lookup"><span data-stu-id="01b9b-112">View rule groups and rules</span></span>

<span data-ttu-id="01b9b-113">De volgende codevoorbeelden laten zien hoe regels en groepen die kunnen worden geconfigureerd met regels weergeven.</span><span class="sxs-lookup"><span data-stu-id="01b9b-113">The following code examples show how to view rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="01b9b-114">Groepen van de regel weergeven</span><span class="sxs-lookup"><span data-stu-id="01b9b-114">View rule groups</span></span>

<span data-ttu-id="01b9b-115">Het volgende voorbeeld ziet u hoe de regelgroepen weergeven:</span><span class="sxs-lookup"><span data-stu-id="01b9b-115">The following example shows how to view the rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="01b9b-116">De volgende uitvoer is een afgekapte reactie van het vorige voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="01b9b-116">The following output is a truncated response from the preceding example:</span></span>

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

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="01b9b-117">Regels weergeven in een regelgroep</span><span class="sxs-lookup"><span data-stu-id="01b9b-117">View rules in a rule group</span></span>

<span data-ttu-id="01b9b-118">Het volgende voorbeeld ziet u hoe regels in een opgegeven regelgroep weergeven:</span><span class="sxs-lookup"><span data-stu-id="01b9b-118">The following example shows how to view rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="01b9b-119">De volgende uitvoer is een afgekapte reactie van het vorige voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="01b9b-119">The following output is a truncated response from the preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="01b9b-120">Regels uitschakelen</span><span class="sxs-lookup"><span data-stu-id="01b9b-120">Disable rules</span></span>

<span data-ttu-id="01b9b-121">Het volgende voorbeeld wordt uitgeschakeld regels `910018` en `910017` op een toepassingsgateway:</span><span class="sxs-lookup"><span data-stu-id="01b9b-121">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="01b9b-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01b9b-122">Next steps</span></span>

<span data-ttu-id="01b9b-123">Nadat u uw uitgeschakelde regels hebt geconfigureerd, kunt u informatie over het weergeven van uw WAF Logboeken.</span><span class="sxs-lookup"><span data-stu-id="01b9b-123">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="01b9b-124">Zie voor meer informatie [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="01b9b-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
