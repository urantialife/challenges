# Dev.to Daily Challenges

My solutions to [Dev.to's Daily challenge series](https://dev.to/thepracticaldev/daily-challenge-1-string-peeler-4nep)

## Daily Challenge #1 - String Peeler

[Challenge link](https://dev.to/thepracticaldev/daily-challenge-1-string-peeler-4nep)

This is just `string.slice(1, -1)`, just check if it's > length 2 and you're good to go!

Solution in javascript:

```js
// Using if:
function peel(string) {
	// Strings with length <= 2 are invalid
	if (string.length <= 2) return null
	return string.slice(1, -1)
}

// Using ternary:
const peel = string => (string.length > 2 ? string.slice(1, -1) : null)

console.log(peel("Hi"))
// -> null
console.log(peel("Hello there"))
// -> ello ther
```

## Daily Challenge #2 - String Diamond

[Challenge link](https://dev.to/thepracticaldev/daily-challenge-2-string-diamond-21n2)

TODO: Some time

## Daily Challenge #3 - Vowel Counter

[Challenge link](https://dev.to/thepracticaldev/daily-challenge-3-vowel-counter-34ni)

Okay, so this one looks like it could be done pretty easily with regex!

```js
const countVowels = str => (str.match(/[aeiou]/gi) || "").length

console.log(countVowels("Hello")) // -> 2
console.log(countVowels("HELLO! WORLD!")) // -> 3
console.log(countVowels(":( vwls? hmmm nty!")) // -> 0
```

## Daily Challenge #4 - Checkbook Balancing

TODO: Some time

## Daily Challenge #5 - Ten Minute Walk

[Challenge link](https://dev.to/thepracticaldev/daily-challenge-5-ten-minute-walk-1188)

My first attempt at one of these coding challenge things!

I'm not great with maths, but I'm guessing that all walks must have an even length, otherwise you can't end up back at your starting location, you'd always be one away...

If that assumption is true, then I think this works:

Basically, for each "pair" of blocks you want to walk, either add ["n", "s"] or ["e", "w"] to an array, then flatten and shuffle! Because you're always adding both a movement and it's inverse, you'll always end up where you started!

Ruby's proc / block thing still confuses me a little so I'm not sure if this is the most elegant one-liner (excluding checking for even walk length), but ayy it works!

Solution in ruby:

```ruby
def genWalk length
    raise "Walk length must be even!" if length % 2 != 0
    (length / 2).times.collect(&Proc.new {[%w(n s), %w(e w)].sample}).flatten.shuffle
end

genWalk 10
# -> ["n", "w", "n", "e", "w", "s", "e", "w", "e", "s"]
```

## Daily Challenge #6 - Grandma and her friends

[Challenge link](https://dev.to/thepracticaldev/daily-challenge-6-grandma-and-her-friends-23kd)

> NOTE: This challenge was a weird one, lots of peeps noted that there was incomplete data to solve the problem, but I did my best anyway! This solution is to the original way that the question was written, if it changes then this might not be right anymore :(

I'm making the following assumptions, but I think I have a solution:

- Town X1 is 1 mile from X0, X2 is 2 miles from X0, etc... (otherwise I don't believe there is enough information to come up with a solution)
- `friendTownList` uses format C (flattened list)
- the return trip from the last friend's house back to X0 is included in the total

Could be one (ugly) line if not counting error handling in the case where we don't know where a friend lives, could also be smaller if `friendTownList` was a hash to start with~

```ruby
def getDistance(visitOrder, friendTownList)
  townHash = Hash[*friendTownList]
  visitOrder.each {|f| raise "IDK where #{f} lives!" if !townHash.key? f }
  [0, *visitOrder.map(&proc {|f| townHash[f][1 .. -1].to_i }), 0]
    .each_cons(2)
    .map(&proc {|a, b| (a - b).abs })
    .sum
end

getDistance(%w(A2 A1 A3), %w(A1 X1 A2 X2 A3 X3))
# -> 8
# Because (0, 2[2], 1[1], 3[2], 0[3]) -> 2 + 1 + 2 + 3 = 8
```

## Daily Challenge #7 - Factorial Decomposition

[Challenge link](https://dev.to/thepracticaldev/daily-challenge-7-factorial-decomposition-176o)

I'm not great at abstract maths, but here's my solution using a standard library function in ruby:

```ruby
require 'prime'

def decomp n
  fact = Math.gamma(n + 1).to_i
  "n = #{n}; n! = #{fact}; decomp(n!) = #{n == 1 ? "1" : Prime.prime_division(fact).map(&proc {|pair| pair[1] > 1 ? "#{pair[0]}^#{pair[1]}" : pair[0]}).join(" * ")}"
end

(1..10).each {|x| puts decomp x}
```

Output:

```
n = 1; n! = 1; decomp(n!) = 1
n = 2; n! = 2; decomp(n!) = 2
n = 3; n! = 6; decomp(n!) = 2 * 3
n = 4; n! = 24; decomp(n!) = 2^3 * 3
n = 5; n! = 120; decomp(n!) = 2^3 * 3 * 5
n = 6; n! = 720; decomp(n!) = 2^4 * 3^2 * 5
n = 7; n! = 5040; decomp(n!) = 2^4 * 3^2 * 5 * 7
n = 8; n! = 40320; decomp(n!) = 2^7 * 3^2 * 5 * 7
n = 9; n! = 362880; decomp(n!) = 2^7 * 3^4 * 5 * 7
n = 10; n! = 3628800; decomp(n!) = 2^8 * 3^4 * 5^2 * 7
```