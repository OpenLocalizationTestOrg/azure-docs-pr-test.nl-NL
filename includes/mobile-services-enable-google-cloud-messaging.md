
1. Navigeer toohello [Google Cloud Console](https://console.developers.google.com/project), meld u aan met de referenties van uw Google-account. 
2. Klik op **Project maken**, typ een naam voor het project en klik vervolgens op **Maken**. Als aangevraagd, verrichten Hallo SMS-verificatie en op **maken** opnieuw.
   
    ![Nieuw project maken](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     Typ uw nieuwe **projectnaam** en klik op **Project maken**.
3. Klik op Hallo **hulpprogramma's en meer** knop en klik vervolgens op **projectgegevens**. Maak een notitie van Hallo **projectnummer**. U tooset moet deze waarde als Hallo `SenderId` variabele in Hallo client-app.
   
    ![Hulpprogramma's en meer](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. Project in Hallo dashboard onder **mobiele API's**, klikt u op **Google Cloud Messaging**, klik op de volgende pagina Hallo **API inschakelen** en Hallo gebruiksrechtovereenkomst accepteren. 
   
    ![GCM inschakelen](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![GCM inschakelen](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. Klik in het projectdashboard hello, **referenties** > **referentie maken** > **API-sleutel**. 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. In **Een nieuwe sleutel maken** klikt u op **Serversleutel**, typt u een naam voor de sleutel en klikt u vervolgens op **Maken**.
7. Maak een notitie van Hallo **API-sleutel** waarde.
   
    U gebruikt deze API-sleutelwaarde tooenable Azure tooauthenticate met GCM en om pushmeldingen te verzenden namens uw app.

