---
title: 'TradingBot: trading basis 📈'
summary: Introduction to the trading of cryptocurrencies
date: 2022-06-03T15:17:38+02:00
showtoc: false
---

### Introduction

Before going into the trading strategy, I will go through the basics of trading
and define what exactly a trading bot is. If you are already familiar with
trading, you can jump directly to the [second part of this
article](#what-is-a-trading-bot-exactly).

---

### Candlesticks

Candlesticks are a graphical representation of the evolution of the price of an
asset over a period of time. It indicates the price of the cryptocurrency at the
beginning of the period and at the end of the period, as well as the highest and
lowest price.

A green candlestick means that the price of the asset increased. A red
candlestick means that the price of the asset decreased over the period of time.

{{< figure src="images/candelsticks_hloc.png" class="only_light" >}}

{{< figure src="images/candelsticks_hloc_dark.png" class="only_dark" >}}

The periods of time are usually 1-5-15 minutes, 1-4 hours, 1-7-30 days depending
on your trading strategy.

### Positions types

There are two types of positions: *long buying* means that you speculate the
market will rise. On the other side, *short selling* means that you speculate
the market will fall.

You then have to decide the price you will place your *take-profit* and
*stop-loss* orders. If you decide to *long*, you will place a *take-profit*
order at a higher price than the one you took the position at and a *stop-loss*
order at a lower price.

{{< figure src="images/long_tp_sl.png" class="only_light" >}}

{{< figure src="images/long_tp_sl_dark.png" class="only_dark" >}}

> In this example, the *take profit* order was triggrered before the *stop loss*
> order so you made a profit. At the moment it triggered, the *stop loss* order
> has been cancelled.

### Leverage

A leverage is a ratio between the amount of money of a position and the amount
of money you use to trade. It means, that if you have a position of 25 BTC and
you use 1 BTC to trade, you will have a leverage of 25x.

It allows you to trade more money than you have in your account to increase your
profits. However, it also means that you will lose more money if the market goes
down.

Liquidation can occur when the market falls and the amount of money you place
for your position does not cover the loss. You will lose your position, leading
to a full loss of your equity.

### What is a trading bot exactly?

A trading bot is a computer program that automatically trades cryptocurrencies
based on given market conditions. It tries to predict market oscillations to
take positions and make profit.

It implements a trading strategy which specifies how to trade. For example, a
strategy can be to *long* if yesterday's closing price is lower than its opening
price and to *short* if yesterday's closing price is higher than its opening
price.

The major goal of the implementation of a trading bot is to find and develop a
trading strategy. There exist many strategies like grid trading, pair trading
and news trading, but it basically takes some inputs and give actions through
outputs.

For the implementation I have been working on, I have used the following inputs
and outputs:

{{< figure src="images/abstract_trading_strategy.png" class="only_light" >}}

{{< figure src="images/abstract_trading_strategy_dark.png" class="only_dark" >}}

On the left side, you can see the inputs of the trading strategy. It needs to
know the current market price, the price history of the asset, the current
positions, and the available balance of the user.

After processing the inputs, the trading strategy outputs two lists. The first
one lists the orders to place to take positions, and the second one lists the
positions to close based on the given current positions. Those two lists can be
empty if the strategy does not want to take or close any position.

---
### Conclusion

Having a good understanding of the basics of trading is mandatory if you want to
make a trading bot. It is also important to define your inputs and outputs for
your strategy, as it will save you a lot of time when actually implementing it.

In the next article, I will start the implementation of the strategy for the
trading bot using Golang. I will also show you how to gather data to back-test
your strategy.
