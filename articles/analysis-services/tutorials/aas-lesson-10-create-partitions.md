---
titel: aaa "Azure Analysis Services-zelfstudie les 10: partities maken | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate partities in de zelfstudie hello Azure Analysis Services-project. Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-10-create-partitions"></a>Les 10: Partities maken

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les kunt u partities toodivide Hallo heeft tabel maken in kleinere logische delen die verwerkt (vernieuwd) onafhankelijk van andere partities worden kunnen. Elke tabel die u in uw model opnemen heeft standaard één partitie, waaronder de kolommen en rijen alle Hallo-tabel. Hallo heeft tabel willen we toodivide Hallo gegevens per jaar; één partitie voor elk van de tabel Hallo vijf jaar. Elke partitie kan vervolgens onafhankelijk worden verwerkt. toolearn meer, Zie [partities](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular). 
  
Geschatte tijd toocomplete deze les: **15 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 9: hiërarchieën maken](../tutorials/aas-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Partities maken  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a>toocreate partities in Hallo heeft tabel  
  
1.  Vouw in Tabular Model Explorer het gedeelte **Tables** uit en klik vervolgens met de rechtermuisknop op **FactInternetSales** > **Partitions**.  
  
2.  Klik in partitiebeheer **kopie**, en wijzig vervolgens de naam van de Hallo te**FactInternetSales2010**.
  
    Omdat u wilt dat Hallo partitie tooinclude alleen die rijen binnen een bepaalde periode Hallo jaar 2010, moet u de query-expressie Hallo wijzigen.
  
4.  Klik op **ontwerp** tooopen Query-Editor en klik vervolgens op Hallo **FactInternetSales2010** query.

5.  Preview-versie, klikt u op Hallo pijl-omlaag in Hallo **OrderDate** kolomkop en klik vervolgens op **datum/tijd-Filters** > **tussen**.

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  Hallo rijen filteren in het dialoogvenster in **rijen weergeven waarvoor: OrderDate**, laat **is na of is gelijk aan**, en voer vervolgens in het veld Hallo **1/1/2010**. Hallo laat **en** operator geselecteerd, selecteer vervolgens **voordat**, voert u vervolgens in het veld Hallo **1-1-2011**, en klik vervolgens op **OK**.

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    In Query-editor ziet u, bij TOEGEPASTE STAPPEN, een andere stap met de naam Filtered Rows. Dit filter is het enige volgorde datums tooselect van 2010.

8.  Klik op **Import**.

    In partitiebeheer u ziet nu expressie heeft een extra rijen gefilterd component Hallo-query.

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    Deze instructie geeft dat deze partitie alleen Hallo-gegevens in deze rijen waar Hallo OrderDate zich in Hallo 2010 kalenderjaar zoals opgegeven in de component van Hallo gefilterde rijen bevindt bevatten.  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a>toocreate een partitie voor Hallo 2011 jaar  
  
1.  Klik in Hallo Partitielijst op Hallo **FactInternetSales2010** partitie-u hebt gemaakt en klik vervolgens op **kopie**.  De partitienaam Hallo ook wijzigen**FactInternetSales2011**. 

    U hoeft niet toouse Query-Editor toocreate een nieuwe gefilterde rijen-component. Omdat u een kopie van Hallo query gemaakt voor 2010, toodo hoeft u een kleine wijziging aanbrengt in het Hallo-query voor 2011.
  
2.  In **Query-expressie**, in volgorde voor deze partitie tooinclude alleen die rijen voor Hallo 2011 jaar, vervang Hallo jaar in Hallo rijen gefilterd-component met **2011** en **2012**respectievelijk, zoals:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a>toocreate partities voor 2012, 2013 en 2014.  
  
- Stappen Hallo vorige, voor het maken van partities voor 2012, 2013 en 2014, Hallo jaren in Hallo rijen gefilterd component tooinclude alleen rijen voor dat jaar wijzigen. 
  

## <a name="delete-hello-factinternetsales-partition"></a>Hallo heeft partitie verwijderen
Nu dat u partities voor elk jaar hebt, kunt u Hallo heeft partitie; verwijderen Zo wordt voorkomen dat overlappen bij het proces alle kiezen bij het verwerken van partities.

#### <a name="toodelete-hello-factinternetsales-partition"></a>toodelete hello heeft partitie
-  Klik op Hallo heeft partitie en klikt u vervolgens op **verwijderen**.



## <a name="process-partitions"></a>Partities verwerken  
In partitiebeheer kennisgeving Hallo **laatste verwerkte** kolom voor elke Hallo nieuwe partities die u hebt gemaakt ziet deze partities nooit is verwerkt. Wanneer u partities maakt, moet u een proces partities of proces bewerking toorefresh Hallo tabelgegevens in deze partities uitvoeren.  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a>tooprocess hello heeft partities  
  
1.  Klik op **OK** tooclose partitiebeheer.  
  
2.  Klik op Hallo **heeft** tabel en klik op Hallo **Model** menu > **proces** > **proces partities**.  
  
3.  Hallo proces partities in het dialoogvenster controleren **modus** te is ingesteld,**Process standaard**.  
  
4.  Hallo selectievakje selecteert in Hallo **proces** kolom voor elke Hallo vijf partities u hebt gemaakt en klik vervolgens op **OK**.  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    Als u wordt gevraagd om referenties voor imitatie, voert u Hallo Windows-gebruikersnaam en wachtwoord die u hebt opgegeven in les 2.  
  
    Hallo **gegevensverwerking** in het dialoogvenster wordt weergegeven en toont de Procesdetails van het voor elke partitie. U ziet dat voor elke partitie een ander aantal rijen wordt overgebracht. Elke partitie bevat alleen die rijen voor de opgegeven in de WHERE-component in SQL-instructie Hallo HALLO hallo-jaar. Zodra de verwerking is voltooid, gaat u verder gaan en Hallo gegevensverwerking dialoogvenster te sluiten.  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>Volgende stappen
De volgende les Ga toohello: [les 11: rollen maken](../tutorials/aas-lesson-11-create-roles.md). 
