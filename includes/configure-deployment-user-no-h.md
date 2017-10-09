<span data-ttu-id="efe03-101">Maak implementatiereferenties Hello [az webapp implementatiegebruiker ingesteld](/cli/azure/webapp/deployment/user#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="efe03-101">Create deployment credentials with hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="efe03-102">Implementatie van een gebruiker is vereist voor de FTP- en lokale Git-implementatie tooa web-app.</span><span class="sxs-lookup"><span data-stu-id="efe03-102">A deployment user is required for FTP and local Git deployment tooa web app.</span></span> <span data-ttu-id="efe03-103">Hallo-gebruikersnaam en wachtwoord zijn niveau.</span><span class="sxs-lookup"><span data-stu-id="efe03-103">hello user name and password are account level.</span></span> <span data-ttu-id="efe03-104">_Deze verschillen van de referenties van uw Azure-abonnement._</span><span class="sxs-lookup"><span data-stu-id="efe03-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="efe03-105">Hallo opdracht, na Vervang in  *\<gebruikersnaam >* en  *\<wachtwoord >* met een nieuwe gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="efe03-105">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="efe03-106">Hallo-gebruikersnaam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="efe03-106">hello user name must be unique.</span></span> <span data-ttu-id="efe03-107">Hallo wachtwoord moet ten minste acht tekens lang zijn, met twee Hallo na drie elementen: letters, cijfers, symbolen.</span><span class="sxs-lookup"><span data-stu-id="efe03-107">hello password must be at least eight characters long, with two of hello following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="efe03-108">Als u krijgt een ` 'Conflict'. Details: 409` fout, wijziging Hallo gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="efe03-108">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="efe03-109">Als er een ` 'Bad Request'. Details: 400`-fout optreedt, kiest u een sterker wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="efe03-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="efe03-110">U hoeft deze implementatiegebruiker maar één keer te maken. Vervolgens kunt u deze voor al uw Azure-implementaties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="efe03-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="efe03-111">Record Hallo-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="efe03-111">Record hello user name and password.</span></span> <span data-ttu-id="efe03-112">U nodig deze web-app voor toodeploy hello later.</span><span class="sxs-lookup"><span data-stu-id="efe03-112">You need them toodeploy hello web app later.</span></span>
>
>