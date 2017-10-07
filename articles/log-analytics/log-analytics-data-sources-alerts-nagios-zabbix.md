---
title: aaaCollect Nagios en Zabbix waarschuwingen in OMS Log Analytics | Microsoft Docs
description: Nagios en Zabbix zijn open-source hulpprogramma's voor controle. U kunt verzamelen waarschuwingen van deze hulpprogramma's in logboekanalyse in volgorde tooanalyze ze samen met waarschuwingen uit andere bronnen.  Dit artikel wordt beschreven hoe tooconfigure Hallo OMS-Agent voor Linux toocollect waarschuwingen uit deze systemen.
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="34bd9-105">Waarschuwingen verzamelen van Nagios en Zabbix in logboekanalyse van OMS-Agent voor Linux</span><span class="sxs-lookup"><span data-stu-id="34bd9-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="34bd9-106">[Nagios](https://www.nagios.org/) en [Zabbix](http://www.zabbix.com/) open-source hulpprogramma's voor controle zijn.</span><span class="sxs-lookup"><span data-stu-id="34bd9-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="34bd9-107">U kunt verzamelen waarschuwingen van deze hulpprogramma's in logboekanalyse in volgorde tooanalyze ze samen met [waarschuwingen uit andere bronnen](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="34bd9-107">You can collect alerts from these tools into Log Analytics in order tooanalyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="34bd9-108">Dit artikel wordt beschreven hoe tooconfigure Hallo OMS-Agent voor Linux toocollect waarschuwingen uit deze systemen.</span><span class="sxs-lookup"><span data-stu-id="34bd9-108">This article describes how tooconfigure hello OMS Agent for Linux toocollect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="34bd9-109">Verzamelen van waarschuwingen configureren</span><span class="sxs-lookup"><span data-stu-id="34bd9-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="34bd9-110">Nagios verzamelen van waarschuwingen configureren</span><span class="sxs-lookup"><span data-stu-id="34bd9-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="34bd9-111">Hallo volgende stappen uit op waarschuwingen toocollect hello Nagios-servers uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="34bd9-111">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="34bd9-112">Verleen Hallo gebruiker **omsagent** leestoegang toohello Nagios-logboekbestand (dat wil zeggen `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="34bd9-112">Grant hello user **omsagent** read access toohello Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="34bd9-113">Ervan uitgaande dat Hallo nagios.log bestand eigendom is van de groep Hallo `nagios`, kunt u Hallo gebruiker toevoegen **omsagent** toohello **nagios** groep.</span><span class="sxs-lookup"><span data-stu-id="34bd9-113">Assuming hello nagios.log file is owned by hello group `nagios`, you can add hello user **omsagent** toohello **nagios** group.</span></span> 

    <span data-ttu-id="34bd9-114">sudo usermod - a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="34bd9-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="34bd9-115">Hallo-configuratiebestand op wijzigen (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="34bd9-115">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="34bd9-116">Zorg ervoor Hallo volgende vermeldingen zijn aanwezig en niet opmerkingen uit:</span><span class="sxs-lookup"><span data-stu-id="34bd9-116">Ensure hello following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="34bd9-117">Hallo omsagent daemon starten</span><span class="sxs-lookup"><span data-stu-id="34bd9-117">Restart hello omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="34bd9-118">Zabbix verzamelen van waarschuwingen configureren</span><span class="sxs-lookup"><span data-stu-id="34bd9-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="34bd9-119">toocollect waarschuwingen van een Zabbix-server, moet u een gebruiker toospecify en het wachtwoord in *leesbare tekst*.</span><span class="sxs-lookup"><span data-stu-id="34bd9-119">toocollect alerts from a Zabbix server, you need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="34bd9-120">Dit is niet ideaal, maar we raden u Hallo-gebruiker maken en verlenen van machtigingen toomonitor onlu.</span><span class="sxs-lookup"><span data-stu-id="34bd9-120">This is not ideal, but we recommend that you create hello user and grant permissions toomonitor onlu.</span></span>

<span data-ttu-id="34bd9-121">Hallo volgende stappen uit op waarschuwingen toocollect hello Nagios-servers uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="34bd9-121">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="34bd9-122">Hallo-configuratiebestand op wijzigen (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="34bd9-122">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="34bd9-123">Zorg ervoor Hallo volgende vermeldingen zijn aanwezig en niet opmerkingen uit.  Hallo gebruiker naam en het wachtwoord toovalues voor uw omgeving Zabbix wijzigen.</span><span class="sxs-lookup"><span data-stu-id="34bd9-123">Ensure hello following entries are present and not commented out.  Change hello user name and password toovalues for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="34bd9-124">Hallo omsagent daemon starten</span><span class="sxs-lookup"><span data-stu-id="34bd9-124">Restart hello omsagent daemon</span></span>

    <span data-ttu-id="34bd9-125">sudo servicel /opt/microsoft/omsagent/bin/service_control opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="34bd9-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="34bd9-126">Waarschuwing records</span><span class="sxs-lookup"><span data-stu-id="34bd9-126">Alert records</span></span>
<span data-ttu-id="34bd9-127">U kunt waarschuwingen records ophalen uit Nagios en Zabbix met [Meld zoekopdrachten](log-analytics-log-searches.md) in logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="34bd9-127">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="34bd9-128">Waarschuwing Nagios records</span><span class="sxs-lookup"><span data-stu-id="34bd9-128">Nagios Alert records</span></span>

<span data-ttu-id="34bd9-129">Waarschuwing die is verzameld door Nagios-records hebben een **Type** van **waarschuwing** en een **SourceSystem** van **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="34bd9-129">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="34bd9-130">Ze hebben Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="34bd9-130">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="34bd9-131">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34bd9-131">Property</span></span> | <span data-ttu-id="34bd9-132">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34bd9-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="34bd9-133">Type</span><span class="sxs-lookup"><span data-stu-id="34bd9-133">Type</span></span> |<span data-ttu-id="34bd9-134">*Een waarschuwing*</span><span class="sxs-lookup"><span data-stu-id="34bd9-134">*Alert*</span></span> |
| <span data-ttu-id="34bd9-135">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="34bd9-135">SourceSystem</span></span> |<span data-ttu-id="34bd9-136">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="34bd9-136">*Nagios*</span></span> |
| <span data-ttu-id="34bd9-137">AlertName</span><span class="sxs-lookup"><span data-stu-id="34bd9-137">AlertName</span></span> |<span data-ttu-id="34bd9-138">Naam van het Hallo-waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="34bd9-138">Name of hello alert.</span></span> |
| <span data-ttu-id="34bd9-139">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="34bd9-139">AlertDescription</span></span> | <span data-ttu-id="34bd9-140">Beschrijving van waarschuwing Hallo.</span><span class="sxs-lookup"><span data-stu-id="34bd9-140">Description of hello alert.</span></span> |
| <span data-ttu-id="34bd9-141">AlertState</span><span class="sxs-lookup"><span data-stu-id="34bd9-141">AlertState</span></span> | <span data-ttu-id="34bd9-142">Status van het Hallo-service of de host.</span><span class="sxs-lookup"><span data-stu-id="34bd9-142">Status of hello service or host.</span></span><br><br><span data-ttu-id="34bd9-143">OK</span><span class="sxs-lookup"><span data-stu-id="34bd9-143">OK</span></span><br><span data-ttu-id="34bd9-144">WAARSCHUWING</span><span class="sxs-lookup"><span data-stu-id="34bd9-144">WARNING</span></span><br><span data-ttu-id="34bd9-145">OMHOOG</span><span class="sxs-lookup"><span data-stu-id="34bd9-145">UP</span></span><br><span data-ttu-id="34bd9-146">OMLAAG</span><span class="sxs-lookup"><span data-stu-id="34bd9-146">DOWN</span></span> |
| <span data-ttu-id="34bd9-147">Hostnaam</span><span class="sxs-lookup"><span data-stu-id="34bd9-147">HostName</span></span> | <span data-ttu-id="34bd9-148">Naam van het Hallo-host die Hallo waarschuwing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="34bd9-148">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="34bd9-149">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="34bd9-149">PriorityNumber</span></span> | <span data-ttu-id="34bd9-150">Het prioriteitsniveau van Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="34bd9-150">Priority level of hello alert.</span></span> |
| <span data-ttu-id="34bd9-151">StateType</span><span class="sxs-lookup"><span data-stu-id="34bd9-151">StateType</span></span> | <span data-ttu-id="34bd9-152">Hallo-type van de status van waarschuwing Hallo.</span><span class="sxs-lookup"><span data-stu-id="34bd9-152">hello type of state of hello alert.</span></span><br><br><span data-ttu-id="34bd9-153">SOFT - probleem dat niet opnieuw is gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="34bd9-153">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="34bd9-154">HARDE - probleem dat is een opgegeven aantal keren opnieuw gecontroleerd.</span><span class="sxs-lookup"><span data-stu-id="34bd9-154">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="34bd9-155">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="34bd9-155">TimeGenerated</span></span> |<span data-ttu-id="34bd9-156">Datum en tijd Hallo waarschuwing is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="34bd9-156">Date and time hello alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="34bd9-157">Waarschuwing Zabbix-records</span><span class="sxs-lookup"><span data-stu-id="34bd9-157">Zabbix alert records</span></span>
<span data-ttu-id="34bd9-158">Waarschuwing die is verzameld door Zabbix-records hebben een **Type** van **waarschuwing** en een **SourceSystem** van **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="34bd9-158">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="34bd9-159">Ze hebben Hallo eigenschappen in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="34bd9-159">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="34bd9-160">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34bd9-160">Property</span></span> | <span data-ttu-id="34bd9-161">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34bd9-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="34bd9-162">Type</span><span class="sxs-lookup"><span data-stu-id="34bd9-162">Type</span></span> |<span data-ttu-id="34bd9-163">*Een waarschuwing*</span><span class="sxs-lookup"><span data-stu-id="34bd9-163">*Alert*</span></span> |
| <span data-ttu-id="34bd9-164">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="34bd9-164">SourceSystem</span></span> |<span data-ttu-id="34bd9-165">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="34bd9-165">*Zabbix*</span></span> |
| <span data-ttu-id="34bd9-166">AlertName</span><span class="sxs-lookup"><span data-stu-id="34bd9-166">AlertName</span></span> | <span data-ttu-id="34bd9-167">Naam van het Hallo-waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="34bd9-167">Name of hello alert.</span></span> |
| <span data-ttu-id="34bd9-168">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="34bd9-168">AlertPriority</span></span> | <span data-ttu-id="34bd9-169">Ernst van waarschuwing Hallo.</span><span class="sxs-lookup"><span data-stu-id="34bd9-169">Severity of hello alert.</span></span><br><br><span data-ttu-id="34bd9-170">niet geclassificeerd</span><span class="sxs-lookup"><span data-stu-id="34bd9-170">not classified</span></span><br><span data-ttu-id="34bd9-171">Informatie</span><span class="sxs-lookup"><span data-stu-id="34bd9-171">information</span></span><br><span data-ttu-id="34bd9-172">Waarschuwing</span><span class="sxs-lookup"><span data-stu-id="34bd9-172">warning</span></span><br><span data-ttu-id="34bd9-173">Gemiddelde</span><span class="sxs-lookup"><span data-stu-id="34bd9-173">average</span></span><br><span data-ttu-id="34bd9-174">Hoog</span><span class="sxs-lookup"><span data-stu-id="34bd9-174">high</span></span><br><span data-ttu-id="34bd9-175">noodherstel</span><span class="sxs-lookup"><span data-stu-id="34bd9-175">disaster</span></span>  |
| <span data-ttu-id="34bd9-176">AlertState</span><span class="sxs-lookup"><span data-stu-id="34bd9-176">AlertState</span></span> | <span data-ttu-id="34bd9-177">De status van waarschuwing Hallo.</span><span class="sxs-lookup"><span data-stu-id="34bd9-177">State of hello alert.</span></span><br><br><span data-ttu-id="34bd9-178">0 - status is maximaal toodate.</span><span class="sxs-lookup"><span data-stu-id="34bd9-178">0 - State is up toodate.</span></span><br><span data-ttu-id="34bd9-179">1 - status is onbekend.</span><span class="sxs-lookup"><span data-stu-id="34bd9-179">1 - State is unknown.</span></span>  |
| <span data-ttu-id="34bd9-180">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="34bd9-180">AlertTypeNumber</span></span> | <span data-ttu-id="34bd9-181">Hiermee geeft u op of in een waarschuwing meerdere gebeurtenissen van het probleem kan worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="34bd9-181">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="34bd9-182">0 - status is maximaal toodate.</span><span class="sxs-lookup"><span data-stu-id="34bd9-182">0 - State is up toodate.</span></span><br><span data-ttu-id="34bd9-183">1 - status is onbekend.</span><span class="sxs-lookup"><span data-stu-id="34bd9-183">1 - State is unknown.</span></span>    |
| <span data-ttu-id="34bd9-184">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="34bd9-184">Comments</span></span> | <span data-ttu-id="34bd9-185">Aanvullende opmerkingen voor waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="34bd9-185">Additional comments for alert.</span></span> |
| <span data-ttu-id="34bd9-186">Hostnaam</span><span class="sxs-lookup"><span data-stu-id="34bd9-186">HostName</span></span> | <span data-ttu-id="34bd9-187">Naam van het Hallo-host die Hallo waarschuwing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="34bd9-187">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="34bd9-188">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="34bd9-188">PriorityNumber</span></span> | <span data-ttu-id="34bd9-189">Waarde die aangeeft ernst van waarschuwing Hallo.</span><span class="sxs-lookup"><span data-stu-id="34bd9-189">Value indicating severity of hello alert.</span></span><br><br><span data-ttu-id="34bd9-190">0 - niet geclassificeerd</span><span class="sxs-lookup"><span data-stu-id="34bd9-190">0 - not classified</span></span><br><span data-ttu-id="34bd9-191">1 - informatie</span><span class="sxs-lookup"><span data-stu-id="34bd9-191">1 - information</span></span><br><span data-ttu-id="34bd9-192">2 - waarschuwing</span><span class="sxs-lookup"><span data-stu-id="34bd9-192">2 - warning</span></span><br><span data-ttu-id="34bd9-193">3 - gemiddelde</span><span class="sxs-lookup"><span data-stu-id="34bd9-193">3 - average</span></span><br><span data-ttu-id="34bd9-194">4 - hoog</span><span class="sxs-lookup"><span data-stu-id="34bd9-194">4 - high</span></span><br><span data-ttu-id="34bd9-195">5 - noodherstel</span><span class="sxs-lookup"><span data-stu-id="34bd9-195">5 - disaster</span></span> |
| <span data-ttu-id="34bd9-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="34bd9-196">TimeGenerated</span></span> |<span data-ttu-id="34bd9-197">Datum en tijd Hallo waarschuwing is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="34bd9-197">Date and time hello alert was created.</span></span> |
| <span data-ttu-id="34bd9-198">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="34bd9-198">TimeLastModified</span></span> |<span data-ttu-id="34bd9-199">Datum en tijd Hallo-status van waarschuwing Hallo het laatst is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="34bd9-199">Date and time hello state of hello alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="34bd9-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34bd9-200">Next steps</span></span>
* <span data-ttu-id="34bd9-201">Meer informatie over [waarschuwingen](log-analytics-alerts.md) in logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="34bd9-201">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="34bd9-202">Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen.</span><span class="sxs-lookup"><span data-stu-id="34bd9-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
