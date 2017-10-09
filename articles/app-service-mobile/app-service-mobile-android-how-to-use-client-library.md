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
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="4cec1-103">Hoe toouse Azure Mobile Apps SDK Hallo voor Android</span><span class="sxs-lookup"><span data-stu-id="4cec1-103">How toouse hello Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="4cec1-104">Deze handleiding wordt getoond hoe Hallo toouse Android client SDK voor Mobile Apps tooimplement algemene scenario's, zoals:</span><span class="sxs-lookup"><span data-stu-id="4cec1-104">This guide shows you how toouse hello Android client SDK for Mobile Apps tooimplement common scenarios, such as:</span></span>

* <span data-ttu-id="4cec1-105">Opvragen van gegevens (invoegen, bijwerken en verwijderen).</span><span class="sxs-lookup"><span data-stu-id="4cec1-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="4cec1-106">-Verificatie.</span><span class="sxs-lookup"><span data-stu-id="4cec1-106">Authentication.</span></span>
* <span data-ttu-id="4cec1-107">Foutafhandeling.</span><span class="sxs-lookup"><span data-stu-id="4cec1-107">Handling errors.</span></span>
* <span data-ttu-id="4cec1-108">Hallo-client aanpassen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-108">Customizing hello client.</span></span>

<span data-ttu-id="4cec1-109">Deze handleiding is gericht op Hallo clientzijde Android SDK.</span><span class="sxs-lookup"><span data-stu-id="4cec1-109">This guide focuses on hello client-side Android SDK.</span></span>  <span data-ttu-id="4cec1-110">informatie over hello serverzijde SDK's voor mobiele Apps, Zie toolearn [werken met .NET back-end SDK] [ 10] of [hoe toouse back-end voor Node.js SDK Hallo] [ 11].</span><span class="sxs-lookup"><span data-stu-id="4cec1-110">toolearn more about hello server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How toouse hello Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="4cec1-111">Naslagdocumentatie</span><span class="sxs-lookup"><span data-stu-id="4cec1-111">Reference Documentation</span></span>

<span data-ttu-id="4cec1-112">U vindt Hallo [Javadocs API-referentiemateriaal] [ 12] voor Android clientbibliotheek Hallo op GitHub.</span><span class="sxs-lookup"><span data-stu-id="4cec1-112">You can find hello [Javadocs API reference][12] for hello Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="4cec1-113">Ondersteunde Platforms</span><span class="sxs-lookup"><span data-stu-id="4cec1-113">Supported Platforms</span></span>

<span data-ttu-id="4cec1-114">Hello Azure Mobile Apps SDK voor Android ondersteunt API niveaus 19 tot en met 24 (KitKat via deze) voor de telefoon en tablet vormfactoren.</span><span class="sxs-lookup"><span data-stu-id="4cec1-114">hello Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="4cec1-115">Verificatie, met name maakt gebruik van een algemene web framework benadering toogather gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="4cec1-115">Authentication, in particular, utilizes a common web framework approach toogather credentials.</span></span>  <span data-ttu-id="4cec1-116">Server-flow-verificatie werkt niet met kleine formulier factor apparaten zoals kijkt naar.</span><span class="sxs-lookup"><span data-stu-id="4cec1-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="4cec1-117">Het installatieprogramma en vereisten</span><span class="sxs-lookup"><span data-stu-id="4cec1-117">Setup and Prerequisites</span></span>

<span data-ttu-id="4cec1-118">Volledige Hallo [Mobile Apps Quick Start](app-service-mobile-android-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4cec1-118">Complete hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="4cec1-119">Deze taak zorgt ervoor dat alle vereisten voor het ontwikkelen van Azure Mobile Apps is voldaan.</span><span class="sxs-lookup"><span data-stu-id="4cec1-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="4cec1-120">Hallo Quick Start helpt u bij het configureren van uw account en uw eerste back-end voor mobiele apps te maken.</span><span class="sxs-lookup"><span data-stu-id="4cec1-120">hello Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="4cec1-121">Als u geen toocomplete Hallo Quick Start-zelfstudie besluit, voltooit u Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cec1-121">If you decide not toocomplete hello Quickstart tutorial, complete hello following tasks:</span></span>

* <span data-ttu-id="4cec1-122">[Maak een back-end voor de mobiele App] [ 13] toouse met uw Android-app.</span><span class="sxs-lookup"><span data-stu-id="4cec1-122">[create a Mobile App backend][13] toouse with your Android app.</span></span>
* <span data-ttu-id="4cec1-123">In Android Studio [update Hallo Gradle bouwen bestanden](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="4cec1-123">In Android Studio, [update hello Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="4cec1-124">[Internet-machtiging wordt ingeschakeld](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="4cec1-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="4cec1-125"><a name="gradle-build"></a>Update Hallo Gradle-bestand maken</span><span class="sxs-lookup"><span data-stu-id="4cec1-125"><a name="gradle-build"></a>Update hello Gradle build file</span></span>

<span data-ttu-id="4cec1-126">Beide wijzigen **build.gradle** bestanden:</span><span class="sxs-lookup"><span data-stu-id="4cec1-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="4cec1-127">Voeg deze code toohello *Project* niveau **build.gradle** bestand in de Hallo *buildscript* tag:</span><span class="sxs-lookup"><span data-stu-id="4cec1-127">Add this code toohello *Project* level **build.gradle** file inside hello *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="4cec1-128">Voeg deze code toohello *Module app* niveau **build.gradle** bestand in de Hallo *afhankelijkheden* tag:</span><span class="sxs-lookup"><span data-stu-id="4cec1-128">Add this code toohello *Module app* level **build.gradle** file inside hello *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="4cec1-129">De meest recente versie Hallo is momenteel 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="4cec1-129">Currently hello latest version is 3.3.0.</span></span> <span data-ttu-id="4cec1-130">Hallo ondersteund versies worden weergegeven [op bintray][14].</span><span class="sxs-lookup"><span data-stu-id="4cec1-130">hello supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="4cec1-131"><a name="enable-internet"></a>Internet-machtiging wordt ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="4cec1-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="4cec1-132">tooaccess Azure, uw app moet gemachtigd Hallo INTERNET ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4cec1-132">tooaccess Azure, your app must have hello INTERNET permission enabled.</span></span> <span data-ttu-id="4cec1-133">Als deze nog niet is ingeschakeld, toevoegen Hallo volgende regel code tooyour **AndroidManifest.xml** bestand:</span><span class="sxs-lookup"><span data-stu-id="4cec1-133">If it's not already enabled, add hello following line of code tooyour **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="4cec1-134">Een clientverbinding maken</span><span class="sxs-lookup"><span data-stu-id="4cec1-134">Create a Client Connection</span></span>

<span data-ttu-id="4cec1-135">Mobiele Apps van Azure biedt vier functies tooyour mobiele toepassing:</span><span class="sxs-lookup"><span data-stu-id="4cec1-135">Azure Mobile Apps provides four functions tooyour mobile application:</span></span>

* <span data-ttu-id="4cec1-136">Toegang tot gegevens en Offline synchronisatie met een Azure Mobile Apps-Service.</span><span class="sxs-lookup"><span data-stu-id="4cec1-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="4cec1-137">Aangepaste API's die zijn geschreven met hello Azure Mobile Apps Server SDK-aanroep.</span><span class="sxs-lookup"><span data-stu-id="4cec1-137">Call Custom APIs written with hello Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="4cec1-138">Verificatie met Azure App Service-verificatie en autorisatie.</span><span class="sxs-lookup"><span data-stu-id="4cec1-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="4cec1-139">Registratie bij Notification Hubs voor pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="4cec1-140">Elk van deze functies, moet u eerst dat u maakt een `MobileServiceClient` object.</span><span class="sxs-lookup"><span data-stu-id="4cec1-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="4cec1-141">Slechts één `MobileServiceClient` object moet worden gemaakt binnen uw mobiele clients (dat wil zeggen, deze moet een Singleton-patroon).</span><span class="sxs-lookup"><span data-stu-id="4cec1-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="4cec1-142">toocreate een `MobileServiceClient` object:</span><span class="sxs-lookup"><span data-stu-id="4cec1-142">toocreate a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

<span data-ttu-id="4cec1-143">Hallo `<MobileAppUrl>` is een tekenreeks of een URL-object dat tooyour mobiele back-end wijst.</span><span class="sxs-lookup"><span data-stu-id="4cec1-143">hello `<MobileAppUrl>` is either a string or a URL object that points tooyour mobile backend.</span></span>  <span data-ttu-id="4cec1-144">Als u van Azure App Service-toohost uw mobiele back-end gebruikmaakt, zorgt u beveiligde Hallo `https://` versie van het Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="4cec1-144">If you are using Azure App Service toohost your mobile backend, then ensure you use hello secure `https://` version of hello URL.</span></span>

<span data-ttu-id="4cec1-145">Hallo-client vereist ook toegang toohello activiteit of Context - hello `this` parameter in Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4cec1-145">hello client also requires access toohello Activity or Context - hello `this` parameter in hello example.</span></span>  <span data-ttu-id="4cec1-146">Hallo MobileServiceClient bouw moet gebeuren binnen Hallo `onCreate()` methode van de activiteit waarnaar wordt verwezen in Hallo Hallo `AndroidManifest.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="4cec1-146">hello MobileServiceClient construction should happen within hello `onCreate()` method of hello Activity referenced in hello `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="4cec1-147">Als een best practice moet u communicatie tussen de server in een eigen (singleton-pattern)-klasse als abstract.</span><span class="sxs-lookup"><span data-stu-id="4cec1-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="4cec1-148">In dit geval moet u doorgeven Hallo activiteit binnen Hallo constructor tooappropriately Hallo service configureren.</span><span class="sxs-lookup"><span data-stu-id="4cec1-148">In this case, you should pass hello Activity within hello constructor tooappropriately configure hello service.</span></span>  <span data-ttu-id="4cec1-149">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4cec1-149">For example:</span></span>

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

<span data-ttu-id="4cec1-150">U kunt nu aanroepen `AzureServiceAdapter.Initialize(this);` in Hallo `onCreate()` methode van uw belangrijkste activiteit.</span><span class="sxs-lookup"><span data-stu-id="4cec1-150">You can now call `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="4cec1-151">Alle andere methoden hoeven toohello toegangsclient gebruiken `AzureServiceAdapter.getInstance();` tooobtain een verwijzing naar een toohello adapter.</span><span class="sxs-lookup"><span data-stu-id="4cec1-151">Any other methods needing access toohello client use `AzureServiceAdapter.getInstance();` tooobtain a reference toohello service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="4cec1-152">Gegevensbewerkingen</span><span class="sxs-lookup"><span data-stu-id="4cec1-152">Data Operations</span></span>

<span data-ttu-id="4cec1-153">Hallo-kern van hello Azure Mobile Apps SDK is tooprovide toegang toodata opgeslagen in SQL Azure op Hallo-backend voor mobiele Apps.</span><span class="sxs-lookup"><span data-stu-id="4cec1-153">hello core of hello Azure Mobile Apps SDK is tooprovide access toodata stored within SQL Azure on hello Mobile App backend.</span></span>  <span data-ttu-id="4cec1-154">U kunt toegang tot deze gegevens met behulp van sterk getypeerde klassen (aanbevolen) of getypeerde query's (niet aanbevolen).</span><span class="sxs-lookup"><span data-stu-id="4cec1-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="4cec1-155">Hallo bulksgewijs van deze sectie behandelt sterk getypeerde klassen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4cec1-155">hello bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="4cec1-156">Definiëren van gegevensklassen client</span><span class="sxs-lookup"><span data-stu-id="4cec1-156">Define client data classes</span></span>

<span data-ttu-id="4cec1-157">tooaccess gegevens uit SQL Azure-tabellen, definiëren van gegevensklassen client die overeenkomen met toohello tabellen in de back-end van Hallo mobiele App.</span><span class="sxs-lookup"><span data-stu-id="4cec1-157">tooaccess data from SQL Azure tables, define client data classes that correspond toohello tables in hello Mobile App backend.</span></span> <span data-ttu-id="4cec1-158">Voorbeelden in dit onderwerp wordt ervan uitgegaan dat een tabel met de naam **MyDataTable**, heeft Hallo kolommen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cec1-158">Examples in this topic assume a table named **MyDataTable**, which has hello following columns:</span></span>

* <span data-ttu-id="4cec1-159">id</span><span class="sxs-lookup"><span data-stu-id="4cec1-159">id</span></span>
* <span data-ttu-id="4cec1-160">Tekst</span><span class="sxs-lookup"><span data-stu-id="4cec1-160">text</span></span>
* <span data-ttu-id="4cec1-161">Voltooien</span><span class="sxs-lookup"><span data-stu-id="4cec1-161">complete</span></span>

<span data-ttu-id="4cec1-162">Hallo bijbehorende getypte client-side '-object bevindt zich in een bestand met de naam **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="4cec1-162">hello corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="4cec1-163">Voeg de getter en setter methoden voor elk veld dat u toevoegt.</span><span class="sxs-lookup"><span data-stu-id="4cec1-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="4cec1-164">Als uw Azure SQL-tabel meer kolommen bevat, zou u Hallo overeenkomende velden toothis klasse toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-164">If your SQL Azure table contains more columns, you would add hello corresponding fields toothis class.</span></span>  <span data-ttu-id="4cec1-165">Bijvoorbeeld, als hello DTO (object data transfer) was een kolom met gehele getallen prioriteit en u kunt dit veld samen met de methoden getter en setter toevoegen:</span><span class="sxs-lookup"><span data-stu-id="4cec1-165">For example, if hello DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

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

<span data-ttu-id="4cec1-166">toolearn hoe toocreate aanvullende tabellen in uw Mobile Apps back-end, Zie [hoe: Definieer een controller tabel] [ 15] (.NET-backend) of [definiëren tabellen met behulp van een dynamische Schema] [ 16] (Node.js back-end).</span><span class="sxs-lookup"><span data-stu-id="4cec1-166">toolearn how toocreate additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="4cec1-167">Een tabel van de back-end van Azure Mobile Apps definieert vijf speciale velden waarvan vier tooclients beschikbaar zijn:</span><span class="sxs-lookup"><span data-stu-id="4cec1-167">An Azure Mobile Apps backend table defines five special fields, four of which are available tooclients:</span></span>

* <span data-ttu-id="4cec1-168">`String id`: globaal unieke ID voor de record Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4cec1-168">`String id`: hello globally unique ID for hello record.</span></span>  <span data-ttu-id="4cec1-169">Als een best practice maken Hallo id Hallo tekenreeksweergave van een [UUID] [ 17] object.</span><span class="sxs-lookup"><span data-stu-id="4cec1-169">As a best practice, make hello id hello String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="4cec1-170">`DateTimeOffset updatedAt`: datum/tijd van laatste update van Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4cec1-170">`DateTimeOffset updatedAt`: hello date/time of hello last update.</span></span>  <span data-ttu-id="4cec1-171">Hallo updatedAt veld is ingesteld door de server Hallo en nooit door uw clientcode moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4cec1-171">hello updatedAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="4cec1-172">`DateTimeOffset createdAt`: Hallo datum/tijd dat Hallo-object is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4cec1-172">`DateTimeOffset createdAt`: hello date/time that hello object was created.</span></span>  <span data-ttu-id="4cec1-173">Hallo createdAt veld is ingesteld door de server Hallo en nooit door uw clientcode moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4cec1-173">hello createdAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="4cec1-174">`byte[] version`: Normaal weergegeven als een tekenreeks, is Hallo-versie ook ingesteld door Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="4cec1-174">`byte[] version`: Normally represented as a string, hello version is also set by hello server.</span></span>
* <span data-ttu-id="4cec1-175">`boolean deleted`: Hiermee wordt aangegeven Hallo-record verwijderd maar nog niet is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4cec1-175">`boolean deleted`: Indicates that hello record has been deleted but not purged yet.</span></span>  <span data-ttu-id="4cec1-176">Gebruik geen `deleted` als in uw klasse-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="4cec1-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="4cec1-177">Hallo `id` veld is vereist.</span><span class="sxs-lookup"><span data-stu-id="4cec1-177">hello `id` field is required.</span></span>  <span data-ttu-id="4cec1-178">Hallo `updatedAt` veld en `version` veld worden gebruikt voor offlinesynchronisatie (voor incrementele synchronisatie en conflict respectievelijk).</span><span class="sxs-lookup"><span data-stu-id="4cec1-178">hello `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="4cec1-179">Hallo `createdAt` veld is een verwijzingsveld en niet wordt gebruikt door het Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="4cec1-179">hello `createdAt` field is a reference field and is not used by hello client.</span></span>  <span data-ttu-id="4cec1-180">Hallo-namen zijn 'in-the-wire' namen van eigenschappen Hallo en zijn niet aanpasbaar.</span><span class="sxs-lookup"><span data-stu-id="4cec1-180">hello names are "across-the-wire" names of hello properties and are not adjustable.</span></span>  <span data-ttu-id="4cec1-181">Echter kunt u een toewijzing tussen uw object en het Hallo 'in-the-wire' namen maken met behulp van Hallo [gson] [ 3] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="4cec1-181">However, you can create a mapping between your object and hello "across-the-wire" names using hello [gson][3] library.</span></span>  <span data-ttu-id="4cec1-182">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4cec1-182">For example:</span></span>

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

### <a name="create-a-table-reference"></a><span data-ttu-id="4cec1-183">De tabelverwijzing van een maken</span><span class="sxs-lookup"><span data-stu-id="4cec1-183">Create a Table Reference</span></span>

<span data-ttu-id="4cec1-184">tooaccess een tabel, maakt u eerst een [MobileServiceTable] [ 8] object door de aanroepende Hallo **getTable** methode op Hallo [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="4cec1-184">tooaccess a table, first create a [MobileServiceTable][8] object by calling hello **getTable** method on hello [MobileServiceClient][9].</span></span>  <span data-ttu-id="4cec1-185">Deze methode heeft twee overloads:</span><span class="sxs-lookup"><span data-stu-id="4cec1-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="4cec1-186">In de volgende code, Hallo **mClient** tooyour MobileServiceClient referentieobject is.</span><span class="sxs-lookup"><span data-stu-id="4cec1-186">In hello following code, **mClient** is a reference tooyour MobileServiceClient object.</span></span>  <span data-ttu-id="4cec1-187">Hallo eerste overbelasting wordt gebruikt waarbij Hallo klassenaam en tabelnaam Hallo zijn Hallo dezelfde en hello een worden in het Hallo Quick Start:</span><span class="sxs-lookup"><span data-stu-id="4cec1-187">hello first overload is used where hello class name and hello table name are hello same, and is hello one used in hello Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="4cec1-188">Hallo tweede overbelasting wordt gebruikt wanneer Hallo tabelnaam van de naam van de klasse Hallo afwijkt: de eerste parameter Hallo Hallo tabelnaam is.</span><span class="sxs-lookup"><span data-stu-id="4cec1-188">hello second overload is used when hello table name is different from hello class name: hello first parameter is hello table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="4cec1-189"><a name="query"></a>Een tabel met back-end</span><span class="sxs-lookup"><span data-stu-id="4cec1-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="4cec1-190">Eerst moet u een tabelverwijzing.</span><span class="sxs-lookup"><span data-stu-id="4cec1-190">First, obtain a table reference.</span></span>  <span data-ttu-id="4cec1-191">Vervolgens moet u een query uitvoeren op Hallo tabelverwijzing.</span><span class="sxs-lookup"><span data-stu-id="4cec1-191">Then execute a query on hello table reference.</span></span>  <span data-ttu-id="4cec1-192">Een query is een combinatie van:</span><span class="sxs-lookup"><span data-stu-id="4cec1-192">A query is any combination of:</span></span>

* <span data-ttu-id="4cec1-193">Een `.where()` [filter-component](#filtering).</span><span class="sxs-lookup"><span data-stu-id="4cec1-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="4cec1-194">Een `.orderBy()` [ordening component](#sorting).</span><span class="sxs-lookup"><span data-stu-id="4cec1-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="4cec1-195">Een `.select()` [veld selectiecomponent](#selection).</span><span class="sxs-lookup"><span data-stu-id="4cec1-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="4cec1-196">Een `.skip()` en `.top()` voor [wisselbare resultaten](#paging).</span><span class="sxs-lookup"><span data-stu-id="4cec1-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="4cec1-197">Hallo-componenten moeten worden opgenomen in het Hallo voorafgaand aan de volgorde.</span><span class="sxs-lookup"><span data-stu-id="4cec1-197">hello clauses must be presented in hello preceding order.</span></span>

### <span data-ttu-id="4cec1-198"><a name="filter"></a>Filteren van resultaten</span><span class="sxs-lookup"><span data-stu-id="4cec1-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="4cec1-199">Hallo algemene vorm van een query is:</span><span class="sxs-lookup"><span data-stu-id="4cec1-199">hello general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

<span data-ttu-id="4cec1-200">Hallo retourneert voorgaande voorbeeld alle resultaten (omhoog toohello maximale paginagrootte ingesteld door Hallo server).</span><span class="sxs-lookup"><span data-stu-id="4cec1-200">hello preceding example returns all results (up toohello maximum page size set by hello server).</span></span>  <span data-ttu-id="4cec1-201">Hallo `.execute()` methode Hallo query uitgevoerd op Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="4cec1-201">hello `.execute()` method executes hello query on hello backend.</span></span>  <span data-ttu-id="4cec1-202">Hallo-query is geconverteerde tooan [OData v3] [ 19] query vóór verzending toohello Mobile Apps back-end.</span><span class="sxs-lookup"><span data-stu-id="4cec1-202">hello query is converted tooan [OData v3][19] query before transmission toohello Mobile Apps backend.</span></span>  <span data-ttu-id="4cec1-203">Ontvangen converteert Hallo Mobile Apps-back-end Hallo-query naar een SQL-instructie voordat deze wordt uitgevoerd op Hallo Azure SQL-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="4cec1-203">On receipt, hello Mobile Apps backend converts hello query into an SQL statement before executing it on hello SQL Azure instance.</span></span>  <span data-ttu-id="4cec1-204">Aangezien netwerkactiviteit enige tijd neemt, Hallo `.execute()` methode retourneert een [ `ListenableFuture<E>` ] [ 18].</span><span class="sxs-lookup"><span data-stu-id="4cec1-204">Since network activity takes some time, hello `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="4cec1-205"><a name="filtering"></a>Geretourneerde gegevens filteren</span><span class="sxs-lookup"><span data-stu-id="4cec1-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="4cec1-206">Hallo na uitvoering van de query retourneert alle items van Hallo **ToDoItem** tabel waar **voltooid** gelijk is aan **false**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-206">hello following query execution returns all items from hello **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="4cec1-207">**mToDoTable** is Hallo toohello mobiele service verwijzingstabel die we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4cec1-207">**mToDoTable** is hello reference toohello mobile service table that we created previously.</span></span>

<span data-ttu-id="4cec1-208">Definieer een filter met de Hallo **waar** methodeaanroep op Hallo tabelverwijzing.</span><span class="sxs-lookup"><span data-stu-id="4cec1-208">Define a filter using hello **where** method call on hello table reference.</span></span> <span data-ttu-id="4cec1-209">Hallo **waar** methode wordt gevolgd door een **veld** methode gevolgd door een methode waarmee Hallo logische predikaat.</span><span class="sxs-lookup"><span data-stu-id="4cec1-209">hello **where** method is followed by a **field** method followed by a method that specifies hello logical predicate.</span></span> <span data-ttu-id="4cec1-210">Mogelijke predikaat methoden omvatten **eq** (is gelijk aan), **ne** (niet gelijk) **gt** (groter dan) **ge** (groter dan of gelijk zijn aan), **lt** (minder dan,) **RP** (kleiner dan of gelijk aan).</span><span class="sxs-lookup"><span data-stu-id="4cec1-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="4cec1-211">Deze methoden kunnen u vergelijken en tekenreeks velden toospecific waarden.</span><span class="sxs-lookup"><span data-stu-id="4cec1-211">These methods let you compare number and string fields toospecific values.</span></span>

<span data-ttu-id="4cec1-212">U kunt filteren op datums.</span><span class="sxs-lookup"><span data-stu-id="4cec1-212">You can filter on dates.</span></span> <span data-ttu-id="4cec1-213">Hallo volgende methoden kunnen u de hele datumveld Hallo of onderdelen van Hallo datum vergelijken: **jaar**, **maand**, **dag**, **uur**, **minuut**, en **tweede**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-213">hello following methods let you compare hello entire date field or parts of hello date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="4cec1-214">Hallo volgende voorbeeld wordt een filter toegevoegd voor artikelen waarvan *vervaldatum* gelijk is aan 2013.</span><span class="sxs-lookup"><span data-stu-id="4cec1-214">hello following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="4cec1-215">Hallo volgt ondersteuning voor complexe filters op tekenreeksvelden: **startsWith**, **endsWith**, **concat**, **subtekenreeks**, **indexOf**, **vervangen**, **toLower**, **toUpper**, **trim**, en  **lengte**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-215">hello following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="4cec1-216">Hallo na voorbeeld filters voor de tabel rijen waar hello *tekst* kolom begint met "PRI0."</span><span class="sxs-lookup"><span data-stu-id="4cec1-216">hello following example filters for table rows where hello *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="4cec1-217">Hallo volgende operator methoden worden ondersteund op numerieke velden: **toevoegen**, **sub**, **mul**, **div**, **mod**, **floor**, **maximum**, en **afronden**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-217">hello following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="4cec1-218">Hallo na voorbeeld filters voor de tabel rijen waar hello **duur** een even getal is.</span><span class="sxs-lookup"><span data-stu-id="4cec1-218">hello following example filters for table rows where hello **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="4cec1-219">U kunt predikaten met deze logische methoden combineren: **en**, **of** en **niet**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="4cec1-220">Hallo volgt combineert twee van de voorgaande voorbeelden Hallo.</span><span class="sxs-lookup"><span data-stu-id="4cec1-220">hello following example combines two of hello preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="4cec1-221">Groep en het nesten van logische operators:</span><span class="sxs-lookup"><span data-stu-id="4cec1-221">Group and nest logical operators:</span></span>

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

<span data-ttu-id="4cec1-222">Zie voor meer gedetailleerde discussie en voorbeelden van filteren, [verkennen Hallo rijke van Hallo Android client querymodel][20].</span><span class="sxs-lookup"><span data-stu-id="4cec1-222">For more detailed discussion and examples of filtering, see [Exploring hello richness of hello Android client query model][20].</span></span>

### <span data-ttu-id="4cec1-223"><a name="sorting"></a>Geretourneerde gegevens sorteren</span><span class="sxs-lookup"><span data-stu-id="4cec1-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="4cec1-224">Hallo volgende code retourneert alle items uit een tabel met **taken** gesorteerd door Hallo oplopende *tekst* veld.</span><span class="sxs-lookup"><span data-stu-id="4cec1-224">hello following code returns all items from a table of **ToDoItems** sorted ascending by hello *text* field.</span></span> <span data-ttu-id="4cec1-225">*mToDoTable* is Hallo toohello back-end verwijzingstabel die u eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="4cec1-225">*mToDoTable* is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="4cec1-226">de eerste parameter van Hallo Hallo **orderBy** methode is de naam van een tekenreeks gelijk toohello van Hallo veld op welke toosort.</span><span class="sxs-lookup"><span data-stu-id="4cec1-226">hello first parameter of hello **orderBy** method is a string equal toohello name of hello field on which toosort.</span></span> <span data-ttu-id="4cec1-227">Hallo maakt gebruik van de tweede parameter Hallo **QueryOrder** opsomming toospecify of toosort oplopende of aflopende.</span><span class="sxs-lookup"><span data-stu-id="4cec1-227">hello second parameter uses hello **QueryOrder** enumeration toospecify whether toosort ascending or descending.</span></span>  <span data-ttu-id="4cec1-228">Als u filtert met behulp van Hallo ***waar*** methode, Hallo ***waar*** methode moet worden aangeroepen voordat Hallo ***orderBy*** methode.</span><span class="sxs-lookup"><span data-stu-id="4cec1-228">If you are filtering using hello ***where*** method, hello ***where*** method must be invoked before hello ***orderBy*** method.</span></span>

### <span data-ttu-id="4cec1-229"><a name="selection"></a>Selecteer specifieke kolommen</span><span class="sxs-lookup"><span data-stu-id="4cec1-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="4cec1-230">Hallo volgende code laat zien hoe tooreturn alle items uit een tabel met **taken**, maar alleen toont Hallo **voltooid** en **tekst** velden.</span><span class="sxs-lookup"><span data-stu-id="4cec1-230">hello following code illustrates how tooreturn all items from a table of **ToDoItems**, but only displays hello **complete** and **text** fields.</span></span> <span data-ttu-id="4cec1-231">**mToDoTable** is Hallo toohello back-end verwijzingstabel die we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4cec1-231">**mToDoTable** is hello reference toohello backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="4cec1-232">functie van Hallo parameters toohello select zijn Hallo tekenreeksnamen van Hallo tabelkolommen die u tooreturn wilt.</span><span class="sxs-lookup"><span data-stu-id="4cec1-232">hello parameters toohello select function are hello string names of hello table's columns that you want tooreturn.</span></span>  <span data-ttu-id="4cec1-233">Hallo **Selecteer** methode moet toofollow methoden zoals **waar** en **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-233">hello **select** method needs toofollow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="4cec1-234">Het kan worden gevolgd door methoden zoals paginering **overslaan** en **boven**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="4cec1-235"><a name="paging"></a>Gegevens weergeven op pagina 's</span><span class="sxs-lookup"><span data-stu-id="4cec1-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="4cec1-236">Gegevens **altijd** geretourneerd op pagina's.</span><span class="sxs-lookup"><span data-stu-id="4cec1-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="4cec1-237">Hallo kunt u het maximum aantal records dat wordt geretourneerd is door Hallo-server ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4cec1-237">hello maximum number of records returned is set by hello server.</span></span>  <span data-ttu-id="4cec1-238">Als de client Hallo meer records vraagt, retourneert Hallo server Hallo kunt u het maximum aantal records.</span><span class="sxs-lookup"><span data-stu-id="4cec1-238">If hello client requests more records, then hello server returns hello maximum number of records.</span></span>  <span data-ttu-id="4cec1-239">Standaard is de maximale paginagrootte Hallo op Hallo server 50 records.</span><span class="sxs-lookup"><span data-stu-id="4cec1-239">By default, hello maximum page size on hello server is 50 records.</span></span>

<span data-ttu-id="4cec1-240">Hallo eerste voorbeeld laat zien hoe tooselect Hallo bovenste vijf items uit een tabel.</span><span class="sxs-lookup"><span data-stu-id="4cec1-240">hello first example shows how tooselect hello top five items from a table.</span></span> <span data-ttu-id="4cec1-241">Hallo query retourneert Hallo items van een tabel met **taken**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-241">hello query returns hello items from a table of **ToDoItems**.</span></span> <span data-ttu-id="4cec1-242">**mToDoTable** is Hallo toohello back-end verwijzingstabel die u eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="4cec1-242">**mToDoTable** is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="4cec1-243">Hier volgt een query of slaat het Hallo eerste vijf items en vervolgens retourneert de volgende vijf Hallo:</span><span class="sxs-lookup"><span data-stu-id="4cec1-243">Here's a query that skips hello first five items, and then returns hello next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="4cec1-244">Als u tooget alle records in een tabel wenst, moet u code tooiterate implementeren via alle pagina's:</span><span class="sxs-lookup"><span data-stu-id="4cec1-244">If you wish tooget all records in a table, implement code tooiterate over all pages:</span></span>

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

<span data-ttu-id="4cec1-245">Een aanvraag voor alle records met deze methode maakt een minimum van twee aanvragen toohello Mobile Apps back-end.</span><span class="sxs-lookup"><span data-stu-id="4cec1-245">A request for all records using this method creates a minimum of two requests toohello Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="4cec1-246">Kiezen Hallo rechts paginagrootte is een evenwicht tussen geheugengebruik tijdens het Hallo-aanvraag gebeurt er, bandbreedtegebruik en vertraging bij het ontvangen van gegevens Hallo volledig.</span><span class="sxs-lookup"><span data-stu-id="4cec1-246">Choosing hello right page size is a balance between memory usage while hello request is happening, bandwidth usage and delay in receiving hello data completely.</span></span>  <span data-ttu-id="4cec1-247">Hallo-standaard (50 records) is geschikt voor alle apparaten.</span><span class="sxs-lookup"><span data-stu-id="4cec1-247">hello default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="4cec1-248">Als u alleen op geheugenapparaten met grotere werkt, verhoogt u up too500.</span><span class="sxs-lookup"><span data-stu-id="4cec1-248">If you exclusively operate on larger memory devices, increase up too500.</span></span>  <span data-ttu-id="4cec1-249">We hebben die toenemende Hallo paginaformaat dan 500 registreert resultaten gevonden in onaanvaardbaar vertragingen en grote geheugenproblemen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-249">We have found that increasing hello page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="4cec1-250"><a name="chaining"></a>Hoe: querymethoden samenvoegen</span><span class="sxs-lookup"><span data-stu-id="4cec1-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="4cec1-251">Hallo-methoden die worden gebruikt bij het zoeken van back-end-tabellen kunnen worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="4cec1-251">hello methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="4cec1-252">Query methoden kunt u specifieke kolommen tooselect gefilterde rijen die worden gesorteerd en wisselbaar geheugen: chaining.</span><span class="sxs-lookup"><span data-stu-id="4cec1-252">Chaining query methods allows you tooselect specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="4cec1-253">U kunt complexe logische filters maken.</span><span class="sxs-lookup"><span data-stu-id="4cec1-253">You can create complex logical filters.</span></span>  <span data-ttu-id="4cec1-254">Elke querymethode retourneert een Query-object.</span><span class="sxs-lookup"><span data-stu-id="4cec1-254">Each query method returns a Query object.</span></span> <span data-ttu-id="4cec1-255">tooend hello reeks methoden en daadwerkelijk uitvoeren Hallo query, aanroep Hallo **uitvoeren** methode.</span><span class="sxs-lookup"><span data-stu-id="4cec1-255">tooend hello series of methods and actually run hello query, call hello **execute** method.</span></span> <span data-ttu-id="4cec1-256">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4cec1-256">For example:</span></span>

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

<span data-ttu-id="4cec1-257">Hallo teruggekoppeld query methoden moeten als volgt zijn gerangschikt:</span><span class="sxs-lookup"><span data-stu-id="4cec1-257">hello chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="4cec1-258">Filteren (**waar**) methoden.</span><span class="sxs-lookup"><span data-stu-id="4cec1-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="4cec1-259">Sorteren (**orderBy**) methoden.</span><span class="sxs-lookup"><span data-stu-id="4cec1-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="4cec1-260">Selectie (**Selecteer**) methoden.</span><span class="sxs-lookup"><span data-stu-id="4cec1-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="4cec1-261">wisselgeheugengebruik (**overslaan** en **boven**) methoden.</span><span class="sxs-lookup"><span data-stu-id="4cec1-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="4cec1-262"><a name="binding"></a>Gebruikersinterface van data toohello binden</span><span class="sxs-lookup"><span data-stu-id="4cec1-262"><a name="binding"></a>Bind data toohello user interface</span></span>

<span data-ttu-id="4cec1-263">Gegevensbinding omvat drie onderdelen:</span><span class="sxs-lookup"><span data-stu-id="4cec1-263">Data binding involves three components:</span></span>

* <span data-ttu-id="4cec1-264">Hallo-gegevensbron</span><span class="sxs-lookup"><span data-stu-id="4cec1-264">hello data source</span></span>
* <span data-ttu-id="4cec1-265">de indeling startscherm Hallo</span><span class="sxs-lookup"><span data-stu-id="4cec1-265">hello screen layout</span></span>
* <span data-ttu-id="4cec1-266">Hallo-adapter dat ties Hallo twee samen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-266">hello adapter that ties hello two together.</span></span>

<span data-ttu-id="4cec1-267">In onze voorbeeldcode we Hallo gegevens worden geretourneerd uit Hallo Mobile Apps SQL Azure-tabel **ToDoItem** in een matrix.</span><span class="sxs-lookup"><span data-stu-id="4cec1-267">In our sample code, we return hello data from hello Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="4cec1-268">Deze activiteit is een algemene patroon voor toepassingen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="4cec1-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="4cec1-269">Databasequery's retourneren vaak een verzameling rijen die Hallo van client opgehaald in een lijst of een matrix.</span><span class="sxs-lookup"><span data-stu-id="4cec1-269">Database queries often return a collection of rows that hello client gets in a list or array.</span></span> <span data-ttu-id="4cec1-270">In dit voorbeeld is de matrix Hallo Hallo-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="4cec1-270">In this sample, hello array is hello data source.</span></span>  <span data-ttu-id="4cec1-271">Hallo-code bevat een indeling startscherm die Hallo-weergave van Hallo-gegevens die wordt weergegeven op Hallo apparaat definieert.</span><span class="sxs-lookup"><span data-stu-id="4cec1-271">hello code specifies a screen layout that defines hello view of hello data that appears on hello device.</span></span>  <span data-ttu-id="4cec1-272">Hallo twee zijn gebonden samen met een netwerkadapter, die in deze code een uitbreiding van Hallo is **ArrayAdapter&lt;ToDoItem&gt;**  klasse.</span><span class="sxs-lookup"><span data-stu-id="4cec1-272">hello two are bound together with an adapter, which in this code is an extension of hello **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="4cec1-273"><a name="layout"></a>Hallo indeling definiëren</span><span class="sxs-lookup"><span data-stu-id="4cec1-273"><a name="layout"></a>Define hello Layout</span></span>

<span data-ttu-id="4cec1-274">Hallo-indeling wordt gedefinieerd door verschillende codefragmenten van XML-code.</span><span class="sxs-lookup"><span data-stu-id="4cec1-274">hello layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="4cec1-275">Uitgaande van een bestaande indeling, Hallo na code vertegenwoordigt Hallo **ListView** willen we toopopulate met onze gegevens van de server.</span><span class="sxs-lookup"><span data-stu-id="4cec1-275">Given an existing layout, hello following code represents hello **ListView** we want toopopulate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="4cec1-276">Hallo in Hallo voorafgaand aan code, *listitem* kenmerk bevat Hallo id Hallo lay-out voor een afzonderlijke rij in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="4cec1-276">In hello preceding code, hello *listitem* attribute specifies hello id of hello layout for an individual row in hello list.</span></span> <span data-ttu-id="4cec1-277">Deze code geeft een selectievakje en de bijbehorende tekst en eenmaal voor elk item in de lijst Hallo opgehaald geïnstantieerd.</span><span class="sxs-lookup"><span data-stu-id="4cec1-277">This code specifies a check box and its associated text and gets instantiated once for each item in hello list.</span></span> <span data-ttu-id="4cec1-278">Deze indeling wordt niet weergegeven Hallo **id** veld en een complexere indeling aanvullende velden geeft in Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="4cec1-278">This layout does not display hello **id** field, and a more complex layout would specify additional fields in hello display.</span></span> <span data-ttu-id="4cec1-279">Deze code wordt Hallo **row_list_to_do.xml** bestand.</span><span class="sxs-lookup"><span data-stu-id="4cec1-279">This code is in hello **row_list_to_do.xml** file.</span></span>

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

#### <span data-ttu-id="4cec1-280"><a name="adapter"></a>Hallo adapter definiëren</span><span class="sxs-lookup"><span data-stu-id="4cec1-280"><a name="adapter"></a>Define hello adapter</span></span>
<span data-ttu-id="4cec1-281">Omdat de gegevensbron Hallo van onze weergave een matrix met is **ToDoItem**, we subklasse onze-adapter van een **ArrayAdapter&lt;ToDoItem&gt;**  klasse.</span><span class="sxs-lookup"><span data-stu-id="4cec1-281">Since hello data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="4cec1-282">Deze subklasse produceert een weergave voor elke **ToDoItem** met Hallo **row_list_to_do** lay-out.</span><span class="sxs-lookup"><span data-stu-id="4cec1-282">This subclass produces a View for every **ToDoItem** using hello **row_list_to_do** layout.</span></span>  <span data-ttu-id="4cec1-283">In onze code definiëren we de volgende klasse die is een uitbreiding van Hallo Hallo **ArrayAdapter&lt;E&gt;**  klasse:</span><span class="sxs-lookup"><span data-stu-id="4cec1-283">In our code, we define hello following class that is an extension of hello **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="4cec1-284">Hallo adapters overschrijven **getView** methode.</span><span class="sxs-lookup"><span data-stu-id="4cec1-284">Override hello adapters **getView** method.</span></span> <span data-ttu-id="4cec1-285">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4cec1-285">For example:</span></span>

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

<span data-ttu-id="4cec1-286">We geen exemplaar maken van deze klasse in onze activiteit als volgt:</span><span class="sxs-lookup"><span data-stu-id="4cec1-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="4cec1-287">Hallo tweede parameter toohello ToDoItemAdapter constructor is een verwijzing toohello-indeling.</span><span class="sxs-lookup"><span data-stu-id="4cec1-287">hello second parameter toohello ToDoItemAdapter constructor is a reference toohello layout.</span></span> <span data-ttu-id="4cec1-288">We kunnen nu Hallo instantiëren **ListView** en toewijzen van Hallo adapter toohello **ListView**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-288">We can now instantiate hello **ListView** and assign hello adapter toohello **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="4cec1-289"><a name="use-adapter"></a>Hallo Adapter tooBind toohello gebruikersinterface gebruiken</span><span class="sxs-lookup"><span data-stu-id="4cec1-289"><a name="use-adapter"></a>Use hello Adapter tooBind toohello UI</span></span>

<span data-ttu-id="4cec1-290">U bent nu klaar toouse gegevensbinding.</span><span class="sxs-lookup"><span data-stu-id="4cec1-290">You are now ready toouse data binding.</span></span> <span data-ttu-id="4cec1-291">Hallo volgende code toont hoe tooget items in de tabel Hallo en opvulling lokale adapter Hallo Hello items geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="4cec1-291">hello following code shows how tooget items in hello table and fills hello local adapter with hello returned items.</span></span>

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

<span data-ttu-id="4cec1-292">Roep Hallo adapter elk gewenst moment wijzigen van Hallo **ToDoItem** tabel.</span><span class="sxs-lookup"><span data-stu-id="4cec1-292">Call hello adapter any time you modify hello **ToDoItem** table.</span></span> <span data-ttu-id="4cec1-293">Omdat wijzigingen op basis van door een andere record klaar bent, kunt u een enkele rij in plaats van een verzameling verwerken.</span><span class="sxs-lookup"><span data-stu-id="4cec1-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="4cec1-294">Wanneer u een item invoegt, roept Hallo **toevoegen** methode op Hallo adapter; wanneer te verwijderen, roept u Hallo **verwijderen** methode.</span><span class="sxs-lookup"><span data-stu-id="4cec1-294">When you insert an item, call hello **add** method on hello adapter; when deleting, call hello **remove** method.</span></span>

<span data-ttu-id="4cec1-295">U vindt een compleet voorbeeld in Hallo [Android Quick Start-Project][21].</span><span class="sxs-lookup"><span data-stu-id="4cec1-295">You can find a complete example in hello [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="4cec1-296"><a name="inserting"></a>Gegevens invoegen in Hallo back-end</span><span class="sxs-lookup"><span data-stu-id="4cec1-296"><a name="inserting"></a>Insert data into hello backend</span></span>

<span data-ttu-id="4cec1-297">Een instantie van Hallo *ToDoItem* klasse en stel de eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-297">Instantiate an instance of hello *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="4cec1-298">Gebruik vervolgens **insert()** tooinsert een object:</span><span class="sxs-lookup"><span data-stu-id="4cec1-298">Then use **insert()** tooinsert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="4cec1-299">Hallo resultaatgegevens entiteit komt overeen met Hallo ingevoegd in de back-end-tabel hello, opgenomen Hallo-ID en andere waarden (zoals Hallo `createdAt`, `updatedAt`, en `version` velden) ingesteld op Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="4cec1-299">hello returned entity matches hello data inserted into hello backend table, included hello ID and any other values (such as hello `createdAt`, `updatedAt`, and `version` fields) set on hello backend.</span></span>

<span data-ttu-id="4cec1-300">Mobile Apps-tabellen vereisen een primaire sleutelkolom met de naam **id**. In deze kolom moet een tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="4cec1-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span></span> <span data-ttu-id="4cec1-301">de standaardwaarde Hallo van Hallo-ID-kolom is een GUID.</span><span class="sxs-lookup"><span data-stu-id="4cec1-301">hello default value of hello ID column is a GUID.</span></span>  <span data-ttu-id="4cec1-302">U kunt andere unieke waarden, zoals e-mailadressen of gebruikersnamen op te geven.</span><span class="sxs-lookup"><span data-stu-id="4cec1-302">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="4cec1-303">Wanneer de waarde van een tekenreeks-ID niet voor een ingevoegde record opgegeven is, genereert Hallo back-end van een nieuwe GUID.</span><span class="sxs-lookup"><span data-stu-id="4cec1-303">When a string ID value is not provided for an inserted record, hello backend generates a new GUID.</span></span>

<span data-ttu-id="4cec1-304">ID tekenreekswaarden bieden Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="4cec1-304">String ID values provide hello following advantages:</span></span>

* <span data-ttu-id="4cec1-305">Id's kunnen worden gegenereerd zonder dat een round trip toohello-database.</span><span class="sxs-lookup"><span data-stu-id="4cec1-305">IDs can be generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="4cec1-306">Records zijn eenvoudiger toomerge uit verschillende tabellen of databases.</span><span class="sxs-lookup"><span data-stu-id="4cec1-306">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="4cec1-307">Id-waarden worden geïntegreerd beter met een toepassing logica.</span><span class="sxs-lookup"><span data-stu-id="4cec1-307">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="4cec1-308">Tekenreeks-ID-waarden zijn **REQUIRED** voor offlinesynchronisatie ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="4cec1-308">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="4cec1-309">U kunt een Id niet wijzigen zodra deze is opgeslagen in Hallo back-end-database.</span><span class="sxs-lookup"><span data-stu-id="4cec1-309">You cannot change an Id once it is stored in hello backend database.</span></span>

## <span data-ttu-id="4cec1-310"><a name="updating"></a>Gegevens bijwerken in een mobiele app</span><span class="sxs-lookup"><span data-stu-id="4cec1-310"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="4cec1-311">tooupdate gegevens in een tabel, geeft het nieuwe object toohello hello **update()** methode.</span><span class="sxs-lookup"><span data-stu-id="4cec1-311">tooupdate data in a table, pass hello new object toohello **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="4cec1-312">In dit voorbeeld *item* is een verwijzing tooa rij in Hallo *ToDoItem* tabel, die een aantal wijzigingen aangebracht tooit heeft gehad.</span><span class="sxs-lookup"><span data-stu-id="4cec1-312">In this example, *item* is a reference tooa row in hello *ToDoItem* table, which has had some changes made tooit.</span></span>  <span data-ttu-id="4cec1-313">Hallo rij Hello dezelfde **id** wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="4cec1-313">hello row with hello same **id** is updated.</span></span>

## <span data-ttu-id="4cec1-314"><a name="deleting"></a>Gegevens in een mobiele app verwijderen</span><span class="sxs-lookup"><span data-stu-id="4cec1-314"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="4cec1-315">Hallo volgende code toont hoe toodelete gegevens uit een tabel door te geven Hallo gegevensobject.</span><span class="sxs-lookup"><span data-stu-id="4cec1-315">hello following code shows how toodelete data from a table by specifying hello data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="4cec1-316">U kunt ook een item verwijderen door op te geven Hallo **id** Hallo rij toodelete veld.</span><span class="sxs-lookup"><span data-stu-id="4cec1-316">You can also delete an item by specifying hello **id** field of hello row toodelete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="4cec1-317"><a name="lookup"></a>Een specifiek item door-Id niet opzoeken</span><span class="sxs-lookup"><span data-stu-id="4cec1-317"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="4cec1-318">Opzoeken van een item met een specifieke **id** veld Hello **lookUp()** methode:</span><span class="sxs-lookup"><span data-stu-id="4cec1-318">Look up an item with a specific **id** field with hello **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="4cec1-319"><a name="untyped"></a>Procedure: werken met niet-getypeerde gegevens</span><span class="sxs-lookup"><span data-stu-id="4cec1-319"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="4cec1-320">niet-getypeerde programmeermodel Hallo biedt u de precieze controle over de JSON-serialisatie.</span><span class="sxs-lookup"><span data-stu-id="4cec1-320">hello untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="4cec1-321">Er zijn enkele algemene scenario's waarin u toouse een niet-getypeerde programmeermodel desgewenst kunt.</span><span class="sxs-lookup"><span data-stu-id="4cec1-321">There are some common scenarios where you may wish toouse an untyped programming model.</span></span> <span data-ttu-id="4cec1-322">Als bijvoorbeeld uw back-end-tabel veel kolommen bevat en u hoeft alleen een subset kolommen Hallo tooreference.</span><span class="sxs-lookup"><span data-stu-id="4cec1-322">For example, if your backend table contains many columns and you only need tooreference a subset of hello columns.</span></span>  <span data-ttu-id="4cec1-323">Hallo getypte model vereist toodefine alle Hallo kolommen gedefinieerd in Hallo Mobile Apps back-end in de gegevensklasse van uw.</span><span class="sxs-lookup"><span data-stu-id="4cec1-323">hello typed model requires you toodefine all hello columns defined in hello Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="4cec1-324">De meeste Hallo API-aanroepen voor toegang tot gegevens lijken toohello getypt programming aanroepen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-324">Most of hello API calls for accessing data are similar toohello typed programming calls.</span></span> <span data-ttu-id="4cec1-325">Hallo belangrijkste verschil is dat in de niet-getypeerde model Hallo u methoden niet voor Hallo aanroepen **MobileServiceJsonTable** object, in plaats van Hallo **MobileServiceTable** object.</span><span class="sxs-lookup"><span data-stu-id="4cec1-325">hello main difference is that in hello untyped model you invoke methods on hello **MobileServiceJsonTable** object, instead of hello **MobileServiceTable** object.</span></span>

### <span data-ttu-id="4cec1-326"><a name="json_instance"></a>Geen exemplaar maken van een niet-getypeerde tabel</span><span class="sxs-lookup"><span data-stu-id="4cec1-326"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="4cec1-327">Vergelijkbare toohello model hebt getypt, u beginnen met het ophalen van een tabelverwijzing, maar in dit geval is een **MobileServicesJsonTable** object.</span><span class="sxs-lookup"><span data-stu-id="4cec1-327">Similar toohello typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="4cec1-328">Hallo verwijzing verkrijgen door de aanroepende Hallo **getTable** methode op een exemplaar van het Hallo-client:</span><span class="sxs-lookup"><span data-stu-id="4cec1-328">Obtain hello reference by calling hello **getTable** method on an instance of hello client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="4cec1-329">Nadat u hebt gemaakt dat een exemplaar van Hallo **MobileServiceJsonTable**, het is vrijwel dezelfde API beschikbaar als met getypte programmeermodel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4cec1-329">Once you have created an instance of hello **MobileServiceJsonTable**, it has virtually hello same API available as with hello typed programming model.</span></span> <span data-ttu-id="4cec1-330">Hallo methoden maken gebruik van een niet-getypeerde parameter in plaats van een type parameter in sommige gevallen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-330">In some cases, hello methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="4cec1-331"><a name="json_insert"></a>Invoegen in een niet-getypeerde tabel</span><span class="sxs-lookup"><span data-stu-id="4cec1-331"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="4cec1-332">Hallo van de volgende code wordt getoond hoe toodo een INSERT-bewerking.</span><span class="sxs-lookup"><span data-stu-id="4cec1-332">hello following code shows how toodo an insert.</span></span> <span data-ttu-id="4cec1-333">Hallo eerste stap is toocreate een [JsonObject][1], die deel uitmaakt van Hallo [gson] [ 3] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="4cec1-333">hello first step is toocreate a [JsonObject][1], which is part of hello [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="4cec1-334">Vervolgens gebruikt u **insert()** tooinsert Hallo niet-getypeerde object in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="4cec1-334">Then, Use **insert()** tooinsert hello untyped object into hello table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="4cec1-335">Als u tooget Hallo-ID van Hallo ingevoegd object moet, gebruikt u Hallo **getAsJsonPrimitive()** methode.</span><span class="sxs-lookup"><span data-stu-id="4cec1-335">If you need tooget hello ID of hello inserted object, use hello **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="4cec1-336"><a name="json_delete"></a>Verwijderen uit een niet-getypeerde tabel</span><span class="sxs-lookup"><span data-stu-id="4cec1-336"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="4cec1-337">Hallo volgende code toont hoe toodelete een instantie, in dit geval Hallo hetzelfde exemplaar van een **JsonObject** die is gemaakt in de voorafgaande Hallo *invoegen* voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4cec1-337">hello following code shows how toodelete an instance, in this case, hello same instance of a **JsonObject** that was created in hello prior *insert* example.</span></span> <span data-ttu-id="4cec1-338">Hallo code Hallo is hetzelfde als bij Hallo aanvraag opgegeven, maar Hallo-methode heeft een andere handtekening omdat deze verwijst naar een **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-338">hello code is hello same as with hello typed case, but hello method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="4cec1-339">U kunt ook een exemplaar rechtstreeks door met de bijbehorende ID verwijderen:</span><span class="sxs-lookup"><span data-stu-id="4cec1-339">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="4cec1-340"><a name="json_get"></a>Retourneert alle rijen uit een niet-getypeerde tabel</span><span class="sxs-lookup"><span data-stu-id="4cec1-340"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="4cec1-341">Hallo van de volgende code wordt getoond hoe tooretrieve een hele tabel.</span><span class="sxs-lookup"><span data-stu-id="4cec1-341">hello following code shows how tooretrieve an entire table.</span></span> <span data-ttu-id="4cec1-342">Omdat u een tabel JSON gebruikt, kunt u slechts enkele Hallo tabelkolommen selectief ophalen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-342">Since you are using a JSON Table, you can selectively retrieve only some of hello table's columns.</span></span>

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

<span data-ttu-id="4cec1-343">Hallo dezelfde set filteren, filteren en methoden die beschikbaar voor de getypte model Hallo zijn paging zijn beschikbaar voor niet-getypeerde Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="4cec1-343">hello same set of filtering, filtering and paging methods that are available for hello typed model are available for hello untyped model.</span></span>

## <span data-ttu-id="4cec1-344"><a name="offline-sync"></a>Offlinesynchronisatie implementeren</span><span class="sxs-lookup"><span data-stu-id="4cec1-344"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="4cec1-345">offline synchronisatie van gegevens van implementeert Hello Azure Mobile Apps Client SDK ook met behulp van een SQLite-database toostore een kopie van servergegevens Hallo lokaal.</span><span class="sxs-lookup"><span data-stu-id="4cec1-345">hello Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database toostore a copy of hello server data locally.</span></span>  <span data-ttu-id="4cec1-346">Bewerkingen die worden uitgevoerd op een offline tabel vereisen geen toowork mobiele connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="4cec1-346">Operations performed on an offline table do not require mobile connectivity toowork.</span></span>  <span data-ttu-id="4cec1-347">Offline synchronisatie helpt prestaties op Hallo kosten van complexere logica voor conflictoplossing en herstelmogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="4cec1-347">Offline sync aids in resilience and performance at hello expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="4cec1-348">Hallo Client-SDK van Azure Mobile Apps implementeert Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="4cec1-348">hello Azure Mobile Apps Client SDK implements hello following features:</span></span>

* <span data-ttu-id="4cec1-349">Incrementele synchronisatie: Alleen bijgewerkt en nieuwe records worden gedownload verbruik van bandbreedte en geheugen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="4cec1-350">Optimistische gelijktijdigheid: Operations wordt aangenomen dat toosucceed.</span><span class="sxs-lookup"><span data-stu-id="4cec1-350">Optimistic Concurrency: Operations are assumed toosucceed.</span></span>  <span data-ttu-id="4cec1-351">Conflictoplossing wordt uitgesteld totdat de updates worden uitgevoerd op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="4cec1-351">Conflict Resolution is deferred until updates are performed on hello server.</span></span>
* <span data-ttu-id="4cec1-352">Conflictoplossing: Hallo die SDK detecteert wanneer een wijziging in de conflicterende op Hallo-server is gemaakt en biedt Hiermee tooalert Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4cec1-352">Conflict Resolution: hello SDK detects when a conflicting change has been made at hello server and provides hooks tooalert hello user.</span></span>
* <span data-ttu-id="4cec1-353">Voorlopig verwijderen: Verwijderde records zijn gemarkeerd als verwijderd, zodat andere apparaten tooupdate hun offline-cache.</span><span class="sxs-lookup"><span data-stu-id="4cec1-353">Soft Delete: Deleted records are marked deleted, allowing other devices tooupdate their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="4cec1-354">Offlinesynchronisatie initialiseren</span><span class="sxs-lookup"><span data-stu-id="4cec1-354">Initialize Offline Sync</span></span>

<span data-ttu-id="4cec1-355">Elke tabel offline moet worden gedefinieerd in de offline cache Hallo vóór gebruik.</span><span class="sxs-lookup"><span data-stu-id="4cec1-355">Each offline table must be defined in hello offline cache before use.</span></span>  <span data-ttu-id="4cec1-356">Normaal gesproken wordt tabeldefinitie uitgevoerd onmiddellijk nadat het maken van de Hallo van client Hallo:</span><span class="sxs-lookup"><span data-stu-id="4cec1-356">Normally, table definition is done immediately after hello creation of hello client:</span></span>

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

### <a name="obtain-a-reference-toohello-offline-cache-table"></a><span data-ttu-id="4cec1-357">Een verwijzing toohello Offline cachetabel verkrijgen</span><span class="sxs-lookup"><span data-stu-id="4cec1-357">Obtain a reference toohello Offline Cache Table</span></span>

<span data-ttu-id="4cec1-358">Voor een online tabel, gebruikt u `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="4cec1-358">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="4cec1-359">Gebruik voor een offline tabel `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="4cec1-359">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="4cec1-360">Alle methoden die beschikbaar zijn voor online-tabellen (inclusief filteren, sorteren, paging, gegevens invoegen, bijwerken van gegevens en verwijderen van gegevens) evenveel werken Hallo goed in online als offline tabellen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-360">All hello methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-hello-local-offline-cache"></a><span data-ttu-id="4cec1-361">Hallo lokale Offline Cache synchroniseren</span><span class="sxs-lookup"><span data-stu-id="4cec1-361">Synchronize hello Local Offline Cache</span></span>

<span data-ttu-id="4cec1-362">Synchronisatie is in het Hallo-besturingselement van uw app.</span><span class="sxs-lookup"><span data-stu-id="4cec1-362">Synchronization is within hello control of your app.</span></span>  <span data-ttu-id="4cec1-363">Hier volgt een voorbeeld van de synchronisatie-methode:</span><span class="sxs-lookup"><span data-stu-id="4cec1-363">Here is an example synchronization method:</span></span>

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

<span data-ttu-id="4cec1-364">Als de naam van een query is opgegeven, toohello `.pull(query, queryname)` methode en vervolgens incrementele synchronisatie alleen gebruikte tooreturn de records die zijn gemaakt of gewijzigd sinds de laatste voltooid Hallo pull is.</span><span class="sxs-lookup"><span data-stu-id="4cec1-364">If a query name is provided toohello `.pull(query, queryname)` method, then incremental sync is used tooreturn only records that have been created or changed since hello last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="4cec1-365">Afhandeling van conflicten tijdens het Offline synchroniseren</span><span class="sxs-lookup"><span data-stu-id="4cec1-365">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="4cec1-366">Als een conflict zich tijdens voordoet een `.push()` bewerking, een `MobileServiceConflictException` gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="4cec1-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="4cec1-367">Hallo server uitgegeven item is ingesloten in Hallo uitzondering en kan worden opgehaald door `.getItem()` op Hallo-uitzondering.</span><span class="sxs-lookup"><span data-stu-id="4cec1-367">hello server-issued item is embedded in hello exception and can be retrieved by `.getItem()` on hello exception.</span></span>  <span data-ttu-id="4cec1-368">Hallo push door aanroepen Hallo volgende items op Hallo MobileServiceSyncContext object aan te passen:</span><span class="sxs-lookup"><span data-stu-id="4cec1-368">Adjust hello push by calling hello following items on hello MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="4cec1-369">Wanneer alle conflicten zijn gemarkeerd als u wilt, aanroepen `.push()` opnieuw tooresolve alle conflicten Hallo.</span><span class="sxs-lookup"><span data-stu-id="4cec1-369">Once all conflicts are marked as you wish, call `.push()` again tooresolve all hello conflicts.</span></span>

## <span data-ttu-id="4cec1-370"><a name="custom-api"></a>Een aangepaste API aanroepen</span><span class="sxs-lookup"><span data-stu-id="4cec1-370"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="4cec1-371">Een aangepaste API kunt u toodefine aangepaste eindpunten die serverfunctionaliteit weergeven die geen toewijzen tooan invoegen, bijwerken, verwijderen of leesbewerking.</span><span class="sxs-lookup"><span data-stu-id="4cec1-371">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="4cec1-372">Met behulp van een aangepaste API gebruiken, kunt u meer controle over messaging, hebben waaronder lezen en HTTP-bericht headers instellen en definiëren van een berichttekst de indeling dan JSON.</span><span class="sxs-lookup"><span data-stu-id="4cec1-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="4cec1-373">In een Android-client u Hallo aanroepen **invokeApi** methode toocall Hallo aangepaste API-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="4cec1-373">From an Android client, you call hello **invokeApi** method toocall hello custom API endpoint.</span></span> <span data-ttu-id="4cec1-374">Hallo volgende voorbeeld laat zien hoe toocall een API-eindpunt met de naam **completeAll**, die de klasse van een verzameling met de naam retourneert **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-374">hello following example shows how toocall an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

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

<span data-ttu-id="4cec1-375">Hallo **invokeApi** methode wordt aangeroepen op Hallo client verzendt een POST-aanvraag toohello nieuwe aangepaste API.</span><span class="sxs-lookup"><span data-stu-id="4cec1-375">hello **invokeApi** method is called on hello client, which sends a POST request toohello new custom API.</span></span> <span data-ttu-id="4cec1-376">Hallo-resultaat geretourneerd door de aangepaste API hello wordt weergegeven in een dialoogvenster weergegeven als er fouten zijn.</span><span class="sxs-lookup"><span data-stu-id="4cec1-376">hello result returned by hello custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="4cec1-377">Andere versies van **invokeApi** kunt u eventueel het verzenden van een object in de aanvraagtekst hello, Hallo HTTP-methode opgeven en queryparameters met Hallo aanvraag verzenden.</span><span class="sxs-lookup"><span data-stu-id="4cec1-377">Other versions of **invokeApi** let you optionally send an object in hello request body, specify hello HTTP method, and send query parameters with hello request.</span></span> <span data-ttu-id="4cec1-378">Versies van getypeerde **invokeApi** ook worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="4cec1-378">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="4cec1-379"><a name="authentication"></a>Verificatie tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="4cec1-379"><a name="authentication"></a>Add authentication tooyour app</span></span>

<span data-ttu-id="4cec1-380">Zelfstudies al in detail beschrijven hoe tooadd deze functies.</span><span class="sxs-lookup"><span data-stu-id="4cec1-380">Tutorials already describe in detail how tooadd these features.</span></span>

<span data-ttu-id="4cec1-381">App Service ondersteunt [verifiëren van gebruikers van de app](app-service-mobile-android-get-started-users.md) met behulp van verschillende externe id-providers: Facebook, Google, Microsoft-Account, Twitter en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4cec1-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="4cec1-382">U kunt machtigingen instellen voor tabellen toorestrict toegang voor specifieke bewerkingen tooonly geverifieerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4cec1-382">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="4cec1-383">U kunt ook Hallo identiteit van de geverifieerde gebruikers tooimplement autorisatieregels gebruiken in uw back-end.</span><span class="sxs-lookup"><span data-stu-id="4cec1-383">You can also use hello identity of authenticated users tooimplement authorization rules in your backend.</span></span>

<span data-ttu-id="4cec1-384">Twee verificatie stromen worden ondersteund: een **server** stroom en een **client** stroom.</span><span class="sxs-lookup"><span data-stu-id="4cec1-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="4cec1-385">Hallo server stroom biedt Hallo eenvoudigste verificatie-ervaring, is afhankelijk van Hallo identiteit providers webinterface.</span><span class="sxs-lookup"><span data-stu-id="4cec1-385">hello server flow provides hello simplest authentication experience, as it relies on hello identity providers web interface.</span></span>  <span data-ttu-id="4cec1-386">Er zijn geen extra SDK's zijn vereist tooimplement stroom serververificatie.</span><span class="sxs-lookup"><span data-stu-id="4cec1-386">No additional SDKs are required tooimplement server flow authentication.</span></span> <span data-ttu-id="4cec1-387">Verificatie van de stroom biedt geen een diepe integratie op Hallo mobiel apparaat en wordt alleen aanbevolen voor bewijs van concept scenario's.</span><span class="sxs-lookup"><span data-stu-id="4cec1-387">Server flow authentication does not provide a deep integration into hello mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="4cec1-388">Hallo stroom kunt voor een betere integratie met apparaatspecifieke mogelijkheden, zoals het eenmalige aanmelding is afhankelijk van de SDK's die worden geleverd door de identiteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="4cec1-388">hello client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by hello identity provider.</span></span>  <span data-ttu-id="4cec1-389">U kunt bijvoorbeeld Hallo Facebook SDK integreren in uw mobiele App.</span><span class="sxs-lookup"><span data-stu-id="4cec1-389">For example, you can integrate hello Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="4cec1-390">Hallo mobiele clients worden omgewisseld in Hallo Facebook-app en bevestigt uw aanmelding voordat het wisselen van de mobiele app back tooyour.</span><span class="sxs-lookup"><span data-stu-id="4cec1-390">hello mobile client swaps into hello Facebook app and confirms your sign-on before swapping back tooyour mobile app.</span></span>

<span data-ttu-id="4cec1-391">Vier stappen zijn vereist tooenable verificatie in uw app:</span><span class="sxs-lookup"><span data-stu-id="4cec1-391">Four steps are required tooenable authentication in your app:</span></span>

* <span data-ttu-id="4cec1-392">Uw app registreren voor verificatie met een id-provider.</span><span class="sxs-lookup"><span data-stu-id="4cec1-392">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="4cec1-393">Configureer uw App Service-back-end.</span><span class="sxs-lookup"><span data-stu-id="4cec1-393">Configure your App Service backend.</span></span>
* <span data-ttu-id="4cec1-394">Tabel machtigingen tooauthenticated gebruikers alleen op Hallo App Service-back-end beperken.</span><span class="sxs-lookup"><span data-stu-id="4cec1-394">Restrict table permissions tooauthenticated users only on hello App Service backend.</span></span>
* <span data-ttu-id="4cec1-395">Verificatie code tooyour app toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-395">Add authentication code tooyour app.</span></span>

<span data-ttu-id="4cec1-396">U kunt machtigingen instellen voor tabellen toorestrict toegang voor specifieke bewerkingen tooonly geverifieerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4cec1-396">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="4cec1-397">U kunt ook Hallo SID van een geverifieerde gebruiker toomodify aanvragen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-397">You can also use hello SID of an authenticated user toomodify requests.</span></span>  <span data-ttu-id="4cec1-398">Raadpleeg voor meer informatie [aan de slag met verificatie] en Hallo procedure van Server SDK-documentatie.</span><span class="sxs-lookup"><span data-stu-id="4cec1-398">For more information, review [Get started with authentication] and hello Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="4cec1-399"><a name="caching"></a>: Verificatiestroom Server</span><span class="sxs-lookup"><span data-stu-id="4cec1-399"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="4cec1-400">Hallo start volgende code een server stroom aanmelding met Hallo Google-provider.</span><span class="sxs-lookup"><span data-stu-id="4cec1-400">hello following code starts a server flow login process using hello Google provider.</span></span>  <span data-ttu-id="4cec1-401">Aanvullende configuratie is vereist vanwege Hallo beveiligingsvereisten voor Hallo Google-provider:</span><span class="sxs-lookup"><span data-stu-id="4cec1-401">Additional configuration is required because of hello security requirements for hello Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="4cec1-402">Daarnaast toevoegen Hallo methode toohello activiteit hoofdklasse te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cec1-402">In addition, add hello following method toohello main Activity class:</span></span>

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

<span data-ttu-id="4cec1-403">Hallo `GOOGLE_LOGIN_REQUEST_CODE` gedefinieerd in uw belangrijkste activiteit wordt gebruikt voor Hallo `login()` methode en binnen Hallo `onActivityResult()` methode.</span><span class="sxs-lookup"><span data-stu-id="4cec1-403">hello `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for hello `login()` method and within hello `onActivityResult()` method.</span></span>  <span data-ttu-id="4cec1-404">U kunt een uniek nummer, zolang hello hetzelfde nummer wordt gebruikt binnen Hallo `login()` methode en Hallo `onActivityResult()` methode.</span><span class="sxs-lookup"><span data-stu-id="4cec1-404">You can choose any unique number, as long as hello same number is used within hello `login()` method and hello `onActivityResult()` method.</span></span>  <span data-ttu-id="4cec1-405">Als u clientcode Hallo abstracte in een service-adapter (zoals eerder is weergegeven), moet u Hallo geschikte methoden aanroepen op Hallo service adapter.</span><span class="sxs-lookup"><span data-stu-id="4cec1-405">If you abstract hello client code into a service adapter (as shown earlier), you should call hello appropriate methods on hello service adapter.</span></span>

<span data-ttu-id="4cec1-406">U moet ook tooconfigure Hallo project voor customtabs.</span><span class="sxs-lookup"><span data-stu-id="4cec1-406">You also need tooconfigure hello project for customtabs.</span></span>  <span data-ttu-id="4cec1-407">Eerst een Omleidings-URL opgeven.</span><span class="sxs-lookup"><span data-stu-id="4cec1-407">First specify a redirect-URL.</span></span>  <span data-ttu-id="4cec1-408">Hallo codefragment te volgen toevoegen`AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="4cec1-408">Add hello following snippet too`AndroidManifest.xml`:</span></span>

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

<span data-ttu-id="4cec1-409">Hallo toevoegen **redirectUriScheme** toohello `build.gradle` bestand voor uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="4cec1-409">Add hello **redirectUriScheme** toohello `build.gradle` file for your application:</span></span>

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

<span data-ttu-id="4cec1-410">Voeg `com.android.support:customtabs:23.0.1` toohello toepassingsafhankelijkheden in Hallo `build.gradle` bestand:</span><span class="sxs-lookup"><span data-stu-id="4cec1-410">Finally, add `com.android.support:customtabs:23.0.1` toohello dependencies list in hello `build.gradle` file:</span></span>

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

<span data-ttu-id="4cec1-411">Hallo-ID van Hallo aangemelde gebruiker van opvragen een **MobileServiceUser** met Hallo **getUserId** methode.</span><span class="sxs-lookup"><span data-stu-id="4cec1-411">Obtain hello ID of hello logged-in user from a **MobileServiceUser** using hello **getUserId** method.</span></span> <span data-ttu-id="4cec1-412">Zie voor een voorbeeld van hoe toouse Futures toocall Hallo asynchrone aanmelding API's, [aan de slag met verificatie].</span><span class="sxs-lookup"><span data-stu-id="4cec1-412">For an example of how toouse Futures toocall hello asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="4cec1-413">Hallo vermeld URL-schema is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="4cec1-413">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="4cec1-414">Zorg ervoor dat alle instanties van `{url_scheme_of_you_app}` hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="4cec1-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="4cec1-415"><a name="caching"></a>Verificatietokens cache</span><span class="sxs-lookup"><span data-stu-id="4cec1-415"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="4cec1-416">Verificatietokens caching, moet u toostore Hallo gebruikers-ID en -verificatietoken lokaal op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4cec1-416">Caching authentication tokens requires you toostore hello User ID and authentication token locally on hello device.</span></span> <span data-ttu-id="4cec1-417">Hallo Hallo-app wordt gestart, zodra u Controleer Hallo-cache, en als deze waarden aanwezig zijn, kunt u overslaan Hallo-logboek in de procedure en rehydrate Hallo-client met deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="4cec1-417">hello next time hello app starts, you check hello cache, and if these values are present, you can skip hello log in procedure and rehydrate hello client with this data.</span></span> <span data-ttu-id="4cec1-418">Deze gegevens is echter gevoelige en moeten worden opgeslagen voor de veiligheid versleuteld als Hallo telefoon wordt gestolen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-418">However this data is sensitive, and it should be stored encrypted for safety in case hello phone gets stolen.</span></span>  <span data-ttu-id="4cec1-419">Ziet u een compleet voorbeeld van hoe toocache verificatie tokens in [verificatiesectie tokens in de Cache][7].</span><span class="sxs-lookup"><span data-stu-id="4cec1-419">You can see a complete example of how toocache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="4cec1-420">Wanneer u een verlopen token toouse probeert, krijgt u een *401-niet-geautoriseerde* antwoord.</span><span class="sxs-lookup"><span data-stu-id="4cec1-420">When you try toouse an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="4cec1-421">U kunt met behulp van filters verificatiefouten verwerken.</span><span class="sxs-lookup"><span data-stu-id="4cec1-421">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="4cec1-422">Filters onderscheppen aanvragen toohello back-end van App Service.</span><span class="sxs-lookup"><span data-stu-id="4cec1-422">Filters intercept requests toohello App Service backend.</span></span> <span data-ttu-id="4cec1-423">Hallo filtercode test antwoord Hallo voor een 401, Hallo aanmelden proces wordt geactiveerd en wordt hervat Hallo-aanvraag die Hallo 401 gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="4cec1-423">hello filter code tests hello response for a 401, triggers hello sign-in process, and then resumes hello request that generated hello 401.</span></span>

### <span data-ttu-id="4cec1-424"><a name="refresh"></a>Vernieuwen van Tokens gebruiken</span><span class="sxs-lookup"><span data-stu-id="4cec1-424"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="4cec1-425">Hallo-token geretourneerd door de Azure App Service-verificatie en autorisatie heeft een gedefinieerde levensduur van een uur.</span><span class="sxs-lookup"><span data-stu-id="4cec1-425">hello token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="4cec1-426">Na deze periode, moet u Hallo gebruiker te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="4cec1-426">After this period, you must reauthenticate hello user.</span></span>  <span data-ttu-id="4cec1-427">Als u Hallo met een lange levensduur token dat u hebt ontvangen via client-flow-verificatie en u kunt verifiëren met Azure App Service-verificatie en autorisatie hetzelfde token.</span><span class="sxs-lookup"><span data-stu-id="4cec1-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using hello same token.</span></span>  <span data-ttu-id="4cec1-428">Een andere Azure App Service-token wordt gegenereerd met een nieuwe levensduur.</span><span class="sxs-lookup"><span data-stu-id="4cec1-428">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="4cec1-429">U kunt ook Hallo provider toouse vernieuwen Tokens registreren.</span><span class="sxs-lookup"><span data-stu-id="4cec1-429">You can also register hello provider toouse Refresh Tokens.</span></span>  <span data-ttu-id="4cec1-430">Een Token voor vernieuwen is niet altijd beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="4cec1-430">A Refresh Token is not always available.</span></span>  <span data-ttu-id="4cec1-431">Er is aanvullende configuratie vereist:</span><span class="sxs-lookup"><span data-stu-id="4cec1-431">Additional configuration is required:</span></span>

* <span data-ttu-id="4cec1-432">Voor **Azure Active Directory**, een clientgeheim voor hello Azure Active Directory-App configureren.</span><span class="sxs-lookup"><span data-stu-id="4cec1-432">For **Azure Active Directory**, configure a client secret for hello Azure Active Directory App.</span></span>  <span data-ttu-id="4cec1-433">Geef Hallo clientgeheim in hello Azure App Service bij het configureren van Azure Active Directory-verificatie.</span><span class="sxs-lookup"><span data-stu-id="4cec1-433">Specify hello client secret in hello Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="4cec1-434">Bij het aanroepen van `.login()`, doorgeven `response_type=code id_token` als een parameter:</span><span class="sxs-lookup"><span data-stu-id="4cec1-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="4cec1-435">Voor **Google**, Hallo doorgeven `access_type=offline` als een parameter:</span><span class="sxs-lookup"><span data-stu-id="4cec1-435">For **Google**, pass hello `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="4cec1-436">Voor **Microsoft-Account**, selecteer Hallo `wl.offline_access` bereik.</span><span class="sxs-lookup"><span data-stu-id="4cec1-436">For **Microsoft Account**, select hello `wl.offline_access` scope.</span></span>

<span data-ttu-id="4cec1-437">aanroepen van een token toorefresh `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="4cec1-437">toorefresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="4cec1-438">Als een best practice een filter die een 401-respons van Hallo-server detecteert en toorefresh Hallo gebruikerstoken probeert te maken.</span><span class="sxs-lookup"><span data-stu-id="4cec1-438">As a best practice, create a filter that detects a 401 response from hello server and tries toorefresh hello user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="4cec1-439">Meld u aan met Client-flow-verificatie</span><span class="sxs-lookup"><span data-stu-id="4cec1-439">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="4cec1-440">Hallo algemene proces voor aangemeld met client-flow-verificatie is als volgt:</span><span class="sxs-lookup"><span data-stu-id="4cec1-440">hello general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="4cec1-441">Azure App Service-verificatie en autorisatie configureert als server-flow-verificatie.</span><span class="sxs-lookup"><span data-stu-id="4cec1-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="4cec1-442">Hallo-verificatieprovider SDK voor verificatie tooproduce een toegangstoken integreren.</span><span class="sxs-lookup"><span data-stu-id="4cec1-442">Integrate hello authentication provider SDK for authentication tooproduce an access token.</span></span>
* <span data-ttu-id="4cec1-443">Hallo aanroepen `.login()` methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="4cec1-443">Call hello `.login()` method as follows:</span></span>

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

<span data-ttu-id="4cec1-444">Vervang Hallo `onSuccess()` methode met wat u code wilt toouse op een geslaagde aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4cec1-444">Replace hello `onSuccess()` method with whatever code you wish toouse on a successful login.</span></span>  <span data-ttu-id="4cec1-445">Hallo `{provider}` tekenreeks is een geldige provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, of **twitter**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-445">hello `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="4cec1-446">Als u aangepaste verificatie hebt geïmplementeerd, kunt u ook aangepaste verificatiecode provider hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4cec1-446">If you have implemented custom authentication, then you can also use hello custom authentication provider tag.</span></span>

### <span data-ttu-id="4cec1-447"><a name="adal"></a>Verificatie van gebruikers met Hallo Active Directory Authentication Library (ADAL)</span><span class="sxs-lookup"><span data-stu-id="4cec1-447"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="4cec1-448">U kunt Hallo Active Directory Authentication Library (ADAL) toosign gebruikers in uw toepassing met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4cec1-448">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="4cec1-449">Met behulp van de aanmelding van een client stroom is vaak beter toousing hello `loginAsync()` methoden zoals deze biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="4cec1-449">Using a client flow login is often preferable toousing hello `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="4cec1-450">Uw mobiele app back-end voor aanmelding bij de AAD configureren door de volgende Hallo [hoe tooconfigure App Service voor Active Directory-aanmelding] [ 22] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4cec1-450">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="4cec1-451">Zorg ervoor dat toocomplete Hallo optionele stap voor het registreren van een systeemeigen clienttoepassing van.</span><span class="sxs-lookup"><span data-stu-id="4cec1-451">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="4cec1-452">ADAL installeren door het wijzigen van uw build.gradle-bestand tooinclude Hallo definities te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cec1-452">Install ADAL by modifying your build.gradle file tooinclude hello following definitions:</span></span>

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

1. <span data-ttu-id="4cec1-453">Hallo code tooyour toepassing te volgen, waardoor Hallo vervangingen volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="4cec1-453">Add hello following code tooyour application, making hello following replacements:</span></span>

* <span data-ttu-id="4cec1-454">Vervang **INSERT-instantie-hier** met de naam van de Hallo van Hallo tenant waarin u uw toepassing hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="4cec1-454">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="4cec1-455">Hallo-indeling moet https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="4cec1-455">hello format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="4cec1-456">Vervang **INSERT RESOURCE-ID hier** met Hallo client-ID voor uw back-end voor de mobiele app.</span><span class="sxs-lookup"><span data-stu-id="4cec1-456">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="4cec1-457">U kunt Hallo client-ID verkrijgen van Hallo **Geavanceerd** tabblad onder **Azure Active Directory-instellingen** in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="4cec1-457">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
* <span data-ttu-id="4cec1-458">Vervang **INSERT-CLIENT-ID-hier** met client-ID Hallo u hebt gekopieerd uit Hallo native client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="4cec1-458">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
* <span data-ttu-id="4cec1-459">Vervang **INSERT-OMLEIDINGS-URI-hier** aan uw site */.auth/login/done* eindpunt, met Hallo HTTPS-schema.</span><span class="sxs-lookup"><span data-stu-id="4cec1-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="4cec1-460">Deze waarde moet er ongeveer te*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="4cec1-460">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

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

## <span data-ttu-id="4cec1-461"><a name="filters"></a>Hallo Client-servercommunicatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="4cec1-461"><a name="filters"></a>Adjust hello Client-Server Communication</span></span>

<span data-ttu-id="4cec1-462">Hallo clientverbinding is doorgaans een eenvoudige HTTP-verbinding met behulp van de onderliggende HTTP-bibliotheek geleverd met Hallo Android SDK Hallo.</span><span class="sxs-lookup"><span data-stu-id="4cec1-462">hello Client connection is normally a basic HTTP connection using hello underlying HTTP library supplied with hello Android SDK.</span></span>  <span data-ttu-id="4cec1-463">Er zijn diverse redenen waarom u toochange zou willen die:</span><span class="sxs-lookup"><span data-stu-id="4cec1-463">There are several reasons why you would want toochange that:</span></span>

* <span data-ttu-id="4cec1-464">U desgewenst een andere HTTP-bibliotheek tooadjust time-outs toouse.</span><span class="sxs-lookup"><span data-stu-id="4cec1-464">You wish toouse an alternate HTTP library tooadjust timeouts.</span></span>
* <span data-ttu-id="4cec1-465">U wilt een voortgangsbalk tooprovide.</span><span class="sxs-lookup"><span data-stu-id="4cec1-465">You wish tooprovide a progress bar.</span></span>
* <span data-ttu-id="4cec1-466">U wilt tooadd een aangepaste header toosupport API management-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="4cec1-466">You wish tooadd a custom header toosupport API management functionality.</span></span>
* <span data-ttu-id="4cec1-467">U wilt toointercept een mislukte reactie zodat u herauthenticatie kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="4cec1-467">You wish toointercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="4cec1-468">Gewenste toolog back-end aanvragen tooan analytics-service.</span><span class="sxs-lookup"><span data-stu-id="4cec1-468">You wish toolog backend requests tooan analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="4cec1-469">Met behulp van een andere HTTP-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="4cec1-469">Using an alternate HTTP Library</span></span>

<span data-ttu-id="4cec1-470">Hallo aanroepen `.setAndroidHttpClientFactory()` methode onmiddellijk na het maken van uw client-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="4cec1-470">Call hello `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="4cec1-471">In dit voorbeeld tooset Hallo verbinding time-out too60 seconden (in plaats van Hallo standaard 10 seconden):</span><span class="sxs-lookup"><span data-stu-id="4cec1-471">For example, tooset hello connection timeout too60 seconds (instead of hello default 10 seconds):</span></span>

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

### <a name="implement-a-progress-filter"></a><span data-ttu-id="4cec1-472">Een Filter voortgang implementeren</span><span class="sxs-lookup"><span data-stu-id="4cec1-472">Implement a Progress Filter</span></span>

<span data-ttu-id="4cec1-473">U kunt een intercept van elke aanvraag implementeren door het implementeren van een `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="4cec1-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="4cec1-474">Bijvoorbeeld, updates Hallo volgende van een vooraf gemaakte voortgangsbalk:</span><span class="sxs-lookup"><span data-stu-id="4cec1-474">For example, hello following updates a pre-created progress bar:</span></span>

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

<span data-ttu-id="4cec1-475">U kunt dit filter toohello client als volgt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="4cec1-475">You can attach this filter toohello client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="4cec1-476">Aanvraagheaders aanpassen</span><span class="sxs-lookup"><span data-stu-id="4cec1-476">Customize Request Headers</span></span>

<span data-ttu-id="4cec1-477">Gebruik de volgende Hallo `ServiceFilter` en koppelt u Hallo-filter in Hallo dezelfde manier als Hallo `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="4cec1-477">Use hello following `ServiceFilter` and attach hello filter in hello same way as hello `ProgressFilter`:</span></span>

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

### <span data-ttu-id="4cec1-478"><a name="conversions"></a>Automatische serialisatie configureren</span><span class="sxs-lookup"><span data-stu-id="4cec1-478"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="4cec1-479">U kunt opgeven dat een strategie voor een conversie die van toepassing tooevery kolom is met behulp van Hallo [gson] [ 3] API.</span><span class="sxs-lookup"><span data-stu-id="4cec1-479">You can specify a conversion strategy that applies tooevery column by using hello [gson][3] API.</span></span> <span data-ttu-id="4cec1-480">maakt gebruik van de Android clientbibliotheek Hallo [gson] [ 3] achter de schermen Hallo tooserialize Java objecten tooJSON gegevens voordat Hallo gegevens tooAzure App Service worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="4cec1-480">hello Android client library uses [gson][3] behind hello scenes tooserialize Java objects tooJSON data before hello data is sent tooAzure App Service.</span></span>  <span data-ttu-id="4cec1-481">Hallo volgende code gebruikt Hallo **setFieldNamingStrategy()** methode tooset Hallo-strategie.</span><span class="sxs-lookup"><span data-stu-id="4cec1-481">hello following code uses hello **setFieldNamingStrategy()** method tooset hello strategy.</span></span> <span data-ttu-id="4cec1-482">In dit voorbeeld worden Hallo eerste teken (een ' m') en vervolgens kleine Hallo volgende teken voor elke veldnaam verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4cec1-482">This example will delete hello initial character (an "m"), and then lower-case hello next character, for every field name.</span></span> <span data-ttu-id="4cec1-483">Bijvoorbeeld, zou het veranderen 'mId' in 'id'.</span><span class="sxs-lookup"><span data-stu-id="4cec1-483">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="4cec1-484">Implementeer een conversie strategie tooreduce Hallo nodig voor `SerializedName()` aantekeningen in de meeste velden.</span><span class="sxs-lookup"><span data-stu-id="4cec1-484">Implement a conversion strategy tooreduce hello need for `SerializedName()` annotations on most fields.</span></span>

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

<span data-ttu-id="4cec1-485">Deze code moet worden uitgevoerd voordat het maken van een mobiele client-verwijzing met Hallo **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="4cec1-485">This code must be executed before creating a mobile client reference using hello **MobileServiceClient**.</span></span>

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
