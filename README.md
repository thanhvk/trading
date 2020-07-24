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

## Elder impulse system & EMAs
```
// LICENSE: CC0 (https://creativecommons.org/publicdomain/zero/1.0/) for Elder Impulse code

study(title="Elder Impulse System & EMAs", shorttitle="Elder Impulse", overlay=true)

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
                       : black // If Neither Bulls or Bears Control the Market

barcolor(elder_color)

// EMA lines
ema20 = ema(close, 20)
ema50 = ema(close, 50)
ema200 = ema(close, 200)

plot(ema, color = green, title="EMA13")
plot(ema20, color = orange, title="EMA20")
plot(ema50, color = aqua, title="EMA50")
plot(ema200, color = blue, title="EMA200")
```

## Elder impulse system & EMAs & BB

study(title="Elder Impulse System & EMA lines & BB", shorttitle="Elder Impulse", overlay=true)

// Bollinger Band
length = input(20, minval=1)
src = input(close, title="Source")
mult = input(2.0, minval=0.001, maxval=50, title="StdDev")
basis = sma(src, length)
dev = mult * stdev(src, length)
upper = basis + dev
lower = basis - dev
offset = input(0, "Offset", type = input.integer, minval = -500, maxval = 500)
plot(basis, "Basis", color=#872323, offset = offset)
p1 = plot(upper, "Upper", color=color.teal, offset = offset)
p2 = plot(lower, "Lower", color=color.teal, offset = offset)
fill(p1, p2, title = "Background", color=#198787, transp=95)

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
elder_color        = elder_bulls ? color.green : elder_bears ? color.red : #0D47A1

barcolor(elder_color)

// EMA lines
ema20 = ema(close, 20)
ema50 = ema(close, 50)
ema200 = ema(close, 200)

plot(ema, color=color.green, title="EMA13")
plot(ema20, color=color.orange, title="EMA20")
plot(ema50, color=color.aqua, title="EMA50")
plot(ema200, color=color.blue, title="EMA200")
