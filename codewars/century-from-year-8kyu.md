# Details

The first century spans from the year 1 up to and including the year 100, The second - from the year 101 up to and including the year 200, etc.

## Examples

    centuryFromYear(1705)  returns (18)
    centuryFromYear(1900)  returns (19)
    centuryFromYear(1601)  returns (17)
    centuryFromYear(2000)  returns (20)

## Solutions

### My Solution

    object CenturyYear {
      def centuryFromYear(year: Int): Int = {
        if (year % 100 > 0) year / 100 + 1 else year / 100
      }
    }

### Other Solution

    object CenturyYear {
      def centuryFromYear(year: Int): Int = {
        (year-1)/100+1
      }
    }
