---
title: Klonen van Web-App met Azure Portal
description: Informatie over het klonen van uw Web-Apps naar de nieuwe Web-Apps met Azure Portal.
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
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="b41d3-103">Azure App Service-App met behulp van Azure-Portal klonen</span><span class="sxs-lookup"><span data-stu-id="b41d3-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="b41d3-104">De functie voor klonen in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) kunt u eenvoudig bestaande klonen web-apps naar een nieuwe app in een andere regio of in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="b41d3-104">The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="b41d3-105">Hiermee schakelt u klanten een aantal apps implementeren in verschillende regio's snel en eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="b41d3-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="b41d3-106">Klonen van de App is momenteel alleen ondersteund voor premium-laag app service-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="b41d3-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="b41d3-107">De nieuwe functie maakt gebruik van dezelfde beperkingen als de functie Web Apps back-up, Zie [Back-up van een web-app in Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b41d3-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="b41d3-108">Klonen van een bestaande App</span><span class="sxs-lookup"><span data-stu-id="b41d3-108">Cloning an existing App</span></span>
<span data-ttu-id="b41d3-109">De web-app moet worden uitgevoerd in de **Premium** modus in als u een kloon voor de web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="b41d3-109">The web app must be running in the **Premium** mode in order for you to create a clone for the web app.</span></span>

1. <span data-ttu-id="b41d3-110">In de [Azure Portal](https://portal.azure.com/), opent u de blade van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="b41d3-110">In the [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="b41d3-111">Klik op **extra**.</span><span class="sxs-lookup"><span data-stu-id="b41d3-111">Click **Tools**.</span></span> <span data-ttu-id="b41d3-112">Klik op de **extra** blade, klikt u op **kloon App**.</span><span class="sxs-lookup"><span data-stu-id="b41d3-112">Then, in the **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="b41d3-113">Als de web-app nog niet in de **Premium** modus, ontvangt u een bericht met de ondersteunde modi voor het klonen van de app.</span><span class="sxs-lookup"><span data-stu-id="b41d3-113">If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning.</span></span> <span data-ttu-id="b41d3-114">Op dit moment hebt u de optie te selecteren **Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="b41d3-114">At this point, you have the option to select **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="b41d3-115">In de **kloon App** blade een naam opgeven van de nieuwe web-app, resourcegroep en App Service-Plan.</span><span class="sxs-lookup"><span data-stu-id="b41d3-115">In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="b41d3-116">Ook de gebruiker kan kiezen of voor het klonen van een aantal instellingen voor web-app bron worden of niet.</span><span class="sxs-lookup"><span data-stu-id="b41d3-116">Also the user will be able to choose whether to clone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="b41d3-117">Wanneer u op **maken** het platform werkt over het maken van een kloon van de bron-web-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b41d3-117">After clicking **create** the platform will start working on creating a clone of the source web app.</span></span>

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="b41d3-118">Klonen van een bestaande App aan een App-serviceomgeving</span><span class="sxs-lookup"><span data-stu-id="b41d3-118">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="b41d3-119">In de **kloon App** blade de klant heeft de optie voor het kiezen van een groep van toepassingen in een bestaand App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="b41d3-119">In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="b41d3-120">Huidige beperkingen</span><span class="sxs-lookup"><span data-stu-id="b41d3-120">Current Restrictions</span></span>
<span data-ttu-id="b41d3-121">Deze functie is momenteel in preview, wij werken als u wilt toevoegen van nieuwe mogelijkheden na verloop van tijd, in de volgende lijst worden de bekende beperkingen voor de huidige ondersteuning van het klonen van de app in Azure-Portal:</span><span class="sxs-lookup"><span data-stu-id="b41d3-121">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="b41d3-122">Azure Traffic Manager-instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="b41d3-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="b41d3-123">Instellingen voor automatisch schalen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="b41d3-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="b41d3-124">Back-upschema instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="b41d3-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="b41d3-125">VNET-instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="b41d3-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="b41d3-126">App Insights worden niet automatisch ingesteld op de doel-web-app</span><span class="sxs-lookup"><span data-stu-id="b41d3-126">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="b41d3-127">Eenvoudige verificatie-instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="b41d3-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="b41d3-128">Kudu extensie worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="b41d3-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="b41d3-129">TiP regels worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="b41d3-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="b41d3-130">Database-inhoud worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="b41d3-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="b41d3-131">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="b41d3-131">References</span></span>
* [<span data-ttu-id="b41d3-132">Klonen van Web-App met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="b41d3-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="b41d3-133">Back-up van een web-app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b41d3-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="b41d3-134">Een App Service-omgeving maken</span><span class="sxs-lookup"><span data-stu-id="b41d3-134">How to Create an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="b41d3-135">Een web-app maken in een App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="b41d3-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="b41d3-136">Inleiding tot de App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="b41d3-136">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
