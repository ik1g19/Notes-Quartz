# Implicit Returns

The last line to be evaluated in a method is implicitly returned

```ruby
def card
	Card.new('Ace', 'Spades') # implicit return
end
```

# Lazy Evaluation

Uses lazy evaluation

# Let Blocks

![[notes/Ruby/RSpec#`let` blocks|RSpec]]


# Predicate Methods

It is a standard in Ruby that all predicate methods (Boolean returning) in Ruby end in a `?`

# Truthiness and Falsiness

Everything in Ruby can be evaluated to `true` or `false`

`nil` and `false` evaluate to `false`

everything else evaluates to `true`