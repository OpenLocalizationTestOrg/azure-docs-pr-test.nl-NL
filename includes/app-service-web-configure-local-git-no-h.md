<span data-ttu-id="4599b-101">Lokale Git-implementatie toohello web-app configureren met Hallo [bron in az webapp implementatie-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4599b-101">Configure local Git deployment toohello web app with hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="4599b-102">App Service biedt ondersteuning voor verschillende manieren toodeploy inhoud tooa web-app, zoals FTP-, lokale Git, Visual Studio Team Services, GitHub en Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="4599b-102">App Service supports several ways toodeploy content tooa web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="4599b-103">In deze snelstartgids gaat u implementeren met behulp van een lokale Git.</span><span class="sxs-lookup"><span data-stu-id="4599b-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="4599b-104">Dit betekent dat u implementeert met behulp van een opdracht Git toopush uit een lokale opslagplaats tooa-opslagplaats in Azure.</span><span class="sxs-lookup"><span data-stu-id="4599b-104">That means you deploy by using a Git command toopush from a local repository tooa repository in Azure.</span></span> 

<span data-ttu-id="4599b-105">Hallo opdracht, na Vervang in  *\<app_naam >* met de naam van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="4599b-105">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="4599b-106">Hallo-uitvoer heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="4599b-106">hello output has hello following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="4599b-107">Hallo `<username>` Hallo is [implementatie gebruiker](#configure-a-deployment-user) die u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4599b-107">hello `<username>` is hello [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="4599b-108">Hallo URI weergegeven; kopiëren u gaat deze in de volgende stap hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4599b-108">Copy hello URI shown; you'll use it in hello next step.</span></span>
