# abracadabra-coding-problem
Growth &amp; Member Coding Challenge: Abracadabra

Given a target string and an array of component strings, generate all possible groups of component strings such that they can be concatenated into the target string.

```
target = "foobar"
input = ["f", "poo", "fa", "foo", "baz", "oo", "bar"], 
output = [["f", "oo", "bar"], ["foo", "bar"]]
```

Assume components cannot be reused.

Assume components are unique (no duplicates)

LONGER INPUT:

```
target: "abracadabra"
Input: ["cad", "bbr", "dab", "rac", "abrad", "bran", "brr", "cadd", "rad", "bra", "a", "abra", "ab", "aba", "dad", "ra"]
Output: [[ abra  cad  abra] [ abra  cad  a  bra] [ abra  cad  ab  ra] [ a  bra  cad  abra] [ a  bra  cad  a  bra] [ a  bra  cad  ab  ra] [ ab  rac  a  dab  ra] [ ab  ra  cad  abra] [ ab  ra  cad  a  bra] [ ab  ra  cad  ab  ra]]
```

Possibile modifications if there is additional time:
- Assume components CANNOT be reused
- Assume there CAN be duplicated components
