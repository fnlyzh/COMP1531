Admin
-
Attend every tutorial; if not, my group project mark gets scaled down  
  
My group (W13B_DREAM):
- Jonathan Shih
- Nahiyan Kader
- Aliemul Islam
- Tharun Khokulan

Javascript - Misc:
-
- I don't need ; in JS
- no main function ; run from top to bottom
- const for everything unless you know you want to change it
- no type in function params; name suffices
- back ticks ` replace " to create string literal
- triple `===` should be used instead of `==` for exact equal
  - if we used `==`, then `"2" == 2` would be true
  - whereas `"2" === 2` would be false

Javascript - Objects:
- 
- I can delete objects or a property of an object using `delete`

Javascript - Loops:
- 
- I must not use C-style loops (this will reduce my style marks)
- Try to use For-in and For-of loops
- for the For loops, use `const` i instead of `let` i; i is updated each loop so const would work!

Javascript - Arrays - Copying:
-
assume that `userData` is an array of objects containing user data  

Shallow-copy:
- is like a pointer to the array
- if you modify the original or the shallow copy, both change
- `let shallowCopy = [ ... userData];`

Deep-copy:
- is an actual separate copy of the array
- modifying either would have no effect on the other
- `let deepCopy = structuredClone(userData);`
- note: `structuredClone` was introduced in a later version of JS, so it might not be accessible to some

Other
-
- there are lambda functions, which are defined and only exist in the line it's defined!
