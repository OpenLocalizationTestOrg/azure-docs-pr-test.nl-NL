---
titel: aaa "Azure Analysis Services-zelfstudie les 1: Maak een nieuw model in tabelvorm project | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate een nieuwe Azure Analysis Services-zelfstudie project. Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: n.v.t. ms.date: 01-06/2017 ms.author: owend
---
# <a name="lesson-1-create-a-tabular-model-project"></a>Les 1: Een nieuw modelproject maken in tabelvorm

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les gebruikt u SQL Server Data Tools (SSDT) toocreate een nieuw model in tabelvorm-project op Hallo 1400 compatibiliteitsniveau. Zodra het nieuwe project is gemaakt, kunt u gegevens gaan toevoegen en het model gaan ontwerpen. Deze les kunt u ook een korte inleiding toohello model in tabelvorm ontwerpomgeving in SSDT.  
  
Geschatte tijd toocomplete deze les: **10 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp is Hallo eerste les in een model in tabelvorm zelfstudie ontwerpen. toocomplete dit les, moet u toohave in-place aan verschillende vereisten. toolearn meer, Zie [Azure Analysis Services - zelfstudie Adventure Works](../tutorials/aas-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Een nieuw project voor een tabellair model maken  
  
#### <a name="toocreate-a-new-tabular-model-project"></a>een nieuw model in tabelvorm project toocreate  
  
1.  In SSDT op Hallo **bestand** menu, klikt u op **nieuw** > **Project**.  
  
2.  In Hallo **nieuw Project** dialoogvenster Vouw **geïnstalleerde** > **Business Intelligence** > **Analysis Services**, en klik vervolgens op **Tabellair Project van Analysis Services**.  
  
3.  In **naam**, type **AW Internet verkoop**, en geef vervolgens een locatie voor Hallo projectbestanden.  
  
    Standaard **oplossingsnaam** is dezelfde als de naam van het project Hallo Hallo; u kunt echter een andere oplossingsnaam typen.  
  
4.  Klik op **OK**.  
  
5.  In Hallo **model in tabelvorm designer** dialoogvenster, **geïntegreerde werkruimte**.  
  
    Hallo werkruimte als host fungeert voor een tabellaire modeldatabase Hello dezelfde naam als Hallo project tijdens het ontwerpen van het model. Geïntegreerde werkruimte betekent dat SSDT gebruikt een ingebouwde exemplaar elimineren Hallo nodig tooinstall een afzonderlijk exemplaar van Analysis Services-server alleen voor het ontwerpen van het model.
      
6.  Selecteer **SQL Server 2017 / Azure Analysis Services (1400)** bij **Compatibility level**.   
 
    ![aas-lesson1-tmd](../tutorials/media/aas-lesson1-tmd.png)
      
    Als er geen SQL Server 2017 / Azure analyseservices (1400) in Hallo compatibiliteit niveau listbox, gebruikt u niet Hallo meest recente versie van SQL Server Data Tools. meest recente versie tooget hello, Zie [installeren SQL Server Data tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  
      
  
## <a name="understanding-hello-ssdt-tabular-model-authoring-environment"></a>Understanding Hallo SSDT model in tabelvorm ontwerpomgeving  
Nu dat u een nieuw model in tabelvorm-project hebt gemaakt, gaat u nu een moment tooexplore Hallo model in tabelvorm ontwerpomgeving in SSDT.  
  
Nadat uw project is gemaakt, wordt het geopend in SSDT. Op Hallo rechts clientzijde in **Tabellaire Model Explorer**, er een structuurweergave van het Hallo-objecten in uw model. Aangezien u gegevens nog niet hebt geïmporteerd, zijn Hallo mappen leeg. U kunt met de rechtermuisknop op een object map tooperform acties, vergelijkbare toohello menubalk. Tijdens het doorlopen van deze zelfstudie gebruikt u Hallo Tabellaire Model Explorer toonavigate verschillende objecten in uw modelproject.

![aas-lesson1-tme](../tutorials/media/aas-lesson1-tme.png)

Klik op Hallo **Solution Explorer** tabblad. Hier ziet u het bestand **Model.bim**. Als er geen Hallo ontwerpvenster toohello links (Hallo leeg venster met Hallo Model.bim tabblad), in **Solution Explorer**onder **AW Internet verkoop Project**, dubbelklikt u op Hallo  **Model.BIM** bestand. Hallo Model.bim bestand bevat Hallo metagegevens voor uw modelproject. 

![aas-lesson1-se](../tutorials/media/aas-lesson1-se.png)
  
Klik op **Model.bim**. In Hallo **eigenschappen** venster er belangrijkste waarvan is Hallo Hallo-modeleigenschappen **DirectQuery-modus** eigenschap. Deze eigenschap geeft als Hallo model wordt geïmplementeerd In het geheugen-modus (uit) of de DirectQuery-modus (aan). Voor deze zelfstudie gaat u het model ontwerpen en implementeren in de modus In-Memory.

![aas-lesson1-properties](../tutorials/media/aas-lesson1-properties.png)
  
Wanneer u een modelproject maakt, bepaalde modeleigenschappen van het zijn ingesteld automatisch gegevens modelleren instellingen die kunnen worden opgegeven in Hallo volgens toohello **extra** menu > **opties** in het dialoogvenster. Eigenschappen gegevensback-up, behoud van de werkruimte en Werkruimteserver opgeven hoe en waar Hallo werkruimtedatabase (uw model database ontwerpen) back-up is gemaakt, blijven in het geheugen behouden en gebouwd. U kunt deze instellingen later altijd nog wijzigen, maar voorlopig laten we deze eigenschappen even voor wat ze zijn.  

Klik in **Solution Explorer** met de rechtermuisknop op **AW Internet Sales** (project) en klik vervolgens op **Properties**. Hallo **AW Internet verkoop eigenschappenpagina's** dialoogvenster wordt weergegeven. Enkele van deze eigenschappen gaat u later instellen, wanneer u het model implementeert.  
  
Wanneer u SSDT hebt geïnstalleerd, zijn enkele nieuwe menuopdrachten toohello Visual Studio-omgeving toegevoegd. Klik op Hallo **Model** menu. Hier kunt kunt u gegevens importeren, vernieuwen van gegevens in de werkruimte, bladeren uw model in Excel, perspectieven en rollen, en selecteer Hallo model weergeven, maken en berekeningsopties ingesteld. Klik op Hallo **tabel** menu. Hier ziet u opdrachten voor het maken en beheren van relaties, het opgeven van instellingen voor gegevenstabellen, het maken van partities en het bewerken van tabeleigenschappen. Als u klikt op Hallo **kolom** menu toevoegen en verwijderen van kolommen in een tabel, kolommen blokkeert en sorteervolgorde opgeven. SSDT voegt ook enkele knoppen toohello-balk. Meest geschikt is Hallo AutoSom functie toocreate een meting standaard aggregatie voor een geselecteerde kolom. Andere werkbalkknoppen bieden snel toegang toofrequently functies en opdrachten gebruikt.  
  
Verkennen van Hallo dialoogvensters en locaties voor verschillende functies specifieke tooauthoring tabellaire modellen. Als sommige items nog niet actief is, kunt u een goed idee van het model in tabelvorm Hallo ontwerpomgeving opvragen.  
  

## <a name="whats-next"></a>Volgende stappen
[Les 2: Gegevens ophalen](../tutorials/aas-lesson-2-get-data.md).

  
  
  
