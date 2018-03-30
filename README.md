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
  >There are times we need to be able to define a wrapping character that is NOT in the string, and using % allows us to do that. This is a powerful, and very usable, way of avoiding "l[leaning toothpick syndrome](https://en.wikipedia.org/wiki/Leaning_toothpick_syndrome)".

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
