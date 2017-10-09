---
title: aaaPublish WebApplicationVM | Microsoft Docs
description: Meer informatie over hoe toodeploy een web application tooa virtuele machine. Dit script maakt Hallo vereist resources in uw Azure-abonnement als deze nog niet bestaan.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="178c0-104">Publiceren WebApplicationVM (Windows PowerShell-script)</span><span class="sxs-lookup"><span data-stu-id="178c0-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="178c0-105">Een web application tooa virtuele machine implementeert.</span><span class="sxs-lookup"><span data-stu-id="178c0-105">Deploys a web application tooa virtual machine.</span></span> <span data-ttu-id="178c0-106">Hallo script maakt Hallo vereist resources in uw Azure-abonnement als deze nog niet bestaan.</span><span class="sxs-lookup"><span data-stu-id="178c0-106">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="178c0-107">Configuratie</span><span class="sxs-lookup"><span data-stu-id="178c0-107">Configuration</span></span>
<span data-ttu-id="178c0-108">Hallo pad toohello JSON-configuratiebestand dat Hallo details van Hallo implementatie beschrijft.</span><span class="sxs-lookup"><span data-stu-id="178c0-108">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="178c0-109">Aliassen</span><span class="sxs-lookup"><span data-stu-id="178c0-109">Aliases</span></span> | <span data-ttu-id="178c0-110">Geen</span><span class="sxs-lookup"><span data-stu-id="178c0-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="178c0-111">Vereist?</span><span class="sxs-lookup"><span data-stu-id="178c0-111">Required?</span></span> |<span data-ttu-id="178c0-112">De waarde True</span><span class="sxs-lookup"><span data-stu-id="178c0-112">true</span></span> |
| <span data-ttu-id="178c0-113">Positie</span><span class="sxs-lookup"><span data-stu-id="178c0-113">Position</span></span> |<span data-ttu-id="178c0-114">Met de naam</span><span class="sxs-lookup"><span data-stu-id="178c0-114">named</span></span> |
| <span data-ttu-id="178c0-115">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="178c0-115">Default value</span></span> |<span data-ttu-id="178c0-116">Geen</span><span class="sxs-lookup"><span data-stu-id="178c0-116">none</span></span> |
| <span data-ttu-id="178c0-117">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-117">Accept pipeline input?</span></span> |<span data-ttu-id="178c0-118">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-118">false</span></span> |
| <span data-ttu-id="178c0-119">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-119">Accept wildcard characters?</span></span> |<span data-ttu-id="178c0-120">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="178c0-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="178c0-121">SubscriptionName</span></span>
<span data-ttu-id="178c0-122">Hallo-naam van hello Azure-abonnement waaraan u toocreate Hallo virtuele machine wilt.</span><span class="sxs-lookup"><span data-stu-id="178c0-122">hello name of hello Azure subscription in which you want toocreate hello virtual machine.</span></span>

| <span data-ttu-id="178c0-123">Aliassen</span><span class="sxs-lookup"><span data-stu-id="178c0-123">Aliases</span></span> | <span data-ttu-id="178c0-124">Geen</span><span class="sxs-lookup"><span data-stu-id="178c0-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="178c0-125">Vereist?</span><span class="sxs-lookup"><span data-stu-id="178c0-125">Required?</span></span> |<span data-ttu-id="178c0-126">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-126">false</span></span> |
| <span data-ttu-id="178c0-127">Positie</span><span class="sxs-lookup"><span data-stu-id="178c0-127">Position</span></span> |<span data-ttu-id="178c0-128">Met de naam</span><span class="sxs-lookup"><span data-stu-id="178c0-128">named</span></span> |
| <span data-ttu-id="178c0-129">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="178c0-129">Default value</span></span> |<span data-ttu-id="178c0-130">Maakt gebruik van het eerste abonnement Hallo in Hallo abonnementsbestand</span><span class="sxs-lookup"><span data-stu-id="178c0-130">Uses hello first subscription in hello subscription file</span></span> |
| <span data-ttu-id="178c0-131">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-131">Accept pipeline input?</span></span> |<span data-ttu-id="178c0-132">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-132">false</span></span> |
| <span data-ttu-id="178c0-133">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-133">Accept wildcard characters?</span></span> |<span data-ttu-id="178c0-134">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="178c0-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="178c0-135">WebDeployPackage</span></span>
<span data-ttu-id="178c0-136">Hallo pad toohello web deployment pakket toopublish toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="178c0-136">hello path toohello web deployment package toopublish toohello virtual machine.</span></span> <span data-ttu-id="178c0-137">U kunt dit pakket kunt maken met behulp van de wizard webpublicatie Hallo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="178c0-137">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="178c0-138">Zie [procedure: een Web-implementatiepakket maken in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="178c0-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="178c0-139">Aliassen</span><span class="sxs-lookup"><span data-stu-id="178c0-139">Aliases</span></span> | <span data-ttu-id="178c0-140">Geen</span><span class="sxs-lookup"><span data-stu-id="178c0-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="178c0-141">Vereist?</span><span class="sxs-lookup"><span data-stu-id="178c0-141">Required?</span></span> |<span data-ttu-id="178c0-142">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-142">false</span></span> |
| <span data-ttu-id="178c0-143">Positie</span><span class="sxs-lookup"><span data-stu-id="178c0-143">Position</span></span> |<span data-ttu-id="178c0-144">Met de naam</span><span class="sxs-lookup"><span data-stu-id="178c0-144">named</span></span> |
| <span data-ttu-id="178c0-145">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="178c0-145">Default value</span></span> |<span data-ttu-id="178c0-146">Geen</span><span class="sxs-lookup"><span data-stu-id="178c0-146">none</span></span> |
| <span data-ttu-id="178c0-147">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-147">Accept pipeline input?</span></span> |<span data-ttu-id="178c0-148">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-148">false</span></span> |
| <span data-ttu-id="178c0-149">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-149">Accept wildcard characters?</span></span> |<span data-ttu-id="178c0-150">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="178c0-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="178c0-151">AllowUntrusted</span></span>
<span data-ttu-id="178c0-152">Indien waar, mogen Hallo gebruik van certificaten die niet zijn ondertekend door een vertrouwde basiscertificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="178c0-152">If true, allow hello use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="178c0-153">Aliassen</span><span class="sxs-lookup"><span data-stu-id="178c0-153">Aliases</span></span> | <span data-ttu-id="178c0-154">Geen</span><span class="sxs-lookup"><span data-stu-id="178c0-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="178c0-155">Vereist?</span><span class="sxs-lookup"><span data-stu-id="178c0-155">Required?</span></span> |<span data-ttu-id="178c0-156">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-156">false</span></span> |
| <span data-ttu-id="178c0-157">Positie</span><span class="sxs-lookup"><span data-stu-id="178c0-157">Position</span></span> |<span data-ttu-id="178c0-158">Met de naam</span><span class="sxs-lookup"><span data-stu-id="178c0-158">named</span></span> |
| <span data-ttu-id="178c0-159">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="178c0-159">Default value</span></span> |<span data-ttu-id="178c0-160">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-160">false</span></span> |
| <span data-ttu-id="178c0-161">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-161">Accept pipeline input?</span></span> |<span data-ttu-id="178c0-162">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-162">false</span></span> |
| <span data-ttu-id="178c0-163">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-163">Accept wildcard characters?</span></span> |<span data-ttu-id="178c0-164">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="178c0-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="178c0-165">VMPassword</span></span>
<span data-ttu-id="178c0-166">Hallo-referenties voor de account van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="178c0-166">hello credentials for hello virtual machine account.</span></span> <span data-ttu-id="178c0-167">Voorbeeld: - VMPassword @{naam = 'admin'; Wachtwoord = 'password'}</span><span class="sxs-lookup"><span data-stu-id="178c0-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="178c0-168">Aliassen</span><span class="sxs-lookup"><span data-stu-id="178c0-168">Aliases</span></span> | <span data-ttu-id="178c0-169">Geen</span><span class="sxs-lookup"><span data-stu-id="178c0-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="178c0-170">Vereist?</span><span class="sxs-lookup"><span data-stu-id="178c0-170">Required?</span></span> |<span data-ttu-id="178c0-171">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-171">false</span></span> |
| <span data-ttu-id="178c0-172">Positie</span><span class="sxs-lookup"><span data-stu-id="178c0-172">Position</span></span> |<span data-ttu-id="178c0-173">Met de naam</span><span class="sxs-lookup"><span data-stu-id="178c0-173">named</span></span> |
| <span data-ttu-id="178c0-174">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="178c0-174">Default value</span></span> |<span data-ttu-id="178c0-175">Geen</span><span class="sxs-lookup"><span data-stu-id="178c0-175">none</span></span> |
| <span data-ttu-id="178c0-176">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-176">Accept pipeline input?</span></span> |<span data-ttu-id="178c0-177">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-177">false</span></span> |
| <span data-ttu-id="178c0-178">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-178">Accept wildcard characters?</span></span> |<span data-ttu-id="178c0-179">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="178c0-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="178c0-180">DatabaseServerPassword</span></span>
<span data-ttu-id="178c0-181">Hallo-referenties voor Hallo SQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="178c0-181">hello credentials for hello SQL database in Azure.</span></span> <span data-ttu-id="178c0-182">Voorbeeld: - DatabaseServerPassword @{naam = 'admin'; Wachtwoord = 'password'}</span><span class="sxs-lookup"><span data-stu-id="178c0-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="178c0-183">Aliassen</span><span class="sxs-lookup"><span data-stu-id="178c0-183">Aliases</span></span> | <span data-ttu-id="178c0-184">Geen</span><span class="sxs-lookup"><span data-stu-id="178c0-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="178c0-185">Vereist?</span><span class="sxs-lookup"><span data-stu-id="178c0-185">Required?</span></span> |<span data-ttu-id="178c0-186">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-186">false</span></span> |
| <span data-ttu-id="178c0-187">Positie</span><span class="sxs-lookup"><span data-stu-id="178c0-187">Position</span></span> |<span data-ttu-id="178c0-188">Met de naam</span><span class="sxs-lookup"><span data-stu-id="178c0-188">named</span></span> |
| <span data-ttu-id="178c0-189">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="178c0-189">Default value</span></span> |<span data-ttu-id="178c0-190">Geen</span><span class="sxs-lookup"><span data-stu-id="178c0-190">none</span></span> |
| <span data-ttu-id="178c0-191">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-191">Accept pipeline input?</span></span> |<span data-ttu-id="178c0-192">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-192">false</span></span> |
| <span data-ttu-id="178c0-193">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-193">Accept wildcard characters?</span></span> |<span data-ttu-id="178c0-194">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="178c0-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="178c0-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="178c0-196">Indien waar, uitvoer afdrukken berichten van Hallo script toohello stroom.</span><span class="sxs-lookup"><span data-stu-id="178c0-196">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="178c0-197">Aliassen</span><span class="sxs-lookup"><span data-stu-id="178c0-197">Aliases</span></span> | <span data-ttu-id="178c0-198">Geen</span><span class="sxs-lookup"><span data-stu-id="178c0-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="178c0-199">Vereist?</span><span class="sxs-lookup"><span data-stu-id="178c0-199">Required?</span></span> |<span data-ttu-id="178c0-200">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-200">false</span></span> |
| <span data-ttu-id="178c0-201">Positie</span><span class="sxs-lookup"><span data-stu-id="178c0-201">Position</span></span> |<span data-ttu-id="178c0-202">Met de naam</span><span class="sxs-lookup"><span data-stu-id="178c0-202">named</span></span> |
| <span data-ttu-id="178c0-203">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="178c0-203">Default value</span></span> |<span data-ttu-id="178c0-204">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-204">false</span></span> |
| <span data-ttu-id="178c0-205">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-205">Accept pipeline input?</span></span> |<span data-ttu-id="178c0-206">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-206">false</span></span> |
| <span data-ttu-id="178c0-207">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="178c0-207">Accept wildcard characters?</span></span> |<span data-ttu-id="178c0-208">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="178c0-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="178c0-209">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="178c0-209">Remarks</span></span>
<span data-ttu-id="178c0-210">Voor een volledige beschrijving van hoe toouse Hallo script toocreate Dev- en testomgevingen, Zie [tooPublish tooDev van Windows PowerShell-Scripts en testomgevingen](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="178c0-210">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="178c0-211">Hallo JSON-configuratiebestand geeft details over Hallo van wat toobe geïmplementeerd is.</span><span class="sxs-lookup"><span data-stu-id="178c0-211">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="178c0-212">Deze bevat Hallo-informatie die u hebt opgegeven toen u Hallo-project, zoals het Hallo-naam, affiniteitsgroep, VHD-installatiekopie en grootte van Hallo virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="178c0-212">It includes hello information that you specified when you created hello project, such as hello name, affinity group, VHD image, and size of hello virtual machine.</span></span> <span data-ttu-id="178c0-213">Ook bevat Hallo-eindpunten op Hallo virtuele machine, Hallo databases tooprovision, indien van toepassing en web-implementatieparameters.</span><span class="sxs-lookup"><span data-stu-id="178c0-213">It also includes hello endpoints on hello virtual machine, hello databases tooprovision, if any, and web deployment parameters.</span></span> <span data-ttu-id="178c0-214">Hallo volgende code toont een voorbeeld van de JSON-configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="178c0-214">hello following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="178c0-215">Hallo JSON configuration file toochange wat is ingericht, kunt u bewerken.</span><span class="sxs-lookup"><span data-stu-id="178c0-215">You can edit hello JSON configuration file toochange what is provisioned.</span></span> <span data-ttu-id="178c0-216">Een virtuele machine en een cloudservice zijn vereist, maar Hallo database sectie is optioneel.</span><span class="sxs-lookup"><span data-stu-id="178c0-216">A virtual machine and a cloud service are required, but hello database section is optional.</span></span>

