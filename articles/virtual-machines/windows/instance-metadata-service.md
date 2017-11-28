---
title: aaaAzure exemplaar metagegevens Service voor Windows | Microsoft Docs
description: RESTful-interface tooget informatie over Windows-VM compute, netwerk en toekomstig onderhoud gebeurtenissen.
services: virtual-machines-windows
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a33c26b5e9ed650be639598cdb6895fc19ccb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-windows-vms"></a><span data-ttu-id="07f07-103">Azure-service metagegevens van het exemplaar voor VM's van Windows</span><span class="sxs-lookup"><span data-stu-id="07f07-103">Azure Instance Metadata service for Windows VMs</span></span>


<span data-ttu-id="07f07-104">Hello Azure exemplaar metagegevens Service biedt informatie over het uitvoeren van de virtuele machine-exemplaren die kunnen worden gebruikt toomanage en configureren van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="07f07-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="07f07-105">Dit omvat gegevens zoals SKU netwerkconfiguratie en toekomstig onderhoud gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="07f07-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="07f07-106">Zie voor meer informatie over wat voor soort informatie beschikbaar is, [metagegevens categorieën](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="07f07-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="07f07-107">Azure instantie metagegevens-Service is een REST-eindpunt toegankelijk tooall IaaS VM's die zijn gemaakt via Hallo [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="07f07-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="07f07-108">Hallo-eindpunt is beschikbaar op een bekende niet-routeerbare IP-adres (`169.254.169.254`) die kan alleen worden benaderd binnen Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="07f07-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>



> [!IMPORTANT]
> <span data-ttu-id="07f07-109">Deze service is **algemeen beschikbaar** in globale Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="07f07-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="07f07-110">Het is openbare Preview voor Government, China en Duitse Azure-Cloud.</span><span class="sxs-lookup"><span data-stu-id="07f07-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="07f07-111">Het ontvangt regelmatig updates tooexpose nieuwe informatie over exemplaren van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07f07-111">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="07f07-112">Deze pagina geeft Hallo up-to-date [gegevenscategorieën](#instance-metadata-data-categories) beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="07f07-112">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>



## <a name="service-availability"></a><span data-ttu-id="07f07-113">Beschikbaarheid van de service</span><span class="sxs-lookup"><span data-stu-id="07f07-113">Service Availability</span></span>
<span data-ttu-id="07f07-114">Hallo-service is beschikbaar in alle algemeen beschikbaar globale Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="07f07-114">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="07f07-115">Hallo-service zich in de openbare preview in Hallo Government, China of Duitsland regio's.</span><span class="sxs-lookup"><span data-stu-id="07f07-115">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="07f07-116">Regio's</span><span class="sxs-lookup"><span data-stu-id="07f07-116">Regions</span></span>                                        | <span data-ttu-id="07f07-117">Beschikbaarheid?</span><span class="sxs-lookup"><span data-stu-id="07f07-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="07f07-118">Alle in het algemeen beschikbare globale Azure-regio 's</span><span class="sxs-lookup"><span data-stu-id="07f07-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="07f07-119">Algemeen beschikbaar</span><span class="sxs-lookup"><span data-stu-id="07f07-119">Generally Available</span></span> 
[<span data-ttu-id="07f07-120">Azure Government</span><span class="sxs-lookup"><span data-stu-id="07f07-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="07f07-121">Preview-versie</span><span class="sxs-lookup"><span data-stu-id="07f07-121">In Preview</span></span> 
[<span data-ttu-id="07f07-122">Azure China</span><span class="sxs-lookup"><span data-stu-id="07f07-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="07f07-123">Preview-versie</span><span class="sxs-lookup"><span data-stu-id="07f07-123">In Preview</span></span>
[<span data-ttu-id="07f07-124">Azure Duitsland</span><span class="sxs-lookup"><span data-stu-id="07f07-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="07f07-125">Preview-versie</span><span class="sxs-lookup"><span data-stu-id="07f07-125">In Preview</span></span>

<span data-ttu-id="07f07-126">Deze tabel wordt bijgewerkt zodra Hallo service beschikbaar in andere Azure-clouds.</span><span class="sxs-lookup"><span data-stu-id="07f07-126">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="07f07-127">tootry uit Hallo Service-exemplaar voor metagegevens, maak een VM van [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) of Hallo [Azure-portal](http://portal.azure.com) in Hallo hierboven regio's en volg de volgende Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="07f07-127">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="07f07-128">Gebruik</span><span class="sxs-lookup"><span data-stu-id="07f07-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="07f07-129">Versiebeheer voor onderdelen</span><span class="sxs-lookup"><span data-stu-id="07f07-129">Versioning</span></span>
<span data-ttu-id="07f07-130">Hallo metagegevens-Service-exemplaar is samengesteld.</span><span class="sxs-lookup"><span data-stu-id="07f07-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="07f07-131">Versies zijn verplicht en de huidige versie Hallo is `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="07f07-131">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="07f07-132">Eerdere versies van de preview van geplande gebeurtenissen {laatste} wordt ondersteund als Hallo api-versie.</span><span class="sxs-lookup"><span data-stu-id="07f07-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="07f07-133">Deze indeling wordt niet meer ondersteund en in toekomstige hello wordt afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="07f07-133">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="07f07-134">Als er nieuwere versies toevoegt, oudere versies is nog steeds toegankelijk voor compatibiliteit als uw scripts afhankelijk van specifieke gegevensindelingen zijn.</span><span class="sxs-lookup"><span data-stu-id="07f07-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="07f07-135">Bedenk wel dat Hallo huidige preview version(2017-03-01) mogelijk niet beschikbaar zodra de service Hallo algemeen beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="07f07-135">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="07f07-136">Met behulp van headers</span><span class="sxs-lookup"><span data-stu-id="07f07-136">Using headers</span></span>
<span data-ttu-id="07f07-137">Wanneer u query Hallo exemplaar metagegevens Service uitvoert, moet u opgeven Hallo header `Metadata: true` tooensure Hallo verzoek is niet per ongeluk omgeleid.</span><span class="sxs-lookup"><span data-stu-id="07f07-137">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="07f07-138">Ophalen van metagegevens</span><span class="sxs-lookup"><span data-stu-id="07f07-138">Retrieving metadata</span></span>

<span data-ttu-id="07f07-139">Metagegevens van het exemplaar is beschikbaar voor het uitvoeren van virtuele machines die zijn gemaakt/beheerd met behulp van [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="07f07-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="07f07-140">Toegang tot alle gegevenscategorieën voor een exemplaar van de virtuele machine met behulp van de volgende aanvraag Hallo:</span><span class="sxs-lookup"><span data-stu-id="07f07-140">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="07f07-141">Alle query's voor exemplaar-metagegevens zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="07f07-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="07f07-142">Data-uitvoer</span><span class="sxs-lookup"><span data-stu-id="07f07-142">Data output</span></span>
<span data-ttu-id="07f07-143">Standaard Hallo exemplaar metagegevens Service gegevens worden geretourneerd in JSON-indeling (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="07f07-143">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="07f07-144">Verschillende API's kunnen echter gegevens in verschillende indelingen geretourneerd als aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="07f07-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="07f07-145">Hallo bevat volgende tabel een verwijzing naar andere indelingen met de die API 's kunnen ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="07f07-145">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="07f07-146">API</span><span class="sxs-lookup"><span data-stu-id="07f07-146">API</span></span> | <span data-ttu-id="07f07-147">Standaardindeling voor gegevens</span><span class="sxs-lookup"><span data-stu-id="07f07-147">Default Data Format</span></span> | <span data-ttu-id="07f07-148">Andere indelingen</span><span class="sxs-lookup"><span data-stu-id="07f07-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="07f07-149">/Instance</span><span class="sxs-lookup"><span data-stu-id="07f07-149">/instance</span></span> | <span data-ttu-id="07f07-150">JSON</span><span class="sxs-lookup"><span data-stu-id="07f07-150">json</span></span> | <span data-ttu-id="07f07-151">Tekst</span><span class="sxs-lookup"><span data-stu-id="07f07-151">text</span></span>
<span data-ttu-id="07f07-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="07f07-152">/scheduledevents</span></span> | <span data-ttu-id="07f07-153">JSON</span><span class="sxs-lookup"><span data-stu-id="07f07-153">json</span></span> | <span data-ttu-id="07f07-154">Geen</span><span class="sxs-lookup"><span data-stu-id="07f07-154">none</span></span>

<span data-ttu-id="07f07-155">een niet-standaard antwoordindeling tooaccess opgeven Hallo aangevraagde indeling als een parameter querystring in Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="07f07-155">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="07f07-156">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="07f07-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="07f07-157">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="07f07-157">Security</span></span>
<span data-ttu-id="07f07-158">Hallo exemplaar metagegevens Service-eindpunt is alleen toegankelijk vanuit Hallo met een exemplaar van de virtuele machine op een niet-routeerbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="07f07-158">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="07f07-159">Bovendien verzoeken met een `X-Forwarded-For` header is geweigerd door Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="07f07-159">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="07f07-160">Ook aanvragen toocontain moet een `Metadata: true` header tooensure die Hallo werkelijke aanvraag rechtstreeks is bestemd en geen deel uit van onbedoelde omleiding.</span><span class="sxs-lookup"><span data-stu-id="07f07-160">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="07f07-161">Fout</span><span class="sxs-lookup"><span data-stu-id="07f07-161">Error</span></span>
<span data-ttu-id="07f07-162">Als er een gegevenselement niet gevonden of een onjuist gevormde aanvraag, retourneert Hallo exemplaar metagegevens Service standaard HTTP-fouten.</span><span class="sxs-lookup"><span data-stu-id="07f07-162">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="07f07-163">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="07f07-163">For example:</span></span>

<span data-ttu-id="07f07-164">HTTP-statuscode</span><span class="sxs-lookup"><span data-stu-id="07f07-164">HTTP Status Code</span></span> | <span data-ttu-id="07f07-165">Reden</span><span class="sxs-lookup"><span data-stu-id="07f07-165">Reason</span></span>
----------------|-------
<span data-ttu-id="07f07-166">200 OK</span><span class="sxs-lookup"><span data-stu-id="07f07-166">200 OK</span></span> |
<span data-ttu-id="07f07-167">400 onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="07f07-167">400 Bad Request</span></span> | <span data-ttu-id="07f07-168">Ontbrekende `Metadata: true` koptekst</span><span class="sxs-lookup"><span data-stu-id="07f07-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="07f07-169">404 – Niet gevonden</span><span class="sxs-lookup"><span data-stu-id="07f07-169">404 Not Found</span></span> | <span data-ttu-id="07f07-170">Hallo gevraagde element does't bestaan</span><span class="sxs-lookup"><span data-stu-id="07f07-170">hello requested element does't exist</span></span> 
<span data-ttu-id="07f07-171">405 methode is niet toegestaan</span><span class="sxs-lookup"><span data-stu-id="07f07-171">405 Method Not Allowed</span></span> | <span data-ttu-id="07f07-172">Alleen `GET` en `POST` aanvragen worden ondersteund</span><span class="sxs-lookup"><span data-stu-id="07f07-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="07f07-173">429 te veel aanvragen</span><span class="sxs-lookup"><span data-stu-id="07f07-173">429 Too Many Requests</span></span> | <span data-ttu-id="07f07-174">Hallo-API ondersteunt momenteel maximaal 5 query's per seconde</span><span class="sxs-lookup"><span data-stu-id="07f07-174">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="07f07-175">Fout 500-Service</span><span class="sxs-lookup"><span data-stu-id="07f07-175">500 Service Error</span></span>     | <span data-ttu-id="07f07-176">Probeer na enige tijd</span><span class="sxs-lookup"><span data-stu-id="07f07-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="07f07-177">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="07f07-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="07f07-178">Alle antwoorden op de API zijn JSON-tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="07f07-178">All API responses are JSON strings.</span></span> <span data-ttu-id="07f07-179">Alle antwoorden op de volgende voorbeeld zijn voor de leesbaarheid pretty afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="07f07-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="07f07-180">Bij het ophalen van informatie over het netwerk</span><span class="sxs-lookup"><span data-stu-id="07f07-180">Retrieving network information</span></span>

<span data-ttu-id="07f07-181">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="07f07-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="07f07-182">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="07f07-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="07f07-183">Hallo-antwoord is een JSON-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="07f07-183">hello response is a JSON string.</span></span> <span data-ttu-id="07f07-184">Hallo volgende voorbeeld van een antwoord is voor de leesbaarheid pretty afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="07f07-184">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="07f07-185">Openbaar IP-adres ophalen</span><span class="sxs-lookup"><span data-stu-id="07f07-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="07f07-186">Ophalen van metagegevens voor een exemplaar van alle</span><span class="sxs-lookup"><span data-stu-id="07f07-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="07f07-187">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="07f07-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="07f07-188">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="07f07-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="07f07-189">Hallo-antwoord is een JSON-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="07f07-189">hello response is a JSON string.</span></span> <span data-ttu-id="07f07-190">Hallo volgende voorbeeld van een antwoord is voor de leesbaarheid pretty afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="07f07-190">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="07f07-191">Ophalen van metagegevens van de virtuele machine voor Windows</span><span class="sxs-lookup"><span data-stu-id="07f07-191">Retrieving metadata in Windows virtual machine</span></span>

<span data-ttu-id="07f07-192">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="07f07-192">**Request**</span></span>

<span data-ttu-id="07f07-193">Metagegevens van het exemplaar kan worden opgehaald in Windows via Hallo PowerShell hulpprogramma `curl`:</span><span class="sxs-lookup"><span data-stu-id="07f07-193">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="07f07-194">Of via Hallo `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="07f07-194">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="07f07-195">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="07f07-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="07f07-196">Hallo-antwoord is een JSON-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="07f07-196">hello response is a JSON string.</span></span> <span data-ttu-id="07f07-197">Hallo volgende voorbeeld van een antwoord is voor de leesbaarheid pretty afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="07f07-197">hello following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="07f07-198">Exemplaar metagegevens gegevenscategorieën</span><span class="sxs-lookup"><span data-stu-id="07f07-198">Instance metadata data categories</span></span>
<span data-ttu-id="07f07-199">Hallo na gegevenscategorieën zijn beschikbaar via Hallo exemplaar metagegevens Service:</span><span class="sxs-lookup"><span data-stu-id="07f07-199">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="07f07-200">Gegevens</span><span class="sxs-lookup"><span data-stu-id="07f07-200">Data</span></span> | <span data-ttu-id="07f07-201">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="07f07-201">Description</span></span>
-----|------------
<span data-ttu-id="07f07-202">location</span><span class="sxs-lookup"><span data-stu-id="07f07-202">location</span></span> | <span data-ttu-id="07f07-203">Azure regio Hallo VM wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="07f07-203">Azure Region hello VM is running in</span></span>
<span data-ttu-id="07f07-204">naam</span><span class="sxs-lookup"><span data-stu-id="07f07-204">name</span></span> | <span data-ttu-id="07f07-205">Naam van Hallo VM</span><span class="sxs-lookup"><span data-stu-id="07f07-205">Name of hello VM</span></span> 
<span data-ttu-id="07f07-206">Aanbieding</span><span class="sxs-lookup"><span data-stu-id="07f07-206">offer</span></span> | <span data-ttu-id="07f07-207">Informatie voor de VM-installatiekopie Hallo bieden.</span><span class="sxs-lookup"><span data-stu-id="07f07-207">Offer information for hello VM image.</span></span> <span data-ttu-id="07f07-208">Deze waarde is alleen aanwezig voor afbeeldingen van afbeelding voor Azure-galerie geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="07f07-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="07f07-209">Uitgever</span><span class="sxs-lookup"><span data-stu-id="07f07-209">publisher</span></span> | <span data-ttu-id="07f07-210">Uitgever van de VM-installatiekopie Hallo</span><span class="sxs-lookup"><span data-stu-id="07f07-210">Publisher of hello VM image</span></span>
<span data-ttu-id="07f07-211">SKU</span><span class="sxs-lookup"><span data-stu-id="07f07-211">sku</span></span> | <span data-ttu-id="07f07-212">Specifieke SKU voor Hallo VM-installatiekopie</span><span class="sxs-lookup"><span data-stu-id="07f07-212">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="07f07-213">Versie</span><span class="sxs-lookup"><span data-stu-id="07f07-213">version</span></span> | <span data-ttu-id="07f07-214">Versie van de VM-installatiekopie Hallo</span><span class="sxs-lookup"><span data-stu-id="07f07-214">Version of hello VM image</span></span> 
<span data-ttu-id="07f07-215">besturingssysteemtype</span><span class="sxs-lookup"><span data-stu-id="07f07-215">osType</span></span> | <span data-ttu-id="07f07-216">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="07f07-216">Linux or Windows</span></span> 
<span data-ttu-id="07f07-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="07f07-217">platformUpdateDomain</span></span> |  <span data-ttu-id="07f07-218">[Updatedomein](manage-availability.md) Hallo VM wordt uitgevoerd in</span><span class="sxs-lookup"><span data-stu-id="07f07-218">[Update domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="07f07-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="07f07-219">platformFaultDomain</span></span> | <span data-ttu-id="07f07-220">[Foutdomein](manage-availability.md) Hallo VM wordt uitgevoerd in</span><span class="sxs-lookup"><span data-stu-id="07f07-220">[Fault domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="07f07-221">vmId</span><span class="sxs-lookup"><span data-stu-id="07f07-221">vmId</span></span> | <span data-ttu-id="07f07-222">[De unieke id](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) voor Hallo VM</span><span class="sxs-lookup"><span data-stu-id="07f07-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="07f07-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="07f07-223">vmSize</span></span> | [<span data-ttu-id="07f07-224">VM-grootte</span><span class="sxs-lookup"><span data-stu-id="07f07-224">VM size</span></span>](sizes.md)
<span data-ttu-id="07f07-225">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="07f07-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="07f07-226">Lokale IPv4-adres van Hallo VM</span><span class="sxs-lookup"><span data-stu-id="07f07-226">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="07f07-227">IPv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="07f07-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="07f07-228">Openbare IPv4-adres van Hallo VM</span><span class="sxs-lookup"><span data-stu-id="07f07-228">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="07f07-229">subnetadres /</span><span class="sxs-lookup"><span data-stu-id="07f07-229">subnet/address</span></span> | <span data-ttu-id="07f07-230">Subnetadres Hallo VM</span><span class="sxs-lookup"><span data-stu-id="07f07-230">Subnet address of hello VM</span></span>
<span data-ttu-id="07f07-231">subnetvoorvoegsel /</span><span class="sxs-lookup"><span data-stu-id="07f07-231">subnet/prefix</span></span> | <span data-ttu-id="07f07-232">Subnetvoorvoegsel, voorbeeld 24</span><span class="sxs-lookup"><span data-stu-id="07f07-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="07f07-233">IPv6/IP-adres</span><span class="sxs-lookup"><span data-stu-id="07f07-233">ipv6/ipAddress</span></span> | <span data-ttu-id="07f07-234">Lokale IPv6-adres van Hallo VM</span><span class="sxs-lookup"><span data-stu-id="07f07-234">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="07f07-235">MAC-adres</span><span class="sxs-lookup"><span data-stu-id="07f07-235">macAddress</span></span> | <span data-ttu-id="07f07-236">Mac-adres van VM</span><span class="sxs-lookup"><span data-stu-id="07f07-236">VM mac address</span></span> 
<span data-ttu-id="07f07-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="07f07-237">scheduledevents</span></span> | <span data-ttu-id="07f07-238">Op dit moment in de openbare Preview Zie [scheduledevents](scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="07f07-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="07f07-239">Voorbeeldscenario's voor gebruik</span><span class="sxs-lookup"><span data-stu-id="07f07-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="07f07-240">Uitgevoerd op Azure VM bijhouden</span><span class="sxs-lookup"><span data-stu-id="07f07-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="07f07-241">Als een serviceprovider gewenste tootrack Hallo aantal virtuele machines met uw software of agenten die tootrack uniekheid Hallo VM nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="07f07-241">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="07f07-242">toobe kunnen tooget een unieke ID voor een virtuele machine, gebruik Hallo `vmId` veld van metagegevens-Service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="07f07-242">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="07f07-243">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="07f07-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="07f07-244">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="07f07-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="07f07-245">Plaatsing van containers domein veroorzaakt of bij te werken op basis van gegevens partities</span><span class="sxs-lookup"><span data-stu-id="07f07-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="07f07-246">Voor bepaalde scenario's, de plaatsing van replica's van verschillende gegevens is van primair belang.</span><span class="sxs-lookup"><span data-stu-id="07f07-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="07f07-247">Bijvoorbeeld: [HDFS replica plaatsing](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) of plaatsing van de container via een [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) mogelijk tooknow hello `platformFaultDomain` en `platformUpdateDomain` Hallo VM wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="07f07-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="07f07-248">U kunt deze gegevens rechtstreeks via Hallo exemplaar metagegevens Service opvragen.</span><span class="sxs-lookup"><span data-stu-id="07f07-248">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="07f07-249">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="07f07-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="07f07-250">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="07f07-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="07f07-251">Meer informatie over Hallo VM tijdens ondersteuningsaanvraag ophalen</span><span class="sxs-lookup"><span data-stu-id="07f07-251">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="07f07-252">Als een serviceprovider mogelijk dat u een telefoongesprek ondersteuning waar u wilt tooknow meer informatie over Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="07f07-252">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="07f07-253">Hallo klant tooshare vragen kunt Hallo compute metagegevens basisinformatie voor Hallo ondersteuning professional tooknow over Hallo-type van de virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="07f07-253">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="07f07-254">**Aanvraag**</span><span class="sxs-lookup"><span data-stu-id="07f07-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="07f07-255">**Antwoord**</span><span class="sxs-lookup"><span data-stu-id="07f07-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="07f07-256">Hallo-antwoord is een JSON-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="07f07-256">hello response is a JSON string.</span></span> <span data-ttu-id="07f07-257">Hallo volgende voorbeeld van een antwoord is voor de leesbaarheid pretty afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="07f07-257">hello following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="07f07-258">Voorbeelden van het aanroepen van metagegevensservice met behulp van verschillende talen in Hallo VM</span><span class="sxs-lookup"><span data-stu-id="07f07-258">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="07f07-259">Taal</span><span class="sxs-lookup"><span data-stu-id="07f07-259">Language</span></span> | <span data-ttu-id="07f07-260">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="07f07-260">Example</span></span> 
---------|----------------
<span data-ttu-id="07f07-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="07f07-261">Ruby</span></span>     | <span data-ttu-id="07f07-262">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.RB</span><span class="sxs-lookup"><span data-stu-id="07f07-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="07f07-263">Ga Lan</span><span class="sxs-lookup"><span data-stu-id="07f07-263">Go Lan</span></span>   | <span data-ttu-id="07f07-264">https://github.com/Microsoft/azureimds/BLOB/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="07f07-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="07f07-265">python</span><span class="sxs-lookup"><span data-stu-id="07f07-265">python</span></span>   | <span data-ttu-id="07f07-266">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.PY</span><span class="sxs-lookup"><span data-stu-id="07f07-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="07f07-267">C++</span><span class="sxs-lookup"><span data-stu-id="07f07-267">C++</span></span>      | <span data-ttu-id="07f07-268">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample-Windows.cpp</span><span class="sxs-lookup"><span data-stu-id="07f07-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="07f07-269">C#</span><span class="sxs-lookup"><span data-stu-id="07f07-269">C#</span></span>       | <span data-ttu-id="07f07-270">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="07f07-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="07f07-271">Javascript</span><span class="sxs-lookup"><span data-stu-id="07f07-271">Javascript</span></span> | <span data-ttu-id="07f07-272">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="07f07-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="07f07-273">PowerShell</span><span class="sxs-lookup"><span data-stu-id="07f07-273">Powershell</span></span> | <span data-ttu-id="07f07-274">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="07f07-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="07f07-275">Bash</span><span class="sxs-lookup"><span data-stu-id="07f07-275">Bash</span></span>       | <span data-ttu-id="07f07-276">https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="07f07-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="07f07-277">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="07f07-277">FAQ</span></span>
1. <span data-ttu-id="07f07-278">Ik krijg Hallo fout `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="07f07-278">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="07f07-279">Wat betekent dit?</span><span class="sxs-lookup"><span data-stu-id="07f07-279">What does this mean?</span></span>
   * <span data-ttu-id="07f07-280">Hallo exemplaar metagegevens Service Hallo header vereist `Metadata: true` toobe doorgegeven in Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="07f07-280">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="07f07-281">Deze header doorgeven in een REST-aanroep hello, kunt access toohello exemplaar metagegevens Service.</span><span class="sxs-lookup"><span data-stu-id="07f07-281">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="07f07-282">Waarom niet krijg ik compute-informatie voor mijn VM?</span><span class="sxs-lookup"><span data-stu-id="07f07-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="07f07-283">Hallo exemplaar metagegevens Service ondersteunt momenteel alleen exemplaren gemaakt met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="07f07-283">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="07f07-284">In toekomstige hello, kunnen we ondersteuning voor virtuele machines van Cloud Service toevoegen.</span><span class="sxs-lookup"><span data-stu-id="07f07-284">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="07f07-285">Ik heb mijn virtuele Machine via Azure Resource Manager een tijd terug gemaakt.</span><span class="sxs-lookup"><span data-stu-id="07f07-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="07f07-286">Waarom kan ik geen Zie compute-metagegevens?</span><span class="sxs-lookup"><span data-stu-id="07f07-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="07f07-287">Voor alle virtuele machines na Sep 2016 is gemaakt, voegt u een [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart zien compute-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="07f07-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="07f07-288">Voor oudere virtuele machines (gemaakt vóór Sep-2016), software-extensies of gegevens schijven toohello VM toorefresh metagegevens.</span><span class="sxs-lookup"><span data-stu-id="07f07-288">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="07f07-289">Waarom krijg ik Hallo fout `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="07f07-289">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="07f07-290">Probeer uw aanvraag op basis van de exponentiële back uit het systeem.</span><span class="sxs-lookup"><span data-stu-id="07f07-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="07f07-291">Neem contact op met de ondersteuning van Azure als Hallo probleem zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="07f07-291">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="07f07-292">Waar kan ik aanvullende vragen/opmerkingen delen</span><span class="sxs-lookup"><span data-stu-id="07f07-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="07f07-293">Uw opmerkingen over http://feedback.azure.com verzenden.</span><span class="sxs-lookup"><span data-stu-id="07f07-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="07f07-294">Dit werkt voor virtuele Machine Scale ingesteld exemplaar, zou?</span><span class="sxs-lookup"><span data-stu-id="07f07-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="07f07-295">Ja is metagegevens-service beschikbaar voor Scale-exemplaren instellen.</span><span class="sxs-lookup"><span data-stu-id="07f07-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="07f07-296">Hoe krijg ik ondersteuning voor Hallo-service</span><span class="sxs-lookup"><span data-stu-id="07f07-296">How do I get support for hello service?</span></span>
   * <span data-ttu-id="07f07-297">tooget ondersteuning voor het Hallo-service een probleem maken in Azure portal voor Hallo VM waar u zich niet kunnen tooget metagegevens antwoord na lang pogingen</span><span class="sxs-lookup"><span data-stu-id="07f07-297">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Ondersteuning voor Instance Metagegevens](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="07f07-299">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07f07-299">Next steps</span></span>

- <span data-ttu-id="07f07-300">Meer informatie over Hallo [gepland gebeurtenissen](scheduled-events.md) API **openbare preview** geleverd door Hallo service-exemplaar metagegevens.</span><span class="sxs-lookup"><span data-stu-id="07f07-300">Learn more about hello [Scheduled Events](scheduled-events.md) API **in public preview** provided by hello Instance Metadata service.</span></span>
