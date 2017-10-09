---
title: aaaUsing PowerShell toomanage Traffic Manager in Azure | Microsoft Docs
description: Met behulp van PowerShell voor Traffic Manager met Azure Resource Manager
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a><span data-ttu-id="c6c32-103">Met behulp van PowerShell toomanage Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c6c32-103">Using PowerShell toomanage Traffic Manager</span></span>

<span data-ttu-id="c6c32-104">Azure Resource Manager is Hallo voorkeursbeheerpunten interface voor services in Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c32-104">Azure Resource Manager is hello preferred management interface for services in Azure.</span></span> <span data-ttu-id="c6c32-105">Azure Traffic Manager-profielen kunnen worden beheerd met Azure Resource Manager gebaseerde API's en hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="c6c32-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="c6c32-106">Resourcemodel</span><span class="sxs-lookup"><span data-stu-id="c6c32-106">Resource model</span></span>

<span data-ttu-id="c6c32-107">Azure Traffic Manager is geconfigureerd met behulp van een verzameling instellingen voor een Traffic Manager-profiel wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="c6c32-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="c6c32-108">Dit profiel bevat DNS-instellingen, instellingen voor verkeersroutering, eindpunt controle-instellingen en een lijst met de service-eindpunten toowhich verkeer wordt gerouteerd.</span><span class="sxs-lookup"><span data-stu-id="c6c32-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints toowhich traffic is routed.</span></span>

<span data-ttu-id="c6c32-109">Elke Traffic Manager-profiel wordt vertegenwoordigd door een resource van het type 'TrafficManagerProfiles'.</span><span class="sxs-lookup"><span data-stu-id="c6c32-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="c6c32-110">Op Hallo REST-API-niveau is Hallo URI voor elk profiel als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="c6c32-110">At hello REST API level, hello URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="c6c32-111">Instellen van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6c32-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="c6c32-112">Deze instructies Microsoft Azure PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c6c32-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="c6c32-113">Hallo volgende artikel wordt uitgelegd hoe tooinstall Azure PowerShell en configureren.</span><span class="sxs-lookup"><span data-stu-id="c6c32-113">hello following article explains how tooinstall and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="c6c32-114">Hoe tooinstall Azure PowerShell en configureren</span><span class="sxs-lookup"><span data-stu-id="c6c32-114">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="c6c32-115">Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u een bestaande resourcegroep hebt.</span><span class="sxs-lookup"><span data-stu-id="c6c32-115">hello examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="c6c32-116">U kunt een resourcegroep met behulp van de volgende opdracht Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="c6c32-116">You can create a resource group using hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="c6c32-117">Azure Resource Manager vereist dat alle resourcegroepen een locatie.</span><span class="sxs-lookup"><span data-stu-id="c6c32-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="c6c32-118">Deze locatie wordt gebruikt als Hallo standaard voor resources in die resourcegroep hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c6c32-118">This location is used as hello default for resources created in that resource group.</span></span> <span data-ttu-id="c6c32-119">Echter, aangezien Traffic Manager-profiel-resources globaal en niet regionaal zijn, Hallo keuze van de locatie voor resourcegroep heeft geen invloed op Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="c6c32-119">However, since Traffic Manager profile resources are global, not regional, hello choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="c6c32-120">Een Traffic Manager-profiel maken</span><span class="sxs-lookup"><span data-stu-id="c6c32-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="c6c32-121">toocreate Traffic Manager-profiel gebruiken Hallo `New-AzureRmTrafficManagerProfile` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c6c32-121">toocreate a Traffic Manager profile, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="c6c32-122">Hallo volgende tabel beschrijft Hallo parameters:</span><span class="sxs-lookup"><span data-stu-id="c6c32-122">hello following table describes hello parameters:</span></span>

| <span data-ttu-id="c6c32-123">Parameter</span><span class="sxs-lookup"><span data-stu-id="c6c32-123">Parameter</span></span> | <span data-ttu-id="c6c32-124">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c6c32-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6c32-125">Naam</span><span class="sxs-lookup"><span data-stu-id="c6c32-125">Name</span></span> |<span data-ttu-id="c6c32-126">Hallo-resourcenaam voor Hallo resource van Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-126">hello resource name for hello Traffic Manager profile resource.</span></span> <span data-ttu-id="c6c32-127">Profielen in Hallo dezelfde resourcegroep moet unieke namen hebben.</span><span class="sxs-lookup"><span data-stu-id="c6c32-127">Profiles in hello same resource group must have unique names.</span></span> <span data-ttu-id="c6c32-128">Deze naam is gescheiden van Hallo DNS-naam gebruikt voor DNS-query's.</span><span class="sxs-lookup"><span data-stu-id="c6c32-128">This name is separate from hello DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="c6c32-129">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="c6c32-129">ResourceGroupName</span></span> |<span data-ttu-id="c6c32-130">Hallo-naam van Hallo resource groep met Hallo profiel resource.</span><span class="sxs-lookup"><span data-stu-id="c6c32-130">hello name of hello resource group containing hello profile resource.</span></span> |
| <span data-ttu-id="c6c32-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="c6c32-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="c6c32-132">Hiermee geeft u Hallo verkeersroutering methode gebruikt toodetermine welk eindpunt wordt geretourneerd als antwoord een DNS-query.</span><span class="sxs-lookup"><span data-stu-id="c6c32-132">Specifies hello traffic-routing method used toodetermine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="c6c32-133">Mogelijke waarden zijn 'Prestaties', 'Gewogen' of 'Prioriteit'.</span><span class="sxs-lookup"><span data-stu-id="c6c32-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="c6c32-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="c6c32-134">RelativeDnsName</span></span> |<span data-ttu-id="c6c32-135">Hiermee geeft u een gedeelte van de Hallo hostname van Hallo DNS-naam op die door dit Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-135">Specifies hello hostname portion of hello DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="c6c32-136">Deze waarde wordt gecombineerd met Hallo DNS-naam die wordt gebruikt door Azure Traffic Manager tooform Hallo volledig gekwalificeerde domeinnaam (FQDN) van Hallo-profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-136">This value is combined with hello DNS domain name used by Azure Traffic Manager tooform hello fully qualified domain name (FQDN) of hello profile.</span></span> <span data-ttu-id="c6c32-137">Hallo-waarde van 'contoso' wordt bijvoorbeeld 'contoso.trafficmanager.net'.</span><span class="sxs-lookup"><span data-stu-id="c6c32-137">For example, setting hello value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="c6c32-138">TTL</span><span class="sxs-lookup"><span data-stu-id="c6c32-138">TTL</span></span> |<span data-ttu-id="c6c32-139">Hiermee geeft u Hallo DNS Time-to-Live (TTL), in seconden.</span><span class="sxs-lookup"><span data-stu-id="c6c32-139">Specifies hello DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="c6c32-140">Deze TTL informeert Hallo lokale DNS-resolvers en DNS-clients hoe lang toocache DNS-antwoorden voor dit Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-140">This TTL informs hello Local DNS resolvers and DNS clients how long toocache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="c6c32-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="c6c32-141">MonitorProtocol</span></span> |<span data-ttu-id="c6c32-142">Hiermee geeft u Hallo protocol toouse toomonitor eindpunt health.</span><span class="sxs-lookup"><span data-stu-id="c6c32-142">Specifies hello protocol toouse toomonitor endpoint health.</span></span> <span data-ttu-id="c6c32-143">Mogelijke waarden zijn 'HTTP' en 'HTTPS'.</span><span class="sxs-lookup"><span data-stu-id="c6c32-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="c6c32-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="c6c32-144">MonitorPort</span></span> |<span data-ttu-id="c6c32-145">Hiermee geeft u op Hallo TCP-poort gebruikt toomonitor eindpunt health.</span><span class="sxs-lookup"><span data-stu-id="c6c32-145">Specifies hello TCP port used toomonitor endpoint health.</span></span> |
| <span data-ttu-id="c6c32-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="c6c32-146">MonitorPath</span></span> |<span data-ttu-id="c6c32-147">Geeft aan Hallo pad relatief toohello endpoint-domeinnaam tooprobe voor eindpunt health gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c6c32-147">Specifies hello path relative toohello endpoint domain name used tooprobe for endpoint health.</span></span> |

<span data-ttu-id="c6c32-148">Hallo-cmdlet een Traffic Manager-profiel maakt in Azure en een bijbehorende profiel object tooPowerShell retourneert.</span><span class="sxs-lookup"><span data-stu-id="c6c32-148">hello cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object tooPowerShell.</span></span> <span data-ttu-id="c6c32-149">Hallo profiel bevat geen eindpunten op dit moment geen.</span><span class="sxs-lookup"><span data-stu-id="c6c32-149">At this point, hello profile does not contain any endpoints.</span></span> <span data-ttu-id="c6c32-150">Zie voor meer informatie over het toevoegen van eindpunten tooa Traffic Manager-profiel [Traffic Manager-eindpunten toe te voegen](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="c6c32-150">For more information about adding endpoints tooa Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="c6c32-151">Een Traffic Manager-profiel ophalen</span><span class="sxs-lookup"><span data-stu-id="c6c32-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="c6c32-152">een bestaand Traffic Manager-profiel te object tooretrieve gebruiken Hallo `Get-AzureRmTrafficManagerProfle` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c6c32-152">tooretrieve an existing Traffic Manager profile object, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="c6c32-153">Deze cmdlet retourneert het object van een Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="c6c32-154">Een Traffic Manager-profiel bijwerken</span><span class="sxs-lookup"><span data-stu-id="c6c32-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="c6c32-155">Wijzigen van Traffic Manager-profielen, volgt een 3-proces:</span><span class="sxs-lookup"><span data-stu-id="c6c32-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="c6c32-156">Met behulp ophalen Hallo profiel `Get-AzureRmTrafficManagerProfile` of gebruik Hallo profiel geretourneerd door `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="c6c32-156">Retrieve hello profile using `Get-AzureRmTrafficManagerProfile` or use hello profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="c6c32-157">Hallo-profiel wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c6c32-157">Modify hello profile.</span></span> <span data-ttu-id="c6c32-158">U kunt toevoegen en verwijderen van eindpunten of wijzigt u de parameters voor het eindpunt of profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="c6c32-159">Deze wijzigingen zijn offline bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="c6c32-159">These changes are off-line operations.</span></span> <span data-ttu-id="c6c32-160">Wijzigt u alleen lokale Hallo-object in het geheugen dat Hallo profiel vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="c6c32-160">You are only changing hello local object in memory that represents hello profile.</span></span>
3. <span data-ttu-id="c6c32-161">Uw wijzigingen met behulp van Hallo `Set-AzureRmTrafficManagerProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c6c32-161">Commit your changes using hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="c6c32-162">Alle eigenschappen van het profiel kunnen worden gewijzigd, met uitzondering van het profiel Hallo RelativeDnsName.</span><span class="sxs-lookup"><span data-stu-id="c6c32-162">All profile properties can be changed except hello profile's RelativeDnsName.</span></span> <span data-ttu-id="c6c32-163">toochange Hallo RelativeDnsName, verwijdert u profiel en een nieuw profiel met een nieuwe naam.</span><span class="sxs-lookup"><span data-stu-id="c6c32-163">toochange hello RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="c6c32-164">Hallo volgende voorbeeld laat zien hoe toochange Hallo TTL van profiel:</span><span class="sxs-lookup"><span data-stu-id="c6c32-164">hello following example demonstrates how toochange hello profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="c6c32-165">Er zijn drie soorten Traffic Manager-eindpunten:</span><span class="sxs-lookup"><span data-stu-id="c6c32-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="c6c32-166">**Azure-eindpunten** zijn services die worden gehost in Azure</span><span class="sxs-lookup"><span data-stu-id="c6c32-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="c6c32-167">**Externe eindpunten** worden services die buiten Azure worden gehost</span><span class="sxs-lookup"><span data-stu-id="c6c32-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="c6c32-168">**Genest eindpunten** gebruikte tooconstruct genest hiërarchieën van Traffic Manager-profielen.</span><span class="sxs-lookup"><span data-stu-id="c6c32-168">**Nested endpoints** are used tooconstruct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="c6c32-169">Geneste eindpunten inschakelen geavanceerde verkeersroutering configuraties voor complexe toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c6c32-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="c6c32-170">In alle drie gevallen kunnen eindpunten worden toegevoegd op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="c6c32-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="c6c32-171">Met behulp van een proces 3-stappen die hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="c6c32-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="c6c32-172">Hallo voordeel van deze methode is dat enkele eindpunt kan worden gewijzigd in één update.</span><span class="sxs-lookup"><span data-stu-id="c6c32-172">hello advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="c6c32-173">Hallo nieuw AzureRmTrafficManagerEndpoint cmdlet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c6c32-173">Using hello New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="c6c32-174">Deze cmdlet voegt een eindpunt tooan bestaand Traffic Manager-profiel in één bewerking.</span><span class="sxs-lookup"><span data-stu-id="c6c32-174">This cmdlet adds an endpoint tooan existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="c6c32-175">Azure-eindpunten toevoegen</span><span class="sxs-lookup"><span data-stu-id="c6c32-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="c6c32-176">Azure-eindpunten verwijzen naar services die worden gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c32-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="c6c32-177">Twee soorten Azure-eindpunten worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="c6c32-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="c6c32-178">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="c6c32-178">Azure Web Apps</span></span>
2. <span data-ttu-id="c6c32-179">Azure PublicIpAddress-resources (die kunnen worden aangesloten tooa load balancer of een virtuele machine NIC).</span><span class="sxs-lookup"><span data-stu-id="c6c32-179">Azure PublicIpAddress resources (which can be attached tooa load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="c6c32-180">Hallo PublicIpAddress moet een DNS-naam toegewezen toobe gebruikt in Traffic Manager hebben.</span><span class="sxs-lookup"><span data-stu-id="c6c32-180">hello PublicIpAddress must have a DNS name assigned toobe used in Traffic Manager.</span></span>

<span data-ttu-id="c6c32-181">In elk geval:</span><span class="sxs-lookup"><span data-stu-id="c6c32-181">In each case:</span></span>

* <span data-ttu-id="c6c32-182">Hallo-service is opgegeven met de parameter 'targetResourceId' Hallo van `Add-AzureRmTrafficManagerEndpointConfig` of `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="c6c32-182">hello service is specified using hello 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="c6c32-183">Hallo 'Target' en 'EndpointLocation' zijn impliciete door Hallo TargetResourceId.</span><span class="sxs-lookup"><span data-stu-id="c6c32-183">hello 'Target' and 'EndpointLocation' are implied by hello TargetResourceId.</span></span>
* <span data-ttu-id="c6c32-184">Hallo opgeven is 'Gewicht' optioneel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-184">Specifying hello 'Weight' is optional.</span></span> <span data-ttu-id="c6c32-185">Gewicht worden alleen gebruikt als Hallo profiel geconfigureerde toouse Hallo 'Gewogen' verkeersroutering methode.</span><span class="sxs-lookup"><span data-stu-id="c6c32-185">Weights are only used if hello profile is configured toouse hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="c6c32-186">Anders worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="c6c32-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="c6c32-187">Indien opgegeven, is het Hallo-waarde moet een getal tussen 1 en 1000.</span><span class="sxs-lookup"><span data-stu-id="c6c32-187">If specified, hello value must be a number between 1 and 1000.</span></span> <span data-ttu-id="c6c32-188">Hallo-standaardwaarde is '1'.</span><span class="sxs-lookup"><span data-stu-id="c6c32-188">hello default value is '1'.</span></span>
* <span data-ttu-id="c6c32-189">Het opgeven van Hallo 'Prioriteit' is optioneel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-189">Specifying hello 'Priority' is optional.</span></span> <span data-ttu-id="c6c32-190">Prioriteiten worden alleen gebruikt als Hallo profiel geconfigureerde toouse Hallo 'Prioriteit' verkeersroutering methode.</span><span class="sxs-lookup"><span data-stu-id="c6c32-190">Priorities are only used if hello profile is configured toouse hello 'Priority' traffic-routing method.</span></span> <span data-ttu-id="c6c32-191">Anders worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="c6c32-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="c6c32-192">Geldige waarden liggen tussen 1 too1000 met lagere waarden die wijzen op een hogere prioriteit.</span><span class="sxs-lookup"><span data-stu-id="c6c32-192">Valid values are from 1 too1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="c6c32-193">Als voor één eindpunt opgegeven, moeten ze worden opgegeven voor alle eindpunten.</span><span class="sxs-lookup"><span data-stu-id="c6c32-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="c6c32-194">Als u dit weglaat, wordt standaardwaarden vanaf '1' worden toegepast in Hallo volgorde worden Hallo-eindpunten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c6c32-194">If omitted, default values starting from '1' are applied in hello order that hello endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="c6c32-195">Voorbeeld 1: Toe te voegen met behulp van Web-App-eindpunten`Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="c6c32-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="c6c32-196">In dit voorbeeld wordt een Traffic Manager-profiel maken en toevoegen van eindpunten van Web-App, met behulp van Hallo `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c6c32-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="c6c32-197">Voorbeeld 2: Toevoegen van een publicIpAddress-eindpunt met`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="c6c32-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="c6c32-198">In dit voorbeeld wordt een openbare IP-adres resource toohello Traffic Manager-profiel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c6c32-198">In this example, a public IP address resource is added toohello Traffic Manager profile.</span></span> <span data-ttu-id="c6c32-199">Hallo openbaar IP-adres moet een DNS-naam zijn geconfigureerd, en kan worden beide toohello NIC van een virtuele machine of tooa load balancer is gebonden.</span><span class="sxs-lookup"><span data-stu-id="c6c32-199">hello public IP address must have a DNS name configured, and can be bound either toohello NIC of a VM or tooa load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="c6c32-200">Externe eindpunten toevoegen</span><span class="sxs-lookup"><span data-stu-id="c6c32-200">Adding External Endpoints</span></span>

<span data-ttu-id="c6c32-201">Traffic Manager maakt gebruik van externe eindpunten toodirect verkeer tooservices buiten Azure worden gehost.</span><span class="sxs-lookup"><span data-stu-id="c6c32-201">Traffic Manager uses external endpoints toodirect traffic tooservices hosted outside of Azure.</span></span> <span data-ttu-id="c6c32-202">Als u met Azure-eindpunten, externe eindpunten kunnen worden toegevoegd, met behulp van `Add-AzureRmTrafficManagerEndpointConfig` gevolgd door `Set-AzureRmTrafficManagerProfile`, of `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="c6c32-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="c6c32-203">Wanneer u externe eindpunten opgeeft:</span><span class="sxs-lookup"><span data-stu-id="c6c32-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="c6c32-204">Hallo eindpunt domeinnaam moet worden opgegeven met de parameter 'Target' Hallo</span><span class="sxs-lookup"><span data-stu-id="c6c32-204">hello endpoint domain name must be specified using hello 'Target' parameter</span></span>
* <span data-ttu-id="c6c32-205">Als Hallo 'Prestaties' verkeersroutering methode wordt gebruikt, is 'EndpointLocation' hello vereist.</span><span class="sxs-lookup"><span data-stu-id="c6c32-205">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="c6c32-206">Anders is optioneel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-206">Otherwise it is optional.</span></span> <span data-ttu-id="c6c32-207">Hallo-waarde moet een [geldig Azure-regionaam](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="c6c32-207">hello value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="c6c32-208">Hallo 'Gewicht' en 'Prioriteit' zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-208">hello 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="c6c32-209">Voorbeeld 1: Externe eindpunten met toevoegen `Add-AzureRmTrafficManagerEndpointConfig` en`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="c6c32-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="c6c32-210">In dit voorbeeld wordt een Traffic Manager-profiel maken, twee externe eindpunten toevoegen en Hallo wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="c6c32-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit hello changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="c6c32-211">Voorbeeld 2: Externe eindpunten met toevoegen`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="c6c32-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="c6c32-212">In dit voorbeeld voegen we een bestaand profiel voor externe eindpunt tooan.</span><span class="sxs-lookup"><span data-stu-id="c6c32-212">In this example, we add an external endpoint tooan existing profile.</span></span> <span data-ttu-id="c6c32-213">Hallo-profiel is opgegeven met behulp van namen Hallo profiel en de resource.</span><span class="sxs-lookup"><span data-stu-id="c6c32-213">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="c6c32-214">'Nested' eindpunten toevoegen</span><span class="sxs-lookup"><span data-stu-id="c6c32-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="c6c32-215">Elke Traffic Manager-profiel geeft één verkeersroutering methode.</span><span class="sxs-lookup"><span data-stu-id="c6c32-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="c6c32-216">Er zijn echter scenario's waarvoor meer geavanceerde voor verkeersroutering dan Hallo routering geleverd door een enkele Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-216">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="c6c32-217">U kunt het Traffic Manager profielen toocombine Hallo voordelen van meer dan één methode voor verkeersroutering nesten.</span><span class="sxs-lookup"><span data-stu-id="c6c32-217">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="c6c32-218">Geneste profielen kunnen u toooverride Hallo standaard Traffic Manager gedrag toosupport grotere en complexere implementaties van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c6c32-218">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span> <span data-ttu-id="c6c32-219">Zie voor meer voorbeelden, [genest Traffic Manager-profielen](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="c6c32-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="c6c32-220">Geneste eindpunten zijn geconfigureerd op Hallo bovenliggende profiel met een specifieke eindpunt-type 'NestedEndpoints'.</span><span class="sxs-lookup"><span data-stu-id="c6c32-220">Nested endpoints are configured at hello parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="c6c32-221">Bij het opgeven van geneste eindpunten:</span><span class="sxs-lookup"><span data-stu-id="c6c32-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="c6c32-222">Hallo-eindpunt moet worden opgegeven met de parameter 'targetResourceId' Hallo</span><span class="sxs-lookup"><span data-stu-id="c6c32-222">hello endpoint must be specified using hello 'targetResourceId' parameter</span></span>
* <span data-ttu-id="c6c32-223">Als Hallo 'Prestaties' verkeersroutering methode wordt gebruikt, is 'EndpointLocation' hello vereist.</span><span class="sxs-lookup"><span data-stu-id="c6c32-223">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="c6c32-224">Anders is optioneel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-224">Otherwise it is optional.</span></span> <span data-ttu-id="c6c32-225">Hallo-waarde moet een [geldig Azure-regionaam](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="c6c32-225">hello value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="c6c32-226">Hallo 'Gewicht' en 'Prioriteit' zijn optioneel, als voor de Azure-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="c6c32-226">hello 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="c6c32-227">Hallo 'MinChildEndpoints'-parameter is optioneel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-227">hello 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="c6c32-228">Hallo-standaardwaarde is '1'.</span><span class="sxs-lookup"><span data-stu-id="c6c32-228">hello default value is '1'.</span></span> <span data-ttu-id="c6c32-229">Als het aantal beschikbare eindpunten Hallo kleiner is dan deze drempelwaarde, beschouwt Hallo bovenliggende profiel Hallo onderliggende profiel 'Gedegradeerd' en verkeer toohello andere eindpunten in Hallo bovenliggende profiel zorgt.</span><span class="sxs-lookup"><span data-stu-id="c6c32-229">If hello number of available endpoints falls below this threshold, hello parent profile considers hello child profile 'degraded' and diverts traffic toohello other endpoints in hello parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="c6c32-230">Voorbeeld 1: Toe te voegen geneste eindpunten met `Add-AzureRmTrafficManagerEndpointConfig` en`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="c6c32-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="c6c32-231">In dit voorbeeld we nieuwe Traffic Manager onderliggende en bovenliggende profielen maken, Hallo onderliggende toevoegen als een geneste eindpunt toohello bovenliggende en Hallo wijzigingen doorvoeren.</span><span class="sxs-lookup"><span data-stu-id="c6c32-231">In this example, we create new Traffic Manager child and parent profiles, add hello child as a nested endpoint toohello parent, and commit hello changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="c6c32-232">Voor beknopt alternatief bevat in dit voorbeeld heeft we andere eindpunten toohello onderliggende of bovenliggende profielen niet toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c6c32-232">For brevity in this example, we did not add any other endpoints toohello child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="c6c32-233">Voorbeeld 2: Geneste eindpunten toevoegen`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="c6c32-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="c6c32-234">In dit voorbeeld toevoegen we een bestaand profiel van de onderliggende als een geneste eindpunt tooan bestaande bovenliggende profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-234">In this example, we add an existing child profile as a nested endpoint tooan existing parent profile.</span></span> <span data-ttu-id="c6c32-235">Hallo-profiel is opgegeven met behulp van namen Hallo profiel en de resource.</span><span class="sxs-lookup"><span data-stu-id="c6c32-235">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="c6c32-236">Bijwerken van een Traffic Manager-eindpunt</span><span class="sxs-lookup"><span data-stu-id="c6c32-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="c6c32-237">Er zijn twee manieren tooupdate een bestaand Traffic Manager-eindpunt:</span><span class="sxs-lookup"><span data-stu-id="c6c32-237">There are two ways tooupdate an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="c6c32-238">Ophalen met behulp Hallo Traffic Manager profiel `Get-AzureRmTrafficManagerProfile`Hallo eindpunt eigenschappen binnen Hallo profiel bijwerken en Hallo wijzigingen met behulp van `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="c6c32-238">Get hello Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update hello endpoint properties within hello profile, and commit hello changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="c6c32-239">Deze methode heeft Hallo voordeel kunnen tooupdate wordt meer dan één eindpunt in één bewerking.</span><span class="sxs-lookup"><span data-stu-id="c6c32-239">This method has hello advantage of being able tooupdate more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="c6c32-240">Hallo Traffic Manager-eindpunt met behulp ophalen `Get-AzureRmTrafficManagerEndpoint`Hallo eindpunt eigenschappen bijwerken en Hallo wijzigingen met behulp van `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="c6c32-240">Get hello Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update hello endpoint properties, and commit hello changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="c6c32-241">Deze methode is eenvoudiger, aangezien hoeven niet te indexeren bij Hallo eindpunten matrix in Hallo-profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-241">This method is simpler, since it does not require indexing into hello Endpoints array in hello profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="c6c32-242">Voorbeeld 1: Bijwerken met behulp van eindpunten `Get-AzureRmTrafficManagerProfile` en`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="c6c32-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="c6c32-243">In dit voorbeeld wijzigen we Hallo-prioriteit op twee eindpunten in een bestaand profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-243">In this example, we modify hello priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="c6c32-244">Voorbeeld 2: Bijwerken van een eindpunt met `Get-AzureRmTrafficManagerEndpoint` en`Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="c6c32-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="c6c32-245">In dit voorbeeld wijzigen we Hallo gewicht van één eindpunt in een bestaand profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-245">In this example, we modify hello weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="c6c32-246">Eindpunten en -profielen inschakelen en uitschakelen</span><span class="sxs-lookup"><span data-stu-id="c6c32-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="c6c32-247">Traffic Manager kunt afzonderlijke eindpunten toobe ingeschakelde en uitgeschakelde, evenals inschakelen en uitschakelen van volledige profielen toestaan.</span><span class="sxs-lookup"><span data-stu-id="c6c32-247">Traffic Manager allows individual endpoints toobe enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="c6c32-248">Deze wijzigingen kunnen worden aangebracht door ophalen/bijwerken/instelling Hallo eindpunt of profiel resources.</span><span class="sxs-lookup"><span data-stu-id="c6c32-248">These changes can be made by getting/updating/setting hello endpoint or profile resources.</span></span> <span data-ttu-id="c6c32-249">toostreamline deze algemene bewerkingen worden ook ondersteund via exclusieve cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c6c32-249">toostreamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="c6c32-250">Voorbeeld 1: Inschakelen en uitschakelen van een Traffic Manager-profiel</span><span class="sxs-lookup"><span data-stu-id="c6c32-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="c6c32-251">tooenable Traffic Manager-profiel gebruiken `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="c6c32-251">tooenable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="c6c32-252">Hallo-profiel kan worden opgegeven met behulp van een object van een profiel.</span><span class="sxs-lookup"><span data-stu-id="c6c32-252">hello profile can be specified using a profile object.</span></span> <span data-ttu-id="c6c32-253">Hallo profile-object kan worden doorgegeven via de pijplijn Hallo of met behulp van Hallo '-TrafficManagerProfile' parameter.</span><span class="sxs-lookup"><span data-stu-id="c6c32-253">hello profile object can be passed via hello pipeline or by using hello '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="c6c32-254">In dit voorbeeld geeft we Hallo profiel door Hallo profiel en resource groepsnaam.</span><span class="sxs-lookup"><span data-stu-id="c6c32-254">In this example, we specify hello profile by hello profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="c6c32-255">toodisable een Traffic Manager-profiel:</span><span class="sxs-lookup"><span data-stu-id="c6c32-255">toodisable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="c6c32-256">Hallo uitschakelen AzureRmTrafficManagerProfile cmdlet vraagt om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="c6c32-256">hello Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="c6c32-257">Dit bericht kan worden onderdrukt met Hallo '-Force' parameter.</span><span class="sxs-lookup"><span data-stu-id="c6c32-257">This prompt can be suppressed using hello '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="c6c32-258">Voorbeeld 2: Inschakelen en uitschakelen van een Traffic Manager-eindpunt</span><span class="sxs-lookup"><span data-stu-id="c6c32-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="c6c32-259">tooenable Traffic Manager-eindpunt gebruik `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="c6c32-259">tooenable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="c6c32-260">Er zijn twee manieren toospecify Hallo-eindpunt</span><span class="sxs-lookup"><span data-stu-id="c6c32-260">There are two ways toospecify hello endpoint</span></span>

1. <span data-ttu-id="c6c32-261">Met behulp van een TrafficManagerEndpoint-object doorgegeven via de pijplijn Hallo of via Hallo '-TrafficManagerEndpoint' parameter</span><span class="sxs-lookup"><span data-stu-id="c6c32-261">Using a TrafficManagerEndpoint object passed via hello pipeline or using hello '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="c6c32-262">Met behulp van eindpuntnaam hello, eindpunttype profielnaam en de naam van resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="c6c32-262">Using hello endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="c6c32-263">Op deze manier toodisable een Traffic Manager-eindpunt:</span><span class="sxs-lookup"><span data-stu-id="c6c32-263">Similarly, toodisable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="c6c32-264">Net als bij `Disable-AzureRmTrafficManagerProfile`, Hallo `Disable-AzureRmTrafficManagerEndpoint` cmdlet vraagt om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="c6c32-264">As with `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="c6c32-265">Dit bericht kan worden onderdrukt met Hallo '-Force' parameter.</span><span class="sxs-lookup"><span data-stu-id="c6c32-265">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="c6c32-266">Een Traffic Manager-eindpunt verwijderen</span><span class="sxs-lookup"><span data-stu-id="c6c32-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="c6c32-267">tooremove afzonderlijke eindpunten, gebruik Hallo `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c6c32-267">tooremove individual endpoints, use hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="c6c32-268">Deze cmdlet vraagt om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="c6c32-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="c6c32-269">Dit bericht kan worden onderdrukt met Hallo '-Force' parameter.</span><span class="sxs-lookup"><span data-stu-id="c6c32-269">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="c6c32-270">Een Traffic Manager-profiel verwijderen</span><span class="sxs-lookup"><span data-stu-id="c6c32-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="c6c32-271">toodelete Traffic Manager-profiel gebruiken Hallo `Remove-AzureRmTrafficManagerProfile` geven namen Hallo profiel en de resource-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c6c32-271">toodelete a Traffic Manager profile, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying hello profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="c6c32-272">Deze cmdlet vraagt om bevestiging.</span><span class="sxs-lookup"><span data-stu-id="c6c32-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="c6c32-273">Dit bericht kan worden onderdrukt met Hallo '-Force' parameter.</span><span class="sxs-lookup"><span data-stu-id="c6c32-273">This prompt can be suppressed using hello '-Force' parameter.</span></span>

<span data-ttu-id="c6c32-274">Hallo profiel toobe verwijderd kan ook worden opgegeven met behulp van een object van een profiel:</span><span class="sxs-lookup"><span data-stu-id="c6c32-274">hello profile toobe deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="c6c32-275">Deze reeks kan ook worden doorgesluisd:</span><span class="sxs-lookup"><span data-stu-id="c6c32-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="c6c32-276">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c6c32-276">Next steps</span></span>

[<span data-ttu-id="c6c32-277">Traffic Manager-controle</span><span class="sxs-lookup"><span data-stu-id="c6c32-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="c6c32-278">Prestatieoverwegingen voor Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c6c32-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
