### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a><span data-ttu-id="8aaed-101">Verleen toegang tooyour Pushcertificaat tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8aaed-101">Grant access tooyour Push Certificate tooMobile Engagement</span></span>
<span data-ttu-id="8aaed-102">tooallow Mobile Engagement toosend Pushmeldingen namens u, moet u deze toegang hebben tot tooyour certificaat toogrant.</span><span class="sxs-lookup"><span data-stu-id="8aaed-102">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour certificate.</span></span> <span data-ttu-id="8aaed-103">Dit wordt gedaan door te configureren en uw certificaat voeren in Hallo Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="8aaed-103">This is done by configuring and entering your certificate into hello Mobile Engagement portal.</span></span> <span data-ttu-id="8aaed-104">Zorg dat u uw .p12-certificaat verkrijgt zoals uitgelegd in de [Apple-documentatie](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="8aaed-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="8aaed-105">Navigeer tooyour Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="8aaed-105">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="8aaed-106">Zorg ervoor dat u in de juiste Hallo bent en klik vervolgens op Hallo **Engage** knop Hallo onderaan:</span><span class="sxs-lookup"><span data-stu-id="8aaed-106">Ensure you're in hello correct and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="8aaed-107">Klik op Hallo **instellingen** pagina in de Engagement-Portal.</span><span class="sxs-lookup"><span data-stu-id="8aaed-107">Click on hello **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="8aaed-108">Klik op Hallo **Native Pushbericht** sectie tooupload uw p12-certificaat:</span><span class="sxs-lookup"><span data-stu-id="8aaed-108">From there click on hello **Native Push** section tooupload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="8aaed-109">Selecteer uw p12, upload het en typ uw wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="8aaed-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="8aaed-110"><a id="send"></a>Een melding tooyour app verzenden</span><span class="sxs-lookup"><span data-stu-id="8aaed-110"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="8aaed-111">We gaan nu een eenvoudige pushmeldingcampagne die een push-tooour-app stuurt maken:</span><span class="sxs-lookup"><span data-stu-id="8aaed-111">We will now create a simple Push Notification campaign that will send a push tooour app:</span></span>

1. <span data-ttu-id="8aaed-112">Navigeer toohello **bereiken** tabblad in uw Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="8aaed-112">Navigate toohello **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="8aaed-113">Klik op **nieuwe aankondiging** toocreate uw pushcampagne</span><span class="sxs-lookup"><span data-stu-id="8aaed-113">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="8aaed-114">Hallo eerste velden van uw campagne instellen:</span><span class="sxs-lookup"><span data-stu-id="8aaed-114">Setup hello first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="8aaed-115">Geef uw campagne een **naam**.</span><span class="sxs-lookup"><span data-stu-id="8aaed-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="8aaed-116">Selecteer Hallo **leveringstijd** als **alleen buiten app**: dit is Hallo eenvoudig Apple-pushmeldingentype met een beetje tekst.</span><span class="sxs-lookup"><span data-stu-id="8aaed-116">Select hello **Delivery time** as **Out of app only**: this is hello simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="8aaed-117">Typ in de berichttekst hello, eerste Hallo **titel** die de eerste regel Hallo in Hallo push worden.</span><span class="sxs-lookup"><span data-stu-id="8aaed-117">In hello notification text, type first hello **Title** which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="8aaed-118">Typ vervolgens uw **bericht** die de tweede regel Hallo zijn</span><span class="sxs-lookup"><span data-stu-id="8aaed-118">Then type your **Message** which will be hello second line</span></span>
4. <span data-ttu-id="8aaed-119">Schuif naar beneden en selecteer in de Hallo sectie inhoud **alleen melding**</span><span class="sxs-lookup"><span data-stu-id="8aaed-119">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="8aaed-120">Instelling Hallo meest elementaire campagne is voltooid.</span><span class="sxs-lookup"><span data-stu-id="8aaed-120">You're done setting hello most basic campaign.</span></span> <span data-ttu-id="8aaed-121">Nu Schuif naar beneden en klik op **maken** knop toosave uw pushmeldingcampagne.</span><span class="sxs-lookup"><span data-stu-id="8aaed-121">Now scroll down and click on **Create** button toosave your push notification campaign.</span></span> 
6. <span data-ttu-id="8aaed-122">Klik ten slotte op **activeren** toosend push-melding.</span><span class="sxs-lookup"><span data-stu-id="8aaed-122">Finally - click on **Activate** toosend push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="8aaed-123">U ontvangt Hallo melding op uw iOS-apparaat in het meldingencentrum Hallo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="8aaed-123">You will be able receive hello notification on your iOS device in hello notification center like hello following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="8aaed-124">Als u een Apple Watch gekoppeld aan dit iOS-apparaat hebt vervolgens ziet u Hallo melding op uw Apple Watch:</span><span class="sxs-lookup"><span data-stu-id="8aaed-124">If you have an Apple Watch paired with this iOS device then you will see hello notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

