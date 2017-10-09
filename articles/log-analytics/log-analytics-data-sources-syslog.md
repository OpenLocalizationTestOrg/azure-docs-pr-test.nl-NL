---
title: aaaCollect en analyseren van Syslog-berichten in OMS Log Analytics | Microsoft Docs
description: Syslog is een gebeurtenis logboekregistratie-protocol die algemene tooLinux. In dit artikel wordt beschreven hoe tooconfigure verzameling van Syslog-berichten in Log Analytics en details van records Hallo ze in Hallo OMS-opslagplaats maken.
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="95a37-104">Syslog-gegevensbronnen in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="95a37-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="95a37-105">Syslog is een gebeurtenis logboekregistratie-protocol die algemene tooLinux.</span><span class="sxs-lookup"><span data-stu-id="95a37-105">Syslog is an event logging protocol that is common tooLinux.</span></span>  <span data-ttu-id="95a37-106">Toepassingen worden verzonden berichten die kunnen worden opgeslagen op de lokale machine Hallo of tooa Syslog collector geleverd.</span><span class="sxs-lookup"><span data-stu-id="95a37-106">Applications will send messages that may be stored on hello local machine or delivered tooa Syslog collector.</span></span>  <span data-ttu-id="95a37-107">Wanneer Hallo OMS-Agent voor Linux is geïnstalleerd, configureert het Hallo lokale Syslog-daemon tooforward berichten toohello agent.</span><span class="sxs-lookup"><span data-stu-id="95a37-107">When hello OMS Agent for Linux is installed, it configures hello local Syslog daemon tooforward messages toohello agent.</span></span>  <span data-ttu-id="95a37-108">Hallo-agent verzendt vervolgens Hallo-bericht tooLog Analytics waarop een record in Hallo OMS-opslagplaats is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="95a37-108">hello agent then sends hello message tooLog Analytics where a corresponding record is created in hello OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="95a37-109">Log Analytics biedt ondersteuning voor verzameling van berichten is verzonden door rsyslog of syslog-ng, waarbij rsyslog Hallo standaard daemon is.</span><span class="sxs-lookup"><span data-stu-id="95a37-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is hello default daemon.</span></span> <span data-ttu-id="95a37-110">Hallo standaard syslog-daemon op versie 5 van Red Hat Enterprise Linux en CentOS, Oracle Linux-versie (sysklog) wordt niet ondersteund voor de verzameling van syslog-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="95a37-110">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="95a37-111">toocollect syslog-gegevens van deze versie van deze verdelingen Hallo [rsyslog daemon](http://rsyslog.com) moet worden geïnstalleerd en geconfigureerd tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="95a37-111">toocollect syslog data from this version of these distributions, hello [rsyslog daemon](http://rsyslog.com) should be installed and configured tooreplace sysklog.</span></span>
>
>

![Syslog-verzameling](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="95a37-113">Syslog configureren</span><span class="sxs-lookup"><span data-stu-id="95a37-113">Configuring Syslog</span></span>
<span data-ttu-id="95a37-114">Hallo OMS-Agent voor Linux worden alleen verzameld van gebeurtenissen met de Hallo opslagruimten en de ernst die zijn opgegeven in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="95a37-114">hello OMS Agent for Linux will only collect events with hello facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="95a37-115">U kunt Syslog configureren via Hallo OMS-portal of met het beheren van configuratiebestanden op uw Linux-agents.</span><span class="sxs-lookup"><span data-stu-id="95a37-115">You can configure Syslog through hello OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-hello-oms-portal"></a><span data-ttu-id="95a37-116">Syslog in Hallo OMS-portal configureren</span><span class="sxs-lookup"><span data-stu-id="95a37-116">Configure Syslog in hello OMS portal</span></span>
<span data-ttu-id="95a37-117">Syslog configureren vanuit Hallo [menu Data in logboekanalyse-instellingen](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="95a37-117">Configure Syslog from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="95a37-118">Deze configuratie wordt doorgegeven toohello-configuratiebestand op elke Linux-agent.</span><span class="sxs-lookup"><span data-stu-id="95a37-118">This configuration is delivered toohello configuration file on each Linux agent.</span></span>

<span data-ttu-id="95a37-119">U kunt een nieuwe opslagruimte toevoegen door in de naam te typen en op  **+** .</span><span class="sxs-lookup"><span data-stu-id="95a37-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="95a37-120">Voor elke faciliteit worden alleen berichten met Hallo geselecteerd ernst verzameld.</span><span class="sxs-lookup"><span data-stu-id="95a37-120">For each facility, only messages with hello selected severities will be collected.</span></span>  <span data-ttu-id="95a37-121">Hallo ernstcategorieën voor bepaalde Hallo-opslagruimte die u toocollect wilt controleren.</span><span class="sxs-lookup"><span data-stu-id="95a37-121">Check hello severities for hello particular facility that you want toocollect.</span></span>  <span data-ttu-id="95a37-122">U kan niet alle aanvullende criteria opgeven toofilter berichten.</span><span class="sxs-lookup"><span data-stu-id="95a37-122">You cannot provide any additional criteria toofilter messages.</span></span>

![Syslog configureren](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="95a37-124">Standaard zijn alle configuratiewijzigingen tooall agents automatisch gepusht.</span><span class="sxs-lookup"><span data-stu-id="95a37-124">By default, all configuration changes are automatically pushed tooall agents.</span></span>  <span data-ttu-id="95a37-125">Als u tooconfigure Syslog handmatig op elke Linux-agent wilt, schakelt u Hallo vak *toepassen onder configuratie toomy Linux-machines*.</span><span class="sxs-lookup"><span data-stu-id="95a37-125">If you want tooconfigure Syslog manually on each Linux agent, then uncheck hello box *Apply below configuration toomy Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="95a37-126">Syslog op Linux-agent configureren</span><span class="sxs-lookup"><span data-stu-id="95a37-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="95a37-127">Wanneer Hallo [OMS-agent is geïnstalleerd op een client voor Linux](log-analytics-linux-agents.md), het installeren van een standaard syslog-configuratiebestand dat Hallo-faciliteit definieert en ernst van het Hallo-berichten die worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="95a37-127">When hello [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines hello facility and severity of hello messages that are collected.</span></span>  <span data-ttu-id="95a37-128">U kunt dit bestand toochange Hallo-configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="95a37-128">You can modify this file toochange hello configuration.</span></span>  <span data-ttu-id="95a37-129">Hallo-configuratiebestand is verschillend, afhankelijk van Hallo Syslog-daemon die Hallo van client is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="95a37-129">hello configuration file is different depending on hello Syslog daemon that hello client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="95a37-130">Als u syslog-configuratie Hallo bewerkt, moet u Hallo syslog-daemon voor Hallo wijzigingen tootake effect opnieuw.</span><span class="sxs-lookup"><span data-stu-id="95a37-130">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="95a37-131">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="95a37-131">rsyslog</span></span>
<span data-ttu-id="95a37-132">Hallo-configuratiebestand voor rsyslog bevindt zich op **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="95a37-132">hello configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="95a37-133">De Standaardinhoud worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="95a37-133">Its default contents are shown below.</span></span>  <span data-ttu-id="95a37-134">Hiermee verzamelt syslog-berichten is verzonden vanaf de lokale agent Hallo voor alle installaties met een niveau van de waarschuwing of hoger.</span><span class="sxs-lookup"><span data-stu-id="95a37-134">This collects syslog messages sent from hello local agent for all facilities with a level of warning or higher.</span></span>

    kern.warning       @127.0.0.1:25224
    user.warning       @127.0.0.1:25224
    daemon.warning     @127.0.0.1:25224
    auth.warning       @127.0.0.1:25224
    syslog.warning     @127.0.0.1:25224
    uucp.warning       @127.0.0.1:25224
    authpriv.warning   @127.0.0.1:25224
    ftp.warning        @127.0.0.1:25224
    cron.warning       @127.0.0.1:25224
    local0.warning     @127.0.0.1:25224
    local1.warning     @127.0.0.1:25224
    local2.warning     @127.0.0.1:25224
    local3.warning     @127.0.0.1:25224
    local4.warning     @127.0.0.1:25224
    local5.warning     @127.0.0.1:25224
    local6.warning     @127.0.0.1:25224
    local7.warning     @127.0.0.1:25224

<span data-ttu-id="95a37-135">U kunt een faciliteit verwijderen door het verwijderen van de sectie van Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="95a37-135">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="95a37-136">Hallo ernst die door het wijzigen van deze faciliteit vermelding voor een bepaalde opslagruimte worden verzameld, kunt u beperken.</span><span class="sxs-lookup"><span data-stu-id="95a37-136">You can limit hello severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="95a37-137">Bijvoorbeeld toolimit Hallo gebruiker faciliteit toomessages met een ernst van de fout of hoger wijzigt u deze regel Hallo configuratie bestand toohello te volgen:</span><span class="sxs-lookup"><span data-stu-id="95a37-137">For example, toolimit hello user facility toomessages with a severity of error or higher you would modify that line of hello configuration file toohello following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="95a37-138">Syslog-ng</span><span class="sxs-lookup"><span data-stu-id="95a37-138">syslog-ng</span></span>
<span data-ttu-id="95a37-139">Hallo-configuratiebestand voor de syslog-ng is de locatie op **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="95a37-139">hello configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="95a37-140">De Standaardinhoud worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="95a37-140">Its default contents are shown below.</span></span>  <span data-ttu-id="95a37-141">Dit verzamelt syslog-berichten is verzonden vanaf de lokale agent Hallo voor alle installaties en alles.</span><span class="sxs-lookup"><span data-stu-id="95a37-141">This collects syslog messages sent from hello local agent for all facilities and all severities.</span></span>   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

<span data-ttu-id="95a37-142">U kunt een faciliteit verwijderen door het verwijderen van de sectie van Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="95a37-142">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="95a37-143">Hallo ernst die door deze te verwijderen uit de lijst voor een bepaalde opslagruimte worden verzameld, kunt u beperken.</span><span class="sxs-lookup"><span data-stu-id="95a37-143">You can limit hello severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="95a37-144">Bijvoorbeeld: toolimit Hallo gebruiker faciliteit toojust waarschuwingen en kritieke berichten, wijzigt u die sectie van Hallo configuratie bestand toohello te volgen:</span><span class="sxs-lookup"><span data-stu-id="95a37-144">For example, toolimit hello user facility toojust alert and critical messages, you would modify that section of hello configuration file toohello following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="95a37-145">Verzamelen van gegevens van aanvullende Syslog-poorten</span><span class="sxs-lookup"><span data-stu-id="95a37-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="95a37-146">Hallo OMS-agent luistert naar de Syslog-berichten op de lokale client Hallo op poort 25224.</span><span class="sxs-lookup"><span data-stu-id="95a37-146">hello OMS agent listens for Syslog messages on hello local client on port 25224.</span></span>  <span data-ttu-id="95a37-147">Wanneer het Hallo-agent is geïnstalleerd, wordt een standaardconfiguratie syslog toegepast en gevonden in Hallo locatie te volgen:</span><span class="sxs-lookup"><span data-stu-id="95a37-147">When hello agent is installed, a default syslog configuration is applied and found in hello following location:</span></span>

* <span data-ttu-id="95a37-148">Rsyslog:`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="95a37-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="95a37-149">Syslog-ng:`/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="95a37-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="95a37-150">U kunt Hallo poortnummer wijzigen door het maken van twee configuratiebestanden: een configuratiebestand FluentD en een bestand rsyslog of syslog-ng, afhankelijk van Hallo Syslog-daemon is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="95a37-150">You can change hello port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on hello Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="95a37-151">Hallo FluentD config-bestand moet een nieuw bestand in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` en vervang de waarde in Hallo Hallo **poort** vermelding met het nummer van uw aangepaste poort.</span><span class="sxs-lookup"><span data-stu-id="95a37-151">hello FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace hello value in hello **port** entry with your custom port number.</span></span>

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* <span data-ttu-id="95a37-152">Voor rsyslog, moet u een nieuw configuratiebestand in maken: `/etc/rsyslog.d/` en Hallo waarde % SYSLOG_PORT % vervangt door uw aangepast poortnummer.</span><span class="sxs-lookup"><span data-stu-id="95a37-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace hello value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="95a37-153">Als u deze waarde in het configuratiebestand Hallo wijzigt `95-omsagent.conf`, wordt deze overschreven wanneer Hallo-agent van toepassing een standaardconfiguratie is.</span><span class="sxs-lookup"><span data-stu-id="95a37-153">If you modify this value in hello configuration file `95-omsagent.conf`, it will be overwritten when hello agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="95a37-154">Hallo syslog ng config moet worden gewijzigd door te kopiëren Hallo voorbeeldconfiguratie hieronder wordt weergegeven en toe te voegen Hallo aangepaste gewijzigde instellingen toohello einde van Hallo syslog-ng.conf-configuratiebestand te vinden in `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="95a37-154">hello syslog-ng config should be modified by copying hello example configuration shown below and adding hello custom modified settings toohello end of hello syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="95a37-155">Doen **niet** standaardlabel hello gebruiken **% WORKSPACE_ID % _oms** of **% WORKSPACE_ID_OMS**, definieert u een aangepast label toohelp onderscheid uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="95a37-155">Do **not** use hello default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label toohelp distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="95a37-156">Als u standaardwaarden Hallo in het configuratiebestand Hallo wijzigt, wordt deze overschreven wanneer Hallo-agent van toepassing een standaardconfiguratie is.</span><span class="sxs-lookup"><span data-stu-id="95a37-156">If you modify hello default values in hello configuration file, they will be overwritten when hello agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="95a37-157">Na het voltooien van Hallo wijzigingen, Hallo Syslog en Hallo moet OMS-agent-service opnieuw gestart toobe tooensure Hallo configuratie wijzigingen pas van kracht.</span><span class="sxs-lookup"><span data-stu-id="95a37-157">After completing hello changes, hello Syslog and hello OMS agent service needs toobe restarted tooensure hello configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="95a37-158">Eigenschappen van de record Syslog</span><span class="sxs-lookup"><span data-stu-id="95a37-158">Syslog record properties</span></span>
<span data-ttu-id="95a37-159">Syslog-records hebben een soort **Syslog** en Hallo eigenschappen in de volgende tabel Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="95a37-159">Syslog records have a type of **Syslog** and have hello properties in hello following table.</span></span>

| <span data-ttu-id="95a37-160">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="95a37-160">Property</span></span> | <span data-ttu-id="95a37-161">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="95a37-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="95a37-162">Computer</span><span class="sxs-lookup"><span data-stu-id="95a37-162">Computer</span></span> |<span data-ttu-id="95a37-163">Computer die gebeurtenis Hallo is verzameld.</span><span class="sxs-lookup"><span data-stu-id="95a37-163">Computer that hello event was collected from.</span></span> |
| <span data-ttu-id="95a37-164">Opslagruimte</span><span class="sxs-lookup"><span data-stu-id="95a37-164">Facility</span></span> |<span data-ttu-id="95a37-165">Hiermee definieert u Hallo-onderdeel van het Hallo-systeem dat het Hallo-bericht heeft gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="95a37-165">Defines hello part of hello system that generated hello message.</span></span> |
| <span data-ttu-id="95a37-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="95a37-166">HostIP</span></span> |<span data-ttu-id="95a37-167">IP-adres van het Hallo-bericht verzenden Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="95a37-167">IP address of hello system sending hello message.</span></span> |
| <span data-ttu-id="95a37-168">Hostnaam</span><span class="sxs-lookup"><span data-stu-id="95a37-168">HostName</span></span> |<span data-ttu-id="95a37-169">Naam van Hallo Hallo-bericht verzenden.</span><span class="sxs-lookup"><span data-stu-id="95a37-169">Name of hello system sending hello message.</span></span> |
| <span data-ttu-id="95a37-170">Foutcode</span><span class="sxs-lookup"><span data-stu-id="95a37-170">SeverityLevel</span></span> |<span data-ttu-id="95a37-171">Ernst van gebeurtenis Hallo.</span><span class="sxs-lookup"><span data-stu-id="95a37-171">Severity level of hello event.</span></span> |
| <span data-ttu-id="95a37-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="95a37-172">SyslogMessage</span></span> |<span data-ttu-id="95a37-173">Tekst van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="95a37-173">Text of hello message.</span></span> |
| <span data-ttu-id="95a37-174">Proces-id</span><span class="sxs-lookup"><span data-stu-id="95a37-174">ProcessID</span></span> |<span data-ttu-id="95a37-175">ID van Hallo-proces dat het Hallo-bericht gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="95a37-175">ID of hello process that generated hello message.</span></span> |
| <span data-ttu-id="95a37-176">eventTime</span><span class="sxs-lookup"><span data-stu-id="95a37-176">EventTime</span></span> |<span data-ttu-id="95a37-177">Datum en tijd waarop Hallo gebeurtenis is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="95a37-177">Date and time that hello event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="95a37-178">Logboek-query's met Syslog-records</span><span class="sxs-lookup"><span data-stu-id="95a37-178">Log queries with Syslog records</span></span>
<span data-ttu-id="95a37-179">Hallo bevat volgende tabel voorbeelden van logboek-query's die Syslog-records ophalen.</span><span class="sxs-lookup"><span data-stu-id="95a37-179">hello following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="95a37-180">Query’s uitvoeren</span><span class="sxs-lookup"><span data-stu-id="95a37-180">Query</span></span> | <span data-ttu-id="95a37-181">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="95a37-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="95a37-182">Type = Syslog</span><span class="sxs-lookup"><span data-stu-id="95a37-182">Type=Syslog</span></span> |<span data-ttu-id="95a37-183">Alle Syslogs.</span><span class="sxs-lookup"><span data-stu-id="95a37-183">All Syslogs.</span></span> |
| <span data-ttu-id="95a37-184">Type = Syslog SeverityLevel fout =</span><span class="sxs-lookup"><span data-stu-id="95a37-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="95a37-185">Alle Syslog-records met de ernst van de fout.</span><span class="sxs-lookup"><span data-stu-id="95a37-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="95a37-186">Type = Syslog &#124; meting count() door Computer</span><span class="sxs-lookup"><span data-stu-id="95a37-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="95a37-187">Telling van Syslog-records op de computer.</span><span class="sxs-lookup"><span data-stu-id="95a37-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="95a37-188">Type = Syslog &#124; meting count() door faciliteit</span><span class="sxs-lookup"><span data-stu-id="95a37-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="95a37-189">Telling van Syslog-records door de faciliteit.</span><span class="sxs-lookup"><span data-stu-id="95a37-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="95a37-190">Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query's toohello volgende wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="95a37-190">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="95a37-191">Query’s uitvoeren</span><span class="sxs-lookup"><span data-stu-id="95a37-191">Query</span></span> | <span data-ttu-id="95a37-192">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="95a37-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="95a37-193">Syslog</span><span class="sxs-lookup"><span data-stu-id="95a37-193">Syslog</span></span> |<span data-ttu-id="95a37-194">Alle Syslogs.</span><span class="sxs-lookup"><span data-stu-id="95a37-194">All Syslogs.</span></span> |
| <span data-ttu-id="95a37-195">Syslog &#124; waar foutcode == "error"</span><span class="sxs-lookup"><span data-stu-id="95a37-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="95a37-196">Alle Syslog-records met de ernst van de fout.</span><span class="sxs-lookup"><span data-stu-id="95a37-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="95a37-197">Syslog &#124; overzicht van AggregatedValue = count() door Computer</span><span class="sxs-lookup"><span data-stu-id="95a37-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="95a37-198">Telling van Syslog-records op de computer.</span><span class="sxs-lookup"><span data-stu-id="95a37-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="95a37-199">Syslog &#124; overzicht van AggregatedValue count() door faciliteit =</span><span class="sxs-lookup"><span data-stu-id="95a37-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="95a37-200">Telling van Syslog-records door de faciliteit.</span><span class="sxs-lookup"><span data-stu-id="95a37-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="95a37-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="95a37-201">Next steps</span></span>
* <span data-ttu-id="95a37-202">Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen.</span><span class="sxs-lookup"><span data-stu-id="95a37-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
* <span data-ttu-id="95a37-203">Gebruik [aangepaste velden](log-analytics-custom-fields.md) tooparse gegevens van syslog-records in afzonderlijke velden.</span><span class="sxs-lookup"><span data-stu-id="95a37-203">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="95a37-204">[Linux-agents configureren](log-analytics-linux-agents.md) toocollect andere typen gegevens.</span><span class="sxs-lookup"><span data-stu-id="95a37-204">[Configure Linux agents](log-analytics-linux-agents.md) toocollect other types of data.</span></span>
