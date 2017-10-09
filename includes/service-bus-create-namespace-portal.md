toobegin met Service Bus-wachtrijen in Azure, moet u eerst een naamruimte maken met een naam die uniek is voor alle Azure. Een naamruimte biedt een scoping container voor het verwerken van Service Bus-resources in uw toepassing.

een naamruimte toocreate:

1. Meld u aan toohello [Azure-portal][Azure portal].
2. Klik in het Hallo navigatiedeelvenster links van de portal Hallo op **nieuw**, klikt u vervolgens op **Enterprise Integration**, en klik vervolgens op **Service Bus**.
3. In Hallo **naamruimte maken** dialoogvenster, voer de naam van een naamruimte. Hallo-systeem wordt onmiddellijk toosee gecontroleerd als Hallo naam beschikbaar is.
4. Nadat u hebt ervoor Hallo naamruimtenaam is beschikbaar, kies Hallo prijscategorie (Basic, Standard of Premium).
5. In Hallo **abonnement** veld, kiest u een Azure-abonnement in welke toocreate Hallo-naamruimte.
6. In Hallo **resourcegroep** veld, kiest u een bestaande resourcegroep in welke Hallo naamruimte live of maak een nieuwe.      
7. In **locatie**, kiest u Hallo land of regio waarin uw naamruimte moet worden gehost.
   
    ![Een naamruimte maken][create-namespace]
8. Klik op **Create**. Hallo system nu uw naamruimte wordt gemaakt en ingeschakeld. Mogelijk hebt u toowait enkele minuten als Hallo bepalingen systeembronnen voor uw account.

### <a name="obtain-hello-management-credentials"></a>Beheerreferenties ophalen Hallo

1. Klik in lijst Hallo van naamruimten op Hallo naamruimtenaam van een nieuw gemaakt.
2. Klik op Hallo naamruimte blade **gedeeld toegangsbeleid**.
3. In Hallo **gedeeld toegangsbeleid** blade, klikt u op **RootManageSharedAccessKey**.
   
    ![verbinding-gegevens][connection-info]
4. In Hallo **beleid: RootManageSharedAccessKey** blade, klik op de knop kopiëren Hallo volgende te**Connection string – primaire sleutel**, toocopy Hallo connection string tooyour Klembord voor later gebruik. Plak deze waarde in Kladblok of een andere tijdelijke locatie.
   
    ![connection-string][connection-string]

5. Herhaal Hallo vorige stap, kopiëren en plakken Hallo-waarde van **primaire sleutel** tooa tijdelijke locatie voor later gebruik.

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
