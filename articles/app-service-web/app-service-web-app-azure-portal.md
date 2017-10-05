---
title: Verwijzing voor het navigeren door de Azure-portal
description: Meer informatie over de verschillende gebruikerservaringen voor Web-App Service tussen de beheerportal en de Azure Portal
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a><span data-ttu-id="e8cf2-103">Verwijzing voor het navigeren door de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e8cf2-103">Reference for navigating the Azure portal</span></span>
<span data-ttu-id="e8cf2-104">Azure Websites heten voortaan [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e8cf2-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="e8cf2-105">We bijwerkt onze documentatie in overeenstemming met deze naamswijziging en met instructies voor de Azure-Portal alle.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-105">We're updating all of our documentation to reflect this name change and to provide instructions for the Azure Portal.</span></span> <span data-ttu-id="e8cf2-106">Totdat dit proces is voltooid, kunt u dit document als richtlijn voor het werken met Web-Apps in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-106">Until that process is done, you can use this document as a guide for working with Web Apps in the Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a><span data-ttu-id="e8cf2-107">De toekomst van de klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e8cf2-107">The future of the Azure Classic Portal</span></span>
<span data-ttu-id="e8cf2-108">Terwijl u de huisstijl wijzigingen in de klassieke Azure-Portal zult, wordt deze portal is bezig te vervangen door de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-108">While you will notice the branding changes on the Azure Classic Portal, that portal is in the process of being replaced by the Azure Portal.</span></span> <span data-ttu-id="e8cf2-109">Als u de klassieke portal is geleidelijk stopgezet, wordt de focus voor het ontwikkelen van nieuwe verschuiving naar de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-109">As the classic portal is being phased out, the focus for new development is shifting to the Azure Portal.</span></span> <span data-ttu-id="e8cf2-110">Alle toekomstige nieuwe functies voor Web-Apps wordt geleverd in de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-110">All upcoming new features for Web Apps will come in the Azure Portal.</span></span> <span data-ttu-id="e8cf2-111">Starten met Azure Portal om te profiteren van de nieuwste en beste dat Web-Apps te bieden hebben.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-111">Start using the Azure Portal to take advantage of the latest and greatest that Web Apps have to offer.</span></span>

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="e8cf2-112">Lay-out verschillen tussen de klassieke Azure-Portal en de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e8cf2-112">Layout differences between the Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="e8cf2-113">Alle Azure-services worden in de klassieke portal weergegeven aan de linkerzijde.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-113">In the classic portal, all the Azure services are listed on the left hand side.</span></span> <span data-ttu-id="e8cf2-114">Navigatie in de klassieke portal volgt boomstructuur, waarbij het starten van de service en gaat u naar elk element.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-114">Navigation in the classic portal follows a tree structure, where you start from the service and navigate into each element.</span></span> <span data-ttu-id="e8cf2-115">Deze structuur is geschikt als onafhankelijke onderdelen beheren.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="e8cf2-116">Toepassingen die zijn gebouwd op Azure zijn echter een verzameling met elkaar verbonden services, en deze structuur is niet ideaal voor het werken met verzamelingen van services.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="e8cf2-117">De Azure-portal kunt eenvoudig toepassingen end-to-end van onderdelen uit meerdere services bouwen.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-117">The Azure portal makes it easy to build applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="e8cf2-118">De portal is ingedeeld als *trajecten*.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-118">The portal is organized as *journeys*.</span></span> <span data-ttu-id="e8cf2-119">Een *reis* is een reeks *blades*, dat zijn containers voor de verschillende onderdelen.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-119">A *journey* is a series of *blades*, which are containers for the different components.</span></span> <span data-ttu-id="e8cf2-120">Bijvoorbeeld, instellen van het automatisch schalen voor een web-app is een *reis* die u gaat verschillende blades zoals weergegeven in het volgende voorbeeld: de **website** blade (dat blade titel nog niet zijn bijgewerkt voor het gebruik van de nieuwe terminologie), de **instellingen** blade en de **uitschalen** blade.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in the following example: the **web-site** blade (that blade title has not yet been updated to use the new terminology), the **Settings** blade, and the **Scale out** blade.</span></span> <span data-ttu-id="e8cf2-121">In het voorbeeld automatische schaling wordt ingesteld afhankelijk is van de CPU-gebruik, dus er ook is een **CPU-Percentage** blade.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-121">In the example, auto scaling is being set up to depend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="e8cf2-122">De onderdelen binnen de *blades* heten *delen*, die eruit tegels.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-122">The components within the *blades* are called *parts*, which look like tiles.</span></span> 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="e8cf2-123">Navigatie-voorbeeld: een web-app maken</span><span class="sxs-lookup"><span data-stu-id="e8cf2-123">Navigation example: create a web app</span></span>
<span data-ttu-id="e8cf2-124">Maken van nieuwe WebApps is nog steeds zo soepel 1-2-3.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="e8cf2-125">De volgende afbeelding toont de klassieke portal en de portal side-by-side ter illustratie van weinig is gewijzigd in het aantal stappen die nodig zijn voor een web-app laten en wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-125">The following image shows the classic portal and the portal side-by-side to demonstrate that not much has changed in the number of steps needed to get a web app up and running.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="e8cf2-126">In de portal kunt u kiezen uit de meest voorkomende typen van web-apps, met inbegrip van toepassingen zoals WordPress populaire galerie.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-126">In the portal you can choose from the most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="e8cf2-127">Voor een volledige lijst met beschikbare toepassingen, gaat u naar de [Azure Marketplace].</span><span class="sxs-lookup"><span data-stu-id="e8cf2-127">For a full list of available applications, visit the [Azure Marketplace].</span></span>

<span data-ttu-id="e8cf2-128">Wanneer u een web-app maakt, u de URL opgeven App Service-abonnement en de locatie in de portal, net zoals u in de klassieke portal doen.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-128">When you create a web app, you specify URL, App Service plan, and location in the portal just as you do in the classic portal.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="e8cf2-129">Bovendien kunt de portal u andere algemene instellingen definiëren.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-129">In addition, the portal lets you define other common settings.</span></span> <span data-ttu-id="e8cf2-130">Bijvoorbeeld: [resourcegroepen](../azure-resource-manager/resource-group-overview.md) kunt u eenvoudig aan bekijken en gerelateerde Azure-resources te beheren.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple to see and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="e8cf2-131">Navigatie-voorbeeld: instellingen en functies</span><span class="sxs-lookup"><span data-stu-id="e8cf2-131">Navigation example: settings and features</span></span>
<span data-ttu-id="e8cf2-132">Alle instellingen en functies worden nu logisch gegroepeerd in een enkel blade, van waaruit u kunt navigeren.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-132">All the settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="e8cf2-133">U kunt bijvoorbeeld aangepaste domeinen maken door te klikken op **aangepaste domeinen en SSL** in de **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-133">For example, you can create custom domains by clicking **Custom domains and SSL** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="e8cf2-134">Als u een waarschuwing voor bewaking instelt, klikt u op **aanvragen en fouten** en vervolgens **waarschuwing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-134">To set up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](./media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="e8cf2-135">Om diagnostische gegevens inschakelen, klikt u op **diagnostische logboeken** in de **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-135">To enable diagnostics, click **Diagnostics logs** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="e8cf2-136">Om toepassingsinstellingen te configureren, klikt u op **toepassingsinstellingen** in de **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-136">To configure application settings, click **Application settings** in the **Settings** blade.</span></span> 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="e8cf2-137">Anders dan de naam van het merk, zijn een aantal items in de portal verwijderd of hernoemd gegroepeerd anders makkelijker te vinden.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-137">Other than the brand name, a few things in the portal have been renamed or grouped differently to make it easier to find them.</span></span> <span data-ttu-id="e8cf2-138">Bijvoorbeeld: hieronder staat een screenshot van de bijbehorende pagina app-instellingen (**configureren**) in de klassieke portal.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-138">For example, below is a screenshot of the corresponding page for app settings (**Configure**) in the classic portal.</span></span>

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="e8cf2-139">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="e8cf2-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="e8cf2-140">[Azure Marketplace]: /marketplace/</span><span class="sxs-lookup"><span data-stu-id="e8cf2-140">[Azure Marketplace]: /marketplace/</span></span>

> [!NOTE]
> <span data-ttu-id="e8cf2-141">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e8cf2-142">U hebt geen creditcard nodig en u gaat geen verplichtingen aan.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="e8cf2-143">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="e8cf2-143">What's changed</span></span>
* <span data-ttu-id="e8cf2-144">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e8cf2-144">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

