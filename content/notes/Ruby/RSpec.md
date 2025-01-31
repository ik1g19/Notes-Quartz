Most popular Ruby gem

RSpec is a DSL (Domain Specific Language)

Consists of 3 independent Ruby Gems
- `rspec core` - organizes and runs the tests
- `rspec-expectations` - the matcher library for assertions
- `rspec mocks` - used for mocking

`rspec-rails` gem integrates RSpec with the Ruby on Rails web framework

# Project Structure

Most projects have a `spec` directory to house all RSpec test files

An RSpec file ends with `_spec.rb` that matches the file it is testing

# Unit Tests vs End-to-End Tests

Unit tests focus on individual units of code in the program
- Elements are tested in isolation
- Specs are easy to write and run fast

![[Images/Pasted image 20250129105846.png|400]]

End-to-end (E2E) or acceptance tests focus on a feature and its interaction with the entire system
- Elements are tested together
	- Complete program is tested with a good deal of confidence
- Specs are hard to write, brittle and run slow

# Install RSpec

```
gem install rspec
```

# Initialize

```
rspec --init
```

The created file `spec_helper.rb` contains a lot of high level configurations

# Spec

## `describe`

```ruby
RSpec.describe 'Card' do

end
```

`describe` takes a parameter which is the class to be tested

then it takes a block

If you pass a class as a parameter to `describe`, instead of a string, it will create an instance of that class

## `it`

`it` creates a specific test case

```ruby
RSpec.describe 'Card' do
  it 'has a type' do
    card = Card.new('Ace of Spades')
    expect(card.type).to eq('Ace of Spades')
  end
end
```

`eq('Ace of Spades')` is a parameter to `to`

parameters can be passed by using a space, as well as `()`

Each `it` method, creates one `example`

## `Before` hooks

```ruby
before do
	@card = Card.new('Ace','Spades')   # instance variable
end
```

`before` will be run before every single example

```ruby
  before(:context) do
    puts 'Before context'
  end

  before(:example) do
    puts 'Before example'
  end
```

Can specify what it runs before

`before(:context)` will run before the surrounding block, e.g. a `describe` block

## `After` hooks

```ruby
  after(:context) do
    puts 'After context'
  end

  after(:example) do
    puts 'After example'
  end
```

## `let` blocks

Pass a symbol to the `let`

Then provide a `block`

The `block` will be evaluated and the result will be assigned to the symbol

```ruby
let(:card) { Card.new('Ace','Spades') }
```

The first time `card` will be evaluated, it will run the `block` and assign the result to `card`

From then on, calling `card` will return the result of the `block` evaluation that was assigned to it

`let`s are good for memory as they will only be evaluated when they are called

You can reuse a `let` variable multiple times, and the first time it is evaluated in each scope, will be a new instance

## `context`

`context` is an alias for `describe`

## `subject`

[[notes/Ruby/RSpec#`describe`|describe]] will create an instance of the class passed to it, `subject` references this instance

`subject` will be a new instance in each new scope it is used, like [[notes/Ruby/RSpec#`let` blocks|let]]

You can provide an explicit `subject` using

```ruby
subject(:bob) do
    { a: 1, b: 2 }
end
```

## `described_class`

References the class passed to `describe`

```Ruby
RSpec.describe Prince do
  subject { described_class.new('Boris') }
  let(:louis) { described_class.new('Louis') }

  it 'represents a great person' do
    expect(subject.name).to eq('Boris')
    expect(louis.name).to eq('Louis')
  end
end
```

## Shared Examples

Declare examples to be re-used in multiple contexts

```ruby
RSpec.shared_examples 'a Ruby object with three elements' do
  it 'returns the number of items' do
    expect(subject.length).to eq(3)
  end
end

RSpec.describe Array do
  subject { [1, 2, 3] }
  include_examples 'a Ruby object with three elements'
end

RSpec.describe String do
  subject { 'abc' }
  include_examples 'a Ruby object with three elements'
end
```

## Matchers

### `not_to`

Matcher for checking two things are not equal

```ruby
expect(5).not_to eq(10)
```

### Equality Matchers

#### `eq` and `eql`

`eq` tests for value and ignores type

```ruby
let(:a) { 3.0 }
let(:b) { 3 }

  describe 'eq matcher' do
    it 'tests for value and ignores type' do
      expect(a).to eq(3)
      expect(b).to eq(3.0)
      expect(a).to eq(b)
    end
  end
```

`eql` tests for value, including same type

```ruby
let(:a) { 3.0 }
let(:b) { 3 }

describe 'eql matcher' do
    it 'tests for value, including same type' do
      expect(a).not_to eql(3)
      expect(b).not_to eql(3.0)
      expect(a).not_to eql(b)

      expect(a).to eql(3.0)
      expect(b).to eql(3)
    end
  end
```

#### `equal`/`be`

`equal` cares about object identity

```ruby
describe 'equal and be matcher' do
    let(:c) { [1, 2, 3] }
    let(:d) { [1, 2, 3] }
    let(:e) { c }

    it 'cares about object identity' do
      expect(c).to eq(d)
      expect(c).to eql(d)

      expect(c).to equal(e)
      expect(c).to be(e)

      expect(c).not_to equal(d)
      expect(c).not_to equal([1, 2, 3])
    end
  end
```

### Comparison Matchers

Allows for comparison with built-in Ruby operators

```ruby
expect(10).to be > 5
```

### Predicate Matchers

Predicate methods normally end in `?`

Any predicate method can be used with `be` by removing the `?` and adding `_predicatename` after `be`

```ruby
expect(16 / 2).to be_even
expect(15).to be_odd
```

### `all` Matcher

Performs a matcher on all elements in a collection

Only passes if all elements in the collection pass

```ruby
expect([5, 7, 9, 13]).to all(be_odd)
expect([4, 6, 8, 10]).to all(be_even)
```

### `change` Matcher

Checks that a method changes object state

```ruby
subject { [1, 2, 3, 4] }

it 'checks that a method changes object state' do
	expect { subject.push(4) }.to change { subject.length }.by(1)
end
```

### `contain_exactly` Matcher

Check for the presence of all elements in a collection

### `have_attributes` Matcher

Checks for object attribute and proper values

### `include` Matcher

Checks for inclusion in the array, regardless of order

### `start_with` and `end_with` Matchers

Checks for things at the beginning or end of an object

### `raise_error` Matcher

Check for errors being raised

```ruby
it 'can check for a specific error being raised' do
    expect { some_method }.to raise_error(NameError)
    expect { 10 / 0 }.to raise_error(ZeroDivisionError)
end
```

### `respond_to` Matcher

Asserts that an object can respond to certain calls

```ruby
class HotChocolate
  def drink
    'Delicious'
  end

  def discard
    'PLOP!'
  end

  def purchase(number)
    "Awesome, I just purchased #{number} more hot chocolate beverages!"
  end
end

it 'confirms an object can respond to a method with arguments' do
	expect(subject).to respond_to(:purchase)
	expect(subject).to respond_to(:purchase).with(1).arguments
end
```

### `satisfy` Matcher

Used to assert with a given predicate