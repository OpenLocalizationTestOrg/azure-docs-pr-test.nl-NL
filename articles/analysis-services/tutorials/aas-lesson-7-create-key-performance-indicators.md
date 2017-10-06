---
titel: aaa "Azure Analysis Services-zelfstudie les 7: Key Performance Indicators maken | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate Key Performance Indicators in Hallo zelfstudie Azure Analysis Services-project. Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-7-create-key-performance-indicators"></a>Les 7: Key Performance Indicators maken

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les gaat u Key Performance Indicators (KPI's) maken. KPI's zijn gebruikte toogauge prestaties van een waarde die is gedefinieerd door een *Base* meting, op basis van een *doel* waarde ook gedefinieerd door een meting of door een absolute waarde. Op rapportage clienttoepassingen, bieden KPI's zakelijke professionals een snelle en gemakkelijke manier toounderstand een samenvatting van zakelijke slagen of tooidentify trends. toolearn meer, Zie [KPI's](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
Geschatte tijd toocomplete deze les: **15 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 6: maken van metingen](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Key Performance Indicators maken  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a>een KPI InternetCurrentQuarterSalesPerformance toocreate  
  
1.  Klik op Hallo in Hallo model designer **heeft** tabel.  
  
2.  Klik op een lege cel in Hallo meting raster.  
  
3.  Typ in de formulebalk Hallo boven Hallo-tabel Hallo volgende formule: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Deze meting fungeert als Hallo basismeting voor Hallo KPI.  
  
4.  Klik met de rechtermuisknop op **InternetCurrentQuarterSalesPerformance** > **Create KPI**.   
  
5.  Hallo Key Performance Indicator (KPI) in het dialoogvenster in **doel** Selecteer **Absolute waarde**, en typ vervolgens **1.1**.  
  
7.  Typ in Hallo links (laag) schuifregelaar veld **1**, en klik vervolgens in Hallo rechts (hoog) schuifregelaar veld **1.07**.  
  
8.  In **Selecteer pictogramstijl**, selecteert u Hallo ruitvormige (rood), driehoek (geel), (groen) Pictogramtype cirkel.
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Kennisgeving Hallo uitbreidbare **beschrijvingen** label onder Hallo pictogram beschikbaar stijlen. Gebruik beschrijvingen voor Hallo verschillende KPI elementen toomake ze meer persoonsgegevens in clienttoepassingen.  
  
9. Klik op **OK** toocomplete Hallo KPI.  
  
    Let op Hallo pictogram volgende toohello in Hallo meting raster **InternetCurrentQuarterSalesPerformance** meting. Dit pictogram geeft aan dat deze meting fungeert als een basislijn voor een KPI.  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a>een KPI InternetCurrentQuarterMarginPerformance toocreate  
  
1.  In Hallo meting raster voor Hallo **heeft** tabel, klikt u op een lege cel.  
  
2.  Typ in de formulebalk Hallo boven Hallo-tabel Hallo volgende formule:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Klik met de rechtermuisknop op **InternetCurrentQuarterMarginPerformance** > **Create KPI**.  
  
4.  Hallo Key Performance Indicator (KPI) in het dialoogvenster in **doel** Selecteer **Absolute waarde**, en typ vervolgens **1,25**.   
  
5.  Schuif totdat Hallo veld wordt weergegeven in Hallo links (laag) schuifregelaar veld **0,8**, en vervolgens dia Hallo rechts (hoog) schuifregelaar veld totdat Hallo veld bevat **1,03**.  
  
6.  In **Selecteer pictogramstijl**Hallo ruitvormige (rood), driehoek (geel), cirkel (groen) Pictogramtype selecteren en klik vervolgens op **OK**.  
  
## <a name="whats-next"></a>Volgende stappen
[Les 8: Perspectieven maken](../tutorials/aas-lesson-8-create-perspectives.md).
  
  
