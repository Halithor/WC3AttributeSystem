# Halithor's Attribute System

This is a system for Warcraft III custom maps that is designed to provide a
way to define and track new attributes for units in WC3. Attributes can be 
dependant on each other allowing interactions between the different attributes.

For example, you could have attributes for `base_hp`, `bonus_hp`, and 
`bonus_hp_percent`. Together, you could use them to calculate total hitpoints
via `max_hp = (base_hp + bonus_hp) * bonus_hp_percent`, resulting in a system
that gives the user multiple methods of control. This could even go another 
layer deeper, as `base_hp` could be calculated `base_hp = str * 25`.

This library defines some **primitive attributes**, which are the attributes 
that are basic to units to in Warcraft III. In addition, common bonuses (displayed as '+#' in green) are also available to the system. See below for a complete listing. 

The system also constructs a tree of attribute dependency. The system then restricts bonuses that can be applied to only **master attributes**, or attributes that are not dependent on another. In the example above, you could never directly set `total_hp`, as it is a **dependent attribute** of the other attributes in the system. Primitive attributes will vary likely be the bottom-most dependent attributes, as they end up being the expression of this system in game.

This tree is also used to efficiently cascade updates down the tree when an attribute is changed. In the example above, changing strength would update `base_hp` and that would cascade into updating `max_hp`.

## Usage Requirements

**Usage of this system will break many attributes and attribute bonuses that are native to WC3** 

This includes hero attribute bonuses, item bonuses, unit basic attacks, etc. 
Essentially, any bonus that is applied outside of this system will most likely
cause an error, cause inconsistencies, or just plain not work. As such, using 
this system requires you to commit to using it for all attribute bonus.

## Primitive Attributes

- Hitpoints
- Mana
- HP Regen (flat)
- Mana Regen (flat)
- Armor
- Attack Cooldown
- Attack Damage Base
- Attack Damage Dice
- Attack Damage Dice Sides
- Movespeed
- Agility
- Strength
- Intelligence

*Note: HP and Mana regen use the abilities to provide their effects*

## Primitive Bonuses

These bonuses are essentially for the graphical difference. You can use them to
clarify what comes from gear vs what comes from base stats. Or whatever you want
them to do.

- Armor
- Attack Damage
- Agility
- Strength
- Intelligence