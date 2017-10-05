---
title: Overzicht van Azure-instantie Service metagegevens | Microsoft Docs
description: RESTful-interface voor informatie over de compute, netwerk en toekomstig onderhoud gebeurtenissen van de virtuele machine.
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: d601d8fdb92bf2d3253ba99cdeee10e09591689c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="417e4-103">Service voor Azure-instantie metagegevens</span><span class="sxs-lookup"><span data-stu-id="417e4-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="417e4-104">De Azure-Service-exemplaar metagegevens bevat informatie over het uitvoeren van de virtuele machine-exemplaren die kunnen worden gebruikt voor het beheren en configureren van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="417e4-104">The Azure Instance Metadata Service provides information about running virtual machine instances that can be used to manage and configure your virtual machines.</span></span>
<span data-ttu-id="417e4-105">Dit omvat gegevens zoals SKU netwerkconfiguratie en toekomstig onderhoud gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="417e4-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="417e4-106">Zie voor meer informatie over wat voor soort informatie beschikbaar is, [metagegevens categorieën](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="417e4-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="417e4-107">Service voor de metagegevens van Azure exemplaar is een REST-eindpunt toegankelijk voor alle IaaS VM's die worden gemaakt via de [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="417e4-107">Azure's Instance Metadata Service is a REST Endpoint accessible to all IaaS VMs created via the [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="417e4-108">Het eindpunt is beschikbaar op een bekende niet-routeerbare IP-adres (`169.254.169.254`) die kan alleen worden benaderd binnen de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="417e4-108">The endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within the VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="417e4-109">Belangrijke informatie</span><span class="sxs-lookup"><span data-stu-id="417e4-109">Important information</span></span>

<span data-ttu-id="417e4-110">Deze service is **algemeen beschikbaar** in globale Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="417e4-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="417e4-111">Het is openbare Preview voor Government, China en Duitse Azure-Cloud.</span><span class="sxs-lookup"><span data-stu-id="417e4-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="417e4-112">Het ontvangt regelmatig updates om nieuwe informatie over de virtuele machine-exemplaren weer te geven.</span><span class="sxs-lookup"><span data-stu-id="417e4-112">It regularly receives updates to expose new information about virtual machine instances.</span></span> <span data-ttu-id="417e4-113">Deze pagina geeft de actuele [gegevenscategorieën](#instance-metadata-data-categories) beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="417e4-113">This page reflects the up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="417e4-114">Beschikbaarheid van de service</span><span class="sxs-lookup"><span data-stu-id="417e4-114">Service Availability</span></span>
<span data-ttu-id="417e4-115">De service is beschikbaar in alle algemeen beschikbaar globale Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="417e4-115">The service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="417e4-116">De service zich in de openbare preview van de overheid, China of Duitsland regio's.</span><span class="sxs-lookup"><span data-stu-id="417e4-116">The service is in public preview  in the Government, China, or Germany regions.</span></span>

<span data-ttu-id="417e4-117">Regio's</span><span class="sxs-lookup"><span data-stu-id="417e4-117">Regions</span></span>                                        | <span data-ttu-id="417e4-118">Beschikbaarheid?</span><span class="sxs-lookup"><span data-stu-id="417e4-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="417e4-119">Alle in het algemeen beschikbare globale Azure-regio 's</span><span class="sxs-lookup"><span data-stu-id="417e4-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="417e4-120">Algemeen beschikbaar</span><span class="sxs-lookup"><span data-stu-id="417e4-120">Generally Available</span></span> 
[<span data-ttu-id="417e4-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="417e4-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="417e4-122">Preview-versie</span><span class="sxs-lookup"><span data-stu-id="417e4-122">In Preview</span></span> 
[<span data-ttu-id="417e4-123">Azure China</span><span class="sxs-lookup"><span data-stu-id="417e4-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="417e4-124">Preview-versie</span><span class="sxs-lookup"><span data-stu-id="417e4-124">In Preview</span></span>
[<span data-ttu-id="417e4-125">Azure Duitsland</span><span class="sxs-lookup"><span data-stu-id="417e4-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="417e4-126">Preview-versie</span><span class="sxs-lookup"><span data-stu-id="417e4-126">In Preview</span></span>

<span data-ttu-id="417e4-127">Deze tabel wordt bijgewerkt zodra de service beschikbaar in andere Azure-clouds.</span><span class="sxs-lookup"><span data-stu-id="417e4-127">This table is updated when the service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="417e4-128">Maak een VM uit om de Service-exemplaar voor metagegevens uitproberen, [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) of de [Azure-portal](http://portal.azure.com) in de bovenstaande regio's en volg de onderstaande voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="417e4-128">To try out the Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or the [Azure portal](http://portal.azure.com) in the above regions and follow the examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="417e4-129">Gebruik</span><span class="sxs-lookup"><span data-stu-id="417e4-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="417e4-130">Versiebeheer voor onderdelen</span><span class="sxs-lookup"><span data-stu-id="417e4-130">Versioning</span></span>
<span data-ttu-id="417e4-131">De Service-exemplaar voor metagegevens is samengestelde.</span><span class="sxs-lookup"><span data-stu-id="417e4-131">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="417e4-132">Versies zijn verplicht en de huidige versie is `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="417e4-132">Versions are mandatory and the current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="417e4-133">Eerdere versies van de preview van geplande gebeurtenissen {laatste} wordt ondersteund als de api-versie.</span><span class="sxs-lookup"><span data-stu-id="417e4-133">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="417e4-134">Deze indeling wordt niet meer ondersteund en in de toekomst wordt afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="417e4-134">This format is no longer supported and will be deprecated in the future.</span></span>

<span data-ttu-id="417e4-135">Als er nieuwere versies toevoegt, oudere versies is nog steeds toegankelijk voor compatibiliteit als uw scripts afhankelijk van specifieke gegevensindelingen zijn.</span><span class="sxs-lookup"><span data-stu-id="417e4-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="417e4-136">Houd er echter rekening mee dat de huidige preview version(2017-03-01) mogelijk niet beschikbaar zodra de service in het algemeen beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="417e4-136">However, note that the current preview version(2017-03-01) may not be available once the service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="417e4-137">Met behulp van Headers</span><span class="sxs-lookup"><span data-stu-id="417e4-137">Using Headers</span></span>
<span data-ttu-id="417e4-138">Wanneer u de Service-exemplaar voor metagegevens query uitvoert, moet u de header geven `Metadata: true` om te controleren of de aanvraag is niet per ongeluk wordt omgeleid.</span><span class="sxs-lookup"><span data-stu-id="417e4-138">When you query the Instance Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="417e4-139">Ophalen van metagegevens</span><span class="sxs-lookup"><span data-stu-id="417e4-139">Retrieving metadata</span></span>

<span data-ttu-id="417e4-140">Metagegevens van het exemplaar is beschikbaar voor het uitvoeren van virtuele machines die zijn gemaakt/beheerd met behulp van [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="417e4-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="417e4-141">Toegang tot alle gegevenscategorieën voor een exemplaar van de virtuele machine met de volgende aanvraag:</span><span class="sxs-lookup"><span data-stu-id="417e4-141">Access all data categories for a virtual machine instance using the following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="417e4-142">Alle query's voor exemplaar-metagegevens zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="417e4-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="417e4-143">Data-uitvoer</span><span class="sxs-lookup"><span data-stu-id="417e4-143">Data output</span></span>
<span data-ttu-id="417e4-144">Standaard stuurt de metagegevens-Service-exemplaar gegevens in JSON-indeling (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="417e4-144">By default, the Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="417e4-145">Verschillende API's kunnen echter gegevens in verschillende indelingen geretourneerd als aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="417e4-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="417e4-146">De volgende tabel bevat een verwijzing naar andere indelingen met de die API 's kunnen ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="417e4-146">The following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="417e4-147">API</span><span class="sxs-lookup"><span data-stu-id="417e4-147">API</span></span> | <span data-ttu-id="417e4-148">Standaardindeling voor gegevens</span><span class="sxs-lookup"><span data-stu-id="417e4-148">Default Data Format</span></span> | <span data-ttu-id="417e4-149">Andere indelingen</span><span class="sxs-lookup"><span data-stu-id="417e4-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="417e4-150">/Instance</span><span class="sxs-lookup"><span data-stu-id="417e4-150">/instance</span></span> | <span data-ttu-id="417e4-151">JSON</span><span class="sxs-lookup"><span data-stu-id="417e4-151">json</span></span> | <span data-ttu-id="417e4-152">Tekst</span><span class="sxs-lookup"><span data-stu-id="417e4-152">text</span></span>
<span data-ttu-id="417e4-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="417e4-153">/scheduledevents</span></span> | <span data-ttu-id="417e4-154">JSON</span><span class="sxs-lookup"><span data-stu-id="417e4-154">json</span></span> | <span data-ttu-id="417e4-155">Geen</span><span class="sxs-lookup"><span data-stu-id="417e4-155">none</span></span>

<span data-ttu-id="417e4-156">Geef de vereiste indeling als een parameter van de querytekenreeks worden opgegeven in de aanvraag voor toegang tot een niet-standaard antwoordindeling moet.</span><span class="sxs-lookup"><span data-stu-id="417e4-156">To access a non-default response format, specify the requested format as a querystring parameter in the request.</span></span> <span data-ttu-id="417e4-157">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="417e4-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="417e4-158">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="417e4-158">Security</span></span>
<span data-ttu-id="417e4-159">Het exemplaar metagegevens Service-eindpunt is alleen toegankelijk vanuit de actieve sessie van de virtuele machine op een niet-routeerbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="417e4-159">The Instance Metadata Service endpoint is accessible only from within the running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="417e4-160">Bovendien verzoeken met een `X-Forwarded-For` header is geweigerd door de service.</span><span class="sxs-lookup"><span data-stu-id="417e4-160">In addition, any request with a `X-Forwarded-For` header is rejected by the service.</span></span>
<span data-ttu-id="417e4-161">Moet ook aanvragen bevatten een `Metadata: true` header om ervoor te zorgen dat de werkelijke aanvraag rechtstreeks bestemd en geen deel uit van onbedoelde omleiding is.</span><span class="sxs-lookup"><span data-stu-id="417e4-161">We also require requests to contain a `Metadata: true` header to ensure that the actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="417e4-162">Fout</span><span class="sxs-lookup"><span data-stu-id="417e4-162">Error</span></span>
<span data-ttu-id="417e4-163">Als er een gegevenselement niet gevonden of een onjuist gevormde aanvraag, retourneert de Service-exemplaar voor metagegevens standaard HTTP-fouten.</span><span class="sxs-lookup"><span data-stu-id="417e4-163">If there is a data element not found or a malformed request, the Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="417e4-164">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="417e4-164">For example:</span></span>

<span data-ttu-id="417e4-165">HTTP-statuscode</span><span class="sxs-lookup"><span data-stu-id="417e4-165">HTTP Status Code</span></span> | <span data-ttu-id="417e4-166">Reden</span><span class="sxs-lookup"><span data-stu-id="417e4-166">Reason</span></span>
----------------|-------
<span data-ttu-id="417e4-167">200 OK</span><span class="sxs-lookup"><span data-stu-id="417e4-167">200 OK</span></span> |
<span data-ttu-id="417e4-168">400 onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="417e4-168">400 Bad Request</span></span> | <span data-ttu-id="417e4-169">Ontbrekende `Metadata: true` koptekst</span><span class="sxs-lookup"><span data-stu-id="417e4-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="417e4-170">404 – Niet gevonden</span><span class="sxs-lookup"><span data-stu-id="417e4-170">404 Not Found</span></span> | <span data-ttu-id="417e4-171">Het gevraagde element does't bestaan</span><span class="sxs-lookup"><span data-stu-id="417e4-171">The requested element does't exist</span></span> 
<span data-ttu-id="417e4-172">405 methode is niet toegestaan</span><span class="sxs-lookup"><span data-stu-id="417e4-172">405 Method Not Allowed</span></span> | <span data-ttu-id="417e4-173">Alleen `GET` en `POST` aanvragen worden ondersteund</span><span class="sxs-lookup"><span data-stu-id="417e4-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="417e4-174">429 te veel aanvragen</span><span class="sxs-lookup"><span data-stu-id="417e4-174">429 Too Many Requests</span></span> | <span data-ttu-id="417e4-175">De API ondersteunt momenteel maximaal 5 query's per seconde</span><span class="sxs-lookup"><span data-stu-id="417e4-175">The API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="417e4-176">Fout 500-Service</span><span class="sxs-lookup"><span data-stu-id="417e4-176">500 Service Error</span></span>     | <span data-ttu-id="417e4-177">Probeer na enige tijd</span><span class="sxs-lookup"><span data-stu-id="417e4-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="417e4-178">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="417e4-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="417e4-179">Alle antwoorden op de API zijn JSON-tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="417e4-179">All API responses are JSON strings.</span></span> <span data-ttu-id="417e4-180">Alle antwoorden op de volgende voorbeeld zijn voor de leesbaarheid pretty afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="417e4-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="417e4-181">Bij het ophalen van informatie over het netwerk</span><span class="sxs-lookup"><span data-stu-id="417e4-181">Retrieving network information</span></span>

<span data-ttu-id="417e4-182">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="417e4-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="417e4-183">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="417e4-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="417e4-184">Het antwoord is een JSON-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="417e4-184">The response is a JSON string.</span></span> <span data-ttu-id="417e4-185">Het volgende voorbeeld-antwoord is voor de leesbaarheid pretty afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="417e4-185">The following example response is pretty-printed for readability.</span></span>

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="417e4-186">Openbaar IP-adres ophalen</span><span class="sxs-lookup"><span data-stu-id="417e4-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="417e4-187">Ophalen van metagegevens voor een exemplaar van alle</span><span class="sxs-lookup"><span data-stu-id="417e4-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="417e4-188">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="417e4-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="417e4-189">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="417e4-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="417e4-190">Het antwoord is een JSON-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="417e4-190">The response is a JSON string.</span></span> <span data-ttu-id="417e4-191">Het volgende voorbeeld-antwoord is voor de leesbaarheid pretty afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="417e4-191">The following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="417e4-192">Ophalen van metagegevens in Windows virtuele Machine</span><span class="sxs-lookup"><span data-stu-id="417e4-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="417e4-193">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="417e4-193">**Request**</span></span>

<span data-ttu-id="417e4-194">Metagegevens van het exemplaar kan worden opgehaald in Windows via het hulpprogramma PowerShell `curl`:</span><span class="sxs-lookup"><span data-stu-id="417e4-194">Instance metadata can be retrieved in Windows via the PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="417e4-195">Of via de `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="417e4-195">Or through the `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="417e4-196">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="417e4-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="417e4-197">Het antwoord is een JSON-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="417e4-197">The response is a JSON string.</span></span> <span data-ttu-id="417e4-198">Het volgende voorbeeld-antwoord is voor de leesbaarheid pretty afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="417e4-198">The following example response  is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="417e4-199">Exemplaar metagegevens gegevenscategorieën</span><span class="sxs-lookup"><span data-stu-id="417e4-199">Instance metadata data categories</span></span>
<span data-ttu-id="417e4-200">De volgende gegevenscategorieën zijn beschikbaar via de Service-exemplaar voor metagegevens:</span><span class="sxs-lookup"><span data-stu-id="417e4-200">The following data categories are available through the Instance Metadata Service:</span></span>

<span data-ttu-id="417e4-201">Gegevens</span><span class="sxs-lookup"><span data-stu-id="417e4-201">Data</span></span> | <span data-ttu-id="417e4-202">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="417e4-202">Description</span></span>
-----|------------
<span data-ttu-id="417e4-203">location</span><span class="sxs-lookup"><span data-stu-id="417e4-203">location</span></span> | <span data-ttu-id="417e4-204">Azure-regio de virtuele machine wordt uitgevoerd in de</span><span class="sxs-lookup"><span data-stu-id="417e4-204">Azure Region the VM is running in</span></span>
<span data-ttu-id="417e4-205">naam</span><span class="sxs-lookup"><span data-stu-id="417e4-205">name</span></span> | <span data-ttu-id="417e4-206">Naam van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="417e4-206">Name of the VM</span></span> 
<span data-ttu-id="417e4-207">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="417e4-207">offer</span></span> | <span data-ttu-id="417e4-208">Bieden informatie over de VM-afbeelding.</span><span class="sxs-lookup"><span data-stu-id="417e4-208">Offer information for the VM image.</span></span> <span data-ttu-id="417e4-209">Deze waarde is alleen aanwezig voor afbeeldingen van afbeelding voor Azure-galerie geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="417e4-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="417e4-210">Uitgever</span><span class="sxs-lookup"><span data-stu-id="417e4-210">publisher</span></span> | <span data-ttu-id="417e4-211">Uitgever van de VM-installatiekopie</span><span class="sxs-lookup"><span data-stu-id="417e4-211">Publisher of the VM image</span></span>
<span data-ttu-id="417e4-212">SKU</span><span class="sxs-lookup"><span data-stu-id="417e4-212">sku</span></span> | <span data-ttu-id="417e4-213">Specifieke SKU voor de VM-installatiekopie</span><span class="sxs-lookup"><span data-stu-id="417e4-213">Specific SKU for the VM image</span></span>  
<span data-ttu-id="417e4-214">Versie</span><span class="sxs-lookup"><span data-stu-id="417e4-214">version</span></span> | <span data-ttu-id="417e4-215">Versie van de VM-afbeelding</span><span class="sxs-lookup"><span data-stu-id="417e4-215">Version of the VM image</span></span> 
<span data-ttu-id="417e4-216">besturingssysteemtype</span><span class="sxs-lookup"><span data-stu-id="417e4-216">osType</span></span> | <span data-ttu-id="417e4-217">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="417e4-217">Linux or Windows</span></span> 
<span data-ttu-id="417e4-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="417e4-218">platformUpdateDomain</span></span> |  <span data-ttu-id="417e4-219">[Updatedomein](virtual-machines-windows-manage-availability.md) in de virtuele machine wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="417e4-219">[Update domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="417e4-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="417e4-220">platformFaultDomain</span></span> | <span data-ttu-id="417e4-221">[Foutdomein](virtual-machines-windows-manage-availability.md) in de virtuele machine wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="417e4-221">[Fault domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="417e4-222">vmId</span><span class="sxs-lookup"><span data-stu-id="417e4-222">vmId</span></span> | <span data-ttu-id="417e4-223">[De unieke id](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) voor de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="417e4-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for the VM</span></span>
<span data-ttu-id="417e4-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="417e4-224">vmSize</span></span> | [<span data-ttu-id="417e4-225">VM-grootte</span><span class="sxs-lookup"><span data-stu-id="417e4-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="417e4-226">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="417e4-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="417e4-227">Lokale IPv4-adres van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="417e4-227">Local IPv4 address of the VM</span></span> 
<span data-ttu-id="417e4-228">IPv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="417e4-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="417e4-229">Openbaar IPv4-adres van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="417e4-229">Public IPv4 address of the VM</span></span>
<span data-ttu-id="417e4-230">subnetadres /</span><span class="sxs-lookup"><span data-stu-id="417e4-230">subnet/address</span></span> | <span data-ttu-id="417e4-231">Subnetadres van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="417e4-231">Subnet address of the VM</span></span>
<span data-ttu-id="417e4-232">subnetvoorvoegsel /</span><span class="sxs-lookup"><span data-stu-id="417e4-232">subnet/prefix</span></span> | <span data-ttu-id="417e4-233">Subnetvoorvoegsel, voorbeeld 24</span><span class="sxs-lookup"><span data-stu-id="417e4-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="417e4-234">IPv6/IP-adres</span><span class="sxs-lookup"><span data-stu-id="417e4-234">ipv6/ipAddress</span></span> | <span data-ttu-id="417e4-235">Lokale IPv6-adres van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="417e4-235">Local IPv6 address of the VM</span></span>
<span data-ttu-id="417e4-236">MAC-adres</span><span class="sxs-lookup"><span data-stu-id="417e4-236">macAddress</span></span> | <span data-ttu-id="417e4-237">Mac-adres van VM</span><span class="sxs-lookup"><span data-stu-id="417e4-237">VM mac address</span></span> 
<span data-ttu-id="417e4-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="417e4-238">scheduledevents</span></span> | <span data-ttu-id="417e4-239">Op dit moment in de openbare Preview Zie [scheduledevents](virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="417e4-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="417e4-240">Voorbeeldscenario's voor gebruik</span><span class="sxs-lookup"><span data-stu-id="417e4-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="417e4-241">Uitgevoerd op Azure VM bijhouden</span><span class="sxs-lookup"><span data-stu-id="417e4-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="417e4-242">Als een serviceprovider mogelijk nodig bij te houden van het aantal virtuele machines met uw software of agents die u wilt volgen Uniekheid van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="417e4-242">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span></span> <span data-ttu-id="417e4-243">Als u een unieke ID voor een virtuele machine ophalen, gebruikt u de `vmId` veld van metagegevens-Service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="417e4-243">To be able to get a unique ID for a VM, use the `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="417e4-244">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="417e4-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="417e4-245">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="417e4-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="417e4-246">Plaatsing van containers domein veroorzaakt of bij te werken op basis van gegevens partities</span><span class="sxs-lookup"><span data-stu-id="417e4-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="417e4-247">Voor bepaalde scenario's, de plaatsing van replica's van verschillende gegevens is van primair belang.</span><span class="sxs-lookup"><span data-stu-id="417e4-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="417e4-248">Bijvoorbeeld: [HDFS replica plaatsing](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) of plaatsing van de container via een [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) mogelijk dat u wilt weten de `platformFaultDomain` en `platformUpdateDomain` op de virtuele machine wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="417e4-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require to know the `platformFaultDomain` and `platformUpdateDomain` the VM is running on.</span></span>
<span data-ttu-id="417e4-249">U kunt deze gegevens rechtstreeks via de Service-exemplaar voor metagegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="417e4-249">You can query this data directly via the Instance Metadata Service.</span></span>

<span data-ttu-id="417e4-250">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="417e4-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="417e4-251">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="417e4-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a><span data-ttu-id="417e4-252">Meer informatie over de virtuele machine tijdens ondersteuningsaanvraag ophalen</span><span class="sxs-lookup"><span data-stu-id="417e4-252">Getting more information about the VM during support case</span></span> 

<span data-ttu-id="417e4-253">Als een serviceprovider krijgt u mogelijk een telefoongesprek ondersteuning waarin u wilt weten van meer informatie over de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="417e4-253">As a service provider, you may get a support call where you would like to know more information about the VM.</span></span> <span data-ttu-id="417e4-254">Vragen van de klant voor het delen van de compute-metagegevens kunt basisinformatie voor de medewerker weten over de aard van de virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="417e4-254">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span></span> 

<span data-ttu-id="417e4-255">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="417e4-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="417e4-256">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="417e4-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="417e4-257">Het antwoord is een JSON-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="417e4-257">The response is a JSON string.</span></span> <span data-ttu-id="417e4-258">Het volgende voorbeeld-antwoord is voor de leesbaarheid pretty afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="417e4-258">The following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-the-vm"></a><span data-ttu-id="417e4-259">Voorbeelden van het aanroepen van metagegevensservice met behulp van verschillende talen in de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="417e4-259">Examples of calling metadata service using different languages inside the VM</span></span> 

<span data-ttu-id="417e4-260">Taal</span><span class="sxs-lookup"><span data-stu-id="417e4-260">Language</span></span> | <span data-ttu-id="417e4-261">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="417e4-261">Example</span></span> 
---------|----------------
<span data-ttu-id="417e4-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="417e4-262">Ruby</span></span>     | <span data-ttu-id="417e4-263">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.RB</span><span class="sxs-lookup"><span data-stu-id="417e4-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="417e4-264">Ga Lan</span><span class="sxs-lookup"><span data-stu-id="417e4-264">Go Lan</span></span>   | <span data-ttu-id="417e4-265">https://github.com/Microsoft/azureimds/BLOB/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="417e4-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="417e4-266">python</span><span class="sxs-lookup"><span data-stu-id="417e4-266">python</span></span>   | <span data-ttu-id="417e4-267">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.PY</span><span class="sxs-lookup"><span data-stu-id="417e4-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="417e4-268">C++</span><span class="sxs-lookup"><span data-stu-id="417e4-268">C++</span></span>      | <span data-ttu-id="417e4-269">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample-Windows.cpp</span><span class="sxs-lookup"><span data-stu-id="417e4-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="417e4-270">C#</span><span class="sxs-lookup"><span data-stu-id="417e4-270">C#</span></span>       | <span data-ttu-id="417e4-271">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="417e4-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="417e4-272">Javascript</span><span class="sxs-lookup"><span data-stu-id="417e4-272">Javascript</span></span> | <span data-ttu-id="417e4-273">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="417e4-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="417e4-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="417e4-274">Powershell</span></span> | <span data-ttu-id="417e4-275">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="417e4-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="417e4-276">Bash</span><span class="sxs-lookup"><span data-stu-id="417e4-276">Bash</span></span>       | <span data-ttu-id="417e4-277">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="417e4-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="417e4-278">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="417e4-278">FAQ</span></span>
1. <span data-ttu-id="417e4-279">Ik krijg de fout `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="417e4-279">I am getting the error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="417e4-280">Wat betekent dit?</span><span class="sxs-lookup"><span data-stu-id="417e4-280">What does this mean?</span></span>
   * <span data-ttu-id="417e4-281">De Service-exemplaar voor metagegevens is vereist voor de header `Metadata: true` in de aanvraag moet worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="417e4-281">The Instance Metadata Service requires the header `Metadata: true` to be passed in the request.</span></span> <span data-ttu-id="417e4-282">Deze header wordt doorgegeven in de REST-aanroep staat toegang tot de Service-exemplaar voor metagegevens.</span><span class="sxs-lookup"><span data-stu-id="417e4-282">Passing this header in the REST call allows access to the Instance Metadata Service.</span></span> 
2. <span data-ttu-id="417e4-283">Waarom niet krijg ik compute-informatie voor mijn VM?</span><span class="sxs-lookup"><span data-stu-id="417e4-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="417e4-284">De Service-exemplaar voor metagegevens ondersteunt momenteel alleen exemplaren gemaakt met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="417e4-284">Currently the Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="417e4-285">In de toekomst kunnen we ondersteuning voor virtuele machines van Cloud Service toevoegen.</span><span class="sxs-lookup"><span data-stu-id="417e4-285">In the future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="417e4-286">Ik heb mijn virtuele Machine via Azure Resource Manager een tijd terug gemaakt.</span><span class="sxs-lookup"><span data-stu-id="417e4-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="417e4-287">Waarom kan ik geen Zie compute-metagegevens?</span><span class="sxs-lookup"><span data-stu-id="417e4-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="417e4-288">Voor alle virtuele machines na Sep 2016 is gemaakt, voegt u een [Tag](../azure-resource-manager/resource-group-using-tags.md) om te beginnen te zien compute metagegevens.</span><span class="sxs-lookup"><span data-stu-id="417e4-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span></span> <span data-ttu-id="417e4-289">Voor oudere virtuele machines (gemaakt vóór Sep-2016), software-extensies of gegevens schijven aan de virtuele machine vernieuwen-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="417e4-289">For older VMs (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span></span>
4. <span data-ttu-id="417e4-290">Waarom krijg ik de fout `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="417e4-290">Why am I getting the error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="417e4-291">Probeer uw aanvraag op basis van de exponentiële back uit het systeem.</span><span class="sxs-lookup"><span data-stu-id="417e4-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="417e4-292">Neem contact op met de ondersteuning van Azure als het probleem zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="417e4-292">If the issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="417e4-293">Waar kan ik aanvullende vragen/opmerkingen delen</span><span class="sxs-lookup"><span data-stu-id="417e4-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="417e4-294">Uw opmerkingen over http://feedback.azure.com verzenden.</span><span class="sxs-lookup"><span data-stu-id="417e4-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="417e4-295">Dit werkt voor virtuele Machine Scale ingesteld exemplaar, zou?</span><span class="sxs-lookup"><span data-stu-id="417e4-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="417e4-296">Ja is metagegevens-service beschikbaar voor Scale-exemplaren instellen.</span><span class="sxs-lookup"><span data-stu-id="417e4-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="417e4-297">Hoe krijg ik ondersteuning voor de service</span><span class="sxs-lookup"><span data-stu-id="417e4-297">How do I get support for the service?</span></span>
   * <span data-ttu-id="417e4-298">Als u ondersteuning voor de service, een ondersteuning probleem maken in Azure-portal voor de virtuele machine waar u ze niet ophalen van metagegevens antwoord na lang pogingen</span><span class="sxs-lookup"><span data-stu-id="417e4-298">To get support for the service, create a support issue in Azure portal for the VM where you are not able to get metadata response after long retries</span></span> 

   ![Ondersteuning voor Instance Metagegevens](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="417e4-300">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="417e4-300">Next Steps</span></span>

- <span data-ttu-id="417e4-301">Meer informatie over de [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** geleverd door de Service-exemplaar voor metagegevens.</span><span class="sxs-lookup"><span data-stu-id="417e4-301">Learn more about the [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by the Instance Metadata Service.</span></span>
