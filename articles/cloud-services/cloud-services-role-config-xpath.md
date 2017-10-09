---
title: aaaCloud Services-rol config XPath-referentieoverzicht | Microsoft Docs
description: Hallo diverse XPath-instellingen die u in de tooexpose instellingen voor de configuratie van Hallo cloud service-functie als een omgevingsvariabele gebruiken kunt.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="93c9d-103">Configuratie-rolinstellingen weergeven als een omgevingsvariabele met XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="93c9d-104">In Hallo cloud service worker of web rol servicedefinitiebestand kan configuratiewaarden runtime worden blootgesteld als omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="93c9d-104">In hello cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="93c9d-105">Hallo volgende XPath waarden worden ondersteund (die overeenkomt met tooAPI waarden).</span><span class="sxs-lookup"><span data-stu-id="93c9d-105">hello following XPath values are supported (which correspond tooAPI values).</span></span>

<span data-ttu-id="93c9d-106">Deze XPath-waarden zijn ook beschikbaar via Hallo [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="93c9d-106">These XPath values are also available through hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="93c9d-107">App uitgevoerd in de emulator</span><span class="sxs-lookup"><span data-stu-id="93c9d-107">App running in emulator</span></span>
<span data-ttu-id="93c9d-108">Hiermee wordt aangegeven dat die Hallo-app wordt uitgevoerd in Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="93c9d-108">Indicates that hello app is running in hello emulator.</span></span>

| <span data-ttu-id="93c9d-109">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-109">Type</span></span> | <span data-ttu-id="93c9d-110">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-111">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-111">XPath</span></span> |<span data-ttu-id="93c9d-112">XPath = "/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="93c9d-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="93c9d-113">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-113">Code</span></span> |<span data-ttu-id="93c9d-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="93c9d-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="93c9d-115">Implementatie-ID</span><span class="sxs-lookup"><span data-stu-id="93c9d-115">Deployment ID</span></span>
<span data-ttu-id="93c9d-116">Hallo implementatie-ID voor Hallo-exemplaar wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="93c9d-116">Retrieves hello deployment ID for hello instance.</span></span>

| <span data-ttu-id="93c9d-117">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-117">Type</span></span> | <span data-ttu-id="93c9d-118">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-119">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-119">XPath</span></span> |<span data-ttu-id="93c9d-120">XPath = "/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="93c9d-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="93c9d-121">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-121">Code</span></span> |<span data-ttu-id="93c9d-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="93c9d-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="93c9d-123">Rol-ID</span><span class="sxs-lookup"><span data-stu-id="93c9d-123">Role ID</span></span>
<span data-ttu-id="93c9d-124">Hallo huidige rol-ID voor Hallo-exemplaar wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="93c9d-124">Retrieves hello current role ID for hello instance.</span></span>

| <span data-ttu-id="93c9d-125">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-125">Type</span></span> | <span data-ttu-id="93c9d-126">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-127">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-127">XPath</span></span> |<span data-ttu-id="93c9d-128">XPath = "/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="93c9d-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="93c9d-129">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-129">Code</span></span> |<span data-ttu-id="93c9d-130">var-id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="93c9d-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="93c9d-131">Bijwerken van domein</span><span class="sxs-lookup"><span data-stu-id="93c9d-131">Update domain</span></span>
<span data-ttu-id="93c9d-132">Hallo updatedomein van Hallo-exemplaar wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="93c9d-132">Retrieves hello update domain of hello instance.</span></span>

| <span data-ttu-id="93c9d-133">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-133">Type</span></span> | <span data-ttu-id="93c9d-134">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-135">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-135">XPath</span></span> |<span data-ttu-id="93c9d-136">XPath = "/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="93c9d-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="93c9d-137">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-137">Code</span></span> |<span data-ttu-id="93c9d-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="93c9d-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="93c9d-139">Foutdomein</span><span class="sxs-lookup"><span data-stu-id="93c9d-139">Fault domain</span></span>
<span data-ttu-id="93c9d-140">Hiermee haalt u foutdomein op Hallo van Hallo-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="93c9d-140">Retrieves hello fault domain of hello instance.</span></span>

| <span data-ttu-id="93c9d-141">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-141">Type</span></span> | <span data-ttu-id="93c9d-142">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-143">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-143">XPath</span></span> |<span data-ttu-id="93c9d-144">XPath = "/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="93c9d-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="93c9d-145">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-145">Code</span></span> |<span data-ttu-id="93c9d-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="93c9d-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="93c9d-147">Rolnaam</span><span class="sxs-lookup"><span data-stu-id="93c9d-147">Role name</span></span>
<span data-ttu-id="93c9d-148">De rolnaam Hallo Hallo exemplaren van opgehaald.</span><span class="sxs-lookup"><span data-stu-id="93c9d-148">Retrieves hello role name of hello instances.</span></span>

| <span data-ttu-id="93c9d-149">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-149">Type</span></span> | <span data-ttu-id="93c9d-150">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-151">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-151">XPath</span></span> |<span data-ttu-id="93c9d-152">XPath = "/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="93c9d-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="93c9d-153">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-153">Code</span></span> |<span data-ttu-id="93c9d-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="93c9d-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="93c9d-155">Configuratie-instelling</span><span class="sxs-lookup"><span data-stu-id="93c9d-155">Config setting</span></span>
<span data-ttu-id="93c9d-156">Haalt Hallo waarde Hallo opgegeven configuratie-instelling.</span><span class="sxs-lookup"><span data-stu-id="93c9d-156">Retrieves hello value of hello specified configuration setting.</span></span>

| <span data-ttu-id="93c9d-157">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-157">Type</span></span> | <span data-ttu-id="93c9d-158">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-159">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-159">XPath</span></span> |<span data-ttu-id="93c9d-160">XPath = "/ RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting [@name= 'Setting1']/@value'</span><span class="sxs-lookup"><span data-stu-id="93c9d-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="93c9d-161">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-161">Code</span></span> |<span data-ttu-id="93c9d-162">de instelling var = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="93c9d-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="93c9d-163">Pad voor lokale opslag</span><span class="sxs-lookup"><span data-stu-id="93c9d-163">Local storage path</span></span>
<span data-ttu-id="93c9d-164">Hallo lokale opslagpad voor Hallo-exemplaar wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="93c9d-164">Retrieves hello local storage path for hello instance.</span></span>

| <span data-ttu-id="93c9d-165">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-165">Type</span></span> | <span data-ttu-id="93c9d-166">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-167">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-167">XPath</span></span> |<span data-ttu-id="93c9d-168">XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name= 'LocalStore1']/@path'</span><span class="sxs-lookup"><span data-stu-id="93c9d-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="93c9d-169">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-169">Code</span></span> |<span data-ttu-id="93c9d-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1"). RootPath;</span><span class="sxs-lookup"><span data-stu-id="93c9d-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="93c9d-171">De grootte van de lokale opslag</span><span class="sxs-lookup"><span data-stu-id="93c9d-171">Local storage size</span></span>
<span data-ttu-id="93c9d-172">Haalt de grootte op Hallo van lokale opslag Hallo voor Hallo-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="93c9d-172">Retrieves hello size of hello local storage for hello instance.</span></span>

| <span data-ttu-id="93c9d-173">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-173">Type</span></span> | <span data-ttu-id="93c9d-174">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-175">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-175">XPath</span></span> |<span data-ttu-id="93c9d-176">XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name= 'LocalStore1']/@sizeInMB'</span><span class="sxs-lookup"><span data-stu-id="93c9d-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="93c9d-177">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-177">Code</span></span> |<span data-ttu-id="93c9d-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1"). MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="93c9d-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="93c9d-179">Protocol voor eindpunt</span><span class="sxs-lookup"><span data-stu-id="93c9d-179">Endpoint protocol</span></span>
<span data-ttu-id="93c9d-180">Hallo eindpunt protocol voor het Hallo-exemplaar wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="93c9d-180">Retrieves hello endpoint protocol for hello instance.</span></span>

| <span data-ttu-id="93c9d-181">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-181">Type</span></span> | <span data-ttu-id="93c9d-182">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-183">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-183">XPath</span></span> |<span data-ttu-id="93c9d-184">XPath = "/ RoleEnvironment/CurrentInstance/eindpunten/het eindpunt [@name= '1']/@protocol'</span><span class="sxs-lookup"><span data-stu-id="93c9d-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="93c9d-185">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-185">Code</span></span> |<span data-ttu-id="93c9d-186">var b RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 = ']. Protocol;</span><span class="sxs-lookup"><span data-stu-id="93c9d-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="93c9d-187">Eindpunt IP</span><span class="sxs-lookup"><span data-stu-id="93c9d-187">Endpoint IP</span></span>
<span data-ttu-id="93c9d-188">Hallo opgehaald van het eindpunt IP-adres opgegeven.</span><span class="sxs-lookup"><span data-stu-id="93c9d-188">Gets hello specified endpoint's IP address.</span></span>

| <span data-ttu-id="93c9d-189">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-189">Type</span></span> | <span data-ttu-id="93c9d-190">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-191">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-191">XPath</span></span> |<span data-ttu-id="93c9d-192">XPath = "/ RoleEnvironment/CurrentInstance/eindpunten/het eindpunt [@name= '1']/@address'</span><span class="sxs-lookup"><span data-stu-id="93c9d-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="93c9d-193">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-193">Code</span></span> |<span data-ttu-id="93c9d-194">adres var RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 = ']. IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="93c9d-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="93c9d-195">Eindpuntpoort</span><span class="sxs-lookup"><span data-stu-id="93c9d-195">Endpoint port</span></span>
<span data-ttu-id="93c9d-196">Hallo eindpuntpoort voor Hallo-exemplaar wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="93c9d-196">Retrieves hello endpoint port for hello instance.</span></span>

| <span data-ttu-id="93c9d-197">Type</span><span class="sxs-lookup"><span data-stu-id="93c9d-197">Type</span></span> | <span data-ttu-id="93c9d-198">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="93c9d-199">XPath</span><span class="sxs-lookup"><span data-stu-id="93c9d-199">XPath</span></span> |<span data-ttu-id="93c9d-200">XPath = "/ RoleEnvironment/CurrentInstance/eindpunten/het eindpunt [@name= '1']/@port'</span><span class="sxs-lookup"><span data-stu-id="93c9d-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="93c9d-201">Code</span><span class="sxs-lookup"><span data-stu-id="93c9d-201">Code</span></span> |<span data-ttu-id="93c9d-202">poort var RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 = ']. IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="93c9d-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="93c9d-203">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="93c9d-203">Example</span></span>
<span data-ttu-id="93c9d-204">Hier volgt een voorbeeld van een werkrol die u een taak starten met een omgevingsvariabele maakt `TestIsEmulated` ingesteld toohello [ @emulated xpath-waarde](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="93c9d-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set toohello [@emulated xpath value](#app-running-in-emulator).</span></span> 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a><span data-ttu-id="93c9d-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93c9d-205">Next steps</span></span>
<span data-ttu-id="93c9d-206">Meer informatie over Hallo [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) bestand.</span><span class="sxs-lookup"><span data-stu-id="93c9d-206">Learn more about hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="93c9d-207">Maak een [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) pakket.</span><span class="sxs-lookup"><span data-stu-id="93c9d-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="93c9d-208">Schakel [extern bureaublad](cloud-services-role-enable-remote-desktop.md) voor een rol.</span><span class="sxs-lookup"><span data-stu-id="93c9d-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

