
1. In de weergave oplossing Hallo (of **Solution Explorer** in Visual Studio), klik met de rechtermuisknop Hallo **onderdelen** map, klikt u op **meer onderdelen ophalen...** , zoekt u Hallo **Google Cloud Messaging-Client** onderdeel en toe te voegen toohello project.
2. Hallo ToDoActivity.cs projectbestand openen en voeg de volgende Hallo met behulp van de instructie toohello klasse:
   
        using Gcm.Client;
3. In Hallo **ToDoActivity** klasse, Hallo na nieuwe code toevoegen: 
   
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
   
    Hiermee kunt u tooaccess Hallo mobiele clientexemplaar van Hallo push handler-serviceproces.
4. Hallo na code toohello toevoegen **OnCreate** methode na Hallo **MobileServiceClient** wordt gemaakt:
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

Uw **ToDoActivity** is nu klaar voor het toevoegen van pushmeldingen.

