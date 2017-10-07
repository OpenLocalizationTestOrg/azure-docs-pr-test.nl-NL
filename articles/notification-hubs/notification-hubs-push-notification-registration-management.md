---
title: aaaRegistration Management
description: Dit onderwerp wordt uitgelegd hoe apparaten met notification hubs in volgorde tooreceive tooregister pushmeldingen.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a><span data-ttu-id="142b0-103">Registratiebeheer</span><span class="sxs-lookup"><span data-stu-id="142b0-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="142b0-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="142b0-104">Overview</span></span>
<span data-ttu-id="142b0-105">Dit onderwerp wordt uitgelegd hoe apparaten met notification hubs in volgorde tooreceive tooregister pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="142b0-105">This topic explains how tooregister devices with notification hubs in order tooreceive push notifications.</span></span> <span data-ttu-id="142b0-106">Hallo onderwerp beschrijft registraties op hoog niveau en vervolgens maakt u kennis met Hallo twee belangrijkste patronen voor het registreren van apparaten: registreren van Hallo apparaat rechtstreeks toohello notification hub en registreren via een back-end voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="142b0-106">hello topic describes registrations at a high level, then introduces hello two main patterns for registering devices: registering from hello device directly toohello notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="142b0-107">Wat is de registratie</span><span class="sxs-lookup"><span data-stu-id="142b0-107">What is device registration</span></span>
<span data-ttu-id="142b0-108">Registreren van apparaten met een Notification Hub wordt bereikt met een **registratie** of **installatie**.</span><span class="sxs-lookup"><span data-stu-id="142b0-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="142b0-109">Registraties</span><span class="sxs-lookup"><span data-stu-id="142b0-109">Registrations</span></span>
<span data-ttu-id="142b0-110">Een registratie koppelt Hallo Platform Notification Service (PNS) voor een apparaat met tags en mogelijk een sjabloon verwerkt.</span><span class="sxs-lookup"><span data-stu-id="142b0-110">A registration associates hello Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="142b0-111">Hallo PNS-ingang is mogelijk een ChannelURI, apparaattoken of GCM-registratie-id. Labels zijn gebruikte tooroute meldingen toohello correcte set apparaat verwerkt.</span><span class="sxs-lookup"><span data-stu-id="142b0-111">hello PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used tooroute notifications toohello correct set of device handles.</span></span> <span data-ttu-id="142b0-112">Zie voor meer informatie [Routering en code-expressies](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="142b0-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="142b0-113">Sjablonen zijn gebruikte tooimplement per registratie transformatie.</span><span class="sxs-lookup"><span data-stu-id="142b0-113">Templates are used tooimplement per-registration transformation.</span></span> <span data-ttu-id="142b0-114">Zie voor meer informatie [sjablonen](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="142b0-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="142b0-115">Installaties</span><span class="sxs-lookup"><span data-stu-id="142b0-115">Installations</span></span>
<span data-ttu-id="142b0-116">Een installatie is een uitgebreide registratie met een groot aantal push gerelateerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="142b0-116">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="142b0-117">Is het nieuwste en beste aanpak tooregistering Hallo uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="142b0-117">It is hello latest and best approach tooregistering your devices.</span></span> <span data-ttu-id="142b0-118">Echter niet ondersteund door de clientkant .NET SDK ([Notification Hub SDK voor back-end-bewerkingen](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) vanaf nog.</span><span class="sxs-lookup"><span data-stu-id="142b0-118">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="142b0-119">Dit betekent dat als u van clientapparaat Hallo zichzelf registreert, hebt u toouse hello [Notification Hubs REST-API](https://msdn.microsoft.com/library/mt621153.aspx) toosupport installaties benaderen.</span><span class="sxs-lookup"><span data-stu-id="142b0-119">This means if you are registering from hello client device itself, you would have toouse hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach toosupport installations.</span></span> <span data-ttu-id="142b0-120">Als u een back-endservice gebruikt, moet u kunnen toouse [Notification Hub SDK voor back-end-bewerkingen](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="142b0-120">If you are using a backend service, you should be able toouse [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="142b0-121">Hallo Hieronder volgen enkele belangrijke voordelen toousing installaties:</span><span class="sxs-lookup"><span data-stu-id="142b0-121">hello following are some key advantages toousing installations:</span></span>

* <span data-ttu-id="142b0-122">Maken of bijwerken van een installatie is volledig idempotent.</span><span class="sxs-lookup"><span data-stu-id="142b0-122">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="142b0-123">Zo kunt u het opnieuw zonder vragen over dubbele registraties.</span><span class="sxs-lookup"><span data-stu-id="142b0-123">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="142b0-124">Hallo installatiemodel maakt het eenvoudig toodo afzonderlijke pushes - doelen specifiek apparaat.</span><span class="sxs-lookup"><span data-stu-id="142b0-124">hello installation model makes it easy toodo individual pushes - targeting specific device.</span></span> <span data-ttu-id="142b0-125">Een Systeemlabel **' $InstallationId: [omwille van] '** automatisch met elke installatie op basis van de registratie wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="142b0-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="142b0-126">Zo kunt u bellen een verzenden toothis tag tootarget een specifiek apparaat zonder toodo extra programmeren.</span><span class="sxs-lookup"><span data-stu-id="142b0-126">So you can call a send toothis tag tootarget a specific device without having toodo any additional coding.</span></span>
* <span data-ttu-id="142b0-127">Installaties ook kunt u toodo gedeeltelijke registratie-updates.</span><span class="sxs-lookup"><span data-stu-id="142b0-127">Using installations also enables you toodo partial registration updates.</span></span> <span data-ttu-id="142b0-128">Hallo gedeeltelijke update van een installatie wordt aangevraagd met een PATCH-methode met Hallo [JSON-Patch standaard](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="142b0-128">hello partial update of an installation is requested with a PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="142b0-129">Dit is vooral handig als u wilt dat tooupdate labels op Hallo registratie.</span><span class="sxs-lookup"><span data-stu-id="142b0-129">This is particularly useful when you want tooupdate tags on hello registration.</span></span> <span data-ttu-id="142b0-130">U heb toopull omlaag Hallo volledige registratie en alle eerdere Hallo-codes opnieuw opnieuw te verzenden.</span><span class="sxs-lookup"><span data-stu-id="142b0-130">You don't have toopull down hello entire registration and then resend all hello previous tags again.</span></span>

<span data-ttu-id="142b0-131">Een installatie kan Hallo Hallo volgende eigenschappen bevatten.</span><span class="sxs-lookup"><span data-stu-id="142b0-131">An installation can contain hello hello following properties.</span></span> <span data-ttu-id="142b0-132">Voor een volledig overzicht van Hallo installatie-eigenschappen Zie [maken of een installatie met REST-API worden overschreven](https://msdn.microsoft.com/library/azure/mt621153.aspx) of [installatie-eigenschappen](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="142b0-132">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for hello .</span></span>

    // Example installation format tooshow some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



<span data-ttu-id="142b0-133">Het is belangrijk toonote waarop registraties en installaties standaard niet meer geldig.</span><span class="sxs-lookup"><span data-stu-id="142b0-133">It is important toonote that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="142b0-134">Registraties en installaties moeten een geldige PNS-ingang voor elk apparaat/kanaal bevatten.</span><span class="sxs-lookup"><span data-stu-id="142b0-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="142b0-135">Omdat PNS-ingangen kunnen alleen worden verkregen in een client-app op Hallo-apparaat, is een patroon tooregister rechtstreeks op het apparaat met Hallo client-app.</span><span class="sxs-lookup"><span data-stu-id="142b0-135">Because PNS handles can only be obtained in a client app on hello device, one pattern is tooregister directly on that device with hello client app.</span></span> <span data-ttu-id="142b0-136">Op Hallo gerelateerde andere hand, beveiligingsoverwegingen en bedrijfslogica tootags moet u mogelijk toomanage apparaatregistratie in de back-end van Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="142b0-136">On hello other hand, security considerations and business logic related tootags might require you toomanage device registration in hello app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="142b0-137">Sjablonen</span><span class="sxs-lookup"><span data-stu-id="142b0-137">Templates</span></span>
<span data-ttu-id="142b0-138">Als u wilt dat toouse [sjablonen](notification-hubs-templates-cross-platform-push-messages.md), de installatie van apparaat Hallo houdt ook alle sjablonen die zijn gekoppeld aan het apparaat in een JSON formatteren (Zie het bovenstaande voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="142b0-138">If you want toouse [Templates](notification-hubs-templates-cross-platform-push-messages.md), hello device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="142b0-139">Hallo sjabloonnamen helpen verschillende sjablonen voor Hallo gericht hetzelfde apparaat.</span><span class="sxs-lookup"><span data-stu-id="142b0-139">hello template names help target different templates for hello same device.</span></span>

<span data-ttu-id="142b0-140">Houd er rekening mee dat de sjabloonnaam van elke tooa sjabloon instantie en een optionele set van labels toegewezen.</span><span class="sxs-lookup"><span data-stu-id="142b0-140">Note that each template name maps tooa template body and an optional set of tags.</span></span> <span data-ttu-id="142b0-141">Elk platform kunt bovendien aanvullende Sjablooneigenschappen hebben.</span><span class="sxs-lookup"><span data-stu-id="142b0-141">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="142b0-142">Voor Windows Store (met WNS) en Windows Phone 8 (met behulp van MPNS), kan een extra set van headers deel uitmaken van Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="142b0-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of hello template.</span></span> <span data-ttu-id="142b0-143">In geval van APNs Hallo kunt u een eigenschap verstrijken tooeither een sjabloonexpressie-constante of -tooa instellen.</span><span class="sxs-lookup"><span data-stu-id="142b0-143">In hello case of APNs, you can set an expiry property tooeither a constant or tooa template expression.</span></span> <span data-ttu-id="142b0-144">Voor een volledig overzicht van Hallo installatie-eigenschappen Zie [maken of een installatie met REST overschrijven](https://msdn.microsoft.com/library/azure/mt621153.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="142b0-144">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="142b0-145">Secundaire tegels voor Windows Store-Apps</span><span class="sxs-lookup"><span data-stu-id="142b0-145">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="142b0-146">Voor Windows Store-clienttoepassingen Hallo verzenden van meldingen toosecondary tegels is hetzelfde als het verzenden van toohello primaire alias.</span><span class="sxs-lookup"><span data-stu-id="142b0-146">For Windows Store client applications, sending notifications toosecondary tiles is hello same as sending them toohello primary one.</span></span> <span data-ttu-id="142b0-147">Dit wordt ook ondersteund in installaties.</span><span class="sxs-lookup"><span data-stu-id="142b0-147">This is also supported in installations.</span></span> <span data-ttu-id="142b0-148">Houd er rekening mee dat secundaire tegels een verschillende ChannelUri hebben, welke Hallo SDK op uw clientapp transparant verwerkt.</span><span class="sxs-lookup"><span data-stu-id="142b0-148">Note that secondary tiles have a different ChannelUri, which hello SDK on your client app handles transparently.</span></span>

<span data-ttu-id="142b0-149">Hallo SecondaryTiles woordenlijst gebruikt Hallo dezelfde TileId die gebruikte toocreate hello SecondaryTiles object in de Windows Store-app.</span><span class="sxs-lookup"><span data-stu-id="142b0-149">hello SecondaryTiles dictionary uses hello same TileId that is used toocreate hello SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="142b0-150">Als de primaire ChannelUri, ChannelUris secundaire tegels Hello op elk moment wijzigen kunt.</span><span class="sxs-lookup"><span data-stu-id="142b0-150">As with hello primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="142b0-151">In de volgorde tookeep Hallo installaties in Hallo notification hub is bijgewerkt Hallo apparaat ze hebt vernieuwd Hello huidige ChannelUris Hallo secundaire tegels.</span><span class="sxs-lookup"><span data-stu-id="142b0-151">In order tookeep hello installations in hello notification hub updated, hello device must refresh them with hello current ChannelUris of hello secondary tiles.</span></span>

## <a name="registration-management-from-hello-device"></a><span data-ttu-id="142b0-152">Beheer van de registratie van Hallo-apparaat</span><span class="sxs-lookup"><span data-stu-id="142b0-152">Registration management from hello device</span></span>
<span data-ttu-id="142b0-153">Bij het beheren van de registratie van de client-apps, is alleen Hallo back-end die verantwoordelijk is voor het verzenden van meldingen.</span><span class="sxs-lookup"><span data-stu-id="142b0-153">When managing device registration from client apps, hello backend is only responsible for sending notifications.</span></span> <span data-ttu-id="142b0-154">Client-apps PNS-ingangen up toodate houden en registreer labels.</span><span class="sxs-lookup"><span data-stu-id="142b0-154">Client apps keep PNS handles up toodate, and register tags.</span></span> <span data-ttu-id="142b0-155">Hallo volgende afbeelding ziet u dit patroon.</span><span class="sxs-lookup"><span data-stu-id="142b0-155">hello following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="142b0-156">Hallo apparaat eerst Hallo PNS verwerken opgehaald uit Hallo PNS vervolgens rechtstreeks voor Hallo notification hub geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="142b0-156">hello device first retrieves hello PNS handle from hello PNS, then registers with hello notification hub directly.</span></span> <span data-ttu-id="142b0-157">Nadat het Hallo-registratie is geslaagd, kan back-end Hallo app een melding die gericht is op deze inschrijving verzenden.</span><span class="sxs-lookup"><span data-stu-id="142b0-157">After hello registration is successful, hello app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="142b0-158">Voor meer informatie over het toosend meldingen, Zie [Routering en code-expressies](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="142b0-158">For more information about how toosend notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="142b0-159">Merk op dat in dit geval gebruikt u luistert alleen rechten tooaccess uw notification hubs van Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="142b0-159">Note that in this case, you will use only Listen rights tooaccess your notification hubs from hello device.</span></span> <span data-ttu-id="142b0-160">Zie voor meer informatie [beveiliging](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="142b0-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="142b0-161">Registreren van apparaat Hallo Hallo eenvoudigste methode is, maar er enkele nadelen.</span><span class="sxs-lookup"><span data-stu-id="142b0-161">Registering from hello device is hello simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="142b0-162">Hallo eerste nadeel is dat een client-app alleen de labels bijwerken kunt wanneer Hallo app actief is.</span><span class="sxs-lookup"><span data-stu-id="142b0-162">hello first drawback is that a client app can only update its tags when hello app is active.</span></span> <span data-ttu-id="142b0-163">Bijvoorbeeld, als een gebruiker heeft twee apparaten die geregistreerd labels gerelateerde toosport teams, wanneer de eerste apparaat Hallo zich voor een aanvullende code (bijvoorbeeld Seahawks registreert), Hallo tweede apparaat wordt niet Hallo meldingen ontvangen over Hallo Seahawks tot Hallo-app op Hallo tweede apparaat wordt een tweede keer worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="142b0-163">For example, if a user has two devices that register tags related toosport teams, when hello first device registers for an additional tag (for example, Seahawks), hello second device will not receive hello notifications about hello Seahawks until hello app on hello second device is executed a second time.</span></span> <span data-ttu-id="142b0-164">Meer in het algemeen als labels worden beïnvloed door meerdere apparaten, is tags beheren vanuit Hallo back-end een wenselijk optie.</span><span class="sxs-lookup"><span data-stu-id="142b0-164">More generally, when tags are affected by multiple devices, managing tags from hello backend is a desirable option.</span></span>
<span data-ttu-id="142b0-165">Hallo tweede nadeel van beheer van de registratie van de client-app Hallo is dat extra aandacht beveiligen Hallo registratie toospecific tags is vereist omdat apps kunnen worden hacked, zoals wordt beschreven in de sectie Hallo "Tag beveiligingsniveau."</span><span class="sxs-lookup"><span data-stu-id="142b0-165">hello second drawback of registration management from hello client app is that, since apps can be hacked, securing hello registration toospecific tags requires extra care, as explained in hello section “Tag-level security.”</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="142b0-166">Voorbeeld van code tooregister met een notification hub van een apparaat gebruikmaakt van een installatie</span><span class="sxs-lookup"><span data-stu-id="142b0-166">Example code tooregister with a notification hub from a device using an installation</span></span>
<span data-ttu-id="142b0-167">Op dit moment is dit wordt alleen ondersteund met Hallo [Notification Hubs REST-API](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="142b0-167">At this time, this is only supported using hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="142b0-168">U kunt ook Hallo PATCH methode met behulp van Hallo [JSON-Patch standaard](https://tools.ietf.org/html/rfc6902) voor het bijwerken van Hallo-installatie.</span><span class="sxs-lookup"><span data-stu-id="142b0-168">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine hello targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="142b0-169">Voorbeeld van code tooregister met een notification hub van een apparaat een registratie</span><span class="sxs-lookup"><span data-stu-id="142b0-169">Example code tooregister with a notification hub from a device using a registration</span></span>
<span data-ttu-id="142b0-170">Deze methoden maken of bijwerken van een registratie voor Hallo-apparaat waarop ze worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="142b0-170">These methods create or update a registration for hello device on which they are called.</span></span> <span data-ttu-id="142b0-171">Dit betekent dat gehele Hallo-registratie in volgorde tooupdate Hallo ingang of Hallo labels, moet overschrijven.</span><span class="sxs-lookup"><span data-stu-id="142b0-171">This means that in order tooupdate hello handle or hello tags, you must overwrite hello entire registration.</span></span> <span data-ttu-id="142b0-172">Houd er rekening mee dat registraties tijdelijk is en zijn dus moet u altijd een betrouwbare archief met huidige Hallo-labels die een specifiek apparaat moet hebben.</span><span class="sxs-lookup"><span data-stu-id="142b0-172">Remember that registrations are transient, so you should always have a reliable store with hello current tags that a specific device needs.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="142b0-173">Beheer van de registratie van een back-end</span><span class="sxs-lookup"><span data-stu-id="142b0-173">Registration management from a backend</span></span>
<span data-ttu-id="142b0-174">Registraties vanuit Hallo back-end beheren, moet aanvullende code schrijven.</span><span class="sxs-lookup"><span data-stu-id="142b0-174">Managing registrations from hello backend requires writing additional code.</span></span> <span data-ttu-id="142b0-175">Hallo-app vanaf Hallo apparaat moet bijgewerkte PNS-ingang toohello back-end Hallo telkens wanneer Hallo-app wordt gestart (samen met tags en sjablonen) en Hallo back-end moet bijwerken deze ingang op Hallo notification hub opgeven.</span><span class="sxs-lookup"><span data-stu-id="142b0-175">hello app from hello device must provide hello updated PNS handle toohello backend every time hello app starts (along with tags and templates), and hello backend must update this handle on hello notification hub.</span></span> <span data-ttu-id="142b0-176">Hallo volgende afbeelding ziet u dit ontwerp.</span><span class="sxs-lookup"><span data-stu-id="142b0-176">hello following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="142b0-177">Hallo voordelen registraties vanuit Hallo back-end beheren Hallo mogelijkheid toomodify labels tooregistrations zelfs wanneer de bijbehorende app Hallo op Hallo-apparaat is niet actief en tooauthenticate Hallo client-app voordat u de registratie van een tag tooits toevoegt.</span><span class="sxs-lookup"><span data-stu-id="142b0-177">hello advantages of managing registrations from hello backend include hello ability toomodify tags tooregistrations even when hello corresponding app on hello device is inactive, and tooauthenticate hello client app before adding a tag tooits registration.</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="142b0-178">Voorbeeld van code tooregister met een notification hub vanuit een back-end gebruikmaakt van een installatie</span><span class="sxs-lookup"><span data-stu-id="142b0-178">Example code tooregister with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="142b0-179">Hallo-clientapparaat nog steeds de PNS-ingang en relevante installatie-eigenschappen als voorheen en aanroepen van aangepaste API op Hallo backend die kunt Hallo-registratie uitvoeren en autoriseren enzovoort Hallo back-end-tags kunnen gebruikmaken van Hallo [Notification Hub SDK voor back-end operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="142b0-179">hello client device still gets its PNS handle and relevant installation properties as before and calls a custom API on hello backend that can perform hello registration and authorize tags etc. hello backend can leverage hello [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="142b0-180">U kunt ook Hallo PATCH methode met behulp van Hallo [JSON-Patch standaard](https://tools.ietf.org/html/rfc6902) voor het bijwerken van Hallo-installatie.</span><span class="sxs-lookup"><span data-stu-id="142b0-180">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="142b0-181">Voorbeeld van code tooregister met een notification hub van een apparaat een registratie-id</span><span class="sxs-lookup"><span data-stu-id="142b0-181">Example code tooregister with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="142b0-182">U kunt CRUDS basisbewerkingen op registraties uitvoeren van uw app-end.</span><span class="sxs-lookup"><span data-stu-id="142b0-182">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="142b0-183">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="142b0-183">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


<span data-ttu-id="142b0-184">Hallo back-end moet verwerken gelijktijdigheid van taken tussen registratie-updates.</span><span class="sxs-lookup"><span data-stu-id="142b0-184">hello backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="142b0-185">Service Bus biedt Optimistisch gelijktijdigheidbeheer voor het beheer van de registratie.</span><span class="sxs-lookup"><span data-stu-id="142b0-185">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="142b0-186">Dit is geïmplementeerd op Hallo HTTP-niveau met Hallo gebruik van ETag op beheerbewerkingen voor registratie.</span><span class="sxs-lookup"><span data-stu-id="142b0-186">At hello HTTP level, this is implemented with hello use of ETag on registration management operations.</span></span> <span data-ttu-id="142b0-187">Deze functie is transparant gebruikt door de Microsoft-SDKs die Veroorzaak een exception als een update is geweigerd voor gelijktijdigheid redenen.</span><span class="sxs-lookup"><span data-stu-id="142b0-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="142b0-188">Hallo app back-end is verantwoordelijk voor het verwerken van deze uitzonderingen en Hallo update opnieuw, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="142b0-188">hello app backend is responsible for handling these exceptions and retrying hello update if required.</span></span>

