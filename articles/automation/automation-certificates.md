---
title: aaaCertificate activa in Azure Automation | Microsoft Docs
description: Certificaten kunnen veilig worden opgeslagen in Azure Automation zodat ze toegankelijk zijn voor runbooks of DSC-configuraties tooauthenticate tegen Azure en resources van derden.  Dit artikel wordt uitgelegd Hallo details van certificaten en hoe toowork ermee in tekstvorm en grafisch ontwerpen.
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Certificaatassets in Azure Automation

Certificaten kunnen worden veilig opgeslagen in Azure Automation zodat ze toegankelijk zijn voor runbooks of DSC-configuraties met Hallo **Get-AzureRmAutomationRmCertificate** activiteit voor Azure Resource Manager-resources. Dit kunt u toocreate runbooks en DSC-configuraties die certificaten voor verificatie gebruiken of tooAzure of een derde partij resources worden toegevoegd.

> [!NOTE] 
> Beveiligde activa in Azure Automation zijn referenties, certificaten, verbindingen en gecodeerde variabelen. Deze activa zijn versleuteld en opgeslagen in hello Azure Automation, met een unieke sleutel die wordt gegenereerd voor elk automation-account. Deze sleutel is versleuteld met een basiscertificaat en opgeslagen in Azure Automation. Voordat u een beveiligd bedrijfsmiddel op te slaan, Hallo-sleutel voor Hallo automation-account wordt ontsleuteld met behulp van het basiscertificaat Hallo en vervolgens gebruikt tooencrypt Hallo asset.
> 

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell-Cmdlets

Hallo-cmdlets in de volgende tabel Hallo gebruikte toocreate zijn en beheren van automation-certificaat activa met Windows PowerShell. Ze worden verzonden als onderdeel van Hallo [Azure PowerShell-module](../powershell-install-configure.md) die beschikbaar is voor gebruik in Automation-runbooks en DSC-configuraties.

|Cmdlets|Beschrijving|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx)|Hiermee haalt informatie over een certificaat toouse in een runbook of de DSC-configuratie. U kunt alleen Hallo certificaat zelf ophalen van Get-AutomationCertificate activiteit.|
|[Nieuwe AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603604.aspx)|Maakt een nieuw certificaat in Azure Automation.|
[Verwijder AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603529.aspx)|Hiermee verwijdert u een certificaat van Azure Automation.|Maakt een nieuw certificaat in Azure Automation.
|[Set-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603760.aspx)|Hiermee stelt u Hallo-eigenschappen voor een bestaand certificaat, waaronder het Hallo-certificaatbestand en het wachtwoord van de instelling Hallo voor een .pfx-bestand uploaden.|
|[Voeg AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Een servicecertificaat voor Hallo uploads opgegeven cloudservice.|


## <a name="creating-a-new-certificate"></a>Een nieuw certificaat maken

Wanneer u een nieuw certificaat maakt, kunt u een cer- of pfx-bestand tooAzure Automation uploaden. Als u Hallo certificaat als exporteerbaar markeren, kunt klikt u vervolgens u overbrengen deze buiten het hello Azure Automation-certificaatarchief. Als het is niet exporteerbaar, kan vervolgens alleen worden gebruikt voor het ondertekenen van binnen het Hallo-runbook of de DSC-configuratie.


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a>toocreate een nieuw certificaat met hello Azure-portal

1. Klik op Hallo van uw Automation-account **activa** tegel tooopen hello **activa** blade.
1. Klik op Hallo **certificaten** tegel tooopen hello **certificaten** blade.
1. Klik op **toevoegen van een certificaat** Hallo boven aan het Hallo-blade.
2. Typ een naam voor Hallo certificaat in Hallo **naam** vak.
2. Klik op **selecteert u een bestand** onder **uploaden van een certificaatbestand** toobrowse voor een cer- of pfx-bestand.  Als u een .pfx-bestand selecteert, geeft u een wachtwoord en of deze moet worden toegestaan toobe geëxporteerd.
1. Klik op **maken** toosave Hallo nieuwe certificaatasset.


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a>toocreate een nieuw certificaat met Windows PowerShell

Hallo volgende voorbeeld laat zien hoe toocreate een nieuw Automation-certificaat en deze exporteerbaar markeren. Hiermee importeert een bestaande pfx-bestand.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>Gebruik van een certificaat

Moet u Hallo **Get-AutomationCertificate** activiteit toouse een certificaat. U kunt geen hello gebruiken [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet omdat deze informatie over het Hallo-certificaatasset maar niet Hallo certificaat zelf retourneert.

### <a name="textual-runbook-sample"></a>Voorbeeld van tekstueel runbook

Hallo volgende voorbeeldcode ziet u hoe een certificaat tooa tooadd cloudservice in een runbook. Hallo-wachtwoord wordt in dit voorbeeld wordt opgehaald uit een versleutelde automation-variabele.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>Grafisch runbook-voorbeeld

U toevoegen een **Get-AutomationCertificate** tooa grafisch runbook door met de rechtermuisknop op het Hallo-certificaat in Hallo bibliotheek deelvenster van de grafische editor Hallo en het selecteren van **toocanvas toevoegen**.

![Certificaat toohello canvas toevoegen](media/automation-certificates/automation-certificate-add-to-canvas.png)

Hallo toont volgende afbeelding een voorbeeld van het gebruik van een certificaat in een grafisch runbook.  Dit Hallo is voor het toevoegen van een cloudservice van certificaat tooa uit tekstueel runbook bovenstaande voorbeeld.

![Voorbeeld grafisch ontwerpen ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a>Volgende stappen

- meer informatie over het werken met koppelingen toocontrol Hallo logische stroom van de activiteiten van uw runbook is toolearn tooperform ontworpen, Zie [koppelingen in het grafisch ontwerpen](automation-graphical-authoring-intro.md#links-and-workflow). 
