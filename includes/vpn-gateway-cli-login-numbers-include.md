1. <span data-ttu-id="9446e-101">Meld u aan bij uw Azure-abonnement met de opdracht [az login](/cli/azure/#login) en volg de instructies op het scherm.</span><span class="sxs-lookup"><span data-stu-id="9446e-101">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> <span data-ttu-id="9446e-102">Zie [Aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) voor meer informatie over aanmelden.</span><span class="sxs-lookup"><span data-stu-id="9446e-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

  ```azurecli
  az login
  ```
2. <span data-ttu-id="9446e-103">Als u meer dan één Azure-abonnement hebt, worden alle abonnementen voor het account weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9446e-103">If you have more than one Azure subscription, list the subscriptions for the account.</span></span>

  ```azurecli
  az account list --all
  ```
3. <span data-ttu-id="9446e-104">Geef het abonnement op dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9446e-104">Specify the subscription that you want to use.</span></span>

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```