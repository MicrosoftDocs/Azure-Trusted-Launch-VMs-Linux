
# Azure Site Recovery support for Azure Trusted Launch VMs running on Linux (private preview) 

[Azure Site Recovery](https://learn.microsoft.com/azure/site-recovery/site-recovery-overview) now supports Azure Trusted Launch virtual machines running Linux OS in a private preview. To enroll in the private preview, fill out this [enrolment form](https://aka.ms/asrlinuxtvmprivatepreviewform). Note that enrolment may take 7–15 business days to complete. After enrolling, you can access the private preview through this [Azure Portal link](https://aka.ms/TrustedVMLinuxSupport).

[Trusted launch](https://learn.microsoft.com/azure/virtual-machines/trusted-launch) actively protects against advanced and persistent attack techniques. It includes several coordinated infrastructure technologies that you can enable independently. Each technology adds another layer of defence against sophisticated threats.

Follow these [steps](https://learn.microsoft.com/azure/virtual-machines/trusted-launch-portal?tabs=portal%2Cportal3%2Cportal2) to deploy an Azure Trusted Launch VM.

## Support matrix

Find the support matrix for private preview of Azure Site Recovery support for Trusted Launch VMs (Linux): 

- **Region**: Support for Azure Trusted Launch virtual machines is available in [all Azure Site Recovery supported public regions](https://learn.microsoft.com/azure/site-recovery/azure-to-azure-support-matrix#region-support).
    > Support for Azure Trusted Launch virtual machines is not yet available in Azure Government regions and Azure in China regions.
- **Operating system**: This private preview is for Linux OS only. Ensure Linux OS is supported by both [Azure Trusted launch VM](https://learn.microsoft.com/azure/virtual-machines/trusted-launch#operating-systems-supported) and [Azure Site Recovery](https://learn.microsoft.com/azure/site-recovery/azure-to-azure-support-matrix#linux). 
    Oracle Linux and SUSE Enterprise Linux are still not supported in this private preview. Note that Azure Site Recovery support for Azure Trusted launch virtual machines (Windows) is already [Generally available](https://azure.microsoft.com/updates/v2/generally-available-azure-site-recovery-support-for-azure-trusted-launch-vms-windows-os).
- **Private endpoints**: Azure trusted virtual machines can be protected using private endpoint configured recovery services vault with the certain [conditions](#private-endpoints).


### Private endpoints

Azure Site Recovery supports Azure Trusted Launch VMs with private endpoints. You can protect Azure trusted virtual machines can be protected using private endpoint configured recovery services vault with these certain conditions:

- You can create a new recovery services vault and [configure private endpoints](https://learn.microsoft.com/azure/site-recovery/azure-to-azure-how-to-enable-replication-private-endpoints) on it. Then you can start protecting Azure Trusted VMs using it.
- You can't protect Azure Trusted VMs using recovery services vault which are already created before 13-May-2024 and have private endpoints configured. 
- **Migrations**: Migration of Azure Site Recovery protected existing Generation 1 Azure VMs to trusted VMs and [Generation 2 Azure virtual machines to trusted VMs](https://learn.microsoft.com/azure/site-recovery/concepts-trusted-vm#migrate-azure-site-recovery-protected-azure-generation-2-vm-to-trusted-vm) isn't supported.
- **Disk Network Access**: Azure Site Recovery creates disks (replica and target disks) with public access enabled by default. To disable public access for these disks follow [these steps](https://learn.microsoft.com/azure/site-recovery/azure-to-azure-common-questions#disk-network-access). 
- **Boot Integrity Monitoring**: Replicating [Boot Integrity Monitoring](https://learn.microsoft.com/azure/virtual-machines/boot-integrity-monitoring-overview?tabs=portal) state is not supported. You will need to enable it explicitly on the failed-over VM, in case you want to use it. 
- **Create a new VM flow**: On the Azure portal, enabling **Management** > **Site Recovery** option in *Create a new Virtual machine* flow isn't supported. 
- **Scenario**: Available only for Azure-to-Azure scenarios.


## Configure Azure Site Recovery for Trusted VMs

You can follow the same steps for configure Azure Site Recovery with Trusted VMs as you use for Azure Site Recovery with standard Azure VMs. 

- To configure Azure Site Recovery on Trusted VMs to another region, [follow these steps](https://learn.microsoft.com/azure/site-recovery/azure-to-azure-tutorial-enable-replication). To enable replication to another zone within the same region, [follow these steps](https://learn.microsoft.com/azure/site-recovery/azure-to-azure-how-to-enable-zone-to-zone-disaster-recovery).
- To failover and failback Azure virtual machines, [follow these steps](https://learn.microsoft.com/azure/site-recovery/azure-to-azure-tutorial-failover-failback).  

> [!NOTE]
>
> - We don't recommend Private Preview with production workloads. Use private preview with development or test workloads only. <br>
> - There'll be no migration channel supported from private preview to public preview or GA. So, you might need to disable Azure Site Recovery on the Trusted VMs on which they have enabled it during private preview and re-enable Azure Site Recovery post the Public Preview / GA.

## Contact

In case of any queries, reach out to askasr@microsoft.com.