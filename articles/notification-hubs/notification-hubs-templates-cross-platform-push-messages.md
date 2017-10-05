---
title: Sjablonen
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
ms.openlocfilehash: 1ca24a4bf08ecdbe1c1e47a931613144309a04a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="templates"></a><span data-ttu-id="acde9-103">Sjablonen</span><span class="sxs-lookup"><span data-stu-id="acde9-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="acde9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="acde9-104">Overview</span></span>
<span data-ttu-id="acde9-105">Sjablonen ingeschakeld een clienttoepassing om op te geven van de precieze indeling van de meldingen wil ontvangen.</span><span class="sxs-lookup"><span data-stu-id="acde9-105">Templates enable a client application to specify the exact format of the notifications it wants to receive.</span></span> <span data-ttu-id="acde9-106">Met behulp van sjablonen, kan een app verschillende verschillende voordelen, waaronder de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="acde9-106">Using templates, an app can realize several different benefits, including the following :</span></span>

* <span data-ttu-id="acde9-107">Een back-end platform networkdirect</span><span class="sxs-lookup"><span data-stu-id="acde9-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="acde9-108">Aangepaste meldingen</span><span class="sxs-lookup"><span data-stu-id="acde9-108">Personalized notifications</span></span>
* <span data-ttu-id="acde9-109">Onafhankelijkheid van de client-versie</span><span class="sxs-lookup"><span data-stu-id="acde9-109">Client-version independence</span></span>
* <span data-ttu-id="acde9-110">Eenvoudig lokalisatie</span><span class="sxs-lookup"><span data-stu-id="acde9-110">Easy localization</span></span>

<span data-ttu-id="acde9-111">Deze sectie bevat twee gedetailleerde voorbeelden van hoe u sjablonen gebruikt om platform networkdirect-meldingen die gericht is op alle apparaten in verschillende platforms te verzenden en te personaliseren broadcast melding aan elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="acde9-111">This section provides two in-depth examples of how to use templates to send platform-agnostic notifications targeting all your devices across platforms, and to personalize broadcast notification to each device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="acde9-112">Met behulp van sjablonen cross-platform</span><span class="sxs-lookup"><span data-stu-id="acde9-112">Using templates cross-platform</span></span>
<span data-ttu-id="acde9-113">Er is de standaardmethode voor het verzenden van pushmeldingen te verzenden, voor elk bericht dat moet worden verzonden, een specifieke nettolading met platform notification services (WNS, APNS).</span><span class="sxs-lookup"><span data-stu-id="acde9-113">The standard way to send push notifications is to send, for each notification that is to be sent, a specific payload to platform notification services (WNS, APNS).</span></span> <span data-ttu-id="acde9-114">De nettolading is bijvoorbeeld een waarschuwing om naar te verzenden APNS, een Json-object van de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="acde9-114">For example, to send an alert to APNS, the payload is a Json object of the following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="acde9-115">Voor het verzenden van een vergelijkbaar pop-up bericht op een Windows Store-toepassing, is de XML-nettolading als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="acde9-115">To send a similar toast message on a Windows Store application, the XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="acde9-116">U kunt vergelijkbare nettoladingen maken voor MPNS (Windows Phone) en (Android) GCM-platforms.</span><span class="sxs-lookup"><span data-stu-id="acde9-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="acde9-117">Deze vereiste zorgt ervoor dat de app-back-end voor het produceren van verschillende nettoladingen voor elk platform, waardoor het effectief de back-end die verantwoordelijk is voor een deel van de laag voor presentatie van de app.</span><span class="sxs-lookup"><span data-stu-id="acde9-117">This requirement forces the app backend to produce different payloads for each platform, and effectively makes the backend responsible for part of the presentation layer of the app.</span></span> <span data-ttu-id="acde9-118">Sommige problemen bevatten te lokaliseren en grafische indelingen (vooral voor Windows Store-apps die meldingen voor verschillende soorten tegels bevatten).</span><span class="sxs-lookup"><span data-stu-id="acde9-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="acde9-119">De functie van de sjabloon Notification Hubs kunt een client-app voor het maken van speciale registraties, aangeroepen sjabloon registraties, waaronder, naast de reeks labels, een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="acde9-119">The Notification Hubs template feature enables a client app to create special registrations, called template registrations, which include, in addition to the set of tags, a template.</span></span> <span data-ttu-id="acde9-120">De functie van de sjabloon Notification Hubs kunt een client-app te koppelen van apparaten met behulp van sjablonen of u met werkt (voorkeur)-installaties of -registraties.</span><span class="sxs-lookup"><span data-stu-id="acde9-120">The Notification Hubs template feature enables a client app to associate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="acde9-121">Gezien de voorgaande voorbeelden van de nettolading, is de informatie alleen platformonafhankelijk het werkelijke waarschuwingsbericht (Hallo!).</span><span class="sxs-lookup"><span data-stu-id="acde9-121">Given the preceding payload examples, the only platform-independent information is the actual alert message (Hello!).</span></span> <span data-ttu-id="acde9-122">Een sjabloon is een verzameling instructies voor de Notification Hub voor het formatteren van een bericht platformonafhankelijk voor de registratie van die specifieke client-app.</span><span class="sxs-lookup"><span data-stu-id="acde9-122">A template is a set of instructions for the Notification Hub on how to format a platform-independent message for the registration of that specific client app.</span></span> <span data-ttu-id="acde9-123">In het voorgaande voorbeeld is het platform onafhankelijke bericht één eigenschap: **bericht = Hallo!**.</span><span class="sxs-lookup"><span data-stu-id="acde9-123">In the preceding example, the platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="acde9-124">De volgende afbeelding ziet u de bovenstaande procedure:</span><span class="sxs-lookup"><span data-stu-id="acde9-124">The following picture illustrates the above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="acde9-125">De sjabloon voor de iOS-app clientregistratie is als volgt:</span><span class="sxs-lookup"><span data-stu-id="acde9-125">The template for the iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="acde9-126">De bijbehorende sjabloon voor de client-app voor Windows Store is:</span><span class="sxs-lookup"><span data-stu-id="acde9-126">The corresponding template for the Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="acde9-127">U ziet dat het werkelijke bericht is vervangen door de expressie $(bericht).</span><span class="sxs-lookup"><span data-stu-id="acde9-127">Notice that the actual message is substituted for the expression $(message).</span></span> <span data-ttu-id="acde9-128">Deze expressie Hiermee geeft u de Notification Hub wanneer deze een bericht naar deze bepaalde registratie verzendt voor het bouwen van een bericht dat volgt op deze en switches in de algemene waarde.</span><span class="sxs-lookup"><span data-stu-id="acde9-128">This expression instructs the Notification Hub, whenever it sends a message to this particular registration, to build a message that follows it and switches in the common value.</span></span>

<span data-ttu-id="acde9-129">Als u met installatie-model werkt, bevat de installatie 'sjablonen' sleutel een JSON met meerdere sjablonen.</span><span class="sxs-lookup"><span data-stu-id="acde9-129">If you are working with Installation model, the installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="acde9-130">Als u met registratie model werkt, kunt de clienttoepassing meerdere registraties maken om te kunnen gebruiken, meerdere sjablonen. bijvoorbeeld, een sjabloon voor waarschuwingsberichten en een sjabloon voor updates van de tegel.</span><span class="sxs-lookup"><span data-stu-id="acde9-130">If you are working with Registration model, the client application can create multiple registrations in order to use multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="acde9-131">Client-toepassingen kunnen u ook systeemeigen registraties (registraties zonder sjabloon) en sjabloon registraties elkaar.</span><span class="sxs-lookup"><span data-stu-id="acde9-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="acde9-132">De Notification Hub verzendt een melding voor elke sjabloon zonder rekening te houden of ze tot dezelfde clientapp behoren.</span><span class="sxs-lookup"><span data-stu-id="acde9-132">The Notification Hub sends one notification for each template without considering whether they belong to the same client app.</span></span> <span data-ttu-id="acde9-133">Dit gedrag kan worden gebruikt om te vertalen platformonafhankelijk meldingen naar meer meldingen.</span><span class="sxs-lookup"><span data-stu-id="acde9-133">This behavior can be used to translate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="acde9-134">Bijvoorbeeld kan hetzelfde platform onafhankelijke bericht met de Notification Hub worden naadloos omgezet in een toast-melding en een update tegel zonder dat de back-end worden hiervan bewust zijn.</span><span class="sxs-lookup"><span data-stu-id="acde9-134">For example, the same platform independent message to the Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring the backend to be aware of it.</span></span> <span data-ttu-id="acde9-135">Houd er rekening mee dat sommige platformen (bijvoorbeeld iOS) meerdere meldingen op hetzelfde apparaat samenvouwen mogelijk als ze worden verzonden in een korte periode.</span><span class="sxs-lookup"><span data-stu-id="acde9-135">Note that some platforms (for example, iOS) might collapse multiple notifications to the same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="acde9-136">Met behulp van sjablonen voor persoonlijke instellingen</span><span class="sxs-lookup"><span data-stu-id="acde9-136">Using templates for personalization</span></span>
<span data-ttu-id="acde9-137">Een ander voordeel van met behulp van sjablonen is de mogelijkheid Notification Hubs gebruiken om uit te voeren per registratie personalisatie van meldingen.</span><span class="sxs-lookup"><span data-stu-id="acde9-137">Another advantage to using templates is the ability to use Notification Hubs to perform per-registration personalization of notifications.</span></span> <span data-ttu-id="acde9-138">Neem bijvoorbeeld een app weer waarin een tegel met de voorwaarden weer op een specifieke locatie.</span><span class="sxs-lookup"><span data-stu-id="acde9-138">For example, consider a weather app that displays a tile with the weather conditions at a specific location.</span></span> <span data-ttu-id="acde9-139">Een gebruiker kan kiezen tussen c of Fahrenheit graden en een prognose enkele of vijf dagen.</span><span class="sxs-lookup"><span data-stu-id="acde9-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="acde9-140">Met behulp van sjablonen, de installatie van elke client-app kunt registreren voor de vereiste indeling (1 dag Celsius, 1 dag Fahrenheit, 5 dagen c 5 dagen Fahrenheit), en de back-end een enkel bericht met de gegevens die zijn vereist voor het vervullen van deze sjablonen verzenden (bijvoorbeeld een prognose met c en Fahrenheit graden vijf dagen).</span><span class="sxs-lookup"><span data-stu-id="acde9-140">Using templates, each client app installation can register for the format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have the backend send a single message that contains all the information required to fill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="acde9-141">De sjabloon voor de prognose één dag met c temperaturen is als volgt:</span><span class="sxs-lookup"><span data-stu-id="acde9-141">The template for the one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="acde9-142">Het bericht verzonden naar de Notification Hub bevat de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="acde9-142">The message sent to the Notification Hub contains all the following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="acde9-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="acde9-143">day1_image</span></span></td><td><span data-ttu-id="acde9-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="acde9-144">day2_image</span></span></td><td><span data-ttu-id="acde9-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="acde9-145">day3_image</span></span></td><td><span data-ttu-id="acde9-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="acde9-146">day4_image</span></span></td><td><span data-ttu-id="acde9-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="acde9-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="acde9-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="acde9-148">day1_tempC</span></span></td><td><span data-ttu-id="acde9-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="acde9-149">day2_tempC</span></span></td><td><span data-ttu-id="acde9-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="acde9-150">day3_tempC</span></span></td><td><span data-ttu-id="acde9-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="acde9-151">day4_tempC</span></span></td><td><span data-ttu-id="acde9-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="acde9-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="acde9-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="acde9-153">day1_tempF</span></span></td><td><span data-ttu-id="acde9-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="acde9-154">day2_tempF</span></span></td><td><span data-ttu-id="acde9-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="acde9-155">day3_tempF</span></span></td><td><span data-ttu-id="acde9-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="acde9-156">day4_tempF</span></span></td><td><span data-ttu-id="acde9-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="acde9-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="acde9-158">Met behulp van dit patroon, verzendt de back-end slechts één bericht zonder voor het opslaan van specifieke personalisatie opties voor de app-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="acde9-158">By using this pattern, the backend only sends a single message without having to store specific personalization options for the app users.</span></span> <span data-ttu-id="acde9-159">De volgende afbeelding ziet u dit scenario:</span><span class="sxs-lookup"><span data-stu-id="acde9-159">The following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-to-register-templates"></a><span data-ttu-id="acde9-160">Het registreren van sjablonen</span><span class="sxs-lookup"><span data-stu-id="acde9-160">How to register templates</span></span>
<span data-ttu-id="acde9-161">Als u wilt registreren met behulp van sjablonen met behulp van de installatie-model (voorkeur), of de registratie, Zie [registratie Management](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="acde9-161">To register with templates using the Installation model (preferred), or the Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="acde9-162">Expressie sjabloontaal</span><span class="sxs-lookup"><span data-stu-id="acde9-162">Template expression language</span></span>
<span data-ttu-id="acde9-163">Sjablonen zijn beperkt tot indelingen van XML- of JSON-document.</span><span class="sxs-lookup"><span data-stu-id="acde9-163">Templates are limited to XML or JSON document formats.</span></span> <span data-ttu-id="acde9-164">Bovendien kunt u alleen plaatsen expressies in bepaalde plaatsen; bijvoorbeeld, de kenmerken van knooppunt of de waarden voor XML tekenreeks eigenschapswaarden voor JSON.</span><span class="sxs-lookup"><span data-stu-id="acde9-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="acde9-165">De volgende tabel ziet u de taal die is toegestaan in sjablonen:</span><span class="sxs-lookup"><span data-stu-id="acde9-165">The following table shows the language allowed in templates:</span></span>

| <span data-ttu-id="acde9-166">expressie</span><span class="sxs-lookup"><span data-stu-id="acde9-166">Expression</span></span> | <span data-ttu-id="acde9-167">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="acde9-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="acde9-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="acde9-168">$(prop)</span></span> |<span data-ttu-id="acde9-169">Verwijzing naar een gebeurteniseigenschap met de opgegeven naam.</span><span class="sxs-lookup"><span data-stu-id="acde9-169">Reference to an event property with the given name.</span></span> <span data-ttu-id="acde9-170">De namen van eigenschappen zijn niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="acde9-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="acde9-171">Deze expressie wordt omgezet in de tekstwaarde van de eigenschap of een lege tekenreeks als de eigenschap niet aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="acde9-171">This expression resolves into the property’s text value or into an empty string if the property is not present.</span></span> |
| <span data-ttu-id="acde9-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="acde9-172">$(prop, n)</span></span> |<span data-ttu-id="acde9-173">Zoals hierboven, maar de tekst expliciet is afgekapt op n tekens, bijvoorbeeld $(titel, 20) knipt de inhoud van de eigenschap title op 20 tekens bestaan.</span><span class="sxs-lookup"><span data-stu-id="acde9-173">As above, but the text is explicitly clipped at n characters, for example $(title, 20) clips the contents of the title property at 20 characters.</span></span> |
| <span data-ttu-id="acde9-174">. (prop, n)</span><span class="sxs-lookup"><span data-stu-id="acde9-174">.(prop, n)</span></span> |<span data-ttu-id="acde9-175">Zoals hierboven, maar de tekst wordt voorafgegaan door drie punten omdat deze is afgekapt.</span><span class="sxs-lookup"><span data-stu-id="acde9-175">As above, but the text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="acde9-176">De totale grootte van de afgekapte tekenreeks en het achtervoegsel overschrijdt niet n tekens.</span><span class="sxs-lookup"><span data-stu-id="acde9-176">The total size of the clipped string and the suffix does not exceed n characters.</span></span> <span data-ttu-id="acde9-177">. (titel, 20) met een invoer-eigenschap van de resultaten in 'Is de titelregel ' **dit is de titel...**</span><span class="sxs-lookup"><span data-stu-id="acde9-177">.(title, 20) with an input property of “This is the title line” results in **This is the title...**</span></span> |
| <span data-ttu-id="acde9-178">%(Prop)</span><span class="sxs-lookup"><span data-stu-id="acde9-178">%(prop)</span></span> |<span data-ttu-id="acde9-179">Vergelijkbaar zijn met $(name), behalve dat de uitvoer is de URI-codering.</span><span class="sxs-lookup"><span data-stu-id="acde9-179">Similar to $(name) except that the output is URI-encoded.</span></span> |
| <span data-ttu-id="acde9-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="acde9-180">#(prop)</span></span> |<span data-ttu-id="acde9-181">In JSON-sjablonen gebruikt (bijvoorbeeld voor iOS en Android-sjablonen).</span><span class="sxs-lookup"><span data-stu-id="acde9-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="acde9-182">Deze functie werkt precies hetzelfde als $(prop) eerder hebt opgegeven, behalve wanneer in JSON-sjablonen (bijvoorbeeld een Apple-sjablonen).</span><span class="sxs-lookup"><span data-stu-id="acde9-182">This function works exactly the same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="acde9-183">In dit geval, als deze functie wordt niet omgeven door '{','}' (bijvoorbeeld myJsonProperty: '#(naam)'), en dit resulteert in een getal in Javascript-indeling, bijvoorbeeld regexp: (0 &#124; (&#91; 1-9, #93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, en vervolgens de JSON-uitvoer een getal is.</span><span class="sxs-lookup"><span data-stu-id="acde9-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates to a number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then the output JSON is a number.</span></span><br><br><span data-ttu-id="acde9-184">Bijvoorbeeld ' badge: '#(naam)', wordt de badge': 40 (en niet 40).</span><span class="sxs-lookup"><span data-stu-id="acde9-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="acde9-185">'text' of 'text'</span><span class="sxs-lookup"><span data-stu-id="acde9-185">‘text’ or “text”</span></span> |<span data-ttu-id="acde9-186">Een letterlijke waarde.</span><span class="sxs-lookup"><span data-stu-id="acde9-186">A literal.</span></span> <span data-ttu-id="acde9-187">Letterlijke waarden bevatten willekeurige tekst tussen enkele of dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="acde9-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="acde9-188">Expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="acde9-188">expr1 + expr2</span></span> |<span data-ttu-id="acde9-189">De samenvoegingsoperator lid te worden twee expressies in één tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="acde9-189">The concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="acde9-190">De expressies mag geen van de voorgaande formulieren.</span><span class="sxs-lookup"><span data-stu-id="acde9-190">The expressions can be any of the preceding forms.</span></span>

<span data-ttu-id="acde9-191">Wanneer u samenvoeging gebruikt, moet u de volledige expressie tussen met {}.</span><span class="sxs-lookup"><span data-stu-id="acde9-191">When using concatenation, the entire expression must be surrounded with {}.</span></span> <span data-ttu-id="acde9-192">Bijvoorbeeld, {$(prop) + '-' + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="acde9-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="acde9-193">Bijvoorbeeld, is het volgende niet een geldig XML-sjabloon:</span><span class="sxs-lookup"><span data-stu-id="acde9-193">For example, the following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="acde9-194">Uitgelegd hierboven, wanneer u samenvoeging moeten expressies worden verpakt tussen accolades.</span><span class="sxs-lookup"><span data-stu-id="acde9-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="acde9-195">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="acde9-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

