---
title: Azure API Management-services in meerdere Azure-regio's implementeren | Microsoft Docs
description: Informatie over het implementeren van een Azure API Management-service-exemplaar op meerdere Azure-regio's.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 1c39fee739c2f5fd4b928e1e76e1ea57f072b5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-an-azure-api-management-service-instance-to-multiple-azure-regions"></a><span data-ttu-id="b4686-103">Een Azure API Management-service-exemplaar implementeren op meerdere Azure-regio 's</span><span class="sxs-lookup"><span data-stu-id="b4686-103">How to deploy an Azure API Management service instance to multiple Azure regions</span></span>
<span data-ttu-id="b4686-104">API Management biedt ondersteuning voor meerdere landen/regio-implementatie waarmee de API-uitgevers voor een enkele API management-service verdelen over een willekeurig aantal gewenste Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="b4686-104">API Management supports multi-region deployment which enables API publishers to distribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="b4686-105">Dit vermindert de latentie waargenomen door geografisch verspreid API consumenten en verbetert tevens de servicebeschikbaarheid als één regio offline gaat.</span><span class="sxs-lookup"><span data-stu-id="b4686-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="b4686-106">Wanneer u een API Management-service in eerste instantie is gemaakt, bevat deze slechts één [eenheid] [ unit] en bevindt zich op één Azure-regio, die is opgegeven als de primaire regio.</span><span class="sxs-lookup"><span data-stu-id="b4686-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as the Primary Region.</span></span> <span data-ttu-id="b4686-107">Extra gebieden kunnen eenvoudig worden toegevoegd via de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="b4686-107">Additional regions can be easily added through the Azure Portal.</span></span> <span data-ttu-id="b4686-108">Een API Management-gatewayserver wordt geïmplementeerd voor elke regio en aanroep verkeer wordt doorgestuurd naar de dichtstbijzijnde gateway.</span><span class="sxs-lookup"><span data-stu-id="b4686-108">An API Management gateway server is deployed to each region and call traffic will be routed to the closest gateway.</span></span> <span data-ttu-id="b4686-109">Als een regio offline gaat, wordt het verkeer automatisch opnieuw gerichte naar de volgende dichtstbijzijnde gateway.</span><span class="sxs-lookup"><span data-stu-id="b4686-109">If a region goes offline, the traffic is automatically re-directed to the next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b4686-110">Implementatie van meerdere landen/regio is alleen beschikbaar in de  **[Premium] [ Premium]**  laag.</span><span class="sxs-lookup"><span data-stu-id="b4686-110">Multi-region deployment is only available in the **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="b4686-111"><a name="add-region"></a>Exemplaar van API Management-service implementeren in een nieuw gebied</span><span class="sxs-lookup"><span data-stu-id="b4686-111"><a name="add-region"> </a>Deploy an API Management service instance to a new region</span></span>
> [!NOTE]
> <span data-ttu-id="b4686-112">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="b4686-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="b4686-113">Navigeer in de Azure Portal naar de **schaal en prijzen** pagina voor uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b4686-113">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Tabblad schaal][api-management-scale-service]

<span data-ttu-id="b4686-115">Als u wilt implementeren op een nieuwe regio, klikt u op **+ toevoegen regio** van de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="b4686-115">To deploy to a new region, click on **+ Add region** from the toolbar.</span></span>

![Regio toevoegen][api-management-add-region]

<span data-ttu-id="b4686-117">Selecteer de locatie in de vervolgkeuzelijst en het aantal eenheden voor met de schuifregelaar ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b4686-117">Select the location from the drop-down list and set the number of units for with the slider.</span></span>

![Geef de eenheden][api-management-select-location-units]

<span data-ttu-id="b4686-119">Klik op **toevoegen** uw selectie in de tabel locaties plaatsen.</span><span class="sxs-lookup"><span data-stu-id="b4686-119">Click **Add** to place your selection in the Locations table.</span></span> 

<span data-ttu-id="b4686-120">Herhaal dit proces totdat u alle geconfigureerde locaties en klik op **opslaan** van de werkbalk om het implementatieproces start.</span><span class="sxs-lookup"><span data-stu-id="b4686-120">Repeat this process until you have all locations configured and click **Save** from the toolbar to start the deployment process.</span></span>

## <span data-ttu-id="b4686-121"><a name="remove-region"></a>Verwijderen van exemplaar van API Management-service van een locatie</span><span class="sxs-lookup"><span data-stu-id="b4686-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="b4686-122">Navigeer in de Azure Portal naar de **schaal en prijzen** pagina voor uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b4686-122">In the Azure Portal navigate to the **Scale and pricing** page for your API Management service instance.</span></span> 

![Tabblad schaal][api-management-scale-service]

<span data-ttu-id="b4686-124">Voor de locatie die u wilt verwijderen open het context-menu met de **...**  knop aan de rechterkant van de tabel.</span><span class="sxs-lookup"><span data-stu-id="b4686-124">For the location you would like to remove open the context menu using the **...** button at the right end of the table.</span></span> <span data-ttu-id="b4686-125">Selecteer de **verwijderen** optie.</span><span class="sxs-lookup"><span data-stu-id="b4686-125">Select the **Delete** option.</span></span>

![Regio verwijderen][api-management-remove-region]

<span data-ttu-id="b4686-127">De verwijdering te bevestigen en klikt u op **opslaan** de wijzigingen toe te passen.</span><span class="sxs-lookup"><span data-stu-id="b4686-127">Confirm the deletion and click **Save** to apply the changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance to a new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

