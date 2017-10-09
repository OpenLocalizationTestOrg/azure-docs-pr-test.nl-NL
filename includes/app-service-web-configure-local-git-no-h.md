Lokale Git-implementatie toohello web-app configureren met Hallo [bron in az webapp implementatie-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) opdracht.

App Service biedt ondersteuning voor verschillende manieren toodeploy inhoud tooa web-app, zoals FTP-, lokale Git, Visual Studio Team Services, GitHub en Bitbucket. In deze snelstartgids gaat u implementeren met behulp van een lokale Git. Dit betekent dat u implementeert met behulp van een opdracht Git toopush uit een lokale opslagplaats tooa-opslagplaats in Azure. 

Hallo opdracht, na Vervang in  *\<app_naam >* met de naam van uw web-app.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Hallo-uitvoer heeft Hallo volgende indeling:

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

Hallo `<username>` Hallo is [implementatie gebruiker](#configure-a-deployment-user) die u in de vorige stap hebt gemaakt.

Hallo URI weergegeven; kopiëren u gaat deze in de volgende stap hello gebruiken.
