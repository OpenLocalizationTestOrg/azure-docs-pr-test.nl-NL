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
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a>Met behulp van Axinom toodeliver Widevine-licenties tooAzure Media Services
> [!div class="op_single_selector"]
> * [castLabs](media-services-castlabs-integration.md)
> * [Axinom](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a>Overzicht
Azure Media Services (AMS) is toegevoegd Google Widevine dynamic beveiliging (Zie [blog van Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) voor meer informatie). Bovendien Azure Media Player (AMP) is ook Widevine ondersteuning toegevoegd (Zie [AMP document](http://amp.azure.net/libs/amp/latest/docs/) voor meer informatie). Dit is een belangrijke vervullen in de streaming DASH-inhoud beveiligd met CENC met meerdere-native-DRM (PlayReady en Widevine) moderne browsers zijn uitgerust met muis en EME.

Media Services vanaf Media Services .NET SDK versie 3.5.2 hello, kunt u tooconfigure Widevine-licentiesjabloon en Widevine-licenties ophalen. U kunt ook Hallo AMS-partners toohelp u leveren met Widevine-licenties te volgen: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Dit artikel wordt beschreven hoe toointegrate en test Widevine server beheerd door Axinom licentie. In het bijzonder omvatten ze:  

* Dynamic Common Encryption configureren met multi-DRM (PlayReady en Widevine) met de bijbehorende licentie overname-URL's;
* Genereren van een JWT-token in volgorde toomeet Hallo server licentievereisten;
* Azure Media Player-app die aanschaf van licentie met JWT-token verificatie zorgt; ontwikkelt

Hallo volledige systeem en Hallo stroom van inhoud die en de belangrijkste-ID, sleutel seed, JTW token en de claims beste door het volgende diagram Hallo kan worden beschreven.

![DASH en CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a>Content Protection
Zie voor het configureren van dynamische beveiliging en belangrijke leveringsbeleid Mingfei van blog: [hoe tooconfigure Widevine-verpakking met Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).

U kunt dynamische CENC beveiliging configureren met multi-DRM voor streaming beide volgende Hallo DASH:

1. PlayReady-beveiliging voor MS Edge en IE11 die kan een token autorisatiebeperkingen hebben. Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS), zoals Azure Active Directory.
2. Widevine-beveiliging voor Chrome, kan deze tokenverificatie vereisen met token dat is uitgegeven door een andere STS. 

Zie [genereren van JWT-tokens](media-services-axinom-integration.md#jwt-token-generation) sectie voor waarom Azure Active Directory kan niet worden gebruikt als een STS voor Axinom van Widevine-licentieserver.

### <a name="considerations"></a>Overwegingen
1. U moet Hallo die axinom sleutel seed (8888000000000000000000000000000000000000) en de gegenereerde of de geselecteerde sleutel ID toogenerate Hallo inhoud sleutel opgegeven voor het configureren van de service voor het leveren van sleutel gebruiken. Licentieserver Axinom verleent alle licenties met inhoud sleutels die zijn gebaseerd op Hallo sleutel seed die geldig voor testen en productie is.
2. Hallo Widevine-licentie de URL voor het testen: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense). HTTP- en HTTS zijn toegestaan.

## <a name="azure-media-player-preparation"></a>Azure Media Player voorbereiding
AMP v1.4.0 ondersteunt het afspelen van inhoud van het AMS die dynamisch wordt verpakt met PlayReady en Widevine DRM.
Als de licentieserver Widevine tokenverificatie niet vereist, zijn er geen extra moet u toodo tootest een streepje inhoud beveiligd door Widevine. Voor een voorbeeld Hallo AMP team biedt een eenvoudige [voorbeeld](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), waar u deze in de werkt rand en IE11 met PlayReady en Chrome met Widevine kunt zien.
Hallo Widevine-licentie verstrekt door Axinom JWT-token is verificatie vereist. Hallo JWT-token moet toobe verzonden met licentieaanvraag via een HTTP-header 'X AxDRM bericht'. Hiertoe moet u tooadd Hallo javascript in Hallo webpagina's die als host fungeert AMP voordat instelling Hallo bron te volgen:

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

Hallo rest AMP code is standaard AMP API zoals in het document AMP [hier](http://amp.azure.net/libs/amp/latest/docs/).

Houd er rekening mee dat Hallo hierboven javascript voor instelling aangepaste autorisatie-header is nog steeds een korte termijn benadering voordat Hallo officiële benadering van de lange termijn in AMP wordt vrijgegeven.

## <a name="jwt-token-generation"></a>Genereren van JWT-tokens
Axinom Widevine-licentie voor het testen van JWT-token is verificatie vereist. Bovendien is een van de claims Hallo in Hallo JWT-token van een type complexe object in plaats van een primitief gegevenstype.

Azure AD kunt helaas alleen JWT-tokens uitgeven met primitieve typen. Op deze manier kunt .NET Framework-API (System.IdentityModel.Tokens.SecurityTokenHandler en JwtPayload) u alleen tooinput complexe objecttype als claims. Hallo claims zijn echter nog steeds geserialiseerd als tekenreeks. Daarom niet we een Hallo twee gebruiken voor genereren Hallo JWT-token voor Widevine-licentie-aanvraag.

John Sheehan van [JWT Nuget-pakket](https://www.nuget.org/packages/JWT) voldoet aan de behoeften Hallo zodat we toouse gaan deze Nuget-pakket.

Hieronder vindt u Hallo code voor het genereren van JWT-token met Hallo nodig claims door de server voor Axinom Widevine-licentie vereist voor het testen:

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

Axinom Widevine-licentieserver

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a>Overwegingen
1. Hoewel AMS PlayReady-service voor het leveren van licentie is vereist ' Bearer = "geen verificatietoken verdergaat Axinom Widevine-licentieserver gebruikt deze niet.
2. Hallo Axinom communicatie sleutel wordt gebruikt als de handtekeningsleutel. Houd er rekening mee dat Hallo-sleutel is een hexadecimale tekenreeks, maar deze moet worden behandeld als een reeks bytes niet naar een tekenreeks als codering. Dit wordt bereikt door Hallo methode ConvertHexStringToByteArray.

## <a name="retrieving-key-id"></a>Bij het ophalen van sleutel-ID
U mogelijk opgevallen dat in Hallo-code voor het genereren van een JWT-token, sleutel-ID is vereist. Omdat Hallo JWT-token toobe gereed is moet voordat het laden van het AMP, in volgorde van ID behoeften toobe opgehaald in toogenerate JWT-token.

Uiteraard er zijn meerdere manieren tooget houdt van sleutel-id. Bijvoorbeeld, een kan opslaan ID sleutel samen met de metagegevens van inhoud in een database. Of u kunt ophalen sleutel-ID van het streepje MPD (beschrijving Media presentatie)-bestand. Hallo-code hieronder is voor de laatste Hallo.

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

## <a name="summary"></a>Samenvatting
Met de meest recente toevoeging van Widevine-ondersteuning in Azure Media Services Content Protection zowel Azure Media Player we kunnen tooimplement streaming van DASH + meerdere native DRM (PlayReady en Widevine) met zowel PlayReady-licentie-service in AMS en Widevine-licentie de server van Axinom voor Hallo moderne browsers te volgen:

* Chrome
* Microsoft Edge op Windows 10
* IE 11 op Windows 8.1 en Windows 10
* Zowel Firefox (Desktop) en Safari op Mac (geen iOS) worden ook ondersteund via Silverlight en dezelfde URL met Azure Media Player Hallo

Hallo zijn volgende parameters vereist in Hallo Mini-oplossing van Axinom Widevine-licentieserver. Met uitzondering van sleutel-ID, Hallo rest van de parameters worden geleverd door Axinom op basis van hun installatie Widevine-server.

| Parameter | Hoe deze wordt gebruikt |
| --- | --- |
| Communicatie ID sleutel |Moet worden opgenomen als waarde van Hallo claim 'com_key_id' in de JWT-token (Zie [dit](media-services-axinom-integration.md#jwt-token-generation) sectie). |
| Communicatie-sleutel |Moet worden gebruikt als Hallo ondertekeningssleutel van JWT-token (Zie [dit](media-services-axinom-integration.md#jwt-token-generation) sectie). |
| Sleutel seed |Moet worden gebruikt toogenerate inhoudssleutel met een opgegeven inhoud ID sleutel (Zie [dit](media-services-axinom-integration.md#content-protection) sectie). |
| URL voor Widevine-licentie |Moet worden gebruikt bij het configureren van het leveringsbeleid voor Assets voor DASH streaming (Zie [dit](media-services-axinom-integration.md#content-protection) sectie). |
| Inhoud sleutel-ID |Moet worden opgenomen als onderdeel van Hallo-waarde van de claim recht bericht van het JWT-token (Zie [dit](media-services-axinom-integration.md#jwt-token-generation) sectie). |

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Bevestigingen
Willen we graag tooacknowledge Hallo personen die hebben bijgedragen tot de verwezenlijking van dit document te volgen: Kristjan Jõgi van Axinom Mingfei Yan en Amit Rajput.

