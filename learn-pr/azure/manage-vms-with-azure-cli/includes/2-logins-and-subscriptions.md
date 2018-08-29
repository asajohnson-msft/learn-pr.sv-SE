Innan vi börjar ska vi ta en titt på syntaxen för verktyget Azure CLI. Om du har gjort modulen **Control Azure services with the Azure CLI** (Kontrollera Azure-tjänster med Azure CLI) vet du att Azure CLI-kommandon antar formen:

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

`[command]` identifierar det specifika område av Azure du vill kontrollera. Du kan exempelvis hantera prenumerationsinformation med kommandot `account`, eller SQL-databaser med kommandot `sql`. `[subcommand]` och `[--parameters]` är sedan beroende av de kommandon du arbetar med. 

Du kan visa en lista över kommandon, underkommandon och parametrar genom att skriva ett partiellt kommando. Om du till exempel skriver `az` på kommandoraden ser du den översta hjälpskärmen, och om du skriver `az vm` får du alla underkommandon för virtuella datorer. Den här metoden kan vara ett bra sätt att utforska Azure CLI-verktyget.

> [!NOTE]
> Vi använder webbläsarbaserade Azure Cloud Shell för att arbeta med Azure CLI. Om du föredrar att arbeta på din lokala dator kan du även köra alla kommandon vi täcker från kommandoraden om du [installerar Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).

## <a name="log-in-to-azure"></a>Logga in på Azure

Det första du ska göra när du arbetar med Azure CLI är att logga in på ditt Azure-konto. Det gör du med kommandot `login`. Om du använder Cloud Shell finns det en knapp för att logga in på Azure.

```azurecli
az login
```

Kommandot öppnar ett webbläsarfönster och gör att du kan välja det Microsoft-konto du vill använda.

## <a name="working-with-subscriptions"></a>Arbeta med prenumerationer

I den här modulen arbetar vi i en tillfällig prenumeration som har skapats som en spelplan, men du använder vanligtvis en prenumeration från ditt eget konto. Om du har mer än en prenumeration kan du få en tydligt formaterad lista över prenumerationer med instruktionen `az account list --output table`.

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

Tänk på att kommandona även identifierar _standardprenumerationen_ där alla dina kommandon gäller. Om du föredrar att arbeta i en annan prenumeration kan du använda kommandot `az account set --subscription "[name]"`. Vi skulle exempelvis kunna ställa in vår aktuella prenumeration på `Visual Studio Enterprise` från listan ovan via följande kommando:

```azurecli
az account set --subscription "Visual Studio Enterprise"
```