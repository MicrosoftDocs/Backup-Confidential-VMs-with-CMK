---
title: Azure Backup - Configure backup of Confidential VM with Customer Managed Key using Azure Backup CMK (preview) 
description: Learn about backing up Confidential VM with CMK using Azure Backup.
ms.topic: conceptual
ms.date: 05/15/2023
ms.custom: references_regions
ms.service: backup
author: jyothisuri
ms.author: jsuri
---

# Back up Confidential VM with Customer Managed Key using Azure Backup (private preview)

This article describes how to configure and back up Confidential VM (CVM) with Customer Managed Key (CMK).

[Azure Backup](https://learn.microsoft.com/en-us/azure/backup/backup-overview) now offers protection of Azure Confidential VMs (CVM) with Customer Managed Keys (CMK). [Azure confidential VMs](https://learn.microsoft.com/en-us/azure/virtual-machines/dcasv5-dcadsv5-series), based on AMD processors with SEV-SNP technology, offers enhanced security. You can protect data from cloud operator and host with VM-level confidentiality. Confidential VMs help meet your security needs by providing hardware-based isolation.

***Note***

*For any queries, write to us at [AskAzureBackupTeam@microsoft.com](mailto:AskAzureBackupTeam@microsoft.com).*

## Create a new Confidential VM with Customer Managed Key

Learn how to [create a new Confidential VM with Customer Managed Key](https://learn.microsoft.com/en-us/azure/confidential-computing/quick-create-confidential-vm-portal-amd), if needed.

## Assign permissions

Azure Backup needs certain access to Key Vault or managed Hardware Security Module (mHSM) that are used to store the key. These permissions also help Azure Backup to back up the key, which you can restore if deleted for some reason.

When you configure backup of CVM with confidential OS disk encryption using CMK, the Azure portal automatically grants access to the Backup Management Service. If you're using other clients such as PowerShell, CLI, or REST API, permissions aren't granted automatically, and you need to grant the permissions.

### Scenario 1: Successful configuration

When you try configuring backup on CVM with CMK via Azure portal, access to the backup of the Key Vault or mHSM is granted automatically.

### Scenario 2: Error while configuring backup

When you try configuring backup on CVM with CMK from PowerShell, an error occurs. This happens because backup needs access to the Key Vault or mHSM.

![Screenshot shows the error while configuring backup when Backup Service doesn't have required access for key.](https://github.com/MicrosoftDocs/Backup-Confidential-VMs-with-CMK/blob/main/articles/media/backup-confidential-vm-with-customer-managed-key/configuration-error-for-missing-access-to-key.png)

You can assign access to the Backup Service, and then try configuring Azure Backup on CVM with CMK from PowerShell, CLI, or REST API. Learn how to [assign permissions for the key vault](https://learn.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption#provide-permissions).

***Note***

*For CVM with CMK, key permissions (Get, List, Backup) only needed; Secret permissions aren't required.*

To assign permissions for mHSM, follow these steps:

1. In the Azure portal, go to **Managed HSM**, and then select **Local RBAC** in **Settings**.

2. Select **Add** to add a *new Role Assignment*.

3. Select one of the following roles:

   - **Built-in roles**: If you want to use a built-in roles, select the **Managed HSM Crypto User** role.

   - **Custom roles**: If you want to use custom role, then *dataActions* of that role should have these values:

     - **Microsoft.KeyVault/managedHsm/keys/read/action**
     - **Microsoft.KeyVault/managedHsm/keys/backup/action**

     You can create a custom role using the [Managed HSM data plane role management](https://learn.microsoft.com/en-us/azure/key-vault/managed-hsm/role-management#create-a-new-role-definition).

4. For **Scope**, select the specific key used to create Confidential VM with Customer Managed Key.

   You can also select **All Keys**. 

5. On the **Security principal**, select **Backup Management Service**.

## Configure backup

Once backup has the necessary permissions, you can continue configuring backup as usual. [Learn more](https://learn.microsoft.com/en-us/azure/backup/backup-during-vm-creation).

## Next steps

[Restore CVM with CMK using Azure Backup (private preview)](https://github.com/MicrosoftDocs/Backup-Confidential-VMs-with-CMK/blob/main/articles/backup-confidential-vm-with-customer-managed-key-restore.md)