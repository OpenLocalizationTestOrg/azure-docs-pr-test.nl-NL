---
title: Meldingen configureren en e-mailsjablonen in Azure API Management | Microsoft Docs
description: Informatie over het configureren van meldingen en e-mailsjablonen in Azure API Management.
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
ms.openlocfilehash: 3d8b74e32059cfc1a4c3a8fc7d3bd04676ee80c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="490de-103">Meldingen en e-mailsjablonen configureren in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="490de-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="490de-104">API Management biedt de mogelijkheid voor het configureren van meldingen voor specifieke gebeurtenissen en de e-mailsjablonen die worden gebruikt om te communiceren met de beheerders en ontwikkelaars van exemplaar van API Management configureren.</span><span class="sxs-lookup"><span data-stu-id="490de-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="490de-105">Dit onderwerp wordt beschreven hoe u meldingen configureren voor de gebeurtenissen beschikbaar en biedt een overzicht van de configuratie van de e-mailsjablonen gebruikt deze gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="490de-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <span data-ttu-id="490de-106"><a name="publisher-notifications"></a>Publisher meldingen configureren</span><span class="sxs-lookup"><span data-stu-id="490de-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="490de-107">Meldingen configureren, klikt u op **publicatieportal** in de Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="490de-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="490de-108">Hiermee gaat u naar de publicatieportal van API Management.</span><span class="sxs-lookup"><span data-stu-id="490de-108">This takes you to the API Management publisher portal.</span></span>

![Publicatieportal][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="490de-110">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="490de-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="490de-111">Klik op **meldingen** van de **API Management** menu aan de linkerkant om de beschikbare meldingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="490de-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span></span>

![Meldingen van de uitgever][api-management-publisher-notifications]

<span data-ttu-id="490de-113">De volgende lijst met gebeurtenissen kan worden geconfigureerd voor meldingen.</span><span class="sxs-lookup"><span data-stu-id="490de-113">The following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="490de-114">**Verzoeken om abonnementen (goedkeuring wordt vereist)** -ontvangt de opgegeven e-mailontvangers en gebruikers e-mailmeldingen over verzoeken om abonnementen voor API-producten goedkeuring wordt vereist.</span><span class="sxs-lookup"><span data-stu-id="490de-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="490de-115">**Nieuwe abonnementen** -ontvangt de opgegeven e-mailontvangers en gebruikers e-mailmeldingen over nieuwe abonnementen voor API-product.</span><span class="sxs-lookup"><span data-stu-id="490de-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="490de-116">**Galerie toepassingsaanvragen** -de opgegeven e-mailontvangers en gebruikers worden e-mailmeldingen ontvangen wanneer nieuwe toepassingen worden verzonden naar de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="490de-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
* <span data-ttu-id="490de-117">**BCC** -ontvangt de opgegeven e-mailontvangers en gebruikers e-mailbericht blind kopie van alle e-mails worden verzonden voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="490de-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
* <span data-ttu-id="490de-118">**Nieuwe probleem of opmerking** : het opgegeven e-mailontvangers en gebruikers e-mailmeldingen wanneer een nieuw actie-item ontvangen of opmerking wordt ingediend op de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="490de-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
* <span data-ttu-id="490de-119">**Account sluiten bericht** -de opgegeven e-mailontvangers en gebruikers worden e-mailmeldingen ontvangen wanneer een account wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="490de-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="490de-120">**Bijna abonnement quotumlimiet** -de volgende e-mailontvangers en gebruikers worden e-mailmeldingen ontvangen wanneer abonnement gebruik bijna gebruiksquotum opgehaald.</span><span class="sxs-lookup"><span data-stu-id="490de-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

<span data-ttu-id="490de-121">Voor elke gebeurtenis, kunt u e-mailontvangers in het tekstvak voor e-mailadres opgeven of u gebruikers kunt kiezen uit een lijst.</span><span class="sxs-lookup"><span data-stu-id="490de-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

<span data-ttu-id="490de-122">Als u de e-mailadressen moeten ontvangen, moet u deze in het tekstvak e-mailadres invoeren.</span><span class="sxs-lookup"><span data-stu-id="490de-122">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="490de-123">Als er meerdere e-mailadressen, scheiden met komma's.</span><span class="sxs-lookup"><span data-stu-id="490de-123">If you have multiple email addresses, separate them using commas.</span></span>

![Geadresseerden voor meldingen][api-management-email-addresses]

<span data-ttu-id="490de-125">Geef de gebruikers om te worden geïnformeerd, klikt u op **ontvanger toevoegen**, schakel het selectievakje in naast de gebruikers een melding en klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="490de-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="490de-126">Alleen beheerders worden weergegeven in de lijst.</span><span class="sxs-lookup"><span data-stu-id="490de-126">Only administrators are displayed in the list.</span></span>


<span data-ttu-id="490de-127">Klik na het configureren van de ontvangers van meldingen op **opslaan** om toe te passen de bijgewerkte melding geadresseerden.</span><span class="sxs-lookup"><span data-stu-id="490de-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="490de-128">Als u de navigatiefunctie weg van de **Publisher meldingen** tabblad de publicatieportal waarschuwt u als er niet-opgeslagen wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="490de-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="490de-129"><a name="email-templates"></a>E-mailsjablonen configureren</span><span class="sxs-lookup"><span data-stu-id="490de-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="490de-130">E-mailsjablonen biedt API Management voor de e-mailberichten die worden verzonden in de loop van beheer en het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="490de-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="490de-131">De volgende e-mailsjablonen worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="490de-131">The following email templates are provided.</span></span>

* <span data-ttu-id="490de-132">Toepassing galerie inzending is goedgekeurd</span><span class="sxs-lookup"><span data-stu-id="490de-132">Application gallery submission approved</span></span>
* <span data-ttu-id="490de-133">Ontwikkelaars afscheidstekst letter</span><span class="sxs-lookup"><span data-stu-id="490de-133">Developer farewell letter</span></span>
* <span data-ttu-id="490de-134">Ontwikkelaars quotalimiet bijna melding</span><span class="sxs-lookup"><span data-stu-id="490de-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="490de-135">Gebruiker uitnodigen</span><span class="sxs-lookup"><span data-stu-id="490de-135">Invite user</span></span>
* <span data-ttu-id="490de-136">Nieuwe opmerking toegevoegd aan een probleem</span><span class="sxs-lookup"><span data-stu-id="490de-136">New comment added to an issue</span></span>
* <span data-ttu-id="490de-137">Nieuwe probleem ontvangen</span><span class="sxs-lookup"><span data-stu-id="490de-137">New issue received</span></span>
* <span data-ttu-id="490de-138">Nieuw abonnement geactiveerd</span><span class="sxs-lookup"><span data-stu-id="490de-138">New subscription activated</span></span>
* <span data-ttu-id="490de-139">Abonnement wordt verlengd bevestigen</span><span class="sxs-lookup"><span data-stu-id="490de-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="490de-140">Abonnementaanvraag heeft geweigerd</span><span class="sxs-lookup"><span data-stu-id="490de-140">Subscription request declines</span></span>
* <span data-ttu-id="490de-141">Abonnementaanvraag ontvangen</span><span class="sxs-lookup"><span data-stu-id="490de-141">Subscription request received</span></span>

<span data-ttu-id="490de-142">Deze sjablonen kunnen worden gewijzigd naar wens.</span><span class="sxs-lookup"><span data-stu-id="490de-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="490de-143">Als u wilt weergeven en configureren van de e-mailsjablonen voor uw API Management-exemplaar, klikt u op **meldingen** van de **API Management** menu aan de linkerkant en selecteer de **e-mailsjablonen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="490de-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span></span>

![E-mailsjablonen][api-management-email-templates]

<span data-ttu-id="490de-145">Als u wilt bekijken of wijzigen van een specifieke sjabloon, selecteert u dit in de **sjablonen** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="490de-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span></span>

![E-Sjabloonlijst][api-management-email-templates-list]

<span data-ttu-id="490de-147">Elk e-mailsjabloon heeft een onderwerp als tekst zonder opmaak en de definitie van een instantie in HTML-indeling.</span><span class="sxs-lookup"><span data-stu-id="490de-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="490de-148">Elk item kan worden aangepast naar wens.</span><span class="sxs-lookup"><span data-stu-id="490de-148">Each item can be customized as desired.</span></span>

![Editor voor e-sjabloon][api-management-email-template]

<span data-ttu-id="490de-150">De **Parameters** lijst bevat een lijst met parameters, die tijdens ingevoegd in het onderwerp of de hoofdtekst, worden de opgegeven waarde wordt vervangen als het e-mailbericht wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="490de-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="490de-151">Als u wilt invoegen een parameter, plaats de cursor waar u wilt dat de parameter om te gaan en klik op de pijl naar links van de parameternaam van de.</span><span class="sxs-lookup"><span data-stu-id="490de-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

<span data-ttu-id="490de-152">Klik op **Preview** of **een test verzenden** om te zien hoe het e-mailbericht wordt zoeken of een testbericht verzenden.</span><span class="sxs-lookup"><span data-stu-id="490de-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="490de-153">De parameters worden niet vervangen door feitelijke waarden wanneer een voorbeeldweergave of verzenden van een test.</span><span class="sxs-lookup"><span data-stu-id="490de-153">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="490de-154">Sla de wijzigingen in het e-mailsjabloon, klikt u op **opslaan**, of het wijzigingen klikt u op Annuleren **annuleren**.</span><span class="sxs-lookup"><span data-stu-id="490de-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
