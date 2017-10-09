---
titel: aaa "zelfstudie aanvullende les Azure Analysis Services: onregelmatige hiërarchieën | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toofix hiërarchieën onregelmatige in hello Azure Analysis Services-zelfstudie.
Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Aanvullende les: Onregelmatige hiërarchieën

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze aanvullende les gaat u een probleem oplossen dat vaak optreedt bij het maken van een draaitabel van hiërarchieën die op verschillende niveaus lege waarden (leden) bevatten. Dit is bijvoorbeeld het geval als een hoge manager in een organisatie zowel afdelingsmanagers als niet-managers als direct ondergeschikten heeft. Of bij een geografische hiërarchie die bestaat uit land-provincie-stad, waarbij voor sommige steden geen bovenliggende provincie is ingevoerd. Wanneer een hiërarchie lege leden heeft, het vaak toodifferent daalt of onregelmatige, niveaus.

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

Tabelmodellen op Hallo 1400 compatibiliteitsniveau hebben een extra **leden verbergen** eigenschap voor hiërarchieën. Hallo **standaard** instelling wordt ervan uitgegaan er zijn geen lege leden op elk niveau. Hallo **lege leden verbergen** instelling lege leden van Hallo hiërarchie bij het toevoegen van uitsluit tooa draaitabel of -rapport.  
  
Geschatte tijd toocomplete deze les: **20 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Deze aanvullende les maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. Voordat u Hallo taken uitvoert in deze aanvullende les, u moet voltooid alle vorige uitkomsten of een voltooide Adventure Works Internet verkoop model voorbeeldproject hebben. 

Als u Hallo AW Internet verkoop-project hebt gemaakt als onderdeel van de zelfstudie hello, bevat het model nog geen gegevens of niet-aaneengesloten hiërarchieën. toocomplete deze aanvullende les u hebben toocreate Hallo probleem door een aantal aanvullende tabellen toe te voegen, maakt u relaties, berekende kolommen, een meting en een nieuwe organisatiehiërarchie. Dat gedeelte neemt ongeveer 15 minuten in beslag. Vervolgens krijgt u toosolve in een paar minuten.  

## <a name="add-tables-and-objects"></a>Tabellen en objecten toevoegen
  
### <a name="tooadd-new-tables-tooyour-model"></a>nieuw model voor tabellen tooyour tooadd
  
1.  Vouw in Tabular Model Explorer de optie **Data Sources** uit, klik met de rechtermuisknop op uw verbinding en klik vervolgens op **Import New Tables**.
  
2.  Selecteer in Navigator **DimEmployee** en **FactResellerSales**, en klik vervolgens op **OK**.

3.  Klik in Query-editor op **Import**.

4.  Maak de volgende Hallo [relaties](../tutorials/aas-lesson-4-create-relationships.md):

    | Tabel 1           | Kolom       | Filterrichting   | Tabel 2     | Kolom      | Actief |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Standaard            | DimDate     | Date        | Ja    |
    | FactResellerSales | DueDate      | Standaard            | DimDate     | Date        | Nee     |
    | FactResellerSales | ShipDateKey  | Standaard            | DimDate     | Date        | Nee     |
    | FactResellerSales | ProductKey   | Standaard            | DimProduct  | ProductKey  | Ja    |
    | FactResellerSales | EmployeeKey  | tooBoth tabellen | DimEmployee | EmployeeKey | Ja    |

5. In Hallo **DimEmployee** tabel, maakt u de volgende Hallo [berekende kolommen](../tutorials/aas-lesson-5-create-calculated-columns.md): 

    **Pad** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  In Hallo **DimEmployee** tabel, maakt u een [hiërarchie](../tutorials/aas-lesson-9-create-hierarchies.md) met de naam **organisatie**. Toevoegen van kolommen in volgorde Hallo: **Level1**, **2**, **3**, **4**, **5**.

7.  In Hallo **FactResellerSales** tabel, maakt u de volgende Hallo [meting](../tutorials/aas-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Gebruik [analyseren in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel en automatisch een draaitabel maken.

9.  In **PivotTable-Fields**, Hallo toevoegen **organisatie** hiërarchie van Hallo **DimEmployee** tabel te**rijen**, en Hallo **ResellerTotalSales** meting uit Hallo **FactResellerSales** tabel te**waarden**.

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    Zoals u in Hallo draaitabel ziet, Hallo hiërarchie rijen worden weergegeven die niet-aaneengesloten zijn. Er zijn veel rijen waarin lege leden worden weergegeven.

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a>Hallo toofix onregelmatige hiërarchie door Hallo verbergen leden eigenschap

1.  Ga naar **Tabular Model Explorer** en vouw **Tables** > **DimEmployee** > **Hierarchies** > **Organization** uit.

2.  Selecteer **Hide blank members** bij **Properties** > **Hide Members**. 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  Vernieuwen Hallo draaitabel in Excel. 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Dat ziet er al veel beter uit.

## <a name="see-also"></a>Zie ook   
[Les 9: Hiërarchieën maken](../tutorials/aas-lesson-9-create-hierarchies.md)  
[Aanvullende les: Dynamische beveiliging](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Aanvullende les: Detailrijen](../tutorials/aas-supplemental-lesson-detail-rows.md)  