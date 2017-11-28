<span data-ttu-id="60c13-101">Implementatiereferenties maken met de opdracht [az webapp deployment user set](/cli/azure/webapp/deployment/user#set).</span><span class="sxs-lookup"><span data-stu-id="60c13-101">Create deployment credentials with the [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="60c13-102">Een implementatiegebruiker is vereist voor FTP- en lokale Git-implementatie naar een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="60c13-102">A deployment user is required for FTP and local Git deployment to a web app.</span></span> <span data-ttu-id="60c13-103">De gebruikersnaam en het wachtwoord staan op accountniveau.</span><span class="sxs-lookup"><span data-stu-id="60c13-103">The user name and password are account level.</span></span> <span data-ttu-id="60c13-104">_Deze verschillen van de referenties van uw Azure-abonnement._</span><span class="sxs-lookup"><span data-stu-id="60c13-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="60c13-105">Vervang in de volgende opdracht *\<user-name>* en *\<password>* door een nieuwe gebruikersnaam en nieuw wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="60c13-105">In the following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="60c13-106">De gebruikersnaam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="60c13-106">The user name must be unique.</span></span> <span data-ttu-id="60c13-107">Het wachtwoord moet ten minste acht tekens lang zijn en minimaal twee van de volgende drie typen elementen bevatten: letters, cijfers, symbolen.</span><span class="sxs-lookup"><span data-stu-id="60c13-107">The password must be at least eight characters long, with two of the following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="60c13-108">Als er een ` 'Conflict'. Details: 409`-fout optreedt, wijzigt u de gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="60c13-108">If you get a ` 'Conflict'. Details: 409` error, change the username.</span></span> <span data-ttu-id="60c13-109">Als er een ` 'Bad Request'. Details: 400`-fout optreedt, kiest u een sterker wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="60c13-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="60c13-110">U hoeft deze implementatiegebruiker maar één keer te maken. Vervolgens kunt u deze voor al uw Azure-implementaties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="60c13-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="60c13-111">Leg de gebruikersnaam en het wachtwoord vast.</span><span class="sxs-lookup"><span data-stu-id="60c13-111">Record the user name and password.</span></span> <span data-ttu-id="60c13-112">U hebt ze later nodig bij het implementeren van de webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="60c13-112">You need them to deploy the web app later.</span></span>
>
>