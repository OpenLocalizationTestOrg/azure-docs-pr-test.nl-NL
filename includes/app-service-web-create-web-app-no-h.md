Maak een [web-app](../articles/app-service-web/app-service-web-overview.md) in Hallo `myAppServicePlan` App Service-abonnement met Hallo [az webapp maken](/cli/azure/webapp#create) opdracht. 

Hallo-web-app hier hosting voor uw code en een URL tooview Hallo geïmplementeerd app biedt.

Hallo opdracht, na Vervang in  *\<app_naam >* met een unieke naam (geldige tekens zijn `a-z`, `0-9`, en `-`). Als `<app_name>` is niet uniek zijn, u krijgt Hallo foutbericht "De Website met de gegeven naam < app_naam > al bestaat." standaard-URL van de web-app Hallo is Hallo `https://<app_name>.azurewebsites.net`. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Wanneer het Hallo-web-app is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

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

Blader toohello site toosee uw nieuwe web-app.

```bash
http://<app_name>.azurewebsites.net
```
