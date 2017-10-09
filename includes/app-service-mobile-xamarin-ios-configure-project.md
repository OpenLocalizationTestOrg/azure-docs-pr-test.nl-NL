#### <a name="configure-hello-ios-project-in-xamarin-studio"></a><span data-ttu-id="f457d-101">Hallo iOS-project in Xamarin Studio configureren</span><span class="sxs-lookup"><span data-stu-id="f457d-101">Configure hello iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="f457d-102">Open in Xamarin.Studio, **Info.plist**, en update Hallo **bundel-id** Hello bundel-ID die u eerder hebt gemaakt met uw nieuwe app-ID.</span><span class="sxs-lookup"><span data-stu-id="f457d-102">In Xamarin.Studio, open **Info.plist**, and update hello **Bundle Identifier** with hello bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="f457d-103">Schuif naar beneden te**Achtergrondmodi**.</span><span class="sxs-lookup"><span data-stu-id="f457d-103">Scroll down too**Background Modes**.</span></span> <span data-ttu-id="f457d-104">Selecteer Hallo **Enable Background Modes** vak en Hallo **Remote notifications** vak.</span><span class="sxs-lookup"><span data-stu-id="f457d-104">Select hello **Enable Background Modes** box and hello **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="f457d-105">Dubbelklik op het project in Hallo oplossing Configuratiescherm tooopen **Projectopties**.</span><span class="sxs-lookup"><span data-stu-id="f457d-105">Double-click your project in hello Solution Panel tooopen **Project Options**.</span></span>
4. <span data-ttu-id="f457d-106">Onder **bouwen**, kies **iOS bundel ondertekening**, en selecteer Hallo bijbehorende identiteit en inrichtingsprofiel u net hebt ingesteld voor dit project.</span><span class="sxs-lookup"><span data-stu-id="f457d-106">Under **Build**, choose **iOS Bundle Signing**, and select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="f457d-107">Dit zorgt ervoor dat project Hallo Hallo nieuwe profiel wordt gebruikt voor ondertekening van programmacode.</span><span class="sxs-lookup"><span data-stu-id="f457d-107">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="f457d-108">Hallo officiële Xamarin apparaten inrichten documentatie, Zie [Xamarin apparaten inrichten].</span><span class="sxs-lookup"><span data-stu-id="f457d-108">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-hello-ios-project-in-visual-studio"></a><span data-ttu-id="f457d-109">Hallo iOS-project in Visual Studio configureren</span><span class="sxs-lookup"><span data-stu-id="f457d-109">Configure hello iOS project in Visual Studio</span></span>
1. <span data-ttu-id="f457d-110">Met de rechtermuisknop op het Hallo-project in Visual Studio en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="f457d-110">In Visual Studio, right-click hello project, and then click **Properties**.</span></span>
2. <span data-ttu-id="f457d-111">Klik in de pagina eigenschappen van Hallo op Hallo **iOS-toepassing** tabblad en update Hallo **id** Hallo-id die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f457d-111">In hello properties pages, click hello **iOS Application** tab, and update hello **Identifier** with hello ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="f457d-112">In Hallo **iOS bundel ondertekening** tabblad Selecteer Hallo bijbehorende identiteit en de inrichting profiel u zojuist hebt ingesteld om voor dit project.</span><span class="sxs-lookup"><span data-stu-id="f457d-112">In hello **iOS Bundle Signing** tab, select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="f457d-113">Dit zorgt ervoor dat project Hallo Hallo nieuwe profiel wordt gebruikt voor ondertekening van programmacode.</span><span class="sxs-lookup"><span data-stu-id="f457d-113">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="f457d-114">Hallo officiële Xamarin apparaten inrichten documentatie, Zie [Xamarin apparaten inrichten].</span><span class="sxs-lookup"><span data-stu-id="f457d-114">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="f457d-115">Dubbelklik op Info.plist tooopen en schakelt u vervolgens **RemoteNotifications** onder **Achtergrondmodi**.</span><span class="sxs-lookup"><span data-stu-id="f457d-115">Double-click Info.plist tooopen it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

[Xamarin apparaten inrichten]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
