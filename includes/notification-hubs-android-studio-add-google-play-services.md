1. <span data-ttu-id="bbe50-101">Open Hallo Android SDK Manager door te klikken op Hallo-pictogram op de werkbalk Hallo van Android Studio of door te klikken op **extra** -> **Android** -> **SDK Manager**Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="bbe50-101">Open hello Android SDK Manager by clicking hello icon on hello toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on hello menu.</span></span> <span data-ttu-id="bbe50-102">De doelversie Hallo Hallo Android SDK die wordt gebruikt in uw project vinden, opent u deze door te klikken op **Pakketgegevens weergeven**, en kies **Google APIs**, als deze nog niet is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bbe50-102">Locate hello target version of hello Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="bbe50-103">Klik op Hallo **SDK-Tools** tabblad. Als u Google Play Service nog niet hebt geïnstalleerd, klikt u op **Google Play Services** zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bbe50-103">Click hello **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="bbe50-104">Klik vervolgens op **toepassen** tooinstall.</span><span class="sxs-lookup"><span data-stu-id="bbe50-104">Then click **Apply** tooinstall.</span></span> 
   
    <span data-ttu-id="bbe50-105">Houd er rekening mee Hallo SDK-pad voor gebruik in een latere stap.</span><span class="sxs-lookup"><span data-stu-id="bbe50-105">Note hello SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="bbe50-106">Open Hallo **build.gradle** in Hallo app map.</span><span class="sxs-lookup"><span data-stu-id="bbe50-106">Open hello **build.gradle** file in hello app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="bbe50-107">Voeg deze regel toe onder *Afhankelijkheden*:</span><span class="sxs-lookup"><span data-stu-id="bbe50-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="bbe50-108">Klik op Hallo **Project met Gradle-bestanden** pictogram in het Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="bbe50-108">Click hello **Sync Project with Gradle Files** icon in hello tool bar.</span></span>
6. <span data-ttu-id="bbe50-109">Open **AndroidManifest.xml** en voeg deze code toohello *toepassing* label.</span><span class="sxs-lookup"><span data-stu-id="bbe50-109">Open **AndroidManifest.xml** and add this tag toohello *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

