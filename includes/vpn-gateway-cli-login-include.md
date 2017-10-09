<span data-ttu-id="af3cc-101">Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="af3cc-101">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="af3cc-102">Zie [Aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) voor meer informatie over aanmelden.</span><span class="sxs-lookup"><span data-stu-id="af3cc-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

```azurecli
az login
```

<span data-ttu-id="af3cc-103">Als u meer dan één Azure-abonnement hebt, lijst Hallo abonnementen voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="af3cc-103">If you have more than one Azure subscription, list hello subscriptions for hello account.</span></span>

```azurecli
az account list --all
```

<span data-ttu-id="af3cc-104">Hallo-abonnement dat u wilt dat toouse opgeven.</span><span class="sxs-lookup"><span data-stu-id="af3cc-104">Specify hello subscription that you want toouse.</span></span>

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```