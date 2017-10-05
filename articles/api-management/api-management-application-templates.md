---
title: Sjablonen voor toepassingen in Azure API Management | Microsoft Docs
description: Informatie over het aanpassen van de inhoud van de toepassing pagina's in de ontwikkelaarsportal in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: f3122c4d-e10e-4cdf-977b-36e8f4133fc8
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 6d2d44465800219f16866a621d4822614ac9e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="4afa2-103">Sjablonen voor toepassingen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="4afa2-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="4afa2-104">Azure API Management biedt de mogelijkheid voor het aanpassen van de inhoud van developer portal-pagina's met behulp van een set van sjablonen die hun inhoud configureren.</span><span class="sxs-lookup"><span data-stu-id="4afa2-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="4afa2-105">Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en de editor van uw keuze, zoals [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), en een opgegeven set gelokaliseerde [resources String](api-management-template-resources.md#strings), [Glyph-resources](api-management-template-resources.md#glyphs), en [pagina besturingselementen](api-management-page-controls.md), hebt u aanzienlijke flexibiliteit voor het configureren van de inhoud van de pagina's naar wens met behulp van deze sjablonen.</span><span class="sxs-lookup"><span data-stu-id="4afa2-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="4afa2-106">De sjablonen in deze sectie kunt u de inhoud van de toepassing pagina's in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="4afa2-106">The templates in this section allow you to customize the content of the Application pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="4afa2-107">Lijst met toepassingen</span><span class="sxs-lookup"><span data-stu-id="4afa2-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="4afa2-108">Toepassing</span><span class="sxs-lookup"><span data-stu-id="4afa2-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="4afa2-109">Standaard-voorbeeldsjablonen zijn opgenomen in de volgende documentatie, maar nog worden gewijzigd vanwege continu verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="4afa2-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="4afa2-110">U kunt de live standaardsjablonen weergeven in de ontwikkelaarsportal door te navigeren naar de gewenste afzonderlijke sjablonen.</span><span class="sxs-lookup"><span data-stu-id="4afa2-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="4afa2-111">Zie voor meer informatie over het werken met sjablonen [het aanpassen van de API Management portal voor ontwikkelaars met behulp van sjablonen](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="4afa2-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="4afa2-112"><a name="ProductList"></a>Lijst met toepassingen</span><span class="sxs-lookup"><span data-stu-id="4afa2-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="4afa2-113">De **toepassingslijst** sjabloon kunt u de hoofdtekst van de pagina van de lijst met toepassingen in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="4afa2-113">The **Application list** template allows you to customize the body of the application list page in the developer portal.</span></span>  
  
 <span data-ttu-id="4afa2-114">![Lijst met pagina Developer Portal Toepassingssjablonen](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM lijst pagina Developer Portal Toepassingssjablonen")</span><span class="sxs-lookup"><span data-stu-id="4afa2-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="4afa2-115">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="4afa2-115">Default template</span></span>  
  
```xml  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "AppStrings|WebApplicationsHeader" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if applications.size > 0 %}  
        <ul class="list-unstyled">  
        {% for app in applications %}  
            <li>  
            {% if app.application.icon.url != "" %}  
                <aside>  
                    <a href="/applications/details/{{app.application.id}}"><img src="{{app.application.icon.url}}" alt="App Icon" /></a>  
                </aside>  
            {% endif %}  
                <h3><a href="/applications/details/{{app.application.id}}">{{app.application.title}}</a></h3>  
                {{app.application.description}}  
            </li>     
        {% endfor %}  
        </ul>  
        <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="4afa2-116">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="4afa2-116">Controls</span></span>  
 <span data-ttu-id="4afa2-117">De `Product list` sjabloon mogelijk gebruikt u de volgende [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="4afa2-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="4afa2-118">besturingselement voor paginering</span><span class="sxs-lookup"><span data-stu-id="4afa2-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="4afa2-119">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="4afa2-119">Data model</span></span>  
  
|<span data-ttu-id="4afa2-120">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4afa2-120">Property</span></span>|<span data-ttu-id="4afa2-121">Type</span><span class="sxs-lookup"><span data-stu-id="4afa2-121">Type</span></span>|<span data-ttu-id="4afa2-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4afa2-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="4afa2-123">Zoekresultaten oproepen</span><span class="sxs-lookup"><span data-stu-id="4afa2-123">Paging</span></span>|<span data-ttu-id="4afa2-124">[Wisselgeheugengebruik](api-management-template-data-model-reference.md#Paging) entiteit.</span><span class="sxs-lookup"><span data-stu-id="4afa2-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="4afa2-125">De paginerings-informatie voor de verzameling van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="4afa2-125">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="4afa2-126">Toepassingen</span><span class="sxs-lookup"><span data-stu-id="4afa2-126">Applications</span></span>|<span data-ttu-id="4afa2-127">Verzameling van [toepassing](api-management-template-data-model-reference.md#Application) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="4afa2-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="4afa2-128">De toepassingen die zichtbaar is voor de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4afa2-128">The applications visible to the current user.</span></span>|  
|<span data-ttu-id="4afa2-129">Categorienaam</span><span class="sxs-lookup"><span data-stu-id="4afa2-129">CategoryName</span></span>|<span data-ttu-id="4afa2-130">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4afa2-130">string</span></span>|<span data-ttu-id="4afa2-131">De categorie van toepassing.</span><span class="sxs-lookup"><span data-stu-id="4afa2-131">The category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="4afa2-132">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="4afa2-132">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Applications": [  
        {  
            "Application": {  
                "Id": "5702b96fb16653124c8f9ba8",  
                "Title": "Contoso Calculator",  
                "Description": "A simple online calculator.",  
                "Url": null,  
                "Version": null,  
                "Requirements": "Free application with no requirements.",  
                "State": 2,  
                "RegistrationDate": "2016-04-04T18:59:00",  
                "CategoryId": 5,  
                "DeveloperId": "5702b5b0b16653124c8f9ba4",  
                "Attachments": [  
                    {  
                        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                        "Type": "Icon",  
                        "ContentType": "image/png"  
                    },  
                    {  
                        "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
                        "Type": "Screenshot",  
                        "ContentType": "image/png"  
                    }  
                ],  
                "Icon": {  
                    "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                    "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                    "Type": "Icon",  
                    "ContentType": "image/png"  
                }  
            },  
            "CategoryName": "Finance"  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="4afa2-133"><a name="Application"></a>Toepassing</span><span class="sxs-lookup"><span data-stu-id="4afa2-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="4afa2-134">De **toepassing** sjabloon kunt u de hoofdtekst van de toepassingspagina in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="4afa2-134">The **Application** template allows you to customize the body of the application page in the developer portal.</span></span>  
  
 <span data-ttu-id="4afa2-135">![Pagina Developer Portal Toepassingssjablonen](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM pagina Developer Portal Toepassingssjablonen")</span><span class="sxs-lookup"><span data-stu-id="4afa2-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="4afa2-136">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="4afa2-136">Default template</span></span>  
  
```xml  
<h2>{{title}}</h2>  
{% if icon.url != "" %}  
<aside class="applications_aside">  
  <div class="image-placeholder">  
    <img src="{{icon.url}}" alt="Application Icon" />  
  </div>  
</aside>  
{% endif %}  
  
<article>  
  {% if url != "" %}  
    <a target="_blank" href="{{url}}">{{url}}</a>  
  {% endif %}  
  
  <p>{{description}}</p>  
  
  {% if requirements != null %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsRequirementsHeader" %}</h3>  
  <p>{{requirements}}</p>  
  {% endif %}  
  
  {% if attachments.size > 0 %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsScreenshotsHeader" %}</h3>  
    {% for screenshot in attachments %}  
      {% if screenshot.type != "Icon" %}  
      <a href="{{screenshot.url}}" data-lightbox="example-set">  
          <img src="/Developer/Applications/Thumbnail?url={{screenshot.url}}" alt='{% localized "AppDetailsStrings|WebApplicationsScreenshotAlt" %}' />  
      </a>  
      {% endif %}  
    {% endfor %}  
  {% endif %}  
</article>  
  
```  
  
### <a name="controls"></a><span data-ttu-id="4afa2-137">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="4afa2-137">Controls</span></span>  
 <span data-ttu-id="4afa2-138">De `Application` sjabloon staat niet toe dat het gebruik van een [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="4afa2-138">The `Application` template does not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="4afa2-139">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="4afa2-139">Data model</span></span>  
 <span data-ttu-id="4afa2-140">[Toepassing](api-management-template-data-model-reference.md#Application) entiteit.</span><span class="sxs-lookup"><span data-stu-id="4afa2-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="4afa2-141">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="4afa2-141">Sample template data</span></span>  
  
```json  
{  
    "Id": "5702b96fb16653124c8f9ba8",  
    "Title": "Contoso Calculator",  
    "Description": "A simple online calculator.",  
    "Url": null,  
    "Version": null,  
    "Requirements": "Free application with no requirements.",  
    "State": 2,  
    "RegistrationDate": "2016-04-04T18:59:00",  
    "CategoryId": 5,  
    "DeveloperId": "5702b5b0b16653124c8f9ba4",  
    "Attachments": [  
        {  
            "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
            "Type": "Icon",  
            "ContentType": "image/png"  
        },  
        {  
            "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
            "Type": "Screenshot",  
            "ContentType": "image/png"  
        }  
    ],  
    "Icon": {  
        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
        "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
        "Type": "Icon",  
        "ContentType": "image/png"  
    }  
}  
```

## <a name="next-steps"></a><span data-ttu-id="4afa2-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4afa2-142">Next steps</span></span>
<span data-ttu-id="4afa2-143">Zie voor meer informatie over het werken met sjablonen [het aanpassen van de API Management portal voor ontwikkelaars met behulp van sjablonen](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4afa2-143">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>