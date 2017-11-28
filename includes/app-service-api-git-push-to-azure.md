<span data-ttu-id="f5983-101">De Azure CLI gebruiken om de externe implementatie-URL voor uw API-toepassing op te halen.</span><span class="sxs-lookup"><span data-stu-id="f5983-101">Use the Azure CLI to get the remote deployment URL for your API App.</span></span> <span data-ttu-id="f5983-102">Vervang in de volgende opdracht *\<app_name>* door de naam van uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="f5983-102">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="f5983-103">Configureer uw lokale Git-implementatie zodat deze naar de externe instantie kan pushen.</span><span class="sxs-lookup"><span data-stu-id="f5983-103">Configure your local Git deployment to be able to push to the remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="f5983-104">Push naar de externe Azure-instantie om uw app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="f5983-104">Push to the Azure remote to deploy your app.</span></span> <span data-ttu-id="f5983-105">U wordt gevraagd naar het wachtwoord dat u eerder hebt gemaakt bij het maken van de implementatiegebruiker.</span><span class="sxs-lookup"><span data-stu-id="f5983-105">You are prompted for the password you created earlier when you created the deployment user.</span></span> <span data-ttu-id="f5983-106">Zorg ervoor dat u het wachtwoord gebruikt dat u eerder in de snelstartgids hebt gemaakt en niet het wachtwoord dat u gebruikt om u aan te melden bij Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f5983-106">Make sure that you enter the password you created in earlier in the quickstart, and not the password you use to log in to the Azure portal.</span></span>

```bash
git push azure master
```
