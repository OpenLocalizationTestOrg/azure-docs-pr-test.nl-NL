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
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="c8ce2-103">Media Services PlayReady licentie sjabloon overzicht</span><span class="sxs-lookup"><span data-stu-id="c8ce2-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="c8ce2-104">Azure Media Services biedt nu een service voor het leveren van Microsoft PlayReady-licenties.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="c8ce2-105">Wanneer Hallo eindgebruiker player (bijvoorbeeld Silverlight) probeert tooplay uw PlayReady beveiligde inhoud, een aanvraag is verzonden toohello licentie delivery service tooobtain een licentie.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-105">When hello end user player (for example, Silverlight) tries tooplay your PlayReady protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="c8ce2-106">Als de licentieservice Hallo Hallo aanvraag goedkeurt, deze Hallo-licentie verzonden toohello client is uitgeeft en kan worden gebruikt toodecrypt en play Hallo opgegeven inhoud.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-106">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="c8ce2-107">Media Services biedt ook API's waarmee u uw PlayReady-licenties te configureren.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="c8ce2-108">Licenties bevatten Hallo rechten en beperkingen dat u voor Hallo PlayReady DRM runtime tooenforce wilt wanneer een gebruiker tooplayback probeert beveiligde inhoud.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-108">Licenses contain hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplayback protected content.</span></span>
<span data-ttu-id="c8ce2-109">Hieronder volgen enkele voorbeelden van PlayReady licentiebeperkingen die u kunt opgeven:</span><span class="sxs-lookup"><span data-stu-id="c8ce2-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="c8ce2-110">Hallo DateTime vanaf welke Hallo licentie geldig is.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-110">hello DateTime from which hello license is valid.</span></span>
* <span data-ttu-id="c8ce2-111">Hallo DateTime-waarde wanneer Hallo-licentie is verlopen.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-111">hello DateTime value when hello license expires.</span></span> 
* <span data-ttu-id="c8ce2-112">Voor Hallo licentie toobe opgeslagen in de permanente opslag op Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-112">For hello license toobe saved in persistent storage on hello client.</span></span> <span data-ttu-id="c8ce2-113">Permanente licenties zijn gewoonlijk gebruikte tooallow offline afspelen van Hallo-inhoud.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-113">Persistent licenses are typically used tooallow offline playback of hello content.</span></span>
* <span data-ttu-id="c8ce2-114">Hallo minimale beveiligingsniveau dat een speler moet tooplay uw inhoud hebben.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-114">hello minimum security level that a player must have tooplay your content.</span></span> 
* <span data-ttu-id="c8ce2-115">Hallo uitvoer beveiligingsniveau voor Hallo uitvoer besturingselementen voor audio\video inhoud.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-115">hello output protection level for hello output controls for audio\video content.</span></span> 
* <span data-ttu-id="c8ce2-116">Zie voor meer informatie, Hallo uitvoer besturingselementen sectie (3.5) in Hallo [Compliantieregels PlayReady](https://www.microsoft.com/playready/licensing/compliance/) document.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-116">For more information, see hello Output Controls section (3.5) in hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="c8ce2-117">U kunt op dit moment alleen Hallo PlayRight van Hallo PlayReady-licenties (dit recht is vereist) configureren.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-117">Currently, you can only configure hello PlayRight of hello PlayReady license (this right is required).</span></span> <span data-ttu-id="c8ce2-118">Hallo PlayRight geeft Hallo client Hallo mogelijkheid tooplayback Hallo inhoud.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-118">hello PlayRight gives hello client hello ability tooplayback hello content.</span></span> <span data-ttu-id="c8ce2-119">Hallo PlayRight kunt ook specifieke tooplayback beperkingen configureren.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-119">hello PlayRight also allows configuring restrictions specific tooplayback.</span></span> <span data-ttu-id="c8ce2-120">Zie voor meer informatie [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="c8ce2-121">tooconfigure PlayReady-licenties met Media Services, moet u Hallo Media Services PlayReady-licentiesjabloon configureren.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-121">tooconfigure PlayReady licenses using Media Services, you must configure hello Media Services PlayReady license template.</span></span> <span data-ttu-id="c8ce2-122">Hallo-sjabloon is gedefinieerd in XML.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-122">hello template is defined in XML.</span></span>

<span data-ttu-id="c8ce2-123">Hallo ziet volgende voorbeeld Hallo eenvoudigste (en meest voorkomende) sjabloon waarmee een streaming standaardlicentie worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-123">hello following example shows hello simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="c8ce2-124">Met deze licentie uw clients kunt tooplayback zou worden uw PlayReady beveiligde inhoud.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-124">With this license, your clients would be able tooplayback your PlayReady protected content.</span></span>

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

<span data-ttu-id="c8ce2-125">Hallo-XML voldoet toohello PlayReady licentie sjabloon XML-schema is gedefinieerd in Hallo PlayReady-licentiesjabloon XML-schema-sectie.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-125">hello XML conforms toohello PlayReady license template XML schema defined in hello PlayReady license template XML schema section.</span></span>

<span data-ttu-id="c8ce2-126">Media Services kunt u ook een set van .NET-klassen die gebruikt tooserialized en gedeserialiseerde tooand van Hallo XML worden kan gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-126">Media Services also defines a set of .NET classes that could be used tooserialized and deserialized tooand from hello XML.</span></span> <span data-ttu-id="c8ce2-127">Zie voor een beschrijving van de belangrijkste klassen [Media Services .NET-klassen](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="c8ce2-128">die zijn gebruikt tooconfigure licentie sjablonen.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-128">that are used tooconfigure license templates.</span></span>

<span data-ttu-id="c8ce2-129">Zie voor een voorbeeld van end-to-end die gebruikmaakt van .NET-tooconfigure Hallo PlayReady-licentiesjabloon klassen, [met behulp van dynamische PlayReady-versleuteling en de Service voor het leveren van licenties](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-129">For an end-to-end example that uses .NET classes tooconfigure hello PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="c8ce2-130"><a id="classes"></a>Media Services .NET-klassen die gebruikt tooconfigure licentie sjablonen zijn</span><span class="sxs-lookup"><span data-stu-id="c8ce2-130"><a id="classes"></a>Media Services .NET classes that are used tooconfigure license templates</span></span>
<span data-ttu-id="c8ce2-131">Hallo hieronder vindt u hoofdklassen .NET voor Hallo gebruikte tooconfigure Media Services PlayReady licentie sjablonen zijn.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-131">hello following are hello main .NET classes are used tooconfigure Media Services PlayReady license templates.</span></span> <span data-ttu-id="c8ce2-132">Deze klassen worden toegewezen toohello-typen gedefinieerd in [PlayReady licentie sjabloon XML-schema](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-132">These classes map toohello types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="c8ce2-133">Hallo [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) klasse is gebruikte tooserialize en tooand van Hallo Media Services-licentiesjabloon XML te deserialiseren.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used tooserialize and deserialize tooand from hello Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="c8ce2-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="c8ce2-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="c8ce2-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -deze klasse vertegenwoordigt het Hallo-sjabloon voor het Hallo-antwoord verzonden back toohello eindgebruiker.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents hello template for hello response sent back toohello end user.</span></span> <span data-ttu-id="c8ce2-136">Het bevat een veld voor een tekenreeks met aangepaste gegevens tussen de licentieserver Hallo en Hallo-toepassing (mogelijk handig voor aangepaste app logica), evenals een lijst met een of meer licentie-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-136">It contains a field for a custom data string between hello license server and hello application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="c8ce2-137">Dit is Hallo 'top niveau' klasse in Hallo Sjabloonhiërarchie.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-137">This is hello “top level” class in hello template hierarchy.</span></span> <span data-ttu-id="c8ce2-138">Wat betekent dat Hallo antwoord sjabloon een lijst met sjablonen licentie bevat en Hallo licentie sjablonen bevatten (direct of indirect) alle andere klassen die gezamenlijk Hallo sjabloon gegevens toobe geserialiseerd Hallo.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-138">Meaning that hello response template includes a list of license templates and hello license templates include (directly or indirectly) all of hello other classes that make up hello template data toobe serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="c8ce2-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="c8ce2-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="c8ce2-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -Hallo klasse vertegenwoordigt een licentiesjabloon voor het maken van PlayReady-licenties toobe toohello eindgebruikers geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - hello class represents a license template for creating PlayReady licenses toobe returned toohello end users.</span></span> <span data-ttu-id="c8ce2-141">Het Hallo-gegevens op Hallo inhoudssleutel in Hallo-licentie bevat en eventuele toobe rechten of beperkingen afgedwongen door Hallo PlayReady DRM runtime bij gebruik van Hallo inhoudssleutel.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-141">It contains hello data on hello content key in hello license and any rights or restrictions toobe enforced by hello PlayReady DRM runtime when using hello content key.</span></span>

### <span data-ttu-id="c8ce2-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="c8ce2-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="c8ce2-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -deze klasse vertegenwoordigt Hallo PlayRight van een PlayReady-licentie.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents hello PlayRight of a PlayReady license.</span></span> <span data-ttu-id="c8ce2-144">Hallo gebruiker Hallo mogelijkheid tooplayback kent het Hallo inhoud onderwerp toohello nul of meer beperkingen in Hallo-licentie en op Hallo PlayRight zelf (voor een specifiek beleid afspelen) geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-144">It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions configured in hello license and on hello PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="c8ce2-145">Veel van Hallo-beleid op Hallo PlayRight heeft toodo met uitvoer beperkingen die Hallo soorten uitvoer die Hallo inhoud kan worden afgespeeld via beheren en de beperkingen die in plaats moeten worden geplaatst bij gebruik van een bepaalde uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-145">Much of hello policy on hello PlayRight has toodo with output restrictions which control hello types of outputs that hello content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="c8ce2-146">Bijvoorbeeld, als Hallo DigitalVideoOnlyContentRestriction is ingeschakeld, klikt u vervolgens Hallo worden DRM runtime mag alleen Hallo video toobe weergegeven via digitale uitvoer (analoge video-uitgangen niet mag toopass Hallo inhoud).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-146">For example, if hello DigitalVideoOnlyContentRestriction is enabled, then hello DRM runtime will only allow hello video toobe displayed over digital outputs (analog video outputs won’t be allowed toopass hello content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8ce2-147">Typen beperkingen kunnen zeer krachtig maar kunnen ook van invloed op Hallo consumer ervaring.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-147">These types of restrictions can be very powerful but can also affect hello consumer experience.</span></span> <span data-ttu-id="c8ce2-148">Als Hallo uitvoer beveiligingen te beperkend zijn geconfigureerd, is het mogelijk dat Hallo inhoud afgespeeld op sommige clients.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-148">If hello output protections are configured too restrictive, hello content might be unplayable on some clients.</span></span> <span data-ttu-id="c8ce2-149">Zie voor meer informatie, Hallo [Compliantieregels PlayReady](https://www.microsoft.com/playready/licensing/compliance/) document.</span><span class="sxs-lookup"><span data-stu-id="c8ce2-149">For more information, see hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="c8ce2-150">Zie voor een voorbeeld van welke beveiliging ondersteunt Silverlight niveaus: [Silverlight-ondersteuning voor uitvoer beveiligingen](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="c8ce2-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="c8ce2-151"><a id="schema"></a>PlayReady-licentie sjabloon XML-schema</span><span class="sxs-lookup"><span data-stu-id="c8ce2-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="c8ce2-152">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="c8ce2-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c8ce2-153">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="c8ce2-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

