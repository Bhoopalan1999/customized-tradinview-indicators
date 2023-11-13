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

