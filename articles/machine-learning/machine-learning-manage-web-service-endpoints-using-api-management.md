---
title: aaaLearn hoe toomanage AzureML web services met behulp van API Management | Microsoft Docs
description: Een handleiding die laat zien hoe toomanage AzureML web services met behulp van API Management.
keywords: machine learning api management
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a>Meer informatie over hoe toomanage AzureML web services met behulp van API Management
## <a name="overview"></a>Overzicht
Deze handleiding ontdekt u hoe tooquickly aan de slag met API Management toomanage AzureML-webservices.

## <a name="what-is-azure-api-management"></a>Wat is Azure API Management?
Azure API Management is een Azure-service waarmee u uw REST-API-eindpunten beheren door gebruikerstoegang, beperking en bewaking van het dashboard te definiëren. Klik op [hier](https://azure.microsoft.com/services/api-management/) voor meer informatie over Azure API Management. Klik op [hier](../api-management/api-management-get-started.md) handleiding over hoe tooget aan de slag met Azure API Management. Deze andere gids, die in deze handleiding is gebaseerd op, vindt meer onderwerpen, waaronder melding configuraties, laag prijzen, antwoord verwerking, gebruikersverificatie, producten, developer-abonnementen en gebruik dashboarding maken.

## <a name="what-is-azureml"></a>Wat is AzureML?
AzureML is een Azure-service voor machine learning waarmee u tooeasily build, implementeren en geavanceerde analyseoplossingen delen. Klik op [hier](https://azure.microsoft.com/services/machine-learning/) voor meer informatie over AzureML.

## <a name="prerequisites"></a>Vereisten
toocomplete deze handleiding, moet u:

* Een Azure-account. Als u geen Azure-account hebt, klikt u op [hier](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie over hoe u een gratis proefaccount toocreate.
* Een AzureML-account. Als u geen account voor met AzureML hebt, klikt u op [hier](https://studio.azureml.net/) voor meer informatie over hoe u een gratis proefaccount toocreate.
* Hallo-werkruimte, service en api_key voor een AzureML-experiment geïmplementeerd als een webservice. Klik op [hier](machine-learning-create-experiment.md) voor meer informatie over hoe een AzureML toocreate experimenteren. Klik op [hier](machine-learning-publish-a-machine-learning-web-service.md) voor meer informatie over hoe een AzureML toodeploy experimenteren als een webservice. Bijlage A bevat ook instructies voor hoe toocreate en test een eenvoudige AzureML experimenteren en als een webservice implementeren.

## <a name="create-an-api-management-instance"></a>Een API Management-exemplaar maken
Hieronder vindt Hallo stappen voor het gebruik van API Management toomanage uw AzureML-webservice. Maak eerst een service-exemplaar. Meld u bij toohello [klassieke Portal](https://manage.windowsazure.com/) en klik op **nieuw** > **App Services** > **API Management**  >  **Maken**.

![instantie maken](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

Geef een unieke **URL**. Maakt gebruik van deze handleiding **demoazureml** – u moet toochoose een ander. Kies Hallo gewenst **abonnement** en **regio** voor uw service-exemplaar. Nadat u uw selecties, klik op de knop voor volgende Hallo.

![maken van service 1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

Geef een waarde op voor Hallo **organisatienaam**. Maakt gebruik van deze handleiding **demoazureml** – u moet toochoose een ander. Voer uw e-mailadres in Hallo **e-mail beheerder** veld. Dit e-mailadres wordt gebruikt voor meldingen van Hallo API Management-systeem.

![maken van service 2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

Klik op Hallo selectievakje toocreate uw service-exemplaar. *Het duurt om toothirty minuten voor een nieuwe service toobe gemaakt*.

## <a name="create-hello-api"></a>Hallo-API maken
Zodra Hallo service-exemplaar is gemaakt, is de volgende stap Hallo toocreate Hallo API. Een API bestaat uit een reeks bewerkingen die vanuit een clienttoepassing kunnen worden aangeroepen. API-bewerkingen worden via proxy tooexisting webservices. Deze handleiding maakt API's die proxy toohello bestaande AzureML RRS en BES webservices.

API's worden gemaakt en geconfigureerd van Hallo API-publicatieportal, die wordt geopend via Hallo klassieke Azure-Portal. tooreach Hallo publisher portal, selecteer uw service-exemplaar.

![Selecteer-service-exemplaar](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

Klik op **beheren** in Hallo klassieke Azure-Portal voor uw API Management-service.

![beheren-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

Klik op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **API toevoegen**.

![menu-beheer-API](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

Type **AzureML Demo API** als Hallo **Web API-naam**. Type **https://ussouthcentral.services.azureml.net** als Hallo **webservice-URL**. Type **azureml-demo** als Hallo **achtervoegsel URL Web-API**. Controleer **HTTPS** als Hallo **URL Web-API** schema. Selecteer **Starter** als **producten**. Wanneer u klaar bent, klikt u op **opslaan** toocreate Hallo API.

![nieuwe-api toevoegen](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a>Hallo bewerkingen toevoegen
Klik op **toevoegbewerking** tooadd operations toothis API.

![toevoegen-bewerking](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

Hallo **nieuwe bewerking** venster wordt weergegeven en Hallo **handtekening** tabblad wordt standaard geselecteerd.

## <a name="add-rrs-operation"></a>RRS bewerking toevoegen
Maak eerst een bewerking voor Hallo AzureML RRS-service. Selecteer **POST** als Hallo **HTTP-term**. Type **/workspaces/ {werkruimte} /services/ {service} / execute? api-version = {apiversion} & details = {details}** als Hallo **URL sjabloon**. Type **RRS uitvoeren** als Hallo **weergavenaam**.

![rrs-bewerking-handtekening toevoegen](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

Klik op **antwoorden** > **toevoegen** op Hallo linker- en selecteer **200 OK**. Klik op **opslaan** toosave deze bewerking.

![toevoegen-rrs--bewerkingsantwoord](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a>BES bewerkingen toevoegen
Schermopnamen worden niet vermeld voor BES operations Hallo zoals ze vergelijkbaar toothose zijn voor het toevoegen van Hallo RRS-bewerking.

### <a name="submit-but-not-start-a-batch-execution-job"></a>Een taak Batchuitvoering verzenden (maar niet worden gestart)
Klik op **toevoegbewerking** tooadd hello AzureML BES bewerking toohello API. Selecteer **POST** voor Hallo **HTTP-term**. Type **/workspaces/ {werkruimte} /services/ {service} / taken? api-version = {apiversion}** voor Hallo **URL sjabloon**. Type **BES indienen** voor Hallo **weergavenaam**. Klik op **antwoorden** > **toevoegen** op Hallo linker- en selecteer **200 OK**. Klik op **opslaan** toosave deze bewerking.

### <a name="start-a-batch-execution-job"></a>Een taak Batchuitvoering starten
Klik op **toevoegbewerking** tooadd hello AzureML BES bewerking toohello API. Selecteer **POST** voor Hallo **HTTP-term**. Type **/workspaces/ {werkruimte} /services/ {service} /jobs/ {jobid} / starten? api-version = {apiversion}** voor Hallo **URL sjabloon**. Type **BES Start** voor Hallo **weergavenaam**. Klik op **antwoorden** > **toevoegen** op Hallo linker- en selecteer **200 OK**. Klik op **opslaan** toosave deze bewerking.

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a>Hallo status of het resultaat van een taak Batchuitvoering ophalen
Klik op **toevoegbewerking** tooadd hello AzureML BES bewerking toohello API. Selecteer **ophalen** voor Hallo **HTTP-term**. Type **/workspaces/ {werkruimte} /services/ {service} /jobs/ {jobid}? api-version = {apiversion}** voor Hallo **URL sjabloon**. Type **BES Status** voor Hallo **weergavenaam**. Klik op **antwoorden** > **toevoegen** op Hallo linker- en selecteer **200 OK**. Klik op **opslaan** toosave deze bewerking.

### <a name="delete-a-batch-execution-job"></a>Een taak Batchuitvoering verwijderen
Klik op **toevoegbewerking** tooadd hello AzureML BES bewerking toohello API. Selecteer **verwijderen** voor Hallo **HTTP-term**. Type **/workspaces/ {werkruimte} /services/ {service} /jobs/ {jobid}? api-version = {apiversion}** voor Hallo **URL sjabloon**. Type **BES verwijderen** voor Hallo **weergavenaam**. Klik op **antwoorden** > **toevoegen** op Hallo linker- en selecteer **200 OK**. Klik op **opslaan** toosave deze bewerking.

## <a name="call-an-operation-from-hello-developer-portal"></a>Een bewerking aanroepen vanuit Hallo-Portal voor ontwikkelaars
Bewerkingen rechtstreeks vanuit de ontwikkelaarsportal hello, waardoor een handige manier tooview kunnen worden aangeroepen en Hallo bewerkingen van een API testen. In deze handleiding stap u roept Hallo **RRS uitvoeren** methode die is toegevoegd toohello **AzureML Demo API**. Klik op **-portal voor ontwikkelaars** in Hallo Hallo menu rechts van de klassieke Portal Hallo top.

![portal voor ontwikkelaars](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

Klik op **API's** van Hallo bovenste menu en klik vervolgens op **AzureML Demo API** toosee Hallo bewerkingen die beschikbaar zijn.

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

Selecteer **RRS uitvoeren** voor Hallo-bewerking. Klik op **Try It**.

![Try it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

Aanvraagparameters, typt u uw **werkruimte**, **service**, **2.0** voor Hallo **apiversion**, en **waar**voor Hallo **details**. U vindt uw **werkruimte** en **service** in Hallo AzureML web servicedashboard (Zie **Hallo webservice testen** in bijlage A).

Aanvraagheaders, klikt u op **header toevoegen** en het type **Content-Type** en **application/json**, klikt u vervolgens op **header toevoegen** en het type  **Autorisatie** en **Bearer <YOUR AZUREML SERVICE API-KEY>** . U vindt uw **api-sleutel** in Hallo AzureML web servicedashboard (Zie **Hallo webservice testen** in bijlage A).

Type **{'Invoer': {"input1": {'ColumnNames': ["Col2"] "waarden": [[' Dit is een goede dag']]}}, "GlobalParameters": {}}** voor Hallo aanvraagtekst.

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

Klik op **verzenden**.

![Verzenden](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

Nadat een bewerking is aangeroepen, Hallo ontwikkelaarsportal hello **aangevraagde URL** van Hallo back-endservice, Hallo **antwoordstatus**, Hallo **antwoordheaders**, en er is een **antwoordinhoud**.

![status van het antwoord](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a>Bijlage A - maken en testen van een eenvoudige AzureML-webservice
### <a name="creating-hello-experiment"></a>Hallo-experiment maken
Hieronder vindt u Hallo stappen voor het maken van een eenvoudig experiment van AzureML en deze is geïmplementeerd als een webservice. web-service wordt als invoer een kolom van willekeurige tekst Hello en retourneert een reeks functies die worden weergegeven als gehele getallen zijn. Bijvoorbeeld:

| Tekst | Gecodeerde tekst |
| --- | --- |
| Dit is een goede dag |1 1 2 2 0 2 0 1 |

Eerst met een browser naar keuze, gaat u naar: [https://studio.azureml.net/](https://studio.azureml.net/) en voer uw referenties toolog in. Maak vervolgens een nieuw, leeg experiment.

![experiment-sjablonen voor het zoeken](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

Wijzig de naam ervan te**SimpleFeatureHashingExperiment**. Vouw **gegevenssets opgeslagen** en sleep **adresboek beoordelingen van Amazon** naar uw experiment.

![eenvoudige-functie-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

Vouw **Data Transformation** en **manipulatie** en sleep **Select Columns in Dataset** naar uw experiment. Verbinding maken met **adresboek beoordelingen van Amazon** te**Select Columns in Dataset**.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

Klik op **Select Columns in Dataset** en klik vervolgens op **Launch column selector** en selecteer **Col2**. Klik op Hallo vinkje tooapply deze wijzigingen.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

Vouw **Tekstanalyse** en sleep **hash-functie** op Hallo experiment. Verbinding maken met **Select Columns in Dataset** te**hash-functie**.

![verbinding maken met project kolommen](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

Type **3** voor Hallo **bitsize Hashing**. Hiermee maakt u 8 (23) kolommen.

![hashing bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

Op dit moment kunt u tooclick **uitvoeren** tootest Hallo experiment.

![uitvoeren](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a>Een webservice maken
Maak nu een webservice. Vouw **webservice** en sleep **invoer** naar uw experiment. Verbinding maken met **invoer** te**hash-functie**. Ook slepen **uitvoer** naar uw experiment. Verbinding maken met **uitvoer** te**hash-functie**.

![output-naar--hash-functies](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

Klik op **publiceren webservice**.

![publiceren-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

Klik op **Ja** toopublish Hallo experiment.

![Ja om te publiceren](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a>Hallo webservice testen
Een webservice AzureML bestaat uit RSS (aanvraag/antwoord-service) en eindpunten van BES (batch uitvoering service). RSS is voor synchrone uitvoering. BES is voor het uitvoeren van asynchrone taak. tootest uw web-service met de onderstaande Hallo voorbeeld Python-bron, moet u mogelijk toodownload en installatie hello Azure SDK voor Python (Zie: [hoe tooinstall Python](../python-how-to-install.md)).

U moet ook Hallo **werkruimte**, **service**, en **api_key** van uw experiment voor Hallo voorbeeld bron hieronder. U kunt Hallo werkruimte en service vinden door te klikken op **aanvragen/reacties** of **Batchuitvoering** voor uw experiment in Hallo web service-dashboard.

![Zoek-werkruimte-en-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

U vindt Hallo **api_key** door te klikken op uw experiment in Hallo web service-dashboard.

![zoeken-api-sleutel](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a>Test RRS-eindpunt
##### <a name="test-button"></a>Knop Testen
Een eenvoudige manier tootest Hallo RRS-eindpunt is tooclick **Test** op Hallo web service-dashboard.

![Test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

Type **dit is een goede dag** voor **col2**. Klik op Hallo vinkje.

![Geef gegevens](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

U ziet ongeveer

![Voorbeeld van uitvoer](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a>Voorbeeldcode
Een andere manier tootest uw RRS is vanuit uw clientcode. Als u op **aanvragen/reacties** onder Hallo dashboard en blader toohello, ziet u de voorbeeldcode van C#, Python en R. U ziet ook Hallo syntaxis van Hallo RRS-aanvraag, waaronder Hallo aanvraag-URI, kopteksten en hoofdtekst.

Deze handleiding ziet u een werkende Python-voorbeeld. U moet toomodify met Hallo **werkruimte**, **service**, en **api_key** van uw experiment.

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a>Test BES eindpunt
Klik op **Batchuitvoering** Hallo dashboard en blader toohello onderaan. Ziet u voorbeelden van code voor C#, Python en R. U ziet ook de syntaxis van de Hallo van Hallo BES aanvragen toosubmit een taak, een taak starten Hallo status of de resultaten van een taak ophalen en verwijderen van een taak.

Deze handleiding ziet u een werkende Python-voorbeeld. U moet toomodify met Hallo **werkruimte**, **service**, en **api_key** van uw experiment. Daarnaast moet u toomodify hello **opslagaccountnaam**, **opslagaccountsleutel**, en **opslag containernaam**. Tot slot moet u toomodify Hallo locatie Hallo **invoerbestand** en de locatie van Hallo Hallo **uitvoerbestand**.

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
