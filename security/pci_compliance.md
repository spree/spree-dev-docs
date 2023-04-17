# PCI Compliance

All store owners wishing to process credit card transactions should be familiar with [PCI Compliance](http://en.wikipedia.org/wiki/Pci\_compliance). [Spree Gateway Stripe integration](https://github.com/spree/spree\_gateway) and [Spree Braintree vzero](https://github.com/spree-contrib/spree\_braintree\_vzero) are PCI-compliant.

### Using payment tokens

We do not transmit or store Credit Card numbers. Instead we're using payment processor tokens supplied by their SDKs to authorize and charge customer cards.&#x20;

### 3-D Secure and Strong Customer Authentication support

[Spree Gateway Stripe integration](https://github.com/spree/spree\_gateway) supports [Strong Customer Authentication (SCA)](https://stripe.com/en-pl/guides/strong-customer-authentication) out of the box. Remember to use **Stripe Elements** gateway with **Payment Intents** option enabled.

[Spree Braintree vzero](https://github.com/spree-contrib/spree\_braintree\_vzero) extension supports [3D Secure 2.0](https://developers.braintreepayments.com/guides/3d-secure/overview).
