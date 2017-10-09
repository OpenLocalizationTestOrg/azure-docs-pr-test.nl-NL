---
title: aaaInstall en Terraform tooprovision VM's en andere infrastructuur configureren in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall en configureer Terraform toocreate Azure resources
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a>Installeer en configureer Terraform tooprovision VM's en andere infrastructuur in Azure 
Dit artikel beschrijft Hallo nodige tooinstall en Terraform tooprovision resources, zoals virtuele machines in Azure te configureren. U leert hoe toocreate en het gebruik van Azure-referenties tooenable Terraform tooprovision cloud-bronnen op een veilige manier.

HashiCorp Terraform biedt een eenvoudige manier toodefine en cloudinfrastructuur implementeren met behulp van een aangepaste templating taal HashiCorp configuratie taal (lijst met compatibele hardware) genoemd. Deze aangepaste taal is [eenvoudig toowrite en eenvoudig toounderstand](terraform-create-complete-vm.md). Bovendien via Hallo `terraform plan` uitvoert, en u kunt Hallo wijzigingen tooyour infrastructuur visualiseren voordat u ze vastlegt. Volg deze stappen toostart Terraform gebruiken met Azure.

## <a name="install-terraform"></a>Terraform installeren
tooinstall Terraform, [downloaden](https://www.terraform.io/downloads.html) Hallo pakket geschikt is voor uw besturingssysteem in een afzonderlijke installatiemap. Hallo download bevat één uitvoerbaar bestand, waarvoor moet u ook een globale pad definiëren. Voor instructies over hoe tooset Hallo pad op Linux- en Mac, gaat u te[deze webpagina](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux). Voor instructies over hoe tooset pad op Windows hello te gaat[deze webpagina](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows). tooverify uw installatie uitvoeren Hallo `terraform` opdracht. U ziet een lijst met beschikbare Terraform opties als uitvoer.

Vervolgens moet u tooallow Terraform toegang tooyour Azure-abonnement tooperform infrastructuur inrichten.

## <a name="set-up-terraform-access-tooazure"></a>Terraform toegang tooAzure instellen
tooenable Terraform tooprovision resources in Azure, moet u twee entiteiten toocreate in Azure Active Directory (Azure AD): een Azure AD-toepassing en een Azure AD-service-principal. Vervolgens gebruikt u deze entiteiten id's in uw Terraform-scripts. Een service-principal is een lokaal exemplaar van een globale Azure AD-toepassing. Een service-principal kunt gedetailleerde lokale toegang tooglobal controlemiddelen.

Er zijn verschillende manieren toocreate een Azure AD-toepassing en een Azure AD-service-principal. Hallo snelst en eenvoudigst is manier vandaag de dag toouse Azure CLI 2.0, die [u kunt downloaden en installeren op Windows, Linux of een Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). U kunt ook PowerShell of Azure CLI 1.0 toocreate Hallo nodig beveiligingsinfrastructuur gebruiken. Hallo instructies hoe u tooconfigure Terraform voor Azure met behulp van alle van deze methoden.

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a>Azure CLI 2.0 gebruiken (voor Windows, Linux of Mac-gebruikers) 
Nadat u downloadt en Hallo installeert [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), tooadminister aanmelden met uw Azure-abonnement door uitgifte van Hallo volgende opdracht:

```
az login
```

>[!NOTE]
>Als u Hallo China, Duitse Azure of Azure Government clouds gebruikt, moet u toofirst hello Azure CLI toowork configureren met die cloud. U kunt dit doen door het uitvoeren van de volgende Hallo:

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

Als u meerdere Azure-abonnementen hebt, de bijbehorende gegevens worden geretourneerd door Hallo `az login` opdracht. Set Hallo `SUBSCRIPTION_ID` omgeving variabele toohold Hallo waarde Hallo geretourneerd `id` veld Hallo abonnement u wilt dat toouse. 

Hallo-abonnement dat u toouse voor deze sessie wilt instellen.

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

Hallo account tooget Hallo abonnements-ID opvragen en tenant-id-waarden.

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

Vervolgens maakt u afzonderlijke referenties voor Terraform.

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

De appId, wachtwoord, sp_name en tenant worden geretourneerd. Maak een notitie van Hallo appId en het wachtwoord.

tooconfirm uw referenties (service-principal), opent u een nieuwe shell en Voer Hallo opdrachten te volgen. Vervang Hallo waarden voor sp_name, wachtwoord en tenant geretourneerd:

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a>Gebruik PowerShell (voor Windows-gebruikers) 
toouse een Windows toowrite machine en voer uw Terraform scripts en toouse PowerShell voor configuratietaken uw machine met de juiste PowerShell hulpmiddelen Hallo configureren. 

1. Hulpprogramma's voor PowerShell installeren door de stappen te volgen Hallo in [installeren en configureren van Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). 

2. Downloaden en uitvoeren van Hallo [azure setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) vanaf Hallo PowerShell-console.

3. toorun hello azure setup.ps1 script downloaden en uitvoeren van Hallo `./azure-setup.ps1 setup` opdracht Hallo PowerShell-console. Meld u vervolgens aan tooyour Azure-abonnement met beheerdersbevoegdheden.

4. Geef de toepassingsnaam van een (willekeurige tekenreeks, vereist) als u wordt gevraagd. Geef eventueel een sterk wachtwoord wanneer u wordt gevraagd. Als u een wachtwoord niet opgeeft, wordt een sterk wachtwoord voor u gegenereerd met behulp van .NET-bibliotheken voor beveiliging.

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a>Gebruik van Azure CLI 1.0 (voor Linux- of Mac-gebruikers)
tooget is gestart met Terraform op Linux-machines of Macs met Azure CLI 1.0 installeren Hallo juiste bibliotheken op uw computer.  

1. Azure xPlat CLI-hulpprogramma's installeren door de stappen te volgen Hallo in [2.0 voor Azure CLI installeren](https://docs.microsoft.com/cli/azure/install-azure-cli). 

2. Download en installeer een JSON-processor door Hallo-instructies in [jq downloaden](https://stedolan.github.io/jq/download/).

3. Downloaden en uitvoeren van Hallo [azure setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script vanaf Hallo-console.

4. toorun hello azure setup.sh script downloaden en uitvoeren van Hallo `./azure-setup setup` opdracht vanuit Hallo-console. Meld u vervolgens aan tooyour Azure-abonnement met beheerdersbevoegdheden.
 
5. Geef de toepassingsnaam van een (willekeurige tekenreeks, vereist) als u wordt gevraagd. Geef eventueel een sterk wachtwoord wanneer u wordt gevraagd. Als u een wachtwoord niet opgeeft, wordt een sterk wachtwoord voor u gegenereerd met behulp van .NET-bibliotheken voor beveiliging.

Alle eerdere Hallo-scripts maken een Azure AD-toepassing en service principal. Hallo service-principal haalt een bijdrager of het niveau van de eigenaar toegang op Hallo-abonnement. Vanwege Hallo hoog niveau van toegang verleend, moet u altijd Hallo beveiligingsgegevens die worden gegenereerd door deze scripts te beschermen. Maak een notitie van vier stukjes beveiligingsinformatie van deze scripts: appId, wachtwoord, subscription_id en tenant_id.

## <a name="set-environment-variables"></a>De omgevingsvariabelen instellen
Nadat u maken en configureren van een service-principal voor Azure AD, moet u toolet Terraform weten Hallo tenant-ID, abonnements-ID, client-ID en de geheime toouse client. U kunt dit doen door deze waarden insluiten in uw Terraform scripts, zoals beschreven in [de basisinfrastructuur maken met behulp van Terraform](terraform-create-complete-vm.md). Ook stelt u na omgevingsvariabelen hello (en dus niet per ongeluk controleren of delen van uw referenties):

- ARM_SUBSCRIPTION_ID
- ARM_CLIENT_ID
- ARM_CLIENT_SECRET
- ARM_TENANT_ID

U kunt dit voorbeeld shell-script tooset die variabelen gebruiken:

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

Bovendien, als u Terraform met Azure in China of ofwel Azure Government of Duitse Azure gebruikt, moet u tooset Hallo omgevingsvariabele op de juiste wijze.

## <a name="next-steps"></a>Volgende stappen
U hebt nu Terraform geïnstalleerd en geconfigureerd Azure-referenties, zodat u kunt starten infrastructuur implementeren in uw Azure-abonnement. Vervolgens leert u hoe te[infrastructuur maken met Terraform](terraform-create-complete-vm.md).
