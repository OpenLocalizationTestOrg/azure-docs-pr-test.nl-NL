---
title: aaaUse SSH tunneling tooaccess Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe een SSH-tunnel toosecurely toouse bladeren webbronnen gehost op uw HDInsight op basis van Linux-knooppunten.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="5377f-103">SSH-Tunneling tooaccess Ambari-webgebruikersinterface, JobHistory, NameNode, Oozie en andere web UI gebruiken</span><span class="sxs-lookup"><span data-stu-id="5377f-103">Use SSH Tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="5377f-104">Linux gebaseerde HDInsight-clusters bieden toegang tooAmbari webgebruikersinterface via Internet hello, maar sommige functies van Hallo gebruikersinterface zijn niet.</span><span class="sxs-lookup"><span data-stu-id="5377f-104">Linux-based HDInsight clusters provide access tooAmbari web UI over hello Internet, but some features of hello UI are not.</span></span> <span data-ttu-id="5377f-105">Bijvoorbeeld, Hallo-webgebruikersinterface voor andere services die via Ambari worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="5377f-105">For example, hello web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="5377f-106">Voor volledige functionaliteit van Hallo Ambari-webgebruikersinterface, moet u een SSH-tunnel toohello cluster head.</span><span class="sxs-lookup"><span data-stu-id="5377f-106">For full functionality of hello Ambari web UI, you must use an SSH tunnel toohello cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="5377f-107">Waarom gebruikt een SSH-tunnel</span><span class="sxs-lookup"><span data-stu-id="5377f-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="5377f-108">Een aantal menu's Hallo in Ambari werken alleen via een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="5377f-108">Several of hello menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="5377f-109">Deze menu's zijn afhankelijk van websites en services worden uitgevoerd op andere knooppunttypen zoals worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="5377f-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="5377f-110">Vaak deze websites zijn niet beveiligd, zodat het niet veilig toodirectly zichtbaar Hallo ze op internet.</span><span class="sxs-lookup"><span data-stu-id="5377f-110">Often, these web sites are not secured, so it is not safe toodirectly expose them on hello internet.</span></span>

<span data-ttu-id="5377f-111">Hallo Web UI na vereisen een SSH-tunnel:</span><span class="sxs-lookup"><span data-stu-id="5377f-111">hello following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="5377f-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="5377f-112">JobHistory</span></span>
* <span data-ttu-id="5377f-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="5377f-113">NameNode</span></span>
* <span data-ttu-id="5377f-114">Thread-Stacks</span><span class="sxs-lookup"><span data-stu-id="5377f-114">Thread Stacks</span></span>
* <span data-ttu-id="5377f-115">Oozie-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="5377f-115">Oozie web UI</span></span>
* <span data-ttu-id="5377f-116">HBase hoofd- en logboeken gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="5377f-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="5377f-117">Als u uw cluster scriptacties toocustomize gebruiken, vereisen geen services of hulpprogramma's die u installeert die een web-UI zichtbaar een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="5377f-117">If you use Script Actions toocustomize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="5377f-118">Bijvoorbeeld, als u Hue met behulp van een scriptactie installeren, moet u een SSH-tunnel tooaccess Hallo Hue-webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="5377f-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel tooaccess hello Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5377f-119">Als u directe toegang tooHDInsight via een virtueel netwerk hebt, hoeft u geen toouse SSH-tunnels.</span><span class="sxs-lookup"><span data-stu-id="5377f-119">If you have direct access tooHDInsight through a virtual network, you do not need toouse SSH tunnels.</span></span> <span data-ttu-id="5377f-120">Zie voor een voorbeeld van rechtstreeks toegang hebben tot HDInsight via een virtueel netwerk, Hallo [verbinding maken met HDInsight tooyour on-premises netwerk](connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="5377f-120">For an example of directly accessing HDInsight through a virtual network, see hello [Connect HDInsight tooyour on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="5377f-121">Wat is een SSH-tunnel</span><span class="sxs-lookup"><span data-stu-id="5377f-121">What is an SSH tunnel</span></span>

<span data-ttu-id="5377f-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) tooa poort verzonden op uw lokale werkstation verkeer gerouteerd.</span><span class="sxs-lookup"><span data-stu-id="5377f-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent tooa port on your local workstation.</span></span> <span data-ttu-id="5377f-123">Hallo-verkeer wordt gerouteerd via een SSH-verbinding tooyour HDInsight-cluster hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="5377f-123">hello traffic is routed through an SSH connection tooyour HDInsight cluster head node.</span></span> <span data-ttu-id="5377f-124">Hallo-aanvraag is opgelost, alsof deze afkomstig van het hoofdknooppunt Hallo is.</span><span class="sxs-lookup"><span data-stu-id="5377f-124">hello request is resolved as if it originated on hello head node.</span></span> <span data-ttu-id="5377f-125">antwoord Hallo wordt vervolgens doorgestuurd teruggestuurd via Hallo tunnel tooyour werkstation.</span><span class="sxs-lookup"><span data-stu-id="5377f-125">hello response is then routed back through hello tunnel tooyour workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5377f-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5377f-126">Prerequisites</span></span>

* <span data-ttu-id="5377f-127">Een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="5377f-127">An SSH client.</span></span> <span data-ttu-id="5377f-128">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5377f-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="5377f-129">Een webbrowser die kan worden geconfigureerd toouse SOCKS5 proxy.</span><span class="sxs-lookup"><span data-stu-id="5377f-129">A web browser that can be configured toouse a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="5377f-130">Hallo SOCKS-proxy-ondersteuning is ingebouwd in Windows biedt geen ondersteuning voor SOCKS5 en werkt niet met Hallo stappen in dit document.</span><span class="sxs-lookup"><span data-stu-id="5377f-130">hello SOCKS proxy support built into Windows does not support SOCKS5, and does not work with hello steps in this document.</span></span> <span data-ttu-id="5377f-131">Hallo volgende browsers zijn afhankelijk van de proxy-instellingen voor Windows, en niet op dit moment werken met Hallo stappen in dit document:</span><span class="sxs-lookup"><span data-stu-id="5377f-131">hello following browsers rely on Windows proxy settings, and do not currently work with hello steps in this document:</span></span>
    >
    > * <span data-ttu-id="5377f-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="5377f-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="5377f-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="5377f-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="5377f-134">Google Chrome is ook afhankelijk van Hallo Windows proxy-instellingen.</span><span class="sxs-lookup"><span data-stu-id="5377f-134">Google Chrome also relies on hello Windows proxy settings.</span></span> <span data-ttu-id="5377f-135">U kunt echter de uitbreidingen die ondersteuning bieden voor SOCKS5 installeren.</span><span class="sxs-lookup"><span data-stu-id="5377f-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="5377f-136">Het is raadzaam [FoxyProxy standaard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="5377f-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="5377f-137"><a name="usessh"></a>Hallo SSH-opdracht met een tunnel maken</span><span class="sxs-lookup"><span data-stu-id="5377f-137"><a name="usessh"></a>Create a tunnel using hello SSH command</span></span>

<span data-ttu-id="5377f-138">Gebruik Hallo volgende opdracht toocreate een SSH-tunnel met Hallo `ssh` opdracht.</span><span class="sxs-lookup"><span data-stu-id="5377f-138">Use hello following command toocreate an SSH tunnel using hello `ssh` command.</span></span> <span data-ttu-id="5377f-139">Vervang **gebruikersnaam** met een SSH-gebruiker voor uw HDInsight-cluster en vervang **CLUSTERNAME** met Hallo-naam van uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="5377f-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="5377f-140">Deze opdracht maakt u een verbinding die verkeer toolocal poort 9876 toohello cluster via SSH van routes.</span><span class="sxs-lookup"><span data-stu-id="5377f-140">This command creates a connection that routes traffic toolocal port 9876 toohello cluster over SSH.</span></span> <span data-ttu-id="5377f-141">Hallo-opties zijn:</span><span class="sxs-lookup"><span data-stu-id="5377f-141">hello options are:</span></span>

* <span data-ttu-id="5377f-142">**D 9876** -lokale poort waarmee verkeer via de tunnel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5377f-142">**D 9876** - hello local port that routes traffic through hello tunnel.</span></span>
* <span data-ttu-id="5377f-143">**C** -alle gegevens te comprimeren omdat webverkeer voornamelijk tekst is.</span><span class="sxs-lookup"><span data-stu-id="5377f-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="5377f-144">**2** -force SSH tootry protocolversie 2 alleen.</span><span class="sxs-lookup"><span data-stu-id="5377f-144">**2** - Force SSH tootry protocol version 2 only.</span></span>
* <span data-ttu-id="5377f-145">**q** -stille modus.</span><span class="sxs-lookup"><span data-stu-id="5377f-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="5377f-146">**T** -toewijzing van de pseudo-tty uitschakelen omdat we zojuist een poort doorstuurt.</span><span class="sxs-lookup"><span data-stu-id="5377f-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="5377f-147">**n**-Voorkomen dat het lezen van STDIN, aangezien we zojuist een poort doorstuurt.</span><span class="sxs-lookup"><span data-stu-id="5377f-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="5377f-148">**N** -een externe opdracht niet uitvoeren omdat er slechts een poort doorstuurt.</span><span class="sxs-lookup"><span data-stu-id="5377f-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="5377f-149">**f** -Hallo achtergrond uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5377f-149">**f** - Run in hello background.</span></span>

<span data-ttu-id="5377f-150">Zodra het Hallo-opdracht is voltooid, is verkeer dat wordt verzonden tooport 9876 op de lokale computer Hallo gerouteerde toohello cluster hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="5377f-150">Once hello command finishes, traffic sent tooport 9876 on hello local computer is routed toohello cluster head node.</span></span>

## <span data-ttu-id="5377f-151"><a name="useputty"></a>Maken van een tunnel met PuTTY</span><span class="sxs-lookup"><span data-stu-id="5377f-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="5377f-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) een grafische SSH-client voor Windows.</span><span class="sxs-lookup"><span data-stu-id="5377f-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="5377f-153">Hallo stappen toocreate na een SSH-tunnel met PuTTY gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5377f-153">Use hello following steps toocreate an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="5377f-154">PuTTY opent en voert u de verbindingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="5377f-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="5377f-155">Als u niet bekend met PuTTY bent, raadpleegt u Hallo [PuTTY-documentatie (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="5377f-155">If you are not familiar with PuTTY, see hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="5377f-156">In Hallo **categorie** sectie toohello links van dialoogvenster hello, vouw **verbinding**, vouw **SSH**, en selecteer vervolgens **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="5377f-156">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="5377f-157">Bieden de volgende informatie op Hallo Hallo **opties voor SSH-poort doorsturen** vorm:</span><span class="sxs-lookup"><span data-stu-id="5377f-157">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="5377f-158">**Bronpoort** -Hallo poort op de gewenste tooforward Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="5377f-158">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="5377f-159">Bijvoorbeeld: **9876**.</span><span class="sxs-lookup"><span data-stu-id="5377f-159">For example, **9876**.</span></span>

   * <span data-ttu-id="5377f-160">**Bestemming** -Hallo SSH-adres voor Hallo Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="5377f-160">**Destination** - hello SSH address for hello Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5377f-161">Bijvoorbeeld **mijncluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="5377f-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="5377f-162">**Dynamisch**: hiermee schakelt u de dynamische routering van SOCKS-proxy's in.</span><span class="sxs-lookup"><span data-stu-id="5377f-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![afbeelding van de opties-tunneling](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="5377f-164">Klik op **toevoegen** tooadd Hallo instellingen en klik vervolgens op **Open** tooopen een SSH-verbinding.</span><span class="sxs-lookup"><span data-stu-id="5377f-164">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>

5. <span data-ttu-id="5377f-165">Wanneer u wordt gevraagd, meld u bij toohello-server.</span><span class="sxs-lookup"><span data-stu-id="5377f-165">When prompted, log in toohello server.</span></span>

## <a name="use-hello-tunnel-from-your-browser"></a><span data-ttu-id="5377f-166">Hallo-tunnel vanuit de browser gebruiken</span><span class="sxs-lookup"><span data-stu-id="5377f-166">Use hello tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5377f-167">Hallo stappen in deze sectie gebruik Hallo Mozilla FireFox browser, aangezien deze Hallo dezelfde proxy-instellingen voor alle platforms biedt.</span><span class="sxs-lookup"><span data-stu-id="5377f-167">hello steps in this section use hello Mozilla FireFox browser, as it provides hello same proxy settings across all platforms.</span></span> <span data-ttu-id="5377f-168">Andere moderne browsers, zoals Google Chrome moet mogelijk een extensie zoals FoxyProxy toowork met Hallo-tunnel.</span><span class="sxs-lookup"><span data-stu-id="5377f-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy toowork with hello tunnel.</span></span>

1. <span data-ttu-id="5377f-169">Configureer Hallo browser toouse **localhost** en het Hallo-poort die u hebt gebruikt toen maken Hallo tunnel als een **SOCKS v5** proxy.</span><span class="sxs-lookup"><span data-stu-id="5377f-169">Configure hello browser toouse **localhost** and hello port you used when creating hello tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="5377f-170">Hier ziet u hoe Hallo Firefox instellingen eruit.</span><span class="sxs-lookup"><span data-stu-id="5377f-170">Here's what hello Firefox settings look like.</span></span> <span data-ttu-id="5377f-171">Als u een andere poort dan 9876 gebruikt, wijzigen Hallo poort toohello die u gebruikt:</span><span class="sxs-lookup"><span data-stu-id="5377f-171">If you used a different port than 9876, change hello port toohello one you used:</span></span>
   
    ![afbeelding van Firefox instellingen](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="5377f-173">Selecteren **externe DNS** wordt omgezet Domain Name System (DNS)-aanvragen via Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="5377f-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using hello HDInsight cluster.</span></span> <span data-ttu-id="5377f-174">Deze instelling wordt omgezet DNS met Hallo hoofdknooppunt van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="5377f-174">This setting resolves DNS using hello head node of hello cluster.</span></span>

2. <span data-ttu-id="5377f-175">Controleer of deze tunnel Hallo werkt via een site, zoals [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="5377f-175">Verify that hello tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="5377f-176">Hallo IP geretourneerd een dient te worden door Microsoft Azure-datacenter Hallo.</span><span class="sxs-lookup"><span data-stu-id="5377f-176">hello IP returned should be one used by hello Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="5377f-177">Controleer met Ambari-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="5377f-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="5377f-178">Zodra het Hallo-cluster is ingesteld, gebruikt u hello te volgen stappen tooverify dat u service-web UI vanaf Hallo Ambari Web openen kunt:</span><span class="sxs-lookup"><span data-stu-id="5377f-178">Once hello cluster has been established, use hello following steps tooverify that you can access service web UIs from hello Ambari Web:</span></span>

1. <span data-ttu-id="5377f-179">Ga in uw browser toohttp://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="5377f-179">In your browser, go toohttp://headnodehost:8080.</span></span> <span data-ttu-id="5377f-180">Hallo `headnodehost` adres wordt verzonden via Hallo tunnel toohello cluster en toohello headnode die Ambari wordt uitgevoerd op te lossen.</span><span class="sxs-lookup"><span data-stu-id="5377f-180">hello `headnodehost` address is sent over hello tunnel toohello cluster and resolve toohello headnode that Ambari is running on.</span></span> <span data-ttu-id="5377f-181">Wanneer u wordt gevraagd, typt u Hallo-beheerdersgebruikersnaam (admin) en het wachtwoord voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="5377f-181">When prompted, enter hello admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="5377f-182">U wordt mogelijk gevraagd een tweede maal door Hallo Ambari-webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="5377f-182">You may be prompted a second time by hello Ambari web UI.</span></span> <span data-ttu-id="5377f-183">Als dit het geval is, voert u Hallo gegevens opnieuw.</span><span class="sxs-lookup"><span data-stu-id="5377f-183">If so, reenter hello information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5377f-184">Wanneer u Hallo http://headnodehost:8080 adres tooconnect toohello cluster gebruikt, wordt u verbinding maakt via Hallo-tunnel.</span><span class="sxs-lookup"><span data-stu-id="5377f-184">When using hello http://headnodehost:8080 address tooconnect toohello cluster, you are connecting through hello tunnel.</span></span> <span data-ttu-id="5377f-185">Communicatie wordt beveiligd met Hallo SSH-tunnel in plaats van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5377f-185">Communication is secured using hello SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="5377f-186">tooconnect meer dan Hallo internet met behulp van HTTPS, gebruikt u https://CLUSTERNAME.azurehdinsight.net, waarbij **CLUSTERNAME** Hallo-naam van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="5377f-186">tooconnect over hello internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of hello cluster.</span></span>

2. <span data-ttu-id="5377f-187">Selecteer in de lijst Hallo op Hallo links van de pagina Hallo Hallo Ambari-Webgebruikersinterface, HDFS.</span><span class="sxs-lookup"><span data-stu-id="5377f-187">From hello Ambari Web UI, select HDFS from hello list on hello left of hello page.</span></span>

    ![Afbeelding met HDFS geselecteerd](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="5377f-189">Wanneer Hallo HDFS-service-informatie wordt weergegeven, selecteert u **snelkoppelingen**.</span><span class="sxs-lookup"><span data-stu-id="5377f-189">When hello HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="5377f-190">Een lijst van head clusterknooppunten hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5377f-190">A list of hello cluster head nodes appears.</span></span> <span data-ttu-id="5377f-191">Selecteer een van de hoofdknooppunten Hallo en selecteer vervolgens **NameNode UI**.</span><span class="sxs-lookup"><span data-stu-id="5377f-191">Select one of hello head nodes, and then select **NameNode UI**.</span></span>

    ![De installatiekopie met de Hallo QuickLinks menu uitgevouwen](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="5377f-193">Wanneer u selecteert __snelkoppelingen__, krijgt u mogelijk een indicator wacht.</span><span class="sxs-lookup"><span data-stu-id="5377f-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="5377f-194">Dit probleem kan optreden als u een trage internetverbinding hebben.</span><span class="sxs-lookup"><span data-stu-id="5377f-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="5377f-195">Wacht een minuut of twee Hallo gegevens toobe ontvangen van Hallo-server en probeer het opnieuw Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="5377f-195">Wait a minute or two for hello data toobe received from hello server, then try hello list again.</span></span>
   >
   > <span data-ttu-id="5377f-196">Een aantal invoergegevens in Hallo **snelkoppelingen** menu kan worden genegeerd door de rechterkant Hallo van welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="5377f-196">Some entries in hello **Quick Links** menu may be cut off by hello right side of hello screen.</span></span> <span data-ttu-id="5377f-197">Zo ja, vouw Hallo menu met de muis en gebruiken van Hallo pijl naar rechts sleutel tooscroll Hallo scherm toohello juiste toosee Hallo rest van Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="5377f-197">If so, expand hello menu using your mouse and use hello right arrow key tooscroll hello screen toohello right toosee hello rest of hello menu.</span></span>

4. <span data-ttu-id="5377f-198">Een pagina vergelijkbaar toohello volgende afbeelding wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5377f-198">A page similar toohello following image is displayed:</span></span>

    ![Afbeelding van Hallo NameNode UI](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="5377f-200">Let op Hallo-URL voor deze pagina. moet vergelijkbaar te**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="5377f-200">Notice hello URL for this page; it should be similar too**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="5377f-201">Deze URI gebruikt Hallo interne volledig gekwalificeerde domeinnaam (FQDN) van Hallo-knooppunt en is alleen toegankelijk wanneer u een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="5377f-201">This URI is using hello internal fully qualified domain name (FQDN) of hello node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5377f-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5377f-202">Next steps</span></span>

<span data-ttu-id="5377f-203">U hebt geleerd hoe toocreate en gebruikt een SSH-tunnel Hallo volgende document voor andere manieren toouse Ambari zien:</span><span class="sxs-lookup"><span data-stu-id="5377f-203">Now that you have learned how toocreate and use an SSH tunnel, see hello following document for other ways toouse Ambari:</span></span>

* [<span data-ttu-id="5377f-204">HDInsight-clusters beheren met Ambari</span><span class="sxs-lookup"><span data-stu-id="5377f-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="5377f-205">Zie voor meer informatie over het gebruik van SSH met HDInsight [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5377f-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

