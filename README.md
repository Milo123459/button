# button
Compression format different to zip producing smaller files

## How

It looks through the files and finds phrases that are used a lot. It then defines them into metadata at the top of the file, and the best part is: it is utf-8.

### Example

Take this snippet of text:

```
Hello world, this is a test, test, test!
Hello world, this is a test, test, another test!
```

We see `Hello world,` is used twice, `this is a test` twice and `test, test!` once. Button sees it like this:

That first line is a phrase, lets test the file for any usage of that same phrase.

On the second line, beacuse the phrase is splitted by space (but is also tested without) it then identifies that the second line starts some-what the same. It'd then define a phrase (In this case, it'd be called `001A` (length can vary, depending on how large the file is)). The result would then be:
```button
METADATA
PHRASES
001A Hello world, this, is a test, test,
CONTENT
001A test!
001A another test!
```

If (for some reason) `001A` was used in the file it would keep testing until it found something that wasn't being used.
