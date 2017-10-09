<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a>Voorbereiden voor updates
U moet tooperform Hallo volgende stappen uit voordat u het scannen en Hallo update toepassen:

1. Een cloud momentopname van Hallo apparaatgegevens.
2. Controleer of uw vaste IP-adressen controller routeerbaar zijn en toohello Internet in verbinding kunnen maken. Deze vaste IP-adressen worden gebruikt tooservice updates tooyour apparaat. U kunt dit testen door het uitvoeren van de volgende cmdlet op elke domeincontroller uit Windows PowerShell-interface van apparaat Hallo HALLO hallo:
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    **Voorbeelduitvoer voor Test-Connection wanneer vaste IP-adressen verbinding toohello Internet kunt maken**

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

Nadat u deze handmatig controles vooraf hebt voltooid, kunt u doorgaan tooscan en Hallo updates installeren.

