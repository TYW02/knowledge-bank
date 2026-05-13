


# Establish a type scale

- Most interfaces use way too many font sizes.

#### Choosing font sizes without a system is a bad idea for 2 reasons:
1. It leads to annoying inconsistencies in your design.
2. It slows down your workflow.

## How to define a type system ?
---
### Choosing a scale
- Similar to spacing and sizing, a linear scale won't work.
- Smaller jumps between font sizes are useful at the ==bottom== of the scale
	- Don't waste time deciding between 46px and 48px for large headline

### Modular scale
- Calculate your type scale using a ratio, like 4:5, 2:3 or 1:1.618 (Golden Ratio)
- Start with a sensible base value (16px is common since it's the default for most browsers)
	- Apply your ratio to get next value.

#### This is not the perfect method
1. You end up with fractional values
2. You usually need more sizes

## Hand-crafted scales
![[Pasted image 20240715204118.png]]

## Avoid em units
When building a type scale, don't use em units to define your scale.
	Because em units are relative to the current font size, the computed font size of nested elements is often not actually a value in your scale.

---
# Use good fonts


## Play it safe
- For UI design, the safest bet is fairly neutral sans-serif like Helvetica

### Ignore typefaces with less than five weights
- NOT ALWAYS TRUE
- Use this as a general rule
- You can go onto google font and filter "Number of styles to 10+"


## Optimize for legibility
- Fonts are usually designed for a specific purpose
- Font meant for headlines usually have tighter letter-spacing and shorter lowercase
- Font for smaller sizes have wider letter-spacing and taller lowercase letters


## Trust the wisdom of the crowd
- If a font is popular, it's probably a good font
- Especially useful when picking something other than a neutral UI typeface

## Steal from people who care
- Inspect your favorite site and see what typeface they are using.

---

# Keep your line length in check
- Try and create the best reading experience
- For the best reading experience, make your paragraphs wide enough to fit between 45 and 75 characters per line.


### Dealing with wider content
- If you are mixing paragraph text with images or other large components, you should still limit the width
![[Pasted image 20240715205154.png]]


![[Pasted image 20240715205201.png]]


---

# Baseline, not center
- When mixing font sizes, you might want o vertically center the text for balance.
![[Pasted image 20240715205325.png]]

- A Better approach is to align mixed font sizes by their baseline, which is the imaginary line that letters rest on
![[Pasted image 20240715205417.png]]



# Line-height is proportional
- A line height of 1.5 is a good starting point
- However, you cannot use the same value for all situations


### Accounting for line length
- We add space between lines of text to make it easy for the reader to fine the next line when it wraps.
- Narrow content can use a shorter line-height like 1.5 but for wide content it might need a height of 2

### Account for font size
- When text is small, extra line spacing is important because it makes it a lot easier for your eyes to find the next line when the text wraps
- BUT when texts get larger you don't need as much help. Hence, a line-height of 1 is fine
![[Pasted image 20240715205836.png]]



# Not every link needs a colour
![[Pasted image 20240715205910.png]]

![[Pasted image 20240715205922.png]]


# Align with readability in mind
- Text should be aligned to match the direction of the language it's written in (left aligned)

### Don't center long form text
- Center alignment can look great for headline or short blocks of text
- But if it is longer than 2 or 3 lines, it will almost always look better left-aligned
![[Pasted image 20240715210113.png]]

If you’ve got a few blocks of text you want to center but one of them is a bit too long, the easiest fix is to rewrite the content and make it shorter:
![[Pasted image 20240715210136.png]]


# Right-align numbers
![[Pasted image 20240715210157.png]]


# Hyphenate justified text
![[Pasted image 20240715210303.png]]

![[Pasted image 20240715210310.png]]


---

# Use letter-spacing effectively
- As a general rule, you should trust the typeface designer and leave letter-spacing alone.
- That said, there are a couple of common situations where adjusting it can improve your design.


## Tightening headlines
![[Pasted image 20240715210542.png]]

### Improving all-caps legibility
![[Pasted image 20240715210601.png]]









































