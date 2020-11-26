# Pay-as-you-go

VPN gateways support the pay-as-you-go billing method. Pay-as-you-go VPN gateways are charged and bills are generated on an hourly basis.

## Billing items

VPN gateways provide the IPsec-VPN and SSL-VPN features. IPsec-VPN and SSL-VPN are charged at different prices.

VPN gateway fee = Instance fee + Data transfer fee + SSL specification fee

-   Instance fee:

    You are charged an instance fee for each VPN gateway. The instance fee is calculated on an hourly basis. If the VPN gateway is used for less than an hour, the usage duration is rounded up to one hour.

-   Data transfer fee:

    You are charged a data transfer fee for each VPN gateway. The data transfer fee is calculated based on the outbound traffic per hour. Inbound traffic is not charged. Outbound traffic flows from the Alibaba Cloud data center to the Internet, while inbound traffic flows from the Internet to the Alibaba Cloud data center.

-   SSL specification fee:

    After the SSL-VPN feature is enabled, you must select an SSL specification based on the number of clients that you can connect at a time. Different SSL specifications are charged at different prices.

    **Note:** You are charged for using SSL-VPN only after the SSL-VPN feature is enabled.


## Instance fee

VPN gateways are provided with different bandwidth specifications. The instance fee varies by bandwidth.

**Note:** The following table lists the unit prices of different bandwidth specifications. If the unit prices in the following table are different from those on the buy page, the unit prices on the buy page shall prevail.

|Region|10 Mbit/s \(USD/hour\)|100 Mbit/s \(USD/hour\)|200 Mbit/s \(USD/hour\)|500 Mbit/s \(USD/hour\)|1000 Mbit/s \(USD/hour\)|
|:-----|:---------------------|:----------------------|-----------------------|-----------------------|------------------------|
|Mainland China|0.059|0.209|0.209|0.767|0.767|
|China \(Hong Kong\)|0.087|0.262|0.262|1.025|1.025|
|Singapore \(Singapore\)|0.087|0.262|0.262|1.025|1.025|
|Australia \(Sydney\)|0.087|0.389|0.389|1.088|1.088|
|US \(Virginia\)|0.066|0.295|0.295|0.826|0.826|
|US \(Silicon Valley\)|0.082|0.392|0.392|1.095|1.095|
|Germany \(Frankfurt\)|0.077|0.359|0.359|1.003|1.095|
|Malaysia \(Kuala Lumpur\)|0.080|0.240|0.240|0.878|0.878|
|UAE \(Dubai\)|0.090|0.420|0.420|1.231|1.231|
|Japan \(Tokyo\)|0.091|0.275|0.275|0.767|0.767|
|India \(Mumbai\)|0.082|0.249|0.249|0.697|0.697|
|Indonesia \(Jakarta\)|0.087|0.262|0.262|0.734|0.734|
|UK \(London\)|0.077|0.359|0.359|1.003|1.003|

## Data transfer fee

**Note:** The following table lists the unit prices of data transfer in different regions. If the unit prices in the following table are different from those on the buy page, the unit prices on the buy page shall prevail.

|Region|Unit price of data transfer \(USD/GB/hour\)|
|:-----|:------------------------------------------|
|Mainland China|0.125|
|China \(Hong Kong\)|0.153|
|Singapore \(Singapore\)|0.117|
|Australia \(Sydney\)|0.096|
|US \(Virginia\)|0.078|
|US \(Silicon Valley\)|0.078|
|Germany \(Frankfurt\)|0.070|
|Malaysia \(Kuala Lumpur\)|0.125|
|UAE \(Dubai\)|0.447|
|Japan \(Tokyo\)|0.120|
|India \(Mumbai\)|0.117|
|Indonesia \(Jakarta\)|0.090|

## SSL specification fee

After the SSL-VPN feature is enabled, you must select an SSL specification based on the number of clients that you can connect at a time. SSL specifications are charged at different unit prices.

**Note:** The following table lists the unit prices of different SSL specifications. If the fees in the following table are different from those the buy page, the unit prices on the buy page shall prevail.

|SSL specification|Unit price \(USD/hour\)|
|:----------------|:----------------------|
|5|0.048|
|10|0.074|
|20|0.117|
|50|0.226|
|100|0.328|
|500|1.09|
|1000|1.547|

