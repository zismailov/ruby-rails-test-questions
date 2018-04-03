# Ruby/Rails Test Questions

Hi guys, I tried to collect the most frequent and popular questions in an interview about Ruby/Rails.

I tried to answer the most frequent questions in interviews, it does not mean that you just need to learn them and everything, for understanding and fixing, you have to work them out in practice. Self-study is the best way.

# Ruby

- **Demonstrate two ways to create an empty hash**
  ```ruby
  {}
  ```
  ```ruby
  Hash.new
  ```
  >Hash is a collection of unique keys and their values, key => value. Also called associative arrays, they are similar to Arrays, but where an Array uses integers as its index, a Hash allows you to use any object type.

  <br/><br/>

- **Build a hash with two symbols as keys that each have different strings as values**
  ```ruby
  newhash = { :one => "foo", two: "bar"}
  ```
  <br/><br/>

- **Demonstrate how to pass a key into a hash**
  ```ruby
  newhash[:one]  ...you build a hash with {} you call with []
  ```
  <br/><br/>

- **What is returned if you pass a key that doesn't exist into a hash?**
  ```ruby
  nil
  ```
  <br/><br/>

- **Demonstrate how to change the value assoc with a key in a hash**
  ```ruby
  newhash = { :one => "foo", two: "bar"}
  newhash[:one] = "fixed"

  newhash = {"one"=>1, "two"=>2}
  newhash["one"] = "text"
  ```
  >pay attention to the ':' sign, it says that :one is not a string, but something like an enum, like in the C language.

  <br/><br/>

- **How would you return all the keys in a hash?**
  ```ruby
  newhash.keys
  ```
  <br/><br/>

- **These keys that are returned... what is their class?**
  ```ruby
  Array   ...when you call the above you are returned an array
  ```
  <br/><br/>

- **How do you see if a key is in a hash?**
  ```ruby
  newhash.keys.include?("value")
  ```
  <br/><br/>

- **How do you return all the values from a hash?**
  ```ruby
  newhash.values
  ```
  <br/><br/>

- **How would you merge one hash into another hash?**
  ```ruby
  newhash.merge!({foo: 3, bar: 4})
  ```
  <br/><br/>

- **How would you add a key value pair to an existing hash?**
  ```ruby
  newhash[:key] = value

  or (worse)

  newhash.merge!({:foo => 7})
  ```
  <br/><br/>

- **Are these both strings "one" ... 'one'**
  ```
  yes
  ```
  <br/><br/>

- **Make a string with quotes inside the string... in a couple ways**
  ```ruby
  "He said 'hi' to me' ... the escapes the"
  'He said "hi" to me'
  %(this is "Quote" here!)
  ```
  <br/><br/>

- **Why would you use double or single quotes?**
  >A single-quoted strings don’t process ASCII escape codes, and they don’t do string interpolation while double-quoted does both.

  ```ruby
  #Escape code example:
  puts 'Hello\nWorld'
  Hello\nWorld

  puts "Hello\nWorld"
  Hello
  World
  ```
  ```ruby
  #Interpolation example:
  age=27

  puts 'Age: #{age}'
  Age: #{age}

  puts "Age: #{age}"
  Age: 27
  ```
  <br/><br/>

- **What are some common escape characters and how do you escape them?**
  ```ruby
  \n - new line
  \\ - backslash
  ...
  ```
  <br/><br/>

- **How do you use flexible quotes to not have to worry about the above? i.e. this is a great way to create a string**
  >There are times we need to be able to define a wrapping character that is NOT in the string, and using % allows us to do that. This is a powerful, and very usable, way of avoiding "[leaning toothpick syndrome](https://en.wikipedia.org/wiki/Leaning_toothpick_syndrome)".

    ```ruby
      %(this is the string)
    ```
    >the "%" is what creates the string after % can be () !! {}

  <br/><br/>

- **Flexible quotes with the delimiter can be used to handle newlines**
  ```
  newstring = %{It was the best of times
                it was the worst of times
               }
  ```
  >this is equal to "it was the best of times\nit was the worst of times\n"

  <br/><br/>

- **What is a here document? describe and create one in ruby**
  ```ruby
  <<text
    some text
    some text
  text
  ```
  ```ruby
  def long_message
    puts(<<-EOT)
      Here goes a very long message...
      Sincerely,
      Dr. Foo
    EOT
  end
  ```
  ```ruby
  #You can also omit the dash and just write <<EOT – if you do this, your terminating sequence
  #must be at the very beginning of the line. It's less pretty:
  def foo
    puts(<<-EOT)
      Here goes my content.
    EOT
    # vs:
    puts(<<EOT)
      Here goes my content.
  EOT
  end
  ```
  <br/><br/>

- **What operator will concatenate two strings? Does it leave the strings in place?**
  ```
  +
  ```
  >yes it will leave the original strings in place

  <br/><br/>

- **Demonstrate how to concatenate to the end of a string**
  ```ruby
    my_str = "Marco "
    my_str += "Polo"

    #but there is a better way to do it : the << method.

    my_str = "Marco "
    my_str << "Polo"
  ```
  <br/><br/>

- **What is the shovel(<<) operator and what does it do for strings?**
  ```ruby
  my_str = "Marco "
  my_str << "Polo"
  => "Marco Polo"
  ```
  <br/><br/>

- **What is the difference between += and << ?**
  ```ruby
    a = 'foo'
    a.object_id #=> 2154889340
    a << 'bar'
    a.object_id #=> 2154889340
    a += 'quux'
    a.object_id #=> 2154742560

    my_str = "Marco "
    my_str << "Polo"
  ```
  >So << alters the original string rather than creating a new one. The reason for this is that in ruby a += b is syntactic shorthand for a = a + b (the same goes for the other <op>= operators) which is an assignment. On the other hand << is an alias of concat() which alters the receiver in-place.

  ```ruby
  #!/usr/bin/env ruby

  require 'benchmark'

  Benchmark.bmbm do |x|
    x.report('+= :') do
      s = ""
      10000.times { s += "something " }
    end
    x.report('<< :') do
      s = ""
      10000.times { s << "something " }
    end
  end
  ```
  <br/><br/>

- **What is the output? "\n".size What is "\t"?**
  ```ruby
  "\n".size
  => 1
  ```
  ```
  \t - is a symbol for tab
  ```
  <br/><br/>


- **Can you escape characters in a ' ' single quote?**
  ```ruby
  "Yaho o".gsub(" ", "\\\'")
  "Yaho'o".gsub("'", "\\\'")
  ```
  <br/><br/>

- **How do you interpolate into a string?**
  >Use double quotes and #{ }

  ```ruby
  "Text #{var}"
  ```
  <br/><br/>

- **Show two ways to get the 4th - 6th letters out of "One is less than two"**
  ```ruby
  text = "One is less than two"
  text[3,3]
  text[3..5]
  ```
  <br/><br/>

- **How would you split this string? "One two three" what do you get back when split?**
  ```ruby
  text = "One two three"
  text.split
  => ["One", "two", "three"] #it returns an array split with no args will split on blank spaces
  ```
  <br/><br/>

- **Show how you would split with a reg expression**
  ```ruby
  text = "One two three"
  text.split(/:/) #the : is the matching reg expression
  => ["One two three"]
  ```
  <br/><br/>

- **Use split and join on strings/array. Is join valid on strings? What does join do to an array? what does it do to a string?**
  ```ruby
  text = "One two three"
  text2 = text.split(/:/)
  => ["One two three"]

  text2.join(" ")
  => "One two three"
  ```
  >text2.join(" ") - that will build a string with `" "` between each element, it will call `to_s` on each element and create a string with whatever you pass into `join` inserted between each element, returns a string.

  <br/><br/>

- **a = "one" b = "one", does a == b?, does a.object_id == b.object_id? What does == usually evaluated for**
  ```ruby
  a = "one"
  b = "one"
  a == b
  => true

  a.object_id == b.object_id
  => false
  ```
  >a == b but they are different objects, `==` defined for strings this way in the class definition obviously

  <br/><br/>

- **Is nil an object?**
  >Yes `nil` is an object

  <br/><br/>

- **nil.nil? returns?**
  >`true`

 <br/><br/>

- **nil.to_s returns?**
  >`=> ""`

  <br/><br/>

- **nil.inspect returns?**
  > `=> "nil"`

  <br/><br/>

- **describe the is_a? method**
  >`kind_of?` and `is_a?` are synonymous.

  >`instance_of?` is different from the other two in that it only returns true if the object is an instance of that exact class, not a subclass.

  >`is_a?` will verify class of the object. e.g. `:text.is_a?(Symbol)` returns true, it checks the superclasses too and modules,a mixed in module will make `is_a?` evaluate to true

  >Example: `"hello".is_a? Object` and `"hello".kind_of? Object` return true because "hello" is a `String` and `String` is a subclass of `Object`. However `"hello".instance_of? Object` returns false.

  <br/><br/>

- **one = :symbol1 and two = :symbol1, are one and two the same object?**
  >Yes. both one and two have the same object_id

  ```ruby
  one = :symbol1.object_id
  => 1166748

  two = :symbol1.object_id
  => 1166748
  ```
  <br/><br/>

- **Discuss method names and their relationship to symbols**
  >all method names will become symbols.

  ```ruby
  #That's the way [Method#name](http://www.ruby-doc.org/core-2.0/Method.html#method-i-name) works, it returns the name of the method as a symbol:
  m = "foo".method(:size)  #=> #<Method: String#size>
  m.name                   #=> :size
  m.call                   #=> 3
  ```
  <br/><br/>

- **Discuss Constants and their relationship to symbols**
  >All Constants will become symbols `RubyConstant = "Hello there"`

  <br/><br/>

- is :symb == :"symb"? or :name == :"name"
  >yes, Ruby turns the quote into a symbol

  ```ruby
  :name == :"name"
  => true

  :name
  => :name
  :"name"
  => :name
  ```
  <br/><br/>

- **Ruby Symbols can never be garbage collected?**
  >If you are using Ruby 2.2.0 or later, it should usually be OK to dynamically create a lot of symbols, because they will be garbage collected according to the Ruby 2.2.0, which has a link to more details about the new symbol GC.

  <br/><br/>

- **How can you make a string into a symbol?**
  >`"String".to_sym`

  <br/><br/>

- **Build a symbol that has spaces in it.**
  >`x = :"this has spaces"`

  <br/><br/>

- **Build a symbol with interpolation**
  >`x = :"This has #{interpolation} in it"`

  <br/><br/>

- **What happens when you pass in a symbol to interpolated string?**
  >The symbol is converted to a string

  <br/><br/>

- **What is the class of a Regular Expression?**
  >`Regexp`

  <br/><br/>

- **Show two ways how you can match a string against a reg expression**
  ```ruby
  "this is string"[/is/] #or if a variable x[/is/]
  ```
  ```ruby
  x =~ /aaba/  # [/ /] - this returns a string NOT MATCHDATA, to get matchdata use .match
  ```
  <br/><br/>

- **What is returned when you get a match? no match?**
  >The matching string is returned, no match nil is returned
  >The position(integer) of the match is returned

  <br/><br/>

- **What do the following do in Regexp?**
  >`?` letter before it is optional `/ab?/` will return `ab` or `a`, `b` is fine but optional

  >`+` must match a least one, then unlimited `/ab+/` matches `ab` or `abbb`, but not `a`, must be `a b`

  >`*` matches zero or more. `/ab*/` matches `a`, `ab`, `abbbb`, `/b*/` matches `b`, `bbb` and `""` (the match must be at beginning, is this an "anchor typish"? thingy in the Regexp you are doing?)

  >`|` or

  >`[]` this will match any character in there. `/[cbr]at`/ matches `cat`, `bat`, `rat`, not `zat` . the `[]` is within a `[]` that starts the regexp, this is a character class

  >`\d` (say "backslash d") will match any digit

  >`\s` (say "backslash s") will match any whitespace

  >`\w` (say "backslash w") is a word character defined by `[/[a-zA-Z0-9_]+/]` ( use `\w+` to get words, just `w` is JUST a word character)

  >`.` any character at all except a `\n` newline

  >`\A` (backslash capital A) matches beginning of a string

  >`\Z` (backslash capital Z) vs `\z`, matches end of a string but wont include newline, `\z` includes the newline

  >`^` matches the start of a line (anchor) e.g. `/^\d/` finds a number if it starts a line good for matching after `\n`, note this and the one below also match when the start of a string (or end as below) a newline does not need to be embedded

  >`$` matches the end of a line (anchor) e.g. `/\d$/` finds a number if it ends a line good for matching after `\n`

  <br/><br/>

- **What is greedy matching?**
  >The Regexp will match as much as it can, repetition operators are greedy

  <br/><br/>

- **If more than one match what gets returned?**
  >The first match encountered will be returned

  <br/><br/>

- **What is this called /? ... what is this called \?**
  >That is a `/` slash, forward slash and a `\` backslash

  <br/><br/>

- **Demonstrate a range match in Regexp**
  ```ruby
  "this is a number 46"[/[0-9]+/]
  ```
  >[0-9] is a range in Regexp

  <br/><br/>

- **Give an example of negating a character class**
  ```ruby
    "new match22 78"[/[^0-9]+/]
  ```
  <br/><br/>

- **How do you get the negative of the character classes?**
  >Capitalize it .. e.g. `\W`

  <br/><br/>

- **How would you return a group of results in an array?**
  >([a-f].+) as an example this will return all the matches

  <br/><br/>

- **How can you take a string and return an array with all the words in it?**
  ```ruby
  "one two-three".scan(/\w+/)
  ```
  >`scan` will take a regualr expression as an parameter and return an array with all matches

  <br/><br/>

- **What does sub method do on a string?**
  ```ruby
  str.sub(pattern, replacement) #-> new_str
  "hello".sub(/[etdsr]/, '@') #-> "h@llo"
  ```
  >Find and replace, pass in two parameters find, replace_with

  <br/><br/>

- **gsub?**
  ```ruby
  "hello".gsub(/[aeiou]/, '@') #-> "h@ll@"
  ```
  >find and replace all pass in two parameters find, replace_with g-(global)sub

  <br/><br/>

- **Talk about global methods**
  >Global methods exist in the program outside of a class definition. `()` are optional for params list
  sometimes lack of parenthesis leads to ambiguity. Having wrong number of
  arguments is not a syntax error. It is a runtime error
  global methods e.g. puts are defined on `Kernal`.
  `Kernal` is mixed into all objects and kernal

<br/><br/>

- **What kind of Runtime Error is called when you call a method with wrong number of arguments?**
  >`ArgumentError`

  <br/><br/>

- **Demonstrate how to define a method with default argument values**
  ```RUBY
  def method(a, b = "default")
  ```
  <br/><br/>

- **Demonstrate how to define a method that takes a variable amount of arguments**
  ```ruby
  def method(*args)
  ```
  >if the `*` sponge operator is in the middle values are assigned left to right then right to left, the `*` sponges up the others

  <br/><br/>

- **If nothing is passed into a method with a variable arg, what is the value of that arg in the method?**
  >`[]`

  <br/><br/>

- **How to you specify a return value in a method? what if you do not specify a return value?**
  >`return :returnvalue`, if you do not specify the last statement executed is returned, once a return is encountered the method passes back control

  <br/><br/>

- **Show two ways to call a method defined in the same class as the method you are in now.**
  ```ruby
  x = method_defined_in_class(3,4)
  x = self.method_defined_in_class(3,4)
  ```
  >the `self` is implied

  <br/><br/>

- **Define a private method in a class**
  ```ruby
  private :private_method

  def private_method(a,b)
    a+b
  end
  ```
  <br/><br/>

- **Talk about if you can call a private method from within another method of that class. How can you not call it?**
  >You can call the private method within the class, but it will not work if you use `self.private_method`
  You will get a NoMethodError

  <br/><br/>

- **How do you declare a top level constant? How can you reference it?**
  >STORE_ADDRESS = "The moon" you can reference it with STORE_ADDRESS or ::STORE_ADDRESS

  <br/><br/>

- **What about declaring constants in a class and referencing them?**
  >Declare it the same way. You can reference it with ClassName::STORE_ADDRESS or even ::ClassName::STORE_ADDRESS

  <br/><br/>

- **Do Nested classes inherit constant values?**
  >yes

  <br/><br/>

- **Do subclasses inherit constants from parent classes?**
  >yes

  <br/><br/>

- **If in nested class and constant declared in both the parent class and in the inherited class which would win?**
  >If you have a nested class that inherits from another class and is also nested in a class the lexical scope would win (nested would take from parent (outside the nest), not from the < inherited)
  the definition of the variable would be searched first locally then searched through the inheritance hierarchy

  <br/><br/>

- **Describe static(lexical) scoping and dynamic scoping.**
  >These examples show how ruby does lexical static scoping. static scoping variables are bound locally... dynamically scoped variables will pop on and off the stack based on environment
  Ruby searches for Constants in this order

  >1 The enclosing scope

  >2 Any outer scopes (repeat until top level is reached)

  >3 Included modules

  >4 Superclass(es)

  >5 Object

  >6 Kernel

  <br/><br/>

- **What kind of statements return a value in Ruby?**
  >Every statement will return a value in Ruby

  <br/><br/>

- **Write an if then else in Ruby**
  ```ruby
  if condition == true
    :returnval
  else
    :otherval
  end
  ```
  <br/><br/>

- **Write an if then else in ruby that assigns a value to a variable. What if the result of a if then statement does not assign a value? What is returned?**
  ```ruby
  value = if condition == 1
            :returnvalue
          elsif condition == 2
            :othervalue
          else
            :finalthing
          end
  ```
  >You can say this, assign a value because, every statement in Ruby returns a value
  If you do this and nothing matches, nil is returned.

  <br/><br/>

- **Assign a value with a condition operator**
  ```ruby
    value = (x == 4 ? "true_value" : "false_value")
   ```
   <br/><br/>

- **Assign a value with a statement modifier**
  ```ruby
  value = 5 if x == 7
  ```
  <br/><br/>


- **Write an unless statement**
  ```ruby
  unless x == 5
    puts "here"
  end
  ```
  <br/><br/>

- **Write a while statement**
  ```ruby
  i = 0
  while i < 5
     puts i
     # Increment.
     i += 1
  end
  ```
  <br/><br/>

- **Write a break statement in a loop, does it stop the whole loop?**
  ```ruby
  i = 0
  while i < 5
    puts i
    i += 1
    break if i == 2
  end
  ```
  <br/><br/>

- **Write a next statement**
  ```ruby
  i = 0
  loop do
    i += 2
    if i == 4
      next  # skip rest of the code in this iteration
    end
    puts i
    if i == 10
      break
    end
  end
  ```
  <br/><br/>

- **Write a for statement**
  ```ruby
  for i in 0..5
    puts "Value of local variable is #{i}"
  end
  ```
  <br/><br/>

- **What are the things that evaluate to false when put into a conditional statement?**
  ```ruby
  false
  ```
  ```ruby
  nil
  ```
  >`0` does not evaluate to false

  <br/><br/>

- **What does the Class method ancestors do when called?**
  >returns an array of all the classes and modules that a given class inherits from

  <br/><br/>

- **Talk about the exception class tree.**
  >`Object` is at top. Exception inherits from `Object`, then `StandardError`, `RuntimeError`

  <br/><br/>

- **Write a rescue clause. Does a rescue have to be in a begin / end clause?**
  ```ruby
  begin
  # something which might raise an exception
  rescue StandardError => ex
  # code that deals with some exception
  rescue SomeOtherException => some_other_variable
  # code that deals with some other exception
  else
  # code that runs only if *no* exception was raised
  ensure
  # ensure that this code always runs, no matter what
  # does not change the final value of the block
  end
  ```
  <br/><br/>

- **What does method fail?**
  >same as `raise`. I guess it causes an `RuntimeError` to be raised always or if in a rescue clause will raise the same exception

  <br/><br/>

- **If an error is a RuntimeError is it also a StandardError?**
  >Yes `StandardError` is higher up the inheritance hierarchy so if it is a `RuntimeError` of course it is also a StandardError

  <br/><br/>

- **What is a synonym for fail?**
  >In Ruby, `fail` is synonymous with `raise`

  >Use `fail` instead of `raise` to signal exceptions

  >Use `raise` instead of `fail` to rethrow exceptions.'

  ```ruby
  # example
  def sample
    fail 'something wrong' unless success?
  rescue => e
    logger.error e
    raise
  end
  ```
  <br/><br/>

- **How could you define and raise your own exception you defined?**
  ```ruby
  #Well you could have class
  class MyError < StandardError
    def initialize(msg="My default message")
      super
    end
  end

  #Then you could
  raise MyError, "My message"
  ```
  <br/><br/>

- **What does map do on an array? what is a synonym for it?**
  >`map` transforms each element of the array according to what is returned by block. Synonym is `collect`
  or better said, `map` transforms a list by applying a function to each of its elements. map! does this in place

  <br/><br/>

- **98. What can you do to find all the matching elements in an array, how do you implement?**
  >When you call a`rray.select { |item| (item % 2) == 0 }`, will iterate over the array, passing into the block each item, it will return the items that match the condition in there

  ```ruby
  arr = [ 4, 8, 15, 16, 23, 42 ]
  result = arr.select { |element| element > 20 }
  puts result   # prints out [23, 42]
  ```
  <br/><br/>

- **What is another name for this above method?**
  >find_all

  <br/><br/>

- **What method will get the first match in an array?**
  >`find` will find the first element that matches a criteria an `array.find { |item| item.size > 4 }`

  <br/><br/>

- **What does inject do? What "traditionally returns an array and what traditionally just returns a number?"**
  >`Inject` takes an initial value as an argument and passes that into the first param of block, second param in block is the collection being passed in to be iterated over
  This is basically an accumulator `enum.inject(initial) {| memo, obj | block } => obj`
  The 'memo' is first set by 'initial' from then on out the memo is whatever is returned by the block. this will iterate over each item that is part of the enum, you can use the memo as part of calculations as you go through the list of stuff, you can only call inject on an enum object like an array or a range.
  `map` and `collect` will change each value in the array and return an array, inject just returns last thing evaluated.. unless of course you are returning an array or something on purpose

  <br/><br/>

- **Is a range a collection that can be used with methods like map?**
  >Sure you can do this `x = (1..3).map { [item] item + 1}` this will add 1 to each element of the array, return that array

  <br/><br/>

- **What does this do? File.open("example_file.txt") do |file|**
  >That will open a file and pass each line of the file into a block

  <br/><br/>

- **Demonstrate how to pass a block into a method, describe what is going on**
  ```ruby
  class Array
    def each 
      index = 0 
      while index < self.length # "self" means the current object in this case the current array.
        yield self[index] # the current element is passed to the block
        index += 1  # then the next item is moved
      end
    end
  end

  ["a", "b", "c"].each { |param| puts param }
  ```
  <br/><br/>

- **Can you call yield multiple times on a block?**
  >Yes, you can call yield tons and it will keep executing the block you have passed in

  <br/><br/>

- **How can you check if a method was called with a block?**
  >if block_given?

  <br/><br/>

- **Show how you can assign a block to a variable, can you pass in two lambdas to a method and never use a &?**
  ```ruby
  code_block = lambda do |argument|
    x = 4
    puts argument
  end

  code_block.call("called")
  ```
  >yes, you do NOT need & just define 2 lambdas and then pass them in, the & is to designate the yield

  <br/><br/>

- **Show another way to call a code block other than, add_one.call(10)**
  >another way to write e.g. `code_block_name.call(10)` is `code_block_name[10]`

  <br/><br/>

- **How would you pass in a code block (lambda) to a method expecting a code block?**
  <br/><br/>

- **How would you define a method that explicitly takes a code block? what if your explicitly define a code block and don't pass in a block?**
  ```ruby
  def method_with_block(&block)
    block.call(10)
  end
  ```
  >you do not have to pass in a block just because it explicitly takes one

  <br/><br/>
