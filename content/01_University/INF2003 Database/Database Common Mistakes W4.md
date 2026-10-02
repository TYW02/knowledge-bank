
# BCNF

> [!question] BCNF
> Given R(A,B,C,D), F = { A → BC, C → D }. Which is correct?  
> A) R is in BCNF  
> B) A is not a key  
> C) C is a superkey  
> D) R violates BCNF
> 
> [[BCNF#Application|Answer]]

> [!question] Given `R(A, B, C, D)`, F = {AB -> CD, C -> A}. Is `C -> A` a BCNF violation ?
> A) Yes, because C⁺ = {C,A} does not cover all attributes, so C is not a superkey  
> B) No, because C → A is trivial  
> C) Yes, because AB is already a key so no other FD matters  
> D) No, because C⁺ = {A,B,C,D}
> > [!Answer]-
> > To see if `C -> A` we need to compute $C^{+}$.
> > - $C^{+}$ = {C, A} but we **cannot add** AB into the set because that **requires BOTH A and B present**. Hence to further change and **C is NOT a superkey**




































