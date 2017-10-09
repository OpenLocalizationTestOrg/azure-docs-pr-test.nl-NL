---
title: aaaTen kunt u dingen doen op Hallo gegevens wetenschappelijke virtuele Machine | Microsoft Docs
description: Verschillende gegevensverkenning en modellering taak uitvoeren op Hallo gegevenswetenschap virtuele Machine.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a>Tien wat u kunt doen voor gegevenswetenschap Hallo virtuele Machine
Hallo gegevens wetenschappelijke virtuele Machine (DSVM) is een krachtige gegevens wetenschappelijke ontwikkelingsomgeving waarmee u tooperform verschillende gegevens te verkennen en modellering taken. Hallo omgeving komt al gebouwd en gebundelde met verschillende populaire gegevens analytics-hulpprogramma's waarmee u eenvoudig tooget snel de slag met uw analyse voor On-premises, Cloud of hybride implementaties. Hallo DSVM nauw met vele Azure-services en is kunnen tooread en gegevens over het installatieproces die al zijn opgeslagen in Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage of Azure Cosmos DB. Het kan ook gebruikmaken van andere hulpprogramma's voor webanalyse zoals Azure Machine Learning en Azure Data Factory.

In dit artikel we zien hoe u toouse uw tooperform DSVM gegevenswetenschap verschillende taken en communiceren met andere Azure-services. Hier volgen enkele Hallo kunt u dingen op Hallo DSVM doen:

1. Gegevens verkennen en ontwikkelen van modellen lokaal op Hallo DSVM met behulp van Microsoft-Server voor R, Python
2. Gebruik van een Jupyter-notebook tooexperiment met uw gegevens op een browser met gebruik van Python 2, 3, Python, Microsoft R een gereed enterprise-versie van R ontworpen voor schaalbaarheid en prestaties
3. Modellen gebouwd met behulp van R- en Python in Azure Machine Learning zodat clienttoepassingen toegang heeft tot uw via een eenvoudige webinterface services modellen operationeel maken
4. Uw Azure-resources met Azure-portal of Powershell beheren
5. Uw opslagruimte uitbreiden en delen van grootschalige gegevenssets / code in uw hele team door het maken van een Azure File storage als een koppelbaar station op uw DSVM
6. Code delen met uw team met behulp van GitHub en toegang tot uw opslagplaats voor Hallo vooraf geïnstalleerde Git clients - Git Bash Git GUI.
7. Toegang krijgen tot diverse Azure gegevens en analyse-services zoals Azure blob-opslag, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB Azure SQL Data Warehouse & databases
8. Maak rapporten en een dashboard met Power BI Desktop vooraf geïnstalleerd zijn op Hallo DSVM hello en deze implementeren op Hallo cloud
9. Dynamisch schalen uw DSVM toomeet die behoeften van uw project
10. Extra hulpprogramma's installeren op de virtuele machine   

> [!NOTE]
> Aanvullende informatie over het gebruik gelden voor een groot aantal Hallo extra opslag en analyses gegevensservices die in dit artikel worden vermeld. Raadpleeg toohello [prijzen van Azure](https://azure.microsoft.com/pricing/) pagina voor meer informatie.
> 
> 

**Vereisten**

* U moet een Azure-abonnement. U kunt zich aanmelden voor een gratis proefversie [hier](https://azure.microsoft.com/free/).
* Instructies voor het inrichten van een Data wetenschappelijke virtuele Machine op Hallo Azure-portal zijn beschikbaar op [maken van een virtuele machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a>1. Gegevens verkennen en ontwikkelen van modellen Microsoft R Server of Python
U kunt talen zoals R- en Python toodo uw gegevensanalyse rechts op Hallo DSVM.

Voor R, kunt u een IDE 'Revolution R Enterprise 8.0' die op Hallo startmenu of Hallo bureaublad kan worden gevonden. Microsoft heeft opgegeven, aanvullende bibliotheken boven op Hallo Open CRAN-bron-R tooenable schaalbare analytics en Hallo mogelijkheid tooanalyze gegevens groter is dan de geheugengrootte Hallo toegestaan door het uitvoeren van parallelle gesegmenteerde analyse. U kunt ook installeren met een R-IDE van uw keuze soortgelijke [RStudio](https://www.rstudio.com/products/rstudio-desktop/).

Voor Python, kunt u een IDE zoals Visual Studio Community Edition waarvoor Hallo Python-Tools voor Visual Studio (PTVS)-extensie die vooraf zijn geïnstalleerd. Een basic Python 2.7 is standaard geconfigureerd op PTVS (zonder een bibliotheek analytics, zoals SciKit, Pandas). In de volgorde tooenable Anaconda Python 2.7 en 3.5 moet u toodo Hallo volgende:

* Maken van aangepaste omgevingen voor elke versie door te navigeren**extra** -> **Python Tools** -> **Python-omgevingen** en vervolgens te klikken op ' **+ Aangepaste**'in hello Visual Studio 2015 Community Edition
* Geef een beschrijving en stel Hallo omgeving paden als voorvoegsel *c:\anaconda* voor Anaconda Python 2.7 of *c:\anaconda\envs\py35* voor Anaconda Python 3.5
* Klik op **automatische detectie** en vervolgens **toepassen** toosave Hallo-omgeving.

Hier wordt de installatie van welke Hallo-aangepaste omgeving in Visual Studio lijkt.

![PTVS Setup](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

Zie Hallo [documentatie bij PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) voor aanvullende details over het toocreate Python-omgevingen.

Nu weet u instellen toocreate een nieuwe Python-project. Navigeer te**bestand** -> **nieuw** -> **Project** -> **Python** en selecteer Hallo type Python-toepassing bouwen. U kunt Python-omgeving Hallo Hallo huidige versie van project toohello gewenste (Anaconda 2.7 of 3.5) instellen: met de rechtermuisknop op Hallo **Python-omgeving**, selecteer **Python-omgevingen toevoegen/verwijderen**, en Selecteer Hallo gewenste vervolgens omgeving tooassociate met Hallo-project. U vindt meer informatie over het werken met PTVS op Hallo product [documentatie](https://github.com/Microsoft/PTVS/wiki) pagina.

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a>2. Een Jupyter-Notebook tooexplore en dit model van uw gegevens gebruiken met Python of R
Hallo Jupyter-Notebook is een krachtige omgeving met een browser gebaseerde 'IDE' voor gegevensverkenning en modellering. U kunt Python 2, 3 Python of R (Open Source en Hallo Microsoft R Server) gebruiken in een Jupyter-Notebook.

toolaunch hello Jupyter-Notebook klikt u op Hallo start menupictogram / pictogram op het bureaublad met de titel **Jupyter-Notebook**. Op Hallo DSVM u kunt ook bladeren te ' https://localhost:9999 / ' tooaccess Hallo Jupiter Notebook. Als u gevraagd een wachtwoord, gebruik instructies in Hallo ***hoe toocreate een sterk wachtwoord op Hallo Jupyter-notebook server*** sectie Hallo [inrichten Hallo Microsoft Data wetenschappelijke Virtual Machine](machine-learning-data-science-provision-vm.md)onderwerp toocreate een sterk wachtwoord tooaccess hello Jupyter-notebook. 

Nadat u de notebook Hallo hebt geopend, ziet u een map met een paar voorbeeld-notitieblokken die vooraf verpakte in Hallo DSVM zijn. U kunt nu:

* Klik op het Hallo-notebook toosee Hallo code.
* elke cel uitvoeren door te drukken **SHIFT + ENTER**.
* Hallo gehele notebook uitvoeren door te klikken op **cel** -> **uitvoeren**
* Maak een nieuwe notebook door te klikken op Hallo Jupyter-pictogram (bovenste linkerhoek) **nieuw** op Hallo rechts en vervolgens Hallo notebook taal (ook wel bekend als kernels) te kiezen.   

> [!NOTE]
> Momenteel er ondersteuning geboden voor Python 2.7, Python 3.5 en R. Hallo R kernel programmering in zowel Open-source R als Hallo enterprise ondersteunt schaalbare Microsoft R Server.   
> 
> 

Wanneer u naar het Hallo-notebook kunt u Verken uw gegevens, Hallo model bouwen, testen met behulp van uw keuze van bibliotheken Hallo-model.

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a>3. Gebruik R of Python en Operationalize ervan met Azure Machine Learning modellen bouwen
Zodra u hebt gemaakt en gevalideerd uw model Hallo volgende stap is het meestal toodeploy deze in productie. Hierdoor kan de client toepassingen tooinvoke Hallo modelvoorspellingen op een realtime of op basis van de batch-modus. Azure Machine Learning biedt een mechanisme toooperationalize een ingebouwd in R- of Python-model.

Wanneer u het Azure Machine Learning-model operationeel maken, wordt een webservice weergegeven waarmee clients toomake REST-aanroepen die doorgeven in de invoerparameters en voorspellingen uit Hallo model ontvangen als uitvoer.   

> [!NOTE]
> Als u hebt nog niet aangemeld voor Azure Machine Learning, kunt u een gratis werkruimte of een standaard werkruimte verkrijgen via Hallo [Azure Machine Learning Studio](https://studio.azureml.net/) startpagina en te klikken op 'aan de slag'.   
> 
> 

### <a name="build-and-operationalize-python-models"></a>Build en Python operationeel modellen
Hier volgt een codefragment aan ontwikkeld als een Jupyter-Notebook van Python die voortbouwt een eenvoudige model met behulp van Hallo SciKit meer bibliotheek.

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

Hallo methode toodeploy uw python modellen tooAzure Machine Learning terugloopt Hallo voorspelling van Hallo-model in een functie gebruikt en wordt deze verfraaid met kenmerken die worden geleverd door Hallo vooraf geïnstalleerde Azure Machine Learning python-bibliotheek basis van uw Azure-Machine Learning-werkruimte-ID, API-sleutel en Hallo invoer en parameters retourneren.  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

Een client kan nu aanroepen toohello webservice maken. Er zijn gemak wrappers die Hallo REST-API-aanvragen samenstellen. Hier volgt een voorbeeld code tooconsume Hallo-webservice.

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> Hello Azure Machine Learning-bibliotheek wordt alleen ondersteund voor Python 2.7 momenteel.   
> 
> 

### <a name="build-and-operationalize-r-models"></a>Build en operationeel R modellen
U kunt implementeren R modellen gebouwd op Hallo gegevens wetenschappelijke virtuele Machine of elders naar Azure Machine Learning op een manier die vergelijkbaar toohow die het voor Python is voltooid. Haar Hallo stappen:

* Maak een settings.json bestand tooprovide uw werkruimte-ID en auth token zoals weergegeven in het volgende codevoorbeeld Hallo.
* Schrijf een wrapper voor Hallo-model functie voorspellen.
* Roep ```publishWebService``` in hello Azure Machine Learning-bibliotheek toopass in Hallo functie wrapper.  

Hier volgt Hallo procedure en code codefragmenten die kunnen worden gebruikt tooset up, maken, publiceren en gebruiken van een model als een webservice in Azure Machine Learning.

#### <a name="setup"></a>Instellen
1. Hallo Machine Learning-R-pakket installeren door te typen ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE of uw R-IDE.
2. Download RTools van [hier](https://cran.r-project.org/bin/windows/Rtools/). U moet uw R-pakket Hallo zip hulpprogramma in Hallo pad (en benoemde zip.exe) toooperationalize in Machine Learning.
3. Maak een bestand settings.json onder de map ```.azureml``` onder de basismap en Voer Hallo-parameters uit uw Azure Machine Learning-werkruimte:

Settings.JSON bestandsstructuur:

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a>Een model in R bouwen en deze publiceren in Azure Machine Learning
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a>Hallo model is geïmplementeerd in Azure Machine Learning gebruiken
tooconsume hello model van een clienttoepassing, gebruiken we hello Azure Machine Learning-bibliotheek toolook up Hallo webservice gepubliceerd op naam Hallo met `services` API-aanroep toodetermine Hallo-eindpunt. Vervolgens u zojuist hebt Hallo roept `consume` functioneren en doorgeven in Hallo gegevens frame toobe voorspeld.
Hallo na de code is gebruikte tooconsume Hallo model is gepubliceerd als een Azure Machine Learning-webservice.

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

Meer informatie over hello Azure Machine Learning R library vindt [hier](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a>4. Uw Azure-resources met Azure-portal of Powershell beheren
Hallo DSVM kunt u niet alleen toobuild analytics-oplossing lokaal op Hallo van virtuele machine, maar kunt u ook tooaccess services op Microsoft Azure-cloud. Azure biedt verschillende compute, storage, gegevens analytics-services en andere services die u kunt beheren en toegang tot van uw DSVM.

tooadminister uw Azure-abonnement en cloud-resources kunt u de browser en punt toothe [Azure-portal](https://portal.azure.com). U kunt ook Azure Powershell tooadminister uw Azure-abonnement en resources via een script.
U kunt Azure Powershell uitvoeren vanaf een snelkoppeling op Hallo bureaublad of op Hallo start menu met de titel 'Microsoft Azure Powershell'. Raadpleeg [documentatie voor Microsoft Azure Powershell](../powershell-azure-resource-manager.md) voor meer informatie over hoe u uw Azure-abonnement en de resources met behulp van Windows Powershell-scripts kunt beheren.

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a>5. Uitbreiden van uw opslagruimte met een gedeelde bestandssysteem
Gegevenswetenschappers kunnen delen grote gegevenssets, code of andere bronnen in Hallo-team. Hallo DSVM zelf heeft 70GB beschikbare ruimte. tooextend uw opslag kunt u hello Azure File-Service en koppel deze aan Hallo DSVM of toegang tot dit via een REST-API.   

> [!NOTE]
> de maximale ruimte Hallo van hello Azure File Service share is 5TB en afzonderlijke maximale bestandsgrootte is 1TB.   
> 
> 

U kunt Azure Powershell toocreate een share Azure File Service gebruiken. Hier volgt Hallo script toorun onder Azure PowerShell toocreate een Azure-service bestandsshare.

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


Nu dat u een Azure-bestandsshare gemaakt hebt, kunt u deze koppelen in een virtuele machine in Azure. Het is raadzaam dat Hallo VM bevindt zich in dezelfde Azure-Datacenter als account Hallo-tooavoid opslaglatentie en gegevens overdracht kosten. Hier volgen Hallo opdrachten toomount Hallo station op Hallo DSVM die u op Azure Powershell uitvoeren kunt.

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


Nu kunt u dit station openen, net als een normale station op Hallo VM.

## <a name="6-share-code-with-your-team-using-github"></a>6. Code delen met uw team met behulp van GitHub
GitHub is een code-opslagplaats waar u een groot aantal voorbeeldcode en bronnen voor verschillende hulpprogramma's met behulp van verschillende technologieën die worden gedeeld door ontwikkelaars Hallo kunt vinden. Git gebruikt technologie tootrack en store-versie van codebestanden Hallo Hallo. GitHub is ook een platform waarin u uw eigen toostore opslagplaats kunt maken van uw team gedeelde code en -documentatie, versiebeheer en ook beheer die toegang tooview hebben en bijdragen code implementeren. Ga naar Hallo [GitHub help-pagina's](https://help.github.com/) voor meer informatie over het gebruik van Git. U kunt GitHub gebruiken als een van Hallo manieren toocollaborate met uw team, gebruik code die is ontwikkeld door Hallo-community en bijdragen code back toohello community.

Hallo DSVM komt al geladen met clienthulpprogramma's op zowel opdrachtregelprogramma als goed GUI tooaccess GitHub-opslagplaats. Hallo opdrachtregelprogramma toowork met Git en GitHub, Git Bash wordt genoemd. Visual Studio is geïnstalleerd op Hallo DSVM heeft Hallo Git-extensies. U vindt opstarten pictogrammen voor deze hulpprogramma's op Hallo startmenu en Hallo bureaublad.

toodownload code vanuit een GitHub-opslagplaats die u met Hallo ```git clone``` opdracht. Bijvoorbeeld toodownload wetenschappelijke gegevensopslagplaats gepubliceerd door Microsoft in de huidige map Hallo kunt uitvoeren Hallo opdracht volgen wanneer u naar ```git-bash```.

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

In Visual Studio, kunt u doen Hallo dezelfde kloonbewerking. Hallo na schermafbeelding ziet u hoe tooaccess Git en GitHub in Visual Studio tools.

![GIT in Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

U vindt meer informatie over het gebruik van Git toowork met uw GitHub-opslagplaats van verschillende bronnen beschikbaar zijn op github.com. Hallo [referentieoverzicht](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is een nuttig verwijzing.

## <a name="7-access-various-azure-data-and-analytics-services"></a>7. Toegang krijgen tot diverse Azure services voor gegevens en analyse
### <a name="azure-blob"></a>Azure Blob
Azure-blob is een betrouwbare, voordelige cloudopslag voor gegevens van grote of kleine. Laat het ons bekijken hoe kunt u gegevens tooAzure Blob en toegang tot gegevens die zijn opgeslagen in een Azure-Blob verplaatsen.

**Vereiste**

* **Maken van uw Azure Blob storage-account van [Azure-portal](https://portal.azure.com).**

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Bevestig dat Hallo vooraf worden geïnstalleerd vanaf de opdrachtregel AzCopy hulpprogramma bevindt zich in ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```. Wanneer dit hulpprogramma wordt uitgevoerd, kunt u Hallo met Hallo azcopy.exe tooyour pad omgeving variabele tooavoid typen Hallo volledige opdracht mappad toevoegen. Voor meer informatie over AzCopy hulpprogramma Raadpleeg te[documentatie van AzCopy](../storage/common/storage-use-azcopy.md)
* Hallo-hulpprogramma voor Azure Storage Explorer starten. Kan worden gedownload vanaf [Microsoft Azure Storage Explorer](http://storageexplorer.com/). 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

**Gegevens verplaatsen van virtuele machine tooAzure Blob: AzCopy**

toomove gegevens tussen uw lokale bestanden en de blob-opslag, u kunt AzCopy gebruiken in een opdrachtregel of PowerShell:

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

Vervang **C:\myfolder** toohello pad waar het bestand wordt opgeslagen, **mystorageaccount** tooyour blob opslagaccountnaam, **mycontainer** toohello containernaam, **opslagaccountsleutel** tooyour blob toegangssleutel voor opslag. U vindt de referenties van het opslagaccount in [Azure-portal](https://portal.azure.com).

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

AzCopy-opdracht uitvoeren in PowerShell of vanaf een opdrachtprompt. Hier volgt een voorbeeld van syntaxis van AzCopy-opdracht:

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



Nadat u uw AzCopy-opdracht toocopy tooan Azure blob ziet u dat het bestand wordt weergegeven in Azure Storage Explorer binnenkort uitvoeren.

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

**Gegevens verplaatsen van virtuele machine tooAzure Blob: Azure Opslagverkenner**

U kunt ook gegevens uit het lokale bestand Hallo uploaden in uw virtuele machine met behulp van Azure Storage Explorer:

* tooupload tooa gegevenscontainer, selecteer Hallo doel container en klikt u op Hallo **uploaden** knop.![ In Opslagverkenner uploaden](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)
* Klik op Hallo **...**  toohello rechts van Hallo **bestanden** tooupload voor een of meerdere bestanden van het bestandssysteem Hallo optie en klik op **uploaden** toobegin Hallo-bestanden te uploaden.![ Uploaden van bestanden tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)

**Gegevens lezen uit Azure Blob: leesmodule Machine Learning**

In Azure Machine Learning Studio kunt u een **gegevens importeren-module** tooread gegevens van uw blob.

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

**Gegevens lezen uit Azure Blob: Python ODBC**

U kunt **BlobService** bibliotheek tooread gegevens direct vanuit de blobs in een Jupyter-Notebook of Python.

Vereiste pakketten eerst importeren:

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

Vervolgens worden in de referenties van uw Azure Blob-account en gegevens uit Blob lezen:

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

Hallo gegevens gelezen als een gegevensframe:

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a>Azure Data Lake
Azure Data Lake Storage is een opslagplaats hyperschaal voor big data-analyses workloads en compatibel is met Hadoop Distributed File System (HDFS). Deze werkt met Hallo Hadoop-ecosysteem en hello Azure Data Lake Analytics. Laten we zien hoe u kunt gegevens in Azure Data Lake Store Hallo verplaatsen en uitvoeren van analytics met Azure Data Lake Analytics.

**Vereiste**

* Maken van uw Azure Data Lake Analytics in [Azure-portal](https://portal.azure.com).

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* Hallo **Azure Data Lake Tools** in **Visual Studio** gevonden op deze [koppeling](https://www.microsoft.com/download/details.aspx?id=49504) op Hallo Visual Studio Community Edition op Hallo virtuele machine al is geïnstalleerd. Na het starten van de Visual Studio en logboekregistratie in uw Azure-abonnement, ziet u uw Azure Data Analytics-account en de opslag in Hallo linkerpaneel van Visual Studio.

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

**Gegevens verplaatsen van virtuele machine tooData Lake: Azure Data Lake Explorer**

U kunt **Azure Data Lake Explorer** tooupload gegevens van lokale bestanden in de opslag van uw virtuele Machine tooData Lake Hallo.

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

U kunt ook maken een pijplijn gegevens tooproductionize uw data movement tooor van Azure Data Lake Hallo met [Azure gegevens Factory(ADF)](https://azure.microsoft.com/services/data-factory/). Verwijzen we u toothis [artikel](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide die u via Hallo stappen toobuild Hallo gegevens pijplijnen.

**Gegevens lezen uit Azure Blob tooData Lake: U-SQL**

Als uw gegevens zich in Azure Blob-opslag bevindt, kunt u gegevens rechtstreeks lezen van Azure storage-blob in U-SQL-query. Controleer of dat uw blob storage-account is gekoppeld tooyour Azure Data Lake voordat het samenstellen van de U-SQL-query. Ga te**Azure-portal**, zoeken van uw Azure Data Lake Analytics-dashboard, klikt u op **gegevensbron toevoegen**, opslagtype te selecteren**Azure Storage** en sluit in uw Azure-opslag Naam en sleutel. U bent vervolgens kunnen tooreference Hallo opgeslagen gegevens in Hallo storage-account.

![Voer storage-account en een sleutel](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

U kunt in Visual Studio-gegevens lezen uit blob storage, worden bepaalde gegevensmanipulatie, de functie-engineering, en de uitvoer Hallo resulterende gegevens tooeither Azure Data Lake of Azure Blob Storage. Wanneer u verwijst naar gegevens in blob storage hello, gebruiken **wasb: / /**; wanneer u verwijst naar Hallo-gegevens in Azure Data Lake gebruik **swbhdfs: / /**

![Gegevensframe](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

U kunt Hallo volgende U-SQL-query's in Visual Studio:

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



Nadat de query verzonden toohello server is, wordt een diagram Hallo status van de taak die weergegeven.

![Diagram van de status van taak](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

**Opvragen van gegevens in Data Lake: U-SQL**

Nadat het Hallo-gegevensset wordt ingenomen in Azure Data Lake, kunt u [U-SQL-taal](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery Hallo gegevens en verkennen. U-SQL-taal is vergelijkbaar tooT-SQL, maar sommige functies van C# combineert zodat gebruikers aangepaste modules, gebruiker gedefinieerde functies en enzovoort schrijven kunnen. U kunt Hallo-scripts in de vorige stap hello gebruiken.

Nadat het Hallo-query is verzonden tooserver, tripdata_summary. CSV vindt u enkele ogenblikken in **Azure Data Lake Explorer**, u mogelijk een voorbeeld Hallo-gegevens door met de rechtermuisknop op Hallo-bestand.

![Bestand in Azure Data Lake Explorer](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

toosee hello bestandsgegevens:

![Samenvatting](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a>HDInsight Hadoop-Clusters
Azure HDInsight is een beheerde Apache Hadoop, Spark, HBase en Storm-service op Hallo cloud. U kunt eenvoudig werken met Azure HDInsight-clusters van Hallo gegevens wetenschappelijke virtuele machine.

**Vereiste**

* Maken van uw Azure Blob storage-account van [Azure-portal](https://portal.azure.com). Dit opslagaccount wordt gebruikt toostore gegevens voor HDInsight-clusters.

![Azure Blob storage-account maken](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Azure HDInsight Hadoop-Clusters van aanpassen [Azure-portal](machine-learning-data-science-customize-hadoop-cluster.md)
  
  * Hallo storage-account is gemaakt met uw HDInsight-cluster wanneer deze wordt gemaakt, moet u koppelen. Dit opslagaccount wordt gebruikt voor toegang tot gegevens die kunnen worden verwerkt binnen Hallo-cluster.

![Koppeling toostorage account is gemaakt met HDInsight-cluster](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* U moet inschakelen **RAS** toohello hoofdknooppunt van Hallo cluster nadat deze is gemaakt. Houd er rekening mee Hallo RAS-referenties die u hier opgeeft (anders dan die zijn opgegeven voor de cluster Hallo bij het maken ervan): u nodig hebt in de volgende procedure Hallo.

![Externe toegang inschakelen](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* Maak een Azure Machine Learning-werkruimte. Uw Machine Learning-experimenten worden opgeslagen in deze Machine Learning-werkruimte. Hallo gemarkeerd opties selecteren in de Portal, zoals wordt weergegeven in de volgende schermafbeelding Hallo:

![Een Azure Machine Learning-werkruimte maken](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* Voer vervolgens Hallo parameters voor uw werkruimte

![Geef parameters van Machine Learning-werkruimte](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* Uploaden van gegevens met behulp van de IPython Notebook. Eerst vereiste pakketten te importeren, plug-referenties, een database maken in uw opslagaccount en laden van gegevens tooHDI clusters.

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* Ook kunt u dit [scenario](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC Taxi gegevens tooHDI cluster. Belangrijke stappen omvatten:
  
  * AzCopy: gecomprimeerde CSV downloaden van de lokale map voor openbare blob-tooyour
  * AzCopy: uitgepakte CSV's van de lokale map tooHDI cluster uploaden
  * Meld u aan bij de hoofdknooppunt Hallo van Hadoop-cluster en bereid voor experimentele data-analyse

Nadat het Hallo-gegevens zijn geladen tooHDI cluster, kunt u uw gegevens in Azure Storage Explorer controleren. En u hebt een database nyctaxidb in HDI-cluster gemaakt.

**Gegevensverkenning: Hive-query's in Python**

Omdat Hallo gegevens zich in de Hadoop-cluster, kunt u Hallo pyodbc pakket tooconnect tooHadoop Clusters en Hive toodo exploratie en functie-engineering met query uitvoeren op database. Hallo bestaande tabellen die in Hallo vereiste stap is gemaakt, kunt u weergeven.

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Bestaande tabellen weergeven](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

Bekijk het aantal records dat in elke maand en het Hallo frequenties van Hallo Gekantelde of niet Hallo reis tabel:

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Grafische voorstelling van het aantal records in elke maand](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![Grafiek van de frequenties tip](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

We kunnen ook compute Hallo afstand tussen ophalen locatie en dropoff locatie en vergelijk dit toohello krachtvoertuigen afstand.

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Tabel ophalen en dropoff](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Grafiek van ophalen/dropoff afstand tootrip afstand](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

Nu gaan we een (% 1) omlaag actieve set van gegevens voorbereiden voor modellering. We kunnen deze gegevens gebruiken in Machine Learning-leesmodule.

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

Na enige tijd ziet u Hallo gegevens zijn geladen in Hadoop-clusters:

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Tabel met gegevens](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

**Gegevens lezen uit HDI met Machine Learning: leesmodule**

U kunt ook Hallo **lezer** module in Machine Learning Studio tooaccess Hallo-database in Hadoop-cluster. Plug-in Hallo referenties van uw HDI-clusters en Azure Storage-Account tooenable ing machine learning-modellen met database in HDI-clusters bouwen.

![Eigenschappen van de module Reader](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

Hallo kan scored gegevensset vervolgens worden weergegeven:

![Scored gegevensset weergeven](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a>Azure SQL Data Warehouse & databases
Azure SQL Data Warehouse is een elastische datawarehouse als een service met SQL Server-ervaring bedrijfsniveau.

U kunt uw Azure SQL Data Warehouse inrichten door Hallo instructies in dit [artikel](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md). Nadat u uw Azure SQL Data Warehouse inricht, kunt u dit [scenario](machine-learning-data-science-process-sqldw-walkthrough.md) toodo het uploaden van gegevens, exploratie en modellering met behulp van gegevens binnen Hallo SQL Data Warehouse.

#### <a name="azure-cosmos-db"></a>Azure Cosmos DB
Azure Cosmos-database is een NoSQL-database in de cloud Hallo. Dit kunt u toowork met zoals JSON-documenten en kunt u toostore en query Hallo-documenten.

U moet toodo Hallo volgende per vereisten stappen tooaccess Azure Cosmos DB uit Hallo DSVM.

1. DocumentDB Python SDK installeren (uitvoeren ```pip install pydocumentdb``` vanaf een opdrachtprompt)
2. Maak een Azure DB die Cosmos-account en een database van [Azure-portal](https://portal.azure.com)
3. 'Azure Cosmos DB hulpprogramma voor migratie' downloaden van [hier](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) en pak tooa directory van uw keuze
4. Importeren van JSON-gegevens (Vulkaan gegevens) opgeslagen op een [openbare blob](https://cahandson.blob.core.windows.net/samples/volcano.json) in Cosmos-database met de volgende opdracht parameters toohello hulpprogramma voor migratie (dtui.exe uit Hallo directory waarin u Hallo Cosmos-hulpprogramma voor migratie van DB hebt geïnstalleerd). Geef de bron en doel locatie Hallo met deze parameters:
   
    /s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/; AccountKey = [[sleutel]; Database = Vulkaan /t.Collection:volcano1

Zodra u Hallo gegevens importeert, kunt u gaan tooJupyter en open Hallo notebook met de titel *DocumentDBSample* die python bevat tooaccess DocumentDB code en voer enkele eenvoudige opvragen. U meer informatie over Cosmos DB via Hallo service [documentatiepagina](https://docs.microsoft.com/azure/cosmos-db/).

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a>8. Maak rapporten en een dashboard met Power BI Desktop Hallo
Laat het ons Hallo Vulkaan JSON-bestand dat we eerder in het voorgaande voorbeeld van de Cosmos-DB in Power BI toogain visual inzicht in gegevens Hallo Hallo visualiseren. Gedetailleerde stappen zijn beschikbaar in Hallo [Power BI-artikel](../cosmos-db/powerbi-visualize.md). Hier volgen de hoofdstappen Hallo:

1. Power BI Desktop openen en "Get-Data" doen. Geef de URL Hallo als: https://cahandson.blob.core.windows.net/samples/volcano.json
2. U ziet Hallo JSON records zijn geïmporteerd als een lijst
3. Hallo lijst tooa tabel converteren zodat Power BI met Hallo dezelfde werken kunt
4. Vouw Hallo kolommen door te klikken op Hallo Uitvouwpictogram (hello een met Hallo 'pijl-links en een pijl naar rechts'-pictogram op Hallo van Hallo kolom)
5. U ziet dat de locatie een veld '-Record is. Vouw Hallo record en selecteert u alleen Hallo coördinaten. Coördinaat is een lijstkolom
6. Een nieuwe kolom tooconvert Hallo lijst coördinaat kolom toevoegen in door komma's gescheiden LatLong kolom Hallo twee elementen in coördinaat lijstveld Hallo Hallo formule met cookievalidatie ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.
7. Ten slotte converteren Hallo ```Elevation``` kolom tooDecimal en selecteer Hallo **sluiten** en **toepassen**.

In plaats van de vorige stappen, u kunt plakken Hallo na de code die Hallo stappen uit die zijn gebruikt in scripts Hallo geavanceerde Editor in Power BI waarmee u toowrite Hallo gegevenstransformaties in een querytaal.

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



U hebt nu Hallo gegevens in uw Power BI-gegevensmodel. Uw Power BI-bureaublad ziet er als volgt:

![Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

U kunt beginnen met opbouwen van rapporten en visualisaties met Hallo-gegevensmodel. U kunt Hallo stappen in deze [Power BI-artikel](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild een rapport. Hallo eindresultaat is een rapport dat op Hallo volgende lijkt.

![Power BI Desktop rapportweergave - Power BI-connector](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a>9. Dynamisch schalen uw DSVM toomeet die behoeften van uw project
U kunt schalen omhoog en omlaag Hallo DSVM toomeet die behoeften van uw project. Als u geen toouse Hallo VM in Hallo 's avonds of in het weekend, kunt u alleen afsluiten Hallo VM van Hallo [Azure-portal](https://portal.azure.com).

> [!NOTE]
> U kosten compute als u alleen Hallo besturingssysteem knop op Hallo VM.  
> 
> 

Als u meer capaciteit van CPU, geheugen of schijfruimte hebt en toohandle een grootschalige analyse moet vindt u een groot aantal VM-grootten in termen van CPU-kernen, geheugencapaciteit en schijftypen (inclusief Solid-State-schijven) en die voldoen aan uw berekenings- en de behoeften. Hallo volledige lijst met VM's samen met de Uurlijkse compute prijscategorie is beschikbaar op Hallo [prijzen van Azure virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/) pagina.

Op dezelfde manier als uw behoefte VM verwerkingscapaciteit vermindert (bijvoorbeeld: u verplaatst van een primaire werkbelasting tooa Hadoop of een Spark-cluster), kunt u Hallo-cluster met Hallo terugschroeven [Azure-portal](https://portal.azure.com) en toohello-instellingen van uw virtuele machine te gaan exemplaar. Hier volgt een schermafbeelding.

![Instellingen voor VM-exemplaar](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a>10. Extra hulpprogramma's installeren op de virtuele machine
We hebben verschillende hulpprogramma's die we zijn ervan overtuigd kunnen tooaddress veel Hallo algemene gegevens analytics behoeften en die moeten bespaart u tijd door te vermijden dat tooinstall en configureer uw omgevingen één voor één en u betaalt alleen voor resources die u geld besparen zijn verpakt gebruik.

U kunt gebruikmaken van andere Azure-gegevens en services analytics-profiel in dit artikel tooenhance uw analytics-omgeving. We begrijpen dat in sommige gevallen de behoeften van uw mogelijk extra hulpprogramma's, waaronder sommige eigen hulpprogramma's van derden. U hebt volledige beheerderstoegang op Hallo virtuele machine tooinstall nieuwe hulpmiddelen die u nodig. U kunt ook extra pakketten installeren in Python en R die niet vooraf zijn geïnstalleerd. Voor Python gebruikt u een ```conda``` of ```pip```. Voor R kunt u Hallo ```install.packages()``` in Hallo R-console of Hallo IDE gebruiken en kies '**pakketten** -> **installatiepakketten...** ".

## <a name="summary"></a>Samenvatting
Dit zijn slechts enkele Hallo dingen die u op Hallo Microsoft Data wetenschappelijke virtuele Machine doen kunt. Er zijn veel meer kunt u dingen doen toomake deze een effectieve analytics-omgeving.

