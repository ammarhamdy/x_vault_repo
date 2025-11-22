
The word variable comes from the latin `variāre` which means “to make changeable.” This is an apt name because the value assigned to a variable can change.

![[Pasted image 20250918161225.png]]

```php
$my_name = "Aisle Nevertell";
```

To declare a variable we use the dollar sign character (`$`) followed by our chosen variable name.

The dollar sign is known as a _`sigil`_; it’s a character that allows the computer to see quickly that something is a variable.

```php
$favorite_food = "Red curry with eggplant, green beans, and peanuts";  
echo $favorite_food;
```

```php
$first_player_rank = "Beginner";  
$second_player_rank = $first_player_rank;  
echo $second_player_rank; // Prints: Beginner  
  
$first_player_rank = "Intermediate"; // Reassign the value of $first_player_rank  
echo $second_player_rank; // Still Prints: Beginner
```

We can also create an alias, or nickname, for a variable. 

Instead of a copy of the original variable’s value, we create a new name which points to the same spot in memory.

We use a different operator for this—the reference assignment operator (`=&`).

```php
$first_player_rank = "Beginner";
$second_player_rank =& $first_player_rank; 
echo $second_player_rank; // Prints: Beginner

$first_player_rank = "Intermediate"; // Reassign the value of $first_player_rank
echo $second_player_rank; // Prints: Intermediate

```