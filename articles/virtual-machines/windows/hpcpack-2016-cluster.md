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
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a>Een HPC Pack 2016-cluster in Azure implementeren

Hallo-stappen in dit artikel toodeploy een [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtuele machines. HPC Pack is oplossing van Microsoft gratis HPC gebaseerd op Microsoft Azure en Windows Server-technologieën en biedt ondersteuning voor een breed bereik van HPC-workloads.

Gebruik een van de Hallo [Azure Resource Manager-sjablonen](https://github.com/MsHpcPack/HPCPack2016) toodeploy Hallo HPC Pack 2016 cluster. U hebt verschillende mogelijkheden van de clustertopologie met verschillende aantallen head clusterknooppunten en met beide Linux of Windows rekenknooppunten.

## <a name="prerequisites"></a>Vereisten

### <a name="pfx-certificate"></a>PFX-certificaat

Een cluster met Microsoft HPC Pack 2016 vereist een Personal Information Exchange (PFX) certificaat toosecure Hallo communicatie tussen Hallo HPC-knooppunten. Hallo-certificaat moet voldoen aan Hallo volgens de vereisten:

* Er moet een persoonlijke sleutel sleuteluitwisseling
* Sleutelgebruik bevat digitale handtekening en sleutelcodering
* Uitgebreid sleutelgebruik bevat clientverificatie en serververificatie

Als u geen al een certificaat dat aan deze vereisten voldoet, kunt u Hallo certificaat aanvragen bij een certificeringsinstantie (CA). U kunt ook Hallo na opdrachten toogenerate Hallo zelf-ondertekend certificaat op basis van Hallo besturingssysteem waarop u Hallo-opdracht uitvoert en Hallo PFX-indeling certificaat met persoonlijke sleutel exporteren.

* **Voor Windows 10 of Windows Server 2016**, uitvoeren van de ingebouwde Hallo **nieuw SelfSignedCertificate** PowerShell-cmdlet als volgt:

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* **Voor besturingssystemen ouder dan Windows 10 of Windows Server 2016**, downloaden Hallo [zelf-ondertekend certificaat generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) van Hallo Microsoft Script Center. Pak de inhoud en Voer Hallo opdrachten op een PowerShell-prompt te volgen:

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a>Certificaat tooan Azure sleutelkluis uploaden

Voordat u Hallo HPC-cluster implementeert, uploaden Hallo certificaat tooan [Azure sleutelkluis](../../key-vault/index.md) als een geheim en record Hallo volgende informatie voor gebruik tijdens de implementatie van Hallo: **kluisnaam**,  **De resourcegroep kluis**, **certificaat-URL**, en **certificaatvingerafdruk**.

Er volgt een voorbeeld PowerShell script tooupload Hallo-certificaat. Zie voor meer informatie over het uploaden van een certificaat tooan Azure sleutelkluis [aan de slag met Azure Key Vault](../../key-vault/key-vault-get-started.md).

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


## <a name="supported-topologies"></a>Ondersteunde topologieën

Kies een van de Hallo [Azure Resource Manager-sjablonen](https://github.com/MsHpcPack/HPCPack2016) toodeploy Hallo HPC Pack 2016 cluster. Hieronder vindt u op hoog niveau van de drie ondersteunde clustertopologieën-architecturen. Hoge beschikbaarheid topologieën bevatten meerdere head clusterknooppunten.

1. Cluster met hoge beschikbaarheid met Active Directory-domein

    ![HA-cluster in AD-domein](./media/hpcpack-2016-cluster/haad.png)



2. Cluster met hoge beschikbaarheid zonder Active Directory-domein

    ![HA cluster zonder AD-domein](./media/hpcpack-2016-cluster/hanoad.png)

3. Cluster met slechts één hoofdknooppunt

   ![Cluster met één hoofdknooppunt](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a>Een cluster implementeren

toocreate hello cluster, kiest u een sjabloon en klikt u op **tooAzure implementeren**. In Hallo [Azure-portal](https://portal.azure.com), Geef parameters op voor de sjabloon Hallo zoals beschreven in de volgende stappen uit Hallo. Elke sjabloon wordt gemaakt van alle Azure-resources die vereist zijn voor Hallo HPC-clusterinfrastructuur. Resources omvatten een Azure-netwerk, openbare IP-adres, load balancer (alleen voor een cluster met hoge beschikbaarheid), netwerkinterfaces, beschikbaarheidssets, opslagaccounts en virtuele machines.

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a>Stap 1: Selecteer Hallo abonnement, de locatie en de resourcegroep

Hallo **abonnement** en Hallo **locatie** moet hetzelfde zijn die u hebt opgegeven dat wanneer u het PFX-certificaat geüpload (Zie vereisten). Het is raadzaam dat u maakt een **resourcegroep** voor Hallo-implementatie.

### <a name="step-2-specify-hello-parameter-settings"></a>Stap 2: Geef de parameterinstellingen Hallo

Invoeren of wijzigen van waarden voor de sjabloonparameters Hallo. Klik op Hallo pictogram volgende tooeach-parameter voor help-informatie. Zie ook Hallo richtlijnen voor [beschikbare VM-grootten](sizes.md).

U hebt vastgelegd in het Hallo-vereisten voor de volgende parameters Hallo Hallo-waarden opgeven: **kluisnaam**, **kluis resourcegroep**, **certificaat-URL**, en **Certificaatvingerafdruk**.

### <a name="step-3-review-legal-terms-and-create"></a>Stap 3. Juridische voorwaarden bekijken en maken
Klik op **juridische voorwaarden bekijken** tooreview Hallo voorwaarden. Als u akkoord gaat, klikt u op **aankoop**, en klik vervolgens op **maken** toostart Hallo-implementatie.

## <a name="connect-toohello-cluster"></a>Verbinding maken met cluster toohello
1. Nadat het Hallo HPC Pack cluster is geïmplementeerd, gaat u toohello [Azure-portal](https://portal.azure.com). Klik op **resourcegroepen**, en zoek Hallo-resourcegroep in welke Hallo cluster is geïmplementeerd. U vindt Hallo hoofdknooppunt virtuele machines.

    ![Head clusterknooppunten in Hallo-portal](./media/hpcpack-2016-cluster/clusterhns.png)

2. Klik op één hoofdknooppunt (in een cluster met hoge beschikbaarheid, klik op een van de hoofdknooppunten Hallo). In **Essentials**, kunt u vinden Hallo openbaar IP-adres of de volledige DNS-naam van Hallo-cluster.

    ![Cluster-verbindingsinstellingen](./media/hpcpack-2016-cluster/clusterconnect.png)

3. Klik op **Connect** toolog op tooany van Hallo hoofdknooppunten met extern bureaublad met uw beheerder van de opgegeven gebruikersnaam. Als Hallo cluster die u hebt geïmplementeerd in een Active Directory-domein, gebruikersnaam Hallo heeft de vorm van Hallo <privateDomainName> \<adminUsername > (bijvoorbeeld hpc.local\hpcadmin).

## <a name="next-steps"></a>Volgende stappen
* Verzenden van taken tooyour cluster. Zie [verzenden van taken tooHPC een HPC Pack-cluster in Azure](hpcpack-cluster-submit-jobs.md) en [een HPC Pack 2016-cluster in Azure met Azure Active Directory beheren](hpcpack-cluster-active-directory.md).

