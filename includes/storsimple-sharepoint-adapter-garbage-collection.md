<!--author=SharS last changed: 9/17/15-->

U wordt in deze procedure:

1. [Uitvoerbaar bestand toorun Hallo Maintainer voorbereiden](#to-prepare-to-run-the-maintainer) .
2. [Hallo inhoud van de database en de Prullenbak voorbereiden voor onmiddellijke verwijdering van zwevende BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).
3. [Voer Maintainer.exe](#to-run-the-maintainer).
4. [Hallo inhoud van de database en de Prullenbak-instellingen herstellen](#to-revert-the-content-database-and-recycle-bin-settings).

#### <a name="tooprepare-toorun-hello-maintainer"></a>tooprepare toorun Hallo Maintainer
1. Open op de front-endwebserver hello, Hallo SharePoint 2013-beheershell als beheerder.
2. Navigeer toohello map *opstartschijf*: \Program Files\Microsoft 10.50\Maintainer SQL externe Blob-opslag\.
3. Wijzig de naam van **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** te**web.config**.
4. Gebruik `aspnet_regiis -pdf connectionStrings` toodecrypt Hallo web.config-bestand.
5. In Hallo ontsleutelde web.config-bestand, onder Hallo `connectionStrings` knooppunt toevoegen Hallo-verbindingsreeks voor de SQL server-exemplaar en Hallo de naam van de inhoud van de database. Zie Hallo voorbeeld te volgen.
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. Gebruik `aspnet_regiis –pef connectionStrings` toore-versleutelen Hallo web.config-bestand. 
7. Wijzig de naam van web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config. 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a>tooprepare hello inhoud van de database en de Prullenbak tooimmediately verwijderen zwevende BLOBs
1. Voer op Hallo SQL-Server in SQL Management Studio Hallo update query's voor Hallo doel inhoudsdatabase te volgen: 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. Op Hallo van web-front-endserver onder **Centraal beheer**, Hallo bewerken **algemene instellingen van webtoepassing** voor Hallo inhoudsdatabase tootemporarily uitschakelen Hallo Prullenbak gewenst. Deze actie wordt ook leeg Hallo Prullenbak voor een verzameling verwante site. toodo, klikt u op **Centraal beheer** -> **Toepassingsbeheer** -> **webtoepassingen (web-apps beheren)**  ->  **SharePoint - 80** -> **algemene toepassingsinstellingen**. Set Hallo **Status van de Prullenbak** te**OFF**.
   
    ![Algemene instellingen van webtoepassing](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a>toorun hello Maintainer
* Op de front-endwebserver hello, in SharePoint 2013-beheershell Hallo Hallo Maintainer als volgt uitvoeren:
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > Alleen Hallo `GarbageCollection` bewerking voor StorSimple wordt ondersteund op dit moment. Let ook op Hallo-parameters die zijn uitgegeven voor Microsoft.Data.SqlRemoteBlobs.Maintainer.exe zijn hoofdlettergevoelig. 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a>toorevert hello inhoud van de database en de Prullenbak-instellingen
1. Voer op Hallo SQL-Server in SQL Management Studio Hallo update query's voor Hallo doel inhoudsdatabase te volgen:
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. Op de front-endwebserver hello, in **Centraal beheer**, Hallo bewerken **algemene instellingen van webtoepassing** voor Hallo inhoudsdatabase toore inschakelen Hallo Prullenbak gewenst. toodo, klikt u op **Centraal beheer** -> **Toepassingsbeheer** -> **webtoepassingen (web-apps beheren)**  ->  **SharePoint - 80** -> **algemene toepassingsinstellingen**. Hallo Status van de Prullenbak te ingesteld**ON**.

