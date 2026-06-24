# Source: https://docs.samply.app/guides/squarespace.html

# Integrating with Squarespace [​](https://docs.samply.app/#integrating-with-squarespace)

In this guide we'll show how to use [upload links](https://docs.samply.app/upload-portal.html) to receive files from website vistors. The information visitors provide in the contact form is automatically passed to Samply so they don't need to provide the same information twice.

## Setup [​](https://docs.samply.app/#setup)

We've setup a simple page with the embedded upload link placed directly above the form block. Samply only requires a `name` and `email` be provided, but your form can have as many fields as you'd like.

TIP

There's a hack that allows you to embed code inside the form block itself. Select the form, go to "Edit form fields" then add a "Text Area" field. Paste your embed code inside of the "description" field and it will appear on the page.

![Embeded upload link above Squarespace form](https://docs.samply.app/img/squarespace-layout.gif)

We'll give our iframe an id (`samply-upload`) so that it will be easy to identify in the custom code that we will add.

html

```
<iframe id="samply-upload" src="https://samply.app/..."></iframe>
```

## Injecting code [​](https://docs.samply.app/#injecting-code)

Squarespace let's you add custom code by using [code injection](https://support.squarespace.com/hc/en-us/articles/205815908-Using-code-injection). You can add javascript code to interact with elements on the page. We found that adding code to the "Footer" section worked best.

If you copy this code and paste it into your website, you should see a pop up that says "Samply!".

html

```
<script>
  alert("Samply!")
</script>
```

## Reading form values [​](https://docs.samply.app/#reading-form-values)

In order to pass `name` and `email` to Samply we first need to read these values from the Squarespace form. In our testing, we found that an easy way to do this was by listening to _all_ keyboard events on the page. Normally this would be excesive, but we had trouble getting [event listeners](https://developer.mozilla.org/en-US/docs/Web/API/Element/input_event) on form inputs to work consistently. You may have better luck.

![Web inspector](https://docs.samply.app/img/squarespace-inspector.png)

Each keyboard event has a `target`. The `target` has an `id` and we can use this to know which input on the page the event is coming from. It can be useful to use the [web inspector](https://developer.chrome.com/docs/devtools/open) to find ids in your form.

javascript

```

// Values of the inputs
let firstName = '';
let lastName = '';
let email = '';

// IDs of the input elements
const firstNameId = 'name-yui_3_17_2_1_1726169935413_20113-fname-field';
const lastNameId = 'name-yui_3_17_2_1_1726169935413_20113-lname-field';
const emailId = 'email-yui_3_17_2_1_1726169935413_20114-field';

window.addEventListener('keyup', (event) => {  
  // Value of current input ("Eric", "eric@samply.app", etc.)
  const inputValue = event.target.value;
  
  // Match IDs with their inputs and store the value
  switch(event.target.id) {
  	case firstNameId:
    	firstName = inputValue;
    	break;
    case lastNameId:
    	lastName = inputValue;
	    break;
    case emailId:
    	email = inputValue;
	    break;    
  }
  
});
```

## Writing form values [​](https://docs.samply.app/#writing-form-values)

Now that we have the form values we can send these values to Samply. We will use the id of the embedded iframe (`samply-upload`) to get a reference to the iframe. We can then use the [Window: postMessage()](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage) api to send the values.

html

```
<script>
  
  // ...code above

  const samplyUpload = document.getElementById("samply-upload");
  samplyUpload.contentWindow.postMessage({ email, name: firstName + ' ' + lastName }, '*');

  // code below...

</script>
```

## Sample code [​](https://docs.samply.app/#sample-code)

This full example passes `name` and `email` values from the Squarespace form into the Samply upload link. It also starts uploads when the Submit button is pressed on the Squarespace form.

html

```

<script>

  // Values of the inputs
  let firstName = '';
  let lastName = '';
  let email = '';

  // IDs of the input elements
  const firstNameId = 'name-yui_3_17_2_1_1726169935413_20113-fname-field';
  const lastNameId = 'name-yui_3_17_2_1_1726169935413_20113-lname-field';
  const emailId = 'email-yui_3_17_2_1_1726169935413_20114-field';

  /**
   * A helper function that returns the embeded Samply <iframe> element
   */
  function getSamplyElement() {
    return document.getElementById("samply-upload");
  }

  window.addEventListener('keyup', (event) => {  
    // Value of current input ("Eric", "eric@samply.app", etc.)
    const inputValue = event.target.value;
    
    // Match IDs with their inputs and store the value
    switch(event.target.id) {
      case firstNameId:
        firstName = inputValue;
        break;
      case lastNameId:
        lastName = inputValue;
        break;
      case emailId:
        email = inputValue;
        break;    
    }

    // Build full name
    const name = firstName + ' ' + lastName;

    // Pass the values to the Samply iframe element
    getSamplyElement().contentWindow.postMessage({ name, email }, '*');    
  });

  window.addEventListener('submit', (event) => {
    // Tell Samply to "submit"
    getSamplyElement().contentWindow.postMessage({ submit: true }, '*');
  });

</script>
```