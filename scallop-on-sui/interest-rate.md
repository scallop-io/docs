---
description: >-
  Smart contracts on Sui are upgradable, so these are the Scallop V1 starting
  parameters.
---

# Interest Rate

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption><p>Dual-Line Interest Rate Mode</p></figcaption></figure>

Scallop is currently using the "Dual-Line Interest Rate Model with Optimal Interest Rate at 80% Utilization Rate and 8% Interest APR": In this model, the X-axis represents the capital utilization rate, while the Y-axis represents the interest APR. This model is designed to achieve an 8% interest rate when the capital utilization rate is at 80%.

Mathematically, the dual-line interest rate model can be represented using two linear functions, where the optimal interest rate occurs at the intersection point of these functions. The functions are defined as follows:

1.  For utilization rates (U) less than or equal to 80%:

    Interest APY = m1 \* U + b1
2.  For utilization rates (U) greater than 80%:

    Interest APY = m2 \* (U - 80%) + b2

Here, m1 and m2 represent the slopes of the respective lines, and b1 and b2 are the Y-intercepts. The coefficients are chosen to ensure a smooth transition between the two lines at the 80% utilization rate, creating an optimal interest rate model for both lenders and borrowers. The intersection point of these two linear functions will have a capital utilization rate of 80% and an interest APR of 8%.
