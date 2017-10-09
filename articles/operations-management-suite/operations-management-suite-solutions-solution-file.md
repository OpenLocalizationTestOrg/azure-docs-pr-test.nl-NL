---
title: oplossingen voor aaaCreating in Operations Management Suite (OMS) | Microsoft Docs
description: Beheeroplossingen Hallo functionaliteit van Operations Management Suite (OMS) uitbreiden door verpakte beheerscenario dat klanten tootheir OMS-werkruimte kunnen toevoegen.  Dit artikel bevat informatie over hoe u management oplossingen toobe kunt maken in uw eigen omgeving gebruikt of beschikbaar tooyour klanten worden gemaakt.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="51d51-104">Maken van een bestand van de oplossing voor beheer in Operations Management Suite (OMS) (Preview)</span><span class="sxs-lookup"><span data-stu-id="51d51-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="51d51-105">Dit is voorlopige documentatie voor het maken van oplossingen voor het beheer in OMS die zich momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="51d51-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="51d51-106">De hieronder beschreven schema is onderwerp toochange.</span><span class="sxs-lookup"><span data-stu-id="51d51-106">Any schema described below is subject toochange.</span></span>  

<span data-ttu-id="51d51-107">Oplossingen voor het beheer in de Operations Management Suite (OMS) worden geïmplementeerd als [Resource Manager-sjablonen](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="51d51-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="51d51-108">de belangrijkste taak Hallo weten hoe tooauthor beheeroplossingen hoe te leren[ontwerpen van een sjabloon](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="51d51-108">hello main task in learning how tooauthor management solutions is learning how too[author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="51d51-109">Dit artikel vindt u unieke gegevens van sjablonen die worden gebruikt voor oplossingen en hoe tooconfigure standaardoplossing resources.</span><span class="sxs-lookup"><span data-stu-id="51d51-109">This article provides unique details of templates used for solutions and how tooconfigure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="51d51-110">Hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="51d51-110">Tools</span></span>

<span data-ttu-id="51d51-111">U kunt tekst editor toowork oplossingsbestanden, maar we raden gebruik Hallo-functies die in Visual Studio of Visual Studio Code, zoals beschreven in de volgende artikelen Hallo.</span><span class="sxs-lookup"><span data-stu-id="51d51-111">You can use any text editor toowork with solution files, but we recommend leveraging hello features provided in Visual Studio or Visual Studio Code as described in hello following articles.</span></span>

- [<span data-ttu-id="51d51-112">Maken en implementeren van Azure-resourcegroepen met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="51d51-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="51d51-113">Werken met Azure Resource Manager-sjablonen in Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="51d51-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="51d51-114">structuur</span><span class="sxs-lookup"><span data-stu-id="51d51-114">Structure</span></span>
<span data-ttu-id="51d51-115">Hallo basisstructuur van een management-oplossing-bestand is Hallo dezelfde zijn als een [Resource Manager-sjabloon](../azure-resource-manager/resource-group-authoring-templates.md#template-format) die is als volgt.</span><span class="sxs-lookup"><span data-stu-id="51d51-115">hello basic structure of a management solution file is hello same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="51d51-116">Elk van de volgende secties voor Hallo Hallo hoogste niveau elementen beschrijft en en de inhoud in een oplossing.</span><span class="sxs-lookup"><span data-stu-id="51d51-116">Each of hello sections below describes hello top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="51d51-117">Parameters</span><span class="sxs-lookup"><span data-stu-id="51d51-117">Parameters</span></span>
<span data-ttu-id="51d51-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) zijn waarden die u nodig van de gebruiker Hallo hebt wanneer ze Hallo-beheeroplossing installeren.</span><span class="sxs-lookup"><span data-stu-id="51d51-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from hello user when they install hello management solution.</span></span>  <span data-ttu-id="51d51-119">Er zijn standaard parameters die alle oplossingen hebben en u kunt zo nodig extra parameters toevoegen voor uw specifieke oplossing.</span><span class="sxs-lookup"><span data-stu-id="51d51-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="51d51-120">Hoe gebruikers parameterwaarden wordt opgeven bij de installatie van uw oplossing afhankelijk van bepaalde Hallo-parameter en hoe de oplossing hello wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="51d51-120">How users will provide parameter values when they install your solution will depend on hello particular parameter and how hello solution is being installed.</span></span>

<span data-ttu-id="51d51-121">Wanneer een gebruiker uw beheeroplossing voor via Hallo installeert [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) of [Azure-snelstartsjablonen](operations-management-suite-solutions.md#finding-and-installing-management-solutions) ze na vragen aan gebruiker tooselect zijn een [OMS werkruimte en de Automation-account ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="51d51-121">When a user installs your management solution through hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted tooselect an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="51d51-122">Dit zijn gebruikte toopopulate Hallo waarden van elk van de standaardparameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="51d51-122">These are used toopopulate hello values of each of hello standard parameters.</span></span>  <span data-ttu-id="51d51-123">Hallo-gebruiker niet gevraagd toodirectly waarden opgeven voor de standaardparameters hello, maar ze na vragen aan gebruiker tooprovide waarden voor eventuele extra parameters zijn.</span><span class="sxs-lookup"><span data-stu-id="51d51-123">hello user is not prompted toodirectly provide values for hello standard parameters, but they are prompted tooprovide values for any additional parameters.</span></span>

<span data-ttu-id="51d51-124">Wanneer Hallo gebruiker installeert voor uw oplossing [een andere methode](operations-management-suite-solutions.md#finding-and-installing-management-solutions), moeten deze een waarde opgeven voor alle standaardparameters en alle extra parameters.</span><span class="sxs-lookup"><span data-stu-id="51d51-124">When hello user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="51d51-125">Een voorbeeld-parameter worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="51d51-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="51d51-126">Hallo volgende tabel beschrijft Hallo kenmerken van een parameter.</span><span class="sxs-lookup"><span data-stu-id="51d51-126">hello following table describes hello attributes of a parameter.</span></span>

| <span data-ttu-id="51d51-127">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="51d51-127">Attribute</span></span> | <span data-ttu-id="51d51-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="51d51-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="51d51-129">type</span><span class="sxs-lookup"><span data-stu-id="51d51-129">type</span></span> |<span data-ttu-id="51d51-130">Het gegevenstype voor Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="51d51-130">Data type for hello parameter.</span></span> <span data-ttu-id="51d51-131">Hallo invoer besturingselement weergegeven voor gebruiker hello, is afhankelijk van Hallo-gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="51d51-131">hello input control displayed for hello user depends on hello data type.</span></span><br><br><span data-ttu-id="51d51-132">Boole - vervolgkeuzelijst</span><span class="sxs-lookup"><span data-stu-id="51d51-132">bool - Drop down box</span></span><br><span data-ttu-id="51d51-133">String - tekstvak</span><span class="sxs-lookup"><span data-stu-id="51d51-133">string - Text box</span></span><br><span data-ttu-id="51d51-134">int - tekstvak</span><span class="sxs-lookup"><span data-stu-id="51d51-134">int - Text box</span></span><br><span data-ttu-id="51d51-135">SecureString - wachtwoordveld</span><span class="sxs-lookup"><span data-stu-id="51d51-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="51d51-136">category</span><span class="sxs-lookup"><span data-stu-id="51d51-136">category</span></span> |<span data-ttu-id="51d51-137">Optionele categorie voor Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="51d51-137">Optional category for hello parameter.</span></span>  <span data-ttu-id="51d51-138">De parameters in dezelfde categorie zijn gegroepeerd Hallo.</span><span class="sxs-lookup"><span data-stu-id="51d51-138">Parameters in hello same category are grouped together.</span></span> |
| <span data-ttu-id="51d51-139">Besturingselement</span><span class="sxs-lookup"><span data-stu-id="51d51-139">control</span></span> |<span data-ttu-id="51d51-140">Aanvullende functionaliteit voor string-parameters.</span><span class="sxs-lookup"><span data-stu-id="51d51-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="51d51-141">datum/tijd - datum/tijd-besturingselement wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="51d51-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="51d51-142">GUID - Guid-waarde wordt automatisch gegenereerd en Hallo-parameter niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="51d51-142">guid - Guid value is automatically generated, and hello parameter is not displayed.</span></span> |
| <span data-ttu-id="51d51-143">description</span><span class="sxs-lookup"><span data-stu-id="51d51-143">description</span></span> |<span data-ttu-id="51d51-144">Optionele beschrijving voor het Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="51d51-144">Optional description for hello parameter.</span></span>  <span data-ttu-id="51d51-145">In een volgende toohello-parameter van informatie ballon weergegeven.</span><span class="sxs-lookup"><span data-stu-id="51d51-145">Displayed in an information balloon next toohello parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="51d51-146">Standaard-parameters</span><span class="sxs-lookup"><span data-stu-id="51d51-146">Standard parameters</span></span>
<span data-ttu-id="51d51-147">Hallo bevat volgende tabel de standaardparameters Hallo voor alle beheeroplossingen voor.</span><span class="sxs-lookup"><span data-stu-id="51d51-147">hello following table lists hello standard parameters for all management solutions.</span></span>  <span data-ttu-id="51d51-148">Deze waarden worden ingevuld voor Hallo-gebruiker in plaats van het betreffende bevestigingsvenster wanneer uw oplossing wordt geïnstalleerd vanuit hello Azure Marketplace of Quick Start-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="51d51-148">These values are populated for hello user instead of prompting for them when your solution is installed from hello Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="51d51-149">Hallo-gebruiker moet waarden opgeven voor deze als Hallo-oplossing is geïnstalleerd met een andere methode.</span><span class="sxs-lookup"><span data-stu-id="51d51-149">hello user must provide values for them if hello solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="51d51-150">Hallo-gebruikersinterface in hello Azure Marketplace en Quick Start-sjablonen verwacht in de tabel Hallo Hallo parameternamen.</span><span class="sxs-lookup"><span data-stu-id="51d51-150">hello user interface in hello Azure Marketplace and Quickstart templates is expecting hello parameter names in hello table.</span></span>  <span data-ttu-id="51d51-151">Als u verschillende parameternamen vervolgens Hallo gebruiker wordt gevraagd om deze en ze niet automatisch ingevuld.</span><span class="sxs-lookup"><span data-stu-id="51d51-151">If you use different parameter names then hello user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="51d51-152">Parameter</span><span class="sxs-lookup"><span data-stu-id="51d51-152">Parameter</span></span> | <span data-ttu-id="51d51-153">Type</span><span class="sxs-lookup"><span data-stu-id="51d51-153">Type</span></span> | <span data-ttu-id="51d51-154">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="51d51-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="51d51-155">Accountnaam</span><span class="sxs-lookup"><span data-stu-id="51d51-155">accountName</span></span> |<span data-ttu-id="51d51-156">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="51d51-156">string</span></span> |<span data-ttu-id="51d51-157">Azure Automation-accountnaam.</span><span class="sxs-lookup"><span data-stu-id="51d51-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="51d51-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="51d51-158">pricingTier</span></span> |<span data-ttu-id="51d51-159">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="51d51-159">string</span></span> |<span data-ttu-id="51d51-160">De prijscategorie van de werkruimte voor logboekanalyse zowel Azure Automation-account.</span><span class="sxs-lookup"><span data-stu-id="51d51-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="51d51-161">regionId</span><span class="sxs-lookup"><span data-stu-id="51d51-161">regionId</span></span> |<span data-ttu-id="51d51-162">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="51d51-162">string</span></span> |<span data-ttu-id="51d51-163">De regio van hello Azure Automation-account.</span><span class="sxs-lookup"><span data-stu-id="51d51-163">Region of hello Azure Automation account.</span></span> |
| <span data-ttu-id="51d51-164">SolutionName</span><span class="sxs-lookup"><span data-stu-id="51d51-164">solutionName</span></span> |<span data-ttu-id="51d51-165">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="51d51-165">string</span></span> |<span data-ttu-id="51d51-166">Naam van het Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="51d51-166">Name of hello solution.</span></span>  <span data-ttu-id="51d51-167">Als u uw oplossing via snelstartsjablonen implementeert, moet vervolgens u definiëren solutionName als een parameter zodat u kunt een tekenreeks in plaats daarvan vereisen Hallo gebruiker toospecify een definiëren.</span><span class="sxs-lookup"><span data-stu-id="51d51-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring hello user toospecify one.</span></span> |
| <span data-ttu-id="51d51-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="51d51-168">workspaceName</span></span> |<span data-ttu-id="51d51-169">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="51d51-169">string</span></span> |<span data-ttu-id="51d51-170">Meld u aan de naam van de werkruimte Analytics.</span><span class="sxs-lookup"><span data-stu-id="51d51-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="51d51-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="51d51-171">workspaceRegionId</span></span> |<span data-ttu-id="51d51-172">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="51d51-172">string</span></span> |<span data-ttu-id="51d51-173">De regio van de werkruimte voor logboekanalyse Hallo.</span><span class="sxs-lookup"><span data-stu-id="51d51-173">Region of hello Log Analytics workspace.</span></span> |


<span data-ttu-id="51d51-174">Hieronder volgt Hallo structuur Hallo standaard parameters die u kunt kopiëren en plakken in uw oplossingsbestand.</span><span class="sxs-lookup"><span data-stu-id="51d51-174">Following is hello structure of hello standard parameters that you can copy and paste into your solution file.</span></span>  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="51d51-175">Raadpleeg van tooparameter waarden in andere elementen van de oplossing Hallo met Hallo syntaxis **parameters (parameter name)**.</span><span class="sxs-lookup"><span data-stu-id="51d51-175">You refer tooparameter values in other elements of hello solution with hello syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="51d51-176">Bijvoorbeeld: tooaccess Hallo Werkruimtenaam, gebruikt u **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="51d51-176">For example, tooaccess hello workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="51d51-177">Variabelen</span><span class="sxs-lookup"><span data-stu-id="51d51-177">Variables</span></span>
<span data-ttu-id="51d51-178">[Variabelen](../azure-resource-manager/resource-group-authoring-templates.md#variables) zijn waarden die u in de rest van de beheeroplossing Hallo Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="51d51-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in hello rest of hello management solution.</span></span>  <span data-ttu-id="51d51-179">Deze waarden zijn niet blootgestelde toohello gebruiker Hallo oplossing installeren.</span><span class="sxs-lookup"><span data-stu-id="51d51-179">These values are not exposed toohello user installing hello solution.</span></span>  <span data-ttu-id="51d51-180">Ze zijn bedoeld tooprovide Hallo auteur met één locatie waar ze de waarden die u mogelijk meerdere keren worden gebruikt in de gehele Hallo oplossing kunnen beheren.</span><span class="sxs-lookup"><span data-stu-id="51d51-180">They are intended tooprovide hello author with a single location where they can manage values that may be used multiple times throughout hello solution.</span></span> <span data-ttu-id="51d51-181">U moet een specifieke tooyour waarden oplossing in variabelen plaatsen als tegengestelde toohard ze coderen in Hallo **resources** element.</span><span class="sxs-lookup"><span data-stu-id="51d51-181">You should put any values specific tooyour solution in variables as opposed toohard coding them in hello **resources** element.</span></span>  <span data-ttu-id="51d51-182">Dit maakt het Hallo-code beter leesbaar en kunt u deze waarden in latere versies tooeasily te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="51d51-182">This makes hello code more readable and allows you tooeasily change these values in later versions.</span></span>

<span data-ttu-id="51d51-183">Hieronder volgt een voorbeeld van een **variabelen** element met de gangbare parameters die worden gebruikt in oplossingen.</span><span class="sxs-lookup"><span data-stu-id="51d51-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="51d51-184">Raadpleeg van toovariable waarden via Hallo-oplossing met Hallo syntaxis **variabelen ('variabele name')**.</span><span class="sxs-lookup"><span data-stu-id="51d51-184">You refer toovariable values through hello solution with hello syntax **variables('variable name')**.</span></span>  <span data-ttu-id="51d51-185">Bijvoorbeeld: tooaccess Hallo SolutionName variabele, gebruikt u **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="51d51-185">For example, tooaccess hello SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="51d51-186">U kunt ook complexe variabelen definiëren die meerdere sets met waarden.</span><span class="sxs-lookup"><span data-stu-id="51d51-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="51d51-187">Dit zijn vooral handig beheersystemen waar het definiëren van meerdere eigenschappen voor verschillende soorten resources.</span><span class="sxs-lookup"><span data-stu-id="51d51-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="51d51-188">U kan bijvoorbeeld opnieuw indelen Hallo oplossing variabelen hierboven toohello hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="51d51-188">For example, you could restructure hello solution variables shown above toohello following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="51d51-189">In dit geval u toovariable waarden via Hallo-oplossing met Hallo syntaxis verwijzen **variables('variable name').property**.</span><span class="sxs-lookup"><span data-stu-id="51d51-189">In this case, you refer toovariable values through hello solution with hello syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="51d51-190">Bijvoorbeeld: tooaccess Hallo oplossingsnaam variabele, gebruikt u **variables('Solution'). Naam**.</span><span class="sxs-lookup"><span data-stu-id="51d51-190">For example, tooaccess hello Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="51d51-191">Resources</span><span class="sxs-lookup"><span data-stu-id="51d51-191">Resources</span></span>
<span data-ttu-id="51d51-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) Hallo andere middelen opgeven die uw beheeroplossing voor installeren en configureren.</span><span class="sxs-lookup"><span data-stu-id="51d51-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define hello different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="51d51-193">Dit is de grootste Hallo en meest complexe gedeelte van het Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="51d51-193">This will be hello largest and most complex portion of hello template.</span></span>  <span data-ttu-id="51d51-194">U krijgt Hallo structuur en volledige beschrijving van de resource-elementen in [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="51d51-194">You can get hello structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="51d51-195">Verschillende bronnen die u doorgaans definieert zijn aangegeven in de andere artikelen in deze documentatie.</span><span class="sxs-lookup"><span data-stu-id="51d51-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="51d51-196">Afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="51d51-196">Dependencies</span></span>
<span data-ttu-id="51d51-197">Hallo **dependsOn** elementen bevat een [afhankelijkheid](../azure-resource-manager/resource-group-define-dependencies.md) op een andere resource.</span><span class="sxs-lookup"><span data-stu-id="51d51-197">hello **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="51d51-198">Wanneer het Hallo-oplossing is geïnstalleerd, wordt een bron is niet gemaakt totdat alle afhankelijkheden ervan zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="51d51-198">When hello solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="51d51-199">Bijvoorbeeld: uw oplossing mogelijk [een runbook start](operations-management-suite-solutions-resources-automation.md#runbooks) wanneer deze geïnstalleerd met behulp van een [taak resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="51d51-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="51d51-200">Hallo taak resource, zijn afhankelijk van Hallo runbook resource toomake ervoor dat Hallo-runbook is gemaakt voordat het Hallo-taak is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="51d51-200">hello job resource would be dependent on hello runbook resource toomake sure that hello runbook is created before hello job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="51d51-201">OMS-werkruimte en de Automation-account</span><span class="sxs-lookup"><span data-stu-id="51d51-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="51d51-202">Oplossingen vereisen een [OMS-werkruimte](../log-analytics/log-analytics-manage-access.md) toocontain weergaven en een [Automation-account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks en verwante resources.</span><span class="sxs-lookup"><span data-stu-id="51d51-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span>  <span data-ttu-id="51d51-203">Deze moeten worden voordat Hallo resources in Hallo oplossing worden gemaakt en moeten niet worden gedefinieerd in Hallo oplossing zelf beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="51d51-203">These must be available before hello resources in hello solution are created and should not be defined in hello solution itself.</span></span>  <span data-ttu-id="51d51-204">Hallo-gebruiker wordt [een werkruimte en de account opgeven](operations-management-suite-solutions.md#oms-workspace-and-automation-account) wanneer ze uw oplossing implementeren, maar als de auteur van het Hallo kunt u overwegen Hallo punten te volgen.</span><span class="sxs-lookup"><span data-stu-id="51d51-204">hello user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as hello author you should consider hello following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="51d51-205">Oplossing resource</span><span class="sxs-lookup"><span data-stu-id="51d51-205">Solution resource</span></span>
<span data-ttu-id="51d51-206">Elke oplossing vereist een resource-vermelding in Hallo **resources** element waarmee wordt gedefinieerd Hallo oplossing zelf.</span><span class="sxs-lookup"><span data-stu-id="51d51-206">Each solution requires a resource entry in hello **resources** element that defines hello solution itself.</span></span>  <span data-ttu-id="51d51-207">Dit heeft een type **Microsoft.OperationsManagement/solutions** en hebben Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="51d51-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have hello following structure.</span></span> <span data-ttu-id="51d51-208">Dit omvat [standaardparameters](#parameters) en [variabelen](#variables) die gewoonlijk gebruikte toodefine eigenschappen van Hallo oplossing zijn.</span><span class="sxs-lookup"><span data-stu-id="51d51-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used toodefine properties of hello solution.</span></span>


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a><span data-ttu-id="51d51-209">Afhankelijkheden</span><span class="sxs-lookup"><span data-stu-id="51d51-209">Dependencies</span></span>
<span data-ttu-id="51d51-210">Hallo oplossing resource moet hebben een [afhankelijkheid](../azure-resource-manager/resource-group-define-dependencies.md) op alle andere bronnen in Hallo oplossing omdat ze tooexist moeten voordat Hallo oplossing kan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="51d51-210">hello solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in hello solution since they need tooexist before hello solution can be created.</span></span>  <span data-ttu-id="51d51-211">U dit doen door het toevoegen van een vermelding voor elke resource in Hallo **dependsOn** element.</span><span class="sxs-lookup"><span data-stu-id="51d51-211">You do this by adding an entry for each resource in hello **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="51d51-212">Eigenschappen</span><span class="sxs-lookup"><span data-stu-id="51d51-212">Properties</span></span>
<span data-ttu-id="51d51-213">Hallo oplossing resource heeft Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="51d51-213">hello solution resource has hello properties in hello following table.</span></span>  <span data-ttu-id="51d51-214">Dit omvat Hallo resources waarnaar wordt verwezen en deel uitmaken van het Hallo-oplossing waarmee wordt gedefinieerd hoe Hallo resource wordt beheerd nadat het Hallo-oplossing is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="51d51-214">This includes hello resources referenced and contained by hello solution which defines how hello resource is managed after hello solution is installed.</span></span>  <span data-ttu-id="51d51-215">Elke resource in Hallo oplossing moet worden opgenomen in beide Hallo **referencedResources** of Hallo **containedResources** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="51d51-215">Each resource in hello solution should be listed in either hello **referencedResources** or hello **containedResources** property.</span></span>

| <span data-ttu-id="51d51-216">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="51d51-216">Property</span></span> | <span data-ttu-id="51d51-217">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="51d51-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="51d51-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="51d51-218">workspaceResourceId</span></span> |<span data-ttu-id="51d51-219">ID van Hallo werkruimte voor logboekanalyse Hallo vorm  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Werkruimtenaam\>*.</span><span class="sxs-lookup"><span data-stu-id="51d51-219">ID of hello Log Analytics workspace in hello form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="51d51-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="51d51-220">referencedResources</span></span> |<span data-ttu-id="51d51-221">Lijst met resources in het Hallo-oplossing die mogen niet worden verwijderd wanneer het Hallo-oplossing is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="51d51-221">List of resources in hello solution that should not be removed when hello solution is removed.</span></span> |
| <span data-ttu-id="51d51-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="51d51-222">containedResources</span></span> |<span data-ttu-id="51d51-223">Lijst met resources in het Hallo-oplossing die moet worden verwijderd als het Hallo-oplossing is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="51d51-223">List of resources in hello solution that should be removed when hello solution is removed.</span></span> |

<span data-ttu-id="51d51-224">Hallo in bovenstaand voorbeeld is voor een oplossing met een runbook, een schema en de weergave.</span><span class="sxs-lookup"><span data-stu-id="51d51-224">hello example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="51d51-225">Hallo-planning en runbook zijn *waarnaar wordt verwezen* in Hallo **eigenschappen** element zodat ze worden niet verwijderd wanneer het Hallo-oplossing is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="51d51-225">hello schedule and runbook are *referenced* in hello  **properties**  element so they are not removed when hello solution is removed.</span></span>  <span data-ttu-id="51d51-226">Hallo-weergave is *opgenomen* zodat het wordt verwijderd wanneer het Hallo-oplossing is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="51d51-226">hello view is *contained* so it is removed when hello solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="51d51-227">Plannen</span><span class="sxs-lookup"><span data-stu-id="51d51-227">Plan</span></span>
<span data-ttu-id="51d51-228">Hallo **plan** entiteit van het Hallo-oplossing resource heeft Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="51d51-228">hello **plan** entity of hello solution resource has hello properties in hello following table.</span></span>

| <span data-ttu-id="51d51-229">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="51d51-229">Property</span></span> | <span data-ttu-id="51d51-230">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="51d51-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="51d51-231">naam</span><span class="sxs-lookup"><span data-stu-id="51d51-231">name</span></span> |<span data-ttu-id="51d51-232">Naam van het Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="51d51-232">Name of hello solution.</span></span> |
| <span data-ttu-id="51d51-233">Versie</span><span class="sxs-lookup"><span data-stu-id="51d51-233">version</span></span> |<span data-ttu-id="51d51-234">Versie van oplossing Hallo zoals wordt bepaald door de auteur van het Hallo.</span><span class="sxs-lookup"><span data-stu-id="51d51-234">Version of hello solution as determined by hello author.</span></span> |
| <span data-ttu-id="51d51-235">Product</span><span class="sxs-lookup"><span data-stu-id="51d51-235">product</span></span> |<span data-ttu-id="51d51-236">Unieke tekenreeks tooidentify Hallo oplossing.</span><span class="sxs-lookup"><span data-stu-id="51d51-236">Unique string tooidentify hello solution.</span></span> |
| <span data-ttu-id="51d51-237">Uitgever</span><span class="sxs-lookup"><span data-stu-id="51d51-237">publisher</span></span> |<span data-ttu-id="51d51-238">Uitgever van Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="51d51-238">Publisher of hello solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="51d51-239">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="51d51-239">Sample</span></span>
<span data-ttu-id="51d51-240">U kunt voorbeelden van oplossingsbestanden met een resource oplossing Hallo volgende locaties bekijken.</span><span class="sxs-lookup"><span data-stu-id="51d51-240">You can view samples of solution files with a solution resource at hello following locations.</span></span>

- [<span data-ttu-id="51d51-241">Automation-resources</span><span class="sxs-lookup"><span data-stu-id="51d51-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="51d51-242">Resources zoeken en waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="51d51-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="51d51-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51d51-243">Next steps</span></span>
* <span data-ttu-id="51d51-244">[Opgeslagen zoekopdrachten en waarschuwingen toevoegen](operations-management-suite-solutions-resources-searches-alerts.md) tooyour-beheeroplossing.</span><span class="sxs-lookup"><span data-stu-id="51d51-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) tooyour management solution.</span></span>
* <span data-ttu-id="51d51-245">[Weergaven toevoegen](operations-management-suite-solutions-resources-views.md) tooyour-beheeroplossing.</span><span class="sxs-lookup"><span data-stu-id="51d51-245">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="51d51-246">[Runbooks en andere Automation-resources toevoegen](operations-management-suite-solutions-resources-automation.md) tooyour-beheeroplossing.</span><span class="sxs-lookup"><span data-stu-id="51d51-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>
* <span data-ttu-id="51d51-247">Meer details op Hallo van [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="51d51-247">Learn hello details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="51d51-248">Search [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates) voor voorbeelden van andere Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="51d51-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
