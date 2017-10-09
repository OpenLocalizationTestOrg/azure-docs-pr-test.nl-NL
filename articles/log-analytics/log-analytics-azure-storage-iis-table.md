---
title: aaaUse blob storage voor IIS en tabel opslag voor gebeurtenissen in de Azure Log Analytics | Microsoft Docs
description: Log Analytics kunt lezen Hallo-logboeken voor Azure-services die diagnostics tootable opslag schrijven of IIS-logboeken geschreven tooblob opslag.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a>Azure blob storage gebruiken voor IIS en Azure-tabelopslag voor gebeurtenissen met Log Analytics

Log Analytics kunt lezen Hallo-logboeken voor Hallo services die schrijven diagnostics tootable opslag of IIS-logboeken geschreven tooblob opslag te volgen:

* Service Fabric-clusters (Preview)
* Virtuele machines
* Web/werkrollen

Voordat u Log Analytics kunt verzamelen van gegevens voor deze bronnen, kan Azure diagnostics moet zijn ingeschakeld.

Als diagnostische gegevens zijn ingeschakeld, kunt u hello Azure-portal of PowerShell logboekanalyse toocollect Hallo logboeken configureren.

Azure Diagnostics is een Azure-uitbreiding waarmee u toocollect diagnostische gegevens van een werkrol, Webrol of virtuele machine in Azure wordt uitgevoerd. Hallo-gegevens worden opgeslagen in Azure storage-account en vervolgens kan worden verzameld door Log Analytics.

Voor logboekanalyse toocollect deze logboeken Azure Diagnostics Hallo logboeken moet in de volgende locaties Hallo:

| Logboektype | Resourcetype | Locatie |
| --- | --- | --- |
| IIS-logboeken |Virtuele machines <br> Web-rollen <br> Werkrollen |af-iis-logboekbestanden (Blob-opslag) |
| Syslog |Virtuele machines |LinuxsyslogVer2v0 (tabel opslag) |
| Operationele gebeurtenissen van de service Fabric |Service Fabric-knooppunten |WADServiceFabricSystemEventTable |
| Gebeurtenissen van de service Fabric betrouwbare Actor |Service Fabric-knooppunten |WADServiceFabricReliableActorEventTable |
| Gebeurtenissen van betrouwbare Service voor service Fabric |Service Fabric-knooppunten |WADServiceFabricReliableServiceEventTable |
| Windows-gebeurtenislogboeken |Service Fabric-knooppunten <br> Virtuele machines <br> Web-rollen <br> Werkrollen |WADWindowsEventLogsTable (Table Storage) |
| Logboeken van Windows (ETW) |Service Fabric-knooppunten <br> Virtuele machines <br> Web-rollen <br> Werkrollen |WADETWEventTable (Table Storage) |

> [!NOTE]
> IIS-logboeken van Azure Websites worden momenteel niet ondersteund.
>
>

Voor virtuele machines die u hebt de optie Hallo Hallo installeren [logboekanalyse agent](log-analytics-azure-vm-extension.md) in uw virtuele machine tooenable extra inzichten. Bovendien kunt u aanvullende analyse, waaronder configuratie bijhouden, SQL-evaluatie en update-evaluatie uitvoeren toobeing kunnen tooanalyze IIS-logboeken en gebeurtenislogboeken.

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a>Inschakelen van Azure diagnostics in een virtuele machine voor het logboek met systeemgebeurtenissen en IIS Meld verzameling
Gebruik hello te volgen procedure tooenable Azure diagnostics in een virtuele machine voor het logboek met systeemgebeurtenissen en IIS Meld u met behulp van Microsoft Azure-portal Hallo verzameling.

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a>tooenable Azure diagnostische gegevens in een virtuele machine met hello Azure-portal
1. Hallo VM-Agent installeren wanneer u een virtuele machine maken. Als Hallo virtuele machine al bestaat, controleert u dat Hallo die VM-Agent is al geïnstalleerd.

   * In hello Azure-portal, gaat u toohello virtuele machine, selecteert u **optionele configuratie**, klikt u vervolgens **Diagnostics** en stel **Status** te**op**.

     Na voltooiing heeft Hallo VM hello Azure Diagnostics extensie geïnstalleerd en uitgevoerd. Deze uitbreiding is verantwoordelijk voor het verzamelen van diagnostische gegevens.
2. Controle inschakelen en configureren van logboekregistratie in een bestaande virtuele machine. U kunt diagnostische gegevens op Hallo VM-niveau inschakelen. tooenable diagnostische gegevens en configureer vervolgens de logboekregistratie van gebeurtenissen, voert u Hallo stappen te volgen:

   1. Selecteer Hallo VM.
   2. Klik op **bewaking**.
   3. Klik op **Diagnostics**.
   4. Set Hallo **Status** te**ON**.
   5. Selecteer elk diagnostics logboek dat u wilt dat toocollect.
   6. Klik op **OK**.

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a>Inschakelen van Azure diagnostics in een Webrol voor IIS-logboek en gebeurtenis-verzameling
Raadpleeg te[hoe diagnostische gegevens in een Cloudservice tooEnable](../cloud-services/cloud-services-dotnet-diagnostics.md) voor algemene stappen over het inschakelen van Azure diagnostics. Hallo onderstaande instructies deze gegevens gebruiken en aanpassen voor gebruik met logboekanalyse.

Met Azure diagnostics ingeschakeld:

* IIS-logboeken worden standaard opgeslagen met logboekgegevens op Hallo scheduledTransferPeriod overdrachtsinterval overgedragen.
* Windows-gebeurtenislogboeken worden standaard niet worden overgedragen.

### <a name="tooenable-diagnostics"></a>tooenable diagnostische gegevens
Windows-gebeurtenislogboeken tooenable of toochange Hallo scheduledTransferPeriod, configureren van Azure Diagnostics Hallo XML-configuratiebestand (diagnostics.wadcfg), zoals wordt weergegeven in [stap 4: maken van uw configuratiebestand diagnostische gegevens en Hallo installeren de extensie](../cloud-services/cloud-services-dotnet-diagnostics.md)

Hallo verzamelt volgende voorbeeldconfiguratiebestand IIS-logboeken en alle gebeurtenissen van Hallo toepassing en het systeemlogboek in Logboeken:

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

Zorg ervoor dat uw ConfigurationSettings geeft u een opslagaccount, zoals in het volgende voorbeeld Hallo:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

Hallo **AccountName** en **AccountKey** waarden zijn gevonden in hello Azure-portal op Hallo storage account dashboard onder toegangssleutels beheren. Hallo-protocol voor het Hallo-verbindingsreeks moet **https**.

Nadat bijgewerkte diagnostische configuratie Hallo is toegepast wordt tooyour cloudservice en het geschreven diagnostics tooAzure opslag, en u bent klaar tooconfigure logboekanalyse.

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a>Hello Azure portal toocollect logboeken van Azure Storage gebruiken
U kunt hello Azure portal tooconfigure logboekanalyse toocollect Hallo Logboeken kunt gebruiken voor hello Azure-services te volgen:

* Service Fabric-clusters
* Virtuele machines
* Web/werkrollen

Werkruimte voor logboekanalyse tooyour navigeren in hello Azure-portal, en Hallo volgende taken uitvoeren:

1. Klik op *opslagaccounts Logboeken*
2. Klik op Hallo *toevoegen* taak
3. Selecteer Hallo opslagaccount waarin Hallo diagnostische logboeken
   * Dit account kan worden een klassieke storage-account of een Azure Resource Manager-storage-account
4. Selecteer Hallo gewenste toocollect logboeken voor gegevenstype
   * Hallo-opties zijn IIS-logboeken; Gebeurtenissen; Syslog (Linux); ETW-Logboeken; Service Fabric-gebeurtenissen
5. Hallo-waarde voor de gegevensbron wordt automatisch ingevuld op basis van Hallo gegevenstype en kan niet worden gewijzigd
6. Klik op OK toosave Hallo configuratie

Herhaal stappen 2 tot en met 6 voor extra opslagruimte accounts en gegevenstypen die u wilt dat Log Analytics toocollect.

U bent kunnen toosee gegevens van Hallo storage-account in logboekanalyse in ongeveer 30 minuten. U ziet alleen de gegevens die worden geschreven toostorage nadat Hallo-configuratie is toegepast. Log Analytics biedt Hallo bestaande gegevens niet lezen uit Hallo storage-account.

> [!NOTE]
> Hallo portal die Hallo-bron in Hallo storage-account bestaat niet valideren of als er nieuwe gegevens worden geschreven.
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a>Inschakelen van Azure diagnostics in een virtuele machine voor het logboek met systeemgebeurtenissen en IIS Meld verzameling met behulp van PowerShell
Gebruik Hallo stappen in [tooindex logboekanalyse configureren van Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread van Azure diagnostics die tootable opslag zijn geschreven.

Met Azure PowerShell kunt u preciezer Hallo gebeurtenissen opgeven die tooAzure opslag zijn geschreven.
Zie voor meer informatie [Diagnostics inschakelen in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).

U kunt inschakelen en Azure diagnostics met behulp van de volgende PowerShell-script Hallo bijwerken.
U kunt dit script ook gebruiken met een aangepaste configuratie voor logboekregistratie.
Hallo script tooset Hallo storage-account, servicenaam en de naam van de virtuele machine wijzigen.
Hallo script maakt gebruik van cmdlets voor klassieke virtuele machines.

Hallo volgende voorbeeldscript bekijken, kopieert u deze zo nodig wijzigen, Hallo voorbeeld opslaan als een PowerShell-scriptbestand en vervolgens Hallo-script uitvoeren.

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a>Volgende stappen
* [Verzamelen van Logboeken en metrische gegevens voor Azure-services](log-analytics-azure-storage.md) voor ondersteunde Azure-services.
* [Inschakelen van oplossingen](log-analytics-add-solutions.md) tooprovide inzicht in Hallo-gegevens.
* [Gebruik zoekquery's](log-analytics-log-searches.md) tooanalyze Hallo gegevens.
