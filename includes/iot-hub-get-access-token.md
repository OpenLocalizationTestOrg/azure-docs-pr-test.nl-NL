## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="3d425-101">Een Azure Resource Manager-token verkrijgen</span><span class="sxs-lookup"><span data-stu-id="3d425-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="3d425-102">De taken die u uitvoert op resources met behulp van de Azure Resource Manager moeten worden geverifieerd door Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d425-102">Azure Active Directory must authenticate all the tasks that you perform on resources using the Azure Resource Manager.</span></span> <span data-ttu-id="3d425-103">Het voorbeeld gebruikt wachtwoordverificatie, voor Zie andere benaderingen [verificatie van Azure Resource Manager-aanvragen][lnk-authenticate-arm].</span><span class="sxs-lookup"><span data-stu-id="3d425-103">The example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="3d425-104">Voeg de volgende code naar de **Main** methode in Program.cs ophalen van een token van Azure AD met behulp van de toepassings-id en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="3d425-104">Add the following code to the **Main** method in Program.cs to retrieve a token from Azure AD using the application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed to obtain the token");
      return;
    }
    ```
2. <span data-ttu-id="3d425-105">Maak een **ResourceManagementClient** -object dat u het token gebruikt door de volgende code toe te voegen aan het einde van de **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="3d425-105">Create a **ResourceManagementClient** object that uses the token by adding the following code to the end of the **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="3d425-106">Maken of een verwijzing naar de resourcegroep die u gebruikt:</span><span class="sxs-lookup"><span data-stu-id="3d425-106">Create, or obtain a reference to, the resource group you are using:</span></span>
   
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