Tags: [[Lecture 4 - Libraries]]
Linked Programs: [[sayings.py]]

# Cowsay
```python
import cowsay
import sys


if len(sys.argv) == 2:
	cowsay.cow("hello, " + sys.argv[1])


$ python say.py David
> Output: 
  ____________
| hello, David |
  ============
            \
             \
               ^__^
               (oo)\_______
               (__)\       )\/\
                   ||----w |
                   ||     ||


----------------------------------------------------------------------------------------

import cowsay
import sys


if len(sys.argv) == 2:
	cowsay.cow("hello, " + sys.argv[1])


$ python say.py David
> Output: 
  ____________                                                                                                                      
| hello, David |
  ============
                   \
                    \
                     \
                      \
                         .-=-==--==--.
                   ..-=="  ,'o`)      `.
                 ,'         `"'         \
                :  (                     `.__...._
                |                  )    /         `-=-.
                :       ,vv.-._   /    /               `---==-._
                 \/\/\/VV ^ d88`;'    /                         `.
                     ``  ^/d88P!'    /             ,              `._
                        ^/    !'   ,.      ,      /                  "-,,__,,--'""""-.
                       ^/    !'  ,'  \ . .(      (         _           )  ) ) ) ))_,-.\
                      ^(__ ,!',"'   ;:+.:%:a.     \:.. . ,'          )  )  ) ) ,"'    '
                      ',,,'','     /o:::":%:%a.    \:.:.:         .    )  ) _,'
                       """'       ;':::'' `+%%%a._  \%:%|         ;.). _,-""
                              ,-='_.-'      ``:%::)  )%:|        /:._,"
                             (/(/"           ," ,'_,'%%%:       (_,'
                                            (  (//(`.___;        \
                                             \     \    `         `
                                              `.    `.   `.        :
                                                \. . .\    : . . . :
                                                 \. . .:    `.. . .:
                                                  `..:.:\     \:...\
                                                   ;:.:.;      ::...:
                                                   ):%::       :::::;
                                               __,::%:(        :::::
                                            ,;:%%%%%%%:        ;:%::
                                              ;,--""-.`\  ,=--':%:%:\
                                             /"       "| /-".:%%%%%%%\
                                                             ;,-"'`)%%)
                                                            /"      "|



```




# Custom library
Import : [[sayings.py]]
```python
import sys
from sayings import hello

if len(sys.argv) == 2:
	hello(sys.argv[1])


```

