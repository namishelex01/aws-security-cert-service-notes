* [Kinesis](https://aws.amazon.com/kinesis/)
    + Ingest and analyse various data sources, notably logs
    * [Data Firehose](https://aws.amazon.com/kinesis/data-firehose/faqs/)
        + "capture, transform, and load streaming data into Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and Splunk"
        + Create delivery stream, with optional Lambda function to transform the data
        + Configure producers to send data to Kinesis with the Kinesis Agent (which monitors log files) or Firehose API
        + Source integrations: CloudWatch Logs subscription filter; CloudWatch Events rule with Firehose target; Kinesis Data Streams. 
        + Configure an IAM role that it assumes to access e.g. S3 or Elasticsearch
        + Manage delivery frequency with buffer size or interval
