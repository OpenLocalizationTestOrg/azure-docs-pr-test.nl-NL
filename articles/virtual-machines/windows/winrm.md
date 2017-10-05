---
title: WinRM toegang instellen voor een virtuele machine in Azure | Microsoft Docs
description: Het instellen van WinRM-toegang voor gebruik met Azure een virtuele machine gemaakt in het Resource Manager-implementatiemodel.
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
ms.openlocfilehash: 2d6533462400bc1d93d0d3b0227769784e2658a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="d5035-103">WinRM toegang instellen voor virtuele Machines in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d5035-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="d5035-104">WinRM in de Azure Service Management vs Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d5035-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="d5035-105">Voor een overzicht van de Azure Resource Manager, raadpleegt u dit [artikel](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d5035-105">For an overview of the Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="d5035-106">Voor de verschillen tussen Azure-servicebeheer en Azure Resource Manager, raadpleegt u dit [artikel](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="d5035-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="d5035-107">Het belangrijkste verschil bij het instellen van de WinRM-configuratie tussen de twee stapels is hoe het certificaat wordt geïnstalleerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5035-107">The key difference in setting up WinRM configuration between the two stacks is how the certificate gets installed on the VM.</span></span> <span data-ttu-id="d5035-108">De certificaten zijn in de Azure Resource Manager-stack gemodelleerd als bronnen die worden beheerd door de Sleutelkluis Resource Provider.</span><span class="sxs-lookup"><span data-stu-id="d5035-108">In the Azure Resource Manager stack, the certificates are modeled as resources managed by the Key Vault Resource Provider.</span></span> <span data-ttu-id="d5035-109">Daarom moet de gebruiker om te bieden hun eigen certificaat en upload het naar een Sleutelkluis voordat u deze in een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5035-109">Therefore, the user needs to provide their own certificate and upload it to a Key Vault before using it in a VM.</span></span>

<span data-ttu-id="d5035-110">Hier volgen de stappen die u nemen moet voor het instellen van een virtuele machine met de WinRM-connectiviteit</span><span class="sxs-lookup"><span data-stu-id="d5035-110">Here are the steps you need to take to set up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="d5035-111">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="d5035-111">Create a Key Vault</span></span>
2. <span data-ttu-id="d5035-112">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="d5035-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="d5035-113">Uw zelf-ondertekend certificaat uploaden naar Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="d5035-113">Upload your self-signed certificate to Key Vault</span></span>
4. <span data-ttu-id="d5035-114">De URL voor uw zelf-ondertekend certificaat in de Sleutelkluis ophalen</span><span class="sxs-lookup"><span data-stu-id="d5035-114">Get the URL for your self-signed certificate in the Key Vault</span></span>
5. <span data-ttu-id="d5035-115">Verwijst naar de URL van uw zelf-ondertekende certificaten tijdens het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="d5035-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="d5035-116">Stap 1: Een Sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="d5035-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="d5035-117">U kunt de onderstaande opdracht om te maken van de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="d5035-117">You can use the below command to create the Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="d5035-118">Stap 2: Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="d5035-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="d5035-119">U kunt een zelfondertekend certificaat met deze PowerShell-script maken</span><span class="sxs-lookup"><span data-stu-id="d5035-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter the certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-to-the-key-vault"></a><span data-ttu-id="d5035-120">Stap 3: Uw zelf-ondertekend certificaat uploaden naar de Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="d5035-120">Step 3: Upload your self-signed certificate to the Key Vault</span></span>
<span data-ttu-id="d5035-121">Voordat u het certificaat uploadt naar de Sleutelkluis in stap 1 hebt gemaakt, moet worden geconverteerd naar een indeling die wordt begrepen door de Microsoft.Compute-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="d5035-121">Before uploading the certificate to the Key Vault created in step 1, it needs to converted into a format the Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="d5035-122">De onderstaande PowerShell script kunt u dat doen</span><span class="sxs-lookup"><span data-stu-id="d5035-122">The below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path to the .pfx file>"
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

## <a name="step-4-get-the-url-for-your-self-signed-certificate-in-the-key-vault"></a><span data-ttu-id="d5035-123">Stap 4: De URL voor uw zelf-ondertekend certificaat in de Sleutelkluis ophalen</span><span class="sxs-lookup"><span data-stu-id="d5035-123">Step 4: Get the URL for your self-signed certificate in the Key Vault</span></span>
<span data-ttu-id="d5035-124">De Microsoft.Compute-resourceprovider moet een URL naar het geheim in de Sleutelkluis tijdens het inrichten van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5035-124">The Microsoft.Compute resource provider needs a URL to the secret inside the Key Vault while provisioning the VM.</span></span> <span data-ttu-id="d5035-125">Hierdoor kunnen de Microsoft.Compute-resourceprovider voor het downloaden van het geheim en de equivalente certificaat maken op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d5035-125">This enables the Microsoft.Compute resource provider to download the secret and create the equivalent certificate on the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="d5035-126">De URL van het geheim moet de versie ook bevatten.</span><span class="sxs-lookup"><span data-stu-id="d5035-126">The URL of the secret needs to include the version as well.</span></span> <span data-ttu-id="d5035-127">Een voorbeeld-URL ziet eruit als hieronder https://contosovault.vault.azure.net:443/geheimen/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="d5035-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="d5035-128">Sjablonen</span><span class="sxs-lookup"><span data-stu-id="d5035-128">Templates</span></span>
<span data-ttu-id="d5035-129">Krijgt u de koppeling naar de URL in de sjabloon met behulp van de onderstaande code</span><span class="sxs-lookup"><span data-stu-id="d5035-129">You can get the link to the URL in the template using the below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="d5035-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5035-130">PowerShell</span></span>
<span data-ttu-id="d5035-131">U krijgt deze URL met de onderstaande PowerShell-opdracht</span><span class="sxs-lookup"><span data-stu-id="d5035-131">You can get this URL using the below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="d5035-132">Stap 5: Verwijzen naar de URL van uw zelf-ondertekende certificaten tijdens het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="d5035-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="d5035-133">Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="d5035-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="d5035-134">Het certificaat opgehaald bij het maken van een virtuele machine via sjablonen verwezen in de geheimen en de sectie winRM zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="d5035-134">While creating a VM through templates, the certificate gets referenced in the secrets section and the winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of the Key Vault containing the secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for the certificate you got in Step 4>",
                  "certificateStore": "<Name of the certificate store on the VM>"
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
                  "certificateUrl": "<URL for the certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="d5035-135">Een voorbeeldsjabloon voor de bovenstaande vindt u hier op [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="d5035-135">A sample template for the above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="d5035-136">De broncode voor deze sjabloon kunt u vinden op [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="d5035-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="d5035-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5035-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-to-the-vm"></a><span data-ttu-id="d5035-138">Stap 6: Verbinding maken met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="d5035-138">Step 6: Connecting to the VM</span></span>
<span data-ttu-id="d5035-139">Voordat u verbinding kunt maken met de virtuele machine moet u controleren of moet uw computer is geconfigureerd voor extern beheer met WinRM.</span><span class="sxs-lookup"><span data-stu-id="d5035-139">Before you can connect to the VM you'll need to make sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="d5035-140">Start PowerShell als beheerder en voer de onderstaande opdracht om te controleren of u alles hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d5035-140">Start PowerShell as an administrator and execute the below command to make sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="d5035-141">Mogelijk moet u controleren of dat de WinRM-service wordt uitgevoerd als de bovenstaande niet werkt.</span><span class="sxs-lookup"><span data-stu-id="d5035-141">You might need to make sure the WinRM service is running if the above does not work.</span></span> <span data-ttu-id="d5035-142">U kunt doen dat met`Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="d5035-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="d5035-143">Als de installatie is voltooid, kunt u met de virtuele machine via de onderstaande opdracht</span><span class="sxs-lookup"><span data-stu-id="d5035-143">Once the setup is done, you can connect to the VM using the below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
