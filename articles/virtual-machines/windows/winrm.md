---
title: aaaSet van WinRM-toegang voor een virtuele machine in Azure | Microsoft Docs
description: Het instellen van WinRM-toegang voor gebruik met Azure een virtuele machine gemaakt in Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="da79c-103">WinRM toegang instellen voor virtuele Machines in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="da79c-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="da79c-104">WinRM in de Azure Service Management vs Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="da79c-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="da79c-105">Voor een overzicht van hello Azure Resource Manager, raadpleegt u dit [artikel](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="da79c-105">For an overview of hello Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="da79c-106">Voor de verschillen tussen Azure-servicebeheer en Azure Resource Manager, raadpleegt u dit [artikel](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="da79c-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="da79c-107">Hallo is belangrijk verschil bij het instellen van de WinRM-configuratie tussen twee stacks Hallo hoe Hallo certificaat op Hallo VM wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="da79c-107">hello key difference in setting up WinRM configuration between hello two stacks is how hello certificate gets installed on hello VM.</span></span> <span data-ttu-id="da79c-108">In Azure Resource Manager-stack hello, worden certificaten Hallo gemodelleerd als bronnen die worden beheerd door Hallo Key Vault Resource Provider.</span><span class="sxs-lookup"><span data-stu-id="da79c-108">In hello Azure Resource Manager stack, hello certificates are modeled as resources managed by hello Key Vault Resource Provider.</span></span> <span data-ttu-id="da79c-109">Daarom Hallo gebruiker moet tooprovide hun eigen certificaat en upload het tooa Sleutelkluis voordat u deze in een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="da79c-109">Therefore, hello user needs tooprovide their own certificate and upload it tooa Key Vault before using it in a VM.</span></span>

<span data-ttu-id="da79c-110">Hier volgen Hallo stappen u moet tootake tooset van een virtuele machine met de WinRM-connectiviteit</span><span class="sxs-lookup"><span data-stu-id="da79c-110">Here are hello steps you need tootake tooset up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="da79c-111">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="da79c-111">Create a Key Vault</span></span>
2. <span data-ttu-id="da79c-112">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="da79c-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="da79c-113">Uploaden van uw zelf-ondertekend certificaat tooKey kluis</span><span class="sxs-lookup"><span data-stu-id="da79c-113">Upload your self-signed certificate tooKey Vault</span></span>
4. <span data-ttu-id="da79c-114">Hallo-URL voor uw zelf-ondertekend certificaat in Hallo Sleutelkluis ophalen</span><span class="sxs-lookup"><span data-stu-id="da79c-114">Get hello URL for your self-signed certificate in hello Key Vault</span></span>
5. <span data-ttu-id="da79c-115">Verwijst naar de URL van uw zelf-ondertekende certificaten tijdens het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="da79c-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="da79c-116">Stap 1: Een Sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="da79c-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="da79c-117">U kunt Hallo onderstaande opdracht toocreate hello Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="da79c-117">You can use hello below command toocreate hello Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="da79c-118">Stap 2: Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="da79c-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="da79c-119">U kunt een zelfondertekend certificaat met deze PowerShell-script maken</span><span class="sxs-lookup"><span data-stu-id="da79c-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a><span data-ttu-id="da79c-120">Stap 3: Uw zelf-ondertekend certificaat toohello Sleutelkluis uploaden</span><span class="sxs-lookup"><span data-stu-id="da79c-120">Step 3: Upload your self-signed certificate toohello Key Vault</span></span>
<span data-ttu-id="da79c-121">Voordat uploaden Hallo certificaat toohello Sleutelkluis in stap 1 gemaakt, moet deze tooconverted in een indeling Hallo Microsoft.Compute-resourceprovider wordt begrepen.</span><span class="sxs-lookup"><span data-stu-id="da79c-121">Before uploading hello certificate toohello Key Vault created in step 1, it needs tooconverted into a format hello Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="da79c-122">Hallo onderstaande PowerShell-script kunt u dat doen</span><span class="sxs-lookup"><span data-stu-id="da79c-122">hello below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path toohello .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a><span data-ttu-id="da79c-123">Stap 4: Hallo-URL voor uw zelf-ondertekend certificaat in Hallo Sleutelkluis ophalen</span><span class="sxs-lookup"><span data-stu-id="da79c-123">Step 4: Get hello URL for your self-signed certificate in hello Key Vault</span></span>
<span data-ttu-id="da79c-124">Hallo Microsoft.Compute-resourceprovider moet een URL toohello geheim binnen Hallo Sleutelkluis tijdens het Hallo VM-inrichting.</span><span class="sxs-lookup"><span data-stu-id="da79c-124">hello Microsoft.Compute resource provider needs a URL toohello secret inside hello Key Vault while provisioning hello VM.</span></span> <span data-ttu-id="da79c-125">Dit kunt Hallo Microsoft.Compute resource provider toodownload Hallo geheim en Hallo gelijkwaardige certificaat maken op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="da79c-125">This enables hello Microsoft.Compute resource provider toodownload hello secret and create hello equivalent certificate on hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="da79c-126">Hallo-URL van Hallo geheim moet ook tooinclude Hallo-versie.</span><span class="sxs-lookup"><span data-stu-id="da79c-126">hello URL of hello secret needs tooinclude hello version as well.</span></span> <span data-ttu-id="da79c-127">Een voorbeeld-URL ziet eruit als hieronder https://contosovault.vault.azure.net:443/geheimen/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="da79c-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="da79c-128">Sjablonen</span><span class="sxs-lookup"><span data-stu-id="da79c-128">Templates</span></span>
<span data-ttu-id="da79c-129">U kunt Hallo koppeling toohello URL krijgen in Hallo onder code met Hallo-sjabloon</span><span class="sxs-lookup"><span data-stu-id="da79c-129">You can get hello link toohello URL in hello template using hello below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="da79c-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da79c-130">PowerShell</span></span>
<span data-ttu-id="da79c-131">U kunt deze URL met Hallo onderstaande PowerShell-opdracht ophalen</span><span class="sxs-lookup"><span data-stu-id="da79c-131">You can get this URL using hello below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="da79c-132">Stap 5: Verwijzen naar de URL van uw zelf-ondertekende certificaten tijdens het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="da79c-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="da79c-133">Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="da79c-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="da79c-134">Hallo certificaat opgehaald bij het maken van een virtuele machine via sjablonen verwezen in Hallo geheimen en Hallo winRM sectie zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="da79c-134">While creating a VM through templates, hello certificate gets referenced in hello secrets section and hello winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="da79c-135">Een voorbeeldsjabloon voor Hallo bovenstaande vindt u hier op [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="da79c-135">A sample template for hello above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="da79c-136">De broncode voor deze sjabloon kunt u vinden op [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="da79c-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="da79c-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da79c-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a><span data-ttu-id="da79c-138">Stap 6: Verbinding maken met toohello VM</span><span class="sxs-lookup"><span data-stu-id="da79c-138">Step 6: Connecting toohello VM</span></span>
<span data-ttu-id="da79c-139">Voordat u verbinding met toohello VM maken kunt moet u ervoor dat uw computer is geconfigureerd voor extern beheer met WinRM toomake.</span><span class="sxs-lookup"><span data-stu-id="da79c-139">Before you can connect toohello VM you'll need toomake sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="da79c-140">Start PowerShell als beheerder en voer uit Hallo onderstaande opdracht toomake zeker dat u alles hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="da79c-140">Start PowerShell as an administrator and execute hello below command toomake sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="da79c-141">Mogelijk moet u toomake ervoor Hallo WinRM-service wordt uitgevoerd als Hallo hierboven niet werkt.</span><span class="sxs-lookup"><span data-stu-id="da79c-141">You might need toomake sure hello WinRM service is running if hello above does not work.</span></span> <span data-ttu-id="da79c-142">U kunt doen dat met`Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="da79c-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="da79c-143">Als Hallo setup is voltooid, kunt u toohello VM Hallo onder opdracht met</span><span class="sxs-lookup"><span data-stu-id="da79c-143">Once hello setup is done, you can connect toohello VM using hello below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
