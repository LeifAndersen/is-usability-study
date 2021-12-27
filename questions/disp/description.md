You are creating a component to output a number between `0` and `7` on a
7-segment display.

<p align="center">
<img src="./questions/disp/display.svg" alt="Display Diagram" 
     style="width:20em;max-width:100%"></p>

The display takes 7 bits, encoding each light's on/off state. The first bit
encodes the top light, `0` for off and `1` for on. Subsequent bits encode the
lights following a clockwise pattern. The final bit encodes the light in the
center of the display.

For example:

* If the component's input is `000` (binary 0), then its output is `1111110`.

* If the component's input is `011` (binary 3), then its output is `1111001`
  (as shown above).

* If the component's input is `111` (binary 7), then its output is `1110000`.


The component is defined as a function, which takes three input bits (referred
to as `in`), and outputs 7 bits (referred to as `out`).
The expected spec for this function is:

```clojurescript
(s/def ::bitvec (s/or string? int?))
(s/fdef display7
  :args (s/cat :in ::bitvec)
  :ret ::bitvec)
```

