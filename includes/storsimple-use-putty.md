<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a><span data-ttu-id="584dc-101">tooconnect via de seriële console Hallo</span><span class="sxs-lookup"><span data-stu-id="584dc-101">tooconnect through hello serial console</span></span>
1. <span data-ttu-id="584dc-102">Sluit de seriële kabel toohello-apparaat (rechtstreeks of via een USB-seriële adapter).</span><span class="sxs-lookup"><span data-stu-id="584dc-102">Connect your serial cable toohello device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="584dc-103">Open Hallo **Configuratiescherm**, en open vervolgens Hallo **Apparaatbeheer**.</span><span class="sxs-lookup"><span data-stu-id="584dc-103">Open hello **Control Panel**, and then open hello **Device Manager**.</span></span>
3. <span data-ttu-id="584dc-104">Hallo COM-poort herkennen zoals weergegeven in de volgende illustratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="584dc-104">Identify hello COM port as shown in hello following illustration.</span></span>
   
     ![Verbinding maken via een seriële console](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="584dc-106">Start PuTTY.</span><span class="sxs-lookup"><span data-stu-id="584dc-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="584dc-107">Wijzig in het rechterdeelvenster Hallo Hallo **verbindingstype** te**seriële**.</span><span class="sxs-lookup"><span data-stu-id="584dc-107">In hello right pane, change hello **Connection type** too**Serial**.</span></span>
6. <span data-ttu-id="584dc-108">Typ in het rechterdeelvenster Hallo Hallo juiste COM-poort.</span><span class="sxs-lookup"><span data-stu-id="584dc-108">In hello right pane, type hello appropriate COM port.</span></span> <span data-ttu-id="584dc-109">Zorg ervoor dat de Hallo seriële configuratieparameters als volgt zijn ingesteld:</span><span class="sxs-lookup"><span data-stu-id="584dc-109">Make sure that hello serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="584dc-110">Snelheid: 115.200</span><span class="sxs-lookup"><span data-stu-id="584dc-110">Speed: 115,200</span></span>
   * <span data-ttu-id="584dc-111">Gegevensbits: 8</span><span class="sxs-lookup"><span data-stu-id="584dc-111">Data bits: 8</span></span>
   * <span data-ttu-id="584dc-112">Stopbits: 1</span><span class="sxs-lookup"><span data-stu-id="584dc-112">Stop bits: 1</span></span>
   * <span data-ttu-id="584dc-113">Pariteit: Geen</span><span class="sxs-lookup"><span data-stu-id="584dc-113">Parity: None</span></span>
   * <span data-ttu-id="584dc-114">Datatransportbesturing: Geen</span><span class="sxs-lookup"><span data-stu-id="584dc-114">Flow control: None</span></span>
     
     <span data-ttu-id="584dc-115">Deze instellingen worden weergegeven in de volgende illustratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="584dc-115">These settings are shown in hello following illustration.</span></span>
     
     ![Instellingen voor PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="584dc-117">Als Hallo standaard instelling voor datatransportbesturing niet werkt, kunt u Hallo flow control tooXON/XOFF.</span><span class="sxs-lookup"><span data-stu-id="584dc-117">If hello default flow control setting does not work, try setting hello flow control tooXON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="584dc-118">Klik op **Open** toostart een seriële sessie.</span><span class="sxs-lookup"><span data-stu-id="584dc-118">Click **Open** toostart a serial session.</span></span>

