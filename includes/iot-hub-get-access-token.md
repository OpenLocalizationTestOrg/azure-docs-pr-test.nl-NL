## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="9211b-101">Een Azure Resource Manager-token verkrijgen</span><span class="sxs-lookup"><span data-stu-id="9211b-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="9211b-102">Azure Active Directory moeten alle Hallo-taken die u uitvoert op resources met behulp van hello Azure Resource Manager verifiëren.</span><span class="sxs-lookup"><span data-stu-id="9211b-102">Azure Active Directory must authenticate all hello tasks that you perform on resources using hello Azure Resource Manager.</span></span> <span data-ttu-id="9211b-103">Hallo voorbeeld gebruikt wachtwoordverificatie, voor Zie andere benaderingen [verificatie van Azure Resource Manager-aanvragen][lnk-authenticate-arm].</span><span class="sxs-lookup"><span data-stu-id="9211b-103">hello example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="9211b-104">Hallo na code toohello toevoegen **Main** methode in Program.cs tooretrieve een token van Azure AD met Hallo toepassings-id en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="9211b-104">Add hello following code toohello **Main** method in Program.cs tooretrieve a token from Azure AD using hello application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. <span data-ttu-id="9211b-105">Maak een **ResourceManagementClient** object dat wordt gebruikt token door toe te voegen na code toohello Hallo HALLO hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="9211b-105">Create a **ResourceManagementClient** object that uses hello token by adding hello following code toohello end of hello **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="9211b-106">Maken of een verwijzing naar Hallo-resourcegroep die u gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9211b-106">Create, or obtain a reference to, hello resource group you are using:</span></span>
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx