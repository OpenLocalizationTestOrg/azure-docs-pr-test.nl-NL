---
title: aangepast domein aaaAdd en SSL tooan Azure web-app | Microsoft Docs
description: Meer informatie over hoe tooprepare uw Azure web-app toogo productie door uw huisstijl toe te voegen. Overzicht van Hallo aangepaste domain name (vanity domein) tooyour web-app en beveilig deze met een aangepaste SSL-certificaat.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a><span data-ttu-id="57a99-104">Aangepast domein- en SSL tooan Azure-web-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="57a99-104">Add custom domain and SSL tooan Azure web app</span></span>

<span data-ttu-id="57a99-105">Deze zelfstudie leert u hoe tooquickly toewijzen van een aangepast domein naam tooyour Azure-web-app en beveilig deze met een aangepaste SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="57a99-105">This tutorial shows you how tooquickly map a custom domain name tooyour Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="57a99-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="57a99-106">Before you begin</span></span>

<span data-ttu-id="57a99-107">Voordat u dit voorbeeld uitvoert, installeert u Hallo [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) lokaal.</span><span class="sxs-lookup"><span data-stu-id="57a99-107">Before running this sample, install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="57a99-108">U moet ook pagina beheerderstoegang toohello DNS-configuratie voor de provider van het desbetreffende domein.</span><span class="sxs-lookup"><span data-stu-id="57a99-108">You also need administrative access toohello DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="57a99-109">Bijvoorbeeld: tooadd `www.contoso.com`, moet u toobe kunnen tooconfigure DNS-vermeldingen voor `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="57a99-109">For example, tooadd `www.contoso.com`, you need toobe able tooconfigure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="57a99-110">Tot slot moet u een geldige. PFX-bestand _en_ het wachtwoord voor Hallo gewenste tooupload SSL-certificaat en bindt.</span><span class="sxs-lookup"><span data-stu-id="57a99-110">Lastly, you need a valid .PFX file _and_ its password for hello SSL certificate you want tooupload and bind.</span></span> <span data-ttu-id="57a99-111">Dit SSL-certificaat moet geconfigureerde toosecure Hallo aangepaste domeinnaam gewenste.</span><span class="sxs-lookup"><span data-stu-id="57a99-111">This SSL certificate should be configured toosecure hello custom domain name you want.</span></span> <span data-ttu-id="57a99-112">In Hallo hierboven voorbeeld uw SSL-certificaat moet beveiligen `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="57a99-112">In hello above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="57a99-113">Stap 1: een Azure-web-app maken</span><span class="sxs-lookup"><span data-stu-id="57a99-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="57a99-114">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="57a99-114">Log in tooAzure</span></span>

<span data-ttu-id="57a99-115">We zijn nu gaat toouse hello Azure CLI 2.0 in een terminalvenster toocreate Hallo bronnen nodig toohost onze Node.js-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="57a99-115">We are now going toouse hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost our Node.js app in Azure.</span></span>  <span data-ttu-id="57a99-116">Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="57a99-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="57a99-117">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="57a99-117">Create a resource group</span></span>   
<span data-ttu-id="57a99-118">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="57a99-118">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="57a99-119">Een Azure-resourcegroep is een logische container waarin Azure-resources, zoals web-apps, databases en opslagaccounts, worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="57a99-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="57a99-120">toosee welke mogelijke waarden u kunt gebruiken voor `---location`, gebruik Hallo `az appservice list-locations` Azure CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="57a99-120">toosee what possible values you can use for `---location`, use hello `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="57a99-121">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="57a99-121">Create an App Service plan</span></span>

<span data-ttu-id="57a99-122">Maken van een App Service-abonnement met Hallo [az appservice-abonnement maken](/cli/azure/appservice/plan#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="57a99-122">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="57a99-123">Hallo volgende voorbeeld maakt u een App Service-abonnement met de naam `myAppServicePlan` met Hallo **Basic** prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="57a99-123">hello following example creates an App Service plan named `myAppServicePlan` using hello **Basic** pricing tier.</span></span>

<span data-ttu-id="57a99-124">AZ appservice-abonnement maken--naam myAppServicePlan--resourcegroep myResourceGroup--sku B1</span><span class="sxs-lookup"><span data-stu-id="57a99-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="57a99-125">Wanneer Hallo App Service-abonnement is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="57a99-125">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a><span data-ttu-id="57a99-126">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="57a99-126">Create a web app</span></span>

<span data-ttu-id="57a99-127">Nu dat een App Service-abonnement is gemaakt, maakt u een web-app binnen Hallo `myAppServicePlan` App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="57a99-127">Now that an App Service plan has been created, create a web app within hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="57a99-128">Hallo web-app biedt u een hosting ruimte toodeploy bent uw code, evenals een URL biedt u tooview Hallo toepassing geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="57a99-128">hello web app gives your a hosting space toodeploy your code as well as provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="57a99-129">Gebruik Hallo [az appservice web maken](/cli/azure/appservice/web#create) opdracht toocreate Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="57a99-129">Use hello [az appservice web create](/cli/azure/appservice/web#create) command toocreate hello web app.</span></span> 

<span data-ttu-id="57a99-130">Vervang de naam van uw eigen unieke app waar u Hallo zien in Hallo opdracht hieronder `<app_name>` tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="57a99-130">In hello command below, please substitute your own unique app name where you see hello `<app_name>` placeholder.</span></span> <span data-ttu-id="57a99-131">Deze unieke naam zal worden gebruikt als onderdeel van de Hallo van Hallo standaarddomeinnaam voor Hallo-web-app zodat Hallo naam toobe uniek zijn in alle apps in Azure moet.</span><span class="sxs-lookup"><span data-stu-id="57a99-131">This unique name will be used as hello part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="57a99-132">U kunt aangepaste DNS-vermelding toohello web-app later toewijzen voordat u deze tooyour gebruikers weergeven.</span><span class="sxs-lookup"><span data-stu-id="57a99-132">You can later map any custom DNS entry toohello web app before you expose it tooyour users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="57a99-133">Wanneer Hallo web-app is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="57a99-133">When hello web app has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

<span data-ttu-id="57a99-134">Van Hallo JSON-uitvoer `defaultHostName` standaarddomeinnaam van uw web-app bevat.</span><span class="sxs-lookup"><span data-stu-id="57a99-134">From hello JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="57a99-135">Navigeer in uw browser toothis adres.</span><span class="sxs-lookup"><span data-stu-id="57a99-135">In your browser, navigate toothis address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="57a99-137">Stap 2: configureer DNS-toewijzing</span><span class="sxs-lookup"><span data-stu-id="57a99-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="57a99-138">In deze stap maakt u een toewijzing toevoegen van een aangepast domein tooyour van web-app standaarddomeinnaam, `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="57a99-138">In this step, you add a mapping from a custom domain tooyour web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="57a99-139">Normaal gesproken uitvoeren u deze stap in de website van de domeinprovider van uw.</span><span class="sxs-lookup"><span data-stu-id="57a99-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="57a99-140">Elke domeinregistrar website is enigszins verschillen, dus u moet de documentatie van uw provider.</span><span class="sxs-lookup"><span data-stu-id="57a99-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="57a99-141">Hier zijn echter enkele algemene richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="57a99-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-tootoodns-management-page"></a><span data-ttu-id="57a99-142">Navigeer tootooDNS management-pagina</span><span class="sxs-lookup"><span data-stu-id="57a99-142">Navigate tootooDNS management page</span></span>

<span data-ttu-id="57a99-143">Meld u eerst in tooyour domeinregistrar website.</span><span class="sxs-lookup"><span data-stu-id="57a99-143">First, log in tooyour domain registrar's website.</span></span>  

<span data-ttu-id="57a99-144">Vervolgens Hallo pagina vinden voor het beheren van DNS-records.</span><span class="sxs-lookup"><span data-stu-id="57a99-144">Then, find hello page for managing DNS records.</span></span> <span data-ttu-id="57a99-145">Zoek naar koppelingen of gebieden van Hallo site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="57a99-145">Look for links or areas of hello site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="57a99-146">U kunt vaak Hallo koppeling vinden door gegevens over uw account weer te geven en te zoeken naar een koppeling zoals **mijn domeinen**.</span><span class="sxs-lookup"><span data-stu-id="57a99-146">Often, you can find hello link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="57a99-147">Wanneer u deze pagina hebt gevonden, zoekt u een koppeling waarmee u DNS-records toevoegt of bewerkt.</span><span class="sxs-lookup"><span data-stu-id="57a99-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="57a99-148">Dit wordt mogelijk een **zonebestand** of **DNS-Records** koppeling of een **geavanceerde configuratie** koppeling.</span><span class="sxs-lookup"><span data-stu-id="57a99-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="57a99-149">Een CNAME-record maken</span><span class="sxs-lookup"><span data-stu-id="57a99-149">Create a CNAME record</span></span>

<span data-ttu-id="57a99-150">Voeg een CNAME-record dat is toegewezen standaarddomeinnaam Hallo gewenste subdomein naam tooyour van web-app (`<app_name>.azurewebsites.net`, waarbij `<app_name>` is de unieke naam van uw app).</span><span class="sxs-lookup"><span data-stu-id="57a99-150">Add a CNAME record that maps hello desired subdomain name tooyour web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="57a99-151">Voor Hallo `www.contoso.com` bijvoorbeeld als u een CNAME dat is toegewezen Hallo maken `www` hostnaam te`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="57a99-151">For hello `www.contoso.com` example, you create a CNAME that maps hello `www` hostname too`<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a><span data-ttu-id="57a99-152">Stap 3: Hallo aangepast domein configureren op uw web-app</span><span class="sxs-lookup"><span data-stu-id="57a99-152">Step 3 - Configure hello custom domain on your web app</span></span>

<span data-ttu-id="57a99-153">Wanneer u klaar bent met het Hallo hostnaam toewijzing configureren in de website van de domeinprovider van uw, bent u klaar tooconfigure Hallo aangepast domein op uw web-app.</span><span class="sxs-lookup"><span data-stu-id="57a99-153">When you finish configuring hello hostname mapping in your domain provider's website, you're ready tooconfigure hello custom domain on your web app.</span></span> <span data-ttu-id="57a99-154">Gebruik Hallo [az appservice web config hostnaam toevoegen](/cli/azure/appservice/web/config/hostname#add) opdracht tooadd deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="57a99-154">Use hello [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command tooadd this configuration.</span></span> 

<span data-ttu-id="57a99-155">In onderstaande Hallo opdracht, Vervang `<app_name>` met unieke app-naam en < your_custom_domain > met Hallo aangepaste FQDN-naam (bijvoorbeeld `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="57a99-155">In hello command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with hello fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="57a99-156">Hallo aangepaste domein is nu volledig toegewezen tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="57a99-156">hello custom domain now is fully mapped tooyour web app.</span></span> <span data-ttu-id="57a99-157">Navigeer in uw browser toohello aangepaste domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="57a99-157">In your browser, navigate toohello custom domain name.</span></span> <span data-ttu-id="57a99-158">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="57a99-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a><span data-ttu-id="57a99-160">Stap 4: een aangepaste SSL-certificaat tooyour web-app binden</span><span class="sxs-lookup"><span data-stu-id="57a99-160">Step 4 - Bind a custom SSL certificate tooyour web app</span></span>

<span data-ttu-id="57a99-161">U hebt nu een Azure-web-app met Hallo-domeinnaam die u wilt dat in de adresbalk van de browser Hallo.</span><span class="sxs-lookup"><span data-stu-id="57a99-161">You now have an Azure web app, with hello domain name you want in hello browser's address bar.</span></span> <span data-ttu-id="57a99-162">Echter, als u de navigatiefunctie toohello `https://<your_custom_domain>` nu het ophalen van een certificaatfout.</span><span class="sxs-lookup"><span data-stu-id="57a99-162">However, if you navigate toohello `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="57a99-164">Deze fout treedt op omdat uw web-app een SSL-certificaat-binding die overeenkomt met de naam van uw aangepaste domein nog geen.</span><span class="sxs-lookup"><span data-stu-id="57a99-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="57a99-165">Echter, u niet krijgt een fout als u te navigeren`https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="57a99-165">However, you don't get an error if you navigate too`https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="57a99-166">Dit is omdat uw app, evenals alle apps van Azure App Service, is beveiligd met SSL-certificaat voor Hallo Hallo `*.azurewebsites.net` jokertekendomein standaard.</span><span class="sxs-lookup"><span data-stu-id="57a99-166">This is because your app, as well as all Azure App Service apps, is secured with hello SSL certificate for hello `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="57a99-167">In het sorteren van de tooaccess uw web-app op uw aangepaste domeinnaam, moet u toobind Hallo SSL-certificaat voor uw aangepaste domein toohello web-app.</span><span class="sxs-lookup"><span data-stu-id="57a99-167">In order tooaccess your web app by your custom domain name, you need toobind hello SSL certificate for your custom domain toohello web app.</span></span> <span data-ttu-id="57a99-168">Dit doet u in deze stap.</span><span class="sxs-lookup"><span data-stu-id="57a99-168">You will do it in this step.</span></span> 

### <a name="upload-hello-ssl-certificate"></a><span data-ttu-id="57a99-169">Hallo SSL-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="57a99-169">Upload hello SSL certificate</span></span>

<span data-ttu-id="57a99-170">Hallo SSL-certificaat voor uw aangepaste domein tooyour web-app uploaden via Hallo [az appservice web config ssl uploaden](/cli/azure/appservice/web/config/ssl#upload) opdracht.</span><span class="sxs-lookup"><span data-stu-id="57a99-170">Upload hello SSL certificate for your custom domain tooyour web app by using hello [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="57a99-171">In onderstaande Hallo opdracht, Vervang `<app_name>` met de naam van uw unieke app `<path_to_ptx_file>` met Hallo pad tooyour. PFX-bestand en `<password>` met het wachtwoord voor uw certificaat.</span><span class="sxs-lookup"><span data-stu-id="57a99-171">In hello command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with hello path tooyour .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="57a99-172">Wanneer het Hallo-certificaat is geüpload, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="57a99-172">When hello certificate is uploaded, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

<span data-ttu-id="57a99-173">Van Hallo JSON-uitvoer `thumbprint` ziet u de vingerafdruk van het geüploade certificaat.</span><span class="sxs-lookup"><span data-stu-id="57a99-173">From hello JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="57a99-174">Kopieer de waarde voor de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="57a99-174">Copy its value for hello next step.</span></span>

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a><span data-ttu-id="57a99-175">BIND Hallo toohello web-app van SSL-certificaat geüpload</span><span class="sxs-lookup"><span data-stu-id="57a99-175">Bind hello uploaded SSL certificate toohello web app</span></span>

<span data-ttu-id="57a99-176">Uw web-app heeft nu de aangepaste domeinnaam Hallo gewenste en heeft ook een SSL-certificaat dat aangepaste domein beveiligt.</span><span class="sxs-lookup"><span data-stu-id="57a99-176">Your web app now has hello custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="57a99-177">Hallo is alleen ding links toodo toobind Hallo geüploade certificaat toohello web-app.</span><span class="sxs-lookup"><span data-stu-id="57a99-177">hello only thing left toodo is toobind hello uploaded certificate toohello web app.</span></span> <span data-ttu-id="57a99-178">U dit doen met behulp van Hallo [az appservice web config ssl-binding](/cli/azure/appservice/web/config/ssl#bind) opdracht.</span><span class="sxs-lookup"><span data-stu-id="57a99-178">You do this by using hello [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="57a99-179">In onderstaande Hallo opdracht, Vervang `<app_name>` met de naam van uw unieke app en `<thumbprint-from-previous-output>` met Hallo certificaatvingerafdruk die u via de vorige opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="57a99-179">In hello command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with hello certificate thumbprint that you get from hello previous command.</span></span> 

<span data-ttu-id="57a99-180">AZ appservice web config ssl bind--naam < app_naam >--resourcegroep myResourceGroup--certificaatvingerafdruk < vingerafdruk-van-vorige-output >--ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="57a99-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="57a99-181">Wanneer het Hallo-certificaat wordt gebonden tooyour web-app, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="57a99-181">When hello certificate is bound tooyour web app, hello Azure CLI shows information similar toohello following example:</span></span>

<span data-ttu-id="57a99-182">{'Meldingenbeheer': 'Normale', 'clientAffinityEnabled': true, 'clientCertEnabled': false 'cloningInfo': null, 'containerSize': 0, "dailyMemoryTimeQuota": 0, "defaultHostName': ' < app_naam >. azurewebsites.net ', 'enabled': true, 'enabledHostNames': ['www.contoso.com' ' < app_naam >. azurewebsites.net ', ' < app_naam >. scm.azurewebsites.net '], 'gatewaySiteName': null, 'hostNameSslStates': [{'hostType': 'Standaard', 'name': ' < app_naam >. azurewebsites.net ', 'sslState': 'Disabled', 'vingerafdruk': null, 'toUpdate': null, 'virtualIp': null}, {'hostType': 'opslagplaats", "name": ' < app_naam >. scm.azurewebsites.net ', 'sslState': "Uitgeschakeld" 'vingerafdruk': null, 'toUpdate': null, 'virtualIp': null}, {'hostType': 'Standaard', 'name': 'www.contoso.com', 'sslState': 'SniEnabled' 'vingerafdruk': '9FD1D2D06E2293673E2A8D1CA484A092BD016D00', 'toUpdate': null, 'virtualIp': null}], 'hostnamen': ['www.contoso.com' ' < app_naam >. azurewebsites.net '], 'hostNamesDisabled': false 'hostingEnvironmentProfile': null 'id': ' /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s / < app_naam > ', 'isDefaultContainer': null, 'type': 'WebApp', 'lastModifiedTimeUtc': ' 2017-03-29T14:36:18.803333 ', 'locatie': 'West-Europa', 'maxNumberOfWorkers': null, 'microService': 'false', 'name': "< app_naam >" 'outboundIpAddresses': '13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1', 'premiumAppDeployed': null, 'repositorySiteName': '< app_naam >', 'gereserveerd': false 'resourceGroup': 'myResourceGroup', 'scmSiteAlsoStopped': false 'serverFarmId': ' / abonnementen/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft t.Web/serverfarms/myAppServicePlan ', 'siteConfig': null, 'slotSwapStatus': null, 'status': 'Actief', 'suspendedTill': null, 'labels': null, 'targetSwapSlot': null, 'trafficManagerHostNames': null, 'type': 'Microsoft.Web/sites', 'usageState': 'Standaard'}</span><span class="sxs-lookup"><span data-stu-id="57a99-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="57a99-183">Navigeer in uw browser tooHTTPS eindpunt van uw aangepaste domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="57a99-183">In your browser, navigate tooHTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="57a99-184">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="57a99-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="57a99-186">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="57a99-186">More resources</span></span>

<span data-ttu-id="57a99-187">[Kopen en een aangepaste domeinnaam configureren in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[kopen en configureren van een SSL-certificaat voor uw Azure App Service](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="57a99-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
