## 🔍 Portal options

| Gateway                     | Android SDK / Support                                                      | What is free / what you pay                                                                                        |
| --------------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Google Pay**              | Yes, there’s the Google Pay API for Android. ([Google for Developers][1]) | Free to integrate. No extra fee from Google for merchants (just the usual card/processor fees). ([ScaleupAlly][2]) |
| **Stripe**                  | Yes,  Stripe’s Android SDK is solid. ([GitHub][3])                         | No setup / monthly fee; you pay per-transaction. “Free integration” in terms of SDK cost. ([GeeksforGeeks][4])     |
| **PayPal**                  | Yes,  PayPal Mobile Android SDK. ([PayPal Developer][5])                   | Same deal: free SDK / dev account; transaction fees apply. ([PayPal Developer][5])                                 |
| **Square**                  | Yes,  has Mobile Payments / SDKs. ([Square][6])                            | SDK is free; but only available fully to merchants in certain countries. Transaction fees apply. ([Square][6])     |
| **Amazon Payment Services** | Yes,  they offer a mobile SDK for Android. ([Amazon Payment Services][7])  | Free to download & integrate; transaction charges apply. ([Amazon Payment Services][7])                            |
| **Cashfree**                | Yes,  there is an Android SDK. ([GitHub][8])                               | Same model: no SDK cost, pay per transaction. ([agilie.com][9])                                                    |

---

## ⚠️ Caveats / what to check

* Even if the SDK / integration is free, **transaction fees** (percentage + maybe fixed amount) are almost always there.
* Location matters. Some gateways are only available in certain countries. If you’re in South Africa, check whether the gateway supports South African merchants / ZAR, etc.
* Compliance (like PCI-DSS) may require you to do some extra work if you’re handling card data directly vs using their hosted UI / tokenisation.
* Currency conversion fees, cross-border fees, etc could apply.

---

[1]: https://developers.google.com/pay/api/android/overview?utm_source=chatgpt.com "Overview | Google Pay API for Android"
[2]: https://scaleupally.io/blog/mobile-payment-gateway/?utm_source=chatgpt.com "Top 13 Mobile Payment Gateway Solutions [2025]"
[3]: https://github.com/stripe/stripe-android?utm_source=chatgpt.com "Stripe Android SDK"
[4]: https://www.geeksforgeeks.org/blogs/top-payment-gateway-apis-that-every-developer-must-know/?utm_source=chatgpt.com "Top 7 Payment Gateway APIs That Every Developer Must ..."
[5]: https://developer.paypal.com/docs/checkout/advanced/android/?utm_source=chatgpt.com "Integrate Card Payments in Android Apps with PayPal SDK"
[6]: https://developer.squareup.com/docs/mobile-payments-sdk/android?utm_source=chatgpt.com "Build on Android - Mobile Payments SDK"
[7]: https://paymentservices.amazon.com/docs/EN/23c.html?utm_source=chatgpt.com "Integrating the Android SDK"
[8]: https://github.com/cashfree/nextgen-android?utm_source=chatgpt.com "cashfree/nextgen-android: Sample app demonstrating ..."
[9]: https://agilie.com/blog/11-best-payment-gateways-to-choose-for-your-android-app?utm_source=chatgpt.com "11 Best Payment Gateways for Android App Integration"
