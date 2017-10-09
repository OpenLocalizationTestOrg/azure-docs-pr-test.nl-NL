---
titel: aaa "Azure Analysis Services-zelfstudie les 9: Maak hiërarchieën | Microsoft Docs' Beschrijving: services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-9-create-hierarchies"></a>Les 9: Hiërarchieën maken

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les gaat u hiërarchieën maken. Hiërarchieën zijn groepen van kolommen die op niveaus zijn gerangschikt. Zo kan een hiërarchie Geografie onderliggende niveaus bevatten voor land, provincie en stad. Hiërarchieën kunnen worden weergegeven gescheiden van andere kolommen in een reporting client veld lijst met toepassingen, zodat u ze gemakkelijker voor client gebruikers toonavigate en opnemen in een rapport. toolearn meer, Zie [hiërarchieën](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)
  
toocreate hiërarchieën, gebruik Hallo model designer in *diagramweergave*. De gegevensweergave is niet geschikt voor het maken en beheren van hiërarchieën.  
  
Geschatte tijd toocomplete deze les: **20 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 8: Maak perspectieven](../tutorials/aas-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Hiërarchieën maken  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a>een hiërarchie in Hallo DimProduct tabel toocreate  
  
1.  Hallo model designer (diagramweergave) met de rechtermuisknop op Hallo **DimProduct** tabel > **hiërarchie maken**. Een nieuwe hiërarchie wordt weergegeven onder Hallo van venster Hallo-tabel. Wijzig de naam van de hiërarchie Hallo **categorie**.  
  
2.  Klik en sleep Hallo **ProductCategoryName** kolom toohello nieuwe **categorie** hiërarchie.  
  
3.  In Hallo **categorie** -hiërarchie, klik met de rechtermuisknop Hallo **ProductCategoryName** > **naam**, en typ vervolgens **categorie**.  
  
    > [!NOTE]  
    > Deze kolom in tabel Hallo niet de naam van een kolom in een hiërarchie wijzigen. Een kolom in een hiërarchie is slechts een weergave van de kolom in tabel Hallo Hallo.  
  
4.  Klik en sleep Hallo **ProductSubcategoryName** kolom toohello **categorie** hiërarchie. Wijzig de naam in **Subcategory**. 
  
5.  Klik met de rechtermuisknop Hallo **ModelName** kolom > **toevoegen toohierarchy**, en selecteer vervolgens **categorie**. Wijzig de naam in **Model**.

6.  Voeg **EnglishProductName** toohello hiërarchie. Wijzig de naam in **Product**.  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a>toocreate hiërarchieën in Hallo DimDate tabel  
  
1.  In Hallo **DimDate** tabel, maakt u een hiërarchie genaamd **kalender**.  
  
3.  Hallo kolommen in volgorde toevoegen:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  In Hallo **DimDate** tabel, maakt u een **fiscale** hiërarchie. Hallo kolommen in order volgende omvatten:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Ten slotte in Hallo **DimDate** tabel, maakt u een **ProductionCalendar** hiërarchie. Hallo kolommen in order volgende omvatten:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>Volgende stappen
[Les 10: Partities maken](../tutorials/aas-lesson-10-create-partitions.md). 
  
  
