---
title: aaaWeb klonen van de App met Azure Portal
description: Meer informatie over hoe tooclone uw Web-Apps toonew Web-Apps met Azure Portal.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="d3ae7-103">Azure App Service-App met behulp van Azure-Portal klonen</span><span class="sxs-lookup"><span data-stu-id="d3ae7-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="d3ae7-104">Hallo-functie in voor het klonen [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) kunt u bestaande web-apps tooa nieuw gemaakt-app in een andere regio of in een eenvoudig kloon Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-104">hello cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="d3ae7-105">Hiermee schakelt u klanten toodeploy een aantal apps over verschillende regio's snel en eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="d3ae7-106">Klonen van de App is momenteel alleen ondersteund voor premium-laag app service-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="d3ae7-107">gebruikt voor nieuwe functie Hallo Hallo dezelfde beperkingen als onderdeel van de back-up van Web Apps, Zie [Back-up van een web-app in Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="d3ae7-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="d3ae7-108">Klonen van een bestaande App</span><span class="sxs-lookup"><span data-stu-id="d3ae7-108">Cloning an existing App</span></span>
<span data-ttu-id="d3ae7-109">Hallo-web-app moet worden uitgevoerd in Hallo **Premium** modus zodat u een kloon voor web-app Hallo toocreate.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-109">hello web app must be running in hello **Premium** mode in order for you toocreate a clone for hello web app.</span></span>

1. <span data-ttu-id="d3ae7-110">In Hallo [Azure Portal](https://portal.azure.com/), opent u de blade van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-110">In hello [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="d3ae7-111">Klik op **extra**.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-111">Click **Tools**.</span></span> <span data-ttu-id="d3ae7-112">Klik op Hallo **extra** blade klikt u op **kloon App**.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-112">Then, in hello **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="d3ae7-113">Als de web-app Hallo nog niet Hallo **Premium** modus, ontvangt u een bericht weergegeven dat aangeeft Hallo ondersteund modi voor het klonen van de app.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-113">If hello web app is not already in hello **Premium** mode, you will receive a message indicating hello supported modes for app cloning.</span></span> <span data-ttu-id="d3ae7-114">Op dit moment hebt u Hallo optie tooselect **Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-114">At this point, you have hello option tooselect **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="d3ae7-115">In Hallo **kloon App** blade Geef een naam op van de nieuwe web-app hello, resourcegroep en App Service-Plan.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-115">In hello **Clone App** blade provide a name of hello new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="d3ae7-116">Ook Hallo gebruiker worden kunnen toochoose of tooclone een aantal instellingen voor web-app bron of niet.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-116">Also hello user will be able toochoose whether tooclone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="d3ae7-117">Wanneer u op **maken** Hallo platform werkt over het maken van een kloon van Hallo bron web-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-117">After clicking **create** hello platform will start working on creating a clone of hello source web app.</span></span>

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="d3ae7-118">Klonen van een bestaande App tooan App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="d3ae7-118">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="d3ae7-119">In Hallo **kloon App** blade Hallo klant hebt Hallo optie toochoose een groep van toepassingen in een bestaand App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-119">In hello **Clone App** blade hello customer will have hello option toochoose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="d3ae7-120">Huidige beperkingen</span><span class="sxs-lookup"><span data-stu-id="d3ae7-120">Current Restrictions</span></span>
<span data-ttu-id="d3ae7-121">Deze functie is momenteel in preview, wij werken tooadd nieuwe mogelijkheden gedurende een bepaalde periode, Hallo volgende lijst worden Hallo bekende beperkingen op Hallo ondersteuning van het klonen van de app in Azure-Portal:</span><span class="sxs-lookup"><span data-stu-id="d3ae7-121">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="d3ae7-122">Azure Traffic Manager-instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="d3ae7-123">Instellingen voor automatisch schalen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="d3ae7-124">Back-upschema instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="d3ae7-125">VNET-instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="d3ae7-126">App Insights worden niet automatisch ingesteld op Hallo bestemming web-app</span><span class="sxs-lookup"><span data-stu-id="d3ae7-126">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="d3ae7-127">Eenvoudige verificatie-instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="d3ae7-128">Kudu extensie worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="d3ae7-129">TiP regels worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="d3ae7-130">Database-inhoud worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="d3ae7-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="d3ae7-131">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="d3ae7-131">References</span></span>
* [<span data-ttu-id="d3ae7-132">Klonen van Web-App met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3ae7-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="d3ae7-133">Back-up van een web-app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d3ae7-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="d3ae7-134">Hoe tooCreate een App-serviceomgeving</span><span class="sxs-lookup"><span data-stu-id="d3ae7-134">How tooCreate an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="d3ae7-135">Een web-app maken in een App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="d3ae7-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="d3ae7-136">Inleiding tooApp Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="d3ae7-136">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
