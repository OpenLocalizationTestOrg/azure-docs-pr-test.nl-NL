<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="9e756-101">U wordt in deze procedure:</span><span class="sxs-lookup"><span data-stu-id="9e756-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="9e756-102">[Uitvoerbaar bestand toorun Hallo Maintainer voorbereiden](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="9e756-102">[Prepare toorun hello Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="9e756-103">[Hallo inhoud van de database en de Prullenbak voorbereiden voor onmiddellijke verwijdering van zwevende BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="9e756-103">[Prepare hello content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="9e756-104">[Voer Maintainer.exe](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="9e756-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="9e756-105">[Hallo inhoud van de database en de Prullenbak-instellingen herstellen](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="9e756-105">[Revert hello content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="tooprepare-toorun-hello-maintainer"></a><span data-ttu-id="9e756-106">tooprepare toorun Hallo Maintainer</span><span class="sxs-lookup"><span data-stu-id="9e756-106">tooprepare toorun hello Maintainer</span></span>
1. <span data-ttu-id="9e756-107">Open op de front-endwebserver hello, Hallo SharePoint 2013-beheershell als beheerder.</span><span class="sxs-lookup"><span data-stu-id="9e756-107">On hello Web front-end server, open hello SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="9e756-108">Navigeer toohello map *opstartschijf*: \Program Files\Microsoft 10.50\Maintainer SQL externe Blob-opslag\.</span><span class="sxs-lookup"><span data-stu-id="9e756-108">Navigate toohello folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="9e756-109">Wijzig de naam van **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** te**web.config**.</span><span class="sxs-lookup"><span data-stu-id="9e756-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** too**web.config**.</span></span>
4. <span data-ttu-id="9e756-110">Gebruik `aspnet_regiis -pdf connectionStrings` toodecrypt Hallo web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="9e756-110">Use `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config file.</span></span>
5. <span data-ttu-id="9e756-111">In Hallo ontsleutelde web.config-bestand, onder Hallo `connectionStrings` knooppunt toevoegen Hallo-verbindingsreeks voor de SQL server-exemplaar en Hallo de naam van de inhoud van de database.</span><span class="sxs-lookup"><span data-stu-id="9e756-111">In hello decrypted web.config file, under hello `connectionStrings` node, add hello connection string for your SQL server instance and hello content database name.</span></span> <span data-ttu-id="9e756-112">Zie Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="9e756-112">See hello following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="9e756-113">Gebruik `aspnet_regiis –pef connectionStrings` toore-versleutelen Hallo web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="9e756-113">Use `aspnet_regiis –pef connectionStrings` toore-encrypt hello web.config file.</span></span> 
7. <span data-ttu-id="9e756-114">Wijzig de naam van web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span><span class="sxs-lookup"><span data-stu-id="9e756-114">Rename web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a><span data-ttu-id="9e756-115">tooprepare hello inhoud van de database en de Prullenbak tooimmediately verwijderen zwevende BLOBs</span><span class="sxs-lookup"><span data-stu-id="9e756-115">tooprepare hello content database and Recycle Bin tooimmediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="9e756-116">Voer op Hallo SQL-Server in SQL Management Studio Hallo update query's voor Hallo doel inhoudsdatabase te volgen:</span><span class="sxs-lookup"><span data-stu-id="9e756-116">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="9e756-117">Op Hallo van web-front-endserver onder **Centraal beheer**, Hallo bewerken **algemene instellingen van webtoepassing** voor Hallo inhoudsdatabase tootemporarily uitschakelen Hallo Prullenbak gewenst.</span><span class="sxs-lookup"><span data-stu-id="9e756-117">On hello web front-end server, under **Central Administration**, edit hello **Web Application General Settings** for hello desired content database tootemporarily disable hello Recycle Bin.</span></span> <span data-ttu-id="9e756-118">Deze actie wordt ook leeg Hallo Prullenbak voor een verzameling verwante site.</span><span class="sxs-lookup"><span data-stu-id="9e756-118">This action will also empty hello Recycle Bin for any related site collections.</span></span> <span data-ttu-id="9e756-119">toodo, klikt u op **Centraal beheer** -> **Toepassingsbeheer** -> **webtoepassingen (web-apps beheren)**  ->  **SharePoint - 80** -> **algemene toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="9e756-119">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="9e756-120">Set Hallo **Status van de Prullenbak** te**OFF**.</span><span class="sxs-lookup"><span data-stu-id="9e756-120">Set hello **Recycle Bin Status** too**OFF**.</span></span>
   
    ![Algemene instellingen van webtoepassing](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a><span data-ttu-id="9e756-122">toorun hello Maintainer</span><span class="sxs-lookup"><span data-stu-id="9e756-122">toorun hello Maintainer</span></span>
* <span data-ttu-id="9e756-123">Op de front-endwebserver hello, in SharePoint 2013-beheershell Hallo Hallo Maintainer als volgt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9e756-123">On hello web front-end server, in hello SharePoint 2013 Management Shell, run hello Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="9e756-124">Alleen Hallo `GarbageCollection` bewerking voor StorSimple wordt ondersteund op dit moment.</span><span class="sxs-lookup"><span data-stu-id="9e756-124">Only hello `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="9e756-125">Let ook op Hallo-parameters die zijn uitgegeven voor Microsoft.Data.SqlRemoteBlobs.Maintainer.exe zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="9e756-125">Also note that hello parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a><span data-ttu-id="9e756-126">toorevert hello inhoud van de database en de Prullenbak-instellingen</span><span class="sxs-lookup"><span data-stu-id="9e756-126">toorevert hello content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="9e756-127">Voer op Hallo SQL-Server in SQL Management Studio Hallo update query's voor Hallo doel inhoudsdatabase te volgen:</span><span class="sxs-lookup"><span data-stu-id="9e756-127">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="9e756-128">Op de front-endwebserver hello, in **Centraal beheer**, Hallo bewerken **algemene instellingen van webtoepassing** voor Hallo inhoudsdatabase toore inschakelen Hallo Prullenbak gewenst.</span><span class="sxs-lookup"><span data-stu-id="9e756-128">On hello web front-end server, in **Central Administration**, edit hello **Web Application General Settings** for hello desired content database toore-enable hello Recycle Bin.</span></span> <span data-ttu-id="9e756-129">toodo, klikt u op **Centraal beheer** -> **Toepassingsbeheer** -> **webtoepassingen (web-apps beheren)**  ->  **SharePoint - 80** -> **algemene toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="9e756-129">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="9e756-130">Hallo Status van de Prullenbak te ingesteld**ON**.</span><span class="sxs-lookup"><span data-stu-id="9e756-130">Set hello Recycle Bin Status too**ON**.</span></span>

