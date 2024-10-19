# HHA504 Assignment: Working with Cloud Storage in Azure and GCP

## **Overview**

This assignment explores how to upload files to Azure Blob Storage and Google Cloud Storage using both the platform's GUI and Python. Additionally, it involves exploring and documenting storage management and security features in both platforms.

---

## **1. File Uploads Using GUI**

### **1.1 Azure Blob Storage**

#### **Steps:**
1. Logged into the Azure Portal and created a new **Storage Account**.

![image](https://github.com/user-attachments/assets/853b9b62-d45d-488a-bea7-18d865bfc411)
   
2. Created a **Blob container** within the Storage Account.
3. Uploaded a sample file (`cat.jpg`) to the Blob container using the Azure portal GUI.

![image](https://github.com/user-attachments/assets/645e6b16-eb77-411b-97cd-a427436ff628)


### **1.2 Google Cloud Storage**

#### **Steps:**
1. Logged into Google Cloud Console and created a new **Cloud Storage bucket**.

![image](https://github.com/user-attachments/assets/7b1f32fc-33eb-4630-b559-1b6b7d2817a0)
   
3. Uploaded the same sample file (`cat.jpg`) to the bucket using the GCP Console GUI.

![image](https://github.com/user-attachments/assets/0fac297f-bc2f-465b-81a7-5ad3d1a66ba3)

---

## **2. File Uploads Using Python**

### **2.1 Azure Blob Storage**

#### **Python Code:**

```python
from azure.storage.blob import BlobServiceClient

# Azure connection string and container information
connect_str = "DefaultEndpointsProtocol=https;AccountName=samsstorage1;AccountKey=GgLRo1saxz+jIbA7CJp252E5N7rr4cUOrd6yDBEozOOOFgQWvsRoDdaBMZllesJCLFptiEqoubYc+AStl922Uw==;EndpointSuffix=core.windows.net"
container_name = "myblobcontainer"

# File to upload
file_path = "eye tumor.png"
blob_name = "eye tumor"

# Create the BlobServiceClient object
blob_service_client = BlobServiceClient.from_connection_string(connect_str)
container_client = blob_service_client.get_container_client(container_name)

# Upload file to the container
with open(file_path, "rb") as data:
    container_client.upload_blob(name=blob_name, data=data)

print("File uploaded successfully!")
```

#### **Steps:**
1. Used **Google Cloud Shell** as the terminal environment.
2. Installed the `azure-storage-blob` Python library.
3. Created a Python script to upload a file to Azure Blob Storage.

![image](https://github.com/user-attachments/assets/bcac03c7-836b-4722-873e-0bbb6177b537)

4. Uploaded the file (`eye tumor.png`) from the Cloud Shell environment to Azure Blob Storage using the provided connection string and container name.

![image](https://github.com/user-attachments/assets/33afce56-a776-497a-9df5-edd72c46b6c2)

### **2.2 GCP Cloud Storage**

#### **Python Code:**

```python
from google.cloud import storage

# Initialize a storage client
storage_client = storage.Client()

# Bucket and file information
bucket_name = "samsbucket1"
file_path = "eye tumor.png"
blob_name = "eye tumor"

# Get the bucket and create a blob object
bucket = storage_client.bucket(bucket_name)
blob = bucket.blob(blob_name)

# Upload file to GCP
blob.upload_from_filename(file_path)

print("File uploaded successfully to GCP!")
```

#### **Steps:**
1. Installed the `google-cloud-storage` Python library in Google Cloud Shell.
2. Created a Python script to upload a file to GCP Cloud Storage.

![image](https://github.com/user-attachments/assets/58a8c104-35a0-4820-a6fe-6ac5eb004d3c)

3. Uploaded the same file (`eye tumor.png`) to GCP Cloud Storage from the Cloud Shell environment.

![image](https://github.com/user-attachments/assets/7dd3b529-61b8-4667-9ee5-4ee2aafb530f)

---

## **3. Storage Management and Security Features**

### **3.1 Azure Blob Storage**

Azure Blob Storage provides several management and security features:
- **Access Policies**: Blob containers can be configured with access levels such as private, blob (anonymous read access to blobs), or container-level access.
- **Storage Tiers**: Azure Blob Storage supports Hot, Cool, and Archive storage tiers for optimizing cost based on data access frequency.
- **Encryption**: Data is encrypted at rest by default using Microsoft-managed keys, and you can also use your own customer-managed keys for additional control.
- **Shared Access Signatures (SAS)**: You can create a SAS token to provide limited-time access to blobs without exposing account keys.

### **3.2 GCP Cloud Storage**

GCP Cloud Storage also provides robust management and security options:
- **IAM Permissions**: GCP allows fine-grained control of who can access buckets and objects using Identity and Access Management (IAM).
- **Lifecycle Rules**: Automatically transition objects to lower-cost storage classes (Nearline, Coldline, or Archive) or delete them after a certain period.
- **Object Versioning**: Enables tracking of changes to files and keeps a history of object modifications.
- **Encryption**: Data is encrypted at rest by default, and customer-managed encryption keys (CMEK) are supported for enhanced control.
