---
title: aaaDeploy Azure API Management services-toomultiple Azure regio's | Microsoft Docs
description: Meer informatie over hoe toodeploy een Azure API Management service-exemplaar toomultiple Azure regio's.
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
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a><span data-ttu-id="10301-103">Hoe toodeploy een Azure API Management service-exemplaar toomultiple Azure regio's</span><span class="sxs-lookup"><span data-stu-id="10301-103">How toodeploy an Azure API Management service instance toomultiple Azure regions</span></span>
<span data-ttu-id="10301-104">API Management biedt ondersteuning voor meerdere landen/regio-implementatie die Hiermee kunt API uitgevers toodistribute een enkele API management-service op een willekeurig aantal gewenste Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="10301-104">API Management supports multi-region deployment which enables API publishers toodistribute a single API management service across any number of desired Azure regions.</span></span> <span data-ttu-id="10301-105">Dit vermindert de latentie waargenomen door geografisch verspreid API consumenten en verbetert tevens de servicebeschikbaarheid als één regio offline gaat.</span><span class="sxs-lookup"><span data-stu-id="10301-105">This helps reduce request latency perceived by geographically distributed API consumers and also improves service availability if one region goes offline.</span></span> 

<span data-ttu-id="10301-106">Wanneer u een API Management-service in eerste instantie is gemaakt, bevat deze slechts één [eenheid] [ unit] en bevindt zich op één Azure-regio, die is opgegeven als primaire regio Hallo.</span><span class="sxs-lookup"><span data-stu-id="10301-106">When an API Management service is created initially, it contains only one [unit][unit] and resides in a single Azure region, which is designated as hello Primary Region.</span></span> <span data-ttu-id="10301-107">Extra gebieden kunnen eenvoudig worden toegevoegd via hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="10301-107">Additional regions can be easily added through hello Azure Portal.</span></span> <span data-ttu-id="10301-108">Een API Management gateway-server is geïmplementeerde tooeach regio en aanroep verkeer worden gerouteerd toohello dichtstbijzijnde gateway.</span><span class="sxs-lookup"><span data-stu-id="10301-108">An API Management gateway server is deployed tooeach region and call traffic will be routed toohello closest gateway.</span></span> <span data-ttu-id="10301-109">Als een regio offline gaat, is het Hallo-verkeer automatisch opnieuw gerichte toohello volgende dichtstbijzijnde gateway.</span><span class="sxs-lookup"><span data-stu-id="10301-109">If a region goes offline, hello traffic is automatically re-directed toohello next closest gateway.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="10301-110">Implementatie van meerdere landen/regio is alleen beschikbaar in Hallo  **[Premium] [ Premium]**  laag.</span><span class="sxs-lookup"><span data-stu-id="10301-110">Multi-region deployment is only available in hello **[Premium][Premium]** tier.</span></span>
> 
> 

## <span data-ttu-id="10301-111"><a name="add-region"></a>Implementeren van een API Management-service-exemplaar tooa nieuwe regio</span><span class="sxs-lookup"><span data-stu-id="10301-111"><a name="add-region"> </a>Deploy an API Management service instance tooa new region</span></span>
> [!NOTE]
> <span data-ttu-id="10301-112">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="10301-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="10301-113">Navigeer in Azure Portal Hallo toohello **schaal en prijzen** pagina voor uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="10301-113">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Tabblad schaal][api-management-scale-service]

<span data-ttu-id="10301-115">toodeploy tooa nieuwe regio, klik op **+ toevoegen regio** Hallo werkbalk van.</span><span class="sxs-lookup"><span data-stu-id="10301-115">toodeploy tooa new region, click on **+ Add region** from hello toolbar.</span></span>

![Regio toevoegen][api-management-add-region]

<span data-ttu-id="10301-117">Selecteer Hallo locatie in de vervolgkeuzelijst Hallo en Hallo aantal eenheden voor met Hallo schuifregelaar ingesteld.</span><span class="sxs-lookup"><span data-stu-id="10301-117">Select hello location from hello drop-down list and set hello number of units for with hello slider.</span></span>

![Geef de eenheden][api-management-select-location-units]

<span data-ttu-id="10301-119">Klik op **toevoegen** tooplace uw selectie in Hallo locaties tabel.</span><span class="sxs-lookup"><span data-stu-id="10301-119">Click **Add** tooplace your selection in hello Locations table.</span></span> 

<span data-ttu-id="10301-120">Herhaal dit proces totdat u alle geconfigureerde locaties en klik op **opslaan** van Hallo werkbalk toostart Hallo-implementatieproces.</span><span class="sxs-lookup"><span data-stu-id="10301-120">Repeat this process until you have all locations configured and click **Save** from hello toolbar toostart hello deployment process.</span></span>

## <span data-ttu-id="10301-121"><a name="remove-region"></a>Verwijderen van exemplaar van API Management-service van een locatie</span><span class="sxs-lookup"><span data-stu-id="10301-121"><a name="remove-region"> </a>Delete an API Management service instance from a location</span></span>
<span data-ttu-id="10301-122">Navigeer in Azure Portal Hallo toohello **schaal en prijzen** pagina voor uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="10301-122">In hello Azure Portal navigate toohello **Scale and pricing** page for your API Management service instance.</span></span> 

![Tabblad schaal][api-management-scale-service]

<span data-ttu-id="10301-124">Voor Hallo locatie die u wilt dat openen tooremove contextmenu Hallo Hallo met **...**  knop aan de rechterkant Hallo van Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="10301-124">For hello location you would like tooremove open hello context menu using hello **...** button at hello right end of hello table.</span></span> <span data-ttu-id="10301-125">Selecteer Hallo **verwijderen** optie.</span><span class="sxs-lookup"><span data-stu-id="10301-125">Select hello **Delete** option.</span></span>

![Regio verwijderen][api-management-remove-region]

<span data-ttu-id="10301-127">Hallo bevestigen en klikt u op **opslaan** tooapply Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="10301-127">Confirm hello deletion and click **Save** tooapply hello changes.</span></span>

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

