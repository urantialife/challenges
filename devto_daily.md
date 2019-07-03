# DEV.TO Daily Challenges

# Day 5

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