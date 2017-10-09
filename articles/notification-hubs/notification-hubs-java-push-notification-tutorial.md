---
title: aaaHow toouse Notification Hubs met behulp van Java
description: Meer informatie over hoe toouse Azure Notification Hubs vanuit een Java-back-end.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a><span data-ttu-id="6811f-103">Hoe toouse Notification Hubs met Java</span><span class="sxs-lookup"><span data-stu-id="6811f-103">How toouse Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="6811f-104">Dit onderwerp wordt beschreven Hallo belangrijke functies van nieuwe volledig ondersteund Hallo officiële Azure Notification Hub Java SDK.</span><span class="sxs-lookup"><span data-stu-id="6811f-104">This topic describes hello key features of hello new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="6811f-105">Dit is een open source-project en kunt u het volledige SDK code op Hallo weergeven [Java SDK].</span><span class="sxs-lookup"><span data-stu-id="6811f-105">This is an open source project and you can view hello entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="6811f-106">In het algemeen kunt u toegang hebt tot alle functies van de Notification Hubs vanuit back-end van een Java/PHP/Python/Ruby Hallo Notification Hub REST-interface gebruiken, zoals beschreven in de MSDN-onderwerp Hallo [Notification Hubs REST-API's](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="6811f-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="6811f-107">Deze SDK voor Java biedt een thin wrapper via deze interfaces REST in Java.</span><span class="sxs-lookup"><span data-stu-id="6811f-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="6811f-108">Hallo ondersteunt SDK momenteel:</span><span class="sxs-lookup"><span data-stu-id="6811f-108">hello SDK supports currently:</span></span>

* <span data-ttu-id="6811f-109">CRUD op Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="6811f-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="6811f-110">CRUD op registraties</span><span class="sxs-lookup"><span data-stu-id="6811f-110">CRUD on Registrations</span></span>
* <span data-ttu-id="6811f-111">Installatie-Management</span><span class="sxs-lookup"><span data-stu-id="6811f-111">Installation Management</span></span>
* <span data-ttu-id="6811f-112">Registraties voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="6811f-112">Import/Export Registrations</span></span>
* <span data-ttu-id="6811f-113">Reguliere verzendt</span><span class="sxs-lookup"><span data-stu-id="6811f-113">Regular Sends</span></span>
* <span data-ttu-id="6811f-114">Geplande verzendt</span><span class="sxs-lookup"><span data-stu-id="6811f-114">Scheduled Sends</span></span>
* <span data-ttu-id="6811f-115">Asynchrone bewerkingen via Java NIO</span><span class="sxs-lookup"><span data-stu-id="6811f-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="6811f-116">Ondersteunde platforms: APNS (iOS), GCM (Android), WNS (Windows Store-apps), MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android zonder Google-services)</span><span class="sxs-lookup"><span data-stu-id="6811f-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="6811f-117">Gebruik van de SDK</span><span class="sxs-lookup"><span data-stu-id="6811f-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="6811f-118">Compileren en bouwen</span><span class="sxs-lookup"><span data-stu-id="6811f-118">Compile and build</span></span>
<span data-ttu-id="6811f-119">Gebruik [Maven]</span><span class="sxs-lookup"><span data-stu-id="6811f-119">Use [Maven]</span></span>

<span data-ttu-id="6811f-120">toobuild:</span><span class="sxs-lookup"><span data-stu-id="6811f-120">toobuild:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="6811f-121">Code</span><span class="sxs-lookup"><span data-stu-id="6811f-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="6811f-122">Notification Hub CRUDs</span><span class="sxs-lookup"><span data-stu-id="6811f-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="6811f-123">**Maak een NamespaceManager:**</span><span class="sxs-lookup"><span data-stu-id="6811f-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="6811f-124">**Notification Hub maken:**</span><span class="sxs-lookup"><span data-stu-id="6811f-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="6811f-125">OF</span><span class="sxs-lookup"><span data-stu-id="6811f-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="6811f-126">**Haal de Notification Hub:**</span><span class="sxs-lookup"><span data-stu-id="6811f-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="6811f-127">**Notification Hub werken:**</span><span class="sxs-lookup"><span data-stu-id="6811f-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="6811f-128">**Verwijderen van Notification Hub:**</span><span class="sxs-lookup"><span data-stu-id="6811f-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="6811f-129">Registratie CRUDs</span><span class="sxs-lookup"><span data-stu-id="6811f-129">Registration CRUDs</span></span>
<span data-ttu-id="6811f-130">**Maak een Notification Hub-client:**</span><span class="sxs-lookup"><span data-stu-id="6811f-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="6811f-131">**Maak de registratie van Windows:**</span><span class="sxs-lookup"><span data-stu-id="6811f-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="6811f-132">**IOS-registratie maken:**</span><span class="sxs-lookup"><span data-stu-id="6811f-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="6811f-133">U kunt ook registraties maken voor Android (GCM), Windows Phone (MPNS) en Kindle Fire (ADM).</span><span class="sxs-lookup"><span data-stu-id="6811f-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="6811f-134">**Sjabloon registraties maken:**</span><span class="sxs-lookup"><span data-stu-id="6811f-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="6811f-135">**Registraties maken met behulp van maken registrationid + upsert patroon**</span><span class="sxs-lookup"><span data-stu-id="6811f-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="6811f-136">Hiermee verwijdert u duplicaten vanwege tooany verloren antwoorden als registratie-id's worden opgeslagen op Hallo apparaat:</span><span class="sxs-lookup"><span data-stu-id="6811f-136">Removes duplicates due tooany lost responses if storing registration ids on hello device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="6811f-137">**Registraties bijwerken:**</span><span class="sxs-lookup"><span data-stu-id="6811f-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="6811f-138">**Registraties verwijderen:**</span><span class="sxs-lookup"><span data-stu-id="6811f-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="6811f-139">**Query-registraties:**</span><span class="sxs-lookup"><span data-stu-id="6811f-139">**Query registrations:**</span></span>

* <span data-ttu-id="6811f-140">**Afzonderlijke registratie ophalen:**</span><span class="sxs-lookup"><span data-stu-id="6811f-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="6811f-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="6811f-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="6811f-142">**Haal alle registraties in hub:**</span><span class="sxs-lookup"><span data-stu-id="6811f-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="6811f-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="6811f-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="6811f-144">**Registraties met code ophalen:**</span><span class="sxs-lookup"><span data-stu-id="6811f-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="6811f-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="6811f-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="6811f-146">**Haal registraties door kanaal:**</span><span class="sxs-lookup"><span data-stu-id="6811f-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="6811f-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="6811f-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="6811f-148">Alle query's ondersteunen $top en voortzetting tokens.</span><span class="sxs-lookup"><span data-stu-id="6811f-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="6811f-149">Gebruik API-installatie</span><span class="sxs-lookup"><span data-stu-id="6811f-149">Installation API usage</span></span>
<span data-ttu-id="6811f-150">API-installatie is een alternatief mechanisme voor het beheer van de registratie.</span><span class="sxs-lookup"><span data-stu-id="6811f-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="6811f-151">In plaats van meerdere registraties die niet is heel eenvoudig en gemakkelijk kan worden gedaan ten onrechte of inefficiënt onderhouden, is het nu mogelijk toouse een installatie van één object.</span><span class="sxs-lookup"><span data-stu-id="6811f-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible toouse a SINGLE Installation object.</span></span> <span data-ttu-id="6811f-152">Installatie bevat alles wat u nodig: push-kanaal (apparaattoken), tags, sjablonen, secundaire tegels (voor WNS en APNS).</span><span class="sxs-lookup"><span data-stu-id="6811f-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="6811f-153">U niet meer nodig hebt toocall Hallo service tooget Id - NET GUID of een andere id genereren, op apparaat behouden en verzenden tooyour back-end samen met push-kanaal (apparaattoken).</span><span class="sxs-lookup"><span data-stu-id="6811f-153">You don't need toocall hello service tooget Id anymore - just generate GUID or any other identifier, keep it on device and send tooyour backend together with push channel (device token).</span></span> <span data-ttu-id="6811f-154">Op Hallo back-end moet u slechts één aanroep doen: CreateOrUpdateInstallation, is volledig idempotent, dus u kunt gratis tooretry indien nodig.</span><span class="sxs-lookup"><span data-stu-id="6811f-154">On hello backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free tooretry if needed.</span></span>

<span data-ttu-id="6811f-155">Als voorbeeld voor Amazon Kindle Fire als volgt uitziet:</span><span class="sxs-lookup"><span data-stu-id="6811f-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="6811f-156">Als u wilt dat tooupdate het:</span><span class="sxs-lookup"><span data-stu-id="6811f-156">If you want tooupdate it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="6811f-157">Voor geavanceerde scenario's hebben we gedeeltelijke updatefunctie waarmee toomodify alleen bepaalde eigenschappen van het Hallo-installatie-object.</span><span class="sxs-lookup"><span data-stu-id="6811f-157">For advanced scenarios we have partial update capability which allows toomodify only particular properties of hello installation object.</span></span> <span data-ttu-id="6811f-158">Gedeeltelijke update is in feite subset van JSON-Patch-bewerkingen die u met de installatie-object uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="6811f-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="6811f-159">Verwijder de installatie:</span><span class="sxs-lookup"><span data-stu-id="6811f-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="6811f-160">CreateOrUpdate, Patch en Delete zijn uiteindelijk consistent is met Get.</span><span class="sxs-lookup"><span data-stu-id="6811f-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="6811f-161">De aangevraagde bewerking NET toohello wachtrij van het systeem tijdens de oproep Hallo gaat en wordt uitgevoerd op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="6811f-161">Your requested operation just goes toohello system queue during hello call and will be executed in background.</span></span> <span data-ttu-id="6811f-162">Houd er rekening mee dat Get is niet ontworpen voor belangrijkste runtime-scenario, maar alleen voor foutopsporing en het oplossen van problemen, het is nauw beperkt door Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="6811f-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by hello service.</span></span>

<span data-ttu-id="6811f-163">Werkstroom voor verzenden voor installaties is hetzelfde als Hallo voor registraties.</span><span class="sxs-lookup"><span data-stu-id="6811f-163">Send flow for Installations is hello same as for Registrations.</span></span> <span data-ttu-id="6811f-164">Er zijn een optie tootarget melding toohello net hebt geïntroduceerd specifieke installatie - alleen gebruik tag ' omwille van: {desired-id} '.</span><span class="sxs-lookup"><span data-stu-id="6811f-164">We've just introduced an option tootarget notification toohello particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="6811f-165">Voor de bovenstaande eruit deze als volgt:</span><span class="sxs-lookup"><span data-stu-id="6811f-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="6811f-166">Voor een van de verschillende sjablonen:</span><span class="sxs-lookup"><span data-stu-id="6811f-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="6811f-167">Meldingen (beschikbaar voor STANDARD-laag) plannen</span><span class="sxs-lookup"><span data-stu-id="6811f-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="6811f-168">Hallo dezelfde als reguliere verzenden, maar met één extra parameter - scheduledTime die aangeeft wanneer de melding moet worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="6811f-168">hello same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="6811f-169">Service accepteert elk punt in tijd tussen nu + 5 minuten en nu + 7 dagen.</span><span class="sxs-lookup"><span data-stu-id="6811f-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="6811f-170">**Plannen van een systeemeigen Windows-melding:**</span><span class="sxs-lookup"><span data-stu-id="6811f-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="6811f-171">(Beschikbaar voor de prijscategorie STANDARD) voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="6811f-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="6811f-172">Soms is het vereiste tooperform bulkbewerking tegen registraties.</span><span class="sxs-lookup"><span data-stu-id="6811f-172">Sometimes it is required tooperform bulk operation against registrations.</span></span> <span data-ttu-id="6811f-173">Meestal is voor de integratie met een ander systeem of alleen een enorme fix toosay update Hallo-tags.</span><span class="sxs-lookup"><span data-stu-id="6811f-173">Usually it is for integration with another system or just a massive fix toosay update hello tags.</span></span> <span data-ttu-id="6811f-174">Het verdient sterk niet toouse stroom Get of bij te werken als we duizenden registraties bedoelen.</span><span class="sxs-lookup"><span data-stu-id="6811f-174">It is strongly not recommended toouse Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="6811f-175">Import/Export-functie is ontworpen toocover Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="6811f-175">Import/Export capability is designed toocover hello scenario.</span></span> <span data-ttu-id="6811f-176">In feite bieden u een toegang toosome blob-container onder uw storage-account als een bron van binnenkomende gegevens en de locatie voor de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6811f-176">Basically you provide an access toosome blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="6811f-177">**Taak voor het exporteren verzenden:**</span><span class="sxs-lookup"><span data-stu-id="6811f-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="6811f-178">**Import-taak verzenden:**</span><span class="sxs-lookup"><span data-stu-id="6811f-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="6811f-179">**Wacht totdat de taak wordt uitgevoerd:**</span><span class="sxs-lookup"><span data-stu-id="6811f-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="6811f-180">**Alle taken ophalen:**</span><span class="sxs-lookup"><span data-stu-id="6811f-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="6811f-181">**URI met SAS-handtekening:** dit Hallo-URL van een aantal blob-bestand of de blob-container plus set parameters zoals machtigingen en verlooptijd plus handtekening van deze dingen die zijn gemaakt met behulp van account-SAS-sleutel is.</span><span class="sxs-lookup"><span data-stu-id="6811f-181">**URI with SAS signature:** This is hello URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="6811f-182">Azure Storage Java SDK heeft geavanceerde mogelijkheden, waaronder het maken van dergelijke soort URI's.</span><span class="sxs-lookup"><span data-stu-id="6811f-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="6811f-183">U kunt als alternatief voor eenvoudige kijken ImportExportE2E test klasse (van Hallo github locatie) met zeer basic en compact uitvoering van handtekeningalgoritme nemen.</span><span class="sxs-lookup"><span data-stu-id="6811f-183">As simple alternative you can take a look at ImportExportE2E test class (from hello github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="6811f-184">Meldingen verzenden</span><span class="sxs-lookup"><span data-stu-id="6811f-184">Send Notifications</span></span>
<span data-ttu-id="6811f-185">Hallo melding object is gewoon een instantie met kopteksten, bepaalde hulpprogrammamethoden voor het helpen bij het bouwen van Hallo systeemeigen en sjabloon meldingen objecten.</span><span class="sxs-lookup"><span data-stu-id="6811f-185">hello Notification object is simply a body with headers, some utility methods help in building hello native and template notifications objects.</span></span>

* <span data-ttu-id="6811f-186">**Windows Store en Windows Phone 8.1 (zonder Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="6811f-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="6811f-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="6811f-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="6811f-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="6811f-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="6811f-189">**Windows Phone 8.0 en 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="6811f-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="6811f-190">**Fire kindle**</span><span class="sxs-lookup"><span data-stu-id="6811f-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="6811f-191">**TooTags verzenden**</span><span class="sxs-lookup"><span data-stu-id="6811f-191">**Send tooTags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="6811f-192">**De expressie tootag verzenden**</span><span class="sxs-lookup"><span data-stu-id="6811f-192">**Send tootag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="6811f-193">**Sjabloon melding verzenden**</span><span class="sxs-lookup"><span data-stu-id="6811f-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="6811f-194">Uw Java-code wordt uitgevoerd, moet u een melding weergegeven op het doelapparaat nu produceren.</span><span class="sxs-lookup"><span data-stu-id="6811f-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="6811f-195"><a name="next-steps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6811f-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="6811f-196">In dit onderwerp we hebt u geleerd hoe toocreate een eenvoudige Java REST-client voor Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="6811f-196">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="6811f-197">Hier kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="6811f-197">From here you can:</span></span>

* <span data-ttu-id="6811f-198">Hallo volledige downloaden [Java SDK], die Hallo gehele SDK-code bevat.</span><span class="sxs-lookup"><span data-stu-id="6811f-198">Download hello full [Java SDK], which contains hello entire SDK code.</span></span> 
* <span data-ttu-id="6811f-199">Spelen met Hallo voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="6811f-199">Play with hello samples:</span></span>
  * <span data-ttu-id="6811f-200">[Aan de slag met Notification Hubs]</span><span class="sxs-lookup"><span data-stu-id="6811f-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="6811f-201">[Belangrijk nieuws te verzenden]</span><span class="sxs-lookup"><span data-stu-id="6811f-201">[Send breaking news]</span></span>
  * <span data-ttu-id="6811f-202">[Gelokaliseerde belangrijk nieuws te verzenden]</span><span class="sxs-lookup"><span data-stu-id="6811f-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="6811f-203">[Meldingen verzenden tooauthenticated gebruikers]</span><span class="sxs-lookup"><span data-stu-id="6811f-203">[Send notifications tooauthenticated users]</span></span>
  * <span data-ttu-id="6811f-204">[Verzenden van meldingen van de platformoverschrijdende tooauthenticated gebruikers]</span><span class="sxs-lookup"><span data-stu-id="6811f-204">[Send cross-platform notifications tooauthenticated users]</span></span>

[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Aan de slag met Notification Hubs]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Belangrijk nieuws te verzenden]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Gelokaliseerde belangrijk nieuws te verzenden]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Meldingen verzenden tooauthenticated gebruikers]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Verzenden van meldingen van de platformoverschrijdende tooauthenticated gebruikers]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

