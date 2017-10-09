---
title: aaaPower BI-Dashboard van de status van de drager en groot gewoonten - Azure | Microsoft Docs
description: Hallo-mogelijkheden van Cortana Intelligence toogain real-time en voorspellende inzicht op vehicle health gebruiken en gewoonten besturen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a>Vehicle telemetrie analytics-oplossing sjabloon Power BI-Dashboard installatie-instructies
Dit **menu** toohello hoofdstukken in deze playbook koppelingen. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Hallo Vehicle telemetrie Analytics-oplossing gepresenteerd hoe auto dealerbedrijven, auto fabrikanten en ondernemingen van Hallo-mogelijkheden van Cortana Intelligence toogain real-time en voorspellende insights op de drager gezondheid en groot gebruikmaken kunnen verbeteringen in Hallo gebied toodrive van klant gewoonten ervaren R & D- en marketingcampagnes. Dit document bevat stapsgewijze instructies over hoe u Hallo Power BI-rapporten en dashboards configureren kunt zodra Hallo-oplossing is geïmplementeerd in uw abonnement. 

## <a name="prerequisites"></a>Vereisten
1. Hallo implementeren [telemetrie Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) oplossing  
2. [Installeren van Microsoft Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331)
3. Een [Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/). Als u geen Azure-abonnement hebt, aan de slag met de gratis Azure-abonnement
4. Microsoft Power BI-account

## <a name="cortana-intelligence-suite-components"></a>Cortana Intelligence Suite-onderdelen
Hallo na Cortana Intelligence-services worden als onderdeel van Hallo Vehicle telemetrie Analytics oplossingssjabloon geïmplementeerd in uw abonnement.

* **Event Hub** voor het opnemen van miljoenen vehicle telemetrische gebeurtenissen in Azure.
* **Stream Analytics** voor realtime-inzichten op vehicle gezondheid en dat de gegevens zich blijft voordoen in langdurige opslag voor uitgebreidere batch analyses.
* **Machine Learning** voor afwijkingsdetectie in realtime en batchverwerking toogain voorspellende insights.
* **HDInsight** gegevens over tootransform op grote schaal is
* **Data Factory** verwerkt orchestration, planning, bronbeheer en controle van de pipeline voor Hallo batch verwerkt.

**Power BI** biedt deze oplossing een uitgebreide dashboard voor realtime-gegevens en visualisaties predictive analytics. 

Hallo-oplossing maakt gebruik van twee verschillende gegevensbronnen: **gesimuleerde vehicle signalen en diagnostische gegevensset** en **vehicle catalogus**.

Er is een vehicle telematica simulator opgenomen als onderdeel van deze oplossing. Deze diagnostische gegevens verzendt en signalen bijbehorende toohello status van Hallo vehicle en groot patroon op een bepaald tijdstip. 

Hallo Vehicle Catalog is een verwijzing gegevensset met VIN toomodel toewijzing

## <a name="power-bi-dashboard-preparation"></a>Voorbereiding van Power BI-Dashboard
### <a name="setup-power-bi-real-time-dashboard"></a>Realtime Power BI-Dashboard instellen

**Hallo realtime dashboardtoepassing starten** nadat Hallo-implementatie is voltooid, moet u Hallo handmatige bewerking instructies volgen

* Realtime dashboardtoepassing RealtimeDashboardApp.zip downloaden en uitpakken van het.
*  Open in de uitgepakte map hello, app configuratiebestand 'RealtimeDashboardApp.exe.config' vervangen appSettings voor verbindingen met de service Eventhub, Blob Storage en ML met Hallo waarden in Hallo handmatige bewerking instructies en sla uw wijzigingen.
* Toepassing RealtimeDashboardApp.exe uitvoeren. Een aanmeldingsvenster wordt pop-, geldige referenties van uw Power BI en klikt u op Hallo **accepteren** knop. Hallo app start vervolgens toorun.

   ![Aanmelden tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Machtigingen voor Power BI-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* Aanmelding tooPowerBI website, en realtime dashboard maken.

Nu u bent klaar tooconfigure Hallo Power BI-dashboard met visualisaties uitgebreide toogain realtime en gewoonten voorspellende insights op de drager gezondheid en groot. Het duurt ongeveer 45 minuten tooan uur toocreate alle hello-rapporten en Hallo dashboard configureren. 

### <a name="configure-power-bi-reports"></a>Power BI-rapporten configureren
over toocomplete 30 tot 45 minuten duren voordat het Hallo realtime rapporten en Hallo-dashboard. Te bladeren[http://powerbi.com](http://powerbi.com) en meld u aan.

![Aanmelden tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

Een nieuwe gegevensset wordt gegenereerd in Power BI. Klik op Hallo **ConnectedCarsRealtime** gegevensset.

![Geselecteerd verbonden realtime gegevensset voor auto 's](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

Opslaan Hallo leeg rapport met **Ctrl + s**.

![Leeg rapport opslaan](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

Geef de naam van rapport *Vehicle telemetrie Analytics realtime - rapporten*.

![Geef de naam van rapport](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a>Realtime-rapporten
Er zijn drie realtime rapporten in deze oplossing:

1. Voertuigen in bewerking
2. Voertuigen onderhoud vereisen
3. Voertuigen Health statistieken

U kunt kiezen tooconfigure alle Hallo drie realtime rapporten of gestopt na elke fase en doorgaan toohello volgende sectie van het Hallo batch rapporten configureren. We raden u alle toocreate Hallo drie rapporten toovisualize Hallo volledige insights van realtime pad Hallo Hallo-oplossing.  

### <a name="1-vehicles-in-operation"></a>1. Voertuigen in bewerking
Dubbelklik op **pagina 1** en te hernoemen 'Voertuigen in bewerking'  
    ![Auto - verbonden voertuigen in bewerking](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)  

Selecteer **vin** veld **velden** en visualisatie kiezen als **'Kaart'**.  

Kaart visualisatie wordt gemaakt, zoals weergegeven in afbeelding.  
    ![Verbonden auto - Selecteer vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

Klik op Hallo leeg gebied tooadd nieuwe visualisatie.  

Selecteer **stad** en **vin** van velden. Visualisatie ook wijzigen**'Kaart'**. Sleep **vin** in waardengebied. Sleep **stad** van velden te**legenda** gebied.   
    ![Auto - kaart visualisatie verbonden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)

Selecteer **indeling** rubriek van **visualisaties**, klikt u op **titel** en wijzig Hallo **tekst** te**'voertuigen in de bewerking op stad'**.  
    ![Auto - verbonden voertuigen in bewerking per plaats](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)   

Laatste visualisatie lijkt zoals weergegeven in afbeelding.    
    ![Verbonden auto - laatste visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

Klik op Hallo leeg gebied tooadd nieuwe visualisatie.  

Selecteer **stad** en **vin**, visualisatie type te wijzigen**kolomdiagram geclusterde**. Zorg ervoor dat **stad** veld **as gebied** en **vin** in **waarde gebied**  

De grafiek sorteren door **'Aantal van vin'**  
    ![Verbonden auto - telling van vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)  

Diagram wijzigen **titel** te**'Voertuigen in bewerking per plaats'**  

Klik op Hallo **indeling** sectie en selecteer vervolgens **gegevens kleuren**, klikt u op Hallo **'Op'** te**Alles weergeven**  
    ![Verbonden auto - weergeven alle gegevens kleuren](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)  

Hallo kleur van afzonderlijke stad wijzigen door op het Kleurenpictogram te klikken.  
    ![Verbonden auto - kleuren wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

Klik op Hallo leeg gebied tooadd nieuwe visualisatie.  

Selecteer **kolomdiagram geclusterde** visualisatie van visualisaties, Sleep **stad** veld **as** gebied **Model** in **Legenda** gebied en **vin** in **waarde** gebied.  
    ![Verbonden auto - gegroepeerd kolomdiagram](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)  
    ![Verbonden auto - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)

Alle visualisaties op deze pagina rangschikken zoals weergegeven in afbeelding.  
    ![Verbonden auto - visualisaties](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

Hallo 'Voertuigen in bewerking' realtime rapport hebt geconfigureerd. U kunt doorgaan toocreate Hallo volgende realtime rapport of hier stoppen en Hallo dashboard configureren. 

### <a name="2-vehicles-requiring-maintenance"></a>2. Voertuigen onderhoud vereisen
Klik op ![toevoegen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd een nieuw rapport te wijzigen**'Voertuigen vereisen onderhoud'**

![Verbonden auto - voertuigen onderhoud vereisen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

Selecteer **vin** veld en visualisatie type te wijzigen**kaart**.  
    ![Verbonden auto - visualisatie Vin-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)  

We hebben een veld met de naam 'MaintenanceLabel' In hello gegevensset. Dit veld kan een waarde van '0' of '1' hebben." Het is ingesteld door hello Azure Machine Learning-model ingericht als onderdeel van de oplossing en geïntegreerd met realtime Hallo-pad. Hallo-waarde '1' geeft dat een medium vereist onderhoud. 

tooadd een **paginaniveau** filter voor het weergeven van voertuigen gegevens, die onderhoud vereisen: 

1. Sleep Hallo **'MaintenanceLabel'** veld in **niveau paginafilters**.  
   ![Verbonden auto - Filters paginaniveau](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)  
2. Klik op **Basic filteren** menu aan de onderkant van het niveau van MaintenanceLabel paginafilter aanwezig.  
   ![Verbonden auto - Basic filteren](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)  
3. Stel de filterwaarde te**'1'**    
   ![Verbonden auto - filterwaarde](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)  

Klik op Hallo leeg gebied tooadd nieuwe visualisatie.  

Selecteer **kolomdiagram geclusterde** van visualisaties  
![Verbonden auto - visualisatie Vind-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)  
![Verbonden auto - gegroepeerd kolomdiagram](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)

Sleep veld **Model** in **as** gebied **Vin** te**waarde** gebied. Sorteer visualisatie door **aantal vin**.  Diagram wijzigen **titel** te**"Voertuigen onderhoud vereisen door model"**  

Sleep **vin** velden in **kleurverzadiging** aanwezig zijn bij **velden** ![velden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) sectie van **visualisatie**tabblad  
![Verbonden auto - kleurverzadiging](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)  

Wijziging **gegevens kleuren** in visualisaties van **indeling** sectie  
Minimale kleur te wijzigen: **F2C812**  
Maximale kleur te wijzigen: **FF6300**  
![Auto - wijzigingen in de kleuren verbonden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)  
![Verbonden auto - nieuwe visualisatie kleuren](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)  

Klik op Hallo leeg gebied tooadd nieuwe visualisatie.  

Selecteer **gegroepeerd kolomdiagram** visualisaties, Sleep **vin** veld in **waarde** gebied slepen **stad** veld in **As** gebied. De grafiek sorteren door **'Aantal van vin'**. Diagram wijzigen **titel** te**'Voertuigen vereisen onderhoud per plaats'**   
![Verbonden auto - voertuigen onderhoud per plaats vereisen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)  

Klik op Hallo leeg gebied tooadd nieuwe visualisatie.  

Selecteer **met meerdere rijen kaart** visualisatie van visualisaties, Sleep **Model** en **vin** in Hallo **velden** gebied.  
![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)    

Alle Hallo visualisatie herschikken, Hallo laatste rapport ziet er als volgt:  
![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

Hallo 'Voertuigen vereisen onderhoud' realtime rapport hebt geconfigureerd. U kunt doorgaan toocreate Hallo volgende realtime rapport of hier stoppen en Hallo dashboard configureren. 

### <a name="3-vehicles-health-statistics"></a>3. Voertuigen Health statistieken
Klik op ![toevoegen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nieuwe rapporteren, te wijzigen**'Voertuigen Health statistieken'**  

Selecteer **meter** visualisatie van visualisaties, sleept u Hallo **snelheid** veld in **waarde, minimumwaarde, maximumwaarde** gebieden.  
![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)  

Hallo standaard aggregatie van wijzigen **snelheid** in **waarde gebied** te**gemiddelde** 

Hallo standaard aggregatie van wijzigen **snelheid** in **Minimum gebied** te**Minimum**

Hallo standaard aggregatie van wijzigen **snelheid** in **Maximum gebied** te**maximale**

![Verbonden auto - meerdere rij-kaart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

Wijzig de naam van Hallo **meter titel** te**'Gemiddelde snelheid'** 

![Verbonden auto - meter](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

Klik op Hallo leeg gebied tooadd nieuwe visualisatie.  

Op dezelfde manier toevoegen een **meter** voor **engine olie gemiddelde**, **gemiddelde brandstof**, en **gemiddelde temperatuur aangeven engine**.  

Hallo standaard aggregatie van velden in elke meter conform bovenstaande stappen in wijzigen **'Gemiddelde snelheid'** meter.

![Verbonden auto - meters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

Klik op Hallo leeg gebied tooadd nieuwe visualisatie.

Selecteer **lijndiagram en gegroepeerd kolomdiagram** van visualisaties, sleept u **stad** veld in **gedeeld as**, sleept u **snelheid**, **velden tirepressure en engineoil** in **kolomwaarden** gebied te wijzigen van hun samenvoegingstype**gemiddelde**. 

Sleep Hallo **engineTemperature** veld in **regelwaarden** gebied Hallo samenvoegingstype ook wijzigen**gemiddelde**. 

![Verbonden auto - visualisaties velden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

Diagram van wijzigen Hallo **titel** te**'Gemiddelde snelheid, band druk, engine olie en temperatuur motor'**.  

![Verbonden auto - visualisaties velden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

Klik op Hallo leeg gebied tooadd nieuwe visualisatie.

Selecteer **Treemap** visualisatie van visualisaties, sleept u Hallo **Model** veld in Hallo **groep** gebied en sleep Hallo veld  **MaintenanceProbability** in Hallo **waarden** gebied.

Diagram van wijzigen Hallo **titel** te**'Vehicle modellen vereisen onderhoud'**.

![Verbonden auto - grafiektitel wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

Klik op Hallo leeg gebied tooadd nieuwe visualisatie.

Selecteer **100% gestapeld staafdiagram** visualisatie, sleep Hallo **stad** veld in Hallo **as** gebied en sleep Hallo **MaintenanceProbability**, **RecallProbability** velden in Hallo **waarde** gebied.

![Verbonden auto - toevoegen nieuwe visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

Klik op **indeling**, selecteer **gegevens kleuren**, en set Hallo **MaintenanceProbability** toohello kleurwaarde **'F2C80F'**.

Wijziging Hallo **titel** Hallo grafiek te**'Waarschijnlijkheid van Vehicle onderhoud & intrekken per plaats'**.

![Verbonden auto - toevoegen nieuwe visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

Klik op Hallo leeg gebied tooadd nieuwe visualisatie.

Selecteer **vlakdiagram** visualisatie van visualisaties Sleep Hallo **Model** veld in Hallo **as** gebied en sleep Hallo **engineOil, tirepressure, snelheid en MaintenanceProbability** velden in Hallo **waarden** gebied. Hun samenvoegingstype ook wijzigen**'Gemiddeld'**. 

![Verbonden auto - aggregatie wijzigingstype](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

Titel van de grafiek Hallo Hallo ook wijzigen**"Gemiddelde engine olie, druk, snelheid en het onderhoud kans genoeg door model"**.

![Verbonden auto - grafiektitel wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

Klik op Hallo leeg gebied tooadd nieuwe visualisatie:

1. Selecteer **grafiek spreidingsdiagrammen** visualisatie van visualisaties.
2. Sleep Hallo **Model** veld in Hallo **Details** en **legenda** gebied.
3. Sleep Hallo **brandstof** veld in Hallo **x-as** gebied Hallo aggregatie ook wijzigen**gemiddelde**.
4. Sleep **engineTemparature** in **y-as gebied**, Hallo aggregatie ook wijzigen**gemiddelde**
5. Sleep Hallo **vin** veld in Hallo **grootte** gebied.

![Verbonden auto - toevoegen nieuwe visualisatie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

Diagram van wijzigen Hallo **titel** te**"Gemiddelden van brandstof, Engine temperatuur door Model"**.

![Verbonden auto - grafiektitel wijzigen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

Hallo laatste rapport eruit zoals hieronder wordt weergegeven.

![Auto-Final rapport verbonden](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a>Pincode visualisaties van Hallo rapporten toohello realtime dashboard
Een lege dashboard door te klikken op Hallo plus pictogram volgende tooDashboards maken. U kunt andere naam 'Vehicle telemetrie Analytics Dashboard'

![Verbonden auto-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

Pincode Hallo visualisatie van Hallo hierboven rapporten toohello dashboard. 

![Verbonden auto-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

Hallo-dashboard ziet er als volgt wanneer alle Hallo drie rapporten worden gemaakt en Hallo overeenkomt visualisaties vastgemaakt toohello dashboard zijn. Als u niet alle Hallo rapporten hebt gemaakt, kan uw dashboard anders zijn. 

![Verbonden auto-Dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

Gefeliciteerd. Hallo realtime dashboard hebt gemaakt. Als u tooexecute CarEventGenerator.exe en RealtimeDashboardApp.exe doorgaat, ziet u live updates op Hallo-dashboard. Het duurt ongeveer 10 too15 minuten toocomplete Hallo stappen te volgen.

## <a name="setup-power-bi-batch-processing-dashboard"></a>Power BI batch-verwerking dashboard instellen
> [!NOTE]
> Het duurt ongeveer twee uur (van Hallo voltooiing van implementatie Hallo) voor Hallo end tooend batch verwerken van de uitvoering van de pipeline-toofinish en een jaar aan gegenereerde gegevens verwerkt. Wacht dus Hallo toofinish voordat u doorgaat met de volgende stappen Hallo verwerken. 
> 
> 

**Hallo Power BI designer-bestand downloaden**

* Een vooraf geconfigureerde Power BI designer-bestand is opgenomen als onderdeel van Hallo implementatie handmatig bewerking instructies
* Zoek naar 2. Het installatieprogramma Power BI batch verwerking dashboard kunt u Hallo Power BI-sjabloon voor batchverwerking dashboard hier aangeroepen downloaden **ConnectedCarsPbiReport.pbix**.
* Lokaal opslaan

**Power BI-rapporten configureren**

* Open Hallo designer bestand '**ConnectedCarsPbiReport.pbix**' met behulp van Power BI Desktop. Als u al hebt, Installeer geen Power BI Desktop van Hallo [Power BI Desktop installeren](http://www.microsoft.com/download/details.aspx?id=45331). 
* Klik op Hallo **query's bewerken**.

![Power BI query bewerken](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* Dubbelklik op Hallo **bron**.

![Set Power BI-bron](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* Server-verbindingsreeks bijwerken met hello Azure SQL-server die als onderdeel van Hallo-implementatie hebt ingericht.  Zoeken in Hallo handmatige bewerking instructies onder 

    4. Azure SQL Database
    
    * Server: somethingsrv.database.windows.net
    * Database: connectedcar
    * Gebruikersnaam: gebruikersnaam
    * Wachtwoord: U kunt het wachtwoord van uw SQL-server beheren vanuit Azure-portal

* Laat **Database** als *connectedcar*.

![Stel de database in Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* Klik op **OK**.
* U ziet **Windows-referentie** tabblad standaard geselecteerd, ook wijzigen**Database referenties** door te klikken op **Database** tabblad rechts.
* Hallo bieden **gebruikersnaam** en **wachtwoord** van uw Azure SQL Database die is opgegeven tijdens de installatie van de implementatie.

![Geef databasereferenties op](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* Klik op **verbinding maken**
* Hallo bovenstaande stappen herhalen voor elk Hallo drie resterende query's aanwezig zijn bij het rechter deelvenster en werk vervolgens details verbinding Hallo van gegevensbron.
* Klik op **sluiten en te laden**. Power BI Desktop-bestand gegevenssets zijn verbonden tooSQL Azure databasetabellen.
* **Sluit** Power BI Desktop-bestand.

![Sluit Power BI desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* Klik op **opslaan** knop toosave Hallo wijzigingen. 

U hebt nu alle Hallo rapporten toohello batch verwerken van het pad in Hallo oplossing overeenkomt geconfigureerd. 

## <a name="upload-toopowerbicom"></a>Te uploaden*powerbi.com*
1. Navigeer toohello Power BI-webportal op http://powerbi.com en meld u aan.
2. Klik op **gegevens ophalen**  
3. Hallo Power BI Desktop-bestand uploaden.  
4. tooupload, klikt u op **gegevens ophalen -> bestanden ophalen -> lokaal bestand**  
5. Navigeer toohello **'**ConnectedCarsPbiReport.pbix**'**  
6. Zodra het Hallo-bestand is geüpload, zult u waarin navigeren back tooyour Power BI-werkruimte.  

Een gegevensset, rapport en een lege dashboard wordt voor u gemaakt.  

Pincode grafieken tooa nieuwe dashboard aangeroepen **Dashboard met analytische telemetrie Vehicle** in **Power BI**. Klik op de lege dashboard Hallo die eerder is gemaakt en navigeer vervolgens toohello **rapporten** sectie Klik Hallo geüpload nieuw rapport.  

![Vehicle telemetrie Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

**Opmerking Hallo rapport heeft zes pagina's:**  
Pagina 1: Vehicle dichtheid  
Pagina 2: Realtime vehicle health  
Pagina 3: Aangestuurd agressief voertuigen   
Pagina 4: Teruggehaald voertuigen  
Pagina 5: Brandstof efficiënt aangedreven voertuigen  
Pagina 6: Contoso-Logo  

![Verbonden auto's Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

**Vanaf 3 pagina**, vastmaken Hallo volgende:  

1. Telling van VIN  
   ![Verbonden auto's Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. Agressief voertuigen aangedreven door model – waterval grafiek  
   ![Vehicle telemetrie - pincode grafieken 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

**Van pagina 5**, vastmaken Hallo volgende: 

1. Telling van vin    
   ![Vehicle telemetrie - grafieken van de pincode 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. Efficiënte voertuigen brandstof door model: gegroepeerd kolomdiagram  
   ![Vehicle telemetrie - pincode grafieken 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

**Van pagina 4**, vastmaken Hallo volgende:  

1. Telling van vin  
   ![Vehicle telemetrie - pincode grafieken 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. Ingetrokken voertuigen per plaats, model: Treemap  
   ![Vehicle telemetrie - pincode grafieken 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

**Pagina 6**, vastmaken Hallo volgende:  

1. Contoso motoren-logo  
   ![Vehicle telemetrie - pincode grafieken 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

**Hallo dashboard ordenen**  

1. Navigeer toohello dashboard
2. Beweeg de muisaanwijzer over elke grafiek en wijzig de naam op basis van het Hallo naming opgegeven in Hallo voltooid dashboard in onderstaande afbeelding. Hallo grafieken rond toolook zoals Hallo dashboard hieronder ook verplaatsen.  
   ![Vehicle telemetrie - Dashboard 2 ordenen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle telemetrie Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. Als u alle Hallo rapporten, zoals vermeld in dit document hebt gemaakt, moet hello laatste voltooide dashboard eruitzien als Hallo volgende afbeelding. 

![Vehicle telemetrie - Dashboard 2 ordenen](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

Gefeliciteerd. U Hallo rapporten hebt gemaakt en Hallo dashboard toogain realtime, voorspellende en gewoonten batch insights op de drager gezondheid en groot.  
