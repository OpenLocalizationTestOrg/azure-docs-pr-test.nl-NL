---
title: aaaInstall MongoDB op een Windows-virtuele machine in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall MongoDB op een Azure-virtuele machine met Windows Server 2012 R2 is gemaakt met Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="070a5-103">Installeren en configureren van MongoDB op een Windows-VM in Azure</span><span class="sxs-lookup"><span data-stu-id="070a5-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="070a5-104">[MongoDB](http://www.mongodb.org) is een populaire open-source, hoogwaardige NoSQL-database.</span><span class="sxs-lookup"><span data-stu-id="070a5-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="070a5-105">In dit artikel begeleidt u bij het installeren en configureren van MongoDB op een Windows Server 2012 R2 virtual machine (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="070a5-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="070a5-106">U kunt ook [MongoDB installeren op een Linux VM in Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="070a5-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="070a5-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="070a5-107">Prerequisites</span></span>
<span data-ttu-id="070a5-108">Voordat u installeren en configureren van MongoDB, u moet toocreate een virtuele machine en, in het ideale geval een schijf gegevens tooit toevoegen.</span><span class="sxs-lookup"><span data-stu-id="070a5-108">Before you install and configure MongoDB, you need toocreate a VM and, ideally, add a data disk tooit.</span></span> <span data-ttu-id="070a5-109">Zie Hallo artikelen toocreate een virtuele machine te volgen en een gegevensschijf toevoegen:</span><span class="sxs-lookup"><span data-stu-id="070a5-109">See hello following articles toocreate a VM and add a data disk:</span></span>

* <span data-ttu-id="070a5-110">Maak een Windows Server-VM met [hello Azure-portal](quick-create-portal.md) of [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="070a5-110">Create a Windows Server VM using [hello Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="070a5-111">Koppel een gegevens schijf tooa Windows Server-VM met [hello Azure-portal](attach-managed-disk-portal.md) of [Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="070a5-111">Attach a data disk tooa Windows Server VM using [hello Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="070a5-112">toobegin installeren en configureren van MongoDB, [tooyour VM van Windows Server aanmelden](connect-logon.md) met behulp van extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="070a5-112">toobegin installing and configuring MongoDB, [log on tooyour Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="070a5-113">MongoDB installeren</span><span class="sxs-lookup"><span data-stu-id="070a5-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="070a5-114">Beveiligingsfuncties van MongoDB, zoals verificatie en IP-adresbinding zijn niet standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="070a5-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="070a5-115">Beveiligingsfuncties moeten worden ingeschakeld voordat u MongoDB tooa productieomgeving implementeert.</span><span class="sxs-lookup"><span data-stu-id="070a5-115">Security features should be enabled before deploying MongoDB tooa production environment.</span></span> <span data-ttu-id="070a5-116">Zie voor meer informatie [MongoDB-beveiliging en verificatie](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="070a5-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="070a5-117">Nadat u verbinding hebt met het tooyour VM maken met extern bureaublad, Internet Explorer openen vanuit Hallo **Start** menu op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="070a5-117">After you've connected tooyour VM using Remote Desktop, open Internet Explorer from hello **Start** menu on hello VM.</span></span>
2. <span data-ttu-id="070a5-118">Selecteer **aanbevolen instellingen voor beveiliging, privacy en compatibiliteit gebruiken** wanneer Internet Explorer eerst wordt geopend en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="070a5-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="070a5-119">Verbeterde beveiliging van Internet Explorer is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="070a5-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="070a5-120">Hallo MongoDB website toohello lijst met toegestane websites toevoegen:</span><span class="sxs-lookup"><span data-stu-id="070a5-120">Add hello MongoDB website toohello list of allowed sites:</span></span>
   
   * <span data-ttu-id="070a5-121">Selecteer Hallo **extra** pictogram in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="070a5-121">Select hello **Tools** icon in hello upper-right corner.</span></span>
   * <span data-ttu-id="070a5-122">In **Internetopties**, selecteer Hallo **beveiliging** tabblad en selecteer vervolgens Hallo **vertrouwde websites** pictogram.</span><span class="sxs-lookup"><span data-stu-id="070a5-122">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="070a5-123">Klik op Hallo **Sites** knop.</span><span class="sxs-lookup"><span data-stu-id="070a5-123">Click hello **Sites** button.</span></span> <span data-ttu-id="070a5-124">Voeg *https://\*. mongodb.org* toohello lijst met vertrouwde sites en het dialoogvenster sluit Hallo.</span><span class="sxs-lookup"><span data-stu-id="070a5-124">Add *https://\*.mongodb.org* toohello list of trusted sites, and then close hello dialog box.</span></span>
     
     ![Instellingen van Internet Explorer configureren](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="070a5-126">Blader toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) pagina (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="070a5-126">Browse toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="070a5-127">Selecteer, indien nodig Hallo **Community Server** edition en selecteer vervolgens Hallo nieuwste huidige stabiele release voor Windows Server 2008 R2 64-bits of hoger.</span><span class="sxs-lookup"><span data-stu-id="070a5-127">If needed, select hello **Community Server** edition and then select hello latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="070a5-128">toodownload Hallo installatieprogramma, klikt u op **downloaden (msi)**.</span><span class="sxs-lookup"><span data-stu-id="070a5-128">toodownload hello installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![MongoDB-installatieprogramma downloaden](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="070a5-130">Voer Hallo installatieprogramma als Hallo downloaden voltooid is.</span><span class="sxs-lookup"><span data-stu-id="070a5-130">Run hello installer after hello download is complete.</span></span>
6. <span data-ttu-id="070a5-131">Lees en accepteer de gebruiksrechtovereenkomst Hallo.</span><span class="sxs-lookup"><span data-stu-id="070a5-131">Read and accept hello license agreement.</span></span> <span data-ttu-id="070a5-132">Wanneer u wordt gevraagd, selecteert u **Complete** installeren.</span><span class="sxs-lookup"><span data-stu-id="070a5-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="070a5-133">Klik op het laatste scherm hello, **installeren**.</span><span class="sxs-lookup"><span data-stu-id="070a5-133">On hello final screen, click **Install**.</span></span>

## <a name="configure-hello-vm-and-mongodb"></a><span data-ttu-id="070a5-134">Hallo VM en MongoDB configureren</span><span class="sxs-lookup"><span data-stu-id="070a5-134">Configure hello VM and MongoDB</span></span>
1. <span data-ttu-id="070a5-135">Hallo-padvariabelen worden niet bijgewerkt door Hallo MongoDB installer.</span><span class="sxs-lookup"><span data-stu-id="070a5-135">hello path variables are not updated by hello MongoDB installer.</span></span> <span data-ttu-id="070a5-136">Zonder Hallo MongoDB `bin` locatie in de variabele path, moet u toospecify Hallo volledig pad telkens wanneer u een uitvoerbaar bestand van MongoDB gebruiken.</span><span class="sxs-lookup"><span data-stu-id="070a5-136">Without hello MongoDB `bin` location in your path variable, you need toospecify hello full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="070a5-137">tooadd hello locatie tooyour padvariabele:</span><span class="sxs-lookup"><span data-stu-id="070a5-137">tooadd hello location tooyour path variable:</span></span>
   
   * <span data-ttu-id="070a5-138">Klik met de rechtermuisknop Hallo **Start** menu en selecteer **System**.</span><span class="sxs-lookup"><span data-stu-id="070a5-138">Right-click hello **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="070a5-139">Klik op **Geavanceerde systeeminstellingen**, en klik vervolgens op **omgevingsvariabelen**.</span><span class="sxs-lookup"><span data-stu-id="070a5-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="070a5-140">Onder **systeemvariabelen**, selecteer **pad**, en klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="070a5-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Padvariabelen configureren](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="070a5-142">Toevoegen van Hallo pad tooyour MongoDB `bin` map.</span><span class="sxs-lookup"><span data-stu-id="070a5-142">Add hello path tooyour MongoDB `bin` folder.</span></span> <span data-ttu-id="070a5-143">MongoDB wordt doorgaans geïnstalleerd in *C:\Program Files\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="070a5-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="070a5-144">Controleer of Hallo-installatiepad op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="070a5-144">Verify hello installation path on your VM.</span></span> <span data-ttu-id="070a5-145">Hallo volgende voorbeeld wordt toegevoegd Hallo standaard MongoDB installeren locatie toohello `PATH` variabele:</span><span class="sxs-lookup"><span data-stu-id="070a5-145">hello following example adds hello default MongoDB install location toohello `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="070a5-146">Ervoor tooadd Hallo toonaangevende puntkomma worden (`;`) toe te voegen een locatie tooyour tooindicate `PATH` variabele.</span><span class="sxs-lookup"><span data-stu-id="070a5-146">Be sure tooadd hello leading semicolon (`;`) tooindicate that you are adding a location tooyour `PATH` variable.</span></span>

2. <span data-ttu-id="070a5-147">MongoDB-gegevens en logboekbestanden mappen op de gegevensschijf van uw maken.</span><span class="sxs-lookup"><span data-stu-id="070a5-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="070a5-148">Van Hallo **Start** selecteert u **opdrachtprompt**.</span><span class="sxs-lookup"><span data-stu-id="070a5-148">From hello **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="070a5-149">Hallo volgen voorbeelden maken Hallo mappen op station F:</span><span class="sxs-lookup"><span data-stu-id="070a5-149">hello following examples create hello directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="070a5-150">Start een MongoDB-exemplaar met Hallo de volgende opdracht, Hallo pad tooyour gegevens aanpassen en meld u mappen dienovereenkomstig:</span><span class="sxs-lookup"><span data-stu-id="070a5-150">Start a MongoDB instance with hello following command, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="070a5-151">Het kan enkele minuten duren voordat MongoDB tooallocate Hallo journaal bestanden en beginnen met luisteren voor verbindingen.</span><span class="sxs-lookup"><span data-stu-id="070a5-151">It may take several minutes for MongoDB tooallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="070a5-152">Alle berichten in het logboek zijn gerichte toohello *F:\MongoLogs\mongolog.log* opslaan als `mongod.exe` server wordt gestart en wijst journaal-bestanden.</span><span class="sxs-lookup"><span data-stu-id="070a5-152">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="070a5-153">Hallo-opdrachtprompt blijft gericht zijn op deze taak terwijl het MongoDB-exemplaar wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="070a5-153">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="070a5-154">Laat Hallo opdrachtprompt venster open toocontinue met MongoDB.</span><span class="sxs-lookup"><span data-stu-id="070a5-154">Leave hello command prompt window open toocontinue running MongoDB.</span></span> <span data-ttu-id="070a5-155">Of MongoDB installeren als service, zoals beschreven in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="070a5-155">Or, install MongoDB as service, as detailed in hello next step.</span></span>

4. <span data-ttu-id="070a5-156">Installeer voor een meer robuuste MongoDB-ervaring Hallo `mongod.exe` als een service.</span><span class="sxs-lookup"><span data-stu-id="070a5-156">For a more robust MongoDB experience, install hello `mongod.exe` as a service.</span></span> <span data-ttu-id="070a5-157">Een service maakt, dat u hoeft niet tooleave een opdrachtprompt uitgevoerd elke keer dat u wilt dat toouse MongoDB.</span><span class="sxs-lookup"><span data-stu-id="070a5-157">Creating a service means you don't need tooleave a command prompt running each time you want toouse MongoDB.</span></span> <span data-ttu-id="070a5-158">Hallo service maken als volgt Hallo pad tooyour gegevens en logboekbestanden mappen dienovereenkomstig aanpassen:</span><span class="sxs-lookup"><span data-stu-id="070a5-158">Create hello service as follows, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="070a5-159">Hallo voorgaande opdracht maakt u een service met de naam MongoDB, met een beschrijving van "DB met Mongo".</span><span class="sxs-lookup"><span data-stu-id="070a5-159">hello preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="070a5-160">volgende parameters Hallo worden ook opgegeven:</span><span class="sxs-lookup"><span data-stu-id="070a5-160">hello following parameters are also specified:</span></span>
   
   * <span data-ttu-id="070a5-161">Hallo `--dbpath` optie geeft u op Hallo-locatie van map Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="070a5-161">hello `--dbpath` option specifies hello location of hello data directory.</span></span>
   * <span data-ttu-id="070a5-162">Hallo `--logpath` optie moet gebruikte toospecify een logboekbestand, omdat de actieve service Hallo geen toodisplay uitvoer van een venster.</span><span class="sxs-lookup"><span data-stu-id="070a5-162">hello `--logpath` option must be used toospecify a log file, because hello running service does not have a command window toodisplay output.</span></span>
   * <span data-ttu-id="070a5-163">Hallo `--logappend` optie geeft u uitvoer tooappend toohello bestaande logboekbestand zorgt ervoor dat Hallo-service opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="070a5-163">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>
   
   <span data-ttu-id="070a5-164">toostart hello MongoDB-service, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="070a5-164">toostart hello MongoDB service, run hello following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="070a5-165">Zie voor meer informatie over het maken van Hallo MongoDB service [configureren van een Windows-Service voor MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="070a5-165">For more information about creating hello MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-hello-mongodb-instance"></a><span data-ttu-id="070a5-166">Test Hallo MongoDB-exemplaar</span><span class="sxs-lookup"><span data-stu-id="070a5-166">Test hello MongoDB instance</span></span>
<span data-ttu-id="070a5-167">Met MongoDB uitgevoerd als één exemplaar of als een service is geïnstalleerd, kunt u nu starten maken en gebruiken van uw databases.</span><span class="sxs-lookup"><span data-stu-id="070a5-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="070a5-168">toostart hello beheerdersrechten MongoDB-shell, een ander opdrachtpromptvenster openen vanuit Hallo **Start** menu en voer de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="070a5-168">toostart hello MongoDB administrative shell, open another command prompt window from hello **Start** menu, and enter hello following command:</span></span>

```
mongo  
```

<span data-ttu-id="070a5-169">Hallo-databases met Hallo aanbieden `db` opdracht.</span><span class="sxs-lookup"><span data-stu-id="070a5-169">You can list hello databases with hello `db` command.</span></span> <span data-ttu-id="070a5-170">Voeg enkele gegeven als volgt:</span><span class="sxs-lookup"><span data-stu-id="070a5-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="070a5-171">Zoek naar gegevens als volgt:</span><span class="sxs-lookup"><span data-stu-id="070a5-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="070a5-172">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="070a5-172">hello output is similar toohello following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="070a5-173">Exit Hallo `mongo` console als volgt:</span><span class="sxs-lookup"><span data-stu-id="070a5-173">Exit hello `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="070a5-174">Netwerkbeveiligingsgroep regels en firewall configureren</span><span class="sxs-lookup"><span data-stu-id="070a5-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="070a5-175">Nu dat MongoDB geïnstalleerd en wordt uitgevoerd is, opent u een poort in Windows Firewall zodat u tooMongoDB op afstand verbinding kan maken.</span><span class="sxs-lookup"><span data-stu-id="070a5-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span> <span data-ttu-id="070a5-176">toocreate een nieuwe regel voor binnenkomende verbindingen tooallow TCP-poort 27017, open een administratieve PowerShell-prompt en voert u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="070a5-176">toocreate a new inbound rule tooallow TCP port 27017, open an administrative PowerShell prompt and enter hello following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="070a5-177">U kunt ook Hallo regel maken met behulp van Hallo **Windows Firewall met geavanceerde beveiliging** grafisch beheerprogramma.</span><span class="sxs-lookup"><span data-stu-id="070a5-177">You can also create hello rule by using hello **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="070a5-178">Maak een nieuwe regel voor binnenkomende verbindingen tooallow TCP-poort 27017.</span><span class="sxs-lookup"><span data-stu-id="070a5-178">Create a new inbound rule tooallow TCP port 27017.</span></span>

<span data-ttu-id="070a5-179">Maak een Netwerkbeveiligingsgroep regel tooallow toegang tooMongoDB van buiten een bestaand virtueel netwerk van Azure-subnet Hallo indien nodig.</span><span class="sxs-lookup"><span data-stu-id="070a5-179">If needed, create a Network Security Group rule tooallow access tooMongoDB from outside of hello existing Azure virtual network subnet.</span></span> <span data-ttu-id="070a5-180">U kunt Hallo Netwerkbeveiligingsgroep regels maken met behulp van Hallo [Azure-portal](nsg-quickstart-portal.md) of [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="070a5-180">You can create hello Network Security Group rules by using hello [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="070a5-181">Net als bij Hallo Windows Firewall-regels, kunt u TCP-poort 27017 toohello virtuele netwerkinterface van de MongoDB-VM.</span><span class="sxs-lookup"><span data-stu-id="070a5-181">As with hello Windows Firewall rules, allow TCP port 27017 toohello virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="070a5-182">TCP-poort 27017 is Hallo standaardpoort die wordt gebruikt door MongoDB.</span><span class="sxs-lookup"><span data-stu-id="070a5-182">TCP port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="070a5-183">U kunt deze poort wijzigen met behulp van Hallo `--port` parameter bij het starten van `mongod.exe` handmatig of via een service.</span><span class="sxs-lookup"><span data-stu-id="070a5-183">You can change this port by using hello `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="070a5-184">Als u poort Hallo wijzigt, moet u ervoor dat tooupdate Hallo Windows Firewall- en Netwerkbeveiligingsgroep regels in de vorige stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="070a5-184">If you change hello port, make sure tooupdate hello Windows Firewall and Network Security Group rules in hello preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="070a5-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="070a5-185">Next steps</span></span>
<span data-ttu-id="070a5-186">In deze zelfstudie hebt u geleerd hoe tooinstall en MongoDB configureren op uw Windows-VM.</span><span class="sxs-lookup"><span data-stu-id="070a5-186">In this tutorial, you learned how tooinstall and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="070a5-187">U kunt nu toegang tot MongoDB op uw Windows-VM door na Hallo geavanceerde onderwerpen in Hallo [MongoDB-documentatie](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="070a5-187">You can now access MongoDB on your Windows VM, by following hello advanced topics in hello [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

