<span data-ttu-id="2c783-101">toobegin met Service Bus-wachtrijen in Azure, moet u eerst een naamruimte maken met een naam die uniek is voor alle Azure.</span><span class="sxs-lookup"><span data-stu-id="2c783-101">toobegin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="2c783-102">Een naamruimte biedt een scoping container voor het verwerken van Service Bus-resources in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="2c783-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="2c783-103">een naamruimte toocreate:</span><span class="sxs-lookup"><span data-stu-id="2c783-103">toocreate a namespace:</span></span>

1. <span data-ttu-id="2c783-104">Meld u aan toohello [Azure-portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="2c783-104">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="2c783-105">Klik in het Hallo navigatiedeelvenster links van de portal Hallo op **nieuw**, klikt u vervolgens op **Enterprise Integration**, en klik vervolgens op **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="2c783-105">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="2c783-106">In Hallo **naamruimte maken** dialoogvenster, voer de naam van een naamruimte.</span><span class="sxs-lookup"><span data-stu-id="2c783-106">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="2c783-107">Hallo-systeem wordt onmiddellijk toosee gecontroleerd als Hallo naam beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="2c783-107">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="2c783-108">Nadat u hebt ervoor Hallo naamruimtenaam is beschikbaar, kies Hallo prijscategorie (Basic, Standard of Premium).</span><span class="sxs-lookup"><span data-stu-id="2c783-108">After making sure hello namespace name is available, choose hello pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="2c783-109">In Hallo **abonnement** veld, kiest u een Azure-abonnement in welke toocreate Hallo-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="2c783-109">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
6. <span data-ttu-id="2c783-110">In Hallo **resourcegroep** veld, kiest u een bestaande resourcegroep in welke Hallo naamruimte live of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="2c783-110">In hello **Resource group** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="2c783-111">In **locatie**, kiest u Hallo land of regio waarin uw naamruimte moet worden gehost.</span><span class="sxs-lookup"><span data-stu-id="2c783-111">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Een naamruimte maken][create-namespace]
8. <span data-ttu-id="2c783-113">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2c783-113">Click **Create**.</span></span> <span data-ttu-id="2c783-114">Hallo system nu uw naamruimte wordt gemaakt en ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2c783-114">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="2c783-115">Mogelijk hebt u toowait enkele minuten als Hallo bepalingen systeembronnen voor uw account.</span><span class="sxs-lookup"><span data-stu-id="2c783-115">You might have toowait several minutes as hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="2c783-116">Beheerreferenties ophalen Hallo</span><span class="sxs-lookup"><span data-stu-id="2c783-116">Obtain hello management credentials</span></span>

1. <span data-ttu-id="2c783-117">Klik in lijst Hallo van naamruimten op Hallo naamruimtenaam van een nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2c783-117">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="2c783-118">Klik op Hallo naamruimte blade **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="2c783-118">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="2c783-119">In Hallo **gedeeld toegangsbeleid** blade, klikt u op **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="2c783-119">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![verbinding-gegevens][connection-info]
4. <span data-ttu-id="2c783-121">In Hallo **beleid: RootManageSharedAccessKey** blade, klik op de knop kopiëren Hallo volgende te**Connection string – primaire sleutel**, toocopy Hallo connection string tooyour Klembord voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="2c783-121">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="2c783-122">Plak deze waarde in Kladblok of een andere tijdelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="2c783-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="2c783-124">Herhaal Hallo vorige stap, kopiëren en plakken Hallo-waarde van **primaire sleutel** tooa tijdelijke locatie voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="2c783-124">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
