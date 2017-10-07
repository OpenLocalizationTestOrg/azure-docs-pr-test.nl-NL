---
title: aaaPython Flask web application zelfstudie voor Azure Cosmos DB | Microsoft Docs
description: Bekijk een databasezelfstudie over het gebruik van Azure DB die Cosmos toostore en toegang tot gegevens uit een Python Flask-webtoepassing gehost op Azure. Oplossingen voor het ontwikkelen van toepassingen zoeken.
keywords: Toepassingsontwikkeling, python flask, python-webtoepassing, python-webontwikkeling
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a>Een Python Flask-webtoepassing bouwen met Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Deze zelfstudie leert u hoe toouse Azure Cosmos DB toostore en toegang tot gegevens uit een Python-webtoepassing gehost op Azure en wordt ervan uitgegaan dat u hebt enige ervaring met behulp van Python en Azure websites.

In deze zelfstudie komen de volgende onderwerpen aan bod:

1. Maken en inrichten van een Cosmos-DB-account.
2. Maken van een Python Flask-toepassing.
3. Verbinding maken met behulp van de Cosmos-DB van uw webtoepassing tooand.
4. Hallo web application tooAzure wordt geïmplementeerd.

Door deze zelfstudie te volgen, bouwt u een eenvoudige stemtoepassing waarmee u toovote voor een poll.

![Schermopname van het Hallo-stemtoepassing is gemaakt met deze databasezelfstudie](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a>Vereisten voor de databasezelfstudie
Voordat u Hallo-instructies in dit artikel uitvoert, moet u ervoor zorgen dat er Hallo volgende zijn geïnstalleerd:

* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.
 
    OF 

    Een lokale installatie van Hallo [Azure Cosmos DB Emulator](local-emulator.md).
* [Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).  
* [Python-Tools voor Visual Studio](https://github.com/Microsoft/PTVS/).  
* [Microsoft Azure SDK voor Python 2.7](https://azure.microsoft.com/downloads/). 
* [Python 2.7.13](https://www.python.org/downloads/windows/). 

> [!IMPORTANT]
> Als u Python 2.7 voor Hallo eerst installeert, zorg ervoor dat in het welkomstscherm aanpassen Python 2.7.13, u selecteert **python.exe tooPath toevoegen**.
> 
> ![Schermopname van het welkomstscherm van aanpassen Python 2.7.11, waar u tooselect Add python.exe tooPath nodig](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* [Microsoft Visual C++ Compiler voor Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a>Stap 1: een Azure Cosmos DB-databaseaccount maken
Begin met het maken van een Cosmos DB-account. Als u al een account hebt of als u Azure Cosmos DB Emulator Hallo voor deze zelfstudie, kunt u overslaan te[stap 2: Maak een nieuwe Python Flask-webtoepassing](#step-2-create-a-new-python-flask-web-application).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
Er wordt nu zien hoe een nieuwe Python Flask-toepassing hello toocreate up gemalen.

## <a name="step-2-create-a-new-python-flask-web-application"></a>Stap 2: een nieuwe Python Flask-webtoepassing maken
1. In Visual Studio op Hallo **bestand** menu te verwijzen**nieuw**, en klik vervolgens op **Project**.
   
    Hallo **nieuw Project** dialoogvenster wordt weergegeven.
2. Vouw in het linkerdeelvenster hello, **sjablonen** en vervolgens **Python**, en klik vervolgens op **Web**. 
3. Selecteer **Flask-webproject** in het middelste deelvenster Hallo en klik vervolgens in Hallo **naam** vak type **zelfstudie**, en klik vervolgens op **OK**. Houd er rekening mee dat Python-pakketnamen alleen kleine letters bevatten, zijn moeten zoals beschreven in Hallo [stijlgids voor Python-Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).
   
    Voor deze nieuwe tooPython Flask is een ontwikkelframework voor webtoepassingen waarmee u sneller webtoepassingen in Python bouwen.
   
    ![Schermopname van het venster van de Hallo-nieuw Project in Visual Studio met Python gemarkeerd op Hallo links, Python Flask-webproject is geselecteerd in Hallo midden en Hallo naam tutorial in het naamvak Hallo](./media/documentdb-python-application/image9.png)
4. In Hallo **Python-Tools voor Visual Studio** venster, klikt u op **installeren in een virtuele omgeving**. 
   
    ![Schermopname van het Hallo-databasezelfstudie - Python-Tools voor Visual Studio-venster](./media/documentdb-python-application/python-install-virtual-environment.png)
5. In Hallo **virtuele omgeving toevoegen** venster kunt u Hallo standaardinstellingen accepteren en Python 2.7 als basisomgeving hello gebruiken, omdat PyDocumentDB biedt momenteel geen ondersteuning voor Python 3.x en klik vervolgens op **maken**. Hiermee stelt u Hallo vereiste virtuele Python-omgeving voor uw project.
   
    ![Schermopname van het Hallo-databasezelfstudie - Python-Tools voor Visual Studio-venster](./media/documentdb-python-application/image10_A.png)
   
    Hallo venster uitvoer `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` wanneer Hallo-omgeving is geïnstalleerd.

## <a name="step-3-modify-hello-python-flask-web-application"></a>Stap 3: Hallo Python Flask-webtoepassing wijzigen
### <a name="add-hello-python-flask-packages-tooyour-project"></a>Hallo Python Flask-pakketten tooyour project toevoegen
Nadat uw project is ingesteld, moet u tooadd Hallo vereiste Flask-pakketten tooyour project, inclusief pydocumentdb, Hallo Python-pakket voor DocumentDB.

1. Open in Solution Explorer Hallo-bestand met de naam **requirements.txt** en vervang Hallo inhoud door Hallo volgende:
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. Hallo opslaan **requirements.txt** bestand. 
3. Klik in Solution Explorer met de rechtermuisknop op **env** en klik op **Install from requirements.txt** (Installeren vanuit requirements.txt).
   
    ![Schermopname waarin env (Python 2.7) met installeren vanuit requirements.txt gemarkeerd in de lijst Hallo geselecteerd](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    Na de installatie is voltooid wordt het uitvoervenster Hallo Hallo volgende:
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > In zeldzame gevallen ziet u mogelijk een fout in het uitvoervenster Hallo. Als dit gebeurt, Controleer of Hallo fout gerelateerde toocleanup. Soms Hallo opschonen mislukt, maar Hallo-installatie is nog steeds geslaagd (omhoog schuiven in Hallo uitvoer venster tooverify dit). U kunt uw installatie controleren door [controleren Hallo virtuele omgeving](#verify-the-virtual-environment). Als het Hallo-installatie is mislukt, maar Hallo controle is geslaagd, is het OK toocontinue.
   > 
   > 

### <a name="verify-hello-virtual-environment"></a>Controleer of de virtuele omgeving Hallo
Zorg ervoor dat alles juist is geïnstalleerd.

1. Hallo-oplossing bouwen door te drukken **Ctrl**+**Shift**+**B**.
2. Wanneer Hallo opbouwbewerking is voltooid, beginnen met het Hallo-website door te drukken **F5**. Dit start Hallo Flask-ontwikkelaarsserver en uw webbrowser gestart. U ziet Hallo na pagina.
   
    ![Hallo lege Python Flask webontwikkelingsproject in een browser](./media/documentdb-python-application/image12.png)
3. Stop de foutopsporing Hallo website door te drukken **Shift**+**F5** in Visual Studio.

### <a name="create-database-collection-and-document-definitions"></a>Database-, verzamelings- en documentdefinities maken
U kunt nu de stemtoepassing maken door nieuwe bestanden toe te voegen en andere bestanden bij te werken.

1. Klik in Solution Explorer met de rechtermuisknop op Hallo **zelfstudie** project, klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item**. Selecteer **lege Python-bestand** en Hallo bestandsnaam **forms.py**.  
2. Toevoegen Hallo na codebestand toohello forms.py en sla Hallo-bestand.

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a>Hallo vereist invoer tooviews.py toevoegen
1. Vouw in Solution Explorer Hallo **zelfstudie** map en open Hallo **views.py** bestand. 
2. Hallo na importeren instructies toohello bovenaan Hallo toevoegen **views.py** bestand en sla vervolgens Hallo-bestand. Deze PythonSDK Cosmos-database importeren en Hallo Flask-pakketten.
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a>De database, de verzameling en het document maken
* Nog steeds in **views.py**, Hallo na code toohello einde van bestand Hallo toevoegen. Dit zorgt voor het Hallo-database die wordt gebruikt door Hallo formulier maken. Hallo bestaande code in niet verwijderen **views.py**. Toe te voegen dit toohello end.

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a>De database, de verzameling en het document lezen en het formulier verzenden
* Nog steeds in **views.py**, Hallo na code toohello einde van bestand Hallo toevoegen. Dit zorgt voor het instellen van een formulier Hallo Hallo-database, verzameling en het document te lezen. Hallo bestaande code in niet verwijderen **views.py**. Toe te voegen dit toohello end.

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a>Hallo HTML-bestanden maken
1. Klik in Solution Explorer in Hallo **zelfstudie** map, rechts, klikt u op Hallo **sjablonen** map, klikt u op **toevoegen**, en klik vervolgens op **Nieuw Item**. 
2. Selecteer **HTML-pagina**, en klik vervolgens in Hallo naam vak type **create.html**. 
3. Herhaal stap 1 en 2 toocreate twee extra HTML-bestanden: results.html en vote.html.
4. Hallo code te volgen toevoegen**create.html** in Hallo `<body>` element. Er wordt een bericht weergegeven dat er een nieuwe database, een nieuwe verzameling en een nieuw document is gemaakt.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. Hallo code te volgen toevoegen**results.html** in Hallo `<body`> element. Hallo-resultaten van Hallo poll wordt weergegeven.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. Hallo code te volgen toevoegen**vote.html** in Hallo `<body`> element. Het Hallo poll wordt weergegeven en Hallo stemmen accepteert. Over het registreren van Hallo stemmen Hallo besturing overgegeven met tooviews.py waar we herkennen Hallo stem cast en Hallo document dienovereenkomstig toevoegen.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. In Hallo **sjablonen** map vervangen Hallo inhoud van **index.html** door Hallo volgende. Dit fungeert als Hallo landingspagina voor uw toepassing.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a>Een configuratiebestand toevoegen en wijzigen van Hallo \_ \_init\_\_.py
1. Klik in Solution Explorer met de rechtermuisknop op Hallo **zelfstudie** project, klikt u op **toevoegen**, klikt u op **Nieuw Item**, selecteer **lege Python-bestand**, en vervolgens bestand met de Hallo **config.py**. Dit configuratiebestand is nodig voor de formulieren in Flask. U kunt deze gebruiken tooprovide ook een geheime sleutel. Deze sleutel is echter niet nodig voor deze zelfstudie.
2. Voeg de volgende Hallo code tooconfig.py, moet u tooalter Hallo waarden van **DOCUMENTDB\_HOST** en **DOCUMENTDB\_sleutel** in de volgende stap Hallo.
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. In Hallo [Azure-portal](https://portal.azure.com/), navigeer toohello **sleutels** blade door te klikken op **Bladeren**, **Azure Cosmos DB Accounts**, dubbelklikt u op Hallo-naam Hallo toouse account en klik vervolgens op Hallo **sleutels** knop in Hallo **Essentials** gebied. In Hallo **sleutels** blade, kopie Hallo **URI** waarde en plak deze in Hallo **config.py** bestand als waarde voor Hallo Hallo **DOCUMENTDB\_HOST**  eigenschap. 
4. Terug in de Azure-portal, op Hallo Hallo **sleutels** blade kopie Hallo waarde Hallo **primaire sleutel** of Hallo **secundaire sleutel**, en plak deze in Hallo **config.py**  bestand als waarde voor Hallo Hallo **DOCUMENTDB\_sleutel** eigenschap.
5. In Hallo  **\_ \_init\_\_.py** bestand, Hallo volgt regel toevoegen. 
   
        app.config.from_object('config')
   
    Zodat Hallo inhoud van het Hallo-bestand is:
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. Na het toevoegen van alle Hallo bestanden er Solution Explorer als volgt uit:
   
    ![Schermopname van het Hallo Visual Studio Solution Explorer-venster](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a>Stap 4: de webtoepassing lokaal uitvoeren
1. Hallo-oplossing bouwen door te drukken **Ctrl**+**Shift**+**B**.
2. Wanneer Hallo opbouwbewerking is voltooid, beginnen met het Hallo-website door te drukken **F5**. Hallo hieronder ziet u op het scherm.
   
    ![Schermopname van Hallo Python + Azure Cosmos DB Stemtoepassing in een webbrowser](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. Klik op **maken/wissen Hallo Voting Database** toogenerate Hallo-database.
   
    ![Schermopname van het Hallo pagina maken van Hallo webtoepassing – ontwikkelingsgegevens](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. Klik vervolgens op **Vote** (Stemmen) en selecteer uw optie.
   
    ![Schermopname van het Hallo-webtoepassing met een vraag waarvoor kan worden gestemd](./media/documentdb-python-application/cosmos-db-vote.png)
5. Voor elke stem die u uitbrengt, wordt Hallo desbetreffende teller verhoogd.
   
    ![Schermopname van het Hallo resultaten van Hallo pagina met stemresultaten](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. Stop de foutopsporing voor Hallo project door op Shift + F5 te drukken.

## <a name="step-5-deploy-hello-web-application-tooazure"></a>Stap 5: Hallo web application tooAzure implementeren
Nu dat u Hallo volledige toepassing correct werkt met Cosmos DB hebt, zal deze tooAzure toodeploy.

1. Klik met de rechtermuisknop Hallo-project in Solution Explorer (Zorg ervoor dat u niet bent nog steeds lokaal wordt uitgevoerd) en selecteer **publiceren**.  
   
     ![Schermopname van Hallo geselecteerde zelfstudie in Solution Explorer met de optie publiceren Hallo gemarkeerd](./media/documentdb-python-application/image20.png)
2. In Hallo **publiceren** dialoogvenster, **Microsoft Azure App Service**, selecteer **nieuw**, en klik vervolgens op **publiceren**.
   
    ![Schermopname van Hallo webpublicatie venster met Microsoft Azure App Service is gemarkeerd](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. In Hallo **Create App Service** dialoogvenster Hallo- naam voor uw web-app samen met uw **abonnement**, **resourcegroep**, en **App Service-Plan** , klikt u vervolgens op **maken**.
   
    ![Schermopname van het Hallo Microsoft Azure Web Apps venster venster](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. Binnen een paar seconden zal Visual Studio publicatie van uw app service voltooien en een browser starten waarin u kunt zien uw werk in Azure wordt uitgevoerd!

    ![Schermopname van het Hallo Microsoft Azure Web Apps venster venster](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a>Problemen oplossen
Als dit Hallo eerste Python-app u hebt uitgevoerd op uw computer, controleert u of Hallo de volgende mappen (of gelijkwaardige installatielocaties voor Hallo) zijn opgenomen in de variabele PATH:

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

Als u een foutbericht weergegeven op de stempagina en u met de naam uw project iets anders dan **zelfstudie**, zorg ervoor dat  **\_ \_init\_\_.py** verwijzingen Hallo juiste projectnaam in Hallo regel: `import tutorial.view`.

## <a name="next-steps"></a>Volgende stappen
Gefeliciteerd. U hebt zojuist uw eerste Python-webtoepassing met behulp van de Cosmos-DB voltooid en tooAzure gepubliceerd.

Dit onderwerp wordt regelmatig bijgewerkt en verbeterd op basis van uw feedback.  Eenmaal u Hallo-zelfstudie hebt voltooid met Neem Hallo stemknoppen Hallo boven en onder aan deze pagina, en ervoor tooinclude uw feedback op welke verbeteringen toosee aangebracht gewenste. Als u graag toocontact u rechtstreeks kunt u gratis tooinclude je e-mailadres in uw opmerkingen.

tooadd aanvullende functionaliteit tooyour webtoepassing, bekijk Hallo beschikbare API's in Hallo [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).

Zie voor meer informatie over Azure, Visual Studio en Python Hallo [Python Developer Center](https://azure.microsoft.com/develop/python/). 

Zie voor aanvullende zelfstudies over Python Flask [hello Flask Mega-Tutorial, deel I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
