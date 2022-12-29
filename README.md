# ansible-onprem-vmdk-import

This playbook automates the processes of exporting a Smart Software Manager OnPrem server from VMware and importing it as an AWS AMI. 

## Prerequisites

- ansible-galaxy collection install community.vmware
- python >= 2.9
- PyVmomi
- You will need to install and configure the AWS CLI on the machine you will be running the playbook from, instructions can be found here:  https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html
- You will need to set up your AWS Import IAM role and bucket, instructions can be found here:  https://docs.aws.amazon.com/vm-import/latest/userguide/vmimport-image-import.html
- You will need to power off your VMware VM prior to beginning the export process

## Update the variables at the top of the vm-import.yml with your VMware and S3 details

```
    vcenter_hostname: '<your-vcenter-host>'
    vcenter_username: '<your-vcenter-username>'
    vcenter_password: '<your-vcenter-password>'
    vm_name: '<your-vm-name>'
    s3_bucket: '<your-s3-bucket>'
    s3_key: '<your-s3-key>'
    s3_description: '<your-s3-description>'
    export_directory_path: '<your-export-path>'
```
*Make sure your S3 details match your bucket details and the containers.json details exactly*

## Update the containers.json file with your AWS S3 Details, you will find an example below

```
[
      {
        "Description": "OnPrem vmdk",
        "Format": "vmdk",
        "UserBucket": {
            "S3Bucket": "your-s3-bucket",
            "S3Key": "OnPrem.vmdk"
        }
    }]
```

Please note that each step in this process can take a considerable amount of time depending on your upload/download speeds, make sure your machine does not fall asleep.  The AMI Import process will continue after the playbook finishes, you can check the status of the import with the following AWS CLI command:
```
aws ec2 describe-import-image-tasks
```



