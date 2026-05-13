
[[#Not all elements are equal]]






# Not all elements are equal
```
When you think of visual design as “styling things so they look good”, it’s
easy to see why it might feel hard to achieve without innate artistic talent.
But it turns out that one of the biggest factors in making something “look
good” has nothing to do with superficial styling at all.
```


### Visual Hierarchy
#VisualHierarchy refers to how important the elements in an interface appear in relation to one another, and it's the most effective tool you have for making something feel "designed"

```
When everything in an interface is competing for attention, it feels noisy and
chaotic, like one big wall of content where it’s not clear what actually
matters:
```


![[Pasted image 20240704190900.png]]


When you deliberately de-emphasize secondary and tertiary information,
and make an effort to ==highlight== the elements that are most important, the
result is immediately more pleasing, even though the color scheme, font
choice, and layout haven’t changed:

![[Pasted image 20240704190940.png]]


# Size isn't everything

Relying too much on font size to control your hierarchy is a mistake — it
often leads to primary content that’s too large, and secondary content that’s
too small.

![[Pasted image 20240704191030.png]]


Instead of leaving all of the heavy lifting to font size alone, try using font
weight or color to do the same job.

For example, making a primary element bolder lets you use a more
reasonable font size, and often does a better job at communicating its
importance anyways:

![[Pasted image 20240704191132.png]]

Similarly, using a softer color for supporting text instead of a tiny font size
makes it clear that the text is secondary while sacrificing less on readability:

![[Pasted image 20240704191155.png]]


```
Try and stick to two or three colors:
• A dark color for primary content (like the headline of an article)
• A grey for secondary content (like the date an article was published)
• A lighter grey for tertiary content (maybe the copyright notice in a
footer)
```


```
Similarly, two font weights are usually enough for UI work:
• A normal font weight (400 or 500 depending on the font) for most text
• A heavier font weight (600 or 700) for text you want to emphasize

Stay away from font weights under 400 for UI work — they can work for
large headings but are too hard to read at smaller sizes. If you’re considering using a lighter weight to de-emphasize some text, use a lighter color or
smaller font size instead.
```



# Don't use grey text on colored backgrounds

```
Making text a lighter grey is a great way to de-emphasize it on white
backgrounds, but it doesn’t look so great on colored backgrounds.
```

![[Pasted image 20240704191356.png]]


Making the text closer to the background color is what actually helps create
hierarchy, not making it light grey.

![[Pasted image 20240704191425.png]]

A better approach is to hand-pick a new color, based on the background
color.

Choose a color with the ==same hue==, and adjust the saturation and lightness
until it looks right to you:

![[Pasted image 20240704191527.png]]


# Emphasize by de-emphasizing

Sometimes you’ll run into a situation where the main element of an interface
isn’t standing out enough, but there’s nothing you can add to it to give it the
emphasis it needs.

For example, despite trying to make this active nav item “pop” by giving it a
different color, it still doesn’t really stand out compared to the inactive items:

![[Pasted image 20240704191620.png]]

```
When you run into situations like this, instead of trying to further emphasize

the element you want to draw attention to, figure out how you can de-
emphasize the elements that are competing with it.
```

In this example, you could do that by giving the inactive items a softer color
so they sit more in the background:

![[Pasted image 20240704191645.png]]


You can apply this thinking to bigger pieces of an interface as well. 

For example, if a sidebar feels like it’s competing with your main content area,
don’t give it a background color — let the content sit directly on the page
background instead:

![[Pasted image 20240704191721.png]]


## Labels are a last resort

When presenting data to the user (especially data from the database), it’s
easy to fall into the trap of displaying it using a naive label: value format.
![[Pasted image 20240706233518.png]]

The problem with this approach is that it makes it difficult to present the
data with any sort of hierarchy; every piece of data is given equal emphasis.

### You might not need a label at all

```
In a lot of situations, you can tell what a piece of data is just by looking at the
format.
```

![[Pasted image 20240706233558.png]]

When you’re able to present data without labels, it’s much easier to
emphasize important or identifying information, making the interface easier
to use while at the same time making it feel more “designed”.

### Combine labels and values
```
Even when a piece of data isn’t completely clear without a label, you can
often avoid adding a label by adding clarifying text to the value.
```

![[Pasted image 20240706233642.png]]

![[Pasted image 20240706233654.png]]

When you’re able to combine labels and values into a single unit, it’s much
easier to give each piece of data meaningful styling without sacrificing on
clarity.

## Labels are secondary

In these situations, add the label, but treat it as supporting content. The data
itself is what matters, the label is just there for clarity.

![[Pasted image 20240706233728.png]]

- De-emphasize the label by making it smaller, reducing the contrast, using a lighter font weight, or some combination of all three.

### When to emphasize a label

If you’re designing an interface where you know the user will be looking for
the label, it might make sense to the emphasize the label instead of the data.

![[Pasted image 20240706233836.png]]

- Don’t de-emphasize the data too much in these scenarios; it’s still important
information. Simply using a darker color for the label and a slightly lighter
color for the value is often enough.


# Separate visual hierarchy from document hierarchy

Using an h1 tag to add a title like Manage Account to a page makes perfect
sense semantically, but because we’re trained to believe that h1 elements
should be big, it’s easy to fall into the trap of making those titles bigger than
they really need to be.

![[Pasted image 20240706234259.png]]

A lot of the time, section titles act more like labels than headings — they are
supportive content, they shouldn’t be stealing all the attention.

Usually the content in that section should be the focus, not the title. That
means that a lot of the time, titles should actually be pretty small:

![[Pasted image 20240706234326.png]]

Don’t let the element you’re using influence how you choose to style it —
pick elements for semantic purposes and style them however you need to
create the best visual hierarchy.


# Balance weight and contrast

The reason bold text feels emphasized compared to regular text is that bold
text covers more surface area — in the same amount of space, more pixels
are used for text than for the background.

![[Pasted image 20240706234423.png]]

So why is this interesting? Well it turns out that the relationship between
surface area and hierarchy has implications on other elements in a UI as well.

## Using contrast to compensate for weight

Just like bold text, icons (especially solid ones) are generally pretty “heavy”
and cover a lot of surface area. As a result, when you put an icon next to
some text, the icon tends to feel emphasized.

![[Pasted image 20240706234526.png]]

Unlike text, there’s no way to change the “weight” of an icon, so to create
balance it needs to be de-emphasized in some other way.

A simple and effective way to do this is to lower the contrast of the icon by
giving it a softer color.

![[Pasted image 20240706234545.png]]

## Using weight to compensate for contrast

This is useful when things like thin 1px borders are too subtle using a soft
color, but darkening the color makes the design feel harsh and noisy.

![[Pasted image 20240706234919.png]]

Making the border a bit heavier by increasing the width helps to emphasize
it without losing the softer look:

![[Pasted image 20240706234930.png]]

# Semantics are secondary

When there are multiple actions a user can take on a page, it’s easy to fall
into the trap of designing those actions based purely on semantics.

![[Pasted image 20240706235003.png]]

- *Primary actions should be obvious* --> Solid high contrast background colours work great here
- Secondary actions should be clear but no prominent --> Outline styles or lower contrast background colours are great options
- Tertiary actions should be discoverable but unobtrusive --> Styling these actions like links is usually the best approach.

![[Pasted image 20240706235231.png]]

![[Pasted image 20240706235256.png]]

### Destructive actions

Being destructive or high severity doesn’t automatically mean a button
should be big, red, and bold.

![[Pasted image 20240706235327.png]]


















