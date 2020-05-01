Create/update Storage Account in Azure
=========

This role creates a storage account of kind: Storage, StorageV2, or BlobStorage (Blob, File, Queue, Table) (when kind = BlobStorage, only service type = Blob is valid).

<https://docs.ansible.com/ansible/latest/modules/azure_rm_storageaccount_module.html>

Requirements
------------

Ansible Azure Module

Role Variables
--------------

``` yaml

resource_group: #name of the resourcegroup you want to create the storage account in
storacc_name: #Unique name of storage account coming from input
storacc_type: #The type of storage account you want to create: Premium_LRS; Standard_GRS; Standard _LRS; StandardSSD_LRS; Standard_RAGRS; Standard_ZRS
storacc_access_tier: #The access tier for this storage account. Required for a storage account of kind 'BlobStorage' and 'StorageV2', Can't be used for General v1 storage, Choices are Hot and Cool from Ansible
storacc_kind: # Storage kind, choices are StorageV2, BlobStorage. Innovapost to use StorageV2 for most options
storacc_https_only: true # Default true. Allows https traffic only to storage service if sets to true
```

Dependencies
------------

Total name length of storracc_name must be between 3 and 24 characters
This role relies on the Ansible Azure Modules

Example Playbook
----------------

``` yaml

# Single Rule Create

---

- name: Create Azure Storage Account
  hosts: localhost
  pre_tasks:
    - name: setting up storage account
      set_fact:
        STORACC_NAME: "test0"
        STORACC_KIND: "BlobStorage"
        STORACC_TYPE: "Standard_RAGRS"
        STORACC_ACCESS_TIER: "Cool"
        STORACC_HTTPS_ONLY: "true"

  connection: local

  roles:
    - azure-storage
```

License
-------

MIT

Author Information
------------------

Adam Brassard: Abrass on IRC
