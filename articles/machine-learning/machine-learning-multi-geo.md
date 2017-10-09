---
title: aaaMulti Geo Help-documentatie | Microsoft Docs
description: Meer informatie over hoe een werkruimte toocreate en publiceren van een webservice in een Azure-regio verschilt Hallo Zuid-centraal VS (SCUS) Azure-regio.
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
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="bebff-103">Help-documentatie voor meerdere geografische gebieden</span><span class="sxs-lookup"><span data-stu-id="bebff-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="bebff-104">Dit artikel wordt beschreven hoe u een werkruimte maken en publiceren van een webservice in verschillende Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="bebff-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="bebff-105">Hallo [Azure producten op de pagina regio](https://azure.microsoft.com/en-us/regions/services/) bevat gebieden waarin Azure Machine Learning beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="bebff-105">hello [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="bebff-106">Een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="bebff-106">Create a workspace</span></span>
1. <span data-ttu-id="bebff-107">Meld u aan toohello klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="bebff-107">Sign in toohello Azure Classic Portal.</span></span>
2. <span data-ttu-id="bebff-108">Klik op **+ nieuw** > **GEGEVENSSERVICES** > **MACHINE LEARNING** > **met snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="bebff-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="bebff-109">Onder **locatie** selecteren, zoals een andere regio **Zuidoost-Azië**.</span><span class="sxs-lookup"><span data-stu-id="bebff-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="bebff-110">![Multi-Geo-Help afbeelding 1][1]</span><span class="sxs-lookup"><span data-stu-id="bebff-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="bebff-111">Hallo-werkruimte selecteren en klik vervolgens op **aanmelden tooML Studio**.</span><span class="sxs-lookup"><span data-stu-id="bebff-111">Select hello workspace, and then click **Sign-in tooML Studio**.</span></span>
   <span data-ttu-id="bebff-112">![Multi-Geo-Help afbeelding 2][2]</span><span class="sxs-lookup"><span data-stu-id="bebff-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="bebff-113">U hebt nu een werkruimte in een andere regio die u net als elke andere werkruimte mag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bebff-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="bebff-114">tooswitch tussen uw werkruimten uiterlijk toohello rechterbovenhoek van het scherm.</span><span class="sxs-lookup"><span data-stu-id="bebff-114">tooswitch among your workspaces, look toohello upper right of your screen.</span></span> <span data-ttu-id="bebff-115">Klik op Hallo dropdown, selecteer Hallo regio en selecteer vervolgens Hallo-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="bebff-115">Click hello dropdown, select hello region, and then select hello workspace.</span></span> <span data-ttu-id="bebff-116">Alles is lokale toohello werkruimte regio.</span><span class="sxs-lookup"><span data-stu-id="bebff-116">Everything is local toohello workspace region.</span></span>  <span data-ttu-id="bebff-117">Alle webservices gemaakt op basis van een werkruimte wordt bijvoorbeeld Hallo zich in dezelfde regio Hallo werkruimte liggen.</span><span class="sxs-lookup"><span data-stu-id="bebff-117">For example, all of your web services created from a workspace will be in hello same region hello workspace is located in.</span></span>
   <span data-ttu-id="bebff-118">![Multi-Geo-Help afbeelding 3][3]</span><span class="sxs-lookup"><span data-stu-id="bebff-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="bebff-119">Een experiment openen vanuit galerie</span><span class="sxs-lookup"><span data-stu-id="bebff-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="bebff-120">Als u een experiment vanuit galerie openen, kunt u ook selecteren welke regio gewenste toocopy Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="bebff-120">If you open an experiment from Gallery, you can also select which region you want toocopy hello experiment to.</span></span>

![Multi-Geo-Help afbeelding 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="bebff-122">Webservice beheren</span><span class="sxs-lookup"><span data-stu-id="bebff-122">Web service management</span></span>
<span data-ttu-id="bebff-123">tooprogrammatically voor het beheren van web-services, zoals voor de retraining, gebruik Hallo regiospecifieke adres:</span><span class="sxs-lookup"><span data-stu-id="bebff-123">tooprogrammatically manage web services, such as for retraining, use hello region-specific address:</span></span>

* <span data-ttu-id="bebff-124">https://asiasoutheast.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="bebff-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="bebff-125">https://europewest.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="bebff-125">https://europewest.management.azureml.net</span></span>

### <a name="things-toonote"></a><span data-ttu-id="bebff-126">Dingen toonote</span><span class="sxs-lookup"><span data-stu-id="bebff-126">Things toonote</span></span>
1. <span data-ttu-id="bebff-127">U kunt alleen experimenten tussen werkruimten die deel uitmaken van toohello kopiëren dezelfde regio op deze manier.</span><span class="sxs-lookup"><span data-stu-id="bebff-127">You can only copy experiments between workspaces that belong toohello same region this way.</span></span> <span data-ttu-id="bebff-128">Als u toocopy experiment moet tussen de werkruimten in verschillende regio's, kunt u Hallo [PowerShell](http://aka.ms/amlps) commandlet [ *kopie AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish die.</span><span class="sxs-lookup"><span data-stu-id="bebff-128">If you need toocopy experiment across workspaces in different regions, you can use hello [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish that.</span></span> <span data-ttu-id="bebff-129">Een andere oplossing toopublish Hallo experiment in de galerie is in de modus voor niet-vermelde en opent u het in de werkruimte Hallo van Hallo andere regio.</span><span class="sxs-lookup"><span data-stu-id="bebff-129">Another workaround is toopublish hello experiment into Gallery in unlisted mode, then open it in hello workspace from hello other region.</span></span>
2. <span data-ttu-id="bebff-130">Hallo regio selector wordt alleen weergegeven voor werkruimten voor één regio tegelijk.</span><span class="sxs-lookup"><span data-stu-id="bebff-130">hello region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="bebff-131">Een gratis werkruimte of gast (anonieme verificatie) werkruimte wordt gemaakt en gehost in Zuid-centraal VS</span><span class="sxs-lookup"><span data-stu-id="bebff-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="bebff-132">Web-services op basis van een werkruimte in Zuidoost-Azië geïmplementeerd zal ook worden gehost in Zuidoost-Azië.</span><span class="sxs-lookup"><span data-stu-id="bebff-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="bebff-133">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="bebff-133">More information</span></span>
<span data-ttu-id="bebff-134">Stel een vraag op Hallo [Azure Machine Learning-forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="bebff-134">Ask a question on hello [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
