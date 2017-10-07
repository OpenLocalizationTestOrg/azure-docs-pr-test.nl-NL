---
title: aaaUse ScaleR en SparkR met Azure HDInsight | Microsoft Docs
description: Gebruik ScaleR en SparkR met R Server en HDInsight
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: da732ff0235cf465a1452b81750c7cdd0351eed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a>Een combinatie van ScaleR en SparkR in HDInsight

Dit artikel laat zien hoe toopredict flight aankomst vertragingen met behulp van een **ScaleR** logistic regressiemodel van gegevens op vertragingen en het weer samengevoegd met **SparkR**. Dit scenario wordt getoond Hallo-mogelijkheden van ScaleR voor gegevensmanipulatie op Spark gebruikt met Microsoft R Server voor analyses. Hallo combinatie van deze technologieën kunt u de nieuwste mogelijkheden voor tooapply Hallo in gedistribueerde verwerking.

Hoewel beide pakketten worden uitgevoerd op de engine voor het uitvoeren van Hadoop Spark, hebben ze geen toegang tot gegevens in het geheugen delen als ze elk hun eigen respectieve Spark-sessies vereist. Hallo tijdelijke oplossing wordt Spark-sessies met niet-overlappende toomaintain en tooexchange gegevens via tussenliggende bestanden totdat dit probleem is opgelost in een toekomstige versie van R Server. Hallo instructies hier wordt aangegeven dat deze vereisten eenvoudige tooachieve zijn.

We gebruiken een voorbeeld dat hier in eerste instantie gedeeld in een Neem contact op lagen 2016 door Mario Inchiosa en Roni Burd die ook beschikbaar via Hallo webinar [bouwen van een schaalbare Platform voor wetenschap met R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). Hallo voorbeeld wordt SparkR toojoin Hallo bekende airlines aankomst vertraging gegevensset met de Weergegevens op vertrek en aankomst luchthavens. Hallo gegevens lid wordt vervolgens gebruikt als invoer tooa ScaleR logistic regression-model voor het voorspellen van vlucht aankomst vertraging.

Hallo Codeoverzicht we oorspronkelijk is geschreven voor R Server op Spark in een HDInsight-cluster in Azure. Maar Hallo concept van een combinatie van Hallo gebruik van SparkR en ScaleR in één script is ook geldig in de context Hallo van on-premises omgevingen. In de volgende hello, we gaan ervan uit dat een tussenliggende niveau van de kennis van R en R Hallo [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) bibliotheek van R Server. Wij ook gebruik van introduceren [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) tijdens het doorlopen van dit scenario.

## <a name="hello-airline-and-weather-datasets"></a>Hallo luchtvaartmaatschappij en weer gegevenssets

Hallo **AirOnTime08to12CSV** airlines openbare gegevensset bevat informatie over vlucht aankomst en vertrek details voor alle commerciële vlucht binnen de Verenigde Staten, Hallo van oktober 1987 tooDecember 2012. Dit is een grote gegevensset: Er zijn bijna 150 miljoen records in totaal. Er is iets minder 4 GB uitgepakt. Deze beschikbaar is via Hallo [US government archieven](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236). Gemakkelijker, is beschikbaar als zipbestand (AirOnTimeCSV.zip) met een verzameling van 303 afzonderlijke maandelijkse CSV-bestanden van Hallo [Revolution Analytics gegevensset opslagplaats](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)

toosee hello gevolgen van het weer op vertragingen, er moet ook Hallo Weergegevens op elk Hallo luchthavens. Deze gegevens kan worden gedownload als zip-bestanden in onbewerkte vorm per maand van Hallo [nationale oceanische en het beheer van de opslagplaats](http://www.ncdc.noaa.gov/orders/qclcd/). Voor Hallo toepassing van dit voorbeeld wordt we weergegevens van mei 2007 – December 2012 ophalen en Hallo per uur gegevensbestanden in elk Hallo 68 maandelijkse zips gebruikt. Hallo maandelijkse zip-bestanden ook bevatten geen toewijzing (YYYYMMstation.txt) tussen hello weer station ID (WBAN), Hallo luchthaven dat deze gekoppeld (CallSign is) en Hallo van de luchthaven tijdzoneverschil van UTC (tijdzone). Al deze informatie is nodig bij het samenvoegen met Hallo luchtvaartmaatschappij vertraging en het weer gegevens.

## <a name="setting-up-hello-spark-environment"></a>Hallo Spark-omgeving instellen

de eerste stap Hallo is tooset Hallo Spark-omgeving. We beginnen met het toohello map waarin de invoergegevens mappen aan te wijzen, het maken van een Spark compute-context en het maken van een functie voor logboekregistratie voor informatief logboekregistratie toohello console:

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session tooreduce startup times 
#   (remember toostop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

Naast toevoegen we 'Spark_Home' toohello zoekpad voor R-pakketten zodat we SparkR gebruiken en geen SparkR-sessie starten:

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-hello-weather-data"></a>Hallo weergegevens voorbereiden

tooprepare Hallo weergegevens we subset deze toohello kolommen die nodig zijn voor het modelleren: 

- 'Zichtbaarheid'
- 'DryBulbCelsius'
- 'DewPointCelsius'
- 'RelativeHumidity'
- "Windsnelheid"
- 'Altimeter'

Vervolgens wordt een luchthaven-code die is gekoppeld aan Hallo weer station toevoegen en Hallo metingen van de lokale tijd tooUTC converteren.

We beginnen met het maken van een bestand toomap Hallo weer station (WBAN) info tooan luchthaven-code. We kan deze correlatie van het toewijzingsbestand Hallo opgenomen met Hallo weergegevens ophalen. Door toewijzing Hallo *CallSign* (bijvoorbeeld LAX) veld in Hallo weer gegevensbestand te*oorsprong* in Hallo luchtvaartmaatschappij gegevens. Echter, we zojuist hebben plaatsgevonden toohave een andere toewijzing voorhanden dat is toegewezen *WBAN* te*AirportID* (bijvoorbeeld 12892 voor LAX) en omvat *tijdzone* die tooa is opgeslagen CSV-bestand met de naam 'wban-naar-luchthaven-id-tz. CSV' die u kunt gebruiken. Bijvoorbeeld:

| AirportID | WBAN | Tijdzone
|-----------|------|---------
| 10685 | 54831 | -6
| 14871 | 24232 | -8
| .. | .. | ..

Hallo na code leest, elke Hallo per uur weer onbewerkte gegevens bestanden, subsets toohello kolommen we nodig, samenvoegingen Hallo weer station toewijzingsbestand Hallo datums en tijden van metingen tooUTC aanpast en schrijft vervolgens een nieuwe versie van bestand Hallo:

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a>Hallo luchtvaartmaatschappij en weer gegevens tooSpark DataFrames importeren

Nu we Hallo SparkR gebruiken [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) tooimport Hallo weer en luchtvaartmaatschappij gegevens tooSpark DataFrames werken. Deze functie, zoals veel andere methoden Spark uitgevoerd vertraagd, wat betekent dat ze in de wachtrij voor uitvoering maar niet uitgevoerd totdat vereist.

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for hello airline data

logmsg('create a SparkR DataFrame for hello airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for hello weather data

logmsg('create a SparkR DataFrame for hello weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a>Gegevens worden opgeschoond en transformatie

Naast doen we enkele opschonen op Hallo luchtvaartmaatschappij gegevens we toorename kolommen hebt geïmporteerd. We alleen Hallo variabelen nodig houden en geplande vertrektijd omlaag toohello dichtstbijzijnde uur tooenable samenvoegen met de meest recente weergegevens bij vertrek Hallo afronden:

```
logmsg('clean hello airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from hello flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time toofull hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

Nu we vergelijkbare bewerkingen uitvoeren op Hallo weergegevens:

```
# Average weather readings by hour
logmsg('clean hello weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-hello-weather-and-airline-data"></a>Het koppelen van de gegevens weer en luchtvaartmaatschappij Hallo

Nu gebruiken we Hallo SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) werken toodo een linker outer join Hallo luchtvaartmaatschappij en weer gegevens door vertrek AirportID en datetime. Hallo outer join kan wij tooretain alle Hallo luchtvaartmaatschappij gegevens registreert, zelfs als er zijn geen overeenkomende weergegevens. Volgende Hallo join we enkele overbodige kolommen verwijderen en wijzig de naam Hallo bewaard kolommen tooremove Hallo binnenkomende DataFrame voorvoegsel geïntroduceerd door Hallo join.

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

Op soortgelijke wijze aanmelden we Hallo weer en luchtvaartmaatschappij gegevens op basis van de aankomst AirportID en datum/tijd:

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-toocsv-for-exchange-with-scaler"></a>Opslaan van resultaten tooCSV voor exchange met ScaleR

Hallo joins moeten we toodo met SparkR is voltooid. We Hallo gegevens van Hallo laatste Spark DataFrame 'joinedDF5' tooa CSV voor invoer tooScaleR opslaan en sluit vervolgens af Hallo SparkR sessie. We SparkR toosave expliciet vertellen Hallo resulterende CSV in 80 afzonderlijke partities tooenable voldoende parallelle uitvoering bij het verwerken van ScaleR:

```
logmsg('output hello joined data from Spark tooCSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result toodirectory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down hello SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-tooxdf-for-use-by-scaler"></a>TooXDF voor gebruik door ScaleR importeren

Hallo CSV-bestand van de gekoppelde luchtvaartmaatschappij en de weergegevens als kan worden gebruikt-is voor het modelleren via een ScaleR tekst-gegevensbron. Maar we importeren tooXDF eerst, omdat het is efficiënter wanneer meerdere bewerkingen op Hallo gegevensset wordt uitgevoerd:

```
logmsg('Import hello CSV toocompressed, binary XDF format') 

# set hello Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a>Gegevens voor trainings- en testset splitsen

We rxDataStep toosplit Hallo 2012 gegevens gebruiken voor het testen en behouden Hallo rest voor training:

```
# split out hello training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out hello testing data

logmsg('split out hello test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a>Trainen en te testen van een logistic regressiemodel

We zijn nu gereed toobuild een model. toosee Hallo invloed van de weergegevens voor de vertraging in aankomsttijd Hallo, gebruiken we de ScaleR logistic regression routine. We gebruiken deze toomodel of een vertraging van de aankomst van meer dan 15 minuten wordt beïnvloed door Hallo weer op Hallo vertrek en aankomst luchthavens:

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use hello scalable rxLogit() function but set max iterations too3 for hello purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

Nu gaan we kijken hoe deze op Hallo test gegevens door te maken van sommige voorspellingen en ROC en AUC kijken.

```
# Predict over test data (Logistic Regression).

logmsg('predict over hello test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use hello scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under hello Curve (AUC).

logmsg('calculate hello roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a>Score berekenen elders

We kunnen ook Hallo model gebruiken voor scoreprofiel gegevens op een ander platform. Door tooan RDS-bestand opslaan en dragen en die RDS importeren in een bestemming score berekenen omgeving zoals SQL Server-R-Services. Het is belangrijk tooensure die Hallo factorniveaus van Hallo gegevens toobe berekend overeenkomen met die op welke Hallo model is opgebouwd. Dat overeenkomst kan worden bereikt door uit te pakken en opslaan kolomgegevens Hallo gekoppeld aan Hallo modelleren van gegevens via de ScaleR `rxCreateColInfo()` functie en vervolgens toe te passen die kolom informatie toohello invoergegevens bron voor de prognose. In de volgende Hallo we een paar rijen van de testgegevensset Hallo opslaan en ophalen en gebruik Hallo kolom van dit voorbeeld in Hallo voorspelling script:

```
# save hello model and a sample of hello test dataset 

logmsg('save serialized version of hello model and a sample of hello test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop hello spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a>Samenvatting

In dit artikel hebben we zien hoe het gebruik van de mogelijke toocombine van SparkR voor gegevensmanipulatie met ScaleR voor model-ontwikkeling in Hadoop Spark is. Dit scenario vereist onderhouden afzonderlijke Spark-sessies, met slechts één sessie op een tijdstip en uitwisselen van gegevens via de CSV-bestanden. Hoewel eenvoudige, moet dit proces nog gemakkelijker in een toekomstige release R Server bij SparkR en ScaleR delen van een Spark-sessie en dus Spark DataFrames delen.

## <a name="next-steps-and-more-information"></a>Volgende stappen en meer informatie

- Zie voor meer informatie over gebruik van R Server op Spark Hallo [aan de slag-gids op MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)

- Raadpleeg voor algemene informatie op R Server Hallo [aan de slag met R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) artikel.

- Zie voor informatie over op HDInsight R Server, [R Server op Azure HDInsight overzicht](hdinsight-hadoop-r-server-overview.md) en [op Azure HDInsight R Server](hdinsight-hadoop-r-server-get-started.md).

Zie voor meer informatie over gebruik van SparkR:

- [Apache SparkR document](https://spark.apache.org/docs/2.1.0/sparkr.html)

- [Overzicht van SparkR](https://docs.databricks.com/spark/latest/sparkr/overview.html) van Databricks
