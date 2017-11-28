---
title: aaaConvert toomicroservices voor Azure Cloud Services-apps | Microsoft Docs
description: Deze handleiding vergelijkt Cloud Services-webserver en werkrollen en Service Fabric stateless services toohelp migreren van Cloudservices tooService Fabric.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a><span data-ttu-id="b6a5d-103">Handleiding voor tooconverting Web- en werkrollen tooService Fabric stateless services</span><span class="sxs-lookup"><span data-stu-id="b6a5d-103">Guide tooconverting Web and Worker Roles tooService Fabric stateless services</span></span>
<span data-ttu-id="b6a5d-104">Dit artikel wordt beschreven hoe toomigrate uw Cloud Services-Web- en werkrollen tooService Fabric stateless services.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-104">This article describes how toomigrate your Cloud Services Web and Worker Roles tooService Fabric stateless services.</span></span> <span data-ttu-id="b6a5d-105">Dit is de eenvoudigste migratiepad Hallo van Cloudservices tooService Fabric voor toepassingen waarvan de algehele architectuur toostay ongeveer gaat Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-105">This is hello simplest migration path from Cloud Services tooService Fabric for applications whose overall architecture is going toostay roughly hello same.</span></span>

## <a name="cloud-service-project-tooservice-fabric-application-project"></a><span data-ttu-id="b6a5d-106">Service-project tooService Fabric-toepassingsproject cloud</span><span class="sxs-lookup"><span data-stu-id="b6a5d-106">Cloud Service project tooService Fabric application project</span></span>
 <span data-ttu-id="b6a5d-107">Een Cloud Service-project en een Service Fabric-toepassing-project hebt een vergelijkbare structuur en beide vertegenwoordigen Hallo implementatie-eenheid voor uw toepassing - dat wil zeggen, ze elk voltooid Hallo-pakket dat geïmplementeerde toorun uw toepassing definiëren.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent hello deployment unit for your application - that is, they each define hello complete package that is deployed toorun your application.</span></span> <span data-ttu-id="b6a5d-108">Een Cloud Service-project bevat een of meer Web- of werkrollen.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="b6a5d-109">Een Service Fabric-toepassing-project bevat ook een of meer services.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="b6a5d-110">Hallo-verschil is dat Hallo Cloudservice project paren Hallo toepassingsimplementatie met een VM-implementatie en dus bevat VM-configuratie-instellingen in dit terwijl Hallo Service Fabric-toepassing project alleen definieert een toepassing die wordt geïmplementeerd tooa set bestaande virtuele machines in een Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-110">hello difference is that hello Cloud Service project couples hello application deployment with a VM deployment and thus contains VM configuration settings in it, whereas hello Service Fabric Application project only defines an application that will be deployed tooa set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="b6a5d-111">Hallo Service Fabric-cluster zelf wordt alleen geïmplementeerd als via een Resource Manager-sjabloon of via hello Azure-portal en meerdere Service Fabric-toepassingen zijn tooit geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-111">hello Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through hello Azure portal, and multiple Service Fabric applications can be deployed tooit.</span></span>

![Vergelijking van service Fabric en Cloud Services-project][3]

## <a name="worker-role-toostateless-service"></a><span data-ttu-id="b6a5d-113">De functieservice toostateless worker</span><span class="sxs-lookup"><span data-stu-id="b6a5d-113">Worker Role toostateless service</span></span>
<span data-ttu-id="b6a5d-114">Conceptueel gezien vertegenwoordigt een Werkrol een staatloze werkbelasting, wat betekent dat elke instantie van Hallo werkbelasting is identiek zijn en kunnen aanvragen gerouteerde tooany exemplaar op elk gewenst moment worden.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of hello workload is identical and requests can be routed tooany instance at any time.</span></span> <span data-ttu-id="b6a5d-115">Elk exemplaar is niet verwachte tooremember Hallo vorige aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-115">Each instance is not expected tooremember hello previous request.</span></span> <span data-ttu-id="b6a5d-116">Status van de werkbelasting Hallo werkt op wordt beheerd door een externe Statusopslag, zoals Azure Table Storage of Azure Documentdb.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-116">State that hello workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="b6a5d-117">Dit soort werkbelasting is in Service Fabric vertegenwoordigd door een Stateless Service.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="b6a5d-118">Hallo eenvoudigste methode toomigrating een Werkrol tooService Fabric kan worden gedaan door de Werkrol code tooa staatloze Service converteren.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-118">hello simplest approach toomigrating a Worker Role tooService Fabric can be done by converting Worker Role code tooa Stateless Service.</span></span>

![Worker-rol tooStateless Service][4]

## <a name="web-role-toostateless-service"></a><span data-ttu-id="b6a5d-120">De functieservice toostateless Web</span><span class="sxs-lookup"><span data-stu-id="b6a5d-120">Web Role toostateless service</span></span>
<span data-ttu-id="b6a5d-121">Vergelijkbare tooWorker rol een Webrol ook vertegenwoordigt een staatloze werkbelasting, en zo in dat geval het te kan worden toegewezen tooa staatloze Service Fabric-service.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-121">Similar tooWorker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped tooa Service Fabric stateless service.</span></span> <span data-ttu-id="b6a5d-122">Echter, in tegenstelling tot webrollen, Service Fabric ondersteunt geen IIS.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="b6a5d-123">toomigrate een webtoepassing van een Webrol tooa staatloze service vereist eerste verplaatsen tooa webframework die automatisch kan worden gehost en is niet afhankelijk van IIS of System.Web, zoals ASP.NET Core 1.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-123">toomigrate a web application from a Web Role tooa stateless service requires first moving tooa web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="b6a5d-124">**Toepassing**</span><span class="sxs-lookup"><span data-stu-id="b6a5d-124">**Application**</span></span> | <span data-ttu-id="b6a5d-125">**Ondersteund**</span><span class="sxs-lookup"><span data-stu-id="b6a5d-125">**Supported**</span></span> | <span data-ttu-id="b6a5d-126">**Migratiepad**</span><span class="sxs-lookup"><span data-stu-id="b6a5d-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6a5d-127">ASP.NET-webformulieren</span><span class="sxs-lookup"><span data-stu-id="b6a5d-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="b6a5d-128">Nee</span><span class="sxs-lookup"><span data-stu-id="b6a5d-128">No</span></span> |<span data-ttu-id="b6a5d-129">Converteren tooASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="b6a5d-129">Convert tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="b6a5d-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="b6a5d-130">ASP.NET MVC</span></span> |<span data-ttu-id="b6a5d-131">Met migratie</span><span class="sxs-lookup"><span data-stu-id="b6a5d-131">With Migration</span></span> |<span data-ttu-id="b6a5d-132">Upgrade tooASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="b6a5d-132">Upgrade tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="b6a5d-133">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="b6a5d-133">ASP.NET Web API</span></span> |<span data-ttu-id="b6a5d-134">Met migratie</span><span class="sxs-lookup"><span data-stu-id="b6a5d-134">With Migration</span></span> |<span data-ttu-id="b6a5d-135">Automatische gehoste-server of ASP.NET Core 1 gebruiken</span><span class="sxs-lookup"><span data-stu-id="b6a5d-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="b6a5d-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="b6a5d-136">ASP.NET Core 1</span></span> |<span data-ttu-id="b6a5d-137">Ja</span><span class="sxs-lookup"><span data-stu-id="b6a5d-137">Yes</span></span> |<span data-ttu-id="b6a5d-138">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="b6a5d-139">Vermelding punt API en de levenscyclus</span><span class="sxs-lookup"><span data-stu-id="b6a5d-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="b6a5d-140">Werkrol en Service Fabric-service-API's bieden vergelijkbare toegangspunten:</span><span class="sxs-lookup"><span data-stu-id="b6a5d-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="b6a5d-141">**Toegangspunt**</span><span class="sxs-lookup"><span data-stu-id="b6a5d-141">**Entry Point**</span></span> | <span data-ttu-id="b6a5d-142">**Werkrol**</span><span class="sxs-lookup"><span data-stu-id="b6a5d-142">**Worker Role**</span></span> | <span data-ttu-id="b6a5d-143">**Service Fabric-service**</span><span class="sxs-lookup"><span data-stu-id="b6a5d-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6a5d-144">Verwerking</span><span class="sxs-lookup"><span data-stu-id="b6a5d-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="b6a5d-145">VM starten</span><span class="sxs-lookup"><span data-stu-id="b6a5d-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="b6a5d-146">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-146">N/A</span></span> |
| <span data-ttu-id="b6a5d-147">VM stoppen</span><span class="sxs-lookup"><span data-stu-id="b6a5d-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="b6a5d-148">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-148">N/A</span></span> |
| <span data-ttu-id="b6a5d-149">Open listener voor aanvragen van clients</span><span class="sxs-lookup"><span data-stu-id="b6a5d-149">Open listener for client requests</span></span> |<span data-ttu-id="b6a5d-150">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-150">N/A</span></span> |<ul><li> <span data-ttu-id="b6a5d-151">`CreateServiceInstanceListener()`voor stateless</span><span class="sxs-lookup"><span data-stu-id="b6a5d-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="b6a5d-152">`CreateServiceReplicaListener()`voor stateful</span><span class="sxs-lookup"><span data-stu-id="b6a5d-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="b6a5d-153">Werkrol</span><span class="sxs-lookup"><span data-stu-id="b6a5d-153">Worker Role</span></span>
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="b6a5d-154">Staatloze service Fabric-Service</span><span class="sxs-lookup"><span data-stu-id="b6a5d-154">Service Fabric Stateless Service</span></span>
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

<span data-ttu-id="b6a5d-155">Een onderdrukking primaire 'uitvoeren' hebben beide in welke toobegin-verwerking.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-155">Both have a primary "Run" override in which toobegin processing.</span></span> <span data-ttu-id="b6a5d-156">Service Fabric-services combineren `Run`, `Start`, en `Stop` in een enkel toegangspunt `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="b6a5d-157">De service moet beginnen met werken wanneer `RunAsync` wordt gestart en mag niet meer werken wanneer hello `RunAsync` van de methode CancellationToken ontvangt een signaal.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-157">Your service should begin working when `RunAsync` starts, and should stop working when hello `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="b6a5d-158">Er zijn enkele belangrijke verschillen tussen Hallo lifecycle en levensduur van Service Fabric- en werkrollen services:</span><span class="sxs-lookup"><span data-stu-id="b6a5d-158">There are several key differences between hello lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="b6a5d-159">**Levenscyclus:** Hallo grootste verschil is dat een Werkrol een virtuele machine is en dus de levenscyclus gebonden toohello VM, waaronder gebeurtenissen voor wanneer Hallo VM wordt gestart en gestopt.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-159">**Lifecycle:** hello biggest difference is that a Worker Role is a VM and so its lifecycle is tied toohello VM, which includes events for when hello VM starts and stops.</span></span> <span data-ttu-id="b6a5d-160">Een Service Fabric-service heeft een levenscyclus dat is gescheiden van Hallo VM levensduur, zodat deze bevat geen gebeurtenissen voor als Hallo host, VM of machine wordt gestart en gestopt, omdat ze niet zijn gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-160">A Service Fabric service has a lifecycle that is separate from hello VM lifecycle, so it does not include events for when hello host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="b6a5d-161">**Levensduur:** een Werkrol-exemplaar wordt gerecycled als hello `Run` methode afgesloten.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-161">**Lifetime:** A Worker Role instance will recycle if hello `Run` method exits.</span></span> <span data-ttu-id="b6a5d-162">Hallo `RunAsync` methode in een Service Fabric-service evenwel toocompletion kunt uitvoeren en service-exemplaar Hallo blijven.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-162">hello `RunAsync` method in a Service Fabric service however can run toocompletion and hello service instance will stay up.</span></span> 

<span data-ttu-id="b6a5d-163">Service Fabric bevat een toegangspunt optionele communicatie-instellingen voor services die naar aanvragen van clients luisteren.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="b6a5d-164">Zowel Hallo RunAsync en communicatie toegangspunt zijn optionele onderdrukkingen in Service Fabric-services - uw service kan kiezen tooonly listen tooclient aanvragen of een lus verwerking of beide alleen worden uitgevoerd - dat is waarom Hallo RunAsync-methode tooexit zonder is toegestaan opnieuw starten van Hallo service-exemplaar, omdat deze toolisten voor clientaanvragen blijven mogelijk.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-164">Both hello RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose tooonly listen tooclient requests, or only run a processing loop, or both - which is why hello RunAsync method is allowed tooexit without restarting hello service instance, because it may continue toolisten for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="b6a5d-165">Application-API en de omgeving</span><span class="sxs-lookup"><span data-stu-id="b6a5d-165">Application API and environment</span></span>
<span data-ttu-id="b6a5d-166">Hallo Cloud Services-omgeving API biedt informatie en -functionaliteit voor de huidige VM-instantie hello, evenals informatie over andere VM-rolexemplaren.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-166">hello Cloud Services environment API provides information and functionality for hello current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="b6a5d-167">Service Fabric bevat informatie over de runtime tooits en enige informatie over het Hallo-knooppunt een service die momenteel wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-167">Service Fabric provides information related tooits runtime and some information about hello node a service is currently running on.</span></span> 

| <span data-ttu-id="b6a5d-168">**Taak omgeving**</span><span class="sxs-lookup"><span data-stu-id="b6a5d-168">**Environment Task**</span></span> | <span data-ttu-id="b6a5d-169">**Cloud Services**</span><span class="sxs-lookup"><span data-stu-id="b6a5d-169">**Cloud Services**</span></span> | <span data-ttu-id="b6a5d-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="b6a5d-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6a5d-171">Configuratie-instellingen en Wijzigingsmelding</span><span class="sxs-lookup"><span data-stu-id="b6a5d-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="b6a5d-172">Lokale opslag</span><span class="sxs-lookup"><span data-stu-id="b6a5d-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="b6a5d-173">Informatie over endpoint</span><span class="sxs-lookup"><span data-stu-id="b6a5d-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="b6a5d-174">Huidige instantie:`RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="b6a5d-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="b6a5d-175">Andere functies en -exemplaar:`RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="b6a5d-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="b6a5d-176">`NodeContext`voor het huidige knooppuntadres</span><span class="sxs-lookup"><span data-stu-id="b6a5d-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="b6a5d-177">`FabricClient`en `ServicePartitionResolver` voor detectie van de service-eindpunt</span><span class="sxs-lookup"><span data-stu-id="b6a5d-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="b6a5d-178">Omgeving emulatie</span><span class="sxs-lookup"><span data-stu-id="b6a5d-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="b6a5d-179">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-179">N/A</span></span> |
| <span data-ttu-id="b6a5d-180">Gelijktijdige wijzigingsgebeurtenis</span><span class="sxs-lookup"><span data-stu-id="b6a5d-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="b6a5d-181">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="b6a5d-182">Configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="b6a5d-182">Configuration settings</span></span>
<span data-ttu-id="b6a5d-183">Configuratie-instellingen in de Cloud-Services worden ingesteld voor een VM-rol en tooall exemplaren van die VM-rol van toepassing.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-183">Configuration settings in Cloud Services are set for a VM role and apply tooall instances of that VM role.</span></span> <span data-ttu-id="b6a5d-184">Deze instellingen zijn ingesteld in ServiceConfiguration.*.cscfg bestanden sleutel-waardeparen en toegankelijk zijn via RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="b6a5d-185">In Service Fabric toepassen instellingen afzonderlijk tooeach service en tooeach toepassing, in plaats van tooa VM, omdat een virtuele machine kan meerdere services en toepassingen hosten.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-185">In Service Fabric, settings apply individually tooeach service and tooeach application, rather than tooa VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="b6a5d-186">Een service bestaat uit drie pakketten:</span><span class="sxs-lookup"><span data-stu-id="b6a5d-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="b6a5d-187">**Code:** Hallo service uitvoerbare bestanden, binaire bestanden, dll's en andere bestanden bevat een service nodig heeft toorun.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-187">**Code:** contains hello service executables, binaries, DLLs, and any other files a service needs toorun.</span></span>
* <span data-ttu-id="b6a5d-188">**Config:** alle configuratiebestanden en instellingen voor een service.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="b6a5d-189">**Gegevens:** statische gegevensbestanden die zijn gekoppeld aan het Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-189">**Data:** static data files associated with hello service.</span></span>

<span data-ttu-id="b6a5d-190">Elk van deze pakketten zijn onafhankelijk samengestelde en bijgewerkte.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="b6a5d-191">Soortgelijke tooCloud diensten, een configuratiepakket programmatisch kunnen worden geopend via een API en gebeurtenissen zijn beschikbaar toonotify Hallo-service van een pakket configuratiewijziging.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-191">Similar tooCloud Services, a config package can be accessed programmatically through an API and events are available toonotify hello service of a config package change.</span></span> <span data-ttu-id="b6a5d-192">Een bestand Settings.xml kan worden gebruikt voor de sleutel / waarde-configuratie en toegang op programmeerniveau vergelijkbare toohello app sectie instellingen van een App.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-192">A Settings.xml file can be used for key-value configuration and programmatic access similar toohello app settings section of an App.config file.</span></span> <span data-ttu-id="b6a5d-193">In tegenstelling tot Cloud-Services, kan een Service Fabric-configuratiepakket echter bevatten alle configuratiebestanden in een willekeurige indeling, of het XML, JSON, YAML of een aangepaste binaire indeling.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="b6a5d-194">Toegang tot configuratie</span><span class="sxs-lookup"><span data-stu-id="b6a5d-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="b6a5d-195">Cloudservices</span><span class="sxs-lookup"><span data-stu-id="b6a5d-195">Cloud Services</span></span>
<span data-ttu-id="b6a5d-196">Configuratie-instellingen van ServiceConfiguration.*.cscfg toegankelijk zijn via `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="b6a5d-197">Deze instellingen zijn algemeen beschikbaar tooall rolinstanties in Hallo dezelfde Cloud Service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-197">These settings are globally available tooall role instances in hello same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="b6a5d-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b6a5d-198">Service Fabric</span></span>
<span data-ttu-id="b6a5d-199">Elke service heeft een eigen afzonderlijke configuratie-pakket.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="b6a5d-200">Er is geen ingebouwde methode voor globale configuratie-instellingen toegankelijk door alle toepassingen in een cluster.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="b6a5d-201">Wanneer u Service-Fabric speciale Settings.xml configuratiebestand binnen een configuratiepakket gebruikt, kunnen waarden in Settings.xml worden overschreven op toepassingsniveau hello, die op toepassingsniveau configuratie-instellingen mogelijk te maken.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at hello application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="b6a5d-202">Configuratie-instellingen zijn toegangspogingen binnen elk service-exemplaar via Hallo-service `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-202">Configuration settings are accesses within each service instance through hello service's `CodePackageActivationContext`.</span></span>

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a><span data-ttu-id="b6a5d-203">Update-Configuratiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="b6a5d-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="b6a5d-204">Cloudservices</span><span class="sxs-lookup"><span data-stu-id="b6a5d-204">Cloud Services</span></span>
<span data-ttu-id="b6a5d-205">Hallo `RoleEnvironment.Changed` gebeurtenis gebruikte toonotify alle rolinstanties wanneer een wijziging optreedt in Hallo-omgeving, zoals een wijziging in de configuratie is.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-205">hello `RoleEnvironment.Changed` event is used toonotify all role instances when a change occurs in hello environment, such as a configuration change.</span></span> <span data-ttu-id="b6a5d-206">Dit is de gebruikte tooconsume configuratie-updates zonder rolinstanties recycling of opnieuw starten van een werkproces.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-206">This is used tooconsume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="b6a5d-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b6a5d-207">Service Fabric</span></span>
<span data-ttu-id="b6a5d-208">Elk van de drie pakkettypen Hallo in een service - Code, configuratie en gegevens - gebeurtenissen die een service-exemplaar wordt gewaarschuwd wanneer er een pakket wordt bijgewerkt, toegevoegd of verwijderd hebben.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-208">Each of hello three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="b6a5d-209">Een service, kan meerdere pakketten van elk type bevatten.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="b6a5d-210">Een service kan bijvoorbeeld meerdere config pakketten elk afzonderlijk samengestelde en kan worden uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="b6a5d-211">Deze gebeurtenissen zijn beschikbaar tooconsume wijzigingen in servicepakketten zonder Hallo service-exemplaar opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-211">These events are available tooconsume changes in service packages without restarting hello service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="b6a5d-212">Starten van de taken</span><span class="sxs-lookup"><span data-stu-id="b6a5d-212">Startup tasks</span></span>
<span data-ttu-id="b6a5d-213">Starten van de taken zijn acties die worden uitgevoerd voordat een toepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="b6a5d-214">Een taak starten is gewoonlijk gebruikte toorun setup scripts met verhoogde bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-214">A startup task is typically used toorun setup scripts using elevated privileges.</span></span> <span data-ttu-id="b6a5d-215">Ondersteuning voor opstarten taken zowel Cloudservices als Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="b6a5d-216">Hallo belangrijkste verschil is dat in Cloud-Services, een starten van de taak is gebonden tooa VM omdat deze deel uitmaakt van een rolinstantie terwijl een taak starten in Service Fabric gebonden tooa-service niet gebonden tooany is bepaalde VM.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-216">hello main difference is that in Cloud Services, a startup task is tied tooa VM because it is part of a role instance, whereas in Service Fabric a startup task is tied tooa service, which is not tied tooany particular VM.</span></span>

| <span data-ttu-id="b6a5d-217">Cloudservices</span><span class="sxs-lookup"><span data-stu-id="b6a5d-217">Cloud Services</span></span> | <span data-ttu-id="b6a5d-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b6a5d-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6a5d-219">Locatie van de configuratie</span><span class="sxs-lookup"><span data-stu-id="b6a5d-219">Configuration location</span></span> |<span data-ttu-id="b6a5d-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="b6a5d-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="b6a5d-221">Bevoegdheden</span><span class="sxs-lookup"><span data-stu-id="b6a5d-221">Privileges</span></span> |<span data-ttu-id="b6a5d-222">'beperkt' of 'verhoogde'</span><span class="sxs-lookup"><span data-stu-id="b6a5d-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="b6a5d-223">Sequentiëren</span><span class="sxs-lookup"><span data-stu-id="b6a5d-223">Sequencing</span></span> |<span data-ttu-id="b6a5d-224">'eenvoudige', 'achtergrond', 'voorgrond'</span><span class="sxs-lookup"><span data-stu-id="b6a5d-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="b6a5d-225">Cloudservices</span><span class="sxs-lookup"><span data-stu-id="b6a5d-225">Cloud Services</span></span>
<span data-ttu-id="b6a5d-226">In de Cloud Services een toegangspunt opstarten geconfigureerd per rol in ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a><span data-ttu-id="b6a5d-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b6a5d-227">Service Fabric</span></span>
<span data-ttu-id="b6a5d-228">In Service Fabric is een toegangspunt starten van de per-service in ServiceManifest.xml geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="b6a5d-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a><span data-ttu-id="b6a5d-229">Een opmerking over ontwikkelomgeving</span><span class="sxs-lookup"><span data-stu-id="b6a5d-229">A note about development environment</span></span>
<span data-ttu-id="b6a5d-230">Zowel Cloudservices als Service Fabric zijn geïntegreerd met Visual Studio met projectsjablonen en ondersteuning voor foutopsporing, configureren en implementeren van zowel lokaal en tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and tooAzure.</span></span> <span data-ttu-id="b6a5d-231">Zowel Cloudservices als Service Fabric bieden ook een runtime-omgeving voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="b6a5d-232">Hallo is verschil dat terwijl hello Service in de Cloud emuleert ontwikkeling runtime hello Azure-omgeving waarop deze wordt uitgevoerd, een emulator maakt geen gebruik van Service Fabric - Hallo volledige Service Fabric-runtime wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-232">hello difference is that while hello Cloud Service development runtime emulates hello Azure environment on which it runs, Service Fabric does not use an emulator - it uses hello complete Service Fabric runtime.</span></span> <span data-ttu-id="b6a5d-233">Hallo Hallo Service Fabric-omgeving u op uw lokale ontwikkelcomputer uitvoeren dezelfde omgeving die wordt uitgevoerd in de productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-233">hello Service Fabric environment you run on your local development machine is hello same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6a5d-234">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b6a5d-234">Next steps</span></span>
<span data-ttu-id="b6a5d-235">Lees meer over Service Fabric Reliable Services en Hallo fundamentele verschillen tussen Cloud Services en de Service Fabric-toepassing architectuur toounderstand hoe tootake profiteren van Hallo volledige van Service Fabric-onderdelen set.</span><span class="sxs-lookup"><span data-stu-id="b6a5d-235">Read more about Service Fabric Reliable Services and hello fundamental differences between Cloud Services and Service Fabric application architecture toounderstand how tootake advantage of hello full set of Service Fabric features.</span></span>

* [<span data-ttu-id="b6a5d-236">Aan de slag met Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="b6a5d-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="b6a5d-237">Conceptuele handleiding toohello verschillen tussen Cloudservices en Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b6a5d-237">Conceptual guide toohello differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
