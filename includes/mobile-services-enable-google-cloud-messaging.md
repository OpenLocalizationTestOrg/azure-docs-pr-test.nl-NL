
1. <span data-ttu-id="4e8f5-101">Navigeer toohello [Google Cloud Console](https://console.developers.google.com/project), meld u aan met de referenties van uw Google-account.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-101">Navigate toohello [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="4e8f5-102">Klik op **Project maken**, typ een naam voor het project en klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="4e8f5-103">Als aangevraagd, verrichten Hallo SMS-verificatie en op **maken** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-103">If requested, carry out hello SMS Verification, and click **Create** again.</span></span>
   
    ![Nieuw project maken](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="4e8f5-105">Typ uw nieuwe **projectnaam** en klik op **Project maken**.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="4e8f5-106">Klik op Hallo **hulpprogramma's en meer** knop en klik vervolgens op **projectgegevens**.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-106">Click hello **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="4e8f5-107">Maak een notitie van Hallo **projectnummer**.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-107">Make a note of hello **Project Number**.</span></span> <span data-ttu-id="4e8f5-108">U tooset moet deze waarde als Hallo `SenderId` variabele in Hallo client-app.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-108">You will need tooset this value as hello `SenderId` variable in hello client app.</span></span>
   
    ![Hulpprogramma's en meer](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="4e8f5-110">Project in Hallo dashboard onder **mobiele API's**, klikt u op **Google Cloud Messaging**, klik op de volgende pagina Hallo **API inschakelen** en Hallo gebruiksrechtovereenkomst accepteren.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-110">In hello project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on hello next page click **Enable API** and accept hello terms of service.</span></span> 
   
    ![GCM inschakelen](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![GCM inschakelen](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="4e8f5-113">Klik in het projectdashboard hello, **referenties** > **referentie maken** > **API-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-113">In hello project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="4e8f5-114">In **Een nieuwe sleutel maken** klikt u op **Serversleutel**, typt u een naam voor de sleutel en klikt u vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="4e8f5-115">Maak een notitie van Hallo **API-sleutel** waarde.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-115">Make a note of hello **API KEY** value.</span></span>
   
    <span data-ttu-id="4e8f5-116">U gebruikt deze API-sleutelwaarde tooenable Azure tooauthenticate met GCM en om pushmeldingen te verzenden namens uw app.</span><span class="sxs-lookup"><span data-stu-id="4e8f5-116">You will use this API key value tooenable Azure tooauthenticate with GCM and send push notifications on behalf of your app.</span></span>

