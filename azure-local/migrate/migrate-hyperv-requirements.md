---
title: Review requirements for Hyper-V VM migration to Azure Local using Azure Migrate (preview) 
description: Learn the system requirements for Hyper-V migration to Azure Local using Azure Migrate (preview).
author: alkohli
ms.topic: how-to
ms.date: 10/31/2024
ms.author: alkohli
---

# Review requirements for Hyper-V VM migration to Azure Local using Azure Migrate (preview)

[!INCLUDE [applies-to](../includes/hci-applies-to-23h2.md)]

This article lists the system requirements for migrating Hyper-V virtual machines (VMs) to Azure Local using Azure Migrate.

[!INCLUDE [important](../includes/hci-preview.md)]

## Supported configurations

The following operating systems (OS) are supported for the source appliance, target appliance, and for the guest VMs that your'e migrating.


|Component  |Supported configurations |
|---------|---------|
|Source environment     |Hyper-V on Windows Server 2022<br>Hyper-V on Windows Server 2019<br>Hyper-V on Windows Server 2016<br>Hyper-V on Windows Server 2012 R2         |
|Source appliance     |Windows Server 2022        |
|Target environment     |Azure Local, version 23H2         |
|Target appliance     |Windows Server 2022         |
|Guest VM (Windows)    |Windows Server 2022<br>Windows Server 2019<br>Windows Server 2016<br>Windows Server 2012 R2<br>Windows Server 2008 R2*       |
|Guest VM (Linux) | Red Hat Linux 6.x, 7.x<br>Ubuntu Server and Pro. 18.x<br>CentOS 7.x <br>SUSE Linux Enterprise 12.x<br>Debian 9.x |

*To migrate Windows Server 2008 R2 VMs, see the [FAQ](migrate-faq.yml).


## Supported geographies

You can create an Azure Migrate project in many geographies in the Azure public cloud. Here's a list of supported geographies for migration to Azure Local:

|Geography|Metadata storage locations|
|-|-|
|Asia-Pacific|South East Asia, East Asia|
|Europe|North Europe, West Europe|
|United States|East US, Central US, West Central US, West US2|

Keep in mind the following information as you create a project:

- Project geography is only used to store the discovered metadata.
- When you create a project, you select a geography. The project and related resources are created in one of the regions in the geography. The region is allocated by the Azure Migrate service. Azure Migrate doesn't move or store customer data outside of the region allocated.

## Azure portal requirements

For more information on Azure subscriptions and roles, see [Azure roles, Azure AD roles, and classic subscription administrator roles](/azure/role-based-access-control/rbac-and-directory-admin-roles).

|Level|Permissions|
|-|-|
|Tenant|Application administrator|
|Subscription|Contributor, User Access Administrator|

## Source Hyper-V requirements

- Hyper-V Server is supported for both standalone server and cluster configuration.

    You can discover and migrate standalone (non highly available) VMs on standalone Hyper-V hosts. However, standalone VMs hosted on clustered Hyper-V hosts can't be discovered or migrated. To migrate these VMs, they need to be [made highly available](https://www.thomasmaurer.ch/2013/01/how-to-make-an-existing-hyper-v-virtual-machine-highly-available/) first.

- The source server used for migration should have sufficient resources to create a Windows Server 2022 VM with this minimum of 16 GB memory, 80 GB disk, and 8 vCPUs.

- In this release, you can only migrate VMs that have disks attached to the cluster shared volumes (CSV). If the VM disks aren't attached to the CSV, the disks can't be migrated.

- DAS and SMB shares on source system are not supported for migrations to Azure Stack HCI.

- Before you begin, for all Windows VMs, bring all the disks online and persist the drive letter. For more information, see how to [configure a SAN policy](/azure/migrate/prepare-for-migration#configure-san-policy) to bring the disks online.

## Target Azure Local requirements

- The target operating system for your Azure Local instance must be running version 23H2.

- An Arc Resource Bridge must exist on the Azure Local, version 23H2 system for migration. The Arc Resource Bridge is automatically created during the deployment. To verify that an Arc Resource Bridge exists on your Azure Local system, see [Deploy using Azure portal](../deploy/deploy-via-portal.md).  

- Ensure that a logical network is configured on your Arc Resource Bridge. For more information, see [Create a logical network](../manage/create-logical-networks.md).

- Ensure that a custom storage path is configured on your Arc Resource Bridge for migration. For more information, see [Create a storage path](../manage/create-storage-path.md).

## Azure Migrate project requirements

Existing Azure Migrate customers that have done VM discovery need to [create a new Azure Migrate project](migrate-hyperv-prerequisites.md#create-an-azure-migrate-project) for migration to Azure Local. You can't use existing Azure Migrate projects for migration.

## Next steps

- [Complete the prerequisites](migrate-hyperv-prerequisites.md).
