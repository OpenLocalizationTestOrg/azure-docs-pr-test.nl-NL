<span data-ttu-id="bff36-101">Als u zeer specifieke regels wilt opgeven voor het opnieuw instellen van het wachtwoord voor een toepassing, kunt u hiervoor een beleid definiëren.</span><span class="sxs-lookup"><span data-stu-id="bff36-101">To enable fine-grained password reset on your application, you will need to create a password reset policy.</span></span> <span data-ttu-id="bff36-102">Informatie over de optie voor het opnieuw instellen van het wachtwoord voor de tenant als geheel vindt u [hier](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="bff36-102">Note that the tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="bff36-103">In dit beleid wordt de ervaring van consumenten beschreven als ze het wachtwoord opnieuw gaan instellen, evenals de inhoud van tokens die de toepassing ontvangt als de bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="bff36-103">This policy describes the experiences that the consumers will go through during password reset and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="bff36-104">Ga in Instellingen naar de sectie Beleid, kies de optie **Beleid voor het opnieuw instellen van het wachtwoord** en klik op **+ Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bff36-104">In the policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Beleid voor registreren of aanmelden selecteren en op de knop Toevoegen klikken](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="bff36-106">Geef een**** naam op voor het beleid waarnaar de toepassing kan verwijzen.</span><span class="sxs-lookup"><span data-stu-id="bff36-106">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="bff36-107">Geef bijvoorbeeld `SSPR` op.</span><span class="sxs-lookup"><span data-stu-id="bff36-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="bff36-108">Selecteer **Id-providers** en schakel de optie **Het wachtwoord opnieuw instellen met e-mailadres** in.</span><span class="sxs-lookup"><span data-stu-id="bff36-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="bff36-109">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bff36-109">Click **OK**.</span></span>

![De optie Het wachtwoord opnieuw instellen met e-mailadres selecteren als een id-provider en op de knop OK klikken](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="bff36-111">Selecteer **Toepassingsclaims**.</span><span class="sxs-lookup"><span data-stu-id="bff36-111">Select **Application claims**.</span></span> <span data-ttu-id="bff36-112">Kies de claims die u wilt opnemen in de autorisatietokens die worden geretourneerd naar de toepassing wanneer het opnieuw instellen van het wachtwoord is gelukt.</span><span class="sxs-lookup"><span data-stu-id="bff36-112">Choose claims you want returned in the authorization tokens sent back to your application after a successful password reset experience.</span></span> <span data-ttu-id="bff36-113">Selecteer bijvoorbeeld **Object-ID van gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="bff36-113">For example, select **User's Object ID**.</span></span>

![Selecteer enkele toepassingsclaims en klik op de knop OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="bff36-115">Klik op **Maken** om het beleid toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="bff36-115">Click **Create** to add the policy.</span></span> <span data-ttu-id="bff36-116">Het beleid wordt vermeld als **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="bff36-116">The policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="bff36-117">Het voorvoegsel **B2C_1_** wordt toegevoegd aan de naam.</span><span class="sxs-lookup"><span data-stu-id="bff36-117">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="bff36-118">Open het beleid door **B2C_1_SSPR** te selecteren.</span><span class="sxs-lookup"><span data-stu-id="bff36-118">Open the policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="bff36-119">Controleer de instellingen die zijn opgegeven in de tabel en klik vervolgens op **Nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="bff36-119">Verify the settings specified in the table then click **Run now**.</span></span>

![Selecteer het beleid en voer dit uit](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="bff36-121">Instelling</span><span class="sxs-lookup"><span data-stu-id="bff36-121">Setting</span></span>      | <span data-ttu-id="bff36-122">Waarde</span><span class="sxs-lookup"><span data-stu-id="bff36-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="bff36-123">**Toepassingen**</span><span class="sxs-lookup"><span data-stu-id="bff36-123">**Applications**</span></span> | <span data-ttu-id="bff36-124">Contoso B2C-app</span><span class="sxs-lookup"><span data-stu-id="bff36-124">Contoso B2C app</span></span> |
| <span data-ttu-id="bff36-125">**Antwoord-URL selecteren**</span><span class="sxs-lookup"><span data-stu-id="bff36-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="bff36-126">Er wordt een nieuw browsertabblad geopend. Hier kunt u controleren hoe het opnieuw instellen van het wachtwoord werkt voor consumenten.</span><span class="sxs-lookup"><span data-stu-id="bff36-126">A new browser tab opens, and you can verify the password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="bff36-127">Het duurt maximaal één minuut voordat het gemaakte beleid en de updates van kracht worden.</span><span class="sxs-lookup"><span data-stu-id="bff36-127">It takes up to a minute for policy creation and updates to take effect.</span></span>
>
