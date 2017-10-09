---
title: aaaHow tooUse Hallo Engagement API voor iOS
description: Meest recente iOS SDK - hoe tooUse Engagement API Hallo op iOS
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a><span data-ttu-id="323c9-103">Hoe tooUse Engagement API Hallo op iOS</span><span class="sxs-lookup"><span data-stu-id="323c9-103">How tooUse hello Engagement API on iOS</span></span>
<span data-ttu-id="323c9-104">Dit document is een invoegtoepassing toohello document hoe tooIntegrate Engagement voor iOS: biedt diepte meer informatie over hoe toouse Hallo Engagement API tooreport de toepassingsstatistieken van uw.</span><span class="sxs-lookup"><span data-stu-id="323c9-104">This document is an add-on toohello document How tooIntegrate Engagement on iOS: it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="323c9-105">Houd er rekening mee dat als u alleen Engagement tooreport van uw toepassing sessies, activiteiten, crashes en technische informatie, Hallo eenvoudigste manier is toomake alle uw aangepaste `UIViewController` objecten overnemen van Hallo overeenkomt `EngagementViewController` klasse .</span><span class="sxs-lookup"><span data-stu-id="323c9-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your custom `UIViewController` objects inherit from hello corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="323c9-106">Als u wilt meer, bijvoorbeeld als u tooreport toepassing specifieke gebeurtenissen, fouten en taken moet toodo, of als er tooreport activiteiten van uw toepassing in een andere manier dan een geïmplementeerd in Hallo Hallo `EngagementViewController` klassen, moet u toouse Hallo Engagement API.</span><span class="sxs-lookup"><span data-stu-id="323c9-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementViewController` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="323c9-107">Hallo Engagement API geleverd door Hallo `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="323c9-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="323c9-108">Een exemplaar van deze klasse kan worden opgehaald door de aanroepende Hallo `[EngagementAgent shared]` statische methode (Houd er rekening mee dat Hallo `EngagementAgent` object dat wordt geretourneerd is een singleton).</span><span class="sxs-lookup"><span data-stu-id="323c9-108">An instance of this class can be retrieved by calling hello `[EngagementAgent shared]` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="323c9-109">Voordat u een API-aanroepen, hello `EngagementAgent` object moet geïnitialiseerd zijn door het Hallo-methode aanroepen`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="323c9-109">Before any API calls, hello `EngagementAgent` object must be initialized by calling hello method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="323c9-110">Engagement-concepten</span><span class="sxs-lookup"><span data-stu-id="323c9-110">Engagement concepts</span></span>
<span data-ttu-id="323c9-111">Hallo volgende delen verfijnen Hallo algemene [Mobile Engagement-concepten](mobile-engagement-concepts.md) voor Hallo iOS-platform.</span><span class="sxs-lookup"><span data-stu-id="323c9-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="323c9-112">`Session` en `Activity`</span><span class="sxs-lookup"><span data-stu-id="323c9-112">`Session` and `Activity`</span></span>
<span data-ttu-id="323c9-113">Een *activiteit* wordt meestal veroorzaakt door een scherm van de toepassing hello, die toosay hello *activiteit* wordt gestart wanneer het welkomstscherm wordt weergegeven en stopt wanneer welkomstscherm is gesloten: dit is Hallo case wanneer Hallo is Engagement SDK geïntegreerd met behulp van Hallo `EngagementViewController` klassen.</span><span class="sxs-lookup"><span data-stu-id="323c9-113">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementViewController` classes.</span></span>

<span data-ttu-id="323c9-114">Maar *activiteiten* kunnen ook handmatig met behulp van Hallo Engagement API worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="323c9-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="323c9-115">Hierdoor kunnen een bepaald scherm toosplit in verschillende sub delen tooget meer informatie over Hallo informatie over het gebruik van dit scherm (bijvoorbeeld hoe vaak tooknown en hoe lang dialoogvensters worden gebruikt in dit scherm).</span><span class="sxs-lookup"><span data-stu-id="323c9-115">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="323c9-116">Rapportage</span><span class="sxs-lookup"><span data-stu-id="323c9-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="323c9-117">Gebruiker start een nieuwe activiteit</span><span class="sxs-lookup"><span data-stu-id="323c9-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="323c9-118">U moet toocall `startActivity()` elke activiteit tijd Hallo gebruiker wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="323c9-118">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="323c9-119">Hallo eerste aanroep toothis functie wordt een nieuwe gebruikerssessie gestart.</span><span class="sxs-lookup"><span data-stu-id="323c9-119">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="323c9-120">Gebruiker eindigt zijn huidige activiteit</span><span class="sxs-lookup"><span data-stu-id="323c9-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="323c9-121">U moet **nooit** aanroep van deze functie in het telefoonboek, behalve als u wilt dat een gebruik van uw toepassing in verschillende sessies toosplit: een aanroep van functie toothis zou eindigen Hallo huidige sessie onmiddellijk, dus een aanroep van de volgende te`startActivity()`een nieuwe sessie wilt starten.</span><span class="sxs-lookup"><span data-stu-id="323c9-121">You should **NEVER** call this function by yourself, except if you want toosplit one use of your application into several sessions: a call toothis function would end hello current session immediately, so, a subsequent call too`startActivity()` would start a new session.</span></span> <span data-ttu-id="323c9-122">Deze functie wordt automatisch aangeroepen door Hallo SDK wanneer uw toepassing wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="323c9-122">This function is automatically called by hello SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="323c9-123">Melden van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="323c9-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="323c9-124">Sessiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="323c9-124">Session events</span></span>
<span data-ttu-id="323c9-125">Sessiegebeurtenissen zijn meestal gebruikte tooreport Hallo bewerkingen worden uitgevoerd door een gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="323c9-125">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="323c9-126">**Voorbeeld zonder extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="323c9-126">**Example without extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

<span data-ttu-id="323c9-127">**Voorbeeld met extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="323c9-127">**Example with extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="323c9-128">Zelfstandige gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="323c9-128">Standalone events</span></span>
<span data-ttu-id="323c9-129">Strijdig toosession gebeurtenissen, zelfstandige gebeurtenissen kunnen worden gebruikt buiten de context van een sessie Hallo.</span><span class="sxs-lookup"><span data-stu-id="323c9-129">Contrary toosession events, standalone events can be used outside of hello context of a session.</span></span>

<span data-ttu-id="323c9-130">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="323c9-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="323c9-131">Rapportage van fouten</span><span class="sxs-lookup"><span data-stu-id="323c9-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="323c9-132">Sessie-fouten</span><span class="sxs-lookup"><span data-stu-id="323c9-132">Session errors</span></span>
<span data-ttu-id="323c9-133">Sessie-fouten worden gewoonlijk gebruikte tooreport Hallo fouten die invloed hebben op Hallo gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="323c9-133">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="323c9-134">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="323c9-134">**Example:**</span></span>

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="323c9-135">Zelfstandige fouten</span><span class="sxs-lookup"><span data-stu-id="323c9-135">Standalone errors</span></span>
<span data-ttu-id="323c9-136">Strijdig toosession fouten, zelfstandige fouten kunnen worden gebruikt buiten de context van een sessie Hallo.</span><span class="sxs-lookup"><span data-stu-id="323c9-136">Contrary toosession errors, standalone errors can be used outside of hello context of a session.</span></span>

<span data-ttu-id="323c9-137">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="323c9-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="323c9-138">Rapportage van taken</span><span class="sxs-lookup"><span data-stu-id="323c9-138">Reporting Jobs</span></span>
<span data-ttu-id="323c9-139">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="323c9-139">**Example:**</span></span>

<span data-ttu-id="323c9-140">Stel dat u wilt dat tooreport Hallo duur van uw aanmelding:</span><span class="sxs-lookup"><span data-stu-id="323c9-140">Suppose you want tooreport hello duration of your login process:</span></span>

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="323c9-141">Rapportfouten tijdens een taak</span><span class="sxs-lookup"><span data-stu-id="323c9-141">Report Errors during a Job</span></span>
<span data-ttu-id="323c9-142">Fouten kunnen worden gerelateerde tooa taak in plaats van met de huidige gebruikerssessie toohello gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="323c9-142">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="323c9-143">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="323c9-143">**Example:**</span></span>

<span data-ttu-id="323c9-144">Stel dat u wilt dat tooreport een fout opgetreden tijdens uw aanmelding:</span><span class="sxs-lookup"><span data-stu-id="323c9-144">Suppose you want tooreport an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a><span data-ttu-id="323c9-145">Gebeurtenissen gedurende een project</span><span class="sxs-lookup"><span data-stu-id="323c9-145">Events during a job</span></span>
<span data-ttu-id="323c9-146">Gebeurtenissen kunnen worden gerelateerde tooa taak in plaats van met de huidige gebruikerssessie toohello gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="323c9-146">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="323c9-147">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="323c9-147">**Example:**</span></span>

<span data-ttu-id="323c9-148">Stel, we hebben een sociaal netwerk en gebruiken we een taak tooreport Hallo totale tijd gedurende welke Hallo gebruiker verbonden toohello server is.</span><span class="sxs-lookup"><span data-stu-id="323c9-148">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="323c9-149">Hallo-gebruiker kunt berichten ontvangen van diens vrienden, dit is een taakgebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="323c9-149">hello user can receive messages from his friends, this is a job event.</span></span>

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a><span data-ttu-id="323c9-150">Extra parameters</span><span class="sxs-lookup"><span data-stu-id="323c9-150">Extra parameters</span></span>
<span data-ttu-id="323c9-151">Willekeurige gegevens kunnen worden aangesloten tooevents, fouten, activiteiten en taken.</span><span class="sxs-lookup"><span data-stu-id="323c9-151">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="323c9-152">Deze gegevens kan worden onderverdeeld, iOS van NSDictionary klasse wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="323c9-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="323c9-153">Houd er rekening mee dat extra's kunnen bevatten `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` of andere `NSDictionary` exemplaren.</span><span class="sxs-lookup"><span data-stu-id="323c9-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="323c9-154">Hallo wordt extra parameter geserialiseerd in JSON.</span><span class="sxs-lookup"><span data-stu-id="323c9-154">hello extra parameter is serialized in JSON.</span></span> <span data-ttu-id="323c9-155">Als u wilt dat de verschillende objecten toopass dan Hallo onderwerp wordt beschreven, moet u Hallo methode in uw klasse volgende implementeren:</span><span class="sxs-lookup"><span data-stu-id="323c9-155">If you want toopass different objects than hello ones described above, you must implement hello following method in your class:</span></span>
> 
> <span data-ttu-id="323c9-156">-(NSString*) JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="323c9-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="323c9-157">Hallo-methode moet een JSON-weergave van het object retourneren.</span><span class="sxs-lookup"><span data-stu-id="323c9-157">hello method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="323c9-158">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="323c9-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="323c9-159">Limieten</span><span class="sxs-lookup"><span data-stu-id="323c9-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="323c9-160">Sleutels</span><span class="sxs-lookup"><span data-stu-id="323c9-160">Keys</span></span>
<span data-ttu-id="323c9-161">Elke sleutel in Hallo `NSDictionary` moet overeenkomen met de volgende reguliere expressie Hallo:</span><span class="sxs-lookup"><span data-stu-id="323c9-161">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="323c9-162">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="323c9-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="323c9-163">Grootte</span><span class="sxs-lookup"><span data-stu-id="323c9-163">Size</span></span>
<span data-ttu-id="323c9-164">Extra's zijn beperkt te**1024** tekens per aanroep (eenmaal gecodeerd in JSON door Hallo Engagement agent).</span><span class="sxs-lookup"><span data-stu-id="323c9-164">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="323c9-165">In Hallo is het vorige voorbeeld Hallo JSON toohello server verzonden 58 tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="323c9-165">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="323c9-166">Rapportage-toepassingsinformatie</span><span class="sxs-lookup"><span data-stu-id="323c9-166">Reporting Application Information</span></span>
<span data-ttu-id="323c9-167">U kunt handmatig rapporteren voor het bijhouden van gegevens (of andere toepassing specifieke gegevens) met behulp van Hallo `sendAppInfo:` functie.</span><span class="sxs-lookup"><span data-stu-id="323c9-167">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo:` function.</span></span>

<span data-ttu-id="323c9-168">Merk op dat deze gegevens stapsgewijs kunnen worden verzonden: alleen Hallo meest recente waarde voor een bepaalde sleutel worden behouden voor een bepaald apparaat.</span><span class="sxs-lookup"><span data-stu-id="323c9-168">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="323c9-169">Als gebeurtenis extra's, hello `NSDictionary` klasse wordt informatie over de gebruikte tooabstract, Let op: matrices of subquery woordenlijsten wordt behandeld als platte tekenreeksen (met behulp van de JSON-serialisatie).</span><span class="sxs-lookup"><span data-stu-id="323c9-169">Like event extras, hello `NSDictionary` class is used tooabstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="323c9-170">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="323c9-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="323c9-171">Limieten</span><span class="sxs-lookup"><span data-stu-id="323c9-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="323c9-172">Sleutels</span><span class="sxs-lookup"><span data-stu-id="323c9-172">Keys</span></span>
<span data-ttu-id="323c9-173">Elke sleutel in Hallo `NSDictionary` moet overeenkomen met de volgende reguliere expressie Hallo:</span><span class="sxs-lookup"><span data-stu-id="323c9-173">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="323c9-174">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="323c9-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="323c9-175">Grootte</span><span class="sxs-lookup"><span data-stu-id="323c9-175">Size</span></span>
<span data-ttu-id="323c9-176">Toepassingsgegevens zijn beperkt te**1024** tekens per aanroep (eenmaal gecodeerd in JSON door Hallo Engagement agent).</span><span class="sxs-lookup"><span data-stu-id="323c9-176">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="323c9-177">In Hallo is het vorige voorbeeld Hallo JSON toohello server verzonden 44 tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="323c9-177">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
