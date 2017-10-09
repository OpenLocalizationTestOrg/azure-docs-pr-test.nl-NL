---
title: aaaHow toouse hello Azure Mobile Apps SDK voor Android | Microsoft Docs
description: Hoe toouse Azure Mobile Apps SDK Hallo voor Android
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a>Hoe toouse Azure Mobile Apps SDK Hallo voor Android

Deze handleiding wordt getoond hoe Hallo toouse Android client SDK voor Mobile Apps tooimplement algemene scenario's, zoals:

* Opvragen van gegevens (invoegen, bijwerken en verwijderen).
* -Verificatie.
* Foutafhandeling.
* Hallo-client aanpassen.

Deze handleiding is gericht op Hallo clientzijde Android SDK.  informatie over hello serverzijde SDK's voor mobiele Apps, Zie toolearn [werken met .NET back-end SDK] [ 10] of [hoe toouse back-end voor Node.js SDK Hallo] [ 11].

## <a name="reference-documentation"></a>Naslagdocumentatie

U vindt Hallo [Javadocs API-referentiemateriaal] [ 12] voor Android clientbibliotheek Hallo op GitHub.

## <a name="supported-platforms"></a>Ondersteunde Platforms

Hello Azure Mobile Apps SDK voor Android ondersteunt API niveaus 19 tot en met 24 (KitKat via deze) voor de telefoon en tablet vormfactoren.  Verificatie, met name maakt gebruik van een algemene web framework benadering toogather gebruikersreferenties.  Server-flow-verificatie werkt niet met kleine formulier factor apparaten zoals kijkt naar.

## <a name="setup-and-prerequisites"></a>Het installatieprogramma en vereisten

Volledige Hallo [Mobile Apps Quick Start](app-service-mobile-android-get-started.md) zelfstudie.  Deze taak zorgt ervoor dat alle vereisten voor het ontwikkelen van Azure Mobile Apps is voldaan.  Hallo Quick Start helpt u bij het configureren van uw account en uw eerste back-end voor mobiele apps te maken.

Als u geen toocomplete Hallo Quick Start-zelfstudie besluit, voltooit u Hallo taken te volgen:

* [Maak een back-end voor de mobiele App] [ 13] toouse met uw Android-app.
* In Android Studio [update Hallo Gradle bouwen bestanden](#gradle-build).
* [Internet-machtiging wordt ingeschakeld](#enable-internet).

### <a name="gradle-build"></a>Update Hallo Gradle-bestand maken

Beide wijzigen **build.gradle** bestanden:

1. Voeg deze code toohello *Project* niveau **build.gradle** bestand in de Hallo *buildscript* tag:

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. Voeg deze code toohello *Module app* niveau **build.gradle** bestand in de Hallo *afhankelijkheden* tag:

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    De meest recente versie Hallo is momenteel 3.3.0. Hallo ondersteund versies worden weergegeven [op bintray][14].

### <a name="enable-internet"></a>Internet-machtiging wordt ingeschakeld

tooaccess Azure, uw app moet gemachtigd Hallo INTERNET ingeschakeld. Als deze nog niet is ingeschakeld, toevoegen Hallo volgende regel code tooyour **AndroidManifest.xml** bestand:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a>Een clientverbinding maken

Mobiele Apps van Azure biedt vier functies tooyour mobiele toepassing:

* Toegang tot gegevens en Offline synchronisatie met een Azure Mobile Apps-Service.
* Aangepaste API's die zijn geschreven met hello Azure Mobile Apps Server SDK-aanroep.
* Verificatie met Azure App Service-verificatie en autorisatie.
* Registratie bij Notification Hubs voor pushmeldingen.

Elk van deze functies, moet u eerst dat u maakt een `MobileServiceClient` object.  Slechts één `MobileServiceClient` object moet worden gemaakt binnen uw mobiele clients (dat wil zeggen, deze moet een Singleton-patroon).  toocreate een `MobileServiceClient` object:

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

Hallo `<MobileAppUrl>` is een tekenreeks of een URL-object dat tooyour mobiele back-end wijst.  Als u van Azure App Service-toohost uw mobiele back-end gebruikmaakt, zorgt u beveiligde Hallo `https://` versie van het Hallo-URL.

Hallo-client vereist ook toegang toohello activiteit of Context - hello `this` parameter in Hallo-voorbeeld.  Hallo MobileServiceClient bouw moet gebeuren binnen Hallo `onCreate()` methode van de activiteit waarnaar wordt verwezen in Hallo Hallo `AndroidManifest.xml` bestand.

Als een best practice moet u communicatie tussen de server in een eigen (singleton-pattern)-klasse als abstract.  In dit geval moet u doorgeven Hallo activiteit binnen Hallo constructor tooappropriately Hallo service configureren.  Bijvoorbeeld:

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

U kunt nu aanroepen `AzureServiceAdapter.Initialize(this);` in Hallo `onCreate()` methode van uw belangrijkste activiteit.  Alle andere methoden hoeven toohello toegangsclient gebruiken `AzureServiceAdapter.getInstance();` tooobtain een verwijzing naar een toohello adapter.

## <a name="data-operations"></a>Gegevensbewerkingen

Hallo-kern van hello Azure Mobile Apps SDK is tooprovide toegang toodata opgeslagen in SQL Azure op Hallo-backend voor mobiele Apps.  U kunt toegang tot deze gegevens met behulp van sterk getypeerde klassen (aanbevolen) of getypeerde query's (niet aanbevolen).  Hallo bulksgewijs van deze sectie behandelt sterk getypeerde klassen gebruiken.

### <a name="define-client-data-classes"></a>Definiëren van gegevensklassen client

tooaccess gegevens uit SQL Azure-tabellen, definiëren van gegevensklassen client die overeenkomen met toohello tabellen in de back-end van Hallo mobiele App. Voorbeelden in dit onderwerp wordt ervan uitgegaan dat een tabel met de naam **MyDataTable**, heeft Hallo kolommen te volgen:

* id
* Tekst
* Voltooien

Hallo bijbehorende getypte client-side '-object bevindt zich in een bestand met de naam **MyDataTable.java**:

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

Voeg de getter en setter methoden voor elk veld dat u toevoegt.  Als uw Azure SQL-tabel meer kolommen bevat, zou u Hallo overeenkomende velden toothis klasse toevoegen.  Bijvoorbeeld, als hello DTO (object data transfer) was een kolom met gehele getallen prioriteit en u kunt dit veld samen met de methoden getter en setter toevoegen:

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

toolearn hoe toocreate aanvullende tabellen in uw Mobile Apps back-end, Zie [hoe: Definieer een controller tabel] [ 15] (.NET-backend) of [definiëren tabellen met behulp van een dynamische Schema] [ 16] (Node.js back-end).

Een tabel van de back-end van Azure Mobile Apps definieert vijf speciale velden waarvan vier tooclients beschikbaar zijn:

* `String id`: globaal unieke ID voor de record Hallo Hallo.  Als een best practice maken Hallo id Hallo tekenreeksweergave van een [UUID] [ 17] object.
* `DateTimeOffset updatedAt`: datum/tijd van laatste update van Hallo Hallo.  Hallo updatedAt veld is ingesteld door de server Hallo en nooit door uw clientcode moet worden ingesteld.
* `DateTimeOffset createdAt`: Hallo datum/tijd dat Hallo-object is gemaakt.  Hallo createdAt veld is ingesteld door de server Hallo en nooit door uw clientcode moet worden ingesteld.
* `byte[] version`: Normaal weergegeven als een tekenreeks, is Hallo-versie ook ingesteld door Hallo-server.
* `boolean deleted`: Hiermee wordt aangegeven Hallo-record verwijderd maar nog niet is verwijderd.  Gebruik geen `deleted` als in uw klasse-eigenschap.

Hallo `id` veld is vereist.  Hallo `updatedAt` veld en `version` veld worden gebruikt voor offlinesynchronisatie (voor incrementele synchronisatie en conflict respectievelijk).  Hallo `createdAt` veld is een verwijzingsveld en niet wordt gebruikt door het Hallo-client.  Hallo-namen zijn 'in-the-wire' namen van eigenschappen Hallo en zijn niet aanpasbaar.  Echter kunt u een toewijzing tussen uw object en het Hallo 'in-the-wire' namen maken met behulp van Hallo [gson] [ 3] bibliotheek.  Bijvoorbeeld:

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a>De tabelverwijzing van een maken

tooaccess een tabel, maakt u eerst een [MobileServiceTable] [ 8] object door de aanroepende Hallo **getTable** methode op Hallo [MobileServiceClient][9].  Deze methode heeft twee overloads:

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

In de volgende code, Hallo **mClient** tooyour MobileServiceClient referentieobject is.  Hallo eerste overbelasting wordt gebruikt waarbij Hallo klassenaam en tabelnaam Hallo zijn Hallo dezelfde en hello een worden in het Hallo Quick Start:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

Hallo tweede overbelasting wordt gebruikt wanneer Hallo tabelnaam van de naam van de klasse Hallo afwijkt: de eerste parameter Hallo Hallo tabelnaam is.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a>Een tabel met back-end

Eerst moet u een tabelverwijzing.  Vervolgens moet u een query uitvoeren op Hallo tabelverwijzing.  Een query is een combinatie van:

* Een `.where()` [filter-component](#filtering).
* Een `.orderBy()` [ordening component](#sorting).
* Een `.select()` [veld selectiecomponent](#selection).
* Een `.skip()` en `.top()` voor [wisselbare resultaten](#paging).

Hallo-componenten moeten worden opgenomen in het Hallo voorafgaand aan de volgorde.

### <a name="filter"></a>Filteren van resultaten

Hallo algemene vorm van een query is:

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

Hallo retourneert voorgaande voorbeeld alle resultaten (omhoog toohello maximale paginagrootte ingesteld door Hallo server).  Hallo `.execute()` methode Hallo query uitgevoerd op Hallo back-end.  Hallo-query is geconverteerde tooan [OData v3] [ 19] query vóór verzending toohello Mobile Apps back-end.  Ontvangen converteert Hallo Mobile Apps-back-end Hallo-query naar een SQL-instructie voordat deze wordt uitgevoerd op Hallo Azure SQL-exemplaar.  Aangezien netwerkactiviteit enige tijd neemt, Hallo `.execute()` methode retourneert een [ `ListenableFuture<E>` ] [ 18].

### <a name="filtering"></a>Geretourneerde gegevens filteren

Hallo na uitvoering van de query retourneert alle items van Hallo **ToDoItem** tabel waar **voltooid** gelijk is aan **false**.

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

**mToDoTable** is Hallo toohello mobiele service verwijzingstabel die we eerder hebben gemaakt.

Definieer een filter met de Hallo **waar** methodeaanroep op Hallo tabelverwijzing. Hallo **waar** methode wordt gevolgd door een **veld** methode gevolgd door een methode waarmee Hallo logische predikaat. Mogelijke predikaat methoden omvatten **eq** (is gelijk aan), **ne** (niet gelijk) **gt** (groter dan) **ge** (groter dan of gelijk zijn aan), **lt** (minder dan,) **RP** (kleiner dan of gelijk aan). Deze methoden kunnen u vergelijken en tekenreeks velden toospecific waarden.

U kunt filteren op datums. Hallo volgende methoden kunnen u de hele datumveld Hallo of onderdelen van Hallo datum vergelijken: **jaar**, **maand**, **dag**, **uur**, **minuut**, en **tweede**. Hallo volgende voorbeeld wordt een filter toegevoegd voor artikelen waarvan *vervaldatum* gelijk is aan 2013.

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

Hallo volgt ondersteuning voor complexe filters op tekenreeksvelden: **startsWith**, **endsWith**, **concat**, **subtekenreeks**, **indexOf**, **vervangen**, **toLower**, **toUpper**, **trim**, en  **lengte**. Hallo na voorbeeld filters voor de tabel rijen waar hello *tekst* kolom begint met "PRI0."

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

Hallo volgende operator methoden worden ondersteund op numerieke velden: **toevoegen**, **sub**, **mul**, **div**, **mod**, **floor**, **maximum**, en **afronden**. Hallo na voorbeeld filters voor de tabel rijen waar hello **duur** een even getal is.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

U kunt predikaten met deze logische methoden combineren: **en**, **of** en **niet**. Hallo volgt combineert twee van de voorgaande voorbeelden Hallo.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

Groep en het nesten van logische operators:

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

Zie voor meer gedetailleerde discussie en voorbeelden van filteren, [verkennen Hallo rijke van Hallo Android client querymodel][20].

### <a name="sorting"></a>Geretourneerde gegevens sorteren

Hallo volgende code retourneert alle items uit een tabel met **taken** gesorteerd door Hallo oplopende *tekst* veld. *mToDoTable* is Hallo toohello back-end verwijzingstabel die u eerder hebt gemaakt:

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

de eerste parameter van Hallo Hallo **orderBy** methode is de naam van een tekenreeks gelijk toohello van Hallo veld op welke toosort. Hallo maakt gebruik van de tweede parameter Hallo **QueryOrder** opsomming toospecify of toosort oplopende of aflopende.  Als u filtert met behulp van Hallo ***waar*** methode, Hallo ***waar*** methode moet worden aangeroepen voordat Hallo ***orderBy*** methode.

### <a name="selection"></a>Selecteer specifieke kolommen

Hallo volgende code laat zien hoe tooreturn alle items uit een tabel met **taken**, maar alleen toont Hallo **voltooid** en **tekst** velden. **mToDoTable** is Hallo toohello back-end verwijzingstabel die we eerder hebben gemaakt.

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

functie van Hallo parameters toohello select zijn Hallo tekenreeksnamen van Hallo tabelkolommen die u tooreturn wilt.  Hallo **Selecteer** methode moet toofollow methoden zoals **waar** en **orderBy**. Het kan worden gevolgd door methoden zoals paginering **overslaan** en **boven**.

### <a name="paging"></a>Gegevens weergeven op pagina 's

Gegevens **altijd** geretourneerd op pagina's.  Hallo kunt u het maximum aantal records dat wordt geretourneerd is door Hallo-server ingesteld.  Als de client Hallo meer records vraagt, retourneert Hallo server Hallo kunt u het maximum aantal records.  Standaard is de maximale paginagrootte Hallo op Hallo server 50 records.

Hallo eerste voorbeeld laat zien hoe tooselect Hallo bovenste vijf items uit een tabel. Hallo query retourneert Hallo items van een tabel met **taken**. **mToDoTable** is Hallo toohello back-end verwijzingstabel die u eerder hebt gemaakt:

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

Hier volgt een query of slaat het Hallo eerste vijf items en vervolgens retourneert de volgende vijf Hallo:

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

Als u tooget alle records in een tabel wenst, moet u code tooiterate implementeren via alle pagina's:

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

Een aanvraag voor alle records met deze methode maakt een minimum van twee aanvragen toohello Mobile Apps back-end.

> [!TIP]
> Kiezen Hallo rechts paginagrootte is een evenwicht tussen geheugengebruik tijdens het Hallo-aanvraag gebeurt er, bandbreedtegebruik en vertraging bij het ontvangen van gegevens Hallo volledig.  Hallo-standaard (50 records) is geschikt voor alle apparaten.  Als u alleen op geheugenapparaten met grotere werkt, verhoogt u up too500.  We hebben die toenemende Hallo paginaformaat dan 500 registreert resultaten gevonden in onaanvaardbaar vertragingen en grote geheugenproblemen.

### <a name="chaining"></a>Hoe: querymethoden samenvoegen

Hallo-methoden die worden gebruikt bij het zoeken van back-end-tabellen kunnen worden samengevoegd. Query methoden kunt u specifieke kolommen tooselect gefilterde rijen die worden gesorteerd en wisselbaar geheugen: chaining. U kunt complexe logische filters maken.  Elke querymethode retourneert een Query-object. tooend hello reeks methoden en daadwerkelijk uitvoeren Hallo query, aanroep Hallo **uitvoeren** methode. Bijvoorbeeld:

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

Hallo teruggekoppeld query methoden moeten als volgt zijn gerangschikt:

1. Filteren (**waar**) methoden.
2. Sorteren (**orderBy**) methoden.
3. Selectie (**Selecteer**) methoden.
4. wisselgeheugengebruik (**overslaan** en **boven**) methoden.

## <a name="binding"></a>Gebruikersinterface van data toohello binden

Gegevensbinding omvat drie onderdelen:

* Hallo-gegevensbron
* de indeling startscherm Hallo
* Hallo-adapter dat ties Hallo twee samen.

In onze voorbeeldcode we Hallo gegevens worden geretourneerd uit Hallo Mobile Apps SQL Azure-tabel **ToDoItem** in een matrix. Deze activiteit is een algemene patroon voor toepassingen van gegevens.  Databasequery's retourneren vaak een verzameling rijen die Hallo van client opgehaald in een lijst of een matrix. In dit voorbeeld is de matrix Hallo Hallo-gegevensbron.  Hallo-code bevat een indeling startscherm die Hallo-weergave van Hallo-gegevens die wordt weergegeven op Hallo apparaat definieert.  Hallo twee zijn gebonden samen met een netwerkadapter, die in deze code een uitbreiding van Hallo is **ArrayAdapter&lt;ToDoItem&gt;**  klasse.

#### <a name="layout"></a>Hallo indeling definiëren

Hallo-indeling wordt gedefinieerd door verschillende codefragmenten van XML-code. Uitgaande van een bestaande indeling, Hallo na code vertegenwoordigt Hallo **ListView** willen we toopopulate met onze gegevens van de server.

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

Hallo in Hallo voorafgaand aan code, *listitem* kenmerk bevat Hallo id Hallo lay-out voor een afzonderlijke rij in de lijst Hallo. Deze code geeft een selectievakje en de bijbehorende tekst en eenmaal voor elk item in de lijst Hallo opgehaald geïnstantieerd. Deze indeling wordt niet weergegeven Hallo **id** veld en een complexere indeling aanvullende velden geeft in Hallo weergeven. Deze code wordt Hallo **row_list_to_do.xml** bestand.

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <a name="adapter"></a>Hallo adapter definiëren
Omdat de gegevensbron Hallo van onze weergave een matrix met is **ToDoItem**, we subklasse onze-adapter van een **ArrayAdapter&lt;ToDoItem&gt;**  klasse. Deze subklasse produceert een weergave voor elke **ToDoItem** met Hallo **row_list_to_do** lay-out.  In onze code definiëren we de volgende klasse die is een uitbreiding van Hallo Hallo **ArrayAdapter&lt;E&gt;**  klasse:

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

Hallo adapters overschrijven **getView** methode. Bijvoorbeeld:

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

We geen exemplaar maken van deze klasse in onze activiteit als volgt:

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

Hallo tweede parameter toohello ToDoItemAdapter constructor is een verwijzing toohello-indeling. We kunnen nu Hallo instantiëren **ListView** en toewijzen van Hallo adapter toohello **ListView**.

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a>Hallo Adapter tooBind toohello gebruikersinterface gebruiken

U bent nu klaar toouse gegevensbinding. Hallo volgende code toont hoe tooget items in de tabel Hallo en opvulling lokale adapter Hallo Hello items geretourneerd.

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

Roep Hallo adapter elk gewenst moment wijzigen van Hallo **ToDoItem** tabel. Omdat wijzigingen op basis van door een andere record klaar bent, kunt u een enkele rij in plaats van een verzameling verwerken. Wanneer u een item invoegt, roept Hallo **toevoegen** methode op Hallo adapter; wanneer te verwijderen, roept u Hallo **verwijderen** methode.

U vindt een compleet voorbeeld in Hallo [Android Quick Start-Project][21].

## <a name="inserting"></a>Gegevens invoegen in Hallo back-end

Een instantie van Hallo *ToDoItem* klasse en stel de eigenschappen.

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

Gebruik vervolgens **insert()** tooinsert een object:

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

Hallo resultaatgegevens entiteit komt overeen met Hallo ingevoegd in de back-end-tabel hello, opgenomen Hallo-ID en andere waarden (zoals Hallo `createdAt`, `updatedAt`, en `version` velden) ingesteld op Hallo back-end.

Mobile Apps-tabellen vereisen een primaire sleutelkolom met de naam **id**. In deze kolom moet een tekenreeks zijn. de standaardwaarde Hallo van Hallo-ID-kolom is een GUID.  U kunt andere unieke waarden, zoals e-mailadressen of gebruikersnamen op te geven. Wanneer de waarde van een tekenreeks-ID niet voor een ingevoegde record opgegeven is, genereert Hallo back-end van een nieuwe GUID.

ID tekenreekswaarden bieden Hallo volgende voordelen:

* Id's kunnen worden gegenereerd zonder dat een round trip toohello-database.
* Records zijn eenvoudiger toomerge uit verschillende tabellen of databases.
* Id-waarden worden geïntegreerd beter met een toepassing logica.

Tekenreeks-ID-waarden zijn **REQUIRED** voor offlinesynchronisatie ondersteuning.  U kunt een Id niet wijzigen zodra deze is opgeslagen in Hallo back-end-database.

## <a name="updating"></a>Gegevens bijwerken in een mobiele app

tooupdate gegevens in een tabel, geeft het nieuwe object toohello hello **update()** methode.

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

In dit voorbeeld *item* is een verwijzing tooa rij in Hallo *ToDoItem* tabel, die een aantal wijzigingen aangebracht tooit heeft gehad.  Hallo rij Hello dezelfde **id** wordt bijgewerkt.

## <a name="deleting"></a>Gegevens in een mobiele app verwijderen

Hallo volgende code toont hoe toodelete gegevens uit een tabel door te geven Hallo gegevensobject.

```java
mToDoTable
    .delete(item);
```

U kunt ook een item verwijderen door op te geven Hallo **id** Hallo rij toodelete veld.

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a>Een specifiek item door-Id niet opzoeken

Opzoeken van een item met een specifieke **id** veld Hello **lookUp()** methode:

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a>Procedure: werken met niet-getypeerde gegevens

niet-getypeerde programmeermodel Hallo biedt u de precieze controle over de JSON-serialisatie.  Er zijn enkele algemene scenario's waarin u toouse een niet-getypeerde programmeermodel desgewenst kunt. Als bijvoorbeeld uw back-end-tabel veel kolommen bevat en u hoeft alleen een subset kolommen Hallo tooreference.  Hallo getypte model vereist toodefine alle Hallo kolommen gedefinieerd in Hallo Mobile Apps back-end in de gegevensklasse van uw.  De meeste Hallo API-aanroepen voor toegang tot gegevens lijken toohello getypt programming aanroepen. Hallo belangrijkste verschil is dat in de niet-getypeerde model Hallo u methoden niet voor Hallo aanroepen **MobileServiceJsonTable** object, in plaats van Hallo **MobileServiceTable** object.

### <a name="json_instance"></a>Geen exemplaar maken van een niet-getypeerde tabel

Vergelijkbare toohello model hebt getypt, u beginnen met het ophalen van een tabelverwijzing, maar in dit geval is een **MobileServicesJsonTable** object. Hallo verwijzing verkrijgen door de aanroepende Hallo **getTable** methode op een exemplaar van het Hallo-client:

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

Nadat u hebt gemaakt dat een exemplaar van Hallo **MobileServiceJsonTable**, het is vrijwel dezelfde API beschikbaar als met getypte programmeermodel Hallo Hallo. Hallo methoden maken gebruik van een niet-getypeerde parameter in plaats van een type parameter in sommige gevallen.

### <a name="json_insert"></a>Invoegen in een niet-getypeerde tabel
Hallo van de volgende code wordt getoond hoe toodo een INSERT-bewerking. Hallo eerste stap is toocreate een [JsonObject][1], die deel uitmaakt van Hallo [gson] [ 3] bibliotheek.

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

Vervolgens gebruikt u **insert()** tooinsert Hallo niet-getypeerde object in de tabel Hallo.

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

Als u tooget Hallo-ID van Hallo ingevoegd object moet, gebruikt u Hallo **getAsJsonPrimitive()** methode.

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a>Verwijderen uit een niet-getypeerde tabel
Hallo volgende code toont hoe toodelete een instantie, in dit geval Hallo hetzelfde exemplaar van een **JsonObject** die is gemaakt in de voorafgaande Hallo *invoegen* voorbeeld. Hallo code Hallo is hetzelfde als bij Hallo aanvraag opgegeven, maar Hallo-methode heeft een andere handtekening omdat deze verwijst naar een **JsonObject**.

```java
mToDoTable
    .delete(insertedItem);
```

U kunt ook een exemplaar rechtstreeks door met de bijbehorende ID verwijderen:

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a>Retourneert alle rijen uit een niet-getypeerde tabel
Hallo van de volgende code wordt getoond hoe tooretrieve een hele tabel. Omdat u een tabel JSON gebruikt, kunt u slechts enkele Hallo tabelkolommen selectief ophalen.

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

Hallo dezelfde set filteren, filteren en methoden die beschikbaar voor de getypte model Hallo zijn paging zijn beschikbaar voor niet-getypeerde Hallo-model.

## <a name="offline-sync"></a>Offlinesynchronisatie implementeren

offline synchronisatie van gegevens van implementeert Hello Azure Mobile Apps Client SDK ook met behulp van een SQLite-database toostore een kopie van servergegevens Hallo lokaal.  Bewerkingen die worden uitgevoerd op een offline tabel vereisen geen toowork mobiele connectiviteit.  Offline synchronisatie helpt prestaties op Hallo kosten van complexere logica voor conflictoplossing en herstelmogelijkheden.  Hallo Client-SDK van Azure Mobile Apps implementeert Hallo volgende kenmerken:

* Incrementele synchronisatie: Alleen bijgewerkt en nieuwe records worden gedownload verbruik van bandbreedte en geheugen.
* Optimistische gelijktijdigheid: Operations wordt aangenomen dat toosucceed.  Conflictoplossing wordt uitgesteld totdat de updates worden uitgevoerd op Hallo-server.
* Conflictoplossing: Hallo die SDK detecteert wanneer een wijziging in de conflicterende op Hallo-server is gemaakt en biedt Hiermee tooalert Hallo gebruiker.
* Voorlopig verwijderen: Verwijderde records zijn gemarkeerd als verwijderd, zodat andere apparaten tooupdate hun offline-cache.

### <a name="initialize-offline-sync"></a>Offlinesynchronisatie initialiseren

Elke tabel offline moet worden gedefinieerd in de offline cache Hallo vóór gebruik.  Normaal gesproken wordt tabeldefinitie uitgevoerd onmiddellijk nadat het maken van de Hallo van client Hallo:

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a>Een verwijzing toohello Offline cachetabel verkrijgen

Voor een online tabel, gebruikt u `.getTable()`.  Gebruik voor een offline tabel `.getSyncTable()`:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

Alle methoden die beschikbaar zijn voor online-tabellen (inclusief filteren, sorteren, paging, gegevens invoegen, bijwerken van gegevens en verwijderen van gegevens) evenveel werken Hallo goed in online als offline tabellen.

### <a name="synchronize-hello-local-offline-cache"></a>Hallo lokale Offline Cache synchroniseren

Synchronisatie is in het Hallo-besturingselement van uw app.  Hier volgt een voorbeeld van de synchronisatie-methode:

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

Als de naam van een query is opgegeven, toohello `.pull(query, queryname)` methode en vervolgens incrementele synchronisatie alleen gebruikte tooreturn de records die zijn gemaakt of gewijzigd sinds de laatste voltooid Hallo pull is.

### <a name="handle-conflicts-during-offline-synchronization"></a>Afhandeling van conflicten tijdens het Offline synchroniseren

Als een conflict zich tijdens voordoet een `.push()` bewerking, een `MobileServiceConflictException` gegenereerd.   Hallo server uitgegeven item is ingesloten in Hallo uitzondering en kan worden opgehaald door `.getItem()` op Hallo-uitzondering.  Hallo push door aanroepen Hallo volgende items op Hallo MobileServiceSyncContext object aan te passen:

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

Wanneer alle conflicten zijn gemarkeerd als u wilt, aanroepen `.push()` opnieuw tooresolve alle conflicten Hallo.

## <a name="custom-api"></a>Een aangepaste API aanroepen

Een aangepaste API kunt u toodefine aangepaste eindpunten die serverfunctionaliteit weergeven die geen toewijzen tooan invoegen, bijwerken, verwijderen of leesbewerking. Met behulp van een aangepaste API gebruiken, kunt u meer controle over messaging, hebben waaronder lezen en HTTP-bericht headers instellen en definiëren van een berichttekst de indeling dan JSON.

In een Android-client u Hallo aanroepen **invokeApi** methode toocall Hallo aangepaste API-eindpunt. Hallo volgende voorbeeld laat zien hoe toocall een API-eindpunt met de naam **completeAll**, die de klasse van een verzameling met de naam retourneert **MarkAllResult**.

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

Hallo **invokeApi** methode wordt aangeroepen op Hallo client verzendt een POST-aanvraag toohello nieuwe aangepaste API. Hallo-resultaat geretourneerd door de aangepaste API hello wordt weergegeven in een dialoogvenster weergegeven als er fouten zijn. Andere versies van **invokeApi** kunt u eventueel het verzenden van een object in de aanvraagtekst hello, Hallo HTTP-methode opgeven en queryparameters met Hallo aanvraag verzenden. Versies van getypeerde **invokeApi** ook worden geleverd.

## <a name="authentication"></a>Verificatie tooyour app toevoegen

Zelfstudies al in detail beschrijven hoe tooadd deze functies.

App Service ondersteunt [verifiëren van gebruikers van de app](app-service-mobile-android-get-started-users.md) met behulp van verschillende externe id-providers: Facebook, Google, Microsoft-Account, Twitter en Azure Active Directory. U kunt machtigingen instellen voor tabellen toorestrict toegang voor specifieke bewerkingen tooonly geverifieerde gebruikers. U kunt ook Hallo identiteit van de geverifieerde gebruikers tooimplement autorisatieregels gebruiken in uw back-end.

Twee verificatie stromen worden ondersteund: een **server** stroom en een **client** stroom. Hallo server stroom biedt Hallo eenvoudigste verificatie-ervaring, is afhankelijk van Hallo identiteit providers webinterface.  Er zijn geen extra SDK's zijn vereist tooimplement stroom serververificatie. Verificatie van de stroom biedt geen een diepe integratie op Hallo mobiel apparaat en wordt alleen aanbevolen voor bewijs van concept scenario's.

Hallo stroom kunt voor een betere integratie met apparaatspecifieke mogelijkheden, zoals het eenmalige aanmelding is afhankelijk van de SDK's die worden geleverd door de identiteitsprovider Hallo.  U kunt bijvoorbeeld Hallo Facebook SDK integreren in uw mobiele App.  Hallo mobiele clients worden omgewisseld in Hallo Facebook-app en bevestigt uw aanmelding voordat het wisselen van de mobiele app back tooyour.

Vier stappen zijn vereist tooenable verificatie in uw app:

* Uw app registreren voor verificatie met een id-provider.
* Configureer uw App Service-back-end.
* Tabel machtigingen tooauthenticated gebruikers alleen op Hallo App Service-back-end beperken.
* Verificatie code tooyour app toevoegen.

U kunt machtigingen instellen voor tabellen toorestrict toegang voor specifieke bewerkingen tooonly geverifieerde gebruikers. U kunt ook Hallo SID van een geverifieerde gebruiker toomodify aanvragen.  Raadpleeg voor meer informatie [aan de slag met verificatie] en Hallo procedure van Server SDK-documentatie.

### <a name="caching"></a>: Verificatiestroom Server

Hallo start volgende code een server stroom aanmelding met Hallo Google-provider.  Aanvullende configuratie is vereist vanwege Hallo beveiligingsvereisten voor Hallo Google-provider:

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

Daarnaast toevoegen Hallo methode toohello activiteit hoofdklasse te volgen:

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

Hallo `GOOGLE_LOGIN_REQUEST_CODE` gedefinieerd in uw belangrijkste activiteit wordt gebruikt voor Hallo `login()` methode en binnen Hallo `onActivityResult()` methode.  U kunt een uniek nummer, zolang hello hetzelfde nummer wordt gebruikt binnen Hallo `login()` methode en Hallo `onActivityResult()` methode.  Als u clientcode Hallo abstracte in een service-adapter (zoals eerder is weergegeven), moet u Hallo geschikte methoden aanroepen op Hallo service adapter.

U moet ook tooconfigure Hallo project voor customtabs.  Eerst een Omleidings-URL opgeven.  Hallo codefragment te volgen toevoegen`AndroidManifest.xml`:

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

Hallo toevoegen **redirectUriScheme** toohello `build.gradle` bestand voor uw toepassing:

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

Voeg `com.android.support:customtabs:23.0.1` toohello toepassingsafhankelijkheden in Hallo `build.gradle` bestand:

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

Hallo-ID van Hallo aangemelde gebruiker van opvragen een **MobileServiceUser** met Hallo **getUserId** methode. Zie voor een voorbeeld van hoe toouse Futures toocall Hallo asynchrone aanmelding API's, [aan de slag met verificatie].

> [!WARNING]
> Hallo vermeld URL-schema is hoofdlettergevoelig.  Zorg ervoor dat alle instanties van `{url_scheme_of_you_app}` hoofdlettergevoelig.

### <a name="caching"></a>Verificatietokens cache

Verificatietokens caching, moet u toostore Hallo gebruikers-ID en -verificatietoken lokaal op Hallo-apparaat. Hallo Hallo-app wordt gestart, zodra u Controleer Hallo-cache, en als deze waarden aanwezig zijn, kunt u overslaan Hallo-logboek in de procedure en rehydrate Hallo-client met deze gegevens. Deze gegevens is echter gevoelige en moeten worden opgeslagen voor de veiligheid versleuteld als Hallo telefoon wordt gestolen.  Ziet u een compleet voorbeeld van hoe toocache verificatie tokens in [verificatiesectie tokens in de Cache][7].

Wanneer u een verlopen token toouse probeert, krijgt u een *401-niet-geautoriseerde* antwoord. U kunt met behulp van filters verificatiefouten verwerken.  Filters onderscheppen aanvragen toohello back-end van App Service. Hallo filtercode test antwoord Hallo voor een 401, Hallo aanmelden proces wordt geactiveerd en wordt hervat Hallo-aanvraag die Hallo 401 gegenereerd.

### <a name="refresh"></a>Vernieuwen van Tokens gebruiken

Hallo-token geretourneerd door de Azure App Service-verificatie en autorisatie heeft een gedefinieerde levensduur van een uur.  Na deze periode, moet u Hallo gebruiker te verifiëren.  Als u Hallo met een lange levensduur token dat u hebt ontvangen via client-flow-verificatie en u kunt verifiëren met Azure App Service-verificatie en autorisatie hetzelfde token.  Een andere Azure App Service-token wordt gegenereerd met een nieuwe levensduur.

U kunt ook Hallo provider toouse vernieuwen Tokens registreren.  Een Token voor vernieuwen is niet altijd beschikbaar.  Er is aanvullende configuratie vereist:

* Voor **Azure Active Directory**, een clientgeheim voor hello Azure Active Directory-App configureren.  Geef Hallo clientgeheim in hello Azure App Service bij het configureren van Azure Active Directory-verificatie.  Bij het aanroepen van `.login()`, doorgeven `response_type=code id_token` als een parameter:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Voor **Google**, Hallo doorgeven `access_type=offline` als een parameter:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Voor **Microsoft-Account**, selecteer Hallo `wl.offline_access` bereik.

aanroepen van een token toorefresh `.refreshUser()`:

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

Als een best practice een filter die een 401-respons van Hallo-server detecteert en toorefresh Hallo gebruikerstoken probeert te maken.

## <a name="log-in-with-client-flow-authentication"></a>Meld u aan met Client-flow-verificatie

Hallo algemene proces voor aangemeld met client-flow-verificatie is als volgt:

* Azure App Service-verificatie en autorisatie configureert als server-flow-verificatie.
* Hallo-verificatieprovider SDK voor verificatie tooproduce een toegangstoken integreren.
* Hallo aanroepen `.login()` methode als volgt:

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

Vervang Hallo `onSuccess()` methode met wat u code wilt toouse op een geslaagde aanmelding.  Hallo `{provider}` tekenreeks is een geldige provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, of **twitter**.  Als u aangepaste verificatie hebt geïmplementeerd, kunt u ook aangepaste verificatiecode provider hello gebruiken.

### <a name="adal"></a>Verificatie van gebruikers met Hallo Active Directory Authentication Library (ADAL)

U kunt Hallo Active Directory Authentication Library (ADAL) toosign gebruikers in uw toepassing met Azure Active Directory. Met behulp van de aanmelding van een client stroom is vaak beter toousing hello `loginAsync()` methoden zoals deze biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.

1. Uw mobiele app back-end voor aanmelding bij de AAD configureren door de volgende Hallo [hoe tooconfigure App Service voor Active Directory-aanmelding] [ 22] zelfstudie. Zorg ervoor dat toocomplete Hallo optionele stap voor het registreren van een systeemeigen clienttoepassing van.
2. ADAL installeren door het wijzigen van uw build.gradle-bestand tooinclude Hallo definities te volgen:

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. Hallo code tooyour toepassing te volgen, waardoor Hallo vervangingen volgende toevoegen:

* Vervang **INSERT-instantie-hier** met de naam van de Hallo van Hallo tenant waarin u uw toepassing hebt ingericht. Hallo-indeling moet https://login.microsoftonline.com/contoso.onmicrosoft.com.
* Vervang **INSERT RESOURCE-ID hier** met Hallo client-ID voor uw back-end voor de mobiele app. U kunt Hallo client-ID verkrijgen van Hallo **Geavanceerd** tabblad onder **Azure Active Directory-instellingen** in Hallo-portal.
* Vervang **INSERT-CLIENT-ID-hier** met client-ID Hallo u hebt gekopieerd uit Hallo native client-toepassing.
* Vervang **INSERT-OMLEIDINGS-URI-hier** aan uw site */.auth/login/done* eindpunt, met Hallo HTTPS-schema. Deze waarde moet er ongeveer te*https://contoso.azurewebsites.net/.auth/login/done*.

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <a name="filters"></a>Hallo Client-servercommunicatie aanpassen

Hallo clientverbinding is doorgaans een eenvoudige HTTP-verbinding met behulp van de onderliggende HTTP-bibliotheek geleverd met Hallo Android SDK Hallo.  Er zijn diverse redenen waarom u toochange zou willen die:

* U desgewenst een andere HTTP-bibliotheek tooadjust time-outs toouse.
* U wilt een voortgangsbalk tooprovide.
* U wilt tooadd een aangepaste header toosupport API management-functionaliteit.
* U wilt toointercept een mislukte reactie zodat u herauthenticatie kunt implementeren.
* Gewenste toolog back-end aanvragen tooan analytics-service.

### <a name="using-an-alternate-http-library"></a>Met behulp van een andere HTTP-bibliotheek

Hallo aanroepen `.setAndroidHttpClientFactory()` methode onmiddellijk na het maken van uw client-verwijzing.  In dit voorbeeld tooset Hallo verbinding time-out too60 seconden (in plaats van Hallo standaard 10 seconden):

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a>Een Filter voortgang implementeren

U kunt een intercept van elke aanvraag implementeren door het implementeren van een `ServiceFilter`.  Bijvoorbeeld, updates Hallo volgende van een vooraf gemaakte voortgangsbalk:

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

U kunt dit filter toohello client als volgt toevoegen:

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a>Aanvraagheaders aanpassen

Gebruik de volgende Hallo `ServiceFilter` en koppelt u Hallo-filter in Hallo dezelfde manier als Hallo `ProgressFilter`:

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <a name="conversions"></a>Automatische serialisatie configureren

U kunt opgeven dat een strategie voor een conversie die van toepassing tooevery kolom is met behulp van Hallo [gson] [ 3] API. maakt gebruik van de Android clientbibliotheek Hallo [gson] [ 3] achter de schermen Hallo tooserialize Java objecten tooJSON gegevens voordat Hallo gegevens tooAzure App Service worden verzonden.  Hallo volgende code gebruikt Hallo **setFieldNamingStrategy()** methode tooset Hallo-strategie. In dit voorbeeld worden Hallo eerste teken (een ' m') en vervolgens kleine Hallo volgende teken voor elke veldnaam verwijderd. Bijvoorbeeld, zou het veranderen 'mId' in 'id'.  Implementeer een conversie strategie tooreduce Hallo nodig voor `SerializedName()` aantekeningen in de meeste velden.

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

Deze code moet worden uitgevoerd voordat het maken van een mobiele client-verwijzing met Hallo **MobileServiceClient**.

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[aan de slag met verificatie]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
