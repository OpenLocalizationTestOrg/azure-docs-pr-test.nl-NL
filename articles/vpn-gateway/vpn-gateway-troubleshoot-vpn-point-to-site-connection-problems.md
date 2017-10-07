---
title: verbindingsproblemen aaaTroubleshoot Azure punt-naar-site | Microsoft Docs
description: Meer informatie over hoe problemen met de tootroubleshoot punt-naar-site-verbinding.
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
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="9bed3-103">Voor probleemoplossing: Problemen met de Azure-punt-naar-site-verbinding</span><span class="sxs-lookup"><span data-stu-id="9bed3-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="9bed3-104">Dit artikel worden veelvoorkomende problemen met de punt-naar-site-verbinding die u kunt ervaren.</span><span class="sxs-lookup"><span data-stu-id="9bed3-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="9bed3-105">Ook wordt beschreven mogelijke oorzaken en oplossingen voor deze problemen.</span><span class="sxs-lookup"><span data-stu-id="9bed3-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="9bed3-106">VPN-Clientfout: kan certificaat niet vinden.</span><span class="sxs-lookup"><span data-stu-id="9bed3-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="9bed3-107">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9bed3-107">Symptom</span></span>

<span data-ttu-id="9bed3-108">Wanneer u tooconnect tooan virtuele Azure-netwerk met behulp van Hallo VPN-client, wordt u Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9bed3-108">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="9bed3-109">**Een certificaat kan niet worden gevonden die kan worden gebruikt met dit Extensible Authentication Protocol. (Fout 798)**</span><span class="sxs-lookup"><span data-stu-id="9bed3-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="9bed3-110">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="9bed3-110">Cause</span></span>

<span data-ttu-id="9bed3-111">Dit probleem treedt op als het clientcertificaat Hallo ontbreekt in **Certificaten - Huidige gebruiker\Persoonlijk\Certificaten**.</span><span class="sxs-lookup"><span data-stu-id="9bed3-111">This problem occurs if hello client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="9bed3-112">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9bed3-112">Solution</span></span>

<span data-ttu-id="9bed3-113">Zorg ervoor dat certificaat Hallo-client is geïnstalleerd in Hallo locatie van het Hallo-archief met certificaten (Certmgr.msc) te volgen:</span><span class="sxs-lookup"><span data-stu-id="9bed3-113">Make sure that hello client certificate is installed in hello following location of hello Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="9bed3-114">**Certificaten - Huidige gebruiker\Persoonlijk\Certificaten**</span><span class="sxs-lookup"><span data-stu-id="9bed3-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="9bed3-115">Zie voor meer informatie over hoe tooinstall clientcertificaat Hallo [genereren en exporteren van certificaten voor punt-naar-site-verbindingen](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="9bed3-115">For more information about how tooinstall hello client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9bed3-116">Wanneer u het clientcertificaat Hallo importeert, selecteer niet Hallo **zware beveiliging van persoonlijke sleutel inschakelen** optie.</span><span class="sxs-lookup"><span data-stu-id="9bed3-116">When you import hello client certificate, do not select hello **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="9bed3-117">VPN-Clientfout: het Hallo-bericht ontvangen is onverwacht of onjuist ingedeeld</span><span class="sxs-lookup"><span data-stu-id="9bed3-117">VPN client error: hello message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="9bed3-118">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9bed3-118">Symptom</span></span>

<span data-ttu-id="9bed3-119">Wanneer u tooconnect tooan virtuele Azure-netwerk met behulp van Hallo VPN-client, wordt u Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9bed3-119">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="9bed3-120">**Hallo-bericht ontvangen is onverwacht of onjuist ingedeeld. (Fout 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="9bed3-120">**hello message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="9bed3-121">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="9bed3-121">Cause</span></span>

<span data-ttu-id="9bed3-122">Dit probleem treedt op als openbare sleutel Hallo hoofdmap is niet geüpload naar hello Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="9bed3-122">This problem occurs if hello root certificate public key is not uploaded into hello Azure VPN gateway.</span></span> <span data-ttu-id="9bed3-123">Het kan ook optreden als het Hallo-sleutel is beschadigd of verlopen.</span><span class="sxs-lookup"><span data-stu-id="9bed3-123">It can also occur if hello key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="9bed3-124">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9bed3-124">Solution</span></span>

<span data-ttu-id="9bed3-125">tooresolve dit probleem op door Hallo de status van Hallo root certificate in Azure portal toosee Hallo of deze is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="9bed3-125">tooresolve this problem, check hello status of hello root certificate in hello Azure portal toosee whether it was revoked.</span></span> <span data-ttu-id="9bed3-126">Als deze niet is ingetrokken, probeert toodelete Hallo-basiscertificaat en reupload.</span><span class="sxs-lookup"><span data-stu-id="9bed3-126">If it is not revoked, try toodelete hello root certificate and reupload.</span></span> <span data-ttu-id="9bed3-127">Zie voor meer informatie [certificaten maken](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="9bed3-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="9bed3-128">VPN-Clientfout: een certificaatketen verwerkt, maar is beëindigd</span><span class="sxs-lookup"><span data-stu-id="9bed3-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="9bed3-129">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9bed3-129">Symptom</span></span> 

<span data-ttu-id="9bed3-130">Wanneer u tooconnect tooan virtuele Azure-netwerk met behulp van Hallo VPN-client, wordt u Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9bed3-130">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="9bed3-131">**Een certificaatketen verwerkt, maar in een basiscertificaat dat wordt niet vertrouwd door Hallo vertrouwensrelatieprovider is beëindigd.**</span><span class="sxs-lookup"><span data-stu-id="9bed3-131">**A certificate chain processed but terminated in a root certificate which is not trusted by hello trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="9bed3-132">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9bed3-132">Solution</span></span>

1. <span data-ttu-id="9bed3-133">Zorg ervoor dat Hallo volgende certificaten in de juiste locatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="9bed3-133">Make sure that hello following certificates are in hello correct location:</span></span>

    | <span data-ttu-id="9bed3-134">Certificaat</span><span class="sxs-lookup"><span data-stu-id="9bed3-134">Certificate</span></span> | <span data-ttu-id="9bed3-135">Locatie</span><span class="sxs-lookup"><span data-stu-id="9bed3-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="9bed3-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="9bed3-136">AzureClient.pfx</span></span>  | <span data-ttu-id="9bed3-137">Huidige gebruiker\Persoonlijk\Certificaten</span><span class="sxs-lookup"><span data-stu-id="9bed3-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="9bed3-138">Azuregateway -*GUID*. cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="9bed3-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="9bed3-139">Huidige User\Trusted basiscertificeringsinstanties</span><span class="sxs-lookup"><span data-stu-id="9bed3-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="9bed3-140">AzureGateway -*GUID*. cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="9bed3-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="9bed3-141">Lokale Computer\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="9bed3-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="9bed3-142">Als Hallo certificaten al op Hallo locatie zijn, probeer toodelete Hallo certificaten en installeert u deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9bed3-142">If hello certificates are already in hello location, try toodelete hello certificates and reinstall them.</span></span> <span data-ttu-id="9bed3-143">Hallo  **azuregateway -*GUID*. cloudapp.net** certificaat bevindt zich in Hallo VPN-configuratie clientpakket die u hebt gedownload van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9bed3-143">hello **azuregateway-*GUID*.cloudapp.net** certificate is in hello VPN client configuration package that you downloaded from hello Azure portal.</span></span> <span data-ttu-id="9bed3-144">U kunt archivers tooextract Hallo-bestanden uit het Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="9bed3-144">You can use file archivers tooextract hello files from hello package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="9bed3-145">Fout bij het downloaden bestand: doel-URI is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9bed3-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="9bed3-146">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9bed3-146">Symptom</span></span>

<span data-ttu-id="9bed3-147">U ontvangt Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9bed3-147">You receive hello following error message:</span></span>

<span data-ttu-id="9bed3-148">**Fout bij het downloaden van het bestand. Doel-URI is niet opgegeven.**</span><span class="sxs-lookup"><span data-stu-id="9bed3-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="9bed3-149">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="9bed3-149">Cause</span></span> 

<span data-ttu-id="9bed3-150">Dit probleem treedt vanwege een onjuiste Gatewaytype.</span><span class="sxs-lookup"><span data-stu-id="9bed3-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="9bed3-151">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9bed3-151">Solution</span></span>

<span data-ttu-id="9bed3-152">Hallo VPN-gateway-type moet **VPN**, en Hallo VPN-type moet **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="9bed3-152">hello VPN gateway type must be **VPN**, and hello VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="9bed3-153">VPN-Clientfout: aangepaste Azure VPN-script is mislukt</span><span class="sxs-lookup"><span data-stu-id="9bed3-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="9bed3-154">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9bed3-154">Symptom</span></span>

<span data-ttu-id="9bed3-155">Wanneer u tooconnect tooan virtuele Azure-netwerk met behulp van Hallo VPN-client, wordt u Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9bed3-155">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="9bed3-156">**Aangepast script (tooupdate uw bewerkingsplan tabel) is mislukt. (Fout 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="9bed3-156">**Custom script (tooupdate your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="9bed3-157">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="9bed3-157">Cause</span></span>

<span data-ttu-id="9bed3-158">Dit probleem kan optreden als u tooopen Hallo site-naar-punt VPN-verbinding probeert met een snelkoppeling.</span><span class="sxs-lookup"><span data-stu-id="9bed3-158">This problem might occur if you are trying tooopen hello site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="9bed3-159">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9bed3-159">Solution</span></span> 

<span data-ttu-id="9bed3-160">Open Hallo VPN-pakket rechtstreeks in plaats van vanuit de snelkoppeling Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="9bed3-160">Open hello VPN package directly instead of opening it from hello shortcut.</span></span>

## <a name="cannot-install-hello-vpn-client"></a><span data-ttu-id="9bed3-161">Hallo VPN-client installeren niet</span><span class="sxs-lookup"><span data-stu-id="9bed3-161">Cannot install hello VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="9bed3-162">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="9bed3-162">Cause</span></span> 

<span data-ttu-id="9bed3-163">Een aanvullend certificaat is vereist tootrust Hallo VPN-gateway voor het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="9bed3-163">An additional certificate is required tootrust hello VPN gateway for your virtual network.</span></span> <span data-ttu-id="9bed3-164">Hallo-certificaat is opgenomen in Hallo VPN-configuratie clientpakket die is gegenereerd op basis van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9bed3-164">hello certificate is included in hello VPN client configuration package that is generated from hello Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="9bed3-165">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9bed3-165">Solution</span></span>

<span data-ttu-id="9bed3-166">Pak Hallo VPN-clientpakket configuratie en Hallo cer-bestand vinden.</span><span class="sxs-lookup"><span data-stu-id="9bed3-166">Extract hello VPN client configuration package, and find hello .cer file.</span></span> <span data-ttu-id="9bed3-167">Hallo tooinstall certificaat, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="9bed3-167">tooinstall hello certificate, follow these steps:</span></span>

1. <span data-ttu-id="9bed3-168">Open mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="9bed3-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="9bed3-169">Hallo toevoegen **certificaten** -module.</span><span class="sxs-lookup"><span data-stu-id="9bed3-169">Add hello **Certificates** snap-in.</span></span>
3. <span data-ttu-id="9bed3-170">Selecteer Hallo **Computer** voor de lokale computer Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="9bed3-170">Select hello **Computer** account for hello local computer.</span></span>
4. <span data-ttu-id="9bed3-171">Klik met de rechtermuisknop Hallo **Trusted Root Certification Authorities** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9bed3-171">Right-click hello **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="9bed3-172">Klik op **All-taak** > **importeren**, en bladeren toohello cer-bestand die u hebt opgehaald uit Hallo VPN-clientpakket configuratie.</span><span class="sxs-lookup"><span data-stu-id="9bed3-172">Click **All-Task** > **Import**, and browse toohello .cer file you extracted from hello VPN client configuration package.</span></span>
5. <span data-ttu-id="9bed3-173">Hallo-computer opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="9bed3-173">Restart hello computer.</span></span> 
6. <span data-ttu-id="9bed3-174">Probeer tooinstall Hallo VPN-client.</span><span class="sxs-lookup"><span data-stu-id="9bed3-174">Try tooinstall hello VPN client.</span></span>

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a><span data-ttu-id="9bed3-175">Azure portal-fout: kan niet toosave Hallo VPN-gateway en Hallo gegevens is ongeldig</span><span class="sxs-lookup"><span data-stu-id="9bed3-175">Azure portal error: Failed toosave hello VPN gateway, and hello data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="9bed3-176">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9bed3-176">Symptom</span></span>

<span data-ttu-id="9bed3-177">Wanneer u wijzigingen in de toosave Hallo voor Hallo VPN-gateway in hello Azure-portal, ontvangen Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9bed3-177">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span>

<span data-ttu-id="9bed3-178">**De virtuele netwerkgateway mislukte toosave &lt;* gatewaynaam*&gt;.</span><span class="sxs-lookup"><span data-stu-id="9bed3-178">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="9bed3-179">Gegevens voor certificaat &lt; *-certificaat-ID* &gt; is invalid.* *</span><span class="sxs-lookup"><span data-stu-id="9bed3-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="9bed3-180">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="9bed3-180">Cause</span></span> 

<span data-ttu-id="9bed3-181">Dit probleem kan optreden als Hallo hoofdmap openbare sleutel die u hebt geüpload een ongeldig teken, zoals een spatie bevat.</span><span class="sxs-lookup"><span data-stu-id="9bed3-181">This problem might occur if hello root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="9bed3-182">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9bed3-182">Solution</span></span>

<span data-ttu-id="9bed3-183">Zorg ervoor dat het Hallo-gegevens in Hallo certificaat bevat geen ongeldige tekens, zoals regeleinden (regelterugloop).</span><span class="sxs-lookup"><span data-stu-id="9bed3-183">Make sure that hello data in hello certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="9bed3-184">Hallo gehele waarde moet een lange regel zijn.</span><span class="sxs-lookup"><span data-stu-id="9bed3-184">hello entire value should be one long line.</span></span> <span data-ttu-id="9bed3-185">na de tekst Hello is een voorbeeld van Hallo certificaat:</span><span class="sxs-lookup"><span data-stu-id="9bed3-185">hello following text is a sample of hello certificate:</span></span>

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

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a><span data-ttu-id="9bed3-186">Azure portal-fout: kan niet toosave Hallo VPN-gateway en Hallo resourcenaam is ongeldig</span><span class="sxs-lookup"><span data-stu-id="9bed3-186">Azure portal error: Failed toosave hello VPN gateway, and hello resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="9bed3-187">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9bed3-187">Symptom</span></span>

<span data-ttu-id="9bed3-188">Wanneer u wijzigingen in de toosave Hallo voor Hallo VPN-gateway in hello Azure-portal, ontvangen Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9bed3-188">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span> 

<span data-ttu-id="9bed3-189">**De virtuele netwerkgateway mislukte toosave &lt;* gatewaynaam*&gt;.</span><span class="sxs-lookup"><span data-stu-id="9bed3-189">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="9bed3-190">Resourcenaam &lt; *certificaatnaam die u probeert tooupload* &gt; is ongeldig **.</span><span class="sxs-lookup"><span data-stu-id="9bed3-190">Resource name &lt;*certificate name you try tooupload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="9bed3-191">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="9bed3-191">Cause</span></span>

<span data-ttu-id="9bed3-192">Dit probleem treedt op omdat het Hallo-naam van Hallo certificaat bevat een ongeldig teken, zoals een spatie.</span><span class="sxs-lookup"><span data-stu-id="9bed3-192">This problem occurs because hello name of hello certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="9bed3-193">Azure portal-fout: VPN-pakket bestand Downloadfout 503</span><span class="sxs-lookup"><span data-stu-id="9bed3-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="9bed3-194">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9bed3-194">Symptom</span></span>

<span data-ttu-id="9bed3-195">Wanneer u toodownload Hallo VPN-clientpakket-configuratie, ontvangen Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9bed3-195">When you try toodownload hello VPN client configuration package, you receive hello following error message:</span></span>

<span data-ttu-id="9bed3-196">**Kan niet toodownload Hallo-bestand. Details van fout: fout 503. Hallo-server is bezet.**</span><span class="sxs-lookup"><span data-stu-id="9bed3-196">**Failed toodownload hello file. Error details: error 503. hello server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="9bed3-197">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9bed3-197">Solution</span></span>

<span data-ttu-id="9bed3-198">Deze fout kan worden veroorzaakt door een tijdelijk netwerkprobleem.</span><span class="sxs-lookup"><span data-stu-id="9bed3-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="9bed3-199">Probeer toodownload Hallo VPN-pakket na een paar minuten opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9bed3-199">Try toodownload hello VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a><span data-ttu-id="9bed3-200">Upgrade uitvoeren voor Azure VPN-Gateway: alle P2S-clients zijn tooconnect</span><span class="sxs-lookup"><span data-stu-id="9bed3-200">Azure VPN Gateway upgrade: All P2S clients are unable tooconnect</span></span>

### <a name="cause"></a><span data-ttu-id="9bed3-201">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="9bed3-201">Cause</span></span>

<span data-ttu-id="9bed3-202">Hallo-certificaat is meer dan 50 procent via hun levensduur Hallo certificaat wordt overgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9bed3-202">If hello certificate is more than 50 percent through its lifetime, hello certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="9bed3-203">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9bed3-203">Solution</span></span>

<span data-ttu-id="9bed3-204">tooresolve dit probleem maken en distribueren van nieuwe certificaten toohello VPN-clients.</span><span class="sxs-lookup"><span data-stu-id="9bed3-204">tooresolve this problem, create and redistribute new certificates toohello VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="9bed3-205">Te veel VPN-clients tegelijk verbonden</span><span class="sxs-lookup"><span data-stu-id="9bed3-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="9bed3-206">Voor elke VPN-gateway is Hallo kunt u het maximum aantal toegestane verbindingen 128.</span><span class="sxs-lookup"><span data-stu-id="9bed3-206">For each VPN gateway, hello maximum number of allowable connections is 128.</span></span> <span data-ttu-id="9bed3-207">Hier ziet u Hallo totaal aantal verbonden clients in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9bed3-207">You can see hello total number of connected clients in hello Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a><span data-ttu-id="9bed3-208">Punt-naar-site VPN wordt een route voor de routetabel voor 10.0.0.0/8 toohello onjuist toegevoegd</span><span class="sxs-lookup"><span data-stu-id="9bed3-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 toohello route table</span></span>

### <a name="symptom"></a><span data-ttu-id="9bed3-209">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9bed3-209">Symptom</span></span>

<span data-ttu-id="9bed3-210">Wanneer u Hallo VPN-verbinding op Hallo punt-naar-site-client kiest, moet Hallo VPN-client een route naar Hallo virtuele Azure-netwerk toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9bed3-210">When you dial hello VPN connection on hello point-to-site client, hello VPN client should add a route toward hello Azure virtual network.</span></span> <span data-ttu-id="9bed3-211">Hallo IP-helper-service moet een route voor subnet Hallo Hallo VPN-clients toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9bed3-211">hello IP helper service should add a route for hello subnet of hello VPN clients.</span></span> 

<span data-ttu-id="9bed3-212">Hallo VPN-client bereik hoort tooa kleinere subnet 10.0.0.0/8, zoals 10.0.12.0/24.</span><span class="sxs-lookup"><span data-stu-id="9bed3-212">hello VPN client range belongs tooa smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="9bed3-213">In plaats van een route voor 10.0.12.0/24, wordt een route voor 10.0.0.0/8 toegevoegd die een hogere prioriteit heeft.</span><span class="sxs-lookup"><span data-stu-id="9bed3-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="9bed3-214">Deze onjuiste route verbroken connectiviteit met andere on-premises-netwerken die mogelijk behoren tooanother subnet binnen Hallo 10.0.0.0/8 bereik, zoals 10.50.0.0/24, waarvoor geen een specifieke route gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="9bed3-214">This incorrect route breaks connectivity with other on-premises networks that might belong tooanother subnet within hello 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="9bed3-215">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="9bed3-215">Cause</span></span>

<span data-ttu-id="9bed3-216">Dit gedrag is inherent aan het ontwerp voor Windows-clients.</span><span class="sxs-lookup"><span data-stu-id="9bed3-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="9bed3-217">Wanneer de client Hallo Hallo IPCP PPP-protocol gebruikt, verkrijgt het Hallo IP-adres voor het Hallo-tunnelinterface van Hallo server (Hallo VPN-gateway in dit geval).</span><span class="sxs-lookup"><span data-stu-id="9bed3-217">When hello client uses hello PPP IPCP protocol, it obtains hello IP address for hello tunnel interface from hello server (hello VPN gateway in this case).</span></span> <span data-ttu-id="9bed3-218">Echter, vanwege een beperking in Hallo-protocol, Hallo client heeft geen Hallo subnetmasker.</span><span class="sxs-lookup"><span data-stu-id="9bed3-218">However, because of a limitation in hello protocol, hello client does not have hello subnet mask.</span></span> <span data-ttu-id="9bed3-219">Omdat er geen andere manier tooget probeert het Hallo-client tooguess Hallo-subnetmasker op basis van de klasse Hallo van Hallo tunnel-interface IP-adres.</span><span class="sxs-lookup"><span data-stu-id="9bed3-219">Because there is no other way tooget it, hello client tries tooguess hello subnet mask based on hello class of hello tunnel interface IP address.</span></span> 

<span data-ttu-id="9bed3-220">Een route is daarom toegevoegd op basis van Hallo statische toewijzing te volgen:</span><span class="sxs-lookup"><span data-stu-id="9bed3-220">Therefore, a route is added based on hello following static mapping:</span></span> 

<span data-ttu-id="9bed3-221">Als het adres behoort tooclass A-->/8 die van toepassing</span><span class="sxs-lookup"><span data-stu-id="9bed3-221">If address belongs tooclass A --> apply /8</span></span>

<span data-ttu-id="9bed3-222">Als het adres behoort toepassen tooclass B--> /16</span><span class="sxs-lookup"><span data-stu-id="9bed3-222">If address belongs tooclass B --> apply /16</span></span>

<span data-ttu-id="9bed3-223">Als het adres behoort toepassen tooclass C--> /24</span><span class="sxs-lookup"><span data-stu-id="9bed3-223">If address belongs tooclass C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="9bed3-224">VPN-client heeft geen toegang tot netwerkbestandsshares</span><span class="sxs-lookup"><span data-stu-id="9bed3-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="9bed3-225">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9bed3-225">Symptom</span></span>

<span data-ttu-id="9bed3-226">Hallo VPN-client is verbonden toohello virtuele Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="9bed3-226">hello VPN client has connected toohello Azure virtual network.</span></span> <span data-ttu-id="9bed3-227">Hallo-client kan echter netwerkshares niet openen.</span><span class="sxs-lookup"><span data-stu-id="9bed3-227">However, hello client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="9bed3-228">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="9bed3-228">Cause</span></span>

<span data-ttu-id="9bed3-229">Hallo SMB-protocol wordt gebruikt voor bestandsshare-toegang.</span><span class="sxs-lookup"><span data-stu-id="9bed3-229">hello SMB protocol is used for file share access.</span></span> <span data-ttu-id="9bed3-230">Wanneer het Hallo-verbinding is geïnitieerd en Hallo VPN-client wordt Hallo sessie referenties en Hallo-fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="9bed3-230">When hello connection is initiated, hello VPN client adds hello session credentials and hello failure occurs.</span></span> <span data-ttu-id="9bed3-231">Nadat het Hallo-verbinding tot stand is gebracht, geforceerd Hallo client toouse Hallo cache referenties voor Kerberos-verificatie.</span><span class="sxs-lookup"><span data-stu-id="9bed3-231">After hello connection is established, hello client is forced toouse hello cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="9bed3-232">Dit proces initieert query's toohello Key Distribution Center (domeincontroller) tooget een token.</span><span class="sxs-lookup"><span data-stu-id="9bed3-232">This process initiates queries toohello Key Distribution Center (a domain controller) tooget a token.</span></span> <span data-ttu-id="9bed3-233">Omdat Hallo client verbinding vanaf Internet hello maakt, mogelijk kunnen tooreach Hallo domeincontroller niet meer.</span><span class="sxs-lookup"><span data-stu-id="9bed3-233">Because hello client connects from hello Internet, it might not be able tooreach hello domain controller.</span></span> <span data-ttu-id="9bed3-234">Daarom kan Hallo-client niet worden overgenomen van Kerberos tooNTLM.</span><span class="sxs-lookup"><span data-stu-id="9bed3-234">Therefore, hello client cannot fail over from Kerberos tooNTLM.</span></span> 

<span data-ttu-id="9bed3-235">Hallo alleen tijd die Hallo-client is gevraagd om een referentie is wanneer er een geldig certificaat (met SAN = UPN) uitgegeven door Hallo domein toowhich deze is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="9bed3-235">hello only time that hello client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by hello domain toowhich it is joined.</span></span> <span data-ttu-id="9bed3-236">Hallo-client ook moet fysiek gekoppeld toohello domeinnetwerk.</span><span class="sxs-lookup"><span data-stu-id="9bed3-236">hello client also must be physically connected toohello domain network.</span></span> <span data-ttu-id="9bed3-237">In dit geval Hallo client probeert toouse Hallo certificaat en gezocht toohello-domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="9bed3-237">In this case, hello client tries toouse hello certificate and reaches out toohello domain controller.</span></span> <span data-ttu-id="9bed3-238">Hallo Key Distribution Center wordt vervolgens een 'KDC_ERR_C_PRINCIPAL_UNKNOWN'-fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9bed3-238">Then hello Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="9bed3-239">Hallo-client is gedwongen toofail via tooNTLM.</span><span class="sxs-lookup"><span data-stu-id="9bed3-239">hello client is forced toofail over tooNTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="9bed3-240">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9bed3-240">Solution</span></span>

<span data-ttu-id="9bed3-241">toowork rond Hallo-probleem uitschakelen Hallo opslaan in cache van de domeinreferenties van Hallo volgende registersubsleutel:</span><span class="sxs-lookup"><span data-stu-id="9bed3-241">toowork around hello problem, disable hello caching of domain credentials from hello following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a><span data-ttu-id="9bed3-242">Hallo punt-naar-site VPN-verbinding kan niet zoeken in Windows nadat Hallo VPN-client opnieuw is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="9bed3-242">Cannot find hello point-to-site VPN connection in Windows after reinstalling hello VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="9bed3-243">Symptoom</span><span class="sxs-lookup"><span data-stu-id="9bed3-243">Symptom</span></span>

<span data-ttu-id="9bed3-244">U Hallo punt-naar-site VPN-verbinding verwijderen en opnieuw installeren Hallo VPN-client.</span><span class="sxs-lookup"><span data-stu-id="9bed3-244">You remove hello point-to-site VPN connection and then reinstall hello VPN client.</span></span> <span data-ttu-id="9bed3-245">In dit geval is Hallo VPN-verbinding niet correct geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9bed3-245">In this situation, hello VPN connection is not configured successfully.</span></span> <span data-ttu-id="9bed3-246">U ziet geen Hallo VPN-verbinding in Hallo **netwerkverbindingen** instellingen in Windows.</span><span class="sxs-lookup"><span data-stu-id="9bed3-246">You do not see hello VPN connection in hello **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="9bed3-247">Oplossing</span><span class="sxs-lookup"><span data-stu-id="9bed3-247">Solution</span></span>

<span data-ttu-id="9bed3-248">tooresolve hello probleem verwijderen Hallo oude VPN-client configuratiebestanden uit **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, en voer het installatieprogramma Hallo VPN-client vervolgens opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9bed3-248">tooresolve hello problem, delete hello old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run hello VPN client installer again.</span></span>
