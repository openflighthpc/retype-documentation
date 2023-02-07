---
order: 
label: Import Flight Solo Image to Azure
icon: dot
---

Several different cloud hosting services can use the downloaded Flight Solo image. This page shall describe how to do it with Azure. This only needs to be done once, and then the imported image can be used any number of times.

1. Start by installing the [Azure Command Line Interface(CLI)](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli), as using it is the simplest way to import a raw image. Alternatively you can follow these instructions on the [Azure Cloud Shell](https://learn.microsoft.com/en-us/azure/cloud-shell/overview)

2. Get the Flight Solo image from [here](/cluster_build_methods/what_is_flight_solo/#where-can-i-download-flight-solo)


3. If you don't already have one, create a storage account:

```
az storage account create --name "storageAccountName" --resource-group "resourceGroupName"
```

4. Check the storage account (either on the azure portal or [CLI](https://learn.microsoft.com/en-us/cli/azure/storage/container?view=azure-cli-latest)) to see if it has any containers, if there aren't any, create one:
```
az storage container create --name "containerName" --account-name "storageAccountName" --resource-group "resourceGroupName"
```

5. Upload a the raw Flight Solo image as a storage blob to the container:
```
az storage blob upload --account-name "storageAccountName" \
                       --container-name "containerName" \
                       --type page \
                       --file FLIGHT-SOLO-IMAGE_azure.raw \
                       --name FLIGHT-SOLO-IMAGE_azure.vhd
```

6. Finally, create an azure image from the storage blob: (Make sure to get the correct source from the uploaded storage blob)
```
az image create --resource-group "resourceGroupName" \
    --name FLIGHT-SOLO-IMAGE_azure \
    --os-type Linux \
    --source  https://clusternameimages.blob.core.windows.net/images/FLIGHT-SOLO-IMAGE_azure.vhd
```



## Changing regions

The storage blob will be placed in the region of the storage account and container it is placed in, and will need to be created into a resource group with the same region.

In case this needs to be changed afterward:

1. Install the Azure CLI image copy extension
```
az extension add --name image-copy-extension
```

2. Set the options for source and target resource group, regions and source image.
```
az image copy --source-resource-group "sourceResourceGroup "
              --source-object-name "myImage" \
              --target-location "uksouth" "westeurope" \
              --target-resource-group "targetResourceGroup" \
              --cleanup
```

3. After a short wait, the source image will have the name `sourceImage-region` and be in the target resource group