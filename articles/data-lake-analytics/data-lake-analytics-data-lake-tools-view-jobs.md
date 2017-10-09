---
title: aaaUse taak Browser en de weergave van de taak voor Azure Data Lake Analytics-taken | Microsoft Docs
description: 'Meer informatie over hoe toouse taak Browser en de weergave van de taak voor Azure Data Lake Analytics-taken. '
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bdf27b4d-6f58-4093-ab83-4fa3a99b5650
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: jgao
ms.openlocfilehash: c45e618426808349ca380b1bcfaefd4c947ce7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-job-browser-and-job-view-for-azure-data-lake-analytics-jobs"></a>Taak Browser en weergave van de taak voor Azure Data lake Analytics-taken gebruiken
Hallo archieven van Azure Data Lake Analytics-service verzonden taken in een [queryarchief](#query-store). In dit artikel leert u hoe toouse taak Browser en taak weergeven in Azure Data Lake Tools voor Visual Studio toofind Hallo historische informatie taak. 

Standaard archiveert Hallo Data Lake Analytics-service Hallo taken voor 30 dagen. Hallo vervalperiode kan worden geconfigureerd vanuit hello Azure-portal door te configureren aangepast hello, vervaldatumbeleid. U ook geen informatie over de taak kunnen tooaccess Hallo na de verloopdatum. 

## <a name="prerequisites"></a>Vereisten
Zie [Data Lake Tools voor Visual Studio vereisten](data-lake-analytics-data-lake-tools-get-started.md#prerequisites).

## <a name="open-hello-job-browser"></a>Hallo taak Browser openen
Toegang Hallo taak Browser via **Server Explorer > Azure > Data Lake Analytics > taken** in Visual Studio.  Hallo taak Browser kunt u de queryopslag Hallo van een Data Lake Analytics-account openen. Taak Browser wordt Query Store op Hallo links, weergegeven met informatie over basic taak en gedetailleerde informatie over de taak van taak weergeven op Hallo rechts weergeeft.

## <a name="job-view"></a>Taak weergeven
Project-weergave bevat gedetailleerde informatie van een taak Hallo. tooopen een taak, dubbelklikt u op een taak in Hallo taak Browser of openen via Hallo Data Lake-menu door te klikken op taak weergeven. U ziet een dialoogvenster met Hallo taak URL zijn ingevuld.

![Data Lake Tools Browser voor Visual Studio-project](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view.png)

Weergave van de taak bevat:

* Taakoverzicht
  
    Hallo taakweergave vernieuwen toosee Hallo meer recente informatie van de uitvoering van taken.
  
  * Status van de taak (grafiek):
    
      De Status van taak geeft een overzicht van Hallo taak fasen:
    
      ![Status fasen Azure Data Lake Analytics-taak](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-phases.png)
    
    * Voorbereiden: Upload uw script toohello compileren en cloud Hallo script met behulp van Hallo compileren service optimaliseren.
    * In de wachtrij: Taken zijn in de wachtrij wei ze voldoende bronnen wachten of Hallo taken overschrijden Hallo maximumaantal gelijktijdige taken per accountbeperking. Hallo prioriteitsinstelling bepaalt Hallo reeks wachtrijtaken - Hallo Hallo minder, Hallo hogere Hallo prioriteit.
    * Wordt uitgevoerd: Hallo taak daadwerkelijk wordt uitgevoerd in uw Data Lake Analytics-account.
    * Voltooien: Hallo-taak is voltooid (bijvoorbeeld bestand Hallo afronden).
      
      Hallo-taak kan mislukken in elke fase. Bijvoorbeeld, compilatiefouten in Hallo voorbereiden fase, time-outfouten in Hallo in de wachtrij geplaatst fase en uitvoeringsfouten in Hallo uitgevoerd fase, enzovoort.
  * Algemene informatie
    
      Hallo basic Taakgegevens weergegeven in de onderste gedeelte Hallo van Hallo taakoverzicht Configuratiescherm.
    
      ![Status fasen Azure Data Lake Analytics-taak](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-info.png)
    
    * Resultaat van taak: Is geslaagd of mislukt. Hallo taak mislukken in elke fase.
    * Totale duur: Wandstructuur kloktijd (duur) tussen het verzenden van tijd- en eindtijd.
    * Totale tijd Compute: Hallo som van de uitvoeringstijd van elke hoekpunt, u kunt overwegen dat deze zoals Hallo tijd die Hallo-taak wordt uitgevoerd in slechts één hoekpunt. Raadpleeg tooTotal hoekpunten toofind meer informatie over het hoekpunt.
    * Verzenden/beginnen of eindigen tijd: Hallo tijd wanneer Hallo Data Lake Analytics-service taak verzending/begint toorun Hallo ontvangt taak/ends Hallo-taak is of niet.
    * In de wachtrij geplaatst-compilatie/uitvoeren: Kloktijd besteed tijdens Hallo in wachtrij-voorbereiden/actief-fase.
    * -Account: Hallo Data Lake Analytics-account gebruikt voor het Hallo-taak uitvoeren.
    * Auteur: Hallo persoon Hallo-taak verzonden kan bestaan uit een echte persoon account of een systeem-account.
    * Prioriteit: prioriteit Hallo van Hallo-taak. Hallo Hallo minder, Hallo hogere Hallo prioriteit. Dit geldt alleen voor Hallo reeks Hallo taken in Hallo wachtrij. Instellen van een hogere prioriteit heeft geen hebben voorrang op taken die worden uitgevoerd.
    * Parallelle uitvoering: Hallo aangevraagd maximum aantal gelijktijdige Azure Data Lake Analytics-eenheden (ADLAUs), ook wel hoekpunten. Op dit moment is één hoekpunt gelijk tooone VM met twee virtuele core en 6 GB RAM-geheugen, hoewel dit kan worden bijgewerkt in de toekomst Data Lake Analytics-updates.
    * Bytes links: Bytes die toobe verwerkt moeten totdat het Hallo-taak is voltooid.
    * Bytes gelezen of weggeschreven: Bytes die zijn gelezen of weggeschreven sinds het Hallo-taak is gestart.
    * Totaal aantal hoekpunten: Hallo-taak wordt opgedeeld in veel werk delen, elke stuk werk een hoekpunt wordt aangeroepen. Deze waarde wordt beschreven hoe veel werk stukken Hallo taak bestaat uit. U kunt een hoekpunt beschouwen als een eenheid basisproces, ook wel Azure Data Lake Analytics Unit (ADLAU), en hoekpunten kunnen worden uitgevoerd in de parallelle uitvoering. 
    * Voltooid/actief/is mislukt: Hallo aantal hoekpunten voltooid/actief/is mislukt. Hoekpunten kunnen mislukken vanwege tooboth gebruiker code en system-fouten, maar Hallo system pogingen zijn mislukt hoekpunten automatisch een paar keer. Als Hallo hoekpunt nog steeds na het opnieuw proberen mislukt is, mislukt Hallo hele taak.
* Taakgrafiek
  
    Een U-SQL-script vertegenwoordigt Hallo logica van het transformeren van invoergegevens toooutput gegevens. Hallo-script wordt gecompileerd en tooa fysieke uitvoeringsplan op Hallo voorbereiden fase geoptimaliseerd. Taakgrafiek is tooshow Hallo fysieke uitvoeringsplan.  Hallo volgende diagram illustreert Hallo proces:
  
    ![Status fasen Azure Data Lake Analytics-taak](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-logical-to-physical-plan.png)
  
    Een taak wordt opgedeeld in veel werk delen. Elke stuk werk wordt een hoekpunt genoemd. Hallo hoekpunten zijn gegroepeerd als Super hoekpunt (aka stap) en weergegeven als Taakgrafiek. Hallo groen fase opschriften in taakgrafiek Hallo weergeven Hallo fasen.
  
    Elke hoekpunt in een stadium doet Hallo dezelfde soort werken met verschillende onderdelen van Hallo dezelfde gegevens. Bijvoorbeeld, als u een bestand met één TB gegevens hebt en er zijn honderden hoekpunten lezen van het, lezen elk van deze van een chunk gevonden. Deze hoekpunten worden gegroepeerd in Hallo dezelfde fase en dezelfde manier werken op verschillende onderdelen van hetzelfde bestand voor invoer.
  
  * <a name="state-information"></a>Fase-informatie
    
      In een bepaalde fase worden sommige getallen Hallo plakkaat met weergegeven.
    
      ![Azure Data Lake Analytics-taak grafiek fase](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage.png)
    
    * SV1 Uitpakken: Hallo-naam van een fase, met de naam van een getal en Hallo bewerking-methode.
    * 84 hoekpunten: totaal aantal hoekpunten Hallo in deze fase. Hallo afbeelding geeft aan hoeveel stukken werk is onderverdeeld in deze fase.
    * 12.90 s/hoekpunt: Hallo hoekpunt gemiddelde uitvoeringstijd voor deze fase. In deze afbeelding wordt berekend door SUM (elke hoekpunt uitvoeringstijd) / (totaal aantal hoekpunt). Wat betekent dat als u alle Hallo hoekpunten uitgevoerd in de parallelle uitvoering toewijst kan, Hallo hele fase is voltooid in 12,90 s. Het betekent ook dat als alle Hallo werk in deze fase opeenvolgend wordt gedaan, Hallo kosten zou #vertices * gemiddelde tijd.
    * 850,895 geschreven rijen: het totale aantal rijen in deze fase wordt geschreven.
    * R/b: hoeveelheid gegevens lezen/schriftelijke in dit stadium in bytes.
    * Kleuren: Kleuren worden gebruikt in Hallo fase tooindicate verschillende hoekpunt status.
      
      * Groen geeft aan Hallo hoekpunt is geslaagd.
      * Oranje geeft Hallo hoekpunt opnieuw wordt gestart. Hallo opnieuw geprobeerd hoekpunt is mislukt maar automatisch opnieuw wordt uitgevoerd en met succes door Hallo systeem- en algemene Hallo fase is voltooid. Als Hallo hoekpunt opnieuw uitgevoerd, maar nog steeds mislukt, wordt de kleur Hallo rood en Hallo hele taak is mislukt.
      * Rood geeft een mislukte, wat betekent dat een bepaalde hoekpunt had al opnieuw geprobeerd een paar keer door Hallo systeem maar nog steeds mislukt. Dit scenario zorgt ervoor dat Hallo hele taak toofail.
      * Blauw betekent dat een bepaalde hoekpunt wordt uitgevoerd.
      * Wit geeft Hallo hoekpunt wacht op. Hallo hoekpunt mogelijk wachten toobe gepland zodra een ADLAU beschikbaar of het kan worden wacht op invoer omdat de invoergegevens mogelijk niet gereed.
      
      U vindt meer informatie voor fase Hallo door de muiswijzer de muisaanwijzer op één status:
      
      ![Azure Data Lake Analytics grafiek fase taakdetails](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage-details.png)
  * Hoekpunten: Beschrijft Hallo hoekpunten details, bijvoorbeeld hoeveel hoekpunten in totaal, hoeveel hoekpunten zijn voltooid, zijn ze is mislukt of nog steeds actief/wachten, enzovoort.
  * Het lezen van gegevens tussen verschillende/intra schil: bestanden en gegevens worden opgeslagen in meerdere gehele product in gedistribueerd bestandssysteem. Hallo waarde hier wordt beschreven hoeveel gegevens zijn gelezen in Hallo dezelfde schil of schil cross.
  * Totale tijd compute: Hallo som van elke hoekpunt uitvoeringstijd in Hallo fase, u kunt overwegen deze als Hallo duurt als alle in de fase Hallo werkt in slechts één hoekpunt wordt uitgevoerd.
  * Gegevens en rijen geschreven leestijd: geeft aan hoeveel gegevens of rijen zijn gelezen of weggeschreven of toobe moeten lezen.
  * Hoekpunt lezen fouten: hierin wordt beschreven hoe veel hoekpunten mislukt tijdens het lezen van gegevens.
  * Verwijdert dubbele hoekpunt: als een hoekpunt te langzaam wordt uitgevoerd, Hallo system meerdere hoekpunten kan plannen toorun Hallo dezelfde stuk werk. Reductant hoekpunten worden verwijderd nadat een Hallo hoekpunten voltooid. Hoekpunt dubbele verwijdert records Hallo aantal hoekpunten dat genegeerd als dubbele in Hallo fase.
  * Hoekpunt intrekkingen: Hallo hoekpunt is geslaagd, maar ophalen later opnieuw uitgevoerd vanwege toosome redenen. Bijvoorbeeld als downstream hoekpunt tussenliggende invoergegevens verliest, wordt het Hallo upstream hoekpunt toorerun gevraagd.
  * Hoekpunt planning uitvoeringen: Hallo totale tijd die Hallo hoekpunten zijn gepland.
  * Gemiddelde-min/Max hoekpunt gegevens gelezen: Hallo minimum/gemiddelde/maximum voor van elke hoekpunt gegevens lezen.
  * Duur: Hallo kloktijd die een fase in beslag neemt, moet u tooload profiel toosee deze waarde.
  * Taak afspelen
    
      Data Lake Analytics taken wordt uitgevoerd en archieven Hallo hoekpunten met informatie van Hallo-taken, zoals wanneer Hallo hoekpunten zijn gestart, gestopt, is mislukt en hoe ze zijn opnieuw gestart, enzovoort. Alle Hallo informatie wordt automatisch geregistreerd in de queryopslag Hallo en opgeslagen in het profiel van de taak. U kunt downloaden Hallo taakprofiel via 'Load profiel' in de weergave van de taak en u kunt Hallo taak afspelen weergeven na het downloaden van Hallo taakprofiel.
    
      Taak afspelen is een epitome visualisatie van wat is er gebeurd in Hallo-cluster. Kunt u de voortgang van de taak bekijken en visueel vaststellen afwijkingen en knelpunten in zeer korte tijd (minder dan meestal 30s).
  * Taak Heat Map weergeven 
    
      Taak Heat Map kan worden geselecteerd via Hallo weergave dropdown in Job Graph. 
    
      ![Azure Data Lake Analytics-taak grafiek heap kaartweergave](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-display.png)
    
      Hallo heatmap i/o-, tijd en doorvoer van een taak, waarmee u kunt vinden waar Hallo taak meestal Hallo besteedt, of of de taak is een i/o-grens-taak, enzovoort worden weergegeven.
    
      ![Azure Data Lake Analytics-taak grafiek heap kaart voorbeeld](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-example.png)
    
    * Voortgang: Hallo voortgang van de taak, Zie de informatie in [fase-informatie](#stage-information).
    * Gegevens lezen/geschreven: Hallo heatmap van de totale gegevens lezen/geschreven in elke fase.
    * COMPUTE tijd: heatmap Hallo van SUM (elke hoekpunt uitvoeringstijd), kunt u overwegen dit hoe lang duren zou als alle werkitems in Hallo fase met slechts 1 hoekpunt wordt uitgevoerd.
    * Gemiddelde uitvoeringstijd per knooppunt: heatmap Hallo van SUM (elke hoekpunt uitvoeringstijd) / (hoekpunt Number). Wat betekent dat als u alle Hallo hoekpunten uitgevoerd in de parallelle uitvoering toewijst kan, Hallo gehele werkgebied binnen deze tijd wordt uitgevoerd.
    * I/o-doorvoer: heatmap Hallo van i/o-doorvoer van elke fase, kunt u controleren of de taak een i/o-afhankelijke taak via deze is.
* Bewerkingen voor metagegevens
  
    U kunt sommige metagegevensbewerkingen uitvoeren in uw U-SQL-script, zoals een database te maken, verwijderen van een tabel, enzovoort. Deze bewerkingen worden weergegeven in de metagegevens na de compilatie. U mag asserties vinden, entiteiten maken, entiteiten hier neerzetten.
  
    ![Bewerkingen van de metagegevens van Azure Data Lake Analytics-taak weergeven](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-metadata-operations.png)
* Geschiedenis van status
  
    Hallo geschiedenis van status wordt ook weergegeven in Taakoverzicht, maar u kunt hier meer informatie krijgen. U vindt gedetailleerde Hallo informatie zoals wanneer de taak Hallo is voorbereid, in de wachtrij, is gestart, is gestopt. Ook vindt u hoe vaak de taak Hallo is gecompileerd (Hallo CcsAttempts: 1), wanneer daadwerkelijk is Hallo taak verzonden toohello cluster (Hallo Detail: tijdens het verzenden van taak toocluster), enzovoort.
  
    ![Geschiedenis van de Azure Data Lake Analytics-taak weergeven](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-state-history.png)
* Diagnostiek
  
    Hallo hulpprogramma diagnoses automatisch uitvoeren van taak. U ontvangt waarschuwingen wanneer er fouten of prestatieproblemen in uw taken. Houd er rekening mee dat u toodownload tooget volledige profielgegevens hier moet. 
  
    ![Diagnostische gegevens van Azure Data Lake Analytics-taak weergeven](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-diagnostics.png)
  
  * Waarschuwingen: Een waarschuwing weergegeven hier met waarschuwing van compiler. U kunt klikken op 'x sporen' koppeling toohave meer details zodra het Hallo-waarschuwing wordt weergegeven.
  * Hoekpunt uitvoeren te lang: als een hoekpunt wordt uitgevoerd buiten de tijd (spreek 5 uur), problemen hier worden gevonden.
  * Resourcegebruik: als u meer of is niet voldoende parallelle uitvoering toegewezen dan nodig hebt, problemen hier worden gevonden. Ook kunt u Resource gebruik toosee meer details en toofind mogelijke scenario's een betere brontoewijzing (Zie voor meer informatie in deze handleiding).
  * Geheugencontrole: als een hoekpunt gebruikmaakt van meer dan 5 GB geheugen, problemen hier worden gevonden. Uitvoeren van taak kan ophalen beëindigd door een systeem als gebruikmaakt van meer geheugen dan de systeembeperking van het.

## <a name="job-detail"></a>Taakdetails
Taakdetails bevat gedetailleerde informatie van de taak hello, waaronder Script, bronnen en Vertex Execution View Hallo.

![Azure Data Lake Analytics-job details](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-details.png)

* Script
  
    Hallo U-SQL-script van de taak hello wordt opgeslagen in de queryopslag Hallo. U kunt bekijken Hallo oorspronkelijke U-SQL-script en opnieuw te verzenden indien nodig.
* Resources
  
    U vindt Hallo taak compilatie uitvoer opgeslagen in de queryopslag Hallo via bronnen. U kunt bijvoorbeeld 'algebra.xml' die is gebruikt tooshow hello Taakgrafiek Hallo-assembly's die u hebt geregistreerd, enz. hier vinden.
* Hoekpunt uitvoering weergeven
  
    Deze hoekpunten uitvoering worden details weergegeven. Hallo taakprofiel archiveert elke uitvoeringslogboek hoekpunt zoals totale gegevens lezen/geschreven, runtime, status, enzovoort. Via deze weergave kunt u meer informatie over hoe een taak duurde krijgen. Zie voor meer informatie [gebruik Hallo Vertex Execution View in Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).

## <a name="next-steps"></a>Volgende stappen
* toolog diagnostische informatie, Zie [toegang tot logboeken met diagnostische gegevens voor Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)
* Zie voor een complexere query toosee [websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* toouse hoekpunt uitvoering weergave Zie [gebruik Hallo Vertex Execution View in Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)

