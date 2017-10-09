---
title: aaaAzure AD v2 Android aan de slag - instellingen | Microsoft Docs
description: Hoe een Android-App kunt ophalen van een toegangstoken en Microsoft Graph API of API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Instellen van uw project

> Voorkeur toodownload dit voorbeeld Android Studio-project in plaats daarvan? [Downloaden van een project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) - en skip-toohello [configuratiestap](#create-an-application-express) tooconfigure Hallo codevoorbeeld voordat wordt uitgevoerd.


### <a name="create-a-new-project"></a>Een nieuw project maken 
1.  Open Android Studio, gaat u naar:`File` > `New` > `New Project`
2.  Naam van uw toepassing en klik op`Next`
3.  Zorg ervoor dat tooselect *API 21 of nieuwere (Android 5.0)* en klikt u op`Next`
4.  Laat `Empty Activity`, klikt u op `Next`, klikt u vervolgens`Finish`


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Hallo Microsoft Authentication Library (MSAL) tooyour project toevoegen
1.  In Android Studio, gaat u naar:`Gradle Scripts` > `build.gradle (Module: app)`
2.  Kopiëren en plakken Hallo hieronder de code onder `Dependencies`:

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a>Over dit pakket

Hallo pakket bovenstaande installeert Hallo Microsoft Authentication Library (MSAL). MSAL verwerkt ophalen, opslaan in cache en vernieuwen van gebruiker tokens die worden gebruikt tooaccess API's die zijn beveiligd door Azure Active Directory-v2-eindpunt.
<!--end-collapse-->

## <a name="create-your-applications-ui"></a>De gebruikersinterface van uw toepassing maken

1.  Open: `activity_main.xml` onder`res` > `layout`
2.  Indeling voor de activiteit van wijzigen Hallo van `android.support.constraint.ConstraintLayout` of een andere te`LinearLayout`
3.  Voeg `android:orientation="vertical"` eigenschap te`LinearLayout` knooppunt
4.  Kopiëren en plakken Hallo volgende code in Hallo `LinearLayout` vervangen de huidige inhoud Hallo-knooppunt:

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

