

1. Start op uw Mac **Sleutelhangertoegang**. Op Hallo onder navigatiebalk links **categorie**Open **mijn certificaten**. Hallo SSL-certificaat die u hebt gedownload in de vorige sectie Hallo vinden en de inhoud ervan worden vermeld. Alleen Hallo certificaat selecteren (geen selecteert Hallo persoonlijke sleutel), en [exporteren](https://support.apple.com/kb/PH20122?locale=en_US).
2. In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **door alles bladeren** > **App Services**, en klikt u op uw back-end van Mobile Apps. Onder **instellingen**, klikt u op **App Service-Push**, en klik vervolgens op de naam van uw notification hub. Ga te**Apple Push Notification Services** > **certificaat uploaden**. Hallo .p12-bestand, Hallo juist selecteren uploaden **modus** (afhankelijk van of uw SSL-clientcertificaat uit eerder is productie of sandbox). Eventuele wijzigingen worden opgeslagen.

De service is nu geconfigureerd toowork met pushmeldingen in iOS.

[1]: ./media/app-service-mobile-apns-configure-push/mobile-push-notification-hub.png
