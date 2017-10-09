1. In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **publiceren**. Kies **Nieuw maken** en klik vervolgens op **Publiceren**. 

    ![Nieuwe functie-app maken publiceren](./media/functions-vstools-publish/functions-vstools-publish-new-function-app.png)

2. Als u dit nog niet hebt al Visual Studio tooyour Azure-account verbonden, klikt u op **account toevoegen...** .  

3. In Hallo **Create App Service** dialoogvenster, gebruik Hallo **Hosting** instellingen opgegeven in de Hallo volgende tabel: 

    ![Lokale Azure-runtime](./media/functions-vstools-publish/functions-vstools-publish.png)

    | Instelling      | Voorgestelde waarde  | Beschrijving                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Naam van app** | Wereldwijd unieke naam | Naam waarmee uw nieuwe functie-app uniek wordt aangeduid. |
    | **Abonnement** | Kies uw abonnement | Hello Azure-abonnement toouse. |
    | **[Resourcegroep](../articles/azure-resource-manager/resource-group-overview.md)** | myResourceGroup |  Naam van de resource Hallo groeperen in welke toocreate functie-app. |
    | **[App-serviceabonnement](../articles/azure-functions/functions-scale.md)** | Verbruiksabonnement | Zorg ervoor dat toochoose hello **verbruik** onder **grootte** wanneer u een nieuw plan maakt.  |
    | **[Opslagaccount](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** | Wereldwijd unieke naam | Gebruik een bestaand opslagaccount of maak een nieuw.   |

4. Klik op **maken** toocreate een functie-app in Azure met deze instellingen. Nadat het Hallo inrichten is voltooid, maak een notitie van Hallo **Site-URL** waarde, Hallo-adres van de functie-app in Azure. 

    ![Lokale Azure-runtime](./media/functions-vstools-publish/functions-vstools-publish-profile.png)
