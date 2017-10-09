Gebruik hello Azure CLI tooget Hallo implementatie van externe URL voor uw API-App. Hallo opdracht, na Vervang in  *\<app_naam >* met de naam van uw web-app.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Configureer uw lokale Git-implementatie toobe kunnen toopush toohello externe.

```bash
git remote add azure <URI from previous step>
```

Push toohello Azure externe toodeploy uw app. U wordt gevraagd voor Hallo wachtwoord die u eerder hebt gemaakt toen u Hallo implementatie gebruiker gemaakt. Zorg ervoor dat u invoert Hallo wachtwoord die u eerder in Hallo Quick Start hebt gemaakt en niet Hallo wachtwoord waarmee u toolog in toohello Azure-portal.

```bash
git push azure master
```
