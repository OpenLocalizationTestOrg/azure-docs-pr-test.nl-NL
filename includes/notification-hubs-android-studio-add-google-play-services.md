1. <span data-ttu-id="6adc9-101">Open Android SDK Manager door te klikken op het pictogram op de werkbalk van Android Studio of door in het menu te klikken op **Extra** -> **Android** -> **SDK Manager**.</span><span class="sxs-lookup"><span data-stu-id="6adc9-101">Open the Android SDK Manager by clicking the icon on the toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on the menu.</span></span> <span data-ttu-id="6adc9-102">Zoek naar de doelversie van de Android SDK die in uw project wordt gebruikt, open deze door te klikken op **Pakketgegevens weergeven** en kies **Google API's**, als deze nog niet is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6adc9-102">Locate the target version of the Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="6adc9-103">Klik op het tabblad **SDK-hulpprogramma's** .</span><span class="sxs-lookup"><span data-stu-id="6adc9-103">Click the **SDK Tools** tab.</span></span> <span data-ttu-id="6adc9-104">Als u Google Play Service nog niet hebt geïnstalleerd, klikt u op **Google Play Services** zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6adc9-104">If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="6adc9-105">Klik vervolgens op **Toepassen** om met de installatie te beginnen.</span><span class="sxs-lookup"><span data-stu-id="6adc9-105">Then click **Apply** to install.</span></span> 
   
    <span data-ttu-id="6adc9-106">Noteer het SDK-pad om het in een later stadium te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6adc9-106">Note the SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="6adc9-107">Open het bestand **build.gradle** in de app-map.</span><span class="sxs-lookup"><span data-stu-id="6adc9-107">Open the **build.gradle** file in the app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="6adc9-108">Voeg deze regel toe onder *Afhankelijkheden*:</span><span class="sxs-lookup"><span data-stu-id="6adc9-108">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="6adc9-109">Klik op het pictogram **Project met Gradle-bestanden synchroniseren** in de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="6adc9-109">Click the **Sync Project with Gradle Files** icon in the tool bar.</span></span>
6. <span data-ttu-id="6adc9-110">Open **AndroidManifest.xml** en voeg dit label toe aan het label *toepassing*.</span><span class="sxs-lookup"><span data-stu-id="6adc9-110">Open **AndroidManifest.xml** and add this tag to the *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

