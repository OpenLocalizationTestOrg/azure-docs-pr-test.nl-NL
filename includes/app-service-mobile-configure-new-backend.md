
1. <span data-ttu-id="5f46c-101">Klik op Hallo **App Services** knop, selecteert u uw back-end van Mobile Apps, selecteer **Quick Start**, en selecteer vervolgens uw clientplatform (iOS, Android, Xamarin, Cordova).</span><span class="sxs-lookup"><span data-stu-id="5f46c-101">Click hello **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Azure Portal met Mobile Apps Quickstart gemarkeerd][quickstart]

2. <span data-ttu-id="5f46c-103">Als de verbinding met een database niet is geconfigureerd, maakt u een door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="5f46c-103">If a database connection is not configured, create one by doing hello following:</span></span>

    ![Azure-portal met Mobile Apps Connect toodatabase][connect]

    <span data-ttu-id="5f46c-105">a.</span><span class="sxs-lookup"><span data-stu-id="5f46c-105">a.</span></span> <span data-ttu-id="5f46c-106">Maak een nieuwe SQL-database en -server.</span><span class="sxs-lookup"><span data-stu-id="5f46c-106">Create a new SQL database and server.</span></span>

    ![Azure Portal met Mobile Apps: nieuwe database en server maken][server]

    <span data-ttu-id="5f46c-108">b.</span><span class="sxs-lookup"><span data-stu-id="5f46c-108">b.</span></span> <span data-ttu-id="5f46c-109">Wacht totdat het Hallo-gegevensverbinding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f46c-109">Wait until hello data connection is successfully created.</span></span>

    ![Melding in Azure Portal dat de gegevensverbinding is gemaakt][notification]

    <span data-ttu-id="5f46c-111">c.</span><span class="sxs-lookup"><span data-stu-id="5f46c-111">c.</span></span> <span data-ttu-id="5f46c-112">Gegevensverbinding moet zijn gelukt.</span><span class="sxs-lookup"><span data-stu-id="5f46c-112">Data connection must be successful.</span></span>

    ![Melding 'U hebt al een gegevensverbinding' in Azure Portal][already-connection]

3. <span data-ttu-id="5f46c-114">Selecteer bij **2. Een tabel-API maken** de optie Node.js voor **Back-endtaal**.</span><span class="sxs-lookup"><span data-stu-id="5f46c-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="5f46c-115">Hallo bevestiging accepteren en selecteer vervolgens **takentabel maken**.</span><span class="sxs-lookup"><span data-stu-id="5f46c-115">Accept hello acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="5f46c-116">Met deze actie wordt er een nieuwe takentabel in uw database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f46c-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="5f46c-117">Alle inhoud overschakelen van een bestaande back-end-tooNode.js worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="5f46c-117">Switching an existing back end tooNode.js overwrites all contents.</span></span> <span data-ttu-id="5f46c-118">een .NET-back-end in plaats daarvan Zie toocreate [werken met .NET back-end Hallo server SDK voor Mobile Apps][instructions].</span><span class="sxs-lookup"><span data-stu-id="5f46c-118">toocreate a .NET back end instead, see [Work with hello .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
