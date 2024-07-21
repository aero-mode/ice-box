[[python]] [[библиотеки]]

```python
>>> from guppy import hpy; h=hpy()
>>> h.heap()
Partition of a set of 30976 objects. Total size = 3544220 bytes.
 Index  Count   %     Size   % Cumulative  % Kind (class / dict of class)
     0   8292  27   739022  21    739022  21 str
     1   7834  25   625624  18   1364646  39 tuple
     2   2079   7   300624   8   1665270  47 types.CodeType
     3    400   1   297088   8   1962358  55 type
     4   4168  13   279278   8   2241636  63 bytes
     5   1869   6   269136   8   2510772  71 function
     6    400   1   228464   6   2739236  77 dict of type
     7     79   0   139704   4   2878940  81 dict of module
     8   1061   3    93368   3   2972308  84 types.WrapperDescriptorType
     9    172   1    81712   2   3054020  86 dict (no owner)
<89 more rows. Type e.g. '_.more' to view.>
>>> h.heap().byid[0].sp
 0: h.Root.i0_modules['os'].__dict__
>>> h.iso(1,[],{})
Partition of a set of 3 objects. Total size = 348 bytes.
 Index  Count   %     Size   % Cumulative  % Kind (class / dict of class)
     0      1  33      248  71       248  71 dict (no owner)
     1      1  33       72  21       320  92 list
     2      1  33       28   8       348 100 int
>>>
```
