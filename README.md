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
- Assume components CAN be reused
- Assume there CAN be duplicated components

One possible solution (Golang):
```
package main

import (
 	"fmt"
)

func main() {
	input := []string{"f", "o", "bar"}
	target := "foobar"
  	fmt.Println(MakeTarget(target, input))
}

func MakeTarget(target string, input []string) [][]string {
	var output [][]string

	// hashmap arranging components by starting letter
	hash := make(map[string][]string)
	for _, str := range input {
		firstLetter := string(str[0])
		hash[firstLetter] = append(hash[firstLetter], str)
	}

	makeTarget(target, hash, []string{}, &output)

	return output
}

func makeTarget(target string, hash map[string][]string, group []string, output *[][]string) {
	// find all potential starting strings
	var starters []string
	firstLetter := string(target[0])
	candidates := hash[firstLetter]
	for _, candidate := range candidates {
		if startsWith(target, candidate) {
			starters = append(starters, candidate)
		}
	}

	// for each starter, recursively call function for each new target
	for _, starter := range starters {
		// make a copy of existing group
		newGroup := make([]string, len(group)+1)
		copy(newGroup, group)
		newGroup = append(newGroup, starter)

		// push to ouput if this is the last component
		if len(target) == len(starter) {
			*output = append(*output, newGroup)
			continue
		}

		newTarget := target[len(starter):]
		makeTarget(newTarget, hash, newGroup, output)
	}
}

func startsWith(word, substr string) bool {
  if len(substr) > len(word) {
    return false
  }

  for i := range substr {
    if substr[i] != word[i] {
      return false
    }
  }

  return true
}
```
