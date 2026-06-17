# AWS Cost Explorer Lambda

# 

# AWS Lambda function that retrieves AWS cost and usage data using the AWS Cost Explorer API and can be integrated with EventBridge, API Gateway, or other AWS services for automated cost reporting and monitoring.

# 

# Features

# 

# \* Retrieve AWS cost and usage metrics

# \* Query costs by date range

# \* Support for daily or monthly granularity

# \* Can be scheduled using Amazon EventBridge

# \* Suitable for cost dashboards and reporting automation

# 

# Prerequisites

# 

# Before deploying this Lambda function, ensure the following:

# 

# &#x20;1. Enable AWS Cost Explorer

# 

# 1\. Sign in to the AWS Management Console.

# 2\. Open \*\*Billing and Cost Management\*\*.

# 3\. Navigate to \*\*Cost Explorer\*\*.

# 4\. Enable Cost Explorer if it is not already enabled.

# 

# > Note: Initial activation may take several hours before cost data becomes available.

# 

# &#x20;2. IAM Permissions

# 

# The Lambda execution role must have permissions to access Cost Explorer.

# 

# Example IAM policy:

# 

# ```json

# {

# &#x20; "Version": "2012-10-17",

# &#x20; "Statement": \[

# &#x20;   {

# &#x20;     "Effect": "Allow",

# &#x20;     "Action": \[

# &#x20;       "ce:GetCostAndUsage",

# &#x20;       "ce:GetCostForecast",

# &#x20;       "ce:GetDimensionValues"

# &#x20;     ],

# &#x20;     "Resource": "\*"

# &#x20;   }

# &#x20; ]

# }

# ```

# 

# &#x20;3. Billing Access

# 

# If using IAM users or roles, ensure billing access is enabled:

# 

# \* Go to \*\*Billing → Account Settings\*\*

# \* Enable \*\*IAM Access to Billing Information\*\*

# 

# &#x20;Project Structure

# 

# ```text

# .

# ├── lambda\_function.py

# ├── requirements.txt

# └── README.md

# ```

# 

# &#x20;Installation

# 

# Clone the repository:

# 

# ```bash

# git clone https://github.com/<your-username>/<repository-name>.git

# cd <repository-name>

# ```

# 

# Install dependencies:

# 

# ```bash

# pip install -r requirements.txt

# ```

# 

# &#x20;Deployment

# 

# &#x20;Using AWS Lambda Console

# 

# 1\. Create a new Lambda function.

# 2\. Select Python runtime.

# 3\. Upload the function code.

# 4\. Configure the execution role with Cost Explorer permissions.

# 5\. Deploy and test.

# 

# &#x20;Using AWS CLI

# 

# Zip the project:

# 

# ```bash

# zip function.zip lambda\_function.py

# ```

# 

# Update Lambda code:

# 

# ```bash

# aws lambda update-function-code \\

# &#x20; --function-name <lambda-function-name> \\

# &#x20; --zip-file fileb://function.zip

# ```

# 

# &#x20;Example Usage

# 

# ```python

# import boto3

# 

# ce = boto3.client("ce")

# 

# response = ce.get\_cost\_and\_usage(

# &#x20;   TimePeriod={

# &#x20;       "Start": "2025-01-01",

# &#x20;       "End": "2025-01-31"

# &#x20;   },

# &#x20;   Granularity="MONTHLY",

# &#x20;   Metrics=\["UnblendedCost"]

# )

# 

# print(response)

# ```

# 

# &#x20;Common Errors

# 

# &#x20;AccessDeniedException

# 

# ```text

# An error occurred (AccessDeniedException) when calling the GetCostAndUsage operation:

# User not enabled for cost explorer access

# ```

# 

# Possible causes:

# 

# \* Cost Explorer is not enabled.

# \* Lambda execution role lacks Cost Explorer permissions.

# \* IAM billing access is disabled.

# \* Using a member account without organization billing permissions.

# 

# &#x20;ValidationException

# 

# Occurs when:

# 

# \* Invalid date range is provided.

# \* Unsupported metrics are requested.

# \* Incorrect API parameters are supplied.

# 

# &#x20;Monitoring

# 

# Monitor Lambda execution through:

# 

# \* Amazon CloudWatch Logs

# \* CloudWatch Metrics

# \* AWS X-Ray (optional)

# 

# &#x20;Security

# 

# \* Follow least-privilege IAM principles.

# \* Avoid hardcoding credentials.

# \* Use IAM roles instead of access keys.

# 

# &#x20;License

# 

# This project is licensed under the MIT License.

# 

# &#x20;Author

# 

# M. Vishal Charlie Pranesh 

# 

# &#x20;Contributing

# 

# Contributions, issues, and feature requests are welcome. Feel free to submit a pull request.



