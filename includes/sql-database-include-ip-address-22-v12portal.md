
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, the following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through the new Azure portal
-->


1. <span data-ttu-id="e18cf-101">Meld u aan bij de [Azure-portal](https://portal.azure.com/) op http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="e18cf-101">Log in to the [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="e18cf-102">Klik in het linkerdeelvenster vaandel **door alles bladeren**.</span><span class="sxs-lookup"><span data-stu-id="e18cf-102">In the left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="e18cf-103">De **Bladeren** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e18cf-103">The **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="e18cf-104">Schuif en klik op **SQL-servers**.</span><span class="sxs-lookup"><span data-stu-id="e18cf-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="e18cf-105">De **SQL-servers** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e18cf-105">The **SQL servers** blade is displayed.</span></span>
   
    ![Uw Azure SQL Database-server niet vinden in de portal][b21-FindServerInPortal]
4. <span data-ttu-id="e18cf-107">Klik op het besturingselement minimaliseren in de eerdere voor het gemak **Bladeren** blade.</span><span class="sxs-lookup"><span data-stu-id="e18cf-107">For convenience, click the minimize control on the earlier **Browse** blade.</span></span>
5. <span data-ttu-id="e18cf-108">Typ de naam van uw server in het filtertekstvak.</span><span class="sxs-lookup"><span data-stu-id="e18cf-108">In the filter text box, start typing the name of your server.</span></span> <span data-ttu-id="e18cf-109">De rij wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e18cf-109">Your row is displayed.</span></span>
6. <span data-ttu-id="e18cf-110">Klik op de rij voor uw server.</span><span class="sxs-lookup"><span data-stu-id="e18cf-110">Click the row for your server.</span></span> <span data-ttu-id="e18cf-111">Een blade voor uw server wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e18cf-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="e18cf-112">Klik op de blade van uw server **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="e18cf-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="e18cf-113">De **instellingen** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e18cf-113">The **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="e18cf-114">Klik op **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="e18cf-114">Click **Firewall**.</span></span> <span data-ttu-id="e18cf-115">De **firewallinstellingen** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e18cf-115">The **Firewall Settings** blade is displayed.</span></span>
   
    ![Klik op Instellingen > Firewall][b31-SettingsFirewallNavig]
9. <span data-ttu-id="e18cf-117">Klik op **-Client toevoegen IP**.</span><span class="sxs-lookup"><span data-stu-id="e18cf-117">Click **Add Client IP**.</span></span> <span data-ttu-id="e18cf-118">Typ een naam voor de nieuwe regel in het eerste tekstvak.</span><span class="sxs-lookup"><span data-stu-id="e18cf-118">Type in a name for your new rule into the first text box.</span></span>
10. <span data-ttu-id="e18cf-119">Typ in de lage en hoge IP-adreswaarden voor het bereik dat u wilt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e18cf-119">Type in the low and high IP address values for the range you want to enable.</span></span>
    
    * <span data-ttu-id="e18cf-120">Het kan zijn bij de hand hebt om het einde van de lage waarde met **.0** en de hoge met **.255**.</span><span class="sxs-lookup"><span data-stu-id="e18cf-120">It can be handy to have the low value end with **.0** and the high with **.255**.</span></span>
    
    ![Toevoegen van een IP-adresbereik om toe te staan][b41-AddRange]
11. <span data-ttu-id="e18cf-122">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e18cf-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
