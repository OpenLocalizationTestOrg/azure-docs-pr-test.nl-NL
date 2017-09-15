<span data-ttu-id="d8c12-101">U moet een aanmeldingsbeleid maken om aanmelden in te schakelen op uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d8c12-101">To enable sign-in on your application, you will need to create a sign-in policy.</span></span> <span data-ttu-id="d8c12-102">In dit beleid wordt de ervaring van consumenten bij het aanmelden beschreven en de inhoud van tokens die de toepassing ontvangt nadat aanmeldingen zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="d8c12-102">This policy describes the experiences that consumers will go through during sign-in and the contents of tokens that the application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="d8c12-103">Selecteer bij instellingen in de sectie Beleid de optie **Registratie- of aanmeldingsbeleid** en klik op **+Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d8c12-103">In the policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![Beleid voor registreren of aanmelden selecteren en op de knop Toevoegen klikken](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="d8c12-105">Geef een**** naam op voor het beleid waarnaar de toepassing kan verwijzen.</span><span class="sxs-lookup"><span data-stu-id="d8c12-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="d8c12-106">Geef bijvoorbeeld `SiUpIn` op.</span><span class="sxs-lookup"><span data-stu-id="d8c12-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="d8c12-107">Selecteer **Id-providers** en schakel **Registreren met e-mailadres** in.</span><span class="sxs-lookup"><span data-stu-id="d8c12-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="d8c12-108">U kunt er ook voor kiezen om sociale id-providers te selecteren als dit al is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d8c12-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="d8c12-109">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8c12-109">Click **OK**.</span></span>

![Selecteer Registreren met e-mailadres als id-provider en klik op de knop OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="d8c12-111">Selecteer **Registratiekenmerken**.</span><span class="sxs-lookup"><span data-stu-id="d8c12-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="d8c12-112">Kies de kenmerken van de consument die u wilt verzamelen tijdens de registratie.</span><span class="sxs-lookup"><span data-stu-id="d8c12-112">Choose attributes you want to collect from the consumer during sign-up.</span></span> <span data-ttu-id="d8c12-113">Schakel bijvoorbeeld **Land/regio**, **Weergavenaam** en **Postcode** in.</span><span class="sxs-lookup"><span data-stu-id="d8c12-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="d8c12-114">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8c12-114">Click **OK**.</span></span>

![Selecteer enkele kenmerken en klik op de knop OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="d8c12-116">Selecteer **Toepassingsclaims**.</span><span class="sxs-lookup"><span data-stu-id="d8c12-116">Select **Application claims**.</span></span> <span data-ttu-id="d8c12-117">Kies de claims die u wilt laten retourneren in de autorisatietokens die, na een geslaagde aanmelding, terug worden gestuurd naar de toepassing .</span><span class="sxs-lookup"><span data-stu-id="d8c12-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="d8c12-118">Selecteer bijvoorbeeld **Weergavenaam**, **Id-provider**, **Postcode**, **Gebruiker is nieuw** en **Object-id van gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="d8c12-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![Selecteer enkele toepassingsclaims en klik op de knop OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="d8c12-120">Klik op **Maken** om het beleid toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="d8c12-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="d8c12-121">Het beleid wordt vermeld als **B2C_1_SiUpln**.</span><span class="sxs-lookup"><span data-stu-id="d8c12-121">The policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="d8c12-122">Het voorvoegsel **B2C_1_** wordt toegevoegd aan de naam.</span><span class="sxs-lookup"><span data-stu-id="d8c12-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="d8c12-123">Open het beleid door **B2C_1_SiUpln** te selecteren.</span><span class="sxs-lookup"><span data-stu-id="d8c12-123">Open the policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="d8c12-124">Controleer de instellingen die zijn opgegeven in de tabel en klik vervolgens op **Nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="d8c12-124">Verify the settings specified in the table then click **Run now**.</span></span>

![Selecteer het beleid en voer dit uit](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="d8c12-126">Instelling</span><span class="sxs-lookup"><span data-stu-id="d8c12-126">Setting</span></span>      | <span data-ttu-id="d8c12-127">Waarde</span><span class="sxs-lookup"><span data-stu-id="d8c12-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="d8c12-128">**Toepassingen**</span><span class="sxs-lookup"><span data-stu-id="d8c12-128">**Applications**</span></span> | <span data-ttu-id="d8c12-129">Contoso B2C-app</span><span class="sxs-lookup"><span data-stu-id="d8c12-129">Contoso B2C app</span></span> |
| <span data-ttu-id="d8c12-130">**Antwoord-URL selecteren**</span><span class="sxs-lookup"><span data-stu-id="d8c12-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="d8c12-131">Er wordt een nieuw browsertabblad geopend. Hier kunt u controleren of het registreren of aanmelden voor consumenten werkt zoals geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d8c12-131">A new browser tab opens, and you can verify the sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="d8c12-132">Het duurt maximaal één minuut voordat het gemaakte beleid en de updates van kracht worden.</span><span class="sxs-lookup"><span data-stu-id="d8c12-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>