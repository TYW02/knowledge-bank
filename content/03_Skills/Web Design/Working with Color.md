
# Ditch hex for HSL
- Using hex or RGB, colors that have a lot in common visually look nothing alike in code
- HSL fixes this by representing colors using attributes the human-eye perceives

SATURATION
- How colourful or vivid a color looks 0% is grey and 100% is vibrant and intense
- Without saturation, hue is irrelevant

LIGHTNESS
- Measures how close a color is to black or white: 0% is pure black, 100% is pure white, 50% is pure color at the given hue

HSL vs HSB
- Lightness and Brightness is not the same thing
- 0% brightness is always BLACK, 100% is only white when saturation is 0%
- BROWSERS ONLY UNDERSTAND HSL


---


# You need more colors than you think

> [!IMPORANT]
> DON'T USE COLOR PALETTE GENERATORS !!

![[Pasted image 20240716204126.png]]

## What you actually need
- To build something real, you need a much more comprehensive set of colors to choose from.

> [!INFO]
> You can break a good color palette down into three categories.


### Greys
- Text, background, panels, form controls - almost everything in an interface is grey
![[Pasted image 20240716204327.png]]

- You'll need more greys than you think.
- In practice, you want 8 - 10 shades to choose from.
	- True black tends to look pretty unnatural, so start with a really dark grey and work your way up to white in steady increments


### Primary Color(s)
- Most sites need one, maybe two colors that are used for primary actions, action navigation elements, etc.
- Just like with grey, you need a variety (5-10) of lighter and darker shades to choose from.
- Ultra-light shades can be useful as a tinted background for things like alerts, while darker shades work great for text.


### Accent Colors
- Every site needs a few accent colors for communicating different things to the user
	- E.g. Using a eye-grabbing color like yellow, pink, or teal to highlight a feature

![[Pasted image 20240716204836.png]]
- You’ll want multiple shades for these colors too, even though they should be used pretty sparingly throughout the UI.

---

# Define your shades up front

- Define a fixed set of shades up front that you can choose from as you work.

```
So how do you put together a palette like this anyways ?
```


## Choose the base color first

- Start with the base color for the scale you want to create - the color in the middle that your lighter and darker shades are based on.
- For PRIMARY and ACCENT colors, pick a color that would work well as a button background


## Finding the edges

- Pick you darkest shade and you lightest shade.
	- The Darkest shade of a color is usually reserved for text
	- The Lightest shade might be used to tint the background of an element

- Start with a color that matches the hue of your base color, and adjust the saturation and lightness until you're satisfied


## Filling in the gaps
- Once you’ve got your base, darkest, and lightest shades, you just need to fill in the gaps in between them
- For most projects, you’ll need at least 5 shades per color, and probably closer to 10 if you don’t want to feel too constrained.
![[Pasted image 20240716205434.png]]


## It's not a science

- You can’t rely purely on math to craft the perfect color palette.
- A systematic approach like the one described above is great to get you started, but don’t be afraid to make little tweaks if you need to.
```
Just try to avoid adding new shades too often if you can avoid it. If you’re not diligent about limiting your palette, you might as well have no color system at all.
```


# Don't let lightness kill your saturation
- In HSL as a color gets closer to 0% or 100% lightness, the impact of saturation is weakened
- The same saturation value at 50% lightness looks more colorful than it does at 90% lightness

> [!info]
> If you don’t want the lighter and darker shades of a given color to look washed out, you need to increase the saturation as the lightness gets further away from 50%.
![[Pasted image 20240716205805.png]]


# Using perceived brightness to your advantage
![[Pasted image 20240716205855.png]]


# Changing brightness by rotating hue

- Normally when you change how light a color looks, you adjust the lightness component
	- Although it works, you often lose some of the color's intensity
![[Pasted image 20240716210118.png]]

- To make a color lighter, rotate the hue towards the nearest bright hue — 60°, 180°, or 300°.
![[Pasted image 20240716210208.png]]

- To make a color darker, rotate the hue towards the nearest dark hue — 0°, 120°, or 240°.
![[Pasted image 20240716210231.png]]

> [!info]
> This can be really useful when trying to create a palette for a light color like yellow. By gradually rotating the hue towards more of an orange as you decrease the lightness, the darker shades will feel warm and rich instead of dull and brown


>[!error]
>Don’t rotate the hue more than 20-30° or it will look like a totally different color instead of just lighter or darker.

---


# Greys don't have to be grey
-  A lot of colors that we think of as grey are actually saturated quite heavily
![[Pasted image 20240716210536.png]]
This is what gives the grey a cool or warm feel


## Color temperature
- If you want your greys to feel cool, saturate them with a bite of blue
![[Pasted image 20240716210640.png]]

- To give you greys a warmer feel, saturate them with a bit of yellow or orange
![[Pasted image 20240716210716.png]]

```
To maintain a consistent temperature, don’t forget to increase the saturation for the lighter and darker shades. If you don’t, those shades will look a bit washed out compared to the greys that are closer to 50% lightness.
```


# Accessible doesn't have to mean ugly
- To make sure your designs are accessible, the Web Content Accessibility Guidelines (WCAG) recommend that normal text (under ~18px) has a contrast ratio of at least 4.5:1, and that larger text has a contrast ratio of at least 3:1.
![[Pasted image 20240716211044.png]]

![[Pasted image 20240716211059.png]]

## Flipping the contrast
- When using white text on a colored background, you’d be surprised how dark the color often needs to be to meet that 4.5:1 contrast ratio.
![[Pasted image 20240716211138.png]]

- This can create hierarchy issues when those elements ==aren’t supposed to be the focus== of the page — dark colored backgrounds will really grab the user’s attention.
![[Pasted image 20240716211157.png]]

- You can solve this problem by flipping the contrast. Instead of using light text on a dark colored background, use ==dark colored text== on a ==light colored background==:
![[Pasted image 20240716211238.png]]


## Rotating the hue
- Even harder than white text on a colored background is colored text on a colored background
- If you start by taking the background color and simply adjusting the lightness and saturation, you’ll find that it’s hard to meet the recommended contrast ratio without getting very close to pure white.

![[Pasted image 20240716211341.png]]

- One way to increase the contrast without getting closer to white is to rotate the hue towards a brighter color, like cyan, magenta, or yellow.
![[Pasted image 20240716211446.png]]


---





