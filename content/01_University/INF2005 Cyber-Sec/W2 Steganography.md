---
title: W2 Steganography
tags:
  - Steganography
---
# Steganography
> Practice of concealing messages or information within other non-secret text or multi-media data

## Acrostics
An acrostic is a poem that has a 'hidden word'

> A boat, beneath a sunny sky
> Lingering onward dreamily
> In an evening of July -
> Children three that nestle near,
> Eager eye and willing ear,
> 
> This is an Acrostics that has the hidden word "Alice"


## The Process
![[Pasted image 20260905201830.png]]

# Steganography Least Significant Bits (LSB) Algorithm
> Hides a payload (message) inside a cover object (image) by replacing the **LSB** of **image pixel** bits with **payload bits**

- By modifying the **RIGHT** most bit of an image pixel we can insert our secret payload and it will also render the changes unnoticeable
- BUT if our payload is too large, the algo will start modifying the next right most bit and so on and an attacker may notice these changes.

## Constraints with LSB Algorithm
![[Pasted image 20260905202214.png]]

> [!NOTE]
> LSB only works on **lossless-compression** images, which means that the files that are stored in compressed format, but the compression does not result in the data being lost or modified, PNG, TIFF, BMP are lossless-compression formats
> - There are 2 main versions, **LSB Replacement** & **LSB Matching**

### LSB Replacement Example
![[Pasted image 20260905202540.png]]
- Most significant bit of payload substitute (Replace) LSB of cover image pixel
Example the letter 'G' (01000111), start from MSB '0' and replace the LSB of the original data
- On average, only **50%** of the cover image pixel LSB are changed

### LSB Matching Example
![[Pasted image 20260905202754.png]]
- Add +1 or -1 (**RANDOMLY**) if the LSB of the pixel value does not match the payload bits (From MSB)

# Bit Planes
Every RGB image is made up of 3 color channels or planes, and a greyscale image is made up of 1 color channel

## nth Bit Plane
> E.g. the 0th blue bit plane is all the LSBs of the blue bytes
> 0111010**1**

![[Pasted image 20260905203725.png]]

![[Pasted image 20260905203800.png]]


# Bit Plane Complexity Segmentation (BPCS) Algorithm
![[Pasted image 20260905204201.png]]

## BPCS Algorithm
- While there is more to hide
	- Get the next bit plane
	- While there is more space in the current bit plane
		- Get the next complex segment
		- Get the next block of payload
		- If the payload information is complex, then hide it in the current segment
		- Else conjugate by performing an exclusive or (XOR) operation then hide it in the current segment

### What is a Complex Segment
![[Pasted image 20260905204436.png]]
> Segments which are 'noisy' (complex) to hide payload
> If payload not noisy enough, perform 'conjugation' operation to make it complex
> Works because human eye cannot notice difference in 'rapidly changing bit patterns'


### What is considered complex ?
- Complexity measures how often neighbouring bits in a segment change value
- Assume there are 8 bytes in a segment:
	- Count number of times bits change value
	- Maximum value is 7, (10101010) or (01010101)
- Do the same for each of the bytes
	- Maximum number of change is 2 * 8 * 7= 112
	- The complexity of a segment $c = actual changes / 112$
	- Define a threshold value $T$ which is a parameter of the algorithm
	- If c > T then the segment is complex
	- T is typically ~0.3

# Steganalysis
![[Pasted image 20260905205452.png]]
- Steganalysis is an attack on steganography

> [!Objective]
> Primary Objective
> - Hidden payload Detection
> 
> Secondary Objective
> - Extract the payload

- Hiding info in digital media changes some media content
- May introduce visual degradation or unusual characteristics

## Visual Steganalysis
![[Pasted image 20260905205722.png]]

![[Pasted image 20260905205843.png]]

> The Stego image's histogram looks noisy unlike the smoother histogram of the original image











