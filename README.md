# Automate AWS Volume Shrink
## Ansible
Ansible is a provisioning tool. Here, it is used to simply automate the process of shrinking AWS Elastic Block Storage specially, GP2 and IO1 volumes.

## What we do
We create a ansible playbook which will basically follow the following steps:  
* Install prerequisites using pip if ansible is not installed:
  ```bash
  pip install -r requirements.txt
  ```
* We manually add host ip addresses and also add path where volume is attached.
* Then run the script using command:  
  ```bash
  ansible-playbook -i path/to/hostfile path/to/playbook.yml
  ```  

Now wait for either the playbook to complete or if worst it could fails.

## What Script do
Below are the steps that script does.  
* Get space occupied by partition and create new volume in same availability zone keeping 10% available space.
* Attach volume in same instance formatting in same filetype as we want to copy file from.
* Stop all the .service file that is dependent in volume.
* Copy all the files in new partition using rsync.
* Unmount both partition and attach new partition to the path where previous partition was attached.
* Detach previous volume replacing volume registration from fstab.
* Finally, start the previously stopped .service

Note 1: This script does not work with root volume.  
Note 2: Script does not delete volume cause script might not work as expected. So, verify that the new partition is working properly and delete volume manually later.

## Directory Structure
```bash
.
├── .gitignore
├── .hosts
│   └── hosts.yml
├── .keys
├── .vscode
│   └── settings.json
├── LICENSE
├── README.md
├── example
│   └── hosts.yml
├── playbook
│   ├── group_vars
│   │   └── all
│   ├── main.yml
│   └── roles
│       └── centos
│           ├── files
│           ├── handlers
│           │   └── main.yml
│           └── tasks
│               └── main.yml
└── requirements.txt

13 directories, 9 files
```


## Point of Contact
[Dexter](diwakarpandey.com.np) -  [dipipandey1@gmail.com](dipipandey1@gmail.com)