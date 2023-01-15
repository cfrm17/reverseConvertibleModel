# Reverse Convertible Model

The payoff of reverse convertible product involves returns on multiple assets and is conditional on hitting of continuous barriers. The Monte Carlo methodology employed by ESP is an efficient conditioning technique.

This is the first structured product that uses this technique (the need for it is due to the presence of multiple underlyings and continuous barriers). It outputs three biased prices (upper and lower bound prices, and an intermediate one). This bias is additional to the usual Monte Carlo statistical error (treated by ESP through implementing both Monte Carlo and Quasi Monte Carlo techniques, a number of variance reduction methods, and, of course, through running sufficiently high number of simulations).

A multi-asset Reverse Convertible deal is defined by the following payoff (to be paid at expiry in the fixed payoff currency):

 

Or, equivalently:

 

Where D is the coupon rate (see https://finpricing.com/lib/IrBasisCurve.html)

Note that in this report we only see this payoff as a being quanto (it depends on different foreign stock returns and barrier hitting events, but it pays in one fixed currency – see below the quanto correction for stock dynamics). 

As this payoff involves continuous barriers, the expectation of this payoff can be calculated using a version of conditional Monte Carlo method as per reference [1]. Biased upper and lower estimator bounds plus a biased price placed between these bounds (using a stock event independence assumption) are proposed. We describe this method below.

Based on above payoff re-write, the price of a Reverse Convertible on single asset is the difference between the price of a Cash-or-Nothing European Digital Call with rebate C and a Down and In Put with strike K , B barrier strike, notional N K , to which the notional is added. Accordingly, one has a closed-form pricing available. 

Arbitrage is possible if, for example, the market uses models that consistently incorporate volatility smile when pricing the simpler Digitals and Barriers, but uses models that do not incorporate it or do incorporate it in an ad hoc manner when pricing Reverse Convertible on single asset (same ideas apply to internal arbitrage too).

We describe here the method. Consider the following general payoff:

 

We are interested in computing its expectation (under risk-neutral measure P ). Note that we have:

 

An unbiased estimator is

 

Where

 

For each j = 0,1,...,m −1 denote:

 

One approximation of j is obtained by assuming event independence:

 


Note that j is between and . Independent version P P (L) j P (U) j P (I ) j is also between P (L) and j P (U) j  and can be used as approximation for . The following Brownian bridge probability formula completes the picture:

 

The value of (the expectations of) and is that they are safe bounds (the real price is between them with high probability). Intuitively, their average L Q U Q ( ) 2 L U Q + Q would be a good choice as an estimator of the real price. Moreover, Greeks obtained out of this average would be automatically between the Greeks obtained out of L and . According to Shevchenko is a better estimator than ( )2 L U Q + Q . Consequently, ESP adopts as “the price” and computes Greeks off it. The relation between Greeks obtained from and Greeks obtained from and is unclear. One can only hope that for high reset frequency and high number of simulations these Greeks fall in line just like the prices do. 

For single asset this Brownian Bridge simulation fully eliminates pricing bias that arises in applications of discretized Monte Carlo to evaluate options with continuous barriers (all three prices presented above are the equal).

