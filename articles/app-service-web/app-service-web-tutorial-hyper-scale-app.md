---
title: aaaBuild hyperschaal-app in Azure | Microsoft Docs
description: Meer informatie over hoe toouse verschillende Azure-services toomaximize Hallo prestaties van een ASP.NET-app in Azure.
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="2e110-103">Een hyperschaal web-app in Azure bouwen</span><span class="sxs-lookup"><span data-stu-id="2e110-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="2e110-104">Deze zelfstudie leert u hoe tooscale uit een ASP.NET-web-app in Azure toomaximize gebruiker vraagt.</span><span class="sxs-lookup"><span data-stu-id="2e110-104">This tutorial shows you how tooscale out an ASP.NET web app in Azure toomaximize user requests.</span></span>

<span data-ttu-id="2e110-105">Voordat u deze zelfstudie begint, zorg ervoor dat [hello Azure CLI is geïnstalleerd](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2e110-105">Before starting this tutorial, ensure that [hello Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="2e110-106">U moet bovendien [Visual Studio](https://www.visualstudio.com/vs/) op uw lokale machine toorun Hallo-voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="2e110-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine toorun hello sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="2e110-107">Stap 1 - Get-voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="2e110-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="2e110-108">In deze stap moet u lokale ASP.NET-project Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="2e110-108">In this step, you set up hello local ASP.NET project.</span></span>

### <a name="clone-hello-application-repository"></a><span data-ttu-id="2e110-109">Kloon Hallo toepassing opslagplaats</span><span class="sxs-lookup"><span data-stu-id="2e110-109">Clone hello application repository</span></span>

<span data-ttu-id="2e110-110">Open Hallo opdrachtregelprogramma terminal van uw keuze en `CD` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="2e110-110">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span> <span data-ttu-id="2e110-111">De opdrachten uitvoeren Hallo volgende vervolgens tooclone Hallo-voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="2e110-111">Then, run hello following commands tooclone hello sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a><span data-ttu-id="2e110-112">Hallo-voorbeeldtoepassing uitvoeren in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e110-112">Run hello sample application in Visual Studio</span></span>

<span data-ttu-id="2e110-113">Hallo-oplossing in Visual Studio openen.</span><span class="sxs-lookup"><span data-stu-id="2e110-113">Open hello solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="2e110-114">Type `F5` toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2e110-114">Type `F5` toorun hello application.</span></span>

<span data-ttu-id="2e110-115">In dit voorbeeld ASP.NET-webtoepassing afkomstig is van de standaardsjabloon Hallo en gebruiker sessies en maakt gebruik van Hallo uitvoercache zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="2e110-115">This sample ASP.NET web application comes from hello default template, and persists user sessions and uses hello output cache.</span></span> <span data-ttu-id="2e110-116">Kijk eens naar `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="2e110-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="2e110-117">Hallo `Index()` methode voegt u een stukje gegevens toohello sessie.</span><span class="sxs-lookup"><span data-stu-id="2e110-117">hello `Index()` method adds a piece of data toohello session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="2e110-118">En Hallo `About()` en `Contact()` methoden in de cache de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="2e110-118">And hello `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a><span data-ttu-id="2e110-119">Stap 2: tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="2e110-119">Step 2 - Deploy tooAzure</span></span>
<span data-ttu-id="2e110-120">In deze stap maakt u een Azure-web-app maken en implementeren van uw tooit voorbeeld ASP.NET-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2e110-120">In this step, you create an Azure web app and deploy your sample ASP.NET application tooit.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="2e110-121">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="2e110-121">Create a resource group</span></span>   
<span data-ttu-id="2e110-122">Gebruik [az groep maken](https://docs.microsoft.com/cli/azure/group#create) toocreate een [resourcegroep](../azure-resource-manager/resource-group-overview.md) in de regio West-Europa Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e110-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) toocreate a [resource group](../azure-resource-manager/resource-group-overview.md) in hello West Europe region.</span></span> <span data-ttu-id="2e110-123">Een resourcegroep is waar u alle plaatsen hello Azure-resources dat u wilt dat toomanage samen, zoals back-end Hallo web-app en alle SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="2e110-123">A resource group is where you put all hello Azure resources that you want toomanage together, such as hello web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="2e110-124">toosee welke mogelijke waarden u kunt gebruiken voor `---location`, gebruik Hallo [az appservice lijst-locaties](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) opdracht.</span><span class="sxs-lookup"><span data-stu-id="2e110-124">toosee what possible values you can use for `---location`, use hello [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="2e110-125">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="2e110-125">Create an App Service plan</span></span>
<span data-ttu-id="2e110-126">Gebruik [az appservice-abonnement maken](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate een "B1' [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e110-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="2e110-127">Een App Service-abonnement is een schaaleenheid, met inbegrip van een willekeurig aantal apps dat u tooscale-up wilt of Hallo uit samen over dezelfde App Service-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="2e110-127">An App Service plan is a scale unit, which can include any number of apps that you want tooscale up or out together over hello same App Service infrastructure.</span></span> <span data-ttu-id="2e110-128">Elk plan is ook toegewezen een [prijscategorie](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="2e110-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="2e110-129">Hogere lagen bevatten betere hardware- en meer functies, zoals meer exemplaren van de scale-out.</span><span class="sxs-lookup"><span data-stu-id="2e110-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="2e110-130">Voor deze zelfstudie is B1 Hallo minimale laag waarmee scale-out toothree exemplaren.</span><span class="sxs-lookup"><span data-stu-id="2e110-130">For this tutorial, B1 is hello minimum tier that enables scale out toothree instances.</span></span> <span data-ttu-id="2e110-131">U kunt uw app altijd verplaatsen omhoog of omlaag Hallo prijscategorie later door te voeren [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="2e110-131">You can always move your app up or down hello pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="2e110-132">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="2e110-132">Create a web app</span></span>
<span data-ttu-id="2e110-133">Gebruik [az appservice web maken](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate een web-app met een unieke naam in `$appName`.</span><span class="sxs-lookup"><span data-stu-id="2e110-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="2e110-134">Implementatiereferenties instellen</span><span class="sxs-lookup"><span data-stu-id="2e110-134">Set deployment credentials</span></span>
<span data-ttu-id="2e110-135">Gebruik [az appservice web implementatiegebruiker ingesteld](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset inzetten van uw account referenties voor App Service.</span><span class="sxs-lookup"><span data-stu-id="2e110-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="2e110-136">Configureer Git-implementatie</span><span class="sxs-lookup"><span data-stu-id="2e110-136">Configure Git deployment</span></span>
<span data-ttu-id="2e110-137">Gebruik [-broncodebeheer in az appservice web-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure lokale Git-implementatie.</span><span class="sxs-lookup"><span data-stu-id="2e110-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="2e110-138">Met deze opdracht kunt u een uitvoer die op Hallo volgende lijkt:</span><span class="sxs-lookup"><span data-stu-id="2e110-138">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="2e110-139">Gebruik Hallo geretourneerd URL tooconfigure uw Git remote.</span><span class="sxs-lookup"><span data-stu-id="2e110-139">Use hello returned URL tooconfigure your Git remote.</span></span> <span data-ttu-id="2e110-140">Hallo volgende opdracht maakt gebruik van Hallo voorgaande voorbeeld van uitvoer.</span><span class="sxs-lookup"><span data-stu-id="2e110-140">hello following command uses hello preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a><span data-ttu-id="2e110-141">Hallo-voorbeeldtoepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="2e110-141">Deploy hello sample application</span></span>
<span data-ttu-id="2e110-142">U bent nu klaar toodeploy uw voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="2e110-142">You are now ready toodeploy your sample application.</span></span> <span data-ttu-id="2e110-143">Voer `git push` uit.</span><span class="sxs-lookup"><span data-stu-id="2e110-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="2e110-144">Wanneer gevraagd om een wachtwoord, hello wachtwoord gebruiken dat u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="2e110-144">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-tooazure-web-app"></a><span data-ttu-id="2e110-145">TooAzure web-app bladeren</span><span class="sxs-lookup"><span data-stu-id="2e110-145">Browse tooAzure web app</span></span>
<span data-ttu-id="2e110-146">Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee voor uw app live in Azure, met deze opdracht uitvoert.</span><span class="sxs-lookup"><span data-stu-id="2e110-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a><span data-ttu-id="2e110-147">Stap 3: verbinding maken met tooRedis</span><span class="sxs-lookup"><span data-stu-id="2e110-147">Step 3 - Connect tooRedis</span></span>
<span data-ttu-id="2e110-148">In deze stap maakt instellen u Azure Redis-Cache als een externe, geplaatste cache tooyour Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="2e110-148">In this step, you set up Azure Redis Cache as an external, colocated cache tooyour Azure web app.</span></span> <span data-ttu-id="2e110-149">U kunt snel gebruikmaken van Redis toocache uw pagina-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="2e110-149">You can quickly utilize Redis toocache your page output.</span></span> <span data-ttu-id="2e110-150">Bovendien wanneer u later uit uw web-apps schaalt, Redis helpt u behouden gebruikerssessies over meerdere exemplaren op betrouwbare wijze.</span><span class="sxs-lookup"><span data-stu-id="2e110-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="2e110-151">Maak een Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="2e110-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="2e110-152">Gebruik [az redis maken](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate in een Azure Redis-Cache en slaat u Hallo JSON-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="2e110-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate an Azure Redis Cache and save hello JSON output.</span></span> <span data-ttu-id="2e110-153">Gebruik een unieke naam in `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="2e110-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a><span data-ttu-id="2e110-154">Hallo toepassing toouse Redis configureren</span><span class="sxs-lookup"><span data-stu-id="2e110-154">Configure hello application toouse Redis</span></span>
<span data-ttu-id="2e110-155">Hallo-verbindingsreeks voor uw cache-notatie.</span><span class="sxs-lookup"><span data-stu-id="2e110-155">Format hello connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="2e110-156">Hallo tweede regel geeft u een uitvoer die er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="2e110-156">hello second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="2e110-157">Maak in Visual Studio een web-configuratiebestand in de hoofdmap van uw project aangeroepen `redis.config` en plakken Hallo de volgende code in de App.</span><span class="sxs-lookup"><span data-stu-id="2e110-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste hello following code into it.</span></span> <span data-ttu-id="2e110-158">In `value`, Hallo-verbindingsreeks uit Hallo uitvoer van PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2e110-158">In `value`, use hello connection string from hello PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="2e110-159">Als u hello bekijkt `.gitignore` bestand in de Git-opslagplaats, ziet u dat dit bestand is uitgesloten van broncodebeheer.</span><span class="sxs-lookup"><span data-stu-id="2e110-159">If you look at hello `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="2e110-160">Op die manier uw vertrouwelijke gegevens veilig blijft.</span><span class="sxs-lookup"><span data-stu-id="2e110-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="2e110-161">Open `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="2e110-161">Open `Web.config`.</span></span> <span data-ttu-id="2e110-162">Kennisgeving Hallo `<appSettings file="redis.config">` -element opgehaald Hallo-instelling die u hebt gemaakt in `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="2e110-162">Notice hello `<appSettings file="redis.config">` element, which gets hello setting you created in `redis.config`.</span></span> 

<span data-ttu-id="2e110-163">Hallo opmerkingen vinden sectie `<sessionState>` en `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="2e110-163">Find hello commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="2e110-164">Verwijder de opmerkingen in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="2e110-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="2e110-165">Deze code lijkt voor Hallo Redis-verbindingsreeks die u hebt gedefinieerd in `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="2e110-165">This code looks for hello Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="2e110-166">Nu uw toepassing maakt gebruik van Redis toomanage sessies en opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="2e110-166">Your application now uses Redis toomanage sessions and caching.</span></span> <span data-ttu-id="2e110-167">Type `F5` toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2e110-167">Type `F5` toorun hello application.</span></span> <span data-ttu-id="2e110-168">Indien gewenst, kunt u downloaden van een Redis-client toovisualize Hallo beheergegevens dat nu toohello cache is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2e110-168">If you like, you can download a Redis management client toovisualize hello data that is now saved toohello cache.</span></span>

### <a name="configure-hello-connection-string-in-azure"></a><span data-ttu-id="2e110-169">Hallo-verbindingsreeks configureren in Azure</span><span class="sxs-lookup"><span data-stu-id="2e110-169">Configure hello connection string in Azure</span></span>

<span data-ttu-id="2e110-170">Voor uw toepassing toowork in Azure, moet u tooconfigure Hallo dezelfde Redis-verbindingsreeks in uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="2e110-170">For your application toowork in Azure, you need tooconfigure hello same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="2e110-171">Aangezien `redis.config` niet behouden in broncodebeheer, het is niet geïmplementeerd tooAzure tijdens het uitvoeren van Git-implementatie.</span><span class="sxs-lookup"><span data-stu-id="2e110-171">Since `redis.config` is not maintained in source control, it is not deployed tooAzure when you run Git deployment.</span></span>

<span data-ttu-id="2e110-172">Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd Hallo connection string Hello dezelfde naam (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="2e110-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello connection string with hello same name (`RedisConnection`).</span></span>

<span data-ttu-id="2e110-173">AZ appservice webconfiguratie appsettings bijwerken--instellingen ' RedisConnection $connstring = '--$appName--resourcegroep myResourceGroup naam</span><span class="sxs-lookup"><span data-stu-id="2e110-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="2e110-174">Vergeet niet dat `$connstring` Hallo geformatteerd-verbindingsreeks bevat.</span><span class="sxs-lookup"><span data-stu-id="2e110-174">Remember that `$connstring` contains hello formatted connection string.</span></span>

### <a name="redeploy-hello-application-tooazure"></a><span data-ttu-id="2e110-175">Hallo toepassing tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="2e110-175">Redeploy hello application tooAzure</span></span>
<span data-ttu-id="2e110-176">Uw wijzigingen tooAzure voor Git-opdrachten toopush gebruiken</span><span class="sxs-lookup"><span data-stu-id="2e110-176">Use Git commands toopush your changes tooAzure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="2e110-177">Wanneer gevraagd om een wachtwoord, hello wachtwoord gebruiken dat u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="2e110-177">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="2e110-178">Toohello Azure-web-app bladeren</span><span class="sxs-lookup"><span data-stu-id="2e110-178">Browse toohello Azure web app</span></span>
<span data-ttu-id="2e110-179">Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee Hallo wijzigingen live in Azure.</span><span class="sxs-lookup"><span data-stu-id="2e110-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a><span data-ttu-id="2e110-180">Stap 4: Scale toomultiple exemplaren</span><span class="sxs-lookup"><span data-stu-id="2e110-180">Step 4 - Scale toomultiple instances</span></span>
<span data-ttu-id="2e110-181">Hallo App Service-abonnement is Hallo schaaleenheid voor uw Azure-web-apps.</span><span class="sxs-lookup"><span data-stu-id="2e110-181">hello App Service plan is hello scale unit for your Azure web apps.</span></span> <span data-ttu-id="2e110-182">tooscale uit uw web-app u schalen Hallo App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2e110-182">tooscale out your web app, you scale hello App Service plan.</span></span>

<span data-ttu-id="2e110-183">Gebruik [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale uit Hallo App Service plan toothree exemplaren die Hallo maximaal toegestane aantal door Hallo B1 prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="2e110-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale out hello App Service plan toothree instances, which is hello maximum number allowed by hello B1 pricing tier.</span></span> <span data-ttu-id="2e110-184">Denk eraan dat B1 Hallo prijscategorie die u hebt gekozen toen u Hallo eerder App Service-abonnement hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2e110-184">Remember that B1 is hello pricing tier that you chose when you created hello App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="2e110-185">Stap 5: Scale geografisch</span><span class="sxs-lookup"><span data-stu-id="2e110-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="2e110-186">Tijdens het geografisch schalen, kunt u uw app uitvoeren in meerdere regio's van hello Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="2e110-186">When scaling geographically, you run your app in multiple regions of hello Azure cloud.</span></span> <span data-ttu-id="2e110-187">Deze setup taakverdelingen van uw app verder op basis van Geografie en verlaagt de reactietijd van Hallo door het plaatsen van uw app dichter tooclient browsers.</span><span class="sxs-lookup"><span data-stu-id="2e110-187">This setup load-balances your app further based on geography and lowers hello response time by placing your app closer tooclient browsers.</span></span>

<span data-ttu-id="2e110-188">In deze stap maakt u uw ASP.NET web app tooa tweede regio met schalen [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="2e110-188">In this step, you scale your ASP.NET web app tooa second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="2e110-189">Aan het einde van de Hallo van Hallo stap hebt u een web-app uitgevoerd in West-Europa (al gemaakt) en een web-app uitgevoerd in Zuidoost-Azië (nog niet gemaakt).</span><span class="sxs-lookup"><span data-stu-id="2e110-189">At hello end of hello step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="2e110-190">Beide apps kunnen worden geleverd vanuit Hallo dezelfde Traffic Manager-URL.</span><span class="sxs-lookup"><span data-stu-id="2e110-190">Both apps will be served from hello same Traffic Manager URL.</span></span>

### <a name="scale-up-hello-europe-app-toostandard-tier"></a><span data-ttu-id="2e110-191">Hallo opschalen met Europa app tooStandard-laag</span><span class="sxs-lookup"><span data-stu-id="2e110-191">Scale up hello Europe app tooStandard tier</span></span>
<span data-ttu-id="2e110-192">Integratie met Azure Traffic Manager vereist in App Service Hallo standaardcategorie prijzen.</span><span class="sxs-lookup"><span data-stu-id="2e110-192">In App Service, integration with Azure Traffic Manager requires hello Standard pricing tier.</span></span> <span data-ttu-id="2e110-193">Gebruik [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale van uw App Service plan tooS1.</span><span class="sxs-lookup"><span data-stu-id="2e110-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale up your App Service plan tooS1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="2e110-194">Een Traffic Manager-profiel maken</span><span class="sxs-lookup"><span data-stu-id="2e110-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="2e110-195">Gebruik [az netwerk traffic manager-profiel maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate een Traffic Manager-profiel en toe te voegen tooyour resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2e110-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate a Traffic Manager profile and add it tooyour resource group.</span></span> <span data-ttu-id="2e110-196">Gebruik een unieke DNS-naam in $dnsName.</span><span class="sxs-lookup"><span data-stu-id="2e110-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="2e110-197">`--routing-method Performance`Hiermee wordt aangegeven dat dit profiel [gebruiker verkeer toohello dichtstbijzijnde endpoint van routes](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="2e110-197">`--routing-method Performance` specifies that this profile [routes user traffic toohello closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-hello-resource-id-of-hello-europe-app"></a><span data-ttu-id="2e110-198">Hallo resource-ID van Hallo Europa app verkrijgen</span><span class="sxs-lookup"><span data-stu-id="2e110-198">Get hello resource ID of hello Europe app</span></span>
<span data-ttu-id="2e110-199">Gebruik [az appservice web weergeven](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Hallo bron-ID van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="2e110-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a><span data-ttu-id="2e110-200">Een Traffic Manager-eindpunt voor Hallo Europa app toevoegen</span><span class="sxs-lookup"><span data-stu-id="2e110-200">Add a Traffic Manager endpoint for hello Europe app</span></span>
<span data-ttu-id="2e110-201">Gebruik [netwerkeindpunt voor het traffic manager az maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd een eindpunt tooyour Traffic Manager-profiel en gebruik Hallo bron-ID van uw web-app als doel Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e110-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd an endpoint tooyour Traffic Manager profile and use hello resource ID of your web app as hello target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a><span data-ttu-id="2e110-202">Hallo Traffic Manager-eindpunt-URL ophalen</span><span class="sxs-lookup"><span data-stu-id="2e110-202">Get hello Traffic Manager endpoint URL</span></span>
<span data-ttu-id="2e110-203">Uw Traffic Manager-profiel heeft nu een eindpunt dat punten tooyour bestaande web-app.</span><span class="sxs-lookup"><span data-stu-id="2e110-203">Your Traffic Manager profile now has an endpoint that points tooyour existing web app.</span></span> <span data-ttu-id="2e110-204">Gebruik [az netwerk traffic manager-profiel weergeven](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget de URL.</span><span class="sxs-lookup"><span data-stu-id="2e110-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="2e110-205">Hallo-uitvoer in uw browser kopiëren.</span><span class="sxs-lookup"><span data-stu-id="2e110-205">Copy hello output into your browser.</span></span> <span data-ttu-id="2e110-206">U ziet uw web-app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="2e110-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="2e110-207">Maken van een Azure Redis-Cache in Azië</span><span class="sxs-lookup"><span data-stu-id="2e110-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="2e110-208">Nu u uw Azure-web-app toohello Zuidoost-Azië regio worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="2e110-208">Now, you replicate your Azure web app toohello Southeast Asia region.</span></span> <span data-ttu-id="2e110-209">toostart, gebruik [az redis maken](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate een tweede Azure Redis-Cache in Zuidoost-Azië.</span><span class="sxs-lookup"><span data-stu-id="2e110-209">toostart, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="2e110-210">Deze cache moet toobe die met uw app in Azië ditzelfde geplaatst.</span><span class="sxs-lookup"><span data-stu-id="2e110-210">This cache needs toobe colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="2e110-211">`--name $cacheName-asia`biedt Hallo Hallo Cachenaam Hallo cache West-Europa, Hello `-asia` achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="2e110-211">`--name $cacheName-asia` gives hello cache hello name of hello West Europe cache, with hello `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="2e110-212">Maken van een App Service-plan in Azië</span><span class="sxs-lookup"><span data-stu-id="2e110-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="2e110-213">Gebruik [az appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate een tweede App Service-plan in Hallo Zuidoost-Azië regio, met behulp van Hallo dezelfde S1 trapsgewijs als Hallo West-Europa plan.</span><span class="sxs-lookup"><span data-stu-id="2e110-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate a second App Service plan in hello Southeast Asia region, using hello same S1 tier as hello West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="2e110-214">Een web-app maken in Azië</span><span class="sxs-lookup"><span data-stu-id="2e110-214">Create a web app in Asia</span></span>
<span data-ttu-id="2e110-215">Gebruik [az appservice web maken](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate een tweede web-app.</span><span class="sxs-lookup"><span data-stu-id="2e110-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="2e110-216">`--name $appName-asia`Geeft app Hallo-naam van app Hallo-West-Europa, Hallo Hello `-asia` achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="2e110-216">`--name $appName-asia` gives hello app hello name of hello West Europe app, with hello `-asia` suffix.</span></span>

### <a name="configure-hello-connection-string-for-redis"></a><span data-ttu-id="2e110-217">Hallo-verbindingsreeks configureren voor Redis</span><span class="sxs-lookup"><span data-stu-id="2e110-217">Configure hello connection string for Redis</span></span>
<span data-ttu-id="2e110-218">Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app Hallo verbindingsreeks voor Hallo cache Zuidoost-Azië.</span><span class="sxs-lookup"><span data-stu-id="2e110-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connection string for hello Southeast Asia cache.</span></span>

<span data-ttu-id="2e110-219">AZ appservice webconfiguratie appsettings bijwerken--instellingen ' RedisConnection = $($redis.hostname): $($redis.sslPort), wachtwoord = $($redis.accessKeys.primaryKey), ssl = True, abortConnect = False '--naam $appName-Azië--resourcegroep myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2e110-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-hello-asia-app"></a><span data-ttu-id="2e110-220">Configureer Git-implementatie voor Hallo Azië app.</span><span class="sxs-lookup"><span data-stu-id="2e110-220">Configure Git deployment for hello Asia app.</span></span>
<span data-ttu-id="2e110-221">Gebruik [-broncodebeheer in az appservice web-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure lokale Git-implementatie voor Hallo tweede web-app.</span><span class="sxs-lookup"><span data-stu-id="2e110-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment for hello second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="2e110-222">Met deze opdracht kunt u een uitvoer die op Hallo volgende lijkt:</span><span class="sxs-lookup"><span data-stu-id="2e110-222">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="2e110-223">Gebruik Hallo geretourneerd URL tooconfigure een tweede Git extern voor uw lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="2e110-223">Use hello returned URL tooconfigure a second Git remote for your local repository.</span></span> <span data-ttu-id="2e110-224">Hallo volgende opdracht maakt gebruik van Hallo voorgaande voorbeeld van uitvoer.</span><span class="sxs-lookup"><span data-stu-id="2e110-224">hello following command uses hello preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="2e110-225">Uw voorbeeldtoepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="2e110-225">Deploy your sample application</span></span>
<span data-ttu-id="2e110-226">Voer `git push` toodeploy uw voorbeeld toepassing toohello tweede Git remote.</span><span class="sxs-lookup"><span data-stu-id="2e110-226">Run `git push` toodeploy your sample application toohello second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="2e110-227">Wanneer gevraagd om een wachtwoord, hello wachtwoord gebruiken dat u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="2e110-227">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-asia-app"></a><span data-ttu-id="2e110-228">Toohello Azië app bladeren</span><span class="sxs-lookup"><span data-stu-id="2e110-228">Browse toohello Asia app</span></span>
<span data-ttu-id="2e110-229">Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify die uw app live in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2e110-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a><span data-ttu-id="2e110-230">Hallo resource-ID van Hallo Azië app verkrijgen</span><span class="sxs-lookup"><span data-stu-id="2e110-230">Get hello resource ID of hello Asia app</span></span>
<span data-ttu-id="2e110-231">Gebruik [az appservice web weergeven](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Hallo bron-ID van uw web-app in Zuidoost-Azië.</span><span class="sxs-lookup"><span data-stu-id="2e110-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a><span data-ttu-id="2e110-232">Een Traffic Manager-eindpunt voor Hallo Azië app toevoegen</span><span class="sxs-lookup"><span data-stu-id="2e110-232">Add a Traffic Manager endpoint for hello Asia app</span></span>
<span data-ttu-id="2e110-233">Gebruik [netwerkeindpunt voor het traffic manager az maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd een tweede eindpunt toohello Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="2e110-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd a second endpoint toohello Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a><span data-ttu-id="2e110-234">Regio id tooweb apps toevoegen</span><span class="sxs-lookup"><span data-stu-id="2e110-234">Add region identifier tooweb apps</span></span>
<span data-ttu-id="2e110-235">Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd een regiospecifiek omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="2e110-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="2e110-236">Deze toepassingsinstelling wordt al gebruikt door de toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="2e110-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="2e110-237">Kijk eens naar `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2e110-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="2e110-238">Voltooid!</span><span class="sxs-lookup"><span data-stu-id="2e110-238">Complete!</span></span>

<span data-ttu-id="2e110-239">Probeer nu tooaccess Hallo-URL van uw Traffic Manager-profiel van browsers in verschillende geografische regio's.</span><span class="sxs-lookup"><span data-stu-id="2e110-239">Now, try tooaccess hello URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="2e110-240">Clientbrowsers van Europa moeten weergeven 'ASP.NET West-Europa' en 'ASP.NET Zuidoost-Azië.' moet worden weergegeven in de browser van de client vanuit Azië</span><span class="sxs-lookup"><span data-stu-id="2e110-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="2e110-241">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="2e110-241">More resources</span></span>
