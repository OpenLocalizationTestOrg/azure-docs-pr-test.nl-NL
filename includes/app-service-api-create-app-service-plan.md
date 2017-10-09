Maken van een App Service-abonnement met Hallo [az appservice-abonnement maken](/cli/azure/appservice/plan#create) opdracht.

[!INCLUDE [app-service-plan](app-service-plan.md)]

Hallo volgende voorbeeld maakt u een App Service-abonnement met de naam `myAppServicePlan` in Hallo **vrije** prijscategorie:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Wanneer Hallo App Service-abonnement is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "West Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
```