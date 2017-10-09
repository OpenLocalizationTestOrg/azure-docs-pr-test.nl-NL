1. Meld u aan toohello [Azure-portal][Azure portal].
2. Klik in het Hallo navigatiedeelvenster links van Hallo-portal op **nieuw**, klikt u vervolgens op **Enterprise Integration**, en klik vervolgens op **Relay**.
3. In Hallo **naamruimte maken** dialoogvenster, voer de naam van een naamruimte. Hallo-systeem wordt onmiddellijk toosee gecontroleerd als Hallo naam beschikbaar is.
4. In Hallo **abonnement** veld, kiest u een Azure-abonnement in welke toocreate Hallo-naamruimte.
5. In Hallo  **[resourcegroep](../articles/azure-resource-manager/resource-group-portal.md)**  veld, kiest u een bestaande resourcegroep in welke Hallo naamruimte live of maak een nieuwe.      
6. In **locatie**, kiest u Hallo land of regio waarin uw naamruimte moet worden gehost.
   
    ![Een naamruimte maken][create-namespace]
7. Klik op **Create**. Hallo system nu uw naamruimte wordt gemaakt en ingeschakeld. Na een paar minuten Hallo bepalingen systeembronnen voor uw account.

### <a name="obtain-hello-management-credentials"></a>Beheerreferenties ophalen Hallo
1. Klik in lijst Hallo van naamruimten op Hallo naamruimtenaam van een nieuw gemaakt.
2. Klik op Hallo naamruimte blade **gedeeld toegangsbeleid**.
3. In Hallo **gedeeld toegangsbeleid** blade, klikt u op **RootManageSharedAccessKey**.
   
    ![verbinding-gegevens][connection-info]
4. In Hallo **beleid: RootManageSharedAccessKey** blade, klik op de knop kopiëren Hallo volgende te**Connection string – primaire sleutel**, toocopy Hallo connection string tooyour Klembord voor later gebruik. Plak deze waarde in Kladblok of een andere tijdelijke locatie.
   
    ![connection-string][connection-string]

5. Herhaal Hallo vorige stap, kopiëren en plakken Hallo-waarde van **primaire sleutel** tooa tijdelijke locatie voor later gebruik.  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
