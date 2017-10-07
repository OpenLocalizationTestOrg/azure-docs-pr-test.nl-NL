---
title: "Zelfstudie: een pijplijn maken met de wizard Kopiëren | Microsoft Docs"
description: "In deze zelfstudie maakt maakt u een Azure Data Factory-pijplijn met een Kopieeractiviteit via Hallo Wizard kopiëren die door Data Factory worden ondersteund"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a>Zelfstudie: een pijplijn maken met de kopieeractiviteit middels de Data Factory-wizard Kopiëren
> [!div class="op_single_selector"]
> * [Overzicht en vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [De wizard Kopiëren](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager-sjabloon](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

Deze zelfstudie leert u hoe toouse hello **Wizard kopiëren** toocopy gegevens uit een Azure blob storage tooan Azure SQL database. 

Hello Azure Data Factory **Wizard kopiëren** kunt u tooquickly een gegevens-pijplijn waarmee gegevens worden gekopieerd van een ondersteunde gegevensbron data store tooa ondersteund doelgegevensopslagplaats maken. Daarom raden we aan Hallo wizard te gebruiken als een eerste stap toocreate een voorbeeldpijplijn voor uw scenario van de verplaatsing van gegevens. Zie [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als doel.  

Deze zelfstudie leert u hoe toocreate een Azure data factory, Hallo Start de Wizard kopiëren, gaat u door een reeks stappen tooprovide details over uw gegevens opname/gegevensverplaatsing scenario. Wanneer u klaar bent met stappen in de wizard Hallo Hallo wizard maakt automatisch een pijplijn met een Kopieeractiviteit toocopy-gegevens van een Azure blob storage tooan Azure SQL database. Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over kopieeractiviteiten.

## <a name="prerequisites"></a>Vereisten
Voldoen aan vereisten die worden vermeld in Hallo [overzicht van de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artikel voordat u deze zelfstudie.

## <a name="create-data-factory"></a>Een gegevensfactory maken
In deze stap gebruikt u Hallo toocreate met Azure portal een Azure-gegevensfactory met de naam **ADFTutorialDataFactory**.

1. Meld u bij te[Azure-portal](https://portal.azure.com).
2. Klik op **+ nieuw** van de linkerbovenhoek hello, klikt u op **gegevens en analyse**, en klik op **Data Factory**. 
   
   ![Nieuw -> DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. In Hallo **nieuwe gegevensfactory** blade:
   
   1. Voer **ADFTutorialDataFactory** voor Hallo **naam**.
       Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn. Als u de foutmelding Hallo: `Data factory name “ADFTutorialDataFactory” is not available`, wijzigt Hallo-naam van gegevensfactory hello (bijvoorbeeld yournameADFTutorialDataFactoryYYYYMMDD) en probeert u het opnieuw. Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.  
      
       ![Naam van gegevensfactory niet beschikbaar](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. Selecteer uw Azure-**abonnement**.
   3. Voor de resourcegroep Doe Hallo stappen te volgen: 
      
      - Selecteer **gebruik bestaande** tooselect een bestaande resourcegroep.
      - Selecteer **nieuw** tooenter een naam voor een resourcegroep.
          
        Sommige van Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u de naam van de Hallo: **ADFTutorialResourceGroup** voor Hallo resourcegroep. toolearn over resourcegroepen, Zie [toomanage uw Azure-resources met behulp van de resource groepen](../azure-resource-manager/resource-group-overview.md).
   4. Selecteer een **locatie** voor Hallo data factory.
   5. Selecteer **pincode toodashboard** selectievakje onderaan Hallo Hallo-blade.  
   6. Klik op **Create**.
      
       ![Blade voor een nieuwe gegevensfactory](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. Nadat het maken van Hallo voltooid is, ziet u Hallo **Data Factory** blade zoals weergegeven in Hallo installatiekopie te volgen:
   
   ![Startpagina van de gegevensfactory](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a>De wizard Kopiëren starten
1. Klik op de Data Factory-blade hello, **kopiëren van gegevens [PREVIEW]** toolaunch hello **Wizard kopiëren**. 
   
   > [!NOTE]
   > Als u ziet dat Hallo webbrowser is vastgelopen bij 'Autoriseren...', schakelt **blokkeren van cookies van derden en sitegegevens** instelling in de browserinstellingen hello (of) Houd deze ingeschakeld en maakt een uitzondering voor  **Login.microsoftonline.com** en probeer het opnieuw starten van Hallo-wizard.
2. In Hallo **eigenschappen** pagina:
   
   1. Voer **CopyFromBlobToAzureSql** in als **taaknaam**
   2. Voer de **beschrijving** in (optioneel).
   3. Wijziging Hallo **begindatum tijd** en Hallo **einddatum en-tijd** zodat Hallo-einddatum is ingesteld tootoday en datum toofive dagen eerder worden gestart.  
   4. Klik op **Volgende**.  
      
      ![Hulpprogramma voor kopiëren - pagina Eigenschappen](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. Op Hallo **brongegevensarchief** pagina, klikt u op **Azure Blob Storage** tegel. U gebruikt deze pagina toospecify Hallo-brongegevensarchief voor Hallo kopieertaak. 
   
    ![Hulpprogramma voor kopiëren - pagina van brongegevensarchief](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. Op Hallo **hello Azure Blob storage-account opgeven** pagina:
   
   1. Voer **AzureStorageLinkedService** in als **naam van de gekoppelde service**.
   2. Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **accountselectiemethode**.
   3. Selecteer uw Azure-**abonnement**.  
   4. Selecteer een **Azure storage-account** van Hallo lijst met Azure storage accounts beschikbaar in het abonnement Hallo geselecteerd. U kunt ook tooenter Opslaginstellingen account handmatig door het selecteren van **handmatig invoeren** optie voor Hallo **Accountselectiemethode**, en klik vervolgens op **volgende**. 
      
      ![Hulpprogramma voor kopiëren - hello Azure Blob storage-account opgeven](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. Op **Kies Hallo invoerbestand of de map** pagina:
   
   1. Dubbelklik op **adftutorial** (map).
   2. Selecteer **emp.txt** en klik op **Kiezen**
      
      ![Hulpprogramma voor kopiëren - Hallo invoerbestand of de invoermap kiezen](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. Op Hallo **Kies Hallo invoerbestand of de map** pagina, klikt u op **volgende**. Selecteer niet **Binaire kopie**. 
   
    ![Hulpprogramma voor kopiëren - Hallo invoerbestand of de invoermap kiezen](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. Op Hallo **bestandsindelingsinstellingen** pagina ziet u Hallo scheidingstekens en het Hallo-schema die automatisch worden gedetecteerd door de wizard Hallo door parseren Hallo-bestand. U kunt ook Hallo scheidingstekens handmatig invoeren voor Hallo kopie wizard toostop auto-detecteren of toooverride. Klik op **volgende** nadat u hello scheidingstekens bekijkt en een voorbeeld van gegevens. 
   
    ![Hulpprogramma voor kopiëren - Bestandsindelingsinstellingen](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. Pagina op Hallo bestemming gegevens opslaan, selecteert u **Azure SQL Database**, en klik op **volgende**.
   
    ![Hulpprogramma voor kopiëren - Doelarchief kiezen](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. Op **Geef hello Azure SQL database** pagina:
   
   1. Voer **AzureSqlLinkedService** voor Hallo **verbindingsnaam** veld.
   2. Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **Server-/databaseselectiemethode**.
   3. Selecteer uw Azure-**abonnement**.  
   4. Selecteer de **servernaam** en **database**.
   5. Voer de **gebruikersnaam** en het **wachtwoord** in.
   6. Klik op **Volgende**.  
      
      ![Hulpprogramma voor kopiëren - Azure SQL-database opgeven](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. Op Hallo **tabeltoewijzing** pagina **emp** voor Hallo **bestemming** veld uit de vervolgkeuzelijst hello, klikt u op **pijl-omlaag** (optioneel) toosee hello schema en toopreview Hallo gegevens.
    
     ![Hulpprogramma voor kopiëren - Tabeltoewijzing](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. Op Hallo **schematoewijzing** pagina, klikt u op **volgende**.
    
    ![Hulpprogramma voor kopiëren - Schematoewijzing](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. Op Hallo **prestatie-instellingen** pagina, klikt u op **volgende**. 
    
    ![Hulpprogramma voor kopiëren - Prestatie-instellingen](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. Bekijk de informatie in Hallo **samenvatting** pagina en klik op **voltooien**. Hallo-wizard maakt twee gekoppelde services, twee gegevenssets (invoer en uitvoer) en één pijplijn in de gegevensfactory hello (van waaruit u Hallo Wizard kopiëren hebt gestart). 
    
    ![Hulpprogramma voor kopiëren - Prestatie-instellingen](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a>Monitor starten en toepassing beheren
1. Op Hallo **implementatie** pagina, klikt u op de koppeling Hallo: `Click here toomonitor copy pipeline`.
   
   ![Hulpprogramma voor kopiëren - Implementeren voltooid](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. Hallo monitoring-toepassing wordt gestart op een afzonderlijke tabblad in uw webbrowser.   
   
   ![App voor bewaking](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. toosee hello laatste status van elk uur segmenten, klikt u op **vernieuwen** knop in Hallo **ACTIVITEITSVENSTERS** lijst Hallo onderaan. Ziet u vijf activiteitsvensters gedurende vijf dagen tussen de begin- en eindtijden voor Hallo pijplijn. Hallo-lijst niet automatisch wordt vernieuwd, zodat u mogelijk de moet tooclick, een paar keer voordat u alle Hallo activiteit windows hello status Ready heeft vernieuwen. 
4. Selecteer een venster van de activiteit in Hallo-lijst. Zie Hallo voor meer informatie over het Hallo **activiteit venster Explorer** op Hallo rechts.

    ![Details van activiteitsvenster](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    Merk op dat Hallo datums 11, 12, 13, 14 en 15 in groen, wat betekent dat Hallo dagelijkse uitvoer segmenten voor deze datums zijn al gemaakt. U ook zien kleurcodering op Hallo pijplijn en uitvoergegevensset in de diagramweergave Hallo Hallo. In de vorige stap Hallo, zoals u ziet dat twee segmenten zijn al gemaakt, een segment wordt verwerkt en hello twee andere toobe verwerkt wachten (gebaseerd op Hallo van kleurcodering). 

    Zie het artikel [Pijplijnen bewaken en beheren met behulp van de app voor bewaking](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van deze toepassing.

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief. Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Klik op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel voor meer informatie over de velden/eigenschappen die u in de wizard voor het kopiëren van een gegevensarchief Hallo ziet. 
