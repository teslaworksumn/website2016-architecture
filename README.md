# website2016-architecture
Software architecture for the 2016 website overhaul.

## General Architecture

The website will be statically generated. There is one type of dynamic content:
displaying a feed of Facebook events from the Tesla Works UMN organization. We
also need to allow users to subcribe to our mailing list, which will require
server side processing to integrate with Mailchimp's API. Due to low request
volume, this backend will be hosted on a serverless compute engine fronted by
a HTTP endpoint

For editing text or image content (not layout), we should have a script to
one-step recompile the website and upload it to the host.

## Pricing

We should aim to have entirely free hosting. Mailchimp will require around 20
requests per month

- Github Pages for static site hosting
  - Free
- AWS Lambda for serverless compute
  - Free for 1,000,000 requests / month
- AWS API Gateway for HTTP endpoints
  - $3.50 per 1,000,000 calls
    - Free 1,000,000 calls per month for 12 months
  - $0.09 per GB transferred out for first 10TB.
  - Expected cost: < $0.01/month

## Concerns

- Making sure we don't get spammed with Mailchimp requests
  - Doesn't happen now
  - Mailchimp will throttle us at 10 concurrent requests
  - Could bother our Lambda costs.
    - Set maximum request rate limit in Lambda? *TODO*
