# Page-Transition-GSAP

```javacsript
    document.addEventListener("DOMContentLoaded", () => {
    });
```

Here, we're defining an easing function from GSAP. "power4.inOut" creates a smooth, natural-looking animation that starts slow, accelerates in the middle, and then slows down at the end. Think of it like a car smoothly starting, reaching full speed, and then gently stopping.


```javascript
 document.querySelectorAll("a").forEach((link) => {
        link.addEventListener("click", (event) => {
            event.preventDefault();
            const href = link.getAttribute("href");
            if (href && !href.startsWith("#") && href !== window.location.pathname){
                animateTransition().then(() => {
                    window.location.href = href;
                });
            }
        });
    });
```


This block does something really interesting:

- It selects ALL anchor (<a>) tags on the page
- Adds a click event listener to each link
- Prevents the default link behavior (immediate page navigation)
- Checks if the link:

1 - Has an actual href attribute
2 - Is not an internal page anchor (doesn't start with #)
3 - Is not the current page


- If these conditions are met, it:

1 - Runs the animateTransition() function
2 - After the transition animation completes, navigates to the new page

```javascript
 revealTransitoin().then(() => {
        gsap.set(".block", {visibility: "hidden"});
    });
```

This line:

- Runs the revealTransitoin() function (note the typo in "transition")
- After the reveal animation completes, it hides all elements with the class "block"


```javascript
 function revealTransitoin(){
        return new Promise((resolve) => {
            gsap.set(".block", {scaleY: 1});
            gsap.to(".block", {
                scaleY : 0,
                duration: 1,
                stagger: {
                    each: 0.1,
                    from: "start",
                    grid: "auto",
                    axis: 'x',
                },
                ease: ease,
                onComplete: resolve,
            });
        });
    }
```


This function creates a reveal transition:

- Sets all ".block" elements to full vertical scale initially
- Animates these blocks to scale down to zero vertically
- The animation takes 1 second
- Blocks animate with a staggered effect:

    - 0.1 second delay between each block
    - Starts from the beginning of a grid
    - Automatically determines grid layout
    - Animates along the x-axis


- Uses the smooth "power4.inOut" easing
- Resolves the Promise when animation completes



```javascript
function animateTransition(){
        return new Promise ((resolve) => {
            gsap.set(".block", {visibility: "visible", scaleY : 0});
            gsap.to(".block", {
                scaleY : 1,
                duration: 1,
                stagger: {
                    each: 0.1,
                    from: "start",
                    grid: [2, 5],
                    axis: 'x',
                },
                ease: ease,
                onComplete: resolve,
            });
        });
    }
```

This function is similar to revealTransitoin(), but does the opposite:

- Makes ".block" elements visible
- Sets their initial vertical scale to zero
- Animates them to full vertical scale
- Uses a 2x5 grid for staggering
- Takes 1 second with the same smooth easing
- Resolves the Promise when animation completes

Overall, this code creates a slick page transition effect where blocks appear to "unfold" or "reveal" when navigating between pages, providing a smooth, animated user experience.