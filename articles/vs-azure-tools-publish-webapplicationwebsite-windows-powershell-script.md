---
title: aaaPublish-WebApplicationWebSite (Windows PowerShell-script) | Microsoft Docs
description: Meer informatie over hoe toopublish een web project tooan Azure-website. Dit script maakt Hallo vereist resources in uw Azure-abonnement als deze nog niet bestaan.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="e16e7-104">Publiceren WebApplicationWebSite (Windows PowerShell-script)</span><span class="sxs-lookup"><span data-stu-id="e16e7-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="e16e7-105">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="e16e7-105">Syntax</span></span>
<span data-ttu-id="e16e7-106">Een web project tooan Azure-website publiceert.</span><span class="sxs-lookup"><span data-stu-id="e16e7-106">Publishes a web project tooan Azure website.</span></span> <span data-ttu-id="e16e7-107">Hallo script maakt Hallo vereist resources in uw Azure-abonnement als deze nog niet bestaan.</span><span class="sxs-lookup"><span data-stu-id="e16e7-107">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="e16e7-108">Configuratie</span><span class="sxs-lookup"><span data-stu-id="e16e7-108">Configuration</span></span>
<span data-ttu-id="e16e7-109">Hallo pad toohello JSON-configuratiebestand dat Hallo details van Hallo implementatie beschrijft.</span><span class="sxs-lookup"><span data-stu-id="e16e7-109">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="e16e7-110">Parameter</span><span class="sxs-lookup"><span data-stu-id="e16e7-110">Parameter</span></span> | <span data-ttu-id="e16e7-111">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="e16e7-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="e16e7-112">Aliassen</span><span class="sxs-lookup"><span data-stu-id="e16e7-112">Aliases</span></span> |<span data-ttu-id="e16e7-113">Geen</span><span class="sxs-lookup"><span data-stu-id="e16e7-113">none</span></span> |
| <span data-ttu-id="e16e7-114">Vereist?</span><span class="sxs-lookup"><span data-stu-id="e16e7-114">Required?</span></span> |<span data-ttu-id="e16e7-115">De waarde True</span><span class="sxs-lookup"><span data-stu-id="e16e7-115">true</span></span> |
| <span data-ttu-id="e16e7-116">Positie</span><span class="sxs-lookup"><span data-stu-id="e16e7-116">Position</span></span> |<span data-ttu-id="e16e7-117">Met de naam</span><span class="sxs-lookup"><span data-stu-id="e16e7-117">named</span></span> |
| <span data-ttu-id="e16e7-118">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="e16e7-118">Default value</span></span> |<span data-ttu-id="e16e7-119">Geen</span><span class="sxs-lookup"><span data-stu-id="e16e7-119">none</span></span> |
| <span data-ttu-id="e16e7-120">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="e16e7-120">Accept pipeline input?</span></span> |<span data-ttu-id="e16e7-121">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-121">false</span></span> |
| <span data-ttu-id="e16e7-122">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="e16e7-122">Accept wildcard characters?</span></span> |<span data-ttu-id="e16e7-123">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="e16e7-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="e16e7-124">SubscriptionName</span></span>
<span data-ttu-id="e16e7-125">Hallo-naam van hello Azure-abonnement dat u wilt dat toocreate Hallo website in.</span><span class="sxs-lookup"><span data-stu-id="e16e7-125">hello name of hello Azure subscription that you want toocreate hello website in.</span></span>

| <span data-ttu-id="e16e7-126">Parameter</span><span class="sxs-lookup"><span data-stu-id="e16e7-126">Parameter</span></span> | <span data-ttu-id="e16e7-127">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="e16e7-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="e16e7-128">Aliassen</span><span class="sxs-lookup"><span data-stu-id="e16e7-128">Aliases</span></span> |<span data-ttu-id="e16e7-129">Geen</span><span class="sxs-lookup"><span data-stu-id="e16e7-129">none</span></span> |
| <span data-ttu-id="e16e7-130">Vereist?</span><span class="sxs-lookup"><span data-stu-id="e16e7-130">Required?</span></span> |<span data-ttu-id="e16e7-131">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-131">false</span></span> |
| <span data-ttu-id="e16e7-132">Positie</span><span class="sxs-lookup"><span data-stu-id="e16e7-132">Position</span></span> |<span data-ttu-id="e16e7-133">Met de naam</span><span class="sxs-lookup"><span data-stu-id="e16e7-133">named</span></span> |
| <span data-ttu-id="e16e7-134">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="e16e7-134">Default value</span></span> |<span data-ttu-id="e16e7-135">Geen</span><span class="sxs-lookup"><span data-stu-id="e16e7-135">none</span></span> |
| <span data-ttu-id="e16e7-136">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="e16e7-136">Accept pipeline input?</span></span> |<span data-ttu-id="e16e7-137">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-137">false</span></span> |
| <span data-ttu-id="e16e7-138">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="e16e7-138">Accept wildcard characters?</span></span> |<span data-ttu-id="e16e7-139">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="e16e7-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="e16e7-140">WebDeployPackage</span></span>
<span data-ttu-id="e16e7-141">Hallo pad toohello web deployment pakket toopublish toohello website.</span><span class="sxs-lookup"><span data-stu-id="e16e7-141">hello path toohello web deployment package toopublish toohello website.</span></span> <span data-ttu-id="e16e7-142">U kunt dit pakket kunt maken met behulp van de wizard webpublicatie Hallo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e16e7-142">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="e16e7-143">Zie voor meer informatie [aan de slag met Azure Cloud Services en ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="e16e7-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="e16e7-144">Parameter</span><span class="sxs-lookup"><span data-stu-id="e16e7-144">Parameter</span></span> | <span data-ttu-id="e16e7-145">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="e16e7-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="e16e7-146">Aliassen</span><span class="sxs-lookup"><span data-stu-id="e16e7-146">Aliases</span></span> |<span data-ttu-id="e16e7-147">Geen</span><span class="sxs-lookup"><span data-stu-id="e16e7-147">none</span></span> |
| <span data-ttu-id="e16e7-148">Vereist?</span><span class="sxs-lookup"><span data-stu-id="e16e7-148">Required?</span></span> |<span data-ttu-id="e16e7-149">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-149">false</span></span> |
| <span data-ttu-id="e16e7-150">Positie</span><span class="sxs-lookup"><span data-stu-id="e16e7-150">Position</span></span> |<span data-ttu-id="e16e7-151">Met de naam</span><span class="sxs-lookup"><span data-stu-id="e16e7-151">named</span></span> |
| <span data-ttu-id="e16e7-152">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="e16e7-152">Default value</span></span> |<span data-ttu-id="e16e7-153">Geen</span><span class="sxs-lookup"><span data-stu-id="e16e7-153">none</span></span> |
| <span data-ttu-id="e16e7-154">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="e16e7-154">Accept pipeline input?</span></span> |<span data-ttu-id="e16e7-155">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-155">false</span></span> |
| <span data-ttu-id="e16e7-156">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="e16e7-156">Accept wildcard characters?</span></span> |<span data-ttu-id="e16e7-157">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="e16e7-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="e16e7-158">DatabaseServerPassword</span></span>
<span data-ttu-id="e16e7-159">Hallo-gebruikersnaam en wachtwoord voor Hallo SQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="e16e7-159">hello username and password for hello SQL database in Azure.</span></span>

| <span data-ttu-id="e16e7-160">Parameter</span><span class="sxs-lookup"><span data-stu-id="e16e7-160">Parameter</span></span> | <span data-ttu-id="e16e7-161">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="e16e7-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="e16e7-162">Aliassen</span><span class="sxs-lookup"><span data-stu-id="e16e7-162">Aliases</span></span> |<span data-ttu-id="e16e7-163">Geen</span><span class="sxs-lookup"><span data-stu-id="e16e7-163">none</span></span> |
| <span data-ttu-id="e16e7-164">Vereist?</span><span class="sxs-lookup"><span data-stu-id="e16e7-164">Required?</span></span> |<span data-ttu-id="e16e7-165">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-165">false</span></span> |
| <span data-ttu-id="e16e7-166">Positie</span><span class="sxs-lookup"><span data-stu-id="e16e7-166">Position</span></span> |<span data-ttu-id="e16e7-167">Met de naam</span><span class="sxs-lookup"><span data-stu-id="e16e7-167">named</span></span> |
| <span data-ttu-id="e16e7-168">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="e16e7-168">Default value</span></span> |<span data-ttu-id="e16e7-169">Geen</span><span class="sxs-lookup"><span data-stu-id="e16e7-169">none</span></span> |
| <span data-ttu-id="e16e7-170">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="e16e7-170">Accept pipeline input?</span></span> |<span data-ttu-id="e16e7-171">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-171">false</span></span> |
| <span data-ttu-id="e16e7-172">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="e16e7-172">Accept wildcard characters?</span></span> |<span data-ttu-id="e16e7-173">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="e16e7-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="e16e7-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="e16e7-175">Indien waar, uitvoer afdrukken berichten van Hallo script toohello stroom.</span><span class="sxs-lookup"><span data-stu-id="e16e7-175">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="e16e7-176">Parameter</span><span class="sxs-lookup"><span data-stu-id="e16e7-176">Parameter</span></span> | <span data-ttu-id="e16e7-177">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="e16e7-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="e16e7-178">Aliassen</span><span class="sxs-lookup"><span data-stu-id="e16e7-178">Aliases</span></span> |<span data-ttu-id="e16e7-179">Geen</span><span class="sxs-lookup"><span data-stu-id="e16e7-179">none</span></span> |
| <span data-ttu-id="e16e7-180">Vereist?</span><span class="sxs-lookup"><span data-stu-id="e16e7-180">Required?</span></span> |<span data-ttu-id="e16e7-181">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-181">false</span></span> |
| <span data-ttu-id="e16e7-182">Positie</span><span class="sxs-lookup"><span data-stu-id="e16e7-182">Position</span></span> |<span data-ttu-id="e16e7-183">Met de naam</span><span class="sxs-lookup"><span data-stu-id="e16e7-183">named</span></span> |
| <span data-ttu-id="e16e7-184">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="e16e7-184">Default value</span></span> |<span data-ttu-id="e16e7-185">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-185">false</span></span> |
| <span data-ttu-id="e16e7-186">Pijpleidinginvoer accepteren?</span><span class="sxs-lookup"><span data-stu-id="e16e7-186">Accept pipeline input?</span></span> |<span data-ttu-id="e16e7-187">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-187">false</span></span> |
| <span data-ttu-id="e16e7-188">Jokertekens accepteren?</span><span class="sxs-lookup"><span data-stu-id="e16e7-188">Accept wildcard characters?</span></span> |<span data-ttu-id="e16e7-189">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="e16e7-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="e16e7-190">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="e16e7-190">Remarks</span></span>
<span data-ttu-id="e16e7-191">Voor een volledige beschrijving van hoe toouse Hallo script toocreate Dev- en testomgevingen, Zie [tooPublish tooDev van Windows PowerShell-Scripts en testomgevingen](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="e16e7-191">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="e16e7-192">Hallo JSON-configuratiebestand geeft details over Hallo van wat toobe geïmplementeerd is.</span><span class="sxs-lookup"><span data-stu-id="e16e7-192">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="e16e7-193">Het bevat Hallo-informatie die u hebt opgegeven tijdens het maken van Hallo-project, zoals Hallo naam- en gebruikersnaam voor Hallo website.</span><span class="sxs-lookup"><span data-stu-id="e16e7-193">It includes hello information that you specified when you created hello project, such as hello name and username for hello website.</span></span> <span data-ttu-id="e16e7-194">Dit omvat ook Hallo database tooprovision, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="e16e7-194">It also includes hello database tooprovision, if any.</span></span> <span data-ttu-id="e16e7-195">Hallo volgende code toont een voorbeeld van de JSON-configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="e16e7-195">hello following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="e16e7-196">Hallo JSON configuration file toochange wat wordt geïmplementeerd, kunt u bewerken.</span><span class="sxs-lookup"><span data-stu-id="e16e7-196">You can edit hello JSON configuration file toochange what is deployed.</span></span> <span data-ttu-id="e16e7-197">Een gedeelte van de webSite is vereist, maar Hallo database sectie is optioneel.</span><span class="sxs-lookup"><span data-stu-id="e16e7-197">A webSite section is required, but hello database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e16e7-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e16e7-198">Next steps</span></span>
<span data-ttu-id="e16e7-199">Zie voor meer informatie [publiceren-WebApplicationVM (Windows PowerShell-script)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="e16e7-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

