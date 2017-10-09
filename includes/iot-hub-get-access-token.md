## <a name="obtain-an-azure-resource-manager-token"></a>Een Azure Resource Manager-token verkrijgen
Azure Active Directory moeten alle Hallo-taken die u uitvoert op resources met behulp van hello Azure Resource Manager verifiëren. Hallo voorbeeld gebruikt wachtwoordverificatie, voor Zie andere benaderingen [verificatie van Azure Resource Manager-aanvragen][lnk-authenticate-arm].

1. Hallo na code toohello toevoegen **Main** methode in Program.cs tooretrieve een token van Azure AD met Hallo toepassings-id en wachtwoord.
   
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
2. Maak een **ResourceManagementClient** object dat wordt gebruikt token door toe te voegen na code toohello Hallo HALLO hallo **Main** methode:
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. Maken of een verwijzing naar Hallo-resourcegroep die u gebruikt:
   
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