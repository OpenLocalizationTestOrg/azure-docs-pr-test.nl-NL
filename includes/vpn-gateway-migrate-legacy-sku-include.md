> [!NOTE]
> * Hallo VPN-gateway openbare IP-adres wordt gewijzigd wanneer u migreert van een oude SKU tooa nieuwe SKU.
> * U kunt geen klassieke VPN-gateways toohello migreren nieuwe SKU's. Klassieke VPN-gateways kunnen alleen gebruik Hallo oudere (oude) SKU's.
> 

U kan niet de grootte van uw Azure VPN gateways tussen Hallo oude SKU's en nieuwe SKU families Hallo. Als u VPN-gateways in Hallo Resource Manager-implementatiemodel die van de oudere versie Hallo Hallo SKU's gebruikmaken hebt, kunt u migreren toohello nieuwe SKU's. toomigrate, u Hallo bestaande VPN-gateway voor het virtuele netwerk verwijderen en vervolgens een nieuwe maken.

Migratiewerkstroom:

1. Verwijder de virtuele netwerkgateway van alle verbindingen-toohello.
2. Verwijder Hallo oude VPN-gateway.
3. Hallo nieuwe VPN-gateway maken.
4. Werk uw on-premises VPN-apparaten met Hallo nieuwe VPN-gateway IP-adres (voor Site-naar-Site-verbindingen).
5. Hallo gateway IP-adreswaarde voor alle lokale netwerkgateways van VNet-naar-VNet waarmee verbinding wordt gemaakt van de gateway toothis bijwerken.
6. Nieuwe client VPN-configuratie-pakketten voor P2S-clients verbinding maken met het virtuele netwerk toohello via deze VPN-gateway downloaden.
7. Maak opnieuw Hallo verbindingen toohello virtuele netwerkgateway.
