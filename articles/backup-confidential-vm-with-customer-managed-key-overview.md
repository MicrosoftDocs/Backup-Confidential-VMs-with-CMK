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

# About protection of Confidential VM with Customer Managed Key using Azure Backup (preview)

[Azure Backup](https://learn.microsoft.com/en-us/azure/backup/backup-overview) now offers protection of Azure Confidential VMs (CVM) with Customer Managed Keys (CMK).

[Azure confidential VMs](https://learn.microsoft.com/en-us/azure/virtual-machines/dcasv5-dcadsv5-series), based on AMD processors with SEV-SNP technology, offers enhanced security. You can protect data from cloud operator and host with VM-level confidentiality. Confidential VMs help meet your security needs by providing hardware-based isolation.

## Limitations

- Support for backup of CVM with CMK (private preview) is only available on an enrollment basis.
- Backup support for CVM with confidential OS disk encryption using CMK is only supported using [Enhanced policy](https://learn.microsoft.com/en-us/azure/backup/backup-azure-vms-enhanced-policy?tabs=azure-portal).
- Original Location Restore (OLR), Alternate-Location Restore (ALR), Cross Zonal Restore, and Restore Disks are the supported restore mechanisms.
- Item-level restore, Cross Subscription Restore, Cross region restore are currently not supported.
- Key rotation of CMK used for CVM isn't supported.

## Recommendation

We recommended you not to try this private preview feature for production workloads.

## Next steps

- [Configure backup for CVM with CMK  using Azure Backup (preview)](https://github.com/MicrosoftDocs/Backup-Confidential-VMs-with-CMK/blob/main/articles/backup-confidential-vm-with-customer-managed-key-configure-backup.md)
