1. <span data-ttu-id="d3cde-101">Meld u aan toohello [Azure-portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d3cde-101">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="d3cde-102">Klik in het Hallo navigatiedeelvenster links van Hallo-portal op **nieuw**, klikt u vervolgens op **Enterprise Integration**, en klik vervolgens op **Relay**.</span><span class="sxs-lookup"><span data-stu-id="d3cde-102">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="d3cde-103">In Hallo **naamruimte maken** dialoogvenster, voer de naam van een naamruimte.</span><span class="sxs-lookup"><span data-stu-id="d3cde-103">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="d3cde-104">Hallo-systeem wordt onmiddellijk toosee gecontroleerd als Hallo naam beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="d3cde-104">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="d3cde-105">In Hallo **abonnement** veld, kiest u een Azure-abonnement in welke toocreate Hallo-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="d3cde-105">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
5. <span data-ttu-id="d3cde-106">In Hallo  **[resourcegroep](../articles/azure-resource-manager/resource-group-portal.md)**  veld, kiest u een bestaande resourcegroep in welke Hallo naamruimte live of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="d3cde-106">In hello **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="d3cde-107">In **locatie**, kiest u Hallo land of regio waarin uw naamruimte moet worden gehost.</span><span class="sxs-lookup"><span data-stu-id="d3cde-107">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Een naamruimte maken][create-namespace]
7. <span data-ttu-id="d3cde-109">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d3cde-109">Click **Create**.</span></span> <span data-ttu-id="d3cde-110">Hallo system nu uw naamruimte wordt gemaakt en ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d3cde-110">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="d3cde-111">Na een paar minuten Hallo bepalingen systeembronnen voor uw account.</span><span class="sxs-lookup"><span data-stu-id="d3cde-111">After a few minutes, hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="d3cde-112">Beheerreferenties ophalen Hallo</span><span class="sxs-lookup"><span data-stu-id="d3cde-112">Obtain hello management credentials</span></span>
1. <span data-ttu-id="d3cde-113">Klik in lijst Hallo van naamruimten op Hallo naamruimtenaam van een nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d3cde-113">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="d3cde-114">Klik op Hallo naamruimte blade **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="d3cde-114">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="d3cde-115">In Hallo **gedeeld toegangsbeleid** blade, klikt u op **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="d3cde-115">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![verbinding-gegevens][connection-info]
4. <span data-ttu-id="d3cde-117">In Hallo **beleid: RootManageSharedAccessKey** blade, klik op de knop kopiëren Hallo volgende te**Connection string – primaire sleutel**, toocopy Hallo connection string tooyour Klembord voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="d3cde-117">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="d3cde-118">Plak deze waarde in Kladblok of een andere tijdelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="d3cde-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="d3cde-120">Herhaal Hallo vorige stap, kopiëren en plakken Hallo-waarde van **primaire sleutel** tooa tijdelijke locatie voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="d3cde-120">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
