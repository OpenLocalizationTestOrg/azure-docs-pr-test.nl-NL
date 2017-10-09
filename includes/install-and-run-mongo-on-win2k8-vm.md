<span data-ttu-id="1bfba-101">Volg deze stappen tooinstall en MongoDB uitgevoerd op een virtuele machine met Windows Server.</span><span class="sxs-lookup"><span data-stu-id="1bfba-101">Follow these steps tooinstall and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1bfba-102">Beveiligingsfuncties van MongoDB, zoals verificatie en IP-adresbinding zijn niet standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1bfba-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="1bfba-103">Beveiligingsfuncties moeten worden ingeschakeld voordat u MongoDB tooa productieomgeving implementeert.</span><span class="sxs-lookup"><span data-stu-id="1bfba-103">Security features should be enabled before deploying MongoDB tooa production environment.</span></span>  <span data-ttu-id="1bfba-104">Zie voor meer informatie [beveiligings- en](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="1bfba-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="1bfba-105">Nadat u verbinding hebt met het toohello virtuele machine via Extern bureaublad, Internet Explorer openen vanuit Hallo **Start** menu op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1bfba-105">After you've connected toohello virtual machine using Remote Desktop, open Internet Explorer from hello **Start** menu on hello virtual machine.</span></span>
2. <span data-ttu-id="1bfba-106">Selecteer Hallo **extra** knop in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="1bfba-106">Select hello **Tools** button in hello upper right corner.</span></span>  <span data-ttu-id="1bfba-107">In **Internetopties**, selecteer Hallo **beveiliging** tabblad en selecteer vervolgens Hallo **vertrouwde websites** pictogram en klik tot slot op Hallo **Sites** de knop.</span><span class="sxs-lookup"><span data-stu-id="1bfba-107">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon, and finally click hello **Sites** button.</span></span> <span data-ttu-id="1bfba-108">Voeg *https://\*. mongodb.org* toohello lijst met vertrouwde sites.</span><span class="sxs-lookup"><span data-stu-id="1bfba-108">Add *https://\*.mongodb.org* toohello list of trusted sites.</span></span>
3. <span data-ttu-id="1bfba-109">Ga te[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="1bfba-109">Go too[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="1bfba-110">Hallo zoeken **huidige stabiele Release** van **Community Server**, selecteer laatste Hallo **64-bits** versie in Hallo Windows kolom.</span><span class="sxs-lookup"><span data-stu-id="1bfba-110">Find hello **Current Stable Release** of **Community Server**, select hello latest **64-bit** version in hello Windows column.</span></span> <span data-ttu-id="1bfba-111">Download en voer vervolgens Hallo MSI-installer.</span><span class="sxs-lookup"><span data-stu-id="1bfba-111">Download, then run hello MSI installer.</span></span>
5. <span data-ttu-id="1bfba-112">MongoDB wordt doorgaans geïnstalleerd in C:\Program Files\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1bfba-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="1bfba-113">Omgevingsvariabelen zoeken op Hallo bureaublad en Hallo MongoDB binaire bestanden toohello pad padvariabele toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1bfba-113">Search for Environment Variables on hello desktop and add hello MongoDB binaries path toohello PATH variable.</span></span> <span data-ttu-id="1bfba-114">U kunt bijvoorbeeld Hallo binaire bestanden vinden op C:\Program Files\MongoDB\Server\3.4\bin op uw computer.</span><span class="sxs-lookup"><span data-stu-id="1bfba-114">For example, you might find hello binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="1bfba-115">MongoDB-gegevens en logboekbestanden mappen maken in de gegevensschijf hello (zoals station **F:**) u hebt gemaakt in de vorige stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="1bfba-115">Create MongoDB data and log directories in hello data disk (such as drive **F:**) you created in hello preceding steps.</span></span> <span data-ttu-id="1bfba-116">Van **Start**, selecteer **opdrachtprompt** tooopen een opdrachtpromptvenster.</span><span class="sxs-lookup"><span data-stu-id="1bfba-116">From **Start**, select **Command Prompt** tooopen a command prompt window.</span></span>  <span data-ttu-id="1bfba-117">Type:</span><span class="sxs-lookup"><span data-stu-id="1bfba-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="1bfba-118">toorun Hallo-database, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1bfba-118">toorun hello database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="1bfba-119">Alle berichten in het logboek zijn gerichte toohello *F:\MongoLogs\mongolog.log* bestand zoals mongod.exe server wordt gestart en preallocates journaal-bestanden.</span><span class="sxs-lookup"><span data-stu-id="1bfba-119">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="1bfba-120">Het kan enkele minuten duren voordat MongoDB toopreallocate Hallo journaal bestanden en beginnen met luisteren voor verbindingen.</span><span class="sxs-lookup"><span data-stu-id="1bfba-120">It may take several minutes for MongoDB toopreallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="1bfba-121">Hallo-opdrachtprompt blijft gericht zijn op deze taak terwijl het MongoDB-exemplaar wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1bfba-121">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="1bfba-122">toostart hello beheerdersrechten MongoDB-shell, opent u een andere opdrachtvenster van **Start** en type Hallo de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="1bfba-122">toostart hello MongoDB administrative shell, open another command window from **Start** and type hello following commands:</span></span>

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    <span data-ttu-id="1bfba-123">Hallo-database is gemaakt door Hallo invoegen.</span><span class="sxs-lookup"><span data-stu-id="1bfba-123">hello database is created by hello insert.</span></span>
9. <span data-ttu-id="1bfba-124">U kunt ook mongod.exe installeren als een service:</span><span class="sxs-lookup"><span data-stu-id="1bfba-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="1bfba-125">Een service is geïnstalleerd met de naam MongoDB met een beschrijving van "DB met Mongo".</span><span class="sxs-lookup"><span data-stu-id="1bfba-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="1bfba-126">Hallo `--logpath` optie moet de gebruikte toospecify een logboekbestand, sinds het Hallo-service uitgevoerd heeft geen toodisplay uitvoer van een venster.</span><span class="sxs-lookup"><span data-stu-id="1bfba-126">hello `--logpath` option must be used toospecify a log file, since hello running service does not have a command window toodisplay output.</span></span>  <span data-ttu-id="1bfba-127">Hallo `--logappend` optie geeft u uitvoer tooappend toohello bestaande logboekbestand zorgt ervoor dat Hallo-service opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="1bfba-127">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>  <span data-ttu-id="1bfba-128">Hallo `--dbpath` optie geeft u op Hallo-locatie van map Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="1bfba-128">hello `--dbpath` option specifies hello location of hello data directory.</span></span> <span data-ttu-id="1bfba-129">Zie voor meer service-gerelateerde opdrachtregelopties, [opdrachtregelopties voor het Service-gerelateerde][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="1bfba-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="1bfba-130">toostart hello service, die deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1bfba-130">toostart hello service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="1bfba-131">Nu dat MongoDB is geïnstalleerd en actief is, u een poort in Windows Firewall tooopen moet zodat u op afstand kunt verbinding maken met tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="1bfba-131">Now that MongoDB is installed and running, you need tooopen a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span>  <span data-ttu-id="1bfba-132">Van Hallo **Start** selecteert u **Systeembeheer** en vervolgens **Windows Firewall met geavanceerde beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="1bfba-132">From hello **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="1bfba-133">een) Selecteer in het linkerdeelvenster Hallo **regels voor binnenkomende verbindingen**.</span><span class="sxs-lookup"><span data-stu-id="1bfba-133">a) In hello left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="1bfba-134">In Hallo **acties** deelvenster op Hallo rechts, selecteer **nieuwe regel...** .</span><span class="sxs-lookup"><span data-stu-id="1bfba-134">In hello **Actions** pane on hello right, select **New Rule...**.</span></span>

    ![Windows Firewall][Image1]

    <span data-ttu-id="1bfba-136">b) in Hallo **nieuwe Wizard regel voor binnenkomende**, selecteer **poort** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1bfba-136">b) In hello **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Windows Firewall][Image2]

    <span data-ttu-id="1bfba-138">c) Selecteer **TCP** en vervolgens **specifieke lokale poorten**.</span><span class="sxs-lookup"><span data-stu-id="1bfba-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="1bfba-139">Geef een '27017' (Hallo standaardpoort MongoDB luistert op)-poort en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1bfba-139">Specify a port of "27017" (hello default port MongoDB listens on) and click **Next**.</span></span>

    ![Windows Firewall][Image3]

    <span data-ttu-id="1bfba-141">d) Selecteer **Hallo verbinding toestaan** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1bfba-141">d) Select **Allow hello connection** and click **Next**.</span></span>

    ![Windows Firewall][Image4]

    <span data-ttu-id="1bfba-143">e) Klik op **volgende** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="1bfba-143">e) Click **Next** again.</span></span>

    ![Windows Firewall][Image5]

    <span data-ttu-id="1bfba-145">f) Geef een naam voor de regel hello, zoals 'MongoPort', en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="1bfba-145">f) Specify a name for hello rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Windows Firewall][Image6]

12. <span data-ttu-id="1bfba-147">Als u niet een eindpunt voor MongoDB configureren wanneer u Hallo virtuele machine hebt gemaakt, kunt u dit nu doen.</span><span class="sxs-lookup"><span data-stu-id="1bfba-147">If you didn't configure an endpoint for MongoDB when you created hello virtual machine, you can do it now.</span></span> <span data-ttu-id="1bfba-148">Moet u zowel de firewallregel Hallo en Hallo eindpunt toobe kunnen tooconnect tooMongoDB op afstand.</span><span class="sxs-lookup"><span data-stu-id="1bfba-148">You need both hello firewall rule and hello endpoint toobe able tooconnect tooMongoDB remotely.</span></span>

  <span data-ttu-id="1bfba-149">Klik in hello Azure-portal, op **virtuele Machines (klassiek)**Hallo-naam van uw nieuwe virtuele machine op en klik vervolgens op **eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="1bfba-149">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Eindpunten][Image7]

13. <span data-ttu-id="1bfba-151">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="1bfba-151">Click **Add**.</span></span>

14. <span data-ttu-id="1bfba-152">Toevoegen van een eindpunt met de naam 'Mongo', protocol **TCP**, en beide **openbare** en **persoonlijke** set-poorten te '27017'.</span><span class="sxs-lookup"><span data-stu-id="1bfba-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set too"27017".</span></span> <span data-ttu-id="1bfba-153">Deze poort opent, kunt MongoDB toobe extern toegankelijk is.</span><span class="sxs-lookup"><span data-stu-id="1bfba-153">Opening this port allows MongoDB toobe accessed remotely.</span></span>

    ![Eindpunten][Image9]

> [!NOTE]
> <span data-ttu-id="1bfba-155">Hallo is 27017 Hallo standaardpoort die wordt gebruikt door MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1bfba-155">hello port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="1bfba-156">U kunt deze standaardpoort wijzigen door op te geven Hallo `--port` parameter bij het starten van Hallo mongod.exe server.</span><span class="sxs-lookup"><span data-stu-id="1bfba-156">You can change this default port by specifying hello `--port` parameter when starting hello mongod.exe server.</span></span> <span data-ttu-id="1bfba-157">Zorg ervoor dat toogive hetzelfde poortnummer in de firewall Hallo Hallo en Hallo 'Mongo' eindpunt in de voorgaande instructies Hallo.</span><span class="sxs-lookup"><span data-stu-id="1bfba-157">Make sure toogive hello same port number in hello firewall and hello "Mongo" endpoint in hello preceding instructions.</span></span>
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
