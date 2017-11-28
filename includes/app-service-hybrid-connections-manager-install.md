
1. <span data-ttu-id="3fe3a-101">In de **hybride verbindingen** blade, klikt u op de hybride verbinding die u zojuist hebt gemaakt en klik op **Listener Setup**.</span><span class="sxs-lookup"><span data-stu-id="3fe3a-101">In the **Hybrid connections** blade, click the hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Klik op Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="3fe3a-103">De **hybride verbindingseigenschappen** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="3fe3a-103">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="3fe3a-104">Onder **On-premises hybride Verbindingsbeheer**, kies **handmatig downloaden en configureren**, sla het gedownloade pakket van HybridConnectionManager.msi en kopieer de verbindingsreeks voor de gateway.</span><span class="sxs-lookup"><span data-stu-id="3fe3a-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save the downloaded HybridConnectionManager.msi package, and copy the gateway connection string.</span></span>
   
    ![Klik hier om te installeren](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="3fe3a-106">Typ de volgende opdracht om het installatieprogramma starten vanaf een beheerdersopdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="3fe3a-106">From an administrator command prompt, type the following command to start the installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="3fe3a-107">Nadat het installatieprogramma wordt uitgevoerd, klikt u op **niet nu**, bladert u naar de map %ProgramFiles%\Microsoft\HybridConnectionManager, HCMConfigWizard.exe uitvoeren en klik op **Ja** in de **gebruikersaccount Besturingselement** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3fe3a-107">After the installer runs, click **Not now**, then browse to the %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in the **User Account Control** dialog.</span></span>
5. <span data-ttu-id="3fe3a-108">Plak de verbindingsreeks voor hybride die u eerder hebt gekopieerd en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3fe3a-108">Paste the hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Installeren](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="3fe3a-110">Wanneer de installatie is voltooid, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="3fe3a-110">When the install completes, click **Close**.</span></span>
   
    ![Klik op sluiten](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="3fe3a-112">Op de **hybride verbindingen** blade de **Status** kolom ziet u nu **verbonden**.</span><span class="sxs-lookup"><span data-stu-id="3fe3a-112">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Status verbonden](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

