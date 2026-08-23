<img width="30%" src="https://github.com/user-attachments/assets/910718ff-ca00-4ff4-9bb7-377dac134882" />

**Make emojis blink**

[Try it](https://bacionejs.github.io/blink)

**TL;DR**: It's a nice algorithm, generalized to work with many faces, but you could simplify it a lot for your specific case.  

The code renders an emoji onto a 200×200 canvas, reads its pixels, then uses a **flood-fill algorithm** to find dark connected regions and **heuristics for shape, density, size, and position** to identify two regions that are likely to be the eyes. It saves the original eye pixels and samples the surrounding colors, then every two seconds replaces the eye pixels with those surrounding colors for 150 ms, making the eyes appear to close before restoring them. It is essentially a tiny bit of **computer vision** that automatically finds and animates the emoji's eyes without knowing the emoji's geometry beforehand.

A lot of that is probably **overkill**. The flood-fill machinery, visited-pixel array, connected-component bounding boxes, density and aspect-ratio tests, and the fairly elaborate search for a plausible pair of eyes are all there to make the technique work without knowing the emoji's geometry, but if the emoji and font are fixed, much of that generality isn't necessary. You could likely simplify it to finding the relevant dark pixels with a much cheaper scan, hard-code or infer a small eye region, and avoid storing every eye pixel individually. Even the surrounding-color sampling could probably be reduced to a single representative color or a known background color.  
