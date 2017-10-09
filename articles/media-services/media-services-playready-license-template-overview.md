---
title: overzicht van aaaMedia Services PlayReady licentie-sjabloon
description: In dit onderwerp geeft een overzicht van de sjabloon van een PlayReady-licentie die tooconfigure PlayReady-licenties gebruikt.
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 5a5ba930c56f70038db204681486ebc4308199fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-playready-license-template-overview"></a>Media Services PlayReady licentie sjabloon overzicht
Azure Media Services biedt nu een service voor het leveren van Microsoft PlayReady-licenties. Wanneer Hallo eindgebruiker player (bijvoorbeeld Silverlight) probeert tooplay uw PlayReady beveiligde inhoud, een aanvraag is verzonden toohello licentie delivery service tooobtain een licentie. Als de licentieservice Hallo Hallo aanvraag goedkeurt, deze Hallo-licentie verzonden toohello client is uitgeeft en kan worden gebruikt toodecrypt en play Hallo opgegeven inhoud.

Media Services biedt ook API's waarmee u uw PlayReady-licenties te configureren. Licenties bevatten Hallo rechten en beperkingen dat u voor Hallo PlayReady DRM runtime tooenforce wilt wanneer een gebruiker tooplayback probeert beveiligde inhoud.
Hieronder volgen enkele voorbeelden van PlayReady licentiebeperkingen die u kunt opgeven:

* Hallo DateTime vanaf welke Hallo licentie geldig is.
* Hallo DateTime-waarde wanneer Hallo-licentie is verlopen. 
* Voor Hallo licentie toobe opgeslagen in de permanente opslag op Hallo-client. Permanente licenties zijn gewoonlijk gebruikte tooallow offline afspelen van Hallo-inhoud.
* Hallo minimale beveiligingsniveau dat een speler moet tooplay uw inhoud hebben. 
* Hallo uitvoer beveiligingsniveau voor Hallo uitvoer besturingselementen voor audio\video inhoud. 
* Zie voor meer informatie, Hallo uitvoer besturingselementen sectie (3.5) in Hallo [Compliantieregels PlayReady](https://www.microsoft.com/playready/licensing/compliance/) document.

> [!NOTE]
> U kunt op dit moment alleen Hallo PlayRight van Hallo PlayReady-licenties (dit recht is vereist) configureren. Hallo PlayRight geeft Hallo client Hallo mogelijkheid tooplayback Hallo inhoud. Hallo PlayRight kunt ook specifieke tooplayback beperkingen configureren. Zie voor meer informatie [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).
> 
> 

tooconfigure PlayReady-licenties met Media Services, moet u Hallo Media Services PlayReady-licentiesjabloon configureren. Hallo-sjabloon is gedefinieerd in XML.

Hallo ziet volgende voorbeeld Hallo eenvoudigste (en meest voorkomende) sjabloon waarmee een streaming standaardlicentie worden geconfigureerd. Met deze licentie uw clients kunt tooplayback zou worden uw PlayReady beveiligde inhoud.

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

Hallo-XML voldoet toohello PlayReady licentie sjabloon XML-schema is gedefinieerd in Hallo PlayReady-licentiesjabloon XML-schema-sectie.

Media Services kunt u ook een set van .NET-klassen die gebruikt tooserialized en gedeserialiseerde tooand van Hallo XML worden kan gedefinieerd. Zie voor een beschrijving van de belangrijkste klassen [Media Services .NET-klassen](media-services-playready-license-template-overview.md#classes). die zijn gebruikt tooconfigure licentie sjablonen.

Zie voor een voorbeeld van end-to-end die gebruikmaakt van .NET-tooconfigure Hallo PlayReady-licentiesjabloon klassen, [met behulp van dynamische PlayReady-versleuteling en de Service voor het leveren van licenties](media-services-protect-with-drm.md).

## <a id="classes"></a>Media Services .NET-klassen die gebruikt tooconfigure licentie sjablonen zijn
Hallo hieronder vindt u hoofdklassen .NET voor Hallo gebruikte tooconfigure Media Services PlayReady licentie sjablonen zijn. Deze klassen worden toegewezen toohello-typen gedefinieerd in [PlayReady licentie sjabloon XML-schema](media-services-playready-license-template-overview.md#schema).

Hallo [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) klasse is gebruikte tooserialize en tooand van Hallo Media Services-licentiesjabloon XML te deserialiseren.

### <a name="playreadylicenseresponsetemplate"></a>PlayReadyLicenseResponseTemplate
[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -deze klasse vertegenwoordigt het Hallo-sjabloon voor het Hallo-antwoord verzonden back toohello eindgebruiker. Het bevat een veld voor een tekenreeks met aangepaste gegevens tussen de licentieserver Hallo en Hallo-toepassing (mogelijk handig voor aangepaste app logica), evenals een lijst met een of meer licentie-sjablonen.

Dit is Hallo 'top niveau' klasse in Hallo Sjabloonhiërarchie. Wat betekent dat Hallo antwoord sjabloon een lijst met sjablonen licentie bevat en Hallo licentie sjablonen bevatten (direct of indirect) alle andere klassen die gezamenlijk Hallo sjabloon gegevens toobe geserialiseerd Hallo.

### <a name="playreadylicensetemplate"></a>PlayReadyLicenseTemplate
[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -Hallo klasse vertegenwoordigt een licentiesjabloon voor het maken van PlayReady-licenties toobe toohello eindgebruikers geretourneerd. Het Hallo-gegevens op Hallo inhoudssleutel in Hallo-licentie bevat en eventuele toobe rechten of beperkingen afgedwongen door Hallo PlayReady DRM runtime bij gebruik van Hallo inhoudssleutel.

### <a id="PlayReadyPlayRight"></a>PlayReadyPlayRight
[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -deze klasse vertegenwoordigt Hallo PlayRight van een PlayReady-licentie. Hallo gebruiker Hallo mogelijkheid tooplayback kent het Hallo inhoud onderwerp toohello nul of meer beperkingen in Hallo-licentie en op Hallo PlayRight zelf (voor een specifiek beleid afspelen) geconfigureerd. Veel van Hallo-beleid op Hallo PlayRight heeft toodo met uitvoer beperkingen die Hallo soorten uitvoer die Hallo inhoud kan worden afgespeeld via beheren en de beperkingen die in plaats moeten worden geplaatst bij gebruik van een bepaalde uitvoer. Bijvoorbeeld, als Hallo DigitalVideoOnlyContentRestriction is ingeschakeld, klikt u vervolgens Hallo worden DRM runtime mag alleen Hallo video toobe weergegeven via digitale uitvoer (analoge video-uitgangen niet mag toopass Hallo inhoud).

> [!IMPORTANT]
> Typen beperkingen kunnen zeer krachtig maar kunnen ook van invloed op Hallo consumer ervaring. Als Hallo uitvoer beveiligingen te beperkend zijn geconfigureerd, is het mogelijk dat Hallo inhoud afgespeeld op sommige clients. Zie voor meer informatie, Hallo [Compliantieregels PlayReady](https://www.microsoft.com/playready/licensing/compliance/) document.
> 
> 

Zie voor een voorbeeld van welke beveiliging ondersteunt Silverlight niveaus: [Silverlight-ondersteuning voor uitvoer beveiligingen](http://go.microsoft.com/fwlink/?LinkId=617318).

## <a id="schema"></a>PlayReady-licentie sjabloon XML-schema
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

