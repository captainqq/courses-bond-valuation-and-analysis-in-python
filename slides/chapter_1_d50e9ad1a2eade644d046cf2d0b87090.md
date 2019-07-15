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
# **- Bond price: present value of expected future cash flows**
![](https://assets.datacamp.com/production/repositories/5224/datasets/6a4e1ff013a83e42e8383cabea18b37704e67154/BondPrice_Formula.png)

`@part2`
# - Yield of maturity: solving the root by trial and error

`@script`
Recall that we can obtain the current price of a plain vanilla fixed bond by calculating its present value. It equals to the sum of expected future cash flows, discounted back using the bond's yield to maturity.
 
Here is the handy formula for it, by plugging in the bond's coupon (C), maturity (n), and yield to maturity (r), we can easily obtain the price.
 
Conversely, if we are given the current bond price, we can estimate its yield to maturity by finding the root of this quadratic function. This is usually done by trial and error. In other words, we start by guessing a number as the proximate yield, then use it to calculate a price. Make some adjustments to the yield for a better guess, then calculate the price again. Do this iteratively, until we get a price equals to the actual market traded price.


---

## Let's practice!

```yaml
type: FinalSlide
key: 75fba13a45
```

`@script`
