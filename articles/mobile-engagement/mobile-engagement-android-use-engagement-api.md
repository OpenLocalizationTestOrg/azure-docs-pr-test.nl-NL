---
title: Het gebruik van de Engagement-API voor Android
description: Meest recente Android SDK - API van de betrokkenheid op Android gebruiken
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
ms.openlocfilehash: d353cd2fe47c54a0282cc5bb1b22b4a56e0cd82c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-android"></a><span data-ttu-id="0e451-103">Het gebruik van de Engagement-API voor Android</span><span class="sxs-lookup"><span data-stu-id="0e451-103">How to Use the Engagement API on Android</span></span>
<span data-ttu-id="0e451-104">Dit document is een invoegtoepassing voor het document [Reporting geavanceerde opties voor Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="0e451-104">This document is an add-on to the document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="0e451-105">Het biedt diepte meer informatie over het gebruik van de Engagement-API voor het rapporteren van de toepassingsstatistieken van uw.</span><span class="sxs-lookup"><span data-stu-id="0e451-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="0e451-106">Houd er rekening mee dat als u alleen Engagement voor het rapporteren van uw toepassing sessies, activiteiten, crashes en technische informatie wilt, klikt u vervolgens de eenvoudigste manier is om alle uw `Activity` onderliggende klassen overnemen van de bijbehorende `EngagementActivity` klasse.</span><span class="sxs-lookup"><span data-stu-id="0e451-106">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Activity` sub-classes inherit from the corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="0e451-107">Als u wilt meer doen, bijvoorbeeld als u wilt rapporteren toepassing specifieke gebeurtenissen, fouten en taken, of als u hebt voor het rapporteren van activiteiten van uw toepassing op een andere manier dan de geïmplementeerd in de `EngagementActivity` klassen, moet u de Engagement-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0e451-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementActivity` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="0e451-108">De Engagement-API wordt geleverd door de `EngagementAgent` klasse.</span><span class="sxs-lookup"><span data-stu-id="0e451-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="0e451-109">Een exemplaar van deze klasse kan worden opgehaald door het aanroepen van de `EngagementAgent.getInstance(Context)` statische methode (Houd er rekening mee dat de `EngagementAgent` object dat wordt geretourneerd is een singleton).</span><span class="sxs-lookup"><span data-stu-id="0e451-109">An instance of this class can be retrieved by calling the `EngagementAgent.getInstance(Context)` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="0e451-110">Engagement-concepten</span><span class="sxs-lookup"><span data-stu-id="0e451-110">Engagement concepts</span></span>
<span data-ttu-id="0e451-111">De volgende onderdelen verfijnen de algemene [Mobile Engagement-concepten](mobile-engagement-concepts.md), voor het Android-platform.</span><span class="sxs-lookup"><span data-stu-id="0e451-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for the Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="0e451-112">`Session` en `Activity`</span><span class="sxs-lookup"><span data-stu-id="0e451-112">`Session` and `Activity`</span></span>
<span data-ttu-id="0e451-113">Als de gebruiker meer dan een paar seconden tussen twee niet-actief blijft *activiteiten*, klikt u vervolgens de volgorde van de *activiteiten* wordt gesplitst in twee afzonderlijke *sessies*.</span><span class="sxs-lookup"><span data-stu-id="0e451-113">If the user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="0e451-114">Deze enkele seconden worden de 'sessietime-out' genoemd.</span><span class="sxs-lookup"><span data-stu-id="0e451-114">These few seconds are called the "session timeout".</span></span>

<span data-ttu-id="0e451-115">Een *activiteit* wordt meestal gekoppeld aan één scherm van de toepassing, dat wil zeggen de *activiteit* wordt gestart wanneer het scherm wordt weergegeven en stopt wanneer het scherm is gesloten: dit is het geval wanneer de Engagement SDK is geïntegreerd met behulp van de `EngagementActivity` klassen.</span><span class="sxs-lookup"><span data-stu-id="0e451-115">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementActivity` classes.</span></span>

<span data-ttu-id="0e451-116">Maar *activiteiten* kunnen ook handmatig met behulp van de Engagement-API worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="0e451-116">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="0e451-117">Hierdoor kan het splitsen van een bepaald scherm in verschillende sub-onderdelen voor meer informatie over het gebruik van dit scherm (bijvoorbeeld hoe vaak bekend is en hoe lang dialoogvensters worden gebruikt in dit scherm).</span><span class="sxs-lookup"><span data-stu-id="0e451-117">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="0e451-118">Rapportage</span><span class="sxs-lookup"><span data-stu-id="0e451-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0e451-119">U hoeft niet te rapport activiteiten, zoals beschreven in dit gedeelte als u de `EngagementActivity` klasse en varianten zoals wordt beschreven in de manier waarop integreren engagement voor Android-document.</span><span class="sxs-lookup"><span data-stu-id="0e451-119">You don't need to report activities like described in this section if you are using the `EngagementActivity` class and its variants as explained in the How to Integrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="0e451-120">Gebruiker start een nieuwe activiteit</span><span class="sxs-lookup"><span data-stu-id="0e451-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing the current activity is required for Reach to display in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="0e451-121">U moet aan te roepen `startActivity()` elke keer dat de wijzigingen van de gebruiker-activiteit.</span><span class="sxs-lookup"><span data-stu-id="0e451-121">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="0e451-122">De eerste aanroep van deze functie wordt een nieuwe gebruikerssessie gestart.</span><span class="sxs-lookup"><span data-stu-id="0e451-122">The first call to this function starts a new user session.</span></span>

<span data-ttu-id="0e451-123">De beste plaats voor aanroep van deze functie is op elke activiteit `onResume` retouraanroep.</span><span class="sxs-lookup"><span data-stu-id="0e451-123">The best place to call this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="0e451-124">Gebruiker eindigt zijn huidige activiteit</span><span class="sxs-lookup"><span data-stu-id="0e451-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="0e451-125">U moet aan te roepen `endActivity()` ten minste eenmaal wanneer de gebruiker is voltooid, de laatste activiteit.</span><span class="sxs-lookup"><span data-stu-id="0e451-125">You need to call `endActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="0e451-126">Dit de Engagement SDK informeert dat de gebruiker die momenteel niet actief is en dat de gebruikerssessie moet worden gesloten eenmaal de sessietime-out verloopt (als u aanroept `startActivity()` voordat de sessietime-out is verlopen, wordt de sessie gewoon hervat).</span><span class="sxs-lookup"><span data-stu-id="0e451-126">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `startActivity()` before the session timeout expires, the session is simply resumed).</span></span>

<span data-ttu-id="0e451-127">De beste plaats voor aanroep van deze functie is op elke activiteit `onPause` retouraanroep.</span><span class="sxs-lookup"><span data-stu-id="0e451-127">The best place to call this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="0e451-128">Melden van gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="0e451-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="0e451-129">Sessiegebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="0e451-129">Session events</span></span>
<span data-ttu-id="0e451-130">Sessiegebeurtenissen worden meestal gebruikt voor het rapporteren van de acties die worden uitgevoerd door een gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="0e451-130">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="0e451-131">**Voorbeeld zonder extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="0e451-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="0e451-132">**Voorbeeld met extra gegevens:**</span><span class="sxs-lookup"><span data-stu-id="0e451-132">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="0e451-133">Zelfstandige gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="0e451-133">Standalone Events</span></span>
<span data-ttu-id="0e451-134">In tegenstelling tot sessiegebeurtenissen, kunnen zelfstandige gebeurtenissen plaatsvinden buiten de context van een sessie.</span><span class="sxs-lookup"><span data-stu-id="0e451-134">Contrary to session events, standalone events can occur outside of the context of a session.</span></span>

<span data-ttu-id="0e451-135">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="0e451-135">**Example:**</span></span>

<span data-ttu-id="0e451-136">Stel dat u wilt rapport gebeurtenissen plaatsvinden wanneer een broadcast-ontvanger is geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="0e451-136">Suppose you want to report events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="0e451-137">Rapportage van fouten</span><span class="sxs-lookup"><span data-stu-id="0e451-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="0e451-138">Sessie-fouten</span><span class="sxs-lookup"><span data-stu-id="0e451-138">Session errors</span></span>
<span data-ttu-id="0e451-139">Sessie-fouten worden gewoonlijk gebruikt voor het rapporteren van de fouten die invloed hebben op de gebruiker tijdens de sessie.</span><span class="sxs-lookup"><span data-stu-id="0e451-139">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="0e451-140">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="0e451-140">**Example:**</span></span>

            /** The user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* The user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="0e451-141">Zelfstandige fouten</span><span class="sxs-lookup"><span data-stu-id="0e451-141">Standalone errors</span></span>
<span data-ttu-id="0e451-142">Zelfstandige fouten kunnen strijd sessie-fouten optreden buiten de context van een sessie.</span><span class="sxs-lookup"><span data-stu-id="0e451-142">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

<span data-ttu-id="0e451-143">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="0e451-143">**Example:**</span></span>

<span data-ttu-id="0e451-144">Het volgende voorbeeld laat zien hoe een fout rapporteren wanneer het geheugen op de telefoon lage wordt terwijl het toepassingsproces van uw wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0e451-144">The following example shows how to report an error whenever the memory becomes low on the phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="0e451-145">Rapportage van taken</span><span class="sxs-lookup"><span data-stu-id="0e451-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="0e451-146">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="0e451-146">Example</span></span>
<span data-ttu-id="0e451-147">Stel dat u wilt rapporteren van de duur van uw aanmelding:</span><span class="sxs-lookup"><span data-stu-id="0e451-147">Suppose you want to report the duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="0e451-148">Rapportfouten tijdens een taak</span><span class="sxs-lookup"><span data-stu-id="0e451-148">Report Errors during a Job</span></span>
<span data-ttu-id="0e451-149">Fouten kunnen zijn gerelateerd aan een actieve taak in plaats van te wijten aan de huidige gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="0e451-149">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="0e451-150">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="0e451-150">**Example:**</span></span>

<span data-ttu-id="0e451-151">Stel dat u wilt rapporteren is een fout tijdens u aanmelden proces:</span><span class="sxs-lookup"><span data-stu-id="0e451-151">Suppose you want to report an error during you login process:</span></span>

<span data-ttu-id="0e451-152">[...] openbare void aanmelding (Context context,...) {</span><span class="sxs-lookup"><span data-stu-id="0e451-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try to sign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report the error to Engagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="0e451-153">Melden van gebeurtenissen gedurende een project</span><span class="sxs-lookup"><span data-stu-id="0e451-153">Reporting Events during a job</span></span>
<span data-ttu-id="0e451-154">Gebeurtenissen kunnen zijn gerelateerd aan een actieve taak in plaats van te wijten aan de huidige gebruikerssessie.</span><span class="sxs-lookup"><span data-stu-id="0e451-154">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="0e451-155">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="0e451-155">**Example:**</span></span>

<span data-ttu-id="0e451-156">Stel, we hebben een sociaal netwerk en we gebruiken een taak voor het rapport de totale tijd gedurende welke de gebruiker is verbonden met de server.</span><span class="sxs-lookup"><span data-stu-id="0e451-156">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="0e451-157">De gebruiker kan Blijf op de achtergrond, zelfs wanneer hij maakt gebruik van een andere toepassing of wanneer de telefoon in de slaapstand staat, dus er geen sessie is.</span><span class="sxs-lookup"><span data-stu-id="0e451-157">The user can stay connected in background even when he's using another application or when the phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="0e451-158">De gebruiker berichten ontvangen zijn vrienden, dit is een taakgebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="0e451-158">The user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="0e451-159">Extra parameters</span><span class="sxs-lookup"><span data-stu-id="0e451-159">Extra parameters</span></span>
<span data-ttu-id="0e451-160">Willekeurige gegevens kunnen worden gekoppeld aan gebeurtenissen, fouten, activiteiten en taken.</span><span class="sxs-lookup"><span data-stu-id="0e451-160">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="0e451-161">Deze gegevens kan worden onderverdeeld, wordt de Android-bundel klasse (daadwerkelijk, werkt als extra parameters in Android Intents).</span><span class="sxs-lookup"><span data-stu-id="0e451-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="0e451-162">Houd er rekening mee dat een bundel-matrices of een andere bundel exemplaren kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="0e451-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e451-163">Als u in de parcelable of serializable parameters plaatst, controleert u of hun `toString()` methode om te retourneren van een leesbare tekenreeks is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="0e451-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented to return a human-readable string.</span></span> <span data-ttu-id="0e451-164">Serialiseerbaar klassen die niet tijdelijke velden bevatten die niet geserialiseerd zijn brengt Android vastlopen wanneer u wordt gebeld`bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="0e451-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="0e451-165">Sparse matrices in extra parameters worden niet ondersteund, dat wil zeggen won't worden geserialiseerd als een matrix.</span><span class="sxs-lookup"><span data-stu-id="0e451-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="0e451-166">U moet deze converteren naar standard matrices voordat u deze in extra parameters.</span><span class="sxs-lookup"><span data-stu-id="0e451-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="0e451-167">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="0e451-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="0e451-168">Limieten</span><span class="sxs-lookup"><span data-stu-id="0e451-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="0e451-169">Sleutels</span><span class="sxs-lookup"><span data-stu-id="0e451-169">Keys</span></span>
<span data-ttu-id="0e451-170">Elke sleutel in de `Bundle` moet overeenkomen met de volgende reguliere expressie:</span><span class="sxs-lookup"><span data-stu-id="0e451-170">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="0e451-171">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="0e451-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="0e451-172">Grootte</span><span class="sxs-lookup"><span data-stu-id="0e451-172">Size</span></span>
<span data-ttu-id="0e451-173">Extra's zijn beperkt tot **1024** tekens per aanroep (eenmaal gecodeerd in JSON door de Engagement-service).</span><span class="sxs-lookup"><span data-stu-id="0e451-173">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="0e451-174">In het vorige voorbeeld is de JSON naar de server verzonden 58 tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="0e451-174">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="0e451-175">Rapportage-toepassingsinformatie</span><span class="sxs-lookup"><span data-stu-id="0e451-175">Reporting Application Information</span></span>
<span data-ttu-id="0e451-176">U kunt handmatig rapporteren met behulp van het bijhouden van gegevens (of een andere toepassing specifieke gegevens) de `sendAppInfo()` functie.</span><span class="sxs-lookup"><span data-stu-id="0e451-176">You can manually report tracking information (or any other application specific information) using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="0e451-177">Merk op dat deze gegevens stapsgewijs kunnen worden verzonden: alleen de meest recente waarde voor een opgegeven sleutel worden behouden voor een bepaald apparaat.</span><span class="sxs-lookup"><span data-stu-id="0e451-177">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="0e451-178">Zoals gebeurtenis extra's, wordt de klasse bundel gebruikt voor abstracte toepassingsinformatie, houd er rekening mee dat matrices of subquery bundels worden behandeld als platte tekenreeksen (met behulp van de JSON-serialisatie).</span><span class="sxs-lookup"><span data-stu-id="0e451-178">Like event extras, the Bundle class is used to abstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="0e451-179">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="0e451-179">Example</span></span>
<span data-ttu-id="0e451-180">Hier volgt een voorbeeld van code voor het verzenden van de gebruiker geslacht en Geboortedatum:</span><span class="sxs-lookup"><span data-stu-id="0e451-180">Here is a code sample to send user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="0e451-181">Limieten</span><span class="sxs-lookup"><span data-stu-id="0e451-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="0e451-182">Sleutels</span><span class="sxs-lookup"><span data-stu-id="0e451-182">Keys</span></span>
<span data-ttu-id="0e451-183">Elke sleutel in de `Bundle` moet overeenkomen met de volgende reguliere expressie:</span><span class="sxs-lookup"><span data-stu-id="0e451-183">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="0e451-184">Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).</span><span class="sxs-lookup"><span data-stu-id="0e451-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="0e451-185">Grootte</span><span class="sxs-lookup"><span data-stu-id="0e451-185">Size</span></span>
<span data-ttu-id="0e451-186">Toepassingsgegevens zijn beperkt tot **1024** tekens per aanroep (eenmaal gecodeerd in JSON door de Engagement-service).</span><span class="sxs-lookup"><span data-stu-id="0e451-186">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="0e451-187">In het vorige voorbeeld is de JSON naar de server verzonden 44 tekens bevatten:</span><span class="sxs-lookup"><span data-stu-id="0e451-187">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
