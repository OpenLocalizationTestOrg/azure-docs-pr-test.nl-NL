---
title: aaaSet een virtuele machine van SQL Server als een server IPython Notebook | Microsoft Docs
description: Instellen van een virtuele Machine met SQL Server en IPython Server van gegevens wetenschap.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1fd6014a-d180-4558-b4eb-d9b5a331a99f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: ee83d1d5de671d9817c1bc1abd6b4f9c256dde8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Een virtuele Azure SQL Server-machine instellen als IPython Notebook-server voor geavanceerde analyses
Dit onderwerp wordt beschreven hoe tooprovision en configureren van een SQL Server-virtuele machine toobe gebruikt als onderdeel van een cloud-gebaseerde gegevens wetenschap-omgeving. Hallo Windows virtuele machine is geconfigureerd met ondersteunende hulpprogramma's zoals IPython laptop, Azure Storage Explorer en AzCopy, evenals andere hulpprogramma's die handig voor gegevens wetenschappelijke projecten zijn. Azure Storage Explorer en AzCopy, bijvoorbeeld bieden handige manieren tooupload gegevens tooAzure blob-opslag van uw lokale computer of toodownload het lokale computer tooyour van blob-opslag.

Hallo galerie met virtuele machine van Azure bevat diverse installatiekopieën met Microsoft SQL Server. Selecteer de installatiekopie van een virtuele machine van SQL Server die geschikt is voor de gegevensbehoeften van uw. Aanbevolen afbeeldingen zijn:

* SQL Server 2012 SP2 Enterprise voor kleine toomedium gegevensgroottes
* SQL Server 2012 SP2 Enterprise geoptimaliseerd voor DataWarehousing werkbelastingen voor grote toovery grote hoeveelheden gegevens grootten
  
  > [!NOTE]
  > Afbeelding van SQL Server 2012 SP2 Enterprise **omvat een gegevensschijf niet**. U wordt moet tooadd en/of koppelen van een of meer virtuele harde schijven toostore uw gegevens. Wanneer u een virtuele machine in Azure maakt, heeft een schijf voor Hallo toegewezen toohello C besturingssysteemstation en een tijdelijke schijf toegewezen toohello D-station. Gebruik geen Hallo D-station toostore gegevens. Zoals Hallo-naam aangeeft, biedt deze alleen tijdelijke opslag. Biedt geen redundantie of back-up omdat deze zich niet in Azure-opslag.
  > 
  > 

## <a name="Provision"></a>Verbinding maken met toohello klassieke Azure-Portal en inrichten van een virtuele machine van SQL Server
1. Meld u bij toohello [klassieke Azure-portal](http://manage.windowsazure.com/) met uw account.
   Als u geen Azure-account hebt, gaat u naar [Azure, gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
2. Klik op de klassieke Azure-portal Hallo in de linkerbenedenhoek Hallo van Hallo webpagina **+ nieuw**, klikt u op **COMPUTE**, klikt u op **virtuele MACHINE**, en klik vervolgens op **FROM GALERIE**.
3. Op Hallo **maken van een virtuele Machine** pagina, selecteert u de installatiekopie van een virtuele machine met SQL Server op basis van de gegevensbehoeften van uw en klik op volgende pijl in de rechterbenedenhoek van pagina Hallo Hallo. Voor de meest actuele informatie Hallo op Hallo ondersteund installatiekopieën van SQL Server op Azure, Zie [aan de slag met SQL Server in Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=294720) onderwerp in Hallo [SQL Server in Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=294719) documentatieset.
   
   ![SQL Server-machine selecteren][1]
4. Op Hallo eerste **Virtuele-machineconfiguratie** pagina, geef de volgende informatie:
   
   * Geef een **virtuele-MACHINENAAM**.
   * In Hallo **nieuwe gebruikersnaam** vak, type unieke gebruikersnaam voor Hallo VM lokale administrator-account.
   * In Hallo **nieuw wachtwoord** typt u een sterk wachtwoord. Zie [Sterke wachtwoorden](http://msdn.microsoft.com/library/ms161962.aspx) voor meer informatie.
   * In Hallo **wachtwoord bevestigen** vak, typ nogmaals Hallo wachtwoord.
   * Selecteer Hallo juiste **grootte** van Hallo vervolgkeuzelijst.
     
     > [!NOTE]
     > Hallo-grootte van Hallo virtuele machine wordt opgegeven tijdens het inrichten: A2 is Hallo kleinste grootte aanbevolen voor productieworkloads. De minimale aanbevolen grootte voor een virtuele machine is A3 bij gebruik van SQL Server Enterprise Edition. Selecteer A3 of hoger als u SQL Server Enterprise Edition. A4 selecteren wanneer u een SQL Server 2012 of 2014 Enterprise geoptimaliseerd voor transactionele werkbelastingen afbeeldingen.
     > A7 selecteren wanneer u een SQL Server 2012 of 2014 Enterprise geoptimaliseerd voor afbeeldingen van Data Warehousing werkbelastingen. Hallo beperkt geselecteerd het aantal gegevensschijven die u kunt configureren. Zie voor de meest actuele informatie over grootten van de beschikbare virtuele machine en het aantal gegevensschijven Hallo dat u tooa virtuele machine kunt koppelen, [grootten van virtuele machines voor Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Zie voor informatie over prijzen, [virtuele Macines prijzen](https://azure.microsoft.com/pricing/details/virtual-machines/).
     > 
     > 
   
   Klik op volgende pijl Hallo op Hallo onderkant rechts toocontinue.
   
   ![VM-configuratie][2]
5. Op Hallo tweede **Virtuele-machineconfiguratie** pagina, resources voor netwerken, opslag en beschikbaarheid te configureren:
   
   * In Hallo **Cloudservice** Kies **Maak een nieuwe cloudservice**.
   * In Hallo **Cloud Service DNS-naam** Geef Hallo het eerste deel van een DNS-naam van uw keuze, zodat deze is voltooid met een naam in de notatie **TESTNAME.cloudapp.net**
   * In Hallo **regio/AFFINITEIT groep/VIRTUEEL netwerk** Selecteer een regio waar deze virtuele-installatiekopie wordt gehost.
   * In Hallo **Opslagaccount**, selecteer een bestaand opslagaccount of Selecteer een automatisch gegenereerde.
   * In Hallo **BESCHIKBAARHEIDSSET** de optie **(geen)**.
   * Lees en accepteer Hallo prijsinformatie.
6. In Hallo **EINDPUNTEN** sectie, klikt u op Hallo leeg vervolgkeuzelijst onder **naam**, en selecteer **MSSQL** typt u het poortnummer Hallo van het exemplaar van Database-Engine (Hallo**1433** voor het standaardexemplaar Hallo).
7. Uw SQL Server VM kan ook fungeren als een IPython laptop-Server, die worden geconfigureerd in een latere stap.
   Voeg een nieuw eindpunt toospecify Hallo poort toouse voor uw laptop IPython-server. Voer een naam in Hallo **naam** kolom, selecteer een poortnummer van uw keuze voor de openbare poort Hallo en 9999 voor Hallo particuliere poort.
   
   Klik op volgende pijl Hallo op Hallo onderkant rechts toocontinue.
   
   ![Selecteer de MSSQL- en IPython-poorten][3]
8. Accepteer de standaardinstelling Hallo **installeren VM-agent** optie gecontroleerd en klikt u op Hallo Hallo vinkje in de rechterbenedenhoek van Hallo wizard toocomplete Hallo VM inrichtingsproces Hallo.
   
   `![Laatste VM-opties][4]
9. Een ogenblik geduld terwijl Azure de virtuele machine wordt voorbereid. Hallo virtuele machine status tooproceed via verwacht:
   
   * (Inrichting) wordt gestart
   * Stopped
   * (Inrichting) wordt gestart
   * Uitgevoerd (Provisioning genoemd)
   * Running

## <a name="RemoteDesktop"></a>Open Hallo virtuele machine met behulp van extern bureaublad- en volledige installatie
1. Bij het inrichten is voltooid, klik op Hallo-naam van de dashboardpagina van virtuele machine toogo toohello. Klik onder aan de pagina Hallo Hallo op **Connect**.
2. Kies tooopen Hallo rpd bestand via Extern bureaublad van Windows-programma Hallo (`%windir%\system32\mstsc.exe`).
3. Op Hallo **Windows-beveiliging** dialoogvenster vak, Hallo wachtwoord opgeven voor het lokale beheerdersaccount dat u in een eerdere stap hebt opgegeven.
   (U wordt mogelijk gevraagd referenties op Hallo tooverify van Hallo virtuele machine.)
4. Hallo eerste keer dat u zich aanmeldt toothis virtuele machine, verschillende processen mogelijk toocomplete, waaronder de instelling van uw bureaublad, Windows-updates en Hallo Windows Initiële configuratietaken (sysprep) is voltooid. Nadat Windows sysprep is voltooid, voltooit de installatie van SQL Server configuratietaken. Deze taken kunnen ertoe leiden dat een vertraging van enkele minuten duren terwijl ze worden voltooid. `SELECT @@SERVERNAME`kan de juiste naam Hallo pas weer beschikbaar nadat SQL Server setup is voltooid, en SQL Server Management Studio mag niet op de startpagina Hallo visable.

Wanneer u verbonden toohello virtuele machine via Extern bureaublad van Windows bent, zoals Hallo virtuele machine werkt veel een andere computer. Verbinding maken met toohello standaardexemplaar van SQL Server met SQL Server Management Studio (Hallo virtuele machine waarop) in Hallo normale wijze.

## <a name="InstallIPython"></a>IPython laptops en andere ondersteunende hulpprogramma's installeren
tooconfigure uw nieuwe SQL Server VM tooserve als IPython Notebook server en installatie extra ondersteunende hulpprogramma's voor anderen deze AzCopy, Azure Storage Explorer en nuttige gegevens wetenschappelijke Python-pakketten, een script speciale aanpassing tooyou is opgegeven. tooinstall:

1. Klik met de rechtermuisknop Hallo **Start Windows** pictogram en klik op **opdrachtprompt (Admin)**
2. Hallo opdrachten na kopiëren en plakken op Hallo-opdrachtregel.
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. Wanneer u wordt gevraagd, voert u een wachtwoord van uw keuze voor Hallo IPython laptop-server.
4. Hallo aanpassing script automatiseert verschillende procedures voor na de installatie, waaronder:
    * Installatie en configuratie van de server IPython Notebook
    * TCP-poorten openen in Hallo Windows firewall voor Hallo eindpunten eerder hebt gemaakt:
    * Voor SQL Server externe verbindingen
    * Voor de IPython Notebook server externe verbindingen
    * Ophalen van voorbeeld IPython notitieblokken en -SQL-scripts
    * Het downloaden en installeren van de nuttige gegevens wetenschappelijke Python-pakketten
    * Downloaden en installeren van Azure-hulpprogramma's zoals AzCopy en Azure Opslagverkenner  
    <br>
5. U kunt toegang tot en IPython Notebook uitvoeren vanaf een lokale of externe browser met een URL van Hallo formulier `https://<virtual_machine_DNS_name>:<port>`, waarbij Hallo IPython openbare poort u is tijdens het inrichten van Hallo virtuele machine hebt geselecteerd.
6. IPython Notebook server wordt uitgevoerd als een achtergrondservice en wordt opnieuw opgestart wanneer u Hallo virtuele machine opnieuw opstart.

## <a name="Optional"></a>Gegevensschijf koppelen, indien nodig
Als uw VM-installatiekopie bevat geen gegevensschijven, dat wil zeggen, schijven dan C-schijf (schijf OS) en de D-station (tijdelijke schijf), moet u tooadd een of meer gegevens schijven toostore uw gegevens. Hallo VM-installatiekopie voor SQL Server 2012 SP2 Enterprise geoptimaliseerd voor DataWarehousing werkbelastingen wordt geleverd met andere schijven voor SQL Server-gegevens en logboekbestanden vooraf geconfigureerd.

> [!NOTE]
> Gebruik geen Hallo D-station toostore gegevens. Zoals Hallo-naam aangeeft, biedt deze alleen tijdelijke opslag. Biedt geen redundantie of back-up omdat deze zich niet in Azure-opslag.
> 
> 

Extra gegevensschijven tooattach, volg de stappen Hallo in [hoe tooAttach een gegevensschijf tooa virtuele Windows-Machine](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), die begeleidt u bij:

1. Een of meer schijven leeg toohello virtuele machine is ingericht in de eerdere stappen koppelen
2. Initialisatie van Hallo nieuwe schijf of schijven in Hallo virtuele machine

## <a name="SSMS"></a>Verbinding maken met tooSQL Server Management Studio en verificatie in gemengde modus inschakelen
Hallo SQL Server Database Engine kan geen Windows-verificatie gebruiken zonder domeinomgeving. SQL Server tooconnect toohello Database-Engine vanaf een andere computer configureren voor verificatie in gemengde modus. Verificatie in gemengde modus maakt zowel SQL Server-verificatie als Windows-verificatie mogelijk. SQL-verificatiemodus is vereist in de volgorde tooingest gegevens rechtstreeks vanuit uw virtuele machine van SQL Server-databases in de [Azure Machine Learning Studio](https://studio.azureml.net) met Hallo gegevens importeren-module.

1. Tijdens het verbonden toohello virtuele machine via Extern bureaublad gebruiken Windows hello **Search** deelvenster en type **SQL Server Management Studio** (SMSS). Klik op toostart Hallo SQL Server Management Studio (SSMS). U kunt op het bureaublad een snelkoppeling tooSSMS tooadd voor toekomstig gebruik.
   
   ![Starten van SSMS][5]
   
   Hallo eerste keer openen van Management Studio het Hallo gebruikers Management Studio omgeving moet maken. Dit kan even duren.
2. Wanneer u opent, Management Studio Hallo geeft **tooServer verbinding** in het dialoogvenster. In Hallo **servernaam** vak, Hallo-typenaam van Hallo virtuele machine tooconnect toohello Database-Engine Hello Object Explorer.
   (In plaats van de naam van de virtuele machine Hallo ook kunt u **(lokaal)** of een enkele periode als Hallo **servernaam**. Selecteer **Windows-verificatie**, en laat  ***uw\_VM\_naam*\\uw\_lokale\_beheerder**  in Hallo **gebruikersnaam** vak. Klik op **Verbinden**.
   
   ![Verbinding maken met tooServer][6]
   
   <br>
   
   > [!TIP]
   > U kunt Hallo SQL Server-verificatiemodus met behulp van een wijziging van de registersleutel Windows of SQL Server Management Studio Hallo via wijzigen. verificatiemodus toochange Hallo wijziging van de registersleutel, start met een **nieuwe Query** en Hallo volgende script uit te voeren:
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    toochange met behulp van SQL Server management Studio Hallo verificatiemodus:

1. In **SQL Server Management Studio Object Explorer**, met de rechtermuisknop op de naam van het Hallo-exemplaar van SQL Server (Hallo virtuele machine-naam) en klik vervolgens op **eigenschappen**.
   
   ![Servereigenschappen][7]
2. Op Hallo **beveiliging** pagina onder **serververificatie**, selecteer **modus van SQL Server en Windows-verificatie**, en klik vervolgens op **OK** .
   
   ![Verificatiemodus selecteren][8]
3. In Hallo **SQL Server Management Studio** in het dialoogvenster, klikt u op **OK** bevestiging Hallo vereiste toorestart SQL Server.
4. In **Objectverkenner**, met de rechtermuisknop op uw server en klik vervolgens op **opnieuw**. (Als SQL Server Agent actief is, moet deze ook opnieuw worden gestart.)
   
   ![Opnieuw starten][9]
5. In Hallo **SQL Server Management Studio** in het dialoogvenster, klikt u op **Ja** accepteren die u wilt dat toorestart SQL Server.

## <a name="Logins"></a>SQL Server-verificatie-aanmeldingen maken
tooconnect toohello Database-Engine vanaf een andere computer, moet u ten minste één aanmelding voor SQL Server-verificatie.  

U kunt nieuwe SQL Server-aanmeldingen via een programma maken of met behulp van SQL Server Management Studio Hallo. een nieuwe gebruiker sysadmin met SQL-verificatie via een programma, start toocreate een **nieuwe Query** en Hallo volgende script uit te voeren. Vervang < nieuwe gebruikersnaam\> en < nieuw wachtwoord\> met van uw keuze *gebruikersnaam* en *wachtwoord*. 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


Hallo-wachtwoordbeleid pas naar wens (Hallo voorbeeldcode wordt uitgeschakeld beleid controleren en het wachtwoord verlopen). Zie [Create a Login](http://msdn.microsoft.com/library/aa337562.aspx) (Een aanmelding maken) voor meer informatie over SQL Server-aanmeldingen.  

toocreate nieuwe SQL Server-aanmeldingen met behulp van SQL Server Management Studio Hallo:

1. In **SQL Server Management Studio Object Explorer**, vouw de map Hallo van server-exemplaar Hallo waarin wordt gezocht toocreate Hallo nieuwe aanmelding.
2. Met de rechtermuisknop op Hallo **beveiliging** map, wijs te**nieuw**, en selecteer **aanmelding...** .
   
   ![Nieuwe aanmelding][10]
3. In Hallo **Login - nieuwe** op Hallo van het dialoogvenster **algemene** pagina, voert u Hallo-naam van de nieuwe gebruiker Hallo in Hallo **aanmeldingsnaam** vak.
4. Selecteer **SQL Server-verificatie**.
5. In Hallo **wachtwoord** Voer een wachtwoord voor de nieuwe gebruiker Hallo. Dit wachtwoord opnieuw invoeren in Hallo **wachtwoord bevestigen** vak.
6. Selecteer tooenforce wachtwoord beleidsopties voor complexiteit en afdwinging **wachtwoordbeleid afdwingen** (aanbevolen). Dit is een standaardoptie wanneer SQL Server-verificatie is geselecteerd.
7. tooenforce wachtwoord beleidsopties voor verloop, selecteer **Wachtwoordverlooptijd afdwingen** (aanbevolen). Wachtwoordbeleid afdwingen moet geselecteerde tooenable dit selectievakje in. Dit is een standaardoptie wanneer SQL Server-verificatie is geselecteerd.
8. tooforce hello gebruiker toocreate een nieuw wachtwoord nadat Hallo de eerste keer dat de aanmelding wordt gebruikt, selecteer **gebruiker moet wachtwoord bij volgende aanmelding wijzigen** (aanbevolen als deze aanmelding voor iemand anders toouse. Als het Hallo-aanmelding is voor eigen gebruik, deze optie niet.) Afdwingen van verlopen van wachtwoorden moet geselecteerde tooenable dit selectievakje in. Dit is een standaardoptie wanneer SQL Server-verificatie is geselecteerd.
9. Van Hallo **standaarddatabase** , selecteert u een standaarddatabase voor Hallo aanmelding. **master** Hallo standaardwaarde voor deze optie is. Als u een gebruikersdatabase nog geen hebt gemaakt, laat u deze set te**master**.
10. In Hallo **standaardtaal** lijst, laat u **standaard** Hallo-waarde.
    
    ![Aanmeldingseigenschappen][11]
11. Als dit de eerste aanmelding Hallo die u maakt, kunt u deze aanmelding aanwijzen als een SQL Server-beheerder. Schakel hiervoor het selectievakje **sysadmin** in op de pagina **Serverrollen**.
    
    > [!IMPORTANT]
    > Leden van de vaste serverrol sysadmin voor Hallo hebben volledige controle over Hallo Database-Engine. Uit veiligheidsoverwegingen moet u zorgvuldig lidmaatschap van deze rol te beperken.
    > 
    > 
    
    ![sysadmin][12]
12. Klik op OK.

## <a name="DNS"></a>Hallo DNS-naam van de virtuele machine van Hallo bepalen
tooconnect toohello SQL Server Database Engine vanaf een andere computer, moet u weten Hallo Domain Name System (DNS) naam van het Hallo virtuele machine.

(Dit is Hallo naam Hallo internet gebruikt tooidentify Hallo virtuele machine. Kunt u Hallo IP-adres, maar Hallo IP-adres veranderen wanneer Azure bronnen voor redundantie en -onderhoud verplaatst. Hallo DNS-naam worden stabiele omdat deze kan worden omgeleid tooa nieuwe IP-adres.)

1. Selecteer in de klassieke Azure-Portal hello (of van de vorige stap Hallo) **virtuele MACHINES**.
2. Op Hallo **exemplaren van de virtuele MACHINE** pagina in Hallo **DNS-naam** kolom, zoeken en kopiëren Hallo DNS-naam voor de Hallo virtuele machine die wordt weergegeven, voorafgegaan door **http://**. (Hallo-gebruikersinterface mogelijk niet weergegeven voor de volledige naam hello, maar u kunt met de rechtermuisknop op het en selecteert u kopiëren.)

## <a name="cde"></a>Verbinding maken met Database-Engine toohello vanaf een andere computer
1. Op een computer verbonden toohello internet, open SQL Server Management Studio.
2. In Hallo **verbinding tooServer** of **tooDatabase Engine verbinding** dialoogvenster in Hallo **servernaam** Hallo DNS- naam van de virtuele machine (zoals bepaald in Hallo vorige taak) en het poortnummer van een openbaar eindpunt in de indeling van Hallo *DNSName, portnumber* zoals **tutorialtestVM.cloudapp.net,57500**.
3. In Hallo **verificatie** de optie **SQL Server-verificatie**.
4. In Hallo **aanmelding** vak, type Hallo-naam van een aanmelding die u in een eerdere taak gemaakt.
5. In Hallo **wachtwoord** vak, het type wachtwoord op Hallo van Hallo-aanmelding die u in een eerdere taak maakt.
6. Klik op **Verbinden**.

## <a name="amlconnect"></a>Verbinding maken met toohello Database-Engine van Azure Machine Learning
In latere stadia van Hallo Team gegevens wetenschappelijke processen, gebruikt u Hallo [Azure Machine Learning Studio](https://studio.azureml.net) toobuild en implementeren van machine learning-modellen. tooingest gegevens uit uw virtuele machine van SQL Server-databases rechtstreeks in Azure Machine Learning voor het trainen of score berekenen, gebruikt u Hallo **importgegevens** module in een nieuw [Azure Machine Learning Studio](https://studio.azureml.net) experimenteren. In dit onderwerp wordt beschreven in meer gegevens via Hallo Team gegevens wetenschap proces handleiding koppelingen. Zie voor een inleiding [wat is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md).

1. In Hallo **eigenschappen** deelvenster Hallo [gegevens importeren-module](https://msdn.microsoft.com/library/azure/dn905997.aspx), selecteer **Azure SQL Database** van Hallo **gegevensbron** vervolgkeuzelijst.
2. In Hallo **databaseservernaam** tekst Voer`tcp:<DNS name of your virtual machine>,1433`
3. Hallo SQL-gebruikersnaam opgeven in Hallo **Server gebruikersaccountnaam** in het tekstvak.
4. Voer het wachtwoord van gebruiker Hallo-sql in Hallo **Server het wachtwoord voor gebruikersaccount** in het tekstvak.
   
   ![Gegevens van Azure Machine Learning importeren][13]

## <a name="shutdown"></a>Afsluiten en toewijzing van de virtuele machine als deze niet in gebruik
Virtuele Machines in Azure worden berekend als **Betaal alleen voor wat u**. tooensure die u niet worden kosten in rekening gebracht wanneer de virtuele machine niet wordt gebruikt, heeft de toobe hello **gestopt (Deallocated)** status.

> [!NOTE]
> Hallo virtuele machine afsluiten uit binnen (met behulp van Windows-Energiebeheer) hello VM is gestopt maar blijft toegewezen. u bent niet in rekening wordt gebracht, tooensure wordt altijd gestopt als virtuele machines van Hallo [klassieke Azure-Portal](http://manage.windowsazure.com/). U kunt ook Hallo VM via Powershell door het aanroepen van ShutdownRoleOperation met 'PostShutdownAction' gelijk te stoppen 'StoppedDeallocated'.
> 
> 

tooshutdown en Hallo virtuele machine ongedaan gemaakt:

1. Meld u bij toohello [klassieke Azure-Portal](http://manage.windowsazure.com/) met uw account.  
2. Selecteer **virtuele MACHINES** van Hallo linkernavigatiebalk.
3. Hallo lijst met virtuele machines, klik op het Hallo-naam van uw virtuele machine en ga toohello **DASHBOARD** pagina.
4. Klik onder aan de pagina Hallo Hallo op **afsluiten**.

![VM afsluiten][15]

Hallo virtuele machine wordt de toewijzing ongedaan gemaakt maar niet verwijderd. U kunt uw virtuele machine opnieuw opstarten op elk gewenst moment Hallo klassieke Azure-Portal.

## <a name="your-azure-sql-server-vm-is-ready-toouse-whats-next"></a>Uw Azure SQL Server-VM is gereed toouse: Wat is het volgende?
De virtuele machine is nu gereed toouse in uw gegevens wetenschappelijke oefeningen. Hallo virtuele machine is ook klaar voor gebruik als een server IPython Notebook voor Hallo exploratie en verwerking van gegevens en andere taken in combinatie met Azure Machine Learning en Hallo Team gegevens wetenschap proces (TDSP).

Hello zijn de volgende stappen in Hallo gegevens wetenschap proces toegewezen in Hallo [Team gegevens wetenschappelijke processen](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) en stappen voor het verplaatsen van gegevens in HDInsight, proces en het voorbeeld ter voorbereiding van het leren van Hallo gegevens met Azure Machine bevatten mogelijk Learning.

[1]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/selectsqlvmimg.png
[2]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/4vm-config.png
[3]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/sqlvmports.png
[4]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmpostopts.png
[5]:./media/machine-learning-data-science-setup-sql-server-virtual-machine/searchssms.png
[6]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/19connect-to-server.png
[7]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/20server-properties.png
[8]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/21mixed-mode.png
[9]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/22restart2.png
[10]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/23new-login.png
[11]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/24test-login.png
[12]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/25sysadmin.png
[13]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/amlreader.png
[15]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmshutdown.png

