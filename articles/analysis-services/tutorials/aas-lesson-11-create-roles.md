---
titel: aaa "Azure Analysis Services-zelfstudie les 11: rollen maken | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toocreate rollen in Hallo zelfstudie Azure Analysis Services-project. Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-11-create-roles"></a>Les 11: Rollen maken

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les gaat u rollen maken. Functies bieden model object en gegevens databasebeveiliging met tooonly toegang beperken die gebruikers die deel uitmaken van de rol. Elke rol is gekoppeld aan één machtiging: None, Read, Read and Process, Process of Administrator. Rollen kunnen tijdens de ontwerpfase van het model worden gedefinieerd met behulp van Role Manager. Nadat een model is geïmplementeerd, kunt u rollen beheren met behulp van SQL Server Management Studio (SSMS). toolearn meer, Zie [rollen](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).
  
> [!NOTE]  
> Rollen maken is niet nodig toocomplete in deze zelfstudie. Standaard Hallo-account die u momenteel bent aangemeld met beheerdersrechten heeft op Hallo-model. Echter, voor andere gebruikers in uw organisatie toobrowse met behulp van een client rapporteert, moet u ten minste één rol maken met lees machtigingen en die gebruikers toevoegen als leden.  
  
U gaat drie rollen maken:  
  
-   **Verkoopmanager** – deze rol kunt gebruikers in uw organisatie waarvoor u toohave lezen machtiging tooall modelobjecten en gegevens wilt opnemen.  
  
-   **Verkoop analist VS** – deze rol kan gebruikers bevatten in uw organisatie waarvoor u wilt dat alleen toobe kunnen toobrowse gegevens gerelateerd toosales in Hallo Verenigde Staten. Voor deze rol die u gebruikt een DAX-formule toodefine een *rijfilter*, waardoor er minder leden toobrowse alleen gegevens voor Hallo Verenigde Staten.  
  
-   **Beheerder** – deze rol kan gebruikers waarvoor u beheerdersrechten toohave, waardoor onbeperkte toegang en machtigingen tooperform administratieve taken op Hallo modeldatabase wilt opnemen.  
  
Omdat Windows-gebruikers- en groepsaccounts in uw organisatie uniek zijn, kunt u de accounts van uw organisatie bepaalde toomembers kunt toevoegen. Echter, voor deze zelfstudie, u kunt ook Hallo leden leeg laten. Hallo effect van elke rol te testen later in les 12: analyseren in Excel.  
  
Geschatte tijd toocomplete deze les: **15 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 10: partities maken](../tutorials/aas-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Rollen maken  
  
#### <a name="toocreate-a-sales-manager-user-role"></a>een gebruikersrol Sales Manager toocreate  
  
1.  Klik in Tabular Model Explorer met de rechtermuisknop op **Roles** > **Roles**.  
  
2.  Klik in Role Manager op **New**.  
  
3.  Klik op de nieuwe rol hello, en klik vervolgens in Hallo **naam** kolom Hallo rol te wijzigen**Sales Manager**.  
  
4.  In Hallo **machtigingen** kolom, klikt u op Hallo vervolgkeuzelijst en selecteer vervolgens Hallo **lezen** machtiging. 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  Optioneel: Klik op Hallo **leden** tabblad en klik vervolgens op **toevoegen**. In Hallo **gebruikers of groepen selecteren** dialoogvenster Voer Hallo Windows-gebruikers of groepen van uw organisatie die u wilt tooinclude Hallo-rol.  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a>een gebruikersrol verkoop analist VS toocreate  
  
1.  Klik in Role Manager op **New**.    
  
2.  Wijzig de naam van de rol Hallo te**verkoop analist VS**.  
  
3.  Geef deze rol de machtiging **Read**.  
  
4.  Klikt u op Hallo rijfilters tabblad, en vervolgens voor Hallo **DimGeography** tabel alleen in Hallo DAX Filter kolom type Hallo volgende formule:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Tooa Booleaans (waar/onwaar)-waarde moet worden omgezet in een rijfilter formule. Met deze formule geeft u aan dat alleen rijen met Hallo landcode regio-waarde van 'VS' zichtbaar toohello gebruiker zijn.  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  Optioneel: Klik op Hallo **leden** tabblad en klik vervolgens op **toevoegen**. In Hallo **gebruikers of groepen selecteren** dialoogvenster Voer Hallo Windows-gebruikers of groepen van uw organisatie die u wilt tooinclude Hallo-rol.  
  
#### <a name="toocreate-an-administrator-user-role"></a>een gebruikersrol Administrator toocreate  
  
1.  Klik op **Nieuw**.  
  
2.  Wijzig de naam van de rol Hallo te**beheerder**.  
  
3.  Geef deze rol de machtiging **Administrator**.  
  
4.  Optioneel: Klik op Hallo **leden** tabblad en klik vervolgens op **toevoegen**. In Hallo **gebruikers of groepen selecteren** dialoogvenster Voer Hallo Windows-gebruikers of groepen van uw organisatie die u wilt tooinclude Hallo-rol. 
  
  
## <a name="whats-next"></a>Volgende stappen
[Les 12: Analyseren in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).

  
  
