---
title: toepassingspakketten aaaInstall op rekenknooppunten - Azure Batch | Microsoft Docs
description: Gebruik hello-pakketten toepassingsfunctie van Azure Batch tooeasily beheren meerdere toepassingen en versies voor de installatie van Batch-rekenknooppunten.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a>Implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten

Hallo toepassingsfunctie pakketten van Azure Batch maakt eenvoudig beheer van toepassingen van de taak en hun implementatie toohello rekenknooppunten in uw groep. U kunt met toepassingspakketten kunt uploaden en beheren van meerdere versies van de taken worden uitgevoerd, met inbegrip van hun ondersteunende bestanden Hallo-toepassingen. Vervolgens kunt u automatisch implementeren een of meer van deze toepassingen toohello rekenknooppunten in uw groep.

In dit artikel leert u hoe tooupload en toepassingspakketten in hello Azure-portal beheren. Vervolgens leert u hoe tooinstall ze op een groep rekenknooppunten met Hallo [Batch .NET] [ api_net] bibliotheek.

> [!NOTE]
> 
> Toepassingspakketten worden ondersteund in alle Batch-pools die na 5 juli 2017 zijn gemaakt. Ze worden ondersteund in de Batch-pools tussen 10 maart 2016 en 5 juli 2017 alleen gemaakt als Hallo-groep is gemaakt met behulp van de configuratie van een Service in de Cloud. Batch-pools gemaakt voorafgaande too10 maart 2016 bieden geen ondersteuning voor toepassingspakketten.
>
> Hallo-API's voor het maken en beheren van toepassingspakketten deel uitmaken van Hallo [Batch Management .NET] [[api_net_mgmt]] bibliotheek. Hallo-API's voor toepassingspakketten installeren op een rekenknooppunt deel uitmaken van Hallo [Batch .NET] [ api_net] bibliotheek.  
>
> hello-pakketten toepassingsfunctie hier beschreven vervangt Hallo Batch Apps-functie die beschikbaar zijn in eerdere versies van het Hallo-service.
> 
> 

## <a name="application-package-requirements"></a>Vereisten voor Application-pakket
toepassingspakketten toouse, moet u te[een Azure Storage-account koppelen](#link-a-storage-account) tooyour Batch-account.

Deze functie is geïntroduceerd [Batch REST-API] [ api_rest] versie 2015-12-01.2.2 en de bijbehorende van Hallo [Batch .NET] [ api_net] library-versie 3.1.0. Het is raadzaam de nieuwste API-versie Hallo altijd te gebruiken bij het werken met de Batch.

> [!NOTE]
> Toepassingspakketten worden ondersteund in alle Batch-pools die na 5 juli 2017 zijn gemaakt. Ze worden ondersteund in de Batch-pools tussen 10 maart 2016 en 5 juli 2017 alleen gemaakt als Hallo-groep is gemaakt met behulp van de configuratie van een Service in de Cloud. Batch-pools gemaakt voorafgaande too10 maart 2016 bieden geen ondersteuning voor toepassingspakketten.
>
>

## <a name="about-applications-and-application-packages"></a>Over de toepassingen en toepassingspakketten
In Azure Batch een *toepassing* tooa set samengestelde binaire bestanden die automatisch gedownloade toohello rekenknooppunten in uw pool worden kunnen verwijst. Een *toepassingspakket* verwijst tooa *specifieke set* van deze binaire bestanden en vertegenwoordigt een gegeven *versie* van Hallo-toepassing.

![Op hoog niveau diagram van toepassingen en toepassingspakketten][1]

### <a name="applications"></a>Toepassingen
Een toepassing in Batch bevat een of meer toepassingen, pakketten en configuratieopties voor de toepassing hello geeft. Een toepassing kan bijvoorbeeld Hallo standaard toepassing pakket versie tooinstall opgeven op de rekenknooppunten en of de pakketten kunnen worden bijgewerkt of verwijderd.

### <a name="application-packages"></a>Toepassingspakketten
Een toepassingspakket is een ZIP-bestand met Hallo toepassing binaire bestanden en ondersteunende bestanden die vereist voor uw taken toorun Hallo-toepassing zijn. Elke toepassingspakket vertegenwoordigt een specifieke versie van de toepassing hello.

U kunt toepassingspakketten op Hallo van toepassingen en taak niveaus opgeven. U kunt een of meer van deze pakketten en (optioneel) een versie opgeven wanneer u een groep of een taak maakt.

* **Toepassingspakketten groep** te worden geïmplementeerd*elke* knooppunt in de pool Hallo. Toepassingen worden geïmplementeerd als een knooppunt aan een pool wordt toegevoegd en wanneer deze wordt opgestart of hersteld met een installatiekopie.
  
    Toepassingspakketten voor toepassingen zijn geschikt wanneer alle knooppunten in een pool van een taak taken uitvoeren. Een of meer toepassingspakketten kunt u opgeven wanneer u een pool maakt en u kunt toevoegen of bijwerken van een bestaande pool-pakketten. Als u een bestaande pool toepassingspakketten bijwerkt, moet u de knooppunten tooinstall Hallo nieuw pakket opnieuw.
* **Taak toepassingspakketten** alleen tooa rekenknooppunt gepland toorun een taak, net voordat de opdrachtregel van Hallo taak uitgevoerd worden geïmplementeerd. Als Hallo opgegeven toepassingspakket en versie is al op Hallo knooppunt niet opnieuw gedistribueerd en Hallo bestaand pakket wordt gebruikt.
  
    Taak toepassingspakketten zijn handig in gedeelde groep omgevingen, waarbij verschillende taken worden uitgevoerd op één groep en het Hallo-groep is niet verwijderd wanneer een taak is voltooid. Als uw project minder taken dan knooppunten in de groep hello heeft, minimaliseren taak toepassingspakketten gegevensoverdracht sinds de toepassing is geïmplementeerd alleen toohello knooppunten die taken uitvoeren.
  
    Andere scenario's waarin u van de taak toepassingspakketten profiteren kunnen zijn taken met een grote toepassing, maar voor alleen enkele taken. Een vooraf verwerken fase of een merge-taak, waarbij de toepassing vooraf verwerken of samenvoegen Hallo zware is, kan bijvoorbeeld profiteren van het gebruik van de taak toepassingspakketten.

> [!IMPORTANT]
> Er gelden beperkingen op Hallo aantal toepassingen en toepassingspakketten in een Batch-account en op Hallo maximale pakketgrootte. Zie [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md) voor meer informatie over deze limieten.
> 
> 

### <a name="benefits-of-application-packages"></a>Voordelen van toepassingspakketten
Toepassingspakketten kunnen vereenvoudigen Hallo-code in uw Batch-oplossing en de lagere Hallo overhead vereist toomanage Hallo toepassingen die de taken worden uitgevoerd.

Met toepassingspakketten kunt uw pool begintaak beschikt niet over toospecify een lange lijst met afzonderlijke resource bestanden tooinstall op Hallo knooppunten. U hebt geen toomanually beheer van meerdere versies van uw toepassingsbestanden in Azure Storage of op de knooppunten. En u hoeft niet tooworry over het genereren van [SAS-URL's](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello-bestanden in uw opslagaccount. Batch-werkt op de achtergrond Hallo met Azure Storage toostore toepassingspakketten en deze toocompute knooppunten te implementeren.

> [!NOTE] 
> Hallo totale grootte van een begintaak moet kleiner zijn dan of gelijk too32768 tekens, inclusief bronbestanden en omgevingsvariabelen. Als uw begintaak deze limiet overschrijdt, is met behulp van toepassingspakketten een andere optie. U kunt ook een ZIP-archief met de resource-bestanden maken, uploaden als een tooAzure blob Storage en pak deze vervolgens vanaf de opdrachtregel Hallo van de begintaak. 
>
>

## <a name="upload-and-manage-applications"></a>Uploaden en beheren van toepassingen
U kunt Hallo [Azure-portal] [ portal] of Hallo [Batch Management .NET](batch-management-dotnet.md) bibliotheek toomanage Hallo-toepassingspakketten in uw Batch-account. In Hallo naast enkele secties, laten we eerst zien hoe toolink een opslagaccount worden besproken toe te voegen toepassingen en pakketten en het beheer ervan met Hallo portal.

### <a name="link-a-storage-account"></a>Storage-account koppelen
toepassingspakketten toouse, moet u eerst een Azure Storage-account tooyour Batch-account koppelen. Als u een opslagaccount nog niet hebt geconfigureerd, hello Azure-portal geeft een waarschuwing Hallo eerste keer dat u op Hallo **toepassingen** -tegel in Hallo **Batch-account** blade.

> [!IMPORTANT]
> Batch ondersteunt momenteel *alleen* hello **algemeen** opslagaccounttype zoals beschreven in stap 5, [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)in [over Azure Storage-accounts](../storage/common/storage-create-storage-account.md). Als u een Azure Storage-account tooyour Batch-account koppelt, koppelt *alleen* een **algemeen** storage-account.
> 
> 

!['Er is geen opslagaccount geconfigureerd' waarschuwing in Azure-portal][9]

Hallo gekoppelde Batch-service gebruikt Hallo Storage-account toostore uw toepassingspakketten. Nadat u hebt twee accounts Hallo gekoppeld, kunt Batch hello-pakketten die zijn opgeslagen in tooyour rekenknooppunten voor Hallo gekoppelde Storage-account automatisch implementeren. toolink een Storage account tooyour Batch-account, klikt u op **instellingen voor de opslag** op Hallo **waarschuwing** blade en klik vervolgens op **Opslagaccount** op Hallo **Opslagaccount** blade.

![Kies de blade opslagaccount in Azure-portal][10]

Het is raadzaam dat u een opslagaccount maken *specifiek* voor gebruik met uw Batch-account en selecteert u deze hier. Voor meer informatie over hoe u een opslagaccount toocreate Zie 'Een opslagaccount maken' in [over Azure Storage-accounts](../storage/common/storage-create-storage-account.md). Nadat u een opslagaccount hebt gemaakt, kunt u vervolgens deze koppelen tooyour Batch-account met behulp van Hallo **Opslagaccount** blade.

> [!WARNING]
> Hallo Batch-service gebruikt Azure Storage toostore uw toepassingspakketten als blok-blobs. U bent [in rekening gebracht als normale] [ storage_pricing] voor Hallo blok-blob-gegevens. Ervoor tooconsider Hallo grootte en het aantal van uw toepassingspakketten zijn en verwijderen periodiek verouderde pakketten toominimize kosten.
> 
> 

### <a name="view-current-applications"></a>De huidige toepassingen weergeven
tooview hello toepassingen in uw Batch-account, klikt u op Hallo **toepassingen** menu-item in het menu aan de linkerkant Hallo terwijl u bekijkt hello **Batch-account** blade.

![Toepassingen-tegel][2]

Met deze optie menu opent Hallo **toepassingen** blade:

![Lijst met toepassingen][3]

Hallo **toepassingen** blade geeft Hallo ID van elke toepassing in uw account en Hallo van de volgende eigenschappen:

* **Pakketten**: Hallo aantal versies die zijn gekoppeld aan deze toepassing.
* **Standaardversie**: Hallo toepassingsversie geïnstalleerd als u niet een versie aangeven wanneer u Hallo-toepassing voor een groep opgeeft. Deze instelling is optioneel.
* **Toestaan dat updates**: Hallo-waarde die aangeeft of het pakket updates, verwijderingen en toevoegingen zijn toegestaan. Als dit te is ingesteld**Nee**, pakket bijwerken en verwijderen voor de toepassing hello zijn uitgeschakeld. Alleen nieuwe toepassingspakketversies kunnen worden toegevoegd. Hallo standaardwaarde is **Ja**.

### <a name="view-application-details"></a>Toepassingdetails weergeven
tooopen hello blade met details voor een toepassing, selecteer Hallo-toepassing hello in Hallo **toepassingen** blade.

![App-details][4]

Hallo toepassing details blade kunt u de volgende instellingen voor uw toepassing hello configureren.

* **Toestaan dat updates**: opgeven of de toepassingspakketten kunnen worden bijgewerkt of verwijderd. Zie 'Werken of te verwijderen van een toepassingspakket' verderop in dit artikel.
* **Standaardversie**: een standaard application-pakket toodeploy toocompute-knooppunten opgeven.
* **Weergavenaam**: Geef een beschrijvende naam die uw oplossing kunt gebruiken bij deze geeft informatie weer over toepassing hello, bijvoorbeeld in de gebruikersinterface van een service die u opgeeft dat klanten via Batch tooyour Hallo Batch.

### <a name="add-a-new-application"></a>Een nieuwe toepassing toevoegen
toocreate een nieuwe toepassing toevoegen van een toepassingspakket en geef een nieuwe, unieke toepassing-ID. Hallo eerste toepassingspakket dat u met de nieuwe toepassings-ID Hallo toevoegen maakt ook een nieuwe toepassing hello.

Klik op **toevoegen** op Hallo **toepassingen** blade tooopen hello **nieuwe toepassing** blade.

![Blade voor een nieuwe toepassing in Azure-portal][5]

Hallo **nieuwe toepassing** blade biedt de volgende Hallo velden toospecify Hallo-instellingen van uw nieuwe toepassing en het application-pakket.

**Toepassings-id**

Dit veld bevat Hallo-ID van uw nieuwe toepassing, onderwerp toohello standaard Azure Batch-ID-validatieregels. Hallo-regels voor het ontwikkelen van een toepassings-ID zijn als volgt:

* Op Windows-knooppunten kan Hallo-ID een combinatie van alfanumerieke tekens, afbreekstreepjes en onderstrepingstekens bevatten. Op Linux-knooppunten mogen alleen alfanumerieke tekens en onderstrepingstekens bevatten.
* Kan niet meer dan 64 tekens bevatten.
* Moet uniek zijn binnen Hallo Batch-account.
* Letters behouden blijven en hoofdlettergevoelig is.

**Versie**

Dit veld geeft Hallo-versie van Hallo-toepassingspakket die wordt geüpload. Versietekenreeksen zijn onderwerp toohello validatieregels te volgen:

* Op Windows-knooppunten kan Hallo versietekenreeks een combinatie van alfanumerieke tekens, streepjes, onderstrepingstekens en punten bevatten. Op Linux-knooppunten mag Hallo versietekenreeks alleen alfanumerieke tekens en onderstrepingstekens bevatten.
* Kan niet meer dan 64 tekens bevatten.
* Moet uniek zijn binnen het Hallo-toepassing.
* Letters behouden blijven en hoofdlettergevoelig zijn.

**Application-pakket**

Dit veld geeft Hallo ZIP-bestand met binaire waarden Hallo van toepassingen en ondersteunende bestanden die vereist tooexecute Hallo-toepassing zijn. Klik op Hallo **selecteert u een bestand** box of Hallo map pictogram toobrowse tooand Selecteer een ZIP-bestand met de bestanden van uw toepassing.

Nadat u een bestand hebt geselecteerd, klikt u op **OK** toobegin Hallo uploaden tooAzure opslag. Wanneer Hallo uploaden voltooid is, wordt Hallo portal een melding weergegeven en wordt gesloten Hallo-blade. Deze bewerking kan enige tijd duren, afhankelijk van de grootte van de Hallo van Hallo-bestand dat u uploadt en Hallo snelheid van uw netwerkverbinding zijn.

> [!WARNING]
> Hallo niet sluiten **nieuwe toepassing** blade voordat Hallo uploaden voltooid is. In dat geval wordt het uploadproces Hallo gestopt.
> 
> 

### <a name="add-a-new-application-package"></a>Een nieuw toepassingspakket toevoegen
een nieuwe Pakketversie voor de toepassing van een bestaande toepassing tooadd een toepassing selecteren in Hallo **toepassingen** blade, klikt u op **pakketten**, klikt u vervolgens op **toevoegen** tooopen Hallo **toevoegen pakket** blade.

![Toepassing pakket blade toevoegen in Azure-portal][8]

Zoals u ziet, Hallo velden overeenkomen met de Hallo **nieuwe toepassing** blade, maar Hallo **toepassings-id** selectievakje is uitgeschakeld. Net als voor de nieuwe toepassing hello, geef Hallo **versie** bladeren voor het nieuwe pakket tooyour **toepassingspakket** ZIP-bestand en klik vervolgens op **OK** tooupload Hallo het pakket.

### <a name="update-or-delete-an-application-package"></a>Bijwerken of verwijderen van een toepassingspakket
tooupdate of verwijder een bestaande toepassingspakket, open Hallo details blade voor de toepassing hello, klikt u op **pakketten** tooopen hello **pakketten** blade, klikt u op Hallo **weglatingsteken**in de rij Hallo van Hallo toepassingspakket dat u toomodify wilt en Hallo-actie die u tooperform wilt selecteren.

![Bijwerken of verwijderen van pakket in Azure-portal][7]

**Update**

Wanneer u klikt op **Update**, Hallo *updatepakket* blade wordt weergegeven. Deze blade is vergelijkbaar toohello *nieuw toepassingspakket* blade echter alleen Hallo pakket selectie-veld is ingeschakeld, zodat u een nieuwe ZIP-bestand tooupload toospecify.

![Blade voor update-pakket in Azure-portal][11]

**Verwijderen**

Wanneer u klikt op **verwijderen**tooconfirm Hallo verwijdering van de Pakketversie hello wordt u gevraagd en Batch Hallo pakket verwijderd uit Azure Storage. Als u de standaardversie Hallo van een toepassing verwijdert, Hallo **standaardversie** instelling voor de toepassing hello is verwijderd.

![Toepassing verwijderen][12]

## <a name="install-applications-on-compute-nodes"></a>Toepassingen installeren op rekenknooppunten
Nu dat u hebt geleerd hoe toomanage toepassingspakketten Hello Azure-portal, bespreken we hoe toodeploy ze toocompute knooppunten en ze worden uitgevoerd met de Batch-taken.

### <a name="install-pool-application-packages"></a>Toepassingspakketten voor toepassingen installeren
tooinstall een toepassingspakket op alle rekenknooppunten in een pool, geeft u een of meer toepassingspakket *verwijzingen* voor Hallo van toepassingen. Hallo-toepassingspakketten die u voor een groep van toepassingen opgeeft zijn geïnstalleerd op elk rekenknooppunt wanneer dat knooppunt aan Hallo-pool wordt toegevoegd en wanneer het Hallo-knooppunt wordt opnieuw opgestart of hersteld met een installatiekopie.

Geef een of meer in Batch .NET [CloudPool][net_cloudpool].[ ApplicationPackageReferences] [ net_cloudpool_pkgref] wanneer u een nieuwe groep maakt of voor een bestaande toepassingen. Hallo [ApplicationPackageReference] [ net_pkgref] klasse geeft een toepassings-ID en versie tooinstall op een pool van rekenknooppunten.

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> Als de implementatie van een toepassing pakket om welke reden dan ook mislukt, Hallo Batch-service aanhalingstekens knooppunt Hallo [onbruikbaar][net_nodestate], en er zijn geen taken zijn gepland voor uitvoering op dat knooppunt. In dit geval moet u **opnieuw** Hallo knooppunt tooreinitiate Hallo pakketimplementatie. Opnieuw te starten Hallo knooppunt kan ook taakplanning opnieuw op Hallo-knooppunt.
> 
> 

### <a name="install-task-application-packages"></a>Taak toepassingspakketten installeren
Vergelijkbare tooa groep, geef toepassingspakket *verwijzingen* voor een taak. Wanneer een taak geplande toorun op een knooppunt is, wordt Hallo pakket gedownload en uitgepakt vlak voordat de opdrachtregel van Hallo taak wordt uitgevoerd. Als u een specifiek pakket en de versie is al geïnstalleerd op Hallo-knooppunt, Hallo pakket wordt niet gedownload en Hallo bestaand pakket wordt gebruikt.

een toepassingspakket taak tooinstall configureren van de taak Hallo [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] eigenschap:

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a>Hallo geïnstalleerd toepassingen uitvoeren
hello-pakketten die u hebt opgegeven voor een groep of de taak zijn gedownload en uitgepakt tooa met de naam map binnen Hallo `AZ_BATCH_ROOT_DIR` van Hallo-knooppunt. Batch maakt ook een omgevingsvariabele die Hallo pad toohello map met de naam bevat. Uw taak opdrachtregels gebruikt deze omgevingsvariabele bij verwijzingen naar de toepassing hello op Hallo-knooppunt. 

Op Windows-knooppunten heeft Hallo variabele Hallo volgende indeling:

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

Op Linux-knooppunten is Hallo indeling enigszins anders. Punten (.), afbreekstreepjes (-) en hekjes (#) zijn platte toounderscores in Hallo-omgevingsvariabele. Bijvoorbeeld:

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

`APPLICATIONID`en `version` zijn waarden die overeenkomen met toohello toepassing en het Pakketversie u hebt opgegeven voor de implementatie. Bijvoorbeeld, als u die versie 2.7 van toepassing opgegeven *blender* moet worden geïnstalleerd op Windows-knooppunten, uw taak opdrachtregels gebruikt deze omgeving variabele tooaccess de bestanden:

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

Geef op Linux-knooppunten Hallo omgevingsvariabele in deze indeling:

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

Wanneer u toepassingspakketten uploadt, geeft u een standaard versie toodeploy tooyour rekenknooppunten. Als u een standaardversie voor een toepassing hebt opgegeven, kunt u Hallo versieachtervoegsel weglaten wanneer u verwijst naar de toepassing hello. Kunt u de standaardversie toepassing hello opgeven in hello Azure-portal op de blade Hallo toepassingen, zoals wordt weergegeven in [uploaden en beheren van toepassingen](#upload-and-manage-applications).

Als u '2.7' ingesteld als de standaardversie Hallo voor toepassing bijvoorbeeld *blender*, en uw taken verwijzen naar Hallo volgende omgevingsvariabele, en vervolgens uw Windows-knooppunten versie 2.7 wordt uitgevoerd:

`AZ_BATCH_APP_PACKAGE_BLENDER`

Hallo volgende codefragment toont een voorbeeld van de taak vanaf de opdrachtregel waarmee wordt gestart Hallo standaardversie van Hallo *blender* toepassing:

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> Zie [omgevingsinstellingen voor taken](batch-api-basics.md#environment-settings-for-tasks) in Hallo [overzicht Batch-functies](batch-api-basics.md) voor meer informatie over omgevingsinstellingen compute-knooppunt.
> 
> 

## <a name="update-a-pools-application-packages"></a>De toepassingspakketten van een groep bijwerken
Als een bestaande pool al is geconfigureerd met een pakket, kunt u een nieuw pakket voor Hallo van toepassingen opgeven. Als u een nieuw pakket verwijzing voor een groep opgeeft, wordt de volgende Hallo toepassen:

* Hallo Batch-service installeert Hallo zojuist opgegeven pakket op alle nieuwe knooppunten die Hallo adresgroep toevoegen en op een bestaande knooppunt dat is opnieuw opgestart of hersteld met een installatiekopie.
* COMPUTE knooppunten die al in de groep Hallo tijdens het bijwerken van Hallo pakket met verwijzingen niet automatisch nieuwe toepassingspakket Hallo geïnstalleerd. Deze berekenen knooppunten moeten opnieuw worden opgestart of hersteld met een installatiekopie tooreceive Hallo nieuw pakket.
* Wanneer een nieuw pakket wordt geïmplementeerd, weerspiegelen Hallo omgevingsvariabelen gemaakt Hallo nieuwe toepassing pakket verwijzingen.

In dit voorbeeld heeft Hallo bestaande toepassingen versie 2.7 Hallo *blender* toepassing geconfigureerd als een van de [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref]. tooupdate hello groep knooppunten met versie 2.76b, Geef een nieuwe [ApplicationPackageReference] [ net_pkgref] met de nieuwe versie Hallo en doorvoeren Hallo wijzigen.

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

Nu dat hello nieuwe versie is geconfigureerd, Hallo Batch-service wordt geïnstalleerd versie 2.76b tooany *nieuwe* knooppunt dat aan Hallo-pool wordt toegevoegd. tooinstall 2.76b op Hallo knooppunten die zijn *al* in de groep hello, opnieuw opstarten of deze installatiekopie. Houd er rekening mee dat opnieuw opgestart knooppunten Hallo-bestanden van eerdere implementaties van het pakket behouden.

## <a name="list-hello-applications-in-a-batch-account"></a>Lijst Hallo toepassingen in een Batch-account
U kunt Hallo toepassingen en hun pakketten in een Batch-account weergeven met behulp van Hallo [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] methode.

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a>Inpakken
Met toepassingspakketten kunt u uw klanten Hallo-toepassingen voor hun werk selecteert en Hallo exacte versie toouse opgeven bij het verwerken van taken met de service Batch is ingeschakeld. U kunt ook Hallo mogelijkheid bieden voor uw klanten tooupload en hun eigen toepassingen in uw service bijhouden.

## <a name="next-steps"></a>Volgende stappen
* Hallo [Batch REST-API] [ api_rest] biedt ook ondersteuning toowork toepassingspakketten. Zie bijvoorbeeld Hallo [applicationPackageReferences] [ rest_add_pool_with_packages] -element in [toevoegen van een account voor toepassingsgroep tooan] [ rest_add_pool] voor informatie over het toospecify tooinstall met behulp van REST-API hello-pakketten. Zie [toepassingen] [ rest_applications] voor meer informatie over hoe de toepassingsinformatie tooobtain met behulp van Batch REST-API Hallo.
* Meer informatie over hoe tooprogrammatically [beheren van Azure Batch-accounts en quota's met Batch Management .NET](batch-management-dotnet.md). Hallo [Batch Management .NET][api_net_mgmt] bibliotheek account maken en verwijderen-functies voor uw Batch-toepassing of service kunt inschakelen.

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Toepassingspakketten op hoog niveau diagram"
[2]: ./media/batch-application-packages/app_pkg_02.png "De tegel toepassingen in Azure-portal"
[3]: ./media/batch-application-packages/app_pkg_03.png "Blade toepassingen in Azure-portal"
[4]: ./media/batch-application-packages/app_pkg_04.png "Toepassing details blade in Azure-portal"
[5]: ./media/batch-application-packages/app_pkg_05.png "Blade voor een nieuwe toepassing in Azure-portal"
[7]: ./media/batch-application-packages/app_pkg_07.png "Bijwerken of verwijderen van pakketten vervolgkeuzelijst in Azure-portal"
[8]: ./media/batch-application-packages/app_pkg_08.png "Nieuwe toepassing pakket blade in Azure-portal"
[9]: ./media/batch-application-packages/app_pkg_09.png "Er is geen gekoppelde Opslagwaarschuwing voor account"
[10]: ./media/batch-application-packages/app_pkg_10.png "Kies de blade opslagaccount in Azure-portal"
[11]: ./media/batch-application-packages/app_pkg_11.png "Blade voor update-pakket in Azure-portal"
[12]: ./media/batch-application-packages/app_pkg_12.png "Dialoogvenster voor bevestiging pakket maken in Azure-portal verwijderen"
