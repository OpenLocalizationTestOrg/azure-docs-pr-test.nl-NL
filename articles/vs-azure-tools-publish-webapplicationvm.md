---
title: Publiceren WebApplicationVM | Microsoft Docs
description: Informatie over het implementeren van een webtoepassing met een virtuele machine. Dit script maakt de vereiste resources in uw Azure-abonnement als deze nog niet bestaan.
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
ms.openlocfilehash: 2738fc1dff50a177a227ae2c7719bd9a192d82ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="07a40-104">Publiceren WebApplicationVM (Windows PowerShell-script)</span><span class="sxs-lookup"><span data-stu-id="07a40-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="07a40-105">Een webtoepassing met een virtuele machine implementeert.</span><span class="sxs-lookup"><span data-stu-id="07a40-105">Deploys a web application to a virtual machine.</span></span> <span data-ttu-id="07a40-106">Het script maakt de vereiste resources in uw Azure-abonnement als deze nog niet bestaan.</span><span class="sxs-lookup"><span data-stu-id="07a40-106">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

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

### <a name="configuration"></a><span data-ttu-id="07a40-107">Configuratie</span><span class="sxs-lookup"><span data-stu-id="07a40-107">Configuration</span></span>
<span data-ttu-id="07a40-108">Het pad naar het JSON-configuratiebestand dat u de details van de implementatie worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="07a40-108">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="07a40-109">Aliassen</span><span class="sxs-lookup"><span data-stu-id="07a40-109">Aliases</span></span> | <span data-ttu-id="07a40-110">Geen</span><span class="sxs-lookup"><span data-stu-id="07a40-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="07a40-111">Vereist?</span><span class="sxs-lookup"><span data-stu-id="07a40-111">Required?</span></span> |<span data-ttu-id="07a40-112">De waarde True</span><span class="sxs-lookup"><span data-stu-id="07a40-112">true</span></span> |
| <span data-ttu-id="07a40-113">Positie</span><span class="sxs-lookup"><span data-stu-id="07a40-113">Position</span></span> |<span data-ttu-id="07a40-114">Met de naam</span><span class="sxs-lookup"><span data-stu-id="07a40-114">named</span></span> |
| <span data-ttu-id="07a40-115">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="07a40-115">Default value</span></span> |<span data-ttu-id="07a40-116">Geen</span><span class="sxs-lookup"><span data-stu-id="07a40-116">none</span></span> |
| <span data-ttu-id="07a40-117">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-117">Accept pipeline input?</span></span> |<span data-ttu-id="07a40-118">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-118">false</span></span> |
| <span data-ttu-id="07a40-119">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-119">Accept wildcard characters?</span></span> |<span data-ttu-id="07a40-120">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="07a40-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="07a40-121">SubscriptionName</span></span>
<span data-ttu-id="07a40-122">De naam van het Azure-abonnement waarin u wilt maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07a40-122">The name of the Azure subscription in which you want to create the virtual machine.</span></span>

| <span data-ttu-id="07a40-123">Aliassen</span><span class="sxs-lookup"><span data-stu-id="07a40-123">Aliases</span></span> | <span data-ttu-id="07a40-124">Geen</span><span class="sxs-lookup"><span data-stu-id="07a40-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="07a40-125">Vereist?</span><span class="sxs-lookup"><span data-stu-id="07a40-125">Required?</span></span> |<span data-ttu-id="07a40-126">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-126">false</span></span> |
| <span data-ttu-id="07a40-127">Positie</span><span class="sxs-lookup"><span data-stu-id="07a40-127">Position</span></span> |<span data-ttu-id="07a40-128">Met de naam</span><span class="sxs-lookup"><span data-stu-id="07a40-128">named</span></span> |
| <span data-ttu-id="07a40-129">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="07a40-129">Default value</span></span> |<span data-ttu-id="07a40-130">Maakt gebruik van het eerste abonnement in het abonnementsbestand</span><span class="sxs-lookup"><span data-stu-id="07a40-130">Uses the first subscription in the subscription file</span></span> |
| <span data-ttu-id="07a40-131">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-131">Accept pipeline input?</span></span> |<span data-ttu-id="07a40-132">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-132">false</span></span> |
| <span data-ttu-id="07a40-133">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-133">Accept wildcard characters?</span></span> |<span data-ttu-id="07a40-134">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="07a40-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="07a40-135">WebDeployPackage</span></span>
<span data-ttu-id="07a40-136">Het pad naar het implementatiepakket web publiceren naar de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07a40-136">The path to the web deployment package to publish to the virtual machine.</span></span> <span data-ttu-id="07a40-137">U kunt dit pakket kunt maken met behulp van de wizard webpublicatie in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07a40-137">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="07a40-138">Zie [procedure: een Web-implementatiepakket maken in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="07a40-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="07a40-139">Aliassen</span><span class="sxs-lookup"><span data-stu-id="07a40-139">Aliases</span></span> | <span data-ttu-id="07a40-140">Geen</span><span class="sxs-lookup"><span data-stu-id="07a40-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="07a40-141">Vereist?</span><span class="sxs-lookup"><span data-stu-id="07a40-141">Required?</span></span> |<span data-ttu-id="07a40-142">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-142">false</span></span> |
| <span data-ttu-id="07a40-143">Positie</span><span class="sxs-lookup"><span data-stu-id="07a40-143">Position</span></span> |<span data-ttu-id="07a40-144">Met de naam</span><span class="sxs-lookup"><span data-stu-id="07a40-144">named</span></span> |
| <span data-ttu-id="07a40-145">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="07a40-145">Default value</span></span> |<span data-ttu-id="07a40-146">Geen</span><span class="sxs-lookup"><span data-stu-id="07a40-146">none</span></span> |
| <span data-ttu-id="07a40-147">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-147">Accept pipeline input?</span></span> |<span data-ttu-id="07a40-148">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-148">false</span></span> |
| <span data-ttu-id="07a40-149">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-149">Accept wildcard characters?</span></span> |<span data-ttu-id="07a40-150">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="07a40-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="07a40-151">AllowUntrusted</span></span>
<span data-ttu-id="07a40-152">Indien waar, wordt het gebruik van certificaten die niet zijn ondertekend door een vertrouwde basiscertificeringsinstantie toestaan.</span><span class="sxs-lookup"><span data-stu-id="07a40-152">If true, allow the use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="07a40-153">Aliassen</span><span class="sxs-lookup"><span data-stu-id="07a40-153">Aliases</span></span> | <span data-ttu-id="07a40-154">Geen</span><span class="sxs-lookup"><span data-stu-id="07a40-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="07a40-155">Vereist?</span><span class="sxs-lookup"><span data-stu-id="07a40-155">Required?</span></span> |<span data-ttu-id="07a40-156">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-156">false</span></span> |
| <span data-ttu-id="07a40-157">Positie</span><span class="sxs-lookup"><span data-stu-id="07a40-157">Position</span></span> |<span data-ttu-id="07a40-158">Met de naam</span><span class="sxs-lookup"><span data-stu-id="07a40-158">named</span></span> |
| <span data-ttu-id="07a40-159">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="07a40-159">Default value</span></span> |<span data-ttu-id="07a40-160">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-160">false</span></span> |
| <span data-ttu-id="07a40-161">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-161">Accept pipeline input?</span></span> |<span data-ttu-id="07a40-162">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-162">false</span></span> |
| <span data-ttu-id="07a40-163">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-163">Accept wildcard characters?</span></span> |<span data-ttu-id="07a40-164">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="07a40-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="07a40-165">VMPassword</span></span>
<span data-ttu-id="07a40-166">De referenties voor de account van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="07a40-166">The credentials for the virtual machine account.</span></span> <span data-ttu-id="07a40-167">Voorbeeld: - VMPassword @{naam = 'admin'; Wachtwoord = 'password'}</span><span class="sxs-lookup"><span data-stu-id="07a40-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="07a40-168">Aliassen</span><span class="sxs-lookup"><span data-stu-id="07a40-168">Aliases</span></span> | <span data-ttu-id="07a40-169">Geen</span><span class="sxs-lookup"><span data-stu-id="07a40-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="07a40-170">Vereist?</span><span class="sxs-lookup"><span data-stu-id="07a40-170">Required?</span></span> |<span data-ttu-id="07a40-171">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-171">false</span></span> |
| <span data-ttu-id="07a40-172">Positie</span><span class="sxs-lookup"><span data-stu-id="07a40-172">Position</span></span> |<span data-ttu-id="07a40-173">Met de naam</span><span class="sxs-lookup"><span data-stu-id="07a40-173">named</span></span> |
| <span data-ttu-id="07a40-174">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="07a40-174">Default value</span></span> |<span data-ttu-id="07a40-175">Geen</span><span class="sxs-lookup"><span data-stu-id="07a40-175">none</span></span> |
| <span data-ttu-id="07a40-176">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-176">Accept pipeline input?</span></span> |<span data-ttu-id="07a40-177">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-177">false</span></span> |
| <span data-ttu-id="07a40-178">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-178">Accept wildcard characters?</span></span> |<span data-ttu-id="07a40-179">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="07a40-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="07a40-180">DatabaseServerPassword</span></span>
<span data-ttu-id="07a40-181">De referenties voor de SQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="07a40-181">The credentials for the SQL database in Azure.</span></span> <span data-ttu-id="07a40-182">Voorbeeld: - DatabaseServerPassword @{naam = 'admin'; Wachtwoord = 'password'}</span><span class="sxs-lookup"><span data-stu-id="07a40-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="07a40-183">Aliassen</span><span class="sxs-lookup"><span data-stu-id="07a40-183">Aliases</span></span> | <span data-ttu-id="07a40-184">Geen</span><span class="sxs-lookup"><span data-stu-id="07a40-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="07a40-185">Vereist?</span><span class="sxs-lookup"><span data-stu-id="07a40-185">Required?</span></span> |<span data-ttu-id="07a40-186">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-186">false</span></span> |
| <span data-ttu-id="07a40-187">Positie</span><span class="sxs-lookup"><span data-stu-id="07a40-187">Position</span></span> |<span data-ttu-id="07a40-188">Met de naam</span><span class="sxs-lookup"><span data-stu-id="07a40-188">named</span></span> |
| <span data-ttu-id="07a40-189">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="07a40-189">Default value</span></span> |<span data-ttu-id="07a40-190">Geen</span><span class="sxs-lookup"><span data-stu-id="07a40-190">none</span></span> |
| <span data-ttu-id="07a40-191">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-191">Accept pipeline input?</span></span> |<span data-ttu-id="07a40-192">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-192">false</span></span> |
| <span data-ttu-id="07a40-193">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-193">Accept wildcard characters?</span></span> |<span data-ttu-id="07a40-194">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="07a40-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="07a40-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="07a40-196">Indien waar, wordt de status van afdrukken berichten van het script naar de uitvoerstroom.</span><span class="sxs-lookup"><span data-stu-id="07a40-196">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="07a40-197">Aliassen</span><span class="sxs-lookup"><span data-stu-id="07a40-197">Aliases</span></span> | <span data-ttu-id="07a40-198">Geen</span><span class="sxs-lookup"><span data-stu-id="07a40-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="07a40-199">Vereist?</span><span class="sxs-lookup"><span data-stu-id="07a40-199">Required?</span></span> |<span data-ttu-id="07a40-200">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-200">false</span></span> |
| <span data-ttu-id="07a40-201">Positie</span><span class="sxs-lookup"><span data-stu-id="07a40-201">Position</span></span> |<span data-ttu-id="07a40-202">Met de naam</span><span class="sxs-lookup"><span data-stu-id="07a40-202">named</span></span> |
| <span data-ttu-id="07a40-203">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="07a40-203">Default value</span></span> |<span data-ttu-id="07a40-204">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-204">false</span></span> |
| <span data-ttu-id="07a40-205">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-205">Accept pipeline input?</span></span> |<span data-ttu-id="07a40-206">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-206">false</span></span> |
| <span data-ttu-id="07a40-207">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="07a40-207">Accept wildcard characters?</span></span> |<span data-ttu-id="07a40-208">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="07a40-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="07a40-209">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="07a40-209">Remarks</span></span>
<span data-ttu-id="07a40-210">Zie voor een volledige uitleg over het gebruik van het script maken Dev- en testomgevingen, [Windows PowerShell-Scripts gebruiken om te publiceren op de ontwikkeling en testomgevingen](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="07a40-210">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="07a40-211">Het JSON-configuratiebestand geeft de details van wat is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="07a40-211">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="07a40-212">Deze bevat de informatie die u hebt opgegeven toen u het project, zoals de naam, de affiniteitsgroep, de VHD-installatiekopie en de grootte van de virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="07a40-212">It includes the information that you specified when you created the project, such as the name, affinity group, VHD image, and size of the virtual machine.</span></span> <span data-ttu-id="07a40-213">Ook bevat de eindpunten van de virtuele machine en de databases naar inricht, indien van toepassing en implementatieparameters van web.</span><span class="sxs-lookup"><span data-stu-id="07a40-213">It also includes the endpoints on the virtual machine, the databases to provision, if any, and web deployment parameters.</span></span> <span data-ttu-id="07a40-214">De volgende code toont een voorbeeld van de JSON-configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="07a40-214">The following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="07a40-215">U kunt het JSON-configuratiebestand om te wijzigen wat is ingericht bewerken.</span><span class="sxs-lookup"><span data-stu-id="07a40-215">You can edit the JSON configuration file to change what is provisioned.</span></span> <span data-ttu-id="07a40-216">Een virtuele machine en een cloudservice zijn vereist, maar de database-sectie is optioneel.</span><span class="sxs-lookup"><span data-stu-id="07a40-216">A virtual machine and a cloud service are required, but the database section is optional.</span></span>

