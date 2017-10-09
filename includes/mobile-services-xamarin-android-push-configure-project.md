
1. <span data-ttu-id="bfea1-101">In de weergave oplossing Hallo (of **Solution Explorer** in Visual Studio), klik met de rechtermuisknop Hallo **onderdelen** map, klikt u op **meer onderdelen ophalen...** , zoekt u Hallo **Google Cloud Messaging-Client** onderdeel en toe te voegen toohello project.</span><span class="sxs-lookup"><span data-stu-id="bfea1-101">In hello Solution view (or **Solution Explorer** in Visual Studio), right-click hello **Components** folder, click  **Get More Components...**, search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>
2. <span data-ttu-id="bfea1-102">Hallo ToDoActivity.cs projectbestand openen en voeg de volgende Hallo met behulp van de instructie toohello klasse:</span><span class="sxs-lookup"><span data-stu-id="bfea1-102">Open hello ToDoActivity.cs project file and add hello following using statement toohello class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="bfea1-103">In Hallo **ToDoActivity** klasse, Hallo na nieuwe code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="bfea1-103">In hello **ToDoActivity** class, add hello following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return hello current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return hello Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="bfea1-104">Hiermee kunt u tooaccess Hallo mobiele clientexemplaar van Hallo push handler-serviceproces.</span><span class="sxs-lookup"><span data-stu-id="bfea1-104">This enables you tooaccess hello mobile client instance from hello push handler service process.</span></span>
4. <span data-ttu-id="bfea1-105">Hallo na code toohello toevoegen **OnCreate** methode na Hallo **MobileServiceClient** wordt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="bfea1-105">Add hello following code toohello **OnCreate** method, after hello **MobileServiceClient** is created:</span></span>
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="bfea1-106">Uw **ToDoActivity** is nu klaar voor het toevoegen van pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="bfea1-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

