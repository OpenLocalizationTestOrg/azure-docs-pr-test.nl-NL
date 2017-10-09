---
title: 'Stap 5: Hallo Machine Learning-webservice implementeren | Microsoft Docs'
description: 'Stap 5 van Hallo een overzicht van de voorspellende oplossing ontwikkelen: implementeert een Voorspellend experiment in Machine Learning Studio als een webservice.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a>Scenario-stap 5: Hello Azure Machine Learning-webservice implementeren
Dit is de vijfde stap Hallo van Hallo-rondleiding [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Een Machine Learning-werkruimte maken](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Bestaande gegevens uploaden](machine-learning-walkthrough-2-upload-data.md)
3. [Een nieuw experiment maken](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Trainen en evalueren Hallo modellen](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. **Hallo-webservice implementeren**
6. [Toegang Hallo-webservice](machine-learning-walkthrough-6-access-web-service.md)

- - -
toogive anderen een kans toouse Hallo Voorspellend model dat we hebben ontwikkeld in dit scenario, we deze kunt implementeren als een webservice in Azure.

Toothis punt Experimenteer we met het model te trainen. Maar Hallo geïmplementeerd service zal niet langer toodo training - toogenerate nieuwe voorspellingen door score berekenen Hallo gebruikersinvoer op basis van onze model gaat. Dus gaan we toodo sommige tooconvert voorbereiding dit experiment uit een ***training*** experimenteren tooa ***voorspellende*** experimenteren. 

Dit is een proces drie stappen:  

1. Verwijder een van de Hallo modellen
2. Hallo converteren *trainingsexperiment* we hebt gemaakt in een *Voorspellend experiment*
3. Hallo Voorspellend experiment implementeren als een webservice

## <a name="remove-one-of-hello-models"></a>Verwijder een van de Hallo modellen

We moeten eerst tootrim dit experiment omlaag enigszins. Momenteel hebben we twee verschillende modellen in Hallo-experiment, maar we willen alleen één model toouse wanneer we dit als een webservice implementeert.  

Stel, dat we hebt besloten dat Hallo boosted structuur model beter presteert dan Hallo SVM model. Zodat het eerste wat toodo Hallo verwijderen Hallo [Two-Class ondersteuning Vectormachine] [ two-class-support-vector-machine] module en Hallo-modules die zijn gebruikt voor het trainen van het. U kunt een kopie van Hallo experiment toomake eerst door te klikken op **OpslaanAls** onderin Hallo Hallo experimenteren canvas.

We moeten toodelete Hallo modules te volgen:  

* [Vectormachine Two-Class-ondersteuning][two-class-support-vector-machine]
* [Model trainen] [ train-model] en [Score Model] [ score-model] modules die verbonden tooit zijn
* [Gegevens normaliseren] [ normalize-data] (van beide)
* [Model evalueren] [ evaluate-model] (omdat we klaar bent met het evalueren van Hallo modellen)

Selecteer elke module en druk op Hallo verwijderen sleutel, of klik met de rechtermuisknop Hallo module en selecteer **verwijderen**. 

![Hallo SVM model verwijderd][3a]

Het model moet nu als volgt uitzien:

![Hallo SVM model verwijderd][3]

Nu we klaar toodeploy dit model met behulp van Hallo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Hallo training experiment tooa Voorspellend experiment converteren

tooget dit model is klaar voor implementatie, moeten we tooconvert dit experiment tooa Voorspellend experiment training. Dit omvat drie stappen:

1. Hallo model we hebben getraind en vervang onze trainingsmodules opslaan
2. Trim Hallo experiment tooremove modules die zijn alleen nodig voor training
3. Definiëren waar Hallo webservice invoer accepteert en waarbij het Hallo-uitvoer genereert

We kunnen dit handmatig doen, maar gelukkig alle drie stappen kunnen worden uitgevoerd door te klikken op **webservice ingesteld** Hallo Hallo experimentcanvas onderaan in (en het selecteren van Hallo **voorspellende webservice** optie).

> [!TIP]
> Als u meer informatie wilt over wat er gebeurt wanneer u een Voorspellend training experiment tooa converteren experimenteren, raadpleegt u [hoe tooprepare uw model voor de implementatie in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Wanneer u klikt op **webservice ingesteld**, op verschillende manieren gebeuren:

* Hallo getrainde model is geconverteerde tooa één **getrainde Model** module en opgeslagen in Hallo module palet toohello links van Hallo Experimenteer canvas (u vindt deze onder **Trained Models**)
* Modules die zijn gebruikt voor training zijn verwijderd; specifieke opdrachten:
  * [Two-Class gestimuleerd beslissingsstructuur][two-class-boosted-decision-tree]
  * [Train Model][train-model]
  * [Gegevens splitsen][split]
  * tweede Hallo [R-Script uitvoeren] [ execute-r-script] module die is gebruikt voor testgegevens
* Hallo opgeslagen getrainde model weer toegevoegd aan Hallo experiment
* **Web-invoer** en **Web service uitvoer** modules worden toegevoegd (deze vaststellen waar Hallo gebruikersgegevens voert Hallo model en welke gegevens worden geretourneerd wanneer Hallo-webservice wordt geopend)

> [!NOTE]
> U kunt zien dat Hallo experiment wordt opgeslagen in twee delen onder tabbladen die Hallo boven aan het experimentcanvas Hallo zijn toegevoegd. Hallo oorspronkelijke trainingsexperiment ligt onder de Hallo tabblad **trainingsexperiment**, en Hallo nieuw gemaakte Voorspellend experiment ligt onder de **Voorspellend experiment**. Hallo Voorspellend experiment is Hallo een die we als een webservice implementeert.

Moet een extra stap tootake met dit bepaalde experiment.
We twee toegevoegd [R-Script uitvoeren] [ execute-r-script] modules tooprovide een weging toohello gegevens werken. Dat is slechts een slag die we nodig voor het trainen en te testen, zodat we uit deze modules in de laatste model Hallo kunt nemen.
Machine Learning Studio verwijderd een [R-Script uitvoeren] [ execute-r-script] module wanneer het Hallo verwijderd [gesplitste] [ split] module. Nu we verwijderen andere Hallo en maak verbinding [metagegevens Editor] [ metadata-editor] rechtstreeks te[Score Model][score-model].    

Onze experiment ziet er nu als volgt:  

![Score berekenen voor het getrainde model Hallo][4]  

> [!NOTE]
> U vraagt zich misschien af waarom we Hallo UCI Duits creditcardgegevens gegevensset links in Hallo Voorspellend experiment. Hallo-service gaat tooscore Hallo van gebruikersgegevens, niet Hallo oorspronkelijke gegevensset, dus waarom laat de oorspronkelijke gegevensset Hallo in Hallo model?
> 
> Het is waar Hallo service oorspronkelijke creditcardgegevens niet nodig Hallo. Maar hoeft Hallo-schema voor die gegevens, waaronder gegevens zoals het aantal kolommen zijn en welke kolommen numeriek zijn. Deze schema-informatie is nodig toointerpret Hallo gegevens van een gebruiker. We laten deze onderdelen die zijn verbonden, zodat hello scoremodule Hallo gegevensset-schema heeft wanneer Hallo-service wordt uitgevoerd. Hallo gegevens wordt niet gebruikt, alleen Hallo schema.  
> 
> 

Hallo-experiment een keer worden uitgevoerd (Klik op **uitvoeren**.) Als u nog steeds tooverify die Hallo model werkt wilt, klikt u op Hallo uitvoer Hallo [Score Model] [ score-model] module en selecteer **resultaten weergeven**. U kunt zien dat de oorspronkelijke gegevens hello wordt weergegeven, samen met de Hallo tegoed risico waarde ('Scored Labels') en Hallo score berekenen voor waarschijnlijkheidswaarde ('berekend kansen'.) 

## <a name="deploy-hello-web-service"></a>Hallo-webservice implementeren
U kunt Hallo experiment implementeren als ofwel Classic webservice of als een nieuwe webservice die gebaseerd op Azure Resource Manager.

### <a name="deploy-as-a-classic-web-service"></a>Als een klassiek-webservice implementeren
een klassiek webservice afgeleid van onze experiment toodeploy klikt u op **webservice implementeren** hieronder Hallo canvas en selecteer **webservice implementeren [klassieke]**. Machine Learning Studio Hallo experiment als een webservice implementeert en gaat u verder toohello dashboard voor de webservice. Op deze pagina kunt u terugkeren toohello experiment (**weergave momentopname** of **weergeven het meest recente**) en een eenvoudige test van de webservice Hallo uitvoeren (Zie **Hallo webservice testen** hieronder). Er is ook hier informatie voor het maken van toepassingen die toegang heeft tot Hallo webservice (meer informatie over die in de volgende stap Hallo van deze rondleiding).

![Web service-dashboard][6]

U kunt Hallo service configureren door te klikken op Hallo **configuratie** tabblad. Hier kunt u de naam van de service Hallo (dit is opgegeven Hallo experiment naam standaard) wijzigen en wijs hieraan een beschrijving. U kunt ook meer beschrijvende labels voor Hallo geeft en uitvoergegevens.  

![Hallo-webservice configureren][5]  

### <a name="deploy-as-a-new-web-service"></a>Als een nieuwe webservice implementeren

> [!NOTE] 
> een nieuwe webservice die u moet voldoende machtigingen hebben in Hallo abonnement toowhich die u implementeert toodeploy Hallo-webservice. Zie voor meer informatie [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md). 

een nieuwe webservice toodeploy afgeleid van onze experiment:

1. Klik op **webservice implementeren** hieronder Hallo canvas en selecteer **Web Service implementeren [New]**. Machine Learning Studio, brengt u toohello Azure Machine Learning-webservices **implementeren Experiment** pagina.

2. Voer een naam voor Hallo-webservice. 

3. Voor **prijs Plan**, kunt u een bestaande prijsstelling of Selecteer 'Nieuw maken' en geven Hallo nieuwe van plan bent een naam en selecteer Hallo-optie voor maandelijks plannen. Hallo plan lagen standaard toohello plannen voor uw regio standaard en uw webservice is geïmplementeerde toothat regio.

4. Klik op **implementeren**.

Na een paar minuten Hallo **Quick Start** pagina voor uw webservice wordt geopend.

U kunt Hallo service configureren door te klikken op Hallo **configureren** tabblad. Hier kunt u wijzigen Hallo service title en wijs hieraan een beschrijving. 

tootest hello webservice, klikt u op Hallo **Test** tabblad (Zie **Hallo webservice testen** hieronder). Klik op Help voor meer informatie over het maken van toepassingen die toegang heeft tot de webservice Hallo Hallo **verbruiken** tabblad (de volgende stap in dit overzicht Hallo Ga dieper).

> [!TIP]
> Nadat u deze hebt geïmplementeerd, kunt u Hallo webservice bijwerken. Bijvoorbeeld, als u uw model toochange wilt, vervolgens u kunt bewerken Hallo trainingsexperiment, Hallo Modelparameters aanpassen, en op **webservice implementeren**, selecteren **webservice implementeren [klassieke]** of  **[New]-webservice implementeren**. Wanneer u een experiment Hallo opnieuw implementeert, vervangt het Hallo-webservice, nu met gebruik van uw bijgewerkte model.  
> 
> 

## <a name="test-hello-web-service"></a>Hallo webservice testen

Als de webservice hello wordt geopend, krijgt de Hallo gebruikersgegevens via Hallo **Web service invoer** module waar deze toohello heeft doorgegeven [Score Model] [ score-model] module en gewaardeerd. Hallo manier die we Hallo Voorspellend experiment hebt ingesteld, Hallo-model verwacht gegevens in dezelfde notatie als Hallo oorspronkelijke tegoed risico gegevensset Hallo.
Hallo resultaten zijn toohello gebruiker van de webservice Hallo via Hallo **Web service uitvoer** module.

> [!TIP]
> Hallo manier hebben we Hallo Voorspellend experiment geconfigureerd, Hallo gehele resultaat is van een Hallo [Score Model] [ score-model] module worden geretourneerd. Dit omvat alle invoergegevens Hallo plus Hallo tegoed risico waarde en Hallo kans score berekenen. Maar u kunt een iets andere betekenis als u wilt terugkeren - u kan bijvoorbeeld alleen Hallo tegoed risico waarde retourneren. toodo deze, invoegen een [Projectkolommen] [ project-columns] module tussen [Score Model] [ score-model] en Hallo **Web service uitvoer** tooeliminate kolommen die u niet wilt dat de web service tooreturn Hallo. 
> 
> 

U kunt een klassiek web testen in service **Machine Learning Studio** of in Hallo **Azure Machine Learning-webservices** portal.
U kunt een nieuwe webservice testen alleen in Hallo **Machine Learning-webservices** portal.

> [!TIP]
> Bij het testen in hello Azure Machine Learning-webservices-portal, kunt u Hallo portal maken waarmee u tootest Hallo aanvragen en antwoorden service kunt voorbeeldgegevens kunt hebben. Op Hallo **configureren** pagina, selecteert u 'Ja' voor **voorbeeld gegevens ingeschakeld?**. Bij het openen van tabblad Hallo aanvragen en antwoorden op Hallo **Test** pagina Hallo portal ingevuld voorbeeldgegevens die afkomstig zijn uit Hallo oorspronkelijke tegoed risico gegevensset.

### <a name="test-a-classic-web-service"></a>Een klassieke webservice testen

In Machine Learning Studio of Hallo Machine Learning-webservices portal, kunt u een webservice klassieke testen. 

#### <a name="test-in-machine-learning-studio"></a>Testen in Machine Learning Studio

1. Op Hallo **DASHBOARD** pagina voor Hallo-webservice, klikt u op Hallo **Test** knop onder **eindpunt standaard**. Een dialoogvenster verschijnt en vraagt u om Hallo invoergegevens voor Hallo-service. Deze Hallo dezelfde kolommen die zijn opgetreden in Hallo oorspronkelijke tegoed risico gegevensset zijn.  

2. Geef een set gegevens en klik op **OK**. 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a>Testen in Hallo Machine Learning-webservices-portal

1. Op Hallo **DASHBOARD** pagina voor Hallo-webservice, klikt u op Hallo **Test preview** koppeling onder **eindpunt standaard**. Hallo testpagina in hello Azure Machine Learning-webservices-portal voor Hallo webservice-eindpunt wordt geopend en u wordt gevraagd de invoergegevens Hallo voor Hallo-service. Deze Hallo dezelfde kolommen die zijn opgetreden in Hallo oorspronkelijke tegoed risico gegevensset zijn.

2. Klik op **testen aanvragen en antwoorden**. 

### <a name="test-a-new-web-service"></a>Een nieuwe webservice testen

U kunt een nieuwe webservice testen alleen in Hallo Machine Learning-webservices-portal.

1. In Hallo [Azure Machine Learning-webservices](https://services.azureml.net/quickstart) en klik op **Test** bovenaan Hallo Hallo pagina. Hallo **Test** pagina wordt geopend en kunt u gegevens voor de service Hallo invoeren. Hallo invoervelden weergegeven overeenkomen toohello kolommen die zijn opgetreden in de oorspronkelijke gegevensset van tegoed risico Hallo. 

2. Geef een set gegevens en klik op **Test aanvragen en antwoorden**.

Hallo worden resultaten van de test Hallo weergegeven op de rechterkant van de pagina Hallo in uitvoerkolom Hallo Hallo. 


## <a name="manage-hello-web-service"></a>Hallo-webservice beheren

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a>Een klassieke webservice in de klassieke Azure-portal Hallo beheren

Nadat u uw webservice klassieke hebt geïmplementeerd, kunt u het beheren van Hallo [klassieke Azure-portal](https://manage.windowsazure.com).

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com)
2. In het Configuratiescherm Hallo Microsoft Azure-services, klikt u op **MACHINE LEARNING**
3. Klik op de werkruimte
4. Klik op Hallo **webservices** tabblad
5. Klik op Hallo-webservice die is gemaakt
6. Klik op Hallo 'standaard' eindpunt

Hier kunt u bijvoorbeeld controleren hoe Hallo webservice presteert en prestaties trucs maken door het wijzigen van het aantal gelijktijdige aanroepen Hallo-service kan verwerken.

Zie voor meer informatie:

* [Eindpunten maken](machine-learning-create-endpoint.md)
* [Web-service schalen](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a>Een klassieke of een nieuwe webservice in hello Azure Machine Learning-webservices portal beheren

Zodra u hebt uw webservice geïmplementeerd of klassieke of nieuwe, kunt u het beheren van Hallo [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/quickstart) portal.

toomonitor hello prestaties van uw web-service:

1. Meld u aan toohello [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/quickstart) portal
2. Klik op **webservices**
3. Klik op uw web-service
4. Klik op Hallo **Dashboard**

- - -
**Volgende stap: [toegang tot Hallo-webservice](machine-learning-walkthrough-6-access-web-service.md)**

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
