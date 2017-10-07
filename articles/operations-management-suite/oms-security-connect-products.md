---
title: aaaConnecting uw beveiliging producten toohello Operations Management Suite (OMS) beveiliging en Audit oplossing | Microsoft Docs
description: Dit document helpt u tooconnect uw beveiliging producten tooOperations Management Suite beveiligings- en Audit-oplossing met behulp van algemene indeling van de gebeurtenis.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a>Verbinding maken met de beveiliging producten toohello Operations Management Suite (OMS) beveiliging en Audit-oplossing 
Dit document helpt u uw beveiligingsproducten verbinding naar hello OMS beveiligings- en Audit-oplossing. Hallo de volgende bronnen worden ondersteund:

- Common Event Format-gebeurtenissen (CEF)
- Cisco ASA-gebeurtenissen


## <a name="what-is-cef"></a>Wat is CEF?
Algemene gebeurtenis-indeling (CEF) is een indeling volgens de industrienorm boven op Syslog-berichten die worden gebruikt door veel beveiliging leveranciers tooallow gebeurtenis interoperabiliteit tussen verschillende platforms. Ondersteuning voor gegevensopname CEF waarmee u tooconnect van uw beveiligingsproducten met OMS-beveiliging met OMS beveiligings- en Audit-oplossing. 

U bent tootake kunnen profiteren van Hallo na mogelijkheden die deel van dit platform uitmaken door verbinding te maken van uw gegevensbron tooOMS:

- Zoeken en correlatie
- Controleren
- Waarschuwing
- Bedreigingsinformatie
- Problemen die aandacht vereisen

## <a name="collection-of-security-solution-logs"></a>Logboeken van beveiligingsoplossingen verzamelen

OMS Security biedt ondersteuning voor het verzamelen van logboeken middels CIS via Syslogs en [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/)-logboeken. In dit voorbeeld Hallo bron (de computer die Hallo logboeken genereert) is een Linux-computer met de syslog-ng daemon en Hallo doel is OMS-beveiliging. tooprepare hello Linux-computer moet u tooperform Hallo volgende taken:

- Hallo OMS-Agent downloaden voor Linux, versie 1.2.0-25 of hoger.
- Ga als volgt Hallo sectie **snelle handleiding installeren** van [in dit artikel](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall en vrijgeven Hallo agent tooyour werkruimte.

Normaal gesproken is Hallo-agent geïnstalleerd op een andere computer dan Hallo één op welke Hallo-logboeken worden gegenereerd. Doorsturen Hallo logboeken toohello-agentcomputer wordt doorgaans vereist voor Hallo stappen te volgen:

- Hallo logboekregistratie product/machine tooforward Hallo vereist gebeurtenissen toohello syslog-daemon (rsyslog of syslog-ng) op de agentcomputer Hallo configureren.
- Schakel Hallo syslog-daemon op Hallo agent machine tooreceive berichten van een extern systeem.

Op de agentcomputer hello moeten Hallo gebeurtenissen toobe verzonden vanuit Hallo syslog-daemon toolocal UDP-poort 25226. Hallo-agent luistert naar binnenkomende gebeurtenissen op deze poort. Hallo Hier volgt een van de voorbeeldconfiguratie voor het verzenden van alle gebeurtenissen uit Hallo lokaal systeem toohello agent (u kunt wijzigen Hallo configuratie toofit uw lokale instellingen):

1. Open Hallo terminalvenster en ga toohello directory */etc/syslog-ng /* 
2. Maak een nieuw bestand *security-config-omsagent.conf* en voeg Hallo volgende inhoud: OMS_facility local4 =
    
    filter f_local4_oms { facility(local4); };

    destination security_oms { tcp("127.0.0.1" port(25226)); };

    log { source(src); filter(f_local4_oms); destination(security_oms); };
    
3. Hallo-bestand downloaden *security_events.conf* en plaats deze in */etc/opt/microsoft/omsagent/conf/omsagent.d/* in Hallo OMS-Agent-computer.
4. Typ de opdracht Hallo hieronder toorestart Hallo syslog-daemon: *voor syslog-ng uitvoeren:*
    
    ```
    sudo service rsyslog restart
    ```

    *Voer voor rsyslog het volgende uit:*
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. Typ de opdracht Hallo hieronder toorestart Hallo OMS-Agent:

    *Voer voor syslog-ng het volgende uit:*
    
    ```
    sudo service omsagent restart
    ```

    *Voer voor rsyslog het volgende uit:*
    
    ```
    systemctl restart omsagent
    ```
6. Onderstaande Hallo-opdracht te typen en te controleren Hallo resultaat tooconfirm er zijn geen fouten in het logboek van Hallo OMS-Agent:

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a>Verzamelde beveiligingsgebeurtenissen controleren

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

Nadat het Hallo configuratie is voltooid, gaat Hallo beveiligingsgebeurtenis toobe ingenomen door OMS-beveiliging. toovisualize deze gebeurtenissen, open Hallo logboek zoeken, typt u Hallo opdracht *Type = CommonSecurityLog* in Hallo zoekvak en druk op ENTER. Hallo volgende voorbeeld ziet u Hallo resultaat van deze opdracht u ziet dat in dit geval OMS beveiliging al beveiligingslogboeken van meerdere leveranciers ingenomen:
   
![Basislijnevaluatie in Beveiliging en controle in OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

U kunt deze zoekopdracht voor één enkele leverancier, bijvoorbeeld toovisualize online Cisco registreert, type verfijnen: *Type = CommonSecurityLog DeviceVendor = Cisco*. Hallo 'CommonSecurityLog' bevat vooraf gedefinieerde van velden voor eventuele CEF-header met inbegrip van basic extensios hello, terwijl een andere uitbreiding of 'Aangepaste extensie' of niet zal worden ingevoegd in het veld 'AdditionalExtensions'. U kunt Hallo aangepaste velden functie tooget toegewezen velden uit het. 

### <a name="accessing-computers-missing-baseline-assessment"></a>Computers openen waarop de evaluatie van de basislijn ontbreekt
OMS ondersteunt lid Hallo-basislijn domeinprofiel op Windows Server 2008 R2 up tooWindows Server 2012 R2. De basislijn voor Windows Server 2016 is nog niet helemaal klaar en wordt toegevoegd zodra deze is gepubliceerd. Alle andere besturingssystemen gescand via OMS beveiligings- en Audit basislijn beoordeling worden weergegeven onder Hallo **Computers met ontbrekende basislijn assessment** sectie.

## <a name="see-also"></a>Zie ook
In dit document, u leert hoe tooconnect uw tooOMS CEF-oplossing. toolearn meer informatie over OMS-beveiliging, Zie Hallo artikelen te volgen:

* [Overzicht van Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Bewaking en reageren tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit-oplossing](oms-security-responding-alerts.md)
* [Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite ](oms-security-monitoring-resources.md)

