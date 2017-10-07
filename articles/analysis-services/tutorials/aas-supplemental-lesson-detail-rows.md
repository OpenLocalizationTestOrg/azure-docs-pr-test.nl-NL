---
titel: aaa "zelfstudie aanvullende les Azure Analysis Services: detailrijen | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate een Detail rijen expressie in Azure analyseservices-zelfstudie Hallo.
Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---detail-rows"></a>Aanvullende les: Detailrijen

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze aanvullende les u Hallo DAX-Editor toodefine een aangepaste Detail rijen expressie. Een expressie van de rijen Detail is een eigenschap van een meting biedt eindgebruikers meer informatie over de resultaten van een meting Hallo geaggregeerd. 
  
Geschatte tijd toocomplete deze les: **10 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Deze aanvullende les maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. Voordat u Hallo taken uitvoert in deze aanvullende les, u moet voltooid alle vorige uitkomsten of een voltooide Adventure Works Internet verkoop model voorbeeldproject hebben.  
  
## <a name="what-do-we-need-toosolve"></a>Wat doen we toosolve nodig?
We bekijken Hallo details van de meting van onze InternetTotalSales, voordat u een expressie van de rijen Detail toevoegt.

1.  In SSDT, klikt u op Hallo **Model** menu > **analyseren in Excel** tooopen Excel en maak een lege draaitabel.
  
2.  In **PivotTable-Fields**, Hallo toevoegen **InternetTotalSales** te meten uit Hallo heeft tabel**waarden**, **kalenderjaar**van Hallo DimDate tabel te**kolommen**, en **EnglishCountryRegionName** te**rijen**. Onze draaitabel biedt nu ons cumulatieve resultaten van Hallo InternetTotalSales meting door regio's en het jaar. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. In de draaitabel Hallo, dubbelklikt u op een cumulatieve waarde voor een jaar en de regionaam van een. Hier we op gedubbelklikt Hallo-waarde voor Australië en Hallo jaar 2014. Er wordt een nieuw blad geopend met gegevens, maar dit zijn niet echt nuttige gegevens.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
Resultaat van de meting van onze InternetTotalSales we zou toosee hier is een tabel met kolommen en rijen met gegevens die toohello bijdragen worden geaggregeerd. toodo dat we een expressie van de rijen Detail als een eigenschap van Hallo meting kunt toevoegen.

## <a name="add-a-detail-rows-expression"></a>Een detailrijenexpressie maken

#### <a name="toocreate-a-detail-rows-expression"></a>een expressie van de rijen Detail toocreate 
  
1. Klik in SSDT, in Hallo heeft tabel maat raster op Hallo **InternetTotalSales** meting. 

2. In **eigenschappen** > **Detail rijen expressie**, klikt u op Hallo editor knop tooopen Hallo DAX-Editor.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. DAX-Editor, Voer Hallo expressie te volgen:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    Deze expressie geeft de namen van kolommen en meting resultaten uit Hallo heeft tabel en gerelateerde tabellen die worden geretourneerd wanneer een gebruiker dubbelklikt op een samengevoegde resultaat in een draaitabel of -rapport.

4. Terug in Excel Hallo blad gemaakt in stap 3 verwijderen en dubbelklik op een cumulatieve waarde. Deze tijd met een eigenschap Detail rijen expressie is gedefinieerd voor de meting hello, een nieuw blad wordt geopend met veel meer bruikbare gegevens.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. Implementeer het model opnieuw.

  
## <a name="see-also"></a>Zie ook  
[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)  (SELECTCOLUMNS, functie (DAX))  
[Aanvullende les: Dynamische beveiliging](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Aanvullende les: Onregelmatige hiërarchieën](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
