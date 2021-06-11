## Fontbakery report

Fontbakery version: 0.7.37

<details>
<summary><b>[1] Family checks</b></summary>
<details>
<summary>⚠ <b>WARN:</b> Is the command `ftxvalidator` (Apple Font Tool Suite) available?</summary>

* [com.google.fonts/check/ftxvalidator_is_available](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/universal.html#com.google.fonts/check/ftxvalidator_is_available)
<pre>--- Rationale ---
There&#x27;s no reasonable (and legal) way to run the command `ftxvalidator` of the
Apple Font Tool Suite on a non-macOS machine. I.e. on GNU+Linux or Windows etc.
If Font Bakery is not running on an OSX machine, the machine running Font Bakery
could access `ftxvalidator` on OSX, e.g. via ssh or a remote procedure call
(rpc).
There&#x27;s an ssh example implementation at:
https://github.com/googlefonts/fontbakery/blob/main/prebuilt/workarounds
/ftxvalidator/ssh-implementation/ftxvalidator</pre>

* ⚠ **WARN** Could not find ftxvalidator. [code: ftxvalidator-available]

</details>
<br>
</details>
<details>
<summary><b>[10] ZenKurenaido-Regular.ttf</b></summary>
<details>
<summary>🔥 <b>FAIL:</b> Font enables smart dropout control in "prep" table instructions?</summary>

* [com.google.fonts/check/smart_dropout](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/smart_dropout)
<pre>--- Rationale ---
This setup is meant to ensure consistent rendering quality for fonts across all
devices (with different rendering/hinting capabilities).
Below is the snippet of instructions we expect to see in the fonts:
B8 01 FF    PUSHW 0x01FF
85          SCANCTRL (unconditinally turn on
                      dropout control mode)
B0 04       PUSHB 0x04
8D          SCANTYPE (enable smart dropout control)
&quot;Smart dropout control&quot; means activating rules 1, 2 and 5:
Rule 1: If a pixel&#x27;s center falls within the glyph outline,
        that pixel is turned on.
Rule 2: If a contour falls exactly on a pixel&#x27;s center,
        that pixel is turned on.
Rule 5: If a scan line between two adjacent pixel centers
        (either vertical or horizontal) is intersected
        by both an on-Transition contour and an off-Transition
        contour and neither of the pixels was already turned on
        by rules 1 and 2, turn on the pixel which is closer to
        the midpoint between the on-Transition contour and
        off-Transition contour. This is &quot;Smart&quot; dropout control.
For more detailed info (such as other rules not enabled in this snippet), please
refer to the TrueType Instruction Set documentation.</pre>

* 🔥 **FAIL** The 'prep' table does not contain TrueType instructions enabling smart dropout control. To fix, export the font with autohinting enabled, or run ttfautohint on the font, or run the `gftools fix-nonhinting` script. [code: lacks-smart-dropout]

</details>
<details>
<summary>⚠ <b>WARN:</b> Is the Grid-fitting and Scan-conversion Procedure ('gasp') table set to optimize rendering?</summary>

* [com.google.fonts/check/gasp](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/gasp)
<pre>--- Rationale ---
Traditionally version 0 &#x27;gasp&#x27; tables were set so that font sizes below 8 ppem
had no grid fitting but did have antialiasing. From 9-16 ppem, just grid
fitting. And fonts above 17ppem had both antialiasing and grid fitting toggled
on. The use of accelerated graphics cards and higher resolution screens make
this approach obsolete. Microsoft&#x27;s DirectWrite pushed this even further with
much improved rendering built into the OS and apps.
In this scenario it makes sense to simply toggle all 4 flags ON for all font
sizes.</pre>

* ⚠ **WARN** The gasp range 0xFFFF value 0x0A should be set to 0x0F. [code: unset-flags]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check if each glyph has the recommended amount of contours.</summary>

* [com.google.fonts/check/contour_count](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/contour_count)
<pre>--- Rationale ---
Visually QAing thousands of glyphs by hand is tiring. Most glyphs can only be
constructured in a handful of ways. This means a glyph&#x27;s contour count will only
differ slightly amongst different fonts, e.g a &#x27;g&#x27; could either be 2 or 3
contours, depending on whether its double story or single story.
However, a quotedbl should have 2 contours, unless the font belongs to a display
family.
This check currently does not cover variable fonts because there&#x27;s plenty of
alternative ways of constructing glyphs with multiple outlines for each feature
in a VarFont. The expected contour count data for this check is currently
optimized for the typical construction of glyphs in static fonts.</pre>

* ⚠ **WARN** This check inspects the glyph outlines and detects the total number of contours in each of them. The expected values are infered from the typical ammounts of contours observed in a large collection of reference font families. The divergences listed below may simply indicate a significantly different design on some of your glyphs. On the other hand, some of these may flag actual bugs in the font such as glyphs mapped to an incorrect codepoint. Please consider reviewing the design and codepoint assignment of these to make sure they are correct.

The following glyphs do not have the recommended number of contours:

Glyph name: A	Contours detected: 1	Expected: 2
Glyph name: Agrave	Contours detected: 2	Expected: 3
Glyph name: Aacute	Contours detected: 2	Expected: 3
Glyph name: Acircumflex	Contours detected: 2	Expected: 3
Glyph name: Atilde	Contours detected: 2	Expected: 3
Glyph name: Adieresis	Contours detected: 3	Expected: 4
Glyph name: AE	Contours detected: 1	Expected: 2
Glyph name: Eth	Contours detected: 1	Expected: 2
Glyph name: ring	Contours detected: 1	Expected: 2
Glyph name: tilde	Contours detected: 2	Expected: 1
Glyph name: Alphatonos	Contours detected: 2	Expected: 3
Glyph name: Alpha	Contours detected: 1	Expected: 2
Glyph name: Beta	Contours detected: 2	Expected: 3
Glyph name: beta	Contours detected: 1	Expected: 2
Glyph name: delta	Contours detected: 1	Expected: 2
Glyph name: rho	Contours detected: 1	Expected: 2
Glyph name: sigma	Contours detected: 1	Expected: 2
Glyph name: uni0410	Contours detected: 1	Expected: 2
Glyph name: uni0412	Contours detected: 2	Expected: 3
Glyph name: uni042F	Contours detected: 1	Expected: 2
Glyph name: uni0432	Contours detected: 2	Expected: 3
Glyph name: uni044F	Contours detected: 1	Expected: 2
Glyph name: A	Contours detected: 1	Expected: 2
Glyph name: AE	Contours detected: 1	Expected: 2
Glyph name: Aacute	Contours detected: 2	Expected: 3
Glyph name: Acircumflex	Contours detected: 2	Expected: 3
Glyph name: Adieresis	Contours detected: 3	Expected: 4
Glyph name: Agrave	Contours detected: 2	Expected: 3
Glyph name: Alpha	Contours detected: 1	Expected: 2
Glyph name: Alphatonos	Contours detected: 2	Expected: 3
Glyph name: Atilde	Contours detected: 2	Expected: 3
Glyph name: Beta	Contours detected: 2	Expected: 3
Glyph name: Eth	Contours detected: 1	Expected: 2
Glyph name: beta	Contours detected: 1	Expected: 2
Glyph name: delta	Contours detected: 1	Expected: 2
Glyph name: rho	Contours detected: 1	Expected: 2
Glyph name: ring	Contours detected: 1	Expected: 2
Glyph name: sigma	Contours detected: 1	Expected: 2
Glyph name: tilde	Contours detected: 2	Expected: 1
Glyph name: uni0410	Contours detected: 1	Expected: 2
Glyph name: uni0412	Contours detected: 2	Expected: 3
Glyph name: uni042F	Contours detected: 1	Expected: 2
Glyph name: uni0432	Contours detected: 2	Expected: 3
Glyph name: uni044F	Contours detected: 1	Expected: 2 [code: contour-count]

</details>
<details>
<summary>⚠ <b>WARN:</b> Font contains '.notdef' as its first glyph?</summary>

* [com.google.fonts/check/mandatory_glyphs](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/universal.html#com.google.fonts/check/mandatory_glyphs)
<pre>--- Rationale ---
The OpenType specification v1.8.2 recommends that the first glyph is the
&#x27;.notdef&#x27; glyph without a codepoint assigned and with a drawing.
https://docs.microsoft.com/en-us/typography/opentype/spec
/recom#glyph-0-the-notdef-glyph
Pre-v1.8, it was recommended that fonts should also contain &#x27;space&#x27;, &#x27;CR&#x27; and
&#x27;.null&#x27; glyphs. This might have been relevant for MacOS 9 applications.</pre>

* ⚠ **WARN** Glyph '.notdef' should contain a drawing, but it is empty. [code: empty]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check mark characters are in GDEF mark glyph class)</summary>

* [com.google.fonts/check/gdef_spacing_marks](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/gdef.html#com.google.fonts/check/gdef_spacing_marks)
<pre>--- Rationale ---
Glyphs in the GDEF mark glyph class should be non-spacing.
Spacing glyphs in the GDEF mark glyph class may have incorrect anchor
positioning that was only intended for building composite glyphs during design.</pre>

* ⚠ **WARN** The following spacing glyphs may be in the GDEF mark glyph class by mistake:
	 acute, cedilla, circumflex, dieresis, dieresistonos, grave, macron, ring, tilde and tonos [code: spacing-mark-glyphs]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check mark characters are in GDEF mark glyph class</summary>

* [com.google.fonts/check/gdef_mark_chars](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/gdef.html#com.google.fonts/check/gdef_mark_chars)
<pre>--- Rationale ---
Mark characters should be in the GDEF mark glyph class.</pre>

* ⚠ **WARN** The following mark characters could be in the GDEF mark glyph class:
	 U+20DD [code: mark-chars]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check GDEF mark glyph class doesn't have characters that are not marks)</summary>

* [com.google.fonts/check/gdef_non_mark_chars](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/gdef.html#com.google.fonts/check/gdef_non_mark_chars)
<pre>--- Rationale ---
Glyphs in the GDEF mark glyph class become non-spacing and may be repositioned
if they have mark anchors.
Only combining mark glyphs should be in that class. Any non-mark glyph must not
be in that class, in particular spacing glyphs.</pre>

* ⚠ **WARN** The following non-mark characters should not be in the GDEF mark glyph class:
	 U+0060, U+00A8, U+00AF, U+00B4, U+00B8, U+02C6, U+02DA, U+02DC, U+0384 and U+0385 [code: non-mark-chars]

</details>
<details>
<summary>⚠ <b>WARN:</b> Do any segments have colinear vectors?</summary>

* [com.google.fonts/check/outline_colinear_vectors](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/<Section: Outline Correctness Checks>.html#com.google.fonts/check/outline_colinear_vectors)
<pre>--- Rationale ---
This check looks for consecutive line segments which have the same angle. This
normally happens if an outline point has been added by accident.
This check is not run for variable fonts, as they may legitimately have colinear
vectors.</pre>

* ⚠ **WARN** The following glyphs have colinear vectors:
	* uni261C: L<<769.0,438.0>--<778.0,171.0>> -> L<<778.0,171.0>--<778.0,170.0>>
	* uni261D: L<<660.0,52.0>--<659.0,52.0>> -> L<<659.0,52.0>--<391.0,61.0>>
	* uni261E: L<<165.0,170.0>--<165.0,171.0>> -> L<<165.0,171.0>--<174.0,438.0>>
	* uni261F: L<<391.0,655.0>--<659.0,665.0>> -> L<<659.0,665.0>--<660.0,665.0>>
	* uni3063.vert: L<<310.0,418.0>--<321.0,423.0>> -> L<<321.0,423.0>--<323.0,424.0>>
	* uni3064: L<<173.0,388.0>--<168.0,386.0>> -> L<<168.0,386.0>--<154.0,380.0>>
	* uni3065: L<<166.0,381.0>--<161.0,379.0>> -> L<<161.0,379.0>--<147.0,373.0>>
	* uni3082: L<<434.0,591.0>--<437.0,616.0>> -> L<<437.0,616.0>--<456.0,778.0>>
	* uni3082: L<<507.0,773.0>--<487.0,610.0>> -> L<<487.0,610.0>--<484.0,586.0>>
	* uni337C: L<<668.0,431.0>--<732.0,373.0>> -> L<<732.0,373.0>--<736.0,369.0>> and 25 more. [code: found-colinear-vectors]

</details>
<details>
<summary>⚠ <b>WARN:</b> Do outlines contain any jaggy segments?</summary>

* [com.google.fonts/check/outline_jaggy_segments](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/<Section: Outline Correctness Checks>.html#com.google.fonts/check/outline_jaggy_segments)
<pre>--- Rationale ---
This check heuristically detects outline segments which form a particularly
small angle, indicative of an outline error. This may cause false positives in
cases such as extreme ink traps, so should be regarded as advisory and backed up
by manual inspection.</pre>

* ⚠ **WARN** The following glyphs have jaggy segments:
	* uni3235: B<<251.0,489.0>-<249.0,496.0>-<252.0,502.0>>/B<<252.0,502.0>-<228.0,449.0>-<191.0,404.0>> = 2.2025981617658017
	* uni3235: B<<280.0,592.0>-<273.0,549.0>-<253.0,504.0>>/B<<253.0,504.0>-<258.0,513.0>-<268.0,516.0>> = 5.092115124498886
	* uni3236: B<<172.5,72.0>-<163.0,73.0>-<157.0,80.0>>/B<<157.0,80.0>-<180.0,43.0>-<204.0,13.0>> = 8.735316951400781
	* uni3236: B<<96.5,219.0>-<120.0,144.0>-<154.0,85.0>>/B<<154.0,85.0>-<147.0,100.0>-<160.0,111.0>> = 4.93671468970148
	* uni5006: B<<588.0,257.0>-<597.0,250.0>-<598.0,243.0>>/L<<598.0,243.0>--<598.0,416.0>> = 8.13010235415596
	* uni50FB: B<<305.0,275.0>-<302.0,282.0>-<305.0,289.0>>/B<<305.0,289.0>-<289.0,256.0>-<270.5,228.0>> = 2.667766280446368
	* uni51AA: B<<441.0,348.0>-<441.0,350.0>-<443.0,350.0>>/L<<443.0,350.0>--<362.0,343.0>> = 4.939215542126153
	* uni548B: L<<334.0,414.0>--<334.0,416.0>>/L<<334.0,416.0>--<331.0,383.0>> = 5.1944289077348
	* uni5BA5: B<<354.0,319.0>-<354.0,329.0>-<360.0,336.0>>/B<<360.0,336.0>-<298.0,269.0>-<218.5,212.0>> = 2.179049801797654
	* uni5BA5: B<<439.0,436.0>-<406.0,385.0>-<361.0,337.0>>/B<<361.0,337.0>-<367.0,343.0>-<377.0,345.0>> = 1.8476102659943183 and 37 more. [code: found-jaggy-segments]

</details>
<details>
<summary>⚠ <b>WARN:</b> Do outlines contain any semi-vertical or semi-horizontal lines?</summary>

* [com.google.fonts/check/outline_semi_vertical](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/<Section: Outline Correctness Checks>.html#com.google.fonts/check/outline_semi_vertical)
<pre>--- Rationale ---
This check detects line segments which are nearly, but not quite, exactly
horizontal or vertical. Sometimes such lines are created by design, but often
they are indicative of a design error.
This check is disabled for italic styles, which often contain nearly-upright
lines.</pre>

* ⚠ **WARN** The following glyphs have semi-vertical/semi-horizontal lines:
 * uni30A3: L<<561.0,406.0>--<562.0,24.0>>
 * uni50AC: L<<448.0,-55.0>--<449.0,293.0>>
 * uni534D: L<<791.0,434.0>--<792.0,720.0>>
 * uni54E6: L<<233.0,417.0>--<234.0,562.0>>
 * uni54E6: L<<284.0,596.0>--<283.0,399.0>>
 * uni6763: L<<427.0,106.0>--<428.0,294.0>>
 * uni6A78: L<<564.0,39.0>--<565.0,280.0>>
 * uni6A78: L<<616.0,309.0>--<614.0,17.0>>
 * uni6AFA: L<<525.0,213.0>--<524.0,-6.0>>
 * uni750C: L<<305.0,319.0>--<306.0,191.0>> and 15 more. [code: found-semi-vertical]

</details>
<br>
</details>

### Summary

| 💔 ERROR | 🔥 FAIL | ⚠ WARN | 💤 SKIP | ℹ INFO | 🍞 PASS | 🔎 DEBUG |
|:-----:|:----:|:----:|:----:|:----:|:----:|:----:|
| 0 | 1 | 10 | 103 | 7 | 83 | 0 |
| 0% | 0% | 5% | 50% | 3% | 41% | 0% |

**Note:** The following loglevels were omitted in this report:
* **SKIP**
* **INFO**
* **PASS**
* **DEBUG**
