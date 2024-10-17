{% docs payment_status %}

One of the following values:

| status  | definition                             |
| ------- | -------------------------------------- |
| success | Payment was processed successfully     |
| failure | Payment was not completed successfully |

{% enddocs %}

{% docs payment_method %}

One of the following values: 

| payment_method | definition                                |
|----------------|--------------------------------------------|
| bank_transfer  | Payment made directly via bank transfer   |
| coupon         | Payment made using a discount coupon      |
| credit_card    | Payment made using a credit card          |
| gift_card      | Payment made using a gift card            |

{% enddocs %}
