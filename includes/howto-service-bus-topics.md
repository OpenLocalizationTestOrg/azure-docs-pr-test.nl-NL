## <a name="what-are-service-bus-topics-and-subscriptions"></a>Wat zijn Service Bus-onderwerpen en -abonnementen?
Service Bus-onderwerpen en -abonnementen bieden ondersteuning voor een berichtencommunicatiemodel op basis van *publiceren/abonneren*. Wanneer u gebruikmaakt van onderwerpen en abonnementen, communiceren onderdelen van een gedistribueerde toepassing niet direct met elkaar. In plaats daarvan wisselen ze berichten uit via een onderwerp dat als intermediair fungeert.

![TopicConcepts](./media/howto-service-bus-topics/sb-topics-01.png)

Anders dan bij Service Bus-wachtrijen, waarin elk bericht door een enkele gebruiker wordt verwerkt, bieden onderwerpen en abonnementen een 'één-naar-veel'-communicatiewijze, waarbij een patroon voor publiceren/abonneren wordt gebruikt. Het is mogelijk meerdere abonnementen tooa onderwerp registreren. Wanneer een bericht wordt verzonden tooa onderwerp, wordt deze beschikbaar tooeach abonnement toohandle/proces vervolgens afzonderlijk gemaakt.

Een abonnement tooa onderwerp lijkt op een virtuele wachtrij die kopieën van Hallo-berichten dat is verzonden toohello onderwerp ontvangt. U kunt eventueel filterregels voor een onderwerp op basis van per abonnement, waarmee u toofilter registreren of beperken welke berichten tooa onderwerp door welke onderwerpabonnementen worden ontvangen.

Service Bus-onderwerpen en abonnementen kunnen u tooscale en verwerken van een zeer groot aantal berichten voor veel gebruikers en toepassingen.

## <a name="create-a-namespace"></a>Een naamruimte maken
toobegin met Service Bus-onderwerpen en abonnementen in Azure, moet u eerst maken een *Servicenaamruimte*. Een naamruimte biedt een scoping container voor het verwerken van Service Bus-resources in uw toepassing.

een naamruimte toocreate:

1. Meld u aan toohello [Azure-portal][Azure portal].
2. Klik in het Hallo navigatiedeelvenster links van de portal Hallo op **nieuw**, klikt u vervolgens op **Enterprise Integration**, en klik vervolgens op **Service Bus**.
3. In Hallo **naamruimte maken** dialoogvenster, voer de naam van een naamruimte. Hallo-systeem wordt onmiddellijk toosee gecontroleerd als Hallo naam beschikbaar is.
4. Nadat u hebt ervoor Hallo naamruimtenaam is beschikbaar, kies Hallo prijscategorie (Basic, Standard of Premium).
5. In Hallo **abonnement** veld, kiest u een Azure-abonnement in welke toocreate Hallo-naamruimte.
6. In Hallo **resourcegroep** veld, kiest u een bestaande resourcegroep in welke Hallo naamruimte live of maak een nieuwe.      
7. In **locatie**, kiest u Hallo land of regio waarin uw naamruimte moet worden gehost.
   
    ![Een naamruimte maken][create-namespace]
8. Klik op Hallo **maken** knop. Hallo system nu uw naamruimte wordt gemaakt en ingeschakeld. Mogelijk hebt u toowait enkele minuten als Hallo bepalingen systeembronnen voor uw account.

### <a name="obtain-hello-credentials"></a>Hallo referenties ophalen
1. Klik in lijst Hallo van naamruimten op Hallo naamruimtenaam van een nieuw gemaakt.
2. In Hallo **Service Bus-naamruimte** blade, klikt u op **gedeeld toegangsbeleid**.
3. In Hallo **gedeeld toegangsbeleid** blade, klikt u op **RootManageSharedAccessKey**.
   
    ![verbinding-gegevens][connection-info]
4. In Hallo **beleid: RootManageSharedAccessKey** blade, klik op de knop kopiëren Hallo volgende te**Connection string – primaire sleutel**, toocopy Hallo connection string tooyour Klembord voor later gebruik.
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


