- Always see whether you can apply size or units in same ration as other. Example if we have base size 16px, can we apply padding 32px etc.
  
- We can use ::before to have some decorative element before content
  - :: before places the pseudo content before content inside element not before element itself
  
  - I don't think we need to sweat a bundle bump of under 20KB for a core component of our application
  
  - When we talk about performance, we should always focus on the actual user experience. Specifically, what is the real-world impact when using a tool?
  
  - Always make sure when using `!important` it must be to override third-party styles, never your own styles
  
  - better to make ```<a>``` tag as block and add padding to it and ```<li>``` increase tap size

  - We want our layout to work irrespective of contents in them 

  - Don't mess with tabIndex, unless want to set it to (-1), i.e. remove from tab order

  - we can check height of property of our sticky element