---
title: Beveiligen van inhoud met Microsoft PlayReady- of Apple FairPlay - Azure HLS | Microsoft Docs
description: Dit onderwerp een overzicht en laat zien hoe u Azure Media Services voor het dynamisch versleutelen van de inhoud van uw HTTP Live Streaming (HLS) met Apple FairPlay. U ziet ook hoe u met het Media Services-service voor het leveren van licenties FairPlay-licenties aan clients leveren.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 895d6307b1cef74e195cc2ffd8dbef4196e97b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="70962-104">Beveiligen van uw inhoud met Apple FairPlay of Microsoft PlayReady HLS</span><span class="sxs-lookup"><span data-stu-id="70962-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="70962-105">Azure Media Services kunt u uw inhoud HTTP Live Streaming (HLS) dynamisch versleutelen met behulp van de volgende indelingen:</span><span class="sxs-lookup"><span data-stu-id="70962-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span></span>  

* <span data-ttu-id="70962-106">**De lege sleutel envelop voor AES-128**</span><span class="sxs-lookup"><span data-stu-id="70962-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="70962-107">De volledige chunk is versleuteld met behulp van de **AES-128 CBC** modus.</span><span class="sxs-lookup"><span data-stu-id="70962-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="70962-108">De ontsleuteling van de stroom wordt ondersteund door iOS en OS X-speler systeemeigen.</span><span class="sxs-lookup"><span data-stu-id="70962-108">The decryption of the stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="70962-109">Zie voor meer informatie [dynamische versleuteling met behulp van AES-128 en sleutellevering service](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="70962-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="70962-110">**FairPlay van Apple**</span><span class="sxs-lookup"><span data-stu-id="70962-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="70962-111">De afzonderlijke video en audio-voorbeelden zijn versleuteld met behulp van de **AES-128 CBC** modus.</span><span class="sxs-lookup"><span data-stu-id="70962-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="70962-112">**FairPlay Streaming** (FPS) is geïntegreerd in de besturingssystemen van apparaten, met systeemeigen ondersteuning op iOS- en Apple TV.</span><span class="sxs-lookup"><span data-stu-id="70962-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="70962-113">Safari op OS X kunt FPS met behulp van de interfaceondersteuning versleuteld Media extensies (EME).</span><span class="sxs-lookup"><span data-stu-id="70962-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="70962-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="70962-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="70962-115">De volgende afbeelding toont de **HLS + FairPlay of PlayReady dynamische versleuteling** werkstroom.</span><span class="sxs-lookup"><span data-stu-id="70962-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagram van de dynamische versleuteling werkstroom](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="70962-117">Dit onderwerp wordt beschreven hoe u Media Services gebruiken voor het dynamisch versleutelen van uw inhoud HLS met Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="70962-117">This topic demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="70962-118">U ziet ook hoe u met het Media Services-service voor het leveren van licenties FairPlay-licenties aan clients leveren.</span><span class="sxs-lookup"><span data-stu-id="70962-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="70962-119">Als u wilt er ook voor het versleutelen van uw inhoud HLS met PlayReady, moet u een algemene inhoudssleutel maken en deze koppelen aan uw asset.</span><span class="sxs-lookup"><span data-stu-id="70962-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span></span> <span data-ttu-id="70962-120">U moet ook configureren autorisatiebeleid voor de inhoudssleutel, zoals beschreven in [PlayReady met behulp van dynamische algemene versleuteling](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="70962-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="70962-121">Vereisten en overwegingen</span><span class="sxs-lookup"><span data-stu-id="70962-121">Requirements and considerations</span></span>

<span data-ttu-id="70962-122">Het volgende is vereist als u Media Services leveren HLS versleuteld met FairPlay en FairPlay-licenties te leveren:</span><span class="sxs-lookup"><span data-stu-id="70962-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span></span>

  * <span data-ttu-id="70962-123">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="70962-123">An Azure account.</span></span> <span data-ttu-id="70962-124">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="70962-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="70962-125">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="70962-125">A Media Services account.</span></span> <span data-ttu-id="70962-126">Als u wilt maken, Zie [een Azure Media Services-account maken met de Azure-portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="70962-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="70962-127">Aanmelden bij [Apple Development Program](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="70962-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="70962-128">Apple vereist dat de eigenaar van de inhoud verkrijgen van de [implementatiepakket](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="70962-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="70962-129">Staat u sleutel Security Module (KSM) met Media Services al geïmplementeerd en dat u het laatste FPS pakket aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="70962-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span></span> <span data-ttu-id="70962-130">Er zijn instructies in het laatste FPS pakket certificeringsinstantie genereren en ophalen van de toepassing geheime sleutel (vraag).</span><span class="sxs-lookup"><span data-stu-id="70962-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span></span> <span data-ttu-id="70962-131">VRAAG kunt u FairPlay configureren.</span><span class="sxs-lookup"><span data-stu-id="70962-131">You use ASK to configure FairPlay.</span></span>
  * <span data-ttu-id="70962-132">Azure Media Services .NET SDK versie **3.6.0** of hoger.</span><span class="sxs-lookup"><span data-stu-id="70962-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="70962-133">De volgende zaken moeten worden ingesteld op Media Services sleutellevering kant:</span><span class="sxs-lookup"><span data-stu-id="70962-133">The following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="70962-134">**App-certificaat (AC)**: dit is een .pfx-bestand dat de persoonlijke sleutel bevat.</span><span class="sxs-lookup"><span data-stu-id="70962-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span></span> <span data-ttu-id="70962-135">Dit bestand te maken en versleuteld met een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="70962-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="70962-136">Wanneer u een sleutel leveringsbeleid configureert, moet u opgeven dat het wachtwoord en het pfx-bestand in Base64-indeling.</span><span class="sxs-lookup"><span data-stu-id="70962-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span></span>

      <span data-ttu-id="70962-137">De volgende stappen wordt beschreven hoe een PFX-certificaatbestand voor FairPlay genereren:</span><span class="sxs-lookup"><span data-stu-id="70962-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="70962-138">OpenSSL van https://slproweb.com/products/Win32OpenSSL.html installeren.</span><span class="sxs-lookup"><span data-stu-id="70962-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="70962-139">Ga naar de map waarin het certificaat FairPlay en andere bestanden die door Apple worden geleverd zijn.</span><span class="sxs-lookup"><span data-stu-id="70962-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="70962-140">Voer de volgende opdracht uit via de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="70962-140">Run the following command from the command line.</span></span> <span data-ttu-id="70962-141">Dit converteert het cer-bestand naar een .pem-bestand.</span><span class="sxs-lookup"><span data-stu-id="70962-141">This converts the .cer file to a .pem file.</span></span>

        <span data-ttu-id="70962-142">'C:\OpenSSL-Win32\bin\openssl.exe' x509-informeren der-in fairplay.cer-out fairplay out.pem</span><span class="sxs-lookup"><span data-stu-id="70962-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="70962-143">Voer de volgende opdracht uit via de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="70962-143">Run the following command from the command line.</span></span> <span data-ttu-id="70962-144">Dit converteert het .pem-bestand naar een pfx-bestand met de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="70962-144">This converts the .pem file to a .pfx file with the private key.</span></span> <span data-ttu-id="70962-145">Het wachtwoord voor het pfx-bestand wordt vervolgens door OpenSSL gevraagd.</span><span class="sxs-lookup"><span data-stu-id="70962-145">The password for the .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="70962-146">'C:\OpenSSL-Win32\bin\openssl.exe' pkcs12-Exporteer - fairplay out.pfx-inkey privatekey.pem-in fairplay out.pem - passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="70962-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="70962-147">**Certificaat van de App-wachtwoord**: het wachtwoord voor het maken van het pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="70962-147">**App Cert password**: The password for creating the .pfx file.</span></span>
  * <span data-ttu-id="70962-148">**App-Cert wachtwoord ID**: U moet het wachtwoord, vergelijkbaar met hoe ze andere Media Services-sleutels uploaden uploaden.</span><span class="sxs-lookup"><span data-stu-id="70962-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span></span> <span data-ttu-id="70962-149">Gebruik de **ContentKeyType.FairPlayPfxPassword** enum-waarde ophalen van de Media Services-ID.</span><span class="sxs-lookup"><span data-stu-id="70962-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span></span> <span data-ttu-id="70962-150">Dit is wat ze moeten binnen de beleidsoptie sleutellevering gebruiken.</span><span class="sxs-lookup"><span data-stu-id="70962-150">This is what they need to use inside the key delivery policy option.</span></span>
  * <span data-ttu-id="70962-151">**IV**: dit is een willekeurige waarde van 16 bytes.</span><span class="sxs-lookup"><span data-stu-id="70962-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="70962-152">Deze moet overeenkomen met de iv in het leveringsbeleid voor Assets.</span><span class="sxs-lookup"><span data-stu-id="70962-152">It must match the iv in the asset delivery policy.</span></span> <span data-ttu-id="70962-153">U de iv genereren en plaatsen op beide plaatsen: het leveringsbeleid voor Assets en de optie voor het beleid van sleutel levering.</span><span class="sxs-lookup"><span data-stu-id="70962-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span></span>
  * <span data-ttu-id="70962-154">**VRAAG**: deze sleutel wordt ontvangen bij het genereren van de certificeringsinstantie van Apple Developer portal.</span><span class="sxs-lookup"><span data-stu-id="70962-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span></span> <span data-ttu-id="70962-155">Elke ontwikkelteam ontvangt een unieke vraag.</span><span class="sxs-lookup"><span data-stu-id="70962-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="70962-156">Sla een kopie van de vraag en sla deze op een veilige plaats.</span><span class="sxs-lookup"><span data-stu-id="70962-156">Save a copy of the ASK, and store it in a safe place.</span></span> <span data-ttu-id="70962-157">U moet de vraag als FairPlayAsk met Media Services later configureren.</span><span class="sxs-lookup"><span data-stu-id="70962-157">You will need to configure ASK as FairPlayAsk to Media Services later.</span></span>
  * <span data-ttu-id="70962-158">**Vraag-ID**: deze ID wordt verkregen tijdens het uploaden van vraag in Media Services.</span><span class="sxs-lookup"><span data-stu-id="70962-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="70962-159">U moet een vraag uploaden met behulp van de **ContentKeyType.FairPlayAsk** enum-waarde.</span><span class="sxs-lookup"><span data-stu-id="70962-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="70962-160">Als het resultaat wordt geretourneerd met de ID van de Media Services en dit is wat moet worden gebruikt bij het instellen van de optie voor het beleid van sleutel levering.</span><span class="sxs-lookup"><span data-stu-id="70962-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span></span>

<span data-ttu-id="70962-161">De volgende zaken moeten worden ingesteld door de client FPS:</span><span class="sxs-lookup"><span data-stu-id="70962-161">The following things must be set by the FPS client side:</span></span>

  * <span data-ttu-id="70962-162">**App-certificaat (AC)**: dit is een.cer/.der-bestand met de openbare sleutel, die het besturingssysteem wordt gebruikt voor het versleutelen van sommige nettolading.</span><span class="sxs-lookup"><span data-stu-id="70962-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span></span> <span data-ttu-id="70962-163">Media Services moet weten over het omdat deze door Windows media player is vereist.</span><span class="sxs-lookup"><span data-stu-id="70962-163">Media Services needs to know about it because it is required by the player.</span></span> <span data-ttu-id="70962-164">De service sleutellevering ontsleuteld met behulp van de bijbehorende persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="70962-164">The key delivery service decrypts it using the corresponding private key.</span></span>

<span data-ttu-id="70962-165">Zorg dat u hebt een echte vraag om af te spelen een versleutelde gegevensstroom FairPlay, en vervolgens een echte certificaat genereren.</span><span class="sxs-lookup"><span data-stu-id="70962-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="70962-166">Dit proces wordt gemaakt van alle drie onderdelen:</span><span class="sxs-lookup"><span data-stu-id="70962-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="70962-167">der-bestand</span><span class="sxs-lookup"><span data-stu-id="70962-167">.der file</span></span>
  * <span data-ttu-id="70962-168">PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="70962-168">.pfx file</span></span>
  * <span data-ttu-id="70962-169">wachtwoord voor de .pfx</span><span class="sxs-lookup"><span data-stu-id="70962-169">password for the .pfx</span></span>

<span data-ttu-id="70962-170">De volgende clients ondersteunen HLS met **AES-128 CBC** versleuteling: Safari op OS X, Apple TV iOS.</span><span class="sxs-lookup"><span data-stu-id="70962-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="70962-171">FairPlay dynamische versleuteling en licentie levering van services configureren</span><span class="sxs-lookup"><span data-stu-id="70962-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="70962-172">Hieronder vindt u algemene stappen voor het beveiligen van uw assets met FairPlay met behulp van de Media Services-service voor het leveren van licenties en met behulp van dynamische versleuteling.</span><span class="sxs-lookup"><span data-stu-id="70962-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="70962-173">Maak een asset en upload bestanden in de asset.</span><span class="sxs-lookup"><span data-stu-id="70962-173">Create an asset, and upload files into the asset.</span></span>
2. <span data-ttu-id="70962-174">Codeer de asset met het bestand naar de adaptive bitrate die MP4-set.</span><span class="sxs-lookup"><span data-stu-id="70962-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="70962-175">Maak een inhoudssleutel en deze koppelen aan de gecodeerde asset.</span><span class="sxs-lookup"><span data-stu-id="70962-175">Create a content key, and associate it with the encoded asset.</span></span>  
4. <span data-ttu-id="70962-176">Configureer het autorisatiebeleid voor de inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="70962-176">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="70962-177">Het volgende opgeven:</span><span class="sxs-lookup"><span data-stu-id="70962-177">Specify the following:</span></span>

   * <span data-ttu-id="70962-178">De leveringsmethode (in dit geval FairPlay).</span><span class="sxs-lookup"><span data-stu-id="70962-178">The delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="70962-179">FairPlay opties beleidsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="70962-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="70962-180">Zie voor meer informatie over het configureren van FairPlay de **ConfigureFairPlayPolicyOptions()** methode in het voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="70962-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="70962-181">Meestal kunt zou u wilt configureren FairPlay beleidsopties slechts één keer omdat er slechts één set van een certificeringsinstantie en een vraag.</span><span class="sxs-lookup"><span data-stu-id="70962-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="70962-182">Beperkingen (openen of token).</span><span class="sxs-lookup"><span data-stu-id="70962-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="70962-183">Specifieke informatie voor het type sleutellevering waarmee wordt gedefinieerd hoe de sleutel aan de client wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="70962-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span></span>
5. <span data-ttu-id="70962-184">Configureer het leveringsbeleid voor Assets.</span><span class="sxs-lookup"><span data-stu-id="70962-184">Configure the asset delivery policy.</span></span> <span data-ttu-id="70962-185">De configuratie van een leveringsbeleid omvat:</span><span class="sxs-lookup"><span data-stu-id="70962-185">The delivery policy configuration includes:</span></span>

   * <span data-ttu-id="70962-186">De leveringsprotocol (HLS).</span><span class="sxs-lookup"><span data-stu-id="70962-186">The delivery protocol (HLS).</span></span>
   * <span data-ttu-id="70962-187">Het type dynamische versleuteling (algemene CBC versleuteling).</span><span class="sxs-lookup"><span data-stu-id="70962-187">The type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="70962-188">De URL aanschaf van licentie.</span><span class="sxs-lookup"><span data-stu-id="70962-188">The license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="70962-189">Als u wilt leveren een stroom die is versleuteld met FairPlay en een ander systeem voor beheer van digitale rechten (DRM), hebt u het beleid voor de afzonderlijke levering configureren:</span><span class="sxs-lookup"><span data-stu-id="70962-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="70962-190">Een IAssetDeliveryPolicy configureren met dynamische adaptief streamen via HTTP-(KOPPELTEKEN) met Common Encryption (CENC) (PlayReady en Widevine) en Smooth met PlayReady</span><span class="sxs-lookup"><span data-stu-id="70962-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="70962-191">Een andere IAssetDeliveryPolicy FairPlay voor HLS configureren</span><span class="sxs-lookup"><span data-stu-id="70962-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="70962-192">Maak een OnDemand-locator om een streaming-URL.</span><span class="sxs-lookup"><span data-stu-id="70962-192">Create an OnDemand locator to get a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="70962-193">FairPlay-sleutellevering door player apps gebruiken</span><span class="sxs-lookup"><span data-stu-id="70962-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="70962-194">U kunt player apps ontwikkelen met behulp van de iOS-SDK.</span><span class="sxs-lookup"><span data-stu-id="70962-194">You can develop player apps by using the iOS SDK.</span></span> <span data-ttu-id="70962-195">U hebt om te kunnen FairPlay inhoud af te spelen, voor het implementeren van de licentie voor exchange-protocol.</span><span class="sxs-lookup"><span data-stu-id="70962-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span></span> <span data-ttu-id="70962-196">Dit protocol is niet opgegeven door Apple.</span><span class="sxs-lookup"><span data-stu-id="70962-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="70962-197">Het is tot elke app het sleutellevering aanvragen verzenden.</span><span class="sxs-lookup"><span data-stu-id="70962-197">It is up to each app how to send key delivery requests.</span></span> <span data-ttu-id="70962-198">De Media Services FairPlay sleutellevering service verwacht dat de SPC bij als een www-form-url gecodeerde post bericht in de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="70962-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="70962-199">FairPlay afspelen gebruiksklaar biedt geen ondersteuning voor Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="70962-199">Azure Media Player doesn’t support FairPlay playback out of the box.</span></span> <span data-ttu-id="70962-200">Als u FairPlay afspelen op MAC OS X, Windows media player voorbeeld te verkrijgen uit het Apple developer-account.</span><span class="sxs-lookup"><span data-stu-id="70962-200">To get FairPlay playback on MAC OS X, obtain the sample player from the Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="70962-201">Streaming-URL 's</span><span class="sxs-lookup"><span data-stu-id="70962-201">Streaming URLs</span></span>
<span data-ttu-id="70962-202">Als uw asset is versleuteld met meer dan één DRM, moet u een tag versleuteling in de streaming-URL: (format = 'm3u8-aapl', versleuteling = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="70962-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="70962-203">Het volgende letten:</span><span class="sxs-lookup"><span data-stu-id="70962-203">The following considerations apply:</span></span>

* <span data-ttu-id="70962-204">Alleen nul of één versleutelingstype kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="70962-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="70962-205">Het versleutelingstype hoeft niet te worden opgegeven in de URL als er slechts één versleuteling is toegepast op de asset.</span><span class="sxs-lookup"><span data-stu-id="70962-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="70962-206">Het versleutelingstype is niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="70962-206">The encryption type is case insensitive.</span></span>
* <span data-ttu-id="70962-207">De volgende versleutelingstypen kunnen worden opgegeven:</span><span class="sxs-lookup"><span data-stu-id="70962-207">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="70962-208">**cenc**: Common encryption (PlayReady of Widevine)</span><span class="sxs-lookup"><span data-stu-id="70962-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="70962-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="70962-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="70962-210">**CBC**: AES envelope-versleuteling</span><span class="sxs-lookup"><span data-stu-id="70962-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="70962-211">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="70962-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="70962-212">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="70962-212">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="70962-213">Voeg de volgende elementen toe aan **appSettings** dat in het bestand app.config is gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="70962-213">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="70962-214">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="70962-214">Example</span></span>

<span data-ttu-id="70962-215">Het volgende voorbeeld demonstreert de mogelijkheid om Media Services gebruiken om uw inhoud die is versleuteld met FairPlay.</span><span class="sxs-lookup"><span data-stu-id="70962-215">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="70962-216">Deze functionaliteit werd geïntroduceerd in Azure Media Services SDK voor .NET versie 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="70962-216">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="70962-217">Overschrijf de code in uw Program.cs-bestand met de code die wordt weergegeven in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="70962-217">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="70962-218">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="70962-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="70962-219">U moet dezelfde beleids-id gebruiken als u altijd dezelfde dagen/toegangsmachtigingen gebruikt, bijvoorbeeld beleidsregels voor locators die zijn bedoeld om gedurende een lange periode gehandhaafd te blijven (niet-upload-beleidsregels).</span><span class="sxs-lookup"><span data-stu-id="70962-219">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="70962-220">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="70962-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="70962-221">Zorg ervoor dat variabelen zo worden bijgewerkt dat ze verwijzen naar de mappen waar uw invoerbestanden zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="70962-221">Make sure to update variables to point to folders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on the the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

            // Associate the key with the asset.
            asset.ContentKeys.Add(key);

            return key;
        }


        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Open",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                        Requirements = null
                    }
                    };


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate the content key authorization policy with the content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Token Authorization Policy",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                        Requirements = tokenTemplateString,
                    }
                    };

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with the cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound to a real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key to generate the response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating the .pfx file.
            string pfxPassword = "<customer password for creating the .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key to generate the response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match the iv in the asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify the .pfx file created by the customer.
            var appCert = new X509Certificate2("path to the .pfx file created by the customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get the FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // The reason the below code replaces "https://" with "skd://" is because
            // in the IOS player sample code which you obtained in Apple developer account,
            // the player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
            assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="70962-222">Volgende stappen: Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="70962-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="70962-223">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="70962-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
