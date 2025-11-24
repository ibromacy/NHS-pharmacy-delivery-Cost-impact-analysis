```DAX
-1. DAX measures for KPI's on dashboard1
Total Orders = 
COUNTROWS('nhs_pharma_clean')

Fulfillment Rate (%) = 
DIVIDE(
    CALCULATE(SUM('nhs_pharma_clean'[quantity_delivered])),
    CALCULATE(SUM('nhs_pharma_clean'[quantity_ordered])),
    0
) * 100

Delayed Delivery (%) = 
DIVIDE(
    [Delayed Deliveries],
    [Total Delivery],
    0
) *100

Incorrect Storage (%) = 
100 - [Correct Storage Rate (%)]

-2. DAX measures for KPI's on dashboard2
Total Delivery = 
COUNTROWS('nhs_pharma_clean')

On Time Delivery (%) = 
DIVIDE(
    [On Time Delivery],
    [Total Delivery],
    0
) *100

Delayed Delivery Cost (£) = 
CALCULATE(
    SUM('nhs_pharma_clean'[total_cost]),
    FILTER('nhs_pharma_clean', 'nhs_pharma_clean'[lead_time] > 7)

Delayed Delivery (%) = 
DIVIDE(
    [Delayed Deliveries],
    [Total Delivery],
    0
) *100

-3. DAX measures for KPI'S on dashboard3
Total Meds = 
COUNTROWS('nhs_pharma_clean')

Correct Storage Rate (%) = 
DIVIDE(
    CALCULATE(
        COUNTROWS('nhs_pharma_clean'),
        'nhs_pharma_clean'[Storage_Match] = "Correct"
    ),
    [Total Meds],
    0
)*100

Total Wastage Cost (£) = [Wastage Cost by Incorrect Storage] + [Wastage Cost by Status]

Incorrect Storage (%) = 
100 - [Correct Storage Rate (%)]







