### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="f1dc6-101">Verleen Mobile Engagement toegang tooyour GCM-API-sleutel</span><span class="sxs-lookup"><span data-stu-id="f1dc6-101">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="f1dc6-102">tooallow Mobile Engagement toosend pushmeldingen namens u, moet u deze toegang hebben tot tooyour API-sleutel toogrant.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-102">tooallow Mobile Engagement toosend push notifications on your behalf, you need toogrant it access tooyour API Key.</span></span> <span data-ttu-id="f1dc6-103">Dit wordt gedaan door te configureren en u uw sleutel in de Mobile Engagement-portal Hallo invoert.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-103">This is done by configuring and entering your key into hello Mobile Engagement portal.</span></span>

1. <span data-ttu-id="f1dc6-104">Zorg ervoor dat Hallo-App wordt gebruikt voor dit project en klik vervolgens op Hallo van de klassieke Azure-Portal **Engage** knop Hallo onderaan:</span><span class="sxs-lookup"><span data-stu-id="f1dc6-104">From your Azure Classic Portal, ensure you're in hello app we're using for this project, and then click hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="f1dc6-105">Klik vervolgens op Hallo **instellingen** -> **Native Pushbericht** sectie tooenter uw GCM-sleutel:</span><span class="sxs-lookup"><span data-stu-id="f1dc6-105">Then click hello **Settings** -> **Native Push** section tooenter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="f1dc6-106">Klik op Hallo **bewerken** pictogram vóór **API-sleutel** in Hallo **GCM-instellingen** sectie zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="f1dc6-106">Click hello **Edit** icon in front of **API Key** in hello **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="f1dc6-107">In het pop-upvenster Hallo plakken Hallo GCM-serversleutel die u eerder hebt verkregen en klik vervolgens op **Ok**.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-107">In hello pop-up, paste hello GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="f1dc6-108"><a id="send"></a>Een melding tooyour app verzenden</span><span class="sxs-lookup"><span data-stu-id="f1dc6-108"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="f1dc6-109">We gaan nu een eenvoudige pushmeldingcampagne die een push notification tooour-app stuurt maken.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-109">We will now create a simple push notification campaign that sends a push notification tooour app.</span></span>

1. <span data-ttu-id="f1dc6-110">Navigeer toohello **bereiken** tabblad in uw Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-110">Navigate toohello **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="f1dc6-111">Klik op **nieuwe aankondiging** toocreate uw pushmeldingcampagne.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-111">Click **New announcement** toocreate your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="f1dc6-112">Instellen van de eerste veld Hallo van uw campagne in via Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f1dc6-112">Set up hello first field of your campaign through hello following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="f1dc6-113">a.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-113">a.</span></span> <span data-ttu-id="f1dc6-114">Geef uw campagne een naam.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-114">Name your campaign.</span></span>
   
    <span data-ttu-id="f1dc6-115">b.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-115">b.</span></span> <span data-ttu-id="f1dc6-116">Selecteer Hallo **bezorgingstype** als *Systeemmelding -> eenvoudig*: dit is Hallo eenvoudige Android-pushmeldingentype met een titel en een korte tekstregel.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-116">Select hello **Delivery type** as *System notification -> Simple*: This is hello simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="f1dc6-117">c.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-117">c.</span></span> <span data-ttu-id="f1dc6-118">Selecteer **leveringstijd** als *elk gewenst moment* tooallow Hallo app tooreceive een melding of Hallo-app wordt gestart of niet.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-118">Select **Delivery time** as *Any time* tooallow hello app tooreceive a notification whether hello app is started or not.</span></span>
   
    <span data-ttu-id="f1dc6-119">d.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-119">d.</span></span> <span data-ttu-id="f1dc6-120">In Hallo melding tekst type Hallo **titel** die worden weergegeven in vet weergegeven in het Hallo-push.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-120">In hello notification text type hello **Title** which will be in bold in hello push.</span></span>
   
    <span data-ttu-id="f1dc6-121">e.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-121">e.</span></span> <span data-ttu-id="f1dc6-122">Typ vervolgens uw **bericht**</span><span class="sxs-lookup"><span data-stu-id="f1dc6-122">Then type your **Message**</span></span>
4. <span data-ttu-id="f1dc6-123">Schuif omlaag en in Hallo **inhoud** sectie **alleen melding**.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-123">Scroll down, and in hello **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="f1dc6-124">Instelling Hallo meest elementaire campagne mogelijk kunt u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-124">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="f1dc6-125">Nu Blader nogmaals naar beneden en klik op Hallo **maken** knop toosave uw campagne.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-125">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
6. <span data-ttu-id="f1dc6-126">Laatste stap: klik op **activeren** tooactivate uw campagne toosend-pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="f1dc6-126">Last step: click **Activate** tooactivate your campaign toosend push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

