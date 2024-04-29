<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/s3-antivirus-cli/blob/master/lib/s3_antivirus/help/bucket/enable.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

## Example

    s3-antivirus bucket enable my-bucket --sqs-arn arn:aws:sqs:us-west-2:111111111111:s3-antivirus-Queue-123456EXAMPLE

If there's an existing bucket notification, you should inspect it and see if it's safe to override it. To see the existing bucket notification:

    s3-antivirus bucket show my-bucket

To override it, use the `--override` option:

    s3-antivirus bucket enable my-bucket --sqs-arn arn:aws:sqs:us-west-2:111111111111:s3-antivirus-Queue-123456EXAMPLE --override