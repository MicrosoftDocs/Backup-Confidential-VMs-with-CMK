---
title: Azure Backup - Configure backup of Confidential VM with Customer Managed Key using Azure Backup CMK overview (preview) 
description: Learn about backing up Confidential VM with CMK using Azure Backup.
ms.topic: conceptual
ms.date: 05/15/2023
ms.custom: references_regions
ms.service: backup
author: jyothisuri
ms.author: jsuri
---

# Back up Confidential VM with Customer Managed Key using Azure Backup (preview)

This articles describes how to configure and back up Confidential VM (CVM) with Customer Managed Key (CMK).

(Awaiting intro from PM)

Learn how to [create a new confidential VM with customer managed key](https://learn.microsoft.com/en-us/azure/confidential-computing/quick-create-confidential-vm-portal-amd), if needed.

## Configure backup

Azure Backup needs certain access to Key Vault or managed Hardware Security Module (mHSM) that are used to store the key. Azure Backup also needs required permissions to back up the key. If it gets deleted for some reasons, you can restore this backed-up key.

When you configure backup of CVM with confidential OS disk encryption using CMK, the Azure portal automatically grants access to the Backup Management Service. If you're using other clients - such as PowerShell, CLI, REST API, permissions aren't granted automatically, and you need to grant the permissions.

**Successful configuration**

When you try configuring backup on CVM with CMK via Azure portal, the access to the backup of the Key Vault or mHSM is granted automatically.

**Error while configuring backup**

When you try configuring backup on CVM with CMK from PowerShell, the following error appears. This happens because backup needs access to the key vault/mHSM.

![Screenshot shows the error while configuring backup when Backup Service doesn't have required access for key.](configuration-error-for-missing-access-to-key.png)

You can assign access to the Backup Service, and then try configuring Azure Backup on CVM with CMK from PowerShell, CLI, or REST API. Learn about how to [assign permissions for the key vault](https://learn.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption#provide-permissions).

***Note***
*For CVM with CMK, key permissions (Get, List, Backup) only needed; Secret permissions aren't required.*

To assign permissions for mHSM, follow these steps:

1. In the Azure portal, go to **Managed HSM**, and then select **Local RBAC** in **Settings**.

2. Select **Add** to add a *new Role Assignment*.

3. Select one of the following roles:

   - **Built-in roles**: If you wanr to use a built-in roles, select the **Managed HSM Crypto User** role.

   - **Custom roles**: If you want to use custom role, then *dataActions* of that role should have these values:

     1. **Microsoft.KeyVault/managedHsm/keys/read/action**
     2. **Microsoft.KeyVault/managedHsm/keys/backup/action**

     You can create a custom role using this **Managed HSM data plane** role management- Azure Key Vault | Microsoft Learn 
4.	For scope you can select the specific key used to create Confidential VM with Customer Managed Key or “All Keys” can be selected as well. 
5.	In the Security principal please select “Backup Management Service”. 

So once Backup has necessary permissions, you can continue configuring Backup as usual.









## Next steps

