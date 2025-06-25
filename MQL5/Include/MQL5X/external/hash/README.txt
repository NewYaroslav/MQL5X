Hash.mqh — Dynamic Hash Table Implementation in MQL5
----------------------------------------------------

This library implements a dynamic hash table for MQL5 using linked-list buckets, 
prime-sized arrays, and optional value ownership (automatic memory management).

It allows you to store arbitrary user-defined objects and supports custom wrapper 
classes for primitive types (string, int, double, datetime, etc.).

Author: Andrew Lord (lordy)
Original Source: https://www.mql5.com/en/code/16123
Version: 1.0 (based on file header: $Id: hash.mqh 125 2014-03-03)

------------------------------------------------------------
Features

- Implements a classical hashtable structure with separate chaining
- Automatically resizes (rehashes) as the number of elements increases
- Optional `adoptValues` mode for automatic memory cleanup
- Provides wrapper classes: `HashInt`, `HashDouble`, `HashString`, `HashDatetime`, etc.
- Supports iteration via the `HashLoop` class
- Collision resolution via linked lists
- Prime-size table for better distribution
- FNV-1a hash algorithm (32 and 64-bit versions)

------------------------------------------------------------
🛠 Example Usage

```mq5
class MyVal : public HashValue {
public:
   int v;
   MyVal(int x) { v = x; }
};

void OnStart()
{
    Hash *h = new Hash(193, true); // true = auto-delete stored values
    h.hPut("a", new MyVal(42));
    h.hPutInt("b", 123);

    Print("a => ", ((MyVal*)h.hGet("a")).v);  // 42
    Print("b => ", h.hGetInt("b"));           // 123

    HashLoop *loop = new HashLoop(h);
    for (; loop.hasNext(); loop.next())
        Print(loop.key(), " => ", loop.valInt());
    delete loop;
    delete h;
}
```

Notes
- All values stored must inherit from HashValue
- Memory ownership is managed via adoptValues flag in constructor
- Null values are supported, but you should check getErrCode() to distinguish "not found" from "null stored"
- No dependencies, single-header implementation

License: Public use (unlicensed), attributed to author