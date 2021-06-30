# ansible-onprem-vmdk-import

This playbook automates the processes of exporting an OnPrem from VMware and Importing it as an AWS AMI. 

## Prerequisites

- You will need to install and configure the AWS CLI on the machine you will be running the playbook from, instructions can be found here:  https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html
- You will need set up your AWS Import IAM role and bucket, instructions can be found here:  https://docs.aws.amazon.com/vm-import/latest/userguide/vmimport-image-import.html

## Update the variables at the top of the vm-import.yml with your VMware and S3 details

```
    vcenter_hostname: '<your-vcenter-host>'
    vcenter_username: '<your-vcenter-username>'
    vcenter_password: '<your-vcenter-password>'
    vm_name: '<your-vm-name>'
    s3_bucket: '<your-s3-bucket>'
    s3_key: '<your-s3-key>'
    s3_description: '<your-s3-description>'
```
*Make sure your S3 details match your bucket details and the containers.json details exactly*

## Update the containers.json file with your AWS S3 Details, you will find an example below

```
[
      {
        "Description": "OnPrem vmdk",
        "Format": "vmdk",
        "UserBucket": {
            "S3Bucket": "onpremovaimport",
            "S3Key": "OnPrem.vmdk"
        }
    }]
```

### Please note that each step in this process can take a considerable amount of time depending on your upload/download speeds, make sure your machine does not fall asleep.  



