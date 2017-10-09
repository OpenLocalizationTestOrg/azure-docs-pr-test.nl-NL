---
title: aaaConfigure meldingen en e-mailsjablonen in Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooconfigure meldingen en e-mailsjablonen in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="a7424-103">Hoe tooconfigure meldingen en e-mailsjablonen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="a7424-103">How tooconfigure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="a7424-104">API Management biedt de mogelijkheid Hallo tooconfigure meldingen voor specifieke gebeurtenissen en tooconfigure Hallo e-mailsjablonen die zijn gebruikt toocommunicate met Hallo-beheerders en ontwikkelaars van exemplaar van API Management.</span><span class="sxs-lookup"><span data-stu-id="a7424-104">API Management provides hello ability tooconfigure notifications for specific events, and tooconfigure hello email templates that are used toocommunicate with hello administrators and developers of an API Management instance.</span></span> <span data-ttu-id="a7424-105">Dit onderwerp wordt beschreven hoe tooconfigure meldingen voor beschikbare gebeurtenissen hello, en biedt een overzicht van het configureren van e-mailsjablonen Hallo gebruikt deze gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="a7424-105">This topic shows how tooconfigure notifications for hello available events, and provides an overview of configuring hello email templates used for these events.</span></span>

## <span data-ttu-id="a7424-106"><a name="publisher-notifications"></a>Publisher meldingen configureren</span><span class="sxs-lookup"><span data-stu-id="a7424-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="a7424-107">tooconfigure meldingen, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="a7424-107">tooconfigure notifications, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="a7424-108">Hiermee gaat u toohello API Management-publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="a7424-108">This takes you toohello API Management publisher portal.</span></span>

![Publicatieportal][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="a7424-110">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a7424-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="a7424-111">Klik op **meldingen** van Hallo **API Management** menu op Hallo links tooview Hallo beschikbare meldingen.</span><span class="sxs-lookup"><span data-stu-id="a7424-111">Click **Notifications** from hello **API Management** menu on hello left tooview hello available notifications.</span></span>

![Meldingen van de uitgever][api-management-publisher-notifications]

<span data-ttu-id="a7424-113">Hallo kan volgende lijst van gebeurtenissen die worden geconfigureerd voor meldingen.</span><span class="sxs-lookup"><span data-stu-id="a7424-113">hello following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="a7424-114">**Verzoeken om abonnementen (goedkeuring wordt vereist)** - Hallo opgegeven e-mailontvangers en ontvangen gebruikers e-mailmeldingen over verzoeken om abonnementen voor API-producten goedkeuring wordt vereist.</span><span class="sxs-lookup"><span data-stu-id="a7424-114">**Subscription requests (requiring approval)** - hello specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="a7424-115">**Nieuwe abonnementen** - Hallo opgegeven e-mailontvangers en e-mailmeldingen over nieuwe abonnementen voor API-product ontvangt de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a7424-115">**New subscriptions** - hello specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="a7424-116">**Galerie toepassingsaanvragen** - Hallo opgegeven e-mailontvangers en gebruikers e-mailmeldingen ontvangen wanneer nieuwe toepassingen ingediend toohello-toepassingsgalerie zijn.</span><span class="sxs-lookup"><span data-stu-id="a7424-116">**Application gallery requests** - hello specified email recipients and users will receive email notifications when new applications are submitted toohello application gallery.</span></span>
* <span data-ttu-id="a7424-117">**BCC** - Hallo opgegeven e-mailontvangers en blind kopie van alle e-mailberichten verzonden toodevelopers e-mailbericht ontvangt de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a7424-117">**BCC** - hello specified email recipients and users will receive email blind carbon copies of all emails sent toodevelopers.</span></span>
* <span data-ttu-id="a7424-118">**Nieuwe probleem of opmerking** - Hallo opgegeven e-mailontvangers en e-mailmeldingen wanneer een nieuw probleem ontvangt de gebruiker of opmerking wordt ingediend op Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="a7424-118">**New issue or comment** - hello specified email recipients and users will receive email notifications when a new issue or comment is submitted on hello developer portal.</span></span>
* <span data-ttu-id="a7424-119">**Account sluiten bericht** - Hallo opgegeven e-mailontvangers en gebruikers e-mailmeldingen ontvangen wanneer een account wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="a7424-119">**Close account message** - hello specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="a7424-120">**Bijna abonnement quotumlimiet** - Hallo e-mailontvangers te volgen en ontvangen gebruikers e-mailmeldingen wanneer abonnement gebruik sluiten toousage quotum opgehaald.</span><span class="sxs-lookup"><span data-stu-id="a7424-120">**Approaching subscription quota limit** - hello following email recipients and users will receive email notifications when subscription usage gets close toousage quota.</span></span>

<span data-ttu-id="a7424-121">Voor elke gebeurtenis kunt u e-mailontvangers Hallo e-mailadres tekstvak met opgeven of u gebruikers kunt kiezen uit een lijst.</span><span class="sxs-lookup"><span data-stu-id="a7424-121">For each event, you can specify email recipients using hello email address text box or you can select users from a list.</span></span>

<span data-ttu-id="a7424-122">toospecify Hallo e-mailadressen toobe gewaarschuwd, ze in het tekstvak voor Hallo e-mailadres invoeren.</span><span class="sxs-lookup"><span data-stu-id="a7424-122">toospecify hello email addresses toobe notified, enter them in hello email address text box.</span></span> <span data-ttu-id="a7424-123">Als er meerdere e-mailadressen, scheiden met komma's.</span><span class="sxs-lookup"><span data-stu-id="a7424-123">If you have multiple email addresses, separate them using commas.</span></span>

![Geadresseerden voor meldingen][api-management-email-addresses]

<span data-ttu-id="a7424-125">toospecify hello gebruikers toobe melding ontvangt, klikt u op **ontvanger toevoegen**Hallo selectievakje naast Hallo gebruikers toobe gewaarschuwd en klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a7424-125">toospecify hello users toobe notified, click **add recipient**, check hello box beside hello users toobe notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="a7424-126">Alleen beheerders worden in Hallo lijst weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a7424-126">Only administrators are displayed in hello list.</span></span>


<span data-ttu-id="a7424-127">Klik na het configureren van de ontvangers van meldingen Hallo **opslaan** tooapply Hallo bijgewerkt geadresseerden voor meldingen.</span><span class="sxs-lookup"><span data-stu-id="a7424-127">After configuring hello notification recipients, click **Save** tooapply hello updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="a7424-128">Als u Hallo verlaat **Publisher meldingen** tabblad Hallo publicatieportal waarschuwt u als er niet-opgeslagen wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="a7424-128">If you navigate away from hello **Publisher Notifications** tab hello publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="a7424-129"><a name="email-templates"></a>E-mailsjablonen configureren</span><span class="sxs-lookup"><span data-stu-id="a7424-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="a7424-130">API Management biedt e-mailsjablonen voor Hallo e-mailberichten die worden verzonden in Hallo verloop van beheer en Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="a7424-130">API Management provides email templates for hello email messages that are sent in hello course of administering and using hello service.</span></span> <span data-ttu-id="a7424-131">Hallo volgende e-mailsjablonen worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="a7424-131">hello following email templates are provided.</span></span>

* <span data-ttu-id="a7424-132">Toepassing galerie inzending is goedgekeurd</span><span class="sxs-lookup"><span data-stu-id="a7424-132">Application gallery submission approved</span></span>
* <span data-ttu-id="a7424-133">Ontwikkelaars afscheidstekst letter</span><span class="sxs-lookup"><span data-stu-id="a7424-133">Developer farewell letter</span></span>
* <span data-ttu-id="a7424-134">Ontwikkelaars quotalimiet bijna melding</span><span class="sxs-lookup"><span data-stu-id="a7424-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="a7424-135">Gebruiker uitnodigen</span><span class="sxs-lookup"><span data-stu-id="a7424-135">Invite user</span></span>
* <span data-ttu-id="a7424-136">Nieuwe opmerking toegevoegd tooan probleem</span><span class="sxs-lookup"><span data-stu-id="a7424-136">New comment added tooan issue</span></span>
* <span data-ttu-id="a7424-137">Nieuwe probleem ontvangen</span><span class="sxs-lookup"><span data-stu-id="a7424-137">New issue received</span></span>
* <span data-ttu-id="a7424-138">Nieuw abonnement geactiveerd</span><span class="sxs-lookup"><span data-stu-id="a7424-138">New subscription activated</span></span>
* <span data-ttu-id="a7424-139">Abonnement wordt verlengd bevestigen</span><span class="sxs-lookup"><span data-stu-id="a7424-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="a7424-140">Abonnementaanvraag heeft geweigerd</span><span class="sxs-lookup"><span data-stu-id="a7424-140">Subscription request declines</span></span>
* <span data-ttu-id="a7424-141">Abonnementaanvraag ontvangen</span><span class="sxs-lookup"><span data-stu-id="a7424-141">Subscription request received</span></span>

<span data-ttu-id="a7424-142">Deze sjablonen kunnen worden gewijzigd naar wens.</span><span class="sxs-lookup"><span data-stu-id="a7424-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="a7424-143">tooview en e-mailsjablonen Hallo voor uw exemplaar van API Management configureren, klikt u op **meldingen** van Hallo **API Management** menu op Hallo links en selecteer Hallo **e-mailsjablonen**  tabblad.</span><span class="sxs-lookup"><span data-stu-id="a7424-143">tooview and configure hello email templates for your API Management instance, click **Notifications** from hello **API Management** menu on hello left, and select hello **Email Templates** tab.</span></span>

![E-mailsjablonen][api-management-email-templates]

<span data-ttu-id="a7424-145">tooview of een specifieke sjabloon niet wijzigen, selecteert u deze in Hallo **sjablonen** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="a7424-145">tooview or modify a specific template, select it from hello **Templates** drop-down list.</span></span>

![E-Sjabloonlijst][api-management-email-templates-list]

<span data-ttu-id="a7424-147">Elk e-mailsjabloon heeft een onderwerp als tekst zonder opmaak en de definitie van een instantie in HTML-indeling.</span><span class="sxs-lookup"><span data-stu-id="a7424-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="a7424-148">Elk item kan worden aangepast naar wens.</span><span class="sxs-lookup"><span data-stu-id="a7424-148">Each item can be customized as desired.</span></span>

![Editor voor e-sjabloon][api-management-email-template]

<span data-ttu-id="a7424-150">Hallo **Parameters** lijst bevat een lijst met parameters, die tijdens ingevoegd in Hallo onderwerp of de hoofdtekst, vervangen Hallo aangewezen waarde wanneer Hallo e-mailbericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="a7424-150">hello **Parameters** list contains a list of parameters, which when inserted into hello subject or body, will be replaced hello designated value when hello email is sent.</span></span> <span data-ttu-id="a7424-151">een parameter tooinsert Hallo cursor waarin u wilt Hallo parameter toogo en klikt u op Hallo pijl toohello links van de parameternaam Hallo plaatsen.</span><span class="sxs-lookup"><span data-stu-id="a7424-151">tooinsert a parameter, place hello cursor where you wish hello parameter toogo, and click hello arrow toohello left of hello parameter name.</span></span>

<span data-ttu-id="a7424-152">Klik op **Preview** of **een test verzenden** toosee hoe Hallo e wordt zoeken of een testbericht verzenden.</span><span class="sxs-lookup"><span data-stu-id="a7424-152">Click **Preview** or **Send a test** toosee how hello email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="a7424-153">Hallo-parameters zijn niet vervangen door feitelijke waarden wanneer een voorbeeldweergave of een test verzenden.</span><span class="sxs-lookup"><span data-stu-id="a7424-153">hello parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="a7424-154">toosave hello wijzigingen toohello e-mailsjabloon, klikt u op **opslaan**, of toocancel Hallo wijzigingen, klikt u op **annuleren**.</span><span class="sxs-lookup"><span data-stu-id="a7424-154">toosave hello changes toohello email template, click **Save**, or toocancel hello changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
