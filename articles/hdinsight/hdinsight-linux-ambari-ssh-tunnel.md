---
title: SSH-tunneling voor toegang tot Azure HDInsight gebruiken | Microsoft Docs
description: Informatie over het gebruik van een SSH-tunnel te zoeken veilig webbronnen gehost op uw HDInsight op basis van Linux-knooppunten.
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
ms.openlocfilehash: 4b606ea3797d685b9deacf72f1bd31e0ef007f98
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="6e131-103">SSH-Tunneling gebruiken voor toegang tot de Ambari-webgebruikersinterface, JobHistory, NameNode, Oozie en andere web-UI</span><span class="sxs-lookup"><span data-stu-id="6e131-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="6e131-104">Linux gebaseerde HDInsight-clusters bieden toegang tot de Ambari-webgebruikersinterface via Internet, maar sommige functies van de gebruikersinterface zijn niet.</span><span class="sxs-lookup"><span data-stu-id="6e131-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span></span> <span data-ttu-id="6e131-105">Bijvoorbeeld: de webgebruikersinterface voor andere services die via Ambari worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="6e131-105">For example, the web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="6e131-106">Voor volledige functionaliteit van de Ambari-webgebruikersinterface, moet u een SSH-tunnel naar de kop van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6e131-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="6e131-107">Waarom gebruikt een SSH-tunnel</span><span class="sxs-lookup"><span data-stu-id="6e131-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="6e131-108">Aantal van de menu's in Ambari werken alleen via een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="6e131-108">Several of the menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="6e131-109">Deze menu's zijn afhankelijk van websites en services worden uitgevoerd op andere knooppunttypen zoals worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="6e131-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="6e131-110">Deze websites zijn vaak niet beveiligd, zodat het is niet veilig om ze rechtstreeks op het internet weer te geven.</span><span class="sxs-lookup"><span data-stu-id="6e131-110">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span></span>

<span data-ttu-id="6e131-111">De volgende Web-UI vereisen een SSH-tunnel:</span><span class="sxs-lookup"><span data-stu-id="6e131-111">The following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="6e131-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="6e131-112">JobHistory</span></span>
* <span data-ttu-id="6e131-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="6e131-113">NameNode</span></span>
* <span data-ttu-id="6e131-114">Thread-Stacks</span><span class="sxs-lookup"><span data-stu-id="6e131-114">Thread Stacks</span></span>
* <span data-ttu-id="6e131-115">Oozie-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="6e131-115">Oozie web UI</span></span>
* <span data-ttu-id="6e131-116">HBase hoofd- en logboeken gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="6e131-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="6e131-117">Als u scriptacties gebruikt voor het aanpassen van uw cluster, vereisen geen services of hulpprogramma's die u installeert die een web-UI zichtbaar een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="6e131-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="6e131-118">Als u Hue met behulp van een scriptactie installeren, moet u een SSH-tunnel gebruiken voor toegang tot de Hue-webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="6e131-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e131-119">Als u directe toegang tot HDInsight via een virtueel netwerk hebt, hoeft u geen gebruik van SSH-tunnels.</span><span class="sxs-lookup"><span data-stu-id="6e131-119">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span></span> <span data-ttu-id="6e131-120">Zie voor een voorbeeld van rechtstreeks toegang hebben tot HDInsight via een virtueel netwerk, de [HDInsight verbinding maken met uw lokale netwerk](connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="6e131-120">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="6e131-121">Wat is een SSH-tunnel</span><span class="sxs-lookup"><span data-stu-id="6e131-121">What is an SSH tunnel</span></span>

<span data-ttu-id="6e131-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) verzonden naar een poort op uw lokale werkstation verkeer gerouteerd.</span><span class="sxs-lookup"><span data-stu-id="6e131-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation.</span></span> <span data-ttu-id="6e131-123">Het verkeer wordt gerouteerd via een SSH-verbinding met het hoofdknooppunt van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6e131-123">The traffic is routed through an SSH connection to your HDInsight cluster head node.</span></span> <span data-ttu-id="6e131-124">De aanvraag is opgelost, alsof deze afkomstig van het hoofdknooppunt is.</span><span class="sxs-lookup"><span data-stu-id="6e131-124">The request is resolved as if it originated on the head node.</span></span> <span data-ttu-id="6e131-125">Het antwoord wordt vervolgens doorgestuurd teruggestuurd via de tunnel naar uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="6e131-125">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e131-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6e131-126">Prerequisites</span></span>

* <span data-ttu-id="6e131-127">Een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="6e131-127">An SSH client.</span></span> <span data-ttu-id="6e131-128">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6e131-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="6e131-129">Een webbrowser die kan worden geconfigureerd om een proxy SOCKS5 te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6e131-129">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="6e131-130">De ondersteuning voor SOCKS-proxy is ingebouwd in Windows biedt geen ondersteuning voor SOCKS5 en werkt niet met de stappen in dit document.</span><span class="sxs-lookup"><span data-stu-id="6e131-130">The SOCKS proxy support built into Windows does not support SOCKS5, and does not work with the steps in this document.</span></span> <span data-ttu-id="6e131-131">De volgende browsers zijn afhankelijk van de proxy-instellingen voor Windows en op dit moment niet werken met de stappen in dit document:</span><span class="sxs-lookup"><span data-stu-id="6e131-131">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    >
    > * <span data-ttu-id="6e131-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="6e131-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="6e131-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="6e131-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="6e131-134">Google Chrome is ook afhankelijk van de proxy-instellingen van Windows.</span><span class="sxs-lookup"><span data-stu-id="6e131-134">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="6e131-135">U kunt echter de uitbreidingen die ondersteuning bieden voor SOCKS5 installeren.</span><span class="sxs-lookup"><span data-stu-id="6e131-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="6e131-136">Het is raadzaam [FoxyProxy standaard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="6e131-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="6e131-137"><a name="usessh"></a>Maken van een tunnel met behulp van de SSH-opdracht</span><span class="sxs-lookup"><span data-stu-id="6e131-137"><a name="usessh"></a>Create a tunnel using the SSH command</span></span>

<span data-ttu-id="6e131-138">Gebruik de volgende opdracht voor het maken van een SSH-tunnel met behulp van de `ssh` opdracht.</span><span class="sxs-lookup"><span data-stu-id="6e131-138">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="6e131-139">Vervang **gebruikersnaam** met een SSH-gebruiker voor uw HDInsight-cluster en vervang **CLUSTERNAME** met de naam van uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="6e131-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="6e131-140">Deze opdracht maakt u een verbinding die verkeer gerouteerd naar lokale poort 9876 aan het cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="6e131-140">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="6e131-141">De opties zijn:</span><span class="sxs-lookup"><span data-stu-id="6e131-141">The options are:</span></span>

* <span data-ttu-id="6e131-142">**D 9876** -de lokale poort waarmee verkeer via de tunnel.</span><span class="sxs-lookup"><span data-stu-id="6e131-142">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="6e131-143">**C** -alle gegevens te comprimeren omdat webverkeer voornamelijk tekst is.</span><span class="sxs-lookup"><span data-stu-id="6e131-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="6e131-144">**2** -force SSH protocol versie 2 alleen proberen.</span><span class="sxs-lookup"><span data-stu-id="6e131-144">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="6e131-145">**q** -stille modus.</span><span class="sxs-lookup"><span data-stu-id="6e131-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="6e131-146">**T** -toewijzing van de pseudo-tty uitschakelen omdat we zojuist een poort doorstuurt.</span><span class="sxs-lookup"><span data-stu-id="6e131-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="6e131-147">**n**-Voorkomen dat het lezen van STDIN, aangezien we zojuist een poort doorstuurt.</span><span class="sxs-lookup"><span data-stu-id="6e131-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="6e131-148">**N** -een externe opdracht niet uitvoeren omdat er slechts een poort doorstuurt.</span><span class="sxs-lookup"><span data-stu-id="6e131-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="6e131-149">**f** -op de achtergrond uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6e131-149">**f** - Run in the background.</span></span>

<span data-ttu-id="6e131-150">Zodra de opdracht is voltooid, wordt verkeer dat wordt verzonden naar poort 9876 op de lokale computer naar het hoofdknooppunt van het cluster gestuurd.</span><span class="sxs-lookup"><span data-stu-id="6e131-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span></span>

## <span data-ttu-id="6e131-151"><a name="useputty"></a>Maken van een tunnel met PuTTY</span><span class="sxs-lookup"><span data-stu-id="6e131-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="6e131-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) een grafische SSH-client voor Windows.</span><span class="sxs-lookup"><span data-stu-id="6e131-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="6e131-153">Gebruik de volgende stappen voor het maken van een SSH-tunnel met PuTTY:</span><span class="sxs-lookup"><span data-stu-id="6e131-153">Use the following steps to create an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="6e131-154">PuTTY opent en voert u de verbindingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="6e131-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="6e131-155">Als u niet bekend met PuTTY bent, raadpleegt u de [PuTTY-documentatie (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="6e131-155">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="6e131-156">In de **categorie** sectie aan de linkerkant van het dialoogvenster uit, vouw **verbinding**, vouw **SSH**, en selecteer vervolgens **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="6e131-156">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="6e131-157">Geef de volgende informatie op de **opties voor SSH-poort doorsturen** vorm:</span><span class="sxs-lookup"><span data-stu-id="6e131-157">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="6e131-158">**Bronpoort**: de poort op de client die u wilt doorsturen.</span><span class="sxs-lookup"><span data-stu-id="6e131-158">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="6e131-159">Bijvoorbeeld: **9876**.</span><span class="sxs-lookup"><span data-stu-id="6e131-159">For example, **9876**.</span></span>

   * <span data-ttu-id="6e131-160">**Bestemming** -de SSH-adres voor het Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6e131-160">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="6e131-161">Bijvoorbeeld **mijncluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="6e131-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="6e131-162">**Dynamisch**: hiermee schakelt u de dynamische routering van SOCKS-proxy's in.</span><span class="sxs-lookup"><span data-stu-id="6e131-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![afbeelding van de opties-tunneling](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="6e131-164">Klik op **toevoegen** toevoegen van de instellingen en klik vervolgens op **openen** een SSH-verbinding openen.</span><span class="sxs-lookup"><span data-stu-id="6e131-164">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="6e131-165">Wanneer u wordt gevraagd, moet u zich aanmelden bij de server.</span><span class="sxs-lookup"><span data-stu-id="6e131-165">When prompted, log in to the server.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="6e131-166">Gebruik de tunnel vanuit de browser</span><span class="sxs-lookup"><span data-stu-id="6e131-166">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e131-167">De stappen in deze sectie de Mozilla FireFox browser gebruiken, aangezien deze dezelfde proxyinstellingen voor alle platforms biedt.</span><span class="sxs-lookup"><span data-stu-id="6e131-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="6e131-168">Andere moderne browsers, zoals Google Chrome moet mogelijk een extensie zoals FoxyProxy werken met de tunnel.</span><span class="sxs-lookup"><span data-stu-id="6e131-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="6e131-169">Configureer de browser te gebruiken **localhost** en het maken van de poort die u hebt gebruikt toen de tunnel als een **SOCKS v5** proxy.</span><span class="sxs-lookup"><span data-stu-id="6e131-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="6e131-170">Hier ziet u hoe de instellingen van Firefox eruit.</span><span class="sxs-lookup"><span data-stu-id="6e131-170">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="6e131-171">Als u een andere poort dan 9876 gebruikt, moet u de poort wijzigen in het abonnement dat u gebruikt:</span><span class="sxs-lookup"><span data-stu-id="6e131-171">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![afbeelding van Firefox instellingen](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="6e131-173">Selecteren **externe DNS** wordt omgezet Domain Name System (DNS) aanvragen met behulp van het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6e131-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="6e131-174">Deze instelling wordt omgezet DNS met het hoofdknooppunt van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6e131-174">This setting resolves DNS using the head node of the cluster.</span></span>

2. <span data-ttu-id="6e131-175">Controleer of de tunnel werkt via een site, zoals [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="6e131-175">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="6e131-176">Het IP-adres geretourneerd moet één die wordt gebruikt door de Microsoft Azure-datacenter.</span><span class="sxs-lookup"><span data-stu-id="6e131-176">The IP returned should be one used by the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="6e131-177">Controleer met Ambari-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="6e131-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="6e131-178">Zodra het cluster is ingesteld, gebruikt u de volgende stappen uit om te controleren of u toegang web service UI van het Ambari Web tot:</span><span class="sxs-lookup"><span data-stu-id="6e131-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="6e131-179">Ga naar http://headnodehost:8080 in uw browser.</span><span class="sxs-lookup"><span data-stu-id="6e131-179">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="6e131-180">De `headnodehost` adres tot het cluster en los naar de headnode die Ambari op wordt uitgevoerd via de tunnel wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="6e131-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span></span> <span data-ttu-id="6e131-181">Wanneer u wordt gevraagd, typt u de beheerdersgebruikersnaam (admin) en het wachtwoord voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6e131-181">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="6e131-182">U wordt mogelijk gevraagd een tweede maal door de Ambari-webgebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="6e131-182">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="6e131-183">Als dit het geval is, voert u de gegevens opnieuw.</span><span class="sxs-lookup"><span data-stu-id="6e131-183">If so, reenter the information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6e131-184">Wanneer u het adres http://headnodehost:8080 verbinding maken met het cluster, wordt u verbinding maakt via de tunnel.</span><span class="sxs-lookup"><span data-stu-id="6e131-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span></span> <span data-ttu-id="6e131-185">Communicatie wordt beveiligd met behulp van de SSH-tunnel in plaats van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6e131-185">Communication is secured using the SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="6e131-186">Als u wilt verbinden via internet met behulp van HTTPS, gebruiken https://CLUSTERNAME.azurehdinsight.net, waarbij **CLUSTERNAME** is de naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6e131-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span></span>

2. <span data-ttu-id="6e131-187">Selecteer in de Ambari-Webgebruikersinterface HDFS uit de lijst aan de linkerkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="6e131-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>

    ![Afbeelding met HDFS geselecteerd](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="6e131-189">Wanneer de gegevens van de HDFS-service wordt weergegeven, selecteert u **snelkoppelingen**.</span><span class="sxs-lookup"><span data-stu-id="6e131-189">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="6e131-190">Er verschijnt een lijst met de hoofdknooppunten van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6e131-190">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="6e131-191">Selecteer een van de hoofdknooppunten en selecteer vervolgens **NameNode UI**.</span><span class="sxs-lookup"><span data-stu-id="6e131-191">Select one of the head nodes, and then select **NameNode UI**.</span></span>

    ![Afbeelding met het menu QuickLinks uitgevouwen](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="6e131-193">Wanneer u selecteert __snelkoppelingen__, krijgt u mogelijk een indicator wacht.</span><span class="sxs-lookup"><span data-stu-id="6e131-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="6e131-194">Dit probleem kan optreden als u een trage internetverbinding hebben.</span><span class="sxs-lookup"><span data-stu-id="6e131-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="6e131-195">Wacht enkele minuten duren om de gegevens te worden ontvangen van de server en probeer het opnieuw de lijst.</span><span class="sxs-lookup"><span data-stu-id="6e131-195">Wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   >
   > <span data-ttu-id="6e131-196">Sommige items in de **snelkoppelingen** menu worden afgekapt door aan de rechterkant van het scherm.</span><span class="sxs-lookup"><span data-stu-id="6e131-196">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="6e131-197">Zo ja, vouw het menu met de muis en pijl-rechts om te schuiven het scherm naar rechts om de rest van het menu te geven.</span><span class="sxs-lookup"><span data-stu-id="6e131-197">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>

4. <span data-ttu-id="6e131-198">Een pagina zoals in de volgende afbeelding wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="6e131-198">A page similar to the following image is displayed:</span></span>

    ![Afbeelding van de gebruikersinterface NameNode](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="6e131-200">U ziet de URL voor deze pagina. moet er ongeveer als **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="6e131-200">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="6e131-201">Deze URI met behulp van de interne volledig gekwalificeerde domeinnaam (FQDN) van het knooppunt en is alleen toegankelijk wanneer u een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="6e131-201">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e131-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e131-202">Next steps</span></span>

<span data-ttu-id="6e131-203">Nu dat u hebt geleerd hoe maken en gebruiken van een SSH-tunnel, Zie het volgende document voor andere manieren om te Ambari gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6e131-203">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span></span>

* [<span data-ttu-id="6e131-204">HDInsight-clusters beheren met Ambari</span><span class="sxs-lookup"><span data-stu-id="6e131-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="6e131-205">Zie voor meer informatie over het gebruik van SSH met HDInsight [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6e131-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

