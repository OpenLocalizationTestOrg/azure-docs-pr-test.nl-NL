---
titel: aaa "zelfstudie aanvullende les Azure Analysis Services: dynamische beveiliging | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe dynamische security toouse met behulp van de rij-filters in hello Azure Analysis Services-zelfstudie.
Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---dynamic-security"></a>Aanvullende les: Dynamische beveiliging

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze aanvullende les gaat u een extra rol maken om dynamische beveiliging te implementeren. Dynamische beveiliging biedt rijniveau-beveiliging op basis van Hallo naam of aanmelding id van Hallo gebruiker momenteel is aangemeld. 
  
dynamische beveiliging tooimplement, dat u een tabel tooyour model met Hallo gebruikersnamen van gebruikers die u kunnen verbinding maken met toohello model en blader modelobjecten en gegevens toevoegen. Hallo model dat u met behulp van deze zelfstudie is in de context Hallo van Adventure Works; echter, toocomplete dit les, moet u een tabel met gebruikers van uw eigen domein toevoegen. U hoeft niet Hallo wachtwoorden voor Hallo gebruikersnamen die worden toegevoegd. toocreate een EmployeeSecurity tabel, met een klein aantal gebruikers van uw eigen domein u plakfunctie hello, werknemersgegevens van een Excel-werkblad plakken. In een Praktijkscenario is Hallo-tabel met de gebruikersnamen doorgaans een tabel uit een werkelijke database als een gegevensbron; bijvoorbeeld, een echte DimEmployee tabel.  
  
dynamische beveiliging tooimplement, als u twee DAX-functies gebruiken: [USERNAME-functie (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) en [LOOKUPVALUE-functie (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Deze functies, toegepast in een formule voor een rijfilter, worden gedefinieerd in een nieuwe rol. Met behulp van de functie LOOKUPVALUE Hallo Hallo formule Hiermee geeft u een waarde uit Hallo EmployeeSecurity tabel. Hallo formule stuurt vervolgens dat waarde toohello gebruikersnaam functie, die Hiermee geeft u de gebruikersnaam Hallo van Hallo gebruiker aangemeld toothis rol behoort. Hallo-gebruiker kan vervolgens alleen de gegevens die zijn opgegeven door Hallo-rol rijfilters bladeren. In dit scenario kunt u opgeven dat verkoop medewerkers kunnen alleen surfen op Internet verkoopgegevens voor Hallo verkoopterritoria waarin ze lid zijn.  
  
De taken in die uniek toothis Adventure Works model in tabelvorm scenario zijn, maar tooa: Praktijkscenario niet noodzakelijkerwijs van toepassing worden als zodanig geïdentificeerd. Elke taak bevat aanvullende informatie over Hallo doel van taak Hallo.  
  
Geschatte tijd toocomplete deze les: **30 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Deze aanvullende les maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze aanvullende les, moet u alle vorige uitkomsten hebt voltooid.  
  
## <a name="add-hello-dimsalesterritory-table-toohello-aw-internet-sales-tabular-model-project"></a>Hallo DimSalesTerritory tabel toohello AW Internet verkoop Tabellair Model Project toevoegen  
tooimplement dynamische beveiliging voor dit scenario Adventure Works, moet u twee aanvullende tabellen tooyour model toevoegen. de eerste tabel Hallo toevoegen DimSalesTerritory (zoals Sales Territorium) is uit Hallo dezelfde AdventureWorksDW-database. U een rij filter toohello SalesTerritory tabel die wordt gedefinieerd op bepaalde gegevens hello later toepassen Hallo aangemelde gebruiker kunt bladeren.  
  
#### <a name="tooadd-hello-dimsalesterritory-table"></a>tooadd hello DimSalesTerritory tabel  
  
1.  Klik in Tabular Model Explorer > **Data Sources** met de rechtermuisknop op uw verbinding en klik vervolgens op **Import New Tables**.  

    Als Hallo Imitatiereferenties dialoogvenster wordt weergegeven, typt u Hallo imitatiereferenties die u hebt gebruikt in les 2: gegevens toevoegen.
  
2.  Selecteer in de Navigator Hallo **DimSalesTerritory** tabel en klik vervolgens op **OK**.    
  
3.  Klik in de Query-Editor op Hallo **DimSalesTerritory** opvragen en verwijder vervolgens **SalesTerritoryAlternateKey** kolom.  
  
7.  Klik op **Import**.  
  
    Hallo nieuwe tabel toegevoegd toohello modelwerkruimte. Objecten en gegevens van de brontabel DimSalesTerritory Hallo worden vervolgens geïmporteerd in uw AW Internet verkoopmodel in tabelvorm.  
  
9. Nadat het Hallo-tabel is geïmporteerd, klikt u op **sluiten**.  

## <a name="add-a-table-with-user-name-data"></a>Een tabel toevoegen met gegevens van gebruikersnamen  
Hallo DimEmployee tabel in de voorbeelddatabase voor AdventureWorksDW Hallo bevat gebruikers uit Hallo AdventureWorks domein. Deze gebruikersnamen bestaan niet in uw eigen omgeving. U moet daarom een tabel maken in het model met een klein aantal (ten minste drie) werkelijke gebruikers uit uw organisatie. Vervolgens voegt u deze gebruikers als leden toohello nieuwe rol. U hoeft geen Hallo wachtwoorden voor gebruikersnamen Hallo-voorbeeld, maar hoeft u werkelijke Windows-gebruikersnamen van uw eigen domein.  
  
#### <a name="tooadd-an-employeesecurity-table"></a>een tabel EmployeeSecurity tooadd  
  
1.  Open Microsoft Excel en maak een werkblad.  
  
2.  Hallo volgende tabel, inclusief veldnamenrij hello, kopieer en plak deze in Hallo werkblad.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Vervangen door Hallo voornaam en achternaam domein\gebruikersnaam Hallo namen en de aanmeldings-id's van drie gebruikers in uw organisatie. Hallo plaatsen dezelfde gebruiker op de eerste twee rijen Hallo voor werknemer-id-1, met deze gebruiker behoort toomore dan één verkoop gebied. Laat Hallo werknemer-id en SalesTerritoryId velden ongewijzigd.  
  
4.  Hallo werkblad opslaan als **SampleEmployee**.  
  
5.  Selecteer in Hallo werkblad alle Hallo cellen met werknemersgegevens, met inbegrip van Hallo kopteksten, en vervolgens met de rechtermuisknop op Hallo geselecteerd gegevens en klik vervolgens op **kopie**.  
  
6.  In SSDT, klikt u op Hallo **bewerken** menu en klik vervolgens op **plakken**.  
  
    Als plakken lichter gekleurd weergegeven, klikt u op elke kolom in een tabel in Hallo model designer-venster en probeer het opnieuw.  
  
7.  In Hallo **plakken Preview** het dialoogvenster **tabelnaam**, type **EmployeeSecurity**.  
  
8.  In **gegevens toobe geplakt**, Controleer of Hallo gegevens omvatten alle Hallo gebruikersgegevens en -koppen van Hallo SampleEmployee werkblad.  
  
9. Controleer of **Use first row as column headers** is ingeschakeld en klik vervolgens op **OK**.  
  
    Een nieuwe tabel met de naam EmployeeSecurity met werknemersgegevens gekopieerd uit Hallo SampleEmployee werkblad wordt gemaakt.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Relaties maken tussen de tabellen FactInternetSales, DimGeography en DimSalesTerritory  
Hallo heeft, DimGeography en DimSalesTerritory tabel alle bevatten een gemeenschappelijke SalesTerritoryId-kolom. Hallo SalesTerritoryId kolom in Hallo DimSalesTerritory tabel bevat de waarden met een andere Id voor elke verkoop Territorium.  
  
#### <a name="toocreate-relationships-between-hello-factinternetsales-dimgeography-and-hello-dimsalesterritory-table"></a>toocreate relaties tussen Hallo heeft, DimGeography en Hallo DimSalesTerritory tabel  
  
1.  In de weergave Diagram Hallo **DimGeography** tabel, klik op en houdt op Hallo **SalesTerritoryId** kolom en sleep Hallo cursor toohello **SalesTerritoryId** kolom in Hallo **DimSalesTerritory** tabel en loslaten.  
  
2.  In Hallo **heeft** tabel, klik op en houdt op Hallo **SalesTerritoryId** kolom en sleep Hallo cursor toohello **SalesTerritoryId** kolom in Hallo  **DimSalesTerritory** tabel en loslaten.  
  
    Kennisgeving Hallo eigenschap Active voor deze relatie is ONWAAR, wat betekent dat deze is niet actief. Hallo heeft tabel heeft al een andere actieve relatie.  
  
## <a name="hide-hello-employeesecurity-table-from-client-applications"></a>Hallo EmployeeSecurity tabel vanuit clienttoepassingen verbergen  
In deze taak verbergen u Hallo EmployeeSecurity tabel, deze wordt weergegeven in de veldenlijst een clienttoepassing te houden. Als u een tabel verbergt, betekent dit niet automatisch dat de tabel is beveiligd. Gebruikers kunnen nog steeds gegevens uit de tabel EmployeeSecurity opvragen als ze weten hoe dat moet. toosecure Hallo EmployeeSecurity tabelgegevens, voorkomen dat gebruikers kunnen tooquery wordt een van de gegevens, u een filter toepassen in een latere taak.  
  
#### <a name="toohide-hello-employeesecurity-table-from-client-applications"></a>toohide hello EmployeeSecurity tabel vanuit clienttoepassingen  
  
-   Hallo model designer in diagramweergave met de rechtermuisknop op Hallo **werknemer** kop tabel en klik vervolgens op **verborgen voor clienthulpprogramma's**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Een gebruikersrol Sales Employees by Territory maken  
In deze taak gaat u een gebruikersrol maken. Deze rol omvat een rijfilter definiëren welke rijen van Hallo DimSalesTerritory tabel toousers zichtbaar zijn. Hallo filter wordt vervolgens toegepast in Hallo een-op-veel-relatie richting tooall andere gerelateerde tooDimSalesTerritory tabellen. U toepassen een filter dat u Hallo gehele EmployeeSecurity tabel beveiligt wordt door elke gebruiker die lid is van de rol Hallo waarop ook.  
  
> [!NOTE]  
> Hallo verkoop werknemers door Territorium-rol die u in deze les maakt beperkt leden toobrowse (of een query) alleen verkoopgegevens voor Hallo verkoop Territorium toowhich die ze behoren. Als u een gebruiker als een lid toohello verkoop werknemers door Territorium rol die ook bestaat toevoegen als een lid in een rol die is gemaakt [les 11: rollen maken](../tutorials/aas-lesson-11-create-roles.md), krijgt u een combinatie van machtigingen. Wanneer een gebruiker lid is van meerdere rollen, Hallo machtigingen en rijfilters gedefinieerd voor elke rol zijn cumulatief. Dat wil zeggen, Hallo gebruiker mag Hallo groter bepaald door de combinatie Hallo van rollen.  
  
#### <a name="toocreate-a-sales-employees-by-territory-user-role"></a>de werknemers van een verkoop van de gebruikersrol Territorium toocreate  
  
1.  In SSDT, klikt u op Hallo **Model** menu en klik vervolgens op **rollen**.  
  
2.  Klik in **Role Manager** op **New**.  
  
    Een nieuwe rol Hello geen machtiging is toohello lijst toegevoegd.  
  
3.  Klik op de nieuwe rol hello, en klik vervolgens in Hallo **naam** kolom Hallo rol te wijzigen**werknemers verkoop per regio**.  
  
4.  In Hallo **machtigingen** kolom, klikt u op Hallo vervolgkeuzelijst en selecteer vervolgens Hallo **lezen** machtiging.  
  
5.  Klik op Hallo **leden** tabblad en klik vervolgens op **toevoegen**.  
  
6.  In Hallo **gebruiker of groep selecteren** het dialoogvenster **Enter Hallo-object met de naam tooselect**, type Hallo eerste voorbeeld gebruikersnaam tijdens het maken van Hallo EmployeeSecurity tabel hebt gebruikt. Klik op **namen controleren** tooverify Hallo gebruikersnaam geldig is en klik vervolgens op **Ok**.  
  
    Herhaal deze stap, toe te voegen Hallo andere voorbeeld gebruikersnamen die u hebt gebruikt bij het maken van Hallo EmployeeSecurity tabel.  
  
7.  Klik op Hallo **rijfilters** tabblad.  
  
8.  Voor Hallo **EmployeeSecurity** tabel in Hallo **DAX-Filter** column, type Hallo volgende formule:  
  
    ```
      =FALSE()  
    ```
  
    Deze formule geeft aan dat alle kolommen toohello false Boole-voorwaarde omzetten. Er zijn geen kolommen voor Hallo EmployeeSecurity tabel kunnen worden doorzocht door een lid van Hallo verkoop werknemers door Territorium gebruikersrol.  
  
9. Voor Hallo **DimSalesTerritory** tabel, type Hallo volgende formule:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    In deze formule retourneert Hallo LOOKUPVALUE functie alle waarden voor Hallo DimEmployeeSecurity [SalesTerritoryId]-kolom, waarbij hello EmployeeSecurity [LoginId] is Hallo dezelfde als de huidige Windows-gebruikersnaam en EmployeeSecurity [aangemeld Hallo SalesTerritoryId] is dezelfde als Hallo DimSalesTerritory [SalesTerritoryId] Hallo.  
  
    Hallo is reeks-id's omzet Territorium geretourneerd door LOOKUPVALUE en gebruikte toorestrict Hallo rijen in Hallo DimSalesTerritory tabel wordt weergegeven. Alleen rijen waar hello SalesTerritoryID voor Hallo rij in de set Hallo met id's die zijn geretourneerd door de functie LOOKUPVALUE Hallo worden weergegeven.  
  
10. Klik in Role Manager op **OK**.  
  
## <a name="test-hello-sales-employees-by-territory-user-role"></a>Hallo verkoop werknemers van de gebruikersrol Territorium testen  
In deze taak kunt u Hallo analyseren in Excel-functie gebruiken in SSDT tootest Hallo effectiviteit van Hallo verkoop werknemers door Territorium gebruikersrol. U één opgeven van de gebruikersnamen Hallo u toohello EmployeeSecurity tabel hebt toegevoegd en als een lid van Hallo-rol. Deze gebruikersnaam wordt vervolgens gebruikt als effectieve gebruikersnaam Hallo in Hallo verbinding gemaakt tussen Excel en Hallo-model.  
  
#### <a name="tootest-hello-sales-employees-by-territory-user-role"></a>tootest hello verkoop werknemers door Territorium gebruikersrol  
  
1.  In SSDT, klikt u op Hallo **Model** menu en klik vervolgens op **analyseren in Excel**.  
  
2.  In Hallo **analyseren in Excel** het dialoogvenster **Geef Hallo naam of rol toouse tooconnect toohello gebruikersmodel**, selecteer **andere Windows-gebruiker**, en klik vervolgens op **Bladeren**.  
  
3.  In Hallo **gebruiker of groep selecteren** het dialoogvenster **Voer Hallo object naam tooselect**, typ een gebruikersnaam die u hebt toegevoegd in Hallo EmployeeSecurity tabel en klik vervolgens op **namen controleren**.  
  
4.  Klik op **Ok** tooclose hello **gebruiker of groep selecteren** in het dialoogvenster en klik vervolgens op **Ok** tooclose hello **analyseren in Excel** in het dialoogvenster.  
  
    Excel wordt geopend met een nieuwe werkmap. Er wordt automatisch een draaitabel gemaakt. Hallo PivotTable-Fields lijst bevat de meest Hallo gegevensvelden die beschikbaar zijn in het nieuwe model.  
  
    Kennisgeving Hallo EmployeeSecurity tabel is niet zichtbaar in Hallo PivotTable-Fields lijst. U hebt deze tabel namelijk in een eerdere taak verborgen voor weergave in clienthulpprogramma's.  
  
5.  In Hallo **velden** lijst in **∑ Internet verkoop** (metingen), selecteer Hallo **InternetTotalSales** meting. Hallo-meting wordt ingevoerd in Hallo **waarden** velden.  
  
6.  Selecteer Hallo **SalesTerritoryId** kolom uit Hallo **DimSalesTerritory** tabel. Hallo-kolom is ingevoerd in Hallo **rijlabels** velden.  
  
    Kennisgeving Internet verkoopcijfers worden alleen weergegeven voor Hallo één regio toowhich Hallo effectieve gebruikersnaam die u gebruikt hoort. Als u een andere kolom selecteert, worden zoals stad uit Hallo DimGeography tabel zoals rij labelveld, alleen plaatsen in Hallo verkoop Territorium toowhich Hallo effectieve gebruiker behoort weergegeven.  
  
    Deze gebruiker kan bladeren of query uitvoeren op een Internet-verkoopgegevens voor gebieden dan Hallo een waartoe ze behoren. Deze beperking is omdat hello rijfilter zijn gedefinieerd voor Hallo DimSalesTerritory tabel in Hallo verkoop werknemers door Territorium gebruikersrol, gegevens voor alle gegevens beveiligt gerelateerd tooother verkoopterritoria.  
  
## <a name="see-also"></a>Zie ook  
[USERNAME, functie (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE, functie (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA, functie (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  