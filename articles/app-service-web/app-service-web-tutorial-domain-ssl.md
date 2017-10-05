---
title: Aangepast domein- en SSL toevoegen aan een Azure-web-app | Microsoft Docs
description: Informatie over het voorbereiden van uw Azure-web-app gaan productie door uw huisstijl toe te voegen. De aangepaste domeinnaam (vanity domein) worden toegewezen aan uw web-app en beveilig deze met een aangepaste SSL-certificaat.
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
ms.openlocfilehash: c9d00f678b6257a8aafb35acd2d5a2292703a2dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="add-custom-domain-and-ssl-to-an-azure-web-app"></a><span data-ttu-id="0fe84-104">Aangepast domein- en SSL toevoegen aan een Azure-web-app</span><span class="sxs-lookup"><span data-stu-id="0fe84-104">Add custom domain and SSL to an Azure web app</span></span>

<span data-ttu-id="0fe84-105">Deze zelfstudie laat zien hoe u snel toewijzen van een aangepaste domeinnaam naar uw Azure-web-app en beveilig deze met een aangepaste SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="0fe84-105">This tutorial shows you how to quickly map a custom domain name to your Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="0fe84-106">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="0fe84-106">Before you begin</span></span>

<span data-ttu-id="0fe84-107">Voordat u dit voorbeeld uitvoert, installeert u de [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) lokaal.</span><span class="sxs-lookup"><span data-stu-id="0fe84-107">Before running this sample, install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="0fe84-108">Ook moet u beheerderstoegang tot de pagina DNS-configuratie voor de provider van het desbetreffende domein.</span><span class="sxs-lookup"><span data-stu-id="0fe84-108">You also need administrative access to the DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="0fe84-109">Bijvoorbeeld, om toe te voegen `www.contoso.com`, moet u mogelijk voor het configureren van DNS-vermeldingen voor `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="0fe84-109">For example, to add `www.contoso.com`, you need to be able to configure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="0fe84-110">Tot slot moet u een geldige. PFX-bestand _en_ het wachtwoord voor het SSL-certificaat dat u wilt uploaden en binden.</span><span class="sxs-lookup"><span data-stu-id="0fe84-110">Lastly, you need a valid .PFX file _and_ its password for the SSL certificate you want to upload and bind.</span></span> <span data-ttu-id="0fe84-111">Dit SSL-certificaat moet worden geconfigureerd voor de aangepaste domeinnaam die u wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="0fe84-111">This SSL certificate should be configured to secure the custom domain name you want.</span></span> <span data-ttu-id="0fe84-112">In het bovenstaande voorbeeld uw SSL-certificaat moet beveiligen `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="0fe84-112">In the above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="0fe84-113">Stap 1: een Azure-web-app maken</span><span class="sxs-lookup"><span data-stu-id="0fe84-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="0fe84-114">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe84-114">Log in to Azure</span></span>

<span data-ttu-id="0fe84-115">We gaan nu de Azure CLI 2.0 in een terminalvenster gebruiken om de resources te maken die nodig zijn voor het hosten van onze Node.js-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe84-115">We are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host our Node.js app in Azure.</span></span>  <span data-ttu-id="0fe84-116">Meld u aan bij uw Azure-abonnement met de opdracht [az login](/cli/azure/#login) en volg de instructies op het scherm.</span><span class="sxs-lookup"><span data-stu-id="0fe84-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="0fe84-117">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="0fe84-117">Create a resource group</span></span>   
<span data-ttu-id="0fe84-118">Maak een resourcegroep met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0fe84-118">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0fe84-119">Een Azure-resourcegroep is een logische container waarin Azure-resources, zoals web-apps, databases en opslagaccounts, worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="0fe84-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="0fe84-120">Gebruik de Azure CLI-opdracht `az appservice list-locations` om te zien welke waarden u kunt gebruiken voor `---location`.</span><span class="sxs-lookup"><span data-stu-id="0fe84-120">To see what possible values you can use for `---location`, use the `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="0fe84-121">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="0fe84-121">Create an App Service plan</span></span>

<span data-ttu-id="0fe84-122">Maak een App Service-plan met de opdracht [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="0fe84-122">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="0fe84-123">Het volgende voorbeeld wordt een App Service-abonnement met de naam `myAppServicePlan` met behulp van de **Basic** prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="0fe84-123">The following example creates an App Service plan named `myAppServicePlan` using the **Basic** pricing tier.</span></span>

<span data-ttu-id="0fe84-124">AZ appservice-abonnement maken--naam myAppServicePlan--resourcegroep myResourceGroup--sku B1</span><span class="sxs-lookup"><span data-stu-id="0fe84-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="0fe84-125">Wanneer de App Service-abonnement is gemaakt, de Azure CLI geeft informatie weer zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0fe84-125">When the App Service plan has been created, the Azure CLI shows information similar to the following example.</span></span> 

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

## <a name="create-a-web-app"></a><span data-ttu-id="0fe84-126">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="0fe84-126">Create a web app</span></span>

<span data-ttu-id="0fe84-127">Nu er een App Service-plan is gemaakt, maakt u binnen dit `myAppServicePlan` App Service-plan een web-app.</span><span class="sxs-lookup"><span data-stu-id="0fe84-127">Now that an App Service plan has been created, create a web app within the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="0fe84-128">De web-app kunt u bent een hosting ruimte om uw code te implementeren als een URL die u kunt de gedistribueerde toepassing weergeven.</span><span class="sxs-lookup"><span data-stu-id="0fe84-128">The web app gives your a hosting space to deploy your code as well as provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="0fe84-129">Gebruik de opdracht [az appservice web create](/cli/azure/appservice/web#create) om de web-app te maken.</span><span class="sxs-lookup"><span data-stu-id="0fe84-129">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the web app.</span></span> 

<span data-ttu-id="0fe84-130">Vervang de naam van uw eigen unieke app waarin u ziet in de onderstaande opdracht de `<app_name>` tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="0fe84-130">In the command below, please substitute your own unique app name where you see the `<app_name>` placeholder.</span></span> <span data-ttu-id="0fe84-131">Deze unieke naam zal worden gebruikt als het deel van naam van het standaarddomein voor de web-app zodat de naam moet uniek zijn in alle apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe84-131">This unique name will be used as the part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="0fe84-132">Later kunt u een aangepaste DNS-vermelding toewijzen aan de web-app voordat u deze beschikbaar maakt voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="0fe84-132">You can later map any custom DNS entry to the web app before you expose it to your users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="0fe84-133">Wanneer de web-app is gemaakt, toont de Azure CLI soortgelijke informatie als in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="0fe84-133">When the web app has been created, the Azure CLI shows information similar to the following example.</span></span> 

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

<span data-ttu-id="0fe84-134">Van de JSON-uitvoer `defaultHostName` standaarddomeinnaam van uw web-app bevat.</span><span class="sxs-lookup"><span data-stu-id="0fe84-134">From the JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="0fe84-135">Ga in uw browser naar dit adres.</span><span class="sxs-lookup"><span data-stu-id="0fe84-135">In your browser, navigate to this address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="0fe84-137">Stap 2: configureer DNS-toewijzing</span><span class="sxs-lookup"><span data-stu-id="0fe84-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="0fe84-138">In deze stap maakt u een toewijzing toevoegen van een aangepast domein voor uw web-app standaarddomeinnaam, `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0fe84-138">In this step, you add a mapping from a custom domain to your web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="0fe84-139">Normaal gesproken uitvoeren u deze stap in de website van de domeinprovider van uw.</span><span class="sxs-lookup"><span data-stu-id="0fe84-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="0fe84-140">Elke domeinregistrar website is enigszins verschillen, dus u moet de documentatie van uw provider.</span><span class="sxs-lookup"><span data-stu-id="0fe84-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="0fe84-141">Hier zijn echter enkele algemene richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="0fe84-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-to-to-dns-management-page"></a><span data-ttu-id="0fe84-142">Ga naar naar DNS-pagina</span><span class="sxs-lookup"><span data-stu-id="0fe84-142">Navigate to to DNS management page</span></span>

<span data-ttu-id="0fe84-143">Eerst aanmelden bij uw domeinregistrar website.</span><span class="sxs-lookup"><span data-stu-id="0fe84-143">First, log in to your domain registrar's website.</span></span>  

<span data-ttu-id="0fe84-144">Zoek de pagina voor het beheren van DNS-records.</span><span class="sxs-lookup"><span data-stu-id="0fe84-144">Then, find the page for managing DNS records.</span></span> <span data-ttu-id="0fe84-145">Zoek naar koppelingen of gebieden van de site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="0fe84-145">Look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="0fe84-146">Vaak kunt u de koppeling vinden door de gegevens over uw account weer te geven en te zoeken naar een koppeling zoals **mijn domeinen**.</span><span class="sxs-lookup"><span data-stu-id="0fe84-146">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="0fe84-147">Wanneer u deze pagina hebt gevonden, zoekt u een koppeling waarmee u DNS-records toevoegt of bewerkt.</span><span class="sxs-lookup"><span data-stu-id="0fe84-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="0fe84-148">Dit wordt mogelijk een **zonebestand** of **DNS-Records** koppeling of een **geavanceerde configuratie** koppeling.</span><span class="sxs-lookup"><span data-stu-id="0fe84-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="0fe84-149">Een CNAME-record maken</span><span class="sxs-lookup"><span data-stu-id="0fe84-149">Create a CNAME record</span></span>

<span data-ttu-id="0fe84-150">Voeg een CNAME-record die de gewenste subdomeinnaam wordt toegewezen aan uw web-app standaarddomeinnaam (`<app_name>.azurewebsites.net`, waarbij `<app_name>` is de unieke naam van uw app).</span><span class="sxs-lookup"><span data-stu-id="0fe84-150">Add a CNAME record that maps the desired subdomain name to your web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="0fe84-151">Voor de `www.contoso.com` wanneer u een CNAME dat is toegewezen bijvoorbeeld maakt de `www` hostname naar `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0fe84-151">For the `www.contoso.com` example, you create a CNAME that maps the `www` hostname to `<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-the-custom-domain-on-your-web-app"></a><span data-ttu-id="0fe84-152">Stap 3: het aangepast domein configureren op uw web-app</span><span class="sxs-lookup"><span data-stu-id="0fe84-152">Step 3 - Configure the custom domain on your web app</span></span>

<span data-ttu-id="0fe84-153">Wanneer u klaar bent met het configureren van de toewijzing van de hostnaam in de website van de domeinprovider van uw, kunt u kunt het aangepast domein configureren op uw web-app.</span><span class="sxs-lookup"><span data-stu-id="0fe84-153">When you finish configuring the hostname mapping in your domain provider's website, you're ready to configure the custom domain on your web app.</span></span> <span data-ttu-id="0fe84-154">Gebruik de [az appservice web config hostnaam toevoegen](/cli/azure/appservice/web/config/hostname#add) opdracht voor het toevoegen van deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="0fe84-154">Use the [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command to add this configuration.</span></span> 

<span data-ttu-id="0fe84-155">In de onderstaande opdracht vervangen `<app_name>` met unieke app-naam en < your_custom_domain > met de aangepaste volledig gekwalificeerde domeinnaam (bijvoorbeeld `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="0fe84-155">In the command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with the fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="0fe84-156">Het aangepaste domein is nu volledig toegewezen aan uw web-app.</span><span class="sxs-lookup"><span data-stu-id="0fe84-156">The custom domain now is fully mapped to your web app.</span></span> <span data-ttu-id="0fe84-157">Ga in uw browser naar de aangepaste domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="0fe84-157">In your browser, navigate to the custom domain name.</span></span> <span data-ttu-id="0fe84-158">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0fe84-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-to-your-web-app"></a><span data-ttu-id="0fe84-160">Stap 4: een aangepaste SSL-certificaat binden aan uw web-app</span><span class="sxs-lookup"><span data-stu-id="0fe84-160">Step 4 - Bind a custom SSL certificate to your web app</span></span>

<span data-ttu-id="0fe84-161">U hebt nu een Azure-web-app met de domeinnaam die u wilt dat in de adresbalk van de browser.</span><span class="sxs-lookup"><span data-stu-id="0fe84-161">You now have an Azure web app, with the domain name you want in the browser's address bar.</span></span> <span data-ttu-id="0fe84-162">Echter, als u naar navigeren de `https://<your_custom_domain>` nu het ophalen van een certificaatfout.</span><span class="sxs-lookup"><span data-stu-id="0fe84-162">However, if you navigate to the `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="0fe84-164">Deze fout treedt op omdat uw web-app een SSL-certificaat-binding die overeenkomt met de naam van uw aangepaste domein nog geen.</span><span class="sxs-lookup"><span data-stu-id="0fe84-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="0fe84-165">Echter, u niet krijgt een fout als u de navigatiefunctie `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0fe84-165">However, you don't get an error if you navigate to `https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="0fe84-166">Dit komt doordat uw app, evenals alle apps van Azure App Service, is beveiligd met SSL-certificaat voor de `*.azurewebsites.net` jokertekendomein standaard.</span><span class="sxs-lookup"><span data-stu-id="0fe84-166">This is because your app, as well as all Azure App Service apps, is secured with the SSL certificate for the `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="0fe84-167">U moet toegang krijgen tot uw web-app op uw aangepaste domeinnaam, de SSL-certificaat voor uw aangepaste domein binden aan de web-app.</span><span class="sxs-lookup"><span data-stu-id="0fe84-167">In order to access your web app by your custom domain name, you need to bind the SSL certificate for your custom domain to the web app.</span></span> <span data-ttu-id="0fe84-168">Dit doet u in deze stap.</span><span class="sxs-lookup"><span data-stu-id="0fe84-168">You will do it in this step.</span></span> 

### <a name="upload-the-ssl-certificate"></a><span data-ttu-id="0fe84-169">Het SSL-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="0fe84-169">Upload the SSL certificate</span></span>

<span data-ttu-id="0fe84-170">Het SSL-certificaat voor uw aangepaste domein uploaden naar uw web-app met behulp van de [az appservice web config ssl uploaden](/cli/azure/appservice/web/config/ssl#upload) opdracht.</span><span class="sxs-lookup"><span data-stu-id="0fe84-170">Upload the SSL certificate for your custom domain to your web app by using the [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="0fe84-171">In de onderstaande opdracht vervangen `<app_name>` met de naam van uw unieke app `<path_to_ptx_file>` met het pad naar uw. PFX-bestand en `<password>` met het wachtwoord voor uw certificaat.</span><span class="sxs-lookup"><span data-stu-id="0fe84-171">In the command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with the path to your .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="0fe84-172">Wanneer het certificaat is geüpload, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0fe84-172">When the certificate is uploaded, the Azure CLI shows information similar to the following example:</span></span>

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

<span data-ttu-id="0fe84-173">Van de JSON-uitvoer `thumbprint` ziet u de vingerafdruk van het geüploade certificaat.</span><span class="sxs-lookup"><span data-stu-id="0fe84-173">From the JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="0fe84-174">Kopieer de waarde voor de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="0fe84-174">Copy its value for the next step.</span></span>

### <a name="bind-the-uploaded-ssl-certificate-to-the-web-app"></a><span data-ttu-id="0fe84-175">Het geüploade SSL-certificaat binden aan de web-app</span><span class="sxs-lookup"><span data-stu-id="0fe84-175">Bind the uploaded SSL certificate to the web app</span></span>

<span data-ttu-id="0fe84-176">Uw web-app heeft nu de aangepaste domeinnaam die u wilt en heeft ook een SSL-certificaat dat aangepaste domein beveiligt.</span><span class="sxs-lookup"><span data-stu-id="0fe84-176">Your web app now has the custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="0fe84-177">De enige nog te doen is de geüploade certificaat binden aan de web-app.</span><span class="sxs-lookup"><span data-stu-id="0fe84-177">The only thing left to do is to bind the uploaded certificate to the web app.</span></span> <span data-ttu-id="0fe84-178">U dit doen met behulp van de [az appservice web config ssl-binding](/cli/azure/appservice/web/config/ssl#bind) opdracht.</span><span class="sxs-lookup"><span data-stu-id="0fe84-178">You do this by using the [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="0fe84-179">In de onderstaande opdracht vervangen `<app_name>` met de naam van uw unieke app en `<thumbprint-from-previous-output>` met de certificaatvingerafdruk die u via de vorige opdracht.</span><span class="sxs-lookup"><span data-stu-id="0fe84-179">In the command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with the certificate thumbprint that you get from the previous command.</span></span> 

<span data-ttu-id="0fe84-180">AZ appservice web config ssl bind--naam < app_naam >--resourcegroep myResourceGroup--certificaatvingerafdruk < vingerafdruk-van-vorige-output >--ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="0fe84-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="0fe84-181">Wanneer het certificaat is gekoppeld aan uw web-app, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0fe84-181">When the certificate is bound to your web app, the Azure CLI shows information similar to the following example:</span></span>

<span data-ttu-id="0fe84-182">{'Meldingenbeheer': 'Normale', 'clientAffinityEnabled': true, 'clientCertEnabled': false 'cloningInfo': null, 'containerSize': 0, "dailyMemoryTimeQuota": 0, "defaultHostName': ' < app_naam >. azurewebsites.net ', 'enabled': true, 'enabledHostNames': ['www.contoso.com' ' < app_naam >. azurewebsites.net ', ' < app_naam >. scm.azurewebsites.net '], 'gatewaySiteName': null, 'hostNameSslStates': [{'hostType': 'Standaard', 'name': ' < app_naam >. azurewebsites.net ', 'sslState': 'Disabled', 'vingerafdruk': null, 'toUpdate': null, 'virtualIp': null}, {'hostType': 'opslagplaats", "name": ' < app_naam >. scm.azurewebsites.net ', 'sslState': "Uitgeschakeld" 'vingerafdruk': null, 'toUpdate': null, 'virtualIp': null}, {'hostType': 'Standaard', 'name': 'www.contoso.com', 'sslState': 'SniEnabled' 'vingerafdruk': '9FD1D2D06E2293673E2A8D1CA484A092BD016D00', 'toUpdate': null, 'virtualIp': null}], 'hostnamen': ['www.contoso.com' ' < app_naam >. azurewebsites.net '], 'hostNamesDisabled': false 'hostingEnvironmentProfile': null 'id': ' /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s / < app_naam > ', 'isDefaultContainer': null, 'type': 'WebApp', 'lastModifiedTimeUtc': ' 2017-03-29T14:36:18.803333 ', 'locatie': 'West-Europa', 'maxNumberOfWorkers': null, 'microService': 'false', 'name': "< app_naam >" 'outboundIpAddresses': '13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1', 'premiumAppDeployed': null, 'repositorySiteName': '< app_naam >', 'gereserveerd': false 'resourceGroup': 'myResourceGroup', 'scmSiteAlsoStopped': false 'serverFarmId': ' / abonnementen/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft t.Web/serverfarms/myAppServicePlan ', 'siteConfig': null, 'slotSwapStatus': null, 'status': 'Actief', 'suspendedTill': null, 'labels': null, 'targetSwapSlot': null, 'trafficManagerHostNames': null, 'type': 'Microsoft.Web/sites', 'usageState': 'Standaard'}</span><span class="sxs-lookup"><span data-stu-id="0fe84-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="0fe84-183">Ga in uw browser naar HTTPS-eindpunt van uw aangepaste domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="0fe84-183">In your browser, navigate to HTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="0fe84-184">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0fe84-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="0fe84-186">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="0fe84-186">More resources</span></span>

<span data-ttu-id="0fe84-187">[Kopen en een aangepaste domeinnaam configureren in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[kopen en configureren van een SSL-certificaat voor uw Azure App Service](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="0fe84-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
