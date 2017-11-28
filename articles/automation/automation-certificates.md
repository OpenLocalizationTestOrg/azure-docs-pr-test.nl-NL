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
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="69364-104">Certificaatassets in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="69364-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="69364-105">Certificaten kunnen worden veilig opgeslagen in Azure Automation zodat ze toegankelijk zijn voor runbooks of DSC-configuraties met Hallo **Get-AzureRmAutomationRmCertificate** activiteit voor Azure Resource Manager-resources.</span><span class="sxs-lookup"><span data-stu-id="69364-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using hello **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="69364-106">Dit kunt u toocreate runbooks en DSC-configuraties die certificaten voor verificatie gebruiken of tooAzure of een derde partij resources worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="69364-106">This allows you toocreate runbooks and DSC configurations that use certificates for authentication or adds them tooAzure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="69364-107">Beveiligde activa in Azure Automation zijn referenties, certificaten, verbindingen en gecodeerde variabelen.</span><span class="sxs-lookup"><span data-stu-id="69364-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="69364-108">Deze activa zijn versleuteld en opgeslagen in hello Azure Automation, met een unieke sleutel die wordt gegenereerd voor elk automation-account.</span><span class="sxs-lookup"><span data-stu-id="69364-108">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="69364-109">Deze sleutel is versleuteld met een basiscertificaat en opgeslagen in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="69364-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="69364-110">Voordat u een beveiligd bedrijfsmiddel op te slaan, Hallo-sleutel voor Hallo automation-account wordt ontsleuteld met behulp van het basiscertificaat Hallo en vervolgens gebruikt tooencrypt Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="69364-110">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="69364-111">Windows PowerShell-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="69364-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="69364-112">Hallo-cmdlets in de volgende tabel Hallo gebruikte toocreate zijn en beheren van automation-certificaat activa met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69364-112">hello cmdlets in hello following table are used toocreate and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="69364-113">Ze worden verzonden als onderdeel van Hallo [Azure PowerShell-module](../powershell-install-configure.md) die beschikbaar is voor gebruik in Automation-runbooks en DSC-configuraties.</span><span class="sxs-lookup"><span data-stu-id="69364-113">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="69364-114">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="69364-114">Cmdlets</span></span>|<span data-ttu-id="69364-115">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="69364-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="69364-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="69364-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="69364-117">Hiermee haalt informatie over een certificaat toouse in een runbook of de DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="69364-117">Retrieves information about a certificate toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="69364-118">U kunt alleen Hallo certificaat zelf ophalen van Get-AutomationCertificate activiteit.</span><span class="sxs-lookup"><span data-stu-id="69364-118">You can only retrieve hello certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="69364-119">Nieuwe AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="69364-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="69364-120">Maakt een nieuw certificaat in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="69364-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="69364-121">Verwijder AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="69364-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="69364-122">Hiermee verwijdert u een certificaat van Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="69364-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="69364-123">Maakt een nieuw certificaat in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="69364-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="69364-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="69364-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="69364-125">Hiermee stelt u Hallo-eigenschappen voor een bestaand certificaat, waaronder het Hallo-certificaatbestand en het wachtwoord van de instelling Hallo voor een .pfx-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="69364-125">Sets hello properties for an existing certificate including uploading hello certificate file and setting hello password for a .pfx.</span></span>|
|[<span data-ttu-id="69364-126">Voeg AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="69364-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="69364-127">Een servicecertificaat voor Hallo uploads opgegeven cloudservice.</span><span class="sxs-lookup"><span data-stu-id="69364-127">Uploads a service certificate for hello specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="69364-128">Een nieuw certificaat maken</span><span class="sxs-lookup"><span data-stu-id="69364-128">Creating a new certificate</span></span>

<span data-ttu-id="69364-129">Wanneer u een nieuw certificaat maakt, kunt u een cer- of pfx-bestand tooAzure Automation uploaden.</span><span class="sxs-lookup"><span data-stu-id="69364-129">When you create a new certificate, you upload a .cer or .pfx file tooAzure Automation.</span></span> <span data-ttu-id="69364-130">Als u Hallo certificaat als exporteerbaar markeren, kunt klikt u vervolgens u overbrengen deze buiten het hello Azure Automation-certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="69364-130">If you mark hello certificate as exportable, then you can transfer it out of hello Azure Automation certificate store.</span></span> <span data-ttu-id="69364-131">Als het is niet exporteerbaar, kan vervolgens alleen worden gebruikt voor het ondertekenen van binnen het Hallo-runbook of de DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="69364-131">If it is not exportable, then it can only be used for signing within hello runbook or DSC configuration.</span></span>


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a><span data-ttu-id="69364-132">toocreate een nieuw certificaat met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="69364-132">toocreate a new certificate with hello Azure portal</span></span>

1. <span data-ttu-id="69364-133">Klik op Hallo van uw Automation-account **activa** tegel tooopen hello **activa** blade.</span><span class="sxs-lookup"><span data-stu-id="69364-133">From your Automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
1. <span data-ttu-id="69364-134">Klik op Hallo **certificaten** tegel tooopen hello **certificaten** blade.</span><span class="sxs-lookup"><span data-stu-id="69364-134">Click hello **Certificates** tile tooopen hello **Certificates** blade.</span></span>
1. <span data-ttu-id="69364-135">Klik op **toevoegen van een certificaat** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="69364-135">Click **Add a certificate** at hello top of hello blade.</span></span>
2. <span data-ttu-id="69364-136">Typ een naam voor Hallo certificaat in Hallo **naam** vak.</span><span class="sxs-lookup"><span data-stu-id="69364-136">Type a name for hello certificate in hello **Name** box.</span></span>
2. <span data-ttu-id="69364-137">Klik op **selecteert u een bestand** onder **uploaden van een certificaatbestand** toobrowse voor een cer- of pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="69364-137">Click **Select a file** under **Upload a certificate file** toobrowse for a .cer or .pfx file.</span></span>  <span data-ttu-id="69364-138">Als u een .pfx-bestand selecteert, geeft u een wachtwoord en of deze moet worden toegestaan toobe geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="69364-138">If you select a .pfx file, specify a password and whether it should be allowed toobe exported.</span></span>
1. <span data-ttu-id="69364-139">Klik op **maken** toosave Hallo nieuwe certificaatasset.</span><span class="sxs-lookup"><span data-stu-id="69364-139">Click **Create** toosave hello new certificate asset.</span></span>


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="69364-140">toocreate een nieuw certificaat met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="69364-140">toocreate a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="69364-141">Hallo volgende voorbeeld laat zien hoe toocreate een nieuw Automation-certificaat en deze exporteerbaar markeren.</span><span class="sxs-lookup"><span data-stu-id="69364-141">hello following example demonstrates how toocreate a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="69364-142">Hiermee importeert een bestaande pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="69364-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="69364-143">Gebruik van een certificaat</span><span class="sxs-lookup"><span data-stu-id="69364-143">Using a certificate</span></span>

<span data-ttu-id="69364-144">Moet u Hallo **Get-AutomationCertificate** activiteit toouse een certificaat.</span><span class="sxs-lookup"><span data-stu-id="69364-144">You must use hello **Get-AutomationCertificate** activity toouse a certificate.</span></span> <span data-ttu-id="69364-145">U kunt geen hello gebruiken [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet omdat deze informatie over het Hallo-certificaatasset maar niet Hallo certificaat zelf retourneert.</span><span class="sxs-lookup"><span data-stu-id="69364-145">You cannot use hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about hello certificate asset but not hello certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="69364-146">Voorbeeld van tekstueel runbook</span><span class="sxs-lookup"><span data-stu-id="69364-146">Textual runbook sample</span></span>

<span data-ttu-id="69364-147">Hallo volgende voorbeeldcode ziet u hoe een certificaat tooa tooadd cloudservice in een runbook.</span><span class="sxs-lookup"><span data-stu-id="69364-147">hello following sample code shows how tooadd a certificate tooa cloud service in a runbook.</span></span> <span data-ttu-id="69364-148">Hallo-wachtwoord wordt in dit voorbeeld wordt opgehaald uit een versleutelde automation-variabele.</span><span class="sxs-lookup"><span data-stu-id="69364-148">In this sample, hello password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="69364-149">Grafisch runbook-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="69364-149">Graphical runbook sample</span></span>

<span data-ttu-id="69364-150">U toevoegen een **Get-AutomationCertificate** tooa grafisch runbook door met de rechtermuisknop op het Hallo-certificaat in Hallo bibliotheek deelvenster van de grafische editor Hallo en het selecteren van **toocanvas toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="69364-150">You add a **Get-AutomationCertificate** tooa graphical runbook by right-clicking on hello certificate in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![Certificaat toohello canvas toevoegen](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="69364-152">Hallo toont volgende afbeelding een voorbeeld van het gebruik van een certificaat in een grafisch runbook.</span><span class="sxs-lookup"><span data-stu-id="69364-152">hello following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="69364-153">Dit Hallo is voor het toevoegen van een cloudservice van certificaat tooa uit tekstueel runbook bovenstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="69364-153">This is hello same example shown above for adding a certificate tooa cloud service from a textual runbook.</span></span>

![<span data-ttu-id="69364-154">Voorbeeld grafisch ontwerpen</span><span class="sxs-lookup"><span data-stu-id="69364-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="69364-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="69364-155">Next steps</span></span>

- <span data-ttu-id="69364-156">meer informatie over het werken met koppelingen toocontrol Hallo logische stroom van de activiteiten van uw runbook is toolearn tooperform ontworpen, Zie [koppelingen in het grafisch ontwerpen](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="69364-156">toolearn more about working with links toocontrol hello logical flow of activities your runbook is designed tooperform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
