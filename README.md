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

## Elder impulse system

```
// LICENSE: CC0 (https://creativecommons.org/publicdomain/zero/1.0/)

study(title="Elder Impulse System", shorttitle="Elder Impulse", overlay=true)

source = close

// MACD Options
macd_length_fast   = input(defval=12, minval=1, title="MACD Fast Length")
macd_length_slow   = input(defval=26, minval=1, title="MACD Slow Length")
macd_length_signal = input(defval=9,  minval=1, title="MACD Signal Length")
// Calculate MACD
macd_ma_fast       = ema(source, macd_length_fast)
macd_ma_slow       = ema(source, macd_length_slow)
macd               = macd_ma_fast - macd_ma_slow
macd_signal        = ema(macd, macd_length_signal)
macd_histogram     = macd - macd_signal

// EMA Option
ema_length         = input(defval=13, minval=1, title="EMA Length")
// Calculate EMA
ema                = ema(source, ema_length)

// Calculate Elder Impulse
elder_bulls        = (ema[0] > ema[1]) and (macd_histogram[0] > macd_histogram[1])
elder_bears        = (ema[0] < ema[1]) and (macd_histogram[0] < macd_histogram[1])
elder_color        = elder_bulls
                     ? green //  If Bulls Control Trend and Momentum
                     : elder_bears
                       ? red //  If Bears Control Trend and Mementum
                       : blue // If Neither Bulls or Bears Control the Market

barcolor(elder_color)
```
