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
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a>WinRM toegang instellen voor virtuele Machines in Azure Resource Manager
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a>WinRM in de Azure Service Management vs Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* Voor een overzicht van hello Azure Resource Manager, raadpleegt u dit [artikel](../../azure-resource-manager/resource-group-overview.md)
* Voor de verschillen tussen Azure-servicebeheer en Azure Resource Manager, raadpleegt u dit [artikel](../../resource-manager-deployment-model.md)

Hallo is belangrijk verschil bij het instellen van de WinRM-configuratie tussen twee stacks Hallo hoe Hallo certificaat op Hallo VM wordt geïnstalleerd. In Azure Resource Manager-stack hello, worden certificaten Hallo gemodelleerd als bronnen die worden beheerd door Hallo Key Vault Resource Provider. Daarom Hallo gebruiker moet tooprovide hun eigen certificaat en upload het tooa Sleutelkluis voordat u deze in een virtuele machine.

Hier volgen Hallo stappen u moet tootake tooset van een virtuele machine met de WinRM-connectiviteit

1. Een sleutelkluis maken
2. Een zelfondertekend certificaat maken
3. Uploaden van uw zelf-ondertekend certificaat tooKey kluis
4. Hallo-URL voor uw zelf-ondertekend certificaat in Hallo Sleutelkluis ophalen
5. Verwijst naar de URL van uw zelf-ondertekende certificaten tijdens het maken van een virtuele machine

## <a name="step-1-create-a-key-vault"></a>Stap 1: Een Sleutelkluis maken
U kunt Hallo onderstaande opdracht toocreate hello Sleutelkluis

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a>Stap 2: Een zelfondertekend certificaat maken
U kunt een zelfondertekend certificaat met deze PowerShell-script maken

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a>Stap 3: Uw zelf-ondertekend certificaat toohello Sleutelkluis uploaden
Voordat uploaden Hallo certificaat toohello Sleutelkluis in stap 1 gemaakt, moet deze tooconverted in een indeling Hallo Microsoft.Compute-resourceprovider wordt begrepen. Hallo onderstaande PowerShell-script kunt u dat doen

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

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a>Stap 4: Hallo-URL voor uw zelf-ondertekend certificaat in Hallo Sleutelkluis ophalen
Hallo Microsoft.Compute-resourceprovider moet een URL toohello geheim binnen Hallo Sleutelkluis tijdens het Hallo VM-inrichting. Dit kunt Hallo Microsoft.Compute resource provider toodownload Hallo geheim en Hallo gelijkwaardige certificaat maken op Hallo VM.

> [!NOTE]
> Hallo-URL van Hallo geheim moet ook tooinclude Hallo-versie. Een voorbeeld-URL ziet eruit als hieronder https://contosovault.vault.azure.net:443/geheimen/contososecret/01h9db0df2cd4300a20ence585a6s7ve
> 
> 

#### <a name="templates"></a>Sjablonen
U kunt Hallo koppeling toohello URL krijgen in Hallo onder code met Hallo-sjabloon

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a>PowerShell
U kunt deze URL met Hallo onderstaande PowerShell-opdracht ophalen

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a>Stap 5: Verwijzen naar de URL van uw zelf-ondertekende certificaten tijdens het maken van een virtuele machine
#### <a name="azure-resource-manager-templates"></a>Azure Resource Manager-sjablonen
Hallo certificaat opgehaald bij het maken van een virtuele machine via sjablonen verwezen in Hallo geheimen en Hallo winRM sectie zoals hieronder:

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

Een voorbeeldsjabloon voor Hallo bovenstaande vindt u hier op [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)

De broncode voor deze sjabloon kunt u vinden op [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)

#### <a name="powershell"></a>PowerShell
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a>Stap 6: Verbinding maken met toohello VM
Voordat u verbinding met toohello VM maken kunt moet u ervoor dat uw computer is geconfigureerd voor extern beheer met WinRM toomake. Start PowerShell als beheerder en voer uit Hallo onderstaande opdracht toomake zeker dat u alles hebt ingesteld.

    Enable-PSRemoting -Force

> [!NOTE]
> Mogelijk moet u toomake ervoor Hallo WinRM-service wordt uitgevoerd als Hallo hierboven niet werkt. U kunt doen dat met`Get-Service WinRM`
> 
> 

Als Hallo setup is voltooid, kunt u toohello VM Hallo onder opdracht met

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
