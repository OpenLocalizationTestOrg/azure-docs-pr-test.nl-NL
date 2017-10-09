---
title: overzicht van de sjabloon aaaWidevine licentie | Microsoft Docs
description: In dit onderwerp geeft een overzicht van de sjabloon van een Widevine-licentie die tooconfigure Widevine-licenties gebruikt.
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 67a6ae38cf3d3c21e1b7282aef15f79b21776414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="widevine-license-template-overview"></a>Overzicht van de sjabloon voor Widevine-licentie
## <a name="overview"></a>Overzicht
Azure Media Services kunt u nu tooconfigure en aanvraag Widevine-licenties. Wanneer Hallo eindgebruiker player tooplay probeert is de inhoud beveiligd Widevine, een aanvraag verzonden toohello licentie delivery service tooobtain een licentie. Als de licentieservice Hallo Hallo aanvraag goedkeurt, deze Hallo-licentie verzonden toohello client is uitgeeft en kan worden gebruikt toodecrypt en play Hallo opgegeven inhoud.

Widevine-licentie-aanvraag is opgemaakt als een JSON-bericht.  

>[!NOTE]
> U kunt toocreate een leeg bericht met geen waarden alleen '{}' en een licentiesjabloon wordt gemaakt met alle standaardwaarden. Hallo standaard werkt voor de meeste gevallen. Bijvoorbeeld: voor op basis van MS licentie levering scenario's die standaard moeten zijn. Als u tooset Hallo 'provider' en 'content_id' waarden hoeft, moet een provider van Google Widevine referenties overeenkomen.

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a>JSON-bericht
| Naam | Waarde | Beschrijving |
| --- | --- | --- |
| nettolading |Base64-gecodeerde tekenreeks |Hallo licentie-aanvraag is verzonden door een client. |
| content_id |Base64-gecodeerde tekenreeks |ID gebruikt tooderive KeyId(s) en inhoud sleutel (s) voor elke content_key_specs.track_type. |
| Provider |Tekenreeks |Gebruikte toolook van inhoud sleutel en het beleid. Als de sleutellevering MS wordt gebruikt voor de levering van Widevine-licentie, wordt deze parameter wordt genegeerd. |
| Naam_van_beleid |Tekenreeks |Naam van een eerder geregistreerde beleid. Optioneel |
| allowed_track_types |Enum |SD_ONLY of SD_HD. Bepaalt welke inhoud sleutels moeten worden opgenomen in een licentie |
| content_key_specs |matrix van JSON-structuren, Zie **inhoud sleutel specificaties** hieronder |Een fijnere geslaagde besturingselement op welke inhoud tooreturn sleutels. Zie inhoud sleutel Spec hieronder voor meer informatie.  Er kan slechts één van allowed_track_types en content_key_specs worden opgegeven. |
| use_policy_overrides_exclusively |Booleaanse waarde. waar of ONWAAR |Gebruik beleid kenmerken opgegeven door policy_overrides en laat alle eerder opgeslagen beleid. |
| policy_overrides |JSON-structuur, Zie **overschreven** hieronder |Beleidsinstellingen voor deze licentie.  In de gebeurtenis Hallo dit activum heeft een vooraf gedefinieerd beleid, deze opgegeven waarden worden gebruikt. |
| session_init |JSON-structuur, Zie **initialisatie van de sessie** hieronder |Optionele gegevens doorgegeven toolicense. |
| parse_only |Booleaanse waarde. waar of ONWAAR |Hallo licentieaanvraag wordt geparseerd, maar er is geen licentie wordt verleend. Waarden formulier Hallo licentieaanvraag worden echter geretourneerd in antwoord Hallo. |

## <a name="content-key-specs"></a>Inhoudssleutel specificaties
Als een bestaande beleid bestaat, is er geen noodzaak toospecify van Hallo in Hallo inhoud sleutel Spec waarden.  gebruikte toodetermine Hallo uitvoer beveiliging zoals HDCP en CGMS zijn Hallo vooraf bestaande beleid die zijn gekoppeld aan deze inhoud.  Als een bestaande beleid is niet geregistreerd bij Hallo Widevine-licentieserver, kan inhoudsprovider Hallo Hallo waarden invoeren in Hallo licentieaanvraag.   

Elke content_key_specs moet worden opgegeven voor alle nummers, ongeacht Hallo optie use_policy_overrides_exclusively. 

| Naam | Waarde | Beschrijving |
| --- | --- | --- |
| content_key_specs. track_type |Tekenreeks |Een typenaam bijhouden. Als content_key_specs is opgegeven in de licentieaanvraag hello, zorg ervoor dat toospecify die alle bijhouden typen expliciet. Fout toodo dus leidt tot mislukte tooplayback afgelopen 10 seconden. |
| content_key_specs  <br/> security_level |UInt32 |Hiermee definieert u robuustheid clientvereisten voor afspelen. <br/> 1 - softwarematige whitebox crypto is vereist. <br/> 2 - crypto-software en een verborgen decoder is vereist. <br/> 3 - Hallo materiaal- en cryptografie sleutelbewerkingen moeten worden uitgevoerd binnen een hardware back-ups vertrouwde uitvoeringsomgeving. <br/> 4 - Hallo crypto en decodering van inhoud moet worden uitgevoerd binnen een hardware back-ups vertrouwde uitvoeringsomgeving.  <br/> 5 - Hallo crypto, decoderen en alle verwerkingstijd Hallo media (gecomprimeerde en ongecomprimeerde) moet worden verwerkt binnen een hardware back-ups vertrouwde uitvoeringsomgeving. |
| content_key_specs <br/> required_output_protection.hDC |String - een van: HDCP_NONE, HDCP_V1, HDCP_V2 |Hiermee wordt aangegeven of HDCP nodig is |
| content_key_specs <br/>sleutel |Base64 <br/>gecodeerde tekenreeks |Sleutel toouse inhoud voor dit nummer. Indien opgegeven, Hallo track_type of key_id is vereist.  Deze optie kunt Hallo inhoudsprovider tooinject hello inhoudssleutel voor dit nummer in plaats van de licentieserver Widevine genereren of het opzoeken van een sleutel te laten. |
| content_key_specs.key_id |Met base64 gecodeerde tekenreeks binaire, 16 bytes |De unieke id voor Hallo-sleutel. |

## <a name="policy-overrides"></a>Beleid negeren
| Naam | Waarde | Beschrijving |
| --- | --- | --- |
| policy_overrides. can_play |Booleaanse waarde. waar of ONWAAR |Hiermee wordt aangegeven dat afspelen Hallo inhoud is toegestaan. Standaard is ingesteld op false. |
| policy_overrides. can_persist |Booleaanse waarde. waar of ONWAAR |Betekent dit dat die licentie Hallo mogelijk persistente toonon-vluchtige opslag voor offlinegebruik. Standaard is ingesteld op false. |
| policy_overrides. can_renew |Booleaanse waarde waar of ONWAAR |Hiermee wordt aangegeven dat de verlenging van deze licentie is toegestaan. Indien waar, kan de duur van Hallo licentie Hallo worden uitgebreid door heartbeat. Standaard is ingesteld op false. |
| policy_overrides. license_duration_seconds |Int64 |Hiermee wordt aangegeven Hallo tijdvenster voor deze specifieke licentiegroep. Een waarde van 0 geeft aan dat er geen limiet toohello duur. De standaardwaarde is 0. |
| policy_overrides. rental_duration_seconds |Int64 |Geeft aan het tijdvenster Hallo tijdens het afspelen is toegestaan. Een waarde van 0 geeft aan dat er geen limiet toohello duur. De standaardwaarde is 0. |
| policy_overrides. playback_duration_seconds |Int64 |Hallo venster tijd wanneer het afspelen is gestart binnen Hallo licentie duur weer te geven. Een waarde van 0 geeft aan dat er geen limiet toohello duur. De standaardwaarde is 0. |
| policy_overrides. renewal_server_url |Tekenreeks |Alle heartbeat (vernieuwing) aanvragen voor deze licentie is gericht toohello URL opgegeven. Dit veld wordt alleen gebruikt als can_renew ingesteld op true is. |
| policy_overrides. renewal_delay_seconds |Int64 |Hoeveel seconden na license_start_time, voordat de vernieuwing wordt eerst geprobeerd. Dit veld wordt alleen gebruikt als can_renew ingesteld op true is. De standaardwaarde is 0 |
| policy_overrides. renewal_retry_interval_seconds |Int64 |Hiermee geeft u Hallo vertraging in seconden tussen opeenvolgende licentie-verlengingsaanvragen in geval van storing. Dit veld wordt alleen gebruikt als can_renew ingesteld op true is. |
| policy_overrides. renewal_recovery_duration_seconds |Int64 |Hallo-venster tijdsduur waarin afspelen toocontinue tijdens het vernieuwen is toegestaan is geprobeerde, nog mislukt vanwege problemen met de licentieserver Hallo toobackend. Een waarde van 0 geeft aan dat er geen limiet toohello duur. Dit veld wordt alleen gebruikt als can_renew ingesteld op true is. |
| policy_overrides. renew_with_usage |Booleaanse waarde waar of ONWAAR |Hiermee wordt aangegeven dat die licentie Hallo toegezonden voor verlenging wanneer gebruik wordt gestart. Dit veld wordt alleen gebruikt als can_renew ingesteld op true is. |

## <a name="session-initialization"></a>De initialisatie-sessie
| Naam | Waarde | Beschrijving |
| --- | --- | --- |
| provider_session_token |Base64-gecodeerde tekenreeks |Dit sessietoken wordt doorgegeven in Hallo-licentie en in daaropvolgende vernieuwingen aanwezig.  Hallo sessietoken bewaard niet afgezien van sessies. |
| provider_client_token |Base64-gecodeerde tekenreeks |Client token toosend weer antwoord Hallo-licentie.  Als de licentieaanvraag Hallo-clienttoken van een bevat, wordt deze waarde wordt genegeerd. Hallo clienttoken bewaard buiten licentie-sessies. |
| override_provider_client_token |Booleaanse waarde. waar of ONWAAR |Als onwaar heeft en Hallo licentieaanvraag-clienttoken van een bevat, gebruikt u Hallo-token van de aanvraag Hallo zelfs als een clienttoken in deze structuur is opgegeven.  Indien waar, altijd Hallo-token opgegeven in deze structuur te gebruiken. |

## <a name="configure-your-widevine-licenses-using-net-types"></a>Configureren van uw .NET-typen met Widevine-licenties
Media Services biedt .NET API's waarmee u uw Widevine-licenties te configureren. 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a>Klassen, zoals gedefinieerd in Hallo Media Services .NET SDK
Hallo volgen Hallo definities van de volgende typen.

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld wordt getoond hoe toouse .NET API's tooconfigure een eenvoudige Widevine-licentie.

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
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


## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zie ook
[PlayReady en/of Widevine Dynamic Common Encryption gebruiken](media-services-protect-with-drm.md)

