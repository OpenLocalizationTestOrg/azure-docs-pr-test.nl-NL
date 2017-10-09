---
title: aaaVMware bewaking oplossing in Log Analytics | Microsoft Docs
description: Meer informatie over hoe Hallo oplossing VMware bewaking kunt logboeken beheren en controleren van ESXi-hosts.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 959d5c2201fc5c7947f8b8870d055cdf9eea8e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a>VMware Monitoring (Preview)-oplossing in Log Analytics

![VMware symbool](./media/log-analytics-vmware/vmware-symbol.png)

Hallo oplossing VMware bewaking in Log Analytics is een oplossing waarmee u een centrale logboekregistratie en controle benadering voor grote VMware logboeken maken. Dit artikel wordt beschreven hoe u kunt oplossen, vastleggen en ESXi-hosts op één locatie met behulp van de oplossing Hallo Hallo beheren. Met Hallo-oplossing, kunt u gedetailleerde gegevens bekijken voor uw ESXi-hosts op één locatie. U kunt aantallen bovenste gebeurtenis, status en trends van VM- en ESXi-hosts via Hallo ESXi-host logboeken zien. Als u problemen met het weergeven en zoeken naar Logboeken van gecentraliseerde ESXi-host. En u waarschuwingen op basis van het logboek zoekquery's kunt maken.

Hallo-oplossing gebruikt systeemeigen syslog-functionaliteit van Hallo ESXi-host toopush tooa Gegevensdoel VM die OMS-Agent heeft. Hallo-oplossing schrijven niet echter bestanden in syslog binnen een Hallo doel-virtuele machine. Hallo OMS-agent wordt poort 1514 geopend en luistert toothis. Zodra het Hallo-gegevens ontvangt, duwt Hallo OMS-agent Hallo gegevens in OMS.

## <a name="installing-and-configuring-hello-solution"></a>Installeren en configureren van Hallo-oplossing
Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren.

* Hallo VMware bewaking oplossing tooyour OMS-werkruimte met behulp van Hallo proces dat wordt beschreven in toevoegen [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).

#### <a name="supported-vmware-esxi-hosts"></a>Ondersteunde VMware ESXi-hosts
vSphere ESXi-Host 5.5 en 6.0

#### <a name="prepare-a-linux-server"></a>Bereid een server voor Linux
Maak een Linux-besturingssysteem VM tooreceive alle syslog-gegevens van Hallo ESXi-hosts. Hallo [OMS Linux-Agent](log-analytics-linux-agents.md) Hallo verzameling punt voor alle ESXi-host syslog-gegevens. U kunt meerdere ESXi-hosts tooforward logboeken tooa één Linux-server, zoals in het volgende voorbeeld Hallo gebruiken.  

   ![Syslog-stroom](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a>Syslog verzamelen configureren
1. Syslog-doorsturen voor VSphere instellen. Zie voor gedetailleerde informatie toohelp instellen syslog doorsturen, [syslog configureren op ESXi 5.x en 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322). Ga te**ESXi-hostconfiguratie** > **Software** > **geavanceerde instellingen** > **Syslog**.
   ![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)  
2. In Hallo *Syslog.global.logHost* veld, het toevoegen van uw Linux-server en het Hallo-poortnummer *1514*. Bijvoorbeeld, `tcp://hostname:1514` of`tcp://123.456.789.101:1514`
3. Open Hallo ESXi hostfirewall voor syslog. **De hostconfiguratie ESXi** > **Software** > **beveiligingsprofiel** > **Firewall** en openen **Eigenschappen**.  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. Controleer Hallo vSphere Console tooverify die syslog correct is ingesteld. Bevestig op Hallo ESXI hosten die poort **1514** is geconfigureerd.
5. Download en installeer Hallo OMS-Agent voor Linux op Hallo Linux-server. Zie voor meer informatie, Hallo [documentatie voor de OMS-Agent voor Linux](https://github.com/Microsoft/OMS-Agent-for-Linux).
6. Nadat het Hallo OMS-Agent voor Linux is geïnstalleerd, gaat u toohello /etc/opt/microsoft/omsagent/sysconf/omsagent.d directory en de kopie Hallo vmware_esxi.conf toohello /etc/opt/microsoft/omsagent/conf/omsagent.d map en Hallo Hallo eigenaar/groep wijzigen en machtigingen van Hallo-bestand. Bijvoorbeeld:

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. Start Hallo OMS-Agent opnieuw voor Linux met `sudo /opt/microsoft/omsagent/bin/service_control restart`.
8. Hallo-connectiviteit tussen Hallo Linux-server en Hallo ESXi-host met Hallo testen `nc` opdracht op Hallo ESXi-Host. Bijvoorbeeld:

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection too123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. In Hallo OMS-Portal, doorzoeken logboek voor `Type=VMware_CL`. Wanneer OMS Hallo syslog-gegevens worden verzameld, behoudt Hallo syslog-indeling. In de portal Hallo sommige specifieke velden zijn vastgelegd, zoals *hostnaam* en *procesnaam*.  

    ![type](./media/log-analytics-vmware/type.png)  

    Als uw zoekresultaten voor weergave logboek vergelijkbare toohello afbeelding hierboven, bent u toouse Hallo OMS VMware oplossing bewakingsdashboard instellen.  

## <a name="vmware-data-collection-details"></a>De verzameling Gegevensdetails VMware
Hallo VMware bewaking oplossing verzamelt verschillende metrische gegevens en logboekbestanden prestatiegegevens van ESXi-hosts met Hallo OMS Agents voor Linux die u hebt ingeschakeld.

Hallo volgende tabel bevat de methoden van de collectie en andere informatie over hoe gegevens worden verzameld.

| Platform | OMS-Agent voor Linux | SCOM-agents | Azure Storage | SCOM vereist? | SCOM-agent gegevens die worden verzonden via de beheergroep | Frequentie van de verzameling |
| --- | --- | --- | --- | --- | --- | --- |
| Linux |&#8226; |  |  |  |  |om de 3 minuten |

Hallo volgende tabel ziet u voorbeelden van gegevensvelden die is verzameld door Hallo VMware bewaking oplossing:

| Veldnaam | description |
| --- | --- |
| Device_s |VMware-opslagapparaten |
| ESXIFailure_s |Fout-typen |
| EventTime_t |tijd waarop de gebeurtenis heeft plaatsgevonden |
| HostName_s |ESXi-hostnaam |
| Operation_s |virtuele machine maken of verwijderen van de virtuele machine |
| ProcessName_s |De naam van gebeurtenis |
| ResourceId_s |naam van Hallo VMware host |
| ResourceLocation_s |VMware |
| ResourceName_s |VMware |
| ResourceType_s |Hyper-V |
| SCSIStatus_s |VMware SCSI-status |
| SyslogMessage_s |Syslog-gegevens |
| UserName_s |gebruiker die zijn gemaakt of verwijderd van virtuele machine |
| VMName_s |VM-naam |
| Computer |hostcomputer |
| TimeGenerated |Hallo tijdgegevens is gegenereerd |
| DataCenter_s |VMware datacenter |
| StorageLatency_s |opslaglatentie (ms) |

## <a name="vmware-monitoring-solution-overview"></a>Overzicht van de bewaking van de VMware-oplossing
Hallo VMware-tegel wordt weergegeven in Hallo OMS-portal. Het bevat een overzichtsweergave van storingen. Wanneer u Hallo tegel klikt, gaat u in een dashboardweergave.

![Tegel](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-hello-dashboard-view"></a>Navigeer Hallo dashboardweergave
In Hallo **VMware** dashboardweergave blades zijn gerangschikt op:

* Aantal mislukte-Status
* Telt bovenste Host door gebeurtenis
* Telt het aantal bovenste gebeurtenis
* Activiteiten van de virtuele Machine
* Gebeurtenissen van ESXi-Host schijf

![solution1](./media/log-analytics-vmware/solutionview1-1.png)

![solution2](./media/log-analytics-vmware/solutionview1-2.png)

Klik op een blade tooopen logboekanalyse zoekvenster die specifiek is voor Hallo blade ziet u gedetailleerde informatie.

Hier kunt u Hallo zoeken query toomodify kunt bewerken voor een bepaald. Bekijk voor een zelfstudie over Hallo basisprincipes van OMS zoeken, Hallo [OMS logboek search-zelfstudie.](log-analytics-log-searches.md)

#### <a name="find-esxi-host-events"></a>Gebeurtenissen van ESXi-host vinden
Eén ESXi-host genereert meerdere logboeken, op basis van hun processen. Hallo VMware bewaking oplossing zijn ze gecentraliseerd en bevat een overzicht van Hallo gebeurtenis telt. Deze centrale weergave helpt u begrijpen welke ESXi-host heeft een groot aantal gebeurtenissen en welke gebeurtenissen treden het vaakst in uw omgeving.

![Gebeurtenis](./media/log-analytics-vmware/events.png)

U kunt inzoomen verdere door te klikken op een ESXi-host of een gebeurtenistype.

Als u op de naam van een ESXi-host, kunt u gegevens vanaf deze host ESXi weergeven. Als u toonarrow resultaten met gebeurtenistype hello wilt, toevoegen `“ProcessName_s=EVENT TYPE”` in uw query. U kunt selecteren **procesnaam** in Hallo zoekfilter. Die Hallo-informatie voor u wordt beperkt.

![Inzoomen](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a>Activiteiten met hoge VM zoeken
Een virtuele machine worden gemaakt en op elke host ESXi verwijderd. Het is nuttig als een beheerder tooidentify hoeveel virtuele machines ESXi-host wordt gemaakt. Die beurt, helpt toounderstand prestaties en capaciteitsplanning. Het bijhouden van activiteitsgebeurtenissen VM is van cruciaal belang bij het beheren van uw omgeving.

![Inzoomen](./media/log-analytics-vmware/vmactivities1.png)

Als u wilt dat toosee extra ESXi host gegevens voor het aanmaken van virtuele machine, klikt u op de naam van een ESXi-host.

![Inzoomen](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a>Algemene zoekquery 's
Hallo-oplossing omvat andere nuttige query's die kunnen helpen bij het beheren van uw ESXi-hosts, zoals hoge opslagruimte opslaglatentie en path-fout.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Query 's](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a>Query's opslaan
Zoekopdrachten opslaan is een standaardfunctie in OMS en kunt u alle query's die u hebt gevonden nuttig. Nadat u een query die nuttig maakt, opslaan door te klikken op Hallo **Favorieten**. Een opgeslagen query kunt u eenvoudig het later opnieuw gebruiken van Hallo [mijn Dashboard](log-analytics-dashboards.md) pagina waar u uw eigen aangepaste dashboards kunt maken.

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a>Waarschuwingen van query's maken
Nadat u uw query's hebt gemaakt, kunt u toouse Hallo query's tooalert u wanneer specifieke gebeurtenissen plaatsvinden. Zie [waarschuwingen in logboekanalyse](log-analytics-alerts.md) voor informatie over het toocreate waarschuwingen. Zie voor voorbeelden van query's en andere voorbeelden van query waarschuwingen Hallo [Monitor VMware met OMS Log Analytics](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) blogbericht.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
### <a name="what-do-i-need-toodo-on-hello-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a>Wat moet ik toodo op Hallo ESXi-host instellen? Wat zijn de gevolgen hebben deze op mijn huidige omgeving?
Hallo-oplossing gebruikt Hallo-mechanisme voor het doorsturen van systeemeigen ESXi-Host Syslog. U hoeft geen aanvullende Microsoft-software op Hallo ESXi-Host toocapture Hallo Logboeken niet. Er moet een lage impact tooyour bestaande omgeving. U moet echter wel tooset syslog doorsturen, ESXI-functionaliteit is.

### <a name="do-i-need-toorestart-my-esxi-host"></a>Moet ik toorestart mijn ESXi-host?
Nee. Dit proces is niet opnieuw opstarten vereist. Soms vSphere niet correct bijgewerkt Hallo syslog. In dat geval aanmelden toohello ESXi-host en opnieuw laden Hallo syslog. Opnieuw, u hebt geen toorestart Hallo host, zodat dit proces wordt niet verstoren tooyour omgeving.

### <a name="can-i-increase-or-decrease-hello-volume-of-log-data-sent-toooms"></a>Kan ik volume verhogen of verlagen Hallo logboekgegevens tooOMS verzonden?
U kunt Ja. In de vSphere kunt u instellingen voor Hallo logboekniveau ESXi-Host. Logboekverzameling is gebaseerd op Hallo *info* niveau. Dus als u wilt dat tooaudit VM maken of verwijderen, moet u tookeep hello *info* niveau op Hostd. Zie voor meer informatie, Hallo [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658).

### <a name="why-is-hostd-not-providing-data-toooms-my-log-setting-is-set-tooinfo"></a>Waarom Hostd verleent geen gegevens tooOMS? Mijn logboek is tooinfo ingesteld.
Er is een fout ESXi-host voor Hallo syslog timestamp. Zie voor meer informatie, Hallo [VMware Knowledge Base](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202). Nadat u Hallo tijdelijke oplossing hebt toegepast, moeten Hostd normaal functioneren.

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-tooa-single-vm-with-omsagent"></a>Kan ik heb meerdere ESXi hosts syslog gegevens tooa doorsturen één virtuele machine met omsagent?
Ja. U kunt meerdere ESXi hebben hosts doorsturen tooa enkele virtuele machine met omsagent.

### <a name="why-dont-i-see-data-flowing-into-oms"></a>Waarom zie ik niet gegevens die binnenkomen in OMS?
Er zijn meerdere redenen:

* Hallo ESXi-host is niet correct gegevens toohello VM actieve omsagent pushen. tootest, Hallo volgende stappen uit te voeren:

  1. tooconfirm, meld u aan toohello ESXi-host met behulp van ssh en Hallo volgende opdracht uitvoeren:`nc -z ipaddressofVM 1514`

      Als dit niet lukt, vSphere-instellingen in Hallo geavanceerde configuratie zijn waarschijnlijk niet worden hersteld. Zie [syslog verzamelen configureren](#configure-syslog-collection) voor meer informatie over hoe tooset up Hallo ESXi hosten voor het doorsturen van syslog.
  2. Als syslog-poort verbinding geslaagd is, maar u geen gegevens nog steeds niet ziet, klikt u vervolgens opnieuw laden Hallo syslog op Hallo ESXi-host met ssh toorun Hallo volgende opdracht:` esxcli system syslog reload`
* Hallo-VM met OMS-Agent is niet juist ingesteld. tootest dit Hallo volgende stappen uit te voeren:

  1. OMS toohello poort 1514 luistert en stuurt de gegevens in OMS. tooverify dat is geopend, voert u Hallo volgende opdracht:`netstat -a | grep 1514`
  2. U ziet poort `1514/tcp` openen. Als u dit niet doet, moet u controleren dat omsagent Hallo juist is geïnstalleerd. Hallo syslog-poort is niet geopend op Hallo VM als er geen poortinformatie hello.

     1. Controleer of deze Hallo OMS-Agent wordt uitgevoerd met behulp van `ps -ef | grep oms`. Als deze niet wordt uitgevoerd, Hallo proces starten met Hallo-opdracht` sudo /opt/microsoft/omsagent/bin/service_control start`
     2. Open Hallo `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` bestand.

         Controleren of de juiste gebruiker Hallo en instelling van de geldige, vergelijkbaar met:`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`

         Als het Hallo-bestand bestaat niet of Hallo gebruiker en groepsinstelling onjuist is, los problemen door [voorbereiden van een Linux-server](#prepare-a-linux-server).

## <a name="next-steps"></a>Volgende stappen
* Gebruik [logboek zoekopdrachten](log-analytics-log-searches.md) in logboekanalyse tooview gedetailleerde gegevens voor VMware-host.
* [Maak uw eigen dashboards](log-analytics-dashboards.md) VMware hostgegevens weergegeven.
* [Waarschuwingen maken](log-analytics-alerts.md) wanneer specifieke VMware hostgebeurtenissen plaatsvinden.
