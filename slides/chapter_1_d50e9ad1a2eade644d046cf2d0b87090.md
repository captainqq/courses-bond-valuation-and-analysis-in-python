---
key: d50e9ad1a2eade644d046cf2d0b87090
title: 'Insert title here'
---

## Title Slide

```yaml
type: TitleSlide
key: 7b4bc7abbd
```

`@lower_third`
name: Chelsea Yang
title: Instructor at DataCamp

`@script`
In this chapter you have learned the yield to maturity (YTM) as an important concept for measuring a bond's internal rate of return. You also have learned various factors that may affect a bond's yield. Now let us learn how to estimate the yield to maturity of a bond using Python.

---

## Bond Pricing Formula

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
Recall that we can obtain the current price of a plain vanilla fixed bond by calculating its present value. It equals to the sum of expected future cash flows, discounted back using the bond's yield to maturity.
 
Here is the handy formula for it, by plugging in the bond's coupon (C), maturity (n), and yield to maturity (r), we can easily obtain the price.
 
Conversely, if we are given the current bond price, we can estimate its yield to maturity by finding the root of this quadratic function. This is usually done by trial and error. In other words, we start by guessing a number as the proximate yield, then use it to calculate a price. Make some adjustments to the yield for a better guess, then calculate the price again. Do this iteratively, until we get a price equals to the actual market traded price.

---

## Estimate YTM with Python

```yaml
type: FullSlide
key: d0ca271956
```

`@part1`
### Automate the YTM estimation by writing a python function

```python
def bond_ytm(price, par, T, coup, freq=2, guess=0.05):
    freq = float(freq)
    periods = T * freq
    coupon = coup/100. * par/freq
    dt = [(i+1)/freq for i in range(int(periods))]
    ytm_func = lambda y:\
    sum([coupon/(1+y / freq)**(freq* t) for t in dt])+\
    par / (1+y / freq)**(freq*max(dt))-price
    ytm = optimize.newton(ytm_func, guess) * 100
    return round(ytm, 2)

```

`@script`
* Thanks to python, we don’t need to play this inefficient guessing game. We can automate this yield calculating process by using the python package scipy. 
 
Here the code demonstrates how to write a python function to estimate a bond yield. First we implement the bond pricing formula in ytm_func. Second, we use ‘optimize’ method from the scipy package to solve the root. The goal is to make the calculated bond price equal to the market quoted price, so that ytm_func equals to zero. By default the scipy optimize function uses the classic ‘Newton Method’ to numerically search for the root. We pass two required parameters: 1) the function (whose zero is wanted), and 2) an initial guess. Voila, it will output the estimated yield.


---

## Let's practice!

```yaml
type: FinalSlide
key: 75fba13a45
```

`@script`
