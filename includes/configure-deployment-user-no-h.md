Maak implementatiereferenties Hello [az webapp implementatiegebruiker ingesteld](/cli/azure/webapp/deployment/user#set) opdracht.

Implementatie van een gebruiker is vereist voor de FTP- en lokale Git-implementatie tooa web-app. Hallo-gebruikersnaam en wachtwoord zijn niveau. _Deze verschillen van de referenties van uw Azure-abonnement._

Hallo opdracht, na Vervang in  *\<gebruikersnaam >* en  *\<wachtwoord >* met een nieuwe gebruikersnaam en wachtwoord. Hallo-gebruikersnaam moet uniek zijn. Hallo wachtwoord moet ten minste acht tekens lang zijn, met twee Hallo na drie elementen: letters, cijfers, symbolen. 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

Als u krijgt een ` 'Conflict'. Details: 409` fout, wijziging Hallo gebruikersnaam. Als er een ` 'Bad Request'. Details: 400`-fout optreedt, kiest u een sterker wachtwoord.

U hoeft deze implementatiegebruiker maar één keer te maken. Vervolgens kunt u deze voor al uw Azure-implementaties gebruiken.

> [!NOTE]
> Record Hallo-gebruikersnaam en wachtwoord. U nodig deze web-app voor toodeploy hello later.
>
>