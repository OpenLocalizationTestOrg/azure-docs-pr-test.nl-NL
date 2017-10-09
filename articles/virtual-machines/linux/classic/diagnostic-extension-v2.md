---
title: een Linux-VM met een VM-extensie aaaMonitoring | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Linux-extensie voor diagnostische toomonitor Hallo prestaties en diagnostische gegevens van een Linux-VM in Azure.
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a>Gebruik Hallo Linux-extensie voor diagnostische toomonitor Hallo prestaties en diagnostische gegevens van een Linux-VM

Dit document beschrijft versie 2.3 Hallo diagnostische Linux-extensie.

> [!IMPORTANT]
> Deze versie is afgeschaft en wordt niet gepubliceerd elk gewenst moment na 30 juni 2018. Het is vervangen door versie 3.0. Zie voor meer informatie, Hallo [documentatie voor versie 3.0 Hallo Linux diagnostische extensie](../diagnostic-extension.md).

## <a name="introduction"></a>Inleiding

(**Opmerking**: Hallo diagnostische Linux-extensie is open source op [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) waarop Hallo meest actuele informatie over het Hallo-extensie voor het eerst wordt gepubliceerd. Kunt u toocheck hello [GitHub-pagina](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) eerste.)

Hallo Linux diagnostische uitbreiding kunt u een gebruiker monitor Hallo virtuele Linux-machines die worden uitgevoerd op Microsoft Azure. Er Hallo volgende mogelijkheden:

* Verzamelt en uploadt Hallo informatie over de systeemprestaties van Hallo Linux VM toohello van gebruiker opslag tabel, met inbegrip van diagnose- en syslog-informatie.
* Hiermee kunt gebruikers toocustomize Hallo gegevens metrische gegevens die worden verzameld en geüpload.
* Hiermee kunt gebruikers tooupload opgegeven logboek bestanden tooa aangewezen opslag tabel.

In huidige versie Hallo 2.3 omvat Hallo gegevens:

* Alle Linux Rsyslog-Logboeken, met inbegrip van systeem, beveiliging en toepassingslogboeken.
* Alle systeemgegevens die opgegeven op [Hallo System Center Cross-Platform oplossingen site](https://scx.codeplex.com/wikipage?title=xplatproviders).
* Door gebruiker opgegeven logboekbestanden.

Deze extensie werkt met zowel klassieke Hallo als Resource Manager-implementatiemodel.

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a>Huidige versie van het Hallo-extensie en afschaffing van oude versies

meest recente versie van de uitbreiding Hallo Hallo is **2.3**, en **eventuele oude versies (2.0, 2.1 en 2.2) wordt afgeschaft en niet-gepubliceerde einde van dit jaar (2017)**. Als u Hallo Linux diagnose uitbreiding geïnstalleerd met automatische secundaire versie upgrade uitgeschakeld, het raadzaam dat u Hallo uitbreiding verwijderen en opnieuw installeren met de upgrade van secundaire versie automatisch ingeschakeld. Op klassieke virtuele machines (ASM), kunt u dit doen door op te geven '2.*' hello versie als u de extensie Hallo via Azure XPLAT CLI of Powershell installeert. Op virtuele machines ARM, u kunt dit doen door op te nemen ' 'autoUpgradeMinorVersion': true' in hello VM-sjabloon voor implementatie. Ook hebt een nieuwe installatie van Hallo uitbreiding Hallo automatisch secundaire versie upgraden optie is ingeschakeld.

## <a name="enable-hello-extension"></a>Hallo-extensie inschakelen

U kunt deze uitbreiding inschakelen met behulp van Hallo [Azure-portal](https://portal.azure.com/#), Azure PowerShell of Azure CLI-scripts.

tooview en Hallo systeem configureren en rechtstreeks prestatiegegevens van hello Azure-portal, volg [deze stappen uit op Hallo Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).

In dit artikel is gericht op het tooenable en Hallo-uitbreiding configureren met behulp van Azure CLI-opdrachten. Hiermee kunt u tooread en bekijkt hello-gegevens direct vanuit Hallo opslag tabel.

Houd er rekening mee dat Hallo configuratiemethoden die hier worden beschreven, niet voor hello Azure-portal werkt. tooview en Hallo systeem- en -gegevens rechtstreeks vanuit hello Azure-portal configureren, Hallo-uitbreiding moet worden ingeschakeld via het Hallo-portal.

## <a name="prerequisites"></a>Vereisten

* **Azure Linux Agent versie 2.0.6 of hoger**.

  Opmerking dat de meeste Azure VM Linux-afbeeldingen versie 2.0.6 bevatten of hoger. U kunt uitvoeren **WAAgent-versie** tooconfirm welke versie is geïnstalleerd op Hallo VM. Als u een versie die ouder is dan 2.0.6 van Hallo VM wordt uitgevoerd, kunt u volgen [deze instructies op GitHub](https://github.com/Azure/WALinuxAgent "instructies") tooupdate deze.
* **Azure CLI**. Ga als volgt [in deze richtlijnen voor het installeren van de CLI](../../../cli-install-nodejs.md) tooset hello Azure CLI-omgeving op uw computer. Nadat u Azure CLI hebt geïnstalleerd, kunt u Hallo **azure** via de opdrachtregelinterface (Bash, Terminal of een opdrachtprompt) tooaccess hello Azure CLI-opdrachten. Bijvoorbeeld:

  * Voer **azure vm-extensie set--help** voor gedetailleerde help-informatie.
  * Voer **azure-aanmelding** toosign in tooAzure.
  * Voer **azure vm lijst** toolist alle virtuele machines die u op Azure hebt Hallo.
* Een storage account toostore Hallo-gegevens. U moet de naam van een account dat eerder is gemaakt en een toegang tot belangrijke tooupload Hallo gegevens tooyour opslag.

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a>Hello Azure CLI opdracht tooenable Hallo Linux diagnostische uitbreiding gebruiken

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a>Scenario 1. Hallo-extensie met Hallo standaardgegevensset inschakelen

In versie 2.3 of hoger bevat de Hallo standaardgegevens die worden verzameld:

* Alle Rsyslog gegevens (inclusief systeem, beveiliging en toepassingslogboeken).  
* Een kernset aan de basisgegevens van het systeem. Let op Hallo van volledige gegevensset wordt beschreven op Hallo [System Center Cross-Platform oplossingen site](https://scx.codeplex.com/wikipage?title=xplatproviders).
  Als u wilt dat tooenable extra gegevens verder met Hallo stappen in scenario's 2 en 3.

Step 1. Maak een bestand met de naam PrivateConfig.json Hello volgende inhoud:

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

Stap 2. Voer  **azure vm-extensie ingesteld vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --persoonlijke configuratiepad PrivateConfig.json**.

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a>Scenario 2. Maatstaven voor prestaties monitor Hallo aanpassen

Deze sectie beschrijft hoe toocustomize Hallo prestaties en diagnostische gegevenstabel.

Step 1. Maak een bestand met de naam PrivateConfig.json met Hallo-inhoud die is beschreven in Scenario 1. Ook een bestand met de naam PublicConfig.json maken. Geef gegevens op bepaalde Hallo gewenste toocollect.

Voor alle ondersteunde providers en variabelen te verwijzen naar Hallo [System Center Cross-Platform oplossingen site](https://scx.codeplex.com/wikipage?title=xplatproviders). U kunt meerdere query's en deze opslaan op meerdere tabellen door meer query's toohello script toe te voegen.

Standaard wordt altijd Hallo Rsyslog gegevens verzameld.

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


Stap 2. Voer  **azure vm-extensie ingesteld vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*'--persoonlijke configuratiepad PrivateConfig.json--openbare configuratiepad PublicConfig.json**.

### <a name="scenario-3-upload-your-own-log-files"></a>Scenario 3. Uploaden van uw eigen logboekbestanden

Deze sectie beschrijft hoe toocollect en uploaden specifieke tooyour storage-account logboekbestanden. U moet beide Hallo tooyour logboek bestands- en Hallo padnaam van Hallo tabel waar u toostore uw logboek toospecify. U kunt meerdere logboekbestanden maken door meerdere toohello script van de tabel file/vermeldingen toe te voegen.

Step 1. Maak een bestand met de naam PrivateConfig.json met Hallo-inhoud die is beschreven in Scenario 1. Maakt u een ander bestand met de naam PublicConfig.json met Hallo volgende inhoud:

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

Stap 2. Voer `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json` uit.

Houd er rekening mee dat met deze instelling op Hallo extensie versies voorafgaande too2.3, alle logboeken geschreven te`/var/log/mysql.err` te kunnen worden gedupliceerd`/var/log/syslog` (of `/var/log/messages` , afhankelijk van Hallo Linux distro) ook. Als u deze dubbele logboekregistratie tooavoid wilt, kunt u het vastleggen van uitsluiten `local6` faciliteit wordt geregistreerd in de configuratie van uw rsyslog. Het Hallo Linux distro afhangt, maar op een systeem Ubuntu 14.04 Hallo bestand toomodify is `/etc/rsyslog.d/50-default.conf` en kunt u de regel Hallo vervangen `*.*;auth,authpriv.none -/var/log/syslog` te`*.*;auth,authpriv,local6.none -/var/log/syslog`. Dit probleem is opgelost in Hallo nieuwste hotfix release van 2.3 (2.3.9007), dus als er Hallo extensie versie 2.3, dit probleem niet moet gebeuren. Als dit wel nog steeds zelfs na het opnieuw opstarten van uw virtuele machine, contact met ons opnemen en help ons waarom Hallo nieuwste hotfixversie niet automatisch wordt geïnstalleerd.

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a>Scenario 4. Hallo-extensie van de logboekbestanden verzamelen stoppen

Deze sectie beschrijft hoe toostop Hallo-extensie van het verzamelen van Logboeken. Let op: Hallo bewakingsproces agent wordt nog steeds actief en werkend worden zelfs met deze herconfiguratie. Als u toostop Hallo agentproces volledig bewaking wilt, kunt u dit doen door het uitschakelen van extensie is Hallo. Hallo opdracht toodisable Hallo extensie is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.

Step 1. Maak een bestand met de naam PrivateConfig.json met Hallo-inhoud die is beschreven in Scenario 1. Maak een ander bestand met de naam PublicConfig.json met Hallo volgende inhoud:

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


Stap 2. Voer  **azure vm-extensie ingesteld vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*'--persoonlijke configuratiepad PrivateConfig.json--openbare configuratiepad PublicConfig.json**.

## <a name="review-your-data"></a>Controleer uw gegevens

Hallo prestaties en diagnostische gegevens worden opgeslagen in een tabel met Azure Storage. Bekijk [hoe toouse Azure Table Storage met Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn tooaccess Hallo gegevens in de opslag van de Hallo tabel weergeven met behulp van Azure CLI-scripts.

Bovendien kunt u na UI extra tooaccess Hallo gegevens:

1. Visual Studio Server Explorer. Ga tooyour storage-account. Nadat het Hallo VM wordt uitgevoerd gedurende vijf minuten, ziet u vier Hallo standaardtabellen: 'LinuxCpu', 'LinuxDisk', 'LinuxMemory' en 'Linuxsyslog'. Dubbelklik op Hallo namen tooview Hallo tabelgegevens.
1. [Azure Opslagverkenner](https://azurestorageexplorer.codeplex.com/ "Azure Opslagverkenner").

![Afbeelding](./media/diagnostic-extension/no1.png)

Als u fileCfg of perfCfg (zoals beschreven in scenario's 2 en 3) hebt ingeschakeld, kunt u Visual Studio Server Explorer en Azure Storage Explorer tooview niet-standaard gegevens.

## <a name="known-issues"></a>Bekende problemen

* Hallo Rsyslog informatie en logboekbestand klant opgegeven alleen toegankelijk via het uitvoeren van scripts.
