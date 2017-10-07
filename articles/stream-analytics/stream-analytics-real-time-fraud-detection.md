# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a>Aan de slag met Azure Stream Analytics: realtime-fraudedetectie

Deze zelfstudie biedt een end-to-end-afbeelding van het toouse Azure Stream Analytics. Procedures voor: 

* Breng streaming-gebeurtenissen in een exemplaar van Azure Event Hubs. In deze zelfstudie gebruikt u een app die wij verstrekken die een stream van records met metagegevens van de mobiele telefoon simuleert.

* SQL-achtige Stream Analytics query's tootransform gegevens, informatie verzamelen of patronen zoekt schrijven. U ziet hoe toouse een query tooexamine stroom inkomende hello en aanroepen die mogelijk frauduleuze zoekt.

* Verzenden Hallo resultaten tooan uitvoerlocatie (opslag) die u voor extra inzichten kunt analyseren. In dit geval ontvangt u Hallo verdachte aanroep gegevens tooAzure Blob-opslag.

In deze zelfstudie gebruiken we Hallo voorbeeld van realtime-fraudedetectie, op basis van gegevens voor telefoongesprek. Maar Hallo techniek die laten we zien is ook geschikt voor andere soorten fraude te detecteren, zoals creditcard fraude of identiteitsdiefstal. 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a>Scenario: Telecommunicatie en SIM fraudedetectie in realtime

Een bedrijf telecommunicatie heeft een grote hoeveelheid gegevens naar binnenkomende oproepen. Hallo bedrijf wil toodetect frauduleuze aanroepen in realtime zodat ze kunnen klanten informeren of -service voor een bepaald aantal afgesloten. Een type SIM fraude omvat meerdere aanroepen uit Hallo dezelfde identiteit rond Hallo dezelfde tijd maar geografisch verschillende locaties. toodetect dit soort fraude, Hallo behoeften tooexamine binnenkomende phone bedrijfsgegevens en zoek naar specifieke patronen: in dit geval voor oproepen rond Hallo hetzelfde moment in andere landen. Telefoon records die in deze categorie vallen zijn geschreven toostorage voor verdere analyse.

## <a name="prerequisites"></a>Vereisten

In deze zelfstudie hebt u telefonische oproep gegevens met behulp van een client-app die voorbeeld telefoongesprek metagegevens genereert simuleren. Aantal Hallo-records die Hallo app eruit frauduleuze aanroepen produceert. 

Zorg voordat u begint, hebt u de volgende Hallo:

* Een Azure-account.
* Hallo-aanroep van de gebeurtenis generator-app. U kunt dit downloaden Hallo krijgen [TelcoGenerator.zip bestand](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) van Hallo Microsoft Download Center. Pak het pakket naar een map op uw computer. Als u toosee Hallo broncode en Voer Hallo-app in een foutopsporingsprogramma wilt, kunt u krijgen Hallo app broncode van [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

    >[!NOTE]
    >Windows hello gedownloade ZIP-bestand kan tot gevolg. Als u deze kan niet uitpakken, met de rechtermuisknop op het Hallo-bestand en selecteer **eigenschappen**. Als u Hallo ziet 'dit bestand afkomstig zijn van een andere computer en mogelijk worden geblokkeerde toohelp beveiliging van deze computer'-bericht, selecteer Hallo **blokkering** optie en klik vervolgens op **toepassen**.

Als u tooexamine Hallo resultaten van Hallo Streaming Analytics-taak wilt, moet u ook een hulpprogramma voor het weergeven van Hallo inhoud van een Azure Blob Storage-container. Als u Visual Studio gebruikt, kunt u [Azure-Tools voor Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) of [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer). U kunt ook zelfstandige hulpprogramma's zoals installeren [Azure Opslagverkenner](http://storageexplorer.com/) of [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction). 

## <a name="create-an-azure-event-hubs-tooingest-events"></a>Een Azure event hubs tooingest gebeurtenissen maken

een gegevensstroom tooanalyze u *opnemen* in Azure. Een gangbare manier tooingest-gegevens is toouse [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md), waarmee u miljoenen gebeurtenissen per seconde opnemen, en vervolgens verwerken en opslaan van informatie over de statuswijzigingsgebeurtenis Hallo. Voor deze zelfstudie die u kunt een event hub maakt en vervolgens hebt Hallo aanroep gebeurtenis generator app verzenden aanroep gegevens toothat event hub. Zie voor meer informatie over event hubs Hallo [Azure Service Bus-documentatie](https://docs.microsoft.com/en-us/azure/service-bus/).

>[!NOTE]
>Zie voor een meer gedetailleerde versie van deze procedure [maken van een naamruimte Event Hubs en Azure-portal een event hub met Hallo](../event-hubs/event-hubs-create.md). 

### <a name="create-a-namespace-and-event-hub"></a>Een naamruimte en event hub maken
In deze procedure maakt u eerst een event hub-naamruimte maken en vervolgens voegt u een event hub toothat namepsace toe. Event hub-naamruimten worden gebruikt toologically groep gerelateerde gebeurtenis bus exemplaren. 

1. Meld u aan bij hello Azure-portal en klikt u op **nieuw** > **Internet der dingen** > **Event Hub**. 

2. In Hallo **naamruimte maken** blade, voer de naam van een naamruimte zoals `<yourname>-eh-ns-demo`. Kunt u een naam voor de naamruimte hello, maar Hallo-naam moet geldig zijn voor een URL en deze uniek zijn binnen Azure. 
    
3. Selecteer een abonnement maken of een resourcegroep kiezen, en klikt u op **maken**. 

    ![Een event hub-naamruimte maken](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. Wanneer het Hallo-naamruimte is voltooid implementeren, vinden Hallo event hub naamruimte in uw lijst met Azure-resources. 

5. Klik op de nieuwe naamruimte Hallo en op Hallo naamruimte Blade  **+ &nbsp;Event Hub**. 

    ![Hallo toevoegen Event Hub knop voor het maken van nieuwe event hub ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. Naam Hallo nieuwe event hub `sa-eh-frauddetection-demo`. U kunt een andere naam gebruiken. Als u dit doet, noteer, omdat u de naam van de hello later nodig. U hoeft niet tooset andere opties voor Hallo event hub nu.

    ![Blade voor het maken van nieuwe event hub](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. Klik op **Create**.
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a>Verleen toegang toohello event hub en een verbindingsreeks ophalen

Voordat een proces gegevens tooan event hub verzendt kan, moet Hallo event hub een beleid waarmee u de juiste toegang hebben. Hallo toegangsbeleid produceert een verbindingsreeks die autorisatie-informatie bevat.

1.  Klik op Hallo gebeurtenis naamruimte blade **Event Hubs** en klik vervolgens op Hallo-naam van uw nieuwe event hub.

2.  Klik op Hallo event hubblade **gedeeld toegangsbeleid** en klik vervolgens op  **+ &nbsp;toevoegen**.

    >[!NOTE]
    >Zorg ervoor dat u werkt met Hallo event hub niet Hallo event hub naamruimte.

3.  Een beleid met de naam toevoegen `sa-policy-manage-demo` en voor **Claim**, selecteer **beheren**.

    ![Blade voor een nieuwe event hub-beleid maken](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  Klik op **Create**.

5.  Nadat Hallo beleid is geïmplementeerd, klikt u op het Hallo-lijst met beleidsregels voor gedeelde toegang.

6.  Hallo-zoekvak met het label **CONNECTION STRING-primaire sleutel** en klik op Hallo kopie knop volgende toohello-verbindingsreeks. 
    
    ![Kopiëren van primaire verbindingssleutel tekenreeks Hallo van Hallo-beleid](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  Hallo-verbindingsreeks in een teksteditor plakken. U moet deze verbindingsreeks voor de volgende sectie hello, nadat u een aantal kleine wijzigingen tooit.

    Hallo-verbindingsreeks ziet er als volgt:

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    U ziet dat Hallo-verbindingsreeks meerdere sleutel / waarde-paren bevat, gescheiden door puntkomma's: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, en `EntityPath`.  

## <a name="configure-and-start-hello-event-generator-application"></a>Configureren en Hallo gebeurtenis generator toepassing starten

Voordat u Hallo TelcoGenerator app, configureren u deze zo dat wordt verzonden aanroep records toohello event hub die u zojuist hebt gemaakt.

### <a name="configure-hello-telcogeneratorapp"></a>Hallo TelcoGeneratorapp configureren

1.  In de editor Hallo waar u de verbindingsreeks Hallo gekopieerd Noteer Hallo `EntityPath` waarde, en verwijder vervolgens Hallo `EntityPath` paar (Vergeet niet tooremove Hallo puntkomma voorafgaande). 

2.  Hallo map waar u Hallo TelcoGenerator.zip bestand hebt uitgepakt, Hallo telcodatagen.exe.config bestand in een teksteditor te openen. (Er is meer dan een .config-bestand, dus zorg ervoor dat u Hallo rechts een opent)

3.  In Hallo `<appSettings>` element dit doen:

    * Hallo-waarde van Hallo `EventHubName` naam key toohello event hub (dat wil zeggen toohello waarde van Hallo entiteit pad).
    * Hallo-waarde van Hallo `Microsoft.ServiceBus.ConnectionString` toohello verbindingsreeks sleutel. 

    Hallo `<appSettings>` sectie eruit Hallo voorbeeld te volgen. (Voor de duidelijkheid we Hallo regels met tekstterugloop en bepaalde tekens uit verwijderd Hallo-verificatietoken.)

    ![App-configuratiebestand voor de TelcoGenerator Hallo event hub en de verbindingsreeks wordt weergegeven](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  Hallo-bestand opslaan. 

### <a name="start-hello-app"></a>Hallo-app te starten
1.  Open een opdrachtvenster en toohello map waarbij Hallo TelcoGenerator app uitgepakte wijzigen.
2.  Voer Hallo volgende opdracht:

        telcodatagen.exe 1000 .2 2

    Hallo-parameters zijn: 

    * Aantal CDR per uur. 
    * SIM-kaart fraude waarschijnlijkheid: Hoe vaak, als een percentage van alle aanroepen die Hallo-app moet simuleren een aanroep van frauduleuze. Hallo waarde.2 betekent dat ongeveer 20% van Hallo aanroep records frauduleuze uitziet.
    * De duur in uren. Hallo aantal uren dat Hallo app moet worden uitgevoerd. U kunt ook Hallo app elk gewenst moment stoppen door op Ctrl + C drukken op Hallo-opdrachtregel.

    Na enkele seconden begint Hallo app weergeven van telefoongesprek records op Hallo scherm, zoals het ze toohello event hub verzendt.

Enkele van Hallo sleutelvelden die u in deze detectie realtime fraude toepassing gebruiken wilt zijn hello volgende:

|**Record**|**Definitie**|
|----------|--------------|
|`CallrecTime`|Begintijd Hallo tijdstempel voor Hallo-aanroep. |
|`SwitchNum`|Hallo telefoon switch gebruikt tooconnect Hallo aanroep. In dit voorbeeld zijn Hallo switches tekenreeksen die staan voor Hallo land van oorsprong (VS, China, UK, Duitsland of Australië). |
|`CallingNum`|telefoonnummer van de aanroepfunctie Hallo Hallo. |
|`CallingIMSI`|Hallo International Mobile Subscriber Identity (IMSI). Dit is de unieke id van de aanroepfunctie Hallo Hallo. |
|`CalledNum`|Hallo telefoonnummer van Hallo aanroep ontvanger. |
|`CalledIMSI`|International Mobile Subscriber Identity (IMSI). Dit is de unieke id van de Hallo van Hallo aanroep ontvanger. |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a>Maken van een Stream Analytics-taak toomanage gegevensstromen

Nu dat u een stream van de aanroep van gebeurtenissen hebt, kunt u een Stream Analytics-taak instellen. Hallo taak leest gegevens van Hallo event hub die u hebt ingesteld. 

### <a name="create-hello-job"></a>Hallo-taak maken 

1. Klik in hello Azure-portal, op **nieuw** > **Internet der dingen** > **Stream Analytics-taak**.

2. Naam Hallo taak `sa_frauddetection_job_demo`, een abonnement, resourcegroep en locatie opgeven.

    Het is een goed idee tooplace Hallo taak en Hallo event hub in Hallo dezelfde regio voor optimale prestaties en doet dat niet u tootransfer gegevens tussen regio's betaalt.

    ![Nieuwe Stream Analytics-taak maken](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. Klik op **Create**.

    Hallo-taak is gemaakt en Hallo portal geeft taakdetails weer. Er is niets echter nog wordt uitgevoerd, u tooconfigure Hallo taak hebben voordat deze kan worden gestart.

### <a name="configure-job-input"></a>Taak invoer configureren

1. In het Hallo-dashboard of Hallo **alle resources** blade, zoek en selecteer Hallo `sa_frauddetection_job_demo` Stream Analytics-taak. 
2. In Hallo **taak topologie** sectie Hallo blade Stream Analytics-taak, klikt u op Hallo **invoer** vak.

    ![Invoervak onder topologie in de blade Hallo Streaming Analytics-taak](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. Klik op  **+ &nbsp;toevoegen** en vult Hallo-blade met deze waarden:

    * **Invoeralias**: Gebruik de naam van Hallo `CallStream`. Als u een andere naam gebruikt, noteer het omdat u hebt deze later nodig.
    * **Gegevensbrontype**: Selecteer **gegevensstroom**. (**Referentiegegevens** toostatic lookup gegevens, die u niet in deze zelfstudie gebruikt verwijst.)
    * **Bron**: Selecteer **Event hub**.
    * **Optie importeren**: Selecteer **gebruik event hub uit het huidige abonnement**. 
    * **Service bus-naamruimte**: Selecteer Hallo event hub naamruimte die u eerder hebt gemaakt (`<yourname>-eh-ns-demo`).
    * **Event hub**: Selecteer Hallo event hub die u eerder hebt gemaakt (`sa-eh-frauddetection-demo`).
    * **Naam Event hub beleid**: Selecteer Hallo-beleid dat u eerder hebt gemaakt (`sa-policy-manage-demo`).

    ![Nieuwe invoer voor Streaming Analytics-taak maken](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. Klik op **Create**.

## <a name="create-queries-tootransform-real-time-data"></a>Query's realtime gegevens tootransform maken

U hebt op dit moment een Stream Analytics-taak tooread instellen met een binnenkomende gegevensstroom. de volgende stap Hallo is toocreate een transformatie die Hallo-gegevens in real-time analyseert. U doen dit door een query te maken. Stream Analytics ondersteunt een eenvoudig, declaratief querymodel die transformaties voor realtime-verwerking beschrijft. Hallo-query's een SQL-achtige taal gebruiken die een aantal specifieke toostream extensies analytics heeft. 

Een zeer eenvoudige query eventueel gewoon alle inkomende hello-gegevens lezen. U maken vaak echter query's die eruit voor specifieke gegevens of relaties in Hallo gegevens zien. In deze sectie van de zelfstudie Hallo maakt en enkele query's toolearn een aantal manieren waarop u een invoerstroom voor analyse kunt transformeren testen. 

Hallo-query's die u hier maakt, wordt alleen Hallo getransformeerde gegevens toohello scherm weergegeven. In een volgende sectie configureert u uitvoerlocatie en een query die Hallo getransformeerde gegevens toothat sink schrijft.

toolearn meer informatie over het Hallo-taal, Zie Hallo [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/dn834998.aspx).

### <a name="get-sample-data-for-testing-queries"></a>Voorbeeldgegevens ophalen voor het testen van query 's

Hallo TelcoGenerator app aanroep records toohello event hub verzendt en de Stream Analytics-taak is geconfigureerde tooread van Hallo event hub. U kunt een query tootest Hallo taak toomake ervoor correct lezen. een query te testen in hello Azure-console, moet u voorbeeldgegevens. Voor dit scenario moet u voorbeeldgegevens extraheren uit het Hallo-stroom die afkomstig is in Hallo event hub.

1. Zorg ervoor dat Hallo TelcoGenerator app wordt uitgevoerd en aanroep records produceren.
2. In de portal voor Hallo retourneren blade toohello Streaming Analytics-taak. (Als u Hallo blade hebt gesloten, zoekt u naar `sa_frauddetection_job_demo` in Hallo **alle resources** blade.)
3. Klik op Hallo **Query** vak. Azure bevat Hallo invoer en uitvoer die zijn geconfigureerd voor Hallo taak en kunnen u een query maken die u kunt de invoerstroom Hallo transformeren toohello uitvoer worden verzonden.
4. In Hallo **Query** blade, klikt u op Hallo punten volgende toohello `CallStream` invoer- en selecteer vervolgens **voorbeeldgegevens uit de invoer**.

    ![Menu Opties toouse voorbeeldgegevens voor Hallo Streaming Analytics-job vermelding met 'Voorbeeldgegevens uit invoer' geselecteerd](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    Hiermee opent u een blade die u opgeven hoeveel sample data tooget kunt, gedefinieerd in termen van hoe lang tooread Hallo stream invoeren.

5. Stel **minuten** too3 en klik vervolgens op **OK**. 
    
    ![Opties voor de invoerstroom hello, een steekproef met '3 minuten' geselecteerd.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    Azure 3 minuten aan gegevens uit de invoerstroom Hallo voorbeelden en waarschuwt u als voorbeeldgegevens Hallo gereed is. (Dit duurt even.) 

Hallo voorbeeldgegevens worden tijdelijk opgeslagen en is beschikbaar tijdens het Hallo-query-venster geopend. Als u Hallo query-venster sluit, Hallo voorbeeldgegevens worden genegeerd en hebt u toocreate een nieuwe set met voorbeeldgegevens. 

Als alternatief kunt u een .json-bestand met voorbeeldgegevens erin krijgen [vanuit GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json), en vervolgens die toouse .json-bestand uploaden als u voorbeeldgegevens voor Hallo `CallStream` invoer. 

### <a name="test-using-a-pass-through-query"></a>Testen met behulp van een Pass Through-query

Als u tooarchive elke gebeurtenis wilt, kunt u een Pass Through-query tooread alle Hallo velden in de nettolading Hallo van Hallo gebeurtenis.

1. Voer deze query in Hallo-query-venster:

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    >Net als bij SQL, trefwoorden zijn niet hoofdlettergevoelig en maakt niet uit witruimte.

    In deze query `CallStream` alias is Hallo die u hebt opgegeven tijdens het maken van Hallo-invoer. Als u een andere alias gebruikt, gebruikt u de naam.

2. Klik op **Test**.

    Hallo Stream Analytics-taak wordt uitgevoerd Hallo query op Hallo voorbeeldgegevens en Hallo uitvoer wordt weergegeven onder Hallo van Hallo-venster. Weet u dat Hallo event hub en Hallo Streaming Analytics-taak juist zijn geconfigureerd. (Zoals is aangegeven, later maakt u een uitvoerlocatie die Hallo query kan gegevens te schrijven.)

    ![Stream Analytics-taak uitvoer geproduceerd, 73 records die zijn gegenereerd worden weergegeven](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    Hallo kunt u het exacte aantal records dat er afhankelijk van hoeveel records zijn opgenomen in uw voorbeeld 3 minuten.
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a>Verminder het aantal velden met behulp van een kolom projectie Hallo

In veel gevallen hoeft uw analyse niet alle Hallo kolommen uit de invoerstroom Hallo. U kunt een query tooproject een kleiner aantal velden dan geretourneerd in Hallo Pass Through-query.

1. Hallo-query in Hallo code-editor toohello volgende wijzigen:

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. Klik op **Test** opnieuw. 

    ![Stream Analytics-taak uitvoer geproduceerd voor projectie, met 25 records die zijn gegenereerd](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a>Aantal binnenkomende aanroepen per regio: tumblingvenster met aggregatie

Stel dat u wilt dat toocount Hallo aantal binnenkomende aanroepen per regio. In het streamen van gegevens als u wilt dat tooperform statistische functies zoals telling, moet u toosegment Hallo stream in de tijdelijke eenheden (omdat het Hallo-gegevensstroom zelf is effectief eindeloze). Hiervoor gebruikt een Streaming Analytics [venster functie](stream-analytics-window-functions.md). Vervolgens kunt u werken met Hallo-gegevens in dit venster als eenheid.

Voor deze transformatie die u wilt een reeks van tijdelijke windows die elkaar niet overlappen, elk venster heeft een aparte set gegevens die u kunt groeperen en statistische functie. Dit type venster waarnaar wordt verwezen tooas is een *tumblingvenster* . Binnen tumblingvenster hello, krijgt u een aantal van de binnenkomende oproepen Hallo gegroepeerd op `SwitchNum`, die staat voor Hallo land waar Hallo oproep afkomstig is. 

1. Hallo-query in Hallo code-editor toohello volgende wijzigen:

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    Deze query gebruikt Hallo `Timestamp By` -sleutelwoord in Hallo `FROM` component toospecify welk tijdstempelveld in Hallo stroom toouse toodefine Hallo-tumblingvenster invoer. In dit geval Hallo venster Hallo gegevens verdeelt in segmenten door Hallo `CallRecTime` veld in elke record. (Als er is geen veld is opgegeven, wordt Hallo windowing bewerking gebruikt Hallo tijd dat elke gebeurtenis op Hallo event hub binnenkomt. Zie 'Tijd tegenover toepassing aankomsttijd' in [Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx). 

    Hallo-projectie omvat `System.Timestamp`, die een tijdstempel voor Hallo einde van elke venster retourneert. 

    toospecify dat u wilt dat een tumblingvenster toouse, gebruikt u Hallo [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) functie in Hallo `GROUP BY `component. In de functie hello geeft u een tijdseenheid (van een microseconden tooa dag) en een venstergrootte (hoeveel units). In dit voorbeeld bestaat Hallo tumblingvenster uit 5 seconden intervallen, zodat u een telling per land voor elke vijf seconden aan aanroepen krijgt.

2. Klik op **Test** opnieuw. In Hallo resultaten, ziet u dat tijdstempels Hallo onder **WindowEnd** in stappen van 5 seconden zijn.

    ![Stream Analytics-taak uitvoer geproduceerd voor aggregatie, met 13 records die zijn gegenereerd](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a>Met behulp van een self-join SIM-fraude te detecteren

Bijvoorbeeld, kunnen we frauduleuze gebruik toobe aanroepen die afkomstig uit Hallo dezelfde zijn beschouwen gebruiker, maar in verschillende locaties binnen 5 seconden van elkaar. Bijvoorbeeld: hello dezelfde gebruiker niet daadwerkelijk maken een aanroep van Hallo VS en Australië op Hallo hetzelfde moment. 

toocheck voor dergelijke gevallen kunt u een self-join Hallo streaming gegevens toojoin Hallo stroom tooitself op basis van Hallo `CallRecTime` waarde. U kunt vervolgens zoeken voor aanroep registreert waar hello `CallingIMSI` waarde (hello oorspronkelijk aantal) is Hallo dezelfde, maar Hallo `SwitchNum` waarde (land van oorsprong) is niet dezelfde Hallo.

Wanneer u een join gebruikt met het streamen van gegevens, moet een aantal beperkingen met betrekking tot hoe ver Hallo die overeenkomen met rijen in de tijd kunnen worden gescheiden Hallo join opgeven. (Zoals eerder opgemerkt, Hallo gegevensstromen is effectief eindeloze.) Hallo tijd grenzen voor Hallo relatie worden opgegeven in de Hallo `ON` component Hallo join, met behulp van Hallo `DATEDIFF` functie. In dit geval is Hallo join gebaseerd op een interval van 5 seconden van de van aanroepgegevens.

1. Hallo-query in Hallo code-editor toohello volgende wijzigen: 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    Deze query is vergelijkbaar met een SQL-join, met uitzondering van Hallo `DATEDIFF` functie Hallo join. Dit is een versie van `DATEDIFF` die specifieke tooStreaming Analytics, en deze moet worden weergegeven in Hallo `ON...BETWEEN` component. Hallo-parameters zijn een tijdseenheid (seconden in dit voorbeeld) en aliassen van twee bronnen voor de join Hallo HALLO hallo. (Dit verschilt van standaard SQL Hallo `DATEDIFF` functie.) 

    Hallo `WHERE` -component bevat Hallo-voorwaarde die Hallo frauduleuze aanroep vlaggen: Hallo oorspronkelijke switches zijn niet dezelfde Hallo. 

2. Klik op **Test** opnieuw. 

    ![Stream Analytics-taak uitvoer geproduceerd voor self-join, zichtbaar 6 records gegenereerd](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. Klik op **Opslaan**. Dit bespaart Hallo zelf join-query als onderdeel van Hallo Streaming Analytics-taak. (Deze kunt Hallo voorbeeldgegevens niet opslaan.)

    ![Opslaan van Stream Analytics-taak](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a>Maken van een toostore getransformeerd uitvoergegevens van de sink

U hebt een stroom gebeurtenissen, een event hub invoer tooingest gebeurtenissen en een query tooperform een transformatie gedefinieerd via Hallo-stroom. de laatste stap Hallo is toodefine uitvoerlocatie voor Hallo taak — dat wil zeggen, een plaats toowrite Hallo stroom moet worden omgezet. 

U kunt veel resources gebruiken als uitvoer put: een SQL Server-database, -tabelopslag Data Lake storage, Power BI en zelfs een ander event hub. Voor deze zelfstudie schrijft u Hallo stroom tooAzure Blob-opslag een typische keuze is voor het verzamelen van gebeurtenisgegevens voor latere analyse, omdat het is geschikt voor niet-gestructureerde gegevens.

Als u een bestaande blob storage-account hebt, kunt u die kunt gebruiken. Voor deze zelfstudie leert u hoe toocreate een nieuwe opslag account alleen voor deze zelfstudie.

### <a name="create-an-azure-blob-storage-account"></a>Een Azure Blob Storage-account maken

1. In de Azure-portal hello, retourneren blade toohello Streaming Analytics-taak. (Als u Hallo blade hebt gesloten, zoekt u naar `sa_frauddetection_job_demo` in Hallo **alle resources** blade.)
2. In Hallo **taak topologie** sectie, klikt u op Hallo **uitvoer** vak. 
3. In Hallo **uitvoer** blade, klikt u op  **+ &nbsp;toevoegen** en vult Hallo-blade met deze waarden:

    * **Uitvoeraliassen**: Gebruik de naam van Hallo `CallStream-FraudulentCalls`. 
    * **Sink**: Selecteer **Blob storage**.
    * **Opties voor het importeren**: Selecteer **gebruik blob storage uit het huidige abonnement**.
    * **Storage-account**. Selecteer **nieuw opslagaccount maken.**
    * **Storage-account** (tweede vak). Voer `YOURNAMEsademo`, waarbij `YOURNAME` uw naam of een andere unieke tekenreeks is. Hallo-naam kan gebruiken die alleen kleine letters en cijfers en deze uniek zijn binnen Azure. 
    * **Container**. Voer `sa-fraudulentcalls-demo`.
    Hallo opslagaccountnaam- en containernaam zijn gebruikte samen tooprovide een URI voor Hallo blob storage als volgt: 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    !['Nieuw uitvoer' blade voor Stream Analytics-taak](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. Klik op **Create**. 

    Azure storage-account Hallo maakt en genereert een sleutel automatisch. 

5. Sluit Hallo **uitvoer** blade. 

## <a name="start-hello-streaming-analytics-job"></a>Hallo Streaming Analytics-taak starten

Hallo-taak is nu geconfigureerd. U hebt opgegeven invoer (Hallo event hub), een transformatie (Hallo query toolook voor frauduleuze aanroepen) en uitvoer (blobopslag). U kunt nu Hallo taak starten. 

1. Zorg ervoor dat Hallo TelcoGenerator app wordt uitgevoerd.

2. Klik op Hallo taakblade **Start**.

    ![Hallo Stream Analytics-taak starten](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. In Hallo **starttaak** blade voor de taak uitvoer begintijd, selecteer **nu**. 

4. Klik op **Start**. 

    ![Blade 'Start de taak' voor Hallo Stream Analytics-taak](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    Azure waarschuwt u als Hallo-taak is gestart en Hallo taak blade Hallo status wordt weergegeven als **met**.

    ![Stream Analytics-taakstatus 'Actief' wordt weergegeven](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a>Hallo getransformeerd gegevens controleren

U hebt nu een volledige Streaming Analytics-taak. Hallo-taak is vindt u in een stream van telefoongesprek metagegevens van frauduleuze telefoongesprekken in realtime zoekt en schrijven van informatie over deze toostorage frauduleuze aanroepen. 

toocomplete in deze zelfstudie kunt u toolook Hallo gegevens wordt vastgelegd door Hallo Streaming Analytics-taak. Hallo gegevens wordt tooAzure Blog opslag geschreven in segmenten (bestanden). U kunt elk hulpprogramma dat Azure Blob Storage gebruiken. Zoals beschreven in de sectie vereisten hello, kunt u Azure-extensies in Visual Studio of kunt u een hulpprogramma zoals [Azure Opslagverkenner](http://storageexplorer.com/) of [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction). 

Wanneer u hello inhoud van een bestand in blob storage bekijkt, weergegeven dat lijkt op Hallo volgende:

![Azure blob storage met Streaming Analytics-uitvoer](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a>Resources opschonen

We hebben meer artikelen die doorgaan met Hallo detecteren van fraude scenario en die Hallo bronnen gebruiken die u in deze zelfstudie hebt gemaakt. Als u toocontinue wilt, raadpleegt u suggesties Hallo onder **Vervolgstappen** later.

Als u bent klaar en u hoeft niet Hallo-resources die u hebt gemaakt, kunt u echter verwijderen ze zodat u geen onnodige Azure kosten. In dat geval is het raadzaam dat u Hallo te volgen:

1. Hallo Streaming Analytics-taak stoppen. In Hallo **taken** blade, klikt u op **stoppen** Hallo bovenaan.
2. Hallo Telco Generator app stoppen. Hallo-opdrachtvenster waar u Hallo app gestart, klikt u op Ctrl + C.
3. Als u een blob storage-account voor deze zelfstudie hebt gemaakt, verwijderen. 
4. Hallo Streaming Analytics-taak verwijderen.
5. Verwijder Hallo event hub.
6. Hallo event hub-naamruimte verwijderd.

## <a name="get-support"></a>Ondersteuning krijgen

Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Volgende stappen

Deze zelfstudie kunt u doorgaan met de Hallo artikelen te volgen:

* [Stream Analytics en Power BI: een realtime analytics-dashboard voor het streamen van gegevens](stream-analytics-power-bi-dashboard.md). Dit artikel laat zien hoe toosend Hallo TelCo uitvoer van de Stream Analytics Hallo taak tooPower BI voor realtime visualisatie en analyse.
* [Hoe toostore gegevens uit Azure Stream Analytics in een Azure Redis-Cache met behulp van Azure Functions](stream-analytics-functions-redis.md). Dit artikel laat zien hoe toouse Azure Functions toowrite frauduleuze tooan Azure Redis-cache via een Service Bus-wachtrij aanroept.

Voor meer informatie over Stream Analytics in het algemeen proberen deze artikelen:

* [Inleiding tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)
