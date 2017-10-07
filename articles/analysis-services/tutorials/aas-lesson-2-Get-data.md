---
titel: aaa "Azure Analysis Services-zelfstudie les 2: gegevens ophalen | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe gegevens tooget en importeren in Hallo zelfstudie Azure Analysis Services-project. Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: n.v.t. ms.date: 01-06/2017 ms.author: owend
---

# <a name="lesson-2-get-data"></a>Les 2: Gegevens ophalen

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les kunt u gegevens ophalen gebruiken in SSDT tooconnect toohello AdventureWorksDW2014 voorbeelddatabase, selecteert u gegevens, voorbeeld en filter, en vervolgens importeren in uw modelwerkruimte.  
  
Met behulp van Get Data kunt u gegevens importeren uit een groot aantal gegevensbronnen: Azure SQL Database, Oracle, Sybase, OData-Feed, Teradata, bestanden en meer. U kunt ook query's uitvoeren op gegevens met een formule-expressie van Power Query M.
  
Geschatte tijd toocomplete deze les: **10 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 1: Maak een nieuw model in tabelvorm project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Een verbinding maken  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a>een databaseverbinding toohello AdventureWorksDW2014 toocreate  
  
1.  Klik in Tabular Model Explorer met de rechtermuisknop op **Data Sources** > **Import from Data Source**.  
  
    Gegevens ophalen die u bij het maken van verbinding tooa gegevensbron begeleidt wordt gestart. Als er geen Tabellair Model Explorer in **Solution Explorer**, dubbelklikt u op **Model.bim** tooopen Hallo-model in Hallo designer. 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  Klik in Get Data op **Database** > **SQL Server database** > **Connect**.  
  
3.  In Hallo **SQL Server-Database** dialoogvenster in **Server**, typ de naam Hallo van Hallo-server waarop u Hallo AdventureWorksDW2014 database hebt geïnstalleerd en klik op **Connect**.  

4.  Als u wordt gevraagd referenties tooenter, moet u toospecify Hallo referenties Analysis Services tooconnect toohello gegevensbron gebruikt bij het importeren en verwerken van gegevens. Selecteer **Impersonate Account** in de lijst **Impersonation Mode**, geef referenties op en klik op **Connect**. Het verdient aanbeveling om dat u een account gebruiken waarbij Hallo wachtwoord verloopt niet.

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > Met een Windows-gebruikersaccount en wachtwoord, biedt de veiligste methode Hallo van verbindende tooa-gegevensbron.
  
5.  Selecteer in de Navigator Hallo **AdventureWorksDW2014** database en klik vervolgens op **OK**. Hiermee maakt u Hallo toohello databaseverbinding. 
  
6.  In Navigator Selecteer selectievakje in voor de tabellen na Hallo Hallo: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, en **heeft**.  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
Als u op OK klikt, wordt Query Editor geopend. In de volgende sectie hello selecteert u alleen Hallo gewenste gegevens tooimport.

  
## <a name="filter-hello-table-data"></a>Hallo tabelgegevens filteren  
Tabellen in Hallo AdventureWorksDW2014 voorbeelddatabase hebben gegevens die niet nodig tooinclude in uw model. Indien mogelijk, wilt u toofilter uit onnodige gegevens toosave in het geheugen die wordt gebruikt door Hallo-model. U kunt uitfilteren aantal kolommen uit tabellen Hallo zodat ze zijn niet geïmporteerd in Hallo werkruimtedatabase, of de modeldatabase Hallo nadat deze is geïmplementeerd. 
  
#### <a name="toofilter-hello-table-data-before-importing"></a>toofilter hello tabelgegevens vóór het importeren  
  
1.  Selecteer in de Query-Editor Hallo **DimCustomer** tabel. Hallo DimCustomer tabel op Hallo datasource (de voorbeelddatabase AdventureWorksDWQ2014) weergegeven. 
  
2.  Selecteer de kolommen **SpanishEducation**, **FrenchEducation**, **SpanishOccupation** en **FrenchOccupation** (Ctrl ingedrukt houden en klikken), klik met de rechtermuisknop en klik op **Remove Columns**. 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    Aangezien het Hallo-waarden voor deze kolommen zijn niet relevant tooInternet analyse, is er geen tooimport nodig deze kolommen. Door overbodige kolommen te verwijderen, wordt uw model kleiner en efficiënter.  
  
4.  Hallo tabellen resterende door het verwijderen van de volgende kolommen in elke tabel Hallo filteren:  
    
    **DimDate**
    
      |Kolom|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Kolom|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Kolom|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |Kolom|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Kolom|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |Kolom|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Hallo geselecteerd tabellen en kolommen gegevens importeren  
Nu dat u hebt bekeken en onnodige gegevens uitgefilterd, kunt u Hallo rest Hallo-gegevens die u wilt importeren. Hallo wizard importeert Hallo tabelgegevens samen met de relaties tussen tabellen. Nieuwe tabellen en kolommen worden gemaakt in Hallo model en gegevens die u hebt gefilterd is niet geïmporteerd.  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a>Hallo tooimport tabellen en kolomgegevens geselecteerd  
  
1.  Bekijk de selecties. Als alles er goed uitziet, klikt u op **Import**. Hallo gegevensverwerking dialoogvenster ziet Hallo status van gegevens uit uw gegevensbron in uw werkruimtedatabase wordt geïmporteerd.
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  Klik op **Sluiten**.  

  
## <a name="save-your-model-project"></a>Het modelproject opslaan  
Het is belangrijk toofrequently Sla het modelproject.  
  
#### <a name="toosave-hello-model-project"></a>toosave hello model-project  
  
-   Klik op **File** > **Save All**.  
  
## <a name="whats-next"></a>Volgende stappen
[Les 3: Als gegevenstabel markeren](../tutorials/aas-lesson-3-mark-as-date-table.md).

  
  
