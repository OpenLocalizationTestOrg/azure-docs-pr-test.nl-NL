
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. <span data-ttu-id="e9393-101">Meld u bij toohello [Azure-portal](https://portal.azure.com/) op http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="e9393-101">Log in toohello [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="e9393-102">Klik in het linkerdeelvenster vaandel hello, **door alles bladeren**.</span><span class="sxs-lookup"><span data-stu-id="e9393-102">In hello left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="e9393-103">Hallo **Bladeren** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e9393-103">hello **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="e9393-104">Schuif en klik op **SQL-servers**.</span><span class="sxs-lookup"><span data-stu-id="e9393-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="e9393-105">Hallo **SQL-servers** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e9393-105">hello **SQL servers** blade is displayed.</span></span>
   
    ![Uw Azure SQL Database-server vinden in Hallo-portal][b21-FindServerInPortal]
4. <span data-ttu-id="e9393-107">Klik op Hallo voor het gemak minimaliseren besturingselement op Hallo eerder **Bladeren** blade.</span><span class="sxs-lookup"><span data-stu-id="e9393-107">For convenience, click hello minimize control on hello earlier **Browse** blade.</span></span>
5. <span data-ttu-id="e9393-108">In de filtertekstvak Hallo begint te typen Hallo-naam van uw server.</span><span class="sxs-lookup"><span data-stu-id="e9393-108">In hello filter text box, start typing hello name of your server.</span></span> <span data-ttu-id="e9393-109">De rij wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e9393-109">Your row is displayed.</span></span>
6. <span data-ttu-id="e9393-110">Klik op de rij Hallo voor uw server.</span><span class="sxs-lookup"><span data-stu-id="e9393-110">Click hello row for your server.</span></span> <span data-ttu-id="e9393-111">Een blade voor uw server wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e9393-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="e9393-112">Klik op de blade van uw server **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="e9393-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="e9393-113">Hallo **instellingen** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e9393-113">hello **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="e9393-114">Klik op **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="e9393-114">Click **Firewall**.</span></span> <span data-ttu-id="e9393-115">Hallo **firewallinstellingen** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e9393-115">hello **Firewall Settings** blade is displayed.</span></span>
   
    ![Klik op Instellingen > Firewall][b31-SettingsFirewallNavig]
9. <span data-ttu-id="e9393-117">Klik op **-Client toevoegen IP**.</span><span class="sxs-lookup"><span data-stu-id="e9393-117">Click **Add Client IP**.</span></span> <span data-ttu-id="e9393-118">Typ een naam voor de nieuwe regel in de eerste tekstvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="e9393-118">Type in a name for your new rule into hello first text box.</span></span>
10. <span data-ttu-id="e9393-119">Type in Hallo hoge en lage IP-adres waarden voor de gewenste Hallo bereik tooenable.</span><span class="sxs-lookup"><span data-stu-id="e9393-119">Type in hello low and high IP address values for hello range you want tooenable.</span></span>
    
    * <span data-ttu-id="e9393-120">Het kan ook handig toohave Hallo lage waarde end met **.0** en Hallo met hoge **.255**.</span><span class="sxs-lookup"><span data-stu-id="e9393-120">It can be handy toohave hello low value end with **.0** and hello high with **.255**.</span></span>
    
    ![Een tooallow bereik van IP-adres toevoegen][b41-AddRange]
11. <span data-ttu-id="e9393-122">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e9393-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
