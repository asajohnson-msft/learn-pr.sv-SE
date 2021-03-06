Nu när du har lärt dig om vilka typer av frågor du kan skapa ska vi använda Datautforskaren i Azure-portalen för att hämta och filtrera dina produktdata.

Observera i fönstret för Datautforskaren att frågan på fliken **Dokument** som standard är inställd på `SELECT * FROM c` enligt vad som visas på följande bild. Den här standardfrågan hämtar och visar alla dokument i samlingen.

![Standardfrågan i Datautforskaren är SELECT * FROM c](../media/5-azure-cosmosdb-data-explorer-query.png)

## <a name="create-a-new-query"></a>Skapa en ny fråga

1. I datautforskaren klickar du på fliken **Ny SQL-fråga**. Observera att standardfrågan för fliken för nya **Fråga 1** åter är `SELECT * from c`, vilket returnerar alla dokument i samlingen. 

1. Klicka på **Kör fråga**. Frågan returnerar alla resultat i databasen.

    ![Ändra standardfrågan genom att lägga till ORDER BY c._ts DESC och klicka på Tillämpa filter](../media/5-azure-cosmosdb-data-explorer-edit-query.png)

2. Nu ska vi köra några av frågorna som diskuterades i föregående kursdel. Ta bort `SELECT * from c` på frågefliken, kopiera och klistra in följande fråga och klicka sedan på **Kör fråga**:

    ```sql
    SELECT * 
    FROM Products p 
    WHERE p.id ="1"
    ```

    Resultaten returnerar produkten vars `productId` är 1.

    ![Fråga efter ett ID för 1](../media/5-azure-cosmosdb-data-explorer-query-by-id.png)

3. Ta bort den föregående frågan, kopiera och klistra in följande fråga, och klicka på **Kör fråga**. Den här frågan returnerar pris, beskrivning och produkt-ID för alla produkter, ordnade efter pris i stigande ordning.
 
    ```sql
    SELECT p.price, p.description, p.productId 
    FROM Products p 
    ORDER BY p.price ASC
    ```

## <a name="summary"></a>Sammanfattning

Nu har du slutfört några grundläggande frågor på dina data i Azure Cosmos DB. 