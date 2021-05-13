# Reload On Back

Let's say we have a web page which has a form that includes a nonce. Our user submits the form but realises they made a mistake. So they click back to return to the form and try again. But, unfortunately, our security team was perhaps a little over-zealous and the form didn't include any old nonce--it was a *true* nonce, which means it really could only be used once. The user submits their corrected form but, since they used the back button, they submit it with the old, already used nonce. So their efforts are rejected.

One potential solution to this problem is to ensure that, if a user navigates to the nonce-possessing form using the 'back' button of their browser, then the browser automatically reloads the page, and so our user gets a nice new, fresh nonce that won't get rejected.

This could be a little tricky because most modern browsers don't re-run any scripts when you navigate back to a page. Fortunately there is a `pageshow` event to which we can attach a function. So all we need to do when the page is shown is check if the user got here by using the 'back' button and, if so, we reload the page:

```
window.addEventListener("pageshow", function() {
  let navtype = window.performance.getEntriesByType("navigation")[0].type;
  if ( navtype == "back_forward" ) {
    window.location.reload(true);
  }
} );
```
