<div align="center">

## Playing Cards


</div>

### Description

A simple program for playing cards manipulation.

The program can shuffle a deck, print cards, deal

cards to players and check for flushes.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Eli](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/eli.md)
**Level**          |Beginner
**User Rating**    |4.0 (16 globes from 4 users)
**Compatibility**  |C\+\+ \(general\)
**Category**       |[Games](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/games__3-13.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/eli-playing-cards__3-361/archive/master.zip)

### API Declarations

```
#include <iostream.h>
#include <time.h>
#include <stdlib.h>
#include <conio.h>
```


### Source Code

```
//**************************************************
//
// A simple program for playing cards manipulation.
// The program can shuffle a deck, print cards, deal
// cards to players and check for flushes.
//
//**************************************************
#include <iostream.h>
#include <time.h>
#include <stdlib.h>
#include <conio.h>
enum suit {clubs, diamonds, hearts, spades};
struct card
{
 suit s;     // The card's suit: C, D, H or S
 int value;    // The value of the card: 2 - 10, A, J, Q or K
};
const int players = 6;  // Number of players
const int pl_cards = 5;  // Number of cards for every player
// Function ptototypes
void pr_card(const card*);
void init_deck(card []);
void shuffle(card []);
void pr_deck(const card []);
void deal_hands(const card [], card [players][pl_cards]);
void print_hands(const card [players][pl_cards]);
int is_flush(const card h[pl_cards]);
// The main program
int main()
{
 card deck[52];    // A deck of 52 cards
 card hand[players][pl_cards];   // 6 hands, 5 cards in each
 clrscr();
 randomize();
 init_deck(deck);
 cout << "Unshuffled card deck: ";
 pr_deck(deck);
 shuffle(deck);
 cout << endl << "Shuffled card deck: ";
 pr_deck(deck);
 deal_hands(deck, hand);
 print_hands(hand);
 for (int i = 0; i < players; i++)
 {
  if (is_flush(hand[i]))
   cout << endl << "Player " << i << " has a flush !";
 }
 cout << endl;
 return 0;
}
// This function prints a single card
void pr_card(const card* cd)
{
 // Check the value of the card, and the 4 special values
 // which are for Ace, Jack, Queen or King
 switch (cd->value)
 {
  case 1 : cout << "A"; break;
  case 11: cout << "J"; break;
  case 12: cout << "Q"; break;
  case 13: cout << "K"; break;
  default: cout << cd->value;
 }
 // Check the card's suit
 switch (cd->s)
 {
  case clubs:  cout << "C"; break;
  case diamonds: cout << "D"; break;
  case hearts:  cout << "H"; break;
  case spades:  cout << "S"; break;
  default: cerr << "suit error" << endl; exit(1);
 }
 cout << " ";
}
// This function initializes a deck of cards
void init_deck(card d[])
{
 for (int i = 0; i < 52; i++)
 {
  // First 13 cards are spades, next 13 are diemonds etc...
  switch (i / 13)
  {
   case 0: d[i].s = clubs; break;
   case 1: d[i].s = diamonds; break;
   case 2: d[i].s = hearts; break;
   case 3: d[i].s = spades; break;
  }
  // Assign the card value
  d[i].value = 1 + i % 13;
 }
}
// This function prints the deck
void pr_deck(const card d[])
{
 for (int i = 0; i < 52; i++)
 {
  // Print a newline after each 13 cards (for a better look)
  if (i % 13 == 0)
   cout << "\n";
  pr_card(&d[i]);  // Print cards using pr_card
 }
 cout << endl;
}
// This function shuffles the deck
void shuffle(card d[])
{
 for (int i = 0; i < 52; i++)
 {
  // Shuffles the cards using a random number generator, each
  // card is replaced with some random card from the same deck
  int k = random(52);
  card temp = d[i];
  d[i] = d[k];
  d[k] = temp;
 }
}
// This function deals the cards to the players
void deal_hands(const card d[], card h[players][pl_cards])
{
 int next_player = 0, next_card = 0;
 for (int i = 0; i < 52; i++)
 {
  // Fill the player's hands equally, card by card
  h[next_player][next_card] = d[i];
  next_player++;
  if (next_player > players)
  {
   next_player = 0;
   next_card++;
  }
 }
}
// This function prints the hands
void print_hands(const card h[players][pl_cards])
{
 cout << endl << "The hands are: "<< endl;
 // Print the hands of all player, each in separate line
 for (int i = 0; i < players; i++)
 {
  cout << "Player " << i << ": ";
  for (int j = 0; j < pl_cards; j++)
   pr_card(&h[i][j]);
  cout << endl;
 }
}
// This function checks for flush
// Flush is 5 or more cards of the
// same suit
// Return 1 if true, 0 if false
int is_flush(const card h[pl_cards])
{
 // Suit counters
 int num_clubs = 0;
 int num_diamonds = 0;
 int num_hearts = 0;
 int num_spades = 0;
 for (int i = 0; i < pl_cards; i++)
 {
  switch(h[i].s)   // Check the card's suit
  {
   case clubs:  num_clubs++ ; break;
   case diamonds: num_diamonds++; break;
   case hearts:  num_hearts++; break;
   case spades:  num_spades++; break;
  }
 }
 // Check for flush
 if (num_clubs >= 5 || num_diamonds >= 5 ||
			 num_hearts >= 5 || num_spades >= 5)
  return 1;
 else
  return 0;
}
```

