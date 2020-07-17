# trading
## EMA script

```
study(title="EMA 20/50/200", overlay=true)

ema20 = ema(close, 20)
ema50 = ema(close, 50)
ema200 = ema(close, 200)

plot(ema20, color = orange)
plot(ema50, color = aqua)
plot(ema200, color = blue)
```
