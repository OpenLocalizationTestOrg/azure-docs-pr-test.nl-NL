---
title: aaaTroubleshooting Azure Storage met diagnostische gegevens & Message Analyzer | Microsoft Docs
description: Een zelfstudie voor end-to-end oplossen met Azure Storage Analytics, AzCopy en Microsoft Message Analyzer te demonstreren
services: storage
documentationcenter: dotnet
author: robinsh
manager: timlt
ms.assetid: 643372a3-1c07-4e88-b4ef-042512a43086
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/15/2017
ms.author: robinsh
ms.openlocfilehash: f0b7886911c35de1fdc0bcbe6f83c220ddb38cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="end-to-end-troubleshooting-using-azure-storage-metrics-and-logging-azcopy-and-message-analyzer"></a>End-to-End-problemen oplossen met behulp van Azure Storage metrische gegevens en logboekregistratie, AzCopy en Message Analyzer
[!INCLUDE [storage-selector-portal-e2e-troubleshooting](../../includes/storage-selector-portal-e2e-troubleshooting.md)]

Is een belangrijke kwalificatie voor bouwen en de client-toepassingen met Microsoft Azure Storage ondersteunende opsporen en oplossen. Vervaldatum toohello gedistribueerde aard van een Azure-toepassing, opsporen en oplossen van fouten en prestatieproblemen mogelijk complexer dan in traditionele omgevingen.

In deze zelfstudie ziet u hoe tooidentify bepaalde fouten die mogelijk van invloed op prestaties en los deze fouten op end-to-end met de hulpprogramma's die worden geleverd door Microsoft en Azure Storage, in volgorde toooptimize Hallo-clienttoepassing.

Deze zelfstudie biedt een praktische exploratie van een end-to-end voor probleemoplossing scenario. Zie voor een gedetailleerde conceptuele handleiding tootroubleshooting Azure storage-toepassingen [Monitor, vaststellen en oplossen van Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="tools-for-troubleshooting-azure-storage-applications"></a>Hulpprogramma's voor probleemoplossing van Azure Storage-toepassingen
tootroubleshoot clienttoepassingen met behulp van Microsoft Azure Storage, kunt u een combinatie van hulpprogramma's voor toodetermine als er een probleem is opgetreden en welke oorzaak Hallo van Hallo probleem kan zijn. Tot deze hulpmiddelen behoren onder meer:

* **Azure Storage Analytics**. [Azure Storage Analytics](/rest/api/storageservices/Storage-Analytics) metrische gegevens en logboekregistratie voor Azure Storage biedt.
  
  * **Metrische gegevens Storage** houdt transactie metrische gegevens en capaciteitsmetrieken voor uw opslagaccount. Met metrische gegevens, kunt u bepalen hoe uw toepassing volgens tooa verscheidenheid aan andere maatregelen presteert. Zie [Storage Analytics metrische gegevens tabelschema](/rest/api/storageservices/Storage-Analytics-Metrics-Table-Schema) voor meer informatie over metrische gegevens die worden bijgehouden door Storage Analytics Hallo typen.
  * **Opslag logboekregistratie** elk logboek met aanvragen toohello Azure Storage-services tooa serverzijde registreert. Hallo logboek houdt gedetailleerde gegevens voor elke aanvraag, waaronder Hallo bewerking uitgevoerd, Hallo status Hallo-werking en latentie informatie. Zie [Storage Analytics logboekindeling](/rest/api/storageservices/Storage-Analytics-Log-Format) voor meer informatie over Hallo aanvraag- en gegevens die toohello Logboeken door Storage Analytics worden geschreven.

> [!NOTE]
> Storage-accounts met een replicatietype van de Zone-redundante opslag (ZRS) hebben geen Hallo metrische gegevens of logboekregistratie kunnen op dit moment is ingeschakeld. 
> 
> 

* **Azure-portal**. U kunt metrische gegevens en logboekregistratie configureren voor uw opslagaccount in Hallo [Azure-portal](https://portal.azure.com). U kunt ook grafieken en diagrammen die laten zien hoe uw toepassing wordt uitgevoerd na verloop van tijd weergeven en configureren van waarschuwingen toonotify die u als uw toepassing wordt uitgevoerd anders dan voor een opgegeven waarde verwacht.
  
    Zie [een opslagaccount in hello Azure-portal bewaken](storage-monitor-storage-account.md) voor informatie over het configureren van de bewaking in hello Azure-portal.
* **AzCopy**. Server-logboeken voor Azure Storage worden opgeslagen als blobs, zodat u kunt AzCopy toocopy Hallo blobs tooa lokale logboekmap voor analyse met behulp van Microsoft Message Analyzer gebruiken. Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md) voor meer informatie over AzCopy.
* **Microsoft Message Analyzer**. Berichtanalyse is een hulpprogramma dat logboekbestanden verbruikt en logboekgegevens in een visuele indeling die het maakt eenvoudig toofilter, zoeken en meld u aan gegevens bij nuttig sets die u tooanalyze fouten en prestatieproblemen gebruiken kunt groep weergegeven. Zie [Microsoft Message Analyzer besturingssysteem Guide](http://technet.microsoft.com/library/jj649776.aspx) voor meer informatie over Message Analyzer.

## <a name="about-hello-sample-scenario"></a>Over Hallo voorbeeldscenario
Voor deze zelfstudie kijken we naar de een scenario waarbij Azure Storage metrische gegevens staat voor een laag percentage slagingspercentage voor een toepassing die Azure storage aanroept. lage percentage geslaagd snelheid metriek Hallo (weergegeven als **PercentSuccess** in Hallo [Azure-portal](https://portal.azure.com) en in Hallo metrische gegevens tabellen) houdt bewerkingen die slagen, maar die een HTTP-statuscode die groter is geretourneerd dan 299. In logboekbestanden Hallo serverzijde opslag, deze bewerkingen worden geregistreerd met een transactiestatus **ClientOtherErrors**. Zie voor meer informatie over Hallo lage percentage geslaagd metriek [metrische gegevens tonen lage PercentSuccess of analytics logboekvermeldingen bewerkingen hebben met de status van ClientOtherErrors](storage-monitoring-diagnosing-troubleshooting.md#metrics-show-low-percent-success).

Azure Storage-bewerkingen kunnen retourneren HTTP-statuscodes groter is dan 299 als onderdeel van hun normale functionaliteit. Maar deze fouten in sommige gevallen aangeven dat u mogelijk kunnen toooptimize uw clienttoepassing voor verbeterde prestaties.

In dit scenario we hebt kunt u een laag percentage geslaagd snelheid toobe iets minder dan 100%. U kunt een andere metrische niveau echter volgens tooyour behoeften. We raden aan dat tijdens het testen van uw toepassing, u een tolerantie basislijn voor uw belangrijkste prestatiemetrieken maakt. Bijvoorbeeld, u kunt bepalen, op basis van testen, dat uw toepassing een consistente percentage slagingspercentage van 90% of 85% moet hebben. Als u uw gegevens metrische gegevens ziet dat de toepassing hello die is afwijken van dit nummer, kunt u vervolgens onderzoeken wat kan worden veroorzaakt door Hallo toename.

In ons scenario voorbeeld wanneer we hebt ingesteld dat Hallo percentage geslaagd snelheid metriek lager is dan 100%, we Hallo logboeken toofind Hallo fouten die toohello metrische gegevens samenhangen controleren en ze gebruiken toofigure wat wordt veroorzaakt door Hallo lagere percentage slagingspercentage voor. Zullen we specifiek fouten in Hallo 400 bereik. Vervolgens je we beter foutmeldingen 404 (niet gevonden).

### <a name="some-causes-of-400-range-errors"></a>Enkele oorzaken van fouten 400-bereik
Hallo voorbeelden hieronder ziet u een voorbeeld van een aantal fouten 400-bereik voor aanvragen op basis van Azure Blob Storage en hun mogelijke oorzaken. Een van deze fouten, evenals de fouten in Hallo 300 bereik en Hallo 500 bereik, kan tooa lage percentage slagingspercentage bijdragen.

Let op Hallo lijsten hieronder staan verre voltooid. Zie [Status en foutcodes](http://msdn.microsoft.com/library/azure/dd179382.aspx) op MSDN voor meer informatie over Azure Storage met algemene fouten en specifieke tooeach van opslagservices Hallo fouten.

**Voorbeelden van status Code 404 (niet gevonden)**

Deze gebeurtenis treedt op wanneer een leesbewerking op basis van een container of blob is mislukt omdat Hallo blob of de container is niet gevonden.

* Deze gebeurtenis treedt op als een container of blob is verwijderd door een andere client voordat deze aanvraag.
* Deze gebeurtenis treedt op als u een API-aanroep die Hallo-container of blob maakt nadat u hebt gecontroleerd of deze bestaat. Hallo CreateIfNotExists APIs een eerste toocheck-aanroep voor Hallo bestaan van het Hallo-container of blob; HEAD maken Als deze niet bestaat nog, een 404-fout is geretourneerd en vervolgens een tweede PUT-aanroep toowrite Hallo container of blob is uitgevoerd.

**Status 409 (Conflict) codevoorbeelden**

* Deze gebeurtenis treedt op als u een API maken toocreate een nieuwe container of blob, zonder eerst aanwezigheid controleren, en een container of blob met die naam al bestaat.
* Deze gebeurtenis treedt op als een container wordt verwijderd en u een nieuwe container met dezelfde naam probeert voordat Hallo verwijderingsbewerking voltooid is Hallo toocreate.
* Deze gebeurtenis treedt op als u een lease op een container of blob opgeven en er al een lease aanwezig is.

**Statuscode 412 (voorwaarde is mislukt) voorbeelden**

* Treedt op wanneer Hallo voorwaarde die is opgegeven door een voorwaardelijke kop niet is voldaan.
* Treedt op wanneer Hallo opgegeven lease-ID komt niet overeen met de Hallo lease-ID op Hallo-container of blob.

## <a name="generate-log-files-for-analysis"></a>Logboekbestanden voor analyse te genereren
In deze zelfstudie kun je Message Analyzer toowork met drie verschillende typen van logbestanden, hoewel u toowork met een van deze kan kiezen:

* Hallo **serverlogboek**, die wordt gemaakt wanneer u Azure Storage-logboekregistratie inschakelt. Hallo serverlogboek bevat gegevens over elke bewerking aangeroepen voor een hello Azure Storage-services - blob, queue, table en bestand. logboek Hallo-server geeft aan welke bewerking is aangeroepen en welke statuscode geretourneerd, evenals andere informatie over het Hallo-aanvraag en -antwoord is.
* Hallo **.NET clientlogboek**, die wordt gemaakt wanneer u logboekregistratie van client-side in uw .NET-toepassing inschakelen. Hallo clientlogboek bevat gedetailleerde informatie over hoe client Hallo Hallo-aanvraag wordt voorbereid en ontvangt en Hallo antwoord verwerkt.
* Hallo **HTTP netwerk traceerlogboek**, verzamelt gegevens op HTTP/HTTPS-aanvraag en antwoord gegevens, inclusief voor bewerkingen op Azure Storage. In deze zelfstudie gaat er Hallo netwerktracering via Message Analyzer gegenereerd.

### <a name="configure-server-side-logging-and-metrics"></a>Logboekregistratie op de server en metrische gegevens configureren
Eerst moet u logboekregistratie van Azure Storage tooconfigure en metrische gegevens, zodat we gegevens uit Hallo client toepassing tooanalyze hebben. U kunt logboekregistratie en metrische gegevens configureren in tal van manieren - via Hallo [Azure-portal](https://portal.azure.com), met behulp van PowerShell, of via een programma. Zie [metrische gegevens Storage inschakelen en weergeven van metrische gegevens](http://msdn.microsoft.com/library/azure/dn782843.aspx) en [opslag vastleggen inschakelen en toegang tot logboekgegevens](http://msdn.microsoft.com/library/azure/dn782840.aspx) op MSDN voor meer informatie over het configureren van logboekregistratie en metrische gegevens.

**Via hello Azure-portal**

tooconfigure logboekregistratie en metrische gegevens voor uw storage-account met Hallo [Azure-portal](https://portal.azure.com), volg de instructies Hallo voor [een opslagaccount in hello Azure-portal bewaken](storage-monitor-storage-account.md).

> [!NOTE]
> Het is niet mogelijk tooset minuut metrieken met hello Azure-portal. We raden echter aan dat u ze stelt voor Hallo doel van deze zelfstudie, en voor het onderzoeken van prestatieproblemen met uw toepassing. U kunt de minuut metrische gegevens met behulp van PowerShell, zoals hieronder wordt weergegeven of programmatisch met behulp van de storage-clientbibliotheek Hallo instellen.
> 
> Houd er rekening mee dat hello Azure-portal minuut metrische gegevens en alleen per uur metrische gegevens kan niet worden weergegeven.
> 
> 

**Via PowerShell**

tooget gestart met PowerShell voor Azure, Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

1. Gebruik Hallo [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0) cmdlet tooadd uw Azure gebruikersaccount toohello PowerShell-venster:
   
    ```powershell
    Add-AzureAccount
    ```

2. In Hallo **tooMicrosoft Azure aanmelden** venster, type Hallo e-mailadres en wachtwoord die zijn gekoppeld aan uw account. Azure verifieert Hallo referentie-informatie wordt opgeslagen en vervolgens Hallo-venster wordt gesloten.
3. Hallo standaard storage account toohello opslagaccount die u voor het Hallo-zelfstudie gebruikt door het uitvoeren van deze opdrachten in de PowerShell-venster Hallo instellen:
   
    ```powershell
    $SubscriptionName = 'Your subscription name'
    $StorageAccountName = 'yourstorageaccount'
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

4. Opslag-registratie voor Hallo Blob-service inschakelen:
   
    ```powershell
    Set-AzureStorageServiceLoggingProperty -ServiceType Blob -LoggingOperations Read,Write,Delete -PassThru -RetentionDays 7 -Version 1.0
    ```

5. Opslag metrische gegevens voor Blob-service, waardoor ervoor tooset Hallo inschakelen **- MetricsType** te`Minute`:
   
    ```powershell
    Set-AzureStorageServiceMetricsProperty -ServiceType Blob -MetricsType Minute -MetricsLevel ServiceAndApi -PassThru -RetentionDays 7 -Version 1.0
    ```

### <a name="configure-net-client-side-logging"></a>.NET-clientzijde logboekregistratie configureren
tooconfigure client-side '-registratie voor een .NET-toepassing inschakelen .NET diagnostische gegevens in het configuratiebestand van de toepassing hello (web.config of app.config). Zie [clientzijde logboekregistratie Hello Storage-clientbibliotheek voor .NET](http://msdn.microsoft.com/library/azure/dn782839.aspx) en [clientzijde logboekregistratie met Microsoft Azure-opslag-SDK voor Java Hallo](http://msdn.microsoft.com/library/azure/dn782844.aspx) op MSDN voor meer informatie.

Hallo-clientzijde logboek bevat gedetailleerde informatie over hoe client Hallo Hallo-aanvraag wordt voorbereid en ontvangt en Hallo antwoord verwerkt.

Hallo Storage-clientbibliotheek slaat clientzijde logboekgegevens in Hallo locatie die is opgegeven in het configuratiebestand van de toepassing hello (web.config of app.config).

### <a name="collect-a-network-trace"></a>Een nieuwe netwerktracering verzamelen
U kunt Message Analyzer toocollect een netwerktracering HTTP/HTTPS gebruiken terwijl u de clienttoepassing wordt uitgevoerd. Message Analyzer gebruikt [Fiddler](http://www.telerik.com/fiddler) op Hallo back-end. Voordat u een netwerktracering Hallo verzamelt, raden we aan dat u Fiddler toorecord ongecodeerd HTTPS-verkeer configureert:

1. Installeer [Fiddler](http://www.telerik.com/download/fiddler).
2. Start Fiddler.
3. Selecteer **extra | Opties voor fiddler**.
4. Zorg ervoor dat in het dialoogvenster Opties voor hello, **HTTPS-Maak verbinding vastleggen** en **HTTPS-verkeer ontsleutelen** beide zijn geselecteerd, zoals hieronder wordt weergegeven.

![Fiddler opties configureren](./media/storage-e2e-troubleshooting/fiddler-options-1.png)

Hallo-zelfstudie verzamelen en een netwerktracering eerst opslaan in Message Analyzer en vervolgens een analyse tooanalyze Hallo sessietracering maken en Hallo Logboeken. een nieuwe netwerktracering in Message Analyzer toocollect:

1. Selecteer in Message Analyzer **bestand | Snelle Trace | Niet-versleuteld HTTPS**.
2. Hallo tracering begint onmiddellijk. Selecteer **stoppen** toostop Hallo trace zodat we alleen tootrace opslagverkeer kunt configureren.
3. Selecteer **bewerken** tooedit Hallo traceringssessie.
4. Selecteer Hallo **configureren** toohello rechts van Hallo koppelen **Microsoft-Pef-WebProxy** ETW-provider.
5. In Hallo **geavanceerde instellingen** dialoogvenster, klikt u op Hallo **Provider** tabblad.
6. In Hallo **Hostname Filter** veld, geeft u de eindpunten van uw opslag, gescheiden door spaties. Bijvoorbeeld, kunt u uw eindpunten als volgt; Wijzig `storagesample` toohello-naam van uw opslagaccount:

    ```   
    storagesample.blob.core.windows.net storagesample.queue.core.windows.net storagesample.table.core.windows.net
    ```

7. Hallo dialoogvenster sluiten en klik op **opnieuw** toobegin Hallo trace verzamelen met Hallo hostnaam filter aanwezig is, zodat alleen Azure Storage-netwerkverkeer wordt opgenomen in Hallo tracering.

> [!NOTE]
> Nadat u klaar bent met het verzamelen van uw netwerk-trace, wordt aangeraden dat u terugzet Hallo-instellingen die u hebt gewijzigd in Fiddler toodecrypt HTTPS-verkeer. In het dialoogvenster van de opties voor Fiddler hello, deselecteren Hallo **vastleggen HTTPS Maak verbinding** en **HTTPS-verkeer ontsleutelen** selectievakjes.
> 
> 

Zie [Hallo tracering netwerkfuncties met](http://technet.microsoft.com/library/jj674819.aspx) op Technet voor meer informatie.

## <a name="review-metrics-data-in-hello-azure-portal"></a>Metrische gegevens controleren in hello Azure-portal
Zodra uw toepassing actief is geweest gedurende een periode, kunt u lezen Hallo metrische gegevens grafieken die worden weergegeven in Hallo [Azure-portal](https://portal.azure.com) tooobserve hoe uw service heeft is uitvoert.

Ga eerst tooyour storage-account in hello Azure-portal. Standaard een controle grafiek met Hallo **Verwerkingsfrequentie** metriek wordt weergegeven op de blade Hallo-account. Als u eerder Hallo grafiek toodisplay andere metrische gegevens hebt gewijzigd, voegt u Hallo **Verwerkingsfrequentie** metriek.

U ziet nu **Verwerkingsfrequentie** in Hallo grafiek bewaking, samen met andere metrische gegevens u hebt toegevoegd. In scenario Hallo die we naast onderzoeken door te analyseren Hallo Logboeken in Message Analyzer is Hallo percentage slagingspercentage enigszins minder dan 100%.

Zie voor meer informatie over het toevoegen en aanpassen van metrische gegevens grafieken [grafieken van de metrische gegevens aanpassen](storage-monitor-storage-account.md#customize-metrics-charts).

> [!NOTE]
> Het kan even duren voor de metrische gegevens tooappear in hello Azure-portal nadat u opslag metrische gegevens inschakelen. Dit komt omdat elk uur metrische gegevens voor Hallo vorige uur niet in hello Azure-portal weergegeven worden totdat Hallo huidige uur is verstreken. Bovendien worden minuut metrische gegevens momenteel niet weergegeven in hello Azure-portal. Zodat het tootwo uren toosee metrische gegevens, afhankelijk van wanneer u metrische gegevens inschakelen duren kan.
> 
> 

## <a name="use-azcopy-toocopy-server-logs-tooa-local-directory"></a>AzCopy toocopy server logboeken tooa lokale directory gebruiken
Azure Storage schrijft server logboek gegevens tooblobs tijdens tootables door metrische gegevens worden geschreven. Logboek blobs zijn beschikbaar in Hallo bekende `$logs` container voor uw opslagaccount. Logboek blobs worden hiërarchisch benoemd met jaar, maand, dag en uur, zodat u eenvoudig hello tijdbereik tooinvestigate gewenst kan vinden. Bijvoorbeeld in Hallo `storagesample` Hallo-container voor Hallo logboek blobs voor van 8-9: 00 uur, 01-02-2015-account is `https://storagesample.blob.core.windows.net/$logs/blob/2015/01/08/0800`. afzonderlijke blobs in deze container Hallo opeenvolgende naam hebben, beginnen met `000000.log`.

U kunt Hallo AzCopy-opdrachtregelprogramma toodownload deze serverzijde bestanden tooa Logboeklocatie van uw keuze op uw lokale machine. Bijvoorbeeld, kunt u opdracht toodownload Hallo logboekbestanden te volgen voor blob-bewerkingen die nodig was plaats op Hallo 2 januari 2015 toohello map `C:\Temp\Logs\Server`; vervangen `<storageaccountname>` met Hallo-naam van uw opslagaccount en `<storageaccountkey>` met uw de toegangssleutel voor:

```azcopy
AzCopy.exe /Source:http://<storageaccountname>.blob.core.windows.net/$logs /Dest:C:\Temp\Logs\Server /Pattern:"blob/2015/01/02" /SourceKey:<storageaccountkey> /S /V
```
AzCopy is beschikbaar voor downloaden op Hallo [Azure downloadt](https://azure.microsoft.com/downloads/) pagina. Zie voor meer informatie over het gebruik van AzCopy [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md).

Zie voor meer informatie over het downloaden van serverzijde logboeken [logboekgegevens downloaden opslag logboekregistratie](http://msdn.microsoft.com/library/azure/dn782840.aspx#DownloadingStorageLogginglogdata).

## <a name="use-microsoft-message-analyzer-tooanalyze-log-data"></a>Gebruik van Microsoft Message Analyzer tooanalyze logboekgegevens
Microsoft Message Analyzer is een hulpprogramma voor het vastleggen, weergeven en analyseren van verkeer, gebeurtenissen en andere systemen of toepassingen berichten in scenario's voor probleemoplossing en diagnostische messaging protocol. Berichtanalyse ook kunt u tooload cumulatieve, en analyseer gegevens van logboekbestanden en traceringsbestanden opgeslagen. Zie voor meer informatie over Message Analyzer [Microsoft Message Analyzer besturingssysteem Guide](http://technet.microsoft.com/library/jj649776.aspx).

Berichtanalyse omvat activa voor Azure Storage waarmee u tooanalyze server, client en netwerk-Logboeken. In deze sectie gaan we hoe toouse die extra tooaddress Hallo probleem van laag percentage slagen in Hallo opslag Logboeken.

### <a name="download-and-install-message-analyzer-and-hello-azure-storage-assets"></a>Download en installeer Message Analyzer en hello Azure Storage activa
1. Download [Message Analyzer](http://www.microsoft.com/download/details.aspx?id=44226) Hallo van Microsoft Download Center en voer het Hallo-installatieprogramma.
2. Start de Message Analyzer.
3. Van Hallo **extra** selecteert u **Asset Manager**. In Hallo **Asset Manager** dialoogvenster Selecteer **downloadt**, vervolgens filteren op **Azure Storage**. U ziet hello Azure Storage activa, zoals wordt weergegeven in de volgende Hallo-afbeelding.
4. Klik op **Sync alle weergegeven objecten** tooinstall hello Azure Storage activa. Hallo beschikbare elementen zijn onder andere:
   * **Azure Storage kleur regels:** Azure Storage kleur regels kunt u toodefine speciale filters die gebruikmaken van de kleur van tekst, en lettertype stijlen toohighlight berichten die specifieke informatie in een tracering bevatten.
   * **Azure Storage-grafieken:** Azure Storage kolomdiagrammen zijn vooraf gedefinieerde diagrammen die in een grafiek weergegeven logboekgegevens van de server. Houd er rekening mee dat toouse Azure Storage grafieken op dit moment, mag u alleen load Hallo serverlogboek in Hallo Analysis raster.
   * **Azure Storage Parsers:** hello Azure Storage parsers parse hello Azure Storage client en server HTTP aanmeldt in volgorde toodisplay ze Hallo Analysis raster.
   * **Azure Storage-Filters:** Azure Storage-filters zijn vooraf gedefinieerde criteria die u tooquery uw gegevens in Hallo Analysis raster gebruiken kunt.
   * **Azure Storage weergave-indelingen:** Azure Storage weergave-indelingen zijn vooraf gedefinieerde kolomindelingen en groeperingen in Hallo Analysis raster.
5. Opnieuw opstarten Message Analyzer nadat u Hallo activa hebt geïnstalleerd.

![Message Analyzer Asset Manager](./media/storage-e2e-troubleshooting/mma-start-page-1.png)

> [!NOTE]
> Installeer alle hello Azure Storage assets weergegeven voor de toepassing hello van deze zelfstudie.
> 
> 

### <a name="import-your-log-files-into-message-analyzer"></a>Importeren van de logboekbestanden in Message Analyzer
U kunt alle opgeslagen logboekbestanden (serverzijde, client-side en netwerk) importeren in één sessie in Microsoft Message Analyzer voor analyse.

1. Op Hallo **bestand** menu van Microsoft Message Analyzer, klikt u op **nieuwe sessie**, en klik vervolgens op **leeg sessie**. In Hallo **nieuwe sessie** dialoogvenster een naam voor uw analyse-sessie. In Hallo **Sessiedetails** -scherm, klikt u op Hallo **bestanden** knop.
2. tooload hello netwerk traceergegevens die worden gegenereerd door Message Analyzer, klikt u op **bestanden toevoegen**, blader toohello-locatie waar u het bestand .matp van uw web-traceringssessie Selecteer Hallo .matp bestand opgeslagen, en klik op **openen**.
3. tooload hello serverzijde logboekgegevens, klikt u op **bestanden toevoegen**, bladeren naar toohello locatie waar u uw logboeken serverzijde hebt gedownload, selecteer Hallo-logboekbestanden voor Hallo tijdsbereik u tooanalyze wilt en klikt u op **Openen**. Klik op Hallo **Sessiedetails** Configuratiescherm, set Hallo **tekst logboekconfiguratie** vervolgkeuzelijst voor elke server-side '-logboekbestand te**AzureStorageLog** tooensure die door Microsoft Berichtanalyse kan Hallo logboekbestand correct worden geparseerd.
4. tooload hello clientzijde logboekgegevens, klikt u op **bestanden toevoegen**, bladeren toohello-locatie waar u uw client-side '-Logboeken hebt opgeslagen, selecteert u logboekbestanden Hallo u tooanalyze wilt en klikt u op **Open**. Klik op Hallo **Sessiedetails** Configuratiescherm, set Hallo **tekst logboekconfiguratie** vervolgkeuzelijst voor elke client-side '-logboekbestand te**AzureStorageClientDotNetV4** tooensure die Microsoft Message Analyzer kunnen Hallo logboekbestand correct worden geparseerd.
5. Klik op **Start** in Hallo **nieuwe sessie** dialoogvenster tooload en parse Hallo logboekgegevens. Hallo-logboekgegevens in Hallo Message Analyzer Analysis rasterlijnen weergeven

Hallo in de volgende afbeelding toont een voorbeeld-sessie die is geconfigureerd met de server, client en netwerk-logboekbestanden voor tracering.

![Message Analyzer sessie configureren](./media/storage-e2e-troubleshooting/configure-mma-session-1.png)

Houd er rekening mee dat Message Analyzer logboekbestanden in het geheugen laadt. Als er een groot aantal logboekgegevens, zult u toofilter in volgorde tooget Hallo optimale prestaties van Message Analyzer.

Bepaal eerst Hallo tijdsbestek dat u wilt beoordelen, en deze periode zo klein mogelijk te houden. In veel gevallen zult u tooreview een periode van minuten of uren maximaal. Hallo kleinste set van logboeken die uw behoeften kunt importeren.

Als u nog steeds een grote hoeveelheid gegevens aan het logboek hebt, vervolgens kunt u een filter sessie toofilter toospecify uw logboekgegevens voordat u het laden. In Hallo **isStrictMode** in, selecteer Hallo **bibliotheek** toochoose een vooraf gedefinieerde filter knop; bijvoorbeeld kiezen **globale tijd Filter I** van hello Azure Storage-filters toofilter op een periode. U kunt vervolgens bewerken Hallo filter criteria toospecify Hallo starten en beëindigen tijdstempel Hallo-interval voor gewenste toosee. U kunt ook filteren op een bepaalde statuscode; u kunt bijvoorbeeld tooload alleen logboekvermeldingen waar Hallo-statuscode 404 is.

Zie voor meer informatie over het importeren van gegevens aan het logboek in Microsoft Message Analyzer [berichtgegevens bij het ophalen van](http://technet.microsoft.com/library/dn772437.aspx) op TechNet.

### <a name="use-hello-client-request-id-toocorrelate-log-file-data"></a>Hallo client aanvraag-ID toocorrelate Logbestandsgegevens gebruiken
Hello Azure Storage-clientbibliotheek genereert automatisch een unieke client aanvraag-ID voor elke aanvraag. Deze waarde wordt geschreven toohello clientlogboek, logboek van de server hello en netwerktracering hello, zodat u deze toocorrelate gegevens over alle drie logboeken binnen Message Analyzer gebruiken kunt. Zie [aanvraag-ID van Client](storage-monitoring-diagnosing-troubleshooting.md#client-request-id) aanvragen voor aanvullende informatie over client hello ID.

Hallo in de volgende secties wordt beschreven hoe toouse vooraf is geconfigureerd en aangepaste indeling weergaven toocorrelate-en groepsgegevens op basis van Hallo clientaanvraag-id.

### <a name="select-a-view-layout-toodisplay-in-hello-analysis-grid"></a>Selecteer een weergave-indeling toodisplay in Hallo Analysis raster
Hallo opslag activa voor Message Analyzer bevatten Azure Storage weergave-indelingen die vooraf geconfigureerde weergaven waarmee u toodisplay uw gegevens met nuttig groeperingen en kolommen voor verschillende scenario's kunt. U kunt ook aangepaste weergave-indelingen maken en opslaan voor hergebruik.

Hallo afbeelding hieronder ziet u Hallo **lay-out** menu beschikbaar door het selecteren van **lay-out** van Hallo werkbalk lint. Hallo indelingen voor Azure Storage zijn gegroepeerd onder Hallo **Azure Storage** knooppunt in het Hallo-menu. U kunt zoeken naar `Azure Storage` in Hallo zoeken vak toofilter op Azure Storage indelingen alleen bekijken. U kunt ook selecteren Hallo ster volgende tooa weergave lay-out toomake deze in een favoriet en Hallo boven aan het Hallo-menu weer te geven.

![Weergavemenu-indeling](./media/storage-e2e-troubleshooting/view-layout-menu.png)

toobegin met Selecteer **gegroepeerd op ClientRequestID en Module**. Deze groepen weergeven lay-out zich gegevens uit alle drie logboeken eerst op client-request-ID, vervolgens op de bron-logboekbestand (of **Module** in Berichtanalyse). Aan deze weergave kunt u inzoomen op een bepaalde client-aanvraag-ID en er gegevens van alle drie logboekbestanden voor die clientaanvraag-id.

Hallo afbeelding hieronder ziet u deze lay-out toegepast toohello logboek voorbeeldgegevens weergeven, met een subset met kolommen weergegeven. U kunt zien dat voor een bepaalde client aanvraag-ID Hallo Analysis raster gegevens worden weergegeven uit clientlogboek hello, serverlogboek en netwerktracering.

![Lay-out van Azure Storage weergeven](./media/storage-e2e-troubleshooting/view-layout-client-request-id-module.png)

> [!NOTE]
> Verschillende logboekbestanden hebben verschillende kolommen, zodat wanneer gegevens uit meerdere logboekbestanden wordt weergegeven in Hallo Analysis raster, sommige kolommen mag niet alle gegevens voor een bepaalde rij bevatten. Bijvoorbeeld in Hallo afbeelding hierboven, de client logboek rijen niet weergeven alle gegevens voor Hallo **tijdstempel**, **TimeElapsed**, **bron**, en **bestemming** kolommen, omdat deze kolommen niet bestaan in clientlogboek hello, maar bestaan in Hallo netwerktracering. Op deze manier Hallo **tijdstempel** kolom tijdstempelgegevens uit Hallo serverlogboek wordt weergegeven, maar geen gegevens weergegeven voor Hallo **TimeElapsed**, **bron**, en  **Bestemming** kolommen die geen deel uitmaken van het logboek voor Hallo-server.
> 
> 

Bovendien toousing hello Azure Storage indelingen, u kunt ook definiëren en opslaan van uw eigen weergave-indelingen. U kunt andere gewenste velden voor het groeperen van gegevens selecteren en Hallo groepering opslaan als onderdeel van uw aangepaste lay-out ook.

### <a name="apply-color-rules-toohello-analysis-grid"></a>Kleur regels toohello Analysis raster toepassen
Hallo opslag activa ook kleur, deze regels bieden dat een visuele betekent tooidentify verschillende typen fouten in Hallo Analysis raster. Hallo vooraf gedefinieerde kleur regels van toepassing tooHTTP fouten, zodat ze alleen voor Hallo logboek- en servertracering worden weergegeven.

tooapply kleur regels, selecteer **kleur regels** van Hallo werkbalk lint. Hier ziet u hello Azure Storage kleur regels in Hallo-menu. Hallo-zelfstudie, selecteert u **Client fouten (StatusCode tussen 400 en 499)**, zoals wordt weergegeven in volgende Hallo-afbeelding.

![Lay-out van Azure Storage weergeven](./media/storage-e2e-troubleshooting/color-rules-menu.png)

Bovendien toousing hello Azure Storage kleur die regels, kunt u ook definiëren en uw eigen regels kleur opslaan.

### <a name="group-and-filter-log-data-toofind-400-range-errors"></a>Groeperen en filteren gegevens toofind 400 bereik fouten in het logboek
Vervolgens we groeperen en filteren Hallo logboek gegevens toofind alle fouten in Hallo 400 bereik.

1. Zoek Hallo **StatusCode** kolom in Hallo Analysis raster, klik met de rechtermuisknop Hallo kolom kop en selecteer **groep**.
2. Vervolgens groeperen op Hallo **ClientRequestId** kolom. U ziet dat Hallo-gegevens in Hallo die Analysis raster nu is geordend op status code en op clientaanvraag van de-id.
3. Hallo hulpprogramma venster weergegeven als deze nog niet wordt weergegeven. Selecteer op de werkbalk-lint hello, **hulpprogramma Windows**, klikt u vervolgens **Filter voor**.
4. toofilter hello gegevens toodisplay alleen 400 bereik fouten in het logboek, toevoegen na filter criteria toohello hello **weergavefilter** venster en klik op **toepassen**:

    ```   
    (AzureStorageLog.StatusCode >= 400 && AzureStorageLog.StatusCode <=499) || (HTTP.StatusCode >= 400 && HTTP.StatusCode <= 499)
    ```

Hallo in de volgende afbeelding toont Hallo resultaten van deze groeperen en filteren. Uitbreidbare Hallo **ClientRequestID** veld onder Hallo groepering voor statuscode 409, bijvoorbeeld toont een bewerking dat heeft geresulteerd in deze statuscode.

![Lay-out van Azure Storage weergeven](./media/storage-e2e-troubleshooting/400-range-errors1.png)

Nadat dit filter is toegepast, ziet u dat de rijen uit de clientlogboek Hallo worden weggelaten, als Hallo clientlogboek omvat geen een **StatusCode** kolom. toobegin met we bekijkt hello server en tracering logboeken toolocate 404 netwerkfouten en retourneert we toohello client logboek tooexamine hello clientbewerkingen die toothem geleid.

> [!NOTE]
> U kunt filteren op Hallo **StatusCode** kolom en nog steeds gegevens weergeven van alle drie logboeken, met inbegrip van Hallo clientlogboek, als u een expressie toohello filter met logboekvermeldingen waar statuscode Hallo null is toevoegen. tooconstruct deze filterexpressie, gebruiken:
> 
> <code>&#42;StatusCode >= 400 or !&#42;StatusCode</code>
> 
> Dit filter retourneert alle rijen van de client Hallo logboek en alleen rijen uit Hallo serverlogboek- en HTTP-logboek waar statuscode Hallo groter is dan 400. Als u deze toohello lay-out weergeven gegroepeerd op aanvraag-ID van client en de module toepast, kunt u zoeken of blader door Hallo Meld u vermeldingen toofind toepassingsgroepen waar alle drie logboeken worden weergegeven.   
> 
> 

### <a name="filter-log-data-toofind-404-errors"></a>404 fouten in het logboek gegevens toofind filteren
Hallo opslag activa bevatten vooraf gedefinieerde filters waarmee u kunt toonarrow logboek gegevens toofind Hallo fouten of trends die u zoekt. Vervolgens twee vooraf gedefinieerde filters moet worden toegepast: die filters Hallo-server en netwerk traceerlogboeken voor 404-fouten en één die gegevens op een opgegeven tijdperiode Hallo worden gefilterd.

1. Hallo hulpprogramma venster weergegeven als deze nog niet wordt weergegeven. Selecteer op de werkbalk-lint hello, **hulpprogramma Windows**, klikt u vervolgens **Filter voor**.
2. Selecteer in het venster Filter Hallo **bibliotheek**, en zoek op `Azure Storage` toofind hello Azure Storage-filters. Selecteer Hallo filter voor **404 (niet gevonden) berichten in alle logboeken**.
3. Weergave Hallo **bibliotheek** menu opnieuw, en zoek en selecteer Hallo **globale tijdfilter**.
4. Hallo tijdstempels wordt weergegeven in Hallo toohello filterbereik dat u tooview wilt bewerken. Dit helpt toonarrow Hallo scala aan gegevens tooanalyze.
5. Het filter moet vergelijkbaar toohello voorbeeld hieronder weergegeven. Klik op **toepassen** tooapply Hallo filter toohello Analysis raster.

    ```   
    ((AzureStorageLog.StatusCode == 404 || HTTP.StatusCode == 404)) And
    (#Timestamp >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39)
    ```

    ![Lay-out van Azure Storage weergeven](./media/storage-e2e-troubleshooting/404-filtered-errors1.png)

### <a name="analyze-your-log-data"></a>De logboekgegevens analyseren
Nu dat u hebt gegroepeerd en uw gegevens gefilterd, Bekijk details op Hallo van afzonderlijke aanvragen die 404-fouten gegenereerd. In de huidige weergave opmaak Hallo Hallo gegevens gegroepeerd op client-aanvraag-ID, klikt u vervolgens door de bron-logboek. Aangezien we op aanvragen waarin Hallo StatusCode veld 404 bevat filtert, ziet er alleen Hallo-server en traceringsgegevens voor netwerk, niet Hallo client logboekgegevens.

Hallo afbeelding hieronder ziet u een specifieke aanvraag waarin een 404 door een ophalen van Blob-bewerking heeft opgeleverd omdat Hallo blob niet bestaat. Houd er rekening mee dat sommige kolommen in de standaardweergave Hallo in volgorde toodisplay Hallo relevante gegevens zijn verwijderd.

![Gefilterde Server en de logboeken met traceringen](./media/storage-e2e-troubleshooting/server-filtered-404-error.png)

We je deze client-request-ID vervolgens correleren met Hallo client logboek gegevens toosee welke acties Hallo-client de failoverbewerking duurt wanneer Hallo-fout is opgetreden. U kunt een nieuwe Analysis rasterweergave voor deze sessie tooview Hallo client logboekgegevens, die wordt geopend in een tweede tabblad weergeven:

1. Hallo-waarde van Hallo eerst kopiëren **ClientRequestId** veld toohello Klembord. U kunt dit doen door het selecteren van een rij zoeken naar Hallo **ClientRequestId** veld met de rechtermuisknop op Hallo van de waarde en het kiezen van **kopie 'ClientRequestId'**.
2. Selecteer op de werkbalk-lint hello, **nieuwe Viewer**, selecteert u vervolgens **Analysis raster** tooopen een nieuw tabblad Hallo nieuwe tabblad toont alle gegevens in de logboekbestanden, zonder groepering, het filteren of kleur regels.
3. Selecteer op de werkbalk-lint hello, **lay-out**, selecteert u vervolgens **kolommen van alle .NET-Client** onder Hallo **Azure Storage** sectie. Deze weergave-indeling geeft gegevens uit clientlogboek hello, evenals Hallo traceerlogboeken server en het netwerk. Standaard wordt gesorteerd op Hallo **MessageNumber** kolom.
4. Zoeken vervolgens clientlogboek Hallo Hallo client aanvraag-ID. Selecteer op de werkbalk-lint hello, **berichten vinden**, geeft u een aangepast filter op Hallo client aanvraag-ID in Hallo **vinden** veld. Gebruik deze syntaxis voor het Hallo-filter, geven de aanvraag-ID van uw eigen client:

    ```
    *ClientRequestId == "398bac41-7725-484b-8a69-2a9e48fc669a"
    ```

Berichtanalyse zoekt en selecteert Hallo eerste logboekvermelding Hallo zoekcriteria overeenkomt met de Hallo client aanvraag-ID. In clientlogboek hello, zijn er meerdere vermeldingen voor elke client-request-ID, zodat u toogroup kunt ze op Hallo **ClientRequestId** veld toomake deze eenvoudiger toosee ze allemaal samen. Hallo-afbeelding hieronder bevat alle Hallo-berichten in Hallo-client zich voor Hallo aanmelden opgegeven client aanvraag-ID.

![Client logboek weergeeft 404-fouten](./media/storage-e2e-troubleshooting/client-log-analysis-grid1.png)

Hallo gegevens weergegeven in de weergave-indelingen op deze twee tabbladen Hallo gebruikt, kunt u analyseren Hallo aanvraag gegevens toodetermine wat Hallo fout hebben veroorzaakt. U kunt ook zoeken op aanvragen die deze één toosee voorafgegaan als een eerdere gebeurtenis mogelijk toohello 404-fout hebben geleid. U kunt bijvoorbeeld Hallo logboekvermeldingen voor client voorafgaand aan deze toodetermine client aanvraag-ID of Hallo blob is mogelijk verwijderd of dat het Hallo-fout is vervallen toohello clienttoepassing een CreateIfNotExists-API aanroepen voor een container of blob bekijken. In client-logboek hello, vindt u Hallo blobadres in Hallo **beschrijving** veld; in Hallo-server en de logboeken met traceringen, wordt deze informatie verschijnt in Hallo **samenvatting** veld.

Zodra u Hallo-adres van Hallo blob die Hallo 404-fout heeft opgeleverd weet, kunt u verder onderzoek. Als u zoekt Hallo logboekvermeldingen voor andere berichten die zijn gekoppeld aan bewerkingen op Hallo dezelfde blob, kunt u controleren of het Hallo-client Hallo entiteit eerder verwijderd.

## <a name="analyze-other-types-of-storage-errors"></a>Andere soorten opslag fouten analyseren
Nu dat u vertrouwd te raken met Message Analyzer tooanalyze uw logboekgegevens bent, kunt u andere soorten fouten bij het gebruik van weergave analyseren indelingen, kleur regels en zoeken/filteren. Hallo tabellen hieronder een lijst met enkele problemen beschreven die u kunt tegenkomen en Hallo filtercriteria toolocate kunt u ze. Voor meer informatie over het samenstellen van filters en Hallo Message Analyzer filteren taal, Zie [berichtgegevens filteren](http://technet.microsoft.com/library/jj819365.aspx).

| tooInvestigate... | Gebruik de filterexpressie... | Expressie van toepassing tooLog (Client-, Server-, netwerk, alle) |
| --- | --- | --- |
| Onverwachte vertragingen bij de levering van berichten in een wachtrij |AzureStorageClientDotNetV4.Description bevat 'Opnieuw proberen is bewerking mislukt.' |Client |
| HTTP-toename van PercentThrottlingError |HTTP. Response.StatusCode == 500 &#124; &#124; HTTP. Response.StatusCode == 503 |Netwerk |
| Toename van het PercentTimeoutError |HTTP. Response.StatusCode == 500 |Netwerk |
| Toename van het PercentTimeoutError (alle) |* StatusCode 500 == |Alle |
| Toename van het PercentNetworkError |AzureStorageClientDotNetV4.EventLogEntry.Level < 2 |Client |
| HTTP-fout 403 (verboden) berichten |HTTP. Response.StatusCode == 403 |Netwerk |
| HTTP 404 (niet gevonden) berichten |HTTP. Response.StatusCode == 404 |Netwerk |
| 404 (alle) |* StatusCode 404 == |Alle |
| Shared Access Signature (SAS) autorisatie probleem |AzureStorageLog.RequestStatus == "SASAuthorizationError" |Netwerk |
| HTTP 409 (Conflict) berichten |HTTP. Response.StatusCode == 409 |Netwerk |
| 409 (alle) |* StatusCode == 409 |Alle |
| Lage PercentSuccess of analytics logboekvermeldingen hebben bewerkingen met de status van ClientOtherErrors |AzureStorageLog.RequestStatus == "ClientOtherError" |Server |
| Nagle waarschuwing |((AzureStorageLog.EndToEndLatencyMS-AzureStorageLog.ServerLatencyMS) > (AzureStorageLog.ServerLatencyMS * 1.5)) en (AzureStorageLog.RequestPacketSize < 1460) en (AzureStorageLog.EndToEndLatencyMS - AzureStorageLog.ServerLatencyMS > = 200) |Server |
| Tijdsbereik in Logboeken Server en het netwerk |#Timestamp > = 2014-10-20T16:36:38 en #Timestamp < = 2014-10-20T16:36:39 |Netwerk-server |
| Tijdsbereik in Server-logboeken |AzureStorageLog.Timestamp > = 2014-10-20T16:36:38 en AzureStorageLog.Timestamp < = 2014-10-20T16:36:39 |Server |

## <a name="next-steps"></a>Volgende stappen
Zie de volgende bronnen voor meer informatie over het oplossen van problemen end-to-end-scenario's in Azure Storage:

* [Controleren, vaststellen en oplossen van Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md)
* [Storage Analytics](http://msdn.microsoft.com/library/azure/hh343270.aspx)
* [Een opslagaccount in hello Azure-portal bewaken](storage-monitor-storage-account.md)
* [Gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md)
* [Microsoft Message Analyzer besturingssysteem handleiding](http://technet.microsoft.com/library/jj649776.aspx)
