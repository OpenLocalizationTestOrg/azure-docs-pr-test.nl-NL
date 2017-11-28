---
title: aaaIssue sjablonen in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toocustomize Hallo inhoud Hallo probleem pagina's in de ontwikkelaarsportal Hallo in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: e12902e52c164f73902a97f15ea550790dfecf1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="5e1bb-103">Probleem sjablonen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="5e1bb-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="5e1bb-104">Azure API Management biedt dat u Hallo mogelijkheid toocustomize Hallo inhoud van developer portal-pagina's met behulp van een set van sjablonen die hun inhoud configureren.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="5e1bb-105">Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en het Hallo-editor naar keuze, zoals [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), en een opgegeven set gelokaliseerde [resources String](api-management-template-resources.md#strings), [ De glyph-resources](api-management-template-resources.md#glyphs), en [pagina besturingselementen](api-management-page-controls.md), hebt u aanzienlijke flexibiliteit tooconfigure Hallo inhoud van het Hallo-pagina's naar wens met behulp van deze sjablonen.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="5e1bb-106">Hallo-sjablonen in deze sectie kunt u toocustomize Hallo inhoud van Hallo probleem's in het Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-106">hello templates in this section allow you toocustomize hello content of hello Issue pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="5e1bb-107">Lijst met kwesties</span><span class="sxs-lookup"><span data-stu-id="5e1bb-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="5e1bb-108">Standaard-voorbeeldsjablonen zijn opgenomen in de volgende documentatie Hallo, maar onderwerp toochange vanwege toocontinuous verbeteringen zijn.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-108">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="5e1bb-109">U kunt Hallo live standaardsjablonen in Hallo developer-portal door te navigeren toohello gewenst afzonderlijke sjablonen weergeven.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-109">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="5e1bb-110">Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5e1bb-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="5e1bb-111"><a name="IssueList"></a>Lijst met kwesties</span><span class="sxs-lookup"><span data-stu-id="5e1bb-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="5e1bb-112">Hallo **probleem lijst** sjabloon kunt u toocustomize Hallo hoofdtekst van Hallo probleem lijstpagina in het Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-112">hello **Issue list** template allows you toocustomize hello body of hello issue list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5e1bb-113">![Lijst Ontwikkelaarsportal uitgeven](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM probleem lijst Developer-Portal")</span><span class="sxs-lookup"><span data-stu-id="5e1bb-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5e1bb-114">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="5e1bb-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="5e1bb-115">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="5e1bb-115">Controls</span></span>  
 <span data-ttu-id="5e1bb-116">Hallo `Issue list` sjabloon mogelijk gebruikt u de volgende Hallo [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5e1bb-116">hello `Issue list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5e1bb-117">besturingselement voor paginering</span><span class="sxs-lookup"><span data-stu-id="5e1bb-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="5e1bb-118">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="5e1bb-118">Data model</span></span>  
  
|<span data-ttu-id="5e1bb-119">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="5e1bb-119">Property</span></span>|<span data-ttu-id="5e1bb-120">Type</span><span class="sxs-lookup"><span data-stu-id="5e1bb-120">Type</span></span>|<span data-ttu-id="5e1bb-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5e1bb-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5e1bb-122">Problemen</span><span class="sxs-lookup"><span data-stu-id="5e1bb-122">Issues</span></span>|<span data-ttu-id="5e1bb-123">Verzameling van [probleem](api-management-template-data-model-reference.md#Issue) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="5e1bb-124">Hallo problemen zichtbaar toohello huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-124">hello issues visible toohello current user.</span></span>|  
|<span data-ttu-id="5e1bb-125">Zoekresultaten oproepen</span><span class="sxs-lookup"><span data-stu-id="5e1bb-125">Paging</span></span>|<span data-ttu-id="5e1bb-126">[Wisselgeheugengebruik](api-management-template-data-model-reference.md#Paging) entiteit.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="5e1bb-127">Hallo paginering informatie voor de verzameling van Hallo-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-127">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="5e1bb-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="5e1bb-128">IsAuthenticated</span></span>|<span data-ttu-id="5e1bb-129">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="5e1bb-129">boolean</span></span>|<span data-ttu-id="5e1bb-130">Hallo-huidige gebruiker wordt aangegeven of aangemelde toohello developer-portal.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-130">Whether hello current user is signed-in toohello developer portal.</span></span>|  
|<span data-ttu-id="5e1bb-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="5e1bb-131">CanReportIssues</span></span>|<span data-ttu-id="5e1bb-132">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="5e1bb-132">boolean</span></span>|<span data-ttu-id="5e1bb-133">Hiermee wordt aangegeven of de huidige gebruiker Hallo machtigingen toofile er een probleem is.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-133">Whether hello current user has permissions toofile an issue.</span></span>|  
|<span data-ttu-id="5e1bb-134">Search</span><span class="sxs-lookup"><span data-stu-id="5e1bb-134">Search</span></span>|<span data-ttu-id="5e1bb-135">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5e1bb-135">string</span></span>|<span data-ttu-id="5e1bb-136">Deze eigenschap is afgeschaft en mag niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5e1bb-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5e1bb-137">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="5e1bb-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how tooconnect my application toohello API",  
            "Description": "I'm having trouble connecting my application toohello backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="5e1bb-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e1bb-138">Next steps</span></span>
<span data-ttu-id="5e1bb-139">Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5e1bb-139">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
