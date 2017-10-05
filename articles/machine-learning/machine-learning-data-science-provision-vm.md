---
title: De gegevens van Microsoft-wetenschappelijke virtuele Machine inrichten | Microsoft Docs
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
ms.openlocfilehash: 76cd54cd234dfe43e8f0d61f0b66f0ed0c09e8b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="provision-the-microsoft-data-science-virtual-machine"></a>De virtuele Microsoft-gegevenswetenschapmachine inrichten
De Microsoft Data wetenschappelijke virtuele Machine is een Windows Azure virtuele machine (VM) vooraf is geïnstalleerd en geconfigureerd met verschillende populaire hulpprogramma's die vaak worden gebruikt voor gegevensanalyse en machine learning. De hulpprogramma's zijn:

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
  * [Rattle](http://rattle.togaware.com/) (de R analytische hulpprogramma voor meer informatie over eenvoudig): een hulpprogramma dat aan de slag met data analytics en machine learning in R eenvoudig met een GUI-gebaseerde gegevensverkenning en modellering met automatische R codegeneratie maakt.
  * [mxnet](https://github.com/dmlc/mxnet): een grondige learning framework ontworpen voor zowel efficiëntie en flexibiliteit
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/) : een visual gegevensanalyse en machine learning-software in Java.
  * [Apache inzoomen](https://drill.apache.org/): een schemavrije SQL Query-Engine voor Hadoop, NoSQL- en Cloud-opslag.  Biedt ondersteuning voor ODBC- en JDBC-interfaces om in te schakelen query NoSQL- en bestanden van de standaard BI-tools zoals Power BI, Excel, Tableau.
* Bibliotheken in R- en Python voor gebruik in Azure Machine Learning en andere Azure-services
* GIT, met inbegrip van Git Bash werken met broncodeopslagplaatsen, met inbegrip van GitHub, Visual Studio Team Services
* Windows-poorten van verschillende populaire Linux opdrachtregelprogramma's (inclusief awk, ype, perl, grep, zoeken, wget, curl enzovoort) toegankelijk zijn via de opdrachtprompt. 

Tijdens het doorzoeken van wetenschappelijke gegevens omvat sequentieel op een reeks taken:

1. Zoeken, laden en vooraf verwerken van gegevens
2. Maken en testen van modellen
3. De modellen voor verbruik in intelligente toepassingen implementeren

Gegevenswetenschappers gebruik tal van hulpprogramma's om deze taken te voltooien. Het kan erg tijd in beslag nemen om te zoeken naar de juiste versies van de software, en vervolgens downloaden en installeren ze zijn. De Microsoft Data wetenschappelijke virtuele Machine kunt deze last vereenvoudigen doordat een kant-en-klare-installatiekopie die kan worden ingericht op Azure met alle verschillende populaire hulpmiddelen vooraf is geïnstalleerd en geconfigureerd. 

De virtuele Machine voor Microsoft Data wetenschappelijke jump-starts uw project analytics. Hiermee kunt u om te werken op taken in verschillende talen, waaronder R, Python, SQL en C#. Visual Studio biedt een IDE voor het ontwikkelen en testen van uw code die eenvoudig te gebruiken. De Azure SDK opgenomen in de virtuele machine kunt u uw toepassingen bouwen met verschillende services op Microsoft cloud-platform. 

Er zijn geen kosten voor software voor deze gegevens wetenschappelijke VM-installatiekopie. U betaalt alleen voor de Azure gebruikskosten welke die afhankelijk zijn van de grootte van de virtuele machine die u inricht. Meer informatie over de compute-kosten vindt u in de sectie Pricing details op de [gegevens wetenschappelijke virtuele Machine](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) pagina. 

## <a name="other-versions-of-the-data-science-virtual-machine"></a>Andere versies van de gegevens wetenschappelijke virtuele Machine
Een [CentOS](machine-learning-data-science-linux-dsvm-intro.md) installatiekopie is ook beschikbaar met veel van dezelfde hulpmiddelen als de Windows-installatiekopie. Een [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) installatiekopie is beschikbaar, evenals met veel vergelijkbare extra plus deep frameworks leren.

## <a name="prerequisites"></a>Vereisten
Voordat u een Microsoft Data wetenschappelijke virtuele Machine maken kunt, moet u het volgende hebben:

* **Een Azure-abonnement**: Zie voor een [gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Een Azure storage-account**: als u wilt maken, Zie [maken van een Azure storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account). U kunt ook kan de storage-account worden gemaakt als onderdeel van het proces voor het maken van de virtuele machine als u niet wilt dat een bestaand account gebruiken.

## <a name="create-your-microsoft-data-science-virtual-machine"></a>Uw Microsoft Data wetenschappelijke virtuele Machine maken
Hier volgen de stappen voor het maken van een exemplaar van de Microsoft wetenschappelijke virtuele Machine gegevens:

1. Navigeer naar de virtuele machine op aanbieding [Azure-portal](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).
2. Selecteer de **maken** knop onderaan in een wizard moeten worden genomen.![ Configureer-gegevens-wetenschappelijke-vm](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. De wizard gebruikt voor het maken van de Microsoft Data wetenschappelijke virtuele Machine vereist **invoer** voor elk van de **vijf stappen** opgesomd aan de rechterkant van de volgende afbeelding. Hier volgen de invoer voor het configureren van deze stappen:
   
   1. **Basisinstellingen**
      
      1. **Naam**: naam van uw gegevens wetenschap-server die u maakt.
      2. **Gebruikersnaam**: Admin-account aanmeldings-id.
      3. **Wachtwoord**: wachtwoord van de beheerder.
      4. **Abonnement**: als u meer dan één abonnement hebt, selecteert u een op waarop de machine is gemaakt en kosten in rekening gebracht.
      5. **Resourcegroep**: U kunt een nieuwe maken of een bestaande groep.
      6. **Locatie**: Selecteer het datacenter die het meest geschikt is. Het is doorgaans het datacenter die de meeste van uw gegevens of heeft de dichtstbijzijnde fysieke voor snelste toegang tot het netwerk.
   2. **De grootte van**: Selecteer een van de servertypen die voldoet aan uw functionele vereisten en kostenbeperkingen. U kunt meer mogelijkheden van VM-formaten ophalen door 'Alles weergeven' selecteren.
   3. **Instellingen**:
      
      1. **Schijftype**: Premium kiezen als u liever een SSD-station (SSD), anders selecteert 'Standaard'.
      2. **Storage-Account**: U kunt een nieuwe Azure storage-account maken in uw abonnement of gebruik een bestaande in dezelfde *locatie* die is gekozen voor de **basisbeginselen** stap van de wizard.
      3. **Andere parameters**: meestal zojuist hebt u de standaardwaarden. U kunt de muisaanwijzer op de informatief koppeling voor meer informatie over de specifieke velden voor het geval wilt u het gebruik van niet-standaard waarden.
   4. **Samenvatting**: Controleer of alle informatie die u hebt ingevoerd juist is.
   5. **Kopen**: klik op **kopen** starten van de inrichting. Een koppeling is met de voorwaarden van de transactie opgegeven. De virtuele machine heeft geen eventuele extra kosten afgezien van de berekening die voor de servergrootte van de die u hebt gekozen in de **grootte** stap. 

> [!NOTE]
> De inrichting duren ongeveer 10-20 minuten. De status van de inrichting wordt weergegeven op de Azure-portal.
> 
> 

## <a name="how-to-access-the-microsoft-data-science-virtual-machine"></a>Toegang tot de Microsoft Data wetenschappelijke virtuele Machine
Nadat de virtuele machine is gemaakt, kunt u extern bureaublad in met behulp van de referenties van het Administrator-account die u hebt geconfigureerd in de voorgaande **basisbeginselen** sectie. 

Als uw virtuele machine is gemaakt en ingericht, bent u klaar om te beginnen met de hulpprogramma's die zijn geïnstalleerd en geconfigureerd op deze. Er zijn start menu tegels en bureaubladpictogrammen voor veel van de hulpprogramma's. 

## <a name="how-to-create-a-strong-password-for-jupyter-and-start-the-notebook-server"></a>Het maken van een sterk wachtwoord voor Jupyter en start de server notebook
Standaard is de Jupyter-notebook server vooraf geconfigureerde maar op de virtuele machine wordt uitgeschakeld totdat u een Jupyter-wachtwoord instellen. Voor het maken van een sterk wachtwoord voor de Jupyter-notebook-server geïnstalleerd op de machine, voer de volgende opdracht vanaf een opdrachtprompt op de gegevens wetenschappelijke virtuele Machine of dubbelklik op de snelkoppeling op het bureaublad bieden wij aangeroepen **Jupyter instellen Wachtwoord & Start** van een lokale administrator-account van VM.

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

Ga als volgt de berichten en kiest u een sterk wachtwoord wanneer u wordt gevraagd.

Dit script maakt een hash van het wachtwoord en de store in het configuratiebestand Jupyter vinden op: **C:\ProgramData\jupyter\jupyter_notebook_config.py** onder de parameternaam van de ***c.NotebookApp.password***.

Het script maakt ook en de Jupyter-server op de achtergrond uitgevoerd. Jupyter-server is gemaakt als een windows-taak in de WIndows Taakplanner genoemd **Start_IPython_Notebook**.  U moet wachten op een paar seconden na het instellen van het wachtwoord voor het openen van de notebook in uw browser. Zie de sectie met de titel **Jupyter-Notebook** over toegang krijgen tot de Jupyter-notebook-server. 


## <a name="tools-installed-on-the-microsoft-data-science-virtual-machine"></a>Hulpprogramma's zijn geïnstalleerd op de Microsoft Data wetenschappelijke virtuele Machine

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Developer Edition
Als u R gebruiken voor uw analyses wilt, heeft de virtuele machine Microsoft R Server Developer edition is geïnstalleerd. Microsoft R Server is een grotendeels implementeerbare bedrijfsniveau analytics platform op basis van R die wordt ondersteund, schaalbare en veilige. Ondersteuning biedt voor tal van big data-statistieken, voorspellende modellen en machine learning-mogelijkheden, R Server biedt ondersteuning voor het volledige bereik van analytics – exploratie, analyse, visualisatie en modellering. Door en open-source R uitbreiden, is Microsoft R Server volledig compatibel is met het R-scripts, functies en CRAN pakketten, om gegevens op grote schaal enterprise te analyseren. Biedt ook een oplossing de beperkingen in het geheugen van de Open Source R door parallelle en gesegmenteerde verwerking van gegevens toe te voegen. Hiermee kunt u analyses uitvoeren op gegevens veel groter dan wat in het hoofdgeheugen past.  Visual Studio Community Edition opgenomen op de virtuele machine bevat de R-Tools voor Visual Studio-extensie die een volledige IDE biedt voor het werken met R. U kunt ook downloaden en gebruiken van andere IDE ook zoals [RStudio](http://www.rstudio.com). 

### <a name="python"></a>Python
Voor de ontwikkeling met behulp van Python, is distributie Anaconda Python 2.7 en 3.5 geïnstalleerd. Deze verdeling bevat de base Python samen met ongeveer 300 van de meest populaire math, engineering en gegevens analytics pakketten. U kunt Python-Tools voor Visual Studio (PTVS) die is geïnstalleerd in de Visual Studio 2015-Community-versie of een van de IDE gebundeld met Anaconda zoals niet-actief of Spyder gebruiken. U kunt een van deze door te zoeken op de zoekbalk starten (**Win** + **S** sleutel).

> [!NOTE]
> Om te verwijzen de Python-Tools voor Visual Studio op Anaconda Python 2.7 en 3.5, moet u aangepaste omgevingen voor elke versie te maken. Navigeer naar deze omgeving paden in de Visual Studio 2015 Community Edition stelt **extra** -> **Python Tools** -> **Python-omgevingen**en klik vervolgens op **+ aangepaste**. 
> 
> 

Anaconda Python 2.7 onder C:\Anaconda is geïnstalleerd en Anaconda Python 3.5 onder c:\Anaconda\envs\py35 is geïnstalleerd. Zie [documentatie bij PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) voor gedetailleerde stappen. 

### <a name="jupyter-notebook"></a>Jupyter Notebook
Anaconda-verdeling wordt ook geleverd met een Jupyter-notebook een omgeving voor het delen van code en -analyse. Een Jupyter-notebook-server is vooraf is geconfigureerd met Python 2.7, Python 3.4 Python 3.5 en R kernels. Er is een pictogram op het bureaublad met de naam 'Jupyter-Notebook starten van de browser voor toegang tot de Notebook-server. Als u op de virtuele machine via Extern bureaublad bent, kunt u ook bezoeken [https://localhost:9999 /](https://localhost:9999/) voor toegang tot de Jupyter-notebook server wanneer aangemeld bij de virtuele machine.

> [!NOTE]
> Doorgaan als u certificaatwaarschuwingen. 
> 
> 

We hebben verschillende voorbeeldquery notitieblokken in Python en in R. verpakt De Jupyter-notebooks laten zien hoe werken met Microsoft R Server, SQL Server 2016 R Services (In de database analytics), Python, Microsoft cognitieve ToolKit (CNTK) voor grondige learning en andere technologieën voor Azure wanneer u zich bij Jupyter aanmelden. Nadat u geverifieerd bij de Jupyter-notebook met het wachtwoord die u in een eerdere stap hebt gemaakt, kunt u de koppeling naar de voorbeelden bekijken op de startpagina van de notebook. 

### <a name="visual-studio-2015-community-edition"></a>Visual Studio 2015 Community edition
Visual Studio Community edition is geïnstalleerd op de virtuele machine. Het is een gratis versie van de populaire IDE van Microsoft die u voor evaluatiedoeleinden gebruikt en voor kleine teams gebruiken kunt. U kunt de licentievoorwaarden uitchecken [hier](https://www.visualstudio.com/support/legal/mt171547).  Visual Studio niet openen door te dubbelklikken op het bureaubladpictogram of de **Start** menu. U kunt ook zoeken naar programma's met **Win** + **S** en 'Visual Studio' in te voeren. Zodra er kunt u projecten in talen zoals C#, Python, R, node.js. Invoegtoepassingen zijn ook geïnstalleerd die werken met Azure-services zoals Azure Data Catalog, Azure HDInsight (Hadoop, Spark) en Azure Data Lake te vergemakkelijken. 

> [!NOTE]
> Mogelijk dat u een bericht waarin staat dat uw evaluatieperiode is verlopen. Voer de referenties van uw Microsoft-account of maak een nieuwe gratis account toegang krijgen tot de Visual Studio Community Edition. 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>Ontwikkelaarsversie van SQL Server 2016
Een developer-versie van SQL Server 2016 met R-Services worden uitgevoerd in de database analytics is beschikbaar op de virtuele machine. R-Services bieden een platform voor het ontwikkelen en implementeren van intelligent toepassingen. U kunt de veel pakketten van de community en de rijke en krachtige R-taal voor modellen maken en het genereren van voorspellingen voor uw SQL Server-gegevens. Omdat het R-Services (In database) de R-taal geïntegreerd met SQL Server, kunt u analytics dicht bij de gegevens behouden. Hierdoor is de kosten en beveiligingsrisico's met de verplaatsing van gegevens.

> [!NOTE]
> De ontwikkelaarsversie van SQL Server 2016 kan alleen worden gebruikt voor ontwikkeling en testdoeleinden. U moet een licentie uit te voeren in de productieomgeving. 
> 
> 

U hebt toegang tot de SQL-server starten **SQL Server Management Studio**. De naam van uw VM is ingevuld als de naam van de Server. Windows-verificatie gebruiken wanneer u bent aangemeld als de beheerder in Windows. Wanneer u naar SQL Server Management Studio kunt u andere gebruikers te maken, databases maken, gegevens importeren en SQL-query's uitvoeren. 

Als u wilt inschakelen In database analytics Microsoft R gebruiken, kunt u de volgende opdracht uitvoeren als een actie in SQL Server management studio na het aanmelden als beheerder van de tijd. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace the %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Azure
Verschillende Azure-hulpprogramma's worden geïnstalleerd op de virtuele machine:

* Er is een snelkoppeling op het bureaublad voor toegang tot de Azure SDK-documentatie. 
* **AzCopy**: gebruikt voor het verplaatsen van gegevens binnen en buiten uw Microsoft Azure Storage-Account. Gebruik Typ **Azcopy** achter de opdrachtprompt om te zien van het gebruik. 
* **Microsoft Azure Storage Explorer**: gebruikt voor het bladeren door de objecten die u hebt opgeslagen in uw Azure Storage-Account en de overdracht gegevens van en naar Azure storage. U kunt typen **Opslagverkenner** in zoeken of deze in het menu Start van Windows voor toegang tot dit hulpprogramma vinden. 
* **Adlcopy**: gebruikt om gegevens te verplaatsen naar Azure Data Lake. Gebruik Typ **adlcopy** in een opdrachtprompt. 
* **dtui**: gebruikt om gegevens te verplaatsen naar en van Azure Cosmos DB, een NoSQL-database in de cloud. Type **dtui** op de opdrachtprompt. 
* **Microsoft Data Management Gateway**: kunt verplaatsing van gegevens tussen on-premises gegevensbronnen en cloud. Binnen hulpmiddelen zoals Azure Data Factory wordt gebruikt. 
* **Microsoft Azure Powershell**: een hulpprogramma dat wordt gebruikt voor het beheren van uw Azure-resources in de Powershell scripttaal is ook geïnstalleerd op de virtuele machine. 

### <a name="power-bi"></a>Power BI
Voor hulp bij het bouwen van dashboards en geweldige visualisaties de **Power BI Desktop** is geïnstalleerd. Met dit hulpprogramma kunt pull gegevens uit verschillende bronnen uw dashboards en rapporten, maken en deze publiceren in de cloud. Zie voor meer informatie, de [Power BI](http://powerbi.microsoft.com) site. Power BI desktop vindt u in het menu Start. 

> [!NOTE]
> U moet een Office 365-account voor toegang tot Power BI. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>Aanvullende Microsoft-ontwikkelprogramma 's
De [ **Microsoft Web Platform Installer** ](https://www.microsoft.com/web/downloads/platform.aspx) kan worden gebruikt om te detecteren en andere Microsoft-ontwikkelprogramma's downloaden. Er is ook een snelkoppeling naar het hulpprogramma dat op het bureaublad van Microsoft Data wetenschappelijke virtuele Machine.  

## <a name="important-directories-on-the-vm"></a>Belangrijke mappen op de virtuele machine
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
> Exemplaren van de Microsoft Data wetenschappelijke virtuele Machine gemaakt voordat 1.5.0 (vóór 3 September 2016) gebruikt een iets andere mapstructuur dan is opgegeven in de voorgaande tabel. 
> 
> 

## <a name="next-steps"></a>Volgende stappen
Hier volgen enkele volgende stappen om door te gaan uw leren en te verkennen. 

* Verken de verschillende beschikbare hulpprogramma wetenschappelijke gegevens op de virtuele machine voor gegevenswetenschap door te klikken op het startmenu en controleren van de hulpprogramma's die worden vermeld in het menu.
* Navigeer naar **C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts** voor voorbeelden weergegeven met behulp van de bibliotheek RevoScaleR in R die ondersteuning biedt voor gegevensanalyse die op grote schaal enterprise.  
* Lees het artikel: [10 dingen die u op de virtuele Machine voor gegevenswetenschap doen kunt](http://aka.ms/dsvmtenthings)
* Informatie over het bouwen van end-to-end analyseoplossingen systematischer met behulp van de [Team gegevens wetenschap proces](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).
* Ga naar de [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com) voor machine learning en analytics voorbeelden die gebruikmaken van de Cortana Intelligence Suite. We hebben ook een pictogram opgegeven op de **Start** menu en op het bureaublad van de virtuele machine aan deze galerie.

