---
title: Problemen met Azure punt-naar-site-verbinding | Microsoft Docs
description: Informatie over het oplossen van problemen met de punt-naar-site-verbinding.
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: de37c8ffd47a2b8e201d18e3a20b5325d528ad59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="3ea2e-103">Voor probleemoplossing: Problemen met de Azure-punt-naar-site-verbinding</span><span class="sxs-lookup"><span data-stu-id="3ea2e-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="3ea2e-104">Dit artikel worden veelvoorkomende problemen met de punt-naar-site-verbinding die u kunt ervaren.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="3ea2e-105">Ook wordt beschreven mogelijke oorzaken en oplossingen voor deze problemen.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="3ea2e-106">VPN-Clientfout: kan certificaat niet vinden.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="3ea2e-107">Symptoom</span><span class="sxs-lookup"><span data-stu-id="3ea2e-107">Symptom</span></span>

<span data-ttu-id="3ea2e-108">Wanneer u probeert verbinding maken met een Azure-netwerk met behulp van de VPN-client, wordt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-108">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="3ea2e-109">**Een certificaat kan niet worden gevonden die kan worden gebruikt met dit Extensible Authentication Protocol. (Fout 798)**</span><span class="sxs-lookup"><span data-stu-id="3ea2e-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="3ea2e-110">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3ea2e-110">Cause</span></span>

<span data-ttu-id="3ea2e-111">Dit probleem treedt op als het clientcertificaat ontbreekt in **Certificaten - Huidige gebruiker\Persoonlijk\Certificaten**.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-111">This problem occurs if the client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="3ea2e-112">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-112">Solution</span></span>

<span data-ttu-id="3ea2e-113">Zorg ervoor dat het certificaat is geïnstalleerd in de volgende locatie van het archief met certificaten (Certmgr.msc):</span><span class="sxs-lookup"><span data-stu-id="3ea2e-113">Make sure that the client certificate is installed in the following location of the Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="3ea2e-114">**Certificaten - Huidige gebruiker\Persoonlijk\Certificaten**</span><span class="sxs-lookup"><span data-stu-id="3ea2e-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="3ea2e-115">Zie voor meer informatie over het installeren van het clientcertificaat [genereren en exporteren van certificaten voor punt-naar-site-verbindingen](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="3ea2e-115">For more information about how to install the client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3ea2e-116">Bij het importeren van het clientcertificaat niet selecteert de **zware beveiliging van persoonlijke sleutel inschakelen** optie.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-116">When you import the client certificate, do not select the **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-the-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="3ea2e-117">VPN-Clientfout: het ontvangen bericht is onverwacht of onjuist ingedeeld</span><span class="sxs-lookup"><span data-stu-id="3ea2e-117">VPN client error: The message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="3ea2e-118">Symptoom</span><span class="sxs-lookup"><span data-stu-id="3ea2e-118">Symptom</span></span>

<span data-ttu-id="3ea2e-119">Wanneer u probeert verbinding maken met een Azure-netwerk met behulp van de VPN-client, wordt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-119">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="3ea2e-120">**Het ontvangen bericht is onverwacht of onjuist ingedeeld. (Fout 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="3ea2e-120">**The message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="3ea2e-121">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3ea2e-121">Cause</span></span>

<span data-ttu-id="3ea2e-122">Dit probleem treedt op als de openbare sleutel van het root-certificaat is niet geüpload naar de Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-122">This problem occurs if the root certificate public key is not uploaded into the Azure VPN gateway.</span></span> <span data-ttu-id="3ea2e-123">Het kan ook optreden als de sleutel is beschadigd of verlopen.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-123">It can also occur if the key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="3ea2e-124">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-124">Solution</span></span>

<span data-ttu-id="3ea2e-125">U lost dit probleem, Controleer de status van het basiscertificaat in de Azure portal om te zien of deze is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-125">To resolve this problem, check the status of the root certificate in the Azure portal to see whether it was revoked.</span></span> <span data-ttu-id="3ea2e-126">Als deze niet is ingetrokken, kunt u proberen te verwijderen van het basiscertificaat en reupload.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-126">If it is not revoked, try to delete the root certificate and reupload.</span></span> <span data-ttu-id="3ea2e-127">Zie voor meer informatie [certificaten maken](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="3ea2e-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="3ea2e-128">VPN-Clientfout: een certificaatketen verwerkt, maar is beëindigd</span><span class="sxs-lookup"><span data-stu-id="3ea2e-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="3ea2e-129">Symptoom</span><span class="sxs-lookup"><span data-stu-id="3ea2e-129">Symptom</span></span> 

<span data-ttu-id="3ea2e-130">Wanneer u probeert verbinding maken met een Azure-netwerk met behulp van de VPN-client, wordt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-130">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="3ea2e-131">**Een certificaatketen verwerkt, maar in een basiscertificaat dat niet wordt vertrouwd door de provider is beëindigd.**</span><span class="sxs-lookup"><span data-stu-id="3ea2e-131">**A certificate chain processed but terminated in a root certificate which is not trusted by the trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="3ea2e-132">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-132">Solution</span></span>

1. <span data-ttu-id="3ea2e-133">Zorg ervoor dat de volgende certificaten in de juiste locatie:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-133">Make sure that the following certificates are in the correct location:</span></span>

    | <span data-ttu-id="3ea2e-134">Certificaat</span><span class="sxs-lookup"><span data-stu-id="3ea2e-134">Certificate</span></span> | <span data-ttu-id="3ea2e-135">Locatie</span><span class="sxs-lookup"><span data-stu-id="3ea2e-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="3ea2e-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="3ea2e-136">AzureClient.pfx</span></span>  | <span data-ttu-id="3ea2e-137">Huidige gebruiker\Persoonlijk\Certificaten</span><span class="sxs-lookup"><span data-stu-id="3ea2e-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="3ea2e-138">Azuregateway -*GUID*. cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="3ea2e-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="3ea2e-139">Huidige User\Trusted basiscertificeringsinstanties</span><span class="sxs-lookup"><span data-stu-id="3ea2e-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="3ea2e-140">AzureGateway -*GUID*. cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="3ea2e-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="3ea2e-141">Lokale Computer\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="3ea2e-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="3ea2e-142">Als de certificaten al op de locatie zijn, kunt u de certificaten verwijderen en installeert u deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-142">If the certificates are already in the location, try to delete the certificates and reinstall them.</span></span> <span data-ttu-id="3ea2e-143">De  **azuregateway -*GUID*. cloudapp.net** certificaat bevindt zich in het configuratiepakket voor VPN-client die u hebt gedownload van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-143">The **azuregateway-*GUID*.cloudapp.net** certificate is in the VPN client configuration package that you downloaded from the Azure portal.</span></span> <span data-ttu-id="3ea2e-144">Bestand archivers kunt u de bestanden extraheren uit het pakket.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-144">You can use file archivers to extract the files from the package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="3ea2e-145">Fout bij het downloaden bestand: doel-URI is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="3ea2e-146">Symptoom</span><span class="sxs-lookup"><span data-stu-id="3ea2e-146">Symptom</span></span>

<span data-ttu-id="3ea2e-147">U ontvangt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-147">You receive the following error message:</span></span>

<span data-ttu-id="3ea2e-148">**Fout bij het downloaden van het bestand. Doel-URI is niet opgegeven.**</span><span class="sxs-lookup"><span data-stu-id="3ea2e-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="3ea2e-149">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3ea2e-149">Cause</span></span> 

<span data-ttu-id="3ea2e-150">Dit probleem treedt vanwege een onjuiste Gatewaytype.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="3ea2e-151">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-151">Solution</span></span>

<span data-ttu-id="3ea2e-152">Het type VPN-gateway moet **VPN**, en het VPN-type moet **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-152">The VPN gateway type must be **VPN**, and the VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="3ea2e-153">VPN-Clientfout: aangepaste Azure VPN-script is mislukt</span><span class="sxs-lookup"><span data-stu-id="3ea2e-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="3ea2e-154">Symptoom</span><span class="sxs-lookup"><span data-stu-id="3ea2e-154">Symptom</span></span>

<span data-ttu-id="3ea2e-155">Wanneer u probeert verbinding maken met een Azure-netwerk met behulp van de VPN-client, wordt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-155">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="3ea2e-156">**Aangepast script (om bij te werken uw routeringstabel) is mislukt. (Fout 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="3ea2e-156">**Custom script (to update your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="3ea2e-157">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3ea2e-157">Cause</span></span>

<span data-ttu-id="3ea2e-158">Dit probleem kan optreden als u probeert te openen van de site-naar-punt VPN-verbinding via een snelkoppeling.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-158">This problem might occur if you are trying to open the site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="3ea2e-159">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-159">Solution</span></span> 

<span data-ttu-id="3ea2e-160">Hiermee opent u het VPN-pakket rechtstreeks in plaats van openen vanuit de snelkoppeling.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-160">Open the VPN package directly instead of opening it from the shortcut.</span></span>

## <a name="cannot-install-the-vpn-client"></a><span data-ttu-id="3ea2e-161">De VPN-client installeren niet</span><span class="sxs-lookup"><span data-stu-id="3ea2e-161">Cannot install the VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="3ea2e-162">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3ea2e-162">Cause</span></span> 

<span data-ttu-id="3ea2e-163">Een aanvullend certificaat is vereist voor het vertrouwen van de VPN-gateway voor het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-163">An additional certificate is required to trust the VPN gateway for your virtual network.</span></span> <span data-ttu-id="3ea2e-164">Het certificaat is opgenomen in het configuratiepakket voor VPN-client die wordt gegenereerd vanuit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-164">The certificate is included in the VPN client configuration package that is generated from the Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="3ea2e-165">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-165">Solution</span></span>

<span data-ttu-id="3ea2e-166">Pak het configuratiepakket voor VPN-client en het .cer-bestand niet vinden.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-166">Extract the VPN client configuration package, and find the .cer file.</span></span> <span data-ttu-id="3ea2e-167">Volg deze stappen voor het installeren van het certificaat:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-167">To install the certificate, follow these steps:</span></span>

1. <span data-ttu-id="3ea2e-168">Open mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="3ea2e-169">Voeg de **certificaten** -module.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-169">Add the **Certificates** snap-in.</span></span>
3. <span data-ttu-id="3ea2e-170">Selecteer de **Computer** account voor de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-170">Select the **Computer** account for the local computer.</span></span>
4. <span data-ttu-id="3ea2e-171">Met de rechtermuisknop op de **Trusted Root Certification Authorities** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-171">Right-click the **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="3ea2e-172">Klik op **All-taak** > **importeren**, en blader naar het cer-bestand dat u hebt opgehaald uit de configuratie van VPN-clientpakket.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-172">Click **All-Task** > **Import**, and browse to the .cer file you extracted from the VPN client configuration package.</span></span>
5. <span data-ttu-id="3ea2e-173">De computer opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-173">Restart the computer.</span></span> 
6. <span data-ttu-id="3ea2e-174">Probeer de VPN-client te installeren.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-174">Try to install the VPN client.</span></span>

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-data-is-invalid"></a><span data-ttu-id="3ea2e-175">Azure portal-fout: kan niet opslaan van de VPN-gateway en de gegevens zijn ongeldig</span><span class="sxs-lookup"><span data-stu-id="3ea2e-175">Azure portal error: Failed to save the VPN gateway, and the data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="3ea2e-176">Symptoom</span><span class="sxs-lookup"><span data-stu-id="3ea2e-176">Symptom</span></span>

<span data-ttu-id="3ea2e-177">Wanneer u probeert de wijzigingen wilt opslaan voor de VPN-gateway in de Azure portal, wordt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-177">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span>

<span data-ttu-id="3ea2e-178">**Virtuele netwerkgateway opslaan is mislukt &lt;* gatewaynaam*&gt;.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-178">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="3ea2e-179">Gegevens voor certificaat &lt; *-certificaat-ID* &gt; is invalid.* *</span><span class="sxs-lookup"><span data-stu-id="3ea2e-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="3ea2e-180">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3ea2e-180">Cause</span></span> 

<span data-ttu-id="3ea2e-181">Dit probleem kan optreden als hoofdmap openbare sleutel van het certificaat dat u hebt geüpload een ongeldig teken, zoals een spatie bevat.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-181">This problem might occur if the root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="3ea2e-182">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-182">Solution</span></span>

<span data-ttu-id="3ea2e-183">Zorg ervoor dat de gegevens in het certificaat bevat geen ongeldige tekens, zoals regeleinden (regelterugloop).</span><span class="sxs-lookup"><span data-stu-id="3ea2e-183">Make sure that the data in the certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="3ea2e-184">De volledige waarde moet een lange regel.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-184">The entire value should be one long line.</span></span> <span data-ttu-id="3ea2e-185">De volgende tekst is een voorbeeld van het certificaat:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-185">The following text is a sample of the certificate:</span></span>

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-resource-name-is-invalid"></a><span data-ttu-id="3ea2e-186">Azure portal-fout: kan niet opslaan van de VPN-gateway en de resourcenaam is ongeldig</span><span class="sxs-lookup"><span data-stu-id="3ea2e-186">Azure portal error: Failed to save the VPN gateway, and the resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="3ea2e-187">Symptoom</span><span class="sxs-lookup"><span data-stu-id="3ea2e-187">Symptom</span></span>

<span data-ttu-id="3ea2e-188">Wanneer u probeert de wijzigingen wilt opslaan voor de VPN-gateway in de Azure portal, wordt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-188">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span> 

<span data-ttu-id="3ea2e-189">**Virtuele netwerkgateway opslaan is mislukt &lt;* gatewaynaam*&gt;.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-189">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="3ea2e-190">Resourcenaam &lt; *certificaatnaam die u probeert te uploaden* &gt; is ongeldig **.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-190">Resource name &lt;*certificate name you try to upload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="3ea2e-191">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3ea2e-191">Cause</span></span>

<span data-ttu-id="3ea2e-192">Dit probleem treedt op omdat de naam van het certificaat een ongeldig teken, zoals een spatie bevat.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-192">This problem occurs because the name of the certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="3ea2e-193">Azure portal-fout: VPN-pakket bestand Downloadfout 503</span><span class="sxs-lookup"><span data-stu-id="3ea2e-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="3ea2e-194">Symptoom</span><span class="sxs-lookup"><span data-stu-id="3ea2e-194">Symptom</span></span>

<span data-ttu-id="3ea2e-195">Wanneer u de configuratie van VPN-clientpakket downloaden, wordt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-195">When you try to download the VPN client configuration package, you receive the following error message:</span></span>

<span data-ttu-id="3ea2e-196">**Download het bestand is mislukt. Details van fout: fout 503. De server is bezet.**</span><span class="sxs-lookup"><span data-stu-id="3ea2e-196">**Failed to download the file. Error details: error 503. The server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="3ea2e-197">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-197">Solution</span></span>

<span data-ttu-id="3ea2e-198">Deze fout kan worden veroorzaakt door een tijdelijk netwerkprobleem.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="3ea2e-199">Probeer de VPN-pakket te downloaden na een paar minuten opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-199">Try to download the VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-to-connect"></a><span data-ttu-id="3ea2e-200">Upgrade uitvoeren voor Azure VPN-Gateway: alle P2S-clients kunnen geen verbinding maken</span><span class="sxs-lookup"><span data-stu-id="3ea2e-200">Azure VPN Gateway upgrade: All P2S clients are unable to connect</span></span>

### <a name="cause"></a><span data-ttu-id="3ea2e-201">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3ea2e-201">Cause</span></span>

<span data-ttu-id="3ea2e-202">Als het certificaat meer dan 50 procent is via hun levensduur, het certificaat wordt overgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-202">If the certificate is more than 50 percent through its lifetime, the certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="3ea2e-203">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-203">Solution</span></span>

<span data-ttu-id="3ea2e-204">U lost dit probleem, maken en distribueren van nieuwe certificaten aan de VPN-clients.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-204">To resolve this problem, create and redistribute new certificates to the VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="3ea2e-205">Te veel VPN-clients tegelijk verbonden</span><span class="sxs-lookup"><span data-stu-id="3ea2e-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="3ea2e-206">Voor elke VPN-gateway is het maximum aantal toegestane verbindingen 128.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-206">For each VPN gateway, the maximum number of allowable connections is 128.</span></span> <span data-ttu-id="3ea2e-207">Hier ziet u het totale aantal verbonden clients in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-207">You can see the total number of connected clients in the Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-to-the-route-table"></a><span data-ttu-id="3ea2e-208">Punt-naar-site VPN wordt een route voor 10.0.0.0/8 onjuist toegevoegd aan de routetabel</span><span class="sxs-lookup"><span data-stu-id="3ea2e-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 to the route table</span></span>

### <a name="symptom"></a><span data-ttu-id="3ea2e-209">Symptoom</span><span class="sxs-lookup"><span data-stu-id="3ea2e-209">Symptom</span></span>

<span data-ttu-id="3ea2e-210">Wanneer u de VPN-verbinding op de client punt-naar-site kiest, moet de VPN-client een route naar de virtuele Azure-netwerk toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-210">When you dial the VPN connection on the point-to-site client, the VPN client should add a route toward the Azure virtual network.</span></span> <span data-ttu-id="3ea2e-211">De IP-helper-service moet een route voor het subnet van de VPN-clients toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-211">The IP helper service should add a route for the subnet of the VPN clients.</span></span> 

<span data-ttu-id="3ea2e-212">Het VPN-client bereik behoort tot een kleinere 10.0.0.0/8, zoals 10.0.12.0/24-subnet.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-212">The VPN client range belongs to a smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="3ea2e-213">In plaats van een route voor 10.0.12.0/24, wordt een route voor 10.0.0.0/8 toegevoegd die een hogere prioriteit heeft.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="3ea2e-214">Deze onjuiste route verbroken connectiviteit met andere on-premises-netwerken die deel kan uitmaken van een ander subnet binnen het bereik 10.0.0.0/8, zoals 10.50.0.0/24, waarvoor geen een specifieke route gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-214">This incorrect route breaks connectivity with other on-premises networks that might belong to another subnet within the 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="3ea2e-215">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3ea2e-215">Cause</span></span>

<span data-ttu-id="3ea2e-216">Dit gedrag is inherent aan het ontwerp voor Windows-clients.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="3ea2e-217">Wanneer de client het PPP IPCP-protocol gebruikt, ontvangt deze het IP-adres voor de tunnelinterface van de server (de VPN-gateway in dit geval).</span><span class="sxs-lookup"><span data-stu-id="3ea2e-217">When the client uses the PPP IPCP protocol, it obtains the IP address for the tunnel interface from the server (the VPN gateway in this case).</span></span> <span data-ttu-id="3ea2e-218">Echter, vanwege een beperking in het protocol, de client heeft geen het subnetmasker.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-218">However, because of a limitation in the protocol, the client does not have the subnet mask.</span></span> <span data-ttu-id="3ea2e-219">Omdat er geen andere manier om toegang te krijgen, wordt de client probeert te raden het subnetmasker op basis van de klasse van het IP-adres van de tunnel-interface.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-219">Because there is no other way to get it, the client tries to guess the subnet mask based on the class of the tunnel interface IP address.</span></span> 

<span data-ttu-id="3ea2e-220">Een route is daarom toegevoegd op basis van de volgende statische toewijzing:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-220">Therefore, a route is added based on the following static mapping:</span></span> 

<span data-ttu-id="3ea2e-221">Als het adres behoort tot klasse A-->/8 die van toepassing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-221">If address belongs to class A --> apply /8</span></span>

<span data-ttu-id="3ea2e-222">Als het adres behoort tot klasse B--> /16 toepassen</span><span class="sxs-lookup"><span data-stu-id="3ea2e-222">If address belongs to class B --> apply /16</span></span>

<span data-ttu-id="3ea2e-223">Als het adres behoort tot klasse C--> /24 toepassen</span><span class="sxs-lookup"><span data-stu-id="3ea2e-223">If address belongs to class C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="3ea2e-224">VPN-client heeft geen toegang tot netwerkbestandsshares</span><span class="sxs-lookup"><span data-stu-id="3ea2e-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="3ea2e-225">Symptoom</span><span class="sxs-lookup"><span data-stu-id="3ea2e-225">Symptom</span></span>

<span data-ttu-id="3ea2e-226">De VPN-client is verbonden met het Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-226">The VPN client has connected to the Azure virtual network.</span></span> <span data-ttu-id="3ea2e-227">Echter, de client geen toegang tot netwerkshares.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-227">However, the client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="3ea2e-228">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="3ea2e-228">Cause</span></span>

<span data-ttu-id="3ea2e-229">Het SMB-protocol wordt gebruikt voor bestandsshare-toegang.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-229">The SMB protocol is used for file share access.</span></span> <span data-ttu-id="3ea2e-230">Wanneer de verbinding wordt gestart, wordt de VPN-client de referenties van de sessie wordt toegevoegd en wordt de fout zich voordoet.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-230">When the connection is initiated, the VPN client adds the session credentials and the failure occurs.</span></span> <span data-ttu-id="3ea2e-231">Nadat de verbinding tot stand is gebracht, wordt de client gedwongen de cache-referenties gebruiken voor Kerberos-verificatie.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-231">After the connection is established, the client is forced to use the cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="3ea2e-232">Dit proces initieert query's naar de Key Distribution Center (domeincontroller) om op te halen van een token.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-232">This process initiates queries to the Key Distribution Center (a domain controller) to get a token.</span></span> <span data-ttu-id="3ea2e-233">Omdat de client verbinding vanaf het Internet maakt, het niet mogelijk om te bereiken van de domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-233">Because the client connects from the Internet, it might not be able to reach the domain controller.</span></span> <span data-ttu-id="3ea2e-234">Daarom kan geen de client failover van Kerberos naar NTLM.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-234">Therefore, the client cannot fail over from Kerberos to NTLM.</span></span> 

<span data-ttu-id="3ea2e-235">Het enige ogenblik waarop de client wordt gevraagd om een referentie wanneer is er een geldig certificaat (met SAN = UPN) uitgegeven door het domein waaraan deze is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-235">The only time that the client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by the domain to which it is joined.</span></span> <span data-ttu-id="3ea2e-236">De client moet ook fysiek verbonden zijn met het domeinnetwerk.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-236">The client also must be physically connected to the domain network.</span></span> <span data-ttu-id="3ea2e-237">In dit geval wordt de client probeert om het certificaat te gebruiken en gezocht naar de domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-237">In this case, the client tries to use the certificate and reaches out to the domain controller.</span></span> <span data-ttu-id="3ea2e-238">De Key Distribution Center wordt vervolgens een 'KDC_ERR_C_PRINCIPAL_UNKNOWN'-fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-238">Then the Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="3ea2e-239">Failover naar NTLM geforceerd op de client.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-239">The client is forced to fail over to NTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="3ea2e-240">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-240">Solution</span></span>

<span data-ttu-id="3ea2e-241">U kunt het probleem omzeilen, uitschakelen in cache opslaan van referenties van het domein van de volgende registersubsleutel:</span><span class="sxs-lookup"><span data-stu-id="3ea2e-241">To work around the problem, disable the caching of domain credentials from the following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set the value to 1 


## <a name="cannot-find-the-point-to-site-vpn-connection-in-windows-after-reinstalling-the-vpn-client"></a><span data-ttu-id="3ea2e-242">De punt-naar-site VPN-verbinding kan niet zoeken in Windows nadat de VPN-client opnieuw is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="3ea2e-242">Cannot find the point-to-site VPN connection in Windows after reinstalling the VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="3ea2e-243">Symptoom</span><span class="sxs-lookup"><span data-stu-id="3ea2e-243">Symptom</span></span>

<span data-ttu-id="3ea2e-244">U verwijdert de punt-naar-site VPN-verbinding en de VPN-client opnieuw installeren.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-244">You remove the point-to-site VPN connection and then reinstall the VPN client.</span></span> <span data-ttu-id="3ea2e-245">In dit geval kan is de VPN-verbinding niet correct geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-245">In this situation, the VPN connection is not configured successfully.</span></span> <span data-ttu-id="3ea2e-246">U ziet geen de VPN-verbinding in de **netwerkverbindingen** instellingen in Windows.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-246">You do not see the VPN connection in the **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="3ea2e-247">Oplossing</span><span class="sxs-lookup"><span data-stu-id="3ea2e-247">Solution</span></span>

<span data-ttu-id="3ea2e-248">Los het probleem op door de oude VPN-client configuratiebestanden verwijderen van **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, en voer het installatieprogramma van de VPN-client vervolgens opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3ea2e-248">To resolve the problem, delete the old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run the VPN client installer again.</span></span>
