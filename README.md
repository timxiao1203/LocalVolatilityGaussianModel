# LocalVolatilityGaussianModel


Lognormal Gaussian Model predicts that, over time, the whole implied volatility surface evolves into a flat (i.e., skewless) surface. Local volatility models, as a class, inherently underestimate forward skew that can be critical to valuing forward start and barrier features

The local volatility Gaussian model represents a significant improvement over the existing Lognormal Gaussian Model in its ability to incorporate FX volatility skew effects and value FX-IR hybrid swaps in line with market consensus.

The model is to be used only for swaps such as those associated with Power Reverse Dual Currency FX Target Redemption Notes (PRDC FX TARNs), PRDC FX Chooser TARNs and the corresponding dual trigger structures (Power Reverse Dual Trigger FX notes and dual trigger FX Chooser TARNs).

The local volatility Gaussian model assumes that the instantaneous volatility of the instantaneous FX rate is a deterministic function of only time and the instantaneous FX rate. The model assumes that local volatility is piecewise constant in time and piecewise quadratic in the logarithm of the instantaneous FX rate where rd(t) and rf (t) are respectively the domestic and foreign instantaneous interest rates and W(t) is a Brownian motion with respect to the risk neutral measure associated with the domestic bank account numeraire. 

In the lognormal model FX volatility ¾S is assumed to be a deterministic function of time only. The implementation of the lognormal model determines ¾S(t) by iteratively calibrating the model to market data for at-the-money vanilla FX options, ignoring the fact that market data exhibits FX volatility skew or smiles where the instantaneous FX volatility ¾S is a deterministic function of both time and instantaneous spot level S(t).

In an idealized world, where market data for vanilla FX options would be available for a continuum of strikes and tenors, ¾S(t; S) is uniquely determined so Eq. 2 would constitute complete specification of the local vol model. In reality, however, market data is only available for a discrete set of strikes and tenors so that a complete specification of the model requires an assumption about the form of ¾S(t; S). 

The choice of spline knots is largely at the discretion of the model builder. The only guiding principle is that one anticipates that significant regions in S-space should roughly correspond to the range of available market strikes for each tenor. One could, for example, choose the spline knots to coincide exactly with the market strikes associated with ATM, 25Δ and 10Δ calls and puts. In any case, the specification of the spline knots is an integral part of the model's definition.

The local vol model assumes different partitions in the S dimension depending on whether or not 10Δ market data are included in the calibration. If only ATM and 25Δ calls and puts are used to calibrate the model, partitions the S-dimension for each tenor into five intervals. In what follows it will be convenient to work in terms of the dimensionless variable where N(¢) is the inverse cumulative normal function (N(0:75) ¼ 0:6745), ¾ATM is the market observed at-the-money implied FX volatility of T-expiry vanilla options, and F is the FX forward.

A general piecewise quadratic function on five intervals requires 5X3 = 15 coefficients. The requirement of constant local vol in the\extrapolated asymptote" intervals fixes the linear and quadratic coefficients in those two intervals to zero leaving 15 -  4 = 11 coefficients. 

Requiring continuity in value and first derivative at the four boundary points eliminates an additional 2 X 4 = 8 degrees of freedom leaving 11 - 8 = 3 degrees of freedom to specify ¾S(t; S). These three remaining degrees in freedom are determined by calibrating the model to market data for ATM and 25Δ calls and puts.

In this case there are naively 7 X 3 = 21 coefficients needed to specify a piecewise quadratic function. As before, 4 coefficients in the extrapolated asymptote intervals are zero, and requiring continuity in value and first derivative at the six interior points eliminates 6X2 = 12 degrees of freedom. This leaves 21 - 4 - 12 = 5 degrees of freedom to be determined by calibrating the model to five market data points corresponding to ATM, 25Δ calls, 25Δ puts, 10Δ calls and 10Δ puts.


Reference:

https://finpricing.com/lib/EqCliquet.html

https://zenodo.org/record/6611928#.YppCZKgpDq4

https://zenodo.org/record/6611928/files/localVolGaussian.pdf



