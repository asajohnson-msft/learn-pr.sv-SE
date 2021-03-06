<!--TODO: explain Etag in knowledge needed-->

När anslutningen till Azure Cosmos DB väl har upprättats är nästa steg att skapa, läsa, ersätta och ta bort dokument som lagras i databasen. I det här momentet skapar du användardokument i WebCustomer-samlingen. Sedan kan du hämta dem via ID, ersätta dem och ta bort dem.

## <a name="working-with-documents-programmatically"></a>Arbeta programmatiskt med dokument

Data lagras i JSON-dokument i Azure Cosmos DB. [Dokument](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) kan skapas, hämtas, ersättas och tas bort i portalen, som du såg i föregående modul. I den här modulen beskrivs hur du gör det programmässigt. Azure Cosmos DB har SDK:er på klientsidan för .NET, .NET Core, Java, Node.js och Python. De har alla stöd för de här åtgärderna. I den här modulen kommer vi att använda SDK:n för .NET Core till att skapa, hämta, uppdatera och ta bort NoSQL-data som lagras på Azure Cosmos DB.

De viktigaste åtgärderna för Azure Cosmos DB-dokument ingår i klassen [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet):
* [CreateDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [ReadDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [ReplaceDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* [UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet). Upsert skapar eller byter ut beroende på om dokumentet redan finns.
* [DeleteDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

Om du vill utföra någon av de här åtgärderna måste du skapa en klass som representerar objektet som lagras i databasen. Eftersom vi arbetar med en databas med användare kan du skapa klassen **User** (Användare) för att lagra viktiga data som förnamn, efternamn och användar-ID (obligatoriskt eftersom det är partitionsnyckeln som möjliggör horisontell skalning) och underklasser för leveransinställningar och orderhistorik.

När du har skapat de här klasserna för dina användare skapar du nya användardokument för varje instans. Sedan ska vi utföra några enkla åtgärder på dokumenten.

## <a name="create-documents"></a>Skapa dokument

1. Skapa först en **User**-klass som representerar objekten som ska lagras i Azure Cosmos DB. Vi skapar också underklasserna **OrderHistory** och **ShippingPreference** som används i klassen **User**. Observera att dokument måste ha en **id**-egenskap serialiserad som **id** i JSON.

    Du kan skapa dem genom att kopiera och klistra in koden för **användaren**, **OrderHistory** och **ShippingPreference** under metoden **BasicOperations**.

    ```csharp
    public class User
    {
        [JsonProperty("id")]
        public string Id { get; set; }
        [JsonProperty("userId")]
        public string UserId { get; set; }
        [JsonProperty("lastName")]
        public string LastName { get; set; }
        [JsonProperty("firstName")]
        public string FirstName { get; set; }
        [JsonProperty("email")]
        public string Email { get; set; }
        [JsonProperty("dividend")]
        public string Dividend { get; set; }
        [JsonProperty("OrderHistory")]
        public OrderHistory[] OrderHistory { get; set; }
        [JsonProperty("ShippingPreference")]
        public ShippingPreference[] ShippingPreference { get; set; }
        [JsonProperty("CouponsUsed")]
        public CouponsUsed[] Coupons { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class OrderHistory
    {
        public string OrderId { get; set; }
        public string DateShipped { get; set; }
        public string Total { get; set; }
    }

    public class ShippingPreference
    {
        public int Priority { get; set; }
        public string AddressLine1 { get; set; }
        public string AddressLine2 { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string ZipCode { get; set; }
        public string Country { get; set; }
    }

    public class CouponsUsed
    {
        public string CouponCode { get; set; }

    }

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }
    ```

1. Ange följande kommando för att köra programmet i den integrerade terminalen och kontrollera att det körs.

    ```csharp
    dotnet run
    ```

1. Kopiera och klistra in uppgiften **CreateUserDocumentIfNotExists** under funktionen **WriteToConsoleAndPromptToContinue** i slutet av filen Program.cs.

    ```csharp
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("User {0} already exists in the database", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), user);
                this.WriteToConsoleAndPromptToContinue("Created User {0}", user.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. Gå sedan tillbaka till metoden **BasicOperations** och lägg till följande i slutet av metoden.

    ```csharp
    User yanhe = new User
    {
        Id = "1",
        UserId = "yanhe",
        LastName = "He",
        FirstName = "Yan",
        Email = "yanhe@contoso.com",
        OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1000",
                    DateShipped = "08/17/2018",
                    Total = "52.49"
                }
            },
            ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "90 W 8th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", yanhe);

    User nelapin = new User
    {
        Id = "2",
        UserId = "nelapin",
        LastName = "Pindakova",
        FirstName = "Nela",
        Email = "nelapin@contoso.com",
        Dividend = "8.50",
        OrderHistory = new OrderHistory[]
        {
            new OrderHistory {
                OrderId = "1001",
                DateShipped = "08/17/2018",
                Total = "105.89"
            }
        },
         ShippingPreference = new ShippingPreference[]
        {
            new ShippingPreference {
                    Priority = 1,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            },
            new ShippingPreference {
                    Priority = 2,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            }
        },
        Coupons = new CouponsUsed[]
        {
            new CouponsUsed{
                CouponCode = "Fall2018"
            }
        }
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);
    ```

1. Ange återigen följande kommando i den integrerade terminalen för att köra programmet.

    ```csharp
    dotnet run
    ```

    Terminalen visar utdata efter hand som programmet skapar varje nytt användardokument. Tryck på valfri tangent för att slutföra programmet.

    ```output
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a>Läsa dokument

1. Om du vill läsa dokument från databasen kopierar du följande kod och placerar den efter metoden WriteToConsoleAndPromptToContinue i filen Program.cs.

    ```csharp
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("Read user {0}", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not read", user.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. Kopiera och klistra in följande kod i slutet av metoden **BasicOperations**, efter raden `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

1. Ange följande kommando i den integrerade terminalen för att köra programmet.

    ```bash
    dotnet run
    ```

    Du ser följande utdata i terminalen, och ”Read user 1” innebär att dokumentet hämtades.

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a>Ersätta dokument

Azure Cosmos DB har stöd för ersättning av JSON-dokument. I det här fallet ska vi uppdatera en användarpost eftersom efternamnet har ändrats.

1. Kopiera och klistra in metoden **ReplaceFamilyDocument** efter metoden ReadUserDocument i slutet av filen Program.cs.

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, User updatedUser)
    {
        try
        {
            await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, updatedUser.Id), updatedUser, new RequestOptions { PartitionKey = new PartitionKey(updatedUser.UserId) });
            this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", updatedUser.LastName);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for replacement", updatedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. Kopiera och klistra in följande kod i slutet av metoden **BasicOperations**, efter raden `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);`.

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe);
    ```

1. Kör följande kommando i den integrerade terminalen.

    ```bash
    dotnet run
    ```
    Du ser följande utdata i terminalen, och ”Replaced last name for Suh” innebär att dokumentet ersattes.

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    Replaced last name for Suh
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a>Ta bort dokument

1. Kopiera och klistra in metoden **DeleteUserDocument** under metoden **ReplaceUserDocument**.

    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, User deletedUser)
    {
        try
        {
            await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, deletedUser.Id), new RequestOptions { PartitionKey = new PartitionKey(deletedUser.UserId) });
            Console.WriteLine("Deleted user {0}", deletedUser.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for deletion", deletedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. Kopiera och klistra in följande kod i slutet av metoden **BasicOperations**.

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", yanhe);
    ```

1. Kör följande kommando i den integrerade terminalen.

    ```bash
    dotnet run
    ```

    Du ser följande utdata i terminalen, och ”Deleted user 1” innebär att dokumentet togs bort.

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    Replaced last name for Suh
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    Deleted user 1
    End of demo, press any key to exit.
    ```

I den här utbildningsenheten har du skapat, ersatt och tagit bort dokument i din Azure Cosmos DB-databas.
