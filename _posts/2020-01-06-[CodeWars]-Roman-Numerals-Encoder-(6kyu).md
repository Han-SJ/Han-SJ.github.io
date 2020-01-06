---
layout: post
title:  "[CodeWars] Roman numberals encoder (6kyu)"
categories: CodeWars
---
## Details

Create a function taking a positive integer as its parameter and returning a string containing the Roman Numeral representation of that integer.
Modern Roman numerals are written by expressing each digit separately starting with the left most digit and skipping any digit with a value of zero. In Roman numerals 1990 is rendered: 1000=M, 900=CM, 90=XC; resulting in MCMXC. 2008 is written as 2000=MM, 8=VIII; or MMVIII. 1666 uses each Roman symbol in descending order: MDCLXVI.

## Example

```
Roman.encode(1000) // should return "M"
```

## Solutions

### My Solution

```scala
object Roman {
  val one = ("I", "V", "X")
  val ten = ("X", "L", "C")
  val oneHundred = ("C", "D", "M")
  val oneThousand = "M"
  
  def encode(arabic: Int): String = {
    var ret = ""
    
    List.fill(arabic / 1000)(oneThousand).mkString +
    translator(oneHundred, arabic%1000/100) +
    translator(ten, arabic%100/10) +
    translator(one, arabic%10)
  }
    
  def translator(tpl: (String, String, String), arabic: Int): String = {
    arabic match {
      case 4 => tpl._1 + tpl._2
      case 5 => tpl._2
      case 9 => tpl._1 + tpl._3
      case n if n < 4 => List.fill(arabic)(tpl._1).mkString
      case n => tpl._2 + List.fill(arabic-5)(tpl._1).mkString
    }
  }
}
```

### Other Solution

```scala
object Roman {

  def encode(arabic: Int): String =
    List(("M", 1000), ("CM", 900), ("D", 500), ("CD", 400), ("C", 100), ("XC", 90), ("L", 50), ("XL", 40), ("X", 10), ("IX", 9), ("V", 5), ("IV", 4), ("I", 1))
      .collectFirst { case (s, v) if v <= arabic => s"$s${encode(arabic-v)}" }
      .getOrElse("")
}
```
