---
titel: aaa "Azure Analysis Services-zelfstudie les 6: eenheden maken | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate maatregelen in de zelfstudie hello Azure Analysis Services-project. Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: n.v.t. ms.date: 01-06/2017 ms.author: owend
---
# <a name="lesson-6-create-measures"></a>Les 6: Metingen maken

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les maakt u maatregelen toobe opgenomen in het model. Vergelijkbare toohello berekende kolommen die u hebt gemaakt, is een meting een berekening gemaakt met behulp van een DAX-formule. In tegenstelling tot berekende kolommen worden metingen echter geëvalueerd op basis van een *filter* dat de gebruiker selecteert, Bijvoorbeeld, een bepaalde kolom of een slicer toohello rijlabels veld toegevoegd in een draaitabel. Een waarde op voor elke cel in Hallo filter wordt berekend door de maateenheid Hallo toegepast. Metingen zijn krachtige, flexibele berekeningen die u wilt dat tooinclude in bijna alle modellen in tabelvorm tooperform dynamische berekeningen voor numerieke gegevens. toolearn meer, Zie [metingen](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).
  
toocreate metingen, gebruikt u Hallo *meting raster*. Elke tabel heeft standaard een leeg metingenraster, maar meestal hoeft u niet voor elke tabel metingen te maken. Hallo meting raster onder een tabel in de ontwerpfunctie voor het model in de gegevensweergave hello wordt weergegeven. wordt weergegeven of toohide Hallo meting raster voor een tabel, klikt u op Hallo **tabel** menu en klik vervolgens op **meting raster weergeven**.  
  
Door een lege cel in Hallo meting raster klikken en vervolgens een DAX-formule typen in de formulebalk Hallo kunt u een meting. Wanneer u klikt u op ENTER toocomplete Hallo formule, Hallo meting en vervolgens wordt weergegeven in de cel Hallo. U kunt ook metingen met behulp van een standaard aggregatiefunctie door te klikken op een kolom maken en vervolgens te klikken op de knop AutoSom Hallo (**∑**) op de werkbalk Hallo. Maatregelen die zijn gemaakt met Hallo AutoSom functie weergegeven in Hallo meting rastercel direct onder de kolom hello, maar kunnen worden verplaatst.  
  
In deze les maakt u maatregelen door zowel een DAX-formule invoeren in de formulebalk Hallo en via Hallo AutoSom functie.  
  
Geschatte tijd toocomplete deze les: **30 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 5: maken van berekende kolommen](../tutorials/aas-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Metingen maken  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a>toocreate een meting DaysCurrentQuarterToDate in Hallo DimDate tabel  
  
1.  Klik op Hallo in Hallo model designer **DimDate** tabel.  
  
2.  Klik in Hallo meting raster op Hallo linksboven lege cel.  
  
3.  Typ in de formulebalk hello, Hallo volgende formule:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Kennisgeving Hallo linksboven cel bevat nu een metingnaam **DaysCurrentQuarterToDate**, gevolgd door het Hallo-resultaat **92**.
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    In tegenstelling tot berekende kolommen met meting formules kunt u de metingnaam hello, gevolgd door een dubbelepunt, gevolgd door de formule Hallo-expressie typen.

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a>toocreate een meting DaysInCurrentQuarter in Hallo DimDate tabel  
  
1.  Hello **DimDate** tabel nog actief in Hallo model designer in Hallo meting raster, klikt u op de lege cel Hallo hieronder Hallo meting die u hebt gemaakt.  
  
2.  Typ in de formulebalk hello, Hallo volgende formule:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Bij het maken van een ratio van de vergelijking tussen één onvolledige periode en Hallo vorige periode. Hallo formule moet Hallo-gedeelte van het Hallo-outperiode is verstreken berekenen en vergelijken het toohello dezelfde in Hallo vorige periode verhoudingen. In dit geval, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] geeft Hallo verhouding huidige periode is verstreken in Hallo.  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a>toocreate een meting InternetDistinctCountSalesOrder in Hallo heeft tabel  
  
1.  Klik op Hallo **heeft** tabel.   
  
2.  Klik op Hallo **SalesOrderNumber** kolomkop.  
  
3.  Klik op Hallo werkbalk op Hallo pijl-omlaag volgende toohello AutoSom (**∑**) en selecteer vervolgens **DistinctCount**.  
  
    Hallo AutoSom functie maakt automatisch een eenheid voor de geselecteerde kolom Hallo Hallo DistinctCount standaard aggregatie formule.  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  Klik in Hallo meting raster op nieuwe meting Hallo, en klik vervolgens in Hallo **eigenschappen** venster in **Metingnaam**, Hallo meting te wijzigen**InternetDistinctCountSalesOrder**. 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a>aanvullende maatregelen toocreate in Hallo heeft tabel  
  
1.  Hallo AutoSom functie gebruikt, maken en noem Hallo maatregelen te volgen:  

    |Kolom|Naam van meting|AutoSom (∑)|Formule|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Count|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|Sum|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|Sum|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|Sum|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|Sum|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|Sum|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|Sum|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|Sum|=SUM([Freight])|  
  
2.  Door te klikken op een lege cel in Hallo meting raster en met behulp van de formulebalk hello, maken en na Hallo meet in volgorde:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Maatregelen die zijn gemaakt voor Hallo heeft tabel mag gebruikte tooanalyze kritische financiële gegevens zoals verkopen, kosten en winstmarge voor items die zijn gedefinieerd door Hallo gebruiker geselecteerde filter.  
  
## <a name="whats-next"></a>Volgende stappen
[Les 7: Key Performance Indicators maken](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  

  
