### <a name="app-service-plan"></a><span data-ttu-id="26490-101">App Service-plan</span><span class="sxs-lookup"><span data-stu-id="26490-101">App Service plan</span></span>
<span data-ttu-id="26490-102">Hallo-serviceplan voor het hosten van Hallo web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="26490-102">Creates hello service plan for hosting hello web app.</span></span> <span data-ttu-id="26490-103">U Hallo naam opgeven van Hallo plan via Hallo **hostingPlanName** parameter.</span><span class="sxs-lookup"><span data-stu-id="26490-103">You provide hello name of hello plan through hello **hostingPlanName** parameter.</span></span> <span data-ttu-id="26490-104">Hallo-locatie van Hallo plan is dezelfde locatie worden gebruikt voor de resourcegroep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="26490-104">hello location of hello plan is hello same location used for hello resource group.</span></span> <span data-ttu-id="26490-105">Hallo prijscategorie laag- en werkrollen grootte zijn opgegeven in Hallo **sku** en **workerSize** parameters</span><span class="sxs-lookup"><span data-stu-id="26490-105">hello pricing tier and worker size are specified in hello **sku** and **workerSize** parameters</span></span>

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

