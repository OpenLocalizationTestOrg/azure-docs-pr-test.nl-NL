
1. Klik op Hallo **App Services** knop, selecteert u uw back-end van Mobile Apps, selecteer **Quick Start**, en selecteer vervolgens uw clientplatform (iOS, Android, Xamarin, Cordova).

    ![Azure Portal met Mobile Apps Quickstart gemarkeerd][quickstart]

2. Als de verbinding met een database niet is geconfigureerd, maakt u een door Hallo volgende te doen:

    ![Azure-portal met Mobile Apps Connect toodatabase][connect]

    a. Maak een nieuwe SQL-database en -server.

    ![Azure Portal met Mobile Apps: nieuwe database en server maken][server]

    b. Wacht totdat het Hallo-gegevensverbinding is gemaakt.

    ![Melding in Azure Portal dat de gegevensverbinding is gemaakt][notification]

    c. Gegevensverbinding moet zijn gelukt.

    ![Melding 'U hebt al een gegevensverbinding' in Azure Portal][already-connection]

3. Selecteer bij **2. Een tabel-API maken** de optie Node.js voor **Back-endtaal**. 
 
4. Hallo bevestiging accepteren en selecteer vervolgens **takentabel maken**.  
    Met deze actie wordt er een nieuwe takentabel in uw database gemaakt. 

    >[!IMPORTANT]
    > Alle inhoud overschakelen van een bestaande back-end-tooNode.js worden overschreven. een .NET-back-end in plaats daarvan Zie toocreate [werken met .NET back-end Hallo server SDK voor Mobile Apps][instructions].

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
