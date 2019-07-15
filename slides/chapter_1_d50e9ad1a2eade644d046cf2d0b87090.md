---
key: d50e9ad1a2eade644d046cf2d0b87090
title: 'Insert title here'
---

## Estimating YTM of a plain vanilla bond

```yaml
type: TitleSlide
key: 7b4bc7abbd
```

`@lower_third`
name: Chelsea Yang
title: Instructor at DataCamp

`@script`
In this chapter you have learned that yield to maturity is a key concept for measuring a bond's internal rate of return, and various risk factors may affect the yield. Now let us learn how to estimate the bond yield using Python.

---

## YTM and Bond Pricing Formula

```yaml
type: TwoRows
key: d16a187084
```

`@part1`
## Bond price: present value of expected future cash flows

![](https://assets.datacamp.com/production/repositories/5224/datasets/6a4e1ff013a83e42e8383cabea18b37704e67154/BondPrice_Formula.png){{2}}

`@part2`
## Yield of maturity: solving the root by trial and error

`@script`
Recall we can obtain the current price of a plain vanilla fixed bond by calculating its present value. It equals to the sum of expected future cash flows, discounted using the bond's yield to maturity.
 
Here is the handy formula for it, by plugging in the bond's coupon (C), maturity (n), and yield (r), we can easily obtain the price.
 
Conversely, if we are given the current bond price, we can estimate its yield by finding the root of this quadratic function. This is usually done by trial and error. In other words, we start by guessing a number as the approximate yield, then use it to calculate a price. Make some adjustments to the yield for a better guess, then calculate the price again. Do this iteratively, until we get a price equals to the actual market traded price.

---

## Estimate YTM with Python

```yaml
type: FullSlide
key: d0ca271956
```

`@part1`
## _from scipy import optimize_

```python
def bond_ytm(price, par, T, coup, freq=2, guess=0.05):
    coupon = coup/100. * par/freq
    dt = [(i+1)/freq for i in range(int(T * freq))]
    
    ytm_func = lambda y:\
    sum([coupon/(1+y / freq)**(freq* t) for t in dt])+\
    par / (1+y / freq)**(freq*max(dt))-price
    
    ytm = optimize.newton(ytm_func, guess) * 100
    return round(ytm, 2)

```

`@script`
Thanks to python, we don't need to play this inefficient guessing game. We can automate it using the python package scipy. 
 
Here the code demonstrates how to write a python function to estimate bond yield. First we implement the bond pricing formula in ytm_func. Second, we use ‘optimize’ method from the scipy package to solve the root. The goal is to make the calculated bond price equal to the market quoted price, so that ytm_func equals to zero. By default the scipy optimize function uses the classic ‘Newton Method’ to numerically search for the root. We pass two required parameters: 1) the function (whose zero is wanted), and 2) an initial guess. Voila, it will output the estimated yield.

---

## YTM of a US Treasury

```yaml
type: TwoRows
key: 7b3d2be1fd
```

`@part1`
![](https://assets.datacamp.com/production/repositories/5224/datasets/f2746e231f1df8bb1279cc80934cb9bcb69928d2/GovBond_US_sm.png){{1}}

`@part2`
```python
ytm_US = bond_ytm(99.43, 100, 5, 1.75, 2) #result:1.87
```
{{2}}

`@script`
Let us test this code in the field. Here we have traded US government bonds information from Bloomberg. Take the 5Y US treasury for example. We can input its coupon 1.75%, price $99.43, maturity 5Y to our python function and solve for the yield. Note in general government bonds pay coupons twice a year, so the payment frequency is set to 2. We obtain the yield 1.87%, which aligns with Bloomberg market data.
 
Also notice: since this US treasury bond is priced slightly below par, its yield (1.87%) is higher than its coupon rate (1.75%) as expected.

---

## YTM of a German government bond

```yaml
type: TwoRows
key: 1992ae2c69
```

`@part1`
![](https://assets.datacamp.com/production/repositories/5224/datasets/bddeeb7ba834550ac5af13a77b584371cd6f73a5/GovBond_Germany_sm.png){{1}}

`@part2`
![](https://assets.datacamp.com/production/repositories/5224/datasets/3f5ce67d4f2cbab3e2698ee63e8d470f6f4374f2/YTM_GM10Y.png =80){{2}}

`@script`
Here is another example: let us calculate the yield for a German government bond. Given the 10Y bond with coupon 0, price 102.17, the yield we get is -0.21%.
 
Yes, we do live in a strange economic environment nowadays where bond yield can be negative. Government of Japan and some European countries have implemented negative interest rate policies in recent years, due to their sluggish economic growth and lower than expected inflation rates. 
 
What does negative yield mean? Intuitively it means if you buy the bond, you are guaranteed to lose money. But why would any rational investors do that? For one thing, large institutional investors, such as mutual funds, insurance companies, etc, may hold negative yielding bonds in order to comply with their investment mandates,  diversification needs, or regulatory requirements. There are also some investors choose to hold negative yielding foreign bonds, hoping to take advantage of the currency appreciation. That is, the gain from foreign currency strengthening can offset the loss from the bonds.

---

## Let's practice!

```yaml
type: FinalSlide
key: 75fba13a45
```

`@script`
Now It is time to get your hands dirty.
