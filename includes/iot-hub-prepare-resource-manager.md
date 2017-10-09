## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a>Azure Resource Manager-aanvragen tooauthenticate voorbereiden
U moet alle Hallo-bewerkingen die u uitvoert op resources met behulp van Hallo verifiëren [Azure Resource Manager] [ lnk-authenticate-arm] met Azure Active Directory (AD). Hallo gemakkelijkste manier tooconfigure toouse PowerShell of Azure CLI.

Hallo installeren [Azure PowerShell-cmdlets] [ lnk-powershell-install] voordat u doorgaat.

Hallo van de volgende stappen tonen hoe tooset up wachtwoordverificatie voor een AD-toepassing met behulp van PowerShell. U kunt deze opdrachten uitvoeren in een standaard PowerShell-sessie.

1. Meld u bij tooyour Azure-abonnement met Hallo volgende opdracht:

    ```powershell
    Login-AzureRmAccount
    ```

1. Aanmelden tooAzure verleent u tooall toegang tot Azure-abonnementen die zijn gekoppeld aan uw referenties in Media Player Hallo als u meerdere Azure-abonnementen hebt. Hallo opdracht toolist hello Azure-abonnementen beschikbaar voor u toouse volgende gebruiken:

    ```powershell
    Get-AzureRMSubscription
    ```

    Gebruik Hallo opdracht tooselect abonnement dat u wilt dat uw IoT-hub-opdrachten toomanage toouse toorun hello te volgen. U kunt Hallo abonnementsnaam of ID van uitvoer van de vorige opdracht Hallo Hallo gebruiken:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. Maak een notitie van uw **TenantId** en **SubscriptionId**. U nodig ze later.
3. Maak een nieuwe Azure Active Directory-toepassing hello de volgende opdracht en vervangt Hallo plaats houders met:
   
   * **{Weergavenaam}:** een weergavenaam voor uw toepassing, zoals **MySampleApp**
   * **{URL startpagina}:** URL van de startpagina Hallo van uw app, zoals Hallo **http://mysampleapp/home**. Deze URL heeft geen toopoint tooa echte toepassing nodig.
   * **{Toepassings-id}:** een unieke id zoals **http://mysampleapp**. Deze URL heeft geen toopoint tooa echte toepassing nodig.
   * **{Wachtwoord}:** een wachtwoord dat u tooauthenticate met uw app.
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. Maak een notitie van Hallo **ApplicationId** van Hallo-toepassing die u hebt gemaakt. U nodig dit later.
5. Maak een nieuwe service-principal maken met Hallo de volgende opdracht en vervangt **{MyApplicationId}** Hello **ApplicationId** uit de vorige stap Hallo:
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. Instellen van een roltoewijzing met Hallo de volgende opdracht en vervangt **{MyApplicationId}** met uw **ApplicationId**.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

U bent nu klaar hello Azure AD-toepassing waarmee u tooauthenticate maken van uw aangepaste C#-toepassing. U moet Hallo waarden verderop in deze zelfstudie te volgen:

* TenantId
* SubscriptionId
* ApplicationId
* Wachtwoord

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
