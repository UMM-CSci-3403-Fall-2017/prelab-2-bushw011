# Leak report

A bunch of space had been allocated to make a string of "saved" characters, along with a slot for the null terminator. This was inside of the 'strip' function, which returned this string. 'strip' would then be called and stored in variable 'cleaned' inside the function 'is_clean'. The space from this string would be used and then never freed up again. 

It was actually pretty convenient that the string from 'strip' was already stored inside of a variable in 'is_clean'. That allowed me access to the pointer which memory was initially allocated for. I then freed the 'cleaned' variable right after the last time it was used in the program. This effectively fixed the memory leak problem.

