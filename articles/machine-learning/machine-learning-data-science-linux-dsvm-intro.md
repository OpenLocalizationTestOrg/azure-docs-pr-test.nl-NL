---
title: aaaProvision hello Linux gegevens wetenschappelijke virtuele Machine | Microsoft Docs
description: Configureren en een Linux gegevens wetenschappelijke virtuele Machine maken op Azure toodo analytics en machine learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3bab0ab9-3ea5-41a6-a62a-8c44fdbae43b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 81dfa90f6cd4b4f33535a20fb97442bf9152d829
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-linux-data-science-virtual-machine"></a>Hallo Linux gegevens wetenschappelijke virtuele Machine inrichten
Hallo Linux gegevens wetenschappelijke virtuele Machine is een CentOS gebaseerde Azure virtuele machine die wordt geleverd met vooraf geïnstalleerde programma's. Deze hulpprogramma's worden meestal gebruikt voor het uitvoeren van gegevensanalyse en machine learning. Hallo belangrijke software-onderdelen opgenomen zijn:

* Besturingssysteem: CentOS Linux-distributie.
* Microsoft R Server Developer Edition
* Anaconda Python-distributie (versies 2.7 en 3.5), met inbegrip van populaire gegevens analysebibliotheken
* JuliaPro - een curated verdeling van Julia taal met populaire wetenschappelijke en gegevens analytics-bibliotheken
* Standalone Spark-exemplaar en één knooppunt Hadoop (HDFS, Yarn)
* JupyterHub - een voor meerdere gebruikers Jupyter-notebook server R, Python, PySpark, Julia kernels ondersteunen
* Azure Opslagverkenner
* Azure-opdrachtregelinterface (CLI) voor het beheren van Azure-resources
* PostgresSQL Database
* Machine learning-hulpprogramma 's
  * [Rekenkundige netwerk Toolkit (CNTK)](https://github.com/Microsoft/CNTK): een diepe learning toolkit software van Microsoft Research.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): een snel machine learning-technieken zoals online, hash, allreduce, kortingen, learning2search, actief, ondersteunende system en interactieve daarvan te leren.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): een hulpprogramma dat snelle en nauwkeurige gestimuleerd structuur-implementatie.
  * [Rattle](http://rattle.togaware.com/) (R analytische hulpprogramma tooLearn eenvoudig hello): een hulpprogramma dat aan de slag met data analytics en machine learning in R eenvoudig met een GUI-gebaseerde gegevensverkenning en modellering met automatische R codegeneratie maakt.
* Azure SDK in Java, Python, node.js, Ruby, PHP
* Bibliotheken in R- en Python voor gebruik in Azure Machine Learning en andere Azure-services
* Ontwikkelingsprogramma's en editors (RStudio, PyCharm, IntelliJ, Emacs, gedit, vi)


Tijdens het doorzoeken van wetenschappelijke gegevens omvat sequentieel op een reeks taken:

1. Zoeken, laden en vooraf verwerken van gegevens
2. Maken en testen van modellen
3. Hallo-modellen voor verbruik in intelligente toepassingen implementeren

Gegevenswetenschappers gebruik toocomplete van verschillende hulpprogramma's voor deze taken. Het kan erg tijdrovend toofind Hallo juiste versies van Hallo-software zijn, en vervolgens toodownload, compileren en installeren van deze versies.

Hallo Linux gegevens wetenschappelijke virtuele Machine kan deze last aanzienlijk verminderen. Daarmee toojump start uw project analytics. Hiermee kunt u toowork op taken in verschillende talen, waaronder R, Python, SQL, Java en C++. Eclipse biedt een IDE-toodevelop en testen van uw code die eenvoudig toouse is. Hello Azure SDK is opgenomen in Hallo VM kunt u toobuild uw toepassingen met behulp van verschillende services op Linux voor Hallo Microsoft cloud-platform. Bovendien hebt u toegang tooother talen zoals Ruby, Perl, PHP en node.js die vooraf zijn geïnstalleerd.

Er zijn geen kosten voor software voor deze gegevens wetenschappelijke VM-installatiekopie. U betaalt alleen Hallo gebruik van Azure hardware kosten die worden beoordeeld op basis van Hallo grootte van Hallo virtuele machine die u met Hallo VM-installatiekopie inricht. Meer informatie over Hallo compute kosten vindt u op Hallo [VM aanbiedingspagina op Hallo Azure Marketplace ](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm/).

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Andere versies van Hallo gegevens wetenschappelijke virtuele Machine
Een [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) installatiekopie ook beschikbaar is, met veel Hallo dezelfde zoals CentOS installatiekopie plus grondige learning frameworks Hallo tools. Een [Windows](machine-learning-data-science-provision-vm.md) installatiekopie is ook beschikbaar.

## <a name="prerequisites"></a>Vereisten
Voordat u een Linux gegevens wetenschappelijke virtuele Machine maken kunt, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**: één, Zie tooobtain [gratis proefversie van Azure ophalen](https://azure.microsoft.com/free/).
* **Een Azure storage-account**: één, Zie toocreate [maken van een Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account). Hallo-opslagaccount kan ook worden gemaakt als onderdeel van het Hallo-proces voor het maken van Hallo VM, als u niet dat een bestaand account toouse wilt.

## <a name="create-your-linux-data-science-virtual-machine"></a>Uw gegevens Linux wetenschappelijke virtuele Machine maken
Hier volgen Hallo stappen toocreate een exemplaar van Hallo Linux gegevens wetenschappelijke virtuele Machine:

1. Navigeer toohello virtuele machine op Hallo aanbieding [Azure-portal](https://portal.azure.com/#create/microsoft-ads.linux-data-science-vmlinuxdsvm).
2. Klik op **maken** (onderin Hallo) toobring Hallo-wizard.![ Configureer-gegevens-wetenschappelijke-vm](./media/machine-learning-data-science-linux-dsvm-intro/configure-linux-data-science-virtual-machine.png)
3. Hallo uit te voeren bieden Hallo invoer voor elk van de stappen Hallo in Hallo wizard (opgesomd op Hallo rechts van de voorgaande afbeelding Hallo) toocreate Hallo Microsoft Data wetenschappelijke virtuele Machine gebruikt. Hier volgen Hallo invoer nodig tooconfigure elk van de volgende stappen:
   
   a. **Basisprincipes**:
   
   * **Naam**: naam van uw gegevens wetenschap-server die u maakt.
   * **Gebruikersnaam**: eerste account aanmelden ID.
   * **Wachtwoord**: eerste wachtwoord (u kunt openbare SSH-sleutel kunt gebruiken in plaats van wachtwoord).
   * **Abonnement**: als u meer dan één abonnement hebt, selecteer Hallo met een op welke Hallo machine toobe gemaakt en kosten in rekening gebracht. U moet bevoegdheden van de resource maken voor dit abonnement hebben.
   * **Resourcegroep**: U kunt een nieuwe maken of een bestaande groep.
   * **Locatie**: Selecteer Hallo datacenter die het meest geschikt is. Meestal is het Hallo-datacenter dat de meeste van uw gegevens en of dichtstbijzijnde tooyour fysieke locatie voor de snelste toegang tot het netwerk is.
   
   b. **De grootte van**:
   
   * Selecteer een van de servertypen Hallo dat voldoet aan uw functionele vereisten en kostenbeperkingen. Selecteer **Alles weergeven** toosee meer mogelijkheden van VM-formaten.
   
   c. **Instellingen**:
   
   * **Schijftype**: kies **Premium** als u liever een solid state schijf (SSD). Kies anders **standaard**.
   * **Storage-Account**: U kunt een nieuw Azure storage-account maken in uw abonnement of gebruik een bestaande in Hallo dezelfde locatie die u hebt gekozen op Hallo **basisbeginselen** stap van de wizard Hallo.
   * **Andere parameters**: In de meeste gevallen u zojuist hebt Hallo standaardwaarden gebruiken. tooconsider niet-standaard waarden, houd de muis boven Hallo informatief koppeling voor help bij Hallo specifieke velden.
   
   d. **Samenvatting**:
   
   * Controleer of alle informatie die u hebt ingevoerd juist is.
   
   e. **Kopen**:
   
   * toostart Hallo inrichten, klikt u op **kopen**. Een koppeling is toohello gebruiksvoorwaarden Hallo transactie opgegeven. Hallo VM beschikt niet over eventuele extra kosten buiten Hallo compute voor de grootte van de server Hallo u hebt gekozen in Hallo **grootte** stap.

Hallo inrichting duren ongeveer 10-20 minuten. Hallo-status van het Hallo-inrichting wordt weergegeven op Hallo Azure-portal.

## <a name="how-tooaccess-hello-linux-data-science-virtual-machine"></a>Hoe tooaccess Hallo Linux gegevens wetenschappelijke virtuele Machine
Na het Hallo die virtuele machine wordt gemaakt, kunt u tooit aanmelden met behulp van SSH. Hallo-accountreferenties die u hebt gemaakt in hello gebruiken **basisbeginselen** sectie van stap 3 voor Hallo tekst shell-interface. Op Windows, kunt u een SSH clienthulpprogramma zoals downloaden [Putty](http://www.putty.org). Als u liever een grafische bureaublad (X Windows-systeem), kunt u X11 doorsturen op Putty gebruiken of Hallo X2Go client installeren.

> [!NOTE]
> Hallo X2Go client uitgevoerd aanzienlijk beter dan X11 doorsturen in de testfase. U wordt aangeraden met Hallo X2Go client voor een grafische interface voor het bureaublad.
> 
> 

## <a name="installing-and-configuring-x2go-client"></a>Installeren en configureren van X2Go client
Hallo Linux VM is al voorzien met X2Go server en -klaar tooaccept clientverbindingen. tooconnect toohello grafische Linux VM-bureaublad Hallo op de client te volgen:

1. Download en installeer de client hello X2Go voor uw clientplatform van [X2Go](http://wiki.x2go.org/doku.php/doc:installation:x2goclient).    
2. Hallo X2Go-client wordt uitgevoerd en selecteer **nieuwe sessie**. Er verschijnt een configuratievenster met meerdere tabbladen. Voer Hallo configuratieparameters te volgen:
   * **Tabblad sessie**:
     * **Host**: Hallo-hostnaam of IP-adres van uw virtuele Linux-gegevens van wetenschappelijke machine.
     * **Aanmelding**: de gebruikersnaam op Hallo Linux VM.
     * **SSH-poort**: 22 Hallo standaardwaarde behoudt.
     * **Sessietype**: wijziging Hallo waarde tooXFCE. Hallo Linux VM ondersteunt momenteel alleen XFCE bureaublad.
   * **Tabblad Media**: U kunt uitschakelen geluid ondersteuning en de client als u geen toouse afdrukken ze.
   * **Gedeelde mappen**: als u mappen van uw clientcomputers op Hallo Linux VM gekoppeld wilt, Hallo client mappen op de computer die u tooshare Hello VM op dit tabblad wilt toevoegen.

Nadat u zich aanmeldt toohello virtuele machine met behulp van Hallo SSH-client of XFCE grafische bureaublad via Hallo X2Go client, bent u klaar toostart met Hallo-hulpprogramma's die zijn geïnstalleerd en geconfigureerd op Hallo VM. Op XFCE, kunt u toepassingen menu, snelkoppelingen en bureaubladpictogrammen bekijken voor een groot aantal Hallo-hulpprogramma's.

## <a name="tools-installed-on-hello-linux-data-science-virtual-machine"></a>Hulpprogramma's zijn geïnstalleerd op Hallo Linux gegevens wetenschappelijke virtuele Machine
### <a name="microsoft-r-server"></a>Microsoft R Server
R is een van de meest populaire talen Hallo voor data-analyse en machine learning. Als u toouse R voor uw analyses wilt, heeft Hallo VM Microsoft R Server (MEVR) Hello Microsoft R openen (BHT) en Math Kernel-bibliotheek (MKL). Hallo MKL optimaliseert rekenkundige bewerkingen gebruikelijk in analytische algoritmen. BHT is 100 procent compatibel is met CRAN R en een Hallo R-bibliotheken die zijn gepubliceerd in CRAN op Hallo BHT kan worden geïnstalleerd. MEVR biedt u schaalbaarheid en uitoefening van R-modellen in de web-services. U kunt uw R-programma's in een Hallo standaard editors, zoals RStudio, vi, Emacs of gedit bewerken. Als u Hallo Emacs editor, houd er rekening mee dat Hallo Emacs pakket eldingen ONDERDRUKKEN (Emacs spreekt statistieken), is die vereenvoudigt het werken met R-bestanden in Hallo Emacs editor, vooraf geïnstalleerd.

toolaunch R-console, typ **R** Hallo shell. Hiermee gaat u tooan interactieve omgeving. toodevelop uw programma R u doorgaans een editor zoals Emacs of vi of gedit gebruiken en voer vervolgens Hallo-scripts in R. Met RStudio hebt u een volledige grafische IDE omgeving toodevelop uw R-programma.

Er is ook een R-script voor u tooinstall hello [Top 20 R-pakketten](http://www.kdnuggets.com/2015/06/top-20-r-packages.html) als u wilt. Dit script kan worden uitgevoerd nadat u zich in de interactieve interface Hallo R, die kan worden ingevoerd (zoals vermeld) door te typen **R** Hallo shell.  

### <a name="python"></a>Python
Voor de ontwikkeling met behulp van Python, is distributie Anaconda Python 2.7 en 3.5 geïnstalleerd. Deze verdeling bevat Hallo baseren Python samen met ongeveer 300 Hallo populairste math, engineering en gegevens analytics pakketten. U kunt Hallo standaard teksteditors gebruiken. Bovendien kunt u Spyder, een Python IDE die wordt meegeleverd met Anaconda Python-distributies. Spyder moet een grafische bureaublad of X11 doorsturen. Een snelkoppeling tooSpyder wordt vermeld in de grafische Hallo-bureaublad.

Aangezien we Python 2.7 en 3.5 hebt, moet u toospecifically Hallo gewenst Python-versie (conda environment) dat u toowork op in Hallo huidige sessie wilt activeren. Hallo-activeringsproces stelt Hallo pad variabele toohello gewenste versie van Python.

tooactivate hello Python 2.7 conda omgeving, Hallo volgende uitvoeren via Hallo shell:

    source /anaconda/bin/activate root

Python 2.7 is geïnstalleerd op *anaconda/bin*.

tooactivate hello Python 3.5 conda omgeving, Hallo volgende uitvoeren via Hallo shell:

    source /anaconda/bin/activate py35


Python 3.5 is geïnstalleerd op */anaconda/envs/py35/bin*.

Typ tooinvoke een interactieve sessie Python, **python** Hallo shell. Als u X11 set bent doorgestuurd of zich op een grafische interface, typt u **pycharm** toolaunch hello PyCharm Python IDE.

tooinstall extra Python-bibliotheken, moet u toorun ```conda``` of ````pip```` opdracht onder sudo en het volledige pad van Hallo Python package manager (conda of pip) tooinstall toohello juiste Python-omgeving te geven. Bijvoorbeeld:

    sudo /anaconda/bin/pip install <package> #for Python 2.7 environment
    sudo /anaconda/envs/py35/bin/pip install <package> # for Python 3.5 environment


### <a name="jupyter-notebook"></a>Jupyter-notebook
Hallo Anaconda-verdeling wordt ook geleverd met een Jupyter-notebook, een omgeving tooshare code en analyse. Hallo Jupyter-notebook toegankelijk is via JupyterHub. U kunt aanmelden met uw lokale Linux-gebruikersnaam en wachtwoord.

Hallo Jupyter-notebook server is vooraf geconfigureerd met Python 2, 3 Python en R kernels. Er is een pictogram op het bureaublad met de naam 'Jupyter-Notebook' toolaunch Hallo browser tooaccess Hallo notebook server. Als u van Hallo VM via SSH of X2Go-client gebruikmaakt, kunt u ook bezoeken [https://localhost:8000 /](https://localhost:8000/) tooaccess Hallo Jupyter-notebook server.

> [!NOTE]
> Doorgaan als u certificaatwaarschuwingen.
> 
> 

U kunt Hallo Jupyter-notebook server openen vanaf een willekeurige host. Typ *https://\<VM DNS-naam of IP-adres\>: 8000 /*

> [!NOTE]
> Poort 8000 wordt geopend in de firewall Hallo standaard wanneer Hallo VM is ingericht.
> 
> 

We hebben verpakt voorbeeldquery notitieblokken--één in Python en één in R. Nadat u de Jupyter-notebook toohello verifiëren met behulp van uw lokale Linux-gebruikersnaam en wachtwoord, kunt u op Hallo notebook startpagina Hallo koppeling toohello voorbeelden zien. U kunt een nieuwe notebook maken door het selecteren van **nieuw**, en vervolgens Hallo relevante taal kernel. Als er geen Hallo **nieuw** knop, klikt u op Hallo **Jupyter** pictogram op Hallo bovenste links toogo toohello startpagina van Hallo notebook server.

### <a name="apache-spark-standalone"></a>Apache Spark zelfstandige 
Een zelfstandig exemplaar van Apache Spark is voorgeïnstalleerd op Hallo Linux DSVM toohelp u eerst lokaal Spark scala-toepassingen ontwikkelen voordat u gaat testen en implementeren op grote clusters. U kunt PySpark-programma's uitvoeren via Hallo Jupyter kernel. Wanneer u Jupyter openen en klik op de knop 'Nieuw' hello ziet u een lijst met beschikbare kernels. Hallo 'Spark--Python' is hello PySpark-kernel waarmee u Spark toepassingen bouwen met Python taal. U kunt ook een Python IDE zoals PyCharm of Spyder toobuild u Spark programma. Aangezien dit een zelfstandig exemplaar is, Hallo Spark stack binnen Hallo aanroepen clientprogramma wordt uitgevoerd. Hierdoor kunt u sneller en eenvoudiger tootroubleshoot problemen vergeleken toodeveloping op een Spark-cluster. 

Een voorbeeld PySpark-notebook is beschikbaar op Jupyter die u in Hallo 'SparkML' map onder de basismap Hallo van Jupyter ($HOME/notitieblokken/SparkML/pySpark vinden kunt). 

Als u in R voor Spark programmeert, kunt u Microsoft R Server SparkR of sparklyr gebruiken. 

Voordat u deze uitvoert in de context voor Spark in Microsoft R Server, moet u toodo een één keer setup stap tooenable lokale één knooppunt Hadoop HDFS en Yarn-instantie. Hadoop-services zijn standaard geïnstalleerd maar op Hallo DSVM uitgeschakeld. In volgorde tooenable, moet u toorun Hallo volgende opdrachten als hoofdmap Hallo eerst:

    echo -e 'y\n' | ssh-keygen -t rsa -P '' -f ~hadoop/.ssh/id_rsa
    cat ~hadoop/.ssh/id_rsa.pub >> ~hadoop/.ssh/authorized_keys
    chmod 0600 ~hadoop/.ssh/authorized_keys
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa.pub
    chown hadoop:hadoop ~hadoop/.ssh/authorized_keys
    systemctl start hadoop-namenode hadoop-datanode hadoop-yarn

U kunt stoppen Hallo Hadoop gerelateerde services wanneer u hoeft ze niet door het uitvoeren van ````systemctl stop hadoop-namenode hadoop-datanode hadoop-yarn```` een voorbeeld van een aan te tonen hoe toodevelop en test MEVR in externe Spark-context (die Hallo zelfstandige Spark-exemplaar op Hallo DSVM) is opgegeven en beschikbaar zijn in Hallo `/dsvm/samples/MRS` directory. 

### <a name="ides-and-editors"></a>IDE en editors
U hebt een keuze uit verschillende code-editors. Dit omvat vi/VIM, Emacs, gEdit, PyCharm, RStudio, Eclipse en IntelliJ. gEdit, Eclipse, IntelliJ, RStudio en PyCharm grafische editors zijn en moet u toobe aangemeld tooa grafische bureaublad toouse ze. Deze editors hebben desktop- en menu Snelkoppelingen toolaunch ze.

**VIM** en **Emacs** editors op basis van tekst zijn. Op Emacs, hebben we een invoegtoepassing pakket aangeroepen Emacs spreekt statistieken (eldingen ONDERDRUKKEN) die werken met R gemakkelijker binnen Hallo Emacs editor geïnstalleerd. Meer informatie kunt vinden op [eldingen ONDERDRUKKEN](http://ess.r-project.org/).

**Eclipse** is een open source, uitbreidbare IDE die ondersteuning biedt voor meerdere talen. Hallo Java ontwikkelaars edition is Hallo-exemplaar op Hallo VM geïnstalleerd. Er zijn invoegtoepassingen beschikbaar zijn voor verschillende veelgebruikte talen die geïnstalleerd tooextend Hallo-omgeving worden kunnen. We hebben ook een invoegtoepassing is geïnstalleerd in Eclipse aangeroepen **Azure Toolkit voor Eclipse**. Hiermee kunt u toocreate, ontwikkelen, testen en implementeren van Azure met behulp van Hallo Eclipse-ontwikkelomgeving die ondersteuning biedt voor talen zoals Java-toepassingen. Er is ook een **Azure SDK voor Java** waarmee toegang toodifferent Azure-services uit binnen een Java-omgeving. Meer informatie over Azure toolkit voor Eclipse kan worden gevonden op [Azure Toolkit voor Eclipse](../azure-toolkit-for-eclipse.md).

**LaTex** wordt geïnstalleerd via Hallo texlive pakket samen met een invoegtoepassing Emacs [auctex](https://www.gnu.org/software/auctex/manual/auctex/auctex.html) , dit vereenvoudigt het ontwerpen van uw documenten LaTex binnen Emacs pakket.  

### <a name="databases"></a>Databases
#### <a name="postgres"></a>Postgres
Hallo open-source database **Postgres** beschikbaar is op Hallo VM, met Hallo services die worden uitgevoerd en initdb al is voltooid. U moet nog steeds toocreate databases en gebruikers. Zie voor meer informatie, Hallo [Postgres documentatie](https://www.postgresql.org/docs/).  

#### <a name="graphical-sql-client"></a>Grafische SQL-client
**SQuirrel SQL**, een grafische SQL-client is opgegeven tooconnect toodifferent databases (zoals Microsoft SQL Server, Postgres en MySQL) en toorun SQL-query's. U kunt dit uitvoeren vanaf een grafische bureaublad-sessiehost (Hallo X2Go client, bijvoorbeeld met). tooinvoke SQuirrel SQL, kunt u deze starten vanuit het Hallo-pictogram op Hallo bureaublad of Hallo volgende opdracht op Hallo shell uitvoeren.

    /usr/local/squirrel-sql-3.7/squirrel-sql.sh

Voordat Hallo het eerst gebruikt, stelt u de stuurprogramma's en de database-aliassen. Hallo JDBC-stuurprogramma's bevinden zich op:

*/usr/share/Java/jdbcdrivers*

Zie voor meer informatie [SQuirrel SQL](http://squirrel-sql.sourceforge.net/index.php?page=screenshots).

#### <a name="command-line-tools-for-accessing-microsoft-sql-server"></a>Opdrachtregelprogramma's voor toegang tot Microsoft SQL Server
Hallo ODBC-stuurprogramma voor massaopslagapparaten voor SQL Server wordt ook geleverd met twee opdrachtregelprogramma's:

**BCP**: Hallo bcp hulpprogramma bulksgewijs gegevens tussen een exemplaar van Microsoft SQL Server en een gegevensbestand in een door de gebruiker opgegeven indeling kopieert. Hallo bcp-hulpprogramma kan worden grote aantallen gebruikte tooimport van nieuwe rijen in SQL Server-tabellen of tooexport gegevens buiten de tabellen in gegevensbestanden. tooimport gegevens in een tabel, u moet ofwel bestand-indeling gemaakt voor die tabel of Hallo-structuur van Hallo tabel en Hallo typen gegevens die geldig voor de kolommen zijn begrijpen.

Zie voor meer informatie [verbinding te maken met bcp](https://msdn.microsoft.com/library/hh568446.aspx).

**Sqlcmd**: kunt u het invoeren van Transact-SQL-instructies met Hallo sqlcmd-hulpprogramma, evenals de procedures van systeem en scriptbestanden achter de opdrachtprompt Hallo. Dit hulpprogramma maakt gebruik van ODBC-tooexecute Transact-SQL-batches.

Zie voor meer informatie [verbinding te maken met sqlcmd](https://msdn.microsoft.com/library/hh568447.aspx).

> [!NOTE]
> Er zijn bepaalde verschillen in dit hulpprogramma tussen Linux- en Windows-platforms. Zie Hallo-documentatie voor meer informatie.
> 
> 

#### <a name="database-access-libraries"></a>Database toegang bibliotheken
Er zijn bibliotheken beschikbaar in R- en Python tooaccess-databases.

* Hallo in R, **RODBC** pakket of **dplyr** pakket kunt u tooquery of SQL-instructies op de databaseserver Hallo uitvoeren.
* Hallo in Python, **pyodbc** -bibliotheek biedt toegang tot de database met behulp van ODBC zoals Hallo onderliggende laag.  

tooaccess **Postgres**:

* Van R: Gebruik Hallo pakket **RPostgreSQL**.
* Met Python: Gebruik Hallo **psycopg2** bibliotheek.

### <a name="azure-tools"></a>Azure-hulpprogramma 's
Hallo volgende Azure-hulpprogramma's zijn geïnstalleerd op Hallo VM:

* **Azure-opdrachtregelinterface**: hello Azure CLI kunt u toocreate en beheren van Azure-resources via de shell-opdrachten. tooinvoke Hallo Azure-hulpprogramma's, typt u **azure help**. Zie voor meer informatie, Hallo [documentatiepagina voor Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* **Microsoft Azure Storage Explorer**: Microsoft Azure Storage Explorer is een grafisch hulpprogramma dat is gebruikt toobrowse via Hallo-objecten die u hebt opgeslagen in uw Azure storage-account en tooupload en downloaden gegevens tooand uit Azure blobs. U kunt een Opslagverkenner openen vanaf Hallo snelkoppeling op het bureaublad pictogram. U kunt het aanroepen van een shell-prompt door **StorageExplorer**. U moet aangemeld vanaf een client X2Go toobe of X11 set up doorgestuurd hebben.
* **Azure-bibliotheken**: Hallo hieronder staan enkele van de vooraf geïnstalleerde Hallo-bibliotheken.
  
  * **Python**: hello Azure-bibliotheken in Python die zijn geïnstalleerd zijn **azure**, **azureml**, **pydocumentdb**, en **pyodbc** . Hallo met de eerste drie bibliotheken, kunt u toegang tot Azure storage-services, Azure Machine Learning en Azure Cosmos-DB (een NoSQL-database in Azure). Hallo vierde bibliotheek pyodbc (samen met de Hallo ODBC-stuurprogramma voor SQL Server), kunt access tooSQL Server, Azure SQL Database en Azure SQL Data Warehouse met Python met behulp van een ODBC-interface. Voer **pip lijst** toosee alle Hallo bibliotheken weergegeven. Ervoor toorun worden met deze opdracht in beide Hallo Python 2.7 en 3.5 omgevingen.
  * **R**: hello Azure-gerelateerde-bibliotheken in R die zijn geïnstalleerd **AzureML** en **RODBC**.
  * **Java**: Hallo lijst met Azure Java bibliotheken vindt u in de directory Hallo **/dsvm/sdk/AzureSDKJava** op Hallo VM. Hallo sleutel bibliotheken zijn Azure opslag en beheer-API's, Azure Cosmos DB en JDBC-stuurprogramma's voor SQL Server.  

U hebt toegang tot Hallo [Azure-portal](https://portal.azure.com) van Hallo vooraf geïnstalleerde Firefox-browser. Op Hallo Azure-portal, kunt u maken, beheren en bewaken van de Azure-resources.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning is een volledig beheerde cloudservice waarmee u toobuild, implementeren en delen van predictive analytics-oplossingen. U maken uw experimenten en modellen van Azure Machine Learning Studio. Deze toegankelijk is vanuit een webbrowser op Hallo gegevens wetenschappelijke virtuele machine in via [Microsoft Azure Machine Learning](https://studio.azureml.net).

Als u zich aanmeldt tooAzure Machine Learning Studio, hebt u toegang tooan experimenteren canvas waar kunt u een logische stroom voor Hallo machine learning-algoritmen. U ook hebt toegang tooa Jupyter-notebook gehost op Azure Machine Learning en werkt naadloos samen met de Hallo experimenten in Machine Learning Studio. Operationeel Hallo machine learning-modellen die u hebt gemaakt door ze in een webservice-interface. Hierdoor kunnen clients die zijn geschreven in elke taal tooinvoke voorspellingen van Hallo machine learning-modellen. Zie voor meer informatie, Hallo [Machine Learning-documentatie](https://azure.microsoft.com/documentation/services/machine-learning/).

U kunt ook uw modellen in R- of Python op Hallo VM maken en vervolgens te implementeren in productie in Azure Machine Learning. We bibliotheken hebt geïnstalleerd in R (**AzureML**) en Python (**azureml**) tooenable deze functionaliteit.

Zie voor informatie over hoe toodeploy in R- en Python in Azure Machine Learning modellen, [tien dingen die u op de virtuele Machine voor gegevenswetenschap hello doen kunt](machine-learning-data-science-vm-do-ten-things.md) (met name Hallo sectie ' bouwen van modellen met R- of Python en ze operationeel maken met behulp van Azure Machine Learning').

> [!NOTE]
> Deze instructies zijn geschreven voor Windows-versie Hallo Hallo gegevens wetenschappelijke VM. Maar Hallo informatie bevat over het implementeren van modellen tooAzure Machine Learning is van toepassing toohello Linux VM.
> 
> 

### <a name="machine-learning-tools"></a>Machine learning-hulpprogramma 's
Hallo VM wordt geleverd met een paar machine learning-hulpprogramma's en -algoritmen die zijn vooraf gecompileerd en vooraf lokaal worden geïnstalleerd. Deze omvatten:

* **CNTK** (rekenkundige netwerk Toolkit van Microsoft Research): een diepe learning-toolkit.
* **Vowpal Wabbit**: een leeralgoritme snelle online.
* **xgboost**: een hulpprogramma waarmee geoptimaliseerde, gestimuleerd structuur algoritmen.
* **Python**: Anaconda Python wordt geleverd met machine learning-algoritmen met bibliotheken zoals Scikit meer. U kunt andere bibliotheken installeren met behulp van Hallo `pip install` opdracht.
* **R**: een uitgebreide bibliotheek met machine learning-functies is beschikbaar voor R. Sommige Hallo-bibliotheken die vooraf zijn geïnstalleerd zijn lm, glm, randomForest, rpart. Andere bibliotheken kunnen worden geïnstalleerd door te voeren:
  
        install.packages(<lib name>)

Hier is een aantal aanvullende informatie over Hallo eerst drie machine learning-hulpprogramma's in de lijst Hallo.

#### <a name="cntk"></a>CNTK
Dit is een open-source, grondige learning-toolkit. Er is een opdrachtregelprogramma (cntk) en is al in Hallo pad.

toorun een eenvoudige voorbeeld uitvoeren Hallo opdrachten in Hallo shell te volgen:

    cd /home/[USERNAME]/notebooks/CNTK/HelloWorld-LogisticRegression
    cntk configFile=lr_bs.cntk makeMode=false command=Train

Zie voor meer informatie sectie CNTK van Hallo [GitHub](https://github.com/Microsoft/CNTK), en Hallo [CNTK wiki](https://github.com/Microsoft/CNTK/wiki).

#### <a name="vowpal-wabbit"></a>Vowpal Wabbit
Vowpal Wabbit is een machine learning-besturingssysteem dat gebruikmaakt van technieken zoals online, hash, allreduce, kortingen, learning2search, actief, en interactieve daarvan te leren.

toorun hello hulpprogramma op een zeer eenvoudige bijvoorbeeld Hallo te volgen:

    cp -r /dsvm/tools/VowpalWabbit/demo vwdemo
    cd vwdemo
    vw house_dataset

Er zijn andere, groter demo's in die map. Zie voor meer informatie over een code [in deze sectie van GitHub](https://github.com/JohnLangford/vowpal_wabbit), en Hallo [Vowpal Wabbit wiki](https://github.com/JohnLangford/vowpal_wabbit/wiki).

#### <a name="xgboost"></a>xgboost
Dit is een tapewisselaar die is ontworpen en geoptimaliseerd voor algoritmen gestimuleerd (structuur). Hallo-doel van deze bibliotheek is toopush Hallo berekening grenzen van de machines toohello uiterste nodig tooprovide grootschalige structuur versterking die schaalbare, draagbare en juist is.

Als een opdrachtregel, evenals een R-bibliotheek is opgegeven.

toouse deze bibliotheek in R, kunt u een interactieve R-sessie starten (eenvoudigweg te typen **R** Hallo Shell), en load Hallo-bibliotheek.

Dit is een eenvoudig voorbeeld die kunt u in R prompt uitvoeren:

    library(xgboost)

    data(agaricus.train, package='xgboost')
    data(agaricus.test, package='xgboost')
    train <- agaricus.train
    test <- agaricus.test
    bst <- xgboost(data = train$data, label = train$label, max.depth = 2,
                    eta = 1, nthread = 2, nround = 2, objective = "binary:logistic")
    pred <- predict(bst, test$data)

toorun hello xgboost opdrachtregel zijn hier Hallo opdrachten tooexecute Hallo shell:

    cp -r /dsvm/tools/xgboost/demo/binary_classification/ xgboostdemo
    cd xgboostdemo
    xgboost mushroom.conf


Een bestand .model wordt opgegeven toohello-map geschreven. Informatie over dit voorbeeld demo vindt [op GitHub](https://github.com/dmlc/xgboost/tree/master/demo/binary_classification).

Zie voor meer informatie over xgboost hello [xgboost documentatiepagina](https://xgboost.readthedocs.org/en/latest/), en de bijbehorende [GitHub-opslagplaats](https://github.com/dmlc/xgboost).

#### <a name="rattle"></a>Rammelaar
Rattle (Hallo **R** **A**nalytical **T**lpmiddel **T**o **L**verdienen **E** asily) maakt gebruik van GUI gebaseerde gegevensverkenning en modellering. Deze geeft statistische en visual overzichten van gegevens, transformaties gegevens die gemakkelijk kan worden gemodelleerd, bouwt zonder supervisie en onder supervisie modellen van Hallo gegevens, geeft Hallo prestaties van modellen grafisch en nieuwe gegevens scores ingesteld. Er wordt ook gegenereerd R-code, repliceren Hallo-bewerkingen in Hallo gebruikersinterface die kunnen worden rechtstreeks in R uitvoeren of als uitgangspunt gebruikt voor verdere analyse.

toorun Rammelaar, moet u toobe in een grafische aanmelden bureaubladsessie. Typ op Hallo terminal ```R``` tooenter Hallo R-omgeving. Voer bij Hallo R-prompt Hallo volgende opdrachten:

    library(rattle)
    rattle()

Nu een grafische interface wordt geopend met een reeks tabbladen. Hier volgen Hallo snel starten stappen in Rammelaar nodig toouse een verzameling voorbeeldgegevens weer en bouwen van een model. In sommige Hallo onderstaande stappen zijn tooautomatically na vragen aan gebruiker installeren en laden van bepaalde vereiste R-pakketten die nog niet op Hallo-systeem.

> [!NOTE]
> Als u geen toegang tooinstall Hallo pakket in de map van het systeem hello (Hallo standaard), ziet u mogelijk een prompt op uw R-console venster tooinstall pakketten tooyour persoonlijke bibliotheek. Antwoord *y* als u deze aanwijzingen ziet.
> 
> 

1. Klik op **Uitvoeren**.
2. Een dialoogvenster weergegeven waarin u wordt gevraagd als u toouse Hallo weer voorbeeldgegevensset zoals. Klik op **Ja** tooload Hallo voorbeeld.
3. Klik op Hallo **Model** tabblad.
4. Klik op **Execute** toobuild een beslissingsstructuur.
5. Klik op **tekenen** toodisplay Hallo beslissingsstructuur.
6. Klik op Hallo **Forest** keuzerondje en klikt u op **Execute** toobuild een willekeurige forest.
7. Klik op Hallo **Evaluate** tabblad.
8. Klik op Hallo **risico** keuzerondje en klikt u op **Execute** toodisplay twee risico (cumulatief) prestaties waarnemingspunten.
9. Klik op Hallo **logboek** tabblad tooshow Hallo R code genereren voor Hallo voorafgaand aan activiteiten.
   (Vanwege tooa fout in de huidige release Hallo van Rammelaar, moet u tooinsert een  *#*  teken vóór *... dit logboek exporteren*  in de tekst hello van Hallo logboek.)
10. Klik op Hallo **exporteren** knop toosave Hallo R-scriptbestand met de naam *weather_script. R* toohello basismap.

U kunt afsluiten Rammelaar en R. Nu kunt u Hallo gegenereerd R-script wijzigen of ongewijzigd toorun gebruiken deze op elk gewenst moment toorepeat alles wat u binnen Hallo Rattle gebruikersinterface werd uitgevoerd. Dit is een eenvoudige manier tooquickly analyse en machine learning in een eenvoudige grafische interface tijdens het automatisch genereren van code in R toomodify en/of meer met name voor beginnende gebruikers in R.

## <a name="next-steps"></a>Volgende stappen
Hier ziet u hoe u kunt blijven uw leren en te verkennen:

* Hallo [gegevenswetenschap op Hallo Linux gegevens wetenschappelijke virtuele Machine](machine-learning-data-science-linux-dsvm-walkthrough.md) overzicht toont u hoe tooperform enkele algemene gegevenswetenschap taken Hello Linux gegevens wetenschappelijke VM hier ingericht. 
* Verken Hallo verschillende hulpmiddelen voor gegevens wetenschappelijke op Hallo gegevenswetenschap VM door het Hallo-hulpprogramma's beschreven in dit artikel uitprobeert. U kunt ook uitvoeren *dsvm meer gegevens* op Hallo shell binnen Hallo virtuele machine voor een algemene inleiding en aanwijzers toomore informatie over Hallo-hulpprogramma's geïnstalleerd op Hallo VM.  
* Meer informatie over hoe toobuild end-to-end-analyseoplossingen systematischer met behulp van Hallo [Team gegevens wetenschap proces](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).
* Ga naar Hallo [Cortana-Analytics galerie](http://gallery.cortanaanalytics.com) voor machine learning en analytics die gebruik Hallo Cortana-Analytics Suite voorbeelden.

