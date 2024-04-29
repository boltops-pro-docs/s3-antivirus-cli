<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/s3-antivirus-cli/blob/master/lib/s3_antivirus/help/batch.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

## Batch Commands

There are some supported batch commands:

    s3-antivirus batch bucket enable --sqs-arn SQS_ARN encrypt FILE.txt # FILE.txt should always be at the end
    s3-antivirus batch bucket disable FILE.txt

The format of FILE.txt is a list of S3 buckets separated by newlines.  Example:

FILE.txt:

    my-bucket-1
    my-bucket-1

