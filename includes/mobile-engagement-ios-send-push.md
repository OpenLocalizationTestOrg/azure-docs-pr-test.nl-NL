### <a name="grant-access-to-your-push-certificate-to-mobile-engagement"></a><span data-ttu-id="eb5f1-101">Uw pushcertificaat toegang verlenen tot Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="eb5f1-101">Grant access to your Push Certificate to Mobile Engagement</span></span>
<span data-ttu-id="eb5f1-102">Om Mobile Engagement namens u pushmeldingen te laten verzenden, moet u het toegang geven tot uw certificaat.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-102">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your certificate.</span></span> <span data-ttu-id="eb5f1-103">Dit kunt u doen door uw certificaat te configureren en in te voeren in de Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-103">This is done by configuring and entering your certificate into the Mobile Engagement portal.</span></span> <span data-ttu-id="eb5f1-104">Zorg dat u uw .p12-certificaat verkrijgt zoals uitgelegd in de [Apple-documentatie](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="eb5f1-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="eb5f1-105">Navigeer naar uw Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-105">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="eb5f1-106">Zorg ervoor dat u zich op de juiste locatie bevindt en klik vervolgens op de knop **Engage** onderaan:</span><span class="sxs-lookup"><span data-stu-id="eb5f1-106">Ensure you're in the correct and then click on the **Engage** button at the bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="eb5f1-107">Klik op de pagina **Instellingen** in de Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-107">Click on the **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="eb5f1-108">Klik daarna op de sectie **Native pushbericht** om uw p12-certificaat te uploaden:</span><span class="sxs-lookup"><span data-stu-id="eb5f1-108">From there click on the **Native Push** section to upload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="eb5f1-109">Selecteer uw p12, upload het en typ uw wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="eb5f1-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="eb5f1-110"><a id="send"></a>Een melding verzenden naar uw app</span><span class="sxs-lookup"><span data-stu-id="eb5f1-110"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="eb5f1-111">We gaan nu een eenvoudige pushmeldingcampagne maken waarbij een pushmelding wordt verzonden naar de app:</span><span class="sxs-lookup"><span data-stu-id="eb5f1-111">We will now create a simple Push Notification campaign that will send a push to our app:</span></span>

1. <span data-ttu-id="eb5f1-112">Navigeer naar het tabblad **Reach** in uw Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-112">Navigate to the **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="eb5f1-113">Klik op **Nieuwe aankondiging** om uw pushcampagne te maken.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-113">Click **New Announcement** to create your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="eb5f1-114">Stel de eerste velden van uw campagne in:</span><span class="sxs-lookup"><span data-stu-id="eb5f1-114">Setup the first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="eb5f1-115">Geef uw campagne een **naam**.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="eb5f1-116">Selecteer als **Leveringstijd** **Alleen buiten app**: dit is het eenvoudig Apple-pushmeldingentype met een beetje tekst.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-116">Select the **Delivery time** as **Out of app only**: this is the simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="eb5f1-117">Typ in de meldingentekst eerst de **Titel** die als eerste regel in de pushmelding wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-117">In the notification text, type first the **Title** which will be the first line in the push.</span></span>
   * <span data-ttu-id="eb5f1-118">Typ vervolgens uw **bericht**. Dit wordt op de tweede regel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-118">Then type your **Message** which will be the second line</span></span>
4. <span data-ttu-id="eb5f1-119">Blader naar beneden en selecteer in de sectie Inhoud **Alleen melding**.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-119">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="eb5f1-120">U hebt nu de meest elementaire campagne gemaakt.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-120">You're done setting the most basic campaign.</span></span> <span data-ttu-id="eb5f1-121">Schuif nu naar beneden en klik op de knop **Maken** om uw pushmeldingcampagne op te slaan.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-121">Now scroll down and click on **Create** button to save your push notification campaign.</span></span> 
6. <span data-ttu-id="eb5f1-122">Klik ten slotte op **Activeren** om de pushmelding te verzenden.</span><span class="sxs-lookup"><span data-stu-id="eb5f1-122">Finally - click on **Activate** to send push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="eb5f1-123">U kunt de melding in het meldingencentrum op uw iOS-apparaat als volgt ontvangen:</span><span class="sxs-lookup"><span data-stu-id="eb5f1-123">You will be able receive the notification on your iOS device in the notification center like the following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="eb5f1-124">Als u een Apple Watch hebt die is gekoppeld aan dit iOS-apparaat, ziet u de melding op uw Apple Watch:</span><span class="sxs-lookup"><span data-stu-id="eb5f1-124">If you have an Apple Watch paired with this iOS device then you will see the notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

