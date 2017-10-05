---
title: Uw beveiligingsproducten koppelen aan de beveiligings- en controleoplossing van de Operations Management Suite (OMS) | Microsoft Docs
description: Met dit document kunt u uw beveiligingsproducten koppelen aan de beveiligings- en controleoplossing van de Operations Management Suite met behulp van Common Event Format.
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
ms.openlocfilehash: 710a1fe0ce2b7a1841187cf75f4ffb090cc161e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-your-security-products-to-the-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="46db5-103">Uw beveiligingsproducten koppelen aan de beveiligings- en controleoplossing van de Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="46db5-103">Connecting your security products to the Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="46db5-104">Met dit document kunt u uw beveiligingsproducten koppelen aan de beveiligings- en controleoplossing van de OMS.</span><span class="sxs-lookup"><span data-stu-id="46db5-104">This document helps you connect your security products into the OMS Security and Audit Solution.</span></span> <span data-ttu-id="46db5-105">De volgende bronnen worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="46db5-105">The following sources are supported:</span></span>

- <span data-ttu-id="46db5-106">Common Event Format-gebeurtenissen (CEF)</span><span class="sxs-lookup"><span data-stu-id="46db5-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="46db5-107">Cisco ASA-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="46db5-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="46db5-108">Wat is CEF?</span><span class="sxs-lookup"><span data-stu-id="46db5-108">What is CEF?</span></span>
<span data-ttu-id="46db5-109">Common Event Format (CEF) is een standaardindeling in de branche voor Syslog-berichten. De indeling wordt door veel leveranciers van beveiligingsproducten gebruikt om gebeurtenisinteroperabiliteit tussen verschillende platforms mogelijk te maken.</span><span class="sxs-lookup"><span data-stu-id="46db5-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors to allow event interoperability among different platforms.</span></span> <span data-ttu-id="46db5-110">De beveiligings- en controleoplossing van OMS biedt ondersteuning voor gegevensopname met CEF. Daardoor kunt u uw beveiligingsproducten koppelen aan OMS Security.</span><span class="sxs-lookup"><span data-stu-id="46db5-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you to connect your security products with OMS Security.</span></span> 

<span data-ttu-id="46db5-111">Als u uw gegevensbron koppelt aan OMS kunt u profiteren van de volgende mogelijkheden die onderdeel uitmaken van dit platform:</span><span class="sxs-lookup"><span data-stu-id="46db5-111">By connecting your data source to OMS, you are able to take advantage of the following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="46db5-112">Zoeken en correlatie</span><span class="sxs-lookup"><span data-stu-id="46db5-112">Search & Correlation</span></span>
- <span data-ttu-id="46db5-113">Controleren</span><span class="sxs-lookup"><span data-stu-id="46db5-113">Auditing</span></span>
- <span data-ttu-id="46db5-114">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="46db5-114">Alert</span></span>
- <span data-ttu-id="46db5-115">Bedreigingsinformatie</span><span class="sxs-lookup"><span data-stu-id="46db5-115">Threat Intelligence</span></span>
- <span data-ttu-id="46db5-116">Problemen die aandacht vereisen</span><span class="sxs-lookup"><span data-stu-id="46db5-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="46db5-117">Logboeken van beveiligingsoplossingen verzamelen</span><span class="sxs-lookup"><span data-stu-id="46db5-117">Collection of security solution logs</span></span>

<span data-ttu-id="46db5-118">OMS Security biedt ondersteuning voor het verzamelen van logboeken middels CIS via Syslogs en [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/)-logboeken.</span><span class="sxs-lookup"><span data-stu-id="46db5-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="46db5-119">In dit voorbeeld is de bron (de computer die de logboeken genereert) een Linux-computer met syslog-ng daemon. De bestemming is OMS Security.</span><span class="sxs-lookup"><span data-stu-id="46db5-119">In this example, the source (computer that generates the logs) is a Linux computer running syslog-ng daemon and the target is OMS Security.</span></span> <span data-ttu-id="46db5-120">U moet de volgende taken uitvoeren om de Linux-computer voor te bereiden:</span><span class="sxs-lookup"><span data-stu-id="46db5-120">To prepare the Linux computer you will need to perform the following tasks:</span></span>

- <span data-ttu-id="46db5-121">Download de OMS-agent voor Linux (versie 1.2.0-25 of hoger).</span><span class="sxs-lookup"><span data-stu-id="46db5-121">Download the OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="46db5-122">Volg de sectie **Korte installatiehandleiding** in [dit artikel](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) om de agent in uw werkruimte te installeren en vrij te geven.</span><span class="sxs-lookup"><span data-stu-id="46db5-122">Follow the section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) to install and onboard the agent to your workspace.</span></span>

<span data-ttu-id="46db5-123">Normaal gesproken wordt de agent op een andere computer geïnstalleerd dan op de computer waarop de logboeken worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="46db5-123">Typically, the agent is installed on a different computer from the one on which the logs are generated.</span></span> <span data-ttu-id="46db5-124">De volgende stappen zijn normaal nodig om de logboeken door te sturen naar de computer met de agent:</span><span class="sxs-lookup"><span data-stu-id="46db5-124">Forwarding the logs to the agent machine will usually require the following steps:</span></span>

- <span data-ttu-id="46db5-125">Configureer het product/apparaat waarop de logboeken worden gemaakt zodanig dat de vereiste gebeurtenissen worden doorgestuurd naar de syslog-daemon (rsyslog of syslog-ng) op de computer met de agent.</span><span class="sxs-lookup"><span data-stu-id="46db5-125">Configure the logging product/machine to forward the required events to the syslog daemon (rsyslog or syslog-ng) on the agent machine.</span></span>
- <span data-ttu-id="46db5-126">Stel in dat de syslog-daemon op de computer met de agent berichten mag ontvangen vanaf een extern systeem.</span><span class="sxs-lookup"><span data-stu-id="46db5-126">Enable the syslog daemon on the agent machine to receive messages from a remote system.</span></span>

<span data-ttu-id="46db5-127">Op de computer met de agent moeten de gebeurtenissen vanuit de syslog-daemon worden verzonden naar lokale UDP-poort 25226.</span><span class="sxs-lookup"><span data-stu-id="46db5-127">On the agent machine, the events need to be sent from the syslog daemon to local UDP port 25226.</span></span> <span data-ttu-id="46db5-128">De agent houdt in de gaten of er gebeurtenissen binnenkomen via deze poort.</span><span class="sxs-lookup"><span data-stu-id="46db5-128">The agent is listening for incoming events on this port.</span></span> <span data-ttu-id="46db5-129">Het volgende is een voorbeeldconfiguratie voor het verzenden van alle gebeurtenissen van het lokale systeem naar de agent (u kunt de configuratie aanpassen zodat deze aansluit op uw lokale instellingen):</span><span class="sxs-lookup"><span data-stu-id="46db5-129">The following is an example configuration for sending all events from the local system to the agent (you can modify the configuration to fit your local settings):</span></span>

1. <span data-ttu-id="46db5-130">Open het terminalvenster en ga naar de map */etc/syslog-ng/*</span><span class="sxs-lookup"><span data-stu-id="46db5-130">Open the terminal window, and go to the directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="46db5-131">Maak een nieuw bestand (*security-config-omsagent.conf*) en voeg de volgende inhoud toe: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="46db5-131">Create a new file *security-config-omsagent.conf* and add the following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="46db5-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="46db5-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="46db5-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="46db5-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="46db5-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="46db5-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="46db5-135">Download het bestand *security_events.conf* en plaats het in */etc/opt/microsoft/omsagent/conf/omsagent.d/* op de computer met de OMS-agent.</span><span class="sxs-lookup"><span data-stu-id="46db5-135">Download the file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in the OMS Agent computer.</span></span>
4. <span data-ttu-id="46db5-136">Typ de volgende opdracht om opnieuw te starten van de syslog-daemon: *voor syslog-ng uitvoeren:*</span><span class="sxs-lookup"><span data-stu-id="46db5-136">Type the command below to restart the syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="46db5-137">*Voer voor rsyslog het volgende uit:*</span><span class="sxs-lookup"><span data-stu-id="46db5-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="46db5-138">Voer de onderstaande opdracht in om de OMS-agent opnieuw op te starten:</span><span class="sxs-lookup"><span data-stu-id="46db5-138">Type the command below to restart the OMS Agent:</span></span>

    <span data-ttu-id="46db5-139">*Voer voor syslog-ng het volgende uit:*</span><span class="sxs-lookup"><span data-stu-id="46db5-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="46db5-140">*Voer voor rsyslog het volgende uit:*</span><span class="sxs-lookup"><span data-stu-id="46db5-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="46db5-141">Voer de onderstaande opdracht in en bekijk het resultaat om te controleren of er fouten in het logboek van de OMS-agent staan:</span><span class="sxs-lookup"><span data-stu-id="46db5-141">Type the command below and review the result to confirm that there are no errors in the OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="46db5-142">Verzamelde beveiligingsgebeurtenissen controleren</span><span class="sxs-lookup"><span data-stu-id="46db5-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="46db5-143">Wanneer de configuratie is voltooid, wordt de beveiligingsgebeurtenis opgenomen door OMS Security.</span><span class="sxs-lookup"><span data-stu-id="46db5-143">After the configuration is over, the security event will start to be ingested by OMS Security.</span></span> <span data-ttu-id="46db5-144">Als u de gebeurtenissen wilt visualiseren, opent u Zoeken in logboeken en voert u de opdracht *Type=CommonSecurityLog* in in het zoekveld. Druk vervolgens op ENTER.</span><span class="sxs-lookup"><span data-stu-id="46db5-144">To visualize those events, open the Log Search, type the command *Type=CommonSecurityLog* in the search field and press ENTER.</span></span> <span data-ttu-id="46db5-145">In het volgende voorbeeld ziet u het resultaat van deze opdracht. In dit geval zijn in OMS Security al beveiligingslogboeken van meerdere leveranciers opgenomen:</span><span class="sxs-lookup"><span data-stu-id="46db5-145">The following example shows the result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Basislijnevaluatie in Beveiliging en controle in OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="46db5-147">U kunt deze zoekopdracht verfijnen voor één enkele leverancier om bijvoorbeeld online Cisco-logboeken te visualiseren. Typ daarvoor: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span><span class="sxs-lookup"><span data-stu-id="46db5-147">You can refine this search for one single vendor, for example, to visualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="46db5-148">CommonSecurityLog bevat vooraf gedefinieerde velden voor eventuele CEF-headers, waaronder de basisextensies. Alle andere extensies, of dat nu aangepaste extensies zijn of niet, worden ingevoerd in het veld AdditionalExtensions.</span><span class="sxs-lookup"><span data-stu-id="46db5-148">The “CommonSecurityLog” has predefined fields for any CEF header including the basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="46db5-149">U kunt de functie Aangepaste velden gebruiken voor speciale velden.</span><span class="sxs-lookup"><span data-stu-id="46db5-149">You can use the Custom Fields feature to get dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="46db5-150">Computers openen waarop de evaluatie van de basislijn ontbreekt</span><span class="sxs-lookup"><span data-stu-id="46db5-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="46db5-151">OMS ondersteunt het basislijnprofiel van het domeinlid op Windows Server 2008 R2 tot en met Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="46db5-151">OMS supports the domain member baseline profile on Windows Server 2008 R2 up to Windows Server 2012 R2.</span></span> <span data-ttu-id="46db5-152">De basislijn voor Windows Server 2016 is nog niet helemaal klaar en wordt toegevoegd zodra deze is gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="46db5-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="46db5-153">Alle andere besturingssystemen die via basislijnevaluatie in Beveiliging en controle in OMS zijn gescand, worden weergegeven onder de sectie **Computers waarop de evaluatie van de basislijn ontbreekt**.</span><span class="sxs-lookup"><span data-stu-id="46db5-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under the **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="46db5-154">Zie ook</span><span class="sxs-lookup"><span data-stu-id="46db5-154">See also</span></span>
<span data-ttu-id="46db5-155">In dit document hebt u geleerd hoe u uw CEF-oplossing koppelt aan OMS.</span><span class="sxs-lookup"><span data-stu-id="46db5-155">In this document, you learned how to connect your CEF solution to OMS.</span></span> <span data-ttu-id="46db5-156">Raadpleeg de volgende artikelen voor meer informatie over OMS Beveiliging:</span><span class="sxs-lookup"><span data-stu-id="46db5-156">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="46db5-157">Overzicht van Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="46db5-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="46db5-158">Beveiligingswaarschuwingen in de oplossing Beveiliging en controle van Operations Management Suite bewaken en erop reageren</span><span class="sxs-lookup"><span data-stu-id="46db5-158">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="46db5-159">Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite </span><span class="sxs-lookup"><span data-stu-id="46db5-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

