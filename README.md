# Azure_SDK_Sample7_Accessing_with_StorageAccountKey

## 1. Get the Azure Storage account key

![image](https://github.com/luiscoco/Azure_SDK_Sample7_Accessing_with_StorageAccountKey/assets/32194879/7522a8e5-ac01-4e0d-a7fc-5634c84e580a)

## 2. Create the C# console application to access the Azure storage account and the blobs inside it

```csharp
using Azure;
using Azure.Identity;
using Azure.Storage.Blobs;

string accountName = "mystorageaccount222222";
string accountKey = "vxZ94bnw0o/7sceGBFhlSEce4hVPcgWNUQldg1qpNdtzn8JzoI0M5EhaDPVIVw1sYBriZ/VZALhz+AStaDWEnw=="; // Replace with your actual storage account key

string connectionString = $"DefaultEndpointsProtocol=https;AccountName={accountName};AccountKey={accountKey};EndpointSuffix=core.windows.net";
BlobServiceClient client = new BlobServiceClient(connectionString);

List<string> containerNames = await GetBlobContainers(client);

Console.WriteLine("Blob Containers:");
foreach (var containerName in containerNames)
{
    Console.WriteLine(containerName);
}

static async Task<List<string>> GetBlobContainers(BlobServiceClient blobServiceClient)
{
    var containerNames = new List<string>();

    await foreach (var containerItem in blobServiceClient.GetBlobContainersAsync())
    {
        containerNames.Add(containerItem.Name);
    }

    return containerNames;
}
```
