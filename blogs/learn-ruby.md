# Ruby tutorials

## What is Ruby?
- Ruby is a pure object-oriented programming language. It was created in 1993 by Yukihiro Matsumoto of Japan.
- Ruby is an open-source and is freely available on the Web, but it is subject to a license.
- Ruby is a general-purpose, interpreted programming language.
- Ruby is a true object-oriented programming language.
- Ruby is a server-side scripting language similar to Python and PERL.
- Current version 2.6.7

Note: **Ruby is "A Programmer's Best Friend".**

## What is rbenv?
- Ruby version manager. Work with multiple ruby versions for differnet applications when needed.
- RVM was another tool which was used widely before
```
$ rbenv list
$ rbenv install 
$ rbenv versions # list of installed ruby versions
$ ruby -v # system ruby default version
```

## What is IRB?
- Interactive ruby shell

```
# to enter ruby shell if you have any default ruby installed in your machine
$ irb 
```

## Write "Hello Ruby!" in Ruby?
```
irb(main)> puts "Hello Ruby!" or p "Hello Ruby!"
```

##  Ruby operators?
Logical Operators:
- ```and```	Called Logical AND operator. If both the operands are true, then the condition becomes true.	(a and b) is true.
- ```or```	Called Logical OR Operator. If any of the two operands are non zero, then the condition becomes true.	(a or b) is true.
- ```&&```	Called Logical AND operator. If both the operands are non zero, then the condition becomes true.	(a && b) is true.
- ```||```	Called Logical OR Operator. If any of the two operands are non zero, then the condition becomes true.	(a || b) is true.
- ```!```	Called Logical NOT Operator. Use to reverses the logical state of its operand. If a condition is true, then Logical NOT operator will make false.	!(a && b) is false.
- ```not```	Called Logical NOT Operator. Use to reverses the logical state of its operand. If a condition is true, then Logical NOT operator will make false.	not(a && b) is false.

Ternary Operator: 
- ```? :```	Conditional Expression	If Condition is true ? Then value X : Otherwise value Y

Range Operators:
- ```..```	Creates a range from start point to end point inclusive.	1..10 Creates a range from 1 to 10 inclusive.
- ```...```	Creates a range from start point to end point exclusive.	1...10 Creates a range from 1 to 9.

Operators Precedence:
- ```::```	Constant resolution operator
- ```* / %```	Multiply, divide, and modulo
-	```+ -```	Addition and subtraction
-	```>> <<```	Right and left bitwise shift
-	```&```	Bitwise 'AND'
-	```^ |```	Bitwise exclusive `OR' and regular `OR'
-	```<= < > >=```	Comparison operators
- ```defined?```	Check if specified symbol defined
- ```not```	Logical negation
- ```or and```	Logical composition

## Ruby Loops?
```
3.times {
  print "hello"
}
```

```
for i in 0..5
   puts "Value of local variable is #{i}"
end
```

```
$i = 0
$num = 5

until $i > $num  do
   puts("Inside the loop i = #$i" )
   $i +=1;
end
```

```
['a', 'b', 'c'].each do |str|
  p str
end
```

## Ruby comments:
- Single line comment
```
# This is a single line comment.
puts "Hello, Ruby!"
```

- Multi line comment
```
=begin
This is a multiline comment and con spwan as many lines as you
like. But =begin and =end should come in the first line only. 
=end
```

## Ruby variables?
- Instance variables: begins with ```@```
- Class variables: begins with ```@@```  must be initialized before can be used.
- Local variables: begin with a ```lowercase``` letter or ```_.``` The scope of a local variable ranges from class, module, def, or do to the corresponding end or from a block's opening brace to its close brace {}.
- Constant variables: begin with an ```uppercase``` letter or all uppercase.
- Pseudo-Variables: 
1. ```self``` - The receiver object of the current method. 
2. ```true``` − Value representing true. 
3. ```false``` − Value representing false.
4. ```nil``` − Value representing undefined.
5. ```__FILE__``` − The name of the current source file.
6. ```__LINE__``` − The current line number in the source file.

## Ruby Methods?
```
def method_name
  # code
end
```

```
def method_with_param(first_name, last_name)
  return first_name + " " + last_name
end
```

## Ruby Arrays?
```
ary = [  "fred", 10, 3.14, "This is a string", "last element", ]

ary.each do |i|
   puts i
end
```

## Ruby Hashes?
```
hsh = colors = { "red" => 0xf00, "green" => 0x0f0, "blue" => 0x00f }
hsh.each do |key, value|
   print key, " is ", value, "\n"
end
```

## Ruby Ranges?
```
(10..15).each do |n| 
   print n, ' ' 
end
```

## Conditional statement?
- if
- else
- unless # if condition is false
- case
- when

```
x = 1

if x > 2
   puts "x is greater than 2"
elsif x <= 2 and x!=0
   puts "x is 1"
else
   puts "I can't guess the number"
end
```

## Ruby blocks?
- A block consists of chunks of code.
- You assign a name to a block.
- You invoke a block by using the yield statement.
- The code in the block is always enclosed within braces ({}).

```
def test
   puts "You are in the method"
   yield # invoke block here
   puts "You are again back to the method"
   yield # invoke block here
end

test { puts "You are in the block" }
```


## Ruby class?

Example - 1:
```
class A

end
```

Example - 2:
```
class Book

  VAR1 = 100
  VAR2 = 200

  @@no_of_books = 0

  def initialize(id, title, pages)
    @id = id
    @title = name
    @pages = pages
  end

  def display_details()
    puts "ID: #@id"
    puts "Title: #@title"
    puts "Pages #@pages"
  end

  def total_no_of_books()
    @@no_of_books += 1
    puts "Total number of books: #@@no_of_books"
   end
end

# Create Objects
book1 = Customer.new(1, "Harry Potter", 400)
book2 = Customer.new(2, "The Lord of the Rings", 550)

# Call Methods
book1.display_details()
book2.display_details()

book1.total_no_of_books()
book2.total_no_of_books()
```

## Ruby Inheritance?
```
class A

end

class B < A

end
```

## Ruby modules?
Modules are a way of grouping together methods, classes, and constants. Modules give you two major benefits.

- Modules provide a namespace and prevent name clashes.
- Modules implement the mixin facility.

**Example - 1:**
```
module Week

  FIRST_DAY = "Sunday"

  def Week.weeks_in_month
    puts "You have four weeks in a month"
    return ""
  end

  def Week.weeks_in_year
    puts "You have 52 weeks in a year"
  end
end

Week::FIRST_DAY
Week.weeks_in_month
Week.weeks_in_year
```

**Example - 2:**
```
module Year

  def Year.current_year()
    puts "2019"
  end

  module Month

    def Month.current_year_month
      puts "December, 2019"
    end

    module Week 

      def Week.current_year_month_week
        puts "2nd week, December, 2019"
      end
    end

  end

end

Year.current_year()
Year::Month.current_year_month()
Year::Month::Week.current_year_month_week()
```

**Example - 3:** 
```
module M
  
  class A
    def self.sum()
      1 + 5
    end
  end

  class B
    def self.subtraction
      5 - 1
    end
  end

end

M::A.sum
M::B.subtraction
```

## Playing with IRB console?
```
1 + 1
3 - 1
Math.sqrt(4)
```

```
str = "Hello Ruby"

str.capitalize
str.upcase
str.class
str.is_a?(String)
str.is_a?(Integer)
```

```
arr = Array.new
arr[0] = 1
arr[1] = 2
```

```
hash = Hash.new
hash[:one] = "One"
hash[:two] = "Two"
```

```
[1, 2, 3, 4, 5].map { |e| e * 2 }
[1, 2, 3, 2, 2].select { |e| e == 2 }
```

```
3.times {
  print "hello"
}

(1...5).each  do |i|
  p i
end
```

```
%i(The quick brown fox jumps over the lazy dog)
%w(The quick brown fox jumps over the lazy dog)
```

```
class A

  def sum(a, b)
    p a + b # Last statement is automatically return
    # return 10
  end
end

a = A.new
a.methods
a.sum(10, 20)
```
