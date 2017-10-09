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
# <a name="how-toouse-hello-engagement-api-on-ios"></a>Hoe tooUse Engagement API Hallo op iOS
Dit document is een invoegtoepassing toohello document hoe tooIntegrate Engagement voor iOS: biedt diepte meer informatie over hoe toouse Hallo Engagement API tooreport de toepassingsstatistieken van uw.

Houd er rekening mee dat als u alleen Engagement tooreport van uw toepassing sessies, activiteiten, crashes en technische informatie, Hallo eenvoudigste manier is toomake alle uw aangepaste `UIViewController` objecten overnemen van Hallo overeenkomt `EngagementViewController` klasse .

Als u wilt meer, bijvoorbeeld als u tooreport toepassing specifieke gebeurtenissen, fouten en taken moet toodo, of als er tooreport activiteiten van uw toepassing in een andere manier dan een geïmplementeerd in Hallo Hallo `EngagementViewController` klassen, moet u toouse Hallo Engagement API.

Hallo Engagement API geleverd door Hallo `EngagementAgent` klasse. Een exemplaar van deze klasse kan worden opgehaald door de aanroepende Hallo `[EngagementAgent shared]` statische methode (Houd er rekening mee dat Hallo `EngagementAgent` object dat wordt geretourneerd is een singleton).

Voordat u een API-aanroepen, hello `EngagementAgent` object moet geïnitialiseerd zijn door het Hallo-methode aanroepen`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`

## <a name="engagement-concepts"></a>Engagement-concepten
Hallo volgende delen verfijnen Hallo algemene [Mobile Engagement-concepten](mobile-engagement-concepts.md) voor Hallo iOS-platform.

### <a name="session-and-activity"></a>`Session` en `Activity`
Een *activiteit* wordt meestal veroorzaakt door een scherm van de toepassing hello, die toosay hello *activiteit* wordt gestart wanneer het welkomstscherm wordt weergegeven en stopt wanneer welkomstscherm is gesloten: dit is Hallo case wanneer Hallo is Engagement SDK geïntegreerd met behulp van Hallo `EngagementViewController` klassen.

Maar *activiteiten* kunnen ook handmatig met behulp van Hallo Engagement API worden beheerd. Hierdoor kunnen een bepaald scherm toosplit in verschillende sub delen tooget meer informatie over Hallo informatie over het gebruik van dit scherm (bijvoorbeeld hoe vaak tooknown en hoe lang dialoogvensters worden gebruikt in dit scherm).

## <a name="reporting-activities"></a>Rapportage
### <a name="user-starts-a-new-activity"></a>Gebruiker start een nieuwe activiteit
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

U moet toocall `startActivity()` elke activiteit tijd Hallo gebruiker wordt gewijzigd. Hallo eerste aanroep toothis functie wordt een nieuwe gebruikerssessie gestart.

### <a name="user-ends-his-current-activity"></a>Gebruiker eindigt zijn huidige activiteit
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> U moet **nooit** aanroep van deze functie in het telefoonboek, behalve als u wilt dat een gebruik van uw toepassing in verschillende sessies toosplit: een aanroep van functie toothis zou eindigen Hallo huidige sessie onmiddellijk, dus een aanroep van de volgende te`startActivity()`een nieuwe sessie wilt starten. Deze functie wordt automatisch aangeroepen door Hallo SDK wanneer uw toepassing wordt gesloten.
> 
> 

## <a name="reporting-events"></a>Melden van gebeurtenissen
### <a name="session-events"></a>Sessiegebeurtenissen
Sessiegebeurtenissen zijn meestal gebruikte tooreport Hallo bewerkingen worden uitgevoerd door een gebruiker tijdens de sessie.

**Voorbeeld zonder extra gegevens:**

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

**Voorbeeld met extra gegevens:**

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

### <a name="standalone-events"></a>Zelfstandige gebeurtenissen
Strijdig toosession gebeurtenissen, zelfstandige gebeurtenissen kunnen worden gebruikt buiten de context van een sessie Hallo.

**Voorbeeld:**

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a>Rapportage van fouten
### <a name="session-errors"></a>Sessie-fouten
Sessie-fouten worden gewoonlijk gebruikte tooreport Hallo fouten die invloed hebben op Hallo gebruiker tijdens de sessie.

**Voorbeeld:**

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

### <a name="standalone-errors"></a>Zelfstandige fouten
Strijdig toosession fouten, zelfstandige fouten kunnen worden gebruikt buiten de context van een sessie Hallo.

**Voorbeeld:**

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a>Rapportage van taken
**Voorbeeld:**

Stel dat u wilt dat tooreport Hallo duur van uw aanmelding:

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

### <a name="report-errors-during-a-job"></a>Rapportfouten tijdens een taak
Fouten kunnen worden gerelateerde tooa taak in plaats van met de huidige gebruikerssessie toohello gerelateerd.

**Voorbeeld:**

Stel dat u wilt dat tooreport een fout opgetreden tijdens uw aanmelding:

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

### <a name="events-during-a-job"></a>Gebeurtenissen gedurende een project
Gebeurtenissen kunnen worden gerelateerde tooa taak in plaats van met de huidige gebruikerssessie toohello gerelateerd.

**Voorbeeld:**

Stel, we hebben een sociaal netwerk en gebruiken we een taak tooreport Hallo totale tijd gedurende welke Hallo gebruiker verbonden toohello server is. Hallo-gebruiker kunt berichten ontvangen van diens vrienden, dit is een taakgebeurtenis.

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

## <a name="extra-parameters"></a>Extra parameters
Willekeurige gegevens kunnen worden aangesloten tooevents, fouten, activiteiten en taken.

Deze gegevens kan worden onderverdeeld, iOS van NSDictionary klasse wordt gebruikt.

Houd er rekening mee dat extra's kunnen bevatten `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` of andere `NSDictionary` exemplaren.

> [!NOTE]
> Hallo wordt extra parameter geserialiseerd in JSON. Als u wilt dat de verschillende objecten toopass dan Hallo onderwerp wordt beschreven, moet u Hallo methode in uw klasse volgende implementeren:
> 
> -(NSString*) JSONRepresentation;
> 
> Hallo-methode moet een JSON-weergave van het object retourneren.
> 
> 

### <a name="example"></a>Voorbeeld
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a>Limieten
#### <a name="keys"></a>Sleutels
Elke sleutel in Hallo `NSDictionary` moet overeenkomen met de volgende reguliere expressie Hallo:

`^[a-zA-Z][a-zA-Z_0-9]*`

Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).

#### <a name="size"></a>Grootte
Extra's zijn beperkt te**1024** tekens per aanroep (eenmaal gecodeerd in JSON door Hallo Engagement agent).

In Hallo is het vorige voorbeeld Hallo JSON toohello server verzonden 58 tekens bevatten:

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Rapportage-toepassingsinformatie
U kunt handmatig rapporteren voor het bijhouden van gegevens (of andere toepassing specifieke gegevens) met behulp van Hallo `sendAppInfo:` functie.

Merk op dat deze gegevens stapsgewijs kunnen worden verzonden: alleen Hallo meest recente waarde voor een bepaalde sleutel worden behouden voor een bepaald apparaat.

Als gebeurtenis extra's, hello `NSDictionary` klasse wordt informatie over de gebruikte tooabstract, Let op: matrices of subquery woordenlijsten wordt behandeld als platte tekenreeksen (met behulp van de JSON-serialisatie).

**Voorbeeld:**

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a>Limieten
#### <a name="keys"></a>Sleutels
Elke sleutel in Hallo `NSDictionary` moet overeenkomen met de volgende reguliere expressie Hallo:

`^[a-zA-Z][a-zA-Z_0-9]*`

Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).

#### <a name="size"></a>Grootte
Toepassingsgegevens zijn beperkt te**1024** tekens per aanroep (eenmaal gecodeerd in JSON door Hallo Engagement agent).

In Hallo is het vorige voorbeeld Hallo JSON toohello server verzonden 44 tekens bevatten:

    {"birthdate":"1983-12-07","gender":"female"}
