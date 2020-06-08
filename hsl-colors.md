# HSL(A) Colors

## Hue:
* 0: red hsl(0, 100%, 50%)  
* 60: yellow hsl(60, 100%, 50%) 
* 120: green hsl(120, 100%, 50%)
* 180: cyan hsl(180, 100%, 50%) 
* 240: blue hsl(240, 100%, 50%)
* 300: violet hsl(300, 100%, 50%);

## Saturation:
* 0%: grey
* 100%: full color
* range of usable color: 10% to 100%

## Lightness:
* 0%: black
* 100%: white
* range of usable color: 10% to 90%

## Opacity:
* 0: transparent
* 1: opaque
* range of usable color: 0.1 to 1

## Base Starting Parameters
* __Saturation__: begin with the default of 50%.
* __Lightness__: start with the default of 50%.
* __Opacity__: start with the default 100%.

## How to create color variations
1. define each base color's hue degree as a CSS variable.
  ```css
  :root {
    --base-color1: 60;
    --base-color2: 120;
    --base-color3: 200;
  }
  ```
2. create other shades from each of those base colors.
  ```css
  :root {
    --base-color1: 60;
    --color1-light: hsla(var(--base-color1), 50%, 75%, 100%);
    --color1-normal: hsla(var(--base-color1), 50%, 50%, 100%);
    --color1-darker: hsla(var(--base-color1), 50%, 35%, 100%);
  }
  ```
  3. apply this method to the rest of the base colors.
  ```css
  :root {
    --base-color1: 60;
    --color1-light: hsla(var(--base-color1), 50%, 75%, 100%);
    --color1-normal: hsla(var(--base-color1), 50%, 50%, 100%);
    --color1-darker: hsla(var(--base-color1), 50%, 35%, 100%);
    
    --base-color2: 120;
    --color2-light: hsla(var(--base-color2), 50%, 75%, 100%);
    --color2-normal: hsla(var(--base-color2), 50%, 50%, 100%);
    --color2-darker: hsla(var(--base-color2), 50%, 35%, 100%);

    --base-color3: 200;
    --color3-light: hsla(var(--base-color3), 50%, 75%, 100%);
    --color3-normal: hsla(var(--base-color3), 50%, 50%, 100%);
    --color3-darker: hsla(var(--base-color3), 50%, 35%, 100%);
  }
  ```

## Making More Common Rules for the Params of the HSL

You can generate CSS variables for the rest of the parameters (saturation, lightness & opacity), to target the most commonly used values.

```css
:root{ 
  /** commonly used saturation/lightness/opacity levels **/ 
  --saturation-level1: 20%;
  --saturation-level2: 50%; /* mid range - normal */
  --saturation-level3: 80%;
  
  --lightness-level1: 75%;
  --lightness-level2: 50%; /* mid range - normal */
  --lightness-level3: 35%;
  
  --opacity-level1: 100%; /* no opacity - normal */
  --opacity-level2: 80%;
  --opacity-level3: 60%;
}
```
Now you can use various combinations of these parameters.

```css
--color1-light:  hsla( var(--base-color1),  
                       var(--saturation-level2),  
                       var(--lightness-level1), 
                       var(--opacity-level1)  );
```
