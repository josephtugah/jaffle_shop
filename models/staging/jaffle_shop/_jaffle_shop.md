{% docs order_status %}
    
One of the following values: 

| status         | definition                                       |
|----------------|--------------------------------------------------|
| placed         | Order placed, not yet shipped                    |
| shipped        | Order has been shipped, not yet been delivered   |
| completed      | Order has been received by customers             |
| return pending | Customer indicated they want to return this item |
| returned       | Item has been returned                           |

{% enddocs %}


{% docs order_status_src %}
    
One of the following values for order status:

| status         | definition                                            |
|----------------|-------------------------------------------------------|
| placed         | Order has been placed, but not yet shipped.           |
| shipped        | Order has been shipped, but not yet delivered.        | 
| completed      | Order has been received by the customer.              |
| return_pending | Customer has indicated they want to return this item. |
| returned       | Item has been returned by the customer.               |

{% enddocs %}


{% docs first_name %}
The first name of the customer.   
{% enddocs %}

{% docs last_name %}
The last name of the customer.    
{% enddocs %}

{% docs order_date %}
The date order was placed.
{% enddocs %}

{% docs num_of_orders %}
The total count of orders placed by the customer. 
{% enddocs %}

{% docs first_order_date %}
Date when customer made last order. NULL when a customer has not yet placed an order.
{% enddocs %}