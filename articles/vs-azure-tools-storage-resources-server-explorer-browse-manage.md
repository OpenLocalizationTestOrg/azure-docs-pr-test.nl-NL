---
title: aaaBrowsing en beheren van opslagbronnen met Server Explorer | Microsoft Docs
description: Bladeren en beheren van opslagbronnen met Server Explorer
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/24/2017
ms.author: kraigb
ms.openlocfilehash: f5b456b812f2ad8103c50538d532a57397bcccbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a>Bladeren en beheren van opslagbronnen met Server Explorer
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Overzicht
Als u hello Azure-hulpprogramma's voor Microsoft Visual Studio hebt geïnstalleerd, kunt u blob, wachtrijen en tabelgegevens weergeven van uw storage-accounts voor Azure. Hello Azure Storage-knooppunt in Server Explorer geeft gegevens in uw lokale emulator opslagaccount en andere Azure storage-accounts.

Kies tooview Server Explorer in Visual Studio op de menubalk Hallo **weergave**, **Server Explorer**. Hallo Opslagknooppunt bevat alle Hallo storage-accounts die bestaan onder elke Azure-abonnement/het certificaat waarmee u bent verbonden. Als uw storage-account niet wordt weergegeven, kunt u deze toevoegen door Hallo instructies te volgen [verderop in dit onderwerp](#add-storage-accounts-by-using-server-explorer).

U start in de Azure SDK 2.7, kunt u ook Hallo nieuwe Cloud Explorer tooview gebruiken en beheren van uw Azure-resources. Zie [Azure-Resources beheren met Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md) voor meer informatie.

## <a name="view-and-manage-storage-resources-in-visual-studio"></a>Weergeven en beheren van opslagbronnen in Visual Studio
Server Explorer wordt automatisch een lijst met blobs, wachtrijen en tabellen in uw opslagaccount van de emulator. Hallo-emulator opslagaccount in Server Explorer wordt vermeld onder Hallo Opslagknooppunt als Hallo **ontwikkeling** knooppunt.

toosee Hallo-emulator van het opslagaccount resources, vouw Hallo **ontwikkeling** knooppunt. Als Hallo opslagemulator nog niet is begonnen, wanneer u Hallo uitbreidt **ontwikkeling** knooppunt, wordt deze automatisch gestart. Dit kan enkele seconden duren. Tijdens het starten van de opslagemulator hello, kunt u de toowork blijven in andere gebieden van Visual Studio.

tooview resources in een opslagaccount, vouw Hallo van het opslagaccount in Server Explorer. Hallo volgende onderliggende knooppunten worden weergegeven:

* Blobs
* Wachtrijen
* Tabellen

## <a name="work-with-blob-resources"></a>Werken met Blob-bronnen
Hallo Blobs knooppunt geeft een lijst van containers voor Hallo geselecteerd storage-account. BLOB-containers blob-bestanden bevat en u kunt deze blobs indelen in mappen en submappen. Zie [hoe toouse Blob Storage in .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md) voor meer informatie.

### <a name="toocreate-a-blob-container"></a>toocreate een blob-container
1. Open Hallo snelmenu voor Hallo **Blobs** knooppunt, en kies vervolgens **Blob-Container maken**.
2. In Hallo **Blob-Container maken** dialoogvenster Hallo- naam van de nieuwe container Hallo.  
3. Druk op **ENTER** op het toetsenbord of u kunt Klik of tik buiten Hallo naam veld toosave Hallo blob-container.
   
   > [!NOTE]
   > Hallo blob-containernaam moet beginnen met een cijfer (0-9) of kleine letter (a-z).
   > 
   > 

### <a name="toodelete-a-blob-container"></a>toodelete een blob-container
* Open Hallo snelmenu voor Hallo blob-container gewenste tooremove en kies vervolgens **verwijderen**.

### <a name="toodisplay-a-list-of-hello-items-contained-in-a-blob-container"></a>toodisplay een lijst met items Hallo opgenomen in een blob-container
* Open Hallo snelmenu voor de naam van een blob-container in Hallo lijst en kies vervolgens **Open**.
  
    Wanneer u hello inhoud van een blob-container bekijkt, wordt deze weergegeven in een tabblad Hallo blob-Containerweergave genoemd.
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    Hallo-bewerkingen op blobs te volgen met Hallo knoppen in Hallo rechtsboven van Hallo blob-Containerweergave kunnen worden uitgevoerd:
  
  * Voer een filterwaarde en dit toepassen
  * Hallo-lijst met blobs in de container Hallo vernieuwen
  * Bestand uploaden
  * Een blob verwijderen
    
    > [!NOTE]
    > Verwijderen van een bestand van een blobcontainer verwijderen Hallo onderliggende bestand; niet deze alleen verwijderd uit Hallo blob-container.
    > 
    > 
  * Open een blob
  * Een blob toohello lokale computer opslaan

### <a name="toocreate-a-folder-or-subfolder-in-a-blob-container"></a>toocreate een map of submap hiervan op in een blob-container
1. Kies Hallo blob-container in Cloud Explorer. Kies in Hallo container venster Hallo **Blob uploaden** knop.
   
    ![Uploaden van een bestand naar een blob-map](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. In Hallo **nieuwe uploaden** dialoogvenster Kies Hallo **Bladeren** knop toospecify Hallo bestand u wilt tooupload en voer de mapnaam van een in Hallo **map (optioneel)** vak .
   
    U kunt toevoegen submappen in de container mappen door Hallo dezelfde procedure. Als u geen naam van een map opgeeft, Hallo bestand zich toohello hoogste niveau van de blob-container Hallo geüpload. Hallo-bestand weergegeven in de opgegeven map in container Hallo Hallo.
   
    ![Map tooa blob-container toevoegen](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. Dubbelklik op Hallo map of druk op ENTER toosee Hallo inhoud van Hallo-map. Wanneer u in de map van de container Hallo bent, kunt u back toohello hoofdmap van de container Hallo gaan door te kiezen Hallo **openen van de bovenliggende map** (pijl-omhoog) knop.

### <a name="toodelete-a-container-folder"></a>een container map toodelete
* Alle bestanden in de map Hallo Hallo verwijderen
  
  > [!NOTE]
  > Omdat in de blob-containers virtuele mappen zijn, u een lege map kan niet maken of kunt u een map toodelete de bestandsinhoud ervan verwijderen. U hebt toodelete Hallo volledige inhoud van een map toodelete Hallo-map.
  > 
  > 

### <a name="toofilter-blobs-in-a-container"></a>toofilter blobs in een container
U kunt filteren Hallo blobs die worden weergegeven door te geven van een algemeen voorvoegsel.

Bijvoorbeeld, als u Hallo voorvoegsel invoeren `hello` in filtervak tekst hello en kies vervolgens Hallo **Execute** (**!**) knop, alleen de blobs die met 'Hallo beginnen' weergegeven.

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> Hallo filterveld is hoofdlettergevoelig en biedt geen ondersteuning voor filteren met jokertekens bevatten. BLOBs kunnen alleen worden gefilterd op voorvoegsel. Hallo-voorvoegsel, omvat mogelijk een scheidingsteken als u een scheidingsteken tooorganize blobs in een virtuele-hiërarchie. Bijvoorbeeld, filteren op voorvoegsel HelloFabric Hallo-retourneert alle blobs vanaf deze tekenreeks.
> 
> 

### <a name="toodownload-blob-data"></a>toodownload blob-gegevens
* In **Cloud Explorer**, open Hallo snelmenu voor een of meer blobs en kies vervolgens **openen**, of kies Hallo blob-naam en kies vervolgens Hallo **openen** of dubbelklik op Hallo blob-naam.
  
    Hallo voortgang van een blob-download wordt weergegeven in Hallo **Azure Activity Log** venster.
  
    Hallo blob in Hallo standaardeditor voor dat bestandstype geopend. Als besturingssysteem Hallo bestandstype hello herkent, Hallo-bestand wordt geopend in een lokaal geïnstalleerde toepassing. anders wordt u gevraagd een toepassing die geschikt is voor het bestandstype Hallo van Hallo blob toochoose. lokale Hallo-bestand dat wordt gemaakt bij het downloaden van een blob is gemarkeerd als alleen-lezen.
  
    BLOB-gegevens wordt lokaal opgeslagen in de cache en gecontroleerd met Hallo van blob laatst gewijzigd in Hallo Blob-service. Als het Hallo-blob is bijgewerkt sinds het laatst is gedownload, wordt het gedownload opnieuw; anders wordt van de lokale schijf Hallo Hallo blob geladen. Een blob is standaard de tijdelijke map gedownload tooa. toodownload blobs tooa specifieke map, open Hallo snelmenu voor Hallo geselecteerd blob-namen en kies **OpslaanAls**. Wanneer u een blob op deze manier opslaat, Hallo blob-bestand is niet geopend en Hallo lokale bestand wordt gemaakt met alleen-lezen-kenmerken.

### <a name="tooupload-blobs"></a>tooupload blobs
* Kies Hallo **Blob uploaden** wanneer Hallo container is geopend voor weergave in de weergave van Hallo blob-container.
  
    U kunt een of meer bestanden tooupload en u kunt bestanden van elk type uploaden. Hallo **Azure Activity Log** toont Hallo voortgang van Hallo uploaden. Voor meer informatie over het toowork met blob-gegevens, Zie [hoe toouse hello Azure Blob Storage-Service in .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).

### <a name="tooview-logs-transferred-tooblobs"></a>tooview logboeken overgedragen tooblobs
* Als u Azure Diagnostics toolog gegevens van uw Azure-toepassing gebruikt en u Logboeken tooyour storage-account hebt overgebracht, ziet u containers die zijn gemaakt door Azure voor deze logboeken. Deze logboeken weergeven in Server Explorer is een eenvoudige manier tooidentify problemen met uw toepassing, vooral als het geïmplementeerde tooAzure is. Zie voor meer informatie over Azure Diagnostics [Logboekregistratiegegevens verzamelen met behulp van Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx).

### <a name="tooget-hello-url-for-a-blob"></a>tooget Hallo-URL voor een blob
* Hallo-blob snelmenu openen en kies vervolgens **kopie URL**.

### <a name="tooedit-a-blob"></a>een blob tooedit
* Selecteer Hallo blob en kies vervolgens Hallo **Open Blob** knop.
  
    Hallo-bestand gedownloade tooa tijdelijke locatie is en op de lokale computer Hallo geopend. Nadat u wijzigingen aanbrengt, moet u Hallo blob opnieuw uploaden.

## <a name="work-with-queue-resources"></a>Werken met Resources van de wachtrij
Opslagwachtrijen services worden gehost in Azure storage-account en u ze kunt gebruiken, kunt u tooallow uw cloud service rollen toocommunicate met elkaar en met andere services door een bericht mechanisme wordt doorgegeven. U kunt toegang tot Hallo wachtrij programmatisch via een cloudservice en via een webservice voor externe clients. U kunt ook toegang tot Hallo wachtrij rechtstreeks via Server Explorer in Visual Studio.

Bij het ontwikkelen van een cloudservice die gebruikmaakt van wachtrijen, kunt u wilt toouse Visual Studio toocreate wachtrijen en interactief te kunnen werken met hen tijdens het ontwikkelen en testen van uw code.

In Server Explorer kunt u Hallo wachtrijen weergeven in een opslagaccount, maken en verwijderen van wachtrijen, opent u een tooview wachtrij de berichten en berichten tooa wachtrij toevoegen. Wanneer u een wachtrij voor weergave opent, kunt u afzonderlijke Hallo-berichten bekijken en kunt u de volgende activiteiten in de wachtrij Hallo met Hallo knoppen in de linkerbovenhoek Hallo Hallo uitvoeren:

* Vernieuw de weergave Hallo van Hallo wachtrij
* Een berichtenwachtrij toohello toevoegen
* Het bovenste Hallo-bericht in wachtrij
* Schakel Hallo gehele wachtrij

Hallo volgende afbeelding ziet u een wachtrij met twee berichten.

![Een wachtrij weergeven](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

Zie voor meer informatie over opslag services wachtrijen, [hoe: gebruik Hallo Queue Storage-Service](http://go.microsoft.com/fwlink/?LinkID=264702). Zie voor informatie over de webservice Hallo voor storage services wachtrijen, [concepten van Queue-Service](http://go.microsoft.com/fwlink/?LinkId=264788). Zie voor meer informatie over hoe toosend berichten tooa opslagservices wachtrij met behulp van Visual Studio [berichten verzenden tooa Services Opslagwachtrij](https://msdn.microsoft.com/library/azure/jj649344.aspx).

> [!NOTE]
> Storage services wachtrijen zijn verschillend van service bus-wachtrijen. Zie voor meer informatie over service bus-wachtrijen, Service Bus-wachtrijen, onderwerpen en abonnementen.
> 
> 

## <a name="work-with-table-resources"></a>Werken met Resources van de tabel
Hello Azure Table storage-service worden opgeslagen voor grote hoeveelheden gestructureerde gegevens. Hallo-service is een NoSQL-gegevensarchief die accepteert geverifieerde aanroepen binnen en buiten hello Azure-cloud. Azure-tabellen zijn ideaal voor het opslaan van gestructureerde, niet-relationele gegevens.

### <a name="toocreate-a-table"></a>toocreate een tabel
1. Selecteer in de Cloud Explorer Hallo **tabellen** knooppunt van Hallo storage-account en kies vervolgens **Create Table**.
2. In Hallo **Create Table** dialoogvenster Voer een naam voor de tabel Hallo.

### <a name="tooview-table-data"></a>de tabelgegevens tooview
1. Open in de Cloud Explorer Hallo **Azure** -knooppunt en open vervolgens Hallo **opslag** knooppunt.
2. Open Hallo storage accountknooppunt dat u geïnteresseerd bent in en vervolgens Hallo Open **tabellen** knooppunt toosee een lijst met tabellen voor Hallo storage-account.
3. Open het snelmenu Hallo voor een tabel en kies vervolgens **tabel**.
   
    ![Een Azure-tabel in Solution Explorer](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

Hallo-tabel is geordend op entiteiten (weergegeven in rijen) en eigenschappen (weergegeven in de kolommen). Hallo volgende afbeelding ziet u bijvoorbeeld entiteiten die worden vermeld in Hallo **tabelontwerp**:

### <a name="tooedit-table-data"></a>de tabelgegevens tooedit
1. In Hallo **tabelontwerp**, opent u het snelmenu Hallo voor een entiteit (één rij) of een eigenschap (één cel) en kies vervolgens **bewerken**.
   
    ![Toevoegen of bewerken van een tabel-entiteit](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    Entiteiten in één tabel zijn niet vereist toohave Hallo dezelfde eigenschappen (kolommen set). Houd er rekening mee Hallo volgen beperkingen voor het weergeven en bewerken van tabelgegevens.
   
   * U kunt weergeven of bewerken van binaire gegevens (type byte[]), maar u kunt het opslaan in een tabel.
   * Hallo kan niet worden bewerkt **PartitionKey** of **RowKey** waarden, omdat in Azure-tabelopslag biedt geen ondersteuning voor deze bewerking.
   * U kunt niet een eigenschap genaamd tijdstempel maken, Azure Storage-services gebruiken een eigenschap met die naam.
   * Als u een datum / tijdwaarde opgeeft, moet u een indeling die geschikt toohello regio en taal-instellingen van de computer volgen (bijvoorbeeld: DD-MM-jjjj: mm: ss [AM | PM] voor VS In het Engels).

### <a name="tooadd-entities"></a>tooadd entiteiten
1. In Hallo **tabelontwerp**, kies Hallo **entiteit toevoegen** knop.
   
    ![Entiteit toevoegen](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. In Hallo **entiteit toevoegen** dialoogvenster Voer Hallo waarden Hallo **PartitionKey** en **RowKey** eigenschappen.
   
    ![Dialoogvenster entiteit toevoegen](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    Voer Hallo waarden zorgvuldig omdat u ze niet wijzigen nadat u het Hallo-dialoogvenster hebt gesloten, tenzij u Hallo entiteit verwijderen en opnieuw toevoegen.

### <a name="toofilter-entities"></a>toofilter entiteiten
Hallo set entiteiten die worden weergegeven in een tabel als u Hallo opbouwfunctie voor query's gebruikt, kunt u aanpassen.

1. tooopen hello opbouwfunctie voor query's, opent u een tabel om weer te geven.
2. Klik op Hallo opbouwfunctie voor Query's om op de werkbalk Hallo tabel weergeven.
   
    Hallo **opbouwfunctie voor Query's** dialoogvenster wordt weergegeven. Hallo volgende afbeelding ziet u een query die wordt samengesteld in Hallo opbouwfunctie voor query's.
   
    ![Opbouwfunctie voor query 's](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. Wanneer u klaar bent Hallo query bouwen, Hallo dialoogvenster te sluiten. Hallo resulterende tekst hello query wordt weergegeven in het tekstvak als een filter WCF Data Services.
4. Hallo toorun query uitvoeren, kiest u Hallo groene driehoek.
   
    U kunt ook filteren entiteitsgegevens die wordt weergegeven in Hallo **tabelontwerp** als u een filtertekenreeks in WCF Data Services rechtstreeks in het filterveld Hallo invoert. Dit soort tekenreeks is vergelijkbaar tooa SQL WHERE-component maar toohello server als een HTTP-aanvraag is verzonden. Zie voor meer informatie over hoe de tekenreeksen voor het filteren van tooconstruct [construeren van tekenreeksen voor Hallo tabelontwerp](https://msdn.microsoft.com/library/azure/ff683669.aspx).
   
    Hallo toont volgende afbeelding een voorbeeld van een geldig filter-tekenreeks:
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a>Storage-gegevens vernieuwen
Als Server Explorer verbinding tooor haalt gegevens uit een opslagaccount maakt, kan het Hallo bewerking toocomplete tooa minuut duren. Als er geen verbinding maken, mogelijk Hallo bewerking time-out. Tijdens het ophalen van gegevens, kunt u blijven toowork in andere onderdelen van Visual Studio. toocancel hello bewerking als het duurt te lang, kies Hallo **vernieuwen annuleren** op de werkbalk van Hallo Server Explorer.

#### <a name="toorefresh-blob-container-data"></a>toorefresh blob-containergegevens
* Selecteer Hallo **Blobs** knooppunt onder **opslag** en kies Hallo **vernieuwen** op de werkbalk van Hallo Server Explorer.
* toorefresh hello lijst met blobs die wordt weergegeven, kies Hallo **Execute** knop.

#### <a name="toorefresh-table-data"></a>de tabelgegevens toorefresh
* Selecteer Hallo **tabellen** knooppunt onder **opslag** en kies Hallo **vernieuwen** knop.
* toorefresh hello lijst van de entiteiten die wordt weergegeven in Hallo **tabelontwerp**, kies Hallo **Execute** knop op Hallo **tabelontwerp**.

#### <a name="toorefresh-queue-data"></a>toorefresh wachtrijgegevens
* Selecteer Hallo **wachtrijen** knooppunt, en kies vervolgens Hallo **vernieuwen** knop.

#### <a name="toorefresh-all-items-in-a-storage-account"></a>alle items in een opslagaccount toorefresh
* Kies Hallo-accountnaam en kies vervolgens Hallo **vernieuwen** op de werkbalk Hallo voor Server Explorer.

### <a name="add-storage-accounts-by-using-server-explorer"></a>Storage-accounts toevoegen met behulp van Server Explorer
Er zijn twee manieren tooadd storage-accounts met behulp van de Server Explorer. U kunt een nieuw opslagaccount maken in uw Azure-abonnement of kunt u een bestaand opslagaccount koppelen.

#### <a name="toocreate-a-new-storage-account-by-using-server-explorer"></a>een nieuw opslagaccount met behulp van de Server Explorer toocreate
1. In Server Explorer open Hallo snelmenu voor Hallo Opslagknooppunt en kies vervolgens de Storage-Account maken.
   
    ![Een nieuw Azure storage-account maken](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. Selecteer of typ de volgende informatie voor het nieuwe opslagaccount in Hallo HALLO hallo **Storage-Account maken** in het dialoogvenster.
   
   * Hello Azure-abonnement toowhich gewenste tooadd Hallo storage-account.
   * Hallo naam toouse voor Hallo nieuw opslagaccount.
   * Hallo regio of affiniteitsgroep (zoals VS-West of Oost-Azië).
   * type Hallo van replicatie gewenste toouse voor Hallo storage-account, zoals geografisch redundante.
3. Kies **Maken**.
   
    Hallo nieuw opslagaccount wordt weergegeven in Hallo **opslag** lijst in Solution Explorer.

#### <a name="tooattach-an-existing-storage-account-by-using-server-explorer"></a>een bestaand opslagaccount met behulp van de Server Explorer tooattach
1. In Server Explorer open Hallo snelmenu voor hello Azure storage-knooppunt en kies vervolgens **externe opslag koppelen**.
   
    ![Een bestaand opslagaccount toevoegen](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. Selecteer of typ de volgende informatie voor het nieuwe opslagaccount in Hallo HALLO hallo **Storage-Account maken** in het dialoogvenster.
   
   * Hallo-naam van Hallo bestaand opslagaccount gewenste tooattach. U kunt een naam invoeren of selecteren in lijst Hallo.
   * Hallo-sleutel voor Hallo storage-account geselecteerd. Deze waarde wordt meestal verzorgd door voor u wanneer u een opslagaccount selecteren. Als u Visual Studio tooremember hello opslagaccountsleutel wilt, schakelt u Hallo onthouden account sleutel in.
   * Hallo protocol toouse tooconnect toohello storage-account, zoals HTTP, HTTPS of een aangepaste eindpunt. Zie [hoe tooConfigure verbinding tekenreeksen](https://msdn.microsoft.com/library/azure/ee758697.aspx) voor meer informatie over aangepaste eindpunten.

### <a name="tooview-hello-secondary-endpoints"></a>secundaire tooview Hallo-eindpunten
* Als u een opslagaccount met Hallo gemaakt **Read-Access Geo-Redundant** replicatieoptie, kunt u de secundaire eindpunten weergeven. Open Hallo snelmenu voor Hallo-accountnaam en kies vervolgens **eigenschappen**.
  
    ![Secundaire opslag-eindpunten](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="tooremove-a-storage-account-from-server-explorer"></a>een opslagaccount in Server Explorer tooremove
* Open Hallo snelmenu voor Hallo-accountnaam in Server Explorer, en kies vervolgens **verwijderen**. Als u een opslagaccount verwijdert, worden alle opgeslagen sleutelgegevens voor dat account wordt ook verwijderd.
  
  > [!NOTE]
  > Als u een opslagaccount in Server Explorer verwijdert, dat geen gevolgen voor uw opslagaccount of gegevens die deze bevat; alleen verwijderd Hallo verwijzing in Server Explorer. toopermanently een opslagaccount verwijderen, gebruikt u Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885).
  > 
  > 

## <a name="next-steps"></a>Volgende stappen
toolearn informatie over het gebruiken van Azure storage-services, Zie [toegang tot Azure-opslagservices Hallo](https://msdn.microsoft.com/library/azure/ee405490.aspx).

