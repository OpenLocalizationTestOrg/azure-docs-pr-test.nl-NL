---
title: aaaHow tooUse Hallo Engagement API op universele Windows-
description: Hoe tooUse Engagement API op Universal Windows hello
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a>Hoe tooUse Engagement API op Universal Windows hello
Dit document is een invoegtoepassing toohello document [hoe tooIntegrate Engagement voor universele Windows-](mobile-engagement-windows-store-integrate-engagement.md): biedt diepte meer informatie over hoe toouse Hallo Engagement API tooreport de toepassingsstatistieken van uw.

Houd er rekening mee dat als u Engagement tooreport van uw toepassing sessies, activiteiten, crashes en technische informatie wilt, hello eenvoudigste manier toomake alle is uw `Page` onderliggende klassen overnemen van Hallo `EngagementPage` klasse.

Als u wilt meer, bijvoorbeeld als u tooreport toepassing specifieke gebeurtenissen, fouten en taken moet toodo, of als er tooreport activiteiten van uw toepassing in een andere manier dan een geïmplementeerd in Hallo Hallo `EngagementPage` klassen, moet u toouse Hallo Engagement API.

Hallo Engagement API geleverd door Hallo `EngagementAgent` klasse. U hebt toegang tot methoden toothose via `EngagementAgent.Instance`.

Zelfs als Hallo agent-module is niet geïnitialiseerd, elke aanroep toohello API wordt uitgesteld en opnieuw worden uitgevoerd wanneer de Hallo agent beschikbaar is.

## <a name="engagement-concepts"></a>Engagement-concepten
Hallo volgende delen verfijnen Hallo algemene [Mobile Engagement-concepten](mobile-engagement-concepts.md) voor Hallo Universal Windows platform.

### <a name="session-and-activity"></a>`Session` en `Activity`
Een *activiteit* wordt meestal veroorzaakt door één pagina van de toepassing hello, die toosay hello *activiteit* wordt gestart wanneer het Hallo-pagina wordt weergegeven en stopt wanneer Hallo pagina is gesloten: dit is Hallo geval wanneer hello Engagement SDK is geïntegreerd met behulp van Hallo `EngagementPage` klasse.

Maar *activiteiten* kunnen ook handmatig met behulp van Hallo Engagement API worden beheerd. Hiermee kunt u een bepaalde pagina in verschillende onderdelen tooget sub meer informatie over het gebruik van deze pagina (bijvoorbeeld hoe vaak tooknow en hoe lang dialoogvensters worden gebruikt binnen deze pagina) Hallo toosplit.

## <a name="reporting-activities"></a>Rapportage
### <a name="user-starts-a-new-activity"></a>Gebruiker start een nieuwe activiteit
#### <a name="reference"></a>Naslaginformatie
            void StartActivity(string name, Dictionary<object, object> extras = null)

U moet toocall `StartActivity()` elke activiteit tijd Hallo gebruiker wordt gewijzigd. Hallo eerste aanroep toothis functie wordt een nieuwe gebruikerssessie gestart.

> [!IMPORTANT]
> Hallo EndActivity methode Hallo SDK automatisch aangeroepen wanneer de toepassing hello wordt gesloten. Dus is het raadzaam toocall hello StartActivity methode wanneer Hallo activiteit van de gebruiker hello wordt gewijzigd en tooNEVER oproep Hallo EndActivity-methode sinds het aanroepen van deze methode forceert toobe van Hallo huidige sessie is beëindigd.
> 
> 

#### <a name="example"></a>Voorbeeld
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>Gebruiker eindigt zijn huidige activiteit
#### <a name="reference"></a>Naslaginformatie
            void EndActivity()

Dit Hallo-activiteit en Hallo-sessie wordt beëindigd. U moet deze methode niet aanroepen, tenzij u zeker weet wat u doet.

#### <a name="example"></a>Voorbeeld
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>Rapportage van taken
### <a name="start-a-job"></a>Een taak starten
#### <a name="reference"></a>Naslaginformatie
            void StartJob(string name, Dictionary<object, object> extras = null)

U kunt Hallo tootrack sommige taken gebruiken gedurende een periode.

#### <a name="example"></a>Voorbeeld
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>Een taak beëindigen
#### <a name="reference"></a>Naslaginformatie
            void EndJob(string name)

Zodra een taak die wordt gevolgd door een taak is beëindigd, moet u Hallo EndJob methode aanroepen voor deze taak door het Hallo-taaknaam opgeven.

#### <a name="example"></a>Voorbeeld
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>Melden van gebeurtenissen
Er is drie soorten gebeurtenissen:

* Zelfstandige gebeurtenissen
* Sessiegebeurtenissen
* Gebeurtenissen van de taak

### <a name="standalone-events"></a>Zelfstandige gebeurtenissen
#### <a name="reference"></a>Naslaginformatie
            void SendEvent(string name, Dictionary<object, object> extras = null)

Er kunnen zelfstandige gebeurtenissen plaatsvinden buiten de context van een sessie Hallo.

#### <a name="example"></a>Voorbeeld
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>Sessiegebeurtenissen
#### <a name="reference"></a>Naslaginformatie
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

Sessiegebeurtenissen zijn meestal gebruikte tooreport Hallo bewerkingen worden uitgevoerd door een gebruiker tijdens de sessie.

#### <a name="example"></a>Voorbeeld
**Zonder gegevens:**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**Met gegevens:**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>Taakgebeurtenissen
#### <a name="reference"></a>Naslaginformatie
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

Gebeurtenissen van de taak zijn meestal gebruikte tooreport Hallo acties die door een gebruiker wordt uitgevoerd tijdens een taak.

#### <a name="example"></a>Voorbeeld
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>Rapportage van fouten
Er zijn drie soorten fouten:

* Zelfstandige fouten
* Sessie-fouten
* Taakfouten

### <a name="standalone-errors"></a>Zelfstandige fouten
#### <a name="reference"></a>Naslaginformatie
            void SendError(string name, Dictionary<object, object> extras = null)

Strijdig toosession fouten, zelfstandige fouten kunnen optreden buiten Hallo context van een sessie.

#### <a name="example"></a>Voorbeeld
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>Sessie-fouten
#### <a name="reference"></a>Naslaginformatie
            void SendSessionError(string name, Dictionary<object, object> extras = null)

Sessie-fouten worden gewoonlijk gebruikte tooreport Hallo fouten die invloed hebben op Hallo gebruiker tijdens de sessie.

#### <a name="example"></a>Voorbeeld
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>Taakfouten
#### <a name="reference"></a>Naslaginformatie
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

Fouten kunnen worden gerelateerde tooa taak in plaats van met de huidige gebruikerssessie toohello gerelateerd.

#### <a name="example"></a>Voorbeeld
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>Reporting Crashes
Hallo agent biedt twee methoden toodeal crashes.

### <a name="send-an-exception"></a>Een uitzondering verzenden
#### <a name="reference"></a>Naslaginformatie
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>Voorbeeld
U kunt een uitzondering op elk gewenst moment kunt verzenden door aan te roepen:

            EngagementAgent.Instance.SendCrash(aCatchedException);

U kunt ook een optionele parameter tooterminate Hallo engagement sessie op Hallo hetzelfde moment dan het Hallo-crash verzenden. toodo dus aanroepen:

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

Als u dat doet, worden Hallo-sessie en taken gesloten na de Hallo crash verzenden.

### <a name="send-an-unhandled-exception"></a>Verzenden van een onverwerkte uitzondering
#### <a name="reference"></a>Naslaginformatie
            void SendCrash(Exception e)

Engagement biedt ook een methode toosend niet-verwerkte uitzonderingen hebt u **UITGESCHAKELDE** Engagement automatisch **crash** reporting. Dit is vooral nuttig wanneer gebruikt in Hallo toepassing UnhandledException gebeurtenis-handler.

Deze methode wordt **altijd** Hallo engagement sessie en taken te beëindigen nadat deze is aangeroepen.

#### <a name="example"></a>Voorbeeld
U kunt deze tooimplement uw eigen UnhandledExceptionEventArgs-handler. Bijvoorbeeld, voeg Hallo `Current_UnhandledException` methode Hallo `App.xaml.cs` bestand:

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

Voeg in App.xaml.cs in "Openbare App() {}" toe:

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a>Apparaat-Id
            String EngagementAgent.Instance.GetDeviceId()

U kunt Hallo engagement apparaat-id ophalen door deze methode aanroept.

## <a name="extras-parameters"></a>Parameters voor extra 's
Willekeurige gegevens kunnen worden aangesloten tooan gebeurtenis, een fout, een activiteit of een taak. Deze gegevens kunnen worden onderverdeeld met behulp van een woordenboek. Sleutels en waarden kunnen van elk type zijn.

Extra gegevens worden geserialiseerd als u uw eigen type in extra's tooinsert wilt u moet daarom tooadd een gegevenscontract voor dit type.

### <a name="example"></a>Voorbeeld
We maken een nieuwe klasse 'Persoon'.

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

Vervolgens voegen we toe een `Person` exemplaar tooan extra.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> Als u andere typen objecten plaatst, zorg ervoor dat de methode ToString() geïmplementeerde tooreturn menselijke leesbare string.
> 
> 

### <a name="limits"></a>Limieten
#### <a name="keys"></a>Sleutels
Elke sleutel in het Hallo-object moet overeenkomen met de volgende reguliere expressie Hallo:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).

#### <a name="size"></a>Grootte
Extra's zijn beperkt te**1024** tekens per aanroep.

## <a name="reporting-application-information"></a>Rapportage-toepassingsinformatie
### <a name="reference"></a>Naslaginformatie
            void SendAppInfo(Dictionary<object, object> appInfos)

U kunt handmatig rapporteert informatie (of andere toepassing specifieke gegevens) met de functie SendAppInfo() Hallo bijhouden.

Merk op dat deze gegevens stapsgewijs kunnen worden verzonden: alleen Hallo meest recente waarde voor een bepaalde sleutel worden behouden voor een bepaald apparaat. Als gebeurtenis extra's, een woordenlijst gebruiken\<-object, object\> tooattach gegevens.

### <a name="example"></a>Voorbeeld
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>Limieten
#### <a name="keys"></a>Sleutels
Elke sleutel in het Hallo-object moet overeenkomen met de volgende reguliere expressie Hallo:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Dit betekent dat sleutels met ten minste één letter beginnen moeten, gevolgd door letters, cijfers of onderstrepingstekens (\_).

#### <a name="size"></a>Grootte
Toepassingsinformatie is beperkt te**1024** tekens per aanroep.

In Hallo is het vorige voorbeeld Hallo JSON toohello server verzonden 44 tekens bevatten:

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a>Logboekregistratie
### <a name="enable-logging"></a>Logboekregistratie inschakelen
Hallo SDK kan worden geconfigureerd tooproduce test Logboeken in Hallo IDE-console.
Deze logboeken worden niet standaard geactiveerd. toocustomize deze, update Hallo eigenschap `EngagementAgent.Instance.TestLogEnabled` tooone van Hallo waarde in Hallo `EngagementTestLogLevel` opsomming, bijvoorbeeld:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

