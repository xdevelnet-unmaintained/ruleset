##Xdevelnet developing ruleset

Some rules might be related to C programming language.


1. Use c99 standard, just to be able to declare variables where you want and assign values at declaration. But make possible to easily rewrite code to c89:

    * Do not use variable length arrays, use [m,c]alloc() instead;
    * Do not use bool types, you probably can avoid it. Also, bool is not bool for real;
    * Do not EVER use any gnu standart (gnu89, gnu99). Keep your code clean.

2. Take care about memory management:

    * Never use malloc() in critical applications. Returned non-null value (pointer TBH) from malloc() does not mean, that u can successfully use whole allocated memory;
    * When allocating array of pointers, use ``sizeof(void *)`` instead of ``sizeof(whatever_u_typed_at_ponter_type)``. Example:
    ```c
    int ***mem = malloc (sizeof(void *)*NUMBER_OF_ELEMENTS);
    ```
    * Do not save floating pointers (you can call it "seeking" or "offset" pointer) at array it is better to hold seek/offset. It will be useful when reallocated memory gives you new pointer with different address;
    * Do not forget to NOT seek pointers without taking notice about pointer type. If you want to seek with bytes, just typecast it.

3. Style:

    * Open curly bracket after round bracket (without line break):
    ```c
    void dummy () {
        //code
    }
    ```
    * Do not use curly brackets for a single line expression (do not forget to keep eval expression at same line):
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
    * Use tabs. Make possible to configure editors to show it as any number of spaces as other people want
    * If somewhere in code appears 3 or more round brackets in a row - separate outer brackets with spaces, make it easier to read&understand:
    ```c
    if( ptr = malloc(elements*sizeof(char)) ) {
        //
    }
    ```
    * Comment every single line if you are not sure you can understand it tomorrow quick enough.

4. Coding tips

    * Please, do not invent bicycles if you aren't sure it worth;
    * Do not write any kind of routines that could be already written and tested by thousands of people. You probably should use POSIX library. If you care about platform-independent code, you should know that this library is present almost anywhere, even in Windows! Of course, if you will not write code for PDP or other weird/unusual devices.
    * Describe every single user's function with comments (not body - but whole function). Live example:
    ```c
    //same as strcpy, but returns pointer to character AFTER null terminator instead of 1st arg
    char *strpcpy_a(char *s1, const char *s2) {
	      while ((*s1++ = *s2++) != 0) ;
	      return s1;
    }
    ```
    * Take care about multiplying dereferenced pointer. You might be confused with code like this:
    ```c
    variable**ptr;
    //or even
    variable***ptr_to_ptr;
    ```
      Of course, in real code you can't find names like "variable" and "ptr", so, it's usually not clear what "asterisk" operator is doing here.
    * Do not declare function inside another function. It's gcc feature and not a part of any standart (not even gnu89 or gnu99). Check your code with clang. If you wish to use global variables, move them from main() body to file.

