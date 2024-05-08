## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

## Overview

### The challenge

Users should be able to:

- View an age in years, months, and days after submitting a valid date through the form
- Receive validation errors if:
  - Any field is empty when the form is submitted
  - The day number is not between 1-31
  - The month number is not between 1-12
  - The year is in the future
  - The date is invalid e.g. 31/04/1991 (there are 30 days in April)
- View the optimal layout for the interface depending on their device's screen size
- See hover and focus states for all interactive elements on the page
- **Bonus**: See the age numbers animate to their final number when the form is submitted

### Screenshot

![](./screenshot.jpg)

Add a screenshot of your solution. The easiest way to do this is to use Firefox to view your project, right-click the page and select "Take a Screenshot". You can choose either a full-height screenshot or a cropped one based on how long the page is. If it's very long, it might be best to crop it.

Alternatively, you can use a tool like [FireShot](https://getfireshot.com/) to take the screenshot. FireShot has a free option, so you don't need to purchase it. 

Then crop/optimize/edit your image however you like, add it to your project, and update the file path in the image above.

**Note: Delete this note and the paragraphs above when you add your screenshot. If you prefer not to add a screenshot, feel free to remove this entire section.**

### Links

- Solution URL: [Add solution URL here](https://your-solution-url.com)
- Live Site URL: [Add live site URL here](https://your-live-site-url.com)

## My process

### Built with

- [Vue.js](https://vuejs.org/) - JS Library
- [Vite.js](https://vitejs.dev/) - JS Library for Front-end tooling
- CSS custom properties
- Flexbox
- Mobile-first workflow

### What I learned

This project allowed me to recap on how to pass properties between components in order to display by dealing with the Vue Composition API which is an API featured in Vue.js and is a set of APIs that allows us to author Vue components using imported functions instead of declaring options. By using the Composition API it allowed me to pass the properties and validate them before passing them. I also found that validating the dates of each month by using the array syntax was great as it allowed me to double check the input separately in a different method than checking if it's null or not by looping through the day properties.

```js
var daysInMonths = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
  
  if(year % 400 == 0 || (year % 100 != 0 && year % 4 == 0)) {
    daysInMonths[1] = 29;
  }

  if(month < 1 || month > 12 || day < 1 || day > daysInMonths[month - 1]) {
    return false;
  }
```

### Useful resources

- [CSS Box Shadow](https://css-tricks.com/snippets/css/css-box-shadow/) - This helped me for the form as it made it more obvious instead of having a plain white background.
- [JS Date Validation](https://www.scaler.com/topics/date-validation-in-javascript/) - This allowed me to validate any dates from the user through JavaScript and handle any Errors.
- [GSAP Animation](https://gsap.com/docs/v3/GSAP/gsap.fromTo()/) - This provided me with some guidance on how to install gsap in my vue project and set it up with the required animation.

## Author

- Website - [Joshua Campbell](https://www.joshua-campbell.net/)
- Frontend Mentor - [@jcampb98](https://www.frontendmentor.io/profile/jcampb98)
- LinkedIn - [Joshua Campbell](https://www.linkedin.com/in/joshua-campbell98/)
- GitHub - [@jcampb98](https://github.com/jcampb98)