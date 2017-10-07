---
title: aaaPower BI-zelfstudie voor Azure DB die Cosmos-connector | Microsoft Docs
description: Gebruik deze zelfstudie tooimport van Power BI JSON, begrijpelijke manier mee rapporten maken en gegevens visualiseren met behulp van hello Azure Cosmos DB en Power BI-connector.
keywords: Power bi zelfstudie, visualiseren van gegevens, power bi-connector
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a>Power BI-zelfstudie voor Azure Cosmos DB: gegevens visualiseren met Power BI-connector Hallo
[PowerBI.com](https://powerbi.microsoft.com/) is een onlineservice waar u kunt maken en delen van dashboards en rapporten met gegevens die belangrijk tooyou en uw organisatie.  Power BI Desktop is een speciaal rapporteren ontwerpgereedschap waarmee u tooretrieve gegevens uit diverse bronnen, samenvoegen en Hallo gegevens transformeren krachtige rapporten en visualisaties maken en publiceren Hallo rapporten tooPower BI.  Met Hallo meest recente versie van Power BI Desktop, kunt u nu tooyour Cosmos DB account via Hallo Cosmos-DB-connector voor Power BI verbinding.   

In deze zelfstudie Power BI we doorlopen Hallo stappen tooconnect tooa Cosmos-DB-account in Power BI Desktop, tooa verzameling waar we tooextract Hallo gegevens met behulp van Hallo Navigator transformatie JSON-gegevens in tabelvorm met Power BI Desktop Query wilt navigeren -Editor en maken en publiceren van een rapport tooPowerBI.com.

Na het voltooien van deze zelfstudie Power BI, moet u kunnen tooanswer Hallo vragen te volgen:  

* Hoe kan ik rapporten maken met gegevens van de Cosmos-database met behulp van Power BI Desktop?
* Hoe kan ik tooa Cosmos-DB-account in Power BI Desktop verbinden?
* Hoe kan ik gegevens ophalen uit een verzameling in Power BI Desktop?
* Hoe kan ik geneste JSON-gegevens in Power BI Desktop transformeren?
* Hoe kan ik publiceren en delen van mijn rapporten op PowerBI.com?

> [!NOTE]
> Hallo Power BI-connector voor Azure Cosmos DB verbindt tooPower BI Desktop voor extractie en transformatie van gegevens. Rapporten die zijn gemaakt in Power BI Desktop kunnen gepubliceerde tooPowerBI.com vervolgens worden. Directe uitpakken en transformatie van Azure DB die Cosmos-gegevens kunnen niet worden uitgevoerd op PowerBI.com. 

## <a name="prerequisites"></a>Vereisten
Voordat Hallo-instructies in deze zelfstudie Power BI, zorg ervoor dat u hebt toegang toohello resources te volgen:

* [Hallo meest recente versie van Power BI Desktop](https://powerbi.microsoft.com/desktop).
* Account voor toegang tot tooour demo of gegevens in uw account Cosmos DB.
  * Hallo demo-account is gevuld met Hallo Vulkaan gegevens weergegeven in deze zelfstudie. Dit account demo niet afhankelijk is van een SLA's en is bedoeld voor demonstratiedoeleinden alleen.  Behoudt Hallo rechts toomake wijzigingen toothis demo account waaronder maar niet beperkt tot wordt beëindigd Hallo account Hallo-sleutel, beperken van toegang, wijzigen, wijzigen en verwijderen Hallo gegevens, op elk moment zonder voorafgaande kennisgeving of reden.
    * URL: https://analytics.documents.azure.com
    * Alleen-lezen-sleutel: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR + YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw ==
  * Of toocreate uw eigen account, Zie [een Azure Cosmos DB database-account maken met Azure-portal Hallo](https://azure.microsoft.com/documentation/articles/create-account/). Vervolgens tooget Vulkaan voorbeeldgegevens die vergelijkbaar toowhat in deze zelfstudie gebruikt (maar bevat geen Hallo GeoJSON blokken), Zie Hallo [NOAA site](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) en importeer Hallo-gegevens met behulp van Hallo [gegevensmigratie Azure Cosmos-DB hulpprogramma](import-data.md).

tooshare uw rapporten op PowerBI.com, hebt u een account op PowerBI.com.  toolearn meer informatie over Power BI voor vrije en Power BI Pro, gaat u naar [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).

## <a name="lets-get-started"></a>Aan de slag
In deze zelfstudie gaan we stelt u zich voor dat u een geologist bestudeert vulkanen Hallo wereld.  Hallo Vulkaan gegevens worden opgeslagen in een Cosmos-DB-account en Hallo JSON-documenten eruitzien als Hallo voorbeelddocument te volgen.

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

Wilt u tooretrieve Hallo Vulkaan gegevens uit Hallo Cosmos-DB-account en visualiseren van gegevens in een interactieve Power BI-rapport zoals Hallo rapport te volgen.

![Door deze zelfstudie Power BI met Hallo Power BI-connector is voltooid, moet u kunnen toovisualize gegevens met Power BI Desktop Vulkaan rapport Hallo](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

Gereed toogive deze in een try? Aan de slag.

1. Power BI Desktop worden uitgevoerd op uw werkstation.
2. Als Power BI Desktop wordt gestart, een *Welkom* scherm wordt weergegeven.
   
    ![Power BI Desktop welkomstscherm - Power BI-connector](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. U kunt **gegevens ophalen**, Zie **recente bronnen**, of **Open andere rapporten** rechtstreeks vanuit Hallo *Welkom* scherm.  Klik op Hallo X op Hallo rechterbovenhoek tooclose welkomstscherm. Hallo **rapport** weergave van Power BI Desktop.
   
    ![Power BI Desktop rapportweergave - Power BI-connector](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. Selecteer Hallo **Start** lint en klik vervolgens op **gegevens ophalen**.  Hallo **gegevens ophalen** venster moet worden weergegeven.
5. Klik op **Azure**, selecteer **Microsoft Azure DocumentDB (bèta)**, en klik vervolgens op **Connect**. 

    ![Power BI Desktop ophalen van gegevens - Power BI-connector](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. Op Hallo **Preview Connector** pagina, klikt u op **doorgaan**. Hallo **Microsoft Azure DocumentDB Connect** venster wordt weergegeven.
7. Geef Hallo Cosmos DB eindpunt URL van account u wilt tooretrieve Hallo gegevens uit zoals hieronder wordt weergegeven, en klik vervolgens op **OK**. toouse uw eigen account, kunt u URL uit Hallo URI vak Hallo Hallo ophalen  **[sleutels](manage-account.md#keys)**  blade van hello Azure-portal. toouse hello demo account, voert u `https://analytics.documents.azure.com` voor Hallo-URL. 
   
    Hallo-databasenaam verzamelingsnaam en SQL-instructie leeg laten als u deze velden zijn optioneel.  We gebruiken in plaats daarvan Hallo Navigator tooselect Hallo Database en verzameling tooidentify waar Hallo gegevens opgehaald.
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, bureaublad-venster verbinding maken](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. Als u verbinding toothis eindpunt voor Hallo eerst maakt, wordt u gevraagd Hallo accountsleutel op te geven. Voor uw eigen account ophalen met de sleutel Hallo Hallo **primaire sleutel** vak Hallo  **[alleen-lezen sleutels](manage-account.md#keys)**  blade van hello Azure-portal. Voor de demo-account Hallo Hallo-sleutel is `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`. Voer de juiste sleutel Hallo en klik vervolgens op **Connect**.
   
    Het is raadzaam dat u de sleutel alleen-lezen Hallo bij het maken van rapporten.  Hierdoor kan onnodige blootstelling van Hallo hoofdsleutel toopotential beveiligingsrisico's. Hallo alleen-lezen-sleutel is beschikbaar via Hallo [sleutels](manage-account.md#keys) blade van hello Azure-portal of u kunt Hallo demo-accountgegevens bovenstaande gebruiken.
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, Accountsleutel](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > Als u krijgt een fout met de tekst is "Hallo opgegeven database niet gevonden." Zie Hallo tijdelijke oplossing in deze stappen [Power BI probleem](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).
    
9. Wanneer het Hallo-account verbinding is gemaakt, Hallo **Navigator** wordt weergegeven.  Hallo **Navigator** ziet een lijst met databases onder Hallo-account.
10. Klik op en vouw op Hallo database waar gegevens Hallo Hallo rapport, zijn afkomstig van, als u Hallo demo-account, selecteert u **volcanodb**.   
11. Selecteer nu een verzameling die u zal Hallo gegevens ophalen uit. Als u Hallo demo-account gebruikt, selecteert u **volcano1**.
    
    Hallo voorbeeldvenster bevat een overzicht van **Record** items.  Een Document wordt weergegeven als een **Record** type in Power BI. Een geneste JSON-blok in het document is op deze manier ook een **Record**.
    
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, Navigator-venster](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. Klik op **bewerken** toolaunch Hallo Query-Editor in een nieuw venster tootransform Hallo-gegevens.

## <a name="flattening-and-transforming-json-documents"></a>Plat en transformeren JSON-documenten
1. Schakeloptie toohello Power BI Query-editorvenster, hello **Document** kolom in het middelste deelvenster Hallo.
   ![Power BI Desktop Query-Editor](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. Klik op Hallo uitbreidingsmodule aan de rechterkant Hallo Hallo **Document** kolomkop.  Hallo contextmenu met een lijst met velden worden weergegeven.  Selecteer het Hallo-velden die u nodig hebt voor uw rapport voor exemplaar, Vulkaan naam, land, regio, locatie, uitbreiding van bevoegdheden, Type, Status en laatste weten uitbreken en klik vervolgens op **OK**.
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector - documenten uitvouwen](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. Hallo middelste deelvenster wordt een voorbeeld van resultaat Hallo weergegeven met Hallo velden geselecteerd.
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector - plat resultaten](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. In ons voorbeeld is Hallo locatie-eigenschap een blok GeoJSON in een document.  Zoals u zien kunt, de locatie wordt weergegeven als een **Record** type in Power BI Desktop.  
5. Klik op Hallo uitbreidingsmodule aan de rechterkant Hallo van Hallo locatie kolomkop te klikken.  Hallo contextmenu met type en coördinaten velden worden weergegeven.  Laten we Selecteer Hallo coördinaten veld en klikt u op **OK**.
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, locatie-record](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. Hallo middelste deelvenster wordt nu een kolom coördinaten van **lijst** type.  Zoals wordt weergegeven aan begin van de zelfstudie Hallo Hallo, wordt de status van Hallo GeoJSON-gegevens in deze zelfstudie is van het type met breedtegraad en lengtegraad waarden worden vastgelegd in Hallo coördinaten matrix.
   
    Hallo coördinaten [0]-element vertegenwoordigt lengtegraad terwijl coördinaten [1] breedtegraad vertegenwoordigt.
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, coördinaten lijst](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. tooflatten hello coördineert de matrix, maken we een **aangepaste kolom** LatLong aangeroepen.  Selecteer Hallo **kolom toevoegen** lint en klik op **aangepaste kolom toevoegen**.  Hallo **aangepaste kolom toevoegen** venster moet worden weergegeven.
8. Geef een naam voor de nieuwe kolom hello, bijvoorbeeld LatLong.
9. Geef vervolgens de aangepaste formule voor de nieuwe kolom Hallo Hallo.  In ons voorbeeld wordt we Hallo breedtegraad en lengtegraad waarden, gescheiden door een komma als volgt met behulp van de volgende formule Hallo samenvoegen: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`. Klik op **OK**.
   
    Ga voor meer informatie over gegevens Analysis expressies (DAX) waaronder DAX-functies [Basic DAX in Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, aangepaste kolom toevoegen](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. Hallo middelste deelvenster wordt nu weergegeven Hallo nieuwe LatLong kolom is gevuld met Hallo breedtegraad en lengtegraadwaarden, gescheiden door komma's.
    
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, aangepaste LatLong kolom](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    Als u een foutbericht in de nieuwe kolom hello ontvangt, controleren of Hallo toegepast stappen onder Query-instellingen overeenkomen met de Hallo volgende afbeelding:
    
    ![Toegepaste stappen moet bron, navigatie, uitgebreid Document, uitgebreid Document.Location, aangepaste toegevoegd](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    Als de stappen van de verschillend zijn, verwijdert u extra stappen Hallo en probeer het opnieuw toe te voegen Hallo aangepaste kolom. 
11. We hebt nu afvlakken Hallo-gegevens in tabelvorm voltooid.  U kunt profiteren van alle Hallo die beschikbaar zijn in Hallo tooshape Query-Editor en transformatie van gegevens in Cosmos-database.  Als u Hallo voorbeeld, Hallo gegevenstype wijzigen voor uitbreiding van bevoegdheden te**geheel getal** door het wijzigen van Hallo **gegevenstype** op Hallo **Start** lint.
    
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector - type van de kolom wijzigen](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. Klik op **sluiten en toepassen** toosave Hallo-gegevensmodel.
    
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, sluit & toepassen](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a>Hallo-rapporten maken
Power BI Desktop rapportweergave is waar u gegevens toovisualize maken van rapporten kan starten.  U kunt rapporten maken met slepen en neerzetten van velden in Hallo **rapport** canvas.

![Power BI Desktop rapportweergave - Power BI-connector](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

U moet in Hallo rapportweergave vinden:

1. Hallo **velden** deelvenster dit is waar u ziet een lijst met gegevensmodellen met velden die u voor uw rapporten gebruiken kunt.
2. Hallo **visualisaties** deelvenster. Een rapport kan één of meerdere visualisaties bevatten.  Kies Hallo visual typen aanpassen van uw behoeften van Hallo **visualisaties** deelvenster.
3. Hallo **rapport** canvas, dit is waar bouwt u Hallo visuele elementen voor uw rapport.
4. Hallo **rapport** pagina. U kunt meerdere pagina's het rapport in Power BI Desktop toevoegen.

Hallo hieronder vindt u eenvoudige stappen Hallo van het maken van een eenvoudige interactieve kaart view-rapport.

1. We gaan een overzichtsweergave met Hallo plaats voor elke Vulkaan maken in ons voorbeeld.  In Hallo **visualisaties** deelvenster, klik op Hallo visual maptype als gemarkeerd in de bovenstaande Hallo.  U ziet Hallo kaart visuele element getekend op Hallo **rapport** canvas.  Hallo **visualisatie** deelvenster moet ook een set eigenschappen gerelateerde toohello visual maptype worden weergegeven.
2. Nu vanuit slepen en neerzetten Hallo LatLong veld Hallo **velden** deelvenster toohello **locatie** eigenschap in **visualisaties** deelvenster.
3. Vervolgens slepen en neerzetten Hallo Vulkaan naam veld toohello **legenda** eigenschap.  
4. Vervolgens slepen en neerzetten Hallo uitbreiding van bevoegdheden veld toohello **grootte** eigenschap.  
5. U ziet nu Hallo kaart visual met een set van bellen Hallo-locatie van elke Vulkaan met Hallo grootte van Hallo belgrootte correleren toohello onrechtmatige uitbreiding van Hallo Vulkaan waarmee wordt aangegeven.
6. U hebt nu een eenvoudig rapport gemaakt.  U kunt verder Hallo rapport aanpassen door meer visualisaties toe te voegen.  In ons geval hebben we een vulkaan slicer toomake Hallo rapport van het Type interactieve toegevoegd.  
   
    ![Schermopname van het laatste Power BI Desktop rapport Hallo na voltooiing van Hallo Power BI-zelfstudie voor Azure Cosmos-DB](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a>Publiceren en delen van uw rapport
tooshare uw rapport hebt u een account op PowerBI.com.

1. Hallo Power BI Desktop, klik op Hallo **Start** lint.
2. Klik op **Publish**.  U zult na vragen aan gebruiker tooenter Hallo-gebruikersnaam en wachtwoord voor uw account PowerBI.com.
3. Zodra het Hallo-referentie is geverifieerd, is Hallo rapport gepubliceerde tooyour bestemming die u hebt geselecteerd.
4. Klik op **Open 'PowerBITutorial.pbix' in Power BI** toosee en delen van uw rapport op PowerBI.com.
   
    ![Publishing tooPower BI geslaagd! Open zelfstudie in Power BI](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>Een dashboard maken in PowerBI.com
Nu dat u een rapport hebt, kunnen delen op PowerBI.com

Wanneer u uw rapport uit Power BI Desktop tooPowerBI.com publiceert, genereert een **rapport** en een **gegevensset** in uw tenant PowerBI.com. Bijvoorbeeld: nadat u een rapport genaamd gepubliceerd **PowerBITutorial** tooPowerBI.com, ziet u PowerBITutorial in beide Hallo **rapporten** en **gegevenssets** secties op PowerBI.com.

   ![Schermopname van Hallo nieuwe rapport en gegevensset in PowerBI.com](./media/powerbi-visualize/powerbi-reports-datasets.png)

toocreate een deelbare dashboard, klikt u op Hallo **pincode Live pagina** knop op uw rapport PowerBI.com.

   ![Schermopname van Hallo nieuwe rapport en gegevensset in PowerBI.com](./media/powerbi-visualize/power-bi-pin-live-tile.png)

Volg de instructies Hallo in [een tegel uit een rapport vastmaken](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate een nieuw dashboard. 

U kunt ook ad-hoc wijzigingen tooreport doen voordat u een dashboard. Het wordt echter aanbevolen dat u gebruik van Power BI Desktop tooperform Hallo wijzigingen en Hallo rapport tooPowerBI.com publiceren.

## <a name="refresh-data-in-powerbicom"></a>Gegevens vernieuwen in PowerBI.com
Er zijn twee manieren toorefresh gegevens, ad-hoc en geplande.

Voor een ad-hoc vernieuwen, klikt u gewoon op Hallo eclipses (...) door Hallo **gegevensset**, bijvoorbeeld PowerBITutorial. U ziet een lijst van acties zoals **nu vernieuwen**. Klik op **nu vernieuwen** toorefresh Hallo gegevens.

![Schermopname van vernieuwing nu in PowerBI.com](./media/powerbi-visualize/power-bi-refresh-now.png)

Een geplande vernieuwing Hallo te volgen.

1. Klik op **schema vernieuwen** in lijst Hallo-actie. 

    ![Schermopname van Hallo schema vernieuwen in PowerBI.com](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. In Hallo **instellingen** pagina uit, vouw **gegevensbronreferenties**. 
3. Klik op **bewerken van referenties**. 
   
    Hallo configureren pop-up wordt weergegeven. 
4. Voer Hallo sleutel tooconnect toohello Cosmos DB account voor deze gegevensset en klik vervolgens op **aanmelden**. 
5. Vouw **schema vernieuwen** en stellen Hallo planning wilt toorefresh Hallo gegevensset. 
6. Klik op **toepassen** en u klaar bent Hallo geplande vernieuwing in te stellen.

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn meer informatie over Power BI [aan de slag met Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).
* toolearn meer informatie over de Cosmos-DB, Zie Hallo [startpagina van Azure DB die Cosmos documentatie](https://azure.microsoft.com/documentation/services/documentdb/).

