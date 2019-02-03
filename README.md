# Goffee

Goffee is an intent to build open source programming language that makes it easy to build simple, reliable and efficient software.

Syntax is Coffeescript-inspired, but compiler uses Go toolchain and Go standard library, and is interoperable with Go code, like Coffeescript is interoperable with JS/ECMAScript.

## Features

* All Go features - obviously, as it uses Go toolchain (minus some of it's safety/redundancy features):
  * static typing
  * interfaces and duck-typing
  * goroutines and channels
  * fast compilation
  * etc, etc.

* Some of Coffeescript features:
  * concise and readable syntax.
  * `#`-based comments, making language shebang compatible.
  * indentation-based blocks and optional parenthesis in function calls:

    ```coffee
    f = (name)->
      fmt.Println "Hello,", name
    f "Goffee"
    ```

  * negative indices to address from the end of slice/array

    ```coffee
    s[-1] == s[len(s)-1] # last element
    s[-5..] == s[len(s)-5..] # last 5 elements, s[len(s)-5:]
    s[..-1] == s[...len(s)-1] # everything except last element, s[:len(s)-1]
    # pop operation becomes readable
    a, s = s[-1], s[...-1]
    ```

* Features unique to Goffee:
  * push/pop/shift operators for slices. This needs to be designed, keeping code short and intuitively readable.

    ```coffee
    slice := []int{10, 20, 30}

    slice <- 5 # append/push
    # same as
    slice = append(slice, 5)

    val := <-slice # shift first value
    # same as
    var val int
    val, slice = slice[0], slice[1..]

    # the rest needs to be designed carefully.
    ```

    See [example](examples/slices.goffee) for other operator candidates.
    
  * Built-in set structure, with iteration support.
  
    It can easily be emulated with `map[Obj]bool`, but it's handy to have `set` around and take less memory than corresponding `map`.
  
    ```go
    s := set[int]{5, 10, 20}
    for n := range s
      fmt.Println(n)
    if s[10]
      # ...
    s[15] = true # add value
    s[10] = false # remove value
    # or
    delete(s, 10)
    ```

  * adjustable syntax

    Just an example, actual implementation might be different:

    ```coffee
    #! switch to // comments
    //! switch to {} blocks
    f = -> {
      if true {
        // etc
      }
    }
    //! switch to # comments
    #! switch to indent blocks
    if true
      # do something
    #! make [] optional
    arr = [1,2,3]
    fmt.Println arr 0
    ```

    This might be opposite of what Go was trying to achieve, but read the next "feature":

  * Recommendation NOT to use Goffee, unless you have mastered Go. 😁

    Go puts a lot of restrictions on developer, teaching him/her to write readable, convention-conforming code. Permissive syntax of Goffee allows you to shoot yourself into both feet, both arms and head. So unless you have learned to follow self-discipline and write clean code without language restrictions, DO NOT use Goffee.     

## Examples

See [examples folder](examples/).

None of examples are final.
