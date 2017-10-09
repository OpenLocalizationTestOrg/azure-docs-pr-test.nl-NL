<span data-ttu-id="db3b3-101">tooenable fijnmazig wachtwoord opnieuw instellen op uw toepassing, moet u een beleid voor wachtwoordherstel toocreate.</span><span class="sxs-lookup"><span data-stu-id="db3b3-101">tooenable fine-grained password reset on your application, you will need toocreate a password reset policy.</span></span> <span data-ttu-id="db3b3-102">Opmerking die Hallo tenant wide wachtwoordherstel optie opgegeven [hier](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="db3b3-102">Note that hello tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="db3b3-103">Dit beleid beschrijft Hallo ervaringen die Hallo consumenten doorlopen tijdens het wachtwoord opnieuw instellen en het Hallo-inhoud van de tokens die toepassing hello ontvangt is gelukt.</span><span class="sxs-lookup"><span data-stu-id="db3b3-103">This policy describes hello experiences that hello consumers will go through during password reset and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="db3b3-104">Hallo beleidsregels sectie van de instellingen en selecteer **beleid voor wachtwoordherstel** en klik op **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="db3b3-104">In hello policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Selecteer registreren of aanmelden beleid en klik op de knop toevoegen Hallo](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="db3b3-106">Voer een beleid **naam** voor uw toepassing tooreference.</span><span class="sxs-lookup"><span data-stu-id="db3b3-106">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="db3b3-107">Geef bijvoorbeeld `SSPR` op.</span><span class="sxs-lookup"><span data-stu-id="db3b3-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="db3b3-108">Selecteer **Id-providers** en schakel de optie **Het wachtwoord opnieuw instellen met e-mailadres** in.</span><span class="sxs-lookup"><span data-stu-id="db3b3-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="db3b3-109">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="db3b3-109">Click **OK**.</span></span>

![Wachtwoord opnieuw instellen met behulp van e-mailadres als een id-provider en klik op de knop OK Hallo](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="db3b3-111">Selecteer **Toepassingsclaims**.</span><span class="sxs-lookup"><span data-stu-id="db3b3-111">Select **Application claims**.</span></span> <span data-ttu-id="db3b3-112">Kies de claims die u opvragen in Hallo autorisatie tokens wilt back tooyour toepassing verzonden nadat een geslaagde wachtwoordherstel ervaring.</span><span class="sxs-lookup"><span data-stu-id="db3b3-112">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful password reset experience.</span></span> <span data-ttu-id="db3b3-113">Selecteer bijvoorbeeld **Object-ID van gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="db3b3-113">For example, select **User's Object ID**.</span></span>

![Selecteer enkele toepassingsclaims en klik op de knop OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="db3b3-115">Klik op **maken** tooadd Hallo beleid.</span><span class="sxs-lookup"><span data-stu-id="db3b3-115">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="db3b3-116">Hallo-beleid wordt vermeld als **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="db3b3-116">hello policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="db3b3-117">Hallo **B2C_1_** voorvoegsel is de naam van de toegevoegde toohello.</span><span class="sxs-lookup"><span data-stu-id="db3b3-117">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="db3b3-118">Hallo beleid openen door te selecteren **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="db3b3-118">Open hello policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="db3b3-119">Hallo-instellingen die zijn opgegeven in de tabel Hallo controleren en klik vervolgens op **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="db3b3-119">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Selecteer het beleid en voer dit uit](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="db3b3-121">Instelling</span><span class="sxs-lookup"><span data-stu-id="db3b3-121">Setting</span></span>      | <span data-ttu-id="db3b3-122">Waarde</span><span class="sxs-lookup"><span data-stu-id="db3b3-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="db3b3-123">**Toepassingen**</span><span class="sxs-lookup"><span data-stu-id="db3b3-123">**Applications**</span></span> | <span data-ttu-id="db3b3-124">Contoso B2C-app</span><span class="sxs-lookup"><span data-stu-id="db3b3-124">Contoso B2C app</span></span> |
| <span data-ttu-id="db3b3-125">**Antwoord-URL selecteren**</span><span class="sxs-lookup"><span data-stu-id="db3b3-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="db3b3-126">Een nieuw browsertabblad geopend en kunt u controleren of Hallo wachtwoordherstel consumer ervaring in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="db3b3-126">A new browser tab opens, and you can verify hello password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="db3b3-127">Het tooa minuut voor het maken van beleid in beslag en updates van kracht tootake.</span><span class="sxs-lookup"><span data-stu-id="db3b3-127">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>
