
1. <span data-ttu-id="280db-101">In Hallo **hybride verbindingen** blade Hallo hybride verbinding die u zojuist hebt gemaakt, klik op **Listener Setup**.</span><span class="sxs-lookup"><span data-stu-id="280db-101">In hello **Hybrid connections** blade, click hello hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Klik op Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="280db-103">Hallo **hybride verbindingseigenschappen** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="280db-103">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="280db-104">Onder **On-premises hybride Verbindingsbeheer**, kies **handmatig downloaden en configureren**Hallo gedownload HybridConnectionManager.msi pakket opslaan en kopieer Hallo gateway-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="280db-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save hello downloaded HybridConnectionManager.msi package, and copy hello gateway connection string.</span></span>
   
    ![Klik hier tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="280db-106">Type Hallo volgende opdracht vanaf een beheerdersopdrachtprompt toostart Hallo installatieprogramma:</span><span class="sxs-lookup"><span data-stu-id="280db-106">From an administrator command prompt, type hello following command toostart hello installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="280db-107">Na het Hallo-installatieprogramma wordt uitgevoerd, klikt u op **niet nu**, bladert u toohello %ProgramFiles%\Microsoft\HybridConnectionManager map, HCMConfigWizard.exe uitvoeren en klik op **Ja** in Hallo **gebruiker Besturingselement account** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="280db-107">After hello installer runs, click **Not now**, then browse toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in hello **User Account Control** dialog.</span></span>
5. <span data-ttu-id="280db-108">Plak de verbindingsreeks van het Hallo-hybride die u eerder hebt gekopieerd en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="280db-108">Paste hello hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Installeren](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="280db-110">Wanneer het Hallo-installatie is voltooid, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="280db-110">When hello install completes, click **Close**.</span></span>
   
    ![Klik op sluiten](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="280db-112">Op Hallo **hybride verbindingen** blade, Hallo **Status** kolom ziet u nu **verbonden**.</span><span class="sxs-lookup"><span data-stu-id="280db-112">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Status verbonden](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

