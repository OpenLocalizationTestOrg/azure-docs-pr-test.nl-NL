Hallo Mobile Apps-functie van Azure App Service gebruikt [Azure Notification Hubs] toosend pushes, zodat u een notification hub voor uw mobiele app configureren.

1. In Hallo [Azure-portal], gaat u te**App Services**, en klik vervolgens op de back-end van uw app. Onder **instellingen**, klikt u op **Push**.
2. Klik op **Connect** tooadd een notification hub resource toohello app. U kunt een hub maken of tooan een bestaande verbinding.

    ![](./media/app-service-mobile-create-notification-hub/configure-hub-flow.png)

U hebt nu een notification hub tooyour Mobile Apps back-end-project gekoppeld. U kunt deze notification hub tooconnect tooa platform notification system (PNS) toopush toodevices later wilt configureren.

[Azure-portal]: https://portal.azure.com/
[Azure Notification Hubs]: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-push-notification-overview/
