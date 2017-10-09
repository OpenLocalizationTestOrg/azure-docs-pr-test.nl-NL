<span data-ttu-id="8428c-101">Gebruik hello Azure CLI tooget Hallo implementatie van externe URL voor uw API-App.</span><span class="sxs-lookup"><span data-stu-id="8428c-101">Use hello Azure CLI tooget hello remote deployment URL for your API App.</span></span> <span data-ttu-id="8428c-102">Hallo opdracht, na Vervang in  *\<app_naam >* met de naam van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="8428c-102">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="8428c-103">Configureer uw lokale Git-implementatie toobe kunnen toopush toohello externe.</span><span class="sxs-lookup"><span data-stu-id="8428c-103">Configure your local Git deployment toobe able toopush toohello remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="8428c-104">Push toohello Azure externe toodeploy uw app.</span><span class="sxs-lookup"><span data-stu-id="8428c-104">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="8428c-105">U wordt gevraagd voor Hallo wachtwoord die u eerder hebt gemaakt toen u Hallo implementatie gebruiker gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8428c-105">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="8428c-106">Zorg ervoor dat u invoert Hallo wachtwoord die u eerder in Hallo Quick Start hebt gemaakt en niet Hallo wachtwoord waarmee u toolog in toohello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8428c-106">Make sure that you enter hello password you created in earlier in hello quickstart, and not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```
