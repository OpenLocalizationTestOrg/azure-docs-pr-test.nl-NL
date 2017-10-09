<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> Wanneer u wijzigingen toohello StorSimple-Adapter voor de configuratie van SharePoint RBS, moet u zijn aangemeld met een gebruikersaccount die deel uitmaakt van de groep Domeinadministrators toohello. Bovendien moet u toegang tot de configuratiepagina Hallo vanuit een browser die wordt uitgevoerd op dezelfde als een Centraalbeheersite host Hallo.
> 
> 

#### <a name="tooconfigure-rbs"></a>tooconfigure Resourcestructuur
1. Open de pagina SharePoint Centraal beheer Hallo en te bladeren**systeeminstellingen**. 
2. In Hallo **Azure StorSimple** sectie, klikt u op **StorSimple-Adapter configureren**.
   
    ![Hallo StorSimple Adapter configureren](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. Op Hallo **StorSimple-Adapter configureren** pagina:
   
   1. Zorg ervoor dat Hallo **inschakelen bewerken pad** selectievakje is ingeschakeld.
   2. Typ in het tekstvak hello, Hallo Universal Naming Convention (UNC) pad naar Hallo bloblarchief.
      
      > [!NOTE]
      > Hallo BLOB store-volume moet worden gehost op een iSCSI-volume dat is geconfigureerd op Hallo StorSimple-apparaat.

   3. Klik op Hallo **inschakelen** knop onder elk van de inhoudsdatabases hello wilt u tooconfigure voor externe opslag.
      
      > [!NOTE]
      > Hallo bloblarchief moet worden gedeeld en bereikbaar door alle web-front-(WFE)-servers en Hallo-gebruikersaccount dat is geconfigureerd voor Hallo SharePoint-serverfarm toegang toohello share moet hebben.
      
      ![Hallo Resourcestructuur provider ingeschakeld](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      Als u inschakelt of Resourcestructuur uitschakelt, ziet u ook Hallo-bericht te volgen.
      
      ![Uitschakelen van StorSimple Adapter configureren](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. Klik op Hallo **Update** knop tooapply Hallo configuratie. Wanneer u klikt op Hallo **Update** knop Hallo Resourcestructuur configuratiestatus wordt bijgewerkt op alle WFE-servers en volledige farm Hallo worden Resourcestructuur ingeschakeld. Hallo volgende bericht wordt weergegeven.
      
      ![Adapter configuratiebericht](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > Als u Resourcestructuur configureert voor een SharePoint-farm met een zeer groot aantal databases (groter dan 200), mogelijk Hallo Centraal beheer van SharePoint-webpagina time-out. Als dit het geval is, moet u Hallo pagina vernieuwen. Dit heeft geen invloed op Hallo-configuratieproces.

4. Hallo-configuratie controleren:
   
   1. Meld u aan toohello Centraal beheer van SharePoint-website en bladeren toohello **StorSimple-Adapter configureren** pagina.
   2. Controleer de configuratie details toomake Hallo zeker van te zijn dat ze overeenkomen met de Hallo-instellingen die u hebt opgegeven. 
5. Controleer of Resourcestructuur correct werkt:
   
   1. Upload een tooSharePoint document. 
   2. Blader toohello UNC-pad dat u hebt geconfigureerd. Zorg ervoor dat Hallo Resourcestructuur mapstructuur is gemaakt en dat deze geüpload Hallo-object bevat.
6. (Optioneel) U kunt Microsoft RBS Hallo `Migrate()` PowerShell-cmdlet die deel uitmaakt van SharePoint toomigrate bestaande BLOB inhoud toohello StorSimple-apparaat. Zie voor meer informatie [inhoud migreert van of naar Resourcestructuur in SharePoint 2013] [ 6] of [inhoud migreert van of naar Resourcestructuur (SharePoint Foundation 2010)] [7].
7. (Optioneel) U kunt op test-installaties controleren Hallo BLOBs als volgt buiten de inhoudsdatabase Hallo zijn verplaatst: 
   
   1. Start SQL Management Studio.
   2. Hallo ListBlobsInDB_2010.sql of ListBlobsInDB_2013.sql query uitvoert, als volgt.
      
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
      
      Als Resourcestructuur correct is geconfigureerd, wordt een NULL-waarde in Hallo SizeOfContentInDB kolom voor elk object dat is geüpload en met succes externalized met Resourcestructuur weergegeven.
8. (Optioneel) Nadat u Resourcestructuur configureren en verplaatst u alle BLOBS inhoud toohello StorSimple-apparaat, kunt u Hallo inhoudsdatabase toohello apparaat verplaatsen. Als u toomove Hallo inhoud van de database kiest, raden wij u Hallo inhoudsdatabase opslag configureren op Hallo-apparaat als primaire volume. Vervolgens gebruik tot stand gebracht dat SQL Server best practices toomigrate Hallo inhoudsdatabase toohello StorSimple-apparaat. 
   
   > [!NOTE]
   > Zwevend Hallo inhoudsdatabase toohello apparaat wordt alleen ondersteund voor Hallo StorSimple 8000 serie (dit wordt niet ondersteund voor Hallo 5000 of 7000-serie).
   
   Als u BLOBs en Hallo inhoudsdatabase in afzonderlijke volumes op Hallo StorSimple-apparaat opslaat, raden wij aan dat u ze in Hallo configureren dezelfde volumecontainer. Dit zorgt ervoor dat er wordt een back-samen.
   
   > [!WARNING]
   > Als u Resourcestructuur niet hebt ingeschakeld, raden we niet verplaatsen Hallo inhoudsdatabase toohello StorSimple-apparaat. Dit is een niet-geteste configuratie.
   
9. De volgende stap gaat u toohello: [garbagecollection configureren](#configure-garbage-collection).

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
