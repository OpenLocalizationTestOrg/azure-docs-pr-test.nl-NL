
1. Voeg in MainPage.xaml.cs projectbestand Hallo Hallo volgende **met** instructies:
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. Vervang Hallo **AuthenticateAsync** methode Hello code te volgen:
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses hello Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use hello PasswordVault toosecurely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try tooget an existing credential from hello vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from hello stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set hello user from hello stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check toodetermine if hello token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with hello identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store hello user credentials.
                    credential = new PasswordCredential(provider.ToString(),
                        user.UserId, user.MobileServiceAuthenticationToken);
                    vault.Add(credential);
   
                    success = true;
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (MobileServiceInvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
   
            return success;
        }
   
    In deze versie van **AuthenticateAsync**, Hallo app probeert toouse-referenties die zijn opgeslagen op Hallo **PasswordVault** tooaccess Hallo service. Een gewone aanmelden wordt ook uitgevoerd wanneer er geen opgeslagen referenties.
   
   > [!NOTE]
   > Een token in cache mogelijk verlopen en verlopen van het token na verificatie kan ook optreden wanneer Hallo-app gebruikt wordt. hoe toodetermine als een token is verlopen, Zie toolearn [controleren voor verlopen verificatietokens](http://aka.ms/jww5vp). Verwante tooexpiring tokens, Zie voor een oplossing toohandling autorisatie fouten Hallo boeken [opslaan in cache en het verwerken van verlopen tokens in Azure Mobile Services SDK beheerd](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx). 
   > 
   > 
3. Hallo app twee keer opnieuw opgestart.
   
    Merk op dat op de eerste opstarten hello, aanmelden met Hallo provider is opnieuw vereist. Echter op de tweede keer opnieuw opstarten Hallo Hallo in de cache opgeslagen referenties worden gebruikt en de aanmeldingspagina wordt overgeslagen. 

