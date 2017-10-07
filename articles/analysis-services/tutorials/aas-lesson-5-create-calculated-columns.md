---
titel: aaa "Azure Analysis Services-zelfstudie les 5: maken van berekende kolommen | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate berekende kolommen in de zelfstudie hello Azure Analysis Services-project. Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: n.v.t. ms.date: 01-06/2017 ms.author: owend
---
# <a name="lesson-5-create-calculated-columns"></a>Les 5: Berekende kolommen maken

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les maakt u gegevens in het model door berekende kolommen toe te voegen. U kunt berekende kolommen (als aangepaste kolommen) maken wanneer u gegevens ophalen, met behulp van Hallo Query-Editor of later in de ontwerpfunctie model-achtige Hallo u hier doen. toolearn meer, Zie [berekende kolommen](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).
  
U gaat vijf nieuwe berekende kolommen maken in drie verschillende tabellen. Hallo stappen zijn enigszins verschillen voor elke taak waarin er zijn verschillende manieren toocreate kolommen, wijzigen en plaats deze in verschillende locaties in een tabel.  

Dit is trouwens ook de les waarin we voor het eerst DAX (Data Analysis Expressions) gaan gebruiken. DAX is een speciale taal voor het maken van in hoge mate aanpasbare formule-expressies voor tabellaire modellen. In deze zelfstudie gebruikt u DAX toocreate berekende kolommen, metingen en filters die rol. toolearn meer, Zie [DAX in modellen in tabelvorm](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular). 
  
Geschatte tijd toocomplete deze les: **15 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 4: relaties](../tutorials/aas-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Berekende kolommen maken  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a>Een berekende kolom van de MonthCalendar in Hallo DimDate tabel maken  
  
1.  Klik op Hallo **Model** menu > **modelweergave** > **gegevensweergave**.  
  
    Berekende kolommen kunnen alleen worden gemaakt met behulp van Hallo model designer in de gegevensweergave.  
  
2.  Klik op Hallo in Hallo model designer **DimDate** tabel (tabblad).  
  
3.  Klik met de rechtermuisknop Hallo **CalendarQuarter** kolomkop en klik vervolgens op **kolom invoegen**.  
  
    Een nieuwe kolom die met de naam **berekende kolom 1** ingevoegde toohello links Hallo **kalenderkwartaal** kolom.  
  
4.  Typ in de formulebalk Hallo boven Hallo tabel Hallo volgende DAX-formule: automatisch aanvullen helpt u typt Hallo FQDN-namen van kolommen en tabellen en lijsten Hallo functies die beschikbaar zijn.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Waarden worden vervolgens voor alle Hallo rijen in de berekende kolom Hallo ingevuld. Als u omlaag Hallo tabel schuift, ziet u rijen kunnen verschillende waarden voor deze kolom op basis van gegevens in elke rij Hallo hebben.    
  
5.  Wijzig de naam van deze kolom te**MonthCalendar**. 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
Hallo MonthCalendar berekende kolom bevat een sorteerbare naam voor de maand.  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a>Maken van een berekende kolom DayOfWeek in Hallo DimDate tabel  
  
1.  Hello **DimDate** tabel steeds actief is, klikt u op Hallo **kolom** menu en klik vervolgens op **kolom toevoegen**.  
  
2.  Typ in de formulebalk hello, Hallo volgende formule:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Wanneer u klaar bent met het bouwen van Hallo formule, druk op ENTER. de nieuwe kolom Hallo is toohello helemaal rechts op Hallo tabel toegevoegd.  
  
3.  Wijzig de naam van de kolom hello te**DayOfWeek**.  
  
4.  Klik op de kolomkop Hallo en sleep Hallo kolom tussen Hallo **EnglishDayNameOfWeek** kolom en Hallo **DayNumberOfMonth** kolom.  
  
    > [!TIP]  
    > Kolommen verplaatsen in de tabel, maakt het eenvoudiger toonavigate.  
  
Hallo DayOfWeek berekende kolom bevat een sorteerbare naam voor de dag van week Hallo.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a>Maken van een berekende kolom ProductSubcategoryName in Hallo DimProduct tabel  
  
  
1.  In Hallo **DimProduct** tabel, toohello uiterst rechts in de tabel Hallo schuiven. Kennisgeving Hallo meest rechtse kolom heet **kolom toevoegen** (cursief) op Hallo kolomkop te klikken.  
  
2.  Typ in de formulebalk hello, Hallo volgende formule:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Wijzig de naam van de kolom hello te**ProductSubcategoryName**.  
  
Hallo ProductSubcategoryName berekende kolom is gebruikte toocreate een hiërarchie in de tabel DimProduct hello, waaronder gegevens van de kolom met Hallo EnglishProductSubcategoryName in Hallo DimProductSubcategory tabel. Hiërarchieën kunnen niet meer dan één tabel omvatten. U gaat later hiërarchieën maken in les 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a>Maken van een berekende kolom ProductCategoryName in Hallo DimProduct tabel  
  
1.  Hello **DimProduct** tabel steeds actief is, klikt u op Hallo **kolom** menu en klik vervolgens op **kolom toevoegen**.  
  
2.  Typ in de formulebalk hello, Hallo volgende formule:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Wijzig de naam van de kolom hello te**ProductCategoryName**.  
  
Hallo ProductCategoryName berekende kolom is gebruikte toocreate een hiërarchie in de tabel DimProduct hello, waaronder gegevens van de kolom met Hallo EnglishProductCategoryName in Hallo DimProductCategory tabel. Hiërarchieën kunnen niet meer dan één tabel omvatten.  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a>Maken van een berekende kolom marge in Hallo heeft tabel  
  
1.  Selecteer Hallo in Hallo model designer **heeft** tabel.  
  
2.  Maak een nieuwe berekende kolom tussen Hallo **SalesAmount** kolom en Hallo **TaxAmt** kolom.  
  
3.  Typ in de formulebalk hello, Hallo volgende formule:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Wijzig de naam van de kolom hello te**marge**.  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    Hallo marge berekende kolom is gebruikte tooanalyze winstmarge voor elke verkoop.  
  
## <a name="whats-next"></a>Volgende stappen
[Les 6: Metingen maken](../tutorials/aas-lesson-6-create-measures.md).
  
  
  
