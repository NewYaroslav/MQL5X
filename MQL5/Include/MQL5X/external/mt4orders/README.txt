MT4Orders.mqh — MT4-like Order Management for MQL5
--------------------------------------------------

This library provides a compatibility layer that mimics the MetaTrader 4 order management functions,
allowing easier porting of code from MT4 to MT5. It emulates common functions like OrderSend(),
OrderSelect(), OrderModify(), and OrderClose().

All MQL5 trading operations are internally based on MQL5 trade classes (e.g. CTrade), but the API surface
provided by MT4Orders resembles the old procedural style used in MQL4.

The library is written entirely in MQL5 and uses no DLLs.

------------------------------------------------------------
Features

- Emulates most commonly used MQL4 order functions:
  - OrderSend
  - OrderClose
  - OrderSelect
  - OrderType
  - OrderLots
  - OrderProfit
  - OrderMagicNumber
  - OrderSymbol
  - OrdersTotal
  - and more...

- Supports both market and pending orders
- Wrapper over MQL5's trade API (CTrade and COrderInfo)
- Useful for migrating older MT4 codebases to MQL5
- Entirely self-contained, no dependencies

------------------------------------------------------------
Example Usage

```cpp
#include <MT4Orders.mqh>

int ticket = OrderSend(Symbol(), OP_BUY, 0.1, Ask, 3, 0, 0, "Test Buy", 12345, 0, clrBlue);
if (ticket >= 0)
{
    if (OrderSelect(ticket, SELECT_BY_TICKET))
    {
        double price = OrderOpenPrice();
        double lots = OrderLots();
        Print("Buy order opened at ", price, " with ", lots, " lots.");
    }
}
```

Version: 1.02
Author: Andrey Kozlov (Integer)
Original source: https://www.mql5.com/en/code/16006
License: Free / Open Use