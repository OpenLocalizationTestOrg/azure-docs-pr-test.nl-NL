---
title: Een hyperschaal-app in Azure bouwen | Microsoft Docs
description: Informatie over het gebruik van andere Azure-services voor de prestaties van een ASP.NET-app in Azure.
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
ms.openlocfilehash: eac9c5b0d8d0f7802d88e6f4f27d9d23c406e025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="c4d1b-103">Een hyperschaal web-app in Azure bouwen</span><span class="sxs-lookup"><span data-stu-id="c4d1b-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="c4d1b-104">Deze zelfstudie laat zien hoe u uit een ASP.NET-web-app in Azure om te maximaliseren gebruikersaanvragen te schalen.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-104">This tutorial shows you how to scale out an ASP.NET web app in Azure to maximize user requests.</span></span>

<span data-ttu-id="c4d1b-105">Voordat u deze zelfstudie begint, zorg ervoor dat [is geïnstalleerd met de Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) op uw computer.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-105">Before starting this tutorial, ensure that [the Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="c4d1b-106">U moet bovendien [Visual Studio](https://www.visualstudio.com/vs/) op uw lokale machine worden uitgevoerd van de voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine to run the sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="c4d1b-107">Stap 1 - Get-voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="c4d1b-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="c4d1b-108">In deze stap moet u het lokale ASP.NET-project instellen.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-108">In this step, you set up the local ASP.NET project.</span></span>

### <a name="clone-the-application-repository"></a><span data-ttu-id="c4d1b-109">Kloon de opslagplaats toepassing</span><span class="sxs-lookup"><span data-stu-id="c4d1b-109">Clone the application repository</span></span>

<span data-ttu-id="c4d1b-110">Open de van uw keuze en `CD` in een werkmap.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-110">Open the command-line terminal of your choice and `CD` to a working directory.</span></span> <span data-ttu-id="c4d1b-111">Voer de volgende opdrachten voor het klonen van de voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-111">Then, run the following commands to clone the sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a><span data-ttu-id="c4d1b-112">De voorbeeldtoepassing uitvoert in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4d1b-112">Run the sample application in Visual Studio</span></span>

<span data-ttu-id="c4d1b-113">Open de oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-113">Open the solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="c4d1b-114">Type `F5` de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-114">Type `F5` to run the application.</span></span>

<span data-ttu-id="c4d1b-115">In dit voorbeeld ASP.NET-webtoepassing afkomstig is van de standaardsjabloon en de gebruiker zich blijft voordoen sessies en maakt gebruik van de uitvoercache.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-115">This sample ASP.NET web application comes from the default template, and persists user sessions and uses the output cache.</span></span> <span data-ttu-id="c4d1b-116">Kijk eens naar `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="c4d1b-117">De `Index()` methode wordt een stukje informatie toegevoegd aan de sessie.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-117">The `Index()` method adds a piece of data to the session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="c4d1b-118">En de `About()` en `Contact()` methoden in de cache de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-118">And the `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a><span data-ttu-id="c4d1b-119">Stap 2 - implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="c4d1b-119">Step 2 - Deploy to Azure</span></span>
<span data-ttu-id="c4d1b-120">In deze stap maakt u een Azure-web-app maken en uw voorbeeld ASP.NET-toepassing te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-120">In this step, you create an Azure web app and deploy your sample ASP.NET application to it.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="c4d1b-121">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="c4d1b-121">Create a resource group</span></span>   
<span data-ttu-id="c4d1b-122">Gebruik [az groep maken](https://docs.microsoft.com/cli/azure/group#create) maken een [resourcegroep](../azure-resource-manager/resource-group-overview.md) in de regio West-Europa.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) to create a [resource group](../azure-resource-manager/resource-group-overview.md) in the West Europe region.</span></span> <span data-ttu-id="c4d1b-123">Een resourcegroep is waar het plaatsen van alle Azure-resources die u beheren, wilt zoals de web-app en alle SQL-databases back-end.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-123">A resource group is where you put all the Azure resources that you want to manage together, such as the web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="c4d1b-124">Om te zien welke mogelijke waarden die u hebt, kunnen gebruiken voor `---location`, gebruiken de [az appservice lijst-locaties](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) opdracht.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-124">To see what possible values you can use for `---location`, use the [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="c4d1b-125">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="c4d1b-125">Create an App Service plan</span></span>
<span data-ttu-id="c4d1b-126">Gebruik [az appservice-abonnement maken](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) voor het maken van een "B1' [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4d1b-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) to create a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="c4d1b-127">Een App Service-abonnement is een schaaleenheid, met inbegrip van een willekeurig aantal apps dat u wilt omhoog of omlaag schalen samen via dezelfde App Service-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-127">An App Service plan is a scale unit, which can include any number of apps that you want to scale up or out together over the same App Service infrastructure.</span></span> <span data-ttu-id="c4d1b-128">Elk plan is ook toegewezen een [prijscategorie](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="c4d1b-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="c4d1b-129">Hogere lagen bevatten betere hardware- en meer functies, zoals meer exemplaren van de scale-out.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="c4d1b-130">Voor deze zelfstudie is B1 de minimale laag waarmee de gebeurtenis uitschalen naar drie exemplaren.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-130">For this tutorial, B1 is the minimum tier that enables scale out to three instances.</span></span> <span data-ttu-id="c4d1b-131">U kunt altijd uw app omhoog of omlaag verplaatsen de prijscategorie later door te voeren [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="c4d1b-131">You can always move your app up or down the pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="c4d1b-132">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="c4d1b-132">Create a web app</span></span>
<span data-ttu-id="c4d1b-133">Gebruik [az appservice web maken](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) een web-app maken met een unieke naam in `$appName`.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="c4d1b-134">Implementatiereferenties instellen</span><span class="sxs-lookup"><span data-stu-id="c4d1b-134">Set deployment credentials</span></span>
<span data-ttu-id="c4d1b-135">Gebruik [az appservice web implementatiegebruiker ingesteld](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) uw account niveau implementatiereferenties instellen voor App Service.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) to set your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="c4d1b-136">Configureer Git-implementatie</span><span class="sxs-lookup"><span data-stu-id="c4d1b-136">Configure Git deployment</span></span>
<span data-ttu-id="c4d1b-137">Gebruik [-broncodebeheer in az appservice web-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) om lokale Git-implementatie te configureren.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="c4d1b-138">Met deze opdracht kunt u een uitvoer die op het volgende lijkt:</span><span class="sxs-lookup"><span data-stu-id="c4d1b-138">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="c4d1b-139">De geretourneerde URL gebruiken voor het configureren van uw externe Git.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-139">Use the returned URL to configure your Git remote.</span></span> <span data-ttu-id="c4d1b-140">De volgende opdracht maakt gebruik van het vorige Uitvoervoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-140">The following command uses the preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a><span data-ttu-id="c4d1b-141">De voorbeeldtoepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="c4d1b-141">Deploy the sample application</span></span>
<span data-ttu-id="c4d1b-142">U bent nu klaar voor het implementeren van uw voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-142">You are now ready to deploy your sample application.</span></span> <span data-ttu-id="c4d1b-143">Voer `git push` uit.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="c4d1b-144">Wanneer wachtwoord wordt gevraagd, gebruikt u het wachtwoord die u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-144">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-azure-web-app"></a><span data-ttu-id="c4d1b-145">Blader naar de Azure-web-app</span><span class="sxs-lookup"><span data-stu-id="c4d1b-145">Browse to Azure web app</span></span>
<span data-ttu-id="c4d1b-146">Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) overzicht van uw app live in Azure met deze opdracht uitvoert.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a><span data-ttu-id="c4d1b-147">Stap 3: verbinding maken met Redis</span><span class="sxs-lookup"><span data-stu-id="c4d1b-147">Step 3 - Connect to Redis</span></span>
<span data-ttu-id="c4d1b-148">In deze stap maakt instellen u Azure Redis-Cache als een externe, geplaatste cache aan uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-148">In this step, you set up Azure Redis Cache as an external, colocated cache to your Azure web app.</span></span> <span data-ttu-id="c4d1b-149">Snel kunt u gebruikmaken van Redis cache opslaan van uw pagina-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-149">You can quickly utilize Redis to cache your page output.</span></span> <span data-ttu-id="c4d1b-150">Bovendien wanneer u later uit uw web-apps schaalt, Redis helpt u behouden gebruikerssessies over meerdere exemplaren op betrouwbare wijze.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="c4d1b-151">Maak een Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="c4d1b-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="c4d1b-152">Gebruik [az redis maken](https://docs.microsoft.com/en-us/cli/azure/redis#create) maken van een Azure Redis-Cache en opslaan van de JSON-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create an Azure Redis Cache and save the JSON output.</span></span> <span data-ttu-id="c4d1b-153">Gebruik een unieke naam in `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a><span data-ttu-id="c4d1b-154">De toepassing configureren voor het gebruik van Redis</span><span class="sxs-lookup"><span data-stu-id="c4d1b-154">Configure the application to use Redis</span></span>
<span data-ttu-id="c4d1b-155">De verbindingsreeks voor uw cache-notatie.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-155">Format the connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="c4d1b-156">De tweede regel geeft u een uitvoer die er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="c4d1b-156">The second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="c4d1b-157">Maak in Visual Studio een web-configuratiebestand in de hoofdmap van uw project aangeroepen `redis.config` en plak de volgende code in de App.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste the following code into it.</span></span> <span data-ttu-id="c4d1b-158">In `value`, gebruikt u de verbindingsreeks van de PowerShell-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-158">In `value`, use the connection string from the PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="c4d1b-159">Als u naar kijkt de `.gitignore` bestand in de Git-opslagplaats, ziet u dat dit bestand is uitgesloten van broncodebeheer.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-159">If you look at the `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="c4d1b-160">Op die manier uw vertrouwelijke gegevens veilig blijft.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="c4d1b-161">Open `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-161">Open `Web.config`.</span></span> <span data-ttu-id="c4d1b-162">U ziet de `<appSettings file="redis.config">` element, dat de instelling die u hebt gemaakt in opgehaald `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-162">Notice the `<appSettings file="redis.config">` element, which gets the setting you created in `redis.config`.</span></span> 

<span data-ttu-id="c4d1b-163">Zoek de opmerkingen sectie waarin `<sessionState>` en `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-163">Find the commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="c4d1b-164">Verwijder de opmerkingen in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="c4d1b-165">Deze code eruitziet voor de Redis-verbindingsreeks die u hebt gedefinieerd in `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-165">This code looks for the Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="c4d1b-166">Nu uw toepassing maakt gebruik van Redis voor het beheren van sessies en opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-166">Your application now uses Redis to manage sessions and caching.</span></span> <span data-ttu-id="c4d1b-167">Type `F5` de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-167">Type `F5` to run the application.</span></span> <span data-ttu-id="c4d1b-168">Indien gewenst, kunt u downloaden van een Redis-management-client om de gegevens die nu wordt opgeslagen in de cache.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-168">If you like, you can download a Redis management client to visualize the data that is now saved to the cache.</span></span>

### <a name="configure-the-connection-string-in-azure"></a><span data-ttu-id="c4d1b-169">De verbindingsreeks configureren in Azure</span><span class="sxs-lookup"><span data-stu-id="c4d1b-169">Configure the connection string in Azure</span></span>

<span data-ttu-id="c4d1b-170">Voor uw toepassing uit te voeren in Azure, moet u de dezelfde Redis-verbindingsreeks configureren in uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-170">For your application to work in Azure, you need to configure the same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="c4d1b-171">Aangezien `redis.config` niet behouden in broncodebeheer, wordt niet geïmplementeerd in Azure tijdens het uitvoeren van Git-implementatie.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-171">Since `redis.config` is not maintained in source control, it is not deployed to Azure when you run Git deployment.</span></span>

<span data-ttu-id="c4d1b-172">Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) om toe te voegen van de verbindingsreeks met dezelfde naam (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="c4d1b-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add the connection string with the same name (`RedisConnection`).</span></span>

<span data-ttu-id="c4d1b-173">AZ appservice webconfiguratie appsettings bijwerken--instellingen ' RedisConnection $connstring = '--$appName--resourcegroep myResourceGroup naam</span><span class="sxs-lookup"><span data-stu-id="c4d1b-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="c4d1b-174">Vergeet niet dat `$connstring` de opgemaakte verbindingsreeks bevat.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-174">Remember that `$connstring` contains the formatted connection string.</span></span>

### <a name="redeploy-the-application-to-azure"></a><span data-ttu-id="c4d1b-175">De toepassing in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="c4d1b-175">Redeploy the application to Azure</span></span>
<span data-ttu-id="c4d1b-176">Git-opdrachten gebruiken om uw wijzigingen naar Azure</span><span class="sxs-lookup"><span data-stu-id="c4d1b-176">Use Git commands to push your changes to Azure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="c4d1b-177">Wanneer wachtwoord wordt gevraagd, gebruikt u het wachtwoord die u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-177">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="c4d1b-178">Blader naar de Azure-web-app</span><span class="sxs-lookup"><span data-stu-id="c4d1b-178">Browse to the Azure web app</span></span>
<span data-ttu-id="c4d1b-179">Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) live in Azure wijzigingen kunnen zien.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see the changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a><span data-ttu-id="c4d1b-180">Stap 4: Scale naar meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="c4d1b-180">Step 4 - Scale to multiple instances</span></span>
<span data-ttu-id="c4d1b-181">De App Service-abonnement is de schaaleenheid voor uw Azure-web-apps.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-181">The App Service plan is the scale unit for your Azure web apps.</span></span> <span data-ttu-id="c4d1b-182">Als u wilt uitbreiden uw web-app, moet u de App Service-abonnement schalen.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-182">To scale out your web app, you scale the App Service plan.</span></span>

<span data-ttu-id="c4d1b-183">Gebruik [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update) moet worden uitgebreid met de App Service-abonnement naar drie exemplaren die het maximumaantal dat is toegestaan door de prijscategorie B1.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale out the App Service plan to three instances, which is the maximum number allowed by the B1 pricing tier.</span></span> <span data-ttu-id="c4d1b-184">Denk eraan dat B1 de prijscategorie die u hebt gekozen toen u de App Service-abonnement eerder gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-184">Remember that B1 is the pricing tier that you chose when you created the App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="c4d1b-185">Stap 5: Scale geografisch</span><span class="sxs-lookup"><span data-stu-id="c4d1b-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="c4d1b-186">Tijdens het geografisch schalen, kunt u uw app uitvoeren in meerdere regio's van de Azure-cloud.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-186">When scaling geographically, you run your app in multiple regions of the Azure cloud.</span></span> <span data-ttu-id="c4d1b-187">Deze setup taakverdelingen van uw app verder op basis van Geografie en verlaagt de reactietijd van de door het plaatsen van uw app dichter clientbrowsers.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-187">This setup load-balances your app further based on geography and lowers the response time by placing your app closer to client browsers.</span></span>

<span data-ttu-id="c4d1b-188">In deze stap maakt u uw ASP.NET-web-app in een tweede regio met schalen [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="c4d1b-188">In this step, you scale your ASP.NET web app to a second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="c4d1b-189">Aan het einde van de stap hebt u een web-app uitgevoerd in West-Europa (al gemaakt) en een web-app uitgevoerd in Zuidoost-Azië (nog niet gemaakt).</span><span class="sxs-lookup"><span data-stu-id="c4d1b-189">At the end of the step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="c4d1b-190">Beide apps kunnen worden geleverd vanuit dezelfde Traffic Manager-URL.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-190">Both apps will be served from the same Traffic Manager URL.</span></span>

### <a name="scale-up-the-europe-app-to-standard-tier"></a><span data-ttu-id="c4d1b-191">De app Europa standaardcategorie opschalen</span><span class="sxs-lookup"><span data-stu-id="c4d1b-191">Scale up the Europe app to Standard tier</span></span>
<span data-ttu-id="c4d1b-192">Integratie met Azure Traffic Manager vereist in App Service, de Standard-prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-192">In App Service, integration with Azure Traffic Manager requires the Standard pricing tier.</span></span> <span data-ttu-id="c4d1b-193">Gebruik [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update) naar uw App Service-abonnement S1 opschalen.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale up your App Service plan to S1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="c4d1b-194">Een Traffic Manager-profiel maken</span><span class="sxs-lookup"><span data-stu-id="c4d1b-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="c4d1b-195">Gebruik [az netwerk traffic manager-profiel maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) een Traffic Manager-profiel maken en toe te voegen aan de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) to create a Traffic Manager profile and add it to your resource group.</span></span> <span data-ttu-id="c4d1b-196">Gebruik een unieke DNS-naam in $dnsName.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="c4d1b-197">`--routing-method Performance`Hiermee wordt aangegeven dat dit profiel [gebruikersverkeer gerouteerd naar het dichtstbijzijnde eindpunt](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="c4d1b-197">`--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-the-resource-id-of-the-europe-app"></a><span data-ttu-id="c4d1b-198">De resource-ID van de app Europa niet ophalen</span><span class="sxs-lookup"><span data-stu-id="c4d1b-198">Get the resource ID of the Europe app</span></span>
<span data-ttu-id="c4d1b-199">Gebruik [az appservice web weergeven](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) ophalen van de bron-ID van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a><span data-ttu-id="c4d1b-200">Een Traffic Manager-eindpunt voor de app Europa toevoegen</span><span class="sxs-lookup"><span data-stu-id="c4d1b-200">Add a Traffic Manager endpoint for the Europe app</span></span>
<span data-ttu-id="c4d1b-201">Gebruik [netwerkeindpunt voor het traffic manager az maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) een eindpunt toevoegen aan uw Traffic Manager-profiel en de bron-ID van uw web-app gebruiken als het doel.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add an endpoint to your Traffic Manager profile and use the resource ID of your web app as the target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a><span data-ttu-id="c4d1b-202">Het Traffic Manager-eindpunt-URL ophalen</span><span class="sxs-lookup"><span data-stu-id="c4d1b-202">Get the Traffic Manager endpoint URL</span></span>
<span data-ttu-id="c4d1b-203">Uw Traffic Manager-profiel heeft nu een eindpunt dat naar uw bestaande web-app wijst.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-203">Your Traffic Manager profile now has an endpoint that points to your existing web app.</span></span> <span data-ttu-id="c4d1b-204">Gebruik [az netwerk traffic manager-profiel weergeven](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) om de URL te krijgen.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) to get its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="c4d1b-205">Kopieer de uitvoer in uw browser.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-205">Copy the output into your browser.</span></span> <span data-ttu-id="c4d1b-206">U ziet uw web-app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="c4d1b-207">Maken van een Azure Redis-Cache in Azië</span><span class="sxs-lookup"><span data-stu-id="c4d1b-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="c4d1b-208">Nu repliceren u uw Azure-web-app naar de regio Zuidoost-Azië.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-208">Now, you replicate your Azure web app to the Southeast Asia region.</span></span> <span data-ttu-id="c4d1b-209">Gebruik om te starten, [az redis maken](https://docs.microsoft.com/en-us/cli/azure/redis#create) voor het maken van een tweede Azure Redis-Cache in Zuidoost-Azië.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-209">To start, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="c4d1b-210">Deze cache moet worden geplaatst met uw app in Azië.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-210">This cache needs to be colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="c4d1b-211">`--name $cacheName-asia`Geeft de cache de naam van de cache West-Europa, met de `-asia` achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-211">`--name $cacheName-asia` gives the cache the name of the West Europe cache, with the `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="c4d1b-212">Maken van een App Service-plan in Azië</span><span class="sxs-lookup"><span data-stu-id="c4d1b-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="c4d1b-213">Gebruik [az appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) voor het maken van een tweede App Service-abonnement in de regio Zuidoost-Azië, met dezelfde S1 laag als het plan West-Europa.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) to create a second App Service plan in the Southeast Asia region, using the same S1 tier as the West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="c4d1b-214">Een web-app maken in Azië</span><span class="sxs-lookup"><span data-stu-id="c4d1b-214">Create a web app in Asia</span></span>
<span data-ttu-id="c4d1b-215">Gebruik [az appservice web maken](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) voor het maken van een tweede web-app.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="c4d1b-216">`--name $appName-asia`biedt de app de naam van de app West-Europa, met de `-asia` achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-216">`--name $appName-asia` gives the app the name of the West Europe app, with the `-asia` suffix.</span></span>

### <a name="configure-the-connection-string-for-redis"></a><span data-ttu-id="c4d1b-217">De verbindingsreeks configureren voor Redis</span><span class="sxs-lookup"><span data-stu-id="c4d1b-217">Configure the connection string for Redis</span></span>
<span data-ttu-id="c4d1b-218">Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) toevoegen aan de web-app van de verbindingsreeks voor de cache Zuidoost-Azië.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add to the web app the connection string for the Southeast Asia cache.</span></span>

<span data-ttu-id="c4d1b-219">AZ appservice webconfiguratie appsettings bijwerken--instellingen ' RedisConnection = $($redis.hostname): $($redis.sslPort), wachtwoord = $($redis.accessKeys.primaryKey), ssl = True, abortConnect = False '--naam $appName-Azië--resourcegroep myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c4d1b-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-the-asia-app"></a><span data-ttu-id="c4d1b-220">Configureer Git-implementatie voor de app Azië.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-220">Configure Git deployment for the Asia app.</span></span>
<span data-ttu-id="c4d1b-221">Gebruik [-broncodebeheer in az appservice web-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) om lokale Git-implementatie voor de tweede web-app te configureren.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment for the second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="c4d1b-222">Met deze opdracht kunt u een uitvoer die op het volgende lijkt:</span><span class="sxs-lookup"><span data-stu-id="c4d1b-222">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="c4d1b-223">De geretourneerde URL gebruiken voor het configureren van een tweede externe Git voor uw lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-223">Use the returned URL to configure a second Git remote for your local repository.</span></span> <span data-ttu-id="c4d1b-224">De volgende opdracht maakt gebruik van het vorige Uitvoervoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-224">The following command uses the preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="c4d1b-225">Uw voorbeeldtoepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="c4d1b-225">Deploy your sample application</span></span>
<span data-ttu-id="c4d1b-226">Voer `git push` voor het implementeren van uw voorbeeldtoepassing naar de tweede externe Git.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-226">Run `git push` to deploy your sample application to the second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="c4d1b-227">Wanneer wachtwoord wordt gevraagd, gebruikt u het wachtwoord die u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-227">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-asia-app"></a><span data-ttu-id="c4d1b-228">Blader naar de app Azië</span><span class="sxs-lookup"><span data-stu-id="c4d1b-228">Browse to the Asia app</span></span>
<span data-ttu-id="c4d1b-229">Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) om te controleren of uw app live in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to verify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a><span data-ttu-id="c4d1b-230">De resource-ID van de app Azië niet ophalen</span><span class="sxs-lookup"><span data-stu-id="c4d1b-230">Get the resource ID of the Asia app</span></span>
<span data-ttu-id="c4d1b-231">Gebruik [az appservice web weergeven](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) ophalen van de bron-ID van uw web-app in Zuidoost-Azië.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a><span data-ttu-id="c4d1b-232">Een Traffic Manager-eindpunt voor de app Azië toevoegen</span><span class="sxs-lookup"><span data-stu-id="c4d1b-232">Add a Traffic Manager endpoint for the Asia app</span></span>
<span data-ttu-id="c4d1b-233">Gebruik [netwerkeindpunt voor het traffic manager az maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) een tweede eindpunt toevoegen aan Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add a second endpoint to the Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a><span data-ttu-id="c4d1b-234">Voeg regio-id toe aan web-apps</span><span class="sxs-lookup"><span data-stu-id="c4d1b-234">Add region identifier to web apps</span></span>
<span data-ttu-id="c4d1b-235">Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) toevoegen van een omgevingsvariabele regio-specifieke.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="c4d1b-236">Deze toepassingsinstelling wordt al gebruikt door de toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="c4d1b-237">Kijk eens naar `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="c4d1b-238">Voltooid!</span><span class="sxs-lookup"><span data-stu-id="c4d1b-238">Complete!</span></span>

<span data-ttu-id="c4d1b-239">Probeer het nu toegang hebben tot de URL van uw Traffic Manager-profiel van de browsers in verschillende geografische regio's.</span><span class="sxs-lookup"><span data-stu-id="c4d1b-239">Now, try to access the URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="c4d1b-240">Clientbrowsers van Europa moeten weergeven 'ASP.NET West-Europa' en 'ASP.NET Zuidoost-Azië.' moet worden weergegeven in de browser van de client vanuit Azië</span><span class="sxs-lookup"><span data-stu-id="c4d1b-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="c4d1b-241">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="c4d1b-241">More resources</span></span>
