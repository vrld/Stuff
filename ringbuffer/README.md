# Ringbuffer

## Introduction

... was part of [hump](http://vrld.github.com/hump), but got removed since I
did not really use it in my own games.

## Module ringbuffer [A data structure that wraps around itself.]

	Ringbuffer = require "hump.ringbuffer"

A ring-buffer is a circular array: It does not have a first nor a last item,
but it has a *selected* or *current* element.

A ring-buffer can be used to implement [Tomb Raider style
inventories](http://www.youtube.com/watch?v=YTdsKq77_lg), looping play-lists,
recurring dialogs (like a unit's answers when selecting it multiple
times in *Warcraft*) and generally everything that has a circular or looping
structure.

### function new(...) [Create a new ringbuffer.]

Create new ring-buffer.

The module name is a shortcut to this function.

#### Parameters:

=mixed ...=
	Initial elements.

#### Returns:

=Ringbuffer=
	The ring-buffer object.

#### Example:

	ringbuffer = require 'hump.ringbuffer'
	rb = ringbuffer.new(1,2,3)
	-- or:
	rb = ringbuffer(1,2,3)

### function ringbuffer:insert(...) [Inser elements.]

Insert items behind current element.

#### Parameters:

=mixed ...=
	Items to insert.

#### Example:

	rb = Ringbuffer(1,5,6) -- content: 1,5,6
	rb:insert(2,3,4)       -- content: 1,2,3,4,5,6


### function ringbuffer:remove() [Remove currently selected item.]

Remove current item, return it and select next element.

#### Returns:

=mixed=
	The removed item.

#### Example:

	rb = Ringbuffer(1,2,3,4) -- content: 1,2,3,4
	val = rb:remove()        -- content: 2,3,4
	print(val)               -- prints `1'


### function ringbuffer:removeAt(pos) [Remove an item.]

Remove the item at a position relative to the current element.

#### Parameters:

=number pos=
	Position of the item to remove.


#### Returns:

=mixed=
	The removed item.


#### Example:

	rb = Ringbuffer(1,2,3,4,5) -- content: 1,2,3,4,5
	rb:removeAt(2)             -- content: 1,2,4,5
	rb:removeAt(-1)            -- content: 1,2,4


### function ringbuffer:next() [Select next item.]

Select and return the next element.

#### Returns:

=mixed=
	The next item.

#### Example:

	rb = Ringbuffer(1,2,3)
	rb:next()     -- content: 2,3,1
	rb:next()     -- content: 3,1,2
	x = rb:next() -- content: 1,2,3
	print(x)      -- prints `1'

### function ringbuffer:prev() [Select previous item.]

Select and return the previous item.

#### Returns:

=mixed=
	The previous item.

#### Example:

	rb = Ringbuffer(1,2,3)
	rb:prev())    -- content: 3,1,2
	rb:prev())    -- content: 2,3,1
	x = rb:prev() -- content: 1,2,3
	print(x)      -- prints `1'


### function ringbuffer:get() [Get currently selected item.]

Return the current element.

#### Returns:

=mixed=
	The currently selected element.


#### Example:

	rb = Ringbuffer(1,2,3)
	rb:next()       -- content: 2,3,1
	print(rb:get()) -- prints '2'


### function ringbuffer:size() [Get ringbuffer size.]

Get number of items in the buffer

#### Returns:

=number=
	Number of items in the buffer.

#### Example:

	rb = Ringbuffer(1,2,3)
	print(rb:size()) -- prints '3'
	rb:remove()
	print(rb:size()) -- prints '2'
