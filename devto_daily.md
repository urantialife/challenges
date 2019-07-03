# Dev.to Daily Challenges

My solutions to [Dev.to's Daily challenge series](https://dev.to/thepracticaldev/daily-challenge-1-string-peeler-4nep)

## Daily Challenge #1 - String Peeler

[Challenge link](https://dev.to/thepracticaldev/daily-challenge-1-string-peeler-4nep)

This is just `string.slice(1, -1)`, just check if it's > length 2 and you're good to go!

```js

// Using if:
function peel(string){
    // Strings with length <= 2 are invalid
    if(string.length <= 2) return null
    return string.slice(1, -1)
}

// Using ternary:
const peel = string => string.length > 2 ? string.slice(1, -1) : null

console.log(peel("Hi"))
// -> null
console.log(peel("Hello there"))
// -> ello ther
```

## Day 2

## Day 3

## Day 4

## Day 5

[Challenge link](https://dev.to/thepracticaldev/daily-challenge-5-ten-minute-walk-1188)

My first attempt at one of these coding challenge things!

I'm not great with maths, but I'm guessing that all walks must have an even length, otherwise you can't end up back at your starting location, you'd always be one away...

If that assumption is true, then I think this works:

Basically, for each "pair" of blocks you want to walk, either add ["n", "s"] or ["e", "w"] to an array, then flatten and shuffle! Because you're always adding both a movement and it's inverse, you'll always end up where you started!

Ruby's proc / block thing still confuses me a little so I'm not sure if this is the most elegant one-liner (excluding checking for even walk length), but ayy it works!

```ruby
def genWalk length
    raise "Walk length must be even!" if length % 2 != 0
    (length / 2).times.collect(&Proc.new {[%w(n s), %w(e w)].sample}).flatten.shuffle
end

genWalk 10
# -> ["n", "w", "n", "e", "w", "s", "e", "w", "e", "s"]
```