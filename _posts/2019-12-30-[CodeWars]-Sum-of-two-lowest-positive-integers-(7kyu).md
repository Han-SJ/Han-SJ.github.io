---
layout: post
title:  "[CodeWars]-Sum-of-two-lowest-positive-integers-(6kyu)"
categories: CodeWars
---

# Details

Create a function that returns the sum of the two lowest positive numbers given an array of minimum 4 positive integers. No floats or non-positive integers will be passed.

## Examples

```
`[19, 5, 42, 2, 77]`, the output should be `7`.

`[10, 343445353, 3453445, 3453545353453]` should return `3453455`.
```

## Solutions

### My solution

```scala
object LowIntSum {
  def sumTwoSmallest(numbers: List[Int]): Int = {
    val sortedNumbers = numbers.sorted
    sortedNumbers(0) + sortedNumbers(1)
  }
}
```

### Another's

```scala
object LowIntSum {
    def sumTwoSmallest(numbers: List[Int]): Int =
        numbers.sorted.take(2).sum
}
```
