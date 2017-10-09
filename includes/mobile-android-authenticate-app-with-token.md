
Hallo vorige voorbeeld had betrekking op een standaard aanmelden, waardoor Hallo client toocontact vereist zowel Hallo-id-provider en Hallo back-end Azure service telkens wanneer Hallo-app wordt gestart. Deze methode is inefficiënt en u kunt problemen met de informatie over het gebruik hebben als veel klanten toostart uw app tegelijk probeert. Er is een betere benadering toocache Hallo verificatietoken geretourneerd door hello Azure-service en probeer toouse dit eerst voordat met behulp van een providergebaseerde aanmelden.

> [!NOTE]
> U kunt Hallo token dat is uitgegeven door de back-end hello Azure-service ongeacht of u van verificatie van client beheerd of service gebruikmaakt-cache. Deze zelfstudie maakt gebruik van authentication service beheerd.
>
>

1. Hallo ToDoActivity.java bestand openen en voeg Hallo volgende importinstructies toe:

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. Toevoegen van leden toohello na Hallo `ToDoActivity` klasse.

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. In het bestand ToDoActivity.java hello, toevoegen na de definitie voor Hallo Hallo `cacheUserToken` methode.

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    Deze methode slaat Hallo gebruikers-ID en -token in een voorkeursbestand dat is gemarkeerd als privé. Dit moet toegang toohello cache beveiligen zodat andere apps op Hallo apparaat hebben geen toohello toegangstoken. Hallo voorkeur is sandbox voor Hallo-app. Als iemand toegang toohello apparaat krijgt, is het echter mogelijk dat ze toegang toohello tokencache via andere middelen kunnen krijgen.

   > [!NOTE]
   > U kunt verder Hallo-token met versleuteling, beschermen tokentoegang tooyour gegevens als zeer vertrouwelijk worden beschouwd als iemand toohello-toegangsapparaat kan krijgen. Een volledig veilige oplossing valt buiten bereik van deze zelfstudie Hallo echter en is afhankelijk van uw beveiligingsvereisten.
   >
   >
4. In het bestand ToDoActivity.java hello, toevoegen na de definitie voor Hallo Hallo `loadUserTokenCache` methode.

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
5. In Hallo *ToDoActivity.java* bestand, vervangt u Hallo `authenticate` methode Hello methode, die gebruikmaakt van een token cache te volgen. Hallo aanmeldingsprovider wijzigen als u wilt dat een ander account dan Google toouse.

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
6. Hallo-app en test verificatie met een geldig account maken. Ten minste tweemaal wordt uitgevoerd. Tijdens Hallo voor het eerst uitvoert, moet u een prompt toosign in ontvangen en Hallo tokencache maken. Daarna probeert elke uitvoering tooload Hallo tokencache voor verificatie. U mag geen vereiste toosign in.
