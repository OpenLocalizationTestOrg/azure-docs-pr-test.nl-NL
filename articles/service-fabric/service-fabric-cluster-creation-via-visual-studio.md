---
title: aaaSetting van een Service Fabric-cluster met behulp van Visual Studio | Microsoft Docs
description: Hierin wordt beschreven hoe tooset van een Service Fabric-cluster met behulp van Azure Resource Manager-sjabloon is gemaakt door een Azure Resource Group-project in Visual Studio
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="39464-103">Een Service Fabric-cluster instellen met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="39464-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="39464-104">Dit artikel wordt beschreven hoe tooset van een Azure Service Fabric-cluster met behulp van Visual Studio en een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="39464-104">This article describes how tooset up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="39464-105">Een Visual Studio Azure resource group toocreate Hallo projectsjabloon zullen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="39464-105">We will use a Visual Studio Azure resource group project toocreate hello template.</span></span> <span data-ttu-id="39464-106">Nadat het Hallo-sjabloon is gemaakt, kan worden geïmplementeerd rechtstreeks tooAzure vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="39464-106">After hello template has been created, it can be deployed directly tooAzure from Visual Studio.</span></span> <span data-ttu-id="39464-107">Het kan ook worden gebruikt vanuit een script of als onderdeel van de faciliteit continue integratie (CI).</span><span class="sxs-lookup"><span data-stu-id="39464-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="39464-108">Een sjabloon voor Service Fabric-cluster met behulp van een Azure-resourcegroepproject maken</span><span class="sxs-lookup"><span data-stu-id="39464-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="39464-109">tooget gestart, opent u Visual Studio en maak een Azure-resourcegroepproject (beschikbaar in Hallo **Cloud** map):</span><span class="sxs-lookup"><span data-stu-id="39464-109">tooget started, open Visual Studio and create an Azure resource group project (it is available in hello **Cloud** folder):</span></span>

![Het dialoogvenster Nieuw Project met de Azure-resourcegroepproject geselecteerd][1]

<span data-ttu-id="39464-111">U kunt een nieuwe Visual Studio-oplossing voor dit project maken of bestaande oplossing tooan toevoegen.</span><span class="sxs-lookup"><span data-stu-id="39464-111">You can create a new Visual Studio solution for this project or add it tooan existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="39464-112">Als u de Azure resourcegroepproject Hallo onder Hallo Cloud knooppunt niet ziet, hebt u geen hello Azure SDK is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="39464-112">If you do not see hello Azure resource group project under hello Cloud node, you do not have hello Azure SDK installed.</span></span> <span data-ttu-id="39464-113">Starten van de Web Platform Installer ([nu installeren](http://www.microsoft.com/web/downloads/platform.aspx) als u nog niet gedaan hebt), en zoek naar 'Azure SDK voor .NET' en installeer Hallo-versie die compatibel is met uw versie van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="39464-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install hello version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="39464-114">Nadat u de knop OK voor Hallo raakt, wordt Visual Studio u gevraagd tooselect Hallo Resource Manager-sjabloon die u wilt dat toocreate:</span><span class="sxs-lookup"><span data-stu-id="39464-114">After you hit hello OK button, Visual Studio will ask you tooselect hello Resource Manager template you want toocreate:</span></span>

![Dialoogvenster van de Azure-sjabloon selecteren met de geselecteerde sjabloon voor Service Fabric-Cluster][2]

<span data-ttu-id="39464-116">Selecteer Hallo Service Fabric-Cluster sjabloon en treffers Hallo OK knop opnieuw.</span><span class="sxs-lookup"><span data-stu-id="39464-116">Select hello Service Fabric Cluster template and hit hello OK button again.</span></span> <span data-ttu-id="39464-117">Hallo-project en Hallo Resource Manager-sjabloon hebt nu gemaakt.</span><span class="sxs-lookup"><span data-stu-id="39464-117">hello project and hello Resource Manager template have now been created.</span></span>

## <a name="prepare-hello-template-for-deployment"></a><span data-ttu-id="39464-118">Hallo-sjabloon voor de implementatie voorbereiden</span><span class="sxs-lookup"><span data-stu-id="39464-118">Prepare hello template for deployment</span></span>
<span data-ttu-id="39464-119">Voordat het Hallo-sjabloon is geïmplementeerde toocreate Hallo cluster, moet u waarden opgeven voor de sjabloonparameters Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="39464-119">Before hello template is deployed toocreate hello cluster, you must provide values for hello required template parameters.</span></span> <span data-ttu-id="39464-120">Deze parameterwaarden worden gelezen uit Hallo `ServiceFabricCluster.parameters.json` bestand, dat zich in Hallo bevindt `Templates` map van het resourcegroepproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="39464-120">These parameter values are read from hello `ServiceFabricCluster.parameters.json` file, which is in hello `Templates` folder of hello resource group project.</span></span> <span data-ttu-id="39464-121">Hallo-bestand openen en geef Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="39464-121">Open hello file and provide hello following values:</span></span>

| <span data-ttu-id="39464-122">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="39464-122">Parameter name</span></span> | <span data-ttu-id="39464-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="39464-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="39464-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="39464-124">adminUserName</span></span> |<span data-ttu-id="39464-125">Hallo-naam van Hallo administrator-account voor Service Fabric-machines (knooppunten).</span><span class="sxs-lookup"><span data-stu-id="39464-125">hello name of hello administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="39464-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="39464-126">certificateThumbprint</span></span> |<span data-ttu-id="39464-127">Hallo vingerafdruk van certificaat Hallo Hallo cluster beveiligt.</span><span class="sxs-lookup"><span data-stu-id="39464-127">hello thumbprint of hello certificate that secures hello cluster.</span></span> |
| <span data-ttu-id="39464-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="39464-128">sourceVaultResourceId</span></span> |<span data-ttu-id="39464-129">Hallo *resource-ID* van Hallo sleutelkluis waar Hallo-certificaat dat Hallo cluster beveiligt wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="39464-129">hello *resource ID* of hello key vault where hello certificate that secures hello cluster is stored.</span></span> |
| <span data-ttu-id="39464-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="39464-130">certificateUrlValue</span></span> |<span data-ttu-id="39464-131">Hallo-URL van beveiligingscertificaat Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="39464-131">hello URL of hello cluster security certificate.</span></span> |

<span data-ttu-id="39464-132">Hallo Visual Studio Service Fabric Resource Manager-sjabloon maakt u een beveiligde cluster dat wordt beveiligd door een certificaat.</span><span class="sxs-lookup"><span data-stu-id="39464-132">hello Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="39464-133">Dit certificaat wordt geïdentificeerd door Hallo laatste drie sjabloonparameters (`certificateThumbprint`, `sourceVaultValue`, en `certificateUrlValue`), en deze moet bestaan in een **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="39464-133">This certificate is identified by hello last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="39464-134">Zie voor meer informatie over hoe toocreate cluster beveiligingscertificaat hello, [scenario's voor beveiliging van Service Fabric-cluster](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) artikel.</span><span class="sxs-lookup"><span data-stu-id="39464-134">For more information on how toocreate hello cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-hello-cluster-name"></a><span data-ttu-id="39464-135">Optioneel: Wijzig de naam van de cluster Hallo</span><span class="sxs-lookup"><span data-stu-id="39464-135">Optional: change hello cluster name</span></span>
<span data-ttu-id="39464-136">Elke Service Fabric-cluster heeft een naam.</span><span class="sxs-lookup"><span data-stu-id="39464-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="39464-137">Wanneer een Fabric-cluster is gemaakt in Azure, clusternaam (samen met hello Azure-regio) bepaalt Hallo Domain Name System (DNS)-naam voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="39464-137">When a Fabric cluster is created in Azure, cluster name determines (together with hello Azure region) hello Domain Name System (DNS) name for hello cluster.</span></span> <span data-ttu-id="39464-138">Bijvoorbeeld, als u uw cluster naam `myBigCluster`, en Hallo locatie (Azure-regio) van de resourcegroep Hallo die als host voor het nieuwe cluster Hallo fungeert VS-Oost, is Hallo DNS-naam van de cluster Hallo `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="39464-138">For example, if you name your cluster `myBigCluster`, and hello location (Azure region) of hello resource group that will host hello new cluster is East US, hello DNS name of hello cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="39464-139">Standaard Hallo clusternaam automatisch gegenereerd en door het koppelen van een willekeurig achtervoegsel tooa 'cluster' voorvoegsel uniek gemaakt.</span><span class="sxs-lookup"><span data-stu-id="39464-139">By default hello cluster name is generated automatically and made unique by attaching a random suffix tooa "cluster" prefix.</span></span> <span data-ttu-id="39464-140">Dit maakt het heel eenvoudig toouse Hallo sjabloon als onderdeel van een **continue integratie** (CI) systeem.</span><span class="sxs-lookup"><span data-stu-id="39464-140">This makes it very easy toouse hello template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="39464-141">Als u wilt dat toouse een specifieke naam voor uw cluster, een zinvolle tooyou Hallo waarde Hallo `clusterName` variabele in Hallo Resource Manager-sjabloonbestand (`ServiceFabricCluster.json`) tooyour gekozen naam.</span><span class="sxs-lookup"><span data-stu-id="39464-141">If you want toouse a specific name for your cluster, one that is meaningful tooyou, set hello value of hello `clusterName` variable in hello Resource Manager template file (`ServiceFabricCluster.json`) tooyour chosen name.</span></span> <span data-ttu-id="39464-142">Is het eerste Hallo-variabele gedefinieerd in dat bestand.</span><span class="sxs-lookup"><span data-stu-id="39464-142">It is hello first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="39464-143">Optioneel: openbare toepassing poorten toevoegen</span><span class="sxs-lookup"><span data-stu-id="39464-143">Optional: add public application ports</span></span>
<span data-ttu-id="39464-144">U kunt ook toochange Hallo openbare toepassing poorten voor Hallo cluster voordat u deze implementeert.</span><span class="sxs-lookup"><span data-stu-id="39464-144">You may also want toochange hello public application ports for hello cluster before you deploy it.</span></span> <span data-ttu-id="39464-145">Standaard wordt Hallo sjabloon geopend slechts twee openbare TCP-poorten (80 en 8081).</span><span class="sxs-lookup"><span data-stu-id="39464-145">By default, hello template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="39464-146">Als u meer voor uw toepassingen moet, wijzigt u hello Azure Load Balancer-definitie in Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="39464-146">If you need more for your applications, modify hello Azure Load Balancer definition in hello template.</span></span> <span data-ttu-id="39464-147">Hallo-definitie wordt opgeslagen in de belangrijkste sjabloonbestand hello (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="39464-147">hello definition is stored in hello main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="39464-148">Open dit bestand en zoek naar `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="39464-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="39464-149">Elke poort is gekoppeld aan de drie onderdelen:</span><span class="sxs-lookup"><span data-stu-id="39464-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="39464-150">Een sjabloonvariabele die Hallo TCP-poortwaarde voor Hallo-poort definieert:</span><span class="sxs-lookup"><span data-stu-id="39464-150">A template variable that defines hello TCP port value for hello port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="39464-151">Een *test* die definieert hoe vaak en hoe lang hello Azure load balancer toouse een specifieke Service Fabric-knooppunt voordat deze is mislukt via tooanother een probeert.</span><span class="sxs-lookup"><span data-stu-id="39464-151">A *probe* that defines how frequently and for how long hello Azure load balancer attempts toouse a specific Service Fabric node before failing over tooanother one.</span></span> <span data-ttu-id="39464-152">Hallo-tests uitmaken deel van Hallo Load Balancer-resource.</span><span class="sxs-lookup"><span data-stu-id="39464-152">hello probes are part of hello Load Balancer resource.</span></span> <span data-ttu-id="39464-153">Hier volgt Hallo test definitie voor Hallo eerste toepassing standaardpoort:</span><span class="sxs-lookup"><span data-stu-id="39464-153">Here is hello probe definition for hello first default application port:</span></span>
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. <span data-ttu-id="39464-154">Een *taakverdeling regel* die samen bindt Hallo poort en het Hallo-test, zodat taakverdeling over een set van clusterknooppunten voor Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="39464-154">A *load-balancing rule* that ties together hello port and hello probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   <span data-ttu-id="39464-155">Als Hallo-toepassingen dat u van plan toodeploy toohello cluster bent meer poorten moeten, kunt u ze kunt toevoegen door het maken van aanvullende test en regeldefinities load balancing.</span><span class="sxs-lookup"><span data-stu-id="39464-155">If hello applications that you plan toodeploy toohello cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="39464-156">Voor meer informatie over het toowork met Azure Load Balancer via Resource Manager-sjablonen, Zie [maken van een interne load balancer met een sjabloon aan de slag](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="39464-156">For more information on how toowork with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-hello-template-by-using-visual-studio"></a><span data-ttu-id="39464-157">Hallo-sjabloon implementeren met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="39464-157">Deploy hello template by using Visual Studio</span></span>
<span data-ttu-id="39464-158">Nadat u hebt opgeslagen Hallo alle vereiste parameter-waarden in de`ServiceFabricCluster.param.dev.json` -bestand, u bent gereed toodeploy Hallo sjabloon en een Service Fabric-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="39464-158">After you have saved all hello required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready toodeploy hello template and create your Service Fabric cluster.</span></span> <span data-ttu-id="39464-159">Hallo resourcegroepproject in Visual Studio Solution Explorer met de rechtermuisknop en kies **implementeren | Nieuwe implementatie...** . Indien nodig, Visual Studio Hallo ziet **tooResource groep implementeren** in het dialoogvenster waarin u wordt gevraagd tooauthenticate tooAzure:</span><span class="sxs-lookup"><span data-stu-id="39464-159">Right-click hello resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**. If necessary, Visual Studio will show hello **Deploy tooResource Group** dialog box, asking you tooauthenticate tooAzure:</span></span>

![Dialoogvenster van de groep tooResource implementeren][3]

<span data-ttu-id="39464-161">Hallo-dialoogvenster kunt u een bestaande resourcegroep voor Resource Manager voor het Hallo-cluster en geeft u een nieuwe optie toocreate Hallo kiezen.</span><span class="sxs-lookup"><span data-stu-id="39464-161">hello dialog box lets you choose an existing Resource Manager resource group for hello cluster and gives you hello option toocreate a new one.</span></span> <span data-ttu-id="39464-162">Normaal gesproken maakt zin toouse een afzonderlijke resourcegroep voor een Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="39464-162">It normally makes sense toouse a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="39464-163">Nadat u Hallo implementeren knop raakt, wordt Visual Studio u gevraagd tooconfirm Hallo sjabloonparameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="39464-163">After you hit hello Deploy button, Visual Studio will prompt you tooconfirm hello template parameter values.</span></span> <span data-ttu-id="39464-164">Treffers Hallo **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="39464-164">Hit hello **Save** button.</span></span> <span data-ttu-id="39464-165">Één parameter heeft geen een persistente waarde: Hallo beheerdersrechten accountwachtwoord voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="39464-165">One parameter does not have a persisted value: hello administrative account password for hello cluster.</span></span> <span data-ttu-id="39464-166">U moet tooprovide een waarde van het wachtwoord als Visual Studio wordt u gevraagd om een.</span><span class="sxs-lookup"><span data-stu-id="39464-166">You need tooprovide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="39464-167">Visual Studio starten met Azure SDK 2.9, ondersteunt lezen wachtwoorden van **Azure Key Vault** tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="39464-167">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="39464-168">U ziet dat Hallo in Hallo sjabloon parametersdialoogvenster `adminPassword` tekstvak parameter heeft een weinig 'sleutel'-pictogram op de juiste Hallo.</span><span class="sxs-lookup"><span data-stu-id="39464-168">In hello template parameters dialog notice that hello `adminPassword` parameter text box has a little "key" icon on hello right.</span></span> <span data-ttu-id="39464-169">Dit pictogram kunt u een bestaande sleutelkluis geheim tooselect als beheerderswachtwoord voor de cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="39464-169">This icon allows you tooselect an existing key vault secret as hello administrative password for hello cluster.</span></span> <span data-ttu-id="39464-170">Zorg ervoor dat toofirst Azure Resource Manager-toegang voor de sjabloonimplementatie in Hallo geavanceerde toegangsbeleid van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="39464-170">Just make sure toofirst enable Azure Resource Manager access for template deployment in hello Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="39464-171">U kunt voortgang Hallo van Hallo-implementatieproces in Visual Studio-uitvoervenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="39464-171">You can monitor hello progress of hello deployment process in hello Visual Studio output window.</span></span> <span data-ttu-id="39464-172">Zodra de sjabloonimplementatie Hallo is voltooid, is het nieuwe cluster gereed toouse!</span><span class="sxs-lookup"><span data-stu-id="39464-172">Once hello template deployment is completed, your new cluster is ready toouse!</span></span>

> [!NOTE]
> <span data-ttu-id="39464-173">Als PowerShell nooit gebruikte tooadminister Azure vanaf Hallo-machine die u nu gebruikt is, moet u toodo wat housekeeping.</span><span class="sxs-lookup"><span data-stu-id="39464-173">If PowerShell was never used tooadminister Azure from hello machine that you are using now, you need toodo a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="39464-174">PowerShell-scripting door het uitvoeren van Hallo inschakelen [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) opdracht.</span><span class="sxs-lookup"><span data-stu-id="39464-174">Enable PowerShell scripting by running hello [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="39464-175">'Onbeperkte' beleid is voor ontwikkeling machines, doorgaans acceptabel.</span><span class="sxs-lookup"><span data-stu-id="39464-175">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="39464-176">Bepaal of tooallow diagnostische gegevens verzamelen van Azure PowerShell-opdrachten en voer [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) of [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) indien nodig.</span><span class="sxs-lookup"><span data-stu-id="39464-176">Decide whether tooallow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="39464-177">Hiermee worden onnodige prompts voorkomen tijdens de sjabloonimplementatie van de.</span><span class="sxs-lookup"><span data-stu-id="39464-177">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="39464-178">Als er fouten zijn, gaat u toohello [Azure-portal](https://portal.azure.com/) en open Hallo resourcegroep die u geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="39464-178">If there are any errors, go toohello [Azure portal](https://portal.azure.com/) and open hello resource group that you deployed to.</span></span> <span data-ttu-id="39464-179">Klik op **alle instellingen**, klikt u vervolgens op **implementaties** op de blade instellingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="39464-179">Click **All settings**, then click **Deployments** on hello settings blade.</span></span> <span data-ttu-id="39464-180">Een mislukte implementatie van de resourcegroep blijven er gedetailleerde diagnostische informatie.</span><span class="sxs-lookup"><span data-stu-id="39464-180">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="39464-181">Service Fabric-clusters vereisen van een bepaald aantal knooppunten toobe toomaintain beschikbaar en het behouden van status - waarnaar wordt verwezen tooas 'onderhoud quorum'.</span><span class="sxs-lookup"><span data-stu-id="39464-181">Service Fabric clusters require a certain number of nodes toobe up toomaintain availability and preserve state - referred tooas "maintaining quorum."</span></span> <span data-ttu-id="39464-182">Het is daarom niet veilig tooshut omlaag alle machines in de cluster Hallo Hallo tenzij u eerst hebt uitgevoerd een [volledige back-up van de staat](service-fabric-reliable-services-backup-restore.md).</span><span class="sxs-lookup"><span data-stu-id="39464-182">Therefore, it is not safe tooshut down all of hello machines in hello cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="39464-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="39464-183">Next steps</span></span>
* [<span data-ttu-id="39464-184">Meer informatie over het instellen van Service Fabric-cluster met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="39464-184">Learn about setting up Service Fabric cluster using hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="39464-185">Meer informatie over hoe toomanage en implementeren van Service Fabric-toepassingen met Visual Studio</span><span class="sxs-lookup"><span data-stu-id="39464-185">Learn how toomanage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
