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
# <a name="how-toouse-hello-engagement-api-on-android"></a>Hoe tooUse Hallo Engagement API voor Android
Dit document is een invoegtoepassing toohello document [Reporting geavanceerde opties voor Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md). Het biedt diepte meer informatie over hoe toouse Hallo Engagement API tooreport de toepassingsstatistieken van uw.

Houd er rekening mee dat als u Engagement tooreport van uw toepassing sessies, activiteiten, crashes en technische informatie wilt, hello eenvoudigste manier toomake alle is uw `Activity` onderliggende klassen overnemen Hallo overeenkomt `EngagementActivity` klasse.

Als u wilt meer, bijvoorbeeld als u tooreport toepassing specifieke gebeurtenissen, fouten en taken moet toodo, of als er tooreport activiteiten van uw toepassing in een andere manier dan een geïmplementeerd in Hallo Hallo `EngagementActivity` klassen, moet u toouse Hallo Engagement API.

Hallo Engagement API geleverd door Hallo `EngagementAgent` klasse. Een exemplaar van deze klasse kan worden opgehaald door de aanroepende Hallo `EngagementAgent.getInstance(Context)` statische methode (Houd er rekening mee dat Hallo `EngagementAgent` object dat wordt geretourneerd is een singleton).

## <a name="engagement-concepts"></a>Engagement-concepten
Hallo volgende delen verfijnen Hallo algemene [Mobile Engagement-concepten](mobile-engagement-concepts.md), voor Hallo Android-platform.

### <a name="session-and-activity"></a>`Session` en `Activity`
Als Hallo gebruiker meer dan een paar seconden tussen twee niet-actief blijft *activiteiten*, klikt u vervolgens de volgorde van de *activiteiten* wordt gesplitst in twee afzonderlijke *sessies*. Deze enkele seconden worden Hallo 'sessietime-out' genoemd.

Een *activiteit* wordt meestal veroorzaakt door een scherm van de toepassing hello, die toosay hello *activiteit* wordt gestart wanneer het welkomstscherm wordt weergegeven en stopt wanneer welkomstscherm is gesloten: dit is Hallo case wanneer Hallo is Engagement SDK geïntegreerd met behulp van Hallo `EngagementActivity` klassen.

Maar *activiteiten* kunnen ook handmatig met behulp van Hallo Engagement API worden beheerd. Hierdoor kunnen een bepaald scherm toosplit in verschillende sub delen tooget meer informatie over Hallo informatie over het gebruik van dit scherm (bijvoorbeeld hoe vaak tooknown en hoe lang dialoogvensters worden gebruikt in dit scherm).

## <a name="reporting-activities"></a>Rapportage
> [!IMPORTANT]
> U hoeft niet tooreport activiteiten zoals beschreven in dit gedeelte als u van Hallo gebruikmaakt `EngagementActivity` klasse en varianten zoals wordt beschreven hoe in Hallo tooIntegrate Engagement voor Android-document.
> 
> 

### <a name="user-starts-a-new-activity"></a>Gebruiker start een nieuwe activiteit
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

U moet toocall `startActivity()` elke activiteit tijd Hallo gebruiker wordt gewijzigd. Hallo eerste aanroep toothis functie wordt een nieuwe gebruikerssessie gestart.

beste plaats toocall deze functie op elke activiteit wordt Hallo `onResume` retouraanroep.

### <a name="user-ends-his-current-activity"></a>Gebruiker eindigt zijn huidige activiteit
            EngagementAgent.getInstance(this).endActivity();

U moet toocall `endActivity()` ten minste eenmaal wanneer de gebruiker Hallo is voltooid, de laatste activiteit. Dit Hallo Engagement SDK dat Hallo gebruiker momenteel niet actief is en dat de gebruikerssessie Hallo toobe moeten eenmaal Hallo sessietime-out gesloten verloopt informeert (als u aanroept `startActivity()` voordat Hallo sessietime-out is verlopen, Hallo sessie gewoon wordt hervat).

beste plaats toocall deze functie op elke activiteit wordt Hallo `onPause` retouraanroep.

## <a name="reporting-events"></a>Melden van gebeurtenissen
### <a name="session-events"></a>Sessiegebeurtenissen
Sessiegebeurtenissen zijn meestal gebruikte tooreport Hallo bewerkingen worden uitgevoerd door een gebruiker tijdens de sessie.

**Voorbeeld zonder extra gegevens:**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**Voorbeeld met extra gegevens:**

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

### <a name="standalone-events"></a>Zelfstandige gebeurtenissen
Strijdig toosession gebeurtenissen, zelfstandige gebeurtenissen kunnen buiten de context van een sessie Hallo optreden.

**Voorbeeld:**

Stel dat u wilt dat tooreport gebeurtenissen plaatsvinden wanneer een broadcast-ontvanger is geactiveerd:

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>Rapportage van fouten
### <a name="session-errors"></a>Sessie-fouten
Sessie-fouten worden gewoonlijk gebruikte tooreport Hallo fouten die invloed hebben op Hallo gebruiker tijdens de sessie.

**Voorbeeld:**

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

### <a name="standalone-errors"></a>Zelfstandige fouten
Strijdig toosession fouten, zelfstandige fouten kunnen optreden buiten Hallo context van een sessie.

**Voorbeeld:**

Hallo volgende voorbeeld ziet u hoe tooreport foutstatus wanneer Hallo geheugen lage op Hallo telefoon tijdens het verwerken van uw toepassing wordt wordt uitgevoerd.

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>Rapportage van taken
### <a name="example"></a>Voorbeeld
Stel dat u wilt dat tooreport Hallo duur van uw aanmelding:

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

### <a name="report-errors-during-a-job"></a>Rapportfouten tijdens een taak
Fouten kunnen worden gerelateerde tooa taak in plaats van met de huidige gebruikerssessie toohello gerelateerd.

**Voorbeeld:**

Stel dat u wilt dat tooreport aanmelden een fout tijdens u proces:

[...] openbare void aanmelding (Context context,...) {

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

### <a name="reporting-events-during-a-job"></a>Melden van gebeurtenissen gedurende een project
Gebeurtenissen kunnen worden gerelateerde tooa taak in plaats van met de huidige gebruikerssessie toohello gerelateerd.

**Voorbeeld:**

Stel, we hebben een sociaal netwerk en gebruiken we een taak tooreport Hallo totale tijd gedurende welke Hallo gebruiker verbonden toohello server is. Hallo-gebruiker kunt Blijf op de achtergrond zelfs wanneer hij maakt gebruik van een andere toepassing of wanneer Hallo phone in de slaapstand staat, dus er geen sessie is.

Hallo-gebruiker kunt berichten ontvangen van diens vrienden, dit is een taakgebeurtenis.

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

## <a name="extra-parameters"></a>Extra parameters
Willekeurige gegevens kunnen worden aangesloten tooevents, fouten, activiteiten en taken.

Deze gegevens kan worden onderverdeeld, wordt de Android-bundel klasse (daadwerkelijk, werkt als extra parameters in Android Intents). Houd er rekening mee dat een bundel-matrices of een andere bundel exemplaren kan bevatten.

> [!IMPORTANT]
> Als u in de parcelable of serializable parameters plaatst, controleert u of hun `toString()` methode geïmplementeerde tooreturn een leesbare tekenreeks is. Serialiseerbaar klassen die niet tijdelijke velden bevatten die niet geserialiseerd zijn brengt Android vastlopen wanneer u wordt gebeld`bundle.putSerializable("key",value);`
> 
> [!WARNING]
> Sparse matrices in extra parameters worden niet ondersteund, dat wil zeggen won't worden geserialiseerd als een matrix. U moet deze converteren naar standard matrices voordat u deze in extra parameters.
> 
> 

### <a name="example"></a>Voorbeeld
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>Limieten
#### <a name="keys"></a>Sleutels
Elke sleutel in Hallo `Bundle` moet overeenkomen met de volgende reguliere expressie Hallo:

`^[a-zA-Z][a-zA-Z_0-9]*`

Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).

#### <a name="size"></a>Grootte
Extra's zijn beperkt te**1024** tekens per aanroep (eenmaal gecodeerd in JSON door Hallo Engagement service).

In Hallo is het vorige voorbeeld Hallo JSON toohello server verzonden 58 tekens bevatten:

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Rapportage-toepassingsinformatie
U kunt handmatig rapporteren voor het bijhouden van gegevens (of andere toepassing specifieke gegevens) met behulp van Hallo `sendAppInfo()` functie.

Merk op dat deze gegevens stapsgewijs kunnen worden verzonden: alleen Hallo meest recente waarde voor een bepaalde sleutel worden behouden voor een bepaald apparaat.

Zoals gebeurtenis extra's, Hallo bundel klasse wordt informatie over de gebruikte tooabstract, let matrices of subplan verzamelt, worden behandeld als platte tekenreeksen (met behulp van de JSON-serialisatie).

### <a name="example"></a>Voorbeeld
Hier volgt een code voorbeeld toosend gebruiker geslacht en Geboortedatum:

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>Limieten
#### <a name="keys"></a>Sleutels
Elke sleutel in Hallo `Bundle` moet overeenkomen met de volgende reguliere expressie Hallo:

`^[a-zA-Z][a-zA-Z_0-9]*`

Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).

#### <a name="size"></a>Grootte
Toepassingsgegevens zijn beperkt te**1024** tekens per aanroep (eenmaal gecodeerd in JSON door Hallo Engagement service).

In Hallo is het vorige voorbeeld Hallo JSON toohello server verzonden 44 tekens bevatten:

            {"expiration":"2016-12-07","status":"premium"}
