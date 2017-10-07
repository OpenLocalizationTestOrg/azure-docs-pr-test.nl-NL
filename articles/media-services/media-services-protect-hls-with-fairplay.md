---
title: aaaProtect HLS inhoud met Microsoft PlayReady of Apple FairPlay - Azure | Microsoft Docs
description: Dit onderwerp een overzicht en ziet u hoe toouse Azure Media Services toodynamically uw HTTP Live Streaming (HLS)-inhoud met Apple FairPlay coderen. U ziet ook hoe toouse Hallo Media Services leveren service toodeliver FairPlay-licenties tooclients licentie.
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
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="dd7c8-104">Beveiligen van uw inhoud met Apple FairPlay of Microsoft PlayReady HLS</span><span class="sxs-lookup"><span data-stu-id="dd7c8-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="dd7c8-105">Azure Media Services kunt u toodynamically versleutelen uw HTTP Live Streaming (HLS)-inhoud met behulp van Hallo volgende indelingen:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-105">Azure Media Services enables you toodynamically encrypt your HTTP Live Streaming (HLS) content by using hello following formats:</span></span>  

* <span data-ttu-id="dd7c8-106">**De lege sleutel envelop voor AES-128**</span><span class="sxs-lookup"><span data-stu-id="dd7c8-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="dd7c8-107">Hallo gehele chunk is versleuteld met Hallo **AES-128 CBC** modus.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-107">hello entire chunk is encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="dd7c8-108">Hallo-ontsleuteling van Hallo stroom wordt ondersteund door iOS en OS X-speler systeemeigen.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-108">hello decryption of hello stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="dd7c8-109">Zie voor meer informatie [dynamische versleuteling met behulp van AES-128 en sleutellevering service](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="dd7c8-110">**FairPlay van Apple**</span><span class="sxs-lookup"><span data-stu-id="dd7c8-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="dd7c8-111">Hallo afzonderlijke video en audio-voorbeelden zijn versleuteld met behulp van Hallo **AES-128 CBC** modus.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-111">hello individual video and audio samples are encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="dd7c8-112">**FairPlay Streaming** (FPS) is geïntegreerd in Hallo besturingssystemen van apparaten, met systeemeigen ondersteuning op iOS- en Apple TV.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-112">**FairPlay Streaming** (FPS) is integrated into hello device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="dd7c8-113">Safari op OS X kunt FPS met behulp van de ondersteuning van de interface Hallo versleuteld Media extensies (EME).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-113">Safari on OS X enables FPS by using hello Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="dd7c8-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="dd7c8-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="dd7c8-115">Hallo volgende afbeelding toont Hallo **HLS + FairPlay of PlayReady dynamische versleuteling** werkstroom.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-115">hello following image shows hello **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagram van de dynamische versleuteling werkstroom](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="dd7c8-117">Dit onderwerp wordt beschreven hoe toouse Media Services toodynamically uw inhoud HLS met Apple FairPlay coderen.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-117">This topic demonstrates how toouse Media Services toodynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="dd7c8-118">U ziet ook hoe toouse Hallo Media Services leveren service toodeliver FairPlay-licenties tooclients licentie.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-118">It also shows how toouse hello Media Services license delivery service toodeliver FairPlay licenses tooclients.</span></span>

> [!NOTE]
> <span data-ttu-id="dd7c8-119">Als u ook tooencrypt uw HLS inhoud met PlayReady wilt, u moet een algemene inhoudssleutel toocreate en deze koppelen aan uw asset.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-119">If you also want tooencrypt your HLS content with PlayReady, you need toocreate a common content key and associate it with your asset.</span></span> <span data-ttu-id="dd7c8-120">U moet ook tooconfigure Hallo voor de inhoudssleutel autorisatie, zoals beschreven in [PlayReady met behulp van dynamische algemene versleuteling](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-120">You also need tooconfigure hello content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="dd7c8-121">Vereisten en overwegingen</span><span class="sxs-lookup"><span data-stu-id="dd7c8-121">Requirements and considerations</span></span>

<span data-ttu-id="dd7c8-122">Hallo volgende is vereist wanneer u Media Services toodeliver die HLS versleuteld met FairPlay en toodeliver FairPlay-licenties:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-122">hello following are required when using Media Services toodeliver HLS encrypted with FairPlay, and toodeliver FairPlay licenses:</span></span>

  * <span data-ttu-id="dd7c8-123">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-123">An Azure account.</span></span> <span data-ttu-id="dd7c8-124">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="dd7c8-125">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-125">A Media Services account.</span></span> <span data-ttu-id="dd7c8-126">toocreate, Zie [een Azure Media Services-account maken met Azure-portal Hallo](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-126">toocreate one, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="dd7c8-127">Aanmelden bij [Apple Development Program](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="dd7c8-128">Apple vereist Hallo inhoudseigenaar tooobtain hello [implementatiepakket](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-128">Apple requires hello content owner tooobtain hello [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="dd7c8-129">Staat u sleutel Security Module (KSM) met Media Services al geïmplementeerd en dat u Hallo laatste FPS pakket aanvraagt.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting hello final FPS package.</span></span> <span data-ttu-id="dd7c8-130">Er zijn instructies in Hallo laatste FPS toogenerate certificeringsinstantie van het pakket en verkrijgen Hallo toepassing geheime sleutel (vraag).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-130">There are instructions in hello final FPS package toogenerate certification and obtain hello Application Secret Key (ASK).</span></span> <span data-ttu-id="dd7c8-131">U vraag tooconfigure FairPlay gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-131">You use ASK tooconfigure FairPlay.</span></span>
  * <span data-ttu-id="dd7c8-132">Azure Media Services .NET SDK versie **3.6.0** of hoger.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="dd7c8-133">Hallo dingen volgende moet zijn ingesteld op Media Services sleutellevering kant:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-133">hello following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="dd7c8-134">**App-certificaat (AC)**: dit is een .pfx-bestand dat Hallo persoonlijke sleutel bevat.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-134">**App Cert (AC)**: This is a .pfx file that contains hello private key.</span></span> <span data-ttu-id="dd7c8-135">Dit bestand te maken en versleuteld met een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="dd7c8-136">Wanneer u een sleutel leveringsbeleid configureert, moet u opgeven dat wachtwoord en Hallo pfx-bestand in Base64-indeling.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-136">When you configure a key delivery policy, you must provide that password and hello .pfx file in Base64 format.</span></span>

      <span data-ttu-id="dd7c8-137">Hallo stappen wordt beschreven hoe toogenerate een pfx-certificaat voor FairPlay bestand:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-137">hello following steps describe how toogenerate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="dd7c8-138">OpenSSL van https://slproweb.com/products/Win32OpenSSL.html installeren.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="dd7c8-139">Ga toohello map Hallo FairPlay certificaat en andere bestanden die door Apple worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-139">Go toohello folder where hello FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="dd7c8-140">Hallo volgende opdracht uit vanaf de opdrachtregel Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-140">Run hello following command from hello command line.</span></span> <span data-ttu-id="dd7c8-141">Dit converteert Hallo .cer-bestand tooa .pem-bestand.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-141">This converts hello .cer file tooa .pem file.</span></span>

        <span data-ttu-id="dd7c8-142">'C:\OpenSSL-Win32\bin\openssl.exe' x509-informeren der-in fairplay.cer-out fairplay out.pem</span><span class="sxs-lookup"><span data-stu-id="dd7c8-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="dd7c8-143">Hallo volgende opdracht uit vanaf de opdrachtregel Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-143">Run hello following command from hello command line.</span></span> <span data-ttu-id="dd7c8-144">Dit converteert Hallo .pem-bestand tooa pfx-bestand met de persoonlijke sleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-144">This converts hello .pem file tooa .pfx file with hello private key.</span></span> <span data-ttu-id="dd7c8-145">Hallo-wachtwoord voor Hallo pfx-bestand wordt vervolgens door OpenSSL gevraagd.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-145">hello password for hello .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="dd7c8-146">'C:\OpenSSL-Win32\bin\openssl.exe' pkcs12-Exporteer - fairplay out.pfx-inkey privatekey.pem-in fairplay out.pem - passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="dd7c8-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="dd7c8-147">**Certificaat van de App-wachtwoord**: Hallo wachtwoord voor het maken van Hallo pfx-bestand.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-147">**App Cert password**: hello password for creating hello .pfx file.</span></span>
  * <span data-ttu-id="dd7c8-148">**App-Cert wachtwoord ID**: U moet uploaden Hallo wachtwoord, vergelijkbare toohow uploaden van andere sleutels Media Services.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-148">**App Cert password ID**: You must upload hello password, similar toohow they upload other Media Services keys.</span></span> <span data-ttu-id="dd7c8-149">Gebruik Hallo **ContentKeyType.FairPlayPfxPassword** enum-waarde tooget Hallo Media Services-ID.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-149">Use hello **ContentKeyType.FairPlayPfxPassword** enum value tooget hello Media Services ID.</span></span> <span data-ttu-id="dd7c8-150">Dit is wat ze moeten toouse binnen Hallo sleutellevering beleidsoptie.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-150">This is what they need toouse inside hello key delivery policy option.</span></span>
  * <span data-ttu-id="dd7c8-151">**IV**: dit is een willekeurige waarde van 16 bytes.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="dd7c8-152">Moet overeenkomen met iv Hallo in Hallo-leveringsbeleid voor Assets.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-152">It must match hello iv in hello asset delivery policy.</span></span> <span data-ttu-id="dd7c8-153">U genereert Hallo iv en plaatsen op beide plaatsen: Hallo-leveringsbeleid voor Assets en Hallo sleutellevering beleidsoptie.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-153">You generate hello iv, and put it in both places: hello asset delivery policy and hello key delivery policy option.</span></span>
  * <span data-ttu-id="dd7c8-154">**VRAAG**: deze sleutel wordt ontvangen bij het genereren van Hallo certificering met behulp van Hallo Apple Developer portal.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-154">**ASK**: This key is received when you generate hello certification by using hello Apple Developer portal.</span></span> <span data-ttu-id="dd7c8-155">Elke ontwikkelteam ontvangt een unieke vraag.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="dd7c8-156">Sla een kopie van Hallo vraag en sla deze op een veilige plaats.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-156">Save a copy of hello ASK, and store it in a safe place.</span></span> <span data-ttu-id="dd7c8-157">U moet tooconfigure vraag later als FairPlayAsk tooMedia Services.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-157">You will need tooconfigure ASK as FairPlayAsk tooMedia Services later.</span></span>
  * <span data-ttu-id="dd7c8-158">**Vraag-ID**: deze ID wordt verkregen tijdens het uploaden van vraag in Media Services.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="dd7c8-159">U moet de vraag uploaden via Hallo **ContentKeyType.FairPlayAsk** enum-waarde.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-159">You must upload ASK by using hello **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="dd7c8-160">Hallo Media Services-ID wordt geretourneerd als resultaat Hallo en dit is wat moet worden gebruikt bij het instellen van Hallo sleutellevering beleidsoptie.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-160">As hello result, hello Media Services ID is returned, and this is what should be used when setting hello key delivery policy option.</span></span>

<span data-ttu-id="dd7c8-161">Hallo moeten volgende bewerkingen worden ingesteld door Hallo FPS clientzijde:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-161">hello following things must be set by hello FPS client side:</span></span>

  * <span data-ttu-id="dd7c8-162">**App-certificaat (AC)**: dit is een.cer/.der-bestand dat Hallo openbare sleutel, welke Hallo-besturingssysteem tooencrypt gebruikt sommige nettolading bevat.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-162">**App Cert (AC)**: This is a .cer/.der file that contains hello public key, which hello operating system uses tooencrypt some payload.</span></span> <span data-ttu-id="dd7c8-163">Media Services moet tooknow erover omdat deze is vereist door Hallo player.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-163">Media Services needs tooknow about it because it is required by hello player.</span></span> <span data-ttu-id="dd7c8-164">Hallo sleutellevering service ontsleutelt met behulp van de bijbehorende persoonlijke sleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-164">hello key delivery service decrypts it using hello corresponding private key.</span></span>

<span data-ttu-id="dd7c8-165">een versleutelde gegevensstroom FairPlay back tooplay, een echte vraag eerste ophalen en vervolgens een echte certificaat genereren.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-165">tooplay back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="dd7c8-166">Dit proces wordt gemaakt van alle drie onderdelen:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="dd7c8-167">der-bestand</span><span class="sxs-lookup"><span data-stu-id="dd7c8-167">.der file</span></span>
  * <span data-ttu-id="dd7c8-168">PFX-bestand</span><span class="sxs-lookup"><span data-stu-id="dd7c8-168">.pfx file</span></span>
  * <span data-ttu-id="dd7c8-169">wachtwoord voor pfx Hallo</span><span class="sxs-lookup"><span data-stu-id="dd7c8-169">password for hello .pfx</span></span>

<span data-ttu-id="dd7c8-170">Hallo volgende clients ondersteunen HLS met **AES-128 CBC** versleuteling: Safari op OS X, Apple TV iOS.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-170">hello following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="dd7c8-171">FairPlay dynamische versleuteling en licentie levering van services configureren</span><span class="sxs-lookup"><span data-stu-id="dd7c8-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="dd7c8-172">Hallo hieronder vindt u algemene stappen voor het beveiligen van uw assets met FairPlay met behulp van Hallo Media Services-licentieservice levering en met behulp van dynamische versleuteling.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-172">hello following are general steps for protecting your assets with FairPlay by using hello Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="dd7c8-173">Maak een asset en upload bestanden in Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-173">Create an asset, and upload files into hello asset.</span></span>
2. <span data-ttu-id="dd7c8-174">Hallo asset met Hallo bestand toohello adaptive bitrate die MP4-set coderen.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-174">Encode hello asset that contains hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="dd7c8-175">Maak een inhoudssleutel en deze koppelen aan Hallo gecodeerde asset.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-175">Create a content key, and associate it with hello encoded asset.</span></span>  
4. <span data-ttu-id="dd7c8-176">Hallo de inhoudssleutel verificatiebeleid configureren.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-176">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="dd7c8-177">Hallo volgende opgeven:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-177">Specify hello following:</span></span>

   * <span data-ttu-id="dd7c8-178">Hallo leveringsmethode (in dit geval FairPlay).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-178">hello delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="dd7c8-179">FairPlay opties beleidsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="dd7c8-180">Voor meer informatie over het tooconfigure FairPlay, Zie Hallo **ConfigureFairPlayPolicyOptions()** methode in Hallo voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-180">For details on how tooconfigure FairPlay, see hello **ConfigureFairPlayPolicyOptions()** method in hello sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="dd7c8-181">Meestal kunt u opties voor tooconfigure FairPlay beleid slechts één keer omdat er slechts één set van een certificeringsinstantie en een vraag.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-181">Usually, you would want tooconfigure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="dd7c8-182">Beperkingen (openen of token).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="dd7c8-183">Informatie specifieke toohello type sleutellevering waarmee wordt gedefinieerd hoe Hallo sleutel toohello client wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-183">Information specific toohello key delivery type that defines how hello key is delivered toohello client.</span></span>
5. <span data-ttu-id="dd7c8-184">Hallo-leveringsbeleid voor Assets configureren.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-184">Configure hello asset delivery policy.</span></span> <span data-ttu-id="dd7c8-185">configuratie van Hallo een leveringsbeleid omvat:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-185">hello delivery policy configuration includes:</span></span>

   * <span data-ttu-id="dd7c8-186">Hallo leveringsprotocol (HLS).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-186">hello delivery protocol (HLS).</span></span>
   * <span data-ttu-id="dd7c8-187">Hallo type dynamische versleuteling (algemene CBC versleuteling).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-187">hello type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="dd7c8-188">Hallo-URL voor het verkrijgen van licentie.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-188">hello license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="dd7c8-189">Als u wilt dat toodeliver een stroom die is versleuteld met FairPlay en een ander systeem voor beheer van digitale rechten (DRM), hebt u beleid voor de afzonderlijke levering tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-189">If you want toodeliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have tooconfigure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="dd7c8-190">Een IAssetDeliveryPolicy tooconfigure dynamische adaptief streamen via HTTP-(KOPPELTEKEN) met Common Encryption (CENC) (PlayReady en Widevine) en Smooth met PlayReady</span><span class="sxs-lookup"><span data-stu-id="dd7c8-190">One IAssetDeliveryPolicy tooconfigure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="dd7c8-191">Een andere IAssetDeliveryPolicy tooconfigure FairPlay voor HLS</span><span class="sxs-lookup"><span data-stu-id="dd7c8-191">Another IAssetDeliveryPolicy tooconfigure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="dd7c8-192">Maak een OnDemand-locator tooget een streaming-URL.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-192">Create an OnDemand locator tooget a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="dd7c8-193">FairPlay-sleutellevering door player apps gebruiken</span><span class="sxs-lookup"><span data-stu-id="dd7c8-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="dd7c8-194">U kunt player apps ontwikkelen met behulp van Hallo iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-194">You can develop player apps by using hello iOS SDK.</span></span> <span data-ttu-id="dd7c8-195">toobe kunnen tooplay FairPlay inhoud, hebt u tooimplement Hallo licentie exchange-protocol.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-195">toobe able tooplay FairPlay content, you have tooimplement hello license exchange protocol.</span></span> <span data-ttu-id="dd7c8-196">Dit protocol is niet opgegeven door Apple.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="dd7c8-197">Het is tooeach-app wordt ingesteld hoe toosend sleutellevering aanvragen.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-197">It is up tooeach app how toosend key delivery requests.</span></span> <span data-ttu-id="dd7c8-198">Hallo Media Services FairPlay sleutellevering service verwacht Hallo SPC toocome als een bericht www-form-url gecodeerde post in Hallo formulier te volgen:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-198">hello Media Services FairPlay key delivery service expects hello SPC toocome as a www-form-url encoded post message, in hello following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="dd7c8-199">FairPlay afspelen out of box Hallo biedt geen ondersteuning voor Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-199">Azure Media Player doesn’t support FairPlay playback out of hello box.</span></span> <span data-ttu-id="dd7c8-200">Hallo voorbeeld player tooget FairPlay af te spelen op MAC OS X verkrijgen van Hallo Apple developer-account.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-200">tooget FairPlay playback on MAC OS X, obtain hello sample player from hello Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="dd7c8-201">Streaming-URL 's</span><span class="sxs-lookup"><span data-stu-id="dd7c8-201">Streaming URLs</span></span>
<span data-ttu-id="dd7c8-202">Als uw asset is versleuteld met meer dan één DRM, moet u een tag versleuteling in Hallo streaming-URL: (format = 'm3u8-aapl', versleuteling = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="dd7c8-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="dd7c8-203">Hallo overwegingen volgende van toepassing:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-203">hello following considerations apply:</span></span>

* <span data-ttu-id="dd7c8-204">Alleen nul of één versleutelingstype kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="dd7c8-205">Hallo versleutelingstype heeft geen toobe opgegeven in Hallo URL als er slechts één versleuteling toegepaste toohello actief is.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-205">hello encryption type doesn't have toobe specified in hello URL if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="dd7c8-206">Hallo versleutelingstype is niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-206">hello encryption type is case insensitive.</span></span>
* <span data-ttu-id="dd7c8-207">Hallo na versleutelingstypen kan worden opgegeven:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-207">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="dd7c8-208">**cenc**: Common encryption (PlayReady of Widevine)</span><span class="sxs-lookup"><span data-stu-id="dd7c8-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="dd7c8-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="dd7c8-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="dd7c8-210">**CBC**: AES envelope-versleuteling</span><span class="sxs-lookup"><span data-stu-id="dd7c8-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="dd7c8-211">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="dd7c8-212">Uw ontwikkelomgeving instellen en vullen Hallo app.config-bestand met de verbindingsinformatie, zoals beschreven in [ontwikkelen van Media Services met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-212">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="dd7c8-213">Hallo elementen te volgen toevoegen**appSettings** gedefinieerd in het bestand app.config:</span><span class="sxs-lookup"><span data-stu-id="dd7c8-213">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="dd7c8-214">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="dd7c8-214">Example</span></span>

<span data-ttu-id="dd7c8-215">Hallo volgende voorbeeld ziet u uw inhoud die is versleuteld met FairPlay Hallo mogelijkheid toouse toodeliver Media Services.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-215">hello following sample demonstrates hello ability toouse Media Services toodeliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="dd7c8-216">Deze functionaliteit werd geïntroduceerd in hello Azure Media Services SDK voor .NET versie 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-216">This functionality was introduced in hello Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="dd7c8-217">Hallo-code in uw Program.cs-bestand met de Hallo-code die wordt weergegeven in deze sectie worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-217">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="dd7c8-218">Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="dd7c8-219">Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn).</span><span class="sxs-lookup"><span data-stu-id="dd7c8-219">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="dd7c8-220">Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="dd7c8-221">Zorg ervoor dat tooupdate variabelen toopoint toofolders waar uw invoerbestanden zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="dd7c8-221">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

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
        // Read values from hello App.config file.
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
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
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

            // Associate hello key with hello asset.
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

            // Associate hello content key authorization policy with hello content key.
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

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

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

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
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

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
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


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="dd7c8-222">Volgende stappen: Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="dd7c8-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dd7c8-223">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="dd7c8-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
