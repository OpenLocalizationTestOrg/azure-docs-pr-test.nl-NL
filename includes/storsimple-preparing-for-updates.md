<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="816ca-101">Voorbereiden voor updates</span><span class="sxs-lookup"><span data-stu-id="816ca-101">Preparing for updates</span></span>
<span data-ttu-id="816ca-102">U moet tooperform Hallo volgende stappen uit voordat u het scannen en Hallo update toepassen:</span><span class="sxs-lookup"><span data-stu-id="816ca-102">You will need tooperform hello following steps before you scan and apply hello update:</span></span>

1. <span data-ttu-id="816ca-103">Een cloud momentopname van Hallo apparaatgegevens.</span><span class="sxs-lookup"><span data-stu-id="816ca-103">Take a cloud snapshot of hello device data.</span></span>
2. <span data-ttu-id="816ca-104">Controleer of uw vaste IP-adressen controller routeerbaar zijn en toohello Internet in verbinding kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="816ca-104">Ensure that your controller fixed IPs are routable and can connect toohello Internet.</span></span> <span data-ttu-id="816ca-105">Deze vaste IP-adressen worden gebruikt tooservice updates tooyour apparaat.</span><span class="sxs-lookup"><span data-stu-id="816ca-105">These fixed IPs will be used tooservice updates tooyour device.</span></span> <span data-ttu-id="816ca-106">U kunt dit testen door het uitvoeren van de volgende cmdlet op elke domeincontroller uit Windows PowerShell-interface van apparaat Hallo HALLO hallo:</span><span class="sxs-lookup"><span data-stu-id="816ca-106">You can test this by running hello following cmdlet on each controller from hello Windows PowerShell interface of hello device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="816ca-107">**Voorbeelduitvoer voor Test-Connection wanneer vaste IP-adressen verbinding toohello Internet kunt maken**</span><span class="sxs-lookup"><span data-stu-id="816ca-107">**Sample output for Test-Connection when fixed IPs can connect toohello Internet**</span></span>

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

<span data-ttu-id="816ca-108">Nadat u deze handmatig controles vooraf hebt voltooid, kunt u doorgaan tooscan en Hallo updates installeren.</span><span class="sxs-lookup"><span data-stu-id="816ca-108">After you have successfully completed these manual pre-checks, you can proceed tooscan and install hello updates.</span></span>

