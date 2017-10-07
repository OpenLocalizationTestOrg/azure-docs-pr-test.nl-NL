---
titel: aaa "Azure Analysis Services-zelfstudie les 12: analyseren in Excel | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toouse analyseren in Excel in hello Azure Analysis Services-zelfstudie project. Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-12-analyze-in-excel"></a>Les 12: Analyseren in Excel

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les Hallo analyseren in Excel functie tooopen Microsoft Excel gebruiken, automatisch een verbinding toohello model-werkruimte maken en een draaitabel toohello werkblad automatisch worden toegevoegd. Hallo analyseren in Excel-functie tooprovide is bedoeld als een snelle en gemakkelijke manier tootest Hallo effectiviteit van uw model ontwerpen voorafgaande toodeploying uw model. U gaat geen gegevensanalyse uitvoeren in deze les. Hallo-doel van deze les is toofamiliarize, Hallo-model te ontwerpen, met Hallo-hulpprogramma's kunt u tootest uw modelontwerp gebruiken.   
  
deze les Excel moet zijn geïnstalleerd op Hallo toocomplete dezelfde computer als SSDT.
  
Geschatte tijd toocomplete deze les: **vijf minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 11: rollen maken](../tutorials/aas-lesson-11-create-roles.md).  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a>Bladeren met behulp van de standaard- en Internet verkoop perspectieven Hallo  
In deze eerste taken u uw model zoeken met behulp van beide standaardperspectief hello, die alle modelobjecten bevat, en met behulp van Hallo Internet verkoop perspectief u eerder. Hallo Internet verkoop perspectief sluit Hallo klant table-object.  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a>toobrowse met behulp van het standaardperspectief Hallo  
  
1.  Klik op Hallo **Model** menu > **analyseren in Excel**.  
  
2.  In Hallo **analyseren in Excel** in het dialoogvenster, klikt u op **OK**.  
  
    Excel wordt geopend met een nieuwe werkmap. Een gegevensbronverbinding wordt gemaakt met het huidige gebruikersaccount Hallo en Hallo standaardperspectief is gebruikte toodefine bekeken velden. Een draaitabel toohello werkblad automatisch toegevoegd.  
  
3.  In Excel in Hallo **PivotTable-veldlijst**, kennisgeving Hallo **DimDate** en **heeft** meetgroepen worden weergegeven. Hallo **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, en **heeft** tabellen met hun respectieve kolommen worden ook weergegeven.  
  
4.  Excel sluiten zonder op te slaan Hallo werkmap.  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a>toobrowse met behulp van Hallo Internet verkoop perspectief  
  
1.  Klik op Hallo **Model** menu en klik vervolgens op **analyseren in Excel**.  
  
2.  In Hallo **analyseren in Excel** in het dialoogvenster laat **huidige Windows-gebruiker** geselecteerd, klikt u vervolgens in Hallo **perspectief** vervolgkeuzelijst, selecteer **Internet verkoop** , en klik vervolgens op **OK**. 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  In Excel in **PivotTable-Fields**, zoals u ziet, Hallo DimCustomer tabel is uitgesloten van de veldenlijst Hallo.  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  Excel sluiten zonder op te slaan Hallo werkmap.  
  
## <a name="browse-by-using-roles"></a>Bladeren met behulp van rollen  
Rollen zijn een belangrijk onderdeel van elke tabellair model. Zonder ten minste één rol worden toowhich gebruikers als leden toegevoegd, gebruikers geen toegang krijgen tot gegevens te analyseren met het model. Hallo analyseren in Excel-functie biedt een manier voor u tootest Hallo functies die u hebt gedefinieerd.  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a>toobrowse met behulp van Hallo Sales Manager-gebruikersrol  
  
1.  In SSDT, klikt u op Hallo **Model** menu en klik vervolgens op **analyseren in Excel**.  
  
2.  In **Geef Hallo naam of rol toouse tooconnect toohello gebruikersmodel**, selecteer **rol**, en selecteer vervolgens in de vervolgkeuzelijst hello, **Sales Manager**, en klik vervolgens op  **OK**.  
  
    Excel wordt geopend met een nieuwe werkmap. Er wordt automatisch een draaitabel gemaakt. Hallo veldenlijst Pivot-tabel bevat alle Hallo gegevensvelden beschikbaar in het nieuwe model.  
      
3.  Excel sluiten zonder op te slaan Hallo werkmap.  
  
## <a name="whats-next"></a>Volgende stappen
De volgende les Ga toohello: [les 13: implementeren](../tutorials/aas-lesson-13-deploy.md).

  
  
  
