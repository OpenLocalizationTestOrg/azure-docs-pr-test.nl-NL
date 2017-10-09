---
title: een Azure Machine Learning-model aaaHow wordt een webservice | Microsoft Docs
description: Een overzicht van Hallo mechanisme van hoe de voortgang van uw Azure Machine Learning-model van een ontwikkel tooan experimenteren geoperationaliseerd webservice.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 25e0c025-f8b0-44ab-beaf-d0f2d485eb91
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 2bbe09fa8fa22662cf8ec4a8b6249d23c87c8ddf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-a-machine-learning-model-progresses-from-an-experiment-tooan-operationalized-web-service"></a>Hoe de loop van een Machine Learning-model van een experiment tooan geoperationaliseerd-webservice
Azure Machine Learning Studio biedt een interactieve canvas waarmee u toodevelop, worden uitgevoerd, te testen en te herhalen een ***experimenteren*** die vertegenwoordigt een predictive Analytics-model. Er zijn tal van modules die kunnen:

* Invoergegevens die in uw experiment
* Hallo gegevens bewerken
* Een model met machine learning-algoritmen trainen
* Hallo-score-model
* Hallo resultaten evalueren
* Laatste uitvoerwaarden

Als u tevreden met uw experiment bent, kunt u het implementeert als een ***klassieke Azure Machine Learning-webservice*** of een ***nieuwe Azure Machine Learning-webservice*** zodat gebruikers kunnen deze nieuwe gegevens verzenden en terug ontvangen resultaten.

In dit artikel biedt we een overzicht van Hallo mechanisme van hoe de voortgang van uw Machine Learning-model van een experiment ontwikkeling tooan geoperationaliseerd webservice.

> [!NOTE]
> Er zijn andere manieren toodevelop en machine learning-modellen implementeren, maar in dit artikel is gericht op hoe u Machine Learning Studio gebruiken. Bijvoorbeeld, een beschrijving van hoe toocreate een klassieke voorspellende webservice met R, Zie Hallo blogbericht tooread [Build & implementeren voorspellende Web-Apps met behulp van RStudio en Azure ML](http://blogs.technet.com/b/machinelearning/archive/2015/09/25/build-and-deploy-a-predictive-web-app-using-rstudio-and-azure-ml.aspx).
> 
> 

Terwijl Azure Machine Learning Studio ontworpen toohelp is ontwikkelen en implementeren van een *predictive Analytics-model*, het is mogelijk toouse Studio toodevelop een experiment waarin een predictive Analytics-model niet. Bijvoorbeeld, een experiment alleen invoergegevens mogelijk, bewerken en vervolgens uitvoer Hallo resultaten. Net als een predictive Analytics-experiment, kunt u deze niet-Voorspellend experiment als een webservice implementeren, maar het is een eenvoudigere proces omdat Hallo experiment niet training of score berekenen voor een machine learning-model. Hoewel het geen Hallo typische toouse Studio op deze manier hebt we het opnemen in Hallo discussie zodat we een volledige uitleg van de werking van Studio kunnen geven.

## <a name="developing-and-deploying-a-predictive-web-service"></a>Ontwikkeling en implementatie van een Voorspellend webservice
Hier volgen Hallo fasen die een gangbare oplossing volgt bij het ontwikkelen en implementeren met behulp van Machine Learning Studio:

![Implementatie-stroom](media/machine-learning-model-progression-experiment-to-web-service/model-stages-from-experiment-to-web-service.png)

*Afbeelding 1: fasen van een typische predictive Analytics-model*

### <a name="hello-training-experiment"></a>Hallo trainingsexperiment
Hallo ***trainingsexperiment*** Hallo eerste fase vormt van het ontwikkelen van uw Web-service in Machine Learning Studio. Hallo-doel van Hallo trainingsexperiment is toogive u een toodevelop plaats testen, herhalen en uiteindelijk een machine learning-model te trainen. U kunt zelfs trainen meerdere modellen tegelijkertijd als u naar de beste oplossing hello zoeken, maar wanneer u klaar bent u experimenteren één getraind kiest model en rest Hallo van Hallo experiment te elimineren. Zie voor een voorbeeld van het ontwikkelen van een predictive Analytics-experiment [predictive analytics-oplossing voor kredietrisicobeoordeling in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="hello-predictive-experiment"></a>Hallo Voorspellend experiment
Wanneer u een getraind model in uw trainingsexperiment hebt, klikt u op **webservice ingesteld** en selecteer **voorspellende webservice** in Machine Learning Studio tooinitiate Hallo proces van het converteren van uw training Experimenteer tooa ***Voorspellend experiment***. doel van een Voorspellend experiment Hallo Hallo toouse is uw getrainde model tooscore nieuwe gegevens, met de Hallo doel van uiteindelijk steeds geoperationaliseerd als een Azure-webservice.

Deze conversie is gedaan om u via Hallo stappen te volgen:

* Hallo modules die worden gebruikt voor training in de module voor een enkele set converteren en deze opslaan als een getraind model
* Alle overbodige modules die niet gerelateerd elimineren tooscoring
* Invoer toevoegen en de uitvoer van de poorten die Hallo uiteindelijke Web-service wordt gebruikt

Mogelijk zijn er meer gewenste wijzigingen toomake tooget uw Voorspellend experiment gereed toodeploy als een webservice. Als u Hallo Web service toooutput slechts een subset van de resultaten wilt, kunt u bijvoorbeeld een module filteren voordat de uitvoerpoort Hallo toevoegen.

In dit conversieproces Hallo trainingsexperiment niet worden verwijderd. Wanneer het Hallo-proces is voltooid, hebt u twee tabbladen in Studio: één voor Hallo trainingsexperiment en één voor Hallo Voorspellend experiment. Deze manier die u wijzigingen toohello trainingsexperiment aanbrengen kunt voordat u uw webservice implementeren en Voorspellend experiment Hallo opnieuw opbouwen. Of u een kopie van Hallo training experiment toostart een andere line-of experimenteren kunt opslaan.

> [!NOTE]
> Wanneer u klikt op **voorspellende webservice** u start een automatische proces tooconvert uw experiment tooa voorspellende trainingsexperiment en dit werkt goed in de meeste gevallen. Als uw trainingsexperiment complex (bijvoorbeeld: u hebt meerdere paden voor training die u samenvoegen), werkt u liever toodo deze conversie handmatig. Zie voor meer informatie [hoe tooprepare uw model voor de implementatie in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).
> 
> 

### <a name="hello-web-service"></a>Hallo-webservice
Als u tevreden bent dat uw Voorspellend experiment gereed is, u uw service als een klassieke webservice implementeren kunt of een nieuwe webservice op basis van Azure Resource Manager. toooperationalize uw model door te implementeren als een *klassieke Machine Learning-webservice*, klikt u op **webservice implementeren** en selecteer **webservice implementeren [klassieke]**. toodeploy als *nieuwe Machine Learning-webservice*, klikt u op **webservice implementeren** en selecteer **Web Service implementeren [New]**. Gebruikers kunnen nu verzenden tooyour gegevensmodel met de webservice Hallo REST-API en vorige Hallo resultaten krijgen. Zie voor meer informatie [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).

## <a name="hello-non-typical-case-creating-a-non-predictive-web-service"></a>niet-standaard Hallo: maken van een niet-predictive-webservice
Als uw experiment heeft geen training een predictive Analytics-model, dan hebt u geen toocreate moet zowel een trainingsexperiment en een score experiment - er is slechts één experiment en kunt u dit implementeren als een webservice. Machine Learning Studio detecteert of uw experiment een Voorspellend model bevat door te analyseren Hallo-modules die u hebt gebruikt.

Nadat u hebt op uw experiment herhaald en u tevreden met het bent:

1. Klik op **webservice ingesteld** en selecteer **webservice Retraining** - invoer en uitvoer knooppunten automatisch worden toegevoegd
2. Klik op **uitvoeren**
3. Klik op **webservice implementeren** en selecteer **webservice implementeren [klassieke]** of **Web Service implementeren [New]** , afhankelijk van Hallo omgeving toowhich gewenste toodeploy.

Uw webservice wordt nu geïmplementeerd, en u kunt toegang tot en beheer deze net als bij een webservice voorspeld.

## <a name="updating-your-web-service"></a>Bijwerken van uw Web-service
Nu u uw experiment als een webservice hebt geïmplementeerd, wat gebeurt er als u moet tooupdate deze?

Dat hangt wat u moet tooupdate:

**U wilt toochange Hallo invoer of uitvoer, of u wilt dat toomodify hoe Hallo webservice gegevens bewerkt**

Als u niet Hallo model wilt wijzigen, maar hoe gegevens worden verwerkt door Hallo webservice NET wijzigt, kunt u Hallo Voorspellend experiment bewerken en klik vervolgens op **webservice implementeren** en selecteer **webservice implementeren [klassieke]** of **Web Service implementeren [New]** opnieuw. Hallo Web-service is gestopt, hello bijgewerkte Voorspellend experiment wordt geïmplementeerd en Hallo Web-service opnieuw wordt opgestart.

Hier volgt een voorbeeld: Stel dat uw Voorspellend experiment retourneert Hallo hele rij met invoergegevens Hello resultaat voorspeld. U kunt bepalen dat Hallo Web service toojust return Hallo resultaat. Zodat u kunt toevoegen een **Projectkolommen** module in Hallo Voorspellend experiment voordat Hallo uitvoerpoort tooexclude kolommen behalve Hallo leiden. Wanneer u klikt op **webservice implementeren** en selecteer **webservice implementeren [klassieke]** of **Web Service implementeren [New]** opnieuw Hallo-webservice wordt bijgewerkt.

**Gewenste tooretrain Hallo model met nieuwe gegevens**

Als u wilt dat tookeep uw machine learning-model, maar u tooretrain wilt dat deze met nieuwe gegevens die u hebt twee keuzes:

1. **Hallo model Retrain terwijl Hallo-webservice wordt uitgevoerd** -als u tooretrain uw model wilt terwijl Hallo voorspellende Web-service wordt uitgevoerd, u kunt dit doen door het maken van een aantal wijzigingen toohello training experiment toomake deze een *** experiment retraining***, en vervolgens kunt u het implementeert als een  ***retraining web* service**. Voor instructies over het toodo deze, Zie [Retrain Machine Learning-modellen programmatisch](machine-learning-retrain-models-programmatically.md).
2. **Oorspronkelijke trainingsexperiment toohello teruggaan en gebruiken van andere training gegevens toodevelop uw model** : uw Voorspellend experiment is gekoppelde toohello webservice, maar Hallo trainingsexperiment niet rechtstreeks op deze manier is gekoppeld. Als u de oorspronkelijke trainingsexperiment Hallo wijzigen en klik op **webservice ingesteld**, wordt gemaakt een *nieuwe* voorspellende experimenteren die, wanneer geïmplementeerd, maakt u een *nieuwe* Web de service. Het niet automatisch oorspronkelijke webservice Hallo NET bijgewerkt.
   
   Als u toomodify hello trainingsexperiment moet, openen en klik op **OpslaanAls** toomake een kopie. Dit betekent dat de oorspronkelijke trainingsexperiment intact Hallo Voorspellend experiment en webservice. U kunt nu een nieuwe webservice maken met uw wijzigingen. Zodra u hebt geïmplementeerd Hallo nieuwe webservice vervolgens kunt u bepalen of toostop Hallo vorige webservice of te laten naast Hallo nieuwe.

**U wilt dat een ander model tootrain**

Als u wilt dat toomake wijzigingen tooyour oorspronkelijke Voorspellend experiment, zoals het selecteren van een andere machine learning-algoritme, moet probeert een ander training methode, enz., u toofollow Hallo tweede procedure voor het model retraining hierboven beschreven: Hallo trainingsexperiment openen, klikt u op **OpslaanAls** toomake een kopie en start omlaag Hallo nieuwe pad van uw model te ontwikkelen, Hallo Voorspellend experiment maken en implementeren van Hallo-webservice. Hiermee maakt u een nieuwe webservice ongerelateerde toohello oorspronkelijke - kunt u bepalen welke één of beide, tookeep uitgevoerd.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Hallo proces van ontwikkeling en experiment Hallo artikelen te volgen:

* Hallo-experiment - converteren [hoe tooprepare uw model voor de implementatie in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md)
* Hallo webservice - implementatie [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md)
* Hallo-model, retraining - [-modellen programmatisch opnieuw trainen Machine Learning](machine-learning-retrain-models-programmatically.md)

Zie voor voorbeelden van het hele proces Hallo:

* [Machine learning-zelfstudie: uw eerste experiment maken in Azure Machine Learning Studio](machine-learning-create-experiment.md)
* [Overzicht: Een predictive analytics-oplossing voor kredietrisicobeoordeling in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)

