





# Start with too much white space

One of the easiest ways to clean up a design is to simply give every element
a little more room to breathe.

![[Pasted image 20240706235423.png]]

# White space should be removed, not added

When designing for the web, white space is almost always added to a design
— if something looks little too cramped, you add a bit of margin or padding
until things look better.

![[Pasted image 20240706235518.png]]

The problem with this approach is that elements are only given the minimum
amount of breathing room necessary to not look actively bad. To make
something actually look great, you usually need more white space.

A better approach is to start by giving something way too much space, then
remove it until it you’re happy with the result.

![[Pasted image 20240706235540.png]]

# Dense UIs have their place

For example, if you’re designing some sort of dashboard where a lot of
information needs to be visible at once, packing that information together so
it all fits on one screen might be worth making the design feel more busy.

![[Pasted image 20240706235627.png]]


# Establish a spacing and sizing system

You shouldn’t be nitpicking between 120px and 125px when trying to decide
on the perfect size for an element in your UI.

![[Pasted image 20240706235719.png]]

## A linear scale won't work

Creating a spacing and sizing system isn’t quite as simple as something like
“make sure everything is a multiple of 4px” — a naive approach like that
doesn’t make it any easier to choose between 120px and 125px.

![[Pasted image 20240706235858.png]]

If you want your system to make sizing decisions easy, make sure no two
values in your scale are ever closer than about ==25%==.


# Defining the system

A simple approach is to start with a sensible base value, then build a scale
using factors and multiples of that value.

==16px== is a great number to start with because it divides nicely, and also
happens to be the default font size in every major web browser.


# You don't have to fill the whole screen

So it’s no surprise that when most of us open our design tool of choice on
our high resolution displays, we give ourselves at least 1200-1400px of space
to fill. But just because you have the space, doesn’t mean you need to use it.

![[Pasted image 20240707164432.png]]

If you only need 600px, use 600px. Spreading things out or making things
unnecessarily wide just makes an interface harder to interpret, while a little
extra space around the edges never hurt anyone.

![[Pasted image 20240707164446.png]]

This is just as applicable to individual sections of an interface, too. You don’t
need to make everything full-width just because something else (like your
navigation) is full-width.

![[Pasted image 20240707164505.png]]


## Shrink the canvas

If you’re having a hard time designing a small interface on a large canvas,
shrink the canvas! A lot of the time it’s easier to design something small
when the constraints are real.

![[Pasted image 20240707164544.png]]

![[Pasted image 20240707164554.png]]

# Thinking in columns

If you’re designing something that works best at a narrower width but feels
unbalanced in the context of an otherwise wide UI, see if you can split it into
columns instead of just making it wider.

![[Pasted image 20240707164635.png]]

If you wanted to make better use of the available space without making the
form harder to use, you could break the supporting text out into a separate
column:

![[Pasted image 20240707164656.png]]

# Don't force it

```
Just like you shouldn’t worry about filling the whole screen, you shouldn’t try
to cram everything into a small area unnecessarily either.

If you need a lot of space, go for it! Just don’t feel obligated to fill it if you
don’t have to.
```


# Grids are overrated

Using a system like a 12-column grid is a great way to simplify layout
decisions, and can bring a satisfying sense of order to your designs.

![[Pasted image 20240707164803.png]]

But even though grids can be useful, outsourcing all of your layout decisions
to a grid can do more harm than good.


## Not all elements should be fluid

Instead of using a relative width with the grid system consider using a fixed width instead

For example, if you have a sidebar of 25% when the screen gets wider the sidebar gets wider too.
And when the screen gets smaller the sidebar shrinks and can cause awkward text wrapping.

Instead consider using a fixed sidebar width:

![[Pasted image 20240707165144.png]]

```
This applies within components, too — don’t use percentages to size
something unless you actually want it to scale.
```

![[Pasted image 20240707165209.png]]


Instead of sizing elements like this based on a grid, give them a max-width
so they don’t get too large, and only force them to shrink when the screen
gets smaller than that max-width.


# Relative sizing doesn't scale

For example, say you’re designing an article at a large screen size. If your
body copy is 18px and your headlines are 45px, it’s tempting to encode that
relationship by defining your headline size as 2.5em; 2.5 times the current
font size.

![[Pasted image 20240707165438.png]]

A better headline size for small screens might be somewhere between 20px
and 24px:

![[Pasted image 20240707165450.png]]


# Avoid ambiguous spacing

When groups of elements are explicitly separated — usually by a border or
background color — it’s obvious which elements belong to which group.

![[Pasted image 20240707165704.png]]

```
Say you’re designing a form with stacked labels and inputs. If the margin
below the label is the same as the margin below the input, the elements in
the form group won’t feel obviously “connected”.
```

![[Pasted image 20240707165735.png]]

The fix is to increase the space between each form group so it’s clear which
label belongs to which input:
![[Pasted image 20240707165752.png]]

This same problem shows up in article design when there’s not enough
space above section headings:
![[Pasted image 20240707165815.png]]

It’s not just vertical spacing that you have to worry about either; it’s easy to
make this mistake with components that are laid out horizontally, too:
![[Pasted image 20240707165839.png]]






