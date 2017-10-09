### <a name="app-service-plan"></a>App Service-plan
Hallo-serviceplan voor het hosten van Hallo web-app maakt. U Hallo naam opgeven van Hallo plan via Hallo **hostingPlanName** parameter. Hallo-locatie van Hallo plan is dezelfde locatie worden gebruikt voor de resourcegroep Hallo Hallo. Hallo prijscategorie laag- en werkrollen grootte zijn opgegeven in Hallo **sku** en **workerSize** parameters

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

