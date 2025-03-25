# Mod-2.15
Q.-	What is needed to authorize your EC2 to retrieve secrets from the AWS Secret Manager?
-	Derive the IAM policy (i.e. JSON)?
-	Using the secret name prod/cart-service/credentials, derive a sensible ARN as the specific resource for access
Ans.-To authorize an EC2 instance to retrieve secrets from AWS Secrets Manager, we need to create an IAM policy that grants the necessary permission to access the secret. The secret name provided is prod/cart-service/credentials, so the IAM policy will allow the EC2 instance to retrieve the value for this specific secret.
IAM Policy (JSON)
Below is a sample IAM policy that provides GetSecretValue permission to the EC2 instance for the prod/cart-service/credentials secret.
json
CopyEdit
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "secretsmanager:GetSecretValue",
      "Resource": "arn:aws:secretsmanager:<region>:<account-id>:secret:prod/cart-service/credentials-??????"
    }
  ]
}
Explanation:
•	Action: secretsmanager:GetSecretValue allows retrieving the value of the secret.
•	Resource: The ARN of the secret is needed. The ARN format for a secret in Secrets Manager is:
arn:aws:secretsmanager:<region>:<account-id>:secret:<secret-name>-<random-string>
o	Replace <region> with AWS region (e.g., us-west-2).
o	Replace <account-id> with  AWS account ID.
o	The prod/cart-service/credentials part is the secret name.
o	AWS Secrets Manager appends a random string to the secret name to create a unique secret ARN (e.g., prod/cart-service/credentials-ABC123).
Assuming the region is us-east-1 and your AWS account ID is 123456789012, the ARN for the secret would look like this:
arn:aws:secretsmanager:us-east-1:123456789012:secret:prod/cart-service/credentials-ABC123

Once the IAM policy is created, attach it to an IAM role.Assign the IAM role to EC2 instance to allow it to access the secret.


