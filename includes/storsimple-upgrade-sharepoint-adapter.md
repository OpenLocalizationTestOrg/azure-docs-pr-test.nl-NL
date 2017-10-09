<!--author=SharS last changed: 9/17/15-->

### <a name="upgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-storsomple-adapter-for-sharepoint"></a>Upgrade van SharePoint 2010 tooSharePoint 2013 en installeer vervolgens Hallo StorSomple Adapter voor SharePoint
> [!IMPORTANT]
> Alle bestanden die eerder zijn verplaatst tooexternal opslag via de Resourcestructuur worden pas beschikbaar Hallo-upgrade is voltooid en Hallo Resourcestructuur functie is weer ingeschakeld. toolimit gebruiker invloed, voert u een upgrade of herinstallatie tijdens een geplande onderhoudsvenster.
> 
> 

#### <a name="tooupgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-adapter"></a>SharePoint 2010 tooupgrade tooSharePoint 2013 en vervolgens het Hallo-adapter installeren
1. Opmerking Hallo BLOB pad voor Hallo opslaan externalized in Hallo SharePoint 2010-farm, BLOBs en het Hallo-inhoudsdatabases waarvoor Resourcestructuur is ingeschakeld. 
2. Installeer en configureer Hallo nieuwe SharePoint 2013-farm. 
3. Het verplaatsen van databases, toepassingen en siteverzamelingen van SharePoint 2010 Hallo farm toohello nieuwe SharePoint 2013-farm. Voor instructies gaat te[overzicht van Hallo upgradeproces tooSharePoint 2013](https://technet.microsoft.com/library/cc262483.aspx).
4. Hallo StorSimple-Adapter installeren voor SharePoint op Hallo nieuwe farm. Ga te[installeren Hallo StorSimple-Adapter voor SharePoint](#install-the-storsimple-adapter-for-sharepoint) voor procedures.
5. Met Hallo-informatie die u in stap 1 hebt genoteerd, Resourcestructuur inschakelen voor Hallo dezelfde set inhoudsdatabases en geef Hallo pad dat is gebruikt dezelfde BLOB opslaan in Hallo SharePoint 2010-installatie. Ga te[Resourcestructuur configureren](#configure-rbs) voor procedures. Nadat u deze stap hebt voltooid, moeten eerder externalized bestanden via Hallo nieuwe farm toegankelijk zijn. 

### <a name="upgrade-hello-storsimple-adapter-for-sharepoint"></a>Hallo StorSimple Adapter voor SharePoint bijwerken
> [!IMPORTANT]
> U moet deze upgrade toooccur plannen tijdens een geplande onderhoudsvenster voor Hallo volgende redenen:
> 
> * Eerder worden externalized inhoud pas beschikbaar Hallo-adapter wordt opnieuw geïnstalleerd.
> * Alle inhoud geüpload toohello site nadat u eerdere versie van de Hallo Hallo StorSimple Adapter voor SharePoint verwijderen, maar voordat u de nieuwe versie hello, installeert in de inhoudsdatabase Hallo worden opgeslagen. U moet toomove dat inhoud toohello StorSimple-apparaat na de installatie van nieuwe Hallo-adapter. U kunt Microsoft hello` RBS Migrate()` PowerShell-cmdlet die deel uitmaakt van SharePoint toomigrate Hallo-inhoud. Zie voor meer informatie [inhoud migreert van of naar Resourcestructuur](https://technet.microsoft.com/library/ff628255.aspx). 
> 
> 

#### <a name="tooupgrade-hello-storsimple-adapter-for-sharepoint"></a>tooupgrade hello StorSimple-Adapter voor SharePoint
1. Hallo eerdere versie van StorSimple-Adapter verwijderen voor SharePoint.
   
   > [!NOTE]
   > Hiermee worden automatisch Resourcestructuur op Hallo inhoudsdatabases uitgeschakeld. Bestaande BLOBs blijven echter op Hallo StorSimple-apparaat. Omdat Resourcestructuur is uitgeschakeld en Hallo BLOBs niet gemigreerde back toohello inhoudsdatabases zijn, mislukken alle aanvragen voor deze BLOBs. 
   > 
   > 
2. Nieuwe StorSimple-Adapter installeren Hallo voor SharePoint. Hallo nieuwe adapter Hallo-inhoudsdatabases die eerder zijn ingeschakeld of uitgeschakeld voor Resourcestructuur automatisch herkent en de bestaande instellingen hello worden gebruikt.

