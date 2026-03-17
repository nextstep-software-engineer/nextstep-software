# Architecture Discussion Record
# ADR-001: Serverless Contact Form Handling for Website Contact Page

## Status
Proposed

## Date
2026-03-12

## Executive Summary
This draft proposes implementing backend handling for the existing website contact form using AWS serverless services managed by our team. The proposed solution uses Amazon API Gateway, AWS Lambda, Amazon DynamoDB, and Amazon SES to receive, validate, store, and email contact form submissions.

This approach is recommended because it has low operating cost, low maintenance overhead, and fits well with the current static Astro website.

## Decision Summary
Build and operate the website contact form in-house using AWS serverless services:

- Amazon API Gateway HTTP API to receive form submissions
- AWS Lambda to validate and process requests
- Amazon DynamoDB to store submissions
- Amazon SES to send notification and acknowledgement emails

This implements backend processing for the current static contact form, which does not submit data today.

## Problem Statement
The current website contact form is visible to users but does not submit data to any backend service. As a result, the company cannot reliably receive enquiries from the website, retain submission records, or trigger notification emails for follow-up.

The business needs a simple and maintainable solution that:

- accepts contact form submissions from the website
- stores submissions for reference and audit purposes
- sends email notifications to the internal team
- optionally sends confirmation emails to the submitter
- avoids the overhead of running and maintaining a traditional backend server

## Current State
- The site is a static Astro website.
- The contact form currently prevents default submit behavior and does not send data anywhere.
- There is no backend, persistence, anti-spam flow, or operational monitoring for form submissions.

## Scope
Included in scope:

- Contact form submission endpoint
- Server-side validation
- Submission storage
- Internal notification email
- Optional acknowledgement email to the submitter
- Basic operational monitoring

## Decision Drivers
- Low running cost
- Minimal infrastructure management
- Good fit for bursty or low-volume traffic
- Easy operational scaling
- Ability to store submissions for audit and follow-up
- Ability to notify internal recipients by email
- Fast implementation without introducing a full backend platform

## Proposed Architecture
### High-Level Flow
1. User submits the contact form from the website.
2. Frontend sends an HTTPS POST request to API Gateway.
3. API Gateway invokes Lambda.
4. Lambda validates and sanitizes the payload.
5. Lambda writes the submission to DynamoDB.
6. Lambda sends notification email through SES.
7. Lambda optionally sends an acknowledgement email to the submitter.
8. Lambda returns success or validation error response to the website.

### AWS Components
- API Gateway HTTP API
  - Public HTTPS endpoint for `/contact`
  - Request throttling and CORS handling
- Lambda
  - Stateless request handler
  - Input validation, spam checks, persistence, and SES integration
- DynamoDB
  - Stores each contact request as an item
  - Supports audit trail and follow-up reporting
- SES
  - Sends internal notification email
  - Optionally sends confirmation email to the user

## Architecture Rationale
This solution is recommended for the following reasons:

- The website is already static, so a serverless backend is a natural extension.
- Contact form traffic is expected to be low to moderate, which makes pay-per-use services cost-effective.
- The proposed architecture avoids maintaining application servers, operating systems, or background services.
- AWS managed services provide sufficient scalability and reliability for this use case.
- The architecture can be extended later if the company wants to add CAPTCHA, CRM integration, or reporting.

## Recommended Data Model
### DynamoDB Table
Table name example: `contact-submissions`

Suggested attributes:
- `submissionId` as partition key
- `createdAt`
- `name`
- `email`
- `message`
- `sourcePage`
- `status`
- `ipHash`
- `userAgent`

Notes:
- Store hashed IP rather than raw IP if privacy requirements are strict.
- Add TTL only if submissions should expire automatically.

## Security And Compliance Considerations
- Validate all input server-side in Lambda.
- Use API Gateway throttling to reduce abuse.
- Add CAPTCHA or bot protection if spam becomes a problem.
- Restrict SES sender identities and verify domains.
- Encrypt data at rest using AWS-managed encryption.
- Avoid storing unnecessary personal data.
- Define retention policy for contact submissions.
- Log errors and metrics to CloudWatch.

## Non-Functional Considerations
- Availability: AWS managed services provide good availability for low-complexity workloads.
- Scalability: The solution scales automatically with traffic.
- Maintainability: The design is small and isolated, making it easier to support.
- Auditability: DynamoDB storage provides a simple record of submitted enquiries.
- Performance: Contact form processing should complete within a few seconds under normal conditions.

## Operational Considerations
- Use CloudWatch logs and alarms for Lambda errors and throttles.
- Add dead-letter or retry handling if email send fails.
- Return user-friendly frontend messages for validation and transient errors.
- Use infrastructure as code for repeatable deployment.
- Prefer API Gateway HTTP API over REST API because it is cheaper for this use case.

## Risks And Mitigations
- Spam or bot traffic
  - Mitigation: rate limiting, CAPTCHA, hidden honeypot field, validation
- Missed notifications if SES send fails
  - Mitigation: persist first in DynamoDB, then alert on send failures
- Privacy concerns around stored contact data
  - Mitigation: minimize stored fields and define retention policy

## Rollout Plan
1. Build Lambda handler and validation logic.
2. Create API Gateway HTTP API endpoint.
3. Create DynamoDB table.
4. Configure SES sender identity and recipient flow.
5. Wire frontend form to the endpoint.
6. Add monitoring, throttling, and spam protection.
7. Test happy path, validation failures, and email failures.
8. Release to production and monitor initial traffic.

## Cost Estimate
## Assumptions
- Region pricing reference: `us-east-1` style public AWS pricing examples; actual region pricing may vary.
- One API request per form submission.
- Lambda memory: `512 MB`
- Lambda duration: `3 seconds`
- One DynamoDB write per submission.
- Average stored submission size: `5 KB`
- Two SES emails per submission:
  - one internal notification
  - one acknowledgement to the sender
- CloudWatch and data transfer costs are small and excluded from the main estimate.

## Public AWS Pricing Used
- Lambda requests: `$0.20 per 1 million requests`
- Lambda compute: `$0.0000166667 per GB-second`
- API Gateway HTTP API: `First 300 million requests per month: $1.00 per million`
- API Gateway HTTP API: `300+ million requests per month: $0.90 per million`
- DynamoDB on-demand writes: `$0.625 per 1 million writes`
- DynamoDB on-demand reads: `$0.125 per 1 million reads`
- DynamoDB Standard table class storage: `First 25 GB stored per month is free`
- DynamoDB Standard table class storage after free tier: `$0.25 per GB-month`
- SES outbound email: `$0.10 per 1,000 emails`

## Estimated Monthly AWS Run Cost
For minimum expected volume, using a low-traffic contact form assumption of around `500 submissions per month`:

- API Gateway: about `$0.0005`
- Lambda request + compute: about `$0.0126`
- DynamoDB write + storage: about `$0.0003`
- SES for 1,000 emails: about `$0.10`
- Total: about `$0.1134` per month, rounded to about `$0.11`

## Cost Observation
For this architecture, SES is likely to be the main ongoing cost driver. API Gateway, Lambda, and DynamoDB remain very inexpensive at typical contact-form volumes.

## Recommendation
Proceed with the AWS serverless option using API Gateway HTTP API, Lambda, DynamoDB, and SES.

This is the preferred option because it provides:

- low monthly operating cost
- low maintenance overhead
- full ownership of submission data
- straightforward integration with the current website
- a clean path for future enhancements

For the current requirement, this option offers the best balance of simplicity, cost, and operational control.

## Source Links
- AWS Lambda pricing: https://aws.amazon.com/lambda/pricing/
- Amazon API Gateway pricing: https://aws.amazon.com/api-gateway/pricing/
- Amazon DynamoDB on-demand pricing: https://aws.amazon.com/dynamodb/pricing/on-demand/
- Amazon SES pricing: https://aws.amazon.com/ses/pricing/
