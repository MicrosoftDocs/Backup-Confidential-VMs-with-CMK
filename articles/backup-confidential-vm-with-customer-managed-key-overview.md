---
title: Azure Backup - Backup Confidential VM with Customer Managed Key using Azure Backup CMK overview (preview) 
description: Learn about backing up Confidential VM with CMK using Azure Backup.
ms.topic: conceptual
ms.date: 05/15/2023
ms.custom: references_regions
ms.service: backup
author: jyothisuri
ms.author: jsuri
---

# About backup of Confidential VM (CVM) with Customer Managed Key (CMK) using Azure Backup (preview)






## Limitations

- Support for backup of CVM with CMK (private preview) is only available on an enrolment basis.
- Backup support for CVM with confidential OS disk encryption using CMK is only supported using [Enhanced policy](https://learn.microsoft.com/en-us/azure/backup/backup-azure-vms-enhanced-policy?tabs=azure-portal).
- Original Location Restore (OLR), Alternate-Location Restore (ALR), Cross Zonal Restore, and Restore Disks are supported restore mechanisms.
- Item-level restore, Cross subscription restore, Cross region restore are currently not supported.
- Key rotation of CMK used for CVM isn't supported.

## Recommendation

We don't recommended to try this private preview feature for production workloads.

## Next steps

- [Configure backup fo CVM with CMK](https://github.com/MicrosoftDocs/Backup-Confidential-VMs-with-CMK/blob/main/articles/backup-confidential-vm-with-customer-managed-key-configure-backup.md)
