---
title: Azure Application Gateway ongeldige Gateway (502) fouten oplossen | Microsoft Docs
description: Meer informatie over het oplossen van Application Gateway 502-fouten
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
ms.openlocfilehash: cbf9c552c4818b3925f449081539f1db6d61918e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="c247a-103">Ongeldige gateway-probleemoplossing in Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c247a-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="c247a-104">Informatie over het oplossen van problemen met ongeldige gateway (502) fouten die zijn ontvangen wanneer u de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="c247a-104">Learn how to troubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="c247a-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c247a-105">Overview</span></span>

<span data-ttu-id="c247a-106">Na het configureren van een application gateway is een van de fouten die gebruikers kunnen ondervinden ' Server-fout: 502 - in webserver heeft een ongeldig antwoord ontvangen terwijl deze fungeerde als gateway of proxy '.</span><span class="sxs-lookup"><span data-stu-id="c247a-106">After configuring an application gateway, one of the errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="c247a-107">Deze fout kan optreden als gevolg van de belangrijkste oorzaken:</span><span class="sxs-lookup"><span data-stu-id="c247a-107">This error may happen due to the following main reasons:</span></span>

* <span data-ttu-id="c247a-108">Azure Application Gateway van [back-end-adresgroep is niet geconfigureerd of lege](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="c247a-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="c247a-109">Geen van de virtuele machines of exemplaren in [VM-Schaalset zijn in orde](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="c247a-109">None of the VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="c247a-110">Back-end-VM's of exemplaren van het VM-Schaalset zijn [reageert niet op de standaard health test](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="c247a-110">Back-end VMs or instances of VM Scale Set are [not responding to the default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="c247a-111">Ongeldige of onjuiste [configuratie van aangepaste statuscontroles](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="c247a-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="c247a-112">[Aanvraag-time-out- of verbindingsproblemen](#request-time-out) met aanvragen van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="c247a-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="c247a-113">Lege BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="c247a-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="c247a-114">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="c247a-114">Cause</span></span>

<span data-ttu-id="c247a-115">Als de toepassingsgateway heeft geen virtuele machines of VM-Schaalset in de back-end-adresgroep geconfigureerd, kan niet alle klantaanvraag routeren en een ongeldige gateway-fout genereert.</span><span class="sxs-lookup"><span data-stu-id="c247a-115">If the Application Gateway has no VMs or VM Scale Set configured in the back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="c247a-116">Oplossing</span><span class="sxs-lookup"><span data-stu-id="c247a-116">Solution</span></span>

<span data-ttu-id="c247a-117">Zorg ervoor dat de back-end-adresgroep is niet leeg.</span><span class="sxs-lookup"><span data-stu-id="c247a-117">Ensure that the back-end address pool is not empty.</span></span> <span data-ttu-id="c247a-118">Dit kan worden gedaan hetzij via PowerShell, CLI of -portal.</span><span class="sxs-lookup"><span data-stu-id="c247a-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="c247a-119">De uitvoer van de voorgaande cmdlet moet niet-lege back-end-adresgroep bevatten.</span><span class="sxs-lookup"><span data-stu-id="c247a-119">The output from the preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="c247a-120">Hieronder volgt een voorbeeld waarin twee groepen worden geretourneerd die zijn geconfigureerd met de FQDN-naam of IP-adressen voor back-end virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c247a-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="c247a-121">De Inrichtingsstatus van de BackendAddressPool moet worden 'is voltooid'.</span><span class="sxs-lookup"><span data-stu-id="c247a-121">The provisioning state of the BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="c247a-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="c247a-122">BackendAddressPoolsText:</span></span>

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

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="c247a-123">Slechte exemplaren in BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="c247a-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="c247a-124">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="c247a-124">Cause</span></span>

<span data-ttu-id="c247a-125">Als alle exemplaren van BackendAddressPool niet in orde zijn, klikt u vervolgens Application Gateway geen een back-end kan route gebruikersaanvraag tot.</span><span class="sxs-lookup"><span data-stu-id="c247a-125">If all the instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end to route user request to.</span></span> <span data-ttu-id="c247a-126">Dit mogelijk ook het geval wanneer back-end-exemplaren in orde zijn, maar niet de vereiste toepassing geïmplementeerd hebben.</span><span class="sxs-lookup"><span data-stu-id="c247a-126">This could also be the case when back-end instances are healthy but do not have the required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="c247a-127">Oplossing</span><span class="sxs-lookup"><span data-stu-id="c247a-127">Solution</span></span>

<span data-ttu-id="c247a-128">Zorg ervoor dat de exemplaren in orde zijn en de toepassing correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c247a-128">Ensure that the instances are healthy and the application is properly configured.</span></span> <span data-ttu-id="c247a-129">Controleer of de back-end-exemplaren kunnen reageren op een ping naar een andere virtuele machine in hetzelfde VNet zijn.</span><span class="sxs-lookup"><span data-stu-id="c247a-129">Check if the back-end instances are able to respond to a ping from another VM in the same VNet.</span></span> <span data-ttu-id="c247a-130">Als met een openbaar eindpunt is geconfigureerd, moet u zorgen dat de aanvraag van een browser naar de webtoepassing geschikte.</span><span class="sxs-lookup"><span data-stu-id="c247a-130">If configured with a public end point, ensure that a browser request to the web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="c247a-131">Problemen met standaard health test</span><span class="sxs-lookup"><span data-stu-id="c247a-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="c247a-132">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="c247a-132">Cause</span></span>

<span data-ttu-id="c247a-133">502 fouten kunnen ook worden regelmatig indicatoren de standaard health test is niet kunnen bereiken back-end virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c247a-133">502 errors can also be frequent indicators that the default health probe is not able to reach back-end VMs.</span></span> <span data-ttu-id="c247a-134">Wanneer een exemplaar van Application Gateway is geconfigureerd, configureert het automatisch een standaard health test naar elke BackendAddressPool met behulp van de eigenschappen van de BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="c247a-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe to each BackendAddressPool using properties of the BackendHttpSetting.</span></span> <span data-ttu-id="c247a-135">Er is geen gebruikersinvoer is vereist voor het instellen van deze test.</span><span class="sxs-lookup"><span data-stu-id="c247a-135">No user input is required to set this probe.</span></span> <span data-ttu-id="c247a-136">In het bijzonder wanneer een taakverdelingsregel is geconfigureerd, wordt een koppeling gemaakt tussen een BackendHttpSetting en BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="c247a-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="c247a-137">Een standaard-test is geconfigureerd voor elk van deze koppelingen en Application Gateway een periodieke controle-verbinding met elk exemplaar in de BackendAddressPool op de opgegeven poort in het element BackendHttpSetting initieert.</span><span class="sxs-lookup"><span data-stu-id="c247a-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection to each instance in the BackendAddressPool at the port specified in the BackendHttpSetting element.</span></span> <span data-ttu-id="c247a-138">Volgende tabel bevat de waarden die zijn gekoppeld aan de standaard health test.</span><span class="sxs-lookup"><span data-stu-id="c247a-138">Following table lists the values associated with the default health probe.</span></span>

| <span data-ttu-id="c247a-139">Test-eigenschap</span><span class="sxs-lookup"><span data-stu-id="c247a-139">Probe property</span></span> | <span data-ttu-id="c247a-140">Waarde</span><span class="sxs-lookup"><span data-stu-id="c247a-140">Value</span></span> | <span data-ttu-id="c247a-141">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c247a-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c247a-142">WebTest-URL</span><span class="sxs-lookup"><span data-stu-id="c247a-142">Probe URL</span></span> |<span data-ttu-id="c247a-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="c247a-143">http://127.0.0.1/</span></span> |<span data-ttu-id="c247a-144">URL-pad</span><span class="sxs-lookup"><span data-stu-id="c247a-144">URL path</span></span> |
| <span data-ttu-id="c247a-145">Interval</span><span class="sxs-lookup"><span data-stu-id="c247a-145">Interval</span></span> |<span data-ttu-id="c247a-146">30</span><span class="sxs-lookup"><span data-stu-id="c247a-146">30</span></span> |<span data-ttu-id="c247a-147">Testinterval in seconden</span><span class="sxs-lookup"><span data-stu-id="c247a-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="c247a-148">Time-out</span><span class="sxs-lookup"><span data-stu-id="c247a-148">Time-out</span></span> |<span data-ttu-id="c247a-149">30</span><span class="sxs-lookup"><span data-stu-id="c247a-149">30</span></span> |<span data-ttu-id="c247a-150">Test time-out in seconden</span><span class="sxs-lookup"><span data-stu-id="c247a-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="c247a-151">Drempelwaarde voor onjuiste status</span><span class="sxs-lookup"><span data-stu-id="c247a-151">Unhealthy threshold</span></span> |<span data-ttu-id="c247a-152">3</span><span class="sxs-lookup"><span data-stu-id="c247a-152">3</span></span> |<span data-ttu-id="c247a-153">Aantal nieuwe pogingen-test.</span><span class="sxs-lookup"><span data-stu-id="c247a-153">Probe retry count.</span></span> <span data-ttu-id="c247a-154">De back-endserver is gemarkeerd als niet actief nadat de foutentelling opeenvolgende test heeft de drempelwaarde voor onjuiste status bereikt.</span><span class="sxs-lookup"><span data-stu-id="c247a-154">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="c247a-155">Oplossing</span><span class="sxs-lookup"><span data-stu-id="c247a-155">Solution</span></span>

* <span data-ttu-id="c247a-156">Zorg ervoor dat een standaard-site is geconfigureerd en luistert naar de 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="c247a-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="c247a-157">Als BackendHttpSetting is opgegeven voor een andere poort dan 80, moet u de standaardsite geconfigureerd om te luisteren op poort.</span><span class="sxs-lookup"><span data-stu-id="c247a-157">If BackendHttpSetting specifies a port other than 80, the default site should be configured to listen at that port.</span></span>
* <span data-ttu-id="c247a-158">De aanroep van http://127.0.0.1:port moet de resultaatcode van een HTTP 200 retourneren.</span><span class="sxs-lookup"><span data-stu-id="c247a-158">The call to http://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="c247a-159">Dit moet worden geretourneerd binnen de time-outperiode van 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="c247a-159">This should be returned within the 30 sec time-out period.</span></span>
* <span data-ttu-id="c247a-160">Zorg ervoor dat poort geconfigureerd open is en dat er zijn geen firewallregels of Azure-Netwerkbeveiligingsgroepen, dit blokkeren van binnenkomend of uitgaand verkeer op de poort die is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c247a-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on the port configured.</span></span>
* <span data-ttu-id="c247a-161">Als Azure classic VM's of een Cloudservice met de FQDN-naam of het openbare IP-adres wordt gebruikt, zorg ervoor dat de bijbehorende [eindpunt](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c247a-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that the corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="c247a-162">Als de virtuele machine via Azure Resource Manager is geconfigureerd en buiten het VNet waar Application Gateway wordt geïmplementeerd ligt, [Netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md) moet worden geconfigureerd voor toegang op de gewenste poort.</span><span class="sxs-lookup"><span data-stu-id="c247a-162">If the VM is configured via Azure Resource Manager and is outside the VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured to allow access on the desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="c247a-163">Problemen met aangepaste health test</span><span class="sxs-lookup"><span data-stu-id="c247a-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="c247a-164">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="c247a-164">Cause</span></span>

<span data-ttu-id="c247a-165">Aangepaste statuscontroles kunnen extra flexibiliteit op de standaardwaarde probing gedrag.</span><span class="sxs-lookup"><span data-stu-id="c247a-165">Custom health probes allow additional flexibility to the default probing behavior.</span></span> <span data-ttu-id="c247a-166">Wanneer u aangepaste tests, kunnen gebruikers de testinterval, de URL en pad voor het testen en hoeveel mislukte reacties op accepteren voordat de back-endpool-instantie als beschadigd gemarkeerd configureren.</span><span class="sxs-lookup"><span data-stu-id="c247a-166">When using custom probes, users can configure the probe interval, the URL, and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span></span> <span data-ttu-id="c247a-167">De volgende aanvullende eigenschappen worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c247a-167">The following additional properties are added.</span></span>

| <span data-ttu-id="c247a-168">Test-eigenschap</span><span class="sxs-lookup"><span data-stu-id="c247a-168">Probe property</span></span> | <span data-ttu-id="c247a-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c247a-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c247a-170">Naam</span><span class="sxs-lookup"><span data-stu-id="c247a-170">Name</span></span> |<span data-ttu-id="c247a-171">Naam van de test.</span><span class="sxs-lookup"><span data-stu-id="c247a-171">Name of the probe.</span></span> <span data-ttu-id="c247a-172">Deze naam wordt gebruikt om te verwijzen naar de instellingen voor back-end-HTTP-test.</span><span class="sxs-lookup"><span data-stu-id="c247a-172">This name is used to refer to the probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="c247a-173">Protocol</span><span class="sxs-lookup"><span data-stu-id="c247a-173">Protocol</span></span> |<span data-ttu-id="c247a-174">Het protocol dat wordt gebruikt voor het verzenden van de test.</span><span class="sxs-lookup"><span data-stu-id="c247a-174">Protocol used to send the probe.</span></span> <span data-ttu-id="c247a-175">De test wordt gebruikt voor het protocol dat is gedefinieerd in de back-end-HTTP-instellingen</span><span class="sxs-lookup"><span data-stu-id="c247a-175">The probe uses the protocol defined in the back-end HTTP settings</span></span> |
| <span data-ttu-id="c247a-176">Host</span><span class="sxs-lookup"><span data-stu-id="c247a-176">Host</span></span> |<span data-ttu-id="c247a-177">De hostnaam voor het verzenden van de test.</span><span class="sxs-lookup"><span data-stu-id="c247a-177">Host name to send the probe.</span></span> <span data-ttu-id="c247a-178">Alleen van toepassing wanneer meerdere locaties op Application Gateway is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c247a-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="c247a-179">Dit wijkt af van de VM-hostnaam.</span><span class="sxs-lookup"><span data-stu-id="c247a-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="c247a-180">Pad</span><span class="sxs-lookup"><span data-stu-id="c247a-180">Path</span></span> |<span data-ttu-id="c247a-181">Relatieve pad van de test.</span><span class="sxs-lookup"><span data-stu-id="c247a-181">Relative path of the probe.</span></span> <span data-ttu-id="c247a-182">Het pad geldig wordt gestart vanuit '/'.</span><span class="sxs-lookup"><span data-stu-id="c247a-182">The valid path starts from '/'.</span></span> <span data-ttu-id="c247a-183">De test wordt verzonden naar \<protocol\>://\<host\>:\<poort\>\<pad\></span><span class="sxs-lookup"><span data-stu-id="c247a-183">The probe is sent to \<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="c247a-184">Interval</span><span class="sxs-lookup"><span data-stu-id="c247a-184">Interval</span></span> |<span data-ttu-id="c247a-185">WebTest interval in seconden.</span><span class="sxs-lookup"><span data-stu-id="c247a-185">Probe interval in seconds.</span></span> <span data-ttu-id="c247a-186">Dit is het interval tussen twee opeenvolgende tests.</span><span class="sxs-lookup"><span data-stu-id="c247a-186">This is the time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="c247a-187">Time-out</span><span class="sxs-lookup"><span data-stu-id="c247a-187">Time-out</span></span> |<span data-ttu-id="c247a-188">WebTest time-outwaarde in seconden.</span><span class="sxs-lookup"><span data-stu-id="c247a-188">Probe time-out in seconds.</span></span> <span data-ttu-id="c247a-189">Als een geldig antwoord niet binnen deze time-outperiode ontvangen is, wordt de test als mislukt gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="c247a-189">If a valid response is not received within this time-out period, the probe is marked as failed.</span></span> |
| <span data-ttu-id="c247a-190">Drempelwaarde voor onjuiste status</span><span class="sxs-lookup"><span data-stu-id="c247a-190">Unhealthy threshold</span></span> |<span data-ttu-id="c247a-191">Aantal nieuwe pogingen-test.</span><span class="sxs-lookup"><span data-stu-id="c247a-191">Probe retry count.</span></span> <span data-ttu-id="c247a-192">De back-endserver is gemarkeerd als niet actief nadat de foutentelling opeenvolgende test heeft de drempelwaarde voor onjuiste status bereikt.</span><span class="sxs-lookup"><span data-stu-id="c247a-192">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="c247a-193">Oplossing</span><span class="sxs-lookup"><span data-stu-id="c247a-193">Solution</span></span>

<span data-ttu-id="c247a-194">Valideren dat de aangepaste Health test is geconfigureerd als de voorgaande tabel.</span><span class="sxs-lookup"><span data-stu-id="c247a-194">Validate that the Custom Health Probe is configured correctly as the preceding table.</span></span> <span data-ttu-id="c247a-195">Naast de voorgaande stappen voor probleemoplossing, zorg er ook voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="c247a-195">In addition to the preceding troubleshooting steps, also ensure the following:</span></span>

* <span data-ttu-id="c247a-196">Zorg ervoor dat de test juist is opgegeven conform de [handleiding](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c247a-196">Ensure that the probe is correctly specified as per the [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="c247a-197">Als Application Gateway is geconfigureerd voor een enkele site, standaard ingesteld op de Host moet naam worden opgegeven als '127.0.0.1', tenzij anders is geconfigureerd in aangepaste test.</span><span class="sxs-lookup"><span data-stu-id="c247a-197">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="c247a-198">Zorg ervoor dat een aanroep naar http://\<host\>:\<poort\>\<pad\> retourneert de resultaatcode van een HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="c247a-198">Ensure that a call to http://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="c247a-199">Zorg ervoor dat Interval, Time-out en UnhealtyThreshold in het acceptabele bereik liggen.</span><span class="sxs-lookup"><span data-stu-id="c247a-199">Ensure that Interval, Time-out and UnhealtyThreshold are within the acceptable ranges.</span></span>
* <span data-ttu-id="c247a-200">Als via een HTTPS-test, ervoor zorgen dat de back-endserver SNI geen vereist door een fallback-certificaat op de back-endserver zelf configureren.</span><span class="sxs-lookup"><span data-stu-id="c247a-200">If using an HTTPS probe, make sure that the backend server doesn't require SNI by configuring a fallback certificate on the backend server itself.</span></span> 
* <span data-ttu-id="c247a-201">Zorg ervoor dat Interval, Time-out en UnhealtyThreshold in het acceptabele bereik liggen.</span><span class="sxs-lookup"><span data-stu-id="c247a-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within the acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="c247a-202">Time-out aanvraag</span><span class="sxs-lookup"><span data-stu-id="c247a-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="c247a-203">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="c247a-203">Cause</span></span>

<span data-ttu-id="c247a-204">Wanneer een gebruikersaanvraag wordt ontvangen, wordt Application Gateway de geconfigureerde regels van toepassing is op de aanvraag en doorgestuurd naar een exemplaar van de back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="c247a-204">When a user request is received, Application Gateway applies the configured rules to the request and routes it to a back-end pool instance.</span></span> <span data-ttu-id="c247a-205">Er wordt gewacht op een configureerbare tijdsinterval op een reactie van de back-end-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c247a-205">It waits for a configurable interval of time for a response from the back-end instance.</span></span> <span data-ttu-id="c247a-206">Dit interval is standaard **30 seconden**.</span><span class="sxs-lookup"><span data-stu-id="c247a-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="c247a-207">Als Application Gateway geen reactie van de back-endtoepassing in dit interval ontvangen heeft, ziet aanvraag van de gebruiker een 502-fout.</span><span class="sxs-lookup"><span data-stu-id="c247a-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="c247a-208">Oplossing</span><span class="sxs-lookup"><span data-stu-id="c247a-208">Solution</span></span>

<span data-ttu-id="c247a-209">Toepassingsgateway kan gebruikers deze instelling via BackendHttpSetting, die vervolgens kan worden toegepast op verschillende groepen wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="c247a-209">Application Gateway allows users to configure this setting via BackendHttpSetting, which can be then applied to different pools.</span></span> <span data-ttu-id="c247a-210">Verschillende groepen van de back-end kunnen hebben verschillende BackendHttpSetting en daarom verschillende aanvraag time-outwaarde is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c247a-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="c247a-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c247a-211">Next steps</span></span>

<span data-ttu-id="c247a-212">Als de voorgaande stappen het probleem niet verhelpen, opent u een [ondersteunen ticket](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="c247a-212">If the preceding steps do not resolve the issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

