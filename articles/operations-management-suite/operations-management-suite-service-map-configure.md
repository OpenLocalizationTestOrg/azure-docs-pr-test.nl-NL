---
title: aaaConfigure Serviceoverzicht in Operations Management Suite | Microsoft Docs
description: Serviceoverzicht is een Operations Management Suite-oplossing die automatisch de onderdelen van toepassing op Windows detecteert en Linux-systemen en maps Hallo communicatie tussen services. Dit artikel bevat informatie voor het Serviceoverzicht implementeren in uw omgeving en gebruiken in verschillende scenario's.
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>Serviceoverzicht configureren in Operations Management Suite
Serviceoverzicht detecteert automatisch de onderdelen van toepassing op Windows-en Linux- en maps Hallo communicatie tussen services. U kunt deze gebruiken tooview uw servers als u denkt dat ze--als onderling verbonden systemen die essentiële services leveren. Service-kaart toont de verbindingen tussen servers, processen en poorten via een TCP-verbinding architectuur waarvoor geen configuratie vereist, behalve de installatie van een agent.

Dit artikel wordt beschreven Hallo details van het Serviceoverzicht en voorbereiding agents configureren. Zie voor meer informatie over het gebruik van Serviceoverzicht [Hallo Serviceoverzicht oplossing gebruiken in Operations Management Suite](operations-management-suite-service-map.md).

## <a name="dependency-agent-downloads"></a>Agent voor afhankelijkheden gedownload
| File | OS | Versie | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>Verbonden bronnen
Serviceoverzicht afkomstig zijn uit Hallo Microsoft-Agent voor afhankelijkheden. Hallo-Agent voor afhankelijkheden, is afhankelijk van Hallo OMS-Agent voor de verbindingen tooOperations Management Suite. Dit betekent dat een server moet Hallo OMS-Agent geïnstalleerd en geconfigureerd, en vervolgens Hallo-Agent voor afhankelijkheden kunnen worden geïnstalleerd. Hallo beschrijft volgende tabel Hallo verbonden bronnen die ondersteuning biedt voor Hallo Serviceoverzicht oplossing.

| Verbonden bron | Ondersteund | Beschrijving |
|:--|:--|:--|
| Windows-agents | Ja | Serviceoverzicht analyseert en verzamelt gegevens van agent-Windows-computers. <br><br>In aanvulling toohello [OMS-Agent](../log-analytics/log-analytics-windows-agents.md), Windows-agents Hallo Microsoft afhankelijkheid Agent vereist. Zie Hallo [ondersteunde besturingssystemen](#supported-operating-systems) voor een volledige lijst met versies van besturingssystemen. |
| Linux-agents | Ja | Serviceoverzicht analyseert en verzamelt gegevens van Linux-agent-computers. <br><br>In aanvulling toohello [OMS-Agent](../log-analytics/log-analytics-linux-agents.md), Linux-agents Hallo Microsoft afhankelijkheid Agent vereist. Zie Hallo [ondersteunde besturingssystemen](#supported-operating-systems) voor een volledige lijst met versies van besturingssystemen. |
| Beheergroep System Center Operations Manager | Ja | Serviceoverzicht analyseert en verzamelt gegevens van Windows en Linux-agents in een verbonden [System Center Operations Manager-beheergroep](../log-analytics/log-analytics-om-agents.md). <br><br>Een rechtstreekse verbinding tussen Hallo System Center Operations Manager-agent computer tooOperations Management Suite is vereist. Gegevens doorgestuurd vanuit Hallo management groep toohello Operations Management Suite-opslagplaats.|
| Azure Storage-account | Nee | Serviceoverzicht verzamelt gegevens van computers die door agents, dus er geen gegevens uit het zijn toocollect uit Azure Storage. |

Serviceoverzicht ondersteunt alleen 64-bits-platforms.

Op Windows hello Microsoft Monitoring Agent (MMA) gebruikt door System Center Operations Manager en Operations Management Suite toogather en bewakingsgegevens verzenden. (Deze agent wordt Hallo System Center Operations Manager-Agent, OMS-Agent, Log Analytics-Agent, MMA of Direct Agent, afhankelijk van de context Hallo genoemd). System Center Operations Manager en Operations Management Suite bieden verschillende out van Hallo vak versies van Hallo MMA. Deze versies kunnen elk rapport tooSystem Center Operations Manager, tooOperations Management Suite of tooboth.  

Hallo OMS-Agent voor Linux Hiermee en verzendt gegevens tooOperations Management Suite bewaking op Linux. U kunt Serviceoverzicht gebruiken op servers met OMS Direct Agents of op servers die aangesloten tooOperations Management Suite via System Center Operations Manager-beheergroepen zijn.  

In dit artikel, verwijzen we tooall agents--of Linux- of Windows, of verbonden tooa System Center Operations Manager-beheergroep of rechtstreeks tooOperations Management Suite--zoals Hallo "OMS-Agent." We gebruiken Hallo implementatienaam Hallo agent alleen indien nodig voor context.

Hallo Serviceoverzicht agent wordt niet verzonden gegevens zelf en hoeven niet alle wijzigingen toofirewalls of poorten. Hallo-gegevens in Serviceoverzicht is altijd verzonden door Hallo OMS-Agent tooOperations Management Suite, rechtstreeks of via Hallo OMS-Gateway.

![Serviceoverzicht agents](media/oms-service-map/agents.png)

Als u een klant System Center Operations Manager met een management groep verbonden tooOperations Management Suite:

- Als de System Center Operations Manager-agents toegang heeft tot Internet tooconnect tooOperations Management Suite hello, is geen aanvullende configuratie vereist.  
- Als de System Center Operations Manager-agents geen toegang Operations Management Suite via Hallo Internet tot, moet u tooconfigure Hallo OMS Gateway toowork met System Center Operations Manager.
  
Als u van Hallo Direct OMS-Agent gebruikmaakt, moet u tooconfigure Hallo OMS-Agent zelf tooconnect tooOperations Management Suite of tooyour OMS-Gateway. Hallo OMS-Gateway kan worden gedownload vanaf Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

### <a name="management-packs"></a>Management packs
Wanneer Serviceoverzicht in een Operations Management Suite-werkruimte is geactiveerd, wordt een 300 KB management pack tooall Hallo Windows-servers in deze werkruimte verzonden. Als u System Center Operations Manager-agents in een [verbonden beheergroep](../log-analytics/log-analytics-om-agents.md), Hallo Serviceoverzicht management pack van System Center Operations Manager is geïmplementeerd. Als agents Hallo rechtstreeks zijn verbonden, levert Operations Management Suite Hallo management pack.

Hallo management pack met de naam Microsoft.IntelligencePacks.ApplicationDependencyMonitor. De schriftelijke too%Programfiles%\Microsoft bewaking Agent\Agent\Health Service State\Management Packs\. Hallo gegevensbron die gebruikmaakt van Hallo management pack is % Program files%\Microsoft bewaking Agent\Agent\Health Service State\Resources\<AutoGeneratedID > \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="installation"></a>Installeren
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a>Hallo-Agent voor afhankelijkheden op Microsoft Windows installeren
Administrator-bevoegdheden zijn vereist tooinstall of Hallo-agent verwijderen.

Hallo afhankelijkheid Agent is geïnstalleerd op Windows-computers via InstallDependencyAgent Windows.exe. Als u dit uitvoerbare bestand zonder opties uitvoert, wordt er een wizard u tooinstall interactief kunt volgen gestart.  

Volgende stappen tooinstall Hallo-Agent voor afhankelijkheden op elke computer met Windows hello gebruiken:

1.  Installatie OMS-Agent met behulp van instructies op Hallo Hallo [verbinding maken met Windows-computers toohello Log Analytics-service in Azure](../log-analytics/log-analytics-windows-agents.md).
2.  Hallo Windows-agent downloaden en uitvoeren met behulp van de volgende opdracht Hallo: <br>`InstallDependencyAgent-Windows.exe`
3.  Ga als volgt Hallo wizard tooinstall Hallo agent.
4.  Als het Hallo-Agent voor afhankelijkheden toostart mislukt, controleert u Hallo-logboeken voor uitgebreide foutinformatie. Hallo logboekmap is op Windows-agents %Programfiles%\Microsoft Agent\logs afhankelijkheid. 

#### <a name="windows-command-line"></a>Windows-opdrachtregel
Gebruik de opties van Hallo tabel tooinstall vanaf een opdrachtregel te volgen. een lijst met Hallo installatie vlaggen, Hallo installatieprogramma uitvoeren met behulp van Hallo toosee /? markering als volgt.

    InstallDependencyAgent-Windows.exe /?

| Vlag | Beschrijving |
|:--|:--|
| /? | Een lijst met opdrachtregelopties Hallo ophalen. |
| / S | Een installatie zonder vragen van de gebruiker op de achtergrond uitvoeren. |

Bestanden voor Windows-Agent voor afhankelijkheden Hallo worden standaard in C:\Program Files\Microsoft afhankelijkheid Agent geplaatst.

### <a name="install-hello-dependency-agent-on-linux"></a>Hallo-Agent voor afhankelijkheden te installeren op Linux
Toegang tot de hoofdmap is vereist tooinstall of Hallo-agent configureren.

Hallo afhankelijkheid Agent is geïnstalleerd op Linux-computers via InstallDependencyAgent-Linux64.bin, een shell-script met een zichzelf uitpakkend binaire waarde. U kunt het Hallo-bestand uit te voeren met behulp van servicel of toevoegen machtigingen toohello bestand zelf.
 
Volgende stappen tooinstall Hallo-Agent voor afhankelijkheden op elke Linux-computer hello gebruiken:

1.  Installatie OMS-Agent met behulp van instructies op Hallo Hallo [verzamelen en beheren van gegevens van Linux-computers](https://technet.microsoft.com/library/mt622052.aspx).
2.  Hallo Linux afhankelijkheid agent als hoofdmap installeren met behulp van de volgende opdracht Hallo:<br>`sh InstallDependencyAgent-Linux64.bin`
3.  Als het Hallo-Agent voor afhankelijkheden toostart mislukt, controleert u Hallo-logboeken voor uitgebreide foutinformatie. Op Linux-agents is de logboekmap Hallo /var/opt/microsoft/dependency-agent/log.

een lijst met Hallo installatie vlaggen, Hallo het installatieprogramma uitvoeren met toosee Hallo - help vlag als volgt.

    InstallDependencyAgent-Linux64.bin -help

| Vlag | Beschrijving |
|:--|:--|
| -help | Een lijst met opdrachtregelopties Hallo ophalen. |
| -s | Een installatie zonder vragen van de gebruiker op de achtergrond uitvoeren. |
| --controleren | Controleer de machtigingen en het Hallo-besturingssysteem, maar geen Hallo-agent installeren. |

Bestanden voor Hallo-Agent voor afhankelijkheden worden geplaatst in Hallo mappen te volgen:

| Bestanden | Locatie |
|:--|:--|
| Core-bestanden | /Opt/Microsoft/Dependency-agent |
| Logboekbestanden | /var/opt/Microsoft/Dependency-agent/log |
| De config-bestanden | /etc/opt/Microsoft/Dependency-agent/config |
| Uitvoerbare bestanden voor service | /Opt/Microsoft/Dependency-agent/bIn/Microsoft-Dependency-agent<br>/Opt/Microsoft/Dependency-agent/bIn/Microsoft-Dependency-Agent-Manager |
| Binaire opslag-bestanden | /var/opt/Microsoft/Dependency-agent/Storage |

## <a name="installation-script-examples"></a>Voorbeelden van scripts voor installatie
tooeasily implementeren Hallo-Agent voor afhankelijkheden op veel servers in één keer, helpt toouse een script. U kunt gebruiken Hallo script voorbeelden toodownload te volgen en Hallo afhankelijkheid Agent installeren op Windows of Linux.

### <a name="powershell-script-for-windows"></a>Windows PowerShell-script
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>Shell-script voor Linux
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a>Desired State Configuration
toodeploy Hallo-Agent voor afhankelijkheden via Desired State Configuration, kunt u Hallo xPSDesiredStateConfiguration module en een codefragment Hallo volgende:
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a>Verwijderen
### <a name="uninstall-hello-dependency-agent-on-windows"></a>Agent voor afhankelijkheden op Windows hello verwijderen
Een beheerder kan Hallo afhankelijkheid Agent voor Windows via het Configuratiescherm kunt verwijderen.

Een beheerder kan ook %Programfiles%\Microsoft afhankelijkheid Agent\Uninstall.exe toouninstall Hallo-Agent voor afhankelijkheden uitgevoerd.

### <a name="uninstall-hello-dependency-agent-on-linux"></a>Hallo op Linux-Agent voor afhankelijkheden verwijderen
toocompletely verwijderen Hallo van Linux-Agent voor afhankelijkheden, moet u Hallo agent zelf verwijderen en Hallo connector die wordt automatisch geïnstalleerd met Hallo-agent. U kunt beide via Hallo na één opdracht verwijderen:

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>Problemen oplossen
Als er problemen installeren of uitvoeren Serviceoverzicht, kunt in deze sectie u. Als u uw probleem niet kunt oplossen, neem contact op met Microsoft Support.

### <a name="dependency-agent-installation-problems"></a>Problemen tijdens de installatie van de afhankelijkheid Agent
#### <a name="installer-asks-for-a-reboot"></a>Installatieprogramma vraagt om de computer opnieuw is opgestart
Hallo-Agent voor afhankelijkheden *doorgaans* hoeft niet opnieuw worden opgestart na het installeren of verwijderen. In bepaalde zeldzame gevallen vereist Windows Server echter een toocontinue opnieuw opstarten met een installatie. Dit gebeurt wanneer een afhankelijkheid, meestal Hallo Microsoft Visual C++ Redistributable, opnieuw worden opgestart vanwege een vergrendeld bestand moet.

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a>Bericht ' kan geen tooinstall-Agent voor afhankelijkheden: Visual Studio-Runtime-bibliotheken tooinstall is mislukt (code = [codenummer]) ' wordt weergegeven

Hallo Microsoft-Agent voor afhankelijkheden is gebouwd op Hallo Microsoft Visual Studio-runtime-bibliotheken. U krijgt een bericht als er een probleem opgetreden tijdens de installatie van het Hallo-bibliotheken. 

Hallo runtime-bibliotheek installatieprogramma's kunt u Logboeken in Hallo %LOCALAPPDATA%\temp map maken. Hallo-bestand is dd_vcredist_arch_yyyymmddhhmmss.log, waarbij *arch* 'x86' of 'amd64' en *jjjjmmdduummss* Hallo datum en tijd (24-uurs klok) waarop Hallo-logboek is gemaakt. Hallo-logboek bevat informatie over Hallo probleem dat door de installatie wordt geblokkeerd.

Kan het nuttig tooinstall Hallo zijn [nieuwste runtimebibliotheken](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) zelf eerste.

Hallo volgende tabel bevat codes en voorgestelde oplossingen.

| Code | Beschrijving | Oplossing |
|:--|:--|:--|
| 0x17 | Hallo bibliotheek installer vereist een Windows-update is niet geïnstalleerd. | Zoek in de meest recente bibliotheek installer-logboekbestand Hallo.<br><br>Als een verwijzing te 'Windows8.1-KB2999226-x64.msu' gevolgd door een regel ' fout 0x80240017: mislukte tooexecute MSU-pakket, "u hebt geen Hallo vereisten tooinstall KB2999226. Volg de instructies Hallo in Hallo sectie voor vereisten in [universeel C Runtime in Windows](https://support.microsoft.com/kb/2999226). U kunt moet toorun Windows Update en opnieuw opstarten van meerdere keren in volgorde tooinstall Hallo vereisten.<br><br>Hallo Microsoft afhankelijkheid Agent-installatieprogramma opnieuw uitvoeren. |

### <a name="post-installation-issues"></a>Na de installatie problemen
#### <a name="server-doesnt-appear-in-service-map"></a>Server niet wordt weergegeven in het Serviceoverzicht
Als uw afhankelijkheid Agent-installatie is voltooid, maar uw server in Hallo Serviceoverzicht oplossing niet wordt weergegeven:
* Hallo-Agent voor afhankelijkheden met succes is geïnstalleerd? U kunt dit controleren door toosee controleren als Hallo-service is geïnstalleerd en wordt uitgevoerd.<br><br>
**Windows**: zoekt Hallo-service met de naam 'Microsoft Dependency Agent'.<br>
**Linux**: zoekt Hallo gestart 'microsoft-afhankelijkheid-agent'.

* Weet u op Hallo [gratis prijscategorie van Operations Management Suite/Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? Hallo gratis-plan kunt u toofive unieke Serviceoverzicht-servers. Alle volgende servers zijn weergegeven niet in het Serviceoverzicht, zelfs als Hallo voorafgaande vijf niet meer gegevens verzendt.

* Is uw server verzenden logboekbestand en de perfmapper gegevens tooOperations Management Suite? Ga tooLog zoeken en Voer Hallo query voor uw computer te volgen: 

        * Computer="<your computer name here>" | measure count() by Type
        
  Krijgt u een aantal gebeurtenissen in de resultaten van de Hallo? Hallo gegevens recente is? Als dit het geval is, wordt de OMS-Agent naar behoren werkt en Hallo Operations Management Suite-service communiceert. Als dit niet het geval is, controleert u Hallo OMS-Agent op uw server: [OMS-Agent voor Windows probleemoplossing](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) of [OMS-Agent voor het oplossen van Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>Server wordt weergegeven in het Serviceoverzicht, maar heeft geen processen
Als u uw server in het Serviceoverzicht zien, maar heeft geen gegevens verwerken of verbinding, die dat Hallo aangeeft afhankelijkheid Agent is geïnstalleerd en actief, maar Hallo kernel-stuurprogramma niet geladen. 

Controleer de Hallo C:\Program Files\Microsoft afhankelijkheid Agent\logs\wrapper.log-bestand (Windows) of /var/opt/microsoft/dependency-agent/log/service.log-bestand (Linux). laatste regels Hallo van Hallo bestand zou moeten aangeven waarom Hallo kernel niet laden. Hallo kernel kan bijvoorbeeld niet worden ondersteund op Linux als u uw kernel bijgewerkt.

## <a name="data-collection"></a>Gegevensverzameling
U kunt elke agent tootransmit ongeveer verwachten 25 MB per dag, afhankelijk van hoe complexe de afhankelijkheden van uw systeem zijn. Elke agent verzendt Serviceoverzicht afhankelijkheid elke 15 seconden.  

Hallo-Agent voor afhankelijkheden verbruikt doorgaans 0,1 procent van het systeemgeheugen en 0,1 procent van CPU-systeem.

## <a name="supported-azure-regions"></a>Ondersteunde Azure-regio 's
Serviceoverzicht is momenteel beschikbaar zijn in hello Azure-regio's te volgen:
- VS - oost
- West-Europa
- West-centraal VS


## <a name="supported-operating-systems"></a>Ondersteunde besturingssystemen
Hallo volgende secties geven lijsten Hallo ondersteunde besturingssystemen voor Hallo-Agent voor afhankelijkheden. Serviceoverzicht biedt geen ondersteuning voor 32-bits architecturen voor elk besturingssysteem.

### <a name="windows-server"></a>Windows Server
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

### <a name="windows-desktop"></a>Windows-bureaublad
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux-, CentOS Linux- en Oracle Linux (met RHEL Kernel)
- Alleen standaard en SMP Linux kernel-versies worden ondersteund.
- Niet-standaard kernel versies, zoals PAE en Xen, worden niet ondersteund voor een Linux-distributie. Bijvoorbeeld, wordt een systeem met Hallo release tekenreeks '2.6.16.21-0.8-xen' niet ondersteund.
- Aangepaste kernels, met inbegrip van hercompilaties van standaard kernels worden niet ondersteund.
- CentOSPlus kernel wordt niet ondersteund.
- Oracle Unbreakable Enterprise Kernel (UEK) wordt in verderop in dit artikel beschreven.


#### <a name="red-hat-linux-7"></a>Red Hat Linux 7
| De versie van besturingssysteem | Kernelversie |
|:--|:--|
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7.2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6
| De versie van besturingssysteem | Kernelversie |
|:--|:--|
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
| De versie van besturingssysteem | Kernelversie |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18-417<br>2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux met Unbreakable Enterprise Kernel

#### <a name="oracle-linux-6"></a>Oracle Linux 6
| De versie van besturingssysteem | Kernelversie
|:--|:--|
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| De versie van besturingssysteem | Kernelversie
|:--|:--|
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11
| De versie van besturingssysteem | Kernelversie
|:--|:--|
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10
| De versie van besturingssysteem | Kernelversie
|:--|:--|
| 10 SP4 | 2.6.16.60 |

## <a name="diagnostic-and-usage-data"></a>Diagnostische gegevens en gebruiksgegevens
Microsoft verzamelt automatisch gebruiks- en via uw gebruik van Hallo Serviceoverzicht service. Microsoft gebruikt deze gegevens tooprovide en Hallo kwaliteit, beveiliging en integriteit van Hallo Serviceoverzicht service te verbeteren. Gegevens omvatten informatie over het configureren van Hallo van uw software, zoals het besturingssysteem en versie. Dit omvat ook IP-adres, DNS-naam en de Werkstationnaam van het in volgorde tooprovide nauwkeurige en efficiënte mogelijkheden voor probleemoplossing. Er worden geen namen, adressen of andere contactgegevens verzameld.

Zie voor meer informatie over het verzamelen van gegevens en gebruiksgegevens Hallo [privacyverklaring van Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=512132).



## <a name="next-steps"></a>Volgende stappen
- Meer informatie over hoe te[Serviceoverzicht gebruiken](operations-management-suite-service-map.md) nadat deze is geïmplementeerd en geconfigureerd.
