---
title: aaaUsing Axinom toodeliver Widevine-licenties tooAzure Media Services | Microsoft Docs
description: Dit artikel wordt beschreven hoe u Azure Media Services (AMS) toodeliver een stroom die dynamisch wordt versleuteld met AMS met PlayReady en Widevine DRM's kunt gebruiken. Hallo PlayReady-licenties afkomstig van de licentieserver Media Services PlayReady en Widevine-licentie wordt geleverd door Axinom licentieserver.
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 2245d9269c30712ef779973ae021c00c76174d0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="0c0a0-104">Met behulp van Axinom toodeliver Widevine-licenties tooAzure Media Services</span><span class="sxs-lookup"><span data-stu-id="0c0a0-104">Using Axinom toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c0a0-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="0c0a0-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="0c0a0-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="0c0a0-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="0c0a0-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="0c0a0-107">Overview</span></span>
<span data-ttu-id="0c0a0-108">Azure Media Services (AMS) is toegevoegd Google Widevine dynamic beveiliging (Zie [blog van Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="0c0a0-109">Bovendien Azure Media Player (AMP) is ook Widevine ondersteuning toegevoegd (Zie [AMP document](http://amp.azure.net/libs/amp/latest/docs/) voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="0c0a0-110">Dit is een belangrijke vervullen in de streaming DASH-inhoud beveiligd met CENC met meerdere-native-DRM (PlayReady en Widevine) moderne browsers zijn uitgerust met muis en EME.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="0c0a0-111">Media Services vanaf Media Services .NET SDK versie 3.5.2 hello, kunt u tooconfigure Widevine-licentiesjabloon en Widevine-licenties ophalen.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-111">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="0c0a0-112">U kunt ook Hallo AMS-partners toohelp u leveren met Widevine-licenties te volgen: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-112">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="0c0a0-113">Dit artikel wordt beschreven hoe toointegrate en test Widevine server beheerd door Axinom licentie.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-113">This article describes how toointegrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="0c0a0-114">In het bijzonder omvatten ze:</span><span class="sxs-lookup"><span data-stu-id="0c0a0-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="0c0a0-115">Dynamic Common Encryption configureren met multi-DRM (PlayReady en Widevine) met de bijbehorende licentie overname-URL's;</span><span class="sxs-lookup"><span data-stu-id="0c0a0-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="0c0a0-116">Genereren van een JWT-token in volgorde toomeet Hallo server licentievereisten;</span><span class="sxs-lookup"><span data-stu-id="0c0a0-116">Generating a JWT token in order toomeet hello license server requirements;</span></span>
* <span data-ttu-id="0c0a0-117">Azure Media Player-app die aanschaf van licentie met JWT-token verificatie zorgt; ontwikkelt</span><span class="sxs-lookup"><span data-stu-id="0c0a0-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="0c0a0-118">Hallo volledige systeem en Hallo stroom van inhoud die en de belangrijkste-ID, sleutel seed, JTW token en de claims beste door het volgende diagram Hallo kan worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-118">hello complete system and hello flow of content key, key ID, key seed, JTW token and its claims can be best described by hello following diagram.</span></span>

![DASH en CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="0c0a0-120">Content Protection</span><span class="sxs-lookup"><span data-stu-id="0c0a0-120">Content Protection</span></span>
<span data-ttu-id="0c0a0-121">Zie voor het configureren van dynamische beveiliging en belangrijke leveringsbeleid Mingfei van blog: [hoe tooconfigure Widevine-verpakking met Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How tooconfigure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="0c0a0-122">U kunt dynamische CENC beveiliging configureren met multi-DRM voor streaming beide volgende Hallo DASH:</span><span class="sxs-lookup"><span data-stu-id="0c0a0-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of hello following:</span></span>

1. <span data-ttu-id="0c0a0-123">PlayReady-beveiliging voor MS Edge en IE11 die kan een token autorisatiebeperkingen hebben.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="0c0a0-124">Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS), zoals Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-124">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="0c0a0-125">Widevine-beveiliging voor Chrome, kan deze tokenverificatie vereisen met token dat is uitgegeven door een andere STS.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="0c0a0-126">Zie [genereren van JWT-tokens](media-services-axinom-integration.md#jwt-token-generation) sectie voor waarom Azure Active Directory kan niet worden gebruikt als een STS voor Axinom van Widevine-licentieserver.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="0c0a0-127">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="0c0a0-127">Considerations</span></span>
1. <span data-ttu-id="0c0a0-128">U moet Hallo die axinom sleutel seed (8888000000000000000000000000000000000000) en de gegenereerde of de geselecteerde sleutel ID toogenerate Hallo inhoud sleutel opgegeven voor het configureren van de service voor het leveren van sleutel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-128">You must use hello Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID toogenerate hello content key for configuring key delivery service.</span></span> <span data-ttu-id="0c0a0-129">Licentieserver Axinom verleent alle licenties met inhoud sleutels die zijn gebaseerd op Hallo sleutel seed die geldig voor testen en productie is.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-129">Axinom license server will issue all licenses containing content keys based on hello same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="0c0a0-130">Hallo Widevine-licentie de URL voor het testen: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-130">hello Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="0c0a0-131">HTTP- en HTTS zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="0c0a0-132">Azure Media Player voorbereiding</span><span class="sxs-lookup"><span data-stu-id="0c0a0-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="0c0a0-133">AMP v1.4.0 ondersteunt het afspelen van inhoud van het AMS die dynamisch wordt verpakt met PlayReady en Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="0c0a0-134">Als de licentieserver Widevine tokenverificatie niet vereist, zijn er geen extra moet u toodo tootest een streepje inhoud beveiligd door Widevine.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-134">If Widevine license server does not require token authentication, there is nothing additional you need toodo tootest a DASH content protected by Widevine.</span></span> <span data-ttu-id="0c0a0-135">Voor een voorbeeld Hallo AMP team biedt een eenvoudige [voorbeeld](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), waar u deze in de werkt rand en IE11 met PlayReady en Chrome met Widevine kunt zien.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-135">For an example, hello AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="0c0a0-136">Hallo Widevine-licentie verstrekt door Axinom JWT-token is verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-136">hello Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="0c0a0-137">Hallo JWT-token moet toobe verzonden met licentieaanvraag via een HTTP-header 'X AxDRM bericht'.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-137">hello JWT token needs toobe submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="0c0a0-138">Hiertoe moet u tooadd Hallo javascript in Hallo webpagina's die als host fungeert AMP voordat instelling Hallo bron te volgen:</span><span class="sxs-lookup"><span data-stu-id="0c0a0-138">For this purpose, you need tooadd hello following javascript in hello web page hosting AMP before setting hello source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="0c0a0-139">Hallo rest AMP code is standaard AMP API zoals in het document AMP [hier](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-139">hello rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="0c0a0-140">Houd er rekening mee dat Hallo hierboven javascript voor instelling aangepaste autorisatie-header is nog steeds een korte termijn benadering voordat Hallo officiële benadering van de lange termijn in AMP wordt vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-140">Note that hello above javascript for setting custom authorization header is still a short term approach before hello official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="0c0a0-141">Genereren van JWT-tokens</span><span class="sxs-lookup"><span data-stu-id="0c0a0-141">JWT Token Generation</span></span>
<span data-ttu-id="0c0a0-142">Axinom Widevine-licentie voor het testen van JWT-token is verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="0c0a0-143">Bovendien is een van de claims Hallo in Hallo JWT-token van een type complexe object in plaats van een primitief gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-143">In addition, one of hello claims in hello JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="0c0a0-144">Azure AD kunt helaas alleen JWT-tokens uitgeven met primitieve typen.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="0c0a0-145">Op deze manier kunt .NET Framework-API (System.IdentityModel.Tokens.SecurityTokenHandler en JwtPayload) u alleen tooinput complexe objecttype als claims.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you tooinput complex object type as claims.</span></span> <span data-ttu-id="0c0a0-146">Hallo claims zijn echter nog steeds geserialiseerd als tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-146">However, hello claims are still serialized as string.</span></span> <span data-ttu-id="0c0a0-147">Daarom niet we een Hallo twee gebruiken voor genereren Hallo JWT-token voor Widevine-licentie-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-147">Therefore we cannot use any of hello two for generating hello JWT token for Widevine license request.</span></span>

<span data-ttu-id="0c0a0-148">John Sheehan van [JWT Nuget-pakket](https://www.nuget.org/packages/JWT) voldoet aan de behoeften Hallo zodat we toouse gaan deze Nuget-pakket.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets hello needs so we are going toouse this Nuget package.</span></span>

<span data-ttu-id="0c0a0-149">Hieronder vindt u Hallo code voor het genereren van JWT-token met Hallo nodig claims door de server voor Axinom Widevine-licentie vereist voor het testen:</span><span class="sxs-lookup"><span data-stu-id="0c0a0-149">Below is hello code for generating JWT token with hello needed claims as required by Axinom Widevine license server for testing:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string toobyte[] Note: Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string toobyte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "hello binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

<span data-ttu-id="0c0a0-150">Axinom Widevine-licentieserver</span><span class="sxs-lookup"><span data-stu-id="0c0a0-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="0c0a0-151">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="0c0a0-151">Considerations</span></span>
1. <span data-ttu-id="0c0a0-152">Hoewel AMS PlayReady-service voor het leveren van licentie is vereist ' Bearer = "geen verificatietoken verdergaat Axinom Widevine-licentieserver gebruikt deze niet.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="0c0a0-153">Hallo Axinom communicatie sleutel wordt gebruikt als de handtekeningsleutel.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-153">hello Axinom communication key is used as signing key.</span></span> <span data-ttu-id="0c0a0-154">Houd er rekening mee dat Hallo-sleutel is een hexadecimale tekenreeks, maar deze moet worden behandeld als een reeks bytes niet naar een tekenreeks als codering.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-154">Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="0c0a0-155">Dit wordt bereikt door Hallo methode ConvertHexStringToByteArray.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-155">This is achieved by hello method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="0c0a0-156">Bij het ophalen van sleutel-ID</span><span class="sxs-lookup"><span data-stu-id="0c0a0-156">Retrieving Key ID</span></span>
<span data-ttu-id="0c0a0-157">U mogelijk opgevallen dat in Hallo-code voor het genereren van een JWT-token, sleutel-ID is vereist.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-157">You may have noticed that in hello code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="0c0a0-158">Omdat Hallo JWT-token toobe gereed is moet voordat het laden van het AMP, in volgorde van ID behoeften toobe opgehaald in toogenerate JWT-token.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-158">Since hello JWT token needs toobe ready before loading AMP player, key ID needs toobe retrieved in order toogenerate JWT token.</span></span>

<span data-ttu-id="0c0a0-159">Uiteraard er zijn meerdere manieren tooget houdt van sleutel-id.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-159">Of course there are multiple ways tooget hold of key ID.</span></span> <span data-ttu-id="0c0a0-160">Bijvoorbeeld, een kan opslaan ID sleutel samen met de metagegevens van inhoud in een database.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="0c0a0-161">Of u kunt ophalen sleutel-ID van het streepje MPD (beschrijving Media presentatie)-bestand.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="0c0a0-162">Hallo-code hieronder is voor de laatste Hallo.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-162">hello code below is for hello latter.</span></span>

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a><span data-ttu-id="0c0a0-163">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="0c0a0-163">Summary</span></span>
<span data-ttu-id="0c0a0-164">Met de meest recente toevoeging van Widevine-ondersteuning in Azure Media Services Content Protection zowel Azure Media Player we kunnen tooimplement streaming van DASH + meerdere native DRM (PlayReady en Widevine) met zowel PlayReady-licentie-service in AMS en Widevine-licentie de server van Axinom voor Hallo moderne browsers te volgen:</span><span class="sxs-lookup"><span data-stu-id="0c0a0-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able tooimplement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for hello following modern browsers:</span></span>

* <span data-ttu-id="0c0a0-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="0c0a0-165">Chrome</span></span>
* <span data-ttu-id="0c0a0-166">Microsoft Edge op Windows 10</span><span class="sxs-lookup"><span data-stu-id="0c0a0-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="0c0a0-167">IE 11 op Windows 8.1 en Windows 10</span><span class="sxs-lookup"><span data-stu-id="0c0a0-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="0c0a0-168">Zowel Firefox (Desktop) en Safari op Mac (geen iOS) worden ook ondersteund via Silverlight en dezelfde URL met Azure Media Player Hallo</span><span class="sxs-lookup"><span data-stu-id="0c0a0-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and hello same URL with Azure Media Player</span></span>

<span data-ttu-id="0c0a0-169">Hallo zijn volgende parameters vereist in Hallo Mini-oplossing van Axinom Widevine-licentieserver.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-169">hello following parameters are required in hello mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="0c0a0-170">Met uitzondering van sleutel-ID, Hallo rest van de parameters worden geleverd door Axinom op basis van hun installatie Widevine-server.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-170">Except for key ID, hello rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="0c0a0-171">Parameter</span><span class="sxs-lookup"><span data-stu-id="0c0a0-171">Parameter</span></span> | <span data-ttu-id="0c0a0-172">Hoe deze wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="0c0a0-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="0c0a0-173">Communicatie ID sleutel</span><span class="sxs-lookup"><span data-stu-id="0c0a0-173">Communication key ID</span></span> |<span data-ttu-id="0c0a0-174">Moet worden opgenomen als waarde van Hallo claim 'com_key_id' in de JWT-token (Zie [dit](media-services-axinom-integration.md#jwt-token-generation) sectie).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-174">Must be included as value of hello claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="0c0a0-175">Communicatie-sleutel</span><span class="sxs-lookup"><span data-stu-id="0c0a0-175">Communication key</span></span> |<span data-ttu-id="0c0a0-176">Moet worden gebruikt als Hallo ondertekeningssleutel van JWT-token (Zie [dit](media-services-axinom-integration.md#jwt-token-generation) sectie).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-176">Must be used as hello signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="0c0a0-177">Sleutel seed</span><span class="sxs-lookup"><span data-stu-id="0c0a0-177">Key seed</span></span> |<span data-ttu-id="0c0a0-178">Moet worden gebruikt toogenerate inhoudssleutel met een opgegeven inhoud ID sleutel (Zie [dit](media-services-axinom-integration.md#content-protection) sectie).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-178">Must be used toogenerate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="0c0a0-179">URL voor Widevine-licentie</span><span class="sxs-lookup"><span data-stu-id="0c0a0-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="0c0a0-180">Moet worden gebruikt bij het configureren van het leveringsbeleid voor Assets voor DASH streaming (Zie [dit](media-services-axinom-integration.md#content-protection) sectie).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="0c0a0-181">Inhoud sleutel-ID</span><span class="sxs-lookup"><span data-stu-id="0c0a0-181">Content Key ID</span></span> |<span data-ttu-id="0c0a0-182">Moet worden opgenomen als onderdeel van Hallo-waarde van de claim recht bericht van het JWT-token (Zie [dit](media-services-axinom-integration.md#jwt-token-generation) sectie).</span><span class="sxs-lookup"><span data-stu-id="0c0a0-182">Must be included as part of hello value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="0c0a0-183">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="0c0a0-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0c0a0-184">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="0c0a0-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="0c0a0-185">Bevestigingen</span><span class="sxs-lookup"><span data-stu-id="0c0a0-185">Acknowledgments</span></span>
<span data-ttu-id="0c0a0-186">Willen we graag tooacknowledge Hallo personen die hebben bijgedragen tot de verwezenlijking van dit document te volgen: Kristjan Jõgi van Axinom Mingfei Yan en Amit Rajput.</span><span class="sxs-lookup"><span data-stu-id="0c0a0-186">We would like tooacknowledge hello following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

