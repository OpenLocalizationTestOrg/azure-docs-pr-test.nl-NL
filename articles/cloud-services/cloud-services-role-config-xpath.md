---
title: Cloud Services-rol config XPath-referentieoverzicht | Microsoft Docs
description: De verschillende XPath-instellingen kunt u in de cloud van de rol serviceconfiguratie instellingen weergeven als een omgevingsvariabele.
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
ms.openlocfilehash: fd6efac829d3fd9e2840362b8d2ff423add566d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="92fed-103">Configuratie-rolinstellingen weergeven als een omgevingsvariabele met XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="92fed-104">In de cloud service worker of web rol servicedefinitiebestand kan configuratiewaarden runtime worden blootgesteld als omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="92fed-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="92fed-105">De volgende waarden voor XPath worden ondersteund (die overeenkomen met de API-waarden).</span><span class="sxs-lookup"><span data-stu-id="92fed-105">The following XPath values are supported (which correspond to API values).</span></span>

<span data-ttu-id="92fed-106">Deze XPath-waarden zijn ook beschikbaar via de [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="92fed-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="92fed-107">App uitgevoerd in de emulator</span><span class="sxs-lookup"><span data-stu-id="92fed-107">App running in emulator</span></span>
<span data-ttu-id="92fed-108">Hiermee wordt aangegeven dat de app wordt uitgevoerd in de emulator.</span><span class="sxs-lookup"><span data-stu-id="92fed-108">Indicates that the app is running in the emulator.</span></span>

| <span data-ttu-id="92fed-109">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-109">Type</span></span> | <span data-ttu-id="92fed-110">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-111">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-111">XPath</span></span> |<span data-ttu-id="92fed-112">XPath = "/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="92fed-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="92fed-113">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-113">Code</span></span> |<span data-ttu-id="92fed-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="92fed-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="92fed-115">Implementatie-ID</span><span class="sxs-lookup"><span data-stu-id="92fed-115">Deployment ID</span></span>
<span data-ttu-id="92fed-116">Hiermee haalt u de implementatie-ID voor het exemplaar.</span><span class="sxs-lookup"><span data-stu-id="92fed-116">Retrieves the deployment ID for the instance.</span></span>

| <span data-ttu-id="92fed-117">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-117">Type</span></span> | <span data-ttu-id="92fed-118">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-119">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-119">XPath</span></span> |<span data-ttu-id="92fed-120">XPath = "/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="92fed-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="92fed-121">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-121">Code</span></span> |<span data-ttu-id="92fed-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="92fed-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="92fed-123">Rol-ID</span><span class="sxs-lookup"><span data-stu-id="92fed-123">Role ID</span></span>
<span data-ttu-id="92fed-124">Hiermee haalt u de huidige rol-ID voor het exemplaar.</span><span class="sxs-lookup"><span data-stu-id="92fed-124">Retrieves the current role ID for the instance.</span></span>

| <span data-ttu-id="92fed-125">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-125">Type</span></span> | <span data-ttu-id="92fed-126">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-127">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-127">XPath</span></span> |<span data-ttu-id="92fed-128">XPath = "/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="92fed-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="92fed-129">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-129">Code</span></span> |<span data-ttu-id="92fed-130">var-id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="92fed-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="92fed-131">Bijwerken van domein</span><span class="sxs-lookup"><span data-stu-id="92fed-131">Update domain</span></span>
<span data-ttu-id="92fed-132">Hiermee haalt u het updatedomein van het exemplaar.</span><span class="sxs-lookup"><span data-stu-id="92fed-132">Retrieves the update domain of the instance.</span></span>

| <span data-ttu-id="92fed-133">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-133">Type</span></span> | <span data-ttu-id="92fed-134">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-135">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-135">XPath</span></span> |<span data-ttu-id="92fed-136">XPath = "/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="92fed-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="92fed-137">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-137">Code</span></span> |<span data-ttu-id="92fed-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="92fed-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="92fed-139">Foutdomein</span><span class="sxs-lookup"><span data-stu-id="92fed-139">Fault domain</span></span>
<span data-ttu-id="92fed-140">Het foutdomein van het exemplaar wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="92fed-140">Retrieves the fault domain of the instance.</span></span>

| <span data-ttu-id="92fed-141">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-141">Type</span></span> | <span data-ttu-id="92fed-142">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-143">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-143">XPath</span></span> |<span data-ttu-id="92fed-144">XPath = "/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="92fed-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="92fed-145">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-145">Code</span></span> |<span data-ttu-id="92fed-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="92fed-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="92fed-147">Rolnaam</span><span class="sxs-lookup"><span data-stu-id="92fed-147">Role name</span></span>
<span data-ttu-id="92fed-148">Haalt de naam van de rol van de exemplaren.</span><span class="sxs-lookup"><span data-stu-id="92fed-148">Retrieves the role name of the instances.</span></span>

| <span data-ttu-id="92fed-149">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-149">Type</span></span> | <span data-ttu-id="92fed-150">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-151">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-151">XPath</span></span> |<span data-ttu-id="92fed-152">XPath = "/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="92fed-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="92fed-153">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-153">Code</span></span> |<span data-ttu-id="92fed-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="92fed-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="92fed-155">Configuratie-instelling</span><span class="sxs-lookup"><span data-stu-id="92fed-155">Config setting</span></span>
<span data-ttu-id="92fed-156">Haalt de waarde van de opgegeven configuratie-instelling.</span><span class="sxs-lookup"><span data-stu-id="92fed-156">Retrieves the value of the specified configuration setting.</span></span>

| <span data-ttu-id="92fed-157">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-157">Type</span></span> | <span data-ttu-id="92fed-158">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-159">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-159">XPath</span></span> |<span data-ttu-id="92fed-160">XPath = "/ RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting [@name= 'Setting1']/@value'</span><span class="sxs-lookup"><span data-stu-id="92fed-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="92fed-161">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-161">Code</span></span> |<span data-ttu-id="92fed-162">de instelling var = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="92fed-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="92fed-163">Pad voor lokale opslag</span><span class="sxs-lookup"><span data-stu-id="92fed-163">Local storage path</span></span>
<span data-ttu-id="92fed-164">Het pad voor lokale opslag voor het exemplaar wordt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="92fed-164">Retrieves the local storage path for the instance.</span></span>

| <span data-ttu-id="92fed-165">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-165">Type</span></span> | <span data-ttu-id="92fed-166">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-167">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-167">XPath</span></span> |<span data-ttu-id="92fed-168">XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name= 'LocalStore1']/@path'</span><span class="sxs-lookup"><span data-stu-id="92fed-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="92fed-169">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-169">Code</span></span> |<span data-ttu-id="92fed-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1"). RootPath;</span><span class="sxs-lookup"><span data-stu-id="92fed-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="92fed-171">De grootte van de lokale opslag</span><span class="sxs-lookup"><span data-stu-id="92fed-171">Local storage size</span></span>
<span data-ttu-id="92fed-172">Haalt de grootte van de lokale opslag voor het exemplaar.</span><span class="sxs-lookup"><span data-stu-id="92fed-172">Retrieves the size of the local storage for the instance.</span></span>

| <span data-ttu-id="92fed-173">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-173">Type</span></span> | <span data-ttu-id="92fed-174">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-175">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-175">XPath</span></span> |<span data-ttu-id="92fed-176">XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name= 'LocalStore1']/@sizeInMB'</span><span class="sxs-lookup"><span data-stu-id="92fed-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="92fed-177">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-177">Code</span></span> |<span data-ttu-id="92fed-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1"). MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="92fed-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="92fed-179">Protocol voor eindpunt</span><span class="sxs-lookup"><span data-stu-id="92fed-179">Endpoint protocol</span></span>
<span data-ttu-id="92fed-180">Haalt de eindpunt-protocol voor het exemplaar.</span><span class="sxs-lookup"><span data-stu-id="92fed-180">Retrieves the endpoint protocol for the instance.</span></span>

| <span data-ttu-id="92fed-181">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-181">Type</span></span> | <span data-ttu-id="92fed-182">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-183">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-183">XPath</span></span> |<span data-ttu-id="92fed-184">XPath = "/ RoleEnvironment/CurrentInstance/eindpunten/het eindpunt [@name= '1']/@protocol'</span><span class="sxs-lookup"><span data-stu-id="92fed-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="92fed-185">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-185">Code</span></span> |<span data-ttu-id="92fed-186">var b RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 = ']. Protocol;</span><span class="sxs-lookup"><span data-stu-id="92fed-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="92fed-187">Eindpunt IP</span><span class="sxs-lookup"><span data-stu-id="92fed-187">Endpoint IP</span></span>
<span data-ttu-id="92fed-188">Het opgegeven eindpunt IP-adres opgehaald.</span><span class="sxs-lookup"><span data-stu-id="92fed-188">Gets the specified endpoint's IP address.</span></span>

| <span data-ttu-id="92fed-189">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-189">Type</span></span> | <span data-ttu-id="92fed-190">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-191">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-191">XPath</span></span> |<span data-ttu-id="92fed-192">XPath = "/ RoleEnvironment/CurrentInstance/eindpunten/het eindpunt [@name= '1']/@address'</span><span class="sxs-lookup"><span data-stu-id="92fed-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="92fed-193">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-193">Code</span></span> |<span data-ttu-id="92fed-194">adres var RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 = ']. IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="92fed-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="92fed-195">Eindpuntpoort</span><span class="sxs-lookup"><span data-stu-id="92fed-195">Endpoint port</span></span>
<span data-ttu-id="92fed-196">Haalt de eindpuntpoort voor het exemplaar.</span><span class="sxs-lookup"><span data-stu-id="92fed-196">Retrieves the endpoint port for the instance.</span></span>

| <span data-ttu-id="92fed-197">Type</span><span class="sxs-lookup"><span data-stu-id="92fed-197">Type</span></span> | <span data-ttu-id="92fed-198">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="92fed-199">XPath</span><span class="sxs-lookup"><span data-stu-id="92fed-199">XPath</span></span> |<span data-ttu-id="92fed-200">XPath = "/ RoleEnvironment/CurrentInstance/eindpunten/het eindpunt [@name= '1']/@port'</span><span class="sxs-lookup"><span data-stu-id="92fed-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="92fed-201">Code</span><span class="sxs-lookup"><span data-stu-id="92fed-201">Code</span></span> |<span data-ttu-id="92fed-202">poort var RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 = ']. IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="92fed-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="92fed-203">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="92fed-203">Example</span></span>
<span data-ttu-id="92fed-204">Hier volgt een voorbeeld van een werkrol die u een taak starten met een omgevingsvariabele maakt `TestIsEmulated` ingesteld op de [ @emulated xpath-waarde](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="92fed-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="92fed-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92fed-205">Next steps</span></span>
<span data-ttu-id="92fed-206">Meer informatie over de [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) bestand.</span><span class="sxs-lookup"><span data-stu-id="92fed-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="92fed-207">Maak een [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) pakket.</span><span class="sxs-lookup"><span data-stu-id="92fed-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="92fed-208">Schakel [extern bureaublad](cloud-services-role-enable-remote-desktop.md) voor een rol.</span><span class="sxs-lookup"><span data-stu-id="92fed-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

