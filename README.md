# Dealer

A card-based DSL  from Groxio. 

A [Groxio](https://grox.io) project that teaches developers the fit and finish we can add to APIs in Elixir. We'll use

- `__using__` macro, to establish imports and aliases
- The `inspect` protocol to establish sorting
- Custom sort functions
- Custom sigils for hands and cards

## Features

DSLs in Elixir have tons of options. We're building a simple one that uses base language features without macros beyond `use`

### Quickly generate a card

Using a string: 

```
iex> card "qh" 
Q♥️ 
iex> card "Qh"
Q♥️ 
```

Using a numeric rank and suit

```
iex> card 1, :hearts
A♥️ 
iex> card 1, :spades
A♠️ 
```

### K sigil for cards

```
iex> ~k|qc|
Q♣️ 
iex> ~k|4d|
4♦️ 
```

### Work with decks

```
iex> deck
[A♠️ , A♥️ , A♦️ , A♣️ , 2♠️ , 2♥️ , 2♦️ , 2♣️ ,
 3♠️ , 3♥️ , 3♦️ , 3♣️ , 4♠️ , 4♥️ , 4♦️ , 4♣️ ,
 5♠️ , 5♥️ , 5♦️ , 5♣️ , 6♠️ , 6♥️ , 6♦️ , 6♣️ ,
 7♠️ , 7♥️ , 7♦️ , 7♣️ , 8♠️ , 8♥️ , 8♦️ , 8♣️ ,
 9♠️ , 9♥️ , 9♦️ , 9♣️ , 10♠️ , 10♥️ , 10♦️ ,
 10♣️ , J♠️ , J♥️ , J♦️ , J♣️ , Q♠️ , Q♥️ ,
 Q♦️ , Q♣️ , K♠️ , K♥️ , ...]
iex> deck |> shuffle
[2♥️ , 10♣️ , 7♦️ , K♥️ , A♠️ , 8♥️ , Q♥️ ,
 9♣️ , 4♥️ , A♦️ , J♣️ , 5♣️ , 2♣️ , 3♦️ ,
 10♠️ , A♣️ , 9♠️ , J♥️ , K♣️ , Q♠️ , 6♥️ ,
 A♥️ , J♠️ , 3♥️ , Q♦️ , 10♦️ , 8♠️ , 4♣️ ,
 2♦️ , 4♦️ , 2♠️ , 7♠️ , 3♣️ , 8♣️ , 7♥️ ,
 10♥️ , 6♦️ , 3♠️ , J♦️ , 5♥️ , 7♣️ , Q♣️ ,
 8♦️ , 6♣️ , 5♦️ , 5♠️ , K♦️ , K♠️ , 9♥️ , 9♦️ ,
 ...]
```

### Sigil h for hands

```
iex(23)> royal_flush = ~h|as ks qs js 10s|
[A♠️ , K♠️ , Q♠️ , J♠️ , 10♠️ ]
```

### Common sort schemes

```
iex> royal_flush |> sort(:bridge)
[A♠️ , K♠️ , Q♠️ , J♠️ , 10♠️ ]
iex> full_house |> sort(:poker)     
[A♠️ , A♦️ , A♥️ , 2♥️ , 2♦️ ]
```

### Deal games from a deck

```
iex(31)> deck |> deal(4, 5, :poker)
[
  [K♦️ , J♠️ , 9♦️ , 4♠️ , 3♠️ ],
  [Q♠️ , 9♠️ , 8♥️ , 7♠️ , 5♦️ ],
  [K♣️ , 10♦️ , 8♦️ , 6♠️ , 2♦️ ],
  [J♥️ , 10♣️ , 6♦️ , 5♥️ , 4♣️ ]
]
```

### Inspect for nice representations

The inspection protocol is implemented for Card. 

```
iex(9)> deal deck(), 4, 13, :bridge
[
  [5♠️ , 10♥️ , 5♥️ , 4♥️ , 3♥️ , K♦️ , 9♦️ ,
   8♦️ , K♣️ , J♣️ , 9♣️ , 4♣️ , 3♣️ ],
  [K♠️ , J♠️ , 8♠️ , 7♠️ , 6♠️ , K♥️ , 7♥️ ,
   J♦️ , 5♦️ , 3♦️ , 2♦️ , A♣️ , Q♣️ ],
  [Q♠️ , 2♠️ , A♥️ , Q♥️ , 9♥️ , 6♥️ , Q♦️ ,
   7♦️ , 6♦️ , 10♣️ , 8♣️ , 5♣️ , 2♣️ ],
  [A♠️ , 10♠️ , 9♠️ , 4♠️ , 3♠️ , J♥️ , 8♥️ ,
   2♥️ , A♦️ , 10♦️ , 4♦️ , 7♣️ , 6♣️ ]
]
```

## Installation

Solve it yourself! Build this project, test first, as part of [groxio](https://grox.io) projects. 

Bring in as a git dependency, then:

```
defmodule MyModule do
  use Dealer
  
  ...use card awesomeness...
  
end
```
