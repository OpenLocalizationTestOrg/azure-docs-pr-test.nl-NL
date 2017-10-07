---
titel: aaa "Azure Analysis Services-zelfstudie les 4: relaties maken | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate relaties in Hallo zelfstudie Azure Analysis Services-project. Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-4-create-relationships"></a>Les 4: Relaties maken

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les Hallo relaties die automatisch zijn gemaakt bij het importeren van gegevens controleren en toevoegen van nieuwe relaties tussen verschillende tabellen. Een relatie is een verbinding tussen twee tabellen die bepaalt hoe Hallo-gegevens in deze tabellen moeten worden gecorreleerd. Hallo DimProduct tabel en Hallo DimProductSubcategory tabel hebben bijvoorbeeld een relatie op basis van Hallo feit dat elk product tooa subcategorie behoort. toolearn meer, Zie [relaties](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular).
  
Geschatte tijd toocomplete deze les: **10 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 3: markeren als Datumtabel](../tutorials/aas-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Bestaande relaties controleren en nieuwe relaties toevoegen  
Bij het importeren van gegevens met behulp van de gegevens ophalen, u hebt gekregen zeven tabellen Hallo AdventureWorksDW2014 database. In het algemeen zijn bestaande relaties automatisch geïmporteerd samen met de Hallo gegevens wanneer u gegevens uit een relationele gegevensbron importeert. Voordat u echter verdergaat met het ontwerpen van uw model, moet u controleren of deze relaties tussen tabellen correct zijn gemaakt. Voor deze zelfstudie gaat u drie nieuwe relaties toevoegen.  
  
#### <a name="tooreview-existing-relationships"></a>bestaande relaties tooreview  
  
1.  Klik op Hallo **Model** menu > **modelweergave** > **diagramweergave**.  

    Hallo model designer wordt nu weergegeven in een grafische indeling weergeven van alle Hallo-tabellen die u hebt geïmporteerd met lijnen tussen deze twee diagramweergave. Hallo lijnen tussen de tabellen geven Hallo relaties die automatisch zijn gemaakt bij het importeren van Hallo-gegevens.
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    Als veel Hallo tabellen mogelijk met minimap besturingselementen in Hallo rechterbenedenhoek van Hallo model designer bevatten. U kunt ook op en sleep tabellen toodifferent locaties, tabellen dichter samen te brengen of ze in een bepaalde volgorde te plaatsen. Het verplaatsen van tabellen, heeft dit geen invloed op Hallo relaties tussen tabellen Hallo al. tooview alle Hallo kolommen in een bepaalde tabel, klikt u op, sleept u op een tabel rand tooexpand of kleiner maken.  
  
2.  Klik op Hallo ononderbroken lijn tussen Hallo **DimCustomer** tabel en Hallo **DimGeography** tabel. Hallo ononderbroken lijn tussen deze twee tabellen ziet u dat deze relatie actief is, dat wil zeggen, dat het standaard wordt gebruikt bij het berekenen van DAX formules.  
  
    Kennisgeving Hallo **GeographyKey** kolom in Hallo **DimCustomer** tabel en Hallo **GeographyKey** kolom in Hallo **DimGeography** tabel nu voorkomen beide elk binnen een vak. Deze kolommen worden in de relatie hello gebruikt. Hallo eigenschappen van een relatie nu ook weergegeven in Hallo **eigenschappen** venster.  
  
    > [!TIP]  
    > Bovendien toousing model designer in diagramweergave hello, kunt u ook Hallo relaties beheren dialoogvenster vak tooshow Hallo relaties tussen alle tabellen in een tabel. Klik hiervoor in Tabular Model Explorer met de rechtermuisknop op **Relationships** > **Manage Relationships**.
  
3.  Controleer of Hallo na relaties zijn gemaakt wanneer elk van Hallo tabellen zijn geïmporteerd uit de database AdventureWorksDW Hallo:  
  
    |Actief|Tabel|Gerelateerde opzoektabel|  
    |----------|---------|------------------------|  
    |Ja|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Ja|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Ja|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Ja|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Ja|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Als een van de relaties Hallo ontbreken, Controleer of het model bevat Hallo tabellen te volgen: DimCustomer, DimDate DimGeography, DimProduct, DimProductCategory, DimProductSubcategory en heeft. Als tabellen vanuit Hallo dezelfde gegevensbronverbinding, worden geïmporteerd op tijdstippen verschillende, worden de relaties tussen deze tabellen niet worden gemaakt en moeten handmatig worden gemaakt.  

### <a name="take-a-closer-look"></a>Diagramweergave
In de diagramweergave ziet u een pijl, een sterretje en een nummer op Hallo-regels die Hallo relatie tussen de tabellen weergeven.

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

Hallo pijl geeft Hallo Filterrichting. Hallo sterretje ziet u dat deze tabel is veel-zijde van een relatie Hallo cardinaliteit Hallo en hello een ziet u dat deze tabel is Hallo-een-zijde van Hallo relatie. Als u nodig hebt tooedit een relatie. bijvoorbeeld, wijzig de Filterrichting of kardinaliteit Hallo van een relatie, dubbelklikt u op Hallo relatie regel tooopen Hallo relatie bewerken dialoogvenster.

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

Deze functies zijn bedoeld voor geavanceerde gegevens modelleren en zijn externe Hallo bereik van deze zelfstudie. toolearn meer, Zie [bidirectionele cross-filters voor modellen in tabelvorm in Analysis Services](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services).

In sommige gevallen moet u mogelijk aanvullende relaties tussen tabellen in uw model toosupport toocreate bepaalde bedrijfsregels in te schakelen. Voor deze zelfstudie moet u toocreate drie extra relaties tussen Hallo heeft tabel en Hallo DimDate tabel.  
  
#### <a name="tooadd-new-relationships-between-tables"></a>nieuwe relaties tussen tabellen tooadd  
  
1.  In Hallo model designer in Hallo **heeft** tabel, klik op en houdt op Hallo **OrderDate** kolom en sleep Hallo cursor toohello **datum** kolom in Hallo  **DimDate** tabel en loslaten.  

    Een ononderbroken lijn wordt weergegeven waarin u een actieve relatie tussen Hallo hebt gemaakt **OrderDate** kolom in Hallo **Internet verkoop** tabel en Hallo **datum** kolom in Hallo **Datum** tabel. 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > Bij het maken van relaties worden Hallo kardinaliteit en filter richting tussen de primaire tabel Hallo en Hallo gerelateerde opzoektabel wordt automatisch geselecteerd.  
  
2.  In Hallo **heeft** tabel en klik op houdt op Hallo **DueDate** kolom en sleep Hallo cursor toohello **datum** kolom in Hallo **DimDate** tabel en loslaten.  
  
    Een stippellijn weergegeven waarin u een niet-actieve relatie tussen Hallo hebt gemaakt **DueDate** kolom in Hallo **heeft** tabel en Hallo **datum** kolom in Hallo **DimDate** tabel. U kunt meerdere relaties maken tussen tabellen, maar er kan altijd maar één relatie actief zijn. Inactieve relaties worden gemaakt active tooperform speciale aggregaties in aangepaste DAX-expressies.  
  
3.  We gaan ter afsluiting nog één relatie maken. In Hallo **heeft** tabel en klik op houdt op Hallo **verzenddatum** kolom en sleep Hallo cursor toohello **datum** kolom in Hallo **DimDate** tabel en loslaten.  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Volgende stappen
[Les 5: Berekende kolommen maken](../tutorials/aas-lesson-5-create-calculated-columns.md).
  
  
  
