---
title: aaaViews beheersystemen Operations Management Suite (OMS) | Microsoft Docs
description: 'Oplossingen voor het beheer in de Operations Management Suite (OMS) wordt gewoonlijk een of meer weergaven toovisualize gegevens bevatten.  In dit artikel wordt beschreven hoe tooexport een weergave gemaakt door Hallo Designer bekijken en deze opnemen in een oplossing. '
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 303861465014a27289f831332b3d95925c0ae66d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="d1171-104">Weergaven in de Operations Management Suite (OMS) oplossingen (Preview)</span><span class="sxs-lookup"><span data-stu-id="d1171-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="d1171-105">Dit is voorlopige documentatie voor het maken van oplossingen voor het beheer in OMS die zich momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="d1171-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="d1171-106">De hieronder beschreven schema is onderwerp toochange.</span><span class="sxs-lookup"><span data-stu-id="d1171-106">Any schema described below is subject toochange.</span></span>    
>
>

<span data-ttu-id="d1171-107">[Oplossingen voor het beheer in de Operations Management Suite (OMS)](operations-management-suite-solutions.md) doorgaans bevat een of meer weergaven toovisualize gegevens.</span><span class="sxs-lookup"><span data-stu-id="d1171-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views toovisualize data.</span></span>  <span data-ttu-id="d1171-108">Dit artikel wordt beschreven hoe tooexport een weergave gemaakt door Hallo [ontwerper](../log-analytics/log-analytics-view-designer.md) en deze opnemen in een oplossing.</span><span class="sxs-lookup"><span data-stu-id="d1171-108">This article describes how tooexport a view created by hello [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="d1171-109">Hallo voorbeelden in dit artikel gebruiken parameters en variabelen die zijn beide vereist of algemene toomanagement oplossingen en wordt beschreven in [beheeroplossingen maken in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="d1171-109">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="d1171-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d1171-110">Prerequisites</span></span>
<span data-ttu-id="d1171-111">In dit artikel wordt ervan uitgegaan dat u al bekend met het te bent[maken van een beheeroplossing](operations-management-suite-solutions-creating.md) en Hallo-structuur van een oplossingsbestand.</span><span class="sxs-lookup"><span data-stu-id="d1171-111">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="d1171-112">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d1171-112">Overview</span></span>
<span data-ttu-id="d1171-113">een weergave in een oplossing voor tooinclude, die u maakt een **resource** voor in Hallo [oplossingsbestand](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="d1171-113">tooinclude a view in a management solution, you create a **resource** for it in hello [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="d1171-114">Hallo JSON die de gedetailleerde configuratie van de weergave van de Hallo beschrijft is doorgaans complexe echter en niet iets dat de auteur van een standaardoplossing handmatig kunnen toocreate zou zijn.</span><span class="sxs-lookup"><span data-stu-id="d1171-114">hello JSON that describes hello view's detailed configuration is typically complex though and not something that a typical solution author would be able toocreate manually.</span></span>  <span data-ttu-id="d1171-115">Hallo wordt meestal toocreate Hallo weergeven met behulp van Hallo [ontwerper](../log-analytics/log-analytics-view-designer.md), exporteren en voeg vervolgens de gedetailleerde configuratie toohello oplossing.</span><span class="sxs-lookup"><span data-stu-id="d1171-115">hello most common method is toocreate hello view using hello [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration toohello solution.</span></span>

<span data-ttu-id="d1171-116">Hallo basisstappen tooadd een weergave tooa oplossing zijn als volgt.</span><span class="sxs-lookup"><span data-stu-id="d1171-116">hello basic steps tooadd a view tooa solution are as follows.</span></span>  <span data-ttu-id="d1171-117">Elke stap wordt beschreven in de volgende secties voor Hallo nader.</span><span class="sxs-lookup"><span data-stu-id="d1171-117">Each step is described in further detail in hello sections below.</span></span>

1. <span data-ttu-id="d1171-118">Hallo weergave tooa-bestand exporteren.</span><span class="sxs-lookup"><span data-stu-id="d1171-118">Export hello view tooa file.</span></span>
2. <span data-ttu-id="d1171-119">Hallo weergave resource maken in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="d1171-119">Create hello view resource in hello solution.</span></span>
3. <span data-ttu-id="d1171-120">Hallo weergavedetails toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d1171-120">Add hello view details.</span></span>

## <a name="export-hello-view-tooa-file"></a><span data-ttu-id="d1171-121">Hallo weergave tooa-bestand exporteren</span><span class="sxs-lookup"><span data-stu-id="d1171-121">Export hello view tooa file</span></span>
<span data-ttu-id="d1171-122">Volg de instructies Hallo voor [Log Analytics-ontwerper](../log-analytics/log-analytics-view-designer.md) tooexport een weergave tooa-bestand.</span><span class="sxs-lookup"><span data-stu-id="d1171-122">Follow hello instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) tooexport a view tooa file.</span></span>  <span data-ttu-id="d1171-123">Hallo geëxporteerde bestand zal worden in JSON-indeling met Hallo dezelfde [elementen als Hallo oplossingsbestand](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="d1171-123">hello exported file will be in JSON format with hello same [elements as hello solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="d1171-124">Hallo **resources** element van Hallo weergavebestand heeft een resource met een type **Microsoft.OperationalInsights/workspaces** dat vertegenwoordigt Hallo OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="d1171-124">hello **resources** element of hello view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents hello OMS workspace.</span></span>  <span data-ttu-id="d1171-125">Dit element heeft een subelement van het type **weergaven** die staat voor Hallo weergeven en de gedetailleerde configuratie bevat.</span><span class="sxs-lookup"><span data-stu-id="d1171-125">This element will have a subelement with a type of **views** that represents hello view and contains its detailed configuration.</span></span>  <span data-ttu-id="d1171-126">U Hallo details van dit element kopiëren en kopieert u deze naar uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="d1171-126">You will copy hello details of this element and then copy it into your solution.</span></span>

## <a name="create-hello-view-resource-in-hello-solution"></a><span data-ttu-id="d1171-127">Hallo weergave resource maken in Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="d1171-127">Create hello view resource in hello solution</span></span>
<span data-ttu-id="d1171-128">Hallo na weergave resource toohello toevoegen **resources** element van het oplossingsbestand van uw.</span><span class="sxs-lookup"><span data-stu-id="d1171-128">Add hello following view resource toohello **resources** element of your solution file.</span></span>  <span data-ttu-id="d1171-129">Dit maakt gebruik van variabelen die hieronder worden beschreven die u ook moet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d1171-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="d1171-130">Houd er rekening mee dat Hallo **Dashboard** en **OverviewTile** eigenschappen zijn tijdelijke aanduidingen die u met de bijbehorende eigenschappen Hallo uit Hallo geëxporteerde weergavebestand wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="d1171-130">Note that hello **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with hello corresponding properties from hello exported view file.</span></span>

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

<span data-ttu-id="d1171-131">Toevoegen van de volgende variabelen toohello variabelen element van het oplossingsbestand Hallo Hallo en vervang Hallo waarden toothose voor uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="d1171-131">Add hello following variables toohello variables element of hello solution file and replace hello values toothose for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of hello view."
    "ViewName": "Provide a name for hello view here."


<span data-ttu-id="d1171-132">Houd er rekening mee dat u Hallo gehele weergave resource vanuit het bestand met geëxporteerde weergave kopiëren kan, maar moet u toomake Hallo volgende wijzigingen voor het toowork in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="d1171-132">Note that you could copy hello entire view resource from your exported view file, but you would need toomake hello following changes for it toowork in your solution.</span></span>  

* <span data-ttu-id="d1171-133">Hallo **type** voor Hallo weergave resource moet toobe gewijzigd van **weergaven** te**Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="d1171-133">hello **type** for hello view resource needs toobe changed from **views** too**Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="d1171-134">Hallo **naam** voor Hallo weergave resource-eigenschap moet toobe gewijzigd tooinclude Hallo Werkruimtenaam.</span><span class="sxs-lookup"><span data-stu-id="d1171-134">hello **name** property for hello view resource needs toobe changed tooinclude hello workspace name.</span></span>
* <span data-ttu-id="d1171-135">Hallo-afhankelijkheid van Hallo werkruimte moet toobe sinds Hallo werkruimte resource is niet gedefinieerd in Hallo-oplossing verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d1171-135">hello dependency on hello workspace needs toobe removed since hello workspace resource isn't defined in hello solution.</span></span>
* <span data-ttu-id="d1171-136">**DisplayName** eigenschap behoeften toobe toohello weergave toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d1171-136">**DisplayName** property needs toobe added toohello view.</span></span>  <span data-ttu-id="d1171-137">Hallo **Id**, **naam**, en **DisplayName** moeten alle overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="d1171-137">hello **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="d1171-138">Namen van parameters moeten worden gewijzigd toomatch Hallo set parameters vereist.</span><span class="sxs-lookup"><span data-stu-id="d1171-138">Parameter names must be changed toomatch hello required set of parameters.</span></span>
* <span data-ttu-id="d1171-139">Variabelen moeten worden gedefinieerd in Hallo oplossing en gebruikt in de juiste Hallo-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="d1171-139">Variables should be defined in hello solution and used in hello appropriate properties.</span></span>

## <a name="add-hello-view-details"></a><span data-ttu-id="d1171-140">Hallo weergavedetails toevoegen</span><span class="sxs-lookup"><span data-stu-id="d1171-140">Add hello view details</span></span>
<span data-ttu-id="d1171-141">Hallo weergave bron in Hallo geëxporteerd weergave bestand bevat twee elementen in Hallo **eigenschappen** element met de naam **Dashboard** en **OverviewTile** die Hallo bevatten gedetailleerde configuratie van Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="d1171-141">hello view resource in hello exported view file will contain two elements in hello **properties** element named **Dashboard** and **OverviewTile** which contain hello detailed configuration of hello view.</span></span>  <span data-ttu-id="d1171-142">Deze twee elementen en hun inhoud kopiëren naar Hallo **eigenschappen** element van de resource van Hallo weergeven in uw oplossingsbestand.</span><span class="sxs-lookup"><span data-stu-id="d1171-142">Copy these two elements and their contents into hello **properties** element of hello view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="d1171-143">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d1171-143">Example</span></span>
<span data-ttu-id="d1171-144">Hallo volgende voorbeeld ziet u bijvoorbeeld een eenvoudige oplossing-bestand met een weergave.</span><span class="sxs-lookup"><span data-stu-id="d1171-144">For example, hello following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="d1171-145">Weglatingstekens (...) worden weergegeven voor Hallo **Dashboard** en **OverviewTile** inhoud omwille van de ruimte.</span><span class="sxs-lookup"><span data-stu-id="d1171-145">Ellipses (...) are shown for hello **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a><span data-ttu-id="d1171-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d1171-146">Next steps</span></span>
* <span data-ttu-id="d1171-147">Meer informatie over alle details van het maken van [beheeroplossingen](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="d1171-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="d1171-148">Omvatten [Automation-runbooks in uw beheeroplossing](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="d1171-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
