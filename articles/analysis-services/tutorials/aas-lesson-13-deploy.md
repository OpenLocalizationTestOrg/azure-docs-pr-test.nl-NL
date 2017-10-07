---
titel: aaa "Azure Analysis Services-zelfstudie les 13: implementeren | Microsoft Docs' Beschrijving: hierin wordt beschreven hoe toodeploy Hallo zelfstudie project tooAzure Analysis Services.
Services: analysis services-documentationcenter: '' auteur: minewiskan manager: erikre-editor: '' tags: ''

MS.AssetID: ms.service: ms.devlang analysis services: N.V.T. ms.topic:-slag-artikel ms.tgt_pltfrm: N.V.T. ms.workload: n.v.t. ms.date: 17-07/2017 ms.author: owend
---
# <a name="lesson-13-deploy"></a>Les 13: Implementeren

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In deze les configureert u de eigenschappen van implementatie; een Azure Analysis Services server toodeploy tooand een naam voor het Hallo-model op te geven. Vervolgens implementeert u Hallo model toothat exemplaar. Nadat uw model is geïmplementeerd, kunnen gebruikers verbinding maken tooit met behulp van een reporting clienttoepassing. toolearn meer, Zie [tooAzure Analysis Services implementeren](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Geschatte tijd toocomplete deze les: **5 minuten**  
  
## <a name="prerequisites"></a>Vereisten  
Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd. Voordat u Hallo taken uitvoert in deze les, u moet voltooid Hallo vorige les: [les 12: analyseren in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> U moet hebben [beheerdersmachtigingen](../analysis-services-server-admins.md) op Hallo externe Analysis Services-server in de volgorde toodeploy tooit.  

> [!IMPORTANT]  
> Als u de voorbeelddatabase Hallo AdventureWorksDW2014 geïnstalleerd op een lokale SQL Server en u bij het implementeren van uw model tooan Azure Analysis Services-server een [On-premises gegevensgateway](../analysis-services-gateway.md) is vereist.
  
## <a name="deploy-hello-model"></a>Hallo model implementeren  
  
#### <a name="tooconfigure-deployment-properties"></a>tooconfigure implementatie-eigenschappen  

  
1.  In **Solution Explorer**, klik met de rechtermuisknop Hallo **AW Internet verkoop** project en klik vervolgens op **eigenschappen**.  
  
2.  In Hallo **AW Internet verkoop eigenschappenpagina's** dialoogvenster onder **implementatieserver**, in Hallo **Server** -eigenschap geeft u de volledige server Hallo.  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  In Hallo **Database** eigenschap, type **Adventure Works Internet verkoop**.  
  
4.  In Hallo **modelnaam** eigenschap, type **Adventure Works Internet verkoopmodel**.  
  
5.  Controleer de invoer en klik vervolgens op **OK**.  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a>toodeploy hello Adventure Works Internet verkoop
  
1.  In **Solution Explorer**, klik met de rechtermuisknop Hallo **AW Internet verkoop** project > **bouwen**.  

2.  Klik met de rechtermuisknop Hallo **AW Internet verkoop** project > **implementeren**.

    Bij het implementeren van tooAzure Analysis Services kan worden na vragen aan gebruiker tooenter uw account. Voer in dat geval uw organisatieaccount en het bijbehorende wachtwoord in, zoals nancy@adventureworks.com. Dit account moet zich in beheerders op Hallo-server.
  
    Hallo implementeren dialoogvenster wordt weergegeven en toont de implementatiestatus Hallo Hallo metagegevens en elke tabel die is opgenomen in het Hallo-model.  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. Als de implementatie is voltooid, kunt u op **Close** klikken.  
  
## <a name="conclusion"></a>Conclusie  
Gefeliciteerd. U bent klaar met het ontwerpen en implementeren van uw eerste tabellaire model van Analysis Services. Deze zelfstudie heeft geholpen helpt u bij het voltooien van de meest algemene taken Hallo bij het maken van een model in tabelvorm. Nu dat uw Adventure Works Internet verkoop-model is geïmplementeerd, kunt u SQL Server Management Studio toomanage Hallo model; proces-scripts en een back-upplan maken. Gebruikers kunnen nu ook verbinding maken met behulp van een reporting clienttoepassing, zoals Microsoft Excel of Power BI toohello-model.  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>Volgende stappen
[Verbinden met Power BI Desktop](../analysis-services-connect-pbi.md)   
[Aanvullende les: Dynamische beveiliging](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[Aanvullende les: Detailrijen](../tutorials/aas-supplemental-lesson-detail-rows.md)   
[Aanvullende les: Onregelmatige hiërarchieën](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
