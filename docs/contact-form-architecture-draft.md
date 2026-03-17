# Draft: Website Contact Form Architecture Discussion

## Purpose
This draft is prepared for internal discussion on how to implement and operate backend handling for the existing website contact form using services managed by our team.

The goal is to implement backend processing for the current static contact form so it can:

- receive form submissions
- store submission data
- send email notifications
- remain simple and cost-effective to operate

## Current Situation
The current website is a static Astro site. The contact form already exists in the user interface, but it does not currently submit data to any backend service.

Because of this:

- enquiries from the website are not processed automatically
- there is no storage of contact requests
- no notification email is sent to the internal team
- there is no operational visibility into form activity or failures

## Proposed Solution
The proposed solution is to build the contact form backend using the following AWS services:

- Amazon API Gateway
- AWS Lambda
- Amazon DynamoDB
- Amazon SES

## Proposed Flow
1. A user fills in the contact form on the website.
2. The website sends the form data to an API Gateway endpoint.
3. API Gateway invokes a Lambda function.
4. The Lambda function validates and sanitizes the request.
5. The Lambda function stores the submission in DynamoDB.
6. The Lambda function sends an email notification through SES.
7. The Lambda function optionally sends a confirmation email to the user.
8. The frontend shows a success or error message based on the response.

## How The Website Would Use This Solution
The website would continue to show the existing contact form to users. The main change would be in how the form is submitted and processed behind the scenes.

- When a user clicks the submit button, the website sends the form data to a secure API Gateway endpoint over HTTPS.
- The website waits for the backend response and then shows a success or failure message to the user.
- No sensitive submission data needs to be stored in the browser after the request is completed.
- The website itself remains a lightweight frontend, while validation, storage, and email processing are handled by AWS services.

This means the website remains simple, while the backend processing is moved into a managed serverless architecture.

## Why This Option Is Recommended
This option is recommended because:

- it is low cost for small to medium traffic volume
- it does not require running a traditional backend server
- it scales automatically
- it fits well with the current static website architecture
- it gives the company full ownership of contact submission data

## Main Components
### API Gateway
- Exposes the public HTTPS endpoint for contact form submission
- Handles request routing and CORS
- Can apply throttling to reduce abuse

### Lambda
- Contains the backend logic
- Validates input data
- Writes records to DynamoDB
- Sends emails through SES

### DynamoDB
- Stores each contact submission
- Provides a simple and scalable way to retain records

### SES
- Sends email notifications to the internal team
- Can also send acknowledgement emails to the submitter

## Suggested Stored Fields
The DynamoDB record can include:

- `submissionId`: unique identifier for each contact form submission
- `createdAt`: date and time when the submission was received
- `name`: sender name provided in the form
- `email`: sender email address for reply and acknowledgement
- `message`: enquiry content submitted by the user
- `sourcePage`: page where the form was submitted from, if this is needed
- `status`: processing state of the submission, if tracking is needed
- `requestMetadata`: optional technical metadata for troubleshooting or abuse detection

## Security Considerations
- Validate all user input on the server side
- Apply throttling at API Gateway level
- Consider CAPTCHA or a honeypot field for spam reduction
- Store only necessary personal data
- Use AWS-managed encryption
- Define a retention policy for stored contact requests

## Additional Steps To Segregate And Protect Sensitive Data
If stronger segregation and protection are required, the following measures can be added:

- Encrypt sensitive data at rest using AWS KMS with a dedicated customer-managed key
- Ensure all communication between the website and API Gateway uses HTTPS only
- Mask or avoid storing unnecessary personal data wherever possible
- Add stricter retention rules so old submissions are deleted after a defined period
- Store only the minimum required fields needed for business follow-up
- Hash or avoid storing network-related metadata unless there is a clear security requirement

## Operational Considerations
- Monitor Lambda errors using CloudWatch
- Monitor failed email sends
- Keep the architecture small and easy to maintain
- Use infrastructure as code for deployment if this moves forward

## Alternative Solution
An alternative option is to use Formspree instead of building the backend in AWS.

This option would reduce implementation effort and allow faster setup because the website form can post directly to a Formspree endpoint without building our own API, Lambda function, database, or email workflow.

Based on Formspree's official help documentation, the Free plan starts at `50 submissions per month`, supports up to `2` notification email addresses, and stores `30 days` of submission history.

Recent pricing snapshots list paid plans at approximately:

- `Personal`: about `$10/month`
- `Professional`: about `$20/month`
- `Business`: about `$60/month`

Formspree can therefore be a practical short-term solution if we want fast implementation with minimal engineering work. However, it provides less control over data handling, storage, and workflow compared with the AWS serverless approach. For a longer-term solution, the AWS serverless approach remains the preferred option.

## Minimum Estimated Monthly AWS Cost
For minimum expected volume, using a low-traffic contact form assumption of around `500 submissions per month`, the minimum estimated monthly AWS cost is about `$0.1134` per month, rounded to about `$0.11`.

Cost breakdown by service:

- API Gateway: about `$0.0005`
  - Based on `$1.00` per `1,000,000` requests
  - `500` requests per month = `500 / 1,000,000 x 1.00 = 0.0005`

- AWS Lambda: about `$0.00135`
  - Request cost:
    - Based on `$0.20` per `1,000,000` requests
    - `500 / 1,000,000 x 0.20 = 0.0001`
  - Compute cost:
    - Based on `512 MB` memory and `3 seconds` average duration
    - `512 MB = 0.5 GB`
    - `0.5 GB x 3 seconds = 1.5 GB-seconds per request`
    - `500 x 1.5 = 750 GB-seconds per month`
    - `750 x 0.0000166667 = 0.012500025`
  - Total Lambda cost:
    - `0.0001 + 0.012500025 = 0.012600025`

- DynamoDB: about `$0.0003`
  - Based on `$0.625` per `1,000,000` write requests
  - `500 / 1,000,000 x 0.625 = 0.0003125`
  - Storage cost is effectively `$0.00` because this use case is far below the first `25 GB` free tier

- Amazon SES: `$0.10`
  - Based on `$0.10` per `1,000` emails
  - Assuming `2` emails per submission:
  - `500 submissions x 2 emails = 1,000 emails`
  - `1,000 / 1,000 x 0.10 = 0.10`

Estimated total:

- API Gateway: `$0.0005`
- Lambda: `$0.012600025`
- DynamoDB: `$0.0003125`
- SES: `$0.10`
- Total: `$0.113412525`, rounded to about `$0.11`

## Cost Observation
The overall AWS cost is expected to remain very low for this use case. Email sending through SES is likely to be the main cost component, while API Gateway, Lambda, and DynamoDB costs are comparatively small.

## Risks
- spam or bot submissions
- delays in SES production setup
- email delivery failures

## Recommendation
Proceed with the AWS serverless approach for the website contact form.

This option provides the best balance of:

- low cost
- low maintenance
- operational simplicity
- ownership of company data
- compatibility with the current website architecture

## References
- AWS Lambda pricing: https://aws.amazon.com/lambda/pricing/
- Amazon API Gateway pricing: https://aws.amazon.com/api-gateway/pricing/
- Amazon DynamoDB pricing: https://aws.amazon.com/dynamodb/pricing/on-demand/
- Amazon SES pricing: https://aws.amazon.com/ses/pricing/
- Formspree account limits: https://help.formspree.io/hc/en-us/articles/47605896654227-Account-limits
- Formspree pricing snapshot: https://www.saasworthy.com/product/formspree-io/pricing
