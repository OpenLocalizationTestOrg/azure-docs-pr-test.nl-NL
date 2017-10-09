---
title: web application firewall-regels in Azure Application Gateway - Azure-portal aaaCustomize | Microsoft Docs
description: In dit artikel bevat informatie over hoe toocustomize web application firewall regels Application Gateway met hello Azure-portal.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a>Web application firewall-regels via hello Azure-portal aanpassen

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

Hello Azure Application Gateway web application firewall (WAF) biedt beveiliging voor webtoepassingen. Deze beveiligingen worden geleverd door Hallo Open Web Application Security Project (OWASP) Core regel ingesteld (CRS). Sommige regels kunnen valse positieven veroorzaken en echte verkeer blokkeert. Daarom biedt Application Gateway Hallo mogelijkheid toocustomize regelgroepen en regels. Zie voor meer informatie over de specifieke regelgroepen Hallo en regels [lijst van groepen met web application firewall CRS regels en voorschriften](application-gateway-crs-rulegroups-rules.md).

>[!NOTE]
> Als uw toepassingsgateway Hallo WAF laag niet gebruikt, wordt in het rechterdeelvenster Hallo Hallo optie tooupgrade Hallo gateway toohello WAF toepassingslaag weergegeven. 

![WAF inschakelen][fig1]

## <a name="view-rule-groups-and-rules"></a>Groepen van de regel weergeven en regels

**tooview regelgroepen en regels**
   1. Toepassingsgateway toohello bladeren en selecteer vervolgens **Web application firewall**.  
   2. Selecteer **geavanceerde regelconfiguratie**.  
   Deze weergave bevat een tabel op de pagina Hallo van alle Hallo regelgroepen Hallo gekozen regelset voorzien. Alle selectievakjes van Hallo regel zijn geselecteerd.

![Uitgeschakelde regels configureren][1]

## <a name="search-for-rules-toodisable"></a>Zoeken naar regels toodisable

Hallo **Web application firewall-instellingen** blade biedt de mogelijkheid van Hallo toofilter Hallo regels via een tekst te zoeken. Hallo resultaat geeft alleen Hallo regelgroepen en regels die u zoekt Hallo-tekst bevatten.

![Zoeken naar regels][2]

## <a name="disable-rule-groups-and-rules"></a>Regelgroepen en regels uitschakelen

Wanneer uw bent regels is uitgeschakeld, kunt u een volledige regelgroep of uitschakelen specifieke regels onder een of meer regelgroepen. 

**toodisable regelgroepen of specifieke regels**

   1. Zoeken naar Hallo regels of groepen met regels die u toodisable wilt.
   2. Schakel de selectievakjes Hallo voor Hallo regels die u toodisable wilt. 
   2. Selecteer **Opslaan**. 

![Wijzigingen opslaan][3]

## <a name="next-steps"></a>Volgende stappen

Nadat u uw uitgeschakelde regels hebt geconfigureerd, leert u hoe tooview uw WAF-Logboeken. Zie voor meer informatie [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
