---
title: aaaManage omgevingen met meerdere in Service Fabric | Microsoft Docs
description: "Service Fabric-toepassingen kunnen worden uitgevoerd op clusters die in grootte van één machine toothousands machines variëren. In sommige gevallen zult u tooconfigure uw toepassing anders voor deze uiteenlopende omgevingen. In dit artikel bevat informatie over hoe de andere toepassingsparameters toodefine per omgeving."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="ac0e4-105">Parameters voor de toepassing voor omgevingen met meerdere beheren</span><span class="sxs-lookup"><span data-stu-id="ac0e4-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="ac0e4-106">U kunt Azure Service Fabric-clusters maken met behulp van een willekeurige plaats uit één toomany duizenden computers.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-106">You can create Azure Service Fabric clusters by using anywhere from one toomany thousands of machines.</span></span> <span data-ttu-id="ac0e4-107">Hoewel binaire bestanden van toepassingen zonder dat aanpassingen nodig over deze breed scala aan omgevingen uitvoeren kunnen, wilt u meestal tooconfigure Hallo toepassing anders, afhankelijk van het aantal machines die u implementeert op Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-107">While application binaries can run without modification across this wide spectrum of environments, you often want tooconfigure hello application differently, depending on hello number of machines you're deploying to.</span></span>

<span data-ttu-id="ac0e4-108">Een eenvoudig voorbeeld kunt u beter `InstanceCount` voor een stateless service.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="ac0e4-109">Wanneer u toepassingen in Azure uitvoert, doorgaans wilt u tooset deze speciale parameter toohello-waarde '1'.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-109">When you are running applications in Azure, you generally want tooset this parameter toohello special value of "-1".</span></span> <span data-ttu-id="ac0e4-110">Deze configuratie zorgt ervoor dat uw service wordt uitgevoerd op elk knooppunt in het Hallo-cluster (of elk knooppunt in knooppunttype Hallo als u een beperking voor de plaatsing hebt ingesteld).</span><span class="sxs-lookup"><span data-stu-id="ac0e4-110">This configuration ensures that your service is running on every node in hello cluster (or every node in hello node type if you have set a placement constraint).</span></span> <span data-ttu-id="ac0e4-111">Deze configuratie is echter niet geschikt voor een cluster met één computer omdat er meerdere processen luistert op Hallo dezelfde geen eindpunt op een enkele computer.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on hello same endpoint on a single machine.</span></span> <span data-ttu-id="ac0e4-112">In plaats daarvan doorgaans ingesteld `InstanceCount` te '1'.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-112">Instead, you typically set `InstanceCount` too"1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="ac0e4-113">Omgeving-specifieke parameters opgeven</span><span class="sxs-lookup"><span data-stu-id="ac0e4-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="ac0e4-114">Hallo oplossing toothis configuratieprobleem is een set met geparameteriseerde standaardservices en toepassingsbestanden parameter die de parameterwaarden van deze voor een bepaalde omgeving invullen.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-114">hello solution toothis configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="ac0e4-115">Standaardservices en de parameters voor de toepassing en worden geconfigureerd in de toepassing hello service manifesten.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-115">Default services and application parameters are configured in hello application and service manifests.</span></span> <span data-ttu-id="ac0e4-116">Hallo schemadefinitie voor Hallo ServiceManifest.xml en ApplicationManifest.xml bestanden is geïnstalleerd met Hallo Service Fabric SDK en hulpprogramma's te*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-116">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml files is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="ac0e4-117">Standaard-services</span><span class="sxs-lookup"><span data-stu-id="ac0e4-117">Default services</span></span>
<span data-ttu-id="ac0e4-118">Service Fabric-toepassingen bestaan uit een verzameling van service-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="ac0e4-119">Terwijl het is mogelijk dat u een lege toepassing toocreate en maak vervolgens alle service-exemplaren dynamisch, hebben de meeste toepassingen een set van core services die altijd moet worden gemaakt wanneer de toepassing hello wordt geïnstantieerd.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-119">While it is possible for you toocreate an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when hello application is instantiated.</span></span> <span data-ttu-id="ac0e4-120">Dit zijn waarnaar wordt verwezen tooas 'standaardservices'.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-120">These are referred tooas "default services".</span></span> <span data-ttu-id="ac0e4-121">Ze worden opgegeven in de toepassingsmanifest Hallo met tijdelijke aanduidingen voor de per-omgeving configuratie opgenomen tussen vierkante haken:</span><span class="sxs-lookup"><span data-stu-id="ac0e4-121">They are specified in hello application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

<span data-ttu-id="ac0e4-122">Elk van de benoemde parameters Hallo moet zijn gedefinieerd binnen Hallo Parameters element van het manifest van de toepassing hello:</span><span class="sxs-lookup"><span data-stu-id="ac0e4-122">Each of hello named parameters must be defined within hello Parameters element of hello application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="ac0e4-123">Hallo DefaultValue kenmerk geeft Hallo waarde toobe in Hallo afwezigheid van een meer specifieke parameter gebruikt voor een bepaalde omgeving.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-123">hello DefaultValue attribute specifies hello value toobe used in hello absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="ac0e4-124">Niet alle parameters van de service-exemplaar zijn geschikt voor configuratie van per-omgeving.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="ac0e4-125">Hallo bovenstaande voorbeeld Hallo LowKey en HighKey waarden voor het partitieschema Hallo-service zijn expliciet is gedefinieerd voor alle exemplaren van Hallo-service sinds Hallo partitiebereik een functie van Hallo gegevens domein, niet Hallo-omgeving is.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-125">In hello example above, hello LowKey and HighKey values for hello service's partitioning scheme are explicitly defined for all instances of hello service since hello partition range is a function of hello data domain, not hello environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="ac0e4-126">Configuratie-instellingen voor de per-omgeving</span><span class="sxs-lookup"><span data-stu-id="ac0e4-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="ac0e4-127">Hallo [Service Fabric-toepassingsmodel](service-fabric-application-model.md) schakelt services tooinclude configuratiepakketten met aangepaste sleutel-waardeparen die kunnen gelezen tijdens runtime worden.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-127">hello [Service Fabric application model](service-fabric-application-model.md) enables services tooinclude configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="ac0e4-128">Hallo-waarden van deze instellingen kunnen ook worden onderscheiden door omgeving door te geven een `ConfigOverride` Hallo-toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-128">hello values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in hello application manifest.</span></span>

<span data-ttu-id="ac0e4-129">Stel dat u de volgende instelling in Hallo Config\Settings.xml bestand voor Hallo Hallo hebt `Stateful1` service:</span><span class="sxs-lookup"><span data-stu-id="ac0e4-129">Suppose that you have hello following setting in hello Config\Settings.xml file for hello `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="ac0e4-130">toooverride deze waarde voor de combinatie van een specifieke toepassingsomgeving, maak een `ConfigOverride` wanneer u Hallo servicemanifest in het toepassingsmanifest Hallo importeert.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-130">toooverride this value for a specific application/environment pair, create a `ConfigOverride` when you import hello service manifest in hello application manifest.</span></span>

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
<span data-ttu-id="ac0e4-131">Deze parameter kan vervolgens worden geconfigureerd door omgeving zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="ac0e4-132">U kunt dit doen door het declareren in Hallo parameters gedeelte van het toepassingsmanifest Hallo en omgeving-specifieke waarden opgeven in de parameter toepassingsbestanden Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-132">You can do this by declaring it in hello parameters section of hello application manifest and specifying environment-specific values in hello application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="ac0e4-133">In geval van configuratie-instellingen service Hallo er zijn drie locaties waar Hallo-waarde van een sleutel kan worden ingesteld: Hallo service configuratiepakket Hallo toepassingsmanifest en parameterbestand Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-133">In hello case of service configuration settings, there are three places where hello value of a key can be set: hello service configuration package, hello application manifest, and hello application parameter file.</span></span> <span data-ttu-id="ac0e4-134">Service Fabric wordt altijd kiezen uit parameterbestand Hallo-toepassing eerst (indien opgegeven), vervolgens Hallo manifest van de toepassing en ten slotte Hallo configuratiepakket.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-134">Service Fabric will always choose from hello application parameter file first (if specified), then hello application manifest, and finally hello configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="ac0e4-135">Instellen en het gebruik van omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="ac0e4-135">Setting and using environment variables</span></span> 
<span data-ttu-id="ac0e4-136">U kunt opgeven en deze omgevingsvariabelen worden ingesteld in Hallo ServiceManifest.xml bestand en vervolgens uitschakelen in Hallo ApplicationManifest.xml bestand per exemplaar op basis van een.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-136">You can specify and set environment variables in hello ServiceManifest.xml file and then override these in hello ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="ac0e4-137">Hallo voorbeeld hieronder ziet u twee omgevingsvariabelen, één met een waarde ingesteld en Hallo andere wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-137">hello example below shows two environment variables, one with a value set and hello other is overridden.</span></span> <span data-ttu-id="ac0e4-138">U kunt de parameters voor de toepassing tooset omgevingsvariabelen worden de waarden in Hallo dezelfde manier dat deze zijn gebruikt voor onderdrukkingen in configuratie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-138">You can use application parameters tooset environment variables values in hello same way that these were used for config overrides.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
<span data-ttu-id="ac0e4-139">toooverride hello environment variables in de Hallo ApplicationManifest.xml, verwijzing Hallo codepakket in Hallo ServiceManifest Hello `EnvironmentOverrides` element.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-139">toooverride hello environment variables in hello ApplicationManifest.xml, reference hello code package in hello ServiceManifest with hello `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="ac0e4-140">Zodra Hallo service-exemplaar met de naam is gemaakt, kunt u omgevingsvariabelen Hallo kunt openen vanaf code.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-140">Once hello named service instance is created you can access hello environment variables from code.</span></span> <span data-ttu-id="ac0e4-141">bijvoorbeeld In C# kunt u doen Hallo volgende</span><span class="sxs-lookup"><span data-stu-id="ac0e4-141">e.g. In C# you can do hello following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="ac0e4-142">Service Fabric-omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="ac0e4-142">Service Fabric environment variables</span></span>
<span data-ttu-id="ac0e4-143">Service Fabric is ingebouwd in de omgevingsvariabelen instellen voor elke service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="ac0e4-144">Hallo volledige lijst met omgevingsvariabelen is hieronder, waar hello toepassingsgroepen in vet weet Hallo toepassingsgroepen die u in uw service gebruiken wilt Hallo andere wordt gebruikt door de Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-144">hello full list of environment variables is below, where hello ones in bold are hello ones that you will use in your service, hello other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="ac0e4-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="ac0e4-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="ac0e4-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="ac0e4-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="ac0e4-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="ac0e4-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="ac0e4-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="ac0e4-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="ac0e4-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="ac0e4-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="ac0e4-151">**TypeEndpoint Fabric_Endpoint_ [YourServiceName]**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="ac0e4-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="ac0e4-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="ac0e4-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="ac0e4-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="ac0e4-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="ac0e4-156">Fabric_NodeId</span></span>
* <span data-ttu-id="ac0e4-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="ac0e4-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="ac0e4-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="ac0e4-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="ac0e4-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="ac0e4-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="ac0e4-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="ac0e4-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="ac0e4-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="ac0e4-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="ac0e4-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="ac0e4-163">FabricPackageFileName</span></span>

<span data-ttu-id="ac0e4-164">Hallo code belows ziet u hoe toolist Service Fabric-omgevingsvariabelen Hallo</span><span class="sxs-lookup"><span data-stu-id="ac0e4-164">hello code belows shows how toolist hello Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="ac0e4-165">Hallo hieronder vindt u voorbeelden van omgevingsvariabelen voor een toepassingstype aangeroepen `GuestExe.Application` aangeroepen met een servicetype `FrontEndService` wanneer uitvoeren op uw lokale dev-computer.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-165">hello following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="ac0e4-166">**Fabric_ApplicationName fabric:/GuestExe.Application =**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="ac0e4-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="ac0e4-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="ac0e4-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="ac0e4-170">**Fabric_NodeName _Node_2 =**</span><span class="sxs-lookup"><span data-stu-id="ac0e4-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="ac0e4-171">Parameter voor toepassingsbestanden</span><span class="sxs-lookup"><span data-stu-id="ac0e4-171">Application parameter files</span></span>
<span data-ttu-id="ac0e4-172">Hallo Service Fabric-toepassingsproject kan een of meer parameter voor toepassingsbestanden bevatten.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-172">hello Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="ac0e4-173">Elk van deze definieert specifieke waarden voor Hallo-parameters die zijn gedefinieerd in het toepassingsmanifest Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="ac0e4-173">Each of them defines hello specific values for hello parameters that are defined in hello application manifest:</span></span>

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
<span data-ttu-id="ac0e4-174">Een nieuwe toepassing bevat drie parameter voor toepassingsbestanden, met de naam Local.1Node.xml Local.5Node.xml en Cloud.xml:</span><span class="sxs-lookup"><span data-stu-id="ac0e4-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Parameter voor toepassingsbestanden in Solution Explorer][app-parameters-solution-explorer]

<span data-ttu-id="ac0e4-176">een parameterbestand toocreate gewoon kopiëren en plakken van een bestaande en een nieuwe naam geven.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-176">toocreate a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="ac0e4-177">Omgeving-specifieke parameters identificeren tijdens de implementatie</span><span class="sxs-lookup"><span data-stu-id="ac0e4-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="ac0e4-178">Tijdens de implementatie moet u toochoose Hallo juiste parameter bestand tooapply met uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-178">At deployment time, you need toochoose hello appropriate parameter file tooapply with your application.</span></span> <span data-ttu-id="ac0e4-179">U kunt dit doen via het dialoogvenster voor het publiceren van Hallo in Visual Studio of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-179">You can do this through hello Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="ac0e4-180">Implementeren vanuit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac0e4-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="ac0e4-181">U kunt kiezen uit Hallo lijst met beschikbare parameterbestanden wanneer u uw toepassing in Visual Studio publiceert.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-181">You can choose from hello list of available parameter files when you publish your application in Visual Studio.</span></span>

![Kies een parameterbestand in Hallo publiceren dialoogvenster][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="ac0e4-183">Implementeren vanaf PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac0e4-183">Deploy from PowerShell</span></span>
<span data-ttu-id="ac0e4-184">Hallo `Deploy-FabricApplication.ps1` PowerShell-script is opgenomen in de projectsjabloon Hallo-toepassing een publicatieprofiel als een parameter accepteert en Hallo PublishProfile bevat een verwijzing toohello toepassingsbestand parameters.</span><span class="sxs-lookup"><span data-stu-id="ac0e4-184">hello `Deploy-FabricApplication.ps1` PowerShell script included in hello application project template accepts a publish profile as a parameter and hello PublishProfile contains a reference toohello application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="ac0e4-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ac0e4-185">Next steps</span></span>
<span data-ttu-id="ac0e4-186">toolearn meer informatie over een aantal Hallo belangrijkste concepten die worden beschreven in dit onderwerp, Zie Hallo [technisch overzicht van Service Fabric](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac0e4-186">toolearn more about some of hello core concepts that are discussed in this topic, see hello [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="ac0e4-187">Zie voor meer informatie over de mogelijkheden van andere app-beheer die beschikbaar in Visual Studio zijn [beheren van uw Service Fabric-toepassingen in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="ac0e4-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
