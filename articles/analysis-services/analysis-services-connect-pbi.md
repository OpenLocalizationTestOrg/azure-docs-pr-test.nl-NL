---
title: aaaConnect tooAzure Analysis Services met Power BI | Microsoft Docs
description: Meer informatie over hoe tooconnect tooan Azure Analysis Services-server met behulp van Power BI.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="58f34-103">Verbinding maken met Power BI</span><span class="sxs-lookup"><span data-stu-id="58f34-103">Connect with Power BI</span></span>

<span data-ttu-id="58f34-104">Nadat u hebt een server in Azure gemaakt en geïmplementeerd een model in tabelvorm tooit, gebruikers in uw organisatie zijn gereed tooconnect en deze gegevens te verkennen.</span><span class="sxs-lookup"><span data-stu-id="58f34-104">Once you've created a server in Azure, and deployed a tabular model tooit, users in your organization are ready tooconnect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="58f34-105">Ervoor toouse Hallo meest recente versie van [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="58f34-105">Be sure toouse hello latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="58f34-106">Verbinding maken in Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="58f34-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="58f34-107">Klik in Power BI Desktop op **gegevens ophalen** > **Azure** > **Azure Analysis Services-database**.</span><span class="sxs-lookup"><span data-stu-id="58f34-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="58f34-108">In **Server**, Voer Hallo servernaam.</span><span class="sxs-lookup"><span data-stu-id="58f34-108">In **Server**, enter hello server name.</span></span> 
    
    <span data-ttu-id="58f34-109">Ervoor tooinclude Hallo volledige URL zijn.</span><span class="sxs-lookup"><span data-stu-id="58f34-109">Be sure tooinclude hello full URL.</span></span> <span data-ttu-id="58f34-110">Bijvoorbeeld: asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="58f34-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="58f34-111">In **Database**, als u de naam Hallo van Hallo model in tabelvorm database of het gewenste tooconnect hier plakken naar perspectief kent.</span><span class="sxs-lookup"><span data-stu-id="58f34-111">In **Database**, if you know hello name of hello tabular model database or perspective you want tooconnect to, paste it here.</span></span> <span data-ttu-id="58f34-112">Anders kunt u dit veld leeg laten en later een database of perspectief selecteren.</span><span class="sxs-lookup"><span data-stu-id="58f34-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="58f34-113">Laat de standaardwaarde Hallo **Connect live** optie en druk vervolgens **Connect**.</span><span class="sxs-lookup"><span data-stu-id="58f34-113">Leave hello default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="58f34-114">Als u wordt gevraagd, voert u de aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="58f34-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="58f34-115">In **Navigator**, vouw Hallo-server uit en selecteer vervolgens Hallo model of perspectief gewenste tooconnect aan, klikt u vervolgens op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="58f34-115">In **Navigator**, expand hello server, then select hello model or perspective you want tooconnect to, then click **Connect**.</span></span> <span data-ttu-id="58f34-116">Klik op een model- of perspectiefparameters tooshow alle Hallo-objecten voor deze weergave.</span><span class="sxs-lookup"><span data-stu-id="58f34-116">Click  a model or perspective tooshow all hello objects for that view.</span></span>

    <span data-ttu-id="58f34-117">Hallo model wordt geopend in Power BI Desktop met een leeg rapport in de rapportweergave.</span><span class="sxs-lookup"><span data-stu-id="58f34-117">hello model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="58f34-118">Hallo veldenlijst bevat alle modelobjecten niet-verborgen.</span><span class="sxs-lookup"><span data-stu-id="58f34-118">hello Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="58f34-119">Verbindingsstatus wordt weergegeven in de rechterbenedenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="58f34-119">Connection status is displayed in hello lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="58f34-120">Verbinding maken in Power BI (service)</span><span class="sxs-lookup"><span data-stu-id="58f34-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="58f34-121">Maak een Power BI Desktop-bestand met een live-verbinding tooyour model op uw server.</span><span class="sxs-lookup"><span data-stu-id="58f34-121">Create a Power BI Desktop file that has a live connection tooyour model on your server.</span></span>
2. <span data-ttu-id="58f34-122">In [Power BI](https://powerbi.microsoft.com), klikt u op **gegevens ophalen** > **bestanden**.</span><span class="sxs-lookup"><span data-stu-id="58f34-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="58f34-123">Zoek en selecteer het bestand.</span><span class="sxs-lookup"><span data-stu-id="58f34-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="58f34-124">Zie ook</span><span class="sxs-lookup"><span data-stu-id="58f34-124">See also</span></span>
<span data-ttu-id="58f34-125">[Verbinding maken met tooAzure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="58f34-125">[Connect tooAzure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="58f34-126">Clientbibliotheken</span><span class="sxs-lookup"><span data-stu-id="58f34-126">Client libraries</span></span>](analysis-services-data-providers.md)

