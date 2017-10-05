---
title: Multi-Geo-Help-documentatie | Microsoft Docs
description: Meer informatie over het maken van een werkruimte en publiceren van een webservice in een Azure-regio verschillende van de Zuid-centraal VS (SCUS) Azure-regio.
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 32f80863308c00c32b1496bb92d39a7ae7d0cc6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="a1966-103">Help-documentatie voor meerdere geografische gebieden</span><span class="sxs-lookup"><span data-stu-id="a1966-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="a1966-104">Dit artikel wordt beschreven hoe u een werkruimte maken en publiceren van een webservice in verschillende Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="a1966-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="a1966-105">De [Azure producten op de pagina regio](https://azure.microsoft.com/en-us/regions/services/) bevat gebieden waarin Azure Machine Learning beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="a1966-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="a1966-106">Een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="a1966-106">Create a workspace</span></span>
1. <span data-ttu-id="a1966-107">Aanmelden bij de klassieke Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a1966-107">Sign in to the Azure Classic Portal.</span></span>
2. <span data-ttu-id="a1966-108">Klik op **+ nieuw** > **GEGEVENSSERVICES** > **MACHINE LEARNING** > **met snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="a1966-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="a1966-109">Onder **locatie** selecteren, zoals een andere regio **Zuidoost-Azië**.</span><span class="sxs-lookup"><span data-stu-id="a1966-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="a1966-110">![Multi-Geo-Help afbeelding 1][1]</span><span class="sxs-lookup"><span data-stu-id="a1966-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="a1966-111">Selecteer de werkruimte en klik vervolgens op **aanmelden bij ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="a1966-111">Select the workspace, and then click **Sign-in to ML Studio**.</span></span>
   <span data-ttu-id="a1966-112">![Multi-Geo-Help afbeelding 2][2]</span><span class="sxs-lookup"><span data-stu-id="a1966-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="a1966-113">U hebt nu een werkruimte in een andere regio die u net als elke andere werkruimte mag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1966-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="a1966-114">U kunt schakelen tussen uw werkruimten, zoek in de rechterbovenhoek van het scherm.</span><span class="sxs-lookup"><span data-stu-id="a1966-114">To switch among your workspaces, look to the upper right of your screen.</span></span> <span data-ttu-id="a1966-115">Klik op de vervolgkeuzelijst, selecteer de regio en selecteer vervolgens de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="a1966-115">Click the dropdown, select the region, and then select the workspace.</span></span> <span data-ttu-id="a1966-116">Alles is lokaal op de werkruimte regio.</span><span class="sxs-lookup"><span data-stu-id="a1966-116">Everything is local to the workspace region.</span></span>  <span data-ttu-id="a1966-117">Bijvoorbeeld, worden alle webservices gemaakt op basis van een werkruimte in de werkruimte bevindt zich in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="a1966-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span></span>
   <span data-ttu-id="a1966-118">![Multi-Geo-Help afbeelding 3][3]</span><span class="sxs-lookup"><span data-stu-id="a1966-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="a1966-119">Een experiment openen vanuit galerie</span><span class="sxs-lookup"><span data-stu-id="a1966-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="a1966-120">Als u een experiment vanuit galerie openen, kunt u ook welke regio die u wilt kopiëren van het experiment te selecteren.</span><span class="sxs-lookup"><span data-stu-id="a1966-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span></span>

![Multi-Geo-Help afbeelding 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="a1966-122">Webservice beheren</span><span class="sxs-lookup"><span data-stu-id="a1966-122">Web service management</span></span>
<span data-ttu-id="a1966-123">Om webservices, zoals programmatisch te beheren voor retraining, het regiospecifieke-adres te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a1966-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span></span>

* <span data-ttu-id="a1966-124">https://asiasoutheast.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="a1966-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="a1966-125">https://europewest.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="a1966-125">https://europewest.management.azureml.net</span></span>

### <a name="things-to-note"></a><span data-ttu-id="a1966-126">Let op</span><span class="sxs-lookup"><span data-stu-id="a1966-126">Things to note</span></span>
1. <span data-ttu-id="a1966-127">U kunt alleen experimenten tussen werkruimten die deel uitmaken van dezelfde regio op deze manier kopiëren.</span><span class="sxs-lookup"><span data-stu-id="a1966-127">You can only copy experiments between workspaces that belong to the same region this way.</span></span> <span data-ttu-id="a1966-128">Als u wilt kopiëren experiment tussen werkruimten in verschillende regio's, kunt u de [PowerShell](http://aka.ms/amlps) commandlet [ *kopie AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) Agent installeert.</span><span class="sxs-lookup"><span data-stu-id="a1966-128">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span></span> <span data-ttu-id="a1966-129">Een andere oplossing is voor het publiceren van het experiment in de galerie in de modus voor niet-vermelde, opent u het in de werkruimte van de andere regio.</span><span class="sxs-lookup"><span data-stu-id="a1966-129">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span></span>
2. <span data-ttu-id="a1966-130">De regio-selector wordt alleen weergegeven voor werkruimten voor één regio tegelijk.</span><span class="sxs-lookup"><span data-stu-id="a1966-130">The region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="a1966-131">Een gratis werkruimte of gast (anonieme verificatie) werkruimte wordt gemaakt en gehost in Zuid-centraal VS</span><span class="sxs-lookup"><span data-stu-id="a1966-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="a1966-132">Web-services op basis van een werkruimte in Zuidoost-Azië geïmplementeerd zal ook worden gehost in Zuidoost-Azië.</span><span class="sxs-lookup"><span data-stu-id="a1966-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="a1966-133">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="a1966-133">More information</span></span>
<span data-ttu-id="a1966-134">Stel een vraag op de [Azure Machine Learning-forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="a1966-134">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
