---
title: 'Genereren en exporteren van certificaten voor punt-naar-Site: PowerShell: Azure | Microsoft Docs'
description: In dit artikel bevat stappen om een zelfondertekend basiscertificaat maken, de openbare sleutel niet exporteren en clientcertificaten op Windows 10 met behulp van PowerShell te genereren.
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
ms.openlocfilehash: f96b9b212b9322d0677e49ff95184d0feccca2df
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="af222-103">Genereren en exporteren van certificaten voor punt-naar-Site-verbindingen op Windows 10 met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="af222-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="af222-104">Punt-naar-Site-verbindingen kunt u certificaten voor verificatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="af222-104">Point-to-Site connections use certificates to authenticate.</span></span> <span data-ttu-id="af222-105">In dit artikel laat zien hoe een zelfondertekend basiscertificaat maken en clientcertificaten op Windows 10 met behulp van PowerShell te genereren.</span><span class="sxs-lookup"><span data-stu-id="af222-105">This article shows you how to create a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="af222-106">Als u zoekt de configuratiestappen punt-naar-Site, zoals het uploaden van basiscertificaten, selecteert u een van de artikelen ' configureren punt-naar-Site' in de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="af222-106">If you are looking for Point-to-Site configuration steps, such as how to upload root certificates, select one of the 'Configure Point-to-Site' articles from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="af222-107">Zelfondertekende certificaten - PowerShell maken</span><span class="sxs-lookup"><span data-stu-id="af222-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="af222-108">Zelfondertekende certificaten - MakeCert maken</span><span class="sxs-lookup"><span data-stu-id="af222-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="af222-109">Punt-naar-Site - Resource Manager - Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="af222-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="af222-110">Punt-naar-Site - Resource Manager - PowerShell configureren</span><span class="sxs-lookup"><span data-stu-id="af222-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="af222-111">Punt-naar-Site - Classic - Azure-portal configureren</span><span class="sxs-lookup"><span data-stu-id="af222-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="af222-112">In dit artikel op een computer met Windows 10, moet u de stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="af222-112">You must perform the steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="af222-113">De PowerShell-cmdlets die u gebruikt voor het genereren van certificaten deel uitmaken van het besturingssysteem Windows 10 en werken niet op andere versies van Windows.</span><span class="sxs-lookup"><span data-stu-id="af222-113">The PowerShell cmdlets that you use to generate certificates are part of the Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="af222-114">De Windows 10-computer is alleen nodig voor het genereren van de certificaten.</span><span class="sxs-lookup"><span data-stu-id="af222-114">The Windows 10 computer is only needed to generate the certificates.</span></span> <span data-ttu-id="af222-115">Zodra de certificaten zijn gegenereerd, kunt u deze uploaden of installeren op een ondersteunde client-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="af222-115">Once the certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="af222-116">Als u geen toegang tot een Windows 10-computer, kunt u [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) voor het genereren van certificaten.</span><span class="sxs-lookup"><span data-stu-id="af222-116">If you do not have access to a Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) to generate certificates.</span></span> <span data-ttu-id="af222-117">De certificaten die u genereren met behulp van beide methoden kunnen worden geïnstalleerd op een [ondersteund](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) clientbesturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="af222-117">The certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="af222-118"><a name="rootcert"></a>Een zelfondertekend basiscertificaat maken</span><span class="sxs-lookup"><span data-stu-id="af222-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="af222-119">Gebruik de cmdlet New-SelfSignedCertificate voor het maken van een zelfondertekend basiscertificaat.</span><span class="sxs-lookup"><span data-stu-id="af222-119">Use the New-SelfSignedCertificate cmdlet to create a self-signed root certificate.</span></span> <span data-ttu-id="af222-120">Zie voor informatie over de extra parameters, [nieuw SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="af222-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="af222-121">Open vanaf een computer met Windows 10, Windows PowerShell-console met verhoogde bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="af222-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="af222-122">Gebruik het volgende voorbeeld voor het maken van het zelfondertekende basiscertificaat.</span><span class="sxs-lookup"><span data-stu-id="af222-122">Use the following example to create the self-signed root certificate.</span></span> <span data-ttu-id="af222-123">Het volgende voorbeeld maakt een zelfondertekend basiscertificaat met de naam 'P2SRootCert', die automatisch wordt geïnstalleerd in 'Certificaten-Huidige gebruiker\Persoonlijk\Certificaten'.</span><span class="sxs-lookup"><span data-stu-id="af222-123">The following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="af222-124">U kunt het certificaat weergeven door het openen van *certmgr.msc*, of *Gebruikerscertificaten beheren*.</span><span class="sxs-lookup"><span data-stu-id="af222-124">You can view the certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="af222-125"><a name="cer"></a>Exporteer de openbare sleutel (.cer)</span><span class="sxs-lookup"><span data-stu-id="af222-125"><a name="cer"></a>Export the public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="af222-126">Het bestand exported.cer moet worden geüpload naar Azure.</span><span class="sxs-lookup"><span data-stu-id="af222-126">The exported.cer file must be uploaded to Azure.</span></span> <span data-ttu-id="af222-127">Zie voor instructies [een punt-naar-Site-verbinding configureren](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="af222-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="af222-128">Toevoegen van een vertrouwd basiscertificaat aanvullende [in deze sectie](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) van het artikel.</span><span class="sxs-lookup"><span data-stu-id="af222-128">To add an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of the article.</span></span>

### <a name="export-the-self-signed-root-certificate-and-public-key-to-store-it-optional"></a><span data-ttu-id="af222-129">Exporteer het zelfondertekende basiscertificaat en openbare sleutel voor het opslaan van het (optioneel)</span><span class="sxs-lookup"><span data-stu-id="af222-129">Export the self-signed root certificate and public key to store it (optional)</span></span>

<span data-ttu-id="af222-130">U kunt het zelfondertekende basiscertificaat exporteren en veilig opslaan.</span><span class="sxs-lookup"><span data-stu-id="af222-130">You may want to export the self-signed root certificate and store it safely.</span></span> <span data-ttu-id="af222-131">Indien nodig zijn, u kunt later op een andere computer installeren en meer clientcertificaten te genereren of een andere cer-bestand exporteren.</span><span class="sxs-lookup"><span data-stu-id="af222-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="af222-132">Als u wilt het zelfondertekende basiscertificaat exporteren als een .pfx-bestand, selecteer het basiscertificaat en gebruik dezelfde stappen zoals beschreven in [exporteren van een clientcertificaat](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="af222-132">To export the self-signed root certificate as a .pfx, select the root certificate and use the same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="af222-133"><a name="clientcert"></a>Een clientcertificaat genereren</span><span class="sxs-lookup"><span data-stu-id="af222-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="af222-134">Op elke clientcomputer die via punt-naar-site verbinding maakt met een VNet, moet een clientcertificaat zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="af222-134">Each client computer that connects to a VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="af222-135">U een clientcertificaat genereren uit het zelfondertekende basiscertificaat en vervolgens exporteren en installeren van het clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="af222-135">You generate a client certificate from the self-signed root certificate, and then export and install the client certificate.</span></span> <span data-ttu-id="af222-136">Als het clientcertificaat niet is geïnstalleerd, mislukt de verificatie.</span><span class="sxs-lookup"><span data-stu-id="af222-136">If the client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="af222-137">De volgende stappen maakt u een clientcertificaat van een zelfondertekend basiscertificaat genereren.</span><span class="sxs-lookup"><span data-stu-id="af222-137">The following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="af222-138">U kunt meerdere clientcertificaten uit hetzelfde basiscertificaat genereren.</span><span class="sxs-lookup"><span data-stu-id="af222-138">You may generate multiple client certificates from the same root certificate.</span></span> <span data-ttu-id="af222-139">Als u clientcertificaten met de onderstaande stappen genereert, wordt het certificaat wordt automatisch geïnstalleerd op de computer die u gebruikt voor het genereren van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="af222-139">When you generate client certificates using the steps below, the client certificate is automatically installed on the computer that you used to generate the certificate.</span></span> <span data-ttu-id="af222-140">Als u een clientcertificaat installeren op een andere clientcomputer wilt, kunt u het certificaat exporteren.</span><span class="sxs-lookup"><span data-stu-id="af222-140">If you want to install a client certificate on another client computer, you can export the certificate.</span></span>

<span data-ttu-id="af222-141">De voorbeelden gebruikt de cmdlet New-SelfSignedCertificate voor het genereren van een clientcertificaat dat na één jaar verloopt.</span><span class="sxs-lookup"><span data-stu-id="af222-141">The examples use the New-SelfSignedCertificate cmdlet to generate a client certificate that expires in one year.</span></span> <span data-ttu-id="af222-142">Zie voor aanvullende parameterinformatie, zoals het instellen van een andere vervaldatum waarde voor het clientcertificaat [nieuw SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="af222-142">For additional parameter information, such as setting a different expiration value for the client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="af222-143">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="af222-143">Example 1</span></span>

<span data-ttu-id="af222-144">In dit voorbeeld wordt de gedeclareerde '$cert' variabele uit de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="af222-144">This example uses the declared '$cert' variable from the previous section.</span></span> <span data-ttu-id="af222-145">Als u de PowerShell-console gesloten na het maken van het zelfondertekende basiscertificaat of extra client certificaten in een nieuwe PowerShell-console-sessie maakt, gebruikt u de stappen in [voorbeeld 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="af222-145">If you closed the PowerShell console after creating the self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use the steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="af222-146">Wijzigen en voer in het voorbeeld voor het genereren van een clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="af222-146">Modify and run the example to generate a client certificate.</span></span> <span data-ttu-id="af222-147">Als u het volgende voorbeeld uitvoert zonder het te wijzigen, is het resultaat een certificaat met de naam 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="af222-147">If you run the following example without modifying it, the result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="af222-148">Als u wilt de naam van het certificaat van de onderliggende iets anders, wijzigt u de CN-waarde.</span><span class="sxs-lookup"><span data-stu-id="af222-148">If you want to name the child certificate something else, modify the CN value.</span></span> <span data-ttu-id="af222-149">Wijzig de TextExtension niet bij het uitvoeren van dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="af222-149">Do not change the TextExtension when running this example.</span></span> <span data-ttu-id="af222-150">Het clientcertificaat dat u genereren wordt automatisch geïnstalleerd in 'Certificaten - Huidige gebruiker\Persoonlijk\Certificaten' op uw computer.</span><span class="sxs-lookup"><span data-stu-id="af222-150">The client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="af222-151"><a name="ex2"></a>Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="af222-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="af222-152">Als u extra clientcertificaten maakt of dezelfde PowerShell-sessie die u gebruikt voor het maken van uw zelfondertekende basiscertificaat niet gebruikt, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="af222-152">If you are creating additional client certificates, or are not using the same PowerShell session that you used to create your self-signed root certificate, use the following steps:</span></span>

1. <span data-ttu-id="af222-153">Identificeer het zelfondertekende basiscertificaat dat is geïnstalleerd op de computer.</span><span class="sxs-lookup"><span data-stu-id="af222-153">Identify the self-signed root certificate that is installed on the computer.</span></span> <span data-ttu-id="af222-154">Deze cmdlet retourneert een lijst met certificaten die zijn geïnstalleerd op uw computer.</span><span class="sxs-lookup"><span data-stu-id="af222-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="af222-155">Zoek de onderwerpnaam in de geretourneerde lijst en kopieer de vingerafdruk die ernaast bevindt zich in een tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="af222-155">Locate the subject name from the returned list, then copy the thumbprint that is located next to it to a text file.</span></span> <span data-ttu-id="af222-156">Er zijn twee certificaten in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="af222-156">In the following example, there are two certificates.</span></span> <span data-ttu-id="af222-157">De CN-naam is de naam van het zelfondertekende basiscertificaat van waaruit u wilt voor het genereren van een onderliggende-certificaat.</span><span class="sxs-lookup"><span data-stu-id="af222-157">The CN name is the name of the self-signed root certificate from which you want to generate a child certificate.</span></span> <span data-ttu-id="af222-158">In dit geval 'P2SRootCert'.</span><span class="sxs-lookup"><span data-stu-id="af222-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="af222-159">Een variabele voor het basiscertificaat met de vingerafdruk van de vorige stap declareren.</span><span class="sxs-lookup"><span data-stu-id="af222-159">Declare a variable for the root certificate using the thumbprint from the previous step.</span></span> <span data-ttu-id="af222-160">Vervang de VINGERAFDRUK met de vingerafdruk van het basiscertificaat van waaruit u wilt voor het genereren van een onderliggende-certificaat.</span><span class="sxs-lookup"><span data-stu-id="af222-160">Replace THUMBPRINT with the thumbprint of the root certificate from which you want to generate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="af222-161">Met de vingerafdruk voor P2SRootCert in de vorige stap, de variabele, ziet er bijvoorbeeld als volgt:</span><span class="sxs-lookup"><span data-stu-id="af222-161">For example, using the thumbprint for P2SRootCert in the previous step, the variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="af222-162">Wijzigen en voer in het voorbeeld voor het genereren van een clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="af222-162">Modify and run the example to generate a client certificate.</span></span> <span data-ttu-id="af222-163">Als u het volgende voorbeeld uitvoert zonder het te wijzigen, is het resultaat een certificaat met de naam 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="af222-163">If you run the following example without modifying it, the result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="af222-164">Als u wilt de naam van het certificaat van de onderliggende iets anders, wijzigt u de CN-waarde.</span><span class="sxs-lookup"><span data-stu-id="af222-164">If you want to name the child certificate something else, modify the CN value.</span></span> <span data-ttu-id="af222-165">Wijzig de TextExtension niet bij het uitvoeren van dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="af222-165">Do not change the TextExtension when running this example.</span></span> <span data-ttu-id="af222-166">Het clientcertificaat dat u genereren wordt automatisch geïnstalleerd in 'Certificaten - Huidige gebruiker\Persoonlijk\Certificaten' op uw computer.</span><span class="sxs-lookup"><span data-stu-id="af222-166">The client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="af222-167"><a name="clientexport"></a>Een clientcertificaat exporteren</span><span class="sxs-lookup"><span data-stu-id="af222-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="af222-168"><a name="install"></a>Een geëxporteerde certificaat installeren</span><span class="sxs-lookup"><span data-stu-id="af222-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="af222-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="af222-169">Next steps</span></span>

<span data-ttu-id="af222-170">Ga door met de punt-naar-Site-configuratie.</span><span class="sxs-lookup"><span data-stu-id="af222-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="af222-171">Voor **Resource Manager** model implementatiestappen Zie [een punt-naar-Site-verbinding met een VNet configureren](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="af222-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection to a VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="af222-172">Voor **klassieke** model implementatiestappen Zie [punt-naar-Site VPN-verbinding geconfigureerd met een VNet (klassiek)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="af222-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection to a VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>