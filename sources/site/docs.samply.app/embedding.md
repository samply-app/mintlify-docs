# Source: https://docs.samply.app/embedding.html

# Embedding Players [​](https://docs.samply.app/#embedding-players)

## Summary [​](https://docs.samply.app/#summary)

Adding a Samply embedded player to your site allows your site visitors to listen to high-fidelity audio directly on the page. And, your custom project color applies to the embedded widget, so you can be assured that the streamlined player UI will look great on your site in addition to sounding exceptional — in typical Samply fashion!

## Copy The Code [​](https://docs.samply.app/#copy-the-code)

Every player has an embed code that can be copied to your clipboard by clicking the "Embed" button.

![A Samply player on a funky gradient background](https://docs.samply.app/img/embed-&-copy.png#img-small)

You'll find this button in various locations:

- Top right of the player (when logged in)
- Context menu in your library
- Context menu in your project's players tab
- The project share dialog

The copied embed code will take the form:

html

```
<iframe src="https://samply.app/embed/<Player ID>"frameborder="0"></iframe>
```

## Add The Code [​](https://docs.samply.app/#add-the-code)

Once you have the code copied, it's time to add it to your website. Do this by editing your website's html and pasting the code into the desired location, this will often be inside the `<body>` or `<main>` tags.

Here's an example:

html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>My Website</title>  
</head>
<body>
  <main class="container">
      <h2>Welcome to Our Website</h2>
      <p>This is a simple demo website for Samply embedded players!</p>

      <!-- **** Embedded Player **** -->
      <iframe src="https://samply.app/embed/<Player ID>"frameborder="0"></iframe>      

  </main>
</body>
</html>
```

## Customize The Code [​](https://docs.samply.app/#customize-the-code)

There are a few properties that can be customized on embedded players.

### Dimensions [​](https://docs.samply.app/#dimensions)

A common customization is to adjust the player width and height. This is simply done by adding `width="<length>"` or `height="<length>"` to the iframe tag:

html

```
<iframe 
  src="https://samply.app/embed/<Player ID>"
  width="100%"
  height="480px"
  frameborder="0">
</iframe>
```

### Color [​](https://docs.samply.app/#color)

Embedded players, like in-app players, assume the color of their project by default. However, unlike in-app players, you may change the color of embedded players! This is done by adding a color query parameter to the source url.

The color query parameter takes a six-digit hex color value string, in the RGB hex format `#rrggbb` . The hash/pound character can be omitted, meaning the actual string in the query parameter becomes `rrggbb` :

html

```
<iframe 
  src="https://samply.app/embed/<Player ID>?color=rrggbb"
  width="100%"
  frameborder="0">
</iframe>
```

## Conclusion [​](https://docs.samply.app/#conclusion)

It's as easy as that - copy the embed code and style as desired! Feel free to contact us with any questions; we would love to help enliven your website with our signature lossless & gapless streaming.