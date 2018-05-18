# banned
Banned.h - deprecated C runtime functions

I wrote this header many, MANY moons ago while working on the early versions of the Security Development Lifecycle (www.microsoft.com/sdl) at Microsoft. 

I have always been a big fan of making tasks as simple as possible and I figured creating a header that deprecated (VC++) or poisoned (gcc) known insecure C runtime functions is very low tech and works well! We made using banned.h a requirement for all unmanaged C and C++ code across the company. 

Over the years we split the list of banned functions into two groups: those that are banned and those you should consider not using in your code.

If you add the following before referencing banned.h:

#define _SDL_BANNED_RECOMMENDED

Then the more agressive list of banned functions are also deprecated/poisoned. 

If you use strsafe.h in the code prior to referencing banned.h; the header will deprecate a smaller list of functions because the 'rogues gallery' is already deprecated by strsafe.h. More info at https://msdn.microsoft.com/en-us/library/windows/desktop/ms647466(v=vs.85).aspx

Finally, by default, banned.h will add these two:

#define _CRT_SECURE_CPP_OVERLOAD_STANDARD_NAMES			(1)
#define _CRT_SECURE_CPP_OVERLOAD_STANDARD_NAMES_MEMORY	(1)

Which auto-migrates certain functions to safer functions if the destination buffer size is known at compile time. More info at https://docs.microsoft.com/en-us/cpp/c-runtime-library/secure-template-overloads
