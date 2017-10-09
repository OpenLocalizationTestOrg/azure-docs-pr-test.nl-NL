---
title: aaaAzure Compute - Linux-extensie voor diagnostische | Microsoft Docs
description: Hoe tooconfigure hello Azure Linux diagnostische extensie (LAD) toocollect metrische gegevens en gebeurtenissen van virtuele Linux-machines in Azure wordt uitgevoerd.
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a>Linux-extensie voor diagnostische toomonitor metrische gegevens en logboekbestanden gebruiken

Dit document beschrijft versie 3.0 en nieuwere Hallo diagnostische Linux-extensie.

> [!IMPORTANT]
> Zie voor meer informatie over versie 2.3 en oudere [dit document](./classic/diagnostic-extension-v2.md).

## <a name="introduction"></a>Inleiding

Hallo Linux diagnostische uitbreiding kunt u een gebruiker controleprogramma Hallo de status van een Linux-VM uitgevoerd op Microsoft Azure. Er Hallo volgende mogelijkheden:

* Verzamelt systeemprestaties van Hallo VM en slaat ze op in een specifieke tabel in een aangewezen storage-account.
* Logboekgebeurtenissen moeten worden opgehaald uit syslog en slaat ze op in een specifieke tabel in Hallo aangewezen storage-account.
* Hiermee kunt gebruikers toocustomize Hallo gegevens metrische gegevens die zijn verzameld en worden geüpload.
* Kunnen gebruikers toocustomize Hallo syslog faciliteiten en niveaus van gebeurtenissen die worden verzameld en worden geüpload.
* Hiermee kunt gebruikers tooupload opgegeven logboek bestanden tooa aangewezen opslag tabel.
* Ondersteunt het verzenden van metrische gegevens en logboekbestanden gebeurtenissen tooarbitrary EventHub eindpunten en blobs JSON-indeling in Hallo aangewezen storage-account.

Deze extensie werkt met beide Azure-implementatiemodellen.

## <a name="installing-hello-extension-in-your-vm"></a>Hallo-uitbreiding installeren in uw virtuele machine

U kunt deze uitbreiding inschakelen met behulp van hello Azure PowerShell-cmdlets, Azure CLI-scripts of sjablonen voor Azure-implementatie. Zie voor meer informatie [extensies functies](./extensions-features.md).

Hello Azure-portal niet gebruikte tooenable of LAD 3.0 configureren. In plaats daarvan installeert en configureert deze versie 2.3. Azure portal grafieken en waarschuwingen werken met gegevens van beide versies van Hallo-uitbreiding.

Deze installatie-instructies en een [downloadbare voorbeeldconfiguratie](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) LAD 3.0 te configureren:

* Leg Hallo dezelfde metrische gegevens zijn verstrekt door LAD 2.3;
* vastleggen van een handig set file system maatstaven voor nieuwe tooLAD 3.0;
* Hallo syslog standaardverzameling ingeschakeld door LAD 2.3; vastleggen
* Schakel hello Azure portal ervaring voor grafieken en waarschuwen voor VM metrische gegevens.

Hallo downloadbare configuratie is slechts een voorbeeld; Wijzig het toosuit uw eigen behoeften.

### <a name="prerequisites"></a>Vereisten

* **Azure Linux Agent versie 2.2.0 of hoger**. De meeste Azure VM Linux galerie met installatiekopieën zijn inclusief versie 2.2.7 of hoger. Voer `/usr/sbin/waagent -version` tooconfirm Hallo versie is geïnstalleerd op Hallo VM. Als Hallo VM is een oudere versie van de guest-agent hello, volgt u [deze instructies](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate deze.
* **Azure CLI**. [Instellen van Azure CLI 2.0 Hallo](https://docs.microsoft.com/cli/azure/install-azure-cli) omgeving op uw computer.
* Hallo wget-opdracht als u dit nog niet hebt: Voer `sudo apt-get install wget`.
* Een bestaande Azure-abonnement en een bestaande opslag account binnen het toostore Hallo gegevens.

### <a name="sample-installation"></a>Voorbeeld-installatie

Vul in de juiste parameters op Hallo Hallo eerste drie regels en voer dit script als hoofdmap:

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

Hallo-URL voor de voorbeeldconfiguratie Hallo en de inhoud ervan zijn onderwerp toochange. Download een exemplaar van Hallo portalinstellingen JSON-bestand en aanpassen voor uw behoeften. Alle sjablonen of automation die u samenstellen moet uw eigen exemplaar, in plaats van telkens te downloaden die URL te gebruiken.

### <a name="updating-hello-extension-settings"></a>Hallo-extensie-instellingen bijwerken

Nadat u uw beveiligde of openbare instellingen hebt gewijzigd, deze implementeren toohello VM door te voeren dezelfde opdracht Hallo. Als alles in het Hallo-instellingen hebt gewijzigd, worden bijgewerkt Hallo instellingen toohello extensie verzonden. LAD Hallo-configuratie wordt opnieuw geladen en zelf opnieuw gestart.

### <a name="migration-from-previous-versions-of-hello-extension"></a>Migratie van eerdere versies van Hallo-uitbreiding

meest recente versie van de uitbreiding Hallo Hallo is **3.0**. **Eventuele oude versies (2.x) zijn afgeschaft en is mogelijk niet-gepubliceerde op of na 31 juli 2018**.

> [!IMPORTANT]
> Deze extensie introduceert recente wijzigingen toohello configuratie van Hallo-uitbreiding. Een dergelijke wijziging is aangebracht tooimprove Hallo beveiliging van Hallo-extensie. Als gevolg hiervan kan achterwaartse compatibiliteit met 2.x niet worden beheerd. Hallo-extensie Publisher voor deze extensie is ook anders dan Hallo publisher voor Hallo 2.x-versies.
>
> toomigrate van 2.x toothis nieuwe versie van Hallo-extensie, moet u oude Hallo-extensie (onder Hallo oude naam van uitgever) en vervolgens installeren versie 3 van Hallo uitbreiding verwijderen.

Aanbevelingen:

* Hallo-uitbreiding te installeren met de upgrade van secundaire versie automatisch ingeschakeld.
  * Geef op klassieke implementatiemodel VMs '3.*' hello versie als u de extensie Hallo via Azure XPLAT CLI of Powershell installeert.
  * Op Azure Resource Manager deployment model VM's, bevatten ' 'autoUpgradeMinorVersion': true' in hello VM-sjabloon voor implementatie.
* Gebruik een nieuwe/verschillende storage-account voor LAD 3.0. Er zijn enkele kleine compatibiliteitsproblemen tussen LAD 2.3 en LAD 3.0 waardoor een account lastige delen:
  * LAD 3.0 slaat syslog-gebeurtenissen in een tabel met een andere naam.
  * Hallo counterSpecifier tekenreeksen voor `builtin` metrische gegevens verschillen LAD 3.0.

## <a name="protected-settings"></a>Beveiligde instellingen

Deze reeks configuratiegegevens gevoelige informatie bevat die moet worden beschermd tegen openbare weergave, bijvoorbeeld storage-referenties. Deze instellingen zijn verzonden tooand door Hallo-uitbreiding in versleutelde vorm opgeslagen.

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

Naam | Waarde
---- | -----
storageAccountName | Hallo-naam van Hallo storage-account waarin gegevens worden geschreven door Hallo-uitbreiding.
storageAccountEndPoint | (optioneel) Hallo-eindpunt te identificeren in welke Hallo storage-account bestaat Hallo-cloud. Als u deze instelling niet aanwezig is, LAD toohello openbare Azure-cloud, standaard `https://core.windows.net`. Deze waarde in een opslagaccount in de Duitse Azure, Azure Government of Azure China toouse dienovereenkomstig instellen.
storageAccountSasToken | Een [Account-SAS-token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) voor Blob- en -services (`ss='bt'`), van toepassing toocontainers en objecten (`srt='co'`), welke verleent toevoegen, maken, weergeven, bijwerken en schrijfmachtigingen (`sp='acluw'`). Voer *niet* Hallo voorloopspaties vraagteken (?) bevatten.
mdsdHttpProxy | (optioneel) HTTP-proxy informatie die nodig is tooenable Hallo extensie tooconnect toohello opgegeven storage-account en -eindpunt.
sinksConfig | (optioneel) Details van alternatieve doelen toowhich metrische gegevens en gebeurtenissen kunnen worden geleverd. Hallo specifieke details van elke gegevens sink ondersteund door Hallo extension worden behandeld in Hallo secties die volgen.

U kunt eenvoudig hello vereist SAS-token via hello Azure-portal opstellen.

1. Hallo opslagaccounts voor algemeen gebruik account toowhich gewenste Hallo extensie toowrite selecteren
1. Selecteer "Shared access signature' hello instellingen deel van Hallo linkermenu
1. Controleer de toepasselijke rubrieken Hallo zoals eerder beschreven
1. Klik op Hallo 'SAS genereren'.

![Afbeelding](./media/diagnostic-extension/make_sas.png)

Kopiëren Hallo SAS gegenereerd in Hallo storageAccountSasToken veld; Hallo voorloopspaties vraagteken verwijderen ('? ').

### <a name="sinksconfig"></a>sinksConfig

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

Deze optionele secties bevatten aanvullende bestemmingen toowhich Hallo extensie stuurt Hallo-gegevens die worden verzameld. Hallo 'sink'-matrix bevat een object voor elke aanvullende gegevens sink. Hallo bepaalt van kenmerk 'type' Hallo andere kenmerken in Hallo-object.

Element | Waarde
------- | -----
naam | Een tekenreeks toorefer toothis sink elders in de configuratie van de uitbreiding Hallo gebruikt.
type | Hallo type sink wordt gedefinieerd. Hiermee bepaalt u andere waarden Hallo (indien aanwezig) in exemplaren van dit type.

Versie 3.0 Hallo Linux diagnostische uitbreiding ondersteunt twee typen van de sink: EventHub en JsonBlob.

#### <a name="hello-eventhub-sink"></a>Hallo EventHub sink

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

Hallo 'sasURL' invoer bevat Hallo volledige URL, met inbegrip van SAS-token voor Hallo Event Hub toowhich gegevens moet worden gepubliceerd. LAD vereist een SAS naamgeving van een beleid waarmee Hallo verzenden claim. Een voorbeeld:

* Een aangeroepen Event Hubs-naamruimte maken`contosohub`
* Een Event Hub maken in de naamruimte van Hallo aangeroepen`syslogmsgs`
* Een gedeeld toegangsbeleid maken op Hallo Event Hub met de naam `writer` dat Hiermee Hallo claim verzenden

Als u hebt gemaakt een SAS goede tot middernacht UTC op 1 januari 2018, mogelijk Hallo sasURL waarde:

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

Zie voor meer informatie over het genereren van SAS-tokens voor Event Hubs [deze webpagina](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).

#### <a name="hello-jsonblob-sink"></a>Hallo JsonBlob sink

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

Gegevens omgeleid tooa JsonBlob sink is opgeslagen in blobs in Azure-opslag. Elk exemplaar van LAD een blob elk uur wordt gemaakt voor elke naam sink. Elke blob bevat altijd een ongeldige syntaxis JSON-matrix van object. Nieuwe vermeldingen moment toohello matrix toegevoegd. BLOBs worden opgeslagen in een container met dezelfde naam als sink Hallo Hallo. Hallo Azure storage-regels voor namen van de blob-containers toohello namen van JsonBlob put toepassen: tussen 3 en 63 kleine alfanumerieke ASCII-tekens of streepjes bevatten.

## <a name="public-settings"></a>Instellingen voor openbare

Deze structuur bevat verschillende blokken met instellingen die Hallo verzamelde Hallo-uitbreiding bepalen. Elke instelling is optioneel. Als u opgeeft `ladCfg`, moet u ook opgeven `StorageAccount`.

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

Element | Waarde
------- | -----
StorageAccount | Hallo-naam van Hallo storage-account waarin gegevens worden geschreven door Hallo-uitbreiding. Moet dezelfde naam, zoals is opgegeven in Hallo Hallo [beveiligde instellingen](#protected-settings).
mdsdHttpProxy | (optioneel) Hetzelfde als in Hallo [beveiligde instellingen](#protected-settings). Hallo openbare waarde wordt overschreven door persoonlijke Hallo-waarde als ingesteld. Proxyinstellingen met een geheim, zoals een wachtwoord, in Hallo plaatsen [beveiligde instellingen](#protected-settings).

Hallo resterende elementen zijn beschreven in Hallo uit te voeren.

### <a name="ladcfg"></a>ladCfg

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

Deze optionele structuur besturingselementen Hallo verzamelen van metrische gegevens en logboeken voor levering toohello Azure-service en tooother gegevens Put. U moet ofwel opgeven `performanceCounters` of `syslogEvents` of beide. U moet opgeven Hallo `metrics` structuur.

Element | Waarde
------- | -----
eventVolume | (optioneel) Besturingselementen Hallo aantal partities binnen Hallo opslag tabel is gemaakt. Moet een van `"Large"`, `"Medium"`, of `"Small"`. Als niet wordt opgegeven, wordt de standaardwaarde Hallo `"Medium"`.
sampleRateInSeconds | (optioneel) Hallo standaardinterval tussen verzameling maatstaven voor onbewerkte (unaggregated). Hallo kleinste ondersteund samplefrequentie is 15 seconden. Als niet wordt opgegeven, wordt de standaardwaarde Hallo `15`.

#### <a name="metrics"></a>metrics

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

Element | Waarde
------- | -----
resourceId | Hello Azure Resource Manager resource-ID van het Hallo VM of van virtuele-machineschaalset Hallo ingesteld toowhich Hallo die virtuele machine deel uitmaakt. Deze instelling moet ook worden opgegeven als een JsonBlob sink is gebruikt in de Hallo-configuratie.
scheduledTransferPeriod | Hallo frequentie waarmee cumulatieve metrische gegevens toobe zijn berekend en tooAzure metrische gegevens, uitgedrukt als een tijdsinterval 8601 IS overgedragen. Hallo kleinste overdracht periode is 60 seconden, dat wil zeggen, PT1M. U moet ten minste één scheduledTransferPeriod opgeven.

Voorbeelden van Hallo metrische gegevens die zijn opgegeven in Hallo performanceCounters sectie elke 15 seconden worden verzameld of op Hallo samplefrequentie expliciet is gedefinieerd voor Hallo teller. Als meerdere scheduledTransferPeriod frequenties wordt weergegeven (zoals in Hallo voorbeeld), wordt elke aggregatie wordt afzonderlijk berekend.

#### <a name="performancecounters"></a>performanceCounters

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

Deze optionele sectie bepaalt Hallo-verzameling van metrische gegevens. Onbewerkte voorbeelden worden samengevoegd voor elk [scheduledTransferPeriod](#metrics) tooproduce deze waarden:

* gemiddelde
* minimale
* Maximum
* laatste verzameld waarde
* aantal steekproeven onbewerkte toocompute Hallo statistische functie gebruikt

Element | Waarde
------- | -----
Put | (optioneel) Een door komma's gescheiden lijst met namen van de sinks toowhich die LAD samengevoegde metrische resultaten verzendt. Alle samengevoegde metrische gegevens zijn gepubliceerde tooeach vermeld sink. Zie [sinksConfig](#sinksconfig). Voorbeeld: `"EHsink1, myjsonsink"`.
type | Werkelijke Hallo-provider van Hallo metriek identificeert.
Klasse | Identificeert samen met 'teller' hello specifieke metrische gegevens in de naamruimte Hallo-provider.
Prestatiemeteritems | Identificeert samen met 'class' hello specifieke metrische gegevens in de naamruimte Hallo-provider.
counterSpecifier | Hallo specifieke metrische gegevens binnen hello Azure metrische gegevens naamruimte identificeert.
Voorwaarde | (optioneel) Van toepassing selecteert een specifiek exemplaar van Hallo object toowhich Hallo metriek of selecteert Hallo aggregatie over alle exemplaren van dat object. Zie voor meer informatie, Hallo [ `builtin` metrische definities](#metrics-supported-by-builtin).
sampleRate | IS 8601 interval dat ingesteld Hallo snelheid waarmee onbewerkte voorbeelden voor deze metrische gegevens worden verzameld. Als niet is ingesteld, Hallo-interval voor gegevensverzameling is ingesteld door de waarde van Hallo [sampleRateInSeconds](#ladcfg). Hallo kortste ondersteunde-samplefrequentie is 15 seconden (PT15S).
eenheid | Moet een van deze tekenreeksen: 'Count', 'Bytes', 'Seconden', 'Percentage', 'CountPerSecond', 'BytesPerSecond', 'Milliseconde'. Hallo-eenheid voor Hallo metriek definieert. Gegevensgebruikers Hallo verzameld verwachten Hallo verzamelde gegevens waarden toomatch deze eenheid. LAD negeert dit veld.
Weergavenaam | Hallo label (in de taal Hallo Hallo gekoppeld landinstelling instellen) toobe gekoppeld toothis gegevens in Azure metrische gegevens. LAD negeert dit veld.

Hallo counterSpecifier is een identifier. CounterSpecifier consumenten van metrische gegevens, zoals hello Azure portal voor grafieken en waarschuwingen van de functie, gebruiken als Hallo 'sleutel', waarmee een waarde of een exemplaar van een metriek. Voor `builtin` metrische gegevens, wordt aangeraden gebruik van counterSpecifier-waarden die met beginnen `/builtin/`. Als u een specifiek exemplaar van een metriek verzamelt, raden wij dat u Hallo-id van Hallo exemplaar toohello counterSpecifier waarde koppelen. Enkele voorbeelden:

* `/builtin/Processor/PercentIdleTime`-Niet-actieve tijd met een gemiddelde van alle kernen
* `/builtin/Disk/FreeSpace(/mnt)`-Vrije ruimte voor Hallo mnt bestandssysteem
* `/builtin/Disk/FreeSpace`-Vrije ruimte met een gemiddelde van alle gekoppelde bestandssystemen

Verwacht Hallo counterSpecifier waarde toomatch een patroon LAD noch hello Azure-portal. In de manier waarop u counterSpecifier waarden samenstelt consistent zijn.

Wanneer u opgeeft `performanceCounters`, tooa gegevenstabel LAD altijd geschreven in Azure-opslag. U kunt hebben Hallo dezelfde gegevens die zijn geschreven tooJSON blobs en/of Event Hubs, maar u kunt opslag tooa gegevenstabel niet uitschakelen. Alle exemplaren van Hallo diagnostische uitbreiding geconfigureerd toouse Hallo hetzelfde opslagaccount naam- en eindpunt toevoegen hun toohello metrische gegevens en Logboeken dezelfde tabel. Als er te veel virtuele machines schrijft schrijft toohello partitie in dezelfde tabel, Azure kunt beperken toothat partitie. Hallo eventVolume oorzaken vermeldingen toobe instelling verdeeld over 1 (klein), 10 (gemiddeld) of 100 (groot) verschillende partities. 'Gemiddeld' is meestal voldoende tooensure verkeer niet wordt beperkt. Hallo metrische gegevens voor Azure-functie van hello Azure-portal gebruikt Hallo-gegevens in deze tabel tooproduce grafieken of tootrigger waarschuwingen. Hallo-tabelnaam is Hallo samenvoeging van deze tekenreeksen:

* `WADMetrics`
* Hallo 'scheduledTransferPeriod' voor Hallo geaggregeerd waarden die zijn opgeslagen in de tabel Hallo
* `P10DV2S`
* Een datum in formulier Hallo 'JJJJMMDD", wijzigingen van elke 10 dagen

Voorbeelden zijn onder meer `WADMetricsPT1HP10DV2S20170410` en `WADMetricsPT1MP10DV2S20170609`.

#### <a name="syslogevents"></a>syslogEvents

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

Deze optionele sectie bepaalt Hallo-verzameling van gebeurtenissen van syslog. Als de sectie hello wordt weggelaten, worden helemaal syslog-gebeurtenissen niet vastgelegd.

Hallo syslogEventConfiguration verzameling heeft een vermelding voor elke syslog-faciliteit van belang. Als minSeverity 'NONE' voor een bepaalde opslagruimte, of als faciliteit niet wordt weergegeven in het element Hallo helemaal, worden er zijn geen gebeurtenissen van de faciliteit vastgelegd.

Element | Waarde
------- | -----
Put | Een door komma's gescheiden lijst met namen van de sinks toowhich afzonderlijk logboek gebeurtenissen worden gepubliceerd. Alle gebeurtenissen die overeenkomt met de Hallo beperkingen in syslogEventConfiguration zijn gepubliceerde tooeach vermeld sink. Voorbeeld: 'EHforsyslog'
voorziening %{facilityname/ | De naam van een syslog-faciliteit (zoals ' logboek\_gebruiker ' of ' LOG\_LOCAL0 '). Zie sectie van de Hallo 'faciliteit' Hallo [syslog man pagina](http://man7.org/linux/man-pages/man3/syslog.3.html) voor Hallo volledige lijst.
minSeverity | Een urgentieniveau syslog (zoals ' logboek\_fout ' of ' LOG\_INFO '). Zie sectie van de Hallo 'niveau' Hallo [syslog man pagina](http://man7.org/linux/man-pages/man3/syslog.3.html) voor Hallo volledige lijst. Hallo-extensie bevat gebeurtenissen die worden verzonden toohello faciliteit op of boven Hallo opgegeven niveau.

Wanneer u opgeeft `syslogEvents`, tooa gegevenstabel LAD altijd geschreven in Azure-opslag. U kunt hebben Hallo dezelfde gegevens die zijn geschreven tooJSON blobs en/of Event Hubs, maar u kunt opslag tooa gegevenstabel niet uitschakelen. Hallo partitioneren gedrag voor deze tabel wordt beschreven voor Hallo `performanceCounters`. Hallo-tabelnaam is Hallo samenvoeging van deze tekenreeksen:

* `LinuxSyslog`
* Een datum in formulier Hallo 'JJJJMMDD", wijzigingen van elke 10 dagen

Voorbeelden zijn onder meer `LinuxSyslog20170410` en `LinuxSyslog20170609`.

### <a name="perfcfg"></a>perfCfg

Deze optionele sectie bepaalt de uitvoering van willekeurige [OMI](https://github.com/Microsoft/omi) query's.

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

Element | Waarde
------- | -----
naamruimte | (optioneel) Hallo OMI naamruimte in welke Hallo query moet worden uitgevoerd. Als u niets opgeeft, Hallo standaardwaarde is "root/scx', geïmplementeerd door Hallo [System Center platformoverschrijdende Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).
query | Hallo OMI query toobe uitgevoerd.
Tabel | (optioneel) hello Azure storage-tabel, in Hallo aangewezen storage-account (Zie [beveiligde instellingen](#protected-settings)).
frequency | (optioneel) Hallo aantal seconden tussen het uitvoeren van query Hallo. Standaardwaarde is 300 (5 minuten); minimumwaarde is 15 seconden.
Put | (optioneel) Een door komma's gescheiden lijst met namen van aanvullende put toowhich onbewerkte metrische voorbeeldresultaten moet worden gepubliceerd. Er is geen aggregatie van deze voorbeelden onbewerkte wordt berekend door Hallo-extensie of Azure metrische gegevens.

Een 'tabel' of 'sinks', of beide moeten worden opgegeven.

### <a name="filelogs"></a>fileLogs

Besturingselementen Hallo vastleggen van logboekbestanden. LAD nieuwe tekstregels vastgelegd als ze zijn toohello bestand geschreven en schrijft deze tootable rijen en/of alle opgegeven Put (JsonBlob of EventHub).

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

Element | Waarde
------- | -----
Bestand | volledige padnaam op Hallo van Hallo log-bestand toobe gecontroleerd en vastgelegd. Hallo padnaam moet één bestand; de naam Deze kan niet de naam van een map of jokertekens bevatten.
Tabel | (optioneel) hello Azure storage tabel in Hallo aangewezen opslag account (zoals opgegeven in configuratie Hallo beveiligd), in welke nieuwe lijnen van Hallo 'staart' Hallo-bestand worden geschreven.
Put | (optioneel) Een door komma's gescheiden lijst met namen van aanvullende put toowhich logboek regels verzonden.

Een 'tabel' of 'sinks', of beide moeten worden opgegeven.

## <a name="metrics-supported-by-hello-builtin-provider"></a>Metrische gegevens die worden ondersteund door Hallo builtin provider

Hallo builtin metrische provider is een bron van de metrische gegevens meest interessante tooa uitgebreide set met gebruikers. Deze metrische gegevens kunnen worden onderverdeeld in vijf brede klassen:

* Processor
* Geheugen
* Netwerk
* Bestandssysteem
* Schijf

### <a name="builtin-metrics-for-hello-processor-class"></a>ingebouwde metrische gegevens voor Hallo Processor-klasse

Hallo Processorklasse van metrische gegevens biedt informatie over het processorgebruik in Hallo VM. Bij het samenvoegen van percentages is Hallo resultaat Hallo gemiddelde over alle CPU's. In een twee belangrijkste VM als één kern 100% bezig was en andere Hallo 100% niet-actief, Hallo gerapporteerd dat percentidletime zou dit 50. Als elke core is 50% bezig voor Hallo dezelfde periode, Hallo gerapporteerde resultaat zou ook 50. In een vier core VM, met één kern 100% bezet en Hallo andere niet-actief, Hallo gerapporteerd dat percentidletime 75 zou zijn.

Prestatiemeteritems | Betekenis
------- | -------
PercentIdleTime | Percentage tijd tijdens Hallo aggregatie venster dat processors zijn worden gebruikt voor het uitvoeren van niet-actieve Hallo kernel-lus
percentProcessorTime | Percentage tijd dat een niet-actieve thread wordt uitgevoerd
PercentIOWaitTime | Percentage tijd wachten toocomplete voor i/o-bewerkingen
PercentInterruptTime | Percentage tijd hardware/software-interrupts en DPC's (uitgestelde procedureaanroepen) wordt uitgevoerd
PercentUserTime | Niet-actieve tijd databaseprestaties aggregatie Hallo Hallo percentage tijd besteed aan in het dialoogvenster gebruiker meer met normale prioriteit
PercentNiceTime | Niet-actieve tijd Hallo percentages verlaagde (nice) prioriteit
PercentPrivilegedTime | Niet-actieve tijd Hallo percentages in de beschermde (kernel) modus

Hallo moeten eerste vier items optellen too100%. Hallo laatste prestatiemeteritems drie ook som too100%; ze Verdeel Hallo som van PercentProcessorTime PercentIOWaitTime en PercentInterruptTime.

instellen van een enkele metrische gegevens geaggregeerd tot alle processors tooobtain `"condition": "IsAggregate=TRUE"`. tooobtain een waarde voor een specifieke processor, zoals Hallo tweede logische processor van een vier VM, core ingesteld `"condition": "Name=\\"1\\""`. De logische processor-nummers zijn in Hallo bereik `[0..n-1]`.

### <a name="builtin-metrics-for-hello-memory-class"></a>ingebouwde metrische gegevens voor Hallo geheugen-klasse

Hallo geheugen klasse van metrische gegevens bevat informatie over geheugengebruik, paginering en wisselen.

Prestatiemeteritems | Betekenis
------- | -------
AvailableMemory | Beschikbaar fysiek geheugen in MiB
PercentAvailableMemory | Beschikbaar fysiek geheugen als percentage van het totale geheugen
UsedMemory | Gebruik fysiek geheugen (MiB)
PercentUsedMemory | Fysiek geheugen in gebruik als een percentage van het totale geheugen
PagesPerSec | Totaal aantal paginering (lezen/schrijven)
PagesReadPerSec | Pagina's lezen uit een back-up store (wisselbestand, programmabestand, toegewezen bestand, enz.)
PagesWrittenPerSec | Toobacking geschreven pagina's opslaan (wisselbestand, toegewezen bestand, enz.)
AvailableSwap | Niet-gebruikte wisselruimte (MiB)
PercentAvailableSwap | Niet-gebruikte wisselruimte als percentage van de totale wisselruimte
UsedSwap | Gebruik wisselruimte (MiB)
PercentUsedSwap | In gebruik wisselruimte als percentage van de totale wisselruimte

Deze klasse van metrische gegevens heeft slechts één exemplaar. Hallo 'voorwaarde'-kenmerk heeft geen nuttig instellingen en moet worden weggelaten.

### <a name="builtin-metrics-for-hello-network-class"></a>ingebouwde metrische gegevens voor Hallo netwerkklasse

Hallo netwerkklasse van metrische gegevens bevat informatie over activiteit op het netwerk op een afzonderlijke netwerkinterfaces sinds het opstarten. LAD maakt geen metrische gegevens bandbreedte, die worden opgehaald van de host metrische gegevens beschikbaar.

Prestatiemeteritems | Betekenis
------- | -------
BytesTransmitted | Totaal aantal bytes dat is verzonden sinds het opstarten
BytesReceived | Totaal aantal bytes dat is ontvangen sinds het opstarten
BytesTotal | Totaal aantal bytes verzonden of ontvangen sinds het opstarten
PacketsTransmitted | Totale aantal pakketten dat is verzonden sinds opstarten
PacketsReceived | Totale aantal pakketten ontvangen sinds het opstarten
TotalRxErrors | Aantal ontvangen fouten sinds opstarten
TotalTxErrors | Aantal verzonden fouten sinds opstarten
TotalCollisions | Aantal conflicten die zijn gerapporteerd door Hallo netwerkpoorten sinds opstarten

 Hoewel deze klasse wordt verwezen, is LAD ondersteunt geen vastleggen netwerk metrische gegevens die worden getotaliseerd over alle netwerkapparaten. Stel tooobtain Hallo metrische gegevens voor een specifieke interface, zoals eth0, `"condition": "InstanceID=\\"eth0\\""`.

### <a name="builtin-metrics-for-hello-filesystem-class"></a>ingebouwde metrische gegevens voor Hallo Filesystem-klasse

Hallo Filesystem-klasse van metrische gegevens bevat informatie over het gebruik van het bestandssysteem. Absolute en het percentage waarden worden gerapporteerd als ze weergegeven tooan gewone gebruiker (geen hoofdmap worden zouden).

Prestatiemeteritems | Betekenis
------- | -------
FreeSpace | Beschikbare schijfruimte in bytes
UsedSpace | Gebruikte schijfruimte in bytes
PercentFreeSpace | Percentage vrije ruimte
PercentUsedSpace | Percentage gebruikte ruimte
PercentFreeInodes | Percentage van de niet-gebruikte inodes
PercentUsedInodes | Percentage van toegewezen (in gebruik) inodes getotaliseerd over alle bestandssystemen
BytesReadPerSecond | Gelezen bytes per seconde
BytesWrittenPerSecond | Bytes per seconde geschreven
BytesPerSecond | Bytes lezen of schrijven per seconde
ReadsPerSecond | Leesbewerkingen per seconde
WritesPerSecond | Schrijfbewerkingen per seconde
TransfersPerSecond | Lees- of schrijfbewerkingen per seconde

Geaggregeerde waarden in alle bestandssystemen kunnen worden verkregen door het instellen van `"condition": "IsAggregate=True"`. Waarden voor een specifieke gekoppelde bestandssysteem, zoals ' / mnt ', kan worden verkregen door het instellen van `"condition": 'Name="/mnt"'`.

### <a name="builtin-metrics-for-hello-disk-class"></a>ingebouwde metrische gegevens voor Hallo schijf klasse

Hallo schijf klasse van metrische gegevens bevat informatie over schijfgebruik van het apparaat. Deze statistieken van toepassing toohello hele station. Als er meerdere bestandssystemen op een apparaat, zijn Hallo tellers voor dat apparaat in feite getotaliseerd over alle mappen.

Prestatiemeteritems | Betekenis
------- | -------
ReadsPerSecond | Leesbewerkingen per seconde
WritesPerSecond | Schrijfbewerkingen per seconde
TransfersPerSecond | Totaal aantal bewerkingen per seconde
AverageReadTime | Gemiddeld aantal seconden per leesbewerking
AverageWriteTime | Gemiddeld aantal seconden per schrijfbewerking
AverageTransferTime | Gemiddeld aantal seconden per bewerking
AverageDiskQueueLength | Gemiddeld aantal bewerkingen in de wachtrij schijven
ReadBytesPerSecond | Aantal gelezen bytes per seconde
WriteBytesPerSecond | Aantal bytes per seconde geschreven
BytesPerSecond | Aantal bytes gelezen of geschreven per seconde

Geaggregeerde waarden over alle schijven kunnen worden verkregen door het instellen van `"condition": "IsAggregate=True"`. informatie voor een specifiek apparaat (bijvoorbeeld/dev/sdf1), tooget ingesteld `"condition": "Name=\\"/dev/sdf1\\""`.

## <a name="installing-and-configuring-lad-30-via-cli"></a>Installeren en configureren van LAD 3.0 via CLI

Ervan uitgaande dat uw beveiligde instellingen zijn in Hallo bestand PrivateConfig.json en uw openbare configuratiegegevens PublicConfig.json, deze opdracht uitvoeren:

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

Hallo-opdracht wordt ervan uitgegaan dat u hello Azure Resource Management-modus (arm) van hello Azure CLI. tooconfigure LAD voor de implementatie van het klassieke model (ASM) virtuele machines, te schakelen 'asm'-modus (`azure config mode asm`) en Hallo Resourcegroepnaam in Hallo opdracht weglaten. Zie voor meer informatie, Hallo [platformoverschrijdende CLI documentatie](https://docs.microsoft.com/azure/xplat-cli-connect).

## <a name="an-example-lad-30-configuration"></a>Een voorbeeldconfiguratie LAD 3.0

Op basis van de voorgaande definities, hier van een configuratie voor uitbreiding LAD 3.0 voorbeeld met een verklaring Hallo. tooapply dit geval tooyour, u moet de naam van uw eigen opslagaccount gebruiken, account-SAS-token en EventHubs SAS-tokens.

### <a name="privateconfigjson"></a>PrivateConfig.json

Deze persoonlijke instellingen configureren:

* een opslagaccount
* een overeenkomende account-SAS-token
* verschillende Put (JsonBlob of EventHubs met SAS-tokens)

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a>PublicConfig.json

Deze instellingen voor openbare veroorzaken LAD naar:

* Percentage processortijd en gebruikte schijfruimte metrische gegevens toohello uploaden `WADMetrics*` tabel
* Uploaden van berichten van syslog-faciliteit 'gebruiker' en de ernst 'info' toohello `LinuxSyslog*` tabel
* Uploaden van onbewerkte OMI query resultaten (PercentProcessorTime en PercentIdleTime) toohello met de naam `LinuxCPU` tabel
* Toegevoegde regels in bestand uploaden `/var/log/myladtestlog` toohello `MyLadTestLog` tabel

In elk geval gegevens ook naar geüpload:

* Azure Blob-opslag (containernaam is zoals gedefinieerd in Hallo JsonBlob sink)
* EventHubs-eindpunt (zoals opgegeven in Hallo EventHubs sink)

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

Hallo `resourceId` Hallo configuratie overeenkomt met dat van Hallo VM of Hallo virtuele-machineschaalset ingesteld.

* Azure-platform metrische gegevens voor grafieken en waarschuwingen kent Hallo resourceId Hallo VM waarmee u werkt. Deze verwacht toofind Hallo gegevens voor uw virtuele machine met behulp van Hallo resourceId Hallo zoeksleutel.
* Als u Azure automatisch schalen, Hallo resourceId in Hallo automatisch schalen configuratie, moet overeenkomen met Hallo resourceId door LAD gebruikt.
* Hallo resourceId is ingebouwd in Hallo namen van JsonBlobs door LAD geschreven.

## <a name="view-your-data"></a>Bekijk uw gegevens

Prestatiegegevens van de Azure portal tooview hello gebruiken of waarschuwingen instellen:

![Afbeelding](./media/diagnostic-extension/graph_metrics.png)

Hallo `performanceCounters` gegevens altijd worden opgeslagen in een tabel met Azure Storage. Azure Storage-API's zijn beschikbaar voor veel talen en platforms.

Gegevens die worden verzonden tooJsonBlob put wordt opgeslagen in blobs in Hallo storage-account met de naam in Hallo [beveiligde instellingen](#protected-settings). U kunt Hallo blob-gegevens met behulp van een Azure Blob Storage-API's gebruiken.

Bovendien kunt u deze gebruikersinterface extra tooaccess Hallo gegevens in Azure Storage:

* Visual Studio Server Explorer.
* [Microsoft Azure Opslagverkenner](https://azurestorageexplorer.codeplex.com/ "Azure Opslagverkenner").

Deze momentopname van een sessie van Microsoft Azure Storage Explorer toont hello Azure Storage-tabellen en containers gegenereerd vanuit een juist geconfigureerde LAD 3.0-extensie op een virtuele testmachine. Hallo installatiekopie komt niet overeen met exact met Hallo [LAD 3.0 voorbeeldconfiguratie](#an-example-lad-30-configuration).

![Afbeelding](./media/diagnostic-extension/stg_explorer.png)

Zie de relevante Hallo [EventHubs-documentatie](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn hoe tooconsume berichten tooan EventHubs eindpunt gepubliceerd.

## <a name="next-steps"></a>Volgende stappen

* Maken van metrische waarschuwingen in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) van Hallo metrische gegevens die u hebt verzameld.
* Maak [grafieken bewaking](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) voor uw metrische gegevens.
* Meer informatie over hoe te[maken van een virtuele-machineschaalset](/azure/virtual-machines/linux/tutorial-create-vmss) met behulp van de metrische gegevens toocontrol automatisch schalen.
