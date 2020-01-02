# MB Engineering 50 Fizz Buzz Task
***JUnit 5*** will be used to ensure both the fizzBuzzGenerator and divisbleBy methods are functioning in accordance to the specification.

***Test Plan***

I intend to use the JUnit assertEquals function to test the results returned from the fizzBuzzGenerator method with a separate ArrayList holding the correct results.

The divisbleBy method will also be tested with JUnit assertEquals function, this will be done to ensure divisibleBy(4,2) returns true and divisibleBy(3,2) returns false.

These tests will be conducive as all JUnit tests will remain failed until the matching result is returned.
# Part 1 - fizzBuzzGenerator
**First Test - Failed**


***Test Code:***
```
import org.junit.jupiter.api.Test;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import static org.junit.jupiter.api.Assertions.*;
    class MainTest {
    
        @Test
        void main() {
            FizzBuzzGenerator fizzBuzzGenerator = new FizzBuzzGenerator();
            List<String> List1 = new ArrayList<String>();
            Collections.addAll(List1,"1", "2", "Fizz", "4", "Buzz", "Fizz", "7", "8", "Fizz", "Buzz", "11", "Fizz", "13", "14", "FizzBuzz");
            assertEquals(List1, fizzBuzzGenerator.FizzBuzz(1,16));
        }
    }*
```             
***Returned Result:***

```
Expected :[1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, FizzBuzz]
Actual   :[1, FizzBuzz, 3, 4, FizzBuzz, 6, FizzBuzz, FizzBuzz, 9, 10, FizzBuzz, FizzBuzz, 13, FizzBuzz, 15]
```
***Issues***
*  Position 2(1) in the list should equals to "2", not "FizzBuzz"
*  Position 15(14) in the list should equals "FizzBuzz" as it is a multiple of both 5 and 3
*  There are no positions equalling to either "Fizz" or "Buzz"

**First Alterations**
***Altered From:***
```
public boolean divisibleBy(int numerator, int Denominator) {
        int answer = 0;
        return numerator % Denominator == 2;
    }
```
***To:***
```
public boolean divisibleBy(int numerator, int Denominator) {
        int answer = 0;
        return numerator % Denominator == 0;
    }
```
***Justification***

The divisbleBy method was returning true when the numerator and denominator had a remainder of "2" as opposed to "0". This gave incorrect results.

**Second Test - Failed**
***Test Code:***
*  *Repeated*
                       
***Returned Result:***

```
Expected :[1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, FizzBuzz]
Actual   :[1, 2, FizzBuzz, 4, FizzBuzz, FizzBuzz, 7, 8, FizzBuzz, FizzBuzz, 11, FizzBuzz, 13, 14, FizzBuzz]
```
***Issues***
*  The issue of only returning "FizzBuzz and not "Fizz" or "Buzz"
*  Position 5 should be "Buzz"

**Second Alterations**
***Altered From:***
```
for (int i = startNumber; i <endNumber ; i++) {
            if(divisibleBy(i, 3) || divisibleBy(i, 5)) fizzBuzzList.add("FizzBuzz");
            else if (divisibleBy(i, 3)) fizzBuzzList.add("Fizz");
            else if (divisibleBy(i, 5)) fizzBuzzList.add("Buz");
            else fizzBuzzList.add(Integer.toString(i));
        }
        return fizzBuzzList;
```
***To:***
```
for (int i = startNumber; i <endNumber ; i++) {
            if(divisibleBy(i, 3) && divisibleBy(i, 5)) fizzBuzzList.add("FizzBuzz");
            else if (divisibleBy(i, 3)) fizzBuzzList.add("Fizz");
            else if (divisibleBy(i, 5)) fizzBuzzList.add("Buz");
            else fizzBuzzList.add(Integer.toString(i));
        }
        return fizzBuzzList;
```
***Justification***

Changing the || operator to an && will prevent the loop from ending as soon as there is a match, this prevented the possibility of reaching any of the else if statements.
##Third Test - Failed
***Test Code:***
*  *Repeated*
                       
***Returned Result:***

```
Expected :[1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, FizzBuzz]
Actual   :[1, 2, Fizz, 4, Buz, Fizz, 7, 8, Fizz, Buz, 11, Fizz, 13, 14, FizzBuzz]
```
***Issues***
*  A spelling mistake within the else if condition, "Buz" should be "Buzz"

**Final Alterations**
***Altered From:***
```
for (int i = startNumber; i <endNumber ; i++) {
            if(divisibleBy(i, 3) || divisibleBy(i, 5)) fizzBuzzList.add("FizzBuzz");
            else if (divisibleBy(i, 3)) fizzBuzzList.add("Fizz");
            else if (divisibleBy(i, 5)) fizzBuzzList.add("Buz");
            else fizzBuzzList.add(Integer.toString(i));
        }
        return fizzBuzzList;
```
***To:***
```
for (int i = startNumber; i <endNumber ; i++) {
            if(divisibleBy(i, 3) && divisibleBy(i, 5)) fizzBuzzList.add("FizzBuzz");
            else if (divisibleBy(i, 3)) fizzBuzzList.add("Fizz");
            else if (divisibleBy(i, 5)) fizzBuzzList.add("Buzz");
            else fizzBuzzList.add(Integer.toString(i));
        }
        return fizzBuzzList;
```
***Justification***

The alteration of the "Buz" parameter to "Buzz" should resolve the test not passing.
##Final Test - Passed
***Test Code:***
``` import org.junit.jupiter.api.Test;
    import java.util.ArrayList;
    import java.util.Collections;
    import java.util.List;
    import static org.junit.jupiter.api.Assertions.*;
    
    class MainTest {
    
        @Test
        void main() {
            FizzBuzzGenerator fizzBuzzGenerator = new FizzBuzzGenerator();
            List<String> List1 = new ArrayList<String>();
            Collections.addAll(List1,"1", "2", "Fizz", "4", "Buzz", "Fizz", "7", "8", "Fizz", "Buzz", "11", "Fizz", "13", "14", "FizzBuzz");
            assertEquals(List1, fizzBuzzGenerator.FizzBuzz(1,16));
    
            System.out.println(fizzBuzzGenerator.FizzBuzz(1,16).toString());
        }
    }
```

               
***Returned Result:***
```   
Passed
Returned   :[1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, FizzBuzz]
```

# Part 2 - divisbleBy
**First Test - Passed**
***Test Code:***
```
import org.junit.jupiter.api.Test;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import static org.junit.jupiter.api.Assertions.*;

class MainTest {

    @Test
    void main() {
        FizzBuzzGenerator fizzBuzzGenerator = new FizzBuzzGenerator();
        assertEquals(true, fizzBuzzGenerator.divisibleBy(4,2));
    }
}
```             
***Returned Result:***
```   
Test passed
Returned true
```

**Second Test - Passed**
***Test Code:***
```
import org.junit.jupiter.api.Test;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import static org.junit.jupiter.api.Assertions.*;

class MainTest {

    @Test
    void main() {
        FizzBuzzGenerator fizzBuzzGenerator = new FizzBuzzGenerator();
        assertEquals(false, fizzBuzzGenerator.divisibleBy(3,2));
    }
}
```             
***Returned Result:***
```   
Test passed
Returned false
```

**Final Test - As Intended**
As a final precaution, I must test if divisblyBy will return as failed against an incorrect test

***Test Code:***
```
import org.junit.jupiter.api.Test;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import static org.junit.jupiter.api.Assertions.*;

class MainTest {

    @Test
    void main() {
        FizzBuzzGenerator fizzBuzzGenerator = new FizzBuzzGenerator();
        assertEquals(true, fizzBuzzGenerator.divisibleBy(3,2));
    }
}
```
***Returned Result:***
```   
Test failed
Returned false
```

# Conclusion
Both methods have been tested effectively to ensure they were functioning in accordance to the specification.

JUnit 5 was a conducive testing framework due to it providing the ability to set conditions that had to be met and being able to test code without altering the Main class.
