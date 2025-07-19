# Frontend Mentor - Testimonials grid section solution

This is a solution to the [Testimonials grid section challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/testimonials-grid-section-Nnw6J7Un7). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

-  [Overview](#overview)
   -  [The challenge](#the-challenge)
   -  [Screenshot](#screenshot)
   -  [Links](#links)
-  [My process](#my-process)
   -  [Built with](#built-with)
   -  [What I learned](#what-i-learned)
   -  [Useful resources](#useful-resources)
-  [Author](#author)

## Overview

### The challenge

Users should be able to:

-  View the optimal layout for the site depending on their device's screen size

### Screenshot

![Desktop Design](<screenshot/Design - Desktop Design - AJ.png>)
![Tablet Design](<screenshot/Design - Tablet Design - AJ.png>)
![Mobile Design](<screenshot/Design - Mobile Design - AJ.png>)

### Links

-  Solution URL: [GitHub Repository](https://github.com/AJ-Tan/7.-Frontend-Mentor---Testimonial-Grid-HTML-SASS-)
-  Live Site URL: [GitHub Pages](https://aj-tan.github.io/7.-Frontend-Mentor---Testimonial-Grid-HTML-SASS-/)

## My process

### Built with

-  Semantic HTML5 markup
-  CSS custom properties
-  CSS Grid
-  CSS Animation
-  CSS (SASS/SCSS)
-  Mobile-first workflow

### What I learned

1. For css animation fill mode forward. Don't include in the keyframes the properties that will also be used in
   hover effect and etc. Due to overlapping, it will not have any effect in the hover effects.

```css
/* Dont do this if we want to use transform in the hover */
.card {
   opacity: 0;
   transition: transform 0.2s ease-in-out;
   animation: fade-in--forward 0.5s ease-in-out forwards;
}

/* This will not work, due to transform property is included in keyframe with fill mode forwards */
.card:hover {
   transform: scale(1.05);
}

@keyframes fade-in--forward {
   from {
      opacity: 0;
      transform: translateX(-10%);
   }
   to {
      opacity: 1;
      transform: translateX(0%);
   }
}

/***********************************************************/

/* Do this instead */
.card {
   opacity: 0;
   transition: transform 0.2s ease-in-out;
   animation: fade-in--forward 0.5s ease-in-out forwards, offset-left-to-origin
         0.5s ease-in-out;
}

.card:hover {
   transform: scale(1.05);
}

/* With fill mode forward */
/* We will not be able to use opacity in other area, like hover and etc for the card class.
   which is ok in this case, but we do want the transform effect in hover. */
@keyframes fade-in--forward {
   from {
      opacity: 0;
   }
   to {
      opacity: 1;
   }
}

/* Without fill forward. So that we will be able to use the transform in hover */
@keyframes offset-left-to-origin {
   from {
      transform: translateX(-10%);
   }
   to {
      transform: translateX(0%);
   }
}
```

2. Looping through a SASS variable object.

```scss
$cardVariant: (
   "key1": (
      "prop1": ...,
      "prop2": ...,
   ),
   "key2": (
      "prop1": ...,
      "prop2": ...,
   ),
   "key3": (
      "prop1": ...,
      "prop2": ...,
   ),
);

@each $key, $variant in $cardVariant {
   //$key value will be like "key1", "key2", "key3" and etc
   /* 
    $variant value will be the object which can be accessed with map-get()
    example: map-get($variant, "prop1") to get the value the prop 1 of the current set.
  */
}
```

3. Linking directly SASS variable with CSS Custom variable is not possible, but there is a workaround.
   Useful when automating generation of css ruleset using SASS while linking these properties to CSS Custom Properties.

Example:

```scss
/* if you want to add new card variants, just add new key and values here */
$cardVariants: (
   "blue": (
      "bgColor": "--color-bg-1",
      "textColor": "--color-text-1",
   ),
   "red": (
      "bgColor": "--color-bg-2",
      "textColor": "--color-text-2",
   ),
   "green": (
      "bgColor": "--color-bg-3",
      "textColor": "--color-text-3",
   ),
);

/* creates card variants depending on the number keys in $cardVariants! */
.card {
   @each $key, $variant in $cardVariants {
      //card--blue, card--red, card--green
      &--#{$key} {
         background-color: var(map-get($variant, "bgColor"));
         color: var(map-get($variant, "textColor"));
      }
   }
}
```

4. Sequence delay for animation.

```scss
@for $i from 1 to $numberOfCards + 1 {
   & > [class|="card"]:nth-child(#{$i}) {
      animation-delay: #{($i - 1) * 0.1}s;
   }
}
```

### Useful resources

-  [SASS Documentation](https://sass-lang.com/documentation/) - Useful resource for the list of SASS features.
-  [CSS Animation](https://www.w3schools.com/css/css3_animations.asp) - Helped me with animation.
-  [CSS Transition](https://www.w3schools.com/css/css3_transitions.asp) - Helped me with transition.
-  [CSS Transform](https://www.w3schools.com/cssref/css3_pr_transform.php) - Transform property.

## Author

-  GitHub - [AJ-Tan](https://github.com/AJ-Tan)
-  Frontend Mentor - [@AJ-Tan](https://www.frontendmentor.io/profile/AJ-Tan)
