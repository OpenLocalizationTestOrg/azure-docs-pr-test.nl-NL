<span data-ttu-id="9f275-101">tooenable aanmelden op uw toepassing, moet u toocreate een aanmeldingspagina beleid.</span><span class="sxs-lookup"><span data-stu-id="9f275-101">tooenable sign-in on your application, you will need toocreate a sign-in policy.</span></span> <span data-ttu-id="9f275-102">Dit beleid wordt Hallo ervaringen die consumenten doorlopen tijdens het aanmelden en het Hallo-inhoud van de tokens die toepassing hello ontvangt op geslaagde aanmeldingen beschreven.</span><span class="sxs-lookup"><span data-stu-id="9f275-102">This policy describes hello experiences that consumers will go through during sign-in and hello contents of tokens that hello application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="9f275-103">Hallo beleidsregels sectie van de instellingen en selecteer **registreren of aanmelden beleid** en klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9f275-103">In hello policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![Beleid voor registreren of aanmelden selecteren en op de knop Toevoegen klikken](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="9f275-105">Voer een beleid **naam** voor uw toepassing tooreference.</span><span class="sxs-lookup"><span data-stu-id="9f275-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="9f275-106">Geef bijvoorbeeld `SiUpIn` op.</span><span class="sxs-lookup"><span data-stu-id="9f275-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="9f275-107">Selecteer **Id-providers** en schakel **Registreren met e-mailadres** in.</span><span class="sxs-lookup"><span data-stu-id="9f275-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="9f275-108">U kunt er ook voor kiezen om sociale id-providers te selecteren als dit al is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9f275-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="9f275-109">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f275-109">Click **OK**.</span></span>

![E-aanmelding als een id-provider en klik op de knop OK Hallo](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="9f275-111">Selecteer **Registratiekenmerken**.</span><span class="sxs-lookup"><span data-stu-id="9f275-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="9f275-112">Kenmerken kiezen gewenste toocollect van Hallo consumer tijdens de registratie.</span><span class="sxs-lookup"><span data-stu-id="9f275-112">Choose attributes you want toocollect from hello consumer during sign-up.</span></span> <span data-ttu-id="9f275-113">Schakel bijvoorbeeld **Land/regio**, **Weergavenaam** en **Postcode** in.</span><span class="sxs-lookup"><span data-stu-id="9f275-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="9f275-114">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f275-114">Click **OK**.</span></span>

![Selecteer enkele kenmerken en klik op OK Hallo](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="9f275-116">Selecteer **Toepassingsclaims**.</span><span class="sxs-lookup"><span data-stu-id="9f275-116">Select **Application claims**.</span></span> <span data-ttu-id="9f275-117">Kies claims opvragen in Hallo autorisatie tokens wilt verzonden back tooyour toepassing na een geslaagde aanmelding of aanmelden ervaring.</span><span class="sxs-lookup"><span data-stu-id="9f275-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="9f275-118">Selecteer bijvoorbeeld **Weergavenaam**, **Id-provider**, **Postcode**, **Gebruiker is nieuw** en **Object-id van gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="9f275-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![Selecteer enkele toepassingsclaims en klik op de knop OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="9f275-120">Klik op **maken** tooadd Hallo beleid.</span><span class="sxs-lookup"><span data-stu-id="9f275-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="9f275-121">Hallo-beleid wordt vermeld als **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="9f275-121">hello policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="9f275-122">Hallo **B2C_1_** voorvoegsel is de naam van de toegevoegde toohello.</span><span class="sxs-lookup"><span data-stu-id="9f275-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="9f275-123">Hallo beleid openen door te selecteren **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="9f275-123">Open hello policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="9f275-124">Hallo-instellingen die zijn opgegeven in de tabel Hallo controleren en klik vervolgens op **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="9f275-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Selecteer het beleid en voer dit uit](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="9f275-126">Instelling</span><span class="sxs-lookup"><span data-stu-id="9f275-126">Setting</span></span>      | <span data-ttu-id="9f275-127">Waarde</span><span class="sxs-lookup"><span data-stu-id="9f275-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="9f275-128">**Toepassingen**</span><span class="sxs-lookup"><span data-stu-id="9f275-128">**Applications**</span></span> | <span data-ttu-id="9f275-129">Contoso B2C-app</span><span class="sxs-lookup"><span data-stu-id="9f275-129">Contoso B2C app</span></span> |
| <span data-ttu-id="9f275-130">**Antwoord-URL selecteren**</span><span class="sxs-lookup"><span data-stu-id="9f275-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="9f275-131">Een nieuw browsertabblad wordt geopend en u kunt controleren of Hallo registreren of aanmelden consumer ervaring zoals geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9f275-131">A new browser tab opens, and you can verify hello sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="9f275-132">Het tooa minuut voor het maken van beleid in beslag en updates van kracht tootake.</span><span class="sxs-lookup"><span data-stu-id="9f275-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>