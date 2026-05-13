
Chapter Content:
[[#Start with a feature, not a layout]] (How to start designing)
[[#Detail comes later]] 
[[#Be a pessimist]] (Design the bare minimum first)
[[#Choose a personality]] (The business's personality)
[[#Border radius]]
[[#Deciding what you actually want]]
[[#Limit your choices]]
[[#Systematize everything]]


# Start with a feature, not a layout
```
The thing is, an “app” is actually a collection of features. Before you’ve
designed a few features, you don’t even have the information you need to
make a decision about how the navigation should work. No wonder it’s
frustrating!
```



Instead of starting with the shell, start with a piece of actual functionality.
For example, say you’re building a flight booking service. You could start
with a feature like “searching for a flight”.

Your interface will need:

• A field for the departure city
• A field for the destination city
• A field for the departure date
• A field for the return date
• A button to perform the search

 
# Detail comes later

```
In the earliest stages of designing a new feature, it’s important that you don’t
get hung up making low-level decisions about things like typefaces,
shadows, icons, etc.
```


### Hold the color

```
By designing in grayscale, you’re forced to use spacing, contrast, and size to
do all of the heavy lifting.
```

### Work in cycles

```
Instead of designing everything up front, work in short cycles. Start by
designing a simple version of the next feature you want to build.
```

Iterate on the working design until there are no more problems left to solve, then jump back into design mode and start working on the next feature.


# Be a pessimist

Don’t imply functionality in your designs that you aren’t ready to build.

"You get deep into implementation only to discover that supporting
attachments is going to be a lot more work than you anticipated. There’s no
way you have time to finish it right now, so the whole commenting system
sits on the backburner while you take care of other priorities."

```
When you’re designing a new feature, expect it to be hard to build.
Designing the smallest useful version you can ship reduces that risk
considerably.
```


# Choose a personality

```
Every design has some sort of personality. A banking site might try to
communicate secure and professional, while a trendy new startup might
have a design that feels fun and playful.
```


## Font Choice

```
Typography plays a huge part in determining how a design feels.
If you want an elegant or classic look, you might want to incorporate a serif
typeface in your design:
```

![[Pasted image 20240704185409.png]]

For a playful look, you could use a rounded sans serif:
![[Pasted image 20240704185430.png]]

If you’re going for a plainer look, or want to rely on other elements to provide
the personality, a neutral sans serif works great:

![[Pasted image 20240704185454.png]]



## Color

```
There’s a lot of science out there on the psychology of color, but in practice,
you really just need to pay attention to how different colors feel to you.
```

Blue is safe and familiar — nobody ever complains about blue:
![[Pasted image 20240704185543.png]]


Gold might say “expensive” and “sophisticated”:
![[Pasted image 20240704185600.png]]


Pink is a bit more fun, and not so serious:
![[Pasted image 20240704185614.png]]


 
* _Mainly choose the color that looks good to you._ 


# Border radius

A small border radius is pretty neutral, and doesn’t really communicate
much of a personality on its own:

![[Pasted image 20240704185952.png]]


A large border radius starts to feel more playful:
![[Pasted image 20240704190005.png]]


...while no border radius at all feels a lot more serious or formal:
![[Pasted image 20240704190020.png]]

```
Whatever you choose, it’s important to stay consistent. Mixing square
corners with rounded corners in the same interface almost always looks
worse than sticking with one or the other.
```



# Deciding what you actually want
A lot of the time you’ll probably just have a gut feeling for the personality
you’re going for. But if you don’t, a great way to simplify the decision is to
take a look at other sites used by the people who want to reach.

If they are mostly pretty “serious business”, maybe that’s how your site
should look too. If they are more playful with a bit of humor, maybe that’s a
better direction to take.

Just try not to borrow too much from direct competitors, you don’t want to
look like a second-rate version of something else.



# Limit your choices

Having millions of colors and thousands of fonts to choose from might
sound nice in theory, but in practice it’s usually a paralyzing curse.

And it’s not just fonts and colors, either — you can easily waste time
agonizing over almost any minor design decision.

```
Should this text be 12px or 13px?
Should this box shadow have a 10% opacity or a 15% opacity?
Should this avatar be 24px or 25px tall?
Should I use a medium font weight for this button or semibold?
Should this headline have a bottom margin of 18px or 20px?
```


## Define systems in advance
Instead of hand-picking values from a limitless pool any time you need to
make a decision, start with a smaller set of options.

Don’t reach for the color picker every time you need to pick a new shade of
blue — choose from a set of 8-10 shades picked out ahead of time.


Similarly, don’t tweak a font size one pixel at a time until it looks perfect.
Define a restrictive type scale in advance and use that to make any future
font size decisions.



## Designing by process of elimination

For example, say you’re trying to choose a size for an icon. You’ve defined a
sizing scale in advance where your only small-to-medium sized options are
12px, 16px, 24px, and 32px.

To pick the best option, start by taking a guess at which one will look best,
maybe 16px. Then try the values on either side (12px and 24px) for
comparison.

![[Pasted image 20240704190427.png]]

Chances are, two of those options will seem like obviously bad choices. If it’s
the options on the outside, you’re done — the middle option is the only good
choice.


If one of the outer options looks best, do another comparison using that
option as the “middle” value and make sure there’s not a better choice.

![[Pasted image 20240704190458.png]]



# Systematize everything

```
The more systems you have in place, the faster you’ll be able to work and the
less you’ll second guess your own decisions.
```

You’ll want systems for things like:
• Font size
• Font weight
• Line height
• Color
• Margin
• Padding
• Width
• Height
• Box shadows
• Border radius
• Border width
• Opacity




