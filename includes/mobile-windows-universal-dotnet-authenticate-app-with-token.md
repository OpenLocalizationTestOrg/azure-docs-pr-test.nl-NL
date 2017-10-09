
1. <span data-ttu-id="34773-101">Voeg in MainPage.xaml.cs projectbestand Hallo Hallo volgende **met** instructies:</span><span class="sxs-lookup"><span data-stu-id="34773-101">In hello MainPage.xaml.cs project file, add hello following **using** statements:</span></span>
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. <span data-ttu-id="34773-102">Vervang Hallo **AuthenticateAsync** methode Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="34773-102">Replace hello **AuthenticateAsync** method with hello following code:</span></span>
   
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
   
    <span data-ttu-id="34773-103">In deze versie van **AuthenticateAsync**, Hallo app probeert toouse-referenties die zijn opgeslagen op Hallo **PasswordVault** tooaccess Hallo service.</span><span class="sxs-lookup"><span data-stu-id="34773-103">In this version of **AuthenticateAsync**, hello app tries toouse credentials stored in hello **PasswordVault** tooaccess hello service.</span></span> <span data-ttu-id="34773-104">Een gewone aanmelden wordt ook uitgevoerd wanneer er geen opgeslagen referenties.</span><span class="sxs-lookup"><span data-stu-id="34773-104">A regular sign-in is also performed when there is no stored credential.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="34773-105">Een token in cache mogelijk verlopen en verlopen van het token na verificatie kan ook optreden wanneer Hallo-app gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="34773-105">A cached token may be expired, and token expiration can also occur after authentication when hello app is in use.</span></span> <span data-ttu-id="34773-106">hoe toodetermine als een token is verlopen, Zie toolearn [controleren voor verlopen verificatietokens](http://aka.ms/jww5vp).</span><span class="sxs-lookup"><span data-stu-id="34773-106">toolearn how toodetermine if a token is expired, see [Check for expired authentication tokens](http://aka.ms/jww5vp).</span></span> <span data-ttu-id="34773-107">Verwante tooexpiring tokens, Zie voor een oplossing toohandling autorisatie fouten Hallo boeken [opslaan in cache en het verwerken van verlopen tokens in Azure Mobile Services SDK beheerd](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="34773-107">For a solution toohandling authorization errors related tooexpiring tokens, see hello post [Caching and handling expired tokens in Azure Mobile Services managed SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span></span> 
   > 
   > 
3. <span data-ttu-id="34773-108">Hallo app twee keer opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="34773-108">Restart hello app twice.</span></span>
   
    <span data-ttu-id="34773-109">Merk op dat op de eerste opstarten hello, aanmelden met Hallo provider is opnieuw vereist.</span><span class="sxs-lookup"><span data-stu-id="34773-109">Notice that on hello first start-up, sign-in with hello provider is again required.</span></span> <span data-ttu-id="34773-110">Echter op de tweede keer opnieuw opstarten Hallo Hallo in de cache opgeslagen referenties worden gebruikt en de aanmeldingspagina wordt overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="34773-110">However, on hello second restart hello cached credentials are used and sign-in is bypassed.</span></span> 

