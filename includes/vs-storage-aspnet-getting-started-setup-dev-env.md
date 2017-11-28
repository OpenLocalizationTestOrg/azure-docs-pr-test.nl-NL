## <a name="set-up-the-development-environment"></a><span data-ttu-id="d2ac5-101">De ontwikkelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="d2ac5-101">Set up the development environment</span></span>

<span data-ttu-id="d2ac5-102">Deze sectie helpt u uw ontwikkelomgeving, inclusief maken van een ASP.NET MVC-app, het toevoegen van een verbonden Services-verbinding toevoegen van een domeincontroller en de vereiste naamruimte richtlijnen geven instellen.</span><span class="sxs-lookup"><span data-stu-id="d2ac5-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying the required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="d2ac5-103">Een ASP.NET MVC-app-project maken</span><span class="sxs-lookup"><span data-stu-id="d2ac5-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="d2ac5-104">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2ac5-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="d2ac5-105">Selecteer **File -> Nieuw Project ->** vanuit het hoofdmenu</span><span class="sxs-lookup"><span data-stu-id="d2ac5-105">Select **File->New->Project** from the main menu</span></span>

1. <span data-ttu-id="d2ac5-106">Op de **nieuw Project** dialoogvenster, geeft u de opties zoals gemarkeerd in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d2ac5-106">On the **New Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![ASP.NET-project maken](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="d2ac5-108">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2ac5-108">Select **OK**.</span></span>

1. <span data-ttu-id="d2ac5-109">Op de **nieuw ASP.NET-Project** dialoogvenster, geeft u de opties zoals gemarkeerd in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="d2ac5-109">On the **New ASP.NET Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![Geef MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="d2ac5-111">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2ac5-111">Select **OK**.</span></span>

### <a name="use-connected-services-to-connect-to-an-azure-storage-account"></a><span data-ttu-id="d2ac5-112">Verbonden Services gebruiken om te verbinden met een Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="d2ac5-112">Use Connected Services to connect to an Azure storage account</span></span>

1. <span data-ttu-id="d2ac5-113">In de **Solution Explorer**, met de rechtermuisknop op het project en selecteer in het contextmenu **toevoegen -> Service verbonden**.</span><span class="sxs-lookup"><span data-stu-id="d2ac5-113">In the **Solution Explorer**, right-click the project, and from the context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="d2ac5-114">Op de **verbonden Service toevoegen** dialoogvenster Selecteer **Azure Storage**, en selecteer vervolgens **configureren**.</span><span class="sxs-lookup"><span data-stu-id="d2ac5-114">On the **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![Het dialoogvenster van de gekoppelde Service](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="d2ac5-116">Op de **Azure Storage** dialoogvenster, selecteer de gewenste Azure storage-account die u wilt werken, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d2ac5-116">On the **Azure Storage** dialog, select the desired Azure storage account with which you want to work, and select **Add**.</span></span>
