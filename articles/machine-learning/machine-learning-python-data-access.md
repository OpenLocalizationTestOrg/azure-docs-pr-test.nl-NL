---
title: aaaAccess gegevenssets met Machine Learning Python-clientbibliotheek | Microsoft Docs
description: Installeren en gebruiken Hallo Python client bibliotheek tooaccess en Azure Machine Learning gegevens veilig beheren vanuit een lokale Python-omgeving.
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a>Gegevenssets toegang met behulp van Python hello Azure Machine Learning Python-clientbibliotheek gebruiken
Hallo preview van Microsoft Azure Machine Learning Python-clientbibliotheek veilige toegang tooyour Azure Machine Learning gegevenssets van een lokale Python-omgeving kunt inschakelen en kunt Hallo maken en beheren van gegevenssets in een werkruimte.

In dit onderwerp bevat instructies over het:

* Hallo-clientbibliotheek voor Machine Learning Python installeren 
* toegang tot en gegevenssets heeft, inclusief aanwijzingen voor het uploaden tooget autorisatie tooaccess Azure Machine Learning gegevenssets van uw lokale omgeving voor Python
* toegang tot tussenliggende gegevenssets van experimenten
* Hallo Python client bibliotheek tooenumerate gegevenssets gebruiken, toegang tot metagegevens, lezen Hallo inhoud van een gegevensset, nieuwe gegevenssets maken en bijwerken van bestaande gegevenssets

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="prerequisites"></a>Vereisten
Hallo Python-clientbibliotheek is getest onder Hallo volgende omgevingen:

* Windows, Mac en Linux
* Python 2.7 3.3 en 3.4

Dit heeft een afhankelijkheid op hello-pakketten te volgen:

* Aanvragen
* Python-dateutil
* pandas

Wordt u aangeraden een Python-distributie, zoals [Anaconda](http://continuum.io/downloads#all) of [bladerdak](https://store.enthought.com/downloads/), die worden geleverd met Python, IPython en drie hello-pakketten die hierboven worden geïnstalleerd. Hoewel IPython niet strikt vereist is, is een geweldige omgeving voor het werken en gegevens interactief te visualiseren.

### <a name="installation"></a>Hoe tooinstall Hallo clientbibliotheek van Azure Machine Learning Python
Hello Azure Machine Learning Python-clientbibliotheek moet ook geïnstalleerde toocomplete Hallo taken die worden beschreven in dit onderwerp. Deze beschikbaar is via Hallo [Python Package Index](https://pypi.python.org/pypi/azureml). tooinstall uitvoeren in uw omgeving Python Hallo volgende opdracht uit uw lokale Python-omgeving:

    pip install azureml

U kunt ook downloaden en installeren vanuit Hallo bronnen op [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).

    python setup.py install

Als u git op deze computer geïnstalleerd hebt, kunt u pip tooinstall rechtstreeks vanuit Hallo git-opslagplaats:

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <a name="datasetAccess"></a>Studio Code codefragmenten tooaccess gegevenssets gebruiken
Hallo Python-clientbibliotheek biedt u toegang op programmeerniveau tooyour bestaande gegevenssets van experimenten die zijn uitgevoerd.

Vanuit de Hallo Studio webinterface kunt u codefragmenten die alle Hallo benodigde informatie toodownload opnemen en gegevenssets te deserialiseren als Pandas DataFrame objecten op uw machine locatie genereren.

### <a name="security"></a>Beveiliging voor toegang tot gegevens
Hallo codefragmenten geleverd door Studio voor gebruik met Hallo Python-clientbibliotheek uw werkruimte-id en -autorisatie bevat-token. Deze volledige toegang tooyour werkruimte bevatten en moeten worden beveiligd, zoals een wachtwoord.

Uit veiligheidsoverwegingen Hallo code codefragment functionaliteit is alleen beschikbaar toousers waarvoor hun rol is ingesteld als **eigenaar** voor Hallo-werkruimte. Uw rol in Azure Machine Learning Studio wordt weergegeven op Hallo **gebruikers** pagina onder **instellingen**.

![Beveiliging][security]

Als uw rol niet is ingesteld als **eigenaar**, kunt u toobe reinvited als eigenaar van een aanvraag, of vraag de eigenaar van de Hallo van Hallo werkruimte tooprovide u met de Hallo codefragment.

verificatietoken voor tooobtain hello, kunt u een van de volgende Hallo kunt doen:

* Vragen om een token van een eigenaar. Eigenaars hebben toegang tot hun autorisatie-tokens van Hallo instellingenpagina van de werkruimte in Studio. Selecteer **instellingen** van Hallo links deelvenster en klik op **AUTORISATIE TOKENS** toosee Hallo primaire en secundaire tokens.  Hoewel Hallo primaire of secundaire autorisatie-tokens Hallo kunnen worden gebruikt in het codefragment hello, wordt u aangeraden eigenaars delen alleen Hallo secundaire autorisatie-tokens.

![Autorisatie-tokens](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* Vraag toobe gepromoveerd toorole van eigenaar.  toodo dit, een huidige eigenaar van Hallo werkruimte behoeften toofirst worden verwijderd uit de werkruimte Hallo en vervolgens u opnieuw uit te nodigen tooit als eigenaar.

Als ontwikkelaars Hallo werkruimte-id en autorisatie hebt verkregen token, ze zijn kunnen tooaccess Hallo werkruimte met Hallo codefragment ongeacht hun rol.

Autorisatie-tokens worden beheerd op Hallo **AUTORISATIE TOKENS** pagina onder **instellingen**. U kunt ze genereren, maar deze procedure worden de vorige toegangstoken toohello ingetrokken.

### <a name="accessingDatasets"></a>Gegevenssets toegang vanuit een lokale Python-toepassing
1. Klik in Machine Learning Studio **GEGEVENSSETS** Hallo navigatiebalk aan de linkerkant Hallo aan.
2. Hallo gegevensset u tooaccess wilt selecteren. U kunt kiezen uit Hallo gegevenssets van Hallo **mijn GEGEVENSSETS** lijst of van Hallo **voorbeelden** lijst.
3. Hallo onderste werkbalk, klik op **toegangscode gegevens genereren**. Als Hallo gegevens in een indeling die incompatibel is met de Hallo Python-clientbibliotheek is, wordt deze knop is uitgeschakeld.
   
    ![Gegevenssets][datasets]
4. Hallo codefragment selecteren in Hallo-venster dat wordt weergegeven en tooyour Klembord kopiëren.
   
    ![Toegangscode][dataset-access-code]
5. Plak Hallo code in de notebook Hallo van uw lokale Python-toepassing.
   
    ![Notebook][ipython-dataset]

## <a name="accessingIntermediateDatasets"></a>Tussenliggende gegevenssets van de toegang van Machine Learning-experimenten
Nadat een experiment in Machine Learning Studio hello wordt uitgevoerd, is het mogelijk tooaccess Hallo tussenliggende gegevenssets van Hallo uitvoerknooppunten van modules. Tussenliggende gegevenssets zijn de gegevens die zijn gemaakt en gebruikt voor de tussenliggende stappen wanneer een model-hulpprogramma is uitgevoerd.

Tussenliggende gegevenssets toegankelijk zijn, zolang Hallo gegevensindeling compatibel met Hallo Python-clientbibliotheek is.

Hallo volgende indelingen worden ondersteund (constanten voor deze zich in Hallo `azureml.DataTypeIds` klasse):

* Tekst zonder opmaak
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

U kunt Hallo indeling bepalen door de muiswijzer op een knooppunt van de uitvoer module. Deze wordt samen met de naam van het Hallo knooppunt, in de knopinfo weergegeven.

Aantal Hallo-modules, zoals Hallo [gesplitste] [ split] module met de naam de indeling van de uitvoer tooa `Dataset`, die niet wordt ondersteund door Hallo Python-clientbibliotheek.

![Indeling van de gegevensset][dataset-format]

Moet u een module conversie toouse zoals [converteren tooCSV][convert-to-csv], tooget uitvoer naar een ondersteunde indeling.

![GenericCSV-indeling][csv-format]

Hallo ziet volgende stappen een voorbeeld van een experiment maakt, worden uitgevoerd en heeft toegang tot de tussenliggende Hallo-gegevensset.

1. Een nieuw experiment maken.
2. Voeg een **volwassenen inventarisering Income binaire classificatie gegevensset** module.
3. Plaats een [gesplitste] [ split] module en verbinding maken met de invoer toohello gegevensset module uitvoer.
4. Voeg een [tooCSV converteren] [ convert-to-csv] module en verbinding maken met de invoer tooone Hallo [gesplitste] [ split] module levert.
5. Hallo-experiment opslaan, uitvoeren en wacht totdat deze toofinish uitgevoerd.
6. Klik op Hallo uitvoer knooppunt op Hallo [converteren tooCSV] [ convert-to-csv] module.
7. Wanneer het Hallo-contextmenu wordt weergegeven, selecteert u **toegangscode gegevens genereren**.
   
    ![Contextmenu][experiment]
8. Hallo-codefragment Selecteer en kopieer het tooyour Klembord vanuit Hallo-venster dat wordt weergegeven.
   
    ![Toegangscode][intermediate-dataset-access-code]
9. Hallo-code plakken in uw laptop.
   
    ![Notebook][ipython-intermediate-dataset]
10. U kunt Hallo gegevens visualiseren met matplotlib. Hiermee wordt in een kolom van de leeftijd Hallo histogram:
    
    ![Histogram][ipython-histogram]

## <a name="clientApis"></a>Gebruik Hallo Machine Learning Python client bibliotheek tooaccess lezen, maken en beheren van gegevenssets
### <a name="workspace"></a>Werkruimte
Hallo-werkruimte is Hallo toegangspunt voor Hallo Python-clientbibliotheek. Hallo bieden `Workspace` klasse met uw werkruimte-id en autorisatie token toocreate een exemplaar:

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a>Gegevenssets opsommen
tooenumerate alle gegevenssets in een bepaalde werkruimte:

    for ds in ws.datasets:
        print(ds.name)

tooenumerate alleen Hallo gebruiker gemaakte gegevenssets:

    for ds in ws.user_datasets:
        print(ds.name)

tooenumerate alleen Hallo voorbeeld gegevenssets:

    for ds in ws.example_datasets:
        print(ds.name)

U kunt toegang krijgen tot een gegevensset met de naam (dit is hoofdlettergevoelig):

    ds = ws.datasets['my dataset name']

Of u toegang hebt tot het met de index:

    ds = ws.datasets[0]


### <a name="metadata"></a>Metagegevens
Gegevenssets hebben metagegevens, in aanvulling toocontent. (Tussenliggende gegevenssets zijn een uitzonderingsregel toothis en hoeft niet alle metagegevens.)

Sommige metagegevenswaarden worden toegewezen door gebruiker Hallo tijdens het maken:

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

Sommige zijn toegewezen door Azure ML waarden:

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

Zie Hallo `SourceDataset` klasse voor meer op Hallo beschikbaar metagegevens.

### <a name="read-contents"></a>Inhoud lezen
Hallo codefragmenten geleverd door Machine Learning Studio automatisch downloaden en te deserialiseren Hallo gegevensset tooa Pandas DataFrame object. Dit wordt gedaan met Hallo `to_dataframe` methode:

    frame = ds.to_dataframe()

Als u liever toodownload Hallo onbewerkte gegevens en uitvoeren van Hallo deserialisatie, is dat een optie. Momenteel Hallo is dit de enige optie Hallo voor indelingen zoals ARFF, welke Hallo Python-clientbibliotheek kan niet worden gedeserialiseerd.

tooread hello inhoud als tekst:

    text_data = ds.read_as_text()

Als binair tooread Hallo-inhoud:

    binary_data = ds.read_as_binary()

U kunt ook gewoon een stroom toohello inhoud openen:

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a>Maak een nieuwe gegevensset
Hallo Python-clientbibliotheek kunt u de gegevenssets tooupload uit een Python-programma. Deze gegevenssets zijn vervolgens beschikbaar voor gebruik in uw werkruimte.

Als u uw gegevens in een DataFrame Pandas hebt, gebruikt u Hallo code te volgen:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Als u al uw gegevens geserialiseerd, kunt u het volgende gebruiken:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Hallo Python-clientbibliotheek is kunnen tooserialize een Pandas DataFrame toohello volgende indelingen (constanten voor deze zich in Hallo `azureml.DataTypeIds` klasse):

* Tekst zonder opmaak
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

### <a name="update-an-existing-dataset"></a>Bijwerken van een bestaande gegevensset
Als u een nieuwe gegevensset met een naam die overeenkomt met een bestaande gegevensset tooupload probeert, ontvangt u een conflict opgetreden.

een bestaande gegevensset tooupdate, moet u eerst een bestaande gegevensset voor verwijzing toohello tooget:

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Gebruik vervolgens `update_from_dataframe` tooserialize en vervang Hallo-inhoud van Hallo gegevensset op Azure:

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Als u tooserialize hello tooa verschillende gegevensindeling wilt, een waarde opgeven voor optionele Hallo `data_type_id` parameter.

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

U kunt desgewenst een nieuwe beschrijving instellen door een waarde opgeeft voor Hallo `description` parameter.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

U kunt desgewenst een nieuwe naam instellen door een waarde opgeeft voor Hallo `name` parameter. U hebt op, Hallo gegevensset met alleen de nieuwe naam Hallo ophalen. Hallo code na updates Hallo gegevens, naam en beschrijving.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

Hallo `data_type_id`, `name` en `description` parameters zijn optioneel en de standaardinstellingen van de vorige waarde tootheir. Hallo `dataframe` parameter is altijd vereist.

Als u al uw gegevens geserialiseerd, gebruikt u `update_from_raw_data` in plaats van `update_from_dataframe`. Als u alleen doorgeeft in `raw_data` in plaats van `dataframe`, het op een vergelijkbare manier werkt.

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

