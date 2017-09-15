<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="99c07-101">Als u wijzigingen aanbrengt aan de StorSimple-Adapter voor de configuratie van SharePoint RBS, moet u zijn aangemeld met een gebruikersaccount die deel uitmaakt van de groep Domeinadministrators.</span><span class="sxs-lookup"><span data-stu-id="99c07-101">When making changes to the StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs to the Domain Admins group.</span></span> <span data-ttu-id="99c07-102">Bovendien moet u toegang tot de configuratiepagina van een browser op dezelfde host als een Centraalbeheersite.</span><span class="sxs-lookup"><span data-stu-id="99c07-102">Additionally, you must access the configuration page from a browser running on the same host as Central Administration.</span></span>
> 
> 

#### <a name="to-configure-rbs"></a><span data-ttu-id="99c07-103">Resourcestructuur configureren</span><span class="sxs-lookup"><span data-stu-id="99c07-103">To configure RBS</span></span>
1. <span data-ttu-id="99c07-104">Open de pagina Centraal beheer van SharePoint en blader naar **systeeminstellingen**.</span><span class="sxs-lookup"><span data-stu-id="99c07-104">Open the SharePoint Central Administration page, and browse to **System Settings**.</span></span> 
2. <span data-ttu-id="99c07-105">In de **Azure StorSimple** sectie, klikt u op **StorSimple-Adapter configureren**.</span><span class="sxs-lookup"><span data-stu-id="99c07-105">In the **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Configureer de StorSimple-Adapter](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="99c07-107">Op de **StorSimple-Adapter configureren** pagina:</span><span class="sxs-lookup"><span data-stu-id="99c07-107">On the **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="99c07-108">Zorg ervoor dat de **inschakelen bewerken pad** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="99c07-108">Make sure that the **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="99c07-109">Typ het pad Universal Naming Convention (UNC) van de BLOB-opslag in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="99c07-109">In the text box, type the Universal Naming Convention (UNC) path of the BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="99c07-110">De BLOB-store-volume moet worden gehost op een iSCSI-volume dat is geconfigureerd op het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="99c07-110">The BLOB store volume must be hosted on an iSCSI volume configured on the StorSimple device.</span></span>

   3. <span data-ttu-id="99c07-111">Klik op de **inschakelen** knop onder elk van de inhoudsdatabases die u wilt configureren voor externe opslag.</span><span class="sxs-lookup"><span data-stu-id="99c07-111">Click the **Enable** button below each of the content databases that you want to configure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="99c07-112">De BLOB-opslag moet worden gedeeld en bereikbaar door alle web-front-(WFE)-servers en de gebruikersaccount die is geconfigureerd voor de SharePoint-serverfarm moet toegang hebben tot de share.</span><span class="sxs-lookup"><span data-stu-id="99c07-112">The BLOB store must be shared and reachable by all web front-end (WFE) servers, and the user account that is configured for the SharePoint server farm must have access to the share.</span></span>
      
      ![De provider Resourcestructuur inschakelen](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="99c07-114">Wanneer u in- of uitschakelen van Resourcestructuur, ziet u ook het volgende bericht.</span><span class="sxs-lookup"><span data-stu-id="99c07-114">When you enable or disable RBS, you will also see the following message.</span></span>
      
      ![Uitschakelen van StorSimple Adapter configureren](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="99c07-116">Klik op de **Update** om de configuratie toepassen.</span><span class="sxs-lookup"><span data-stu-id="99c07-116">Click the **Update** button to apply the configuration.</span></span> <span data-ttu-id="99c07-117">Wanneer u klikt op de **Update** knop klikt, wordt de status van de configuratie Resourcestructuur bijgewerkt op alle WFE-servers en de gehele farm worden Resourcestructuur ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="99c07-117">When you click the **Update** button, the RBS configuration status will be updated on all WFE servers, and the entire farm will be RBS-enabled.</span></span> <span data-ttu-id="99c07-118">Het volgende bericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="99c07-118">The following message appears.</span></span>
      
      ![Adapter configuratiebericht](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="99c07-120">Als u Resourcestructuur configureert voor een SharePoint-farm met een zeer groot aantal databases (groter dan 200), kan de Centraal beheer van SharePoint-webpagina time-out.</span><span class="sxs-lookup"><span data-stu-id="99c07-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), the SharePoint Central Administration web page might time out.</span></span> <span data-ttu-id="99c07-121">Als dit het geval is, wordt de pagina vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="99c07-121">If that occurs, refresh the page.</span></span> <span data-ttu-id="99c07-122">Dit heeft geen invloed op het configuratieproces.</span><span class="sxs-lookup"><span data-stu-id="99c07-122">This does not affect the configuration process.</span></span>

4. <span data-ttu-id="99c07-123">Controleer of de configuratie:</span><span class="sxs-lookup"><span data-stu-id="99c07-123">Verify the configuration:</span></span>
   
   1. <span data-ttu-id="99c07-124">Meld u aan bij de website Centraal beheer van SharePoint en blader naar de **StorSimple-Adapter configureren** pagina.</span><span class="sxs-lookup"><span data-stu-id="99c07-124">Log on to the SharePoint Central Administration website, and browse to the **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="99c07-125">Controleer de configuratiedetails om ervoor te zorgen dat ze overeenkomen met de instellingen die u hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="99c07-125">Check the configuration details to make sure that they match the settings that you entered.</span></span> 
5. <span data-ttu-id="99c07-126">Controleer of Resourcestructuur correct werkt:</span><span class="sxs-lookup"><span data-stu-id="99c07-126">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="99c07-127">Een document uploaden naar SharePoint.</span><span class="sxs-lookup"><span data-stu-id="99c07-127">Upload a document to SharePoint.</span></span> 
   2. <span data-ttu-id="99c07-128">Blader naar het UNC-pad dat u hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="99c07-128">Browse to the UNC path that you configured.</span></span> <span data-ttu-id="99c07-129">Zorg ervoor dat de mapstructuur Resourcestructuur is gemaakt en dat deze het geüploade object bevat.</span><span class="sxs-lookup"><span data-stu-id="99c07-129">Make sure that the RBS directory structure was created and that it contains the uploaded object.</span></span>
6. <span data-ttu-id="99c07-130">(Optioneel) U kunt de Microsoft-RBS `Migrate()` PowerShell-cmdlet die deel uitmaakt van SharePoint voor het migreren van bestaande BLOB-inhoud naar het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="99c07-130">(Optional) You can use the Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint to migrate existing BLOB content to the StorSimple device.</span></span> <span data-ttu-id="99c07-131">Zie voor meer informatie [inhoud migreert van of naar Resourcestructuur in SharePoint 2013] [ 6] of [inhoud migreert van of naar Resourcestructuur (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="99c07-131">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="99c07-132">(Optioneel) Bij installaties van de test, kunt u controleren dat de BLOBs als volgt buiten de inhoud van de database zijn verplaatst:</span><span class="sxs-lookup"><span data-stu-id="99c07-132">(Optional) On test installations, you can verify that the BLOBs were moved out of the content database as follows:</span></span> 
   
   1. <span data-ttu-id="99c07-133">Start SQL Management Studio.</span><span class="sxs-lookup"><span data-stu-id="99c07-133">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="99c07-134">De query ListBlobsInDB_2010.sql of ListBlobsInDB_2013.sql als volgt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="99c07-134">Run the ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="99c07-135">Als Resourcestructuur correct is geconfigureerd, kan een NULL-waarde moet worden weergegeven in de kolom SizeOfContentInDB voor elk object dat is geüpload en met succes externalized met Resourcestructuur.</span><span class="sxs-lookup"><span data-stu-id="99c07-135">If RBS was configured correctly, a NULL value should appear in the SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="99c07-136">(Optioneel) Nadat u Resourcestructuur configureert en alle BLOB-inhoud naar het StorSimple-apparaat verplaatsen, kunt u de inhoud van de database kunt verplaatsen naar het apparaat.</span><span class="sxs-lookup"><span data-stu-id="99c07-136">(Optional) After you configure RBS and move all BLOB content to the StorSimple device, you can move the content database to the device.</span></span> <span data-ttu-id="99c07-137">Als u kiest voor het verplaatsen van de inhoud van de database, raden wij u aan de inhoud van de database-opslag te configureren op het apparaat als primaire volume.</span><span class="sxs-lookup"><span data-stu-id="99c07-137">If you choose to move the content database, we recommend that you configure the content database storage on the device as a primary volume.</span></span> <span data-ttu-id="99c07-138">Gebruik vervolgens tot stand gebracht aanbevolen procedures voor SQL Server voor het migreren van de inhoud van de database op het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="99c07-138">Then, use established SQL Server best practices to migrate the content database to the StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="99c07-139">De inhoud van de database te verplaatsen naar het apparaat wordt alleen ondersteund voor de StorSimple 8000 serie (dit wordt niet ondersteund voor de 5000 of 7000-serie).</span><span class="sxs-lookup"><span data-stu-id="99c07-139">Moving the content database to the device is only supported for the StorSimple 8000 series (it is not supported for the 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="99c07-140">Als u BLOBs en de inhoud van de database in afzonderlijke volumes op het StorSimple-apparaat opslaat, raden wij u ze configureren in dezelfde volumecontainer.</span><span class="sxs-lookup"><span data-stu-id="99c07-140">If you store BLOBs and the content database in separate volumes on the StorSimple device, we recommend that you configure them in the same volume container.</span></span> <span data-ttu-id="99c07-141">Dit zorgt ervoor dat er wordt een back-samen.</span><span class="sxs-lookup"><span data-stu-id="99c07-141">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="99c07-142">Als u Resourcestructuur niet hebt ingeschakeld, niet aangeraden de inhoudsdatabase te verplaatsen naar de StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="99c07-142">If you have not enabled RBS, we do not recommend moving the content database to the StorSimple device.</span></span> <span data-ttu-id="99c07-143">Dit is een niet-geteste configuratie.</span><span class="sxs-lookup"><span data-stu-id="99c07-143">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="99c07-144">Ga naar de volgende stap: [garbagecollection configureren](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="99c07-144">Go to the next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
