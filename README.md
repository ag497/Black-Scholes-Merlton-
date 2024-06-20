# Black-Scholes-Merlton-Model

Python Implementation of the Black Scholes Merlton Model from scratch, including First Order Greeks and Second Order Greeks.

## Overview

The Black Scholes Merlton Model is used to price assets that follow Geometric Brownian Motion, with their derivatives following Ito's process.

### Assumptions of the Model:

1. The underlying asset prices (S) follow a log-normal Random Walk.
2. Risk-free interest rate (r) and asset volatility (sigma) are known functions over the life of the option.
3. No transaction costs for hedging.
4. No arbitrage conditions.
5. Trading is continuous.
6. Shorting is allowed, and assets are divisible.

### Mathematical Derivation:

The BSM stochastic partial differential equation is derived as follows:

For the asset price (S):

dS/S = μdt + σdW

where μ is the drift parameter, σ is the volatility parameter, and dW is the Wiener process.


For the derivative (V):

dV = (∂V/∂t + μ ∂V/∂S + 1/2 σ^2 ∂^2V/∂S^2)dt + σ(∂V/∂S)dW

where V is the option, ∂V/∂t is the time rate, ∂V/∂S  is the slope, and ∂^2V/∂S^2 is the curvature term.


### Delta Hedging:

To price any derivative, we construct an equivalent portfolio π:

π = V - ΔS 

which implies

dπ = dV - ΔdS

where Δ represents the number of underlying shares.

By using the delta hedging technique 

dπ = (∂V/∂t + μ ∂V/∂S + 1/2 σ^2 ∂^2V/∂S^2)dt + σ(∂V/∂S)dW -Δ(μSdt + σSdW),

we remove stochasticity from our equation to make overall portfolio sensitivity to price fluctuations 0.

### Technique:
make Δ= ∂V/∂S

This is also called the hedge ratio and this removes the stochasticity or randomness by eliminating the dW term (Weiner Process) from our equation.

dπ = (1/2 σ^2 S^2 ∂^2V/∂S^2 + ∂V/∂t)dt

Now we can either buy insurance with this or we can invest in savings bank account and while pricing under no arbitrage condition both situations must give same return:

return in savings bank account = rπdt

rπdt = (1/2 σ^2 S^2 ∂^2V/∂S^2 + ∂V/∂t)dt


(if it is unequal then arbitraging condition exists in market)

### Black-Scholes-Merlton Equation:

By substituting and solving this equation we get our BSM SPDE:

∂V/∂t + 1/2 σ^2 S^2 ∂^2V/∂S^2 + rS ∂V/∂S + rV=0

2 striking features of this model are:

1.no drift parameter present in our BSM SPDE.

2.delta hedging (Δ= ∂V/∂S) indicates correlation of option price with stock price

## Solution for European Options:

### European Call:

C(S,t) = S N(d1) - E e^(-r(T-t)) N(d2)

### European Put:

P(S,t) = E e^(-r(T-t)) N(-d2)- S N(-d1)

where E is strike price, N is std normal distribution function, d1 and d2 are params estimated as follows:

d1 = (ln(S/X) + (r + 0.5σ^2)(T-t)) / (σ√(T-t))

d2 = d1 - σ√(T-t)

### Hedge Ratios for Call and Put:

Δ=∂C/∂S=N(d1) for CALL

Δ=∂P/∂S=N(d1)-1 for PUT





