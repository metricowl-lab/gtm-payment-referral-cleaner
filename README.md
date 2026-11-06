# Payment Referral Cleaner

A web variable template that stops payment pages being credited with sales in GA4. When a customer comes back from Klarna, Clearpay, PayPal, Stripe, a bank's 3-D Secure check or another payment page, it returns `true` for GA4's `ignore_referrer` setting. GA4 then doesn't treat that page's referrer as a traffic source, and the customer keeps the source they arrived with.

## Why

Customers who pay off-site come back from the provider's domain, and GA4 credits the sale to that referral. Paid search and Google Ads then look worse than they are. GA4's **List unwanted referrals** setting fixes this too, and you should use it, but providers use many domains and the list is easy to leave incomplete. This variable keeps a maintained list in Tag Manager. More in [Klarna, Clearpay and PayPal referrals in GA4](https://www.metricowl.co.uk/article/klarna-clearpay-paypal-referrals-ga4).

## Set up

1. Add the template from the gallery, or import `template.tpl`.
2. Create a variable from it, for example **Payment referrer**.
3. In your GA4 Google tag, add the configuration parameter `ignore_referrer` with the value `{{Payment referrer}}`.
4. Place test orders with each payment method, and check the session source in GA4's DebugView and reports.

For every other visit the variable returns nothing, so the parameter isn't sent at all.

## Settings

| Setting | What it does |
|---|---|
| Also treat bank verification pages as payment pages | Off by default. Matches hostnames starting with `acs` or `3ds`, such as `acs.bank.example`. |
| Extra payment domains | One per line, as a domain or a full address. Subdomains are included. |
| Referrer to check | Advanced: check another value instead of the page referrer |

## Built-in domains

klarna.com, klarnaservices.com, clearpay.co.uk, afterpay.com, paypal.com, zip.co, laybuy.com, stripe.com, checkout.com, adyen.com, worldpay.com, opayo.co.uk, sagepay.com, braintreegateway.com, pay.google.com and mollie.com, with their subdomains.

## Permissions

Reads the page referrer.

## Licence

Apache License 2.0. See [LICENSE](LICENSE).

Built and maintained by Marc Alexander at [Metric Owl](https://www.metricowl.co.uk), a GA4 and Google Tag Manager consultancy in London. Issues and suggestions are welcome.
