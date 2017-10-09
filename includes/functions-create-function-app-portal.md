1. Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

1. Klik op **Compute** > **Functie-app**, selecteer uw **Abonnement**. Vervolgens Hallo functie app-instellingen gebruikt zoals opgegeven in de tabel Hallo.

    ![Functie-app maken in hello Azure-portal](./media/functions-create-function-app-portal/function-app-create-flow.png)

    | Instelling      | Voorgestelde waarde  | Beschrijving                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Naam van app** | Wereldwijd unieke naam | Naam waarmee uw nieuwe functie-app wordt aangeduid. | 
    | **[Resourcegroep](../articles/azure-resource-manager/resource-group-overview.md)** |  myResourceGroup | Geef een naam voor de nieuwe resourcegroep in welke toocreate Hallo functie-app. | 
    | **[Hostingplan](../articles/azure-functions/functions-scale.md)** |   Verbruiksabonnement | Hosting plan die definieert hoe tooyour functie-app worden toegewezen. In de standaard Hallo **verbruik plannen**, bronnen dynamisch zoals vereist door uw functies zijn toegevoegd. U betaalt alleen voor Hallo tijd die uw functies worden uitgevoerd.   |
    | **Locatie** | West-Europa | Kies een locatie in de buurt of in de buurt van andere services die door uw functies worden gebruikt. |
    | **[Opslagaccount](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** |  Wereldwijd unieke naam |  Naam van Hallo nieuwe opslagaccount die wordt gebruikt door de functie-app. Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten. U kunt ook een bestaand account gebruiken. |

1. Klik op **maken** tooprovision en Hallo nieuwe functie-app implementeren.
