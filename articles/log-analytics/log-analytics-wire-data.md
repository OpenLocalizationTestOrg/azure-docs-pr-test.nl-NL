---
title: aaaWire oplossing in Log Analytics | Microsoft Docs
description: Draadgegevens worden geleverd zijn geconsolideerde netwerk en de prestaties gegevens van computers met OMS-agent, met inbegrip van Operations Manager en verbonden met een Windows-agents. Gegevens van het netwerk wordt gecombineerd met uw logboek gegevens toohelp u correleren van gegevens.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a>Kabel gegevens 2.0 (Preview)-oplossing in Log Analytics

![Kabel gegevens symbool](./media/log-analytics-wire-data/wire-data2-symbol.png)

Draadgegevens worden geleverd is geconsolideerde netwerk en de prestaties van gegevens van computers met OMS-agents, waaronder Operations Manager, Windows verbonden en Linux-agents. Gegevens van het netwerk wordt gecombineerd met de andere logboek gegevens toohelp u correleren van gegevens.

Bovendien tooOMS agents, Hallo Draadgegevens worden geleverd oplossing maakt gebruik van Microsoft Dependency agents die u op computers in uw IT-infrastructuur installeert. Afhankelijkheid Agents monitor netwerk verzonden gegevens tooand van uw computers voor netwerk in Hallo 2-3 niveaus [OSI-model](https://en.wikipedia.org/wiki/OSI_model), met inbegrip van Hallo verschillende protocollen en poorten die worden gebruikt. Gegevens worden vervolgens tooLog Analytics verzonden met behulp van agents.

> [!NOTE]
> U kunt geen eerdere versie van Hallo Draadgegevens worden geleverd oplossing toonew werkruimten Hallo toevoegen. Als u Hallo oorspronkelijke Draadgegevens worden geleverd oplossing is ingeschakeld hebt, kunt u toouse blijven deze. Echter toouse kabel gegevens 2.0, moet u eerst verwijderen Hallo oorspronkelijke versie.

Standaard verzamelt logboekanalyse logboekgegevens voor CPU, geheugen, schijf en netwerk prestatiegegevens van items die zijn ingebouwd in Windows. Netwerk- en andere gegevensverzameling is uitgevoerd realtime voor elke agent, met inbegrip van subnetten en op toepassingsniveau-protocollen die worden gebruikt door Hallo-computer. U kunt andere prestatiemeteritems toevoegen op de instellingenpagina Hallo van tabblad Hallo-Logboeken.

Als u hebt gebruikt [sFlow](http://www.sflow.org/) of andere software met [Cisco NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), vervolgens Hallo statistieken is en gegevens die u in de kabel gegevens zien bekend tooyou.

Hallo typen ingebouwde logboek zoekquery's zijn onder andere:

- Agents waarmee draadgegevens worden
- IP-adres van de agents waarmee draadgegevens worden geleverd
- Uitgaande communicatie per IP-adressen
- Aantal verzonden bytes per toepassingsprotocollen
- Aantal bytes dat door een toepassingsservice is verzonden
- Bytes ontvangen door verschillende protocollen
- Totaal aantal bytes verzonden en ontvangen door de IP-versie
- Gemiddelde latentie voor verbindingen die betrouwbaar zijn gemeten
- Computerprocessen die gestart of ontvangen van netwerkverkeer
- Hoeveelheid netwerkverkeer voor een proces

Wanneer u met draadgegevens worden geleverd zoekt, kunt u filteren en gegevens tooview groepsgegevens Hallo bovenste agents en bovenste protocollen. Of u kunt bekijken wanneer bepaalde computers (IP-adressen/MAC-adressen) gecommuniceerd met elkaar, hoe lang en hoeveel gegevens zijn verzonden, in principe u metagegevens over het netwerkverkeer, op basis van een zoekopdracht bekijken.

Aangezien u metagegevens bekijkt, is het echter niet per se nuttig is voor de diepgaande probleemoplossing. Draadgegevens worden geleverd in logboekanalyse is niet een volledige vastleggen van gegevens van het netwerk. Het dus niet bedoeld voor het oplossen van diep pakketniveau. Hallo voordeel van het gebruik van de agent hello, tooother verzameling methoden vergeleken, is dat u niet tooinstall toestellen hebt, opnieuw configureren van uw netwerkswitches of complexe configuraties uitvoeren. Draadgegevens worden geleverd is gewoon op agent gebaseerde — u Hallo-agent installeren op een computer en wordt het controleren van een eigen netwerkverkeer. Een ander voordeel is dat u toomonitor werkbelastingen in de cloudproviders of hostserviceprovider of Microsoft Azure wilt, waarbij Hallo gebruiker niet de eigenaar van Hallo fabric laag.

## <a name="connected-sources"></a>Verbonden bronnen

Draadgegevens worden afkomstig de gegevens uit Hallo Microsoft-Agent voor afhankelijkheden. Hallo-Agent voor afhankelijkheden, is afhankelijk van Hallo OMS-Agent voor de verbindingen tooLog Analytics. Dit betekent dat een server Hallo OMS-Agent geïnstalleerd en geconfigureerd eerste moet hebben, en vervolgens u Hallo-Agent voor afhankelijkheden installeert. Hallo beschrijft volgende tabel Hallo verbonden bronnen die ondersteuning biedt voor Hallo Draadgegevens worden geleverd oplossing.

| **Verbonden bron** | **Ondersteund** | **Beschrijving** |
| --- | --- | --- |
| Windows-agents | Ja | Draadgegevens worden geleverd, analyseert en verzamelt gegevens van agent-Windows-computers. <br><br> In aanvulling toohello [OMS-Agent](log-analytics-windows-agents.md), Windows-agents Hallo Microsoft afhankelijkheid Agent vereist. Zie Hallo [ondersteunde besturingssystemen](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) voor een volledige lijst met versies van besturingssystemen. |
| Linux-agents | Ja | Draadgegevens worden geleverd, analyseert en verzamelt gegevens van Linux-agent-computers.<br><br> In aanvulling toohello [OMS-Agent](log-analytics-linux-agents.md), Linux-agents Hallo Microsoft afhankelijkheid Agent vereist. Zie Hallo [ondersteunde besturingssystemen](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) voor een volledige lijst met versies van besturingssystemen. |
| Beheergroep System Center Operations Manager | Ja | Kabel gegevens analyseert en verzamelt gegevens van Windows en Linux-agents in een verbonden [System Center Operations Manager-beheergroep](log-analytics-om-agents.md). <br><br> Een rechtstreekse verbinding tussen Hallo System Center Operations Manager-agent computer tooLog Analytics is vereist. Gegevens doorgestuurd vanaf Hallo management groep tooLog Analytics. |
| Azure Storage-account | Nee | Draadgegevens worden geleverd verzamelt gegevens van computers die door agents, dus er geen gegevens van het zijn toocollect uit Azure Storage. |

Op Windows hello Microsoft Monitoring Agent (MMA) wordt gebruikt door System Center Operations Manager en Log Analytics toogather en gegevens verzenden. Afhankelijk van het Hallo-context wordt Hallo agent Hallo System Center Operations Manager-Agent, OMS-Agent, Log Analytics-Agent, MMA of directe Agent genoemd. System Center Operations Manager en Log Analytics bieden enigszins verschillende versies van Hallo MMA. Deze versies kunnen elk rapport tooSystem Center Operations Manager, tooLog Analytics of tooboth.

Op Linux, Hallo OMS-Agent voor Linux verzamelt en verzendt gegevens tooLog Analytics. U kunt Draadgegevens worden geleverd op servers met OMS Direct Agents of op servers die aangesloten tooLog Analytics via System Center Operations Manager-beheergroepen zijn.

In dit artikel wordt verwezen naar tooall agents, of Linux- of Windows, of System Center Operations Manager-beheergroep verbonden tooa of rechtstreeks tooLog Analytics Hallo worden genoemd _OMS-agent_. We gebruiken Hallo implementatienaam Hallo agent alleen indien nodig voor context.

Hallo-Agent voor afhankelijkheden stuurt de gegevens zelf geen en hoeven niet alle wijzigingen toofirewalls of poorten. Hallo gegevens in Draadgegevens worden altijd verzonden door Hallo OMS-agent tooLog Analytics, ofwel rechtstreeks of met behulp van Hallo OMS-Gateway.

![diagram van agent](./media/log-analytics-wire-data/agents.png)

Als u een System Center Operations Manager-gebruiker met een management groep verbonden tooLog Analytics:

- Er is geen aanvullende configuratie vereist wanneer de System Center Operations Manager-agents Hallo Internet tooconnect tooLog Analytics kunnen openen.
- Wanneer de System Center Operations Manager-agents geen toegang de logboekanalyse via Hallo Internet tot moet u tooconfigure Hallo OMS Gateway toowork met System Center Operations Manager.

Als u Hallo Direct Agent gebruikt, moet u tooconfigure Hallo OMS-agent zelf tooconnect tooLog Analytics of tooyour OMS-Gateway. U kunt Hallo OMS Gateway downloaden van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

## <a name="prerequisites"></a>Vereisten

- Hallo vereist [inzicht en analyse](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) oplossing aanbieding.
- Als u Hallo eerdere versie van Hallo oplossing Draadgegevens worden geleverd, moet u deze eerst verwijderen. Alle gegevens die zijn vastgelegd via Hallo oorspronkelijke Draadgegevens worden geleverd oplossing is echter nog steeds beschikbaar in de kabel gegevens 2.0 en logboek zoeken.
- Administrator-bevoegdheden zijn vereist tooinstall of Hallo-Agent voor afhankelijkheden te verwijderen.
- Hallo-Agent voor afhankelijkheden moet worden geïnstalleerd op een computer met een 64-bits besturingssysteem.

### <a name="operating-systems"></a>Besturingssystemen

Hallo volgende secties geven lijsten Hallo ondersteunde besturingssystemen voor Hallo-Agent voor afhankelijkheden. 32-bits architecturen biedt geen voor elk besturingssysteem ondersteuning voor draadgegevens worden geleverd.

#### <a name="windows-server"></a>Windows Server

- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

#### <a name="windows-desktop"></a>Windows-bureaublad

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux-, CentOS Linux- en Oracle Linux (met RHEL Kernel)

- Alleen standaard en SMP Linux kernel-versies worden ondersteund.
- Niet-standaard kernel versies, zoals PAE en Xen, worden niet ondersteund voor een Linux-distributie. Bijvoorbeeld, een systeem met Hallo release tekenreeks _2.6.16.21-0.8-xen_ wordt niet ondersteund.
- Aangepaste kernels, met inbegrip van hercompilaties van standaard kernels worden niet ondersteund.
- CentOSPlus kernel wordt niet ondersteund.
- Oracle Unbreakable Enterprise Kernel (UEK) wordt in verderop in dit artikel beschreven.

#### <a name="red-hat-linux-7"></a>Red Hat Linux 7

| **De versie van besturingssysteem** | **Kernelversie** |
| --- | --- |
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7.2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6

| **De versie van besturingssysteem** | **Kernelversie** |
| --- | --- |
| 6.0 | 2.6.32-71 |
| 6.1 | 2.6.32-131 |
| 6.2 | 2.6.32-220 |
| 6.3 | 2.6.32-279 |
| 6.4 | 2.6.32-358 |
| 6.5 | 2.6.32-431 |
| 6.6 | 2.6.32-504 |
| 6.7 | 2.6.32-573 |
| 6.8 | 2.6.32-642 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5

| **De versie van besturingssysteem** | **Kernelversie** |
| --- | --- |
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398 <br> 2.6.18-400 <br>2.6.18-402 <br>2.6.18-404 <br>2.6.18-406 <br> 2.6.18-407 <br> 2.6.18-408 <br> 2.6.18-409 <br> 2.6.18-410 <br> 2.6.18-411 <br> 2.6.18-412 <br> 2.6.18-416 <br> 2.6.18-417 <br> 2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux met Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6

| **De versie van besturingssysteem** | **Kernelversie** |
| --- | --- |
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| **De versie van besturingssysteem** | **Kernelversie** |
| --- | --- |
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11

| **De versie van besturingssysteem** | **Kernelversie** |
| --- | --- |
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10

| **De versie van besturingssysteem** | **Kernelversie** |
| --- | --- |
| 10 SP4 | 2.6.16.60 |

#### <a name="dependency-agent-downloads"></a>Agent voor afhankelijkheden gedownload

| **File** | **BESTURINGSSYSTEEM** | **Versie** | **SHA-256** |
| --- | --- | --- | --- |
| [InstallDependencyAgent Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |



## <a name="configuration"></a>Configuratie

Volgende stappen tooconfigure hello Draadgegevens worden geleverd oplossing voor uw werkruimten Hallo uitvoeren.

1. Hallo activiteit Log Analytics-oplossing van Hallo inschakelen [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).
2. Hallo-Agent voor afhankelijkheden op elke computer waar u tooget gegevens wilt installeren. Hallo-Agent voor afhankelijkheden kunt verbindingen tooimmediate neighbors, bewaken, dus u niet een agent op elke computer moet wellicht.

### <a name="install-hello-dependency-agent-on-windows"></a>Hallo-Agent voor afhankelijkheden op Windows installeren

Administrator-bevoegdheden zijn vereist tooinstall of Hallo-agent verwijderen.

Hallo afhankelijkheid Agent is geïnstalleerd op computers waarop Windows wordt uitgevoerd via InstallDependencyAgent Windows.exe. Als u dit uitvoerbare bestand zonder opties uitvoert, wordt er een wizard u tooinstall interactief kunt volgen gestart.

Volgende stappen tooinstall Hallo-Agent voor afhankelijkheden op elke computer met Windows hello gebruiken:

1. Installatie OMS-Agent met behulp van instructies op Hallo Hallo [verbinding maken met Windows-computers toohello Log Analytics-service in Azure](log-analytics-windows-agents.md).
2. Hallo via Hallo-koppeling in de vorige sectie Hallo Windows-agent downloaden en uitvoeren met behulp van de volgende opdracht Hallo: InstallDependencyAgent Windows.exe
3. Ga als volgt Hallo wizard tooinstall Hallo agent.
4. Als het Hallo-Agent voor afhankelijkheden toostart mislukt, controleert u Hallo-logboeken voor uitgebreide foutinformatie. Hallo logboekmap is op Windows-agents %Programfiles%\Microsoft Agent\logs afhankelijkheid.

#### <a name="windows-command-line"></a>Windows-opdrachtregel

Gebruik de opties van Hallo tabel tooinstall vanaf een opdrachtregel te volgen. een lijst met Hallo installatie vlaggen, Hallo installatieprogramma uitvoeren met behulp van Hallo toosee /? markering als volgt.

InstallDependencyAgent Windows.exe /?

| **Vlag** | **Beschrijving** |
| --- | --- |
| <code>/?</code> | Een lijst met opdrachtregelopties Hallo ophalen. |
| <code>/S</code> | Een installatie zonder vragen van de gebruiker op de achtergrond uitvoeren. |

Bestanden voor Windows-Agent voor afhankelijkheden Hallo worden standaard in C:\Program Files\Microsoft afhankelijkheid Agent geplaatst.

### <a name="install-hello-dependency-agent-on-linux"></a>Hallo-Agent voor afhankelijkheden te installeren op Linux

Toegang tot de hoofdmap is vereist tooinstall of Hallo-agent configureren.

Hallo afhankelijkheid Agent is geïnstalleerd op Linux-computers via InstallDependencyAgent-Linux64.bin, een shell-script met een zichzelf uitpakkend binaire waarde. U kunt Hallo bestand uitvoeren met behulp van _servicel_ of Voeg machtigingen toohello bestand zelf.

Volgende stappen tooinstall Hallo-Agent voor afhankelijkheden op elke Linux-computer hello gebruiken:

1. Installatie OMS-Agent met behulp van instructies op Hallo Hallo [verzamelen en beheren van gegevens van Linux-computers](log-analytics-agent-linux.md).
2. Hallo via Hallo-koppeling in de vorige sectie Hallo afhankelijkheid van Linux-agent downloaden en installeer deze vervolgens als hoofdmap met behulp van de volgende opdracht Hallo: servicel InstallDependencyAgent Linux64.bin
3. Als het Hallo-Agent voor afhankelijkheden toostart mislukt, controleert u Hallo-logboeken voor uitgebreide foutinformatie. Op Linux-agents Hallo logboekmap is: /var/opt/microsoft/dependency-agent/log.

een lijst met Hallo installatie vlaggen, Hallo het installatieprogramma uitvoeren met Hallo toosee `-help` markeren als volgt.

```
InstallDependencyAgent-Linux64.bin -help
```

| **Vlag** | **Beschrijving** |
| --- | --- |
| <code>-help</code> | Een lijst met opdrachtregelopties Hallo ophalen. |
| <code>-s</code> | Een installatie zonder vragen van de gebruiker op de achtergrond uitvoeren. |
| <code>--check</code> | Controleer de machtigingen en het Hallo-besturingssysteem, maar geen Hallo-agent installeren. |

Bestanden voor Hallo-Agent voor afhankelijkheden worden geplaatst in Hallo mappen te volgen:

| **Bestanden** | **Locatie** |
| --- | --- |
| Core-bestanden | /Opt/Microsoft/Dependency-agent |
| Logboekbestanden | /var/opt/Microsoft/Dependency-agent/log |
| De config-bestanden | /etc/opt/Microsoft/Dependency-agent/config |
| Uitvoerbare bestanden voor service | /Opt/Microsoft/Dependency-agent/bIn/Microsoft-Dependency-agent<br><br>/Opt/Microsoft/Dependency-agent/bIn/Microsoft-Dependency-Agent-Manager |
| Binaire opslag-bestanden | /var/opt/Microsoft/Dependency-agent/Storage |

### <a name="installation-script-examples"></a>Voorbeelden van scripts voor installatie

tooeasily implementeren Hallo-Agent voor afhankelijkheden op veel servers in één keer, helpt toouse een script. U kunt gebruiken Hallo script voorbeelden toodownload te volgen en Hallo afhankelijkheid Agent installeren op Windows of Linux.

#### <a name="powershell-script-for-windows"></a>Windows PowerShell-script

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a>Shell-script voor Linux

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a>Desired State Configuration

toodeploy Hallo-Agent voor afhankelijkheden via Desired State Configuration, kunt u Hallo xPSDesiredStateConfiguration module en een codefragment Hallo volgende:

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a>Hallo-Agent voor afhankelijkheden verwijderen

Gebruik Hallo volgende secties toohelp u Hallo-Agent voor afhankelijkheden verwijderen.

#### <a name="uninstall-hello-dependency-agent-on-windows"></a>Agent voor afhankelijkheden op Windows hello verwijderen

Een beheerder kan Hallo afhankelijkheid Agent voor Windows via het Configuratiescherm kunt verwijderen.

Een beheerder kan ook %Programfiles%\Microsoft afhankelijkheid Agent\Uninstall.exe toouninstall Hallo-Agent voor afhankelijkheden uitgevoerd.

#### <a name="uninstall-hello-dependency-agent-on-linux"></a>Hallo op Linux-Agent voor afhankelijkheden verwijderen

toocompletely verwijderen Hallo van Linux-Agent voor afhankelijkheden, moet u Hallo agent zelf verwijderen en Hallo connector die wordt automatisch geïnstalleerd met Hallo-agent. U kunt beide via Hallo na één opdracht verwijderen:

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a>Management packs

Wanneer Draadgegevens worden geleverd in een werkruimte voor logboekanalyse is geactiveerd, wordt een 300 KB management pack tooall Hallo Windows-servers in deze werkruimte verzonden. Als u System Center Operations Manager-agents in een [verbonden beheergroep](log-analytics-om-agents.md), Hallo Afhankelijkheidsmonitor management pack van System Center Operations Manager is geïmplementeerd. Als agents Hallo rechtstreeks zijn verbonden, levert logboekanalyse Hallo management pack.

Hallo management pack met de naam Microsoft.IntelligencePacks.ApplicationDependencyMonitor. Deze naar worden geschreven: %Programfiles%\Microsoft bewaking Agent\Agent\Health State\Management servicepacks. Hallo-gegevensbron die gebruikmaakt van Hallo management pack: % Program files%\Microsoft bewaking Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing

**Installeren en configureren van Hallo-oplossing**

Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren.

- Hallo Draadgegevens worden geleverd oplossing verkrijgt gegevens van computers met Windows Server 2012 R2, Windows 8.1 en latere besturingssystemen.
- Microsoft .NET Framework 4.0 of hoger is vereist op computers waar u tooacquire kabel gegevens uit.
- Hallo Draadgegevens worden geleverd oplossing tooyour werkruimte voor logboekanalyse via Hallo-proces dat wordt beschreven in toevoegen [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md). Er is geen verdere configuratie nodig.
- Als u tooview draadgegevens worden geleverd voor een specifieke oplossing wilt, moet u toohave Hallo oplossing is al toegevoegd tooyour werkruimte.

Nadat er agents zijn geïnstalleerd en u Hallo oplossing installeert, wordt Hallo kabel gegevens 2.0-tegel wordt weergegeven in de werkruimte.

> [!NOTE]
> Op dit moment moet u Hallo OMS portal tooview draadgegevens worden geleverd. U kunt hello Azure portal tooview draadgegevens worden niet gebruiken.

![Tegel draadgegevens worden geleverd](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a>Met behulp van de oplossing Hallo kabel gegevens 2.0

Klik in het Hallo-OMS-portal op Hallo **kabel gegevens 2.0** tegel tooopen hello Draadgegevens worden geleverd dashboard. Hallo dashboard bevat Hallo blades Hallo volgende tabel. Elke blade geeft een lijst van too10 items die overeenkomen met die van de blade criteria voor Hallo bereik en tijdbereik opgegeven. U kunt een logboek-zoekquery waarmee alle records door te klikken op uitvoeren **alle** onderin Hallo van Hallo-blade of door te klikken op Hallo blade-header.

| **Blade** | **Beschrijving** |
| --- | --- |
| Agents netwerkverkeer vastleggen | Toont het aantal agents die netwerkverkeer vastlegt Hallo en lijsten Hallo bovenste 10 computers die verkeer vastlegt. Klik op Hallo nummer toorun logboek zoekt <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>. Klik op een computer in Hallo lijst toorun een logboek zoekopdracht retourneren Hallo kunt u het totale aantal bytes dat is vastgelegd. |
| Lokale subnetten | Toont het aantal lokale subnetten die agents gedetecteerd Hallo.  Klik op Hallo nummer toorun logboek zoekt <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> die een lijst met alle subnetten met het aantal bytes dat is verzonden via elke Hallo. Klik op een subnet in Hallo lijst toorun een logboek zoekopdracht Hallo kunt u het totale aantal bytes dat is verzonden via Hallo subnet retourneren. |
| Protocollen op toepassingsniveau | Toont Hallo aantal protocollen op toepassingsniveau in gebruik is, zoals gedetecteerd door agents. Klik op Hallo nummer toorun logboek zoekt <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>. Klik op een protocol toorun een logboek zoekopdracht retourneren Hallo kunt u het totale aantal bytes dat is verzonden via Hallo-protocol. |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Kabel gegevens dashboard](./media/log-analytics-wire-data/wire-data-dash.png)

U kunt Hallo **Agents netwerkverkeer vastleggen** blade toodetermine hoeveel netwerkbandbreedte wordt verbruikt door computers. Deze blade kunt u eenvoudig zoeken Hallo _chattiest_ computer in uw omgeving. Deze computers kunnen worden overbelast abnormaal fungeert, of gebruik meer netwerkbronnen dan normaal.

![Voorbeeld van logboek zoeken](./media/log-analytics-wire-data/log-search-example01.png)

Op deze manier kunt u Hallo **lokale subnetten** blade toodetermine hoeveel netwerkverkeer via de subnetten wordt verplaatst. Gebruikers definiëren vaak subnetten rond de essentiële gebieden voor hun toepassingen. Deze blade biedt een overzicht van deze gebieden.

![Voorbeeld van logboek zoeken](./media/log-analytics-wire-data/log-search-example02.png)

Hallo **protocollen op toepassingsniveau** blade is nuttig omdat het is nuttig weten welke protocollen worden gebruikt. U zou bijvoorbeeld verwachten SSH toonot worden gebruikt in uw netwerkomgeving. Weergeven van informatie die beschikbaar zijn in de blade Hallo snel wilt controleren of uw verwachting bewijzen.

![Voorbeeld van logboek zoeken](./media/log-analytics-wire-data/log-search-example03.png)

In dit voorbeeld kunt u inzoomen in SSH details toosee welke computers zijn met behulp van SSH en veel andere communicatiegegevens.

![servicel zoekresultaten](./media/log-analytics-wire-data/ssh-details.png)

Het is ook nuttig tooknow als protocolverkeer is verhogen of verlagen gedurende een bepaalde periode. Bijvoorbeeld, als hoeveelheid gegevens die worden verzonden door een toepassing hello stijgt, die mogelijk iets rekening houden met moet zijn of dat u wellicht opmerkelijk.

## <a name="input-data"></a>Invoergegevens

Kabel gegevens verzamelt metagegevens over het netwerkverkeer met behulp van Hallo-agents die u hebt ingeschakeld. Elke agent verzendt gegevens over elke 15 seconden.

## <a name="output-data"></a>uitvoergegevens

Een record met een type _WireData_ is gemaakt voor elk type invoergegevens. WireData-records hebben eigenschappen die worden weergegeven in de volgende tabel Hallo:

| Eigenschap | Beschrijving |
|---|---|
| Computer | De naam van de computer waar de gegevens zijn verzameld |
| TimeGenerated | Tijd van Hallo record |
| LocalIP | IP-adres van de lokale computer Hallo |
| SessionState | Verbonden of verbroken |
| ReceivedBytes | Hoeveelheid ontvangen bytes |
| Protocolnaam | Naam van Hallo netwerkprotocol gebruikt |
| IPVersion | IP-versie |
| Richting | Binnenkomend of uitgaand |
| MaliciousIP | IP-adres van een bekende schadelijke bron |
| Ernst | Ernst van de mogelijke malware |
| RemoteIPCountry | Land van Hallo extern IP-adres |
| ManagementGroupName | Naam van Hallo Operations Manager-beheergroep |
| SourceSystem | Bron waar de gegevens zijn verzameld |
| SessionStartTime | Begintijd van sessie |
| SessionEndTime | Eindtijd van sessie |
| LocalSubnet | Subnet waar de gegevens zijn verzameld |
| LocalPortNumber | Lokale poortnummer |
| RemoteIP | Extern IP-adres gebruikt door de externe computer Hallo |
| RemotePortNumber | Poortnummer van Hallo extern IP-adres |
| Sessie-id | Een unieke waarde die sessie van de communicatie tussen twee IP-adressen aangeeft |
| SentBytes | Aantal verzonden bytes |
| TotalBytes | Totaal aantal bytes dat tijdens de sessie is verzonden |
| ApplicationProtocol | Type netwerkprotocol gebruikt   |
| Proces-id | Windows-proces-ID |
| Procesnaam | Pad en de naam van het Hallo-proces |
| RemoteIPLongitude | IP-Lengtegraadwaarde |
| RemoteIPLatitude | IP-Breedtegraadwaarde |


## <a name="next-steps"></a>Volgende stappen

- [Zoeken in een logboek](log-analytics-log-searches.md) tooview gedetailleerde kabel zoeken gegevensrecords.
