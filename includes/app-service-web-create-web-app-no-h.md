<span data-ttu-id="4b6f4-101">Maak een [web-app](../articles/app-service-web/app-service-web-overview.md) in Hallo `myAppServicePlan` App Service-abonnement met Hallo [az webapp maken](/cli/azure/webapp#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b6f4-101">Create a [web app](../articles/app-service-web/app-service-web-overview.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="4b6f4-102">Hallo-web-app hier hosting voor uw code en een URL tooview Hallo geïmplementeerd app biedt.</span><span class="sxs-lookup"><span data-stu-id="4b6f4-102">hello web app provides a hosting space for your code and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="4b6f4-103">Hallo opdracht, na Vervang in  *\<app_naam >* met een unieke naam (geldige tekens zijn `a-z`, `0-9`, en `-`).</span><span class="sxs-lookup"><span data-stu-id="4b6f4-103">In hello following command, replace *\<app_name>* with a unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="4b6f4-104">Als `<app_name>` is niet uniek zijn, u krijgt Hallo foutbericht "De Website met de gegeven naam < app_naam > al bestaat."</span><span class="sxs-lookup"><span data-stu-id="4b6f4-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="4b6f4-105">standaard-URL van de web-app Hallo is Hallo `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="4b6f4-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="4b6f4-106">Wanneer het Hallo-web-app is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b6f4-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="4b6f4-107">Blader toohello site toosee uw nieuwe web-app.</span><span class="sxs-lookup"><span data-stu-id="4b6f4-107">Browse toohello site toosee your newly created web app.</span></span>

```bash
http://<app_name>.azurewebsites.net
```
