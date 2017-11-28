## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="966b9-101">Uw Intel NUC voorbereiden</span><span class="sxs-lookup"><span data-stu-id="966b9-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="966b9-102">U voltooit de installatie van de hardware, moet u:</span><span class="sxs-lookup"><span data-stu-id="966b9-102">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="966b9-103">Verbinding maken met uw NUC Intel de voeding die is opgenomen in het pakket.</span><span class="sxs-lookup"><span data-stu-id="966b9-103">Connect your Intel NUC to the power supply included in the kit.</span></span>
- <span data-ttu-id="966b9-104">Verbinding maken met uw NUC Intel via een Ethernet-kabel met het netwerk.</span><span class="sxs-lookup"><span data-stu-id="966b9-104">Connect your Intel NUC to your network using an Ethernet cable.</span></span>

<span data-ttu-id="966b9-105">U hebt nu de hardware-instellingen van uw gatewayapparaat Intel NUC voltooid.</span><span class="sxs-lookup"><span data-stu-id="966b9-105">You have now completed the hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="966b9-106">Aanmelden en toegang tot de terminal</span><span class="sxs-lookup"><span data-stu-id="966b9-106">Sign in and access the terminal</span></span>

<span data-ttu-id="966b9-107">U hebt twee opties voor toegang tot een terminal omgeving op uw NUC Intel:</span><span class="sxs-lookup"><span data-stu-id="966b9-107">You have two options to access a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="966b9-108">Als u een toetsenbord en de monitor die zijn verbonden met uw NUC Intel hebt, kunt u de shell rechtstreeks openen.</span><span class="sxs-lookup"><span data-stu-id="966b9-108">If you have a keyboard and monitor connected to your Intel NUC, you can access the shell directly.</span></span> <span data-ttu-id="966b9-109">De standaardreferenties zijn gebruikersnaam **hoofdmap** en het wachtwoord **hoofdmap**.</span><span class="sxs-lookup"><span data-stu-id="966b9-109">The default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="966b9-110">Toegang tot de shell op uw Intel NUC gebruik van SSH op uw computer.</span><span class="sxs-lookup"><span data-stu-id="966b9-110">Access the shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="966b9-111">Meld u aan met SSH</span><span class="sxs-lookup"><span data-stu-id="966b9-111">Sign in with SSH</span></span>

<span data-ttu-id="966b9-112">Als u wilt aanmelden met SSH, moet u het IP-adres van uw NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="966b9-112">To sign in with SSH, you need the IP address of your Intel NUC.</span></span> <span data-ttu-id="966b9-113">Als u een toetsenbord en de monitor die zijn verbonden met uw NUC Intel hebt, gebruikt de `ifconfig` opdracht de IP-adres vinden.</span><span class="sxs-lookup"><span data-stu-id="966b9-113">If you have a keyboard and monitor connected to your Intel NUC, use the `ifconfig` command to find the IP address.</span></span> <span data-ttu-id="966b9-114">U kunt ook verbinding maken met uw router voor het weergeven van de adressen van apparaten in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="966b9-114">Alternatively, connect to your router to list the addresses of devices on your network.</span></span>

<span data-ttu-id="966b9-115">Aanmelden met gebruikersnaam **hoofdmap** en het wachtwoord **hoofdmap**.</span><span class="sxs-lookup"><span data-stu-id="966b9-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="966b9-116">Optioneel: Een map op uw NUC Intel delen</span><span class="sxs-lookup"><span data-stu-id="966b9-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="966b9-117">U kunt desgewenst een map op uw NUC Intel delen met uw bureaublad omgeving.</span><span class="sxs-lookup"><span data-stu-id="966b9-117">Optionally, you may want to share a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="966b9-118">Delen van een map, kunt u gebruikmaken van uw voorkeur bureaublad teksteditor (zoals [Visual Studio Code](https://code.visualstudio.com/) of [Sublime Text](http://www.sublimetext.com/)) voor het bewerken van bestanden op uw NUC Intel in plaats van `nano` of `vi`.</span><span class="sxs-lookup"><span data-stu-id="966b9-118">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="966b9-119">Als u wilt delen een map met Windows, een Samba-server in de Intel NUC te configureren.</span><span class="sxs-lookup"><span data-stu-id="966b9-119">To share a folder with Windows, configure a Samba server on the Intel NUC.</span></span> <span data-ttu-id="966b9-120">De SFTP-server ook gebruiken op de Intel NUC met een SFTP-client op uw computer.</span><span class="sxs-lookup"><span data-stu-id="966b9-120">Alternatively, use the SFTP server on the Intel NUC with an SFTP client on your desktop machine.</span></span>
