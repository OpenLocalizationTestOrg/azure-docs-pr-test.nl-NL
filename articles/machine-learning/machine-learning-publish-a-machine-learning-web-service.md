---
title: een Machine Learning-webservice aaaDeploy | Microsoft Docs
description: Hoe een training tooconvert experimenteren tooa Voorspellend experiment, voorbereiden voor implementatie en klik vervolgens als een Azure Machine Learning-webservice implementeren.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 73a3e9c6-00d0-41d4-8cf1-2ec87713867e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9cb7af637632b2c3688c11483f29cf24df8fd065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a>Een Azure Machine Learning-webservice implementeren
Azure Machine Learning, kunt u toobuild, testen en implementeren van voorspellende analytische oplossingen.

Dit is van een punt-van-overzichtsweergave gedaan in drie stappen:

* **[Maken van een trainingsexperiment]**  -Azure Machine Learning Studio is een gezamenlijke visual ontwikkelomgeving tootrain te gebruiken en testen van een predictive analytics model met trainingsgegevens die u opgeeft.
* **[Converteert u deze tooa Voorspellend experiment]**  - nadat uw model is getraind met bestaande gegevens en u klaar toouse bent het tooscore nieuwe gegevens, u voorbereidt en uw experiment voor voorspellingen stroomlijnen.
* **[Als een webservice implementeren]**  -u kunt uw Voorspellend experiment als een [nieuwe] of [klassieke] Azure-web-service. Gebruikers kunnen tooyour gegevensmodel verzenden en ontvangen van uw model voorspellingen.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a>Een trainingsexperiment maken
tootrain een predictive analytics-model, gebruikt u Azure Machine Learning Studio toocreate een trainingsexperiment waar u verschillende modules tooload trainingsgegevens bevatten, Hallo-gegevens zo nodig voorbereiden toepassen van machine learning-algoritmen en Hallo resultaten evalueren . U kunt een experiment herhalen en probeer andere machine learning-algoritmen toocompare en Hallo resultaten evalueren.

Hallo-proces voor het maken en beheren van training experimenten wordt uitgebreid elders besproken. Zie voor meer informatie in deze artikelen:

* [Een eenvoudige experiment maken in Azure Machine Learning Studio](machine-learning-create-experiment.md)
* [Een voorspellende oplossing met Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)
* [Uw trainingsgegevens importeren in Azure Machine Learning Studio](machine-learning-data-science-import-data.md)
* [Experimentherhalingen in Azure Machine Learning Studio beheren](machine-learning-manage-experiment-iterations.md)

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Hallo training experiment tooa Voorspellend experiment converteren
Zodra u uw model te trainen hebt, bent u klaar tooconvert uw training experimenteren aan een Voorspellend experiment tooscore nieuwe gegevens.

Door het converteren van voorspellende tooa experimenteren, u bij het ophalen van het getrainde model klaar toobe geïmplementeerd als een score-webservice. Gebruikers van de webservice Hallo kunnen verzenden invoergegevens tooyour model en het model van uw back-Hallo voorspelling resultaten wordt verzonden. Zoals u converteren wordt voorspeld tooa experimenteren, houd er rekening mee hoe u van plan bent uw model toobe door anderen gebruikt.

tooconvert uw experiment tooa voor training Voorspellend experiment, klikt u op **uitvoeren** onderaan Hallo Hallo experimentcanvas, klikt u op **webservice ingesteld**, selecteer daarna **voorspellende Web Service** .

![Tooscoring experiment converteren](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

Voor meer informatie over het tooperform deze conversie Zie [hoe tooprepare uw model voor de implementatie in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Hallo volgende stappen beschrijven een Voorspellend experiment als een nieuwe webservice implementeren. U kunt ook Hallo experiment implementeren als webservice klassiek.

## <a name="deploy-it-as-a-web-service"></a>Als een webservice implementeren

U kunt Hallo Voorspellend experiment implementeren als een nieuwe webservice of als een klassiek-webservice.

### <a name="deploy-hello-predictive-experiment-as-a-new-web-service"></a>Hallo Voorspellend experiment implementeren als een nieuwe webservice
Nu dat Hallo Voorspellend experiment is voorbereid, kunt u deze kunt implementeren als een nieuwe Azure-web-service. Via de webservice hello, kunnen gebruikers tooyour gegevensmodel verzenden en Hallo model retourneert de voorspellingen.

toodeploy uw Voorspellend experiment, klikt u op **uitvoeren** onderin Hallo Hallo experimenteren canvas. Zodra het Hallo-experiment is voltooid, klikt u op **webservice implementeren** en selecteer **webservice implementeren [nieuw]**.  Hallo implementatie pagina van Hallo Machine Learning-webservice portal wordt geopend.

> [!NOTE] 
> toodeploy een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich u Hallo-webservice implementeren. Zie voor meer informatie, [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md). 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a>Machine Learning-webservice portal implementeren Experiment pagina
Voer een naam voor de webservice Hallo op Hallo implementeren Experiment pagina.
Een prijscategorie selecteren. Als u een bestaande prijsstelling dat kunt u dit hebt, moet anders u een nieuw plan prijs voor Hallo-service.

1. In Hallo **prijs Plan** vervolgkeuzelijst, selecteer een bestaand abonnement of Hallo **Selecteer nieuw plan** optie.
2. In **naam**, typ een naam die wordt geïdentificeerd Hallo plan op uw factuur.
3. Selecteer een van de Hallo **maandelijks plannen lagen**. Hallo plan lagen standaard toohello plannen voor uw regio standaard en uw webservice is geïmplementeerde toothat regio.

Klik op **implementeren** en Hallo **Quick Start** pagina voor uw webservice wordt geopend.

Hallo pagina Quick Start webservice biedt u toegang en richtlijnen op Hallo meest algemene taken die u uitvoeren wilt na het maken van een webservice. Hier kunt u eenvoudig toegang tot zowel Hallo testpagina en verbruiken pagina.

<!-- ![Deploy hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a>Uw nieuwe webservice testen
tootest uw nieuwe webservice, klikt u op **webservice testen** onder algemene taken. U kunt uw webservice als een aanvraag en antwoord-Service (RR's) of een batchuitvoeringsservice (BES) testen op Hallo testpagina.

Hallo RRS testpagina weergeven Hallo invoer, uitvoer en algemene parameters die u hebt gedefinieerd voor Hallo experiment tootest Hallo-webservice, u kunt handmatig een door komma's gescheiden waarden (CSV) opgemaakt bestand Hallo testwaarden met juiste waarden voor Hallo invoer of geef invoeren.

tootest RRS, met behulp van de modus voor Hallo lijst weergeven, geef de juiste waarden voor Hallo invoer en klik op **Test aanvragen en antwoorden**. De voorspelling van de resultaten weergeven in Hallo uitvoer kolom toohello links.

![Hallo-webservice implementeren](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

Klik op tootest uw BES **Batch**. Klik op Bladeren onder uw invoer op Hallo Batch testpagina, en selecteer een CSV-bestand met de juiste voorbeeldwaarden. Als u een CSV-bestand niet hebt en u uw Voorspellend experiment met Machine Learning Studio hebt gemaakt, kunt u Hallo gegevensset voor uw Voorspellend experiment downloaden en gebruiken.

toodownload gegevensset hello, open Machine Learning Studio. Open uw Voorspellend experiment en klikt u met de rechtermuisknop op Hallo invoer voor uw experiment. Selecteer in het contextmenu hello, **gegevensset** en selecteer vervolgens **downloaden**.

![Hallo-webservice implementeren](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

Klik op **Test**. Hallo-status van de taak Batchuitvoering weergegeven toohello rechts onder **Test batchtaken**.

![Hallo-webservice implementeren](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

Op Hallo **configuratie** pagina Hallo beschrijving wijzigen, titel, Hallo account opslagsleutel bijwerken en voorbeeldgegevens inschakelen voor uw webservice.

![Hallo-webservice configureren](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

Nadat u de webservice Hallo hebt geïmplementeerd, kunt u:

* **Toegang** deze via API Hallo-webservice.
* **Beheren** deze via Azure Machine Learning web services-portal of Hallo klassieke Azure-portal.
* **Update** deze als het model wordt gewijzigd.

#### <a name="access-your-new-web-service"></a>Toegang tot uw nieuwe webservice
Nadat u uw webservice van Machine Learning Studio implementeert, kunt u toohello gegevensservice verzenden en antwoorden programmatisch ontvangen.

Hallo **verbruiken** pagina vindt u alle benodigde tooaccess uw webservice Hallo-gegevens. Hallo API-sleutel biedt bijvoorbeeld tooallow geautoriseerd access toohello-service.

Zie voor meer informatie over het openen van een Machine Learning-webservice [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).

#### <a name="manage-your-new-web-service"></a>Beheren van uw nieuwe webservice
U kunt uw nieuwe web services Machine Learning-webservices portal beheren. Van Hallo [portal hoofdpagina](https://services.azureml-test.net/), klikt u op **webservices**. U kunt vanaf Hallo services webpagina, verwijderen of kopiëren van een service. een specifieke service toomonitor Hallo-service op en klik op **Dashboard**. toomonitor batchtaken die zijn gekoppeld aan het Hallo-webservice, klikt u op **Batch aanvragen logboek**.

### <a name="deploy-hello-predictive-experiment-as-a-classic-web-service"></a>Hallo Voorspellend experiment implementeren als een klassiek-webservice

Nu dat Hallo Voorspellend experiment is voldoende voorbereid, kunt u deze kunt implementeren als een klassieke Azure-webservice. Via de webservice hello, kunnen gebruikers tooyour gegevensmodel verzenden en Hallo model retourneert de voorspellingen.

toodeploy uw Voorspellend experiment, klikt u op **uitvoeren** experimenteren canvas Hallo Hallo onderaan in en klik vervolgens op **webservice implementeren**. Hallo-webservice is ingesteld en u in Hallo web servicedashboard worden geplaatst.

![Hallo-webservice implementeren](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a>Test uw webservice klassiek

U kunt Hallo-webservice testen in Hallo Machine Learning-webservices portal of Machine Learning Studio.

tootest hello Request Response-webservice, klikt u op Hallo **Test** knop in Hallo web service-dashboard. Een dialoogvenster weergegeven tooask u voor de invoergegevens Hallo voor Hallo-service. Dit zijn werd verwacht door Hallo score berekenen experiment Hallo-kolommen. Geef een set gegevens en klik op **OK**. Hallo-resultaten die zijn gegenereerd door de webservice Hallo worden Hallo onderaan Hallo dashboard weergegeven.

U kunt klikken op Hallo **Test** preview-koppeling tootest uw service in Azure Machine Learning-webservices-portal Hallo zoals eerder in Hallo nieuwe sectie van de web service.

tootest hello Batch-Service kan worden uitgevoerd, klikt u op **Test** link bekijken. Klik op Bladeren onder uw invoer op Hallo Batch testpagina, en selecteer een CSV-bestand met de juiste voorbeeldwaarden. Als u een CSV-bestand niet hebt en u uw Voorspellend experiment met Machine Learning Studio hebt gemaakt, kunt u Hallo gegevensset voor uw Voorspellend experiment downloaden en gebruiken.

![Hallo webservice testen](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

Op Hallo **configuratie** pagina kunt u de weergavenaam Hallo van Hallo-service wijzigen en een omschrijving. Hallo-naam en beschrijving wordt weergegeven in Hallo [klassieke Azure-portal](http://manage.windowsazure.com/) waar u uw webservices beheren.

U kunt een beschrijving opgeven voor uw invoergegevens, uitvoergegevens en web parameters van de service door een tekenreeks opgeven voor elke kolom onder **INVOERSCHEMA**, **UITVOERSCHEMA**, en **Web SERVICE PARAMETER**. Deze beschrijvingen worden in Hallo voorbeeld code documentatie voor de webservice hello gebruikt.

Eventuele fouten die u ziet, wanneer uw webservice wordt geopend, kunt u logboekregistratie toodiagnose inschakelen. Zie voor meer informatie [logboekregistratie inschakelen voor Machine Learning-webservices](machine-learning-web-services-logging.md).

![Hallo-webservice configureren](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

U kunt ook Hallo eindpunten voor Hallo-webservice configureren in Azure Machine Learning-webservices portal vergelijkbare toohello procedure eerder weergegeven in de nieuwe sectie van de web service Hallo Hallo. zijn er andere Hallo-opties, kunt u toevoegen of wijzigen Hallo servicebeschrijving logboekregistratie inschakelen en de voorbeeldgegevens inschakelen voor het testen.

#### <a name="access-your-classic-web-service"></a>Toegang tot uw webservice klassiek
Nadat u uw webservice van Machine Learning Studio implementeert, kunt u toohello gegevensservice verzenden en antwoorden programmatisch ontvangen.

Hallo dashboard bevat alle benodigde tooaccess uw webservice Hallo-gegevens. Hallo-API-sleutel is bijvoorbeeld tooallow geautoriseerd toohello-access-service en de API help-pagina's worden geleverd toohelp die u aan de slag uw code te schrijven.

Zie voor meer informatie over het openen van een Machine Learning-webservice [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).

#### <a name="manage-your-classic-web-service"></a>Uw webservice klassieke beheren
Er zijn verschillende acties kunt u een webservice toomonitor uitvoeren. U kunt bijwerken en verwijderen. U kunt ook extra eindpunten tooa klassieke-webservice toevoegen in toevoeging toohello standaardeindpunt dat wordt gemaakt wanneer u deze implementeert.

Zie voor meer informatie [beheren van een Azure Machine Learning-werkruimte](machine-learning-manage-workspace.md) en [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md).

<!-- When this article gets published, fix hello link and uncomment
For more information on how toomanage Azure Machine Learning web service endpoints using hello REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-hello-web-service"></a>Hallo webservice bijwerken
U kunt wijzigingen aanbrengen tooyour webservice, zoals het Hallo-model met extra trainingsgegevens, bijwerken en implementeert u deze opnieuw, wordt de oorspronkelijke webservice hallo overschreven.

tooupdate Hallo-webservice, open Hallo oorspronkelijke Voorspellend experiment toodeploy Hallo-webservice die wordt gebruikt en een bewerkbare kopie maken door te klikken op **SAVE AS**. Breng uw wijzigingen en klik vervolgens op **webservice implementeren**.

Omdat u dit experiment voordat hebt geïmplementeerd, wordt u gevraagd of u toooverwrite (klassieke webservice) of update (nieuwe webservice) Hallo bestaande service wilt. Te klikken op **Ja** of **Update** Hallo bestaande web-service gestopt en implementeert Hallo nieuwe Voorspellend experiment in plaats daarvan wordt geïmplementeerd.

> [!NOTE]
> Als u configuratiewijzigingen in de oorspronkelijke webservice hello aangebracht, bijvoorbeeld, moet u een nieuwe weergavenaam of beschrijving, u tooenter die waarden opnieuw.
> 
> 

Een mogelijkheid voor het bijwerken van uw web-service is tooretrain Hallo model programmatisch. Zie [Machine Learning-modellen programmatisch opnieuw trainen](machine-learning-retrain-models-programmatically.md) voor meer informatie.

<!-- internal links -->
[Maken van een trainingsexperiment]: #create-a-training-experiment
[Converteert u deze tooa Voorspellend experiment]: #convert-the-training-experiment-to-a-predictive-experiment
[Als een webservice implementeren]: #deploy-it-as-a-web-service
[nieuwe]: #deploy-the-predictive-experiment-as-a-new-Web-service
[klassieke]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
