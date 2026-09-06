---
title: Lab 01
tags:
  - Caesar
  - Base64
---
## Break the following code:
```
UGRhIGx3b29za256IGJrbiBwZGEgeWR3aGhhamNhIGx3Y2EgZW86IHludWxwaw==
```

> [!Solution]-
> Usually if you see == at the end that indicates that it was encoded using Base64
> ```
> Pda lwoosknz bkn pda ydwhhajca lwca eo: ynulpk
> This looks like the message has its alphabet shifted
> ```
> So we perform a reverse caesar cipher to find the plaintext (Key = 3)
> ```
> The password for the challenge page is: crypto
> ```
> 


## The following is using Columnar Transposition Cipher
```
PRRO IEACLCHSEO
```
Key is 'KEY'
> [!Solution]-
> Original
> 
> | Y | E | K |
> |--|--|--|
> |P | I | C | 
> | R | E | H |
> | R | A | S |
> | O | C | E |
> | - | L | O |
> 
> Decryption
> 
> | K | E | Y |
> |--|--|--|
> |C | I | P | 
> | H | E | R |
> | S | A | R |
> | E | C | O |
> | O | L | - |
> 
> ```
> CIPHERS ARE COOL
> ```


## Morse Code
```
- .... . .--. .- ... ... .-- --- .-. -.. ..-. --- .-. - .... .. ... .-.. . ...- . .-.. .. ... .-- . .-.. .-.. -.. --- -. .
```

> [!Solution]-
> Errm just use an online decoder.


## XOR
First Input
```
10010011001010011001010010000110101001010001010110100111010  
10101010101101001010101100011110011010011101011010010101011  
0100101000101011101101011101011010
```

Second Input
```
11100111010000011111000110100110110101010111010011010100001  
00110001000011111101000010001101010010001101010111011110111  
1000001000110011001011111000110100
```

> [!Solution]-
> Converted XOR
> 
> ```
> 1110100011010000110010100100000011100000110000101110011011100110  
1110111011011110111001001100100001000000110100101110011001000000  
11000100110100101101110
> ```
> 
> Use a Binary to Hexadecimal Converter
> ```
> 7468652070617373776F72642069732062696E
> ```
> 
> Use a Hexadecimal to ASCII Converter
> ```
> the password is bin
> ```


## Delimiter, decimal 
```
8490910490910190911290997909115  
909115909119909111909114909100  
9091059091159091009091019099990999  
909111909110909118909101909114909116
```

> [!Solution]-
> Here we can see that the string '909' is repeated that could mean that it is a delimiter. So if we replace it we are left with
> 
> ```
> 84 104 101 112 97 115  
115 119 111 114 100  
105 115 100 101 99 99  
111 110 118 101 114 116
> ```
> 
> Then we convert from Decimal to ASCII
> ```
> Thepasswordisdecconvert
> ```


## ASCII Shifting & LeetSpeek
```
8i4 q5tt/>/>1se g1s 8i4 di5mm4oa4 t284 2t; 4mju4
```

> [!Solution]-
> We shift each character 1 down on the ASCII table
> ```
> 7h3 p4ss .=.= 0rd f0r 7he ch4ll3n@3 s173 1s: 3lit3
> ```
> 
> Here the ciphertext looks a little more like sentences now. We use a LeetSpeek converted to make it more readable
> ```
> the passw ord for the challenge site is: elite
> ```

## Frequency Analysis
```
GFS WMY OG LGDVS MF SFNKYHOSU ESLLMRS, PC WS BFGW POL DMFRQMRS, PL OG CPFU M  
UPCCSKSFO HDMPFOSXO GC OIS LMES DMFRQMRS DGFR SFGQRI OG CPDD GFS LISSO GK LG,  
MFU OISF WS NGQFO OIS GNNQKKSFNSL GC SMNI DSOOSK. WS NMDD OIS EGLO CKSJQSFODY  
GNNQKKPFR DSOOSK OIS 'CPKLO', OIS FSXO EGLO GNNQKKPFR DSOOSK OIS 'LSNGFU' OIS  
CGDDGWPFR EGLO GNNQKKPFR DSOOSK OIS 'OIPKU', MFU LG GF, QFOPD WS MNNGQFO CGK  
MDD OIS UPCCSKSFO DSOOSKL PF OIS HDMPFOSXO LMEHDS. OISF WS DGGB MO OIS NPHISK  
OSXO WS WMFO OG LGDVS MFU WS MDLG NDMLLPCY POL LYEAGDL. WS CPFU OIS EGLO  
GNNQKKPFR LYEAGD MFU NIMFRS PO OG OIS CGKE GC OIS 'CPKLO' DSOOSK GC OIS  
HDMPFOSXO LMEHDS, OIS FSXO EGLO NGEEGF LYEAGD PL NIMFRSU OG OIS CGKE GC OIS  
'LSNGFU' DSOOSK, MFU OIS CGDDGWPFR EGLO NGEEGF LYEAGD PL NIMFRSU OG OIS CGKE GC  
OIS 'OIPKU' DSOOSK, MFU LG GF, QFOPD WS MNNGQFO CGK MDD LYEAGDL GC OIS  
NKYHOGRKME WS WMFO OG LGDVS
```

> [!Solution]-
> Here we use a tool to get count which letter has the highest frequency. Here we see that 'S' and 'O' are the most used so we replace those letters with 'E' & 'T'
> ```
> GFe WMY tG LGDVe MF eFNKYHteU EeLLMRe, PC We BFGW PtL DMFRQMRe, PL tG CPFU M  
UPCCeKeFt HDMPFteXt GC tIe LMEe DMFRQMRe DGFR eFGQRI tG CPDD GFe LIeet GK LG, MFU  
tIeF We NGQFt tIe GNNQKKeFNeL GC eMNI DetteK. We NMDD tIe EGLt CKeJQeFtDY  
GNNQKKPFR DetteK tIe 'CPKLt', tIe FeXt EGLt GNNQKKPFR DetteK tIe 'LeNGFU' tIe  
CGDDGWPFR EGLt GNNQKKPFR DetteK tIe 'tIPKU', MFU LG GF, QFtPD We MNNGQFt CGK MDD  
tIe UPCCeKeFt DetteKL PF tIe HDMPFteXt LMEHDe. tIeF We DGGB Mt tIe NPHIeK teXt We  
WMFt tG LGDVe MFU We MDLG NDMLLPCY PtL LYEAGDL. We CPFU tIe EGLt GNNQKKPFR  
LYEAGD MFU NIMFRe Pt tG tIe CGKE GC tIe 'CPKLt' DetteK GC tIe HDMPFteXt LMEHDe, tIe FeXt  
EGLt NGEEGF LYEAGD PL NIMFReU tG tIe CGKE GC tIe 'LeNGFU' DetteK, MFU tIe CGDDGWPFR 
EGLt NGEEGF LYEAGD PL NIMFReU tG tIe CGKE GC tIe 'tIPKU' DetteK, MFU LG GF, QFtPD We  
MNNGQFt CGK MDD LYEAGDL GC tIe NKYHtGRKME We WMFt tG LGDVe.
> ```
> 
> Here we notice that the word 'tle' is appearing frequently in the passage. Which is most likely 'the' so we replace 'l' with 'h'
> We also see that the next most common letter is 'G' which is either (a, o, i) but we also see words like 'tG' so 'G' has to be 'o'
> ```
> oFe WMY to LoDVe MF eFNKYHteU EeLLMRe, PC We BFoW PtL DMFRQMRe, PL to CPFU M  
UPCCeKeFt HDMPFteXt oC the LMEe DMFRQMRe DoFR eFoQRh to CPDD oFe Lheet oK Lo, MFU  
theF We NoQFt the oNNQKKeFNeL oC eMNh DetteK. We NMDD the EoLt CKeJQeFtDY  
oNNQKKPFR DetteK the 'CPKLt', the FeXt EoLt oNNQKKPFR DetteK the 'LeNoFU' the  
CoDDoWPFR EoLt oNNQKKPFR DetteK the 'thPKU', MFU Lo oF, QFtPD We MNNoQFt CoK MDD  
the UPCCeKeFt DetteKL PF the HDMPFteXt LMEHDe. theF We DooB Mt the NPHheK teXt We  
WMFt to LoDVe MFU We MDLo NDMLLPCY PtL LYEAoDL. We CPFU the EoLt oNNQKKPFR LYEAoD  
MFU NhMFRe Pt to the CoKE oC the 'CPKLt' DetteK oC the HDMPFteXt LMEHDe, the FeXt EoLt  
NoEEoF LYEAoD PL NhMFReU to the CoKE oC the 'LeNoFU' DetteK, MFU the CoDDoWPFR EoLt  
NoEEoF LYEAoD PL NhMFReU to the CoKE oC the 'thPKU' DetteK, MFU Lo oF, QFtPD We  
MNNoQFt CoK MDD LYEAoDL oC the NKYHtoRKME We WMFt to LoDVe.
> ```
> l
> Looking at the first word 'oFe' we can see that and 'theF' and conclude that 'F' = 'n'
> And 'Lheet' can be converted to 'Sheet'
> ```
> one WMY to soDVe Mn enNKYHteU EessMRe, PC We BnoW Pts DMnRQMRe, Ps to CPnU M  
UPCCeKent HDMPnteXt oC the sMEe DMnRQMRe DonR enoQRh to CPDD one sheet oK so, MnU  
then We NoQnt the oNNQKKenNes oC eMNh DetteK. We NMDD the Eost CKeJQentDY  
oNNQKKPnR DetteK the 'CPKst', the neXt Eost oNNQKKPnR DetteK the 'seNonU' the  
CoDDoWPnR Eost oNNQKKPnR DetteK the 'thPKU', MnU so on, QntPD We MNNoQnt CoK MDD  
the UPCCeKent DetteKs Pn the HDMPnteXt sMEHDe. then We DooB Mt the NPHheK teXt We  
WMnt to soDVe MnU We MDso NDMssPCY Pts sYEAoDs. We CPnU the Eost oNNQKKPnR  
sYEAoD MnU NhMnRe Pt to the CoKE oC the 'CPKst' DetteK oC the HDMPnteXt sMEHDe, the  
neXt Eost NoEEon sYEAoD Ps NhMnReU to the CoKE oC the 'seNonU' DetteK, MnU the  
CoDDoWPnR Eost NoEEon sYEAoD Ps NhMnReU to the CoKE oC the 'thPKU' DetteK, MnU so on,  
QntPD We MNNoQnt CoK MDD sYEAoDs oC the NKYHtoRKME We WMnt to soDVe.
> ```
> 
> Basically slowly replace the letters with reasonably good guesses
> 
> Final Message
> ```
> one way to solve an encrypted message, if we know its language, is to find a different plaintext  
of the same language long enough to fill one sheet or so, and then we count the occurrences of  
each letter. we call the most frequently occurring letter the 'first', the next most occurring letter  
the 'second' the following most occurring letter the 'third', and so on, until we account for all  
the different letters in the plaintext sample. then we look at the cipher text we want to solve  
and we also classify its symbols. we find the most occurring symbol and change it to the form  
of the 'first' letter of the plaintext sample, the next most common symbol is changed to the  
form of the 'second' letter, and the following most common symbol is changed to the form of  
the 'third' letter, and so on, until we account for all symbols of the cryptogram we want to solve.
> ```













