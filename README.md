##Just a few rules that should be followed while programming and working with Xdevelnet
Some rules are related to C programming language.


1. Use c99 standart, just to make possible declare variables where u want and assign values at declaration. But make possible to easily rewrite code to c89:

    * Do not use variable lenght arrays, use [m,c]alloc() instead;
    * Do not use bool types (you probably can avoid it, bool is not bool 4 real);
    * Do not EVER use any gnu standart (gnu89, gnu99). Keep your code clear.

2. Take care about memory management:

    * Never use malloc() in critical applications. Returned non-null value (pointer TBH) from malloc() does not mean, that u can succesfully use whole allocated memory;
    * When allocing array of pointers, use ``sizeof(void *)`` instead of ``sizeof(whatever_u_typed_at_ponter_type)``. Example:
    ```c
    int ***mem = malloc (sizeof(void *)*NUMBER_OF_ELEMENTS);
    ```
    * Do not save floating pointers (or seeking/offset pointer) at array - better to hold seek/offset. It will be userful when reallocated memory gives u new pointer with different address;
    * Don't forget to NOT seek pointers without taking notice about pointer type. If u wanna seek with bytes, just typecast.

3. Style:

    * Open curly bracket after round bracket (without line break):
    ```c
    void dummy () {
        //code
    }
    ```
    * Do not use curly brackets when only 1 expression present:
    ```c
    while (i_am_playing_games()) nobody_should_not_distrub_me();
    ```
    * Close and open curly brackets with ``else`` keyword at one line:
    ```c
    if (what_a_lovely_morning()) {
        stop_sleeping();
        walk_with_dog();
    } else {
        stay_at_your_bed();
        and_drik_coffee();
    }
    ```
    * Use tabs. Make possible to configure editors to showing it as any number of spaces as other people want
    * Separate multiple numbers of round brackets with spaces if it's difficult to read:
    ```c
    if( ptr = malloc(elements*sizeof(char) ) ) {
        //
    }
    ```
      You can decide where to put space (or where not) freely.
    * Comment every single line if you are not sure you can understand it tomorrow quick enough.

4. Coding tips

    * Please, do not invent bicycles if you aren't sure if it worth;
    * Do not write any kind of routines which is already written&rewritten&tested by thousands people. You probably should use POSIX library. If you're care about platform-independent code - this library present almost anywhere, even in Windows! Of course, if you will not write code for PDP or other weird machines.
    * Describe every single user's function with comments (not body - but whole function). Live example:
    ```c
    //same as strcpy, but returns pointer to character AFTER null terminator instead of 1st arg
    char *strpcpy_a(char *s1, const char *s2) {
	      while ((*s1++ = *s2++) != 0) ;
	      return s1;
    }
    ```
    * Take care about multiplying with dereferencing pointer. You might be confused with code like this:
    ```c
    variable**ptr;
    //or even
    variable***ptr_to_ptr;
    ```
      Of course, in real code you can't find names like "variable" and "ptr", so, it's usually not clear what "asterisk" operator is doing here.
    * Do not declare function inside another function. It's gcc feature, not any kind of standart (not even gnu89 or gnu99). Check your code with clang. If you wish to use global variables, move them from main() body to file.

