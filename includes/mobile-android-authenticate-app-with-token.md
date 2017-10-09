
<span data-ttu-id="4f19b-101">Hallo vorige voorbeeld had betrekking op een standaard aanmelden, waardoor Hallo client toocontact vereist zowel Hallo-id-provider en Hallo back-end Azure service telkens wanneer Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="4f19b-101">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello back-end Azure service every time hello app starts.</span></span> <span data-ttu-id="4f19b-102">Deze methode is inefficiënt en u kunt problemen met de informatie over het gebruik hebben als veel klanten toostart uw app tegelijk probeert.</span><span class="sxs-lookup"><span data-stu-id="4f19b-102">This method is inefficient, and you can have usage-related issues if many customers try toostart your app simultaneously.</span></span> <span data-ttu-id="4f19b-103">Er is een betere benadering toocache Hallo verificatietoken geretourneerd door hello Azure-service en probeer toouse dit eerst voordat met behulp van een providergebaseerde aanmelden.</span><span class="sxs-lookup"><span data-stu-id="4f19b-103">A better approach is toocache hello authorization token returned by hello Azure service, and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="4f19b-104">U kunt Hallo token dat is uitgegeven door de back-end hello Azure-service ongeacht of u van verificatie van client beheerd of service gebruikmaakt-cache.</span><span class="sxs-lookup"><span data-stu-id="4f19b-104">You can cache hello token issued by hello back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="4f19b-105">Deze zelfstudie maakt gebruik van authentication service beheerd.</span><span class="sxs-lookup"><span data-stu-id="4f19b-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="4f19b-106">Hallo ToDoActivity.java bestand openen en voeg Hallo volgende importinstructies toe:</span><span class="sxs-lookup"><span data-stu-id="4f19b-106">Open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="4f19b-107">Toevoegen van leden toohello na Hallo `ToDoActivity` klasse.</span><span class="sxs-lookup"><span data-stu-id="4f19b-107">Add hello following members toohello `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="4f19b-108">In het bestand ToDoActivity.java hello, toevoegen na de definitie voor Hallo Hallo `cacheUserToken` methode.</span><span class="sxs-lookup"><span data-stu-id="4f19b-108">In hello ToDoActivity.java file, add hello following definition for hello `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="4f19b-109">Deze methode slaat Hallo gebruikers-ID en -token in een voorkeursbestand dat is gemarkeerd als privé.</span><span class="sxs-lookup"><span data-stu-id="4f19b-109">This method stores hello user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="4f19b-110">Dit moet toegang toohello cache beveiligen zodat andere apps op Hallo apparaat hebben geen toohello toegangstoken.</span><span class="sxs-lookup"><span data-stu-id="4f19b-110">This should protect access toohello cache so that other apps on hello device do not have access toohello token.</span></span> <span data-ttu-id="4f19b-111">Hallo voorkeur is sandbox voor Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="4f19b-111">hello preference is sandboxed for hello app.</span></span> <span data-ttu-id="4f19b-112">Als iemand toegang toohello apparaat krijgt, is het echter mogelijk dat ze toegang toohello tokencache via andere middelen kunnen krijgen.</span><span class="sxs-lookup"><span data-stu-id="4f19b-112">However, if someone gains access toohello device, it is possible that they may gain access toohello token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4f19b-113">U kunt verder Hallo-token met versleuteling, beschermen tokentoegang tooyour gegevens als zeer vertrouwelijk worden beschouwd als iemand toohello-toegangsapparaat kan krijgen.</span><span class="sxs-lookup"><span data-stu-id="4f19b-113">You can further protect hello token with encryption, if token access tooyour data is considered highly sensitive and someone may gain access toohello device.</span></span> <span data-ttu-id="4f19b-114">Een volledig veilige oplossing valt buiten bereik van deze zelfstudie Hallo echter en is afhankelijk van uw beveiligingsvereisten.</span><span class="sxs-lookup"><span data-stu-id="4f19b-114">A completely secure solution is beyond hello scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="4f19b-115">In het bestand ToDoActivity.java hello, toevoegen na de definitie voor Hallo Hallo `loadUserTokenCache` methode.</span><span class="sxs-lookup"><span data-stu-id="4f19b-115">In hello ToDoActivity.java file, add hello following definition for hello `loadUserTokenCache` method.</span></span>

        private boolean loadUserTokenCache(MobileServiceClient client)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            String userId = prefs.getString(USERIDPREF, null);
            if (userId == null)
                return false;
            String token = prefs.getString(TOKENPREF, null);
            if (token == null)
                return false;

            MobileServiceUser user = new MobileServiceUser(userId);
            user.setAuthenticationToken(token);
            client.setCurrentUser(user);

            return true;
        }
5. <span data-ttu-id="4f19b-116">In Hallo *ToDoActivity.java* bestand, vervangt u Hallo `authenticate` methode Hello methode, die gebruikmaakt van een token cache te volgen.</span><span class="sxs-lookup"><span data-stu-id="4f19b-116">In hello *ToDoActivity.java* file, replace hello `authenticate` method with hello following method, which uses a token cache.</span></span> <span data-ttu-id="4f19b-117">Hallo aanmeldingsprovider wijzigen als u wilt dat een ander account dan Google toouse.</span><span class="sxs-lookup"><span data-stu-id="4f19b-117">Change hello login provider if you want toouse an account other than Google.</span></span>

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. <span data-ttu-id="4f19b-118">Hallo-app en test verificatie met een geldig account maken.</span><span class="sxs-lookup"><span data-stu-id="4f19b-118">Build hello app and test authentication using a valid account.</span></span> <span data-ttu-id="4f19b-119">Ten minste tweemaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4f19b-119">Run it at least twice.</span></span> <span data-ttu-id="4f19b-120">Tijdens Hallo voor het eerst uitvoert, moet u een prompt toosign in ontvangen en Hallo tokencache maken.</span><span class="sxs-lookup"><span data-stu-id="4f19b-120">During hello first run, you should receive a prompt toosign in and create hello token cache.</span></span> <span data-ttu-id="4f19b-121">Daarna probeert elke uitvoering tooload Hallo tokencache voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="4f19b-121">After that, each run attempts tooload hello token cache for authentication.</span></span> <span data-ttu-id="4f19b-122">U mag geen vereiste toosign in.</span><span class="sxs-lookup"><span data-stu-id="4f19b-122">You should not be required toosign in.</span></span>
