---
title: Het certificaat van de activa in Azure Automation | Microsoft Docs
description: Certificaten kunnen veilig worden opgeslagen in Azure Automation zodat ze toegankelijk zijn voor runbooks of DSC-configuraties worden geverifieerd bij Azure en resources van derden.  Dit artikel wordt uitgelegd dat de details van certificaten en het werken met hen in tekstvorm en grafisch ontwerpen.
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
ms.openlocfilehash: fd1737a420c132dace9307436bfea98a9bde94a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="794fc-104">Certificaatassets in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="794fc-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="794fc-105">Certificaten kunnen worden veilig opgeslagen in Azure Automation zodat ze toegankelijk zijn voor runbooks of DSC-configuraties met behulp van de **Get-AzureRmAutomationRmCertificate** activiteit voor Azure Resource Manager-resources.</span><span class="sxs-lookup"><span data-stu-id="794fc-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using the **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="794fc-106">Dit kunt u runbooks en DSC-configuraties die certificaten voor verificatie gebruiken maken of deze worden toegevoegd aan de resources in Azure of een derde partij.</span><span class="sxs-lookup"><span data-stu-id="794fc-106">This allows you to create runbooks and DSC configurations that use certificates for authentication or adds them to Azure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="794fc-107">Beveiligde activa in Azure Automation zijn referenties, certificaten, verbindingen en gecodeerde variabelen.</span><span class="sxs-lookup"><span data-stu-id="794fc-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="794fc-108">Deze activa zijn versleuteld en opgeslagen in de Azure Automation met een unieke sleutel die wordt gegenereerd voor elk automation-account.</span><span class="sxs-lookup"><span data-stu-id="794fc-108">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="794fc-109">Deze sleutel is versleuteld met een basiscertificaat en opgeslagen in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="794fc-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="794fc-110">Voordat u een beveiligd bedrijfsmiddel op te slaan, wordt de sleutel voor het automation-account worden ontsleuteld met het basiscertificaat en vervolgens worden gebruikt voor het versleutelen van de asset.</span><span class="sxs-lookup"><span data-stu-id="794fc-110">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="794fc-111">Windows PowerShell-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="794fc-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="794fc-112">De cmdlets in de volgende tabel worden gebruikt voor het maken en beheren van automation-certificaat activa met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="794fc-112">The cmdlets in the following table are used to create and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="794fc-113">Ze worden verzonden als onderdeel van de [Azure PowerShell-module](../powershell-install-configure.md) die beschikbaar is voor gebruik in Automation-runbooks en DSC-configuraties.</span><span class="sxs-lookup"><span data-stu-id="794fc-113">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="794fc-114">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="794fc-114">Cmdlets</span></span>|<span data-ttu-id="794fc-115">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="794fc-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="794fc-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="794fc-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="794fc-117">Hiermee haalt informatie over een certificaat wilt gebruiken in een runbook of de DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="794fc-117">Retrieves information about a certificate to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="794fc-118">U kunt alleen het certificaat zelf ophalen van Get-AutomationCertificate activiteit.</span><span class="sxs-lookup"><span data-stu-id="794fc-118">You can only retrieve the certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="794fc-119">Nieuwe AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="794fc-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="794fc-120">Maakt een nieuw certificaat in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="794fc-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="794fc-121">Verwijder AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="794fc-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="794fc-122">Hiermee verwijdert u een certificaat van Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="794fc-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="794fc-123">Maakt een nieuw certificaat in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="794fc-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="794fc-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="794fc-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="794fc-125">Hiermee stelt u de eigenschappen voor een bestaand certificaat, met inbegrip van het certificaat te uploaden en het instellen van het wachtwoord voor een .pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="794fc-125">Sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.</span></span>|
|[<span data-ttu-id="794fc-126">Voeg AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="794fc-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="794fc-127">Een certificaat voor de opgegeven cloud-service geüpload.</span><span class="sxs-lookup"><span data-stu-id="794fc-127">Uploads a service certificate for the specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="794fc-128">Een nieuw certificaat maken</span><span class="sxs-lookup"><span data-stu-id="794fc-128">Creating a new certificate</span></span>

<span data-ttu-id="794fc-129">Wanneer u een nieuw certificaat maakt, wordt het een cer- of pfx-bestand uploaden naar Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="794fc-129">When you create a new certificate, you upload a .cer or .pfx file to Azure Automation.</span></span> <span data-ttu-id="794fc-130">Als u het certificaat als exporteerbaar markeren, kunt klikt u vervolgens u overbrengen deze buiten het Azure Automation-certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="794fc-130">If you mark the certificate as exportable, then you can transfer it out of the Azure Automation certificate store.</span></span> <span data-ttu-id="794fc-131">Als het is niet exporteerbaar, kan vervolgens alleen worden gebruikt voor het ondertekenen van binnen het runbook of de DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="794fc-131">If it is not exportable, then it can only be used for signing within the runbook or DSC configuration.</span></span>


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a><span data-ttu-id="794fc-132">Een nieuw certificaat maken met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="794fc-132">To create a new certificate with the Azure portal</span></span>

1. <span data-ttu-id="794fc-133">Van uw Automation-account, klikt u op de **activa** tegel openen de **activa** blade.</span><span class="sxs-lookup"><span data-stu-id="794fc-133">From your Automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
1. <span data-ttu-id="794fc-134">Klik op de **certificaten** tegel openen de **certificaten** blade.</span><span class="sxs-lookup"><span data-stu-id="794fc-134">Click the **Certificates** tile to open the **Certificates** blade.</span></span>
1. <span data-ttu-id="794fc-135">Klik op **toevoegen van een certificaat** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="794fc-135">Click **Add a certificate** at the top of the blade.</span></span>
2. <span data-ttu-id="794fc-136">Typ een naam voor het certificaat in de **naam** vak.</span><span class="sxs-lookup"><span data-stu-id="794fc-136">Type a name for the certificate in the **Name** box.</span></span>
2. <span data-ttu-id="794fc-137">Klik op **selecteert u een bestand** onder **uploaden van een certificaatbestand** naar een cer- of pfx-bestand te bladeren.</span><span class="sxs-lookup"><span data-stu-id="794fc-137">Click **Select a file** under **Upload a certificate file** to browse for a .cer or .pfx file.</span></span>  <span data-ttu-id="794fc-138">Als u een .pfx-bestand selecteert, geeft u een wachtwoord en of deze moet kunnen worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="794fc-138">If you select a .pfx file, specify a password and whether it should be allowed to be exported.</span></span>
1. <span data-ttu-id="794fc-139">Klik op **maken** om op te slaan van het nieuwe certificaat actief.</span><span class="sxs-lookup"><span data-stu-id="794fc-139">Click **Create** to save the new certificate asset.</span></span>


### <a name="to-create-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="794fc-140">Een nieuw certificaat maken met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="794fc-140">To create a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="794fc-141">Het volgende voorbeeld laat zien hoe u een nieuw Automation-certificaat maken en deze exporteerbaar markeren.</span><span class="sxs-lookup"><span data-stu-id="794fc-141">The following example demonstrates how to create a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="794fc-142">Hiermee importeert een bestaande pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="794fc-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="794fc-143">Gebruik van een certificaat</span><span class="sxs-lookup"><span data-stu-id="794fc-143">Using a certificate</span></span>

<span data-ttu-id="794fc-144">Moet u de **Get-AutomationCertificate** activiteit om een certificaat te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="794fc-144">You must use the **Get-AutomationCertificate** activity to use a certificate.</span></span> <span data-ttu-id="794fc-145">U kunt geen gebruiken de [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet omdat deze informatie over het certificaat actief, maar niet het certificaat zelf retourneert.</span><span class="sxs-lookup"><span data-stu-id="794fc-145">You cannot use the [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about the certificate asset but not the certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="794fc-146">Voorbeeld van tekstueel runbook</span><span class="sxs-lookup"><span data-stu-id="794fc-146">Textual runbook sample</span></span>

<span data-ttu-id="794fc-147">De volgende voorbeeldcode laat zien hoe een certificaat toevoegen aan een cloudservice in een runbook.</span><span class="sxs-lookup"><span data-stu-id="794fc-147">The following sample code shows how to add a certificate to a cloud service in a runbook.</span></span> <span data-ttu-id="794fc-148">In dit voorbeeld wordt wordt het wachtwoord opgehaald uit een versleutelde automation-variabele.</span><span class="sxs-lookup"><span data-stu-id="794fc-148">In this sample, the password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="794fc-149">Grafisch runbook-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="794fc-149">Graphical runbook sample</span></span>

<span data-ttu-id="794fc-150">U toevoegen een **Get-AutomationCertificate** aan een grafisch runbook door met de rechtermuisknop op het certificaat in het deelvenster bibliotheek van de grafische editor en **toevoegen aan papier**.</span><span class="sxs-lookup"><span data-stu-id="794fc-150">You add a **Get-AutomationCertificate** to a graphical runbook by right-clicking on the certificate in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![Certificaat toevoegen aan het canvas](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="794fc-152">De volgende afbeelding toont een voorbeeld van het gebruik van een certificaat in een grafisch runbook.</span><span class="sxs-lookup"><span data-stu-id="794fc-152">The following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="794fc-153">Dit is het hetzelfde voorbeeld hierboven weergegeven voor het toevoegen van een certificaat aan een cloudservice van tekstueel runbook.</span><span class="sxs-lookup"><span data-stu-id="794fc-153">This is the same example shown above for adding a certificate to a cloud service from a textual runbook.</span></span>

![<span data-ttu-id="794fc-154">Voorbeeld grafisch ontwerpen</span><span class="sxs-lookup"><span data-stu-id="794fc-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="794fc-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="794fc-155">Next steps</span></span>

- <span data-ttu-id="794fc-156">Zie voor meer informatie over het werken met koppelingen naar de logische stroom van uw runbook is ontworpen om uit te voeren activiteiten te regelen, [koppelingen in het grafisch ontwerpen](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="794fc-156">To learn more about working with links to control the logical flow of activities your runbook is designed to perform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
