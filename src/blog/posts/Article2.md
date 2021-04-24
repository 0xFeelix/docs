---
title: Quotes Card Hover Effect With CSS
type: article
sidebar: auto

---

# Quotes Card Hover Effect With CSS

![Happy-sad](/post-images/happy-sad.webp)

---

Switches are used when the user has to choose from two different choices. One of the options is set as the default choice in case the user does not make any choice. In today’s tutorial, we create Happy-Sad switch. As the name suggests, the user has to choose one from two possible options Happy Or Sad.
To create this switch, all we need is a single checkbox and some pure CSS. So let us get started.

## HTML

For the HTML code, we don’t need anything much but just an input element with the type ‘checkbox’.

``` html
<input type="checkbox">
```

## CSS

### Adding Basic Styling:
To style and customize the switch, we add some CSS. Styling checkboxes might look a bit complicated, but they are pretty straightforward.

``` css
body{
    background-color: #1a191e;
    padding: 0;
    margin: 0;
}
```

### Hiding Default Checkbox:
We start by hiding the default checkbox with the help of the ‘appearance’ property. Next, we set dimensions of 200 pixels into 80 pixels to the checkbox. Once we have the dimensions set, we can now center the checkbox. You can check out the little trick I have used to center the checkbox here.

Add some box-shadow to the unselected end of the checkbox to make it look a bit lifted from the surface.

``` css
input[type="checkbox"]{
    -webkit-appearance: none;
    background-color: #222127;
    height: 80px;
    width: 200px;
    position: absolute;
    margin: auto;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    box-shadow: 18px 12px 18px -5px
                  rgba(0,0,0,0.35);
    border-radius: 40px;
    outline: none;
    cursor: pointer;
    transition: 0.3s;
}
```

### Creating Eyes Using Box-Shadow:
We use the ‘:before’ pseudo-element to create the two pairs of eyes on each end of the switch.

``` css
input[type="checkbox"]:before{
    position: absolute;
    content: "";
    height: 10px;
    width: 10px;
    background-color: #0ba041;
    border-radius: 50%;
    top: 20px;
    left: 27px;
    box-shadow: 0 33px 0 0 #0ba041,
		135px 33px 0 0 #b5b2b3,
	        135px 0 0 0 #b5b2b3;
}
```

### Creating Smile:
To create the smile, we make use of the ‘:after’ pseudo-element. Here make sure you add the ‘content’ property to each of the pseudo-elements to make them work.

``` css
input[type="checkbox"]:after{
    position: absolute;
    content: "";
    height: 23px;
    width: 10px;
    border: 4px solid #0ba041;
    border-left: none;
    border-radius: 0 23px 23px 0;
    margin: auto;
    top: 0;
    bottom: 0;
    left: 50px;
    transition: 0.3s;
}
```

### Smile To Frown Transition:
When the user checks the checkbox, the pseudo-element, i.e., the smile, moves to the opposite end of the switch. This thereby turns the smiling face into a frowning face.

On clicking the checkbox again, the smile returns to the original position creating the smiling face again.

``` css
input[type="checkbox"]:checked:after{
    left: 138px;
    border-color: #b5b2b3;
}
```

### Shifting Box-Shadow:
Also, in the checked state, the box-shadow is applied to the other end of the switch.

``` css
input[type="checkbox"]:checked{
     box-shadow: -18px 12px 18px -5px
                  rgba(0,0,0,0.35);	
}
```

---
[Back](/blog/)
