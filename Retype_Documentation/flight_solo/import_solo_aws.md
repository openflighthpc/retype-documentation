---
order: 60
label: Import solo to AWS
icon: dot-fill
visibility: hidden
---


Several different cloud hosting services can use the downloaded Flight Solo image. This page shall describe how to do it with AWS. This only needs to be done once, and then the imported image can be used multiple times.


## Setting up a bucket

1. To set this up, you will need to install the AWS Command Line Interface(CLI). Confirm that you have the [prerequisites](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-prereqs.html) for the AWS CLI.

2. Install the AWS CLI by following the [AWS guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

3. Configure basic the basic AWS CLI by following [this guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html). There is more information about configuration in other parts of the [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html#cli-quick-configuration).

4. Download the Flight Solo AWS image [here](https://repo.openflighthpc.org/images/SOLO2-2022.2-0211221545_aws.raw).

5. Create a bucket, directory in the bucket and upload the Flight Solo image either on the CLI or on the Web Interface.

+++ AWS Command Line Interface
a. Create an S3 bucket, and set a name of your choosing. !HOWTOMAKEWORK?!?

```
aws s3 create-bucket --bucket <bucketname>
```

b. Upload the downloaded Flight Solo image to a directory called `images` in the S3 bucket with this command:
```
aws s3 cp SOLO2-2022.2-0211221545_aws.raw s3://<bucketname>/images/
```

c. Wait until it has finished uploaded before proceeding.

+++ AWS Web Interface
a. Go to the [AWS S3 Web Interface for buckets](https://s3.console.aws.amazon.com/s3/buckets). It should look like this:

![](/images/aws_s3_buckets.png)

!!!
Make sure that your region is set correctly.
!!!

b. Click "Create Bucket". 

c. On the bucket creation page, set the bucket name, and any other desired settings.

![](/images/aws_s3_bucket_name.png)

d. Scroll down to the bottom and click "Create Bucket". A success message should appear at the top of the screen and you will return to the bucket overview.

e. Click on the newly created bucket to view it.

![](/images/aws_s3_click_bucket.png)

f. This is what it should look like:

![](/images/aws_s3_bucket_view.png)

g. Make a folder by clicking "Make Folder" and name it `images`.

![](/images/aws_s3_bucket_makedir.png)

h. Click "Create Folder" to finish creation.

i. Enter the `images` folder by clicking on its name.

![](/images/aws_s3_showdir.png)

j. Click on "Upload" to open the upload screen. Click on "Add Files", and select the downloaded Flight Solo image.

![](/images/aws_s3_upload.png)

k. Click "Upload" to begin uploading, and wait for it to complete before proceeding.

![](/images/aws_s3_upload_status.png)

+++


## Import as Disk Snapshot

6. Create a vmimport policy file to enable vm import operations. Make a file called `trust-policy.json` with these contents:

!!UHH VERSION?? !!
```
{
"Version": "2012-10-17",
"Statement": [
  {
     "Effect": "Allow",
     "Principal": { "Service": "vmie.amazonaws.com" },
     "Action": "sts:AssumeRole",
     "Condition": {
        "StringEquals":{
           "sts:Externalid": "vmimport"
        }
     }
  }
]
}
```

7. Create a role from the vmimport policy file.
```
aws iam create-role --role-name vmimport --assume-role-policy-document "file://trust-policy.json"
```

8. Create a bucket association with the vmimport role in a file called `role-policy.json`, replacing `<bucketname>` with the name of your S3 bucket.
```
{
"Version": "2012-10-17",
"Statement": [
    {
        "Effect": "Allow",
        "Action": [
            "s3:GetBucketLocation",
            "s3:GetObject",
            "s3:ListBucket",
            "s3:PutObject",
            "s3:GetBucketAcl"
        ],
        "Resource": [
            "arn:aws:s3:::<bucketname>",
            "arn:aws:s3:::<bucketname>/*"
        ]
    },
    {
        "Effect": "Allow",
        "Action": [
            "ec2:ModifySnapshotAttribute",
            "ec2:CopySnapshot",
            "ec2:RegisterImage",
            "ec2:Describe*"
        ],
        "Resource": "*"
    }
]
}
```

9. Apply the role policy.
```
aws iam put-role-policy --role-name vmimport --policy-name vmimport --policy-document "file://role-policy.json"
```

10. Create a file called `containers.json` with raw disk image information. These are the contents (replace `<bucketname>` with your bucket name):

```
{
"Description": "SOLO2-2022.2-0211221545_aws.raw",
"Format": "raw",
"UserBucket": {
    "S3Bucket": "<bucketname>",
    "S3Key": "SOLO2-2022.2-0211221545_aws.raw"
}
}
```

11. Import the raw image as a disk snapshot.
```
aws ec2 import-snapshot --description "SOLO2-2022.2-0211221545_aws.raw" --disk-container "file://containers.json"
```

12. Wait until the import is complete. You can check the progress with this command: (replace the import task ID with the ID output of the previous command)

```
aws ec2 describe-import-snapshot-tasks --import-task-ids import-snap-00000000000000000
```

## Create AMI from Snapshot

13. Navigate to the [snapshots page](https://eu-west-2.console.aws.amazon.com/ec2/home?region=eu-west-2#Snapshots:) of AWS EC2. It should look something like this:

![](/images/aws_ec2_snapshots.png)
!!!
Make sure that your region is set correctly.
!!!

14. Locate the newly created snapshot

15. Right-click on the snapshot and select "Create image from snapshot".

![](/images/aws_ec2_snapshots_rmb.png)

16. Name it something descriptive like `Flight Solo`.

![](/images/aws_ec2_createfromsnapshot_name.png)

17. Set the Size to at least 16 GB.

![](/images/aws_ec2_createfromsnapshot_size.png)

18. Leave everything else default.

19. Click "Create Image" to create the AMI. The creation process can take several minutes to complete.


