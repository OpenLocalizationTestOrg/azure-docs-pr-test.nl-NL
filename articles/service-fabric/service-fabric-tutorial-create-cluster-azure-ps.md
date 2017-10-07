---
title: aaaCreate een Service Fabric-cluster in Azure | Microsoft Docs
description: Meer informatie over hoe toocreate een Windows- of Linux Service Fabric-cluster in Azure met behulp van PowerShell.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="edbf3-103">Een beveiligde cluster maken in Azure met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="edbf3-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="edbf3-104">Deze zelfstudie laat zien hoe toocreate een Service Fabric-cluster (Windows of Linux) wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="edbf3-104">This tutorial shows you how toocreate a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="edbf3-105">Wanneer u klaar bent, hebt u een cluster met in Hallo cloud die u kunt toepassingen implementeren op.</span><span class="sxs-lookup"><span data-stu-id="edbf3-105">When you're finished, you have a cluster running in hello cloud that you can deploy applications to.</span></span>

<span data-ttu-id="edbf3-106">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="edbf3-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="edbf3-107">Maken van een beveiligde Service Fabric-cluster in Azure met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="edbf3-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="edbf3-108">Beveiligde Hallo-cluster met een X.509-certificaat</span><span class="sxs-lookup"><span data-stu-id="edbf3-108">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="edbf3-109">Verbinding maken met behulp van PowerShell toohello-cluster</span><span class="sxs-lookup"><span data-stu-id="edbf3-109">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="edbf3-110">Verwijderen van een cluster</span><span class="sxs-lookup"><span data-stu-id="edbf3-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edbf3-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="edbf3-111">Prerequisites</span></span>
<span data-ttu-id="edbf3-112">Voordat u deze zelfstudie begint:</span><span class="sxs-lookup"><span data-stu-id="edbf3-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="edbf3-113">Als u geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="edbf3-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="edbf3-114">Hallo installeren [Service Fabric SDK en PowerShell-module](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="edbf3-114">Install hello [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="edbf3-115">Hallo installeren [Azure Powershell-moduleversie 4.1 of hoger](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="edbf3-115">Install hello [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="edbf3-116">Hallo na procedure maakt een voorbeeld van één knooppunt (één virtuele machine) Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="edbf3-116">hello following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="edbf3-117">Hallo-cluster wordt beveiligd door een zelfondertekend certificaat dat wordt naast het Hallo-cluster gemaakt en vervolgens in een sleutelkluis geplaatst.</span><span class="sxs-lookup"><span data-stu-id="edbf3-117">hello cluster is secured by a self-signed certificate that gets created along with hello cluster and then placed in a key vault.</span></span> <span data-ttu-id="edbf3-118">Clusters met één knooppunt dan één virtuele machine kunnen niet worden geschaald en clusters preview kunnen niet worden toonewer bijgewerkte versies.</span><span class="sxs-lookup"><span data-stu-id="edbf3-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded toonewer versions.</span></span>

<span data-ttu-id="edbf3-119">toocalculate kosten door het uitvoeren van een Service Fabric-cluster in Azure gebruik Hallo [Azure Prijscalculator](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="edbf3-119">toocalculate cost incurred by running a Service Fabric cluster in Azure use hello [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="edbf3-120">Zie voor meer informatie over het maken van Service Fabric-clusters [Service Fabric-cluster maken met behulp van Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="edbf3-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-hello-cluster-using-azure-powershell"></a><span data-ttu-id="edbf3-121">Hallo-cluster met behulp van PowerShell voor Azure maken</span><span class="sxs-lookup"><span data-stu-id="edbf3-121">Create hello cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="edbf3-122">Downloaden van een lokale kopie van hello Azure Resource Manager-sjabloon en het parameterbestand Hallo van Hallo [Azure Resource Manager-sjabloon voor Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="edbf3-122">Download a local copy of hello Azure Resource Manager template and hello parameter file from hello [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="edbf3-123">*azuredeploy.JSON* hello Azure Resource Manager-sjabloon die een Service Fabric-cluster definieert is.</span><span class="sxs-lookup"><span data-stu-id="edbf3-123">*azuredeploy.json* is hello Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="edbf3-124">*azuredeploy.parameters.JSON* een parameterbestand is voor u toocustomize Hallo Clusterimplementatie.</span><span class="sxs-lookup"><span data-stu-id="edbf3-124">*azuredeploy.parameters.json* is a parameters file for you toocustomize hello cluster deployment.</span></span>

2. <span data-ttu-id="edbf3-125">Aanpassen van de volgende parameters in Hallo Hallo *azuredeploy.parameters.json* parameterbestand:</span><span class="sxs-lookup"><span data-stu-id="edbf3-125">Customize hello following parameters in hello *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="edbf3-126">Parameter</span><span class="sxs-lookup"><span data-stu-id="edbf3-126">Parameter</span></span>       | <span data-ttu-id="edbf3-127">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="edbf3-127">Description</span></span> | <span data-ttu-id="edbf3-128">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="edbf3-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="edbf3-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="edbf3-129">clusterLocation</span></span> | <span data-ttu-id="edbf3-130">Hello Azure-regio toowhich toodeploy Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="edbf3-130">hello Azure region toowhich toodeploy hello cluster.</span></span> | <span data-ttu-id="edbf3-131">*bijvoorbeeld, westeurope, Oost-Aziatische, eastus*</span><span class="sxs-lookup"><span data-stu-id="edbf3-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="edbf3-132">Clusternaam</span><span class="sxs-lookup"><span data-stu-id="edbf3-132">clusterName</span></span>     | <span data-ttu-id="edbf3-133">Naam van de cluster Hallo gewenste toocreate.</span><span class="sxs-lookup"><span data-stu-id="edbf3-133">Name of hello cluster you want toocreate.</span></span> | <span data-ttu-id="edbf3-134">*bijvoorbeeld, bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="edbf3-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="edbf3-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="edbf3-135">adminUserName</span></span>   | <span data-ttu-id="edbf3-136">Hallo lokale beheerdersaccount op Hallo cluster virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="edbf3-136">hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="edbf3-137">*Een geldige gebruikersnaam voor Windows Server*</span><span class="sxs-lookup"><span data-stu-id="edbf3-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="edbf3-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="edbf3-138">adminPassword</span></span>   | <span data-ttu-id="edbf3-139">Wachtwoord van de lokale beheerdersaccount Hallo op Hallo cluster virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="edbf3-139">Password of hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="edbf3-140">*Een geldig wachtwoord voor Windows Server*</span><span class="sxs-lookup"><span data-stu-id="edbf3-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="edbf3-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="edbf3-141">clusterCodeVersion</span></span> | <span data-ttu-id="edbf3-142">Hallo Service Fabric-versie toorun.</span><span class="sxs-lookup"><span data-stu-id="edbf3-142">hello Service Fabric version toorun.</span></span> <span data-ttu-id="edbf3-143">(255.255.X.255 preview-versies zijn).</span><span class="sxs-lookup"><span data-stu-id="edbf3-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="edbf3-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="edbf3-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="edbf3-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="edbf3-145">vmInstanceCount</span></span> | <span data-ttu-id="edbf3-146">Hallo aantal virtuele machines in uw cluster (kan worden 1 of 3-99).</span><span class="sxs-lookup"><span data-stu-id="edbf3-146">hello number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="edbf3-147">**1**</span><span class="sxs-lookup"><span data-stu-id="edbf3-147">**1**</span></span> | <span data-ttu-id="edbf3-148">*Geef slechts één virtuele machine voor een preview-cluster.*</span><span class="sxs-lookup"><span data-stu-id="edbf3-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="edbf3-149">Open een PowerShell-console, aanmelding tooAzure en selecteer Hallo abonnement die u toodeploy Hallo cluster wilt toevoegen in:</span><span class="sxs-lookup"><span data-stu-id="edbf3-149">Open a PowerShell console, login tooAzure, and select hello subscription you want toodeploy hello cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="edbf3-150">Maken en een wachtwoord voor Hallo certificaat toobe die wordt gebruikt door de Service Fabric versleutelen.</span><span class="sxs-lookup"><span data-stu-id="edbf3-150">Create and encrypt a password for hello certificate toobe used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="edbf3-151">Hallo-cluster en het certificaat door het uitvoeren van de volgende opdracht Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="edbf3-151">Create hello cluster and its certificate by running hello following command:</span></span>

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   ><span data-ttu-id="edbf3-152">Hallo `-CertificateSubjectName` parameter moet worden uitgelijnd met de Hallo clusterName parameter die is opgegeven in het parameterbestand hello, ook als het domein gekoppeld toohello Azure-regio Hallo u hebt gekozen, zoals: `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="edbf3-152">hello `-CertificateSubjectName` parameter should align with hello clusterName parameter specified in hello parameters file, as well as hello domain tied toohello Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="edbf3-153">Zodra het Hallo-configuratie is voltooid, wordt deze informatie over het Hallo-cluster gemaakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="edbf3-153">Once hello configuration finishes, it outputs information about hello cluster created in Azure.</span></span> <span data-ttu-id="edbf3-154">Hallo cluster certificaat toohello - CertificateOutputFolder directory op Hallo-pad voor deze parameter opgegeven worden ook gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="edbf3-154">It also copies hello cluster certificate toohello -CertificateOutputFolder directory on hello path you specified for this parameter.</span></span> <span data-ttu-id="edbf3-155">U moet dit certificaat tooaccess Service Fabric Explorer en bekijk Hallo-status van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="edbf3-155">You need this certificate tooaccess Service Fabric Explorer and view hello health of your cluster.</span></span>

<span data-ttu-id="edbf3-156">Hallo-URL voor uw cluster, die mogelijk vergelijkbare toohello Noteer de volgende URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="edbf3-156">Take note of hello URL for your cluster, which may be similar toohello following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a><span data-ttu-id="edbf3-157">Toegang tot Service Fabric Explorer & Hallo-certificaat wijzigen</span><span class="sxs-lookup"><span data-stu-id="edbf3-157">Modify hello certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="edbf3-158">Dubbelklik op Hallo certificaat tooopen Hallo Wizard Certificaat importeren.</span><span class="sxs-lookup"><span data-stu-id="edbf3-158">Double-click hello certificate tooopen hello Certificate Import Wizard.</span></span>

2. <span data-ttu-id="edbf3-159">Standaardinstellingen gebruiken, maar zorg ervoor dat toocheck hello **deze sleutel als exporteerbaar markeren.**</span><span class="sxs-lookup"><span data-stu-id="edbf3-159">Use default settings, but make sure toocheck hello **Mark this key as exportable.**</span></span> <span data-ttu-id="edbf3-160">of u het selectievakje in Hallo **beveiliging voor persoonlijke sleutels** stap.</span><span class="sxs-lookup"><span data-stu-id="edbf3-160">check box, in hello **private key protection** step.</span></span> <span data-ttu-id="edbf3-161">Visual Studio moet tooexport Hallo certificaat bij het configureren van Azure Container register tooService Fabric-Cluster authenticatie verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="edbf3-161">Visual Studio needs tooexport hello certificate when configuring Azure Container Registry tooService Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="edbf3-162">U kunt nu Service Fabric Explorer openen in een browser.</span><span class="sxs-lookup"><span data-stu-id="edbf3-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="edbf3-163">toodo Ga dus toohello **ManagementEndpoint** URL voor uw cluster met een webbrowser en selecteer Hallo-certificaat dat is opgeslagen op uw computer.</span><span class="sxs-lookup"><span data-stu-id="edbf3-163">toodo so, navigate toohello **ManagementEndpoint** URL for your cluster using a web browser, and select hello certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="edbf3-164">Wanneer u Service Fabric Explorer opent, ziet u een certificaatfout als u een zelfondertekend certificaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="edbf3-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="edbf3-165">In de rand, hebt u tooclick *Details* en vervolgens Hallo *gaat u op de webpagina toohello* koppeling.</span><span class="sxs-lookup"><span data-stu-id="edbf3-165">In Edge, you have tooclick *Details* and then hello *Go on toohello webpage* link.</span></span> <span data-ttu-id="edbf3-166">In Chrome, hebt u tooclick *Geavanceerd* en vervolgens Hallo *gaan* koppeling.</span><span class="sxs-lookup"><span data-stu-id="edbf3-166">In Chrome, you have tooclick *Advanced* and then hello *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="edbf3-167">Als Hallo maken van het cluster is mislukt, kunt u altijd opnieuw uitgevoerd Hallo opdracht Hallo-resources die al is geïmplementeerd werkt.</span><span class="sxs-lookup"><span data-stu-id="edbf3-167">If hello cluster creation fails, you can always rerun hello command, which updates hello resources already deployed.</span></span> <span data-ttu-id="edbf3-168">Als een certificaat is gemaakt als onderdeel van de implementatie Hallo is mislukt, wordt een nieuwe gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="edbf3-168">If a certificate was created as part of hello failed deployment, a new one is generated.</span></span> <span data-ttu-id="edbf3-169">maken van het cluster tootroubleshoot Zie [Service Fabric-cluster maken met behulp van Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="edbf3-169">tootroubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-toohello-secure-cluster"></a><span data-ttu-id="edbf3-170">Verbinding maken met de beveiligde cluster toohello</span><span class="sxs-lookup"><span data-stu-id="edbf3-170">Connect toohello secure cluster</span></span>
<span data-ttu-id="edbf3-171">Verbinding maken met behulp van Hallo Service Fabric PowerShell-module geïnstalleerd met Hallo Service Fabric SDK toohello-cluster.</span><span class="sxs-lookup"><span data-stu-id="edbf3-171">Connect toohello cluster using hello Service Fabric PowerShell module installed with hello Service Fabric SDK.</span></span>  <span data-ttu-id="edbf3-172">Installeer eerst Hallo certificaat in archief van de Hallo persoonlijke (Mijn) van de huidige gebruiker Hallo op uw computer.</span><span class="sxs-lookup"><span data-stu-id="edbf3-172">First, install hello certificate into hello Personal (My) store of hello current user on your computer.</span></span>  <span data-ttu-id="edbf3-173">Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="edbf3-173">Run hello following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="edbf3-174">U bent nu klaar tooconnect tooyour beveiligde cluster.</span><span class="sxs-lookup"><span data-stu-id="edbf3-174">You are now ready tooconnect tooyour secure cluster.</span></span>

<span data-ttu-id="edbf3-175">Hallo **Service Fabric** PowerShell-module biedt veel cmdlets voor het beheren van Service Fabric-clusters, toepassingen en services.</span><span class="sxs-lookup"><span data-stu-id="edbf3-175">hello **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="edbf3-176">Gebruik Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello beveiligde cluster.</span><span class="sxs-lookup"><span data-stu-id="edbf3-176">Use hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello secure cluster.</span></span> <span data-ttu-id="edbf3-177">Hallo certificaatvingerafdruk en eindpunt Verbindingsdetails zijn gevonden in het Hallo-uitvoer van de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="edbf3-177">hello certificate thumbprint and connection endpoint details are found in hello output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="edbf3-178">Controleer of u verbonden bent en Hallo-cluster is in orde Hallo met [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="edbf3-178">Check that you are connected and hello cluster is healthy using hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="edbf3-179">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="edbf3-179">Clean up resources</span></span>

<span data-ttu-id="edbf3-180">Een cluster is opgebouwd uit andere Azure-resources bovendien toohello clusterbron zelf.</span><span class="sxs-lookup"><span data-stu-id="edbf3-180">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="edbf3-181">Hallo eenvoudigste manier toodelete Hallo cluster en alle Hallo resources verbruikt is toodelete Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="edbf3-181">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span>

<span data-ttu-id="edbf3-182">Meld u bij tooAzure en selecteer Hallo abonnements-ID waarmee u tooremove Hallo cluster wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="edbf3-182">Log in tooAzure and select hello subscription ID with which you want tooremove hello cluster.</span></span>  <span data-ttu-id="edbf3-183">U kunt uw abonnements-ID vinden door logboekregistratie in toohello [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="edbf3-183">You can find your subscription ID by logging in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="edbf3-184">Hallo-resourcegroep en alle Hallo clusterbronnen met behulp van Hallo verwijderen [cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="edbf3-184">Delete hello resource group and all hello cluster resources using hello [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="edbf3-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edbf3-185">Next steps</span></span>
<span data-ttu-id="edbf3-186">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="edbf3-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="edbf3-187">Maken van een Service Fabric-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="edbf3-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="edbf3-188">Beveiligde Hallo-cluster met een X.509-certificaat</span><span class="sxs-lookup"><span data-stu-id="edbf3-188">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="edbf3-189">Verbinding maken met behulp van PowerShell toohello-cluster</span><span class="sxs-lookup"><span data-stu-id="edbf3-189">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="edbf3-190">Verwijderen van een cluster</span><span class="sxs-lookup"><span data-stu-id="edbf3-190">Remove a cluster</span></span>

<span data-ttu-id="edbf3-191">Vervolgens gaan toohello zelfstudie toolearn hoe na toodeploy een bestaande toepassing.</span><span class="sxs-lookup"><span data-stu-id="edbf3-191">Next, advance toohello following tutorial toolearn how toodeploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="edbf3-192">Implementeer een bestaande .NET-toepassing met Docker Compose</span><span class="sxs-lookup"><span data-stu-id="edbf3-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
