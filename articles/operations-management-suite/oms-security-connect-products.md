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
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="7e28c-103">Verbinding maken met de beveiliging producten toohello Operations Management Suite (OMS) beveiliging en Audit-oplossing</span><span class="sxs-lookup"><span data-stu-id="7e28c-103">Connecting your security products toohello Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="7e28c-104">Dit document helpt u uw beveiligingsproducten verbinding naar hello OMS beveiligings- en Audit-oplossing.</span><span class="sxs-lookup"><span data-stu-id="7e28c-104">This document helps you connect your security products into hello OMS Security and Audit Solution.</span></span> <span data-ttu-id="7e28c-105">Hallo de volgende bronnen worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="7e28c-105">hello following sources are supported:</span></span>

- <span data-ttu-id="7e28c-106">Common Event Format-gebeurtenissen (CEF)</span><span class="sxs-lookup"><span data-stu-id="7e28c-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="7e28c-107">Cisco ASA-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="7e28c-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="7e28c-108">Wat is CEF?</span><span class="sxs-lookup"><span data-stu-id="7e28c-108">What is CEF?</span></span>
<span data-ttu-id="7e28c-109">Algemene gebeurtenis-indeling (CEF) is een indeling volgens de industrienorm boven op Syslog-berichten die worden gebruikt door veel beveiliging leveranciers tooallow gebeurtenis interoperabiliteit tussen verschillende platforms.</span><span class="sxs-lookup"><span data-stu-id="7e28c-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors tooallow event interoperability among different platforms.</span></span> <span data-ttu-id="7e28c-110">Ondersteuning voor gegevensopname CEF waarmee u tooconnect van uw beveiligingsproducten met OMS-beveiliging met OMS beveiligings- en Audit-oplossing.</span><span class="sxs-lookup"><span data-stu-id="7e28c-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you tooconnect your security products with OMS Security.</span></span> 

<span data-ttu-id="7e28c-111">U bent tootake kunnen profiteren van Hallo na mogelijkheden die deel van dit platform uitmaken door verbinding te maken van uw gegevensbron tooOMS:</span><span class="sxs-lookup"><span data-stu-id="7e28c-111">By connecting your data source tooOMS, you are able tootake advantage of hello following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="7e28c-112">Zoeken en correlatie</span><span class="sxs-lookup"><span data-stu-id="7e28c-112">Search & Correlation</span></span>
- <span data-ttu-id="7e28c-113">Controleren</span><span class="sxs-lookup"><span data-stu-id="7e28c-113">Auditing</span></span>
- <span data-ttu-id="7e28c-114">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="7e28c-114">Alert</span></span>
- <span data-ttu-id="7e28c-115">Bedreigingsinformatie</span><span class="sxs-lookup"><span data-stu-id="7e28c-115">Threat Intelligence</span></span>
- <span data-ttu-id="7e28c-116">Problemen die aandacht vereisen</span><span class="sxs-lookup"><span data-stu-id="7e28c-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="7e28c-117">Logboeken van beveiligingsoplossingen verzamelen</span><span class="sxs-lookup"><span data-stu-id="7e28c-117">Collection of security solution logs</span></span>

<span data-ttu-id="7e28c-118">OMS Security biedt ondersteuning voor het verzamelen van logboeken middels CIS via Syslogs en [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/)-logboeken.</span><span class="sxs-lookup"><span data-stu-id="7e28c-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="7e28c-119">In dit voorbeeld Hallo bron (de computer die Hallo logboeken genereert) is een Linux-computer met de syslog-ng daemon en Hallo doel is OMS-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="7e28c-119">In this example, hello source (computer that generates hello logs) is a Linux computer running syslog-ng daemon and hello target is OMS Security.</span></span> <span data-ttu-id="7e28c-120">tooprepare hello Linux-computer moet u tooperform Hallo volgende taken:</span><span class="sxs-lookup"><span data-stu-id="7e28c-120">tooprepare hello Linux computer you will need tooperform hello following tasks:</span></span>

- <span data-ttu-id="7e28c-121">Hallo OMS-Agent downloaden voor Linux, versie 1.2.0-25 of hoger.</span><span class="sxs-lookup"><span data-stu-id="7e28c-121">Download hello OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="7e28c-122">Ga als volgt Hallo sectie **snelle handleiding installeren** van [in dit artikel](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall en vrijgeven Hallo agent tooyour werkruimte.</span><span class="sxs-lookup"><span data-stu-id="7e28c-122">Follow hello section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall and onboard hello agent tooyour workspace.</span></span>

<span data-ttu-id="7e28c-123">Normaal gesproken is Hallo-agent geïnstalleerd op een andere computer dan Hallo één op welke Hallo-logboeken worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="7e28c-123">Typically, hello agent is installed on a different computer from hello one on which hello logs are generated.</span></span> <span data-ttu-id="7e28c-124">Doorsturen Hallo logboeken toohello-agentcomputer wordt doorgaans vereist voor Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e28c-124">Forwarding hello logs toohello agent machine will usually require hello following steps:</span></span>

- <span data-ttu-id="7e28c-125">Hallo logboekregistratie product/machine tooforward Hallo vereist gebeurtenissen toohello syslog-daemon (rsyslog of syslog-ng) op de agentcomputer Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="7e28c-125">Configure hello logging product/machine tooforward hello required events toohello syslog daemon (rsyslog or syslog-ng) on hello agent machine.</span></span>
- <span data-ttu-id="7e28c-126">Schakel Hallo syslog-daemon op Hallo agent machine tooreceive berichten van een extern systeem.</span><span class="sxs-lookup"><span data-stu-id="7e28c-126">Enable hello syslog daemon on hello agent machine tooreceive messages from a remote system.</span></span>

<span data-ttu-id="7e28c-127">Op de agentcomputer hello moeten Hallo gebeurtenissen toobe verzonden vanuit Hallo syslog-daemon toolocal UDP-poort 25226.</span><span class="sxs-lookup"><span data-stu-id="7e28c-127">On hello agent machine, hello events need toobe sent from hello syslog daemon toolocal UDP port 25226.</span></span> <span data-ttu-id="7e28c-128">Hallo-agent luistert naar binnenkomende gebeurtenissen op deze poort.</span><span class="sxs-lookup"><span data-stu-id="7e28c-128">hello agent is listening for incoming events on this port.</span></span> <span data-ttu-id="7e28c-129">Hallo Hier volgt een van de voorbeeldconfiguratie voor het verzenden van alle gebeurtenissen uit Hallo lokaal systeem toohello agent (u kunt wijzigen Hallo configuratie toofit uw lokale instellingen):</span><span class="sxs-lookup"><span data-stu-id="7e28c-129">hello following is an example configuration for sending all events from hello local system toohello agent (you can modify hello configuration toofit your local settings):</span></span>

1. <span data-ttu-id="7e28c-130">Open Hallo terminalvenster en ga toohello directory */etc/syslog-ng /*</span><span class="sxs-lookup"><span data-stu-id="7e28c-130">Open hello terminal window, and go toohello directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="7e28c-131">Maak een nieuw bestand *security-config-omsagent.conf* en voeg Hallo volgende inhoud: OMS_facility local4 =</span><span class="sxs-lookup"><span data-stu-id="7e28c-131">Create a new file *security-config-omsagent.conf* and add hello following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="7e28c-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="7e28c-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="7e28c-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="7e28c-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="7e28c-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="7e28c-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="7e28c-135">Hallo-bestand downloaden *security_events.conf* en plaats deze in */etc/opt/microsoft/omsagent/conf/omsagent.d/* in Hallo OMS-Agent-computer.</span><span class="sxs-lookup"><span data-stu-id="7e28c-135">Download hello file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in hello OMS Agent computer.</span></span>
4. <span data-ttu-id="7e28c-136">Typ de opdracht Hallo hieronder toorestart Hallo syslog-daemon: *voor syslog-ng uitvoeren:*</span><span class="sxs-lookup"><span data-stu-id="7e28c-136">Type hello command below toorestart hello syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="7e28c-137">*Voer voor rsyslog het volgende uit:*</span><span class="sxs-lookup"><span data-stu-id="7e28c-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="7e28c-138">Typ de opdracht Hallo hieronder toorestart Hallo OMS-Agent:</span><span class="sxs-lookup"><span data-stu-id="7e28c-138">Type hello command below toorestart hello OMS Agent:</span></span>

    <span data-ttu-id="7e28c-139">*Voer voor syslog-ng het volgende uit:*</span><span class="sxs-lookup"><span data-stu-id="7e28c-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="7e28c-140">*Voer voor rsyslog het volgende uit:*</span><span class="sxs-lookup"><span data-stu-id="7e28c-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="7e28c-141">Onderstaande Hallo-opdracht te typen en te controleren Hallo resultaat tooconfirm er zijn geen fouten in het logboek van Hallo OMS-Agent:</span><span class="sxs-lookup"><span data-stu-id="7e28c-141">Type hello command below and review hello result tooconfirm that there are no errors in hello OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="7e28c-142">Verzamelde beveiligingsgebeurtenissen controleren</span><span class="sxs-lookup"><span data-stu-id="7e28c-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="7e28c-143">Nadat het Hallo configuratie is voltooid, gaat Hallo beveiligingsgebeurtenis toobe ingenomen door OMS-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="7e28c-143">After hello configuration is over, hello security event will start toobe ingested by OMS Security.</span></span> <span data-ttu-id="7e28c-144">toovisualize deze gebeurtenissen, open Hallo logboek zoeken, typt u Hallo opdracht *Type = CommonSecurityLog* in Hallo zoekvak en druk op ENTER.</span><span class="sxs-lookup"><span data-stu-id="7e28c-144">toovisualize those events, open hello Log Search, type hello command *Type=CommonSecurityLog* in hello search field and press ENTER.</span></span> <span data-ttu-id="7e28c-145">Hallo volgende voorbeeld ziet u Hallo resultaat van deze opdracht u ziet dat in dit geval OMS beveiliging al beveiligingslogboeken van meerdere leveranciers ingenomen:</span><span class="sxs-lookup"><span data-stu-id="7e28c-145">hello following example shows hello result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Basislijnevaluatie in Beveiliging en controle in OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="7e28c-147">U kunt deze zoekopdracht voor één enkele leverancier, bijvoorbeeld toovisualize online Cisco registreert, type verfijnen: *Type = CommonSecurityLog DeviceVendor = Cisco*.</span><span class="sxs-lookup"><span data-stu-id="7e28c-147">You can refine this search for one single vendor, for example, toovisualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="7e28c-148">Hallo 'CommonSecurityLog' bevat vooraf gedefinieerde van velden voor eventuele CEF-header met inbegrip van basic extensios hello, terwijl een andere uitbreiding of 'Aangepaste extensie' of niet zal worden ingevoegd in het veld 'AdditionalExtensions'.</span><span class="sxs-lookup"><span data-stu-id="7e28c-148">hello “CommonSecurityLog” has predefined fields for any CEF header including hello basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="7e28c-149">U kunt Hallo aangepaste velden functie tooget toegewezen velden uit het.</span><span class="sxs-lookup"><span data-stu-id="7e28c-149">You can use hello Custom Fields feature tooget dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="7e28c-150">Computers openen waarop de evaluatie van de basislijn ontbreekt</span><span class="sxs-lookup"><span data-stu-id="7e28c-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="7e28c-151">OMS ondersteunt lid Hallo-basislijn domeinprofiel op Windows Server 2008 R2 up tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="7e28c-151">OMS supports hello domain member baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="7e28c-152">De basislijn voor Windows Server 2016 is nog niet helemaal klaar en wordt toegevoegd zodra deze is gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="7e28c-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="7e28c-153">Alle andere besturingssystemen gescand via OMS beveiligings- en Audit basislijn beoordeling worden weergegeven onder Hallo **Computers met ontbrekende basislijn assessment** sectie.</span><span class="sxs-lookup"><span data-stu-id="7e28c-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="7e28c-154">Zie ook</span><span class="sxs-lookup"><span data-stu-id="7e28c-154">See also</span></span>
<span data-ttu-id="7e28c-155">In dit document, u leert hoe tooconnect uw tooOMS CEF-oplossing.</span><span class="sxs-lookup"><span data-stu-id="7e28c-155">In this document, you learned how tooconnect your CEF solution tooOMS.</span></span> <span data-ttu-id="7e28c-156">toolearn meer informatie over OMS-beveiliging, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e28c-156">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="7e28c-157">Overzicht van Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="7e28c-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="7e28c-158">Bewaking en reageren tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit-oplossing</span><span class="sxs-lookup"><span data-stu-id="7e28c-158">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="7e28c-159">Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite </span><span class="sxs-lookup"><span data-stu-id="7e28c-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

