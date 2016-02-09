---
title: string_segmenter
---
I just completed the 'string_segmenter' algorythm and it was extremely difficult.  I loved my original method, which would iterate each letter of the string into an array, and as soon as a verified word was in the array, it would be emptied into another array.  The first array would be emptied and the loop continued from where it stopped last.  If it came to a word it didnt couldnt verify, it would go to the last verified word, and attatch it to the front of the unknown word.  If that word was verified that loop would continue.  It worked, but not for every word.  I had to start all over on a new concept, I made a new sketch.  Basically what I did was iterate over the string in reverse.

while i < str.length
sample = str[front,back]
if valid_word?(sample)
words << sample

sample gets the characters from the end of the string to the beggining.  When it gets all the characters of a word that has been verified, its dumped into words (an empty array).  Its much simpler than my other attempt, and it works much better.