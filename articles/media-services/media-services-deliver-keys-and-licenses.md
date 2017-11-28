---
title: Azure Media Services gebruiken om te leveren van DRM-licenties of AES-sleutels
description: Dit artikel wordt beschreven hoe u Azure Media Services (AMS) kunt gebruiken voor het leveren van PlayReady en/of Widevine-licenties en AES-sleutels, maar bieden de overige (codering, versleutelen, streaming) met behulp van uw on-premises servers.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 8546c2c1-430b-4254-a88d-4436a83f9192
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 263a381dc72105eea60ad9b39434599ff04a4531
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-services-to-deliver-drm-licenses-or-aes-keys"></a><span data-ttu-id="d73f7-103">Azure Media Services gebruiken om te leveren van DRM-licenties of AES-sleutels</span><span class="sxs-lookup"><span data-stu-id="d73f7-103">Use Azure Media Services to deliver DRM licenses or AES keys</span></span>
<span data-ttu-id="d73f7-104">Azure Media Services (AMS) kunt u opnemen, coderen, beveiliging van inhoud toevoegen en de inhoud streamen (Zie [dit](media-services-protect-with-drm.md) artikel voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="d73f7-104">Azure Media Services (AMS) enables you to ingest, encode, add content protection, and stream your content (see [this](media-services-protect-with-drm.md) article for details).</span></span> <span data-ttu-id="d73f7-105">Er zijn echter alleen gebruiken AMS wilt te leveren van licenties en/of sleutels en codering, coderen en streamen met hun lokale servers-klanten.</span><span class="sxs-lookup"><span data-stu-id="d73f7-105">However, there are customers who only want to use AMS to deliver licenses and/or keys and do encoding, encrypting and streaming using their on-premises servers.</span></span> <span data-ttu-id="d73f7-106">Dit artikel wordt beschreven hoe u AMS kunt gebruiken voor het leveren van PlayReady en/of Widevine-licenties, maar de overige doen met uw on-premises servers.</span><span class="sxs-lookup"><span data-stu-id="d73f7-106">This article describes how you can use AMS to deliver PlayReady and/or Widevine licenses but do the rest with your on-premises servers.</span></span> 

## <a name="overview"></a><span data-ttu-id="d73f7-107">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d73f7-107">Overview</span></span>
<span data-ttu-id="d73f7-108">Media Services biedt een service voor het leveren van PlayReady en Widevine DRM-licenties en AES-128 sleutels.</span><span class="sxs-lookup"><span data-stu-id="d73f7-108">Media Services provides a service for delivering PlayReady and Widevine DRM licenses and AES-128 keys.</span></span> <span data-ttu-id="d73f7-109">Media Services biedt ook API's waarmee u het configureren van de rechten en beperkingen die u de runtime DRM af te dwingen wenst wanneer een gebruiker de DRM afspeelt beveiligde inhoud.</span><span class="sxs-lookup"><span data-stu-id="d73f7-109">Media Services also provides APIs that let you configure the rights and restrictions that you want for the DRM runtime to enforce when a user plays back the DRM protected content.</span></span> <span data-ttu-id="d73f7-110">Wanneer een gebruiker de beveiligde inhoud aanvraagt, wordt de spelertoepassing een licentie aangevraagd bij de AMS-licentieservice.</span><span class="sxs-lookup"><span data-stu-id="d73f7-110">When a user requests the protected content, the player application will request a license from the AMS license service.</span></span> <span data-ttu-id="d73f7-111">De AMS-licentieservice geven de licentie aan de speler (als dit is toegestaan).</span><span class="sxs-lookup"><span data-stu-id="d73f7-111">The AMS license service will issue the license to the player (if it is authorized).</span></span> <span data-ttu-id="d73f7-112">De PlayReady en Widevine-licenties bevatten de ontsleutelingssleutel die kan worden gebruikt door de clientspeler om te ontsleutelen en de inhoud streamen.</span><span class="sxs-lookup"><span data-stu-id="d73f7-112">The PlayReady and Widevine licenses contain the decryption key that can be used by the client player to decrypt and stream the content.</span></span>

<span data-ttu-id="d73f7-113">Media Services ondersteunt meerdere manieren om gebruikers die een licentie of sleutels aanvragen maken te autoriseren.</span><span class="sxs-lookup"><span data-stu-id="d73f7-113">Media Services supports multiple ways of authorizing users who make license or key requests.</span></span> <span data-ttu-id="d73f7-114">U autorisatiebeleid voor de inhoudssleutel configureren en het beleid kan een of meer beperkingen hebben: openen of tokenbeperking beperking.</span><span class="sxs-lookup"><span data-stu-id="d73f7-114">You configure the content key's authorization policy and the policy could have one or more restrictions: open or token restriction.</span></span> <span data-ttu-id="d73f7-115">Het beleid met de tokenbeperking moet vergezeld gaan van een token dat is uitgegeven door Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="d73f7-115">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="d73f7-116">Media Services ondersteunt tokens in de indeling Simple Web Tokens (SWT) en JSON Web Token (JWT)-indeling.</span><span class="sxs-lookup"><span data-stu-id="d73f7-116">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span>

<span data-ttu-id="d73f7-117">Het volgende diagram toont de belangrijkste stappen dat u moet uitvoeren met AMS PlayReady en/of Widevine-licenties te leveren, maar de rest met uw on-premises servers.</span><span class="sxs-lookup"><span data-stu-id="d73f7-117">The following diagram shows the main steps you need to take to use AMS to deliver PlayReady and/or Widevine licenses but do the rest with your on-premises servers.</span></span>

![Beveiligen met PlayReady](./media/media-services-deliver-keys-and-licenses/media-services-diagram1.png)

## <a name="download-sample"></a><span data-ttu-id="d73f7-119">Voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="d73f7-119">Download sample</span></span>
<span data-ttu-id="d73f7-120">U kunt [hier](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses) het voorbeeld downloaden dat in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="d73f7-120">You can download the sample described in this article from [here](https://github.com/Azure/media-services-dotnet-deliver-drm-licenses).</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d73f7-121">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="d73f7-121">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="d73f7-122">Stel uw ontwikkelomgeving in en vul in het bestand app.config de verbindingsinformatie in, zoals beschreven in [Media Services ontwikkelen met .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d73f7-122">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="d73f7-123">Voeg de volgende elementen toe aan **appSettings** dat in het bestand app.config is gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="d73f7-123">Add the following elements to **appSettings** defined in your app.config file:</span></span>

    <span data-ttu-id="d73f7-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span><span class="sxs-lookup"><span data-stu-id="d73f7-124"><add key="Issuer" value="http://testacs.com"/> <add key="Audience" value="urn:test"/></span></span>

## <a name="net-code-example"></a><span data-ttu-id="d73f7-125">.NET-codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="d73f7-125">.NET code example</span></span>

<span data-ttu-id="d73f7-126">Het volgende codevoorbeeld toont het maken van een algemene inhoudssleutel en PlayReady of Widevine-licentie-URL's voor overname ophalen.</span><span class="sxs-lookup"><span data-stu-id="d73f7-126">The following code example shows how to create a common content key and get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="d73f7-127">U moet de volgende soorten informatie ophalen van AMS en uw lokale server configureren: **inhoudssleutel**, **sleutel-id**, **licentie-URL voor het**.</span><span class="sxs-lookup"><span data-stu-id="d73f7-127">You need to get the following pieces of information from AMS and configure your on-premises server: **content key**, **key id**, **license acquisition URL**.</span></span> <span data-ttu-id="d73f7-128">Nadat u uw lokale server configureert, kan u streamen vanaf uw eigen streaming-server.</span><span class="sxs-lookup"><span data-stu-id="d73f7-128">Once you configure your on-premises server, you could stream from your own streaming server.</span></span> <span data-ttu-id="d73f7-129">Omdat de versleutelde gegevensstroom verwijst naar AMS licentieserver, wordt de speler een licentie aangevraagd bij de AMS.</span><span class="sxs-lookup"><span data-stu-id="d73f7-129">Since the encrypted stream points to AMS license server, your player will request a license from AMS.</span></span> <span data-ttu-id="d73f7-130">Als u tokenverificatie kiest, wordt de AMS-licentieserver valideert het token dat u via HTTPS is verzonden en (indien geldig) de licentie levert terug naar de speler.</span><span class="sxs-lookup"><span data-stu-id="d73f7-130">If you choose token authentication, the AMS license server will validate the token you sent through HTTPS and (if valid) will deliver the license back to your player.</span></span> <span data-ttu-id="d73f7-131">(Het codevoorbeeld alleen laat zien hoe u een algemene inhoudssleutel maken en PlayReady of Widevine-licentie-URL's voor overname ophalen.</span><span class="sxs-lookup"><span data-stu-id="d73f7-131">(The code example only shows how to create a common content key and  get PlayReady or Widevine license acquisition URLs.</span></span> <span data-ttu-id="d73f7-132">Als u de levering van AES-128 sleutels wilt, moet u voor het maken van een inhoudssleutel envelop en ophalen van een sleutel overname-URL en [dit](media-services-protect-with-aes128.md) artikel laat zien hoe u dit doet).</span><span class="sxs-lookup"><span data-stu-id="d73f7-132">If you want to delivery AES-128 keys, you need to create an envelope content key and get a key acquisition URL and [this](media-services-protect-with-aes128.md) article shows how to do it).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DeliverDRMLicenses
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

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                bool tokenRestriction = true;
                string tokenTemplateString = null;


                IContentKey key = CreateCommonTypeContentKey();

                // Print out the key ID and Key in base64 string format
                Console.WriteLine("Created key {0} with key value {1} ",
                    key.Id, System.Convert.ToBase64String(key.GetClearKeyValue()));

                Console.WriteLine("PlayReady License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));

                Console.WriteLine("Widevine License Key delivery URL: {0}",
                    key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine));

                if (tokenRestriction)
                    tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
                else
                    AddOpenAuthorizationPolicy(key);

                Console.WriteLine("Added authorization policy: {0}",
                    key.AuthorizationPolicyId);
                Console.WriteLine();
                Console.ReadLine();
            }

            static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
            {

                // Create ContentKeyAuthorizationPolicy with Open restrictions 
                // and create authorization policy          

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Open",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                            Requirements = null
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("",
                        ContentKeyDeliveryType.Widevine,
                        restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with no restrictions").
                            Result;


                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
                // Associate the content key authorization policy with the content key.
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;
            }

            public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
            {
                string tokenTemplateString = GenerateTokenRequirements();

                List<ContentKeyAuthorizationPolicyRestriction> restrictions =
                    new List<ContentKeyAuthorizationPolicyRestriction>
                {
                        new ContentKeyAuthorizationPolicyRestriction
                        {
                            Name = "Token Authorization Policy",
                            KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                            Requirements = tokenTemplateString,
                        }
                };

                // Configure PlayReady and Widevine license templates.
                string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

                string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

                IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.PlayReadyLicense,
                            restrictions, PlayReadyLicenseTemplate);

                IContentKeyAuthorizationPolicyOption WidevinePolicy =
                    _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                        ContentKeyDeliveryType.Widevine,
                            restrictions, WidevineLicenseTemplate);

                IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                            ContentKeyAuthorizationPolicies.
                            CreateAsync("Deliver Common Content Key with token restrictions").
                            Result;

                contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
                contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

                // Associate the content key authorization policy with the content key
                contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
                contentKey = contentKey.UpdateAsync().Result;

                return tokenTemplateString;
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

            static private string ConfigurePlayReadyLicenseTemplate()
            {
                // The following code configures PlayReady License Template using .NET classes
                // and returns the XML string.

                //The PlayReadyLicenseResponseTemplate class represents the template 
                //for the response sent back to the end user. 
                //It contains a field for a custom data string between the license server 
                //and the application (may be useful for custom app logic) 
                //as well as a list of one or more license templates.

                PlayReadyLicenseResponseTemplate responseTemplate =
                    new PlayReadyLicenseResponseTemplate();

                // The PlayReadyLicenseTemplate class represents a license template 
                // for creating PlayReady licenses
                // to be returned to the end users. 
                // It contains the data on the content key in the license 
                // and any rights or restrictions to be 
                // enforced by the PlayReady DRM runtime when using the content key.
                PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();

                // Configure whether the license is persistent 
                // (saved in persistent storage on the client) 
                // or non-persistent (only held in memory while the player is using the license).  
                licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

                // AllowTestDevices controls whether test devices can use the license or not.  
                // If true, the MinimumSecurityLevel property of the license
                // is set to 150.  If false (the default), 
                // the MinimumSecurityLevel property of the license is set to 2000.
                licenseTemplate.AllowTestDevices = true;

                // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class. 
                // It grants the user the ability to playback the content subject to the zero or more restrictions 
                // configured in the license and on the PlayRight itself (for playback specific policy). 
                // Much of the policy on the PlayRight has to do with output restrictions 
                // which control the types of outputs that the content can be played over and 
                // any restrictions that must be put in place when using a given output.
                // For example, if the DigitalVideoOnlyContentRestriction is enabled, 
                //then the DRM runtime will only allow the video to be displayed over digital outputs 
                //(analog video outputs won’t be allowed to pass the content).

                // IMPORTANT: These types of restrictions can be very powerful 
                // but can also affect the consumer experience. 
                // If the output protections are configured too restrictive, 
                // the content might be unplayable on some clients. 
                // For more information, see the PlayReady Compliance Rules document.

                // For example:
                //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

                responseTemplate.LicenseTemplates.Add(licenseTemplate);

                return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
            }


            private static string ConfigureWidevineLicenseTemplate()
            {
                var template = new WidevineMessage
                {
                    allowed_track_types = AllowedTrackTypes.SD_HD,
                    content_key_specs = new[]
                    {
                            new ContentKeySpecs
                            {
                                required_output_protection =
                                    new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                                security_level = 1,
                                track_type = "SD"
                            }
                        },
                    policy_overrides = new
                    {
                        can_play = true,
                        can_persist = true,
                        can_renew = false
                    }
                };

                string configuration = JsonConvert.SerializeObject(template);
                return configuration;
            }


            static public IContentKey CreateCommonTypeContentKey()
            {
                // Create envelope encryption content key
                Guid keyId = Guid.NewGuid();
                byte[] contentKey = GetRandomBuffer(16);

                IContentKey key = _context.ContentKeys.Create(
                                        keyId,
                                        contentKey,
                                        "ContentKey",
                                        ContentKeyType.CommonEncryption);

                return key;
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="d73f7-133">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="d73f7-133">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d73f7-134">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="d73f7-134">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d73f7-135">Zie ook</span><span class="sxs-lookup"><span data-stu-id="d73f7-135">See also</span></span>
[<span data-ttu-id="d73f7-136">PlayReady en/of Widevine Dynamic Common Encryption gebruiken</span><span class="sxs-lookup"><span data-stu-id="d73f7-136">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="d73f7-137">Met behulp van dynamische AES-128-versleuteling en Sleutellevering Service</span><span class="sxs-lookup"><span data-stu-id="d73f7-137">Using AES-128 Dynamic Encryption and Key Delivery Service</span></span>](media-services-protect-with-aes128.md)

[<span data-ttu-id="d73f7-138">Partners gebruiken om Widevine-licenties te leveren aan Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="d73f7-138">Using partners to deliver Widevine licenses to Azure Media Services</span></span>](media-services-licenses-partner-integration.md)

