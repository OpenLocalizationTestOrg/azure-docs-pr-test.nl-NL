---
title: Voorbeeld met MLlib Spark in HDInsight - Azure learning aaaMachine | Microsoft Docs
description: Meer informatie over hoe toouse Spark MLlib toocreate een machine learning-app die een gegevensset met behulp van classificatie via logistic regression analyseert.
keywords: Spark machine learning spark machine learning-voorbeeld
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a>Een machine learning-toepassing voor Spark MLlib toobuild gebruiken en analyseren van een gegevensset

Meer informatie over hoe toouse Spark **MLlib** toocreate een machine learning-toepassing toodo eenvoudige predictive Analytics op een open gegevensset. Van Spark van ingebouwde machine learning-bibliotheken, in dit voorbeeld wordt *classificatie* via logistic regression. 

> [!TIP]
> In dit voorbeeld is ook beschikbaar als een Jupyter-notebook op een cluster Spark (Linux) die u in HDInsight maakt. Hallo-notebook ervaring kunt u Hallo Python codefragmenten uit Hallo laptop zelf uitvoeren. toofollow hello zelfstudie uit binnen een laptop een Spark-cluster en start een Jupyter-notebook maken (`https://CLUSTERNAME.azurehdinsight.net/jupyter`). Voer vervolgens de notebook Hallo **Spark Machine Learning - Predictive Analytics op voeding inspectie gegevens met behulp van MLlib.ipynb** onder Hallo **Python** map.
>
>

MLlib is een core Spark-bibliotheek met veel nuttige hulpprogramma's voor machine learning taken, waaronder hulpprogramma's die geschikt zijn voor:

* Classificatie
* Regressie
* Clustering
* Onderwerp-model
* Enkelvoudige waarde afbreken (SVD) en analyse van de principal-onderdeel (Pso)
* Hypothese testen en het berekenen van de voorbeeld-statistieken

## <a name="what-are-classification-and-logistic-regression"></a>Wat zijn de classificatie en logistic regression?
*Classificatie*, een populaire machine learning-taak is Hallo-proces voor het sorteren van invoergegevens in categorieën. Is het Hallo-taak van een classificatie algoritme toofigure hoe tooassign 'labels' tooinput gegevens die u opgeeft. Bijvoorbeeld, u een machine learning-algoritme dat vooraf gedefinieerde gegevens als invoer accepteert kan zien en delen Hallo stock in twee categorieën: bestanden die u moet verkoopt en bestanden die u dient te houden.

Logistic regression is Hallo-algoritme dat u voor classificatie gebruikt. De Spark logistic regression API is nuttig voor *binaire classificatie*, of de ingevoerde gegevens classificeren in een van twee groepen. Zie voor meer informatie over logistic regressies [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).

Kortom, Hallo proces logistic regression produceert een *logistic functie* die kunnen worden gebruikt toopredict Hallo kans dat een invoer-vector in een groep of andere Hallo behoort.  

## <a name="predictive-analysis-example-on-food-inspection-data"></a>Predictive Analytics-voorbeeld op voeding inspectie gegevens
In dit voorbeeld u Spark tooperform sommige predictive Analytics op voeding inspectie gegevens gebruiken (**Food_Inspections1.csv**) die is verkregen via Hallo [Den Haag gegevensportal](https://data.cityofchicago.org/). Deze gegevensset bevat informatie over voeding inrichting controles zijn uitgevoerd in Chicago, inclusief informatie over elke inrichting, Hallo schendingen gevonden (indien aanwezig) en resultaten van Hallo inspectie Hallo. Hallo CSV-bestand is al beschikbaar in Hallo storage-account is gekoppeld aan het cluster op Hallo **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.

In onderstaande Hallo stappen, ontwikkelen van een model toosee wat er toopass nodig is of een voeding inspectie mislukken.

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a>Beginnen met het samenstellen van een Spark-MMLib machine learning-app
1. Van Hallo [Azure-portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt). U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.   
1. Klik op Hallo blade Spark-cluster **Cluster-Dashboard**, en klik vervolgens op **Jupyter-Notebook**. Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.

   > [!NOTE]
   > U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken. Vervang **CLUSTERNAME** met Hallo-naam van het cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. Maak een notebook. Klik op **Nieuw** en klik vervolgens op **PySpark**.

    ![Maken van een Jupyter-notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "een nieuwe Jupyter-notebook maken")
1. Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb. Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.

    ![Geef een naam voor de notebook Hallo](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Geef een naam voor de notebook Hallo")
1. Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet. Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert. U kunt beginnen met het bouwen van uw machine learning-toepassing hello typen die nodig zijn voor dit scenario te importeren. Hallo cursor toodo dus plaats in Hallo cel en druk op **SHIFT + ENTER**.

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a>Maken van een invoer dataframe
We kunnen gebruiken `sqlContext` tooperform transformaties voor gestructureerde gegevens. de eerste taak Hallo is tooload Hallo voorbeeldgegevens ((**Food_Inspections1.csv**)) in een Spark SQL *dataframe*.

1. Omdat de onbewerkte gegevens Hallo zich in een CSV-indeling, moeten we toouse Hallo Spark context toopull elke regel van het Hallo-bestand in het geheugen als niet-gestructureerde tekst; vervolgens gebruikt u Python van CSV-bibliotheek tooparse elke regel afzonderlijk.

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. We nu hebben Hallo CSV-bestand als een RDD.  toounderstand hello schema van Hallo gegevens, we één rij ophalen vanuit Hallo RDD.

        inspections.take(1)

    Hier ziet u uitvoer Hallo volgende:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. Hallo geeft voorgaande uitvoer ons een idee van schema van het invoerbestand Hallo Hallo. Het bevat Hallo-naam van elke tot stand brengen, Hallo type tot stand brengen, Hallo-adres, Hallo gegevens van Hallo inspecties en Hallo locatie, onder andere. Laten we enkele kolommen selecteren die zijn handig voor onze predictive Analytics en Hallo resultaten groeperen als een dataframe welke we vervolgens toocreate een tijdelijke tabel gebruikt.

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. Nu een *dataframe*, `df` waarop we onze analyse kunt uitvoeren. We hebben ook een aanroep van de tijdelijke tabel **CountResults**. Vindt u vier kolommen in Hallo dataframe van belang: **id**, **naam**, **resultaten**, en **schendingen**.

    We gaan een klein aantal Hallo-gegevens ophalen:

        df.show(5)

    Hier ziet u uitvoer Hallo volgende:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a>Hallo gegevens begrijpen
1. Laten we beginnen tooget een beeld krijgt van wat onze gegevensset bevat. Wat zijn bijvoorbeeld verschillende waarden in Hallo Hallo **resultaten** kolom?

        df.select('results').distinct().show()

    Hier ziet u uitvoer Hallo volgende:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. Een snelle visualisatie kan we beter reden over Hallo verdeling van deze resultaten. Er bestaat reeds Hallo gegevens in een tijdelijke tabel **CountResults**. U kunt volgende SQL-query op Hallo tabel tooget Hallo uitvoeren een beter inzicht in hoe Hallo resultaten worden gedistribueerd.

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    Hallo `%%sql` magic gevolgd door `-o countResultsdf` zorgt ervoor dat Hallo-uitvoer van Hallo query lokaal worden bewaard op Hallo Jupyter-server (meestal Hallo headnode van Hallo cluster). Hallo-uitvoer is doorgevoerd als een [Pandas](http://pandas.pydata.org/) dataframe Hello naam opgegeven **countResultsdf**.

    Hier ziet u uitvoer Hallo volgende:

    ![Uitvoer van de SQL-query](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "uitvoer van de SQL-query")

    Voor meer informatie over Hallo `%%sql` magic en andere magics die beschikbaar zijn met de PySpark-kernel hello, Zie [beschikbare Kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
1. U kunt ook Matplotlib gebruiken, een bibliotheek tooconstruct visualisatie van gegevens, toocreate tekent gebruikt. Omdat Hallo grafiek moet worden gemaakt van Hallo lokaal persistent **countResultsdf** dataframe, Hallo codefragment moet beginnen met Hallo `%%local` verwerkt Magic-pakket. Dit zorgt ervoor dat Hallo-code op Hallo Jupyter server lokaal wordt uitgevoerd.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Hier ziet u uitvoer Hallo volgende:

    ![Spark machine learning-toepassing output - cirkeldiagram met vijf verschillende controleresultaten](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning-resultaat-uitvoer")
1. U kunt zien dat er 5 verschillende resultaten, waarvoor een inspectie kan zijn:

   * Bedrijven niet vinden
   * Mislukt
   * Doorgeven
   * PSS met voorwaarden
   * Buiten bedrijf

     Laat het ons een model voor het resultaat van een opgegeven Hallo schendingen van het inspectie voeding Hallo kan raden ontwikkelen. Aangezien logistic regression een classificatiemethode binaire is, maakt zin toogroup onze gegevens in twee categorieën: **mislukken** en **doorgeven**. Een 'doorgeven met voorwaarden"is nog steeds een Pass, zodat wanneer we Hallo model trainen, we beschouwen Hallo twee equivalent resulteert. Gegevens met Hallo andere resultaten ('Bedrijven niet vinden' of 'Out of Business') zijn niet handig zodat we uit onze trainingset verwijderen. Dit mag geen probleem omdat deze twee categorieën gezamenlijk een kleine hoeveelheid van Hallo resultaten toch.
1. Laat het ons opwekken en onze bestaande dataframe converteren (`df`) in een nieuwe dataframe waar elke inspectie wordt weergegeven als een combinatie van schendingen van het label. In ons geval een label van `0.0` vertegenwoordigt een fout optreedt, wordt een label van `1.0` vertegenwoordigt een is voltooid en een label van `-1.0` bepaalde resultaten naast deze twee vertegenwoordigt. We uitfilteren die andere resultaten bij het berekenen van de nieuwe gegevensframe Hallo.

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    toosee welke Hallo gelabeld gegevens lijkt, gaan we één rij ophalen.

        labeledData.take(1)

    Hier ziet u uitvoer Hallo volgende:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a>Een logistic regressiemodel maken van de invoer dataframe Hallo
De laatste taak is tooconvert Hallo gegevens naar een indeling die kan worden geanalyseerd door logistic regression gelabeld. Hallo invoer tooa logistic regression-algoritme moet een reeks *label-functie vector paren*, waarbij 'functie vector' hello vector van de getallen die invoer Hallo-punt. Dus moeten we tooconvert Hallo 'schendingen' kolom, die is semi-gestructureerde en bevat veel opmerkingen in vrije tekst tooan matrix van real-getallen die met een machine gemakkelijk kan begrijpen.

Een standaard machine learning-benadering voor de verwerking van natuurlijke taal is tooassign elk woord distinct 'index' en geeft u een vector toohello machine learning-algoritme dat de waarde voor elke index Hallo relatieve frequentie van dat woord in de tekst hello bevat tekenreeks.

MLlib biedt een eenvoudige manier tooperform deze bewerking. Eerst 'basisvormen' elke schendingen tekenreeks tooget Hallo afzonderlijke woorden in elke tekenreeks. Vervolgens gebruikt u een `HashingTF` tooconvert elke set tokens in een functie-vector vervolgens doorgegeven toohello logistic regression-algoritme tooconstruct worden kan een model. We uitvoeren alle deze stappen in de reeks met behulp van een "pipeline".

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a>Hallo-model op een afzonderlijke testgegevensset evalueren
We kunnen gebruiken we eerder hebben gemaakt Hallo-model te*voorspellen* welke Hallo resultaten van de nieuwe inspecties zijn zal, op basis van Hallo schendingen die zijn waargenomen. We dit model op Hallo gegevensset getraind **Food_Inspections1.csv**. Laat het ons gebruik van een tweede gegevensset **Food_Inspections2.csv**, te*evalueren* Hallo sterkte van dit model op nieuwe gegevens. Deze tweede gegevensverzameling (**Food_Inspections2.csv**) moet al Hallo standaardopslagcontainer die zijn gekoppeld aan het Hallo-cluster.

1. Hallo volgende codefragment maakt een nieuwe dataframe **predictionsDf** die Hallo voorspelling gegenereerd door Hallo model bevat. Hallo-codefragment maakt ook een tijdelijke tabel genaamd **voorspellingen** op basis van Hallo dataframe.

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    Hier ziet u uitvoer Hallo volgende:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. Bekijk een Hallo voorspellingen. In dit fragment uitvoeren:

        predictionsDf.take(1)

   Er is een voorspelling voor Hallo eerste item in de gegevensset Hallo-test.
1. Hallo `model.transform()` methode toepassing hello dezelfde transformatie tooany nieuwe gegevens met Hallo van hetzelfde schema en een voorspelling van hoe tooclassify Hallo gegevens aankomen. Wij kunnen enkele eenvoudige statistieken tooget nu een beeld van hoe nauwkeurig onze voorspellingen zijn:

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    Hallo-uitvoer ziet er Hallo volgende:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    Met behulp van logistic regression met Spark biedt ons een nauwkeurige model van Hallo relatie tussen schendingen beschrijvingen in het Engels en een opgegeven bedrijf zou doorgeven of afbreken van een voeding inspectie.

## <a name="create-a-visual-representation-of-hello-prediction"></a>Een visuele representatie van Hallo voorspelling maken
We kunt nu een definitieve visualisatie toohelp die ons over Hallo resultaten van deze test reden opstellen.

1. Begin met het uitpakken van de verschillende voorspellingen Hallo en resultaten van Hallo **voorspellingen** tijdelijke tabel die eerder hebt gemaakt. Hallo volgende query's scheiden Hallo uitvoer als *true_positive*, *false_positive*, *true_negative*, en *false_negative*. Hallo-query's hieronder, we uitschakelen visualisatie met `-q` en Hallo uitvoer ook op te slaan (met behulp van `-o`) als dataframes die vervolgens kunnen worden gebruikt met Hallo `%%local` verwerkt Magic-pakket.

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. Gebruik tot slot Hallo volgende codefragment toogenerate Hallo tekent met behulp van **Matplotlib**.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Hallo volgende uitvoer weergegeven:

    ![Spark machine learning-uitvoer van de toepassing - cirkeldiagram percentages van mislukte voeding controles. ] (./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning-resultaat-uitvoer")

    In deze grafiek verwijst ' ' positief voeding inspectie van toohello is mislukt, terwijl een negatief resultaat tooa inspectie doorgegeven verwijst.

## <a name="shut-down-hello-notebook"></a>Hallo-notebook afsluiten
Nadat u klaar bent met het uitvoeren van de toepassing hello, moet u Hallo notebook toorelease Hallo resources afgesloten. toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**. Dit wordt afgesloten en wordt gesloten Hallo notebook.

## <a name="seealso"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)
