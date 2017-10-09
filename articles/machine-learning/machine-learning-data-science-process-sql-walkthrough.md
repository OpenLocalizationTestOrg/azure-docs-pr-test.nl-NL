---
title: aaaBuild en implementeren van een machine learning-model met SQL Server op een virtuele machine in Azure | Microsoft-Docs
description: Geavanceerde analyses proces en de technologie in actie
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a>Hallo Team gegevens wetenschappelijke processen in actie: met behulp van SQL Server
In deze zelfstudie helpt u bij het Hallo-proces voor het maken en implementeren van een machine learning-model met behulp van SQL Server en een openbare gegevensset--hello [NYC Taxi reizen](http://www.andresmh.com/nyctaxitrips/) gegevensset. Hallo procedure volgt een standaard wetenschappelijke werkstroom: opnemen en Hallo gegevens verkennen, functies toofacilitate learning, engineering en vervolgens bouwen en implementeren van een model.

## <a name="dataset"></a>NYC Taxi reizen gegevensset beschrijving
Hallo NYC Taxi reis gegevens is ongeveer 20GB gecomprimeerde CSV-bestanden (~ 48GB ongecomprimeerde), die bestaat uit meer dan 173 miljoen afzonderlijke reizen en Hallo ervoor staat voor elke reis betaald. Elke record reis omvat Hallo ophalen en inleverbibliotheek locatie en tijd, geanonimiseerde hack (van stuurprogramma) licentienummer en nummer straten (taxi van unieke id). Hallo-gegevens bevat informatie over alle reizen Hallo jaar 2013 en is beschikbaar in twee gegevenssets voor elke maand na Hallo:

1. Hallo 'trip_data' CSV bevat reis details, zoals het aantal passagiers, ophalen en dropoff punten reis duur en duur van reis. Hier volgen enkele voorbeeldrecords:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Hello trip_fare CSV details van Hallo tarief betaald voor elke reis, zoals betalingstype tarief bedrag, extra kosten en belastingen, tips en tolgelden en Hallo totaalbedrag betaald bevat. Hier volgen enkele voorbeeldrecords:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hallo unieke sleutel toojoin reis\_gegevens en reis\_tarief dat bestaat uit Hallo velden: straten, hack\_en ophalen van certificaat\_datetime.

## <a name="mltasks"></a>Voorbeelden van voorspelling taken
We drie voorspelling problemen op basis van Hallo wordt formuleren *tip\_bedrag*, namelijk:

1. Binaire classificatie: voorspellen of een tip betaald is voor een reis, dat wil zeggen een *tip\_bedrag* die groter is dan $0 een voorbeeld van een positieve is, terwijl een *tip\_bedrag* van $0 is een voorbeeld van een negatief.
2. Multiklassen classificatie: toopredict Hallo bereik van een tip voor Hallo reis betaald. We delen Hallo *tip\_bedrag* in vijf opslaglocaties of klassen:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. Taak regressie: toopredict Hallo hoeveelheid tip voor een reis betaald.  

## <a name="setup"></a>Instellen hello Azure gegevens wetenschappelijke omgeving voor geavanceerde analyses
Zoals u van Hallo zien kunt [uw omgeving plannen](machine-learning-data-science-plan-your-environment.md) handleiding, er zijn verschillende opties toowork met Hallo NYC Taxi reizen gegevensset in Azure:

* Werken met gegevens in Azure blobs Hallo vervolgens Azure Machine Learning-model
* Hallo gegevens laden in een SQL Server-database en de Azure Machine Learning-model

In deze zelfstudie wordt gedemonstreerd parallelle bulkimport van Hallo gegevens tooa SQL Server, gegevensverkenning, functie engineering en omlaag sampling met behulp van SQL Server Management Studio, alsmede IPython laptop gebruiken. [Voorbeeld van scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) en [IPython notitieblokken](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) in GitHub worden gedeeld. Een voorbeeld IPython notebook toowork met Hallo-gegevens in Azure BLOB's is ook beschikbaar in Hallo dezelfde locatie.

tooset van uw omgeving voor Gegevenswetenschap Azure:

1. [Een opslagaccount maken](../storage/common/storage-create-storage-account.md)
2. [Een Azure Machine Learning-werkruimte maken](machine-learning-create-workspace.md)
3. [Inrichten van een virtuele Machine van de gegevens wetenschappelijke](machine-learning-data-science-setup-sql-server-virtual-machine.md), waarmee u een SQL-Server en een IPython laptop-server.
   
   > [!NOTE]
   > Hallo-voorbeeldscripts en IPython notitieblokken gedownloade tooyour Gegevenswetenschap virtuele machine worden tijdens het installatieproces Hallo. Wanneer Hallo VM-script voor na de installatie is voltooid, zijn Hallo voorbeelden in de bibliotheek documenten van de VM:  
   > 
   > * Voorbeeld Scripts:`C:\Users\<user_name>\Documents\Data Science Scripts`  
   > * Voorbeeld IPython notitieblokken:`C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`  
   >   waar `<user_name>` is Windows-aanmeldingsnaam van de VM. Toohello voorbeeld mappen als wordt verwezen **voorbeeldscripts** en **voorbeeld IPython notitieblokken**.
   > 
   > 

Op basis van Hallo gegevensset grootte, de locatie van de gegevensbron en Hallo geselecteerde Azure doelomgeving, dit scenario is vergelijkbaar te[Scenario \#5: grote gegevensset in een lokale bestanden doel-SQL-Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).

## <a name="getdata"></a>Hallo gegevens ophalen uit de openbare bron
Hallo tooget [NYC Taxi reizen](http://www.andresmh.com/nyctaxitrips/) gegevensset van de openbare locatie, mag u Hallo-methoden die zijn beschreven in [gegevens verplaatsen tooand uit Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy Hallo gegevens tooyour nieuwe virtuele machine.

toocopy hello gegevens met behulp van AzCopy:

1. Meld u bij tooyour virtuele machine (VM)
2. Een nieuwe map maken in de gegevensschijf Hallo van de virtuele machine (Opmerking: gebruik geen tijdelijke schijf die wordt geleverd bij de virtuele machine als een gegevensschijf Hallo Hallo).
3. Voer Hallo Azcopy-opdrachtregel de volgende, waarbij < path_to_data_folder > vervangt door de gegevensmap van uw in (2) gemaakt in een opdrachtpromptvenster:
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    Wanneer Hallo AzCopy is voltooid, in totaal 24 ingepakte CSV-bestanden (12 voor reis\_gegevens en 12 voor reis\_tarief) moet in de map data Hallo.
4. Pak de bestanden gedownload Hallo. Houd er rekening mee Hallo map waar Hallo ongecomprimeerde bestanden zich bevinden. Deze map worden waarnaar wordt verwezen tooas Hallo < pad\_naar\_gegevens\_bestanden\>.

## <a name="dbload"></a>Gegevens voor bulksgewijs importeren in SQL Server-Database
Hallo prestaties laden/overdracht van grote hoeveelheden gegevens tooan SQL-database en de volgende query's kunnen worden verbeterd via *gepartitioneerde tabellen en weergaven*. In deze sectie zult we Hallo-instructies die worden beschreven [parallelle bulksgewijs gegevens importeren met behulp van SQL partitietabellen](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate een nieuwe database en Hallo gegevens laden in gepartitioneerde tabellen parallel.

1. Terwijl u bent aangemeld tooyour VM, start **SQL Server Management Studio**.
2. Verbinding maken met Windows-verificatie.
   
    ![SSMS verbinden][12]
3. Als u hebt nog niet gewijzigd Hallo SQL Server-verificatiemodus en een nieuwe SQL-aanmeldingsgebruiker gemaakt, opent u Hallo scriptbestand met de naam **wijzigen\_auth.sql** in Hallo **voorbeeldscripts** map. Hallo standaard-gebruikersnaam en wachtwoord wijzigen. Klik op **! Uitvoeren van** in Hallo werkbalk toorun Hallo script.
   
    ![Script uitvoeren][13]
4. Controleren en/of SQL Server standaard database en logboekbestanden mappen tooensure die zojuist databases gemaakt worden opgeslagen in een gegevensschijf Hallo wijzigen. Hallo SQL Server VM-installatiekopie die is geoptimaliseerd voor datawarehousing belastingen is vooraf geconfigureerd met gegevens en logboekbestanden schijven. Als u nieuwe virtuele harde schijven toegevoegd tijdens het Hallo VM-installatieproces uw virtuele machine bevat geen een gegevensschijf Hallo standaardmappen als volgt te wijzigen:
   
   * Klik met de rechtermuisknop Hallo SQL-servernaam in Hallo links deelvenster en klik op **eigenschappen**.
     
       ![Eigenschappen van SQL Server][14]
   * Selecteer **Database-instellingen** van Hallo **een pagina selecteren** toohello links lijst.
   * Controleren en/of Hallo wijzigen **Database standaardlocaties** toohello **gegevensschijf** locaties van uw keuze. Dit is waar nieuwe databases zich bevinden als gemaakt met de standaardinstellingen locatie Hallo.
     
       ![Standaardinstellingen van de SQL-Database][15]  
5. toocreate een nieuwe database en een set bestandsgroepen toohold Hallo gepartitioneerde tabellen, opent u het voorbeeldscript Hallo **maken\_db\_default.sql**. Hallo script maakt een nieuwe database met de naam **TaxiNYC** en 12 bestandsgroepen op Hallo gegevens standaardlocatie. Elke bestandsgroep bevatten één maand in reis\_gegevens en reis\_ritbedrag gegevens. Wijzig de databasenaam hello, desgewenst. Klik op **! Uitvoeren van** toorun Hallo script.
6. Maak vervolgens twee partitietabellen, één voor Hallo reis\_gegevens en een andere voor Hallo reis\_tarief. Hallo-voorbeeldscript Open **maken\_gepartitioneerde\_table.sql**, die wordt:
   
   * Maak een partitie functie toosplit Hallo gegevens per maand.
   * Maak een partitie schema toomap elke maand gegevens tooa andere bestandsgroep.
   * Maken van twee partitieschema van gepartitioneerde tabellen toegewezen toohello: **nyctaxi\_reis** bevatten Hallo reis\_gegevens en **nyctaxi\_tarief** Hallo reis bevatten \_ritbedrag gegevens.
     
     Klik op **! Uitvoeren van** toorun Hallo script en Hallo gepartitioneerde tabellen maken.
7. In Hallo **voorbeeldscripts** map, er zijn twee PowerShell-voorbeeldscripts opgegeven toodemonstrate parallelle bulkimport gegevenstabellen tooSQL-Server.
   
   * **BCP\_parallelle\_generic.ps1** is een algemeen script tooparallel bulksgewijs Importeer gegevens in een tabel. Wijzig dit script tooset Hallo invoer- en variabelen zoals aangegeven in de regels met opmerkingen in script Hallo Hallo.
   * **BCP\_parallelle\_nyctaxi.ps1** is een vooraf geconfigureerde versie van de algemene script Hallo en gebruikte tootooload beide tabellen voor Hallo NYC Taxi reizen gegevens kan worden.  
8. Klik met de rechtermuisknop Hallo **bcp\_parallelle\_nyctaxi.ps1** scriptnaam en klikt u op **bewerken** tooopen in PowerShell. Revisie Hallo vooraf ingestelde variabelen en wijzigen van de naam van de geselecteerde database volgens tooyour, invoergegevens map doelmap logboek en paden toohello voorbeeldbestanden indeling **nyctaxi_trip.xml** en **nyctaxi\_ fare.XML** (opgegeven in Hallo **voorbeeldscripts** map).
   
    ![Gegevens voor bulksgewijs importeren][16]
   
    U kunt ook Hallo verificatiemodus selecteren, standaard Windows-verificatie. Klik op Hallo groene pijl in Hallo werkbalk toorun. Hallo-script wordt gestart, 24 importeren bulkbewerkingen in parallelle 12 voor elke gepartitioneerde tabel. U kunt voortgang Hallo gegevens importeren door het Hallo-standaardgegevensmap voor SQL Server te openen als hierboven.
9. Hallo PowerShell script rapporten Hallo begin- en eindtijd. Wanneer alle bulksgewijs invoer is voltooid, wordt de Hallo eindtijd gerapporteerd. Controleer Hallo doel logboek map tooverify die Hallo bulkimport is gelukt, dat wil zeggen, er geen fouten in de doelmap logboek Hallo gemeld.
10. Uw database is nu gereed voor exploratie, functie-engineering en andere bewerkingen. Aangezien Hallo tabellen worden gepartitioneerd volgens toohello **ophalen\_datetime** veld, query's, waaronder **ophalen\_datetime** voorwaarden in Hallo  **WAAR** component profiteert van Hallo partitieschema.
11. In **SQL Server Management Studio**, verkennen Hallo opgegeven voorbeeldscript **voorbeeld\_queries.sql**. toorun van Hallo voorbeeldquery's markeren Hallo regels query en klik vervolgens op **! Uitvoeren van** op Hallo-werkbalk.
12. Hallo NYC Taxi reizen gegevens is geladen in twee afzonderlijke tabellen. tooimprove join-bewerkingen, het is raadzaam tooindex Hallo tabellen. Hallo voorbeeldscript **maken\_gepartitioneerde\_index.sql** maakt gepartitioneerde indexen op Hallo samengestelde join-sleutel **straten, hack\_licentie en ophalen\_datetime**.

## <a name="dbexplore"></a>Gegevensverkenning en functie-Engineering in SQL Server
In deze sectie voert we gegevens te verkennen en functie genereren met behulp van SQL-query's rechtstreeks in Hallo **SQL Server Management Studio** met behulp van SQL Server-database Hallo eerder hebt gemaakt. Een voorbeeld van een script met de naam **voorbeeld\_queries.sql** vindt u in Hallo **voorbeeldscripts** map. Hallo script toochange Hallo-databasenaam wijzigen als deze van de standaard Hallo verschilt: **TaxiNYC**.

In deze oefening wordt:

* Verbinding te maken met**SQL Server Management Studio** met behulp van op Windows-verificatie of via SQL-verificatie en Hallo SQL-aanmeldingsnaam en wachtwoord.
* Verken de gegevens distributies van enkele velden in verschillende tijdvensters.
* Onderzoek de kwaliteit van de gegevens van Hallo breedtegraad velden.
* Genereren van binaire en multiklassen classificatielabels op basis van Hallo **tip\_bedrag**.
* Genereren van functies en reis afstanden compute/vergelijken.
* Hallo twee tabellen samenvoegen en uitpakken van een steekproef die gebruikt toobuild modellen worden.

Wanneer u klaar tooproceed tooAzure Machine Learning bent, mag u ofwel:  

1. Sla Hallo uiteindelijke SQL query tooextract en voorbeeld Hallo gegevens en kopiëren en plakken Hallo query rechtstreeks in een [importgegevens] [ import-data] -module in Azure Machine Learning, of
2. Hallo door actieve behouden en engineering gegevens die u van plan bent toouse voor model bouwen in een nieuwe database tabel en nieuwe tabel Hallo gebruiken in Hallo [importgegevens] [ import-data] -module in Azure Machine Learning.

In deze sectie wordt we Hallo laatste querybewerking tooextract en voorbeeld Hallo gegevens opslaan. de tweede methode Hello wordt geïllustreerd in Hallo [Gegevensverkenning en functie-Engineering in IPython Notebook](#ipnb) sectie.

Voor een snelle verificatie van Hallo aantal rijen en kolommen in hello in tabellen ingevuld eerder met parallelle bulkimport,

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a>Exploratie: Reis distributie door straten
In dit voorbeeld identificeert Hallo straten (taxi getallen) met meer dan 100 reizen binnen een bepaalde periode. Hallo query wilt profiteren van Hallo gepartitioneerde tabeltoegang omdat deze wordt waarbij door Hallo partitieschema van **ophalen\_datetime**. Opvragen van de volledige gegevensset Hallo maakt ook gebruik van de gepartitioneerde tabel Hallo en/of index van de scan.

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploratie: Reis distributie door straten en hack_license
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Gegevens beoordeling: Controleer of records met onjuiste lengtegraad en/of breedtegraad
In dit voorbeeld onderzoekt als Hallo lengtegraad en/of breedtegraad velden een ongeldige waarde bevatten (radiaal graden moet tussen-90 en 90), of (0, 0) coördinaten.

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Exploratie: Gekantelde vs. Niet reizen punt distributie
Dit voorbeeld wordt gezocht naar Hallo aantal reizen die zijn punt versus geen punt in een bepaald moment periode (of in de volledige gegevensset Hallo als die betrekking hebben op Hallo volledige jaar). Deze verdeling weerspiegelt Hallo binaire label distributie toobe later gebruikt voor het modelleren van de binaire indeling.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a>Exploratie: Tip distributie van de klasse-bereik
In dit voorbeeld berekent Hallo distributie van tip bereiken in een bepaald moment periode (of in de volledige gegevensset Hallo als die betrekking hebben op Hallo volledige jaar). Dit is distributiepunt Hallo Hallo label klassen die later wordt gebruikt voor multiklassen classificatie modellering.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a>Exploratie: Berekenen en reis afstand vergelijken
In dit voorbeeld Hallo ophalen en inleverbibliotheek lengtegraad converteert en breedtegraad tooSQL Geografie verwijst, Hallo reis afstand met behulp van SQL Geografie punten verschil wordt berekend en retourneert een willekeurig aantal Hallo resultaten voor vergelijking. Hallo voorbeeld beperkt Hallo resultaten toovalid coördineert alleen met behulp van Hallo kwaliteit assessment gegevensquery eerder besproken.

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a>Functie-Engineering in SQL-query 's
Hallo label genereren en Geografie conversie exploratie query's kunnen ook gebruikte toogenerate labels en-functies worden door het verwijderen van onderdeel tellen Hallo. Voorbeelden van technische SQL aanvullende functies zijn beschikbaar in Hallo [Gegevensverkenning en functie-Engineering in IPython Notebook](#ipnb) sectie. Het is efficiënter toorun Hallo functie generatie query's in de volledige gegevensset hello of een grote subset van met behulp van SQL-query's die rechtstreeks op Hallo SQL Server database-exemplaar worden uitgevoerd. Hallo-query's kunnen worden uitgevoerd in **SQL Server Management Studio**, IPython laptop of elk hulpprogramma/ontwikkelomgeving die toegang heeft tot database Hallo lokaal of extern.

#### <a name="preparing-data-for-model-building"></a>Voorbereiden van gegevens voor het Model bouwen
Hallo volgende joins Hallo query **nyctaxi\_reis** en **nyctaxi\_tarief** tabellen, genereert een label binaire classificatie **punt**, een meerdere klasse classificatie label **tip\_klasse**, en extraheert met een willekeurige steekproef 1% uit Hallo volledige gekoppelde gegevensset. Deze query kan worden gekopieerd en geplakt rechtstreeks in Hallo [Azure Machine Learning Studio](https://studio.azureml.net) [importgegevens] [ import-data] -module voor directe gegevensopname van Hallo SQL Server-database exemplaar in Azure. Hallo query worden records met onjuiste uitgesloten (0, 0) coördinaten.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <a name="ipnb"></a>Gegevensverkenning en functie-Engineering in IPython Notebook
In deze sectie wordt uitgevoerd, er gegevensverkenning en functie genereren met behulp van Python- en SQL-query's op Hallo SQL Server-database eerder hebt gemaakt. Een voorbeeld IPython notebook met de naam **machine-Learning-data-science-process-sql-story.ipynb** vindt u in Hallo **voorbeeld IPython notitieblokken** map. Deze laptop is ook beschikbaar op [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).

Hallo aanbevolen volgorde bij het werken met big data is Hallo volgende:

* Gelezen in een klein aantal Hallo gegevens in een kader gegevens in het geheugen.
* Uitvoeren van sommige visualisaties en explorations met Hallo steekproefgegevens.
* Experiment met functie-engineering Hallo met voorbeeldgegevens.
* Voor grotere gegevensverkenning gebruiken voor gegevensmanipulatie en functie-engineering, Python tooissue SQL-query's rechtstreeks op Hallo SQL Server-database in hello Azure VM.
* Bepaal Hallo voorbeeld grootte toouse voor het bouwen van Azure Machine Learning-model.

Als u klaar bent tooproceed tooAzure Machine Learning, mag u ofwel:  

1. Sla Hallo uiteindelijke SQL query tooextract en voorbeeld Hallo gegevens en kopiëren en plakken Hallo query rechtstreeks in een [importgegevens] [ import-data] -module in Azure Machine Learning. Deze methode wordt geïllustreerd in Hallo [gebouw modellen in Azure Machine Learning](#mlmodel) sectie.    
2. Hallo door actieve en engineering gegevens die u van plan bent toouse voor model bouwen in een nieuwe database behouden en gebruik deze nieuwe tabel Hallo in Hallo [importgegevens] [ import-data] module.

Hallo volgen een paar gegevensverkenning: gegevensvisualisatie en voorbeelden engineering-functie. Zie voor meer voorbeelden Hallo voorbeeld SQL IPython laptop in Hallo **voorbeeld IPython notitieblokken** map.

#### <a name="initialize-database-credentials"></a>Databasereferenties initialiseren
De verbindingsinstellingen voor database in de volgende variabelen Hallo initialiseren:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a>Databaseverbinding maken
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Rapport aantal rijen en kolommen in tabel nyctaxi_trip
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Totale aantal rijen 173179759 =  
* Totale aantal kolommen = 14

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a>Lees in een kleine hoeveelheden gegevens voorbeeld Hallo SQL Server-Database
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Tijd tooread Hallo-voorbeeldtabel is 6.492000 seconden  
Aantal rijen en kolommen opgehaald = (84952, 21)

#### <a name="descriptive-statistics"></a>Beschrijvende statistiek
U bent nu klaar tooexplore Hallo door actieve gegevens. We beginnen met de beschrijvende statistieken voor Hallo kijken **reis\_afstand** (of andere) sleutelvelden:

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a>Visualisatie: Voorbeeld van grafiek
Vervolgens kijken we Hallo BoxPlot voor Hallo reis afstand toovisualize hello quantiles

    df1.boxplot(column='trip_distance',return_type='dict')

![Tekenen van #1][1]

#### <a name="visualization-distribution-plot-example"></a>Visualisatie: Distributie tekent voorbeeld
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Tekenen van #2][2]

#### <a name="visualization-bar-and-line-plots"></a>Visualisatie: De balk en de regel waarnemingspunten
In dit voorbeeld we Hallo reis afstand in vijf opslaglocaties bin en visualiseren Hallo binning resultaten.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

We kunnen tekenen Hallo hierboven bin distributie in een balk of regel tekent zoals hieronder

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Tekenen van #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Tekenen van #4][4]

#### <a name="visualization-scatterplot-example"></a>Visualisatie: Scatterplot voorbeeld
Laten we zien spreidingsgrafiek tekent tussen **reis\_tijd\_in\_sec** en **reis\_afstand** toosee als er correlatie

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![#6 tekenen][6]

We kunnen op dezelfde manier controleren of Hallo relatie tussen **snelheid\_code** en **reis\_afstand**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![#8 tekenen][8]

### <a name="sub-sampling-hello-data-in-sql"></a>Onderliggende steekproeven Hallo gegevens in SQL
Bij het voorbereiden van gegevens voor model bouwen in [Azure Machine Learning Studio](https://studio.azureml.net), desgewenst kunt u ofwel op Hallo **toouse voor SQL-query rechtstreeks in Hallo importgegevens module** of Hallo is ontworpen en actieve behouden gegevens in een nieuwe tabel, kunt u in Hallo [importgegevens] [ import-data] module met een eenvoudige **Selecteer * FROM < uw\_nieuwe\_tabel\_name >**.

In deze sectie we maken een nieuwe tabel toohold Hallo door actieve en engineering gegevens. Een voorbeeld van een directe SQL-query voor het model bouwen wordt verstrekt in Hallo [Gegevensverkenning en functie-Engineering in SQL Server](#dbexplore) sectie.

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a>Maak een voorbeeldtabel en Populate met % 1 van Hallo die lid zijn van tabellen. Verwijderen in de eerste tabel als deze bestaat.
In deze sectie we Hallo-tabellen samenvoegen **nyctaxi\_reis** en **nyctaxi\_tarief**, ophalen van een steekproef van 1% en Hallo door actieve gegevens in de naam van een nieuwe tabel behouden  **nyctaxi\_één\_procent**:

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a>Gegevensverkenning met SQL-query's in IPython Notebook
In deze sectie besproken voor gegevens distributies met Hallo 1-% actieve gegevens op die wordt bewaard in de nieuwe tabel Hallo die we eerder hebben gemaakt. Houd er rekening mee dat vergelijkbare explorations kunnen worden uitgevoerd met behulp van de oorspronkelijke tabellen hello, waarbij optioneel **TABLESAMPLE** toolimit Hallo exploratie voorbeeld of door het beperken van Hallo resulteert tooa opgegeven tijdsperiode Hallo **ophalen \_datetime** partities, zoals geïllustreerd in Hallo [Gegevensverkenning en functie-Engineering in SQL Server](#dbexplore) sectie.

#### <a name="exploration-daily-distribution-of-trips"></a>Exploratie: Dagelijkse distributie van reizen
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Exploratie: Reis distributie per straten
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a>Functie genereren met behulp van SQL-query's in IPython Notebook
In deze sectie er nieuwe labels worden gegenereerd en functies direct met SQL-query's, op Hallo 1% voorbeeldtabel we gemaakt in de vorige sectie Hallo.

#### <a name="label-generation-generate-class-labels"></a>Label generatie: Labels van de klasse te genereren
In Hallo voorbeeld te volgen, er twee sets met labels toouse voor modellering gegenereerd:

1. Binaire klasse Labels **punt** (als een tip krijgt voorspellen)
2. Multiklassen Labels **tip\_klasse** (voorspellen Hallo tip bin of bereik)
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a>Functie-Engineering: Aantal functies voor Categorische kolommen
In dit voorbeeld transformeert een categorische veld in een numeriek veld door te vervangen elke categorie met Hallo telling van de instanties in Hallo-gegevens.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a>Functie-Engineering: Bin functies voor numerieke kolommen
In dit voorbeeld transformeert een continue numeriek veld in de vooraf ingestelde categorie bereiken, numeriek veld dat wil zeggen, transformatie in een categorische veld.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a>Functie-Engineering: Functies van de locatie van decimale breedtegraad/lengtegraad uitpakken
In dit voorbeeld uitvalt Hallo decimale weergave van een veld breedtegraad en/of lengtegraad in meerdere regio velden van verschillende mate van granulatie, zoals land, stad, stad, blok, enzovoort. Hallo nieuwe geo-velden zijn niet toegewezen tooactual locaties. Zie voor informatie over toewijzing geocode locaties, [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Controleer of de uiteindelijke vorm Hallo van Hallo featurized tabel
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

Er zijn nu gereed tooproceed toomodel bouwen en implementeren van modellen in [Azure Machine Learning](https://studio.azureml.net). Hallo-gegevens is gereed voor Hallo voorspelling problemen geïdentificeerd eerder, namelijk:

1. Binaire classificatie: toopredict al dan niet een tip voor een zakenreis is betaald.
2. Multiklassen classificatie: toopredict Hallo bereik van een tip betaald, toohello op basis van vooraf gedefinieerde klassen.
3. Taak regressie: toopredict Hallo hoeveelheid tip voor een reis betaald.  

## <a name="mlmodel"></a>Gebouw modellen in Azure Machine Learning
toobegin Hallo oefening modelleren, meld u bij tooyour Azure Machine Learning-werkruimte. Als u nog geen een machine learning-werkruimte hebt gemaakt, raadpleegt u [maken van een Azure Machine Learning-werkruimte](machine-learning-create-workspace.md).

1. de slag met Azure Machine Learning tooget Zie [wat is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)
2. Meld u bij te[Azure Machine Learning Studio](https://studio.azureml.net).
3. Hallo-startpagina Studio biedt een schat aan informatie, video's, zelfstudies, koppelingen toohello Modules verwijzing en andere bronnen. Raadpleeg voor meer informatie over Azure Machine Learning Hallo [Azure Machine Learning-documentatiecentrum](https://azure.microsoft.com/documentation/services/machine-learning/).

Een typische trainingsexperiment bestaat uit Hallo volgende:

1. Maak een **+ nieuw** experimenteren.
2. Hallo gegevens tooAzure Machine Learning ophalen.
3. Vooraf verwerken, transformeren en manipuleren van Hallo gegevens zo nodig.
4. Genereren onderdelen naar behoefte.
5. Hallo gegevens splitsen in training/testen/validatie gegevenssets (of afzonderlijke gegevenssets hebben voor elk).
6. Selecteer een of meer machine learning-algoritmen, afhankelijk van Hallo probleem toosolve leren. Bijvoorbeeld binaire classificatie, multiklassen classificatie, regressie.
7. Een of meer modellen Hallo training gegevensset met trainen.
8. Hallo validatie gegevensset met Hallo getraind modellen beoordelen.
9. Hallo modellen toocompute Hallo relevante meetgegevens voor Hallo learning probleem evalueren.
10. Afstellen Hallo modellen en selecteer Hallo best model toodeploy.

In deze oefening hebben we al verkend en engineering Hallo-gegevens in SQL Server en besloten op Hallo voorbeeld grootte tooingest in Azure Machine Learning. toobuild een of meer van de Hallo voorspellende modellen die we besloten:

1. Hallo gegevens tooAzure Machine Learning ophalen met behulp van Hallo [gegevens importeren] [ import-data] module beschikbaar in Hallo **gegevensinvoer en uitvoer** sectie. Zie voor meer informatie, Hallo [importgegevens] [ import-data] verwijzingspagina module.
   
    ![Gegevens van Azure Machine Learning importeren][17]
2. Selecteer **Azure SQL Database** als Hallo **gegevensbron** in Hallo **eigenschappen** Configuratiescherm.
3. Voer Hallo database DNS-naam in Hallo **databaseservernaam** veld. Indeling:`tcp:<your_virtual_machine_DNS_name>,1433`
4. Voer Hallo **databasenaam** in het bijbehorende veld Hallo.
5. Voer Hallo **SQL-gebruikersnaam** in Hallo ** Server aqccount gebruikersnaam en wachtwoord in Hallo Hallo **Server het wachtwoord voor gebruikersaccount**.
6. Controleer **accepteren servercertificaat** optie.
7. In Hallo **databasequery** bewerken van tekst, Hallo query welke uitgepakt Hallo nodig databasevelden (inclusief eventuele berekende velden zoals Hallo labels) en pijl-omlaag voorbeelden Hallo gegevens toohello gewenst samplegrootte plakken.

Een voorbeeld van een binaire indeling experiment lezen van gegevens rechtstreeks van Hallo SQL Server-database is in Hallo afbeelding hieronder. Vergelijkbare experimenten kunnen worden samengesteld voor multiklassen classificatie en regressie problemen.

![Azure Machine Learning Train][10]

> [!IMPORTANT]
> In Hallo modelleren ophalen van gegevens en wordt de query-voorbeelden die zijn opgegeven in de vorige secties **alle labels voor Hallo drie modellering oefeningen zijn opgenomen in de query Hallo**. Een belangrijke (vereist) stap in elk Hallo modelleren oefeningen is te**uitsluiten** onnodige labels voor Hallo Hallo andere twee problemen en andere **doel lekken**. Voor bijvoorbeeld bij gebruik van binaire classificatie gebruiken Hallo label **punt** en Hallo velden uitsluiten **tip\_klasse**, **tip\_bedrag**, en **totale\_bedrag**. Hallo laatste doel lekken omdat ze Hallo tip impliceren worden betaald.
> 
> overbodige kolommen tooexclude en/of doel lekken, mag u Hallo [Select Columns in Dataset] [ select-columns] module of Hallo [metagegevens bewerken] [ edit-metadata]. Zie voor meer informatie [Select Columns in Dataset] [ select-columns] en [metagegevens bewerken] [ edit-metadata] verwijzen naar pagina's.
> 
> 

## <a name="mldeploy"></a>Implementeren van modellen in Azure Machine Learning
Wanneer uw model klaar is, kunt u het eenvoudig implementeren als een webservice rechtstreeks vanuit het Hallo-experiment. Zie voor meer informatie over het implementeren van Azure Machine Learning-webservices [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).

een nieuwe webservice toodeploy, moet u:

1. Een score experiment maken.
2. Hallo-webservice implementeren.

toocreate een score berekenen experimenteren van een **voltooid** training experiment, klikt u op **maken score berekenen EXPERIMENTEREN** in lagere actiebalk Hallo.

![Score berekenen voor Azure][18]

Azure Machine Learning probeert een score experiment op basis van onderdelen van Hallo trainingsexperiment Hallo toocreate. In het bijzonder wordt:

1. Hallo getraind model opslaan en Hallo model trainingsmodules verwijderen.
2. Een logische identificeren **poort invoer** toorepresent Hallo invoergegevens schema verwacht.
3. Een logische identificeren **uitvoerpoort** toorepresent Hallo verwachte web service-uitvoerschema.

Wanneer Hallo experiment score berekenen is gemaakt, bekijken en indien nodig aanpassen. Een typische aanpassing is tooreplace hello invoergegevensset en/of de query met een exclusief label velden, zoals deze is alleen beschikbaar wanneer het Hallo-service wordt genoemd. Het is ook dat een goede gewoonte tooreduce Hallo grootte van Hallo invoer gegevensset en/of queryparameters tooa enkele records, net voldoende tooindicate Hallo invoer schema. Voor de uitvoerpoort hello, het algemene tooexclude alle invoervelden en bevat alleen Hallo **Scored Labels** en **berekend kansen** in uitvoer met behulp van Hallo Hallo [kolommen in gegevensset selecteren ] [ select-columns] module.

Een voorbeeld van een experiment score berekenen is in Hallo afbeelding hieronder. Als u klaar bent toodeploy, klikt u op Hallo **WEBSERVICE PUBLICEERT** knop in lagere actiebalk Hallo.

![Azure Machine Learning publiceren][11]

toorecap, in deze zelfstudie scenario hebt u een Azure data wetenschap-omgeving hebt gewerkt met een grote openbare gegevensset alle Hallo manier van gegevens overname toomodel trainings- en implementeren van een Azure Machine Learning-webservice gemaakt.

### <a name="license-information"></a>Licentie-informatie
In dit voorbeeld scenario en de bijbehorende scripts en IPython notebook(s) worden gedeeld door Microsoft onder Hallo MIT-licentie. Controleer de Hallo LICENSE.txt bestand in de directory Hallo van Hallo voorbeeldcode op GitHub voor meer informatie.

### <a name="references"></a>Verwijzingen
• [Andrés Monroy NYC Taxi reizen downloadpagina](http://www.andresmh.com/nyctaxitrips/)  
• [FOILing NYC Taxi reis gegevens door Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [NYC Taxi en Limousine Commissie onderzoek en statistieken](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
