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
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="0d7c2-103">Web application firewall-regels via hello Azure-portal aanpassen</span><span class="sxs-lookup"><span data-stu-id="0d7c2-103">Customize web application firewall rules through hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d7c2-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0d7c2-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="0d7c2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d7c2-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="0d7c2-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0d7c2-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="0d7c2-107">Hello Azure Application Gateway web application firewall (WAF) biedt beveiliging voor webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="0d7c2-108">Deze beveiligingen worden geleverd door Hallo Open Web Application Security Project (OWASP) Core regel ingesteld (CRS).</span><span class="sxs-lookup"><span data-stu-id="0d7c2-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="0d7c2-109">Sommige regels kunnen valse positieven veroorzaken en echte verkeer blokkeert.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="0d7c2-110">Daarom biedt Application Gateway Hallo mogelijkheid toocustomize regelgroepen en regels.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="0d7c2-111">Zie voor meer informatie over de specifieke regelgroepen Hallo en regels [lijst van groepen met web application firewall CRS regels en voorschriften](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="0d7c2-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="0d7c2-112">Als uw toepassingsgateway Hallo WAF laag niet gebruikt, wordt in het rechterdeelvenster Hallo Hallo optie tooupgrade Hallo gateway toohello WAF toepassingslaag weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-112">If your application gateway is not using hello WAF tier, hello option tooupgrade hello application gateway toohello WAF tier appears in hello right pane.</span></span> 

![WAF inschakelen][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="0d7c2-114">Groepen van de regel weergeven en regels</span><span class="sxs-lookup"><span data-stu-id="0d7c2-114">View rule groups and rules</span></span>

<span data-ttu-id="0d7c2-115">**tooview regelgroepen en regels**</span><span class="sxs-lookup"><span data-stu-id="0d7c2-115">**tooview rule groups and rules**</span></span>
   1. <span data-ttu-id="0d7c2-116">Toepassingsgateway toohello bladeren en selecteer vervolgens **Web application firewall**.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-116">Browse toohello application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="0d7c2-117">Selecteer **geavanceerde regelconfiguratie**.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="0d7c2-118">Deze weergave bevat een tabel op de pagina Hallo van alle Hallo regelgroepen Hallo gekozen regelset voorzien.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-118">This view shows a table on hello page of all hello rule groups provided with hello chosen rule set.</span></span> <span data-ttu-id="0d7c2-119">Alle selectievakjes van Hallo regel zijn geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-119">All of hello rule's check boxes are selected.</span></span>

![Uitgeschakelde regels configureren][1]

## <a name="search-for-rules-toodisable"></a><span data-ttu-id="0d7c2-121">Zoeken naar regels toodisable</span><span class="sxs-lookup"><span data-stu-id="0d7c2-121">Search for rules toodisable</span></span>

<span data-ttu-id="0d7c2-122">Hallo **Web application firewall-instellingen** blade biedt de mogelijkheid van Hallo toofilter Hallo regels via een tekst te zoeken.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-122">hello **Web application firewall settings** blade provides hello capability toofilter hello rules through a text search.</span></span> <span data-ttu-id="0d7c2-123">Hallo resultaat geeft alleen Hallo regelgroepen en regels die u zoekt Hallo-tekst bevatten.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-123">hello result displays only hello rule groups and rules that contain hello text you searched for.</span></span>

![Zoeken naar regels][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="0d7c2-125">Regelgroepen en regels uitschakelen</span><span class="sxs-lookup"><span data-stu-id="0d7c2-125">Disable rule groups and rules</span></span>

<span data-ttu-id="0d7c2-126">Wanneer uw bent regels is uitgeschakeld, kunt u een volledige regelgroep of uitschakelen specifieke regels onder een of meer regelgroepen.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="0d7c2-127">**toodisable regelgroepen of specifieke regels**</span><span class="sxs-lookup"><span data-stu-id="0d7c2-127">**toodisable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="0d7c2-128">Zoeken naar Hallo regels of groepen met regels die u toodisable wilt.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-128">Search for hello rules or rule groups that you want toodisable.</span></span>
   2. <span data-ttu-id="0d7c2-129">Schakel de selectievakjes Hallo voor Hallo regels die u toodisable wilt.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-129">Clear hello check boxes for hello rules that you want toodisable.</span></span> 
   2. <span data-ttu-id="0d7c2-130">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-130">Select **Save**.</span></span> 

![Wijzigingen opslaan][3]

## <a name="next-steps"></a><span data-ttu-id="0d7c2-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0d7c2-132">Next steps</span></span>

<span data-ttu-id="0d7c2-133">Nadat u uw uitgeschakelde regels hebt geconfigureerd, leert u hoe tooview uw WAF-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="0d7c2-133">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="0d7c2-134">Zie voor meer informatie [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="0d7c2-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
