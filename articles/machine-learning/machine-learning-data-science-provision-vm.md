---
title: aaaProvision hello Microsoft Data wetenschappelijke Virtual Machine | Microsoft Docs
description: Configureren en een virtuele Machine van de gegevens wetenschappelijke in Azure maken voor analytics en machine learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 907a3bdc7e480d05e8e245f5e50d632900fcf471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-microsoft-data-science-virtual-machine"></a>Hallo Microsoft Data wetenschappelijke Virtual Machine inrichten
Hallo Microsoft Data wetenschappelijke virtuele Machine is een Windows Azure virtuele machine (VM) vooraf is geïnstalleerd en geconfigureerd met verschillende populaire hulpprogramma's die vaak worden gebruikt voor gegevensanalyse en machine learning. Hallo-hulpprogramma's zijn:

* Microsoft R Server Developer Edition
* Anaconda Python-distributie
* Jupyter-notebook (met R, Python kernels)
* Visual Studio Community Edition
* Power BI Desktop
* Developer Edition van SQL Server 2016
* Machine learning en hulpprogramma's voor gegevensanalyse
  * [Rekenkundige netwerk Toolkit (CNTK)](https://github.com/Microsoft/CNTK): een diepe learning toolkit software van Microsoft Research.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): een snel machine learning-technieken zoals online, hash, allreduce, kortingen, learning2search, actief, ondersteunende system en interactieve daarvan te leren.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): een hulpprogramma dat snelle en nauwkeurige gestimuleerd structuur-implementatie.
  * [Rattle](http://rattle.togaware.com/) (R analytische hulpprogramma tooLearn eenvoudig hello): een hulpprogramma dat aan de slag met data analytics en machine learning in R eenvoudig met een GUI-gebaseerde gegevensverkenning en modellering met automatische R codegeneratie maakt.
  * [mxnet](https://github.com/dmlc/mxnet): een grondige learning framework ontworpen voor zowel efficiëntie en flexibiliteit
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/) : een visual gegevensanalyse en machine learning-software in Java.
  * [Apache inzoomen](https://drill.apache.org/): een schemavrije SQL Query-Engine voor Hadoop, NoSQL- en Cloud-opslag.  Biedt ondersteuning voor ODBC en JDBC interfaces tooenable NoSQL en bestanden van de standaard BI-tools zoals Power BI, Excel, Tableau opvragen.
* Bibliotheken in R- en Python voor gebruik in Azure Machine Learning en andere Azure-services
* GIT, met inbegrip van Git Bash toowork met broncodeopslagplaatsen, met inbegrip van GitHub, Visual Studio Team Services
* Windows-poorten van verschillende populaire Linux opdrachtregelprogramma's (inclusief awk, ype, perl, grep, zoeken, wget, curl enzovoort) toegankelijk zijn via de opdrachtprompt. 

Tijdens het doorzoeken van wetenschappelijke gegevens omvat sequentieel op een reeks taken:

1. Zoeken, laden en vooraf verwerken van gegevens
2. Maken en testen van modellen
3. Hallo-modellen voor verbruik in intelligente toepassingen implementeren

Gegevenswetenschappers gebruiken een groot aantal toocomplete in hulpprogramma's voor deze taken. Deze kan worden heel veel tijd in beslag toofind Hallo juiste softwareversies hello, en vervolgens downloaden en te installeren. Hallo Microsoft Data wetenschappelijke virtuele Machine kan deze last vereenvoudigen doordat een kant-en-klare-installatiekopie die kan worden ingericht op Azure met alle verschillende populaire hulpmiddelen vooraf is geïnstalleerd en geconfigureerd. 

Hallo Microsoft Data wetenschappelijke Virtual Machine jump-starts uw project analytics. Hiermee kunt u toowork op taken in verschillende talen, waaronder R, Python, SQL en C#. Visual Studio biedt een IDE-toodevelop en testen van uw code die eenvoudig toouse is. Hello Azure SDK is opgenomen in Hallo VM kunt u toobuild uw toepassingen met behulp van verschillende services op Microsoft cloud-platform. 

Er zijn geen kosten voor software voor deze gegevens wetenschappelijke VM-installatiekopie. U betaalt alleen voor hello Azure gebruikskosten welke die afhankelijk zijn van de grootte van de Hallo van Hallo virtuele machine die u inricht. Meer informatie over Hallo compute kosten vindt u in de detailsectie op Hallo Hallo [gegevens wetenschappelijke virtuele Machine](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) pagina. 

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Andere versies van Hallo gegevens wetenschappelijke virtuele Machine
Een [CentOS](machine-learning-data-science-linux-dsvm-intro.md) installatiekopie ook beschikbaar is, met veel Hallo dezelfde als de installatiekopie van Windows hello tools. Een [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) installatiekopie is beschikbaar, evenals met veel vergelijkbare extra plus deep frameworks leren.

## <a name="prerequisites"></a>Vereisten
Voordat u een Microsoft Data wetenschappelijke virtuele Machine maken kunt, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**: één, Zie tooobtain [gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Een Azure storage-account**: één, Zie toocreate [maken van een Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account). Hallo-opslagaccount kan ook worden gemaakt als onderdeel van het Hallo-proces voor het Hallo VM maken als u niet dat een bestaand account toouse wilt.

## <a name="create-your-microsoft-data-science-virtual-machine"></a>Uw Microsoft Data wetenschappelijke virtuele Machine maken
Hier volgen een exemplaar van Microsoft Data wetenschappelijke Virtual Machine Hallo Hallo stappen toocreate:

1. Navigeer toohello virtuele machine op aanbieding [Azure-portal](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).
2. Selecteer Hallo **maken** knop Hallo onder toobe in een wizard genomen.![ Configureer-gegevens-wetenschappelijke-vm](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. Hallo wizard gebruikt toocreate Hallo Microsoft Data wetenschappelijke virtuele Machine vereist **invoer** voor elk Hallo **vijf stappen** opgesomd op Hallo rechts van de volgende afbeelding. Hier volgen Hallo invoer nodig tooconfigure elk van de volgende stappen:
   
   1. **Basisinstellingen**
      
      1. **Naam**: naam van uw gegevens wetenschap-server die u maakt.
      2. **Gebruikersnaam**: Admin-account aanmeldings-id.
      3. **Wachtwoord**: wachtwoord van de beheerder.
      4. **Abonnement**: als u meer dan één abonnement hebt, selecteer Hallo met een op welke Hallo machine toobe gemaakt en kosten in rekening gebracht.
      5. **Resourcegroep**: U kunt een nieuwe maken of een bestaande groep.
      6. **Locatie**: Selecteer Hallo datacenter die het meest geschikt is. Meestal is het Hallo-datacenter die dichtstbijzijnde tooyour fysieke locatie voor de snelste toegang tot het netwerk of heeft de meeste van uw gegevens.
   2. **De grootte van**: Selecteer een van de servertypen Hallo dat voldoet aan uw functionele vereisten en kostenbeperkingen. U kunt meer mogelijkheden van VM-formaten ophalen door 'Alles weergeven' selecteren.
   3. **Instellingen**:
      
      1. **Schijftype**: Premium kiezen als u liever een SSD-station (SSD), anders selecteert 'Standaard'.
      2. **Storage-Account**: U kunt een nieuwe Azure storage-account maken in uw abonnement of gebruik een bestaande in Hallo dezelfde *locatie* die is gekozen op Hallo **basisbeginselen** stap van de wizard Hallo.
      3. **Andere parameters**: meestal net u Hallo standaardwaarden. U kunt de muisaanwijzer op Hallo informatief koppeling voor meer informatie over specifieke velden Hallo als u wilt dat tooconsider Hallo gebruik van niet-standaard waarden.
   4. **Samenvatting**: Controleer of alle informatie die u hebt ingevoerd juist is.
   5. **Kopen**: klik op **kopen** toostart Hallo inrichten. Een koppeling is toohello gebruiksvoorwaarden Hallo transactie opgegeven. Hallo VM beschikt niet over eventuele extra kosten buiten Hallo compute voor de grootte van de server Hallo u hebt gekozen in Hallo **grootte** stap. 

> [!NOTE]
> Hallo inrichting duren ongeveer 10-20 minuten. Hallo-status van het Hallo-inrichting wordt weergegeven op Hallo Azure-portal.
> 
> 

## <a name="how-tooaccess-hello-microsoft-data-science-virtual-machine"></a>Hoe tooaccess Hallo Microsoft Data wetenschappelijke virtuele Machine
Eenmaal Hallo virtuele machine wordt gemaakt, kunt u extern bureaublad in met behulp van de accountreferenties op Hallo beheerder die u hebt geconfigureerd in de voorgaande Hallo **basisbeginselen** sectie. 

Als uw virtuele machine is gemaakt en ingericht, bent u klaar toostart met Hallo-hulpprogramma's die zijn geïnstalleerd en geconfigureerd op deze. Er zijn start menu tegels en bureaubladpictogrammen voor een groot aantal Hallo-hulpprogramma's. 

## <a name="how-toocreate-a-strong-password-for-jupyter-and-start-hello-notebook-server"></a>Hoe een sterk wachtwoord voor Jupyter en begin toocreate Hallo notebook server
Standaard Hallo Jupyter-notebook server vooraf geconfigureerde maar uitgeschakeld op Hallo VM totdat u een Jupyter-wachtwoord instellen. een sterk wachtwoord voor Hallo Jupyter-notebook server zijn geïnstalleerd op machine Hallo toocreate, Voer Hallo volgende opdracht vanaf een opdrachtprompt op Hallo gegevens wetenschappelijke virtuele Machine of dubbelklik op de bureaubladsnelkoppeling Hallo bieden wij aangeroepen  **Wachtwoord voor instellen van Jupyter & Start** van een lokale administrator-account van VM.

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

Ga als volgt Hallo-berichten en kiest u een sterk wachtwoord wanneer u wordt gevraagd.

Hallo voorgaande script maakt een hash van het wachtwoord en de store in Hallo Jupyter-configuratiebestand zich bevindt op: **C:\ProgramData\jupyter\jupyter_notebook_config.py** onder de naam van de parameter Hallo ***c. NotebookApp.password***.

Hallo script kan ook en Hallo Jupyter-server op Hallo achtergrond worden uitgevoerd. Jupyter-server is gemaakt als een taak van windows hello WIndows Taakplanner genoemd **Start_IPython_Notebook**.  Mogelijk hebt u toowait enkele seconden na het Hallo-wachtwoord instellen voordat het Hallo-notebook in uw browser te openen. Hallo gedeelte hieronder Zie **Jupyter-Notebook** op hoe tooaccess Hallo Jupyter-notebook server. 


## <a name="tools-installed-on-hello-microsoft-data-science-virtual-machine"></a>Hulpprogramma's zijn geïnstalleerd op Hallo Microsoft Data wetenschappelijke virtuele Machine

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Developer Edition
Als u toouse R voor uw analyses wenst, heeft Hallo VM Microsoft R Server Developer edition is geïnstalleerd. Microsoft R Server is een grotendeels implementeerbare bedrijfsniveau analytics platform op basis van R die wordt ondersteund, schaalbare en veilige. Ondersteuning biedt voor tal van big data-statistieken, voorspellende modellen en machine learning-mogelijkheden, ondersteunt R Server Hallo volledige reeks analytics – exploratie, analyse, visualisatie en modellering. Door en open-source R uitbreiden, is Microsoft R Server volledig compatibel is met het R-scripts, functies en CRAN pakketten, tooanalyze gegevens op grote schaal enterprise. Biedt ook een oplossing Hallo in het geheugen beperkingen van de Open Source R door toe te voegen parallelle en gesegmenteerde verwerking van gegevens. Hiermee kunt u analytics toorun op gegevens die veel groter dan wat in het hoofdgeheugen past.  Visual Studio Community Edition opgenomen op Hallo die VM Hallo R-Tools voor Visual Studio-extensie die een volledige IDE biedt bevat voor het werken met R. U kunt ook downloaden en gebruiken van andere IDE ook zoals [RStudio](http://www.rstudio.com). 

### <a name="python"></a>Python
Voor de ontwikkeling met behulp van Python, is distributie Anaconda Python 2.7 en 3.5 geïnstalleerd. Deze verdeling bevat Hallo baseren Python samen met ongeveer 300 Hallo populairste math, engineering en gegevens analytics pakketten. U kunt Python-Tools voor Visual Studio (PTVS) die is geïnstalleerd binnen Hallo Visual Studio 2015 Community edition of een van de Hallo die IDE gebundeld met Anaconda zoals niet-actief of Spyder gebruiken. U kunt een van deze door te zoeken op Hallo zoekbalk starten (**Win** + **S** sleutel).

> [!NOTE]
> toopoint hello Python-Tools voor Visual Studio op Anaconda Python 2.7 en 3.5, moet u toocreate aangepaste omgevingen voor elke versie. tooset deze paden omgeving in Visual Studio 2015 Community Edition Hallo Navigeer te**extra** -> **Python Tools** -> **Python-omgevingen** en klik vervolgens op **+ aangepaste**. 
> 
> 

Anaconda Python 2.7 onder C:\Anaconda is geïnstalleerd en Anaconda Python 3.5 onder c:\Anaconda\envs\py35 is geïnstalleerd. Zie [documentatie bij PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) voor gedetailleerde stappen. 

### <a name="jupyter-notebook"></a>Jupyter Notebook
Anaconda-verdeling wordt ook geleverd met een Jupyter-notebook, een omgeving tooshare code en analyse. Een Jupyter-notebook-server is vooraf is geconfigureerd met Python 2.7, Python 3.4 Python 3.5 en R kernels. Er is een pictogram op het bureaublad met de naam "Jupyter-Notebook toolaunch Hallo browser tooaccess hello Notebook-server. Als u op Hallo VM via Extern bureaublad bent, kunt u ook bezoeken [https://localhost:9999 /](https://localhost:9999/) tooaccess Hallo Jupyter-notebook server wanneer toohello VM aangemeld.

> [!NOTE]
> Doorgaan als u certificaatwaarschuwingen. 
> 
> 

We hebben verschillende voorbeeldquery notitieblokken in Python verpakt en Hallo in R. Jupyter-notitieblokken weergeven hoe toowork met Microsoft R Server, SQL Server 2016 R Services (In de database analytics), Python, Microsoft cognitieve ToolKit (CNTK) voor grondige learning en andere Azure Zodra u zich aanmeldt tooJupyter-technologieën. Nadat u verifieert toohello Jupyter-notebook met Hallo wachtwoord die u in een eerdere stap hebt gemaakt, kunt u op Hallo notebook startpagina Hallo koppeling toohello voorbeelden zien. 

### <a name="visual-studio-2015-community-edition"></a>Visual Studio 2015 Community edition
Visual Studio Community edition is geïnstalleerd op Hallo VM. Het is een gratis versie van Hallo populaire IDE van Microsoft die u voor evaluatiedoeleinden gebruikt en voor kleine teams gebruiken kunt. U kunt Hallo licentievoorwaarden uitchecken [hier](https://www.visualstudio.com/support/legal/mt171547).  Visual Studio niet openen door te dubbelklikken op het bureaubladpictogram Hallo of Hallo **Start** menu. U kunt ook zoeken naar programma's met **Win** + **S** en 'Visual Studio' in te voeren. Zodra er kunt u projecten in talen zoals C#, Python, R, node.js. Invoegtoepassingen zijn ook geïnstalleerd om het handige toowork met Azure-services zoals Azure Data Catalog, Azure HDInsight (Hadoop, Spark) en Azure Data Lake. 

> [!NOTE]
> Mogelijk dat u een bericht waarin staat dat uw evaluatieperiode is verlopen. Voer de referenties van uw Microsoft-account of maak een nieuwe gratis account tooget toegang-toohello Visual Studio Community Edition. 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>Ontwikkelaarsversie van SQL Server 2016
Een developer-versie van SQL Server 2016 met R Services toorun in database analytics is beschikbaar op Hallo VM. R-Services bieden een platform voor het ontwikkelen en implementeren van intelligent toepassingen. U kunt Hallo rijke en krachtige R taal gebruiken en Hallo veel pakketten uit Hallo community toocreate modellen en voorspellingen voor uw SQL Server-gegevens genereren. Omdat het R-Services (In database) Hallo R-taal geïntegreerd met SQL Server, kunt u analytics sluiten toohello gegevens bewaren. Dit voorkomt Hallo kosten en beveiligingsrisico's met de verplaatsing van gegevens.

> [!NOTE]
> Hallo SQL Server 2016 ontwikkelaarsversie kan alleen worden gebruikt voor ontwikkeling en tests doeleinden. U moet een licentie toorun in productie. 
> 
> 

U kunt toegang tot Hallo SQL server door het starten van **SQL Server Management Studio**. De naam van uw VM is ingevuld als Hallo servernaam. Windows-verificatie wanneer aangemeld als beheerder op Windows hello gebruiken. Wanneer u naar SQL Server Management Studio kunt u andere gebruikers te maken, databases maken, gegevens importeren en SQL-query's uitvoeren. 

tooenable In database-analyses met behulp van Microsoft-R, Voer Hallo volgende opdracht als een één-bewerking in SQL Server management studio na het aanmelden als beheerder van de server Hallo tijd. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace hello %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Azure
Verschillende Azure-hulpprogramma's zijn geïnstalleerd op Hallo VM:

* Er is een snelkoppeling op het bureaublad tooaccess hello Azure SDK-documentatie. 
* **AzCopy**: toomove gegevens binnen en buiten uw Microsoft Azure Storage-Account gebruikt. toosee gebruik van het type **Azcopy** bij een opdrachtprompt toosee Hallo gebruik. 
* **Microsoft Azure Storage Explorer**: toobrowse via Hallo-objecten die u hebt opgeslagen in uw Azure Storage-Account en de overdracht tooand van gegevens naar Azure storage gebruikt. U kunt typen **Opslagverkenner** bij zoeken of zoeken op Hallo tooaccess van menu Start van Windows met dit hulpprogramma. 
* **Adlcopy**: toomove gegevens tooAzure Data Lake gebruikt. toosee gebruik van het type **adlcopy** in een opdrachtprompt. 
* **dtui**: toomove gegevens tooand uit Azure Cosmos DB, een NoSQL-database op Hallo cloud gebruikt. Type **dtui** op de opdrachtprompt. 
* **Microsoft Data Management Gateway**: kunt verplaatsing van gegevens tussen on-premises gegevensbronnen en cloud. Binnen hulpmiddelen zoals Azure Data Factory wordt gebruikt. 
* **Microsoft Azure Powershell**: een hulpprogramma gebruikt tooadminister uw Azure-resources in Hallo Powershell scripttaal is ook geïnstalleerd op de virtuele machine. 

### <a name="power-bi"></a>Power BI
toohelp u bouwt dashboards en geweldige visualisaties hello **Power BI Desktop** is geïnstalleerd. Dit hulpprogramma toopull-gegevens uit verschillende bronnen, tooauthor gebruiken uw dashboards en rapporten en toopublish ze toohello cloud. Zie voor informatie Hallo [Power BI](http://powerbi.microsoft.com) site. U kunt Power BI desktop vinden op Hallo startmenu. 

> [!NOTE]
> U moet een Office 365-account tooaccess Power BI. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>Aanvullende Microsoft-ontwikkelprogramma 's
Hallo [ **Microsoft Web Platform Installer** ](https://www.microsoft.com/web/downloads/platform.aspx) kunnen worden gebruikt toodiscover en andere Microsoft-ontwikkelprogramma's downloaden. Er is ook een snelkoppeling toohello hulpprogramma op Hallo Microsoft Data wetenschappelijke Virtual Machine bureaublad.  

## <a name="important-directories-on-hello-vm"></a>Belangrijke mappen op Hallo VM
| Item | Directory |
| --- | --- |
| Jupyter-notebook serverconfiguraties |C:\ProgramData\jupyter |
| Basismap van Jupyter-Notebook-voorbeelden |c:\dsvm\notebooks |
| Andere voorbeelden |c:\dsvm\samples |
| Anaconda (standaard: Python 2.7) |c:\Anaconda |
| Anaconda 3.5 Python-omgeving |c:\Anaconda\envs\py35 |
| R Server zelfstandig exemplaar directory (standaard R-exemplaren op basis van R3.2.2) |C:\Program Files\Microsoft SQL Server\130\R_SERVER |
| R Server In de database-exemplaar directory (R3.2.2) |C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES |
| Microsoft R openen (R3.3.1) exemplaar directory |C:\Program Files\Microsoft\MRO-3.3.1 |
| Diverse hulpprogramma 's |c:\dsvm\tools |

> [!NOTE]
> Exemplaren van Hallo die Microsoft Data wetenschappelijke virtuele Machine voordat 1.5.0 (vóór 3 September 2016 gemaakt) gebruikt een iets andere mapstructuur dan is opgegeven in de voorgaande tabel Hallo. 
> 
> 

## <a name="next-steps"></a>Volgende stappen
Hier volgen enkele volgende stappen toocontinue uw leren en te verkennen. 

* Verken Hallo verschillende hulpmiddelen voor gegevens wetenschappelijke op Hallo gegevenswetenschap VM door te klikken op Hallo menu start en Hallo-hulpprogramma's die worden weergegeven op Hallo menu wordt uitgecheckt.
* Navigeer te**C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts** voor voorbeelden weergegeven met behulp van Hallo RevoScaleR bibliotheek in R die ondersteuning biedt voor gegevensanalyse die op grote schaal enterprise.  
* Hallo-artikel lezen: [10 dingen die u op Hallo gegevenswetenschap virtuele Machine doen kunt](http://aka.ms/dsvmtenthings)
* Meer informatie over hoe toobuild end tooend analytische oplossingen systematischer met Hallo [Team gegevens wetenschap proces](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).
* Ga naar Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com) voor machine learning en analytics die gebruik Hallo Cortana Intelligence Suite voorbeelden. We hebben ook een pictogram gegeven op Hallo **Start** menu en op Hallo bureaublad van Hallo toothis galerie met virtuele machines.

