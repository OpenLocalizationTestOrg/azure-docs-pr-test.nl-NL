---
title: aaaHPC Pack 2016-cluster in Azure | Microsoft Docs
description: Meer informatie over hoe een HPC Pack 2016 toodeploy-cluster in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="252d1-103">Een HPC Pack 2016-cluster in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="252d1-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="252d1-104">Hallo-stappen in dit artikel toodeploy een [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="252d1-104">Follow hello steps in this article toodeploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="252d1-105">HPC Pack is oplossing van Microsoft gratis HPC gebaseerd op Microsoft Azure en Windows Server-technologieën en biedt ondersteuning voor een breed bereik van HPC-workloads.</span><span class="sxs-lookup"><span data-stu-id="252d1-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="252d1-106">Gebruik een van de Hallo [Azure Resource Manager-sjablonen](https://github.com/MsHpcPack/HPCPack2016) toodeploy Hallo HPC Pack 2016 cluster.</span><span class="sxs-lookup"><span data-stu-id="252d1-106">Use one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="252d1-107">U hebt verschillende mogelijkheden van de clustertopologie met verschillende aantallen head clusterknooppunten en met beide Linux of Windows rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="252d1-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="252d1-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="252d1-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="252d1-109">PFX-certificaat</span><span class="sxs-lookup"><span data-stu-id="252d1-109">PFX certificate</span></span>

<span data-ttu-id="252d1-110">Een cluster met Microsoft HPC Pack 2016 vereist een Personal Information Exchange (PFX) certificaat toosecure Hallo communicatie tussen Hallo HPC-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="252d1-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate toosecure hello communication between hello HPC nodes.</span></span> <span data-ttu-id="252d1-111">Hallo-certificaat moet voldoen aan Hallo volgens de vereisten:</span><span class="sxs-lookup"><span data-stu-id="252d1-111">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="252d1-112">Er moet een persoonlijke sleutel sleuteluitwisseling</span><span class="sxs-lookup"><span data-stu-id="252d1-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="252d1-113">Sleutelgebruik bevat digitale handtekening en sleutelcodering</span><span class="sxs-lookup"><span data-stu-id="252d1-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="252d1-114">Uitgebreid sleutelgebruik bevat clientverificatie en serververificatie</span><span class="sxs-lookup"><span data-stu-id="252d1-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="252d1-115">Als u geen al een certificaat dat aan deze vereisten voldoet, kunt u Hallo certificaat aanvragen bij een certificeringsinstantie (CA).</span><span class="sxs-lookup"><span data-stu-id="252d1-115">If you don’t already have a certificate that meets these requirements, you can request hello certificate from a certification authority.</span></span> <span data-ttu-id="252d1-116">U kunt ook Hallo na opdrachten toogenerate Hallo zelf-ondertekend certificaat op basis van Hallo besturingssysteem waarop u Hallo-opdracht uitvoert en Hallo PFX-indeling certificaat met persoonlijke sleutel exporteren.</span><span class="sxs-lookup"><span data-stu-id="252d1-116">Alternatively, you can use hello following commands toogenerate hello self-signed certificate based on hello operating system on which you run hello command, and export hello PFX format certificate with private key.</span></span>

* <span data-ttu-id="252d1-117">**Voor Windows 10 of Windows Server 2016**, uitvoeren van de ingebouwde Hallo **nieuw SelfSignedCertificate** PowerShell-cmdlet als volgt:</span><span class="sxs-lookup"><span data-stu-id="252d1-117">**For Windows 10 or Windows Server 2016**, run hello built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="252d1-118">**Voor besturingssystemen ouder dan Windows 10 of Windows Server 2016**, downloaden Hallo [zelf-ondertekend certificaat generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) van Hallo Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="252d1-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download hello [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from hello Microsoft Script Center.</span></span> <span data-ttu-id="252d1-119">Pak de inhoud en Voer Hallo opdrachten op een PowerShell-prompt te volgen:</span><span class="sxs-lookup"><span data-stu-id="252d1-119">Extract its contents and run hello following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a><span data-ttu-id="252d1-120">Certificaat tooan Azure sleutelkluis uploaden</span><span class="sxs-lookup"><span data-stu-id="252d1-120">Upload certificate tooan Azure key vault</span></span>

<span data-ttu-id="252d1-121">Voordat u Hallo HPC-cluster implementeert, uploaden Hallo certificaat tooan [Azure sleutelkluis](../../key-vault/index.md) als een geheim en record Hallo volgende informatie voor gebruik tijdens de implementatie van Hallo: **kluisnaam**,  **De resourcegroep kluis**, **certificaat-URL**, en **certificaatvingerafdruk**.</span><span class="sxs-lookup"><span data-stu-id="252d1-121">Before deploying hello HPC cluster, upload hello certificate tooan [Azure key vault](../../key-vault/index.md) as a secret, and record hello following information for use during hello deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="252d1-122">Er volgt een voorbeeld PowerShell script tooupload Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="252d1-122">A sample PowerShell script tooupload hello certificate follows.</span></span> <span data-ttu-id="252d1-123">Zie voor meer informatie over het uploaden van een certificaat tooan Azure sleutelkluis [aan de slag met Azure Key Vault](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="252d1-123">For more information about uploading a certificate tooan Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="252d1-124">Ondersteunde topologieën</span><span class="sxs-lookup"><span data-stu-id="252d1-124">Supported topologies</span></span>

<span data-ttu-id="252d1-125">Kies een van de Hallo [Azure Resource Manager-sjablonen](https://github.com/MsHpcPack/HPCPack2016) toodeploy Hallo HPC Pack 2016 cluster.</span><span class="sxs-lookup"><span data-stu-id="252d1-125">Choose one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="252d1-126">Hieronder vindt u op hoog niveau van de drie ondersteunde clustertopologieën-architecturen.</span><span class="sxs-lookup"><span data-stu-id="252d1-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="252d1-127">Hoge beschikbaarheid topologieën bevatten meerdere head clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="252d1-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="252d1-128">Cluster met hoge beschikbaarheid met Active Directory-domein</span><span class="sxs-lookup"><span data-stu-id="252d1-128">High-availability cluster with Active Directory domain</span></span>

    ![HA-cluster in AD-domein](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="252d1-130">Cluster met hoge beschikbaarheid zonder Active Directory-domein</span><span class="sxs-lookup"><span data-stu-id="252d1-130">High-availability cluster without Active Directory domain</span></span>

    ![HA cluster zonder AD-domein](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="252d1-132">Cluster met slechts één hoofdknooppunt</span><span class="sxs-lookup"><span data-stu-id="252d1-132">Cluster with a single head node</span></span>

   ![Cluster met één hoofdknooppunt](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="252d1-134">Een cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="252d1-134">Deploy a cluster</span></span>

<span data-ttu-id="252d1-135">toocreate hello cluster, kiest u een sjabloon en klikt u op **tooAzure implementeren**.</span><span class="sxs-lookup"><span data-stu-id="252d1-135">toocreate hello cluster, choose a template and click **Deploy tooAzure**.</span></span> <span data-ttu-id="252d1-136">In Hallo [Azure-portal](https://portal.azure.com), Geef parameters op voor de sjabloon Hallo zoals beschreven in de volgende stappen uit Hallo.</span><span class="sxs-lookup"><span data-stu-id="252d1-136">In hello [Azure portal](https://portal.azure.com), specify parameters for hello template as described in hello following steps.</span></span> <span data-ttu-id="252d1-137">Elke sjabloon wordt gemaakt van alle Azure-resources die vereist zijn voor Hallo HPC-clusterinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="252d1-137">Each template creates all Azure resources required for hello HPC cluster infrastructure.</span></span> <span data-ttu-id="252d1-138">Resources omvatten een Azure-netwerk, openbare IP-adres, load balancer (alleen voor een cluster met hoge beschikbaarheid), netwerkinterfaces, beschikbaarheidssets, opslagaccounts en virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="252d1-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a><span data-ttu-id="252d1-139">Stap 1: Selecteer Hallo abonnement, de locatie en de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="252d1-139">Step 1: Select hello subscription, location, and resource group</span></span>

<span data-ttu-id="252d1-140">Hallo **abonnement** en Hallo **locatie** moet hetzelfde zijn die u hebt opgegeven dat wanneer u het PFX-certificaat geüpload (Zie vereisten).</span><span class="sxs-lookup"><span data-stu-id="252d1-140">hello **Subscription** and hello **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="252d1-141">Het is raadzaam dat u maakt een **resourcegroep** voor Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="252d1-141">We recommend that you create a **Resource group** for hello deployment.</span></span>

### <a name="step-2-specify-hello-parameter-settings"></a><span data-ttu-id="252d1-142">Stap 2: Geef de parameterinstellingen Hallo</span><span class="sxs-lookup"><span data-stu-id="252d1-142">Step 2: Specify hello parameter settings</span></span>

<span data-ttu-id="252d1-143">Invoeren of wijzigen van waarden voor de sjabloonparameters Hallo.</span><span class="sxs-lookup"><span data-stu-id="252d1-143">Enter or modify values for hello template parameters.</span></span> <span data-ttu-id="252d1-144">Klik op Hallo pictogram volgende tooeach-parameter voor help-informatie.</span><span class="sxs-lookup"><span data-stu-id="252d1-144">Click hello icon next tooeach parameter for help information.</span></span> <span data-ttu-id="252d1-145">Zie ook Hallo richtlijnen voor [beschikbare VM-grootten](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="252d1-145">Also see hello guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="252d1-146">U hebt vastgelegd in het Hallo-vereisten voor de volgende parameters Hallo Hallo-waarden opgeven: **kluisnaam**, **kluis resourcegroep**, **certificaat-URL**, en **Certificaatvingerafdruk**.</span><span class="sxs-lookup"><span data-stu-id="252d1-146">Specify hello values you recorded in hello Prerequisites for hello following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="252d1-147">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="252d1-147">Step 3.</span></span> <span data-ttu-id="252d1-148">Juridische voorwaarden bekijken en maken</span><span class="sxs-lookup"><span data-stu-id="252d1-148">Review legal terms and create</span></span>
<span data-ttu-id="252d1-149">Klik op **juridische voorwaarden bekijken** tooreview Hallo voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="252d1-149">Click **Review legal terms** tooreview hello terms.</span></span> <span data-ttu-id="252d1-150">Als u akkoord gaat, klikt u op **aankoop**, en klik vervolgens op **maken** toostart Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="252d1-150">If you agree, click **Purchase**, and then click **Create** toostart hello deployment.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="252d1-151">Verbinding maken met cluster toohello</span><span class="sxs-lookup"><span data-stu-id="252d1-151">Connect toohello cluster</span></span>
1. <span data-ttu-id="252d1-152">Nadat het Hallo HPC Pack cluster is geïmplementeerd, gaat u toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="252d1-152">After hello HPC Pack cluster is deployed, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="252d1-153">Klik op **resourcegroepen**, en zoek Hallo-resourcegroep in welke Hallo cluster is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="252d1-153">Click **Resource groups**, and find hello resource group in which hello cluster was deployed.</span></span> <span data-ttu-id="252d1-154">U vindt Hallo hoofdknooppunt virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="252d1-154">You can find hello head node virtual machines.</span></span>

    ![Head clusterknooppunten in Hallo-portal](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="252d1-156">Klik op één hoofdknooppunt (in een cluster met hoge beschikbaarheid, klik op een van de hoofdknooppunten Hallo).</span><span class="sxs-lookup"><span data-stu-id="252d1-156">Click one head node (in a high-availability cluster, click any of hello head nodes).</span></span> <span data-ttu-id="252d1-157">In **Essentials**, kunt u vinden Hallo openbaar IP-adres of de volledige DNS-naam van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="252d1-157">In **Essentials**, you can find hello public IP address or full DNS name of hello cluster.</span></span>

    ![Cluster-verbindingsinstellingen](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="252d1-159">Klik op **Connect** toolog op tooany van Hallo hoofdknooppunten met extern bureaublad met uw beheerder van de opgegeven gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="252d1-159">Click **Connect** toolog on tooany of hello head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="252d1-160">Als Hallo cluster die u hebt geïmplementeerd in een Active Directory-domein, gebruikersnaam Hallo heeft de vorm van Hallo <privateDomainName> \<adminUsername > (bijvoorbeeld hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="252d1-160">If hello cluster you deployed is in an Active Directory Domain, hello user name is of hello form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="252d1-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="252d1-161">Next steps</span></span>
* <span data-ttu-id="252d1-162">Verzenden van taken tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="252d1-162">Submit jobs tooyour cluster.</span></span> <span data-ttu-id="252d1-163">Zie [verzenden van taken tooHPC een HPC Pack-cluster in Azure](hpcpack-cluster-submit-jobs.md) en [een HPC Pack 2016-cluster in Azure met Azure Active Directory beheren](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="252d1-163">See [Submit jobs tooHPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

