# Black-Scholes-Merlton-Model
Python Implementation of Black Scholes Merlton Model from scratch along with First Order Greeks and Second Order Greeks:
Black Scholes Merlton Model is used to price any asset that follows Geometric Brownian Motion and its derivative follows Ito's process.
Assumptions of the model:-
1.The underlying asset prices(S) follow log-normal Random Walk.
2.Riskfree IR (r) and asset volatility (sigma) are known functions of time over life of option
3.No transaction costs for hedging.
4.No arbitrage condition.
5.Trading is continuous.
6.Shorting is allowed and assets are divisible.
The BSM stochastic partial differential equation has been derived as follows:
dS/S = μdt + σdW (asset price follows Geometric Brownian Motion)
where μ is drift parameter and σ is diffusion/volatility parameter and dW is Wiener process
dV = (∂V/∂t + μ ∂V/∂S + 1/2 σ^2 ∂^2V/∂S^2)dt + σ(∂V/∂S)dW (Derivative follows Ito's Lemma Process)
where V is the option, ∂V/∂t is the time rate, ∂V/∂S is the slope and ∂^2V/∂S^2 is the curvature term
To price any derivative, we build an equivalent portfolio π.
π consists of one option V and a certain number(Δ) of underlying shares:
π = V - ΔS
dπ = dV - ΔdS
dπ = (∂V/∂t + μ ∂V/∂S + 1/2 σ^2 ∂^2V/∂S^2)dt + σ(∂V/∂S)dW -Δ(μSdt + σSdW)
Use delta hedging technique to make overall portfolio sensitivity to price fluctuations 0.
(make Δ= ∂V/∂S) this is also called the hedge ratio and this removes the stochasticity or randomness by eliminating the dW term (Weiner Process) from our equation
dπ = (1/2 σ^2 S^2 ∂^2V/∂S^2 + ∂V/∂t)dt
Now we can either buy insurance with this or we can invest in savings bank account and while pricing under no arbitrage condition both situations must give same return.
return in savings bank account = rπdt
rπdt = (1/2 σ^2 S^2 ∂^2V/∂S^2 + ∂V/∂t)dt
(if it is unequal then arbitraging condition exists in market)
By substituting and solving this equation we get our BSM SPDE:
∂V/∂t + 1/2 σ^2 S^2 ∂^2V/∂S^2 + rS ∂V/∂S + rV=0
 2 striking features of this model  are:
 1.no drift parameter present in our BSM SPDE.
 2.delta hedging (Δ= ∂V/∂S) indicates correlation of option price with stock price
 Solution To BSM Equation for European Options:
 EUROPEAN CALL:
 C(S,t) = S N(d1) - E e^(-r(T-t)) N(d2)
EUROPEAN PUT:
P(S,t) = E e^(-r(T-t)) N(-d2)- S N(-d1)
where E is strike price, N is std normal distribution function, d1 and d2 are params estimated as follows:
d1 = (ln(S/X) + (r + 0.5σ^2)(T-t)) / (σ√(T-t))
d2 = d1 - σ√(T-t)
Hedge Ratios for Call and Put:
Δ=∂C/∂S=N(d1) for CALL
Δ=∂P/∂S=N(d1)-1 for PUT



