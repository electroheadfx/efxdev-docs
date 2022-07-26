# Display contents in CSS rule

|                                                                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Hey! Welcome to the second issue of this newsletter. Let’s create a responsive blog post display layout using the lesser known CSS rule `display: contents`. |
|                                                                                                                                                              |

Responsive Blog Post Display using Grid and display:contents

Consider this blog post display section. On a wider screen, we want the image to be on the right **separated** from the text. While on a mobile screen, we want the image to appear **in between** our heading and the paragraph.

![Desktop and mobile layouts](https://s3.amazonaws.com/revue/items/images/016/701/090/mail/Layouts.png?1656655770 "Desktop and mobile layouts")

Desktop and mobile layouts

This layout could easily be a hero section of your website too. There are multiple ways to approach this, based on the HTML markup. Likely, your markup looks something like this:

![HTML](https://s3.amazonaws.com/revue/items/images/016/702/546/mail/html.png?1656661490 "HTML")

HTML

With this markup, the desktop layout is straight forward. You can use flexbox like this:

![Desktop layout with flexbox](https://s3.amazonaws.com/revue/items/images/016/702/579/mail/css-1.png?1656661837 "Desktop layout with flexbox")

Desktop layout with flexbox

But for smaller screens, how do you get that image in between heading and paragraph?

**Introducting** `**display: contents**` **CSS rule**

When you set use `display: contents` on an element, that element’s children become direct children of the element’s parent. It’s like, that element disappears from the Markup.

So, in our case, for mobile layout, if we use `display: contents` on our `.text`element, it gets ignored:

![display: contents makes the element get ignored](https://s3.amazonaws.com/revue/items/images/016/702/751/mail/html2.png?1656662466 "display: contents makes the element get ignored")

display: contents makes the element get ignored

And now it’s equivalent to the below markup, for styling:

![](https://s3.amazonaws.com/revue/items/images/016/702/774/mail/html3.png?1656662533)

Now we can use flexbox for the `.container` with `flex-direction` as `column`and then use `order` property to get the image element in between heading and para! 🪄

Here’s the simplified CSS snippet:

![Simplified CSS snippet](https://s3.amazonaws.com/revue/items/images/016/702/892/mail/final.png?1656663026 "Simplified CSS snippet")

Simplified CSS snippet

You can see the [full working demo on Codepen](http://click.revue.email/ss/c/DMfKibboC_ZTmX8uI5IvEHTAKakfkolK60BzI4_Gwe8WfPBgivxNVfs48XJHmHL6AErBtti-W9NKCAiQW_b-XXhnYReOyHcHvKZYVoNt6FSy0EmFwH5wm_OlfdZNNHoAZkMkWcuFJUMGvT8D-RoHkRHdxfuc1x_c5nJweSEjU4w1SBqc_BZqqAch2-SW1D5Vrd4vdZnKZzcxjbOuVwTNerk-poXcjUotccZbtxKAiBs/3ni/JCX_O6OGR3uOz5z-etS_jA/h3/mp5GILNDVfmL_lTLUt_hGTFG9ZtgI32hdHpAvI-DY5g)

[![Responsive blog post display](https://s3.amazonaws.com/revue/items/images/016/702/913/thumb/6172a5385e023f562d35922b8f8f6c02-800.jpg?1656663120)](http://click.revue.email/ss/c/DMfKibboC_ZTmX8uI5IvEHTAKakfkolK60BzI4_Gwe8WfPBgivxNVfs48XJHmHL6AErBtti-W9NKCAiQW_b-XXhnYReOyHcHvKZYVoNt6FSy0EmFwH5wm_OlfdZNNHoAZkMkWcuFJUMGvT8D-RoHkRHdxfuc1x_c5nJweSEjU4w1SBqc_BZqqAch2-SW1D5Vrd4vdZnKZzcxjbOuVwTNerk-poXcjUotccZbtxKAiBs/3ni/JCX_O6OGR3uOz5z-etS_jA/h4/39SdcN8s1cKCC59WghHrthnlM6dHtRMjD4Gr9Yh4kbw)

[Responsive blog post display](http://click.revue.email/ss/c/DMfKibboC_ZTmX8uI5IvEHTAKakfkolK60BzI4_Gwe8WfPBgivxNVfs48XJHmHL6AErBtti-W9NKCAiQW_b-XXhnYReOyHcHvKZYVoNt6FSy0EmFwH5wm_OlfdZNNHoAZkMkWcuFJUMGvT8D-RoHkRHdxfuc1x_c5nJweSEjU4w1SBqc_BZqqAch2-SW1D5Vrd4vdZnKZzcxjbOuVwTNerk-poXcjUotccZbtxKAiBs/3ni/JCX_O6OGR3uOz5z-etS_jA/h5/-vr5I7ohWd-z4Np_q2tbBJiIfM8_D3tnr_31YAqgjNw)

Image appears in different places on mobile and in desktop layouts

[codepen.io](http://click.revue.email/ss/c/DMfKibboC_ZTmX8uI5IvEHTAKakfkolK60BzI4_Gwe8WfPBgivxNVfs48XJHmHL6AErBtti-W9NKCAiQW_b-XXhnYReOyHcHvKZYVoNt6FSy0EmFwH5wm_OlfdZNNHoAZkMkWcuFJUMGvT8D-RoHkRHdxfuc1x_c5nJweSEjU4w1SBqc_BZqqAch2-SW1D5Vrd4vdZnKZzcxjbOuVwTNerk-poXcjUotccZbtxKAiBs/3ni/JCX_O6OGR3uOz5z-etS_jA/h6/LkJ4Jh1mTaHwkFjEUEsvQ62pZN7Kx2tPzNBnifsmXWs)
