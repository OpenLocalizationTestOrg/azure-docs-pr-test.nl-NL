---
title: Azure Application Gateway ongeldige Gateway (502)-fouten aaaTroubleshoot | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Application Gateway 502-fouten
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="81e69-103">Ongeldige gateway-probleemoplossing in Application Gateway</span><span class="sxs-lookup"><span data-stu-id="81e69-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="81e69-104">Meer informatie over hoe tootroubleshoot Ongeldige gateway (502) fouten ontvangen wanneer u de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="81e69-104">Learn how tootroubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="81e69-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="81e69-105">Overview</span></span>

<span data-ttu-id="81e69-106">Na het configureren van een application gateway is een Hallo fouten die gebruikers kunnen ondervinden ' Server-fout: 502 - in webserver heeft een ongeldig antwoord ontvangen terwijl deze fungeerde als gateway of proxy '.</span><span class="sxs-lookup"><span data-stu-id="81e69-106">After configuring an application gateway, one of hello errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="81e69-107">Deze fout kan optreden vanwege de volgende toohello belangrijkste redenen:</span><span class="sxs-lookup"><span data-stu-id="81e69-107">This error may happen due toohello following main reasons:</span></span>

* <span data-ttu-id="81e69-108">Azure Application Gateway van [back-end-adresgroep is niet geconfigureerd of lege](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="81e69-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="81e69-109">Geen van de Hallo virtuele machines of exemplaren in [VM-Schaalset zijn in orde](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="81e69-109">None of hello VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="81e69-110">Back-end-VM's of exemplaren van het VM-Schaalset zijn [reageert niet toohello standaard health test](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="81e69-110">Back-end VMs or instances of VM Scale Set are [not responding toohello default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="81e69-111">Ongeldige of onjuiste [configuratie van aangepaste statuscontroles](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="81e69-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="81e69-112">[Aanvraag-time-out- of verbindingsproblemen](#request-time-out) met aanvragen van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="81e69-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="81e69-113">Lege BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="81e69-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="81e69-114">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="81e69-114">Cause</span></span>

<span data-ttu-id="81e69-115">Als Hallo Application Gateway geen VM's heeft of VM-Schaalset geconfigureerd in het back-end-adresgroep hello, kan niet alle klantaanvraag routeren en een ongeldige gateway-fout genereert.</span><span class="sxs-lookup"><span data-stu-id="81e69-115">If hello Application Gateway has no VMs or VM Scale Set configured in hello back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="81e69-116">Oplossing</span><span class="sxs-lookup"><span data-stu-id="81e69-116">Solution</span></span>

<span data-ttu-id="81e69-117">Zorg ervoor dat Hallo back-end-adresgroep is niet leeg.</span><span class="sxs-lookup"><span data-stu-id="81e69-117">Ensure that hello back-end address pool is not empty.</span></span> <span data-ttu-id="81e69-118">Dit kan worden gedaan hetzij via PowerShell, CLI of -portal.</span><span class="sxs-lookup"><span data-stu-id="81e69-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="81e69-119">Hallo-uitvoer van Hallo voorafgaand aan de cmdlet moet niet-lege back-end-adresgroep bevatten.</span><span class="sxs-lookup"><span data-stu-id="81e69-119">hello output from hello preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="81e69-120">Hieronder volgt een voorbeeld waarin twee groepen worden geretourneerd die zijn geconfigureerd met de FQDN-naam of IP-adressen voor back-end virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="81e69-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="81e69-121">Hallo Inrichtingsstatus Hallo BackendAddressPool moet worden 'is voltooid'.</span><span class="sxs-lookup"><span data-stu-id="81e69-121">hello provisioning state of hello BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="81e69-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="81e69-122">BackendAddressPoolsText:</span></span>

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="81e69-123">Slechte exemplaren in BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="81e69-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="81e69-124">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="81e69-124">Cause</span></span>

<span data-ttu-id="81e69-125">Als alle Hallo exemplaren van BackendAddressPool niet in orde zijn, klikt u vervolgens Application Gateway geen een back-end tooroute gebruikersaanvraag tot.</span><span class="sxs-lookup"><span data-stu-id="81e69-125">If all hello instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end tooroute user request to.</span></span> <span data-ttu-id="81e69-126">Dit kan ook Hallo geval zijn wanneer back-end-exemplaren in orde zijn, maar nog geen toepassing hello vereist die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="81e69-126">This could also be hello case when back-end instances are healthy but do not have hello required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="81e69-127">Oplossing</span><span class="sxs-lookup"><span data-stu-id="81e69-127">Solution</span></span>

<span data-ttu-id="81e69-128">Zorg ervoor dat Hallo exemplaren zijn in orde en Hallo toepassing correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="81e69-128">Ensure that hello instances are healthy and hello application is properly configured.</span></span> <span data-ttu-id="81e69-129">Selectievakje Hallo als Hallo back-end-exemplaren kunnen toorespond tooa ping uit een andere virtuele machine in hetzelfde VNet.</span><span class="sxs-lookup"><span data-stu-id="81e69-129">Check if hello back-end instances are able toorespond tooa ping from another VM in hello same VNet.</span></span> <span data-ttu-id="81e69-130">Als met een openbaar eindpunt is geconfigureerd, zorg ervoor dat een webtoepassing browser aanvraag toohello geschikte is.</span><span class="sxs-lookup"><span data-stu-id="81e69-130">If configured with a public end point, ensure that a browser request toohello web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="81e69-131">Problemen met standaard health test</span><span class="sxs-lookup"><span data-stu-id="81e69-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="81e69-132">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="81e69-132">Cause</span></span>

<span data-ttu-id="81e69-133">502 fouten kunnen ook worden regelmatig indicatoren die Hallo standaard health test is niet mogelijk tooreach back-end virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="81e69-133">502 errors can also be frequent indicators that hello default health probe is not able tooreach back-end VMs.</span></span> <span data-ttu-id="81e69-134">Wanneer een exemplaar van Application Gateway is geconfigureerd, configureert het automatisch een standaard health test tooeach BackendAddressPool met behulp van de eigenschappen van Hallo BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="81e69-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe tooeach BackendAddressPool using properties of hello BackendHttpSetting.</span></span> <span data-ttu-id="81e69-135">Er is geen gebruikersinvoer is vereist tooset deze test.</span><span class="sxs-lookup"><span data-stu-id="81e69-135">No user input is required tooset this probe.</span></span> <span data-ttu-id="81e69-136">In het bijzonder wanneer een taakverdelingsregel is geconfigureerd, wordt een koppeling gemaakt tussen een BackendHttpSetting en BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="81e69-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="81e69-137">Een standaard-test is geconfigureerd voor elk van deze koppelingen en Application Gateway initieert een periodieke controle verbinding tooeach exemplaar in Hallo BackendAddressPool op Hallo opgegeven poort in Hallo BackendHttpSetting element.</span><span class="sxs-lookup"><span data-stu-id="81e69-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection tooeach instance in hello BackendAddressPool at hello port specified in hello BackendHttpSetting element.</span></span> <span data-ttu-id="81e69-138">Volgende tabel bevat Hallo waarden die zijn gekoppeld aan Hallo standaard health test.</span><span class="sxs-lookup"><span data-stu-id="81e69-138">Following table lists hello values associated with hello default health probe.</span></span>

| <span data-ttu-id="81e69-139">Test-eigenschap</span><span class="sxs-lookup"><span data-stu-id="81e69-139">Probe property</span></span> | <span data-ttu-id="81e69-140">Waarde</span><span class="sxs-lookup"><span data-stu-id="81e69-140">Value</span></span> | <span data-ttu-id="81e69-141">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="81e69-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="81e69-142">WebTest-URL</span><span class="sxs-lookup"><span data-stu-id="81e69-142">Probe URL</span></span> |<span data-ttu-id="81e69-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="81e69-143">http://127.0.0.1/</span></span> |<span data-ttu-id="81e69-144">URL-pad</span><span class="sxs-lookup"><span data-stu-id="81e69-144">URL path</span></span> |
| <span data-ttu-id="81e69-145">Interval</span><span class="sxs-lookup"><span data-stu-id="81e69-145">Interval</span></span> |<span data-ttu-id="81e69-146">30</span><span class="sxs-lookup"><span data-stu-id="81e69-146">30</span></span> |<span data-ttu-id="81e69-147">Testinterval in seconden</span><span class="sxs-lookup"><span data-stu-id="81e69-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="81e69-148">Time-out</span><span class="sxs-lookup"><span data-stu-id="81e69-148">Time-out</span></span> |<span data-ttu-id="81e69-149">30</span><span class="sxs-lookup"><span data-stu-id="81e69-149">30</span></span> |<span data-ttu-id="81e69-150">Test time-out in seconden</span><span class="sxs-lookup"><span data-stu-id="81e69-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="81e69-151">Drempelwaarde voor onjuiste status</span><span class="sxs-lookup"><span data-stu-id="81e69-151">Unhealthy threshold</span></span> |<span data-ttu-id="81e69-152">3</span><span class="sxs-lookup"><span data-stu-id="81e69-152">3</span></span> |<span data-ttu-id="81e69-153">Aantal nieuwe pogingen-test.</span><span class="sxs-lookup"><span data-stu-id="81e69-153">Probe retry count.</span></span> <span data-ttu-id="81e69-154">Hallo back-end-server is gemarkeerd als niet actief nadat Hallo opeenvolgende test foutentelling Hallo slecht drempel bereikt.</span><span class="sxs-lookup"><span data-stu-id="81e69-154">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="81e69-155">Oplossing</span><span class="sxs-lookup"><span data-stu-id="81e69-155">Solution</span></span>

* <span data-ttu-id="81e69-156">Zorg ervoor dat een standaard-site is geconfigureerd en luistert naar de 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="81e69-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="81e69-157">Als BackendHttpSetting is opgegeven voor een andere poort dan 80, moet standaardsite Hallo geconfigureerde toolisten op deze poort.</span><span class="sxs-lookup"><span data-stu-id="81e69-157">If BackendHttpSetting specifies a port other than 80, hello default site should be configured toolisten at that port.</span></span>
* <span data-ttu-id="81e69-158">Hallo moet aanroep toohttp://127.0.0.1:port retourneren de resultaatcode van een HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="81e69-158">hello call toohttp://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="81e69-159">Dit moet worden geretourneerd binnen de time-outperiode voor Hallo 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="81e69-159">This should be returned within hello 30 sec time-out period.</span></span>
* <span data-ttu-id="81e69-160">Zorg ervoor dat poort geconfigureerd open is en dat er zijn geen firewallregels of Azure-Netwerkbeveiligingsgroepen, dit blokkeren van binnenkomend of uitgaand verkeer op Hallo poort geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="81e69-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on hello port configured.</span></span>
* <span data-ttu-id="81e69-161">Als Azure classic VM's of een Cloudservice met de FQDN-naam of het openbare IP-adres wordt gebruikt, zorg ervoor dat Hallo er overeenkomende [eindpunt](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="81e69-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that hello corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="81e69-162">Als Hallo VM via Azure Resource Manager is geconfigureerd en buiten Hallo VNet waar Application Gateway wordt geïmplementeerd, [Netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md) moet worden geconfigureerd tooallow toegang op Hallo gewenst poort.</span><span class="sxs-lookup"><span data-stu-id="81e69-162">If hello VM is configured via Azure Resource Manager and is outside hello VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured tooallow access on hello desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="81e69-163">Problemen met aangepaste health test</span><span class="sxs-lookup"><span data-stu-id="81e69-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="81e69-164">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="81e69-164">Cause</span></span>

<span data-ttu-id="81e69-165">Aangepaste statuscontroles kunnen extra flexibiliteit toohello standaard probing gedrag.</span><span class="sxs-lookup"><span data-stu-id="81e69-165">Custom health probes allow additional flexibility toohello default probing behavior.</span></span> <span data-ttu-id="81e69-166">Wanneer u aangepaste tests, kunnen gebruikers het testinterval hello, Hallo-URL, en pad tootest en hoeveel mislukte reacties tooaccept configureren voordat Hallo back-end-pool exemplaar als beschadigd gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="81e69-166">When using custom probes, users can configure hello probe interval, hello URL, and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span> <span data-ttu-id="81e69-167">Hallo volgende extra eigenschappen worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="81e69-167">hello following additional properties are added.</span></span>

| <span data-ttu-id="81e69-168">Test-eigenschap</span><span class="sxs-lookup"><span data-stu-id="81e69-168">Probe property</span></span> | <span data-ttu-id="81e69-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="81e69-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="81e69-170">Naam</span><span class="sxs-lookup"><span data-stu-id="81e69-170">Name</span></span> |<span data-ttu-id="81e69-171">Naam van het Hallo-test.</span><span class="sxs-lookup"><span data-stu-id="81e69-171">Name of hello probe.</span></span> <span data-ttu-id="81e69-172">Deze naam wordt gebruikt toorefer toohello test in de back-end-HTTP-instellingen.</span><span class="sxs-lookup"><span data-stu-id="81e69-172">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="81e69-173">Protocol</span><span class="sxs-lookup"><span data-stu-id="81e69-173">Protocol</span></span> |<span data-ttu-id="81e69-174">Protocol gebruikt toosend Hallo test.</span><span class="sxs-lookup"><span data-stu-id="81e69-174">Protocol used toosend hello probe.</span></span> <span data-ttu-id="81e69-175">Hallo test gebruikt Hallo-protocol gedefinieerd in Hallo back-end-HTTP-instellingen</span><span class="sxs-lookup"><span data-stu-id="81e69-175">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="81e69-176">Host</span><span class="sxs-lookup"><span data-stu-id="81e69-176">Host</span></span> |<span data-ttu-id="81e69-177">Host naam toosend Hallo test.</span><span class="sxs-lookup"><span data-stu-id="81e69-177">Host name toosend hello probe.</span></span> <span data-ttu-id="81e69-178">Alleen van toepassing wanneer meerdere locaties op Application Gateway is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="81e69-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="81e69-179">Dit wijkt af van de VM-hostnaam.</span><span class="sxs-lookup"><span data-stu-id="81e69-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="81e69-180">Pad</span><span class="sxs-lookup"><span data-stu-id="81e69-180">Path</span></span> |<span data-ttu-id="81e69-181">Relatieve pad van het Hallo-test.</span><span class="sxs-lookup"><span data-stu-id="81e69-181">Relative path of hello probe.</span></span> <span data-ttu-id="81e69-182">Hallo geldig pad wordt gestart vanuit '/'.</span><span class="sxs-lookup"><span data-stu-id="81e69-182">hello valid path starts from '/'.</span></span> <span data-ttu-id="81e69-183">Hallo-test wordt verzonden, te\<protocol\>://\<host\>:\<poort\>\<pad\></span><span class="sxs-lookup"><span data-stu-id="81e69-183">hello probe is sent too\<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="81e69-184">Interval</span><span class="sxs-lookup"><span data-stu-id="81e69-184">Interval</span></span> |<span data-ttu-id="81e69-185">WebTest interval in seconden.</span><span class="sxs-lookup"><span data-stu-id="81e69-185">Probe interval in seconds.</span></span> <span data-ttu-id="81e69-186">Dit is de tijdsinterval Hallo tussen twee opeenvolgende tests.</span><span class="sxs-lookup"><span data-stu-id="81e69-186">This is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="81e69-187">Time-out</span><span class="sxs-lookup"><span data-stu-id="81e69-187">Time-out</span></span> |<span data-ttu-id="81e69-188">WebTest time-outwaarde in seconden.</span><span class="sxs-lookup"><span data-stu-id="81e69-188">Probe time-out in seconds.</span></span> <span data-ttu-id="81e69-189">Als een geldig antwoord niet binnen deze time-outperiode ontvangen is, wordt Hallo test als mislukt gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="81e69-189">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span> |
| <span data-ttu-id="81e69-190">Drempelwaarde voor onjuiste status</span><span class="sxs-lookup"><span data-stu-id="81e69-190">Unhealthy threshold</span></span> |<span data-ttu-id="81e69-191">Aantal nieuwe pogingen-test.</span><span class="sxs-lookup"><span data-stu-id="81e69-191">Probe retry count.</span></span> <span data-ttu-id="81e69-192">Hallo back-end-server is gemarkeerd als niet actief nadat Hallo opeenvolgende test foutentelling Hallo slecht drempel bereikt.</span><span class="sxs-lookup"><span data-stu-id="81e69-192">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="81e69-193">Oplossing</span><span class="sxs-lookup"><span data-stu-id="81e69-193">Solution</span></span>

<span data-ttu-id="81e69-194">Valideren dat aangepaste Health test correct is geconfigureerd als de voorgaande tabel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="81e69-194">Validate that hello Custom Health Probe is configured correctly as hello preceding table.</span></span> <span data-ttu-id="81e69-195">Bovendien toohello voorgaande probleemoplossingsstappen, zorg er ook voor Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="81e69-195">In addition toohello preceding troubleshooting steps, also ensure hello following:</span></span>

* <span data-ttu-id="81e69-196">Controleer dat test Hallo juist is opgegeven volgens Hallo [handleiding](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="81e69-196">Ensure that hello probe is correctly specified as per hello [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="81e69-197">Als Application Gateway is geconfigureerd voor een enkele site, door standaard Hallo Host moet naam worden opgegeven als '127.0.0.1', tenzij anders is geconfigureerd in aangepaste test.</span><span class="sxs-lookup"><span data-stu-id="81e69-197">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="81e69-198">Zorg ervoor dat een aanroep van toohttp: / /\<host\>:\<poort\>\<pad\> retourneert de resultaatcode van een HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="81e69-198">Ensure that a call toohttp://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="81e69-199">Zorg ervoor dat Interval, Time-out en UnhealtyThreshold binnen acceptabele Hallo-adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="81e69-199">Ensure that Interval, Time-out and UnhealtyThreshold are within hello acceptable ranges.</span></span>
* <span data-ttu-id="81e69-200">Als via een HTTPS-test, ervoor zorgen dat back-endserver Hallo geen SNI vereist door een fallback-certificaat op Hallo back-endserver zelf configureren.</span><span class="sxs-lookup"><span data-stu-id="81e69-200">If using an HTTPS probe, make sure that hello backend server doesn't require SNI by configuring a fallback certificate on hello backend server itself.</span></span> 
* <span data-ttu-id="81e69-201">Zorg ervoor dat Interval, Time-out en UnhealtyThreshold binnen acceptabele Hallo-adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="81e69-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within hello acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="81e69-202">Time-out aanvraag</span><span class="sxs-lookup"><span data-stu-id="81e69-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="81e69-203">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="81e69-203">Cause</span></span>

<span data-ttu-id="81e69-204">Wanneer een gebruikersaanvraag wordt ontvangen, wordt Application Gateway is van toepassing hello geconfigureerd regels toohello aanvraag en tooa back-end-pool exemplaar doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="81e69-204">When a user request is received, Application Gateway applies hello configured rules toohello request and routes it tooa back-end pool instance.</span></span> <span data-ttu-id="81e69-205">Er wordt gewacht op een configureerbare tijdsinterval op een reactie van Hallo back-end-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="81e69-205">It waits for a configurable interval of time for a response from hello back-end instance.</span></span> <span data-ttu-id="81e69-206">Dit interval is standaard **30 seconden**.</span><span class="sxs-lookup"><span data-stu-id="81e69-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="81e69-207">Als Application Gateway geen reactie van de back-endtoepassing in dit interval ontvangen heeft, ziet aanvraag van de gebruiker een 502-fout.</span><span class="sxs-lookup"><span data-stu-id="81e69-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="81e69-208">Oplossing</span><span class="sxs-lookup"><span data-stu-id="81e69-208">Solution</span></span>

<span data-ttu-id="81e69-209">Toepassingsgateway kan gebruikers tooconfigure deze instelling via BackendHttpSetting die kan worden en toodifferent pools toegepast.</span><span class="sxs-lookup"><span data-stu-id="81e69-209">Application Gateway allows users tooconfigure this setting via BackendHttpSetting, which can be then applied toodifferent pools.</span></span> <span data-ttu-id="81e69-210">Verschillende groepen van de back-end kunnen hebben verschillende BackendHttpSetting en daarom verschillende aanvraag time-outwaarde is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="81e69-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="81e69-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81e69-211">Next steps</span></span>

<span data-ttu-id="81e69-212">Als hello voorgaande stappen probleem niet hello verhelpen, opent u een [ondersteunen ticket](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="81e69-212">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

