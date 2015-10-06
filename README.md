# smartenum
Macros for declaring enums in C++ that include to_string conversion and looping through all enum values

## Purpose
Sometimes, you find the need of converting enum values to strings mostly for debugging/logging purposes. This can easily be achieved by maintaining a map that maps the enum values to strings. Doing this manually however is a source for errors since one might forget to update it when enum values are added, or just do a mistake when copy-pasting. I am also a fan of reducing boilerplating. These factors made me create this header file.

## Features
* Automatic generation of to_string functions for converting enum values to string representations
* Provides a way to loop through all values of an enum
* Supports both enums and enum classes
* Self contained header file

## Usage
Smart enums are very easy to use. The code below shows it all.

```
#include "smartenum.hpp"

//declares a normal enum 'Day'
smart_enum(Day, MONDAY, TUESDAY, THURSDAY = 4, FRIDAY);

//declares an enum class 'Dish'. Newline works as expected
smart_enum_class(Dish, PANCAKE,
    OMELETTE = 2,
    WAFFLES = 42);

int main()
{
    //with normal enums, the to_string function is prepended with <ENUM_NAME>_ to avoid collisions
    std::cout << Day_to_string(MONDAY) << " " << Day_to_string(TUESDAY) << " " << Day_to_string(THURSDAY) << " " << Day_to_string(FRIDAY) << "\n";

    //with enum classes, the to_string function is used as is
    std::cout << to_string(Dish::PANCAKE) << " " << to_string(Dish::OMELETTE) << " " << to_string(Dish::WAFFLES) << "\n";
    //enum classes also support ostream conversion directly
    std::cout << Dish::PANCAKE << " " << Dish::OMELETTE << " " << Dish::WAFFLES << "\n\n";

    //The macros define a way to access the enum values as a list (std::vector)
    std::cout << "The days of the week are:\n";
    for(Day day : Day_list)
    {   
        std::cout << Day_to_string(day) << " ";
    }   
    std::cout << "\n\n";

    std::cout << "The dishes we have are:\n";
    for(Dish dish : Dish_list)
    {   
        std::cout << to_string(dish) << " ";
    }   
    std::cout << "\n\n";
}
```

The above code prints:

```
MONDAY TUESDAY THURSDAY FRIDAY
PANCAKE OMELETTE WAFFLES
PANCAKE OMELETTE WAFFLES

The days of the week are:
MONDAY TUESDAY THURSDAY FRIDAY 

The dishes we have are:
PANCAKE OMELETTE WAFFLES
```

## Feedback
Any suggestions on how to improve the existing codes or features to add are welcome!
