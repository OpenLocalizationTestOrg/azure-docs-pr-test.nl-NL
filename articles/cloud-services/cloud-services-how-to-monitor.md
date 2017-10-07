---
title: aaaHow toomonitor een cloudservice | Microsoft Docs
description: Meer informatie over hoe toomonitor cloudservices met behulp van Hallo klassieke Azure-portal.
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: ee98c56e0b98b85d75a5c1d796800069c4f06d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-cloud-services"></a>Hoe tooMonitor Cloud-Services
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

U kunt bewaken `key` maatstaven voor prestaties voor uw cloudservices in Hallo klassieke Azure-portal. U kunt instellen Hallo niveau van de bewaking van toominimal en uitgebreide voor elke rol service en Hallo geeft bewaking kunt aanpassen. Uitgebreide controle gegevens worden opgeslagen in een opslagaccount dat u toegang hebt tot buiten Hallo-portal. 

Controle worden weergegeven in de klassieke Azure-portal Hallo zijn configureerbaar. U kunt metrische gegevens Hallo gewenste toomonitor in de lijst met de Hallo metrische gegevens op Hallo **Monitor** pagina, en kunt u welke tooplot metrische gegevens in de grafieken metrische gegevens op Hallo **Monitor** pagina en Hallo dashboard. 

## <a name="concepts"></a>Concepten
Standaard is minimale bewaking opgegeven voor een nieuwe cloudservice met behulp van prestatiemeteritems die afkomstig zijn van het hostbesturingssysteem Hallo voor Hallo rollen exemplaren (virtuele machines). Hallo minimale metrische gegevens zijn beperkt tooCPU Percentage, Data, gegevensuitvoer, doorvoercapaciteit van de schijf lezen en schrijven doorvoercapaciteit van de schijf. Uitgebreide bewaking configureert, kunt u aanvullende gegevens op basis van prestatiegegevens Hallo virtuele machines (rolexemplaren) ontvangen. Hallo uitgebreide metrische gegevens inschakelen dichter analyse van problemen die tijdens de bewerkingen van de toepassing optreden.

Standaard prestatiemeteritemgegevens van rolinstanties door actieve en van de rolinstantie Hallo overgedragen om de 3 minuten. Wanneer u uitgebreide bewaking inschakelt, wordt Hallo onbewerkte gegevens van prestatiemeteritems voor elk rolexemplaar en over rolexemplaren voor elke rol geaggregeerd met een interval van 5 minuten, 1 uur en 12 uur. Hallo worden verzamelde gegevens verwijderd na 10 dagen.

Nadat u hebt ingeschakeld verbose bewaking, Hallo geaggregeerd wordt bewakingsgegevens opgeslagen in de tabellen in uw opslagaccount. tooenable uitgebreide bewaking voor een rol, moet u een verbindingsreeks voor diagnostische gegevens die is gekoppeld aan toohello storage-account configureren. U kunt verschillende storage-accounts gebruiken voor andere rollen.

Inschakelen van uitgebreide bewaking toeneemt uw opslagkosten gerelateerd toodata storage, gegevensoverdracht en opslagtransacties. Minimale bewaking is niet vereist voor een opslagaccount. Hallo-gegevens voor Hallo metrische gegevens die beschikbaar worden gesteld op Hallo minimumniveau bewaking worden niet opgeslagen in uw opslagaccount, zelfs als u bewaking niveau tooverbose Hallo instelt.

## <a name="how-to-configure-monitoring-for-cloud-services"></a>Procedure: het bewaken configureren voor cloud-services
Gebruik Hallo procedures tooconfigure uitgebreide of minimale bewaken in de klassieke Azure-portal hello te volgen. 

### <a name="before-you-begin"></a>Voordat u begint
* Maak een *klassieke* storage account toostore Hallo bewakingsgegevens. U kunt verschillende storage-accounts gebruiken voor andere rollen. Zie voor meer informatie [hoe toocreate een opslagaccount](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Schakel diagnostische Azure-gegevens voor rollen van uw cloudservice. Zie [diagnostische gegevens configureren voor Cloudservices](cloud-services-dotnet-diagnostics.md).

Zorg ervoor dat Hallo diagnostics verbindingsreeks aanwezig is in de configuratie van de functie Hallo. U inschakelen uitgebreide bewaking totdat u Azure diagnostische gegevens inschakelen en een verbindingsreeks diagnostische gegevens in de rolconfiguratie Hallo opnemen niet.   

> [!NOTE]
> Projecten die gericht is op Azure SDK 2.5 bevat automatisch geen Hallo diagnostics verbindingsreeks in de projectsjabloon Hallo. Voor deze projecten, moet u toomanually Hallo diagnostics verbinding tekenreeks toohello rolconfiguratie toevoegen.
> 
> 

**toomanually diagnostics connection string tooRole configuratie toevoegen**

1. Open Hallo Cloud Services-project in Visual Studio
2. Dubbelklik op Hallo **rol** tooopen rol designer Hallo en selecteer Hallo **instellingen** tabblad
3. Zoek naar een instelling met de naam **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**. 
4. Als deze instelling niet aanwezig is is, klikt u op Hallo **instelling toevoegen** knop tooadd het toohello configuratie en wijzig Hallo type voor Hallo nieuwe instelling te**ConnectionString**
5. Hallo waarde instellen voor verbinding tekenreeks Hallo door te klikken op Hallo **...**  knop. Hiermee opent u een dialoogvenster waarin u tooselect een opslagaccount.
   
    ![Visual Studio-instellingen](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="toochange-hello-monitoring-level-tooverbose-or-minimal"></a>toochange hello niveau tooverbose bewaking of minimale
1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/)Open Hallo **configureren** pagina voor Hallo cloud service-implementatie.
2. In **niveau**, klikt u op **uitgebreid** of **minimale**. 
3. Klik op **Opslaan**.

Nadat u ingeschakeld verbose bewaking, moet u eerst Hallo voor het bewaken van gegevens in de klassieke Azure-portal Hallo binnen Hallo uur te zien.

Hallo onbewerkte gegevens van prestatiemeteritems en geaggregeerde bewakingsgegevens worden opgeslagen in de opslagaccount hello in tabellen gekwalificeerd door Hallo implementatie-ID voor Hallo rollen. 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a>Procedure: waarschuwingen voor cloud service metrische gegevens ontvangen
U kunt waarschuwingen op basis van de cloudservice bewaken metrische gegevens kunt ontvangen. Op Hallo **beheerservices** pagina van Hallo klassieke Azure-portal, kunt u een tootrigger regel een waarschuwing wanneer Hallo metrische gegevens die u kiest een waarde die u opgeeft bereikt. U kunt ook toohave e-mail verzonden wanneer Hallo waarschuwing wordt geactiveerd. Zie voor meer informatie [hoe: waarschuwingsmeldingen ontvangen en regels voor waarschuwingen beheren in Azure](http://go.microsoft.com/fwlink/?LinkId=309356).

## <a name="how-to-add-metrics-toohello-metrics-table"></a>Hoe: metrische gegevens toohello metrische gegevens tabel toevoegen
1. In Hallo [klassieke Azure-portal](http://manage.windowsazure.com/)Open Hallo **Monitor** pagina voor het Hallo-cloudservice.
   
    Hallo metrische gegevens tabel geeft standaard een subset van de beschikbare metrische gegevens Hallo weer. Hallo-afbeelding ziet u Hallo standaard uitgebreide metrische gegevens voor een cloudservice, die het prestatiemeteritem Geheugen\Beschikbare megabytes (MB) voor beperkte toohello, met gegevens geaggregeerd op Hallo rolniveau. Gebruik **toevoegen metrische gegevens** tooselect extra aggregaat- en toomonitor quotumwaarde op metrische gegevens in de klassieke Azure-portal Hallo.
   
    ![Uitgebreide weergave](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. tooadd metrische gegevens toohello metrische gegevens tabel:
   
   1. Klik op **toevoegen metrische gegevens** tooopen **kiezen metrische gegevens**, u hieronder kunt zien.
      
       de eerste beschikbare metriek Hallo is uitgevouwen tooshow opties die beschikbaar zijn. Voor elke metriek weergegeven Hallo optie geaggregeerde bewakingsgegevens voor alle functies. Bovendien kunt u afzonderlijke rollen toodisplay gegevens voor.
      
       ![Metrische gegevens toevoegen](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. tooselect metrische gegevens toodisplay
      
      * Klik op Hallo pijl-omlaag door Hallo metrische tooexpand Hallo controle-opties.
      * Selecteer Hallo selectievakje in voor elke bewaken optie die u wilt toodisplay.
        
        U kunt maximaal too50 metrische gegevens in de tabel van Hallo metrische gegevens weergeven.
        
        > [!TIP]
        > In uitgebreide bewaking bevatten Hallo metrische gegevens lijst tientallen metrische gegevens. toodisplay een scrollbar Beweeg de muisaanwijzer over de rechterkant Hallo van dialoogvenster Hallo. toofilter Hallo-lijst, klik op het zoekpictogram Hallo en voer tekst in het zoekvak hello, zoals hieronder wordt weergegeven.
        > 
        > 
        
        ![Toevoegen van metrische gegevens zoeken](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. Nadat u metrische gegevens te selecteren, klik op OK (vinkje).
   
    Hallo worden geselecteerde metrische gegevens toegevoegd toohello metrische gegevens tabel, zoals hieronder wordt weergegeven.
   
    ![monitor metrische gegevens](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. toodelete metric van Hallo metrische gegevens tabel, klikt u op Hallo metrische tooselect en klik vervolgens op **metriek verwijderen**. (Alleen zien **metriek verwijderen** wanneer er een geselecteerde waarde.)

### <a name="tooadd-custom-metrics-toohello-metrics-table"></a>tooadd aangepaste metrische gegevens toohello metrische gegevens tabel
Hallo **uitgebreid** niveau bewaking biedt u een lijst met standaard metrische gegevens die u kunt controleren op Hallo-portal. Bovendien toothese u kunt aangepaste metrische gegevens of bewaken prestatiemeteritems die zijn gedefinieerd door uw toepassing via Hallo-portal.

Hallo volgende stappen wordt ervan uitgegaan dat u hebt ingeschakeld **uitgebreid** niveau bewaking en uw toepassing toocollect en overdracht aangepaste prestatiemeteritems hebt geconfigureerd. 

toodisplay hello aangepaste prestatiemeters in Hallo portal moet u de configuratie van de tooupdate Hallo in af-besturingselement-container:

1. Hallo af-besturingselement-container blob in uw opslagaccount voor diagnostische gegevens openen. U kunt Visual Studio of een andere opslag explorer toodo dit.
   
    ![Visual Studio Server Explorer](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. Navigeer Hallo blobpad met Hallo patroon **RoleName/DeploymentId/RoleInstance** toofind Hallo configuratie voor uw rolexemplaar. 
   
    ![Visual Studio Opslagverkenner](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. Hallo-configuratiebestand voor de rolinstantie downloaden bij te werken tooinclude aangepaste prestatiemeteritems. Bijvoorbeeld toomonitor *schijf geschreven Bytes per seconde* voor Hallo *station C* Voeg de volgende Hallo onder **PerformanceCounters\Subscriptions** knooppunt
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. Sla Hallo wijzigingen en het uploaden van Hallo configuratie bestand back toohello dezelfde locatie wordt overschreven Hallo bestaand bestand in Hallo blob.
5. Wisselknop tooVerbose modus in hello Azure classic portal-configuratie. Als u in de uitgebreide modus al hebt u tootoggle toominimal en terug tooverbose.
6. Hallo aangepaste prestatiemeteritem is nu beschikbaar in Hallo **toevoegen metrische gegevens** in het dialoogvenster. 

## <a name="how-to-customize-hello-metrics-chart"></a>Hoe: Hallo metrische gegevens grafiek aanpassen
1. Selecteer in de tabel van de metrische gegevens Hallo, too6 metrische gegevens tooplot op Hallo metrische gegevens grafiek. een metriek tooselect klikt u op Hallo selectievakje aan de linkerkant. tooremove metric van Hallo metrische gegevens grafiek, schakel het selectievakje in Hallo metrische gegevens tabel.
   
    Als u metrische gegevens in de tabel van Hallo metrische gegevens selecteert, kan Hallo metrische gegevens toohello metrische gegevens grafiek worden toegevoegd. Op een beperkte weergave een **n meer** vervolgkeuzelijst metrische headers die niet, Hallo-weergave past bevat.
2. tooswitch tussen de weergave relatieve waarden (laatste waarde alleen voor elke metriek) en absolute waarden (Y-as weergegeven), selecteer relatieve of een absoluut Hallo boven aan het Hallo-grafiek.
   
    ![Relatief of absoluut](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. toochange hello tijd bereik Hallo metrische gegevens grafiek wordt weergegeven, selecteert u 1 uur, 24 uur of zeven dagen Hallo boven aan het Hallo-grafiek.
   
    ![Weergaveperiode van de monitor](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    Op Hallo dashboard metrische gegevens grafiek verschilt Hallo-methode voor het tekengebied metrische gegevens. Een standaardset metrische gegevens beschikbaar is en metrische gegevens worden toegevoegd of verwijderd door het selecteren van metrische Hallo-header.

### <a name="toocustomize-hello-metrics-chart-on-hello-dashboard"></a>diagram van toocustomize Hallo metrische gegevens op Hallo-dashboard
1. Open Hallo dashboard voor Hallo-cloudservice.
2. Toevoegen of verwijderen van metrische gegevens uit Hallo grafiek:
   
   * tooplot nieuwe Hallo metrische, selecteer het selectievakje voor de metriek Hallo in Hallo grafiek headers. Klik op een beperkte weergave Hallo pijl-omlaag door  ***n* veldnamenrij? metrische gegevens** tooplot een koptekst van metrische Hallo grafiekgebied kan niet worden weergegeven.
   * een waarde die wordt getekend op Hallo grafiek, selectievakje Hallo wissen door de header toodelete.
   
3. Schakelen tussen **relatieve** en **Absolute** wordt weergegeven.
4. 1 uur, 24 uur of zeven dagen aan gegevens toodisplay kiezen.

## <a name="how-to-access-verbose-monitoring-data-outside-hello-azure-classic-portal"></a>Procedure: toegang tot uitgebreide bewakingsgegevens buiten Hallo klassieke Azure-portal
Uitgebreide bewakingsgegevens wordt opgeslagen in de tabellen in Hallo storage-accounts die u voor elke rol opgeeft. Voor elke cloud service-implementatie worden de zes tabellen gemaakt voor Hallo-rol. Twee tabellen worden gemaakt voor elk (5 minuten, 1 uur en 12 uur). Een van deze tabellen slaat quotumwaarde op aggregaties; Hallo andere tabel winkels aggregaties voor rolinstanties. 

Hallo tabelnamen hebben Hallo volgende indeling:

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

Waarbij:

* *deploymentID* is Hallo GUID die is toegewezen toohello cloud service-implementatie
* *aggregation_interval* = 5 M, 1U of 12 uur
* niveau van de rol aggregaties = R
* aggregaties voor rolinstanties k =

Bijvoorbeeld: hello volgende tabellen opgeslagen uitgebreide bewakingsgegevens geaggregeerd interval van 1 uur:

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for hello role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
