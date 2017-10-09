---
title: 'Azure Active Directory Domain Services: Beheerdershandleiding | Microsoft Docs'
description: Lid worden van een Windows virtuele machine tooa beheerde domein met behulp van Azure PowerShell en Hallo klassieke implementatiemodel.
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a>Lid worden van een Windows Server virtuele machine tooa beheerde domein met behulp van PowerShell
> [!div class="op_single_selector"]
> * [Klassieke Azure-portal - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Azure AD Domain Services biedt momenteel geen ondersteuning voor Hallo Resource Manager-model.
>
>

Deze stappen ziet u hoe toocustomize een set van Azure PowerShell-opdrachten die maken en vooraf configureren van een op basis van Windows Azure virtuele machine met behulp van een benadering bouwsteen. Deze stappen kunt u een op basis van Windows Azure virtuele machine maken en deelnemen aan het beheerde domein van tooan Azure AD Domain Services.

Deze stappen volgt een benadering invullen-in-the-lege waarden voor het maken van Azure PowerShell-opdrachtsets. Deze methode kan nuttig zijn als u nieuwe tooPowerShell of tooknow welke toospecify waarden voor geslaagde configuratie gewenste. Geavanceerde PowerShell-gebruikers kunnen ondernemen Hallo opdrachten en vervangen door hun eigen waarden voor Hallo variabelen (Hallo regels beginnen met '$').

Als u dit nog niet hebt gedaan, gebruikt u de instructies Hallo in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell op de lokale computer. Vervolgens opent u een Windows PowerShell-opdrachtprompt.

## <a name="step-1-add-your-account"></a>Stap 1: Uw account toevoegen
1. Typ achter de PowerShell-prompt Hallo **Add-AzureAccount** en klik op **Enter**.
2. Typ Hallo e-mailadres gekoppeld aan uw Azure-abonnement en klik op **doorgaan**.
3. Typ in het Hallo-wachtwoord voor je account.
4. Klik op **aanmelden**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>Stap 2: Uw abonnement en storage-account instellen
Uw Azure-abonnement en storage-account instellen door deze opdrachten in Windows PowerShell-opdrachtprompt Hallo. Alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens, met de juiste namen Hallo vervangen.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Kunt u de naam van de juiste abonnement Hallo krijgen via Hallo SubscriptionName-eigenschap van Hallo Hallo **Get-AzureSubscription** opdracht. Kunt u Hallo juist opslagaccountnaam krijgen via de eigenschap Label van de uitvoer Hallo HALLO hallo **Get-AzureStorageAccount** opdracht, na het uitvoeren van Hallo **Select-AzureSubscription** opdracht.

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a>Stap 3: Stapsgewijze - Hallo virtuele machine in te richten en deelnemen aan het beheerde domein toohello
Hier volgt Hallo bijbehorende Azure PowerShell-opdracht set toocreate van deze virtuele machine, met lege regels tussen elk blok omwille van de leesbaarheid.

Geef informatie op over Hallo Windows virtuele machine toobe ingericht.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

Zie voor Hallo InstanceSize waarden voor D, DS of G-serie virtuele machines [virtuele Machine en Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

Bevatten informatie over Hallo beheerd domein.

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

Geef de naam Hallo van Hallo-cloudservice.

    $svcname="Contoso100-test"

Geef de naam Hallo Hallo virtueel netwerk toowhich Hallo die VM moet worden samengevoegd. Zorg ervoor dat Hallo beheerd AAD-DS-domein is beschikbaar in dit virtuele netwerk.

    $vnetname="MyPreviewVnet"

Selecteer Hallo VM-installatiekopie gebruikt toobe tooprovision Hallo VM.

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

Configureer Hallo VM - naam van de VM, exemplaar grootte en de installatiekopie toobe gebruikt.

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Lokale administrator-referenties voor Hallo VM ophalen. Kies een sterke lokale administrator-wachtwoord.

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

Referenties voor een gebruikersaccount die behoren too'AAD DC beheerders groep toojoin VM toohello beheerd domein ophalen. Geef geen domeinnaam Hallo - voor het exemplaar in ons voorbeeld opgegeven "bob" als Hallo-gebruikersnaam.

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

Configureer Hallo VM - domain join vereiste & vereiste referenties opgeven.

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

Een subnet voor VM Hallo ingesteld.

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

Optioneel: Punt toohello IP-adres van Hallo-domein. Als u op DNS-servers voor het virtuele netwerk Hallo Hallo IP-adressen van hello Azure AD Domain Services beheerd domein toobe Hallo instelt, is deze stap niet vereist.

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

Nu domein inrichten Hallo virtuele machine van Windows.

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a>Script tooprovision een virtuele machine van Windows en automatisch deelnemen aan tooan AAD Domain Services beheerd domein
Deze set PowerShell-opdracht maakt een virtuele machine voor een line-of-business-server die:

* Hallo Windows Server 2012 R2 Datacenter installatiekopie gebruikt.
* Is een extra klein virtuele machine.
* Hallo naam Contoso100-test heeft.
* Wordt automatisch lid toohello contoso100 beheerde domein.
* Is toegevoegd toohello hetzelfde virtuele netwerk als Hallo beheerd domein.

Hier volgt virtuele machine met het volledige voorbeeld script toocreate Hallo Windows hello en automatisch deelnemen aan toohello Azure AD Domain Services beheerd domein.

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a>Gerelateerde inhoud
* [Azure AD Domain Services - handleiding aan de slag](active-directory-ds-getting-started.md)
* [Een beheerd domein van Azure AD Domain Services beheren](active-directory-ds-admin-guide-administer-domain.md)
