---
title: Uitgeven van sjablonen in Azure API Management | Microsoft Docs
description: Informatie over het aanpassen van de inhoud van het probleem pagina's in de ontwikkelaarsportal in Azure API Management.
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
ms.openlocfilehash: e13344df198bca4f73c75fa58221436b94e2f258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="1acc9-103">Probleem sjablonen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="1acc9-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="1acc9-104">Azure API Management biedt de mogelijkheid voor het aanpassen van de inhoud van developer portal-pagina's met behulp van een set van sjablonen die hun inhoud configureren.</span><span class="sxs-lookup"><span data-stu-id="1acc9-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="1acc9-105">Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en de editor van uw keuze, zoals [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), en een opgegeven set gelokaliseerde [resources String](api-management-template-resources.md#strings), [Glyph-resources](api-management-template-resources.md#glyphs), en [pagina besturingselementen](api-management-page-controls.md), hebt u aanzienlijke flexibiliteit voor het configureren van de inhoud van de pagina's naar wens met behulp van deze sjablonen.</span><span class="sxs-lookup"><span data-stu-id="1acc9-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="1acc9-106">De sjablonen in deze sectie kunnen u de inhoud van het probleem pagina's in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="1acc9-106">The templates in this section allow you to customize the content of the Issue pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="1acc9-107">Lijst met kwesties</span><span class="sxs-lookup"><span data-stu-id="1acc9-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="1acc9-108">Standaard-voorbeeldsjablonen zijn opgenomen in de volgende documentatie, maar nog worden gewijzigd vanwege continu verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="1acc9-108">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="1acc9-109">U kunt de live standaardsjablonen weergeven in de ontwikkelaarsportal door te navigeren naar de gewenste afzonderlijke sjablonen.</span><span class="sxs-lookup"><span data-stu-id="1acc9-109">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="1acc9-110">Zie voor meer informatie over het werken met sjablonen [het aanpassen van de API Management portal voor ontwikkelaars met behulp van sjablonen](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1acc9-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="1acc9-111"><a name="IssueList"></a>Lijst met kwesties</span><span class="sxs-lookup"><span data-stu-id="1acc9-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="1acc9-112">De **probleem lijst** sjabloon kunt u de hoofdtekst van de pagina van de lijst met probleem in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="1acc9-112">The **Issue list** template allows you to customize the body of the issue list page in the developer portal.</span></span>  
  
 <span data-ttu-id="1acc9-113">![Lijst Ontwikkelaarsportal uitgeven](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM probleem lijst Developer-Portal")</span><span class="sxs-lookup"><span data-stu-id="1acc9-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="1acc9-114">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="1acc9-114">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="1acc9-115">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="1acc9-115">Controls</span></span>  
 <span data-ttu-id="1acc9-116">De `Issue list` sjabloon mogelijk gebruikt u de volgende [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="1acc9-116">The `Issue list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="1acc9-117">besturingselement voor paginering</span><span class="sxs-lookup"><span data-stu-id="1acc9-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="1acc9-118">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="1acc9-118">Data model</span></span>  
  
|<span data-ttu-id="1acc9-119">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1acc9-119">Property</span></span>|<span data-ttu-id="1acc9-120">Type</span><span class="sxs-lookup"><span data-stu-id="1acc9-120">Type</span></span>|<span data-ttu-id="1acc9-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1acc9-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="1acc9-122">Problemen</span><span class="sxs-lookup"><span data-stu-id="1acc9-122">Issues</span></span>|<span data-ttu-id="1acc9-123">Verzameling van [probleem](api-management-template-data-model-reference.md#Issue) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="1acc9-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="1acc9-124">De problemen die zichtbaar is voor de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1acc9-124">The issues visible to the current user.</span></span>|  
|<span data-ttu-id="1acc9-125">Zoekresultaten oproepen</span><span class="sxs-lookup"><span data-stu-id="1acc9-125">Paging</span></span>|<span data-ttu-id="1acc9-126">[Wisselgeheugengebruik](api-management-template-data-model-reference.md#Paging) entiteit.</span><span class="sxs-lookup"><span data-stu-id="1acc9-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="1acc9-127">De paginerings-informatie voor de verzameling van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1acc9-127">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="1acc9-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="1acc9-128">IsAuthenticated</span></span>|<span data-ttu-id="1acc9-129">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="1acc9-129">boolean</span></span>|<span data-ttu-id="1acc9-130">Hiermee wordt aangegeven of de huidige gebruiker is aangemeld bij de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="1acc9-130">Whether the current user is signed-in to the developer portal.</span></span>|  
|<span data-ttu-id="1acc9-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="1acc9-131">CanReportIssues</span></span>|<span data-ttu-id="1acc9-132">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="1acc9-132">boolean</span></span>|<span data-ttu-id="1acc9-133">Hiermee wordt aangegeven of de huidige gebruiker machtigingen naar het bestand een probleem heeft.</span><span class="sxs-lookup"><span data-stu-id="1acc9-133">Whether the current user has permissions to file an issue.</span></span>|  
|<span data-ttu-id="1acc9-134">Search</span><span class="sxs-lookup"><span data-stu-id="1acc9-134">Search</span></span>|<span data-ttu-id="1acc9-135">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1acc9-135">string</span></span>|<span data-ttu-id="1acc9-136">Deze eigenschap is afgeschaft en mag niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1acc9-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="1acc9-137">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="1acc9-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how to connect my application to the API",  
            "Description": "I'm having trouble connecting my application to the backend API.",  
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

## <a name="next-steps"></a><span data-ttu-id="1acc9-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1acc9-138">Next steps</span></span>
<span data-ttu-id="1acc9-139">Zie voor meer informatie over het werken met sjablonen [het aanpassen van de API Management portal voor ontwikkelaars met behulp van sjablonen](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1acc9-139">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>