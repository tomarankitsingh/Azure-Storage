# Azure-Storage-Account-Project

## Overview
The project focuses on managing files within an Azure Storage Account, where specific access permissions are established for users. The main objectives include allowing an anonymous user to upload files to a container using a Shared Access Signature (SAS) token, while also ensuring the admin is alerted upon any file uploads or changes made by users. Additionally, access controls and monitoring are configured to secure the storage account and track user activities effectively.

# As an Administrator -----  u have to -
1. Upload a sample internship letter to a private container within the Azure Storage Account.
2. Grant access to the container for a designated user.
3. Configure alerts to notify the administrator whenever a new file is uploaded to the container.

# As an User -----  u have to -
- Access the internship letter, digitally sign it, and upload the signed document back to the container.

## Admin Tasks

### Step 1: Create a Resource Group for Storage Account ![image](https://github.com/user-attachments/assets/56c9b407-f3d0-4f7a-9993-c6879f99691a)
1. Go to [Azure Portal](https://portal.azure.com/).
2. From the left-hand menu, select `Resource groups`.
3. Click `Create`.
4. Fill in the necessary details, such as **Resource Group Name** and **Region**.
5. Click `Review + create`, then finalize by selecting `Create`.

### Step 2: Configure the Storage Account ![image](https://github.com/user-attachments/assets/13a5cd06-bc31-4824-9685-6bb14e55c942)
1. In the Azure Portal, go to `Storage accounts`.
2. Click on `Create`.
3. Enter details such as **Subscription**, **Resource Group**, **Storage Account Name**, **Region**, and **Performance** options.
4. Click `Review + create` and then `Create`.

### Step 3: Create a Container in the Storage Account ![image](https://github.com/user-attachments/assets/ba837d0a-4911-4524-a235-e5896d5c7b3d)

1. **Create a Container:**
   - In the storage account menu, under `Data storage`, click on `Containers`.
   - Click on `Create`.
   - Provide a name for the container and set the `Public access level` to **Private**.
   - Click `Create`.

2. **Upload Files:**
   - Go to the created container.
   - Click on `Upload`.
   - Select the internship letter and other documents to upload.
   - Click `Upload`.

3. Ensure that the container’s access level is set to **Private**.

### Step 4: Generate SAS Token for Assigning Blob Role to User ![Screenshot 2024-10-02 205752](https://github.com/user-attachments/assets/027fe562-e1c9-4111-9b09-81267ba75fb3)
1. In the storage account menu, under `Security + networking`, click on `Shared Access Signature`.
2. Configure the SAS token settings (permissions, start and end date).
3. Click **Generate SAS and connection string**.
4. Copy the **Blob service SAS URL**.

### Step 5: Create Log Analytics Workspace ![image](https://github.com/user-attachments/assets/17511c70-30ac-4057-914a-da67b1b82bf3)
1. In the Azure Portal, go to `Log Analytics Workspaces`.
2. Click on `Create`.
3. Provide required details.
4. Click `Review + create` and then `Create`.

### Step 6: Sync Log Analytics Workspace with Storage Account ![image](https://github.com/user-attachments/assets/08127e3c-864a-410a-831a-efbf6c37626f)
1. In the storage account, click on `Diagnostic settings` under `Monitoring`.
2. Click `Add diagnostic setting`.
3. Name the setting and select the **Log Analytics workspace** as the destination.
4. Check the **audit**, **all logs** and **transaction** service.
5. Click `Save`.

### Step 7: Create Alert Rule ![image](https://github.com/user-attachments/assets/80d49d21-4c33-4bce-884d-bf3d41377c28)
1. In the Storage Account, go to `Monitoring` and then `Alerts`.
2. Click `New alert rule`.
3. **Scope:** Select the storage account.
4. **Condition:** Click `Add condition`.
   - Choose `Custom log search` to use Log Analytics for querying.
   - Use the following KQL query:
       ```kql
      StorageBlobLogs
      | where OperationName == "PutBlob" or OperationName == "PutBlockList"
      | project TimeGenerated, OperationName, CallerIpAddress, _ResourceId
      | order by TimeGenerated desc
       ```
5. **Action Group:** Configure an action group to notify the administrator.
6. Provide alert details and click `Create alert rule`.

## User Tasks

### Step 1: Download and Install Azure Storage Explorer ![image](https://github.com/user-attachments/assets/9054bb4b-8a81-48cb-b9f5-6129360bd270)

### Step 2: Access and Download the Letter

1. **Add Account Using Blob Service SAS URL:** ![image](https://github.com/user-attachments/assets/176695d0-0c60-4440-99bb-5685f541a5f6)
1. Click `Add Account` or `Attach to a resource`.
2. Select `Storage Account or Service`.
3. Select `Shared Access Signature (URL) SAS`.
4. Paste the `SAS URL` provided by the admin in the **service URL**.
5. Click `Next` and follow the prompts to connect.

2. **Download the Internship Letter:** ![image](https://github.com/user-attachments/assets/ca72b1f0-76f3-48f9-b957-dc410eb57e57)
1. Navigate to the container.
2. Find and download the internship letter.

### Step 3: Digitally Sign the Letter
1. Open the downloaded letter in a PDF editor or digital signature tool.
2. Apply your digital signature.

### Step 4: Upload the Signed Letter Back ![image](https://github.com/user-attachments/assets/37e5729f-95d6-4e05-90b7-0d62c278875b)
1. In Azure Storage Explorer, navigate to the container.
2. Click `Upload`.
3. Select the signed document and click `Upload`.
  
## When the user uploads the signed internship letter back to the container, the administrator will receive an alert via email. ![image](https://github.com/user-attachments/assets/7db6ec02-933d-431b-8325-f98d1f1300a2)

Congratulations! You have successfully completed the Azure Storage Account project, implementing user access permissions, enabling anonymous uploads via SAS tokens, and setting up admin alerts for file activities. Access controls and monitoring are now fully in place.

## Contact

For any questions, doubts, or clarifications regarding this repository, feel free to reach out:

- Email: mailto:tomarankitsingh2000@gmail.com
- LinkedIn: https://www.linkedin.com/in/tomarankitsingh/
