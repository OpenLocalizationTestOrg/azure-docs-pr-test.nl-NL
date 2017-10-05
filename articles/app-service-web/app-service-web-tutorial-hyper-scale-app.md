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
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Een hyperschaal web-app in Azure bouwen

Deze zelfstudie laat zien hoe u uit een ASP.NET-web-app in Azure om te maximaliseren gebruikersaanvragen te schalen.

Voordat u deze zelfstudie begint, zorg ervoor dat [is geïnstalleerd met de Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) op uw computer. U moet bovendien [Visual Studio](https://www.visualstudio.com/vs/) op uw lokale machine worden uitgevoerd van de voorbeeldtoepassing.

## <a name="step-1---get-sample-application"></a>Stap 1 - Get-voorbeeldtoepassing
In deze stap moet u het lokale ASP.NET-project instellen.

### <a name="clone-the-application-repository"></a>Kloon de opslagplaats toepassing

Open de van uw keuze en `CD` in een werkmap. Voer de volgende opdrachten voor het klonen van de voorbeeldtoepassing. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a>De voorbeeldtoepassing uitvoert in Visual Studio

Open de oplossing in Visual Studio.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

Type `F5` de toepassing uit te voeren.

In dit voorbeeld ASP.NET-webtoepassing afkomstig is van de standaardsjabloon en de gebruiker zich blijft voordoen sessies en maakt gebruik van de uitvoercache. Kijk eens naar `HighScaleApp\Controllers\HomeController.cs`. De `Index()` methode wordt een stukje informatie toegevoegd aan de sessie.

```csharp
Session.Add("visited", "true"); 
```

En de `About()` en `Contact()` methoden in de cache de uitvoer.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a>Stap 2 - implementeren in Azure
In deze stap maakt u een Azure-web-app maken en uw voorbeeld ASP.NET-toepassing te implementeren.

### <a name="create-a-resource-group"></a>Een resourcegroep maken   
Gebruik [az groep maken](https://docs.microsoft.com/cli/azure/group#create) maken een [resourcegroep](../azure-resource-manager/resource-group-overview.md) in de regio West-Europa. Een resourcegroep is waar het plaatsen van alle Azure-resources die u beheren, wilt zoals de web-app en alle SQL-databases back-end.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

Om te zien welke mogelijke waarden die u hebt, kunnen gebruiken voor `---location`, gebruiken de [az appservice lijst-locaties](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) opdracht.

### <a name="create-an-app-service-plan"></a>Een App Service-plan maken
Gebruik [az appservice-abonnement maken](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) voor het maken van een "B1' [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

Een App Service-abonnement is een schaaleenheid, met inbegrip van een willekeurig aantal apps dat u wilt omhoog of omlaag schalen samen via dezelfde App Service-infrastructuur. Elk plan is ook toegewezen een [prijscategorie](https://azure.microsoft.com/en-us/pricing/details/app-service/). Hogere lagen bevatten betere hardware- en meer functies, zoals meer exemplaren van de scale-out.

Voor deze zelfstudie is B1 de minimale laag waarmee de gebeurtenis uitschalen naar drie exemplaren. U kunt altijd uw app omhoog of omlaag verplaatsen de prijscategorie later door te voeren [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update). 

### <a name="create-a-web-app"></a>Een webtoepassing maken
Gebruik [az appservice web maken](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) een web-app maken met een unieke naam in `$appName`.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>Implementatiereferenties instellen
Gebruik [az appservice web implementatiegebruiker ingesteld](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) uw account niveau implementatiereferenties instellen voor App Service.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Configureer Git-implementatie
Gebruik [-broncodebeheer in az appservice web-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) om lokale Git-implementatie te configureren.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

Met deze opdracht kunt u een uitvoer die op het volgende lijkt:

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

De geretourneerde URL gebruiken voor het configureren van uw externe Git. De volgende opdracht maakt gebruik van het vorige Uitvoervoorbeeld.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a>De voorbeeldtoepassing implementeren
U bent nu klaar voor het implementeren van uw voorbeeldtoepassing. Voer `git push` uit.

```powershell
git push azure master
```

Wanneer wachtwoord wordt gevraagd, gebruikt u het wachtwoord die u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.

### <a name="browse-to-azure-web-app"></a>Blader naar de Azure-web-app
Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) overzicht van uw app live in Azure met deze opdracht uitvoert.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a>Stap 3: verbinding maken met Redis
In deze stap maakt instellen u Azure Redis-Cache als een externe, geplaatste cache aan uw Azure-web-app. Snel kunt u gebruikmaken van Redis cache opslaan van uw pagina-uitvoer. Bovendien wanneer u later uit uw web-apps schaalt, Redis helpt u behouden gebruikerssessies over meerdere exemplaren op betrouwbare wijze.

### <a name="create-an-azure-redis-cache"></a>Maak een Azure Redis Cache
Gebruik [az redis maken](https://docs.microsoft.com/en-us/cli/azure/redis#create) maken van een Azure Redis-Cache en opslaan van de JSON-uitvoer. Gebruik een unieke naam in `$cacheName`.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a>De toepassing configureren voor het gebruik van Redis
De verbindingsreeks voor uw cache-notatie.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

De tweede regel geeft u een uitvoer die er als volgt uit:

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

Maak in Visual Studio een web-configuratiebestand in de hoofdmap van uw project aangeroepen `redis.config` en plak de volgende code in de App. In `value`, gebruikt u de verbindingsreeks van de PowerShell-uitvoer.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Als u naar kijkt de `.gitignore` bestand in de Git-opslagplaats, ziet u dat dit bestand is uitgesloten van broncodebeheer. Op die manier uw vertrouwelijke gegevens veilig blijft. 

Open `Web.config`. U ziet de `<appSettings file="redis.config">` element, dat de instelling die u hebt gemaakt in opgehaald `redis.config`. 

Zoek de opmerkingen sectie waarin `<sessionState>` en `<caching>`. Verwijder de opmerkingen in deze sectie.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

Deze code eruitziet voor de Redis-verbindingsreeks die u hebt gedefinieerd in `RedisConnection`. 

Nu uw toepassing maakt gebruik van Redis voor het beheren van sessies en opslaan in cache. Type `F5` de toepassing uit te voeren. Indien gewenst, kunt u downloaden van een Redis-management-client om de gegevens die nu wordt opgeslagen in de cache.

### <a name="configure-the-connection-string-in-azure"></a>De verbindingsreeks configureren in Azure

Voor uw toepassing uit te voeren in Azure, moet u de dezelfde Redis-verbindingsreeks configureren in uw Azure-web-app. Aangezien `redis.config` niet behouden in broncodebeheer, wordt niet geïmplementeerd in Azure tijdens het uitvoeren van Git-implementatie.

Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) om toe te voegen van de verbindingsreeks met dezelfde naam (`RedisConnection`).

AZ appservice webconfiguratie appsettings bijwerken--instellingen ' RedisConnection $connstring = '--$appName--resourcegroep myResourceGroup naam

Vergeet niet dat `$connstring` de opgemaakte verbindingsreeks bevat.

### <a name="redeploy-the-application-to-azure"></a>De toepassing in Azure implementeren
Git-opdrachten gebruiken om uw wijzigingen naar Azure

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

Wanneer wachtwoord wordt gevraagd, gebruikt u het wachtwoord die u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.

### <a name="browse-to-the-azure-web-app"></a>Blader naar de Azure-web-app
Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) live in Azure wijzigingen kunnen zien.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a>Stap 4: Scale naar meerdere exemplaren
De App Service-abonnement is de schaaleenheid voor uw Azure-web-apps. Als u wilt uitbreiden uw web-app, moet u de App Service-abonnement schalen.

Gebruik [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update) moet worden uitgebreid met de App Service-abonnement naar drie exemplaren die het maximumaantal dat is toegestaan door de prijscategorie B1. Denk eraan dat B1 de prijscategorie die u hebt gekozen toen u de App Service-abonnement eerder gemaakt. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>Stap 5: Scale geografisch
Tijdens het geografisch schalen, kunt u uw app uitvoeren in meerdere regio's van de Azure-cloud. Deze setup taakverdelingen van uw app verder op basis van Geografie en verlaagt de reactietijd van de door het plaatsen van uw app dichter clientbrowsers.

In deze stap maakt u uw ASP.NET-web-app in een tweede regio met schalen [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/). Aan het einde van de stap hebt u een web-app uitgevoerd in West-Europa (al gemaakt) en een web-app uitgevoerd in Zuidoost-Azië (nog niet gemaakt). Beide apps kunnen worden geleverd vanuit dezelfde Traffic Manager-URL.

### <a name="scale-up-the-europe-app-to-standard-tier"></a>De app Europa standaardcategorie opschalen
Integratie met Azure Traffic Manager vereist in App Service, de Standard-prijscategorie. Gebruik [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update) naar uw App Service-abonnement S1 opschalen. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Een Traffic Manager-profiel maken 
Gebruik [az netwerk traffic manager-profiel maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) een Traffic Manager-profiel maken en toe te voegen aan de resourcegroep. Gebruik een unieke DNS-naam in $dnsName.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`Hiermee wordt aangegeven dat dit profiel [gebruikersverkeer gerouteerd naar het dichtstbijzijnde eindpunt](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="get-the-resource-id-of-the-europe-app"></a>De resource-ID van de app Europa niet ophalen
Gebruik [az appservice web weergeven](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) ophalen van de bron-ID van uw web-app.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a>Een Traffic Manager-eindpunt voor de app Europa toevoegen
Gebruik [netwerkeindpunt voor het traffic manager az maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) een eindpunt toevoegen aan uw Traffic Manager-profiel en de bron-ID van uw web-app gebruiken als het doel.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a>Het Traffic Manager-eindpunt-URL ophalen
Uw Traffic Manager-profiel heeft nu een eindpunt dat naar uw bestaande web-app wijst. Gebruik [az netwerk traffic manager-profiel weergeven](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) om de URL te krijgen. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Kopieer de uitvoer in uw browser. U ziet uw web-app opnieuw.

### <a name="create-an-azure-redis-cache-in-asia"></a>Maken van een Azure Redis-Cache in Azië
Nu repliceren u uw Azure-web-app naar de regio Zuidoost-Azië. Gebruik om te starten, [az redis maken](https://docs.microsoft.com/en-us/cli/azure/redis#create) voor het maken van een tweede Azure Redis-Cache in Zuidoost-Azië. Deze cache moet worden geplaatst met uw app in Azië.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`Geeft de cache de naam van de cache West-Europa, met de `-asia` achtervoegsel.

### <a name="create-an-app-service-plan-in-asia"></a>Maken van een App Service-plan in Azië
Gebruik [az appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) voor het maken van een tweede App Service-abonnement in de regio Zuidoost-Azië, met dezelfde S1 laag als het plan West-Europa.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>Een web-app maken in Azië
Gebruik [az appservice web maken](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) voor het maken van een tweede web-app.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`biedt de app de naam van de app West-Europa, met de `-asia` achtervoegsel.

### <a name="configure-the-connection-string-for-redis"></a>De verbindingsreeks configureren voor Redis
Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) toevoegen aan de web-app van de verbindingsreeks voor de cache Zuidoost-Azië.

AZ appservice webconfiguratie appsettings bijwerken--instellingen ' RedisConnection = $($redis.hostname): $($redis.sslPort), wachtwoord = $($redis.accessKeys.primaryKey), ssl = True, abortConnect = False '--naam $appName-Azië--resourcegroep myResourceGroup

### <a name="configure-git-deployment-for-the-asia-app"></a>Configureer Git-implementatie voor de app Azië.
Gebruik [-broncodebeheer in az appservice web-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) om lokale Git-implementatie voor de tweede web-app te configureren.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

Met deze opdracht kunt u een uitvoer die op het volgende lijkt:

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

De geretourneerde URL gebruiken voor het configureren van een tweede externe Git voor uw lokale opslagplaats. De volgende opdracht maakt gebruik van het vorige Uitvoervoorbeeld.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>Uw voorbeeldtoepassing implementeren
Voer `git push` voor het implementeren van uw voorbeeldtoepassing naar de tweede externe Git. 

```bash
git push azure-asia master
```

Wanneer wachtwoord wordt gevraagd, gebruikt u het wachtwoord die u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.

### <a name="browse-to-the-asia-app"></a>Blader naar de app Azië
Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) om te controleren of uw app live in Azure wordt uitgevoerd.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a>De resource-ID van de app Azië niet ophalen
Gebruik [az appservice web weergeven](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) ophalen van de bron-ID van uw web-app in Zuidoost-Azië.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a>Een Traffic Manager-eindpunt voor de app Azië toevoegen
Gebruik [netwerkeindpunt voor het traffic manager az maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) een tweede eindpunt toevoegen aan Traffic Manager-profiel.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a>Voeg regio-id toe aan web-apps
Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) toevoegen van een omgevingsvariabele regio-specifieke.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

Deze toepassingsinstelling wordt al gebruikt door de toepassingscode. Kijk eens naar `HighScaleApp\Views\Home\Index.cshtml`.

### <a name="complete"></a>Voltooid!

Probeer het nu toegang hebben tot de URL van uw Traffic Manager-profiel van de browsers in verschillende geografische regio's. Clientbrowsers van Europa moeten weergeven 'ASP.NET West-Europa' en 'ASP.NET Zuidoost-Azië.' moet worden weergegeven in de browser van de client vanuit Azië

## <a name="more-resources"></a>Meer bronnen
