---
title: 'Genereren en exporteren van certificaten voor punt-naar-Site: PowerShell: Azure | Microsoft Docs'
description: Dit artikel bevat stappen toocreate een zelfondertekend basiscertificaat, Hallo openbare sleutel niet exporteren en met PowerShell op Windows 10 clientcertificaten te genereren.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="9dbe9-103">Genereren en exporteren van certificaten voor punt-naar-Site-verbindingen op Windows 10 met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dbe9-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="9dbe9-104">Punt-naar-Site-verbindingen gebruiken certificaten tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="9dbe9-105">In dit artikel leest u hoe toocreate een zelfondertekend basiscertificaat en genereren met behulp van PowerShell op Windows 10 clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="9dbe9-106">Als u configuratiestappen voor punt-naar-Site, zoekt zoals hoe tooupload basiscertificaten, selecteert u een van de Hallo ' configureren punt-naar-Site' artikelen van Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="9dbe9-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9dbe9-107">Zelfondertekende certificaten - PowerShell maken</span><span class="sxs-lookup"><span data-stu-id="9dbe9-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="9dbe9-108">Zelfondertekende certificaten - MakeCert maken</span><span class="sxs-lookup"><span data-stu-id="9dbe9-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="9dbe9-109">Punt-naar-Site - Resource Manager - Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="9dbe9-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="9dbe9-110">Punt-naar-Site - Resource Manager - PowerShell configureren</span><span class="sxs-lookup"><span data-stu-id="9dbe9-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="9dbe9-111">Punt-naar-Site - Classic - Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="9dbe9-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="9dbe9-112">In dit artikel op een computer met Windows 10, moet u Hallo stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-112">You must perform hello steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="9dbe9-113">Hallo PowerShell-cmdlets is dat u toogenerate certificaten deel uitmaken van Hallo Windows 10-besturingssysteem en werken niet op andere versies van Windows.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-113">hello PowerShell cmdlets that you use toogenerate certificates are part of hello Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="9dbe9-114">Hallo Windows 10-computer is alleen nodig toogenerate Hallo certificaten.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-114">hello Windows 10 computer is only needed toogenerate hello certificates.</span></span> <span data-ttu-id="9dbe9-115">Zodra het Hallo-certificaten worden gegenereerd, kunt u deze uploaden of installeren op een ondersteunde client-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-115">Once hello certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="9dbe9-116">Als u geen toegang tot tooa Windows 10-computer, kunt u [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificaten.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-116">If you do not have access tooa Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificates.</span></span> <span data-ttu-id="9dbe9-117">Hallo-certificaten die u genereren met behulp van beide methoden kunnen worden geïnstalleerd op een [ondersteund](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) clientbesturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-117">hello certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="9dbe9-118"><a name="rootcert"></a>Een zelfondertekend basiscertificaat maken</span><span class="sxs-lookup"><span data-stu-id="9dbe9-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="9dbe9-119">Hallo nieuw SelfSignedCertificate cmdlet toocreate een zelfondertekend basiscertificaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-119">Use hello New-SelfSignedCertificate cmdlet toocreate a self-signed root certificate.</span></span> <span data-ttu-id="9dbe9-120">Zie voor informatie over de extra parameters, [nieuw SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="9dbe9-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="9dbe9-121">Open vanaf een computer met Windows 10, Windows PowerShell-console met verhoogde bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="9dbe9-122">Gebruik hello voorbeeld toocreate Hallo zelfondertekende basiscertificaat te volgen.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-122">Use hello following example toocreate hello self-signed root certificate.</span></span> <span data-ttu-id="9dbe9-123">Hallo wordt volgende voorbeeld een zelfondertekend basiscertificaat met de naam 'P2SRootCert', die automatisch wordt geïnstalleerd in 'Certificaten-Huidige gebruiker\Persoonlijk\Certificaten'.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-123">hello following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="9dbe9-124">U kunt Hallo certificaat weergeven door het openen van *certmgr.msc*, of *Gebruikerscertificaten beheren*.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-124">You can view hello certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="9dbe9-125"><a name="cer"></a>Hallo openbare sleutel (.cer) exporteren</span><span class="sxs-lookup"><span data-stu-id="9dbe9-125"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="9dbe9-126">Hallo exported.cer bestand moet geüploade tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-126">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="9dbe9-127">Zie voor instructies [een punt-naar-Site-verbinding configureren](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="9dbe9-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="9dbe9-128">een vertrouwd basiscertificaat aanvullende tooadd [in deze sectie](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) van Hallo artikel.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-128">tooadd an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of hello article.</span></span>

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a><span data-ttu-id="9dbe9-129">Het zelfondertekende basiscertificaat Hallo en openbare sleutel toostore exporteren deze (optioneel)</span><span class="sxs-lookup"><span data-stu-id="9dbe9-129">Export hello self-signed root certificate and public key toostore it (optional)</span></span>

<span data-ttu-id="9dbe9-130">U kunt tooexport Hallo zelfondertekend basiscertificaat en veilig opslaan.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-130">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="9dbe9-131">Indien nodig zijn, u kunt later op een andere computer installeren en meer clientcertificaten te genereren of een andere cer-bestand exporteren.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="9dbe9-132">tooexport hello zelfondertekend basiscertificaat als een .pfx, selecteer Hallo-basiscertificaat en gebruik dezelfde stappen Hallo zoals beschreven in [exporteren van een clientcertificaat](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="9dbe9-132">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="9dbe9-133"><a name="clientcert"></a>Een clientcertificaat genereren</span><span class="sxs-lookup"><span data-stu-id="9dbe9-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="9dbe9-134">Elke clientcomputer die verbinding tooa maakt VNet met punt-naar-Site moet beschikken over een clientcertificaat dat is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-134">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="9dbe9-135">U een clientcertificaat genereren uit het zelfondertekende basiscertificaat hello, en vervolgens exporteren en installeren van Hallo clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-135">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="9dbe9-136">Als het Hallo-clientcertificaat niet is geïnstalleerd, mislukt de verificatie.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-136">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="9dbe9-137">Hallo volgende stappen maakt u een clientcertificaat van een zelfondertekend basiscertificaat genereren.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-137">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="9dbe9-138">U kunt meerdere clientcertificaten genereren van Hallo hetzelfde basiscertificaat.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-138">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="9dbe9-139">Als u clientcertificaten gebruik Hallo stappen hieronder genereert, wordt Hallo clientcertificaat automatisch geïnstalleerd op Hallo-computer die u hebt toogenerate Hallo certificaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-139">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="9dbe9-140">Als u een certificaat op een andere clientcomputer tooinstall wilt, kunt u Hallo certificaat exporteren.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-140">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>

<span data-ttu-id="9dbe9-141">Hallo voorbeelden gebruikt Hallo nieuw SelfSignedCertificate cmdlet toogenerate een clientcertificaat dat na één jaar verloopt.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-141">hello examples use hello New-SelfSignedCertificate cmdlet toogenerate a client certificate that expires in one year.</span></span> <span data-ttu-id="9dbe9-142">Zie voor aanvullende parameterinformatie, zoals het instellen van een andere verlopen waarde voor het clientcertificaat Hallo [nieuw SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="9dbe9-142">For additional parameter information, such as setting a different expiration value for hello client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="9dbe9-143">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="9dbe9-143">Example 1</span></span>

<span data-ttu-id="9dbe9-144">In dit voorbeeld wordt de variabele '$cert' uit de vorige sectie Hallo gedeclareerd Hallo.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-144">This example uses hello declared '$cert' variable from hello previous section.</span></span> <span data-ttu-id="9dbe9-145">Als u de PowerShell-console Hallo gesloten nadat het maken van zelfondertekende basiscertificaat Hallo of zijn extra client certificaten in een nieuwe sessie van de PowerShell-console, gebruiken Hallo stappen in [voorbeeld 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="9dbe9-145">If you closed hello PowerShell console after creating hello self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use hello steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="9dbe9-146">Wijzigen en Voer Hallo voorbeeld toogenerate een clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-146">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="9dbe9-147">Als u Hallo voorbeeld te volgen zonder het te wijzigen uitvoert, is het Hallo resultaat een certificaat met de naam 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-147">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="9dbe9-148">Als u tooname Hallo onderliggende certificaat iets anders wilt, wijzigt u Hallo CN-waarde.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-148">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="9dbe9-149">Hallo TextExtension niet wijzigt wanneer u dit voorbeeld uitvoert.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-149">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="9dbe9-150">Hallo-clientcertificaat dat u genereren wordt automatisch geïnstalleerd in 'Certificaten - Huidige gebruiker\Persoonlijk\Certificaten' op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-150">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="9dbe9-151"><a name="ex2"></a>Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="9dbe9-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="9dbe9-152">Als u extra client certificaten maakt of worden niet met behulp van Hallo dezelfde PowerShell-sessie die u hebt gebruikt toocreate uw zelfondertekende basiscertificaat gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9dbe9-152">If you are creating additional client certificates, or are not using hello same PowerShell session that you used toocreate your self-signed root certificate, use hello following steps:</span></span>

1. <span data-ttu-id="9dbe9-153">Hallo zelfondertekende basiscertificaat dat is geïnstalleerd op de computer Hallo identificeren.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-153">Identify hello self-signed root certificate that is installed on hello computer.</span></span> <span data-ttu-id="9dbe9-154">Deze cmdlet retourneert een lijst met certificaten die zijn geïnstalleerd op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="9dbe9-155">Hallo-naam voor onderwerp van de geretourneerde lijst en klik vervolgens kopiëren Hallo vingerafdruk die is gevonden volgende tooit tooa tekst hello vinden bestand.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-155">Locate hello subject name from hello returned list, then copy hello thumbprint that is located next tooit tooa text file.</span></span> <span data-ttu-id="9dbe9-156">In de Hallo voorbeeld te volgen, zijn er twee certificaten.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-156">In hello following example, there are two certificates.</span></span> <span data-ttu-id="9dbe9-157">Hallo CN-naam is Hallo-naam van zelfondertekende basiscertificaat Hallo van waaruit u wilt dat een certificaat van de onderliggende toogenerate.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-157">hello CN name is hello name of hello self-signed root certificate from which you want toogenerate a child certificate.</span></span> <span data-ttu-id="9dbe9-158">In dit geval 'P2SRootCert'.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="9dbe9-159">Een variabele voor het basiscertificaat Hallo met vingerafdruk van de vorige stap Hallo Hallo declareren.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-159">Declare a variable for hello root certificate using hello thumbprint from hello previous step.</span></span> <span data-ttu-id="9dbe9-160">Vervang de VINGERAFDRUK Hallo vingerafdruk van waaruit u wilt dat een certificaat van de onderliggende toogenerate Hallo-basiscertificaat.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-160">Replace THUMBPRINT with hello thumbprint of hello root certificate from which you want toogenerate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="9dbe9-161">Met de vingerafdruk van het Hallo voor P2SRootCert in de vorige stap hello, Hallo variabele ziet er bijvoorbeeld als volgt:</span><span class="sxs-lookup"><span data-stu-id="9dbe9-161">For example, using hello thumbprint for P2SRootCert in hello previous step, hello variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="9dbe9-162">Wijzigen en Voer Hallo voorbeeld toogenerate een clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-162">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="9dbe9-163">Als u Hallo voorbeeld te volgen zonder het te wijzigen uitvoert, is het Hallo resultaat een certificaat met de naam 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-163">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="9dbe9-164">Als u tooname Hallo onderliggende certificaat iets anders wilt, wijzigt u Hallo CN-waarde.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-164">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="9dbe9-165">Hallo TextExtension niet wijzigt wanneer u dit voorbeeld uitvoert.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-165">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="9dbe9-166">Hallo-clientcertificaat dat u genereren wordt automatisch geïnstalleerd in 'Certificaten - Huidige gebruiker\Persoonlijk\Certificaten' op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-166">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="9dbe9-167"><a name="clientexport"></a>Een clientcertificaat exporteren</span><span class="sxs-lookup"><span data-stu-id="9dbe9-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="9dbe9-168"><a name="install"></a>Een geëxporteerde certificaat installeren</span><span class="sxs-lookup"><span data-stu-id="9dbe9-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="9dbe9-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9dbe9-169">Next steps</span></span>

<span data-ttu-id="9dbe9-170">Ga door met de punt-naar-Site-configuratie.</span><span class="sxs-lookup"><span data-stu-id="9dbe9-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="9dbe9-171">Voor **Resource Manager** model implementatiestappen Zie [configureren van een punt-naar-Site-verbinding tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9dbe9-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="9dbe9-172">Voor **klassieke** model implementatiestappen Zie [configureren van een punt-naar-Site VPN-verbinding tooa VNet (klassiek)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9dbe9-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
