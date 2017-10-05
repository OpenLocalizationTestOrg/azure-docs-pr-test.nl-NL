---
title: Verbinding maken met Azure analyseservices met Power BI | Microsoft Docs
description: Informatie over het verbinding maken met een Azure Analysis Services-server met behulp van Power BI.
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
ms.openlocfilehash: 3a2af043feddb4a1d6d63f50e838c8a39035449f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="d8b82-103">Verbinding maken met Power BI</span><span class="sxs-lookup"><span data-stu-id="d8b82-103">Connect with Power BI</span></span>

<span data-ttu-id="d8b82-104">Zodra u hebt een server in Azure gemaakt en geïmplementeerd een model in tabelvorm, zijn gebruikers in uw organisatie gereed om te koppelen en gebruiken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="d8b82-104">Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="d8b82-105">Zorg ervoor dat u de nieuwste versie van [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="d8b82-105">Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="d8b82-106">Verbinding maken in Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="d8b82-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="d8b82-107">Klik in Power BI Desktop op **gegevens ophalen** > **Azure** > **Azure Analysis Services-database**.</span><span class="sxs-lookup"><span data-stu-id="d8b82-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="d8b82-108">In **Server**, voer de naam van de server.</span><span class="sxs-lookup"><span data-stu-id="d8b82-108">In **Server**, enter the server name.</span></span> 
    
    <span data-ttu-id="d8b82-109">Zorg dat u de volledige URL opnemen.</span><span class="sxs-lookup"><span data-stu-id="d8b82-109">Be sure to include the full URL.</span></span> <span data-ttu-id="d8b82-110">Bijvoorbeeld: asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="d8b82-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="d8b82-111">In **Database**, als u weet dat de naam van de tabellaire modeldatabase of perspectief die u verbinding maken met wilt, plakt u deze hier.</span><span class="sxs-lookup"><span data-stu-id="d8b82-111">In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here.</span></span> <span data-ttu-id="d8b82-112">Anders kunt u dit veld leeg laten en later een database of perspectief selecteren.</span><span class="sxs-lookup"><span data-stu-id="d8b82-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="d8b82-113">Laat de standaardwaarde **Connect live** optie en druk vervolgens **Connect**.</span><span class="sxs-lookup"><span data-stu-id="d8b82-113">Leave the default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="d8b82-114">Als u wordt gevraagd, voert u de aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="d8b82-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="d8b82-115">In **Navigator**, vouw de server uit en selecteer vervolgens het model of perspectief die u verbinding wilt, klikt u vervolgens op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="d8b82-115">In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**.</span></span> <span data-ttu-id="d8b82-116">Klik op een model of perspectief om alle objecten voor deze weergave weer te geven.</span><span class="sxs-lookup"><span data-stu-id="d8b82-116">Click  a model or perspective to show all the objects for that view.</span></span>

    <span data-ttu-id="d8b82-117">Het model wordt geopend in Power BI Desktop met een leeg rapport in de rapportweergave.</span><span class="sxs-lookup"><span data-stu-id="d8b82-117">The model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="d8b82-118">De veldenlijst bevat alle modelobjecten niet-verborgen.</span><span class="sxs-lookup"><span data-stu-id="d8b82-118">The Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="d8b82-119">Verbindingsstatus wordt weergegeven in de rechterbenedenhoek.</span><span class="sxs-lookup"><span data-stu-id="d8b82-119">Connection status is displayed in the lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="d8b82-120">Verbinding maken in Power BI (service)</span><span class="sxs-lookup"><span data-stu-id="d8b82-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="d8b82-121">Maak een Power BI Desktop-bestand met een actieve verbinding met het model op uw server.</span><span class="sxs-lookup"><span data-stu-id="d8b82-121">Create a Power BI Desktop file that has a live connection to your model on your server.</span></span>
2. <span data-ttu-id="d8b82-122">In [Power BI](https://powerbi.microsoft.com), klikt u op **gegevens ophalen** > **bestanden**.</span><span class="sxs-lookup"><span data-stu-id="d8b82-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="d8b82-123">Zoek en selecteer het bestand.</span><span class="sxs-lookup"><span data-stu-id="d8b82-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="d8b82-124">Zie ook</span><span class="sxs-lookup"><span data-stu-id="d8b82-124">See also</span></span>
<span data-ttu-id="d8b82-125">[Verbinding maken met Azure analyseservices](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="d8b82-125">[Connect to Azure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="d8b82-126">Clientbibliotheken</span><span class="sxs-lookup"><span data-stu-id="d8b82-126">Client libraries</span></span>](analysis-services-data-providers.md)

