---
title: aaaTemplates
description: Dit onderwerp worden de sjablonen voor Azure notification hubs.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a><span data-ttu-id="e20a4-103">Sjablonen</span><span class="sxs-lookup"><span data-stu-id="e20a4-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="e20a4-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e20a4-104">Overview</span></span>
<span data-ttu-id="e20a4-105">Sjablonen inschakelen een client toepassing toospecify Hallo precieze indeling van Hallo meldingen dat deze tooreceive wil.</span><span class="sxs-lookup"><span data-stu-id="e20a4-105">Templates enable a client application toospecify hello exact format of hello notifications it wants tooreceive.</span></span> <span data-ttu-id="e20a4-106">Met behulp van sjablonen, kan een app diverse verschillende voordelen, waaronder Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="e20a4-106">Using templates, an app can realize several different benefits, including hello following :</span></span>

* <span data-ttu-id="e20a4-107">Een back-end platform networkdirect</span><span class="sxs-lookup"><span data-stu-id="e20a4-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="e20a4-108">Aangepaste meldingen</span><span class="sxs-lookup"><span data-stu-id="e20a4-108">Personalized notifications</span></span>
* <span data-ttu-id="e20a4-109">Onafhankelijkheid van de client-versie</span><span class="sxs-lookup"><span data-stu-id="e20a4-109">Client-version independence</span></span>
* <span data-ttu-id="e20a4-110">Eenvoudig lokalisatie</span><span class="sxs-lookup"><span data-stu-id="e20a4-110">Easy localization</span></span>

<span data-ttu-id="e20a4-111">Deze sectie bevat twee gedetailleerde voorbeelden van hoe toouse sjablonen toosend platform networkdirect meldingen die gericht is op al uw apparaten op platforms en toopersonalize tooeach meldingsapparaten broadcast.</span><span class="sxs-lookup"><span data-stu-id="e20a4-111">This section provides two in-depth examples of how toouse templates toosend platform-agnostic notifications targeting all your devices across platforms, and toopersonalize broadcast notification tooeach device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="e20a4-112">Met behulp van sjablonen cross-platform</span><span class="sxs-lookup"><span data-stu-id="e20a4-112">Using templates cross-platform</span></span>
<span data-ttu-id="e20a4-113">Hallo standaardmanier toosend pushmeldingen is toosend voor elk bericht dat is verzonden, toobe een specifieke nettolading tooplatform notification services (WNS, APNS).</span><span class="sxs-lookup"><span data-stu-id="e20a4-113">hello standard way toosend push notifications is toosend, for each notification that is toobe sent, a specific payload tooplatform notification services (WNS, APNS).</span></span> <span data-ttu-id="e20a4-114">Hallo nettolading is bijvoorbeeld een waarschuwing tooAPNS toosend een Json-object Hallo formulier te volgen:</span><span class="sxs-lookup"><span data-stu-id="e20a4-114">For example, toosend an alert tooAPNS, hello payload is a Json object of hello following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="e20a4-115">toosend een vergelijkbare pop-up bericht op een Windows Store-toepassing, Hallo XML-nettolading is als volgt:</span><span class="sxs-lookup"><span data-stu-id="e20a4-115">toosend a similar toast message on a Windows Store application, hello XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="e20a4-116">U kunt vergelijkbare nettoladingen maken voor MPNS (Windows Phone) en (Android) GCM-platforms.</span><span class="sxs-lookup"><span data-stu-id="e20a4-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="e20a4-117">Deze vereiste forceert Hallo app back-end tooproduce verschillende nettoladingen voor elk platform, waardoor het effectief Hallo back-end die verantwoordelijk is voor een deel van Hallo presentation beschermingslaag Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="e20a4-117">This requirement forces hello app backend tooproduce different payloads for each platform, and effectively makes hello backend responsible for part of hello presentation layer of hello app.</span></span> <span data-ttu-id="e20a4-118">Sommige problemen bevatten te lokaliseren en grafische indelingen (vooral voor Windows Store-apps die meldingen voor verschillende soorten tegels bevatten).</span><span class="sxs-lookup"><span data-stu-id="e20a4-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="e20a4-119">Hallo Notification Hubs sjabloon functie kunt een client-app toocreate speciale registraties, aangeroepen sjabloon registraties, waaronder, Daarnaast toohello reeks labels, een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e20a4-119">hello Notification Hubs template feature enables a client app toocreate special registrations, called template registrations, which include, in addition toohello set of tags, a template.</span></span> <span data-ttu-id="e20a4-120">Hallo Notification Hubs sjabloon functie kunt een client-app tooassociate apparaten met behulp van sjablonen of u met werkt (voorkeur)-installaties of -registraties.</span><span class="sxs-lookup"><span data-stu-id="e20a4-120">hello Notification Hubs template feature enables a client app tooassociate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="e20a4-121">Hallo voorafgaand aan de nettolading van voorbeelden gegeven, is hello alleen platformonafhankelijk informatie Hallo werkelijke-waarschuwingsbericht (Hallo!).</span><span class="sxs-lookup"><span data-stu-id="e20a4-121">Given hello preceding payload examples, hello only platform-independent information is hello actual alert message (Hello!).</span></span> <span data-ttu-id="e20a4-122">Een sjabloon is een verzameling instructies voor het Hallo Notification Hub op hoe tooformat een platformonafhankelijk bericht voor de registratie van Hallo van die specifieke client-app.</span><span class="sxs-lookup"><span data-stu-id="e20a4-122">A template is a set of instructions for hello Notification Hub on how tooformat a platform-independent message for hello registration of that specific client app.</span></span> <span data-ttu-id="e20a4-123">Hallo voorgaande voorbeeld, onafhankelijke welkomstbericht platform is één eigenschap: **bericht = Hallo!**.</span><span class="sxs-lookup"><span data-stu-id="e20a4-123">In hello preceding example, hello platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="e20a4-124">Hallo volgende afbeelding ziet u Hallo hierboven proces:</span><span class="sxs-lookup"><span data-stu-id="e20a4-124">hello following picture illustrates hello above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="e20a4-125">Hallo-sjabloon voor Hallo iOS-app clientregistratie is als volgt:</span><span class="sxs-lookup"><span data-stu-id="e20a4-125">hello template for hello iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="e20a4-126">Hallo bijbehorende sjabloon voor Windows Store-clientapp Hallo is:</span><span class="sxs-lookup"><span data-stu-id="e20a4-126">hello corresponding template for hello Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="e20a4-127">U ziet dat werkelijke Hallo-bericht is vervangen door Hallo expressie $(bericht).</span><span class="sxs-lookup"><span data-stu-id="e20a4-127">Notice that hello actual message is substituted for hello expression $(message).</span></span> <span data-ttu-id="e20a4-128">Deze expressie geïnstrueerd Hallo Notification Hub wanneer het verzendt een bericht toothis bepaalde registratie, toobuild een bericht dat volgt op deze en switches in Hallo algemene waarde.</span><span class="sxs-lookup"><span data-stu-id="e20a4-128">This expression instructs hello Notification Hub, whenever it sends a message toothis particular registration, toobuild a message that follows it and switches in hello common value.</span></span>

<span data-ttu-id="e20a4-129">Als u met installatie-model werkt, bevat Hallo installatie 'sjablonen' sleutel een JSON met meerdere sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e20a4-129">If you are working with Installation model, hello installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="e20a4-130">Als u met registratie model werkt, kunt Hallo clienttoepassing maken meerdere registraties volgorde toouse meerdere sjablonen. bijvoorbeeld, een sjabloon voor waarschuwingsberichten en een sjabloon voor updates van de tegel.</span><span class="sxs-lookup"><span data-stu-id="e20a4-130">If you are working with Registration model, hello client application can create multiple registrations in order toouse multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="e20a4-131">Client-toepassingen kunnen u ook systeemeigen registraties (registraties zonder sjabloon) en sjabloon registraties elkaar.</span><span class="sxs-lookup"><span data-stu-id="e20a4-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="e20a4-132">Hallo Notification Hub verzendt een melding voor elke sjabloon zonder rekening te houden of ze toohello horen dezelfde client-app.</span><span class="sxs-lookup"><span data-stu-id="e20a4-132">hello Notification Hub sends one notification for each template without considering whether they belong toohello same client app.</span></span> <span data-ttu-id="e20a4-133">Dit gedrag kan worden gebruikt tootranslate platformonafhankelijk meldingen naar meer meldingen.</span><span class="sxs-lookup"><span data-stu-id="e20a4-133">This behavior can be used tootranslate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="e20a4-134">Bijvoorbeeld, Hallo hetzelfde platform onafhankelijke bericht toohello die Notification Hub naadloos kan worden omgezet in een toast-melding en een update tegel Hallo zonder back-end toobe hiervan bewust zijn.</span><span class="sxs-lookup"><span data-stu-id="e20a4-134">For example, hello same platform independent message toohello Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring hello backend toobe aware of it.</span></span> <span data-ttu-id="e20a4-135">Opmerking dat sommige platformen (bijvoorbeeld iOS) meerdere meldingen toohello mogelijk samenvouwen hetzelfde apparaat als ze worden verzonden in een korte periode.</span><span class="sxs-lookup"><span data-stu-id="e20a4-135">Note that some platforms (for example, iOS) might collapse multiple notifications toohello same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="e20a4-136">Met behulp van sjablonen voor persoonlijke instellingen</span><span class="sxs-lookup"><span data-stu-id="e20a4-136">Using templates for personalization</span></span>
<span data-ttu-id="e20a4-137">Een ander voordeel toousing sjablonen is Hallo mogelijkheid toouse Notification Hubs tooperform per registratie personalisatie van meldingen.</span><span class="sxs-lookup"><span data-stu-id="e20a4-137">Another advantage toousing templates is hello ability toouse Notification Hubs tooperform per-registration personalization of notifications.</span></span> <span data-ttu-id="e20a4-138">Neem bijvoorbeeld een app weer waarin een tegel met de voorwaarden van Hallo weer op een specifieke locatie.</span><span class="sxs-lookup"><span data-stu-id="e20a4-138">For example, consider a weather app that displays a tile with hello weather conditions at a specific location.</span></span> <span data-ttu-id="e20a4-139">Een gebruiker kan kiezen tussen c of Fahrenheit graden en een prognose enkele of vijf dagen.</span><span class="sxs-lookup"><span data-stu-id="e20a4-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="e20a4-140">Met behulp van sjablonen, de installatie van elke client-app kunt registreren voor vereiste Hallo-indeling (1 dag Celsius, 1 dag Fahrenheit, 5 dagen c 5 dagen Fahrenheit), en Hallo back-end voor één bericht met alle Hallo informatie vereiste toofill die sturen sjablonen (bijvoorbeeld vijf maal prognose met c en Fahrenheit graden).</span><span class="sxs-lookup"><span data-stu-id="e20a4-140">Using templates, each client app installation can register for hello format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have hello backend send a single message that contains all hello information required toofill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="e20a4-141">Hallo-sjabloon voor Hallo één dag prognose met c temperaturen is als volgt:</span><span class="sxs-lookup"><span data-stu-id="e20a4-141">hello template for hello one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="e20a4-142">Hallo-bericht verzonden toohello Notification Hub bevat alle Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="e20a4-142">hello message sent toohello Notification Hub contains all hello following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="e20a4-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="e20a4-143">day1_image</span></span></td><td><span data-ttu-id="e20a4-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="e20a4-144">day2_image</span></span></td><td><span data-ttu-id="e20a4-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="e20a4-145">day3_image</span></span></td><td><span data-ttu-id="e20a4-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="e20a4-146">day4_image</span></span></td><td><span data-ttu-id="e20a4-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="e20a4-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="e20a4-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="e20a4-148">day1_tempC</span></span></td><td><span data-ttu-id="e20a4-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="e20a4-149">day2_tempC</span></span></td><td><span data-ttu-id="e20a4-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="e20a4-150">day3_tempC</span></span></td><td><span data-ttu-id="e20a4-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="e20a4-151">day4_tempC</span></span></td><td><span data-ttu-id="e20a4-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="e20a4-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="e20a4-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="e20a4-153">day1_tempF</span></span></td><td><span data-ttu-id="e20a4-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="e20a4-154">day2_tempF</span></span></td><td><span data-ttu-id="e20a4-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="e20a4-155">day3_tempF</span></span></td><td><span data-ttu-id="e20a4-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="e20a4-156">day4_tempF</span></span></td><td><span data-ttu-id="e20a4-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="e20a4-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="e20a4-158">Met behulp van dit patroon verzendt Hallo back-end slechts één bericht zonder toostore specifieke personalisatie opties voor het Hallo-app-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e20a4-158">By using this pattern, hello backend only sends a single message without having toostore specific personalization options for hello app users.</span></span> <span data-ttu-id="e20a4-159">Hallo volgende afbeelding ziet u dit scenario:</span><span class="sxs-lookup"><span data-stu-id="e20a4-159">hello following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a><span data-ttu-id="e20a4-160">Hoe tooregister sjablonen</span><span class="sxs-lookup"><span data-stu-id="e20a4-160">How tooregister templates</span></span>
<span data-ttu-id="e20a4-161">Zie tooregister met sjablonen met Hallo installatiemodel (aanbevolen) of Hallo registratie model [registratie Management](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="e20a4-161">tooregister with templates using hello Installation model (preferred), or hello Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="e20a4-162">Expressie sjabloontaal</span><span class="sxs-lookup"><span data-stu-id="e20a4-162">Template expression language</span></span>
<span data-ttu-id="e20a4-163">Sjablonen zijn beperkt tooXML of de opmaak van de JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="e20a4-163">Templates are limited tooXML or JSON document formats.</span></span> <span data-ttu-id="e20a4-164">Bovendien kunt u alleen plaatsen expressies in bepaalde plaatsen; bijvoorbeeld, de kenmerken van knooppunt of de waarden voor XML tekenreeks eigenschapswaarden voor JSON.</span><span class="sxs-lookup"><span data-stu-id="e20a4-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="e20a4-165">Hallo ziet volgende tabel u Hallo taal toegestaan in sjablonen:</span><span class="sxs-lookup"><span data-stu-id="e20a4-165">hello following table shows hello language allowed in templates:</span></span>

| <span data-ttu-id="e20a4-166">expressie</span><span class="sxs-lookup"><span data-stu-id="e20a4-166">Expression</span></span> | <span data-ttu-id="e20a4-167">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e20a4-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e20a4-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="e20a4-168">$(prop)</span></span> |<span data-ttu-id="e20a4-169">Tooan gebeurtenis verwijzingseigenschap met Hallo opgegeven naam.</span><span class="sxs-lookup"><span data-stu-id="e20a4-169">Reference tooan event property with hello given name.</span></span> <span data-ttu-id="e20a4-170">De namen van eigenschappen zijn niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="e20a4-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="e20a4-171">Deze expressie wordt omgezet in de tekstwaarde van de eigenschap hello of een lege tekenreeks als Hallo-eigenschap niet aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="e20a4-171">This expression resolves into hello property’s text value or into an empty string if hello property is not present.</span></span> |
| <span data-ttu-id="e20a4-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="e20a4-172">$(prop, n)</span></span> |<span data-ttu-id="e20a4-173">Zoals hierboven, maar hello tekst expliciet is afgekapt op n tekens, bijvoorbeeld $(titel, 20) knipt Hallo inhoud van de eigenschap title Hallo op 20 tekens bestaan.</span><span class="sxs-lookup"><span data-stu-id="e20a4-173">As above, but hello text is explicitly clipped at n characters, for example $(title, 20) clips hello contents of hello title property at 20 characters.</span></span> |
| <span data-ttu-id="e20a4-174">. (prop, n)</span><span class="sxs-lookup"><span data-stu-id="e20a4-174">.(prop, n)</span></span> |<span data-ttu-id="e20a4-175">Als hierboven, maar hello tekst met de drie puntjes voorafgegaan, zoals deze is afgekapt.</span><span class="sxs-lookup"><span data-stu-id="e20a4-175">As above, but hello text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="e20a4-176">totale grootte van de Hallo Hallo afgekapt tekenreeks en Hallo achtervoegsel niet meer dan n tekens.</span><span class="sxs-lookup"><span data-stu-id="e20a4-176">hello total size of hello clipped string and hello suffix does not exceed n characters.</span></span> <span data-ttu-id="e20a4-177">. (titel, 20) met een invoer-eigenschap van de resultaten in 'Is Hallo titelregel' **dit is de titel Hallo...**</span><span class="sxs-lookup"><span data-stu-id="e20a4-177">.(title, 20) with an input property of “This is hello title line” results in **This is hello title...**</span></span> |
| <span data-ttu-id="e20a4-178">%(Prop)</span><span class="sxs-lookup"><span data-stu-id="e20a4-178">%(prop)</span></span> |<span data-ttu-id="e20a4-179">Vergelijkbare too$(name) behalve die Hallo-uitvoer is de URI-codering.</span><span class="sxs-lookup"><span data-stu-id="e20a4-179">Similar too$(name) except that hello output is URI-encoded.</span></span> |
| <span data-ttu-id="e20a4-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="e20a4-180">#(prop)</span></span> |<span data-ttu-id="e20a4-181">In JSON-sjablonen gebruikt (bijvoorbeeld voor iOS en Android-sjablonen).</span><span class="sxs-lookup"><span data-stu-id="e20a4-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="e20a4-182">Deze functie werkt Hallo precies hetzelfde als $(prop) eerder hebt opgegeven, behalve wanneer in JSON-sjablonen (bijvoorbeeld een Apple-sjablonen).</span><span class="sxs-lookup"><span data-stu-id="e20a4-182">This function works exactly hello same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="e20a4-183">In dit geval, als deze functie wordt niet omgeven door '{','}' (bijvoorbeeld myJsonProperty: '#(naam)'), en het nummer in Javascript-indeling, bijvoorbeeld regexp tooa evalueert: (0 &#124; (&#91; 1-9, #93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, en vervolgens Hallo uitvoer JSON is een getal.</span><span class="sxs-lookup"><span data-stu-id="e20a4-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates tooa number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then hello output JSON is a number.</span></span><br><br><span data-ttu-id="e20a4-184">Bijvoorbeeld ' badge: '#(naam)', wordt de badge': 40 (en niet 40).</span><span class="sxs-lookup"><span data-stu-id="e20a4-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="e20a4-185">'text' of 'text'</span><span class="sxs-lookup"><span data-stu-id="e20a4-185">‘text’ or “text”</span></span> |<span data-ttu-id="e20a4-186">Een letterlijke waarde.</span><span class="sxs-lookup"><span data-stu-id="e20a4-186">A literal.</span></span> <span data-ttu-id="e20a4-187">Letterlijke waarden bevatten willekeurige tekst tussen enkele of dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="e20a4-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="e20a4-188">Expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="e20a4-188">expr1 + expr2</span></span> |<span data-ttu-id="e20a4-189">Hallo samenvoegingsoperator lid te worden twee expressies in één tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="e20a4-189">hello concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="e20a4-190">Hallo-expressies zijn Hallo voorafgaand aan formulieren.</span><span class="sxs-lookup"><span data-stu-id="e20a4-190">hello expressions can be any of hello preceding forms.</span></span>

<span data-ttu-id="e20a4-191">Wanneer u samenvoeging gebruikt, moet u Hallo gehele expressie tussen met {}.</span><span class="sxs-lookup"><span data-stu-id="e20a4-191">When using concatenation, hello entire expression must be surrounded with {}.</span></span> <span data-ttu-id="e20a4-192">Bijvoorbeeld, {$(prop) + '-' + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="e20a4-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="e20a4-193">Hallo volgende is bijvoorbeeld niet een geldig XML-sjabloon:</span><span class="sxs-lookup"><span data-stu-id="e20a4-193">For example, hello following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="e20a4-194">Uitgelegd hierboven, wanneer u samenvoeging moeten expressies worden verpakt tussen accolades.</span><span class="sxs-lookup"><span data-stu-id="e20a4-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="e20a4-195">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e20a4-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

