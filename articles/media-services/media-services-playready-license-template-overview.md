---
title: Media Services PlayReady licentie sjabloon overzicht
description: In dit onderwerp geeft een overzicht van een PlayReady-licentie-sjabloon die wordt gebruikt voor het configureren van PlayReady-licenties.
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
ms.openlocfilehash: be19f616e36916655390cd05e738e93c08dcdf68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="ef642-103">Media Services PlayReady licentie sjabloon overzicht</span><span class="sxs-lookup"><span data-stu-id="ef642-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="ef642-104">Azure Media Services biedt nu een service voor het leveren van Microsoft PlayReady-licenties.</span><span class="sxs-lookup"><span data-stu-id="ef642-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="ef642-105">Wanneer de eindgebruiker speler (bijvoorbeeld Silverlight), probeert uw PlayReady beveiligde inhoud af te spelen, wordt een aanvraag verzonden naar de service voor het leveren van licenties voor het verkrijgen van een licentie.</span><span class="sxs-lookup"><span data-stu-id="ef642-105">When the end user player (for example, Silverlight) tries to play your PlayReady protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="ef642-106">Als de licentieservice de aanvraag goedkeurt, moet deze de licentie die is verzonden naar de client en kan worden gebruikt om te ontsleutelen en de inhoud van de opgegeven spelen uitgeeft.</span><span class="sxs-lookup"><span data-stu-id="ef642-106">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="ef642-107">Media Services biedt ook API's waarmee u uw PlayReady-licenties te configureren.</span><span class="sxs-lookup"><span data-stu-id="ef642-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="ef642-108">Licenties bevat rechten en beperkingen die u voor de runtime PlayReady DRM afdwingen wilt wanneer een gebruiker te afspelen beveiligde inhoud probeert.</span><span class="sxs-lookup"><span data-stu-id="ef642-108">Licenses contain the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to playback protected content.</span></span>
<span data-ttu-id="ef642-109">Hieronder volgen enkele voorbeelden van PlayReady licentiebeperkingen die u kunt opgeven:</span><span class="sxs-lookup"><span data-stu-id="ef642-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="ef642-110">De datum/tijd van waaruit de licentie geldig is.</span><span class="sxs-lookup"><span data-stu-id="ef642-110">The DateTime from which the license is valid.</span></span>
* <span data-ttu-id="ef642-111">De DateTime-waarde wanneer de licentie is verlopen.</span><span class="sxs-lookup"><span data-stu-id="ef642-111">The DateTime value when the license expires.</span></span> 
* <span data-ttu-id="ef642-112">Voor de licentie op de client worden opgeslagen in de permanente opslag.</span><span class="sxs-lookup"><span data-stu-id="ef642-112">For the license to be saved in persistent storage on the client.</span></span> <span data-ttu-id="ef642-113">Permanente licenties worden meestal gebruikt voor het toestaan van offline afspelen van de inhoud.</span><span class="sxs-lookup"><span data-stu-id="ef642-113">Persistent licenses are typically used to allow offline playback of the content.</span></span>
* <span data-ttu-id="ef642-114">Het minimale beveiligingsniveau dat een speler hebben moet tot uw inhoud afspelen.</span><span class="sxs-lookup"><span data-stu-id="ef642-114">The minimum security level that a player must have to play your content.</span></span> 
* <span data-ttu-id="ef642-115">Het beveiligingsniveau voor de uitvoer van de uitvoer-besturingselementen voor audio\video inhoud.</span><span class="sxs-lookup"><span data-stu-id="ef642-115">The output protection level for the output controls for audio\video content.</span></span> 
* <span data-ttu-id="ef642-116">Zie voor meer informatie de sectie uitvoer-besturingselementen (3.5) in de [Compliantieregels PlayReady](https://www.microsoft.com/playready/licensing/compliance/) document.</span><span class="sxs-lookup"><span data-stu-id="ef642-116">For more information, see the Output Controls section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="ef642-117">Op dit moment kunt u alleen de PlayRight van de PlayReady-licenties (dit recht is vereist) configureren.</span><span class="sxs-lookup"><span data-stu-id="ef642-117">Currently, you can only configure the PlayRight of the PlayReady license (this right is required).</span></span> <span data-ttu-id="ef642-118">De PlayRight geeft de client de mogelijkheid voor het afspelen van de inhoud.</span><span class="sxs-lookup"><span data-stu-id="ef642-118">The PlayRight gives the client the ability to playback the content.</span></span> <span data-ttu-id="ef642-119">De PlayRight kunt ook beperkingen die specifiek zijn voor het afspelen te configureren.</span><span class="sxs-lookup"><span data-stu-id="ef642-119">The PlayRight also allows configuring restrictions specific to playback.</span></span> <span data-ttu-id="ef642-120">Zie voor meer informatie [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="ef642-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="ef642-121">PlayReady-licenties met Media Services configureren, moet u de Media Services PlayReady-licentiesjabloon configureren.</span><span class="sxs-lookup"><span data-stu-id="ef642-121">To configure PlayReady licenses using Media Services, you must configure the Media Services PlayReady license template.</span></span> <span data-ttu-id="ef642-122">De sjabloon is gedefinieerd in XML.</span><span class="sxs-lookup"><span data-stu-id="ef642-122">The template is defined in XML.</span></span>

<span data-ttu-id="ef642-123">Het volgende voorbeeld ziet de sjabloon eenvoudigste (en meest voorkomende) die een streaming standaardlicentie configureert.</span><span class="sxs-lookup"><span data-stu-id="ef642-123">The following example shows the simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="ef642-124">Met deze licentie uw clients zou kunnen afspelen uw PlayReady beveiligde inhoud.</span><span class="sxs-lookup"><span data-stu-id="ef642-124">With this license, your clients would be able to playback your PlayReady protected content.</span></span>

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

<span data-ttu-id="ef642-125">Het XML-bestand voldoet aan de PlayReady licentie sjabloon XML-schema gedefinieerd in de sjabloon van PlayReady licentie sectie XML-schema.</span><span class="sxs-lookup"><span data-stu-id="ef642-125">The XML conforms to the PlayReady license template XML schema defined in the PlayReady license template XML schema section.</span></span>

<span data-ttu-id="ef642-126">Media Services definieert ook een set van .NET-klassen die kunnen worden gebruikt voor geserialiseerd en gedeserialiseerd naar en van het XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="ef642-126">Media Services also defines a set of .NET classes that could be used to serialized and deserialized to and from the XML.</span></span> <span data-ttu-id="ef642-127">Zie voor een beschrijving van de belangrijkste klassen [Media Services .NET-klassen](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="ef642-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="ef642-128">die worden gebruikt voor het configureren van de licentie-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ef642-128">that are used to configure license templates.</span></span>

<span data-ttu-id="ef642-129">Zie voor een voorbeeld van end-to-end die gebruikmaakt van .NET-klassen voor het configureren van de sjabloon PlayReady-licenties [met behulp van dynamische PlayReady-versleuteling en de Service voor het leveren van licenties](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="ef642-129">For an end-to-end example that uses .NET classes to configure the PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="ef642-130"><a id="classes"></a>Media Services .NET-klassen die worden gebruikt voor het licentie-sjablonen configureren</span><span class="sxs-lookup"><span data-stu-id="ef642-130"><a id="classes"></a>Media Services .NET classes that are used to configure license templates</span></span>
<span data-ttu-id="ef642-131">Hier volgen dat de belangrijkste .NET-klassen worden gebruikt voor het configureren van Media Services PlayReady licentie sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ef642-131">The following are the main .NET classes are used to configure Media Services PlayReady license templates.</span></span> <span data-ttu-id="ef642-132">Deze klassen worden toegewezen aan de typen gedefinieerd in [PlayReady licentie sjabloon XML-schema](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="ef642-132">These classes map to the types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="ef642-133">De [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) klasse wordt gebruikt voor het serialiseren en deserialiseren van en naar de Media Services-licentiesjabloon XML.</span><span class="sxs-lookup"><span data-stu-id="ef642-133">The [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used to serialize and deserialize to and from the Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="ef642-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="ef642-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="ef642-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -deze klasse vertegenwoordigt de sjabloon voor het antwoord terug naar de eindgebruiker wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="ef642-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents the template for the response sent back to the end user.</span></span> <span data-ttu-id="ef642-136">Het bevat een veld voor een tekenreeks met aangepaste gegevens tussen de licentieserver en de toepassing (mogelijk handig voor aangepaste app logica), evenals een lijst met een of meer licentie-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ef642-136">It contains a field for a custom data string between the license server and the application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="ef642-137">Dit is de klasse 'hoofdniveau' in de Sjabloonhiërarchie.</span><span class="sxs-lookup"><span data-stu-id="ef642-137">This is the “top level” class in the template hierarchy.</span></span> <span data-ttu-id="ef642-138">Wat betekent dat de sjabloon antwoord een lijst met sjablonen licentie bevat en de licentie-sjablonen bevatten (direct of indirect) alle klassen waaruit de sjabloongegevens moet worden geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="ef642-138">Meaning that the response template includes a list of license templates and the license templates include (directly or indirectly) all of the other classes that make up the template data to be serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="ef642-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="ef642-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="ef642-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -de klasse vertegenwoordigt een licentiesjabloon voor het maken van PlayReady-licenties moet worden geretourneerd voor de eindgebruikers.</span><span class="sxs-lookup"><span data-stu-id="ef642-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - The class represents a license template for creating PlayReady licenses to be returned to the end users.</span></span> <span data-ttu-id="ef642-141">De gegevens op de inhoudssleutel in de licentie en rechten of beperkingen moeten worden afgedwongen door de runtime PlayReady DRM bij gebruik van de inhoudssleutel bevat.</span><span class="sxs-lookup"><span data-stu-id="ef642-141">It contains the data on the content key in the license and any rights or restrictions to be enforced by the PlayReady DRM runtime when using the content key.</span></span>

### <span data-ttu-id="ef642-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="ef642-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="ef642-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -deze klasse vertegenwoordigt de PlayRight van een PlayReady-licentie.</span><span class="sxs-lookup"><span data-stu-id="ef642-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents the PlayRight of a PlayReady license.</span></span> <span data-ttu-id="ef642-144">Deze geeft de gebruiker de mogelijkheid voor het afspelen van de inhoud onderworpen aan de nul of meer beperkingen die zijn geconfigureerd in de licentievoorwaarden en klik op de PlayRight zelf (voor een specifiek beleid afspelen).</span><span class="sxs-lookup"><span data-stu-id="ef642-144">It grants the user the ability to playback the content subject to the zero or more restrictions configured in the license and on the PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="ef642-145">Veel van de beleidsregels op de PlayRight heeft te maken met uitvoer beperkingen die de soorten uitvoer die de inhoud kan worden afgespeeld via beheren en de beperkingen die in plaats moeten worden geplaatst bij gebruik van een bepaalde uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ef642-145">Much of the policy on the PlayRight has to do with output restrictions which control the types of outputs that the content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="ef642-146">Bijvoorbeeld als de DigitalVideoOnlyContentRestriction is ingeschakeld, klikt u vervolgens de runtime DRM alleen, krijgt de video moet worden weergegeven via digitale uitvoer (analoge video-uitgangen niet mag doorgeven van de inhoud).</span><span class="sxs-lookup"><span data-stu-id="ef642-146">For example, if the DigitalVideoOnlyContentRestriction is enabled, then the DRM runtime will only allow the video to be displayed over digital outputs (analog video outputs won’t be allowed to pass the content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef642-147">Typen beperkingen kunnen zeer krachtig maar kunnen ook van invloed op de ervaring van de consumer.</span><span class="sxs-lookup"><span data-stu-id="ef642-147">These types of restrictions can be very powerful but can also affect the consumer experience.</span></span> <span data-ttu-id="ef642-148">Als de uitvoer goed te beperkend zijn geconfigureerd, is het mogelijk dat de inhoud op sommige clients afgespeeld.</span><span class="sxs-lookup"><span data-stu-id="ef642-148">If the output protections are configured too restrictive, the content might be unplayable on some clients.</span></span> <span data-ttu-id="ef642-149">Zie voor meer informatie de [Compliantieregels PlayReady](https://www.microsoft.com/playready/licensing/compliance/) document.</span><span class="sxs-lookup"><span data-stu-id="ef642-149">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="ef642-150">Zie voor een voorbeeld van welke beveiliging ondersteunt Silverlight niveaus: [Silverlight-ondersteuning voor uitvoer beveiligingen](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="ef642-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="ef642-151"><a id="schema"></a>PlayReady-licentie sjabloon XML-schema</span><span class="sxs-lookup"><span data-stu-id="ef642-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="ef642-152">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="ef642-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ef642-153">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="ef642-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

