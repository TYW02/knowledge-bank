---
title: W3 Access Control
---
![[CS W3.svg]]

# Access Control
> **Authenticate** and **Authorize** individuals to access the information they are **allowed to see** and use

## Authentication
- Prove you are who you claim to be
- Using distinguishing characteristic (Identification)

### Authentication Categories
1. Knowledge: Something you **know** (Password, Passphrase)
2. Token/Device: Something you **have** (ID card, Access card, Mobile phone)
3. Biometrics: Something you **are** (Fingerprint, Iris)


## Knowledge - Password

### Best Practices
- Mix **upper** & **lower** case with numbers/special characters and at least X characters long
- Use special characters 
- Don't use common words
- Don't use "tricks" like [[Password Walking]]
- Change it every 90 days, no reuse
- Use of 2FA
- Use of secured password managers

## Password Managers 
- Support use of unique strong password
- Help prevent password re-use attack
- Easier to **STEAL ALL** your password (Single point of failure)
- Runs in memory (Master password can be leaked)
- Other attacks (Keyloggers, Trojans)

> [!Note]
> Ultimately, strong password helps.
> Formulating a Good Password is as important as storing it securely


## Password Cracking
- **Password Space** is the number of possible **combinations** of characters given the **length** of password and the **character set** used.

> [!Note]
> Theoretical, because people don't choose randomly from entire password space

### Cain and Abel
- Password recovery tool
- Uses many possible attacks to get the password of a system
- Exclusive to Windows, cannot be ran on Linux and OSX
- Used by attackers who wish to gain unauthorized access to a system
- Can be used by defender when an attacker locks them out of their system or to test the strengths of their defenses.

# Brute Force
- Try all possible combination of letters, characters (Not efficient unless sufficient computing power)
- **Reverse Brute Force** (Attacker tries 1 password against multiple usernames)
- **Account lock out** is 1 way to prevent brute-force

# Dictionary
- Dictionary containing commonly used **password and variations**
- Potentially quite slow (Unless obvious password is used)
- Given a list of **hashes**, **hash the dictionary password** and see if you get any **matches** with the list of hashes you have, then you know the plaintext
![[Pasted image 20260913095104.png]]

# Social Engineering
- If you know a user, you can guess their password based on their preferences
- If you don't know them you could still try variations on select keywords in their social media

# Passphrases and other good coping techniques

## Password Managers
- Store login information for all website to log you in automatically
- Encrypt your password DB with master password
- Master password is the only one you have to remember

> Pick memorable, long passphrases of unrelated words.

- Take nth letter or number equivalent of each word in your passphrase as your password
> **i** **l**ove **t**o **w**atch **p**hysical **100** **o**n **n**etflix **e**very **friday**, **saturday** **a**nd **sunday**
- Password: iltwp100one56a7

![[Pasted image 20260913095600.png]]

## Secure Storing of Passwords
- SALT: A random string of characters added to a password before hashing it
- Hashes of salted password also become **randomized**
- **CANNOT** precompute lookup tables because salt not known in advance


## Hash Table
Lookup table attack / Rainbow table attack

- Hash, password pairs are stored
- You can then search for a hash, and establish the corresponding password


# As a System Administrator
- Enforce password change and password formulation policy (Password guessing attacks)
- Implement additional layer of authentication (2FA)
- Store password securely (Database compromise)
- Salt and hash password, hash sensitive data >= 2x
- Educate users on security best practices and awareness (Social Engineering)
- Maintain correct access rights to web-based accounts (Google dorking & Dictionary traversal)
- Monitor authentication logs (Support account forensics)

![[Pasted image 20260913100056.png]]



# Recognition-based Graphical Password
![[Pasted image 20260913100158.png]]

![[Pasted image 20260913100216.png]]


# Recall-based Graphical Password
![[Pasted image 20260913100247.png]]


# Hybrid Approach
![[Pasted image 20260913100324.png]]



# Tokens
- Digital authentication
	- Physical device to aid authentication
	- Requires user to insert device or use it to generate a code to authenticate
	- Commonly used as part of 2FA in financial transactions

### Common Examples
- eToken
- Smart Cards
- RFID Tags

## eTokens Capabilities
- Can be implemented on USB key or smart card
- Data physically protected on device. May store credential
- Successful client-side authentication with password invokes token to retrieve stored key or generate passcode, which is sent to server-side for authentication
- Can offer on-board 2FA and digital signing, used in addition to or in place of password

### Application
- Aladdin eToken (Crypto device)
- Gain access to secured premise (Electronic Key)
- Account access (Bank provides tokens)
- Blockchain Transactions

## Smart Cards
- Size of a credit card
- Embedded microprocessor 
- Chip OS support multiple application and secure independent data storage on 1 single card
	- JavaCard: Allows applets to be loaded and securely executed
	- MULTOS: Allows you to dynamically load, update or delete any application
- **Store** information (PIN Code)
- Provide better privacy for **biometrics** storage
- Protect information (Encryption)
- Securely communicate with digital endpoint via card reader
- Built-in tamper resistance

## RFID Tags
- Integrated Circuit with antenna that can respond to RF signal with identity information
- Power supply optional (IC uses RF signal to power itself)
- Susceptible to OTA spoof attacks and theft
- Example of attacks:
	- Side Channel Attacks [[Cryptanalysis Techniques#Side Channel Analysis|Note]] (Power Analysis)
	- MITM or Sniffing

### Capabilities
- Proximity (Short-range) and vicinity (Long-range)
- **Active** RFID tag system, battery powered, continuously broadcasting tags
- **Passive** RFID tag system, powered by RF energy transmitted from RFID reader
- Ability to read affected by nearby media (Metal, textiles)
- About 2KB of storage

### Application
- Logistics: Supply chain track and trace apps, product authentication
- Healthcare Facilities: Tracking and location of patients
- Prison facilities: Tracking and location of inmates


# Biometrics
- Physiological or behavioural (Feature set extracted and compared to template in DB)
- Can be used for Identification and Authentication
- Operation (Enrollment and Verification Modes)
![[Pasted image 20260913102340.png]]

# Essential Requirements of Characteristic as a Security Biometric
- **Universality**: Each person should have the characteristic
- **Distinctiveness**: Any 2 person should be sufficiently different in terms of the characteristics
- **Permanence**: The characteristic should be sufficiently invariant (With respect to the matching criterion) over a period of time
- **Collectability**: The characteristic can be measured quantitatively

## Acceptability
- Authentication needs to be **acceptable to end user**, if it's inconvenient they won't use it
- If it takes too long or inconvenient to enrol, they **may not use it**
- If they see it as an **invasion of privacy**, they won't use it 
- Certain biometrics may have **stigma** associated with them (Fingerprint and criminality) which can negatively impact user perception in certain cultures


## Accuracy
- False Accept Rate (FAR): Likelihood of false acceptance, lets you in when it shouldn't
- True Accept Rate (TAR): Likelihood of true acceptance, lets you in when it should
- Receiver Operating Characteristic (ROC): Shows tradeoff between TAR & FAR

> Accuracy of biometric system is quantified most typically by a ROC plot indicating FAR and TAR
> - Well-performing system is characterized by high TAR and low FAR rates
> - Higher TAR on real-world system however corresponds to an increase in FAR


## Iris Scanning

- Iris is very complex colour and pattern wise (256 unique characteristics), Iris pattern of 2 people are very different, even genetically identical twins
- **More accurate than fingerprint** and less than retinal scanning. FAR is around 1 in 10 million
- Enrollment comprises photos taken in **natural** and **infrared light**, takes a few seconds to enrol and < 5s to verify, **Less invasive** than retinal scanning, only requires snapshot of eye
- Unlike retina, iris **does not change** with diseases such as glaucoma
- **More costly** than fingerprint scanner ($200-2000) but reducing for smart phones (Higher end systems used by Immigration, Police)

## Retinal Scanning
- **Complex capillary structure** ensures each person's retina is unique, up to 400 **unique** characteristics (VS iris's 256)
- **Very high accuracy** in normal circumstances; About **70 times more accurate than iris** scans and **20,000 times more accurate** than fingerprinting
- More **invasive** than iris scanning, requires subject to **focus on a single point** for 15 seconds.
- Enrollment is **lengthy** due to requirement of multiple image capture, which can cause **user discomfort**
- Verification comparisons take > 10s
- **Patterns can change** with some diseases 
- Scanners are **very expensive**, bulky and challenging to operate.

## Fingerprint Scanning
- Fingerprints are nearly unique **1 in 64 billion chance of match**
	- Features include characteristics of ridges, arches, delta and whorls
- Fairly **easy**, **repetitive**, **non-invasive** enrolment < 1 minute, contactless verification within 1s, contact verification about 5 to 10s
- Fingerprints **do not change over time** but can be affected by dryness and injuries
- Fingerprint produce around **1 in 100,000 false positives** for smart phones
- Fingerprint scanners are relatively cheap: $30 to < $1000

## Facial Recognition
- Every face has geometric landmarks to make up facial feature
	- Distance between eyes, width of nose, length of jawline
- Less intrusive than iris/retinal, fast enrolment and verification
- Physical characteristics change over time
	- May be affected by wearables, unsuitable for pandemic tracking and tracing
- Possible above 90% accuracy (Needs machine learning support)
	- FAR around 1 in 1,000,000 (Normal conditions)
	- Less than iris better than fingerprint
- More expensive than fingerprint scanner ($90 to $1500) but cost reducing for smartphone


## Hacking Biometrics
> Facial recognition and fingerprinting are vulnerable to spoofing attacks that undermine authentication

- Facial recognition algorithms showed false positive rates for Asian and black that were as much as 100 times higher than for whites
- Fingerprint recognition is often used in mobile solutions to provide convenient authentication. 
- Spoofing risk poses a threat to apps like mobile payment


## Behavioural Biometrics
- Things you do in a specific way (How you hold yourself/walk)
- Sufficiently discriminatory to allow verification in some low-security application (AI, achieves accuracy of 99.3%)
- Can change over time
- Keystroke Dynamic: Hold time, Pause between keys
- Implementation Cost: Gait significantly more than keystroke dynamics

## Voice Recognition
- Voice has physical and behavioural parts
- **Physical** (Mouth, Nose, Tongue affect sound produced)
- **Behavioural** (Emotional state, cold)
- **Not universal** (Speech impaired) and not very distinctive
- Text-dependent (Specific passphrase) or text-independent (Registration/enrolment)
- Enrolment involves the capture of voice samples and it typically slow
- Cost similar to fingerprint scanner

## Authentication Wrap-up
> Factors to consider when deciding on and implementing an authentication mechanism

- **Ease of use** for users (Remember acceptability, ease of enrolment, intrusiveness) 
- What **accuracy level** is needed ? (Higher -> more accurate, more false alarm)
- **Cost** - Budget allocated
- **Ease of administration / maintenance** for administrator


# Authorization

> Already authenticated (Proved you are who you claim to be), but are you authorised to **carry out a particular action** ?

Authorisation: **What** you are allowed to do (Access)

> Subject -> Access Request -> Reference Monitor -> Object

## 3 main types of access control system
- Discretionary Access Control (DAC)
- Role Based Access Control (RBAC)
- Mandatory Access Control (MAC)

- Ensures that **authenticated** subject can only access objects using **secure** and **pre-approved** methods


## Discretionary Access Control
> Assigns access rights based on rules specified by users (Owners)

- Subjects can determine who has access to their objects.
- The DAC model uses access control list (ACL) and capability tables.
- OS checks the table to determine the type of access allowed.
- **Owner** (User) created the object 
- **Group** is a defined group of specific users
- **Other** (World) is anyone else

## Role-Based Access Control
> Also known as **Non-discretionary Access Control**

- System admin assign rights based on organizational roles instead of individual user accounts within an organization.
- Allows organization to address the **principle of least privilege**. This gives an individual only the access needed to do their job, since access is connected to their job

![[Pasted image 20260913152723.png]]


## Mandatory Access Control
> Access to resource objects is controlled by OS based on system administrator-configured settings.

- MAX uses "Security labels" to assign resource objects.
	- Security labels have Classification (Top secret, Confidential, Unclassified)
	- Category / Clearance levels (Specific department provides "Need to know")
	- Each user account is also assigned classification and category properties 

- User access is **granted** if **both** properties match. 
- MAC is the most secure access control but requires a considerable amount of planning and system management due to constant updating of objects and account labels.

# Principle of Least Privilege
> Security best practice that requires limiting privileges to the minimum necessary to perform the job or task.

- IT admin reference this principle when assigning **access rights for user accounts**, admin rights and configuring computer **security setting**
- Reduces risk of un-authorized access to critical system or sensitive data by **compromising a low-level user account**, device, or application

## POLP on Mobile
> Mobile applications increasingly want access to various function on mobile device.
> - Flashlight application
> 	- DO NOT require access to phone information 


A mobile app may be considered **intrusive or malicious** due to the **permissions** it requests when it is installed, and the activities it then carries out.

## Separation of Duties
> Control mechanism in organizations that **divides tasks** and **responsibilities** for a process among **multiple people** 

- Prevents any **single** individual from having complete control over it, thus **reducing the risk** of fraud, errors, and security breaches.
- For example, the person authorizing a paycheck **should not** also be the one who can prepare them.


















