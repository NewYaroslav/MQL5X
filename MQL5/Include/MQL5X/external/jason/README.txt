Jason.mqh — Lightweight JSON Parser for MQL5
--------------------------------------------

This file implements a simple JSON parser written entirely in MQL5, with no external dependencies.
It allows you to parse JSON-formatted strings and access the data using a lightweight internal structure.

Features:
- Fully written in MQL5
- Does not use DLLs or external APIs
- Supports all basic JSON types: object, array, string, number, boolean, null
- Supports Unicode escape sequences like "\u041d" (Cyrillic, etc.)
- Compact, self-contained: only one file (jason.mqh)

Usage:
Include the file in your script or expert:

    #include <MQL5X/external/jason/jason.mqh>

Deserialize and access values:

    CJAVal js;
    if(js.Deserialize("{ \"key\": 123 }"))
        Print(js["key"].ToInt());

You can also serialize back:

    string out = "";
    js.Serialize(out);
    Print(out);

------------------------------------------------------------
🛠 Example
------------------------------------------------------------

    void OnStart()
    {
        CJAVal js;
        string in = "{\"a\":[{\"b\":1},{\"c\":2}]}";
        string out = "";

        if(js.Deserialize(in))
        {
            js.Serialize(out);
            Print(in + " -> " + out);
        }

        js.Clear();
        js["Test"] = 1.4;

        string output = "";
        js.Serialize(output);
        Print("Serialized: " + output);

        js["Array"][0] = 42;
        js["Array"][1] = 100;
        js["ArrayText"].Add("foo");
        js["ArrayText"].Add("bar");

        js.Serialize(output);
        Print("Array JSON: " + output);
    }

------------------------------------------------------------
📜 Version History
------------------------------------------------------------

- v1.00 — Initial version
- v1.04 — Fixed parsing issues with arrays and nested objects
- v1.06 — Improved Unicode support (e.g. \u041d)
- v1.08 — Improved recursive serialization and deserialization, cleaner structure

⚠ Note: as of v1.08, CJAVal supports nested array/object access, copy of tree elements, and deep serialization.

------------------------------------------------------------
👤 Author
------------------------------------------------------------

Roman Kornev  
Original source: https://www.mql5.com/en/code/13663  
License: Public domain / free use for any purpose.