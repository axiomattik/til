# The ch Unit

If you're anything like me, then the width of your paragraphs are defined using `rem` and you aim for widths that will fit roughly 45-75 characters per line. (By the way, when/how did this become the widely accepted (albeit clearly correct) standard?)

I recently learnt about the `ch` unit and got excited because for a niave moment I believed it would allow me to have greater control over how many characters each line has. However, it only took a little bit of thought to realise this was a little optimistic. `rem` and `em` are defined by the width of the current font's point size (traditionally \'em\' was defined as the width of a capital M, which is, pragmatically speaking, a very similar definition). `ch` on the other hand, is defined by the width of a single zero in the current font. 

When we're defining the width of text using some unit, the number of characters on a line is going to be affected the specific characters and their invidual widths. Which, for most fonts, will vary quite a bit. 

A paragraph of width 80ch probably won't have exactly 80 characters per line. So I'll stick to using `rem`.

However, `ch` does have a use case that I hadn't yet encountered before: numeric input boxes that have a specific number of characters, such as used for entering a year.

```
input[type="number"] {
	width: 4ch;
}

<input type="number" value="1984">
```

Our input box will have a width of exactly four zeroes, which for the vast majority of fonts, will be equal to a width of four numbers.
