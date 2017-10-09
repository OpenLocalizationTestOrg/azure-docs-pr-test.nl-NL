<span data-ttu-id="ee42d-101">tooenable profiel bewerken op uw toepassing, moet u toocreate een profiel te bewerken van beleid.</span><span class="sxs-lookup"><span data-stu-id="ee42d-101">tooenable profile editing on your application, you will need toocreate a profile editing policy.</span></span> <span data-ttu-id="ee42d-102">Dit beleid beschrijft Hallo ervaringen die consumenten doorlopen tijdens profiel bewerken en het Hallo-inhoud van de tokens die de toepassing hello is gelukt ontvangt.</span><span class="sxs-lookup"><span data-stu-id="ee42d-102">This policy describes hello experiences that consumers will go through during profile editing and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="ee42d-103">Hallo beleidsregels sectie van de instellingen en selecteer **profiel bewerken van beleid** en klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ee42d-103">In hello policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Selecteer het profiel bewerken van beleid en klik op de knop toevoegen Hallo](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="ee42d-105">Voer een beleid **naam** voor uw toepassing tooreference.</span><span class="sxs-lookup"><span data-stu-id="ee42d-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="ee42d-106">Geef bijvoorbeeld `SiPe` op.</span><span class="sxs-lookup"><span data-stu-id="ee42d-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="ee42d-107">Selecteer **Id-providers** en schakel **Aanmelden met lokaal account** in.</span><span class="sxs-lookup"><span data-stu-id="ee42d-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="ee42d-108">U kunt er ook voor kiezen om sociale id-providers te selecteren als dit al is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ee42d-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="ee42d-109">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee42d-109">Click **OK**.</span></span>

![Lokale Account aanmelding als een id-provider en klik op de knop OK Hallo](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="ee42d-111">Selecteer **Profielkenmerken**.</span><span class="sxs-lookup"><span data-stu-id="ee42d-111">Select **Profile attributes**.</span></span> <span data-ttu-id="ee42d-112">Kies kenmerken Hallo consumer kunt bekijken en bewerken in het profiel.</span><span class="sxs-lookup"><span data-stu-id="ee42d-112">Choose attributes hello consumer can view and edit in their profile.</span></span> <span data-ttu-id="ee42d-113">Schakel bijvoorbeeld **Land/regio**, **Weergavenaam** en **Postcode** in.</span><span class="sxs-lookup"><span data-stu-id="ee42d-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="ee42d-114">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee42d-114">Click **OK**.</span></span>

![Selecteer enkele kenmerken en klik op OK Hallo](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="ee42d-116">Selecteer **Toepassingsclaims**.</span><span class="sxs-lookup"><span data-stu-id="ee42d-116">Select **Application claims**.</span></span> <span data-ttu-id="ee42d-117">Kies de claims die u opvragen in Hallo autorisatie tokens wilt verzonden back tooyour toepassing na een geslaagde profiel te bewerken.</span><span class="sxs-lookup"><span data-stu-id="ee42d-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful profile editing experience.</span></span> <span data-ttu-id="ee42d-118">Selecteer bijvoorbeeld **Weergavenaam**, **Postcode**.</span><span class="sxs-lookup"><span data-stu-id="ee42d-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Selecteer enkele toepassingsclaims en klik op de knop OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="ee42d-120">Klik op **maken** tooadd Hallo beleid.</span><span class="sxs-lookup"><span data-stu-id="ee42d-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="ee42d-121">Hallo-beleid wordt vermeld als **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="ee42d-121">hello policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="ee42d-122">Hallo **B2C_1_** voorvoegsel is de naam van de toegevoegde toohello.</span><span class="sxs-lookup"><span data-stu-id="ee42d-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="ee42d-123">Hallo beleid openen door te selecteren **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="ee42d-123">Open hello policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="ee42d-124">Hallo-instellingen die zijn opgegeven in de tabel Hallo controleren en klik vervolgens op **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="ee42d-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Selecteer het beleid en voer dit uit](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="ee42d-126">Instelling</span><span class="sxs-lookup"><span data-stu-id="ee42d-126">Setting</span></span>      | <span data-ttu-id="ee42d-127">Waarde</span><span class="sxs-lookup"><span data-stu-id="ee42d-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="ee42d-128">**Toepassingen**</span><span class="sxs-lookup"><span data-stu-id="ee42d-128">**Applications**</span></span> | <span data-ttu-id="ee42d-129">Contoso B2C-app</span><span class="sxs-lookup"><span data-stu-id="ee42d-129">Contoso B2C app</span></span> |
| <span data-ttu-id="ee42d-130">**Antwoord-URL selecteren**</span><span class="sxs-lookup"><span data-stu-id="ee42d-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="ee42d-131">Een nieuw browsertabblad geopend en kunt u controleren of Hallo profiel te bewerken consumer zoals geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ee42d-131">A new browser tab opens, and you can verify hello profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="ee42d-132">Het tooa minuut voor het maken van beleid in beslag en updates van kracht tootake.</span><span class="sxs-lookup"><span data-stu-id="ee42d-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>