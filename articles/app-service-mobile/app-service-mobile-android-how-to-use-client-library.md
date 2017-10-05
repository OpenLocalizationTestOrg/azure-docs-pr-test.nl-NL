---
title: Het gebruik van de Azure Mobile Apps SDK voor Android | Microsoft Docs
description: Het gebruik van de Azure Mobile Apps SDK voor Android
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
ms.openlocfilehash: 4b15d024ca6d5bbafe83d321a64021aecd78c4a8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="06172-103">Het gebruik van de Azure Mobile Apps SDK voor Android</span><span class="sxs-lookup"><span data-stu-id="06172-103">How to use the Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="06172-104">Deze handleiding wordt beschreven hoe u de Android SDK voor Mobile Apps-client gebruiken voor het implementeren van algemene scenario's, zoals:</span><span class="sxs-lookup"><span data-stu-id="06172-104">This guide shows you how to use the Android client SDK for Mobile Apps to implement common scenarios, such as:</span></span>

* <span data-ttu-id="06172-105">Opvragen van gegevens (invoegen, bijwerken en verwijderen).</span><span class="sxs-lookup"><span data-stu-id="06172-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="06172-106">-Verificatie.</span><span class="sxs-lookup"><span data-stu-id="06172-106">Authentication.</span></span>
* <span data-ttu-id="06172-107">Foutafhandeling.</span><span class="sxs-lookup"><span data-stu-id="06172-107">Handling errors.</span></span>
* <span data-ttu-id="06172-108">Aanpassing van de client.</span><span class="sxs-lookup"><span data-stu-id="06172-108">Customizing the client.</span></span>

<span data-ttu-id="06172-109">Deze handleiding is gericht op de client-side Android SDK.</span><span class="sxs-lookup"><span data-stu-id="06172-109">This guide focuses on the client-side Android SDK.</span></span>  <span data-ttu-id="06172-110">Zie voor meer informatie over de serverzijde SDK's voor mobiele Apps, [werken met .NET back-end SDK] [ 10] of [het gebruik van de SDK back-end Node.js][11].</span><span class="sxs-lookup"><span data-stu-id="06172-110">To learn more about the server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How to use the Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="06172-111">Naslagdocumentatie</span><span class="sxs-lookup"><span data-stu-id="06172-111">Reference Documentation</span></span>

<span data-ttu-id="06172-112">U vindt de [Javadocs API-referentiemateriaal] [ 12] voor de Android-clientbibliotheek op GitHub.</span><span class="sxs-lookup"><span data-stu-id="06172-112">You can find the [Javadocs API reference][12] for the Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="06172-113">Ondersteunde Platforms</span><span class="sxs-lookup"><span data-stu-id="06172-113">Supported Platforms</span></span>

<span data-ttu-id="06172-114">De Azure Mobile Apps SDK voor Android ondersteunt API niveaus 19 tot en met 24 (KitKat via deze) voor de telefoon en tablet vormfactoren.</span><span class="sxs-lookup"><span data-stu-id="06172-114">The Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="06172-115">Verificatie, met name maakt gebruik van een benadering van de algemene framework voor het verzamelen van referenties.</span><span class="sxs-lookup"><span data-stu-id="06172-115">Authentication, in particular, utilizes a common web framework approach to gather credentials.</span></span>  <span data-ttu-id="06172-116">Server-flow-verificatie werkt niet met kleine formulier factor apparaten zoals kijkt naar.</span><span class="sxs-lookup"><span data-stu-id="06172-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="06172-117">Het installatieprogramma en vereisten</span><span class="sxs-lookup"><span data-stu-id="06172-117">Setup and Prerequisites</span></span>

<span data-ttu-id="06172-118">Voltooi de [Mobile Apps Quick Start](app-service-mobile-android-get-started.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="06172-118">Complete the [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="06172-119">Deze taak zorgt ervoor dat alle vereisten voor het ontwikkelen van Azure Mobile Apps is voldaan.</span><span class="sxs-lookup"><span data-stu-id="06172-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="06172-120">De Quick Start helpt u bij het configureren van uw account en uw eerste back-end voor mobiele apps te maken.</span><span class="sxs-lookup"><span data-stu-id="06172-120">The Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="06172-121">Als u besluit niet op de Quick Start-zelfstudie hebt voltooid, kunt u de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="06172-121">If you decide not to complete the Quickstart tutorial, complete the following tasks:</span></span>

* <span data-ttu-id="06172-122">[Maak een back-end voor de mobiele App] [ 13] voor gebruik met uw Android-app.</span><span class="sxs-lookup"><span data-stu-id="06172-122">[create a Mobile App backend][13] to use with your Android app.</span></span>
* <span data-ttu-id="06172-123">In Android Studio [update de Gradle bouwen bestanden](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="06172-123">In Android Studio, [update the Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="06172-124">[Internet-machtiging wordt ingeschakeld](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="06172-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="06172-125"><a name="gradle-build"></a>Het bestand van de build Gradle bijwerken</span><span class="sxs-lookup"><span data-stu-id="06172-125"><a name="gradle-build"></a>Update the Gradle build file</span></span>

<span data-ttu-id="06172-126">Beide wijzigen **build.gradle** bestanden:</span><span class="sxs-lookup"><span data-stu-id="06172-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="06172-127">Deze code toevoegen aan de *Project* niveau **build.gradle** bestand binnen de *buildscript* tag:</span><span class="sxs-lookup"><span data-stu-id="06172-127">Add this code to the *Project* level **build.gradle** file inside the *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="06172-128">Deze code toevoegen aan de *Module app* niveau **build.gradle** bestand binnen de *afhankelijkheden* tag:</span><span class="sxs-lookup"><span data-stu-id="06172-128">Add this code to the *Module app* level **build.gradle** file inside the *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="06172-129">De meest recente versie is momenteel 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="06172-129">Currently the latest version is 3.3.0.</span></span> <span data-ttu-id="06172-130">De ondersteunde versies zijn vermeld [op bintray][14].</span><span class="sxs-lookup"><span data-stu-id="06172-130">The supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="06172-131"><a name="enable-internet"></a>Internet-machtiging wordt ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="06172-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="06172-132">Voor toegang tot Azure, moet uw app de INTERNET-machtiging ingeschakeld hebben.</span><span class="sxs-lookup"><span data-stu-id="06172-132">To access Azure, your app must have the INTERNET permission enabled.</span></span> <span data-ttu-id="06172-133">Als deze nog niet is ingeschakeld, voeg de volgende regel code naar uw **AndroidManifest.xml** bestand:</span><span class="sxs-lookup"><span data-stu-id="06172-133">If it's not already enabled, add the following line of code to your **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="06172-134">Een clientverbinding maken</span><span class="sxs-lookup"><span data-stu-id="06172-134">Create a Client Connection</span></span>

<span data-ttu-id="06172-135">Mobiele Apps van Azure biedt vier functies voor uw mobiele App:</span><span class="sxs-lookup"><span data-stu-id="06172-135">Azure Mobile Apps provides four functions to your mobile application:</span></span>

* <span data-ttu-id="06172-136">Toegang tot gegevens en Offline synchronisatie met een Azure Mobile Apps-Service.</span><span class="sxs-lookup"><span data-stu-id="06172-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="06172-137">Aangepaste API's die zijn geschreven met de Azure Mobile Apps Server SDK-aanroep.</span><span class="sxs-lookup"><span data-stu-id="06172-137">Call Custom APIs written with the Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="06172-138">Verificatie met Azure App Service-verificatie en autorisatie.</span><span class="sxs-lookup"><span data-stu-id="06172-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="06172-139">Registratie bij Notification Hubs voor pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="06172-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="06172-140">Elk van deze functies, moet u eerst dat u maakt een `MobileServiceClient` object.</span><span class="sxs-lookup"><span data-stu-id="06172-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="06172-141">Slechts één `MobileServiceClient` object moet worden gemaakt binnen uw mobiele clients (dat wil zeggen, deze moet een Singleton-patroon).</span><span class="sxs-lookup"><span data-stu-id="06172-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="06172-142">Maken van een `MobileServiceClient` object:</span><span class="sxs-lookup"><span data-stu-id="06172-142">To create a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with the Site URL
    this);                  // Your application Context
```

<span data-ttu-id="06172-143">De `<MobileAppUrl>` is een tekenreeks of een URL-object dat naar uw mobiele back-end verwijst.</span><span class="sxs-lookup"><span data-stu-id="06172-143">The `<MobileAppUrl>` is either a string or a URL object that points to your mobile backend.</span></span>  <span data-ttu-id="06172-144">Als u van Azure App Service gebruikmaakt voor het hosten van uw mobiele back-end, klikt u vervolgens te zorgen dat u de beveiligde `https://` versie van de URL.</span><span class="sxs-lookup"><span data-stu-id="06172-144">If you are using Azure App Service to host your mobile backend, then ensure you use the secure `https://` version of the URL.</span></span>

<span data-ttu-id="06172-145">De client vereist ook toegang tot de activiteit of Context - de `this` parameter in het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="06172-145">The client also requires access to the Activity or Context - the `this` parameter in the example.</span></span>  <span data-ttu-id="06172-146">De constructie MobileServiceClient moet gebeuren binnen de `onCreate()` methode van de activiteit waarnaar wordt verwezen in de `AndroidManifest.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="06172-146">The MobileServiceClient construction should happen within the `onCreate()` method of the Activity referenced in the `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="06172-147">Als een best practice moet u communicatie tussen de server in een eigen (singleton-pattern)-klasse als abstract.</span><span class="sxs-lookup"><span data-stu-id="06172-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="06172-148">In dit geval moet u de activiteit in de constructor voor het configureren van de service op de juiste wijze doorgeven.</span><span class="sxs-lookup"><span data-stu-id="06172-148">In this case, you should pass the Activity within the constructor to appropriately configure the service.</span></span>  <span data-ttu-id="06172-149">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="06172-149">For example:</span></span>

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

<span data-ttu-id="06172-150">U kunt nu aanroepen `AzureServiceAdapter.Initialize(this);` in de `onCreate()` methode van uw belangrijkste activiteit.</span><span class="sxs-lookup"><span data-stu-id="06172-150">You can now call `AzureServiceAdapter.Initialize(this);` in the `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="06172-151">Alle andere methoden die behoefte hebben toegang tot het gebruik van de client `AzureServiceAdapter.getInstance();` verkrijgen van een verwijzing naar de service-adapter.</span><span class="sxs-lookup"><span data-stu-id="06172-151">Any other methods needing access to the client use `AzureServiceAdapter.getInstance();` to obtain a reference to the service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="06172-152">Gegevensbewerkingen</span><span class="sxs-lookup"><span data-stu-id="06172-152">Data Operations</span></span>

<span data-ttu-id="06172-153">De kern van de Azure Mobile Apps SDK is voor toegang tot gegevens die in SQL Azure worden opgeslagen op de back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="06172-153">The core of the Azure Mobile Apps SDK is to provide access to data stored within SQL Azure on the Mobile App backend.</span></span>  <span data-ttu-id="06172-154">U kunt toegang tot deze gegevens met behulp van sterk getypeerde klassen (aanbevolen) of getypeerde query's (niet aanbevolen).</span><span class="sxs-lookup"><span data-stu-id="06172-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="06172-155">Het merendeel van deze sectie behandelt sterk getypeerde klassen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="06172-155">The bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="06172-156">Definiëren van gegevensklassen client</span><span class="sxs-lookup"><span data-stu-id="06172-156">Define client data classes</span></span>

<span data-ttu-id="06172-157">Toegang tot gegevens uit SQL Azure-tabellen definiëren van client gegevensklassen die overeenkomen met de tabellen in de back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="06172-157">To access data from SQL Azure tables, define client data classes that correspond to the tables in the Mobile App backend.</span></span> <span data-ttu-id="06172-158">Voorbeelden in dit onderwerp wordt ervan uitgegaan dat een tabel met de naam **MyDataTable**, heeft de volgende kolommen:</span><span class="sxs-lookup"><span data-stu-id="06172-158">Examples in this topic assume a table named **MyDataTable**, which has the following columns:</span></span>

* <span data-ttu-id="06172-159">id</span><span class="sxs-lookup"><span data-stu-id="06172-159">id</span></span>
* <span data-ttu-id="06172-160">Tekst</span><span class="sxs-lookup"><span data-stu-id="06172-160">text</span></span>
* <span data-ttu-id="06172-161">Voltooien</span><span class="sxs-lookup"><span data-stu-id="06172-161">complete</span></span>

<span data-ttu-id="06172-162">Het bijbehorende getypte client-side '-object bevindt zich in een bestand met de naam **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="06172-162">The corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="06172-163">Voeg de getter en setter methoden voor elk veld dat u toevoegt.</span><span class="sxs-lookup"><span data-stu-id="06172-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="06172-164">Als uw Azure SQL-tabel meer kolommen bevat, zou u de overeenkomende velden toevoegen aan deze klasse.</span><span class="sxs-lookup"><span data-stu-id="06172-164">If your SQL Azure table contains more columns, you would add the corresponding fields to this class.</span></span>  <span data-ttu-id="06172-165">Bijvoorbeeld, als de DTO (object data transfer) was een kolom met gehele getallen prioriteit en u kunt dit veld samen met de methoden getter en setter toevoegen:</span><span class="sxs-lookup"><span data-stu-id="06172-165">For example, if the DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns the item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets the item priority
*
* @param priority
*            priority to set
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="06172-166">Zie voor meer informatie over het maken van aanvullende tabellen in uw back-end van Mobile Apps, [hoe: definiëren van een domeincontroller tabel] [ 15] (.NET-backend) of [definiëren tabellen met behulp van een dynamische Schema] [ 16] (Node.js back-end).</span><span class="sxs-lookup"><span data-stu-id="06172-166">To learn how to create additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="06172-167">Een tabel van de back-end van Azure Mobile Apps definieert vijf speciale velden vier die beschikbaar voor clients zijn:</span><span class="sxs-lookup"><span data-stu-id="06172-167">An Azure Mobile Apps backend table defines five special fields, four of which are available to clients:</span></span>

* <span data-ttu-id="06172-168">`String id`: De globaal unieke ID voor de record.</span><span class="sxs-lookup"><span data-stu-id="06172-168">`String id`: The globally unique ID for the record.</span></span>  <span data-ttu-id="06172-169">Als een best practice, maakt u de-id de tekenreeksweergave van een [UUID] [ 17] object.</span><span class="sxs-lookup"><span data-stu-id="06172-169">As a best practice, make the id the String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="06172-170">`DateTimeOffset updatedAt`: De datum/tijd van de laatste update.</span><span class="sxs-lookup"><span data-stu-id="06172-170">`DateTimeOffset updatedAt`: The date/time of the last update.</span></span>  <span data-ttu-id="06172-171">Het veld updatedAt is ingesteld door de server en nooit door uw clientcode moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="06172-171">The updatedAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="06172-172">`DateTimeOffset createdAt`: De datum/tijd die het object is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="06172-172">`DateTimeOffset createdAt`: The date/time that the object was created.</span></span>  <span data-ttu-id="06172-173">Het veld createdAt is ingesteld door de server en nooit door uw clientcode moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="06172-173">The createdAt field is set by the server and should never be set by your client code.</span></span>
* <span data-ttu-id="06172-174">`byte[] version`: Normaal weergegeven als een tekenreeks, is de versie ook ingesteld door de server.</span><span class="sxs-lookup"><span data-stu-id="06172-174">`byte[] version`: Normally represented as a string, the version is also set by the server.</span></span>
* <span data-ttu-id="06172-175">`boolean deleted`: Dit geeft aan dat de record is verwijderd, maar nog niet is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="06172-175">`boolean deleted`: Indicates that the record has been deleted but not purged yet.</span></span>  <span data-ttu-id="06172-176">Gebruik geen `deleted` als in uw klasse-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="06172-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="06172-177">De `id` veld is vereist.</span><span class="sxs-lookup"><span data-stu-id="06172-177">The `id` field is required.</span></span>  <span data-ttu-id="06172-178">De `updatedAt` veld en `version` veld worden gebruikt voor offlinesynchronisatie (voor incrementele synchronisatie en conflict respectievelijk).</span><span class="sxs-lookup"><span data-stu-id="06172-178">The `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="06172-179">De `createdAt` veld is een verwijzingsveld en wordt niet gebruikt door de client.</span><span class="sxs-lookup"><span data-stu-id="06172-179">The `createdAt` field is a reference field and is not used by the client.</span></span>  <span data-ttu-id="06172-180">De namen zijn namen van de eigenschappen 'in-the-wire' en niet aanpasbaar.</span><span class="sxs-lookup"><span data-stu-id="06172-180">The names are "across-the-wire" names of the properties and are not adjustable.</span></span>  <span data-ttu-id="06172-181">U kunt echter een toewijzing maken tussen uw object en de namen van de 'in-the-wire' met behulp van de [gson] [ 3] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="06172-181">However, you can create a mapping between your object and the "across-the-wire" names using the [gson][3] library.</span></span>  <span data-ttu-id="06172-182">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="06172-182">For example:</span></span>

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

### <a name="create-a-table-reference"></a><span data-ttu-id="06172-183">De tabelverwijzing van een maken</span><span class="sxs-lookup"><span data-stu-id="06172-183">Create a Table Reference</span></span>

<span data-ttu-id="06172-184">Als u een tabel, maakt u eerst een [MobileServiceTable] [ 8] object door het aanroepen van de **getTable** methode op de [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="06172-184">To access a table, first create a [MobileServiceTable][8] object by calling the **getTable** method on the [MobileServiceClient][9].</span></span>  <span data-ttu-id="06172-185">Deze methode heeft twee overloads:</span><span class="sxs-lookup"><span data-stu-id="06172-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="06172-186">In de volgende code **mClient** is een verwijzing naar uw MobileServiceClient-object.</span><span class="sxs-lookup"><span data-stu-id="06172-186">In the following code, **mClient** is a reference to your MobileServiceClient object.</span></span>  <span data-ttu-id="06172-187">De eerste overbelasting wordt gebruikt voor naam van de klasse en de naam van de tabel hetzelfde zijn waarbij de in de Snelstartgids wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="06172-187">The first overload is used where the class name and the table name are the same, and is the one used in the Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="06172-188">De tweede overbelasting wordt gebruikt wanneer de tabelnaam die van de naam van de klasse afwijkt: de eerste parameter is de naam van de tabel.</span><span class="sxs-lookup"><span data-stu-id="06172-188">The second overload is used when the table name is different from the class name: the first parameter is the table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="06172-189"><a name="query"></a>Een tabel met back-end</span><span class="sxs-lookup"><span data-stu-id="06172-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="06172-190">Eerst moet u een tabelverwijzing.</span><span class="sxs-lookup"><span data-stu-id="06172-190">First, obtain a table reference.</span></span>  <span data-ttu-id="06172-191">Vervolgens wordt een query uitgevoerd op de tabelverwijzing.</span><span class="sxs-lookup"><span data-stu-id="06172-191">Then execute a query on the table reference.</span></span>  <span data-ttu-id="06172-192">Een query is een combinatie van:</span><span class="sxs-lookup"><span data-stu-id="06172-192">A query is any combination of:</span></span>

* <span data-ttu-id="06172-193">Een `.where()` [filter-component](#filtering).</span><span class="sxs-lookup"><span data-stu-id="06172-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="06172-194">Een `.orderBy()` [ordening component](#sorting).</span><span class="sxs-lookup"><span data-stu-id="06172-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="06172-195">Een `.select()` [veld selectiecomponent](#selection).</span><span class="sxs-lookup"><span data-stu-id="06172-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="06172-196">Een `.skip()` en `.top()` voor [wisselbare resultaten](#paging).</span><span class="sxs-lookup"><span data-stu-id="06172-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="06172-197">De componenten moeten worden opgenomen in de voorgaande bewerkingsvolgorde.</span><span class="sxs-lookup"><span data-stu-id="06172-197">The clauses must be presented in the preceding order.</span></span>

### <span data-ttu-id="06172-198"><a name="filter"></a>Filteren van resultaten</span><span class="sxs-lookup"><span data-stu-id="06172-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="06172-199">De algemene vorm van een query is:</span><span class="sxs-lookup"><span data-stu-id="06172-199">The general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts the async into a sync result
```

<span data-ttu-id="06172-200">Het vorige voorbeeld retourneert alle resultaten (maximaal de maximale paginagrootte ingesteld door de server).</span><span class="sxs-lookup"><span data-stu-id="06172-200">The preceding example returns all results (up to the maximum page size set by the server).</span></span>  <span data-ttu-id="06172-201">De `.execute()` methode voert u de query op de back-end.</span><span class="sxs-lookup"><span data-stu-id="06172-201">The `.execute()` method executes the query on the backend.</span></span>  <span data-ttu-id="06172-202">De query wordt geconverteerd naar een [OData v3] [ 19] query voor verzending naar de back-end van Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="06172-202">The query is converted to an [OData v3][19] query before transmission to the Mobile Apps backend.</span></span>  <span data-ttu-id="06172-203">Hebben ontvangen converteert de back-end voor mobiele Apps van de query naar een SQL-instructie voordat deze wordt uitgevoerd op de SQL Azure-instantie.</span><span class="sxs-lookup"><span data-stu-id="06172-203">On receipt, the Mobile Apps backend converts the query into an SQL statement before executing it on the SQL Azure instance.</span></span>  <span data-ttu-id="06172-204">Aangezien netwerkactiviteit enige tijd neemt de `.execute()` methode retourneert een [ `ListenableFuture<E>` ] [ 18].</span><span class="sxs-lookup"><span data-stu-id="06172-204">Since network activity takes some time, The `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="06172-205"><a name="filtering"></a>Geretourneerde gegevens filteren</span><span class="sxs-lookup"><span data-stu-id="06172-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="06172-206">De uitvoering van de volgende query retourneert alle items uit de **ToDoItem** tabel waar **voltooid** gelijk is aan **false**.</span><span class="sxs-lookup"><span data-stu-id="06172-206">The following query execution returns all items from the **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="06172-207">**mToDoTable** is de verwijzing naar de tabel van de mobiele service die we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="06172-207">**mToDoTable** is the reference to the mobile service table that we created previously.</span></span>

<span data-ttu-id="06172-208">Definieer een filter met de **waar** methodeaanroep op de tabelverwijzing.</span><span class="sxs-lookup"><span data-stu-id="06172-208">Define a filter using the **where** method call on the table reference.</span></span> <span data-ttu-id="06172-209">De **waar** methode wordt gevolgd door een **veld** methode gevolgd door een methode die het predicaat logische aangeeft.</span><span class="sxs-lookup"><span data-stu-id="06172-209">The **where** method is followed by a **field** method followed by a method that specifies the logical predicate.</span></span> <span data-ttu-id="06172-210">Mogelijke predikaat methoden omvatten **eq** (is gelijk aan), **ne** (niet gelijk) **gt** (groter dan) **ge** (groter dan of gelijk zijn aan), **lt** (minder dan,) **RP** (kleiner dan of gelijk aan).</span><span class="sxs-lookup"><span data-stu-id="06172-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="06172-211">Deze methoden kunnen u velden en de tekenreeks op specifieke waarden te vergelijken.</span><span class="sxs-lookup"><span data-stu-id="06172-211">These methods let you compare number and string fields to specific values.</span></span>

<span data-ttu-id="06172-212">U kunt filteren op datums.</span><span class="sxs-lookup"><span data-stu-id="06172-212">You can filter on dates.</span></span> <span data-ttu-id="06172-213">De volgende methoden kunnen u de volledige datumveld of delen van de datum vergelijken: **jaar**, **maand**, **dag**, **uur**, **minuut**, en **tweede**.</span><span class="sxs-lookup"><span data-stu-id="06172-213">The following methods let you compare the entire date field or parts of the date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="06172-214">Het volgende voorbeeld wordt een filter voor artikelen waarvan *vervaldatum* gelijk is aan 2013.</span><span class="sxs-lookup"><span data-stu-id="06172-214">The following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="06172-215">De volgende methoden ondersteuning voor complexe filters op tekenreeksvelden: **startsWith**, **endsWith**, **concat**, **subtekenreeks**, **indexOf**, **vervangen**, **toLower**, **toUpper**, **trim**, en **lengte**.</span><span class="sxs-lookup"><span data-stu-id="06172-215">The following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="06172-216">Het volgende voorbeeld-filters voor de tabel rijen waar de *tekst* kolom begint met "PRI0."</span><span class="sxs-lookup"><span data-stu-id="06172-216">The following example filters for table rows where the *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="06172-217">De volgende methoden van de operator worden ondersteund op numerieke velden: **toevoegen**, **sub**, **mul**, **div**, **mod**, **floor**, **maximum**, en **afronden**.</span><span class="sxs-lookup"><span data-stu-id="06172-217">The following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="06172-218">Het volgende voorbeeld-filters voor de tabel rijen waar de **duur** een even getal is.</span><span class="sxs-lookup"><span data-stu-id="06172-218">The following example filters for table rows where the **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="06172-219">U kunt predikaten met deze logische methoden combineren: **en**, **of** en **niet**.</span><span class="sxs-lookup"><span data-stu-id="06172-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="06172-220">Twee van de voorgaande voorbeelden worden gecombineerd voor het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="06172-220">The following example combines two of the preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="06172-221">Groep en het nesten van logische operators:</span><span class="sxs-lookup"><span data-stu-id="06172-221">Group and nest logical operators:</span></span>

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

<span data-ttu-id="06172-222">Zie voor meer gedetailleerde discussie en voorbeelden van filteren, [verkennen van de uitgebreide functionaliteit van het model van de query Android client][20].</span><span class="sxs-lookup"><span data-stu-id="06172-222">For more detailed discussion and examples of filtering, see [Exploring the richness of the Android client query model][20].</span></span>

### <span data-ttu-id="06172-223"><a name="sorting"></a>Geretourneerde gegevens sorteren</span><span class="sxs-lookup"><span data-stu-id="06172-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="06172-224">De volgende code retourneert alle items uit een tabel met **taken** gesorteerd oplopende door de *tekst* veld.</span><span class="sxs-lookup"><span data-stu-id="06172-224">The following code returns all items from a table of **ToDoItems** sorted ascending by the *text* field.</span></span> <span data-ttu-id="06172-225">*mToDoTable* is de verwijzing naar de back-end-tabel die u eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="06172-225">*mToDoTable* is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="06172-226">De eerste parameter van de **orderBy** methode is een tekenreeks die gelijk is aan de naam van het veld op waarop u wilt sorteren.</span><span class="sxs-lookup"><span data-stu-id="06172-226">The first parameter of the **orderBy** method is a string equal to the name of the field on which to sort.</span></span> <span data-ttu-id="06172-227">De tweede parameter gebruikt de **QueryOrder** opsomming om op te geven of u wilt sorteren oplopende of aflopende.</span><span class="sxs-lookup"><span data-stu-id="06172-227">The second parameter uses the **QueryOrder** enumeration to specify whether to sort ascending or descending.</span></span>  <span data-ttu-id="06172-228">Als u filtert met behulp van de ***waar*** methode, de ***waar*** methode moet worden aangeroepen voordat de ***orderBy*** methode.</span><span class="sxs-lookup"><span data-stu-id="06172-228">If you are filtering using the ***where*** method, the ***where*** method must be invoked before the ***orderBy*** method.</span></span>

### <span data-ttu-id="06172-229"><a name="selection"></a>Selecteer specifieke kolommen</span><span class="sxs-lookup"><span data-stu-id="06172-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="06172-230">De volgende code laat zien hoe het retourneren van alle items van een tabel met **taken**, maar worden alleen de **voltooid** en **tekst** velden.</span><span class="sxs-lookup"><span data-stu-id="06172-230">The following code illustrates how to return all items from a table of **ToDoItems**, but only displays the **complete** and **text** fields.</span></span> <span data-ttu-id="06172-231">**mToDoTable** is de verwijzing naar de back-end-tabel die we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="06172-231">**mToDoTable** is the reference to the backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="06172-232">De parameters voor de functie select zijn de tekenreeksnamen van de van de tabel kolommen die u wilt retourneren.</span><span class="sxs-lookup"><span data-stu-id="06172-232">The parameters to the select function are the string names of the table's columns that you want to return.</span></span>  <span data-ttu-id="06172-233">De **Selecteer** methode moet volgen methoden zoals **waar** en **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="06172-233">The **select** method needs to follow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="06172-234">Het kan worden gevolgd door methoden zoals paginering **overslaan** en **boven**.</span><span class="sxs-lookup"><span data-stu-id="06172-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="06172-235"><a name="paging"></a>Gegevens weergeven op pagina 's</span><span class="sxs-lookup"><span data-stu-id="06172-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="06172-236">Gegevens **altijd** geretourneerd op pagina's.</span><span class="sxs-lookup"><span data-stu-id="06172-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="06172-237">Het maximum aantal records dat wordt geretourneerd is door de server ingesteld.</span><span class="sxs-lookup"><span data-stu-id="06172-237">The maximum number of records returned is set by the server.</span></span>  <span data-ttu-id="06172-238">Als de client meer records vraagt, retourneert de server het maximum aantal records.</span><span class="sxs-lookup"><span data-stu-id="06172-238">If the client requests more records, then the server returns the maximum number of records.</span></span>  <span data-ttu-id="06172-239">De maximale grootte op de server is standaard 50 records.</span><span class="sxs-lookup"><span data-stu-id="06172-239">By default, the maximum page size on the server is 50 records.</span></span>

<span data-ttu-id="06172-240">Het eerste voorbeeld laat zien hoe de bovenste vijf items selecteren uit een tabel.</span><span class="sxs-lookup"><span data-stu-id="06172-240">The first example shows how to select the top five items from a table.</span></span> <span data-ttu-id="06172-241">De query retourneert de items van een tabel met **taken**.</span><span class="sxs-lookup"><span data-stu-id="06172-241">The query returns the items from a table of **ToDoItems**.</span></span> <span data-ttu-id="06172-242">**mToDoTable** is de verwijzing naar de back-end-tabel die u eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="06172-242">**mToDoTable** is the reference to the backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="06172-243">Hier volgt een query die de eerste vijf items wordt overgeslagen en retourneert vervolgens de volgende vijf:</span><span class="sxs-lookup"><span data-stu-id="06172-243">Here's a query that skips the first five items, and then returns the next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="06172-244">Als u ophalen van alle records in een tabel wilt, implementeert u code worden herhaald voor alle pagina's:</span><span class="sxs-lookup"><span data-stu-id="06172-244">If you wish to get all records in a table, implement code to iterate over all pages:</span></span>

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

<span data-ttu-id="06172-245">Een aanvraag voor alle records met deze methode maakt een minimum van twee aanvragen voor de back-end van Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="06172-245">A request for all records using this method creates a minimum of two requests to the Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="06172-246">Het formaat van de juiste kiezen een evenwicht tussen geheugengebruik terwijl de aanvraag er gebeurt, bandbreedtegebruik en vertraging bij het ontvangen van de gegevens volledig is.</span><span class="sxs-lookup"><span data-stu-id="06172-246">Choosing the right page size is a balance between memory usage while the request is happening, bandwidth usage and delay in receiving the data completely.</span></span>  <span data-ttu-id="06172-247">De standaardwaarde (50 records) is geschikt voor alle apparaten.</span><span class="sxs-lookup"><span data-stu-id="06172-247">The default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="06172-248">Als u alleen op geheugenapparaten met grotere werkt, verhoogt u maximaal 500.</span><span class="sxs-lookup"><span data-stu-id="06172-248">If you exclusively operate on larger memory devices, increase up to 500.</span></span>  <span data-ttu-id="06172-249">We hebben vastgesteld dat de pagina vergroten dan 500 registreert resultaten in onaanvaardbaar vertragingen en grote geheugenproblemen.</span><span class="sxs-lookup"><span data-stu-id="06172-249">We have found that increasing the page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="06172-250"><a name="chaining"></a>Hoe: querymethoden samenvoegen</span><span class="sxs-lookup"><span data-stu-id="06172-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="06172-251">De methoden die worden gebruikt in het opvragen van de back-end-tabellen kunnen worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="06172-251">The methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="06172-252">Methoden voor het query-koppeling kunt u specifieke kolommen met gefilterde rijen die worden gesorteerd en wisselbare selecteren.</span><span class="sxs-lookup"><span data-stu-id="06172-252">Chaining query methods allows you to select specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="06172-253">U kunt complexe logische filters maken.</span><span class="sxs-lookup"><span data-stu-id="06172-253">You can create complex logical filters.</span></span>  <span data-ttu-id="06172-254">Elke querymethode retourneert een Query-object.</span><span class="sxs-lookup"><span data-stu-id="06172-254">Each query method returns a Query object.</span></span> <span data-ttu-id="06172-255">Aanroepen om te beëindigen van de reeks methoden en daadwerkelijk uitvoeren van de query, het **uitvoeren** methode.</span><span class="sxs-lookup"><span data-stu-id="06172-255">To end the series of methods and actually run the query, call the **execute** method.</span></span> <span data-ttu-id="06172-256">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="06172-256">For example:</span></span>

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

<span data-ttu-id="06172-257">De keten querymethoden moeten als volgt worden gerangschikt:</span><span class="sxs-lookup"><span data-stu-id="06172-257">The chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="06172-258">Filteren (**waar**) methoden.</span><span class="sxs-lookup"><span data-stu-id="06172-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="06172-259">Sorteren (**orderBy**) methoden.</span><span class="sxs-lookup"><span data-stu-id="06172-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="06172-260">Selectie (**Selecteer**) methoden.</span><span class="sxs-lookup"><span data-stu-id="06172-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="06172-261">wisselgeheugengebruik (**overslaan** en **boven**) methoden.</span><span class="sxs-lookup"><span data-stu-id="06172-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="06172-262"><a name="binding"></a>Gegevens binden aan de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="06172-262"><a name="binding"></a>Bind data to the user interface</span></span>

<span data-ttu-id="06172-263">Gegevensbinding omvat drie onderdelen:</span><span class="sxs-lookup"><span data-stu-id="06172-263">Data binding involves three components:</span></span>

* <span data-ttu-id="06172-264">De gegevensbron</span><span class="sxs-lookup"><span data-stu-id="06172-264">The data source</span></span>
* <span data-ttu-id="06172-265">De indeling startscherm</span><span class="sxs-lookup"><span data-stu-id="06172-265">The screen layout</span></span>
* <span data-ttu-id="06172-266">De adapter die de twee elkaar verbindt.</span><span class="sxs-lookup"><span data-stu-id="06172-266">The adapter that ties the two together.</span></span>

<span data-ttu-id="06172-267">In onze voorbeeldcode we de gegevens retourneert uit de tabel Mobile Apps SQL Azure **ToDoItem** in een matrix.</span><span class="sxs-lookup"><span data-stu-id="06172-267">In our sample code, we return the data from the Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="06172-268">Deze activiteit is een algemene patroon voor toepassingen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="06172-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="06172-269">Databasequery's retourneren vaak een verzameling rijen die de client in een lijst of matrix opgehaald.</span><span class="sxs-lookup"><span data-stu-id="06172-269">Database queries often return a collection of rows that the client gets in a list or array.</span></span> <span data-ttu-id="06172-270">De matrix is in dit voorbeeld wordt de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="06172-270">In this sample, the array is the data source.</span></span>  <span data-ttu-id="06172-271">De code wordt een schermindeling die de weergave van de gegevens die wordt weergegeven op het apparaat wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="06172-271">The code specifies a screen layout that defines the view of the data that appears on the device.</span></span>  <span data-ttu-id="06172-272">Afhankelijk van de twee samen met een netwerkadapter, die in deze code een uitbreiding is van de **ArrayAdapter&lt;ToDoItem&gt;**  klasse.</span><span class="sxs-lookup"><span data-stu-id="06172-272">The two are bound together with an adapter, which in this code is an extension of the **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="06172-273"><a name="layout"></a>De indeling definiëren</span><span class="sxs-lookup"><span data-stu-id="06172-273"><a name="layout"></a>Define the Layout</span></span>

<span data-ttu-id="06172-274">De indeling wordt gedefinieerd door verschillende codefragmenten van XML-code.</span><span class="sxs-lookup"><span data-stu-id="06172-274">The layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="06172-275">Uitgaande van een bestaande indeling, het volgende codevoorbeeld geeft de **ListView** wilt vullen met onze gegevens van de server.</span><span class="sxs-lookup"><span data-stu-id="06172-275">Given an existing layout, the following code represents the **ListView** we want to populate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="06172-276">In de vorige code de *listitem* kenmerk geeft de id van de indeling voor een afzonderlijke rij in de lijst.</span><span class="sxs-lookup"><span data-stu-id="06172-276">In the preceding code, the *listitem* attribute specifies the id of the layout for an individual row in the list.</span></span> <span data-ttu-id="06172-277">Deze code geeft een selectievakje en de bijbehorende tekst en eenmaal voor elk item in de lijst wordt geïnstantieerd.</span><span class="sxs-lookup"><span data-stu-id="06172-277">This code specifies a check box and its associated text and gets instantiated once for each item in the list.</span></span> <span data-ttu-id="06172-278">Deze indeling niet wordt weergegeven de **id** veld en een complexere indeling aanvullende velden in de weergave wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="06172-278">This layout does not display the **id** field, and a more complex layout would specify additional fields in the display.</span></span> <span data-ttu-id="06172-279">Deze code is in de **row_list_to_do.xml** bestand.</span><span class="sxs-lookup"><span data-stu-id="06172-279">This code is in the **row_list_to_do.xml** file.</span></span>

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

#### <span data-ttu-id="06172-280"><a name="adapter"></a>De adapter definiëren</span><span class="sxs-lookup"><span data-stu-id="06172-280"><a name="adapter"></a>Define the adapter</span></span>
<span data-ttu-id="06172-281">Omdat de gegevensbron van onze weergave een matrix met is **ToDoItem**, we subklasse onze-adapter van een **ArrayAdapter&lt;ToDoItem&gt;**  klasse.</span><span class="sxs-lookup"><span data-stu-id="06172-281">Since the data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="06172-282">Deze subklasse produceert een weergave voor elke **ToDoItem** met behulp van de **row_list_to_do** lay-out.</span><span class="sxs-lookup"><span data-stu-id="06172-282">This subclass produces a View for every **ToDoItem** using the **row_list_to_do** layout.</span></span>  <span data-ttu-id="06172-283">In onze code definiëren we de volgende klasse die is een uitbreiding van de **ArrayAdapter&lt;E&gt;**  klasse:</span><span class="sxs-lookup"><span data-stu-id="06172-283">In our code, we define the following class that is an extension of the **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="06172-284">Onderdrukking van de adapters **getView** methode.</span><span class="sxs-lookup"><span data-stu-id="06172-284">Override the adapters **getView** method.</span></span> <span data-ttu-id="06172-285">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="06172-285">For example:</span></span>

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

<span data-ttu-id="06172-286">We geen exemplaar maken van deze klasse in onze activiteit als volgt:</span><span class="sxs-lookup"><span data-stu-id="06172-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="06172-287">De tweede parameter voor de constructor ToDoItemAdapter is een verwijzing naar de indeling.</span><span class="sxs-lookup"><span data-stu-id="06172-287">The second parameter to the ToDoItemAdapter constructor is a reference to the layout.</span></span> <span data-ttu-id="06172-288">We kunnen nu exemplaar maken van de **ListView** en toewijzen van de adapter in de **ListView**.</span><span class="sxs-lookup"><span data-stu-id="06172-288">We can now instantiate the **ListView** and assign the adapter to the **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="06172-289"><a name="use-adapter"></a>Gebruik de Adapter moet worden gebonden aan de gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="06172-289"><a name="use-adapter"></a>Use the Adapter to Bind to the UI</span></span>

<span data-ttu-id="06172-290">U bent nu klaar voor gebruik van de gegevensbinding.</span><span class="sxs-lookup"><span data-stu-id="06172-290">You are now ready to use data binding.</span></span> <span data-ttu-id="06172-291">De volgende code laat zien hoe het ophalen van items in de tabel en wordt de lokale adapter gevuld met de geretourneerde artikelen.</span><span class="sxs-lookup"><span data-stu-id="06172-291">The following code shows how to get items in the table and fills the local adapter with the returned items.</span></span>

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

<span data-ttu-id="06172-292">Aanroepen van de adapter elk gewenst moment u wijzigt de **ToDoItem** tabel.</span><span class="sxs-lookup"><span data-stu-id="06172-292">Call the adapter any time you modify the **ToDoItem** table.</span></span> <span data-ttu-id="06172-293">Omdat wijzigingen op basis van door een andere record klaar bent, kunt u een enkele rij in plaats van een verzameling verwerken.</span><span class="sxs-lookup"><span data-stu-id="06172-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="06172-294">Wanneer u een item invoegt, roept de **toevoegen** methode op de adapter; wanneer te verwijderen, roept de **verwijderen** methode.</span><span class="sxs-lookup"><span data-stu-id="06172-294">When you insert an item, call the **add** method on the adapter; when deleting, call the **remove** method.</span></span>

<span data-ttu-id="06172-295">U vindt een compleet voorbeeld in de [Android Quick Start-Project][21].</span><span class="sxs-lookup"><span data-stu-id="06172-295">You can find a complete example in the [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="06172-296"><a name="inserting"></a>Gegevens invoegen in de back-end</span><span class="sxs-lookup"><span data-stu-id="06172-296"><a name="inserting"></a>Insert data into the backend</span></span>

<span data-ttu-id="06172-297">Een instantie van de *ToDoItem* klasse en stel de eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="06172-297">Instantiate an instance of the *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="06172-298">Gebruik vervolgens **insert()** een object in te voegen:</span><span class="sxs-lookup"><span data-stu-id="06172-298">Then use **insert()** to insert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="06172-299">Het geretourneerde entiteit overeenkomt met de gegevens ingevoegd in de tabel back-end van de ID en andere waarden opgenomen (zoals de `createdAt`, `updatedAt`, en `version` velden) ingesteld voor de back-end.</span><span class="sxs-lookup"><span data-stu-id="06172-299">The returned entity matches the data inserted into the backend table, included the ID and any other values (such as the `createdAt`, `updatedAt`, and `version` fields) set on the backend.</span></span>

<span data-ttu-id="06172-300">Mobile Apps-tabellen vereisen een primaire sleutelkolom met de naam **id**.</span><span class="sxs-lookup"><span data-stu-id="06172-300">Mobile Apps tables require a primary key column named **id**.</span></span> <span data-ttu-id="06172-301">In deze kolom moet een tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="06172-301">This column must be a string.</span></span> <span data-ttu-id="06172-302">De standaardwaarde van de kolom-ID is een GUID.</span><span class="sxs-lookup"><span data-stu-id="06172-302">The default value of the ID column is a GUID.</span></span>  <span data-ttu-id="06172-303">U kunt andere unieke waarden, zoals e-mailadressen of gebruikersnamen op te geven.</span><span class="sxs-lookup"><span data-stu-id="06172-303">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="06172-304">Wanneer de waarde van een tekenreeks-ID niet voor een ingevoegde record opgegeven is, genereert de back-end een nieuwe GUID.</span><span class="sxs-lookup"><span data-stu-id="06172-304">When a string ID value is not provided for an inserted record, the backend generates a new GUID.</span></span>

<span data-ttu-id="06172-305">ID van tekenreekswaarden bieden de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="06172-305">String ID values provide the following advantages:</span></span>

* <span data-ttu-id="06172-306">Id's kunnen worden gegenereerd zonder dat een retouren naar de database.</span><span class="sxs-lookup"><span data-stu-id="06172-306">IDs can be generated without making a round trip to the database.</span></span>
* <span data-ttu-id="06172-307">Records zijn gemakkelijker te samenvoegen uit verschillende tabellen of databases.</span><span class="sxs-lookup"><span data-stu-id="06172-307">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="06172-308">Id-waarden worden geïntegreerd beter met een toepassing logica.</span><span class="sxs-lookup"><span data-stu-id="06172-308">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="06172-309">Tekenreeks-ID-waarden zijn **REQUIRED** voor offlinesynchronisatie ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="06172-309">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="06172-310">U kunt een Id niet wijzigen zodra deze is opgeslagen in de back-end-database.</span><span class="sxs-lookup"><span data-stu-id="06172-310">You cannot change an Id once it is stored in the backend database.</span></span>

## <span data-ttu-id="06172-311"><a name="updating"></a>Gegevens bijwerken in een mobiele app</span><span class="sxs-lookup"><span data-stu-id="06172-311"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="06172-312">Voor het bijwerken van gegevens in een tabel, geeft u het nieuwe object wilt de **update()** methode.</span><span class="sxs-lookup"><span data-stu-id="06172-312">To update data in a table, pass the new object to the **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="06172-313">In dit voorbeeld *item* is een verwijzing naar een rij in de *ToDoItem* tabel een aantal wijzigingen aangebracht heeft.</span><span class="sxs-lookup"><span data-stu-id="06172-313">In this example, *item* is a reference to a row in the *ToDoItem* table, which has had some changes made to it.</span></span>  <span data-ttu-id="06172-314">De rij met dezelfde **id** wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="06172-314">The row with the same **id** is updated.</span></span>

## <span data-ttu-id="06172-315"><a name="deleting"></a>Gegevens in een mobiele app verwijderen</span><span class="sxs-lookup"><span data-stu-id="06172-315"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="06172-316">De volgende code laat zien hoe om gegevens te verwijderen uit een tabel door te geven van het gegevensobject.</span><span class="sxs-lookup"><span data-stu-id="06172-316">The following code shows how to delete data from a table by specifying the data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="06172-317">U kunt ook een item verwijderen door op te geven de **id** veld van de rij te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="06172-317">You can also delete an item by specifying the **id** field of the row to delete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="06172-318"><a name="lookup"></a>Een specifiek item door-Id niet opzoeken</span><span class="sxs-lookup"><span data-stu-id="06172-318"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="06172-319">Opzoeken van een item met een specifieke **id** veld met de **lookUp()** methode:</span><span class="sxs-lookup"><span data-stu-id="06172-319">Look up an item with a specific **id** field with the **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="06172-320"><a name="untyped"></a>Procedure: werken met niet-getypeerde gegevens</span><span class="sxs-lookup"><span data-stu-id="06172-320"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="06172-321">De niet-getypeerde programmeermodel biedt u de precieze controle over de JSON-serialisatie.</span><span class="sxs-lookup"><span data-stu-id="06172-321">The untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="06172-322">Er zijn enkele algemene scenario's waar u kunt desgewenst een niet-getypeerde programmeermodel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="06172-322">There are some common scenarios where you may wish to use an untyped programming model.</span></span> <span data-ttu-id="06172-323">Als bijvoorbeeld uw back-end-tabel veel kolommen bevat en u hoeft alleen te verwijzen naar een subset van de kolommen.</span><span class="sxs-lookup"><span data-stu-id="06172-323">For example, if your backend table contains many columns and you only need to reference a subset of the columns.</span></span>  <span data-ttu-id="06172-324">De getypte model, moet u de kolommen die zijn gedefinieerd in de back-end voor mobiele Apps in uw gegevensklasse definiëren.</span><span class="sxs-lookup"><span data-stu-id="06172-324">The typed model requires you to define all the columns defined in the Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="06172-325">De meeste van de API-aanroepen voor toegang tot gegevens zijn vergelijkbaar met de getypte programming aanroepen.</span><span class="sxs-lookup"><span data-stu-id="06172-325">Most of the API calls for accessing data are similar to the typed programming calls.</span></span> <span data-ttu-id="06172-326">Het belangrijkste verschil is dat in het model niet-getypeerde u methoden aanroepen op de **MobileServiceJsonTable** object, in plaats van de **MobileServiceTable** object.</span><span class="sxs-lookup"><span data-stu-id="06172-326">The main difference is that in the untyped model you invoke methods on the **MobileServiceJsonTable** object, instead of the **MobileServiceTable** object.</span></span>

### <span data-ttu-id="06172-327"><a name="json_instance"></a>Geen exemplaar maken van een niet-getypeerde tabel</span><span class="sxs-lookup"><span data-stu-id="06172-327"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="06172-328">Net als bij de getypte model kunt u beginnen met het ophalen van een tabelverwijzing, maar in dit geval is een **MobileServicesJsonTable** object.</span><span class="sxs-lookup"><span data-stu-id="06172-328">Similar to the typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="06172-329">De verwijzing verkrijgen door het aanroepen van de **getTable** methode op een exemplaar van de client:</span><span class="sxs-lookup"><span data-stu-id="06172-329">Obtain the reference by calling the **getTable** method on an instance of the client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="06172-330">Nadat u hebt gemaakt dat een exemplaar van de **MobileServiceJsonTable**, heeft bijna de dezelfde API beschikbaar als met de getypte programmeermodel.</span><span class="sxs-lookup"><span data-stu-id="06172-330">Once you have created an instance of the **MobileServiceJsonTable**, it has virtually the same API available as with the typed programming model.</span></span> <span data-ttu-id="06172-331">In sommige gevallen kan de methoden maken gebruik van een niet-getypeerde parameter in plaats van een type parameter.</span><span class="sxs-lookup"><span data-stu-id="06172-331">In some cases, the methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="06172-332"><a name="json_insert"></a>Invoegen in een niet-getypeerde tabel</span><span class="sxs-lookup"><span data-stu-id="06172-332"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="06172-333">De volgende code laat zien hoe een INSERT-bewerking uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="06172-333">The following code shows how to do an insert.</span></span> <span data-ttu-id="06172-334">De eerste stap is het maken van een [JsonObject][1], die deel uitmaakt van de [gson] [ 3] bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="06172-334">The first step is to create a [JsonObject][1], which is part of the [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="06172-335">Vervolgens gebruikt u **insert()** het niet-getypeerde object in de tabel invoegen.</span><span class="sxs-lookup"><span data-stu-id="06172-335">Then, Use **insert()** to insert the untyped object into the table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="06172-336">Als u de ID van het ingevoegde object niet ophalen moet, gebruikt u de **getAsJsonPrimitive()** methode.</span><span class="sxs-lookup"><span data-stu-id="06172-336">If you need to get the ID of the inserted object, use the **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="06172-337"><a name="json_delete"></a>Verwijderen uit een niet-getypeerde tabel</span><span class="sxs-lookup"><span data-stu-id="06172-337"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="06172-338">De volgende code toont hoe u verwijdert een exemplaar, in dit geval hetzelfde exemplaar van een **JsonObject** die is gemaakt in de voorafgaande *invoegen* voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="06172-338">The following code shows how to delete an instance, in this case, the same instance of a **JsonObject** that was created in the prior *insert* example.</span></span> <span data-ttu-id="06172-339">De code is hetzelfde als bij de getypte letters, maar de methode heeft een andere handtekening omdat deze verwijst naar een **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="06172-339">The code is the same as with the typed case, but the method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="06172-340">U kunt ook een exemplaar rechtstreeks door met de bijbehorende ID verwijderen:</span><span class="sxs-lookup"><span data-stu-id="06172-340">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="06172-341"><a name="json_get"></a>Retourneert alle rijen uit een niet-getypeerde tabel</span><span class="sxs-lookup"><span data-stu-id="06172-341"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="06172-342">De volgende code laat zien hoe een hele tabel ophalen.</span><span class="sxs-lookup"><span data-stu-id="06172-342">The following code shows how to retrieve an entire table.</span></span> <span data-ttu-id="06172-343">Omdat u een tabel JSON gebruikt, kunt u slechts een deel van de tabelkolommen selectief ophalen.</span><span class="sxs-lookup"><span data-stu-id="06172-343">Since you are using a JSON Table, you can selectively retrieve only some of the table's columns.</span></span>

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

<span data-ttu-id="06172-344">Dezelfde set voor het filteren van filteren en methoden die beschikbaar voor het model getypte zijn paging beschikbaar zijn voor de niet-getypeerde model.</span><span class="sxs-lookup"><span data-stu-id="06172-344">The same set of filtering, filtering and paging methods that are available for the typed model are available for the untyped model.</span></span>

## <span data-ttu-id="06172-345"><a name="offline-sync"></a>Offlinesynchronisatie implementeren</span><span class="sxs-lookup"><span data-stu-id="06172-345"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="06172-346">Offline synchronisatie van gegevens van implementeert de Client-SDK van Azure Mobile Apps ook met behulp van een SQLite-database voor het opslaan van een kopie van de servergegevens lokaal.</span><span class="sxs-lookup"><span data-stu-id="06172-346">The Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database to store a copy of the server data locally.</span></span>  <span data-ttu-id="06172-347">Bewerkingen die worden uitgevoerd op een offline tabel vereisen geen mobiele connectiviteit te werken.</span><span class="sxs-lookup"><span data-stu-id="06172-347">Operations performed on an offline table do not require mobile connectivity to work.</span></span>  <span data-ttu-id="06172-348">Offline synchronisatie helpt prestaties ten koste van de complexere logica voor conflictoplossing en herstelmogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="06172-348">Offline sync aids in resilience and performance at the expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="06172-349">De Client-SDK van Azure Mobile Apps implementeert de volgende functies:</span><span class="sxs-lookup"><span data-stu-id="06172-349">The Azure Mobile Apps Client SDK implements the following features:</span></span>

* <span data-ttu-id="06172-350">Incrementele synchronisatie: Alleen bijgewerkt en nieuwe records worden gedownload verbruik van bandbreedte en geheugen.</span><span class="sxs-lookup"><span data-stu-id="06172-350">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="06172-351">Optimistische gelijktijdigheid: Operations wordt aangenomen dat slagen.</span><span class="sxs-lookup"><span data-stu-id="06172-351">Optimistic Concurrency: Operations are assumed to succeed.</span></span>  <span data-ttu-id="06172-352">Conflictoplossing wordt uitgesteld totdat de updates worden uitgevoerd op de server.</span><span class="sxs-lookup"><span data-stu-id="06172-352">Conflict Resolution is deferred until updates are performed on the server.</span></span>
* <span data-ttu-id="06172-353">Conflictoplossing: De SDK detecteert wanneer een conflicterende wijziging heeft aangebracht op de server en hooks biedt Waarschuw de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="06172-353">Conflict Resolution: The SDK detects when a conflicting change has been made at the server and provides hooks to alert the user.</span></span>
* <span data-ttu-id="06172-354">Voorlopig verwijderen: Verwijderde records zijn gemarkeerd als verwijderd, zodat andere apparaten hun offline configuratiecache bij te werken.</span><span class="sxs-lookup"><span data-stu-id="06172-354">Soft Delete: Deleted records are marked deleted, allowing other devices to update their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="06172-355">Offlinesynchronisatie initialiseren</span><span class="sxs-lookup"><span data-stu-id="06172-355">Initialize Offline Sync</span></span>

<span data-ttu-id="06172-356">Elke tabel offline moet worden gedefinieerd in de cache offline vóór gebruik.</span><span class="sxs-lookup"><span data-stu-id="06172-356">Each offline table must be defined in the offline cache before use.</span></span>  <span data-ttu-id="06172-357">Normaal gesproken tabeldefinitie gebeurt onmiddellijk na het maken van de client:</span><span class="sxs-lookup"><span data-stu-id="06172-357">Normally, table definition is done immediately after the creation of the client:</span></span>

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

                // Create a table definition.  As a best practice, store this with the model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define the table in the local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize the local store
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

### <a name="obtain-a-reference-to-the-offline-cache-table"></a><span data-ttu-id="06172-358">Een verwijzing naar de tabel Offline Cache</span><span class="sxs-lookup"><span data-stu-id="06172-358">Obtain a reference to the Offline Cache Table</span></span>

<span data-ttu-id="06172-359">Voor een online tabel, gebruikt u `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="06172-359">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="06172-360">Gebruik voor een offline tabel `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="06172-360">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="06172-361">De methoden die beschikbaar voor online-tabellen zijn (inclusief filteren, sorteren, paging, gegevens invoegen, bijwerken van gegevens en verwijderen van gegevens) werkt goed in online als offline tabellen.</span><span class="sxs-lookup"><span data-stu-id="06172-361">All the methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-the-local-offline-cache"></a><span data-ttu-id="06172-362">De lokale Cache voor het Offline synchroniseren</span><span class="sxs-lookup"><span data-stu-id="06172-362">Synchronize the Local Offline Cache</span></span>

<span data-ttu-id="06172-363">Synchronisatie is binnen het besturingselement van uw app.</span><span class="sxs-lookup"><span data-stu-id="06172-363">Synchronization is within the control of your app.</span></span>  <span data-ttu-id="06172-364">Hier volgt een voorbeeld van de synchronisatie-methode:</span><span class="sxs-lookup"><span data-stu-id="06172-364">Here is an example synchronization method:</span></span>

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

<span data-ttu-id="06172-365">Als de naam van de query is opgegeven voor de `.pull(query, queryname)` methode en vervolgens incrementele synchronisatie wordt gebruikt om terug te keren alleen de records die zijn gemaakt of gewijzigd sinds de laatste pull voltooid.</span><span class="sxs-lookup"><span data-stu-id="06172-365">If a query name is provided to the `.pull(query, queryname)` method, then incremental sync is used to return only records that have been created or changed since the last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="06172-366">Afhandeling van conflicten tijdens het Offline synchroniseren</span><span class="sxs-lookup"><span data-stu-id="06172-366">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="06172-367">Als een conflict zich tijdens voordoet een `.push()` bewerking, een `MobileServiceConflictException` gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="06172-367">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="06172-368">Het item server uitgegeven is ingesloten in de uitzondering en kan worden opgehaald door `.getItem()` op de uitzondering.</span><span class="sxs-lookup"><span data-stu-id="06172-368">The server-issued item is embedded in the exception and can be retrieved by `.getItem()` on the exception.</span></span>  <span data-ttu-id="06172-369">De push-bewerking door het aanroepen van de volgende items op het object MobileServiceSyncContext aanpassen:</span><span class="sxs-lookup"><span data-stu-id="06172-369">Adjust the push by calling the following items on the MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="06172-370">Wanneer alle conflicten zijn gemarkeerd als u wilt, aanroepen `.push()` om opnieuw op te lossen alle conflicten.</span><span class="sxs-lookup"><span data-stu-id="06172-370">Once all conflicts are marked as you wish, call `.push()` again to resolve all the conflicts.</span></span>

## <span data-ttu-id="06172-371"><a name="custom-api"></a>Een aangepaste API aanroepen</span><span class="sxs-lookup"><span data-stu-id="06172-371"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="06172-372">Een aangepaste API kunt u aangepaste eindpunten die serverfunctionaliteit weergeven die niet worden toegewezen aan een invoegen, bijwerken, verwijderen of leesbewerking definiëren.</span><span class="sxs-lookup"><span data-stu-id="06172-372">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="06172-373">Met behulp van een aangepaste API gebruiken, kunt u meer controle over messaging, hebben waaronder lezen en HTTP-bericht headers instellen en definiëren van een berichttekst de indeling dan JSON.</span><span class="sxs-lookup"><span data-stu-id="06172-373">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="06172-374">U aanroepen in een Android-client de **invokeApi** methode voor het eindpunt van de aangepaste API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="06172-374">From an Android client, you call the **invokeApi** method to call the custom API endpoint.</span></span> <span data-ttu-id="06172-375">Het volgende voorbeeld toont het aanroepen van een API-eindpunt met de naam **completeAll**, die de klasse van een verzameling met de naam retourneert **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="06172-375">The following example shows how to call an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

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

<span data-ttu-id="06172-376">De **invokeApi** methode wordt aangeroepen op de client, die een POST-aanvraag naar de nieuwe aangepaste API verzendt.</span><span class="sxs-lookup"><span data-stu-id="06172-376">The **invokeApi** method is called on the client, which sends a POST request to the new custom API.</span></span> <span data-ttu-id="06172-377">Het resultaat geretourneerd door de aangepaste API wordt weergegeven in een dialoogvenster weergegeven als er fouten zijn.</span><span class="sxs-lookup"><span data-stu-id="06172-377">The result returned by the custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="06172-378">Andere versies van **invokeApi** kunt u eventueel het verzenden van een object in de aanvraagtekst, geeft u de HTTP-methode en queryparameters aan de aanvraag te verzenden.</span><span class="sxs-lookup"><span data-stu-id="06172-378">Other versions of **invokeApi** let you optionally send an object in the request body, specify the HTTP method, and send query parameters with the request.</span></span> <span data-ttu-id="06172-379">Versies van getypeerde **invokeApi** ook worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="06172-379">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="06172-380"><a name="authentication"></a>Verificatie toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="06172-380"><a name="authentication"></a>Add authentication to your app</span></span>

<span data-ttu-id="06172-381">Het toevoegen van deze functies beschrijven zelfstudies al in detail.</span><span class="sxs-lookup"><span data-stu-id="06172-381">Tutorials already describe in detail how to add these features.</span></span>

<span data-ttu-id="06172-382">App Service ondersteunt [verifiëren van gebruikers van de app](app-service-mobile-android-get-started-users.md) met behulp van verschillende externe id-providers: Facebook, Google, Microsoft-Account, Twitter en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="06172-382">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="06172-383">U kunt machtigingen instellen voor tabellen toegang voor specifieke bewerkingen voor alleen geverifieerde gebruikers te beperken.</span><span class="sxs-lookup"><span data-stu-id="06172-383">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="06172-384">U kunt ook de identiteit van de geverifieerde gebruikers gebruiken voor het implementeren van autorisatieregels in uw back-end.</span><span class="sxs-lookup"><span data-stu-id="06172-384">You can also use the identity of authenticated users to implement authorization rules in your backend.</span></span>

<span data-ttu-id="06172-385">Twee verificatie stromen worden ondersteund: een **server** stroom en een **client** stroom.</span><span class="sxs-lookup"><span data-stu-id="06172-385">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="06172-386">De stroom van de server biedt de eenvoudigste verificatie-ervaring, is afhankelijk van de identiteit providers webinterface.</span><span class="sxs-lookup"><span data-stu-id="06172-386">The server flow provides the simplest authentication experience, as it relies on the identity providers web interface.</span></span>  <span data-ttu-id="06172-387">Er zijn geen extra SDK's zijn vereist voor het implementeren van verificatie van de stroom.</span><span class="sxs-lookup"><span data-stu-id="06172-387">No additional SDKs are required to implement server flow authentication.</span></span> <span data-ttu-id="06172-388">Verificatie van de stroom biedt geen een diepe integratie in het mobiele apparaat en wordt alleen aanbevolen voor bewijs van concept scenario's.</span><span class="sxs-lookup"><span data-stu-id="06172-388">Server flow authentication does not provide a deep integration into the mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="06172-389">De stroom kunt voor een betere integratie met apparaatspecifieke mogelijkheden, zoals het eenmalige aanmelding is afhankelijk van de SDK's die worden geleverd door de identiteitsprovider.</span><span class="sxs-lookup"><span data-stu-id="06172-389">The client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by the identity provider.</span></span>  <span data-ttu-id="06172-390">U kunt bijvoorbeeld de Facebook SDK integreren in uw mobiele App.</span><span class="sxs-lookup"><span data-stu-id="06172-390">For example, you can integrate the Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="06172-391">Mobiele clients worden omgewisseld in de Facebook-app en bevestigt de aanmelding voordat wisselen terug naar uw mobiele app.</span><span class="sxs-lookup"><span data-stu-id="06172-391">The mobile client swaps into the Facebook app and confirms your sign-on before swapping back to your mobile app.</span></span>

<span data-ttu-id="06172-392">Vier stappen zijn vereist voor verificatie in uw app inschakelen:</span><span class="sxs-lookup"><span data-stu-id="06172-392">Four steps are required to enable authentication in your app:</span></span>

* <span data-ttu-id="06172-393">Uw app registreren voor verificatie met een id-provider.</span><span class="sxs-lookup"><span data-stu-id="06172-393">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="06172-394">Configureer uw App Service-back-end.</span><span class="sxs-lookup"><span data-stu-id="06172-394">Configure your App Service backend.</span></span>
* <span data-ttu-id="06172-395">Tabelmachtigingen beperken voor geverifieerde gebruikers alleen op de App Service-back-end.</span><span class="sxs-lookup"><span data-stu-id="06172-395">Restrict table permissions to authenticated users only on the App Service backend.</span></span>
* <span data-ttu-id="06172-396">Verificatiecode toevoegen aan uw app.</span><span class="sxs-lookup"><span data-stu-id="06172-396">Add authentication code to your app.</span></span>

<span data-ttu-id="06172-397">U kunt machtigingen instellen voor tabellen toegang voor specifieke bewerkingen voor alleen geverifieerde gebruikers te beperken.</span><span class="sxs-lookup"><span data-stu-id="06172-397">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="06172-398">U kunt ook de SID van een geverifieerde gebruiker te wijzigen van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="06172-398">You can also use the SID of an authenticated user to modify requests.</span></span>  <span data-ttu-id="06172-399">Raadpleeg voor meer informatie [aan de slag met verificatie] en de procedure voor Server SDK-documentatie.</span><span class="sxs-lookup"><span data-stu-id="06172-399">For more information, review [Get started with authentication] and the Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="06172-400"><a name="caching"></a>: Verificatiestroom Server</span><span class="sxs-lookup"><span data-stu-id="06172-400"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="06172-401">De volgende code start een server stroom aanmelding met de Google-provider.</span><span class="sxs-lookup"><span data-stu-id="06172-401">The following code starts a server flow login process using the Google provider.</span></span>  <span data-ttu-id="06172-402">Aanvullende configuratie is vereist vanwege de beveiligingsvereisten voor de Google-provider:</span><span class="sxs-lookup"><span data-stu-id="06172-402">Additional configuration is required because of the security requirements for the Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="06172-403">Voeg bovendien de volgende methode toe aan de hoofdklasse van de activiteit:</span><span class="sxs-lookup"><span data-stu-id="06172-403">In addition, add the following method to the main Activity class:</span></span>

```java
// You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check the request code matches the one we send in the login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check the error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="06172-404">De `GOOGLE_LOGIN_REQUEST_CODE` gedefinieerd in uw belangrijkste activiteit wordt gebruikt voor de `login()` methode en binnen de `onActivityResult()` methode.</span><span class="sxs-lookup"><span data-stu-id="06172-404">The `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for the `login()` method and within the `onActivityResult()` method.</span></span>  <span data-ttu-id="06172-405">U kunt een uniek nummer, zolang de hetzelfde nummer wordt gebruikt binnen de `login()` methode en de `onActivityResult()` methode.</span><span class="sxs-lookup"><span data-stu-id="06172-405">You can choose any unique number, as long as the same number is used within the `login()` method and the `onActivityResult()` method.</span></span>  <span data-ttu-id="06172-406">Als u de clientcode abstracte in een service-adapter (zoals eerder is weergegeven), moet u de juiste methoden aanroepen op de adapter van de service.</span><span class="sxs-lookup"><span data-stu-id="06172-406">If you abstract the client code into a service adapter (as shown earlier), you should call the appropriate methods on the service adapter.</span></span>

<span data-ttu-id="06172-407">Ook moet u het project voor customtabs configureren.</span><span class="sxs-lookup"><span data-stu-id="06172-407">You also need to configure the project for customtabs.</span></span>  <span data-ttu-id="06172-408">Eerst een Omleidings-URL opgeven.</span><span class="sxs-lookup"><span data-stu-id="06172-408">First specify a redirect-URL.</span></span>  <span data-ttu-id="06172-409">Voeg het volgende codefragment aan `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="06172-409">Add the following snippet to `AndroidManifest.xml`:</span></span>

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

<span data-ttu-id="06172-410">Voeg de **redirectUriScheme** naar de `build.gradle` bestand voor uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="06172-410">Add the **redirectUriScheme** to the `build.gradle` file for your application:</span></span>

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

<span data-ttu-id="06172-411">Voeg `com.android.support:customtabs:23.0.1` aan de lijst met afhankelijkheden in de `build.gradle` bestand:</span><span class="sxs-lookup"><span data-stu-id="06172-411">Finally, add `com.android.support:customtabs:23.0.1` to the dependencies list in the `build.gradle` file:</span></span>

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

<span data-ttu-id="06172-412">Verkrijgen van de ID van de aangemelde gebruiker van een **MobileServiceUser** met behulp van de **getUserId** methode.</span><span class="sxs-lookup"><span data-stu-id="06172-412">Obtain the ID of the logged-in user from a **MobileServiceUser** using the **getUserId** method.</span></span> <span data-ttu-id="06172-413">Zie voor een voorbeeld van het gebruik van Futures aanroepen van de asynchrone aanmelding API's [aan de slag met verificatie].</span><span class="sxs-lookup"><span data-stu-id="06172-413">For an example of how to use Futures to call the asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="06172-414">Het URL-schema vermeld is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="06172-414">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="06172-415">Zorg ervoor dat alle instanties van `{url_scheme_of_you_app}` hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="06172-415">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="06172-416"><a name="caching"></a>Verificatietokens cache</span><span class="sxs-lookup"><span data-stu-id="06172-416"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="06172-417">Verificatietokens caching, moet u de gebruikers-ID en -verificatietoken lokaal opslaan op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="06172-417">Caching authentication tokens requires you to store the User ID and authentication token locally on the device.</span></span> <span data-ttu-id="06172-418">De volgende keer dat de app wordt gestart, controleren van de cache, en als deze waarden aanwezig zijn, kunt u het logboek in procedure overslaan en de client bij deze gegevens rehydrate.</span><span class="sxs-lookup"><span data-stu-id="06172-418">The next time the app starts, you check the cache, and if these values are present, you can skip the log in procedure and rehydrate the client with this data.</span></span> <span data-ttu-id="06172-419">Deze gegevens is echter gevoelige en moeten worden opgeslagen voor de veiligheid versleuteld als de telefoon wordt gestolen.</span><span class="sxs-lookup"><span data-stu-id="06172-419">However this data is sensitive, and it should be stored encrypted for safety in case the phone gets stolen.</span></span>  <span data-ttu-id="06172-420">Ziet u een compleet voorbeeld van hoe u aan de cache verificatietokens in [verificatiesectie tokens in de Cache][7].</span><span class="sxs-lookup"><span data-stu-id="06172-420">You can see a complete example of how to cache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="06172-421">Wanneer u een verlopen token gebruiken probeert, krijgt u een *401-niet-geautoriseerde* antwoord.</span><span class="sxs-lookup"><span data-stu-id="06172-421">When you try to use an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="06172-422">U kunt met behulp van filters verificatiefouten verwerken.</span><span class="sxs-lookup"><span data-stu-id="06172-422">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="06172-423">Filters onderscheppen aanvragen voor de App Service-back-end.</span><span class="sxs-lookup"><span data-stu-id="06172-423">Filters intercept requests to the App Service backend.</span></span> <span data-ttu-id="06172-424">De filtercode test van het antwoord op een 401, activeert het proces aanmelden en hervat vervolgens de aanvraag die de 401 gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="06172-424">The filter code tests the response for a 401, triggers the sign-in process, and then resumes the request that generated the 401.</span></span>

### <span data-ttu-id="06172-425"><a name="refresh"></a>Vernieuwen van Tokens gebruiken</span><span class="sxs-lookup"><span data-stu-id="06172-425"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="06172-426">Het token dat is geretourneerd door de Azure App Service-verificatie en autorisatie heeft een gedefinieerde levensduur van een uur.</span><span class="sxs-lookup"><span data-stu-id="06172-426">The token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="06172-427">Na deze periode, moet u de gebruiker te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="06172-427">After this period, you must reauthenticate the user.</span></span>  <span data-ttu-id="06172-428">Als u een lange levensduur token die u hebt ontvangen via client-flow-verificatie gebruikt, kunt u andere referenties met Azure App Service-verificatie en autorisatie met hetzelfde token.</span><span class="sxs-lookup"><span data-stu-id="06172-428">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using the same token.</span></span>  <span data-ttu-id="06172-429">Een andere Azure App Service-token wordt gegenereerd met een nieuwe levensduur.</span><span class="sxs-lookup"><span data-stu-id="06172-429">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="06172-430">U kunt ook de provider voor het gebruik van Tokens vernieuwen registreren.</span><span class="sxs-lookup"><span data-stu-id="06172-430">You can also register the provider to use Refresh Tokens.</span></span>  <span data-ttu-id="06172-431">Een Token voor vernieuwen is niet altijd beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="06172-431">A Refresh Token is not always available.</span></span>  <span data-ttu-id="06172-432">Er is aanvullende configuratie vereist:</span><span class="sxs-lookup"><span data-stu-id="06172-432">Additional configuration is required:</span></span>

* <span data-ttu-id="06172-433">Voor **Azure Active Directory**, een clientgeheim configureren voor Azure Active Directory-App.</span><span class="sxs-lookup"><span data-stu-id="06172-433">For **Azure Active Directory**, configure a client secret for the Azure Active Directory App.</span></span>  <span data-ttu-id="06172-434">Geef het clientgeheim in de Azure App Service bij het configureren van Azure Active Directory-verificatie.</span><span class="sxs-lookup"><span data-stu-id="06172-434">Specify the client secret in the Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="06172-435">Bij het aanroepen van `.login()`, doorgeven `response_type=code id_token` als een parameter:</span><span class="sxs-lookup"><span data-stu-id="06172-435">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="06172-436">Voor **Google**, geven de `access_type=offline` als een parameter:</span><span class="sxs-lookup"><span data-stu-id="06172-436">For **Google**, pass the `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="06172-437">Voor **Microsoft-Account**, selecteer de `wl.offline_access` bereik.</span><span class="sxs-lookup"><span data-stu-id="06172-437">For **Microsoft Account**, select the `wl.offline_access` scope.</span></span>

<span data-ttu-id="06172-438">Als u wilt vernieuwen van een token, aanroepen `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="06172-438">To refresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="06172-439">Als een best practice een filter maken waarmee een 401-respons van de server detecteert en probeert het gebruikerstoken te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="06172-439">As a best practice, create a filter that detects a 401 response from the server and tries to refresh the user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="06172-440">Meld u aan met Client-flow-verificatie</span><span class="sxs-lookup"><span data-stu-id="06172-440">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="06172-441">Het algemene proces voor aangemeld met client-flow-verificatie is als volgt:</span><span class="sxs-lookup"><span data-stu-id="06172-441">The general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="06172-442">Azure App Service-verificatie en autorisatie configureert als server-flow-verificatie.</span><span class="sxs-lookup"><span data-stu-id="06172-442">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="06172-443">De verificatieprovider SDK voor verificatie voor het produceren van een toegangstoken integreren.</span><span class="sxs-lookup"><span data-stu-id="06172-443">Integrate the authentication provider SDK for authentication to produce an access token.</span></span>
* <span data-ttu-id="06172-444">Roep de `.login()` methode als volgt:</span><span class="sxs-lookup"><span data-stu-id="06172-444">Call the `.login()` method as follows:</span></span>

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

<span data-ttu-id="06172-445">Vervang de `onSuccess()` methode met wat u code wilt gebruiken op een geslaagde aanmelding.</span><span class="sxs-lookup"><span data-stu-id="06172-445">Replace the `onSuccess()` method with whatever code you wish to use on a successful login.</span></span>  <span data-ttu-id="06172-446">De `{provider}` tekenreeks is een geldige provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, of **twitter**.</span><span class="sxs-lookup"><span data-stu-id="06172-446">The `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="06172-447">Als u aangepaste verificatie hebt geïmplementeerd, kunt u ook de code van de provider aangepaste verificatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="06172-447">If you have implemented custom authentication, then you can also use the custom authentication provider tag.</span></span>

### <span data-ttu-id="06172-448"><a name="adal"></a>Verificatie van gebruikers met de Active Directory Authentication Library (ADAL)</span><span class="sxs-lookup"><span data-stu-id="06172-448"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="06172-449">U kunt de Active Directory Authentication Library (ADAL) gebruiken voor het ondertekenen van gebruikers in uw toepassing met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="06172-449">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="06172-450">Met behulp van de aanmelding van een client stroom is het handiger voor het gebruik van de `loginAsync()` methoden zoals deze biedt een meer systeemeigen UX idee en kunt u extra aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="06172-450">Using a client flow login is often preferable to using the `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="06172-451">Uw mobiele app back-end voor aanmelding bij de AAD instellen door de [App Service configureren voor Active Directory-aanmelding] [ 22] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="06172-451">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="06172-452">Zorg ervoor dat de optionele stap voor het registreren van een systeemeigen clienttoepassing van voltooien.</span><span class="sxs-lookup"><span data-stu-id="06172-452">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="06172-453">ADAL installeren door uw build.gradle-bestand om op te nemen van de volgende definities te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="06172-453">Install ADAL by modifying your build.gradle file to include the following definitions:</span></span>

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

1. <span data-ttu-id="06172-454">De volgende code toevoegen aan uw toepassing, waardoor de volgende vervangingen:</span><span class="sxs-lookup"><span data-stu-id="06172-454">Add the following code to your application, making the following replacements:</span></span>

* <span data-ttu-id="06172-455">Vervang **INSERT-instantie-hier** met de naam van de tenant waarin u uw toepassing hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="06172-455">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="06172-456">De indeling moet https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="06172-456">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="06172-457">Vervang **INSERT RESOURCE-ID hier** met de client-ID voor uw back-end voor de mobiele app.</span><span class="sxs-lookup"><span data-stu-id="06172-457">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="06172-458">U vindt de client-ID van de **Geavanceerd** tabblad onder **Azure Active Directory-instellingen** in de portal.</span><span class="sxs-lookup"><span data-stu-id="06172-458">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
* <span data-ttu-id="06172-459">Vervang **INSERT-CLIENT-ID-hier** met de client-ID die u hebt gekopieerd uit de native client-toepassing.</span><span class="sxs-lookup"><span data-stu-id="06172-459">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
* <span data-ttu-id="06172-460">Vervang **INSERT-OMLEIDINGS-URI-hier** aan uw site */.auth/login/done* eindpunt, met behulp van het HTTPS-schema.</span><span class="sxs-lookup"><span data-stu-id="06172-460">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="06172-461">Deze waarde moet er ongeveer als *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="06172-461">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

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

## <span data-ttu-id="06172-462"><a name="filters"></a>De Client-servercommunicatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="06172-462"><a name="filters"></a>Adjust the Client-Server Communication</span></span>

<span data-ttu-id="06172-463">De clientverbinding is normaal gesproken een eenvoudige HTTP-verbinding met de onderliggende HTTP-bibliotheek geleverd met de Android-SDK.</span><span class="sxs-lookup"><span data-stu-id="06172-463">The Client connection is normally a basic HTTP connection using the underlying HTTP library supplied with the Android SDK.</span></span>  <span data-ttu-id="06172-464">Er zijn diverse redenen waarom u deze instelling wijzigen zou willen:</span><span class="sxs-lookup"><span data-stu-id="06172-464">There are several reasons why you would want to change that:</span></span>

* <span data-ttu-id="06172-465">Wilt u een alternatieve HTTP-bibliotheek gebruiken om aan te passen time-outs.</span><span class="sxs-lookup"><span data-stu-id="06172-465">You wish to use an alternate HTTP library to adjust timeouts.</span></span>
* <span data-ttu-id="06172-466">Wilt u een voortgangsbalk bieden.</span><span class="sxs-lookup"><span data-stu-id="06172-466">You wish to provide a progress bar.</span></span>
* <span data-ttu-id="06172-467">U wilt toevoegen van een aangepaste header ter ondersteuning van API management-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="06172-467">You wish to add a custom header to support API management functionality.</span></span>
* <span data-ttu-id="06172-468">Wilt u een mislukte reactie intercept zodat u herauthenticatie kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="06172-468">You wish to intercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="06172-469">Wilt u back-end-aanvragen met een analytics-service aanmelden.</span><span class="sxs-lookup"><span data-stu-id="06172-469">You wish to log backend requests to an analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="06172-470">Met behulp van een andere HTTP-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="06172-470">Using an alternate HTTP Library</span></span>

<span data-ttu-id="06172-471">Roep de `.setAndroidHttpClientFactory()` methode onmiddellijk na het maken van uw client-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="06172-471">Call the `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="06172-472">Als u bijvoorbeeld de verbindingstime-out ingesteld op 60 seconden (in plaats van de standaard 10 seconden):</span><span class="sxs-lookup"><span data-stu-id="06172-472">For example, to set the connection timeout to 60 seconds (instead of the default 10 seconds):</span></span>

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

### <a name="implement-a-progress-filter"></a><span data-ttu-id="06172-473">Een Filter voortgang implementeren</span><span class="sxs-lookup"><span data-stu-id="06172-473">Implement a Progress Filter</span></span>

<span data-ttu-id="06172-474">U kunt een intercept van elke aanvraag implementeren door het implementeren van een `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="06172-474">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="06172-475">Bijvoorbeeld updates de volgende van een vooraf gemaakte voortgangsbalk:</span><span class="sxs-lookup"><span data-stu-id="06172-475">For example, the following updates a pre-created progress bar:</span></span>

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

<span data-ttu-id="06172-476">U kunt dit filter koppelen aan de client als volgt:</span><span class="sxs-lookup"><span data-stu-id="06172-476">You can attach this filter to the client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="06172-477">Aanvraagheaders aanpassen</span><span class="sxs-lookup"><span data-stu-id="06172-477">Customize Request Headers</span></span>

<span data-ttu-id="06172-478">Gebruik de volgende `ServiceFilter` en koppelt u het filter op dezelfde manier als de `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="06172-478">Use the following `ServiceFilter` and attach the filter in the same way as the `ProgressFilter`:</span></span>

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

### <span data-ttu-id="06172-479"><a name="conversions"></a>Automatische serialisatie configureren</span><span class="sxs-lookup"><span data-stu-id="06172-479"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="06172-480">U kunt opgeven dat een strategie voor een conversie die wordt toegepast op elke kolom met de [gson] [ 3] API.</span><span class="sxs-lookup"><span data-stu-id="06172-480">You can specify a conversion strategy that applies to every column by using the [gson][3] API.</span></span> <span data-ttu-id="06172-481">Maakt gebruik van de Android-clientbibliotheek [gson] [ 3] achter de schermen Java om objecten te serialiseren naar JSON-gegevens voordat de gegevens worden verzonden naar Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="06172-481">The Android client library uses [gson][3] behind the scenes to serialize Java objects to JSON data before the data is sent to Azure App Service.</span></span>  <span data-ttu-id="06172-482">De volgende code gebruikt de **setFieldNamingStrategy()** methode voor het instellen van de strategie.</span><span class="sxs-lookup"><span data-stu-id="06172-482">The following code uses the **setFieldNamingStrategy()** method to set the strategy.</span></span> <span data-ttu-id="06172-483">In dit voorbeeld wordt het eerste teken (een ' m'), verwijderen en vervolgens kleine het volgende teken, voor elke veldnaam.</span><span class="sxs-lookup"><span data-stu-id="06172-483">This example will delete the initial character (an "m"), and then lower-case the next character, for every field name.</span></span> <span data-ttu-id="06172-484">Bijvoorbeeld, zou het veranderen 'mId' in 'id'.</span><span class="sxs-lookup"><span data-stu-id="06172-484">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="06172-485">Een strategie voor conversie zodat de noodzaak van implementeren `SerializedName()` aantekeningen in de meeste velden.</span><span class="sxs-lookup"><span data-stu-id="06172-485">Implement a conversion strategy to reduce the need for `SerializedName()` annotations on most fields.</span></span>

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

<span data-ttu-id="06172-486">Deze code moet worden uitgevoerd voordat het maken van een mobiele clients verwijzing met de **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="06172-486">This code must be executed before creating a mobile client reference using the **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
<span data-ttu-id="06172-487">[aan de slag met verificatie]: app-service-mobile-android-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="06172-487">[Get started with authentication]: app-service-mobile-android-get-started-users.md</span></span>
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
