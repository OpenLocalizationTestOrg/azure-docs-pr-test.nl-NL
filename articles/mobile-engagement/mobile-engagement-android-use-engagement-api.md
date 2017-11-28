---
title: aaaHow tooUse Hallo Engagement API voor Android
description: Meest recente Android SDK - hoe tooUse Hallo Engagement API voor Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a><span data-ttu-id="91e42-103">Hoe tooUse Hallo Engagement API voor Android</span><span class="sxs-lookup"><span data-stu-id="91e42-103">How tooUse hello Engagement API on Android</span></span>
<span data-ttu-id="91e42-104">Dit document is een invoegtoepassing toohello document [Reporting geavanceerde opties voor Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="91e42-104">This document is an add-on toohello document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="91e42-105">Het biedt diepte meer informatie over hoe toouse Hallo Engagement API tooreport de toepassingsstatistieken van uw.</span><span class="sxs-lookup"><span data-stu-id="91e42-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="91e42-106">Houd er rekening mee dat als u Engagement tooreport van uw toepassing sessies, activiteiten, crashes en technische informatie wilt, hello eenvoudigste manier toomake alle is uw `Activity` onderliggende klassen overnemen Hallo overeenkomt `EngagementActivity` klasse.</span><span class="sxs-lookup"><span data-stu-id="91e42-106">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Activity` sub-classes inherit from hello corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="91e42-107">Als u wilt meer, bijvoorbeeld als u tooreport toepassing specifieke gebeurtenissen, fouten en taken moet toodo, of als er tooreport activiteiten van uw toepassing in een andere manier dan een geïmplementeerd in Hallo Hallo `EngagementActivity` klassen, moet u toouse Hallo Engagement API.</span><span class="sxs-lookup"><span data-stu-id="91e42-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementActivity` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="91e42-108">Hallo Engagement API geleverd door Hallo `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="91e42-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="91e42-109">Een exemplaar van deze klasse kan worden opgehaald door de aanroepende Hallo `EngagementAgent.getInstance(Context)` statische methode (Houd er rekening mee dat Hallo `EngagementAgent` object dat wordt geretourneerd is een singleton).</span><span class="sxs-lookup"><span data-stu-id="91e42-109">An instance of this class can be retrieved by calling hello `EngagementAgent.getInstance(Context)` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="91e42-110">Engagement-concepten</span><span class="sxs-lookup"><span data-stu-id="91e42-110">Engagement concepts</span></span>
<span data-ttu-id="91e42-111">Hallo volgende delen verfijnen Hallo algemene [Mobile Engagement-concepten](mobile-engagement-concepts.md), voor Hallo Android-platform.</span><span class="sxs-lookup"><span data-stu-id="91e42-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for hello Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="91e42-112">`Session` en `Activity`</span><span class="sxs-lookup"><span data-stu-id="91e42-112">`Session` and `Activity`</span></span>
<span data-ttu-id="91e42-113">Als Hallo gebruiker meer dan een paar seconden tussen twee niet-actief blijft *activiteiten*, klikt u vervolgens de volgorde van de *activiteiten* wordt gesplitst in twee afzonderlijke *sessies*.</span><span class="sxs-lookup"><span data-stu-id="91e42-113">If hello user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="91e42-114">Deze enkele seconden worden Hallo 'sessietime-out' genoemd.</span><span class="sxs-lookup"><span data-stu-id="91e42-114">These few seconds are called hello "session timeout".</span></span>

<span data-ttu-id="91e42-115">Een *activiteit* wordt meestal veroorzaakt door een scherm van de toepassing hello, die toosay hello *activiteit* wordt gestart wanneer het welkomstscherm wordt weergegeven en stopt wanneer welkomstscherm is gesloten: dit is Hallo case wanneer Hallo is Engagement SDK geïntegreerd met behulp van Hallo `EngagementActivity` klassen.</span><span class="sxs-lookup"><span data-stu-id="91e42-115">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementActivity` classes.</span></span>

<span data-ttu-id="91e42-116">Maar *activiteiten* kunnen ook handmatig met behulp van Hallo Engagement API worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="91e42-116">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="91e42-117">Hierdoor kunnen een bepaald scherm toosplit in verschillende sub delen tooget meer informatie over Hallo informatie over het gebruik van dit scherm (bijvoorbeeld hoe vaak tooknown en hoe lang dialoogvensters worden gebruikt in dit scherm).</span><span class="sxs-lookup"><span data-stu-id="91e42-117">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="91e42-118">Rapportage</span><span class="sxs-lookup"><span data-stu-id="91e42-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="91e42-119">U hoeft niet tooreport activiteiten zoals beschreven in dit gedeelte als u van Hallo gebruikmaakt `EngagementActivity` klasse en varianten zoals wordt beschreven hoe in Hallo tooIntegrate Engagement voor Android-document.</span><span class="sxs-lookup"><span data-stu-id="91e42-119">You don't need tooreport activities like described in this section if you are using hello `EngagementActivity` class and its variants as explained in hello How tooIntegrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="91e42-120">Gebruiker start een nieuwe activiteit</span><span class="sxs-lookup"><span data-stu-id="91e42-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="91e42-121">U moet toocall `startActivity()` elke activiteit tijd Hallo gebruiker wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="91e42-121">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="91e42-122">Hallo eerste aanroep toothis functie wordt een nieuwe gebruikerssessie gestart.</span><span class="sxs-lookup"><span data-stu-id="91e42-122">hello first call toothis function starts a new user session.</span></span>

<span data-ttu-id="91e42-123">beste plaats toocall deze functie op elke activiteit wordt Hallo `onResume` retouraanroep.</span><span class="sxs-lookup"><span data-stu-id="91e42-123">hello best place toocall this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="91e42-124">Gebruiker eindigt zijn huidige activiteit</span><span class="sxs-lookup"><span data-stu-id="91e42-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="91e42-125">U moet toocall `endActivity()` ten minste eenmaal wanneer de gebruiker Hallo is voltooid, de laatste activiteit.</span><span class="sxs-lookup"><span data-stu-id="91e42-125">You need toocall `endActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="91e42-126">Dit Hallo Engagement SDK dat Hallo gebruiker momenteel niet actief is en dat de gebruikerssessie Hallo toobe moeten eenmaal Hallo sessietime-out gesloten verloopt informeert (als u aanroept `startActivity()` voordat Hallo sessietime-out is verlopen, Hallo sessie gewoon wordt hervat).</span><span class="sxs-lookup"><span data-stu-id="91e42-126">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `startActivity()` before hello session timeout expires, hello session is simply resumed).</span></span>

<span data-ttu-id="91e42-127">beste plaats toocall deze functie op elke activiteit wordt Hallo `onPause` retouraanroep.</span><span class="sxs-lookup"><span data-stu-id="91e42-127">hello best place toocall this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="91e42-128">Melden van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="91e42-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="91e42-129">Sessiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="91e42-129">Session events</span></span>
<span data-ttu-id="91e42-130">Sessiegebeurtenissen zijn meestal gebruikte tooreport Hallo bewerkingen worden uitgevoerd door een gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="91e42-130">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="91e42-131">**Voorbeeld zonder extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="91e42-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="91e42-132">**Voorbeeld met extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="91e42-132">**Example with extra data:**</span></span>

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a><span data-ttu-id="91e42-133">Zelfstandige gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="91e42-133">Standalone Events</span></span>
<span data-ttu-id="91e42-134">Strijdig toosession gebeurtenissen, zelfstandige gebeurtenissen kunnen buiten de context van een sessie Hallo optreden.</span><span class="sxs-lookup"><span data-stu-id="91e42-134">Contrary toosession events, standalone events can occur outside of hello context of a session.</span></span>

<span data-ttu-id="91e42-135">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="91e42-135">**Example:**</span></span>

<span data-ttu-id="91e42-136">Stel dat u wilt dat tooreport gebeurtenissen plaatsvinden wanneer een broadcast-ontvanger is geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="91e42-136">Suppose you want tooreport events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="91e42-137">Rapportage van fouten</span><span class="sxs-lookup"><span data-stu-id="91e42-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="91e42-138">Sessie-fouten</span><span class="sxs-lookup"><span data-stu-id="91e42-138">Session errors</span></span>
<span data-ttu-id="91e42-139">Sessie-fouten worden gewoonlijk gebruikte tooreport Hallo fouten die invloed hebben op Hallo gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="91e42-139">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="91e42-140">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="91e42-140">**Example:**</span></span>

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="91e42-141">Zelfstandige fouten</span><span class="sxs-lookup"><span data-stu-id="91e42-141">Standalone errors</span></span>
<span data-ttu-id="91e42-142">Strijdig toosession fouten, zelfstandige fouten kunnen optreden buiten Hallo context van een sessie.</span><span class="sxs-lookup"><span data-stu-id="91e42-142">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

<span data-ttu-id="91e42-143">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="91e42-143">**Example:**</span></span>

<span data-ttu-id="91e42-144">Hallo volgende voorbeeld ziet u hoe tooreport foutstatus wanneer Hallo geheugen lage op Hallo telefoon tijdens het verwerken van uw toepassing wordt wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="91e42-144">hello following example shows how tooreport an error whenever hello memory becomes low on hello phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="91e42-145">Rapportage van taken</span><span class="sxs-lookup"><span data-stu-id="91e42-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="91e42-146">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="91e42-146">Example</span></span>
<span data-ttu-id="91e42-147">Stel dat u wilt dat tooreport Hallo duur van uw aanmelding:</span><span class="sxs-lookup"><span data-stu-id="91e42-147">Suppose you want tooreport hello duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="91e42-148">Rapportfouten tijdens een taak</span><span class="sxs-lookup"><span data-stu-id="91e42-148">Report Errors during a Job</span></span>
<span data-ttu-id="91e42-149">Fouten kunnen worden gerelateerde tooa taak in plaats van met de huidige gebruikerssessie toohello gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="91e42-149">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="91e42-150">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="91e42-150">**Example:**</span></span>

<span data-ttu-id="91e42-151">Stel dat u wilt dat tooreport aanmelden een fout tijdens u proces:</span><span class="sxs-lookup"><span data-stu-id="91e42-151">Suppose you want tooreport an error during you login process:</span></span>

<span data-ttu-id="91e42-152">[...] openbare void aanmelding (Context context,...) {</span><span class="sxs-lookup"><span data-stu-id="91e42-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="91e42-153">Melden van gebeurtenissen gedurende een project</span><span class="sxs-lookup"><span data-stu-id="91e42-153">Reporting Events during a job</span></span>
<span data-ttu-id="91e42-154">Gebeurtenissen kunnen worden gerelateerde tooa taak in plaats van met de huidige gebruikerssessie toohello gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="91e42-154">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="91e42-155">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="91e42-155">**Example:**</span></span>

<span data-ttu-id="91e42-156">Stel, we hebben een sociaal netwerk en gebruiken we een taak tooreport Hallo totale tijd gedurende welke Hallo gebruiker verbonden toohello server is.</span><span class="sxs-lookup"><span data-stu-id="91e42-156">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="91e42-157">Hallo-gebruiker kunt Blijf op de achtergrond zelfs wanneer hij maakt gebruik van een andere toepassing of wanneer Hallo phone in de slaapstand staat, dus er geen sessie is.</span><span class="sxs-lookup"><span data-stu-id="91e42-157">hello user can stay connected in background even when he's using another application or when hello phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="91e42-158">Hallo-gebruiker kunt berichten ontvangen van diens vrienden, dit is een taakgebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="91e42-158">hello user can receive messages from his friends, this is a job event.</span></span>

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a><span data-ttu-id="91e42-159">Extra parameters</span><span class="sxs-lookup"><span data-stu-id="91e42-159">Extra parameters</span></span>
<span data-ttu-id="91e42-160">Willekeurige gegevens kunnen worden aangesloten tooevents, fouten, activiteiten en taken.</span><span class="sxs-lookup"><span data-stu-id="91e42-160">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="91e42-161">Deze gegevens kan worden onderverdeeld, wordt de Android-bundel klasse (daadwerkelijk, werkt als extra parameters in Android Intents).</span><span class="sxs-lookup"><span data-stu-id="91e42-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="91e42-162">Houd er rekening mee dat een bundel-matrices of een andere bundel exemplaren kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="91e42-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91e42-163">Als u in de parcelable of serializable parameters plaatst, controleert u of hun `toString()` methode geïmplementeerde tooreturn een leesbare tekenreeks is.</span><span class="sxs-lookup"><span data-stu-id="91e42-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented tooreturn a human-readable string.</span></span> <span data-ttu-id="91e42-164">Serialiseerbaar klassen die niet tijdelijke velden bevatten die niet geserialiseerd zijn brengt Android vastlopen wanneer u wordt gebeld`bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="91e42-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="91e42-165">Sparse matrices in extra parameters worden niet ondersteund, dat wil zeggen won't worden geserialiseerd als een matrix.</span><span class="sxs-lookup"><span data-stu-id="91e42-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="91e42-166">U moet deze converteren naar standard matrices voordat u deze in extra parameters.</span><span class="sxs-lookup"><span data-stu-id="91e42-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="91e42-167">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="91e42-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="91e42-168">Limieten</span><span class="sxs-lookup"><span data-stu-id="91e42-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="91e42-169">Sleutels</span><span class="sxs-lookup"><span data-stu-id="91e42-169">Keys</span></span>
<span data-ttu-id="91e42-170">Elke sleutel in Hallo `Bundle` moet overeenkomen met de volgende reguliere expressie Hallo:</span><span class="sxs-lookup"><span data-stu-id="91e42-170">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="91e42-171">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="91e42-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="91e42-172">Grootte</span><span class="sxs-lookup"><span data-stu-id="91e42-172">Size</span></span>
<span data-ttu-id="91e42-173">Extra's zijn beperkt te**1024** tekens per aanroep (eenmaal gecodeerd in JSON door Hallo Engagement service).</span><span class="sxs-lookup"><span data-stu-id="91e42-173">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="91e42-174">In Hallo is het vorige voorbeeld Hallo JSON toohello server verzonden 58 tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="91e42-174">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="91e42-175">Rapportage-toepassingsinformatie</span><span class="sxs-lookup"><span data-stu-id="91e42-175">Reporting Application Information</span></span>
<span data-ttu-id="91e42-176">U kunt handmatig rapporteren voor het bijhouden van gegevens (of andere toepassing specifieke gegevens) met behulp van Hallo `sendAppInfo()` functie.</span><span class="sxs-lookup"><span data-stu-id="91e42-176">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="91e42-177">Merk op dat deze gegevens stapsgewijs kunnen worden verzonden: alleen Hallo meest recente waarde voor een bepaalde sleutel worden behouden voor een bepaald apparaat.</span><span class="sxs-lookup"><span data-stu-id="91e42-177">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="91e42-178">Zoals gebeurtenis extra's, Hallo bundel klasse wordt informatie over de gebruikte tooabstract, let matrices of subplan verzamelt, worden behandeld als platte tekenreeksen (met behulp van de JSON-serialisatie).</span><span class="sxs-lookup"><span data-stu-id="91e42-178">Like event extras, hello Bundle class is used tooabstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="91e42-179">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="91e42-179">Example</span></span>
<span data-ttu-id="91e42-180">Hier volgt een code voorbeeld toosend gebruiker geslacht en Geboortedatum:</span><span class="sxs-lookup"><span data-stu-id="91e42-180">Here is a code sample toosend user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="91e42-181">Limieten</span><span class="sxs-lookup"><span data-stu-id="91e42-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="91e42-182">Sleutels</span><span class="sxs-lookup"><span data-stu-id="91e42-182">Keys</span></span>
<span data-ttu-id="91e42-183">Elke sleutel in Hallo `Bundle` moet overeenkomen met de volgende reguliere expressie Hallo:</span><span class="sxs-lookup"><span data-stu-id="91e42-183">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="91e42-184">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="91e42-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="91e42-185">Grootte</span><span class="sxs-lookup"><span data-stu-id="91e42-185">Size</span></span>
<span data-ttu-id="91e42-186">Toepassingsgegevens zijn beperkt te**1024** tekens per aanroep (eenmaal gecodeerd in JSON door Hallo Engagement service).</span><span class="sxs-lookup"><span data-stu-id="91e42-186">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="91e42-187">In Hallo is het vorige voorbeeld Hallo JSON toohello server verzonden 44 tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="91e42-187">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
