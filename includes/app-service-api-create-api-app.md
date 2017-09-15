
<span data-ttu-id="0b263-101">Maak een gratis [API-app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in het App Service-plan `myAppServicePlan` met de opdracht [az webapp create](/cli/azure/appservice/web#create).</span><span class="sxs-lookup"><span data-stu-id="0b263-101">Create a [API app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/appservice/web#create) command.</span></span> 

<span data-ttu-id="0b263-102">De web-app biedt hostruimte voor uw API en biedt een URL waarmee u de geïmplementeerde app kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="0b263-102">The web app provides a hosting space for your API and provides a URL to view the deployed app.</span></span>

<span data-ttu-id="0b263-103">Vervang in de volgende opdracht *\<app_name>* door een unieke naam.</span><span class="sxs-lookup"><span data-stu-id="0b263-103">In the following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="0b263-104">Als `<app_name>` niet uniek is, wordt er een foutbericht weergegeven met de mededeling dat er al een website bestaat met die naam.</span><span class="sxs-lookup"><span data-stu-id="0b263-104">If `<app_name>` is not unique, you get the error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="0b263-105">De standaard-URL van de web-app is `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0b263-105">The default URL of the web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="0b263-106">Wanneer de web-app is gemaakt, toont de Azure CLI soortgelijke informatie als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0b263-106">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```