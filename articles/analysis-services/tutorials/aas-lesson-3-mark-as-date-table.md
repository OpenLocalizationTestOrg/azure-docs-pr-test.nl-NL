---
titel: aaa "Azure Analysis Services-zelfstudie les 3: markeren als Datumtabel | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toomark een datum tabel in de zelfstudie hello Azure Analysis Services-project. Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: n.v.t. ms.date: 01-06/2017 ms.author: owend
---
# <a name="lesson-3-mark-as-date-table"></a>Les 3: Als gegevenstabel markeren

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In les 2, Gegevens ophalen, hebt u een dimensietabel met de naam DimDate geïmporteerd. Hoewel deze tabel in uw model DimDate heet, kan er ook naar worden verwezen als een *gegevenstabel*, simpelweg omdat de tabel datum- en tijdgegevens bevat.  
  
Wanneer u tijd-intelligente DAX-functies gebruikt, zoals later als u metingen gaat maken, moet u eigenschappen opgeven die een *gegevenstabel* en een unieke id *Gegevenskolom* in die tabel bevatten.
  
In deze les u Hallo DimDate tabel als Hallo markeren *datumtabel* en Hallo datumkolom (in Hallo datum-tabel) als Hallo *datumkolom* (de unieke id).  

Voordat u Hallo tabel- en datum datumkolom markeert, is het een goed moment toodo enigszins uw model eenvoudiger toounderstand huishoudelijke toomake. U ziet in Hallo DimDate tabel een kolom genaamd **FullDateAlternateKey**. In deze kolom bevat een rij voor elke dag elk opgenomen in de tabel Hallo kalenderjaar. U gebruikt deze kolom veel in formules voor metingen en in rapporten. Maar eigenlijk is FullDateAlternateKey niet echt een goede id voor deze kolom. U de naam wijzigen te**datum**, waardoor het gemakkelijker tooidentify en opnemen in formules. Waar mogelijk, is een goed idee toorename zoals tabellen en kolommen toomake deze objecten gemakkelijker tooidentify in SSDT en rapportage van toepassingen als Power BI en Excel-client. 
  
Geschatte tijd toocomplete deze les: **drie minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 2: gegevens ophalen](../tutorials/aas-lesson-2-get-data.md). 

### <a name="toorename-hello-fulldatealternatekey-column"></a>toorename hello FullDateAlternateKey kolom

1.  Klik op Hallo in Hallo model designer **DimDate** tabel.

2.  Dubbelklik op Hallo-header voor Hallo **FullDateAlternateKey** kolom en wijzig de naam te**datum**.

  
### <a name="tooset-mark-as-date-table"></a>tooset markeren als Datumtabel  
  
1.  Selecteer Hallo **datum** kolom, en klik vervolgens in Hallo **eigenschappen** venster onder **gegevenstype**, zorg ervoor dat **datum** is geselecteerd.  
  
2.  Klik op Hallo **tabel** menu, klikt u vervolgens op **datum**, en klik vervolgens op **markeren als Datumtabel**.  
  
3.  In Hallo **markeren als Datumtabel** dialoogvenster in Hallo **datum** listbox, selecteer Hallo **datum** kolom als unieke id Hallo. Deze kolom is meestal standaard geselecteerd. Klik op **OK**. 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>Volgende stappen
[Les 4: Relaties maken](../tutorials/aas-lesson-4-create-relationships.md).
  
