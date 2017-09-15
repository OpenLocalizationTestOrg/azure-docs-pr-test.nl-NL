<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="3bca1-101">U wordt in deze procedure:</span><span class="sxs-lookup"><span data-stu-id="3bca1-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="3bca1-102">[Voorbereiden om uit te voeren uitvoerbare bestand van de Maintainer](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="3bca1-102">[Prepare to run the Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="3bca1-103">[De inhoud van de database en de Prullenbak voorbereiden voor onmiddellijke verwijdering van zwevende BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="3bca1-103">[Prepare the content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="3bca1-104">[Voer Maintainer.exe](#to-run-the-maintainer).</span><span class="sxs-lookup"><span data-stu-id="3bca1-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="3bca1-105">[Herstellen van de inhoud van de database en de instellingen van de Prullenbak](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="3bca1-105">[Revert the content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="to-prepare-to-run-the-maintainer"></a><span data-ttu-id="3bca1-106">Voorbereiden om uit te voeren de Maintainer</span><span class="sxs-lookup"><span data-stu-id="3bca1-106">To prepare to run the Maintainer</span></span>
1. <span data-ttu-id="3bca1-107">Open de SharePoint 2013-beheershell als beheerder op de front-end-webserver.</span><span class="sxs-lookup"><span data-stu-id="3bca1-107">On the Web front-end server, open the SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="3bca1-108">Navigeer naar de map *opstartschijf*: \Program Files\Microsoft 10.50\Maintainer SQL externe Blob-opslag\.</span><span class="sxs-lookup"><span data-stu-id="3bca1-108">Navigate to the folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="3bca1-109">Wijzig de naam van **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** naar **web.config**.</span><span class="sxs-lookup"><span data-stu-id="3bca1-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** to **web.config**.</span></span>
4. <span data-ttu-id="3bca1-110">Gebruik `aspnet_regiis -pdf connectionStrings` voor het ontsleutelen van het bestand web.config.</span><span class="sxs-lookup"><span data-stu-id="3bca1-110">Use `aspnet_regiis -pdf connectionStrings` to decrypt the web.config file.</span></span>
5. <span data-ttu-id="3bca1-111">In het bestand web.config te ontsleutelen onder de `connectionStrings` knooppunt toevoegen van de verbindingsreeks voor de SQL server-exemplaar en de naam van de inhoud van de database.</span><span class="sxs-lookup"><span data-stu-id="3bca1-111">In the decrypted web.config file, under the `connectionStrings` node, add the connection string for your SQL server instance and the content database name.</span></span> <span data-ttu-id="3bca1-112">Zie het volgende voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3bca1-112">See the following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="3bca1-113">Gebruik `aspnet_regiis –pef connectionStrings` opnieuw versleutelen van het bestand web.config.</span><span class="sxs-lookup"><span data-stu-id="3bca1-113">Use `aspnet_regiis –pef connectionStrings` to re-encrypt the web.config file.</span></span> 
7. <span data-ttu-id="3bca1-114">De naam van web.config Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span><span class="sxs-lookup"><span data-stu-id="3bca1-114">Rename web.config to Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs"></a><span data-ttu-id="3bca1-115">Als u wilt de inhoud voorbereiden zwevende database en de Prullenbak worden onmiddellijk verwijderd BLOBs</span><span class="sxs-lookup"><span data-stu-id="3bca1-115">To prepare the content database and Recycle Bin to immediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="3bca1-116">Voer op de SQL-Server in SQL Management Studio de volgende update-query's voor de doel-inhoudsdatabase:</span><span class="sxs-lookup"><span data-stu-id="3bca1-116">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="3bca1-117">Op de front-endwebserver onder **Centraal beheer**, bewerk de **algemene instellingen van webtoepassing** voor de gewenste inhoudsdatabase tijdelijk uitschakelen van de Prullenbak.</span><span class="sxs-lookup"><span data-stu-id="3bca1-117">On the web front-end server, under **Central Administration**, edit the **Web Application General Settings** for the desired content database to temporarily disable the Recycle Bin.</span></span> <span data-ttu-id="3bca1-118">Deze actie wordt ook de Prullenbak voor alle siteverzamelingen verwante.</span><span class="sxs-lookup"><span data-stu-id="3bca1-118">This action will also empty the Recycle Bin for any related site collections.</span></span> <span data-ttu-id="3bca1-119">Om dit te doen, klikt u op **Centraal beheer** -> **Toepassingsbeheer** -> **webtoepassingen (web-apps beheren)**  ->  **SharePoint - 80** -> **algemene toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="3bca1-119">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="3bca1-120">Stel de **Status van de Prullenbak** naar **OFF**.</span><span class="sxs-lookup"><span data-stu-id="3bca1-120">Set the **Recycle Bin Status** to **OFF**.</span></span>
   
    ![Algemene instellingen van webtoepassing](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="to-run-the-maintainer"></a><span data-ttu-id="3bca1-122">De Maintainer uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3bca1-122">To run the Maintainer</span></span>
* <span data-ttu-id="3bca1-123">Op de front-endwebserver in SharePoint 2013-beheershell de Maintainer als volgt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3bca1-123">On the web front-end server, in the SharePoint 2013 Management Shell, run the Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="3bca1-124">Alleen de `GarbageCollection` bewerking voor StorSimple wordt ondersteund op dit moment.</span><span class="sxs-lookup"><span data-stu-id="3bca1-124">Only the `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="3bca1-125">Let ook op dat de parameters die zijn uitgegeven voor Microsoft.Data.SqlRemoteBlobs.Maintainer.exe hoofdlettergevoelig zijn.</span><span class="sxs-lookup"><span data-stu-id="3bca1-125">Also note that the parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="to-revert-the-content-database-and-recycle-bin-settings"></a><span data-ttu-id="3bca1-126">De inhoud van de database en de Prullenbak-instellingen herstellen</span><span class="sxs-lookup"><span data-stu-id="3bca1-126">To revert the content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="3bca1-127">Voer op de SQL-Server in SQL Management Studio de volgende update-query's voor de doel-inhoudsdatabase:</span><span class="sxs-lookup"><span data-stu-id="3bca1-127">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="3bca1-128">Op de front-endwebserver in **Centraal beheer**, bewerk de **algemene instellingen van webtoepassing** voor de gewenste inhoud van de database opnieuw inschakelen van de Prullenbak.</span><span class="sxs-lookup"><span data-stu-id="3bca1-128">On the web front-end server, in **Central Administration**, edit the **Web Application General Settings** for the desired content database to re-enable the Recycle Bin.</span></span> <span data-ttu-id="3bca1-129">Om dit te doen, klikt u op **Centraal beheer** -> **Toepassingsbeheer** -> **webtoepassingen (web-apps beheren)**  ->  **SharePoint - 80** -> **algemene toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="3bca1-129">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="3bca1-130">De Status van Recycle Bin instellen op **ON**.</span><span class="sxs-lookup"><span data-stu-id="3bca1-130">Set the Recycle Bin Status to **ON**.</span></span>

