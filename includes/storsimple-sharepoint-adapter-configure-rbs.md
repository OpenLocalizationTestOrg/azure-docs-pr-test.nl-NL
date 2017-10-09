<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="7b080-101">Wanneer u wijzigingen toohello StorSimple-Adapter voor de configuratie van SharePoint RBS, moet u zijn aangemeld met een gebruikersaccount die deel uitmaakt van de groep Domeinadministrators toohello.</span><span class="sxs-lookup"><span data-stu-id="7b080-101">When making changes toohello StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs toohello Domain Admins group.</span></span> <span data-ttu-id="7b080-102">Bovendien moet u toegang tot de configuratiepagina Hallo vanuit een browser die wordt uitgevoerd op dezelfde als een Centraalbeheersite host Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b080-102">Additionally, you must access hello configuration page from a browser running on hello same host as Central Administration.</span></span>
> 
> 

#### <a name="tooconfigure-rbs"></a><span data-ttu-id="7b080-103">tooconfigure Resourcestructuur</span><span class="sxs-lookup"><span data-stu-id="7b080-103">tooconfigure RBS</span></span>
1. <span data-ttu-id="7b080-104">Open de pagina SharePoint Centraal beheer Hallo en te bladeren**systeeminstellingen**.</span><span class="sxs-lookup"><span data-stu-id="7b080-104">Open hello SharePoint Central Administration page, and browse too**System Settings**.</span></span> 
2. <span data-ttu-id="7b080-105">In Hallo **Azure StorSimple** sectie, klikt u op **StorSimple-Adapter configureren**.</span><span class="sxs-lookup"><span data-stu-id="7b080-105">In hello **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Hallo StorSimple Adapter configureren](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="7b080-107">Op Hallo **StorSimple-Adapter configureren** pagina:</span><span class="sxs-lookup"><span data-stu-id="7b080-107">On hello **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="7b080-108">Zorg ervoor dat Hallo **inschakelen bewerken pad** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7b080-108">Make sure that hello **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="7b080-109">Typ in het tekstvak hello, Hallo Universal Naming Convention (UNC) pad naar Hallo bloblarchief.</span><span class="sxs-lookup"><span data-stu-id="7b080-109">In hello text box, type hello Universal Naming Convention (UNC) path of hello BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="7b080-110">Hallo BLOB store-volume moet worden gehost op een iSCSI-volume dat is geconfigureerd op Hallo StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7b080-110">hello BLOB store volume must be hosted on an iSCSI volume configured on hello StorSimple device.</span></span>

   3. <span data-ttu-id="7b080-111">Klik op Hallo **inschakelen** knop onder elk van de inhoudsdatabases hello wilt u tooconfigure voor externe opslag.</span><span class="sxs-lookup"><span data-stu-id="7b080-111">Click hello **Enable** button below each of hello content databases that you want tooconfigure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="7b080-112">Hallo bloblarchief moet worden gedeeld en bereikbaar door alle web-front-(WFE)-servers en Hallo-gebruikersaccount dat is geconfigureerd voor Hallo SharePoint-serverfarm toegang toohello share moet hebben.</span><span class="sxs-lookup"><span data-stu-id="7b080-112">hello BLOB store must be shared and reachable by all web front-end (WFE) servers, and hello user account that is configured for hello SharePoint server farm must have access toohello share.</span></span>
      
      ![Hallo Resourcestructuur provider ingeschakeld](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="7b080-114">Als u inschakelt of Resourcestructuur uitschakelt, ziet u ook Hallo-bericht te volgen.</span><span class="sxs-lookup"><span data-stu-id="7b080-114">When you enable or disable RBS, you will also see hello following message.</span></span>
      
      ![Uitschakelen van StorSimple Adapter configureren](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="7b080-116">Klik op Hallo **Update** knop tooapply Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="7b080-116">Click hello **Update** button tooapply hello configuration.</span></span> <span data-ttu-id="7b080-117">Wanneer u klikt op Hallo **Update** knop Hallo Resourcestructuur configuratiestatus wordt bijgewerkt op alle WFE-servers en volledige farm Hallo worden Resourcestructuur ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7b080-117">When you click hello **Update** button, hello RBS configuration status will be updated on all WFE servers, and hello entire farm will be RBS-enabled.</span></span> <span data-ttu-id="7b080-118">Hallo volgende bericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7b080-118">hello following message appears.</span></span>
      
      ![Adapter configuratiebericht](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="7b080-120">Als u Resourcestructuur configureert voor een SharePoint-farm met een zeer groot aantal databases (groter dan 200), mogelijk Hallo Centraal beheer van SharePoint-webpagina time-out. Als dit het geval is, moet u Hallo pagina vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="7b080-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), hello SharePoint Central Administration web page might time out. If that occurs, refresh hello page.</span></span> <span data-ttu-id="7b080-121">Dit heeft geen invloed op Hallo-configuratieproces.</span><span class="sxs-lookup"><span data-stu-id="7b080-121">This does not affect hello configuration process.</span></span>

4. <span data-ttu-id="7b080-122">Hallo-configuratie controleren:</span><span class="sxs-lookup"><span data-stu-id="7b080-122">Verify hello configuration:</span></span>
   
   1. <span data-ttu-id="7b080-123">Meld u aan toohello Centraal beheer van SharePoint-website en bladeren toohello **StorSimple-Adapter configureren** pagina.</span><span class="sxs-lookup"><span data-stu-id="7b080-123">Log on toohello SharePoint Central Administration website, and browse toohello **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="7b080-124">Controleer de configuratie details toomake Hallo zeker van te zijn dat ze overeenkomen met de Hallo-instellingen die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7b080-124">Check hello configuration details toomake sure that they match hello settings that you entered.</span></span> 
5. <span data-ttu-id="7b080-125">Controleer of Resourcestructuur correct werkt:</span><span class="sxs-lookup"><span data-stu-id="7b080-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="7b080-126">Upload een tooSharePoint document.</span><span class="sxs-lookup"><span data-stu-id="7b080-126">Upload a document tooSharePoint.</span></span> 
   2. <span data-ttu-id="7b080-127">Blader toohello UNC-pad dat u hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7b080-127">Browse toohello UNC path that you configured.</span></span> <span data-ttu-id="7b080-128">Zorg ervoor dat Hallo Resourcestructuur mapstructuur is gemaakt en dat deze geüpload Hallo-object bevat.</span><span class="sxs-lookup"><span data-stu-id="7b080-128">Make sure that hello RBS directory structure was created and that it contains hello uploaded object.</span></span>
6. <span data-ttu-id="7b080-129">(Optioneel) U kunt Microsoft RBS Hallo `Migrate()` PowerShell-cmdlet die deel uitmaakt van SharePoint toomigrate bestaande BLOB inhoud toohello StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7b080-129">(Optional) You can use hello Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint toomigrate existing BLOB content toohello StorSimple device.</span></span> <span data-ttu-id="7b080-130">Zie voor meer informatie [inhoud migreert van of naar Resourcestructuur in SharePoint 2013] [ 6] of [inhoud migreert van of naar Resourcestructuur (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="7b080-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="7b080-131">(Optioneel) U kunt op test-installaties controleren Hallo BLOBs als volgt buiten de inhoudsdatabase Hallo zijn verplaatst:</span><span class="sxs-lookup"><span data-stu-id="7b080-131">(Optional) On test installations, you can verify that hello BLOBs were moved out of hello content database as follows:</span></span> 
   
   1. <span data-ttu-id="7b080-132">Start SQL Management Studio.</span><span class="sxs-lookup"><span data-stu-id="7b080-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="7b080-133">Hallo ListBlobsInDB_2010.sql of ListBlobsInDB_2013.sql query uitvoert, als volgt.</span><span class="sxs-lookup"><span data-stu-id="7b080-133">Run hello ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
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
      
      <span data-ttu-id="7b080-134">Als Resourcestructuur correct is geconfigureerd, wordt een NULL-waarde in Hallo SizeOfContentInDB kolom voor elk object dat is geüpload en met succes externalized met Resourcestructuur weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7b080-134">If RBS was configured correctly, a NULL value should appear in hello SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="7b080-135">(Optioneel) Nadat u Resourcestructuur configureren en verplaatst u alle BLOBS inhoud toohello StorSimple-apparaat, kunt u Hallo inhoudsdatabase toohello apparaat verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="7b080-135">(Optional) After you configure RBS and move all BLOB content toohello StorSimple device, you can move hello content database toohello device.</span></span> <span data-ttu-id="7b080-136">Als u toomove Hallo inhoud van de database kiest, raden wij u Hallo inhoudsdatabase opslag configureren op Hallo-apparaat als primaire volume.</span><span class="sxs-lookup"><span data-stu-id="7b080-136">If you choose toomove hello content database, we recommend that you configure hello content database storage on hello device as a primary volume.</span></span> <span data-ttu-id="7b080-137">Vervolgens gebruik tot stand gebracht dat SQL Server best practices toomigrate Hallo inhoudsdatabase toohello StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7b080-137">Then, use established SQL Server best practices toomigrate hello content database toohello StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7b080-138">Zwevend Hallo inhoudsdatabase toohello apparaat wordt alleen ondersteund voor Hallo StorSimple 8000 serie (dit wordt niet ondersteund voor Hallo 5000 of 7000-serie).</span><span class="sxs-lookup"><span data-stu-id="7b080-138">Moving hello content database toohello device is only supported for hello StorSimple 8000 series (it is not supported for hello 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="7b080-139">Als u BLOBs en Hallo inhoudsdatabase in afzonderlijke volumes op Hallo StorSimple-apparaat opslaat, raden wij aan dat u ze in Hallo configureren dezelfde volumecontainer.</span><span class="sxs-lookup"><span data-stu-id="7b080-139">If you store BLOBs and hello content database in separate volumes on hello StorSimple device, we recommend that you configure them in hello same volume container.</span></span> <span data-ttu-id="7b080-140">Dit zorgt ervoor dat er wordt een back-samen.</span><span class="sxs-lookup"><span data-stu-id="7b080-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="7b080-141">Als u Resourcestructuur niet hebt ingeschakeld, raden we niet verplaatsen Hallo inhoudsdatabase toohello StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7b080-141">If you have not enabled RBS, we do not recommend moving hello content database toohello StorSimple device.</span></span> <span data-ttu-id="7b080-142">Dit is een niet-geteste configuratie.</span><span class="sxs-lookup"><span data-stu-id="7b080-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="7b080-143">De volgende stap gaat u toohello: [garbagecollection configureren](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="7b080-143">Go toohello next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
