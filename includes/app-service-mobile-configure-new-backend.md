
1. <span data-ttu-id="28b72-101">Klik op de **App Services** knop, selecteert u uw back-end van Mobile Apps, selecteer **Quick Start**, en selecteer vervolgens uw clientplatform (iOS, Android, Xamarin, Cordova).</span><span class="sxs-lookup"><span data-stu-id="28b72-101">Click the **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Azure-portal met Mobile Apps Quick Start gemarkeerd][quickstart]

2. <span data-ttu-id="28b72-103">Als een databaseverbinding niet is geconfigureerd, maakt u een door de volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="28b72-103">If a database connection is not configured, create one by doing the following:</span></span>

    ![Azure-portal met Mobile Apps verbinding maken met database][connect]

    <span data-ttu-id="28b72-105">a.</span><span class="sxs-lookup"><span data-stu-id="28b72-105">a.</span></span> <span data-ttu-id="28b72-106">Maak een nieuwe SQL-database en de server.</span><span class="sxs-lookup"><span data-stu-id="28b72-106">Create a new SQL database and server.</span></span>

    ![Azure-portal met Mobile Apps nieuwe database en de server maken][server]

    <span data-ttu-id="28b72-108">b.</span><span class="sxs-lookup"><span data-stu-id="28b72-108">b.</span></span> <span data-ttu-id="28b72-109">Wacht totdat de gegevensverbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="28b72-109">Wait until the data connection is successfully created.</span></span>

    ![Azure portal gemaakt gegevensverbinding-melding][notification]

    <span data-ttu-id="28b72-111">c.</span><span class="sxs-lookup"><span data-stu-id="28b72-111">c.</span></span> <span data-ttu-id="28b72-112">Gegevensverbinding moet zijn gelukt.</span><span class="sxs-lookup"><span data-stu-id="28b72-112">Data connection must be successful.</span></span>

    ![Azure portal melding 'U hebt al een gegevensverbinding'][already-connection]

3. <span data-ttu-id="28b72-114">Selecteer bij **2. Een tabel-API maken** de optie Node.js voor **Back-endtaal**.</span><span class="sxs-lookup"><span data-stu-id="28b72-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="28b72-115">Accepteer de bevestiging en selecteer vervolgens **takentabel maken**.</span><span class="sxs-lookup"><span data-stu-id="28b72-115">Accept the acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="28b72-116">Deze actie wordt een nieuwe taak item tabel gemaakt in uw database.</span><span class="sxs-lookup"><span data-stu-id="28b72-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="28b72-117">Alle inhoud overschakelen van een bestaande back-end voor Node.js worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="28b72-117">Switching an existing back end to Node.js overwrites all contents.</span></span> <span data-ttu-id="28b72-118">Als u wilt maken in plaats daarvan een .NET-back-end, Zie [werken met de .NET-back-end-server SDK voor Mobile Apps][instructions].</span><span class="sxs-lookup"><span data-stu-id="28b72-118">To create a .NET back end instead, see [Work with the .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
