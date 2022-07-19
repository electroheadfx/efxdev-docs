# CSS line animation on hover



See this text underline animation? Looks really nice right? Let’s go straight into understanding how to create it step-by-step.

![Text underline animation on hover](https://s3.amazonaws.com/revue/items/images/016/838/608/original/underline-animation.gif?1657445138 "Text underline animation on hover")

Text underline animation on hover

The Markup

![HTML](https://s3.amazonaws.com/revue/items/images/016/838/678/mail/html.png?1657445476 "HTML")

HTML

The CSS

There are two ways to achieve the animation 

**Using** `**::after**` **pseudo-element**

In this method we can create a pseudo-element, position it below the link using `position: absolute`, give it a `2px` height and animate the width from 0 to 100%. Something like this:

![Method 1: Using pseudo element](https://s3.amazonaws.com/revue/items/images/016/838/777/mail/css1.png?1657446502 "Method 1: Using pseudo element")

Method 1: Using pseudo element

And it works! Here’s the [working demo](http://click.revue.email/ss/c/DMfKibboC_ZTmX8uI5IvEHTAKakfkolK60BzI4_Gwe-xOdS5-gBtoTg38FYpgr1jkUhH47e2RFzGbLBtm_ZAaRoRQl6bLuH1YbHQ-pQmWITysCRu9eHddBFcXPZFPpwBrRyW_Fv5XBXMppvr0xLNRDWixnr0c1wv3v-uhmdT01M7gSWK_yfyYpt7Ss477dGX3KRTNpIV3-QVmQm4eLN3RMrC7LRNuTigTGmBsyoWENk/3np/r9wFEUR-SiazLBU6TV6v-Q/h3/MGshSAghJmAoXFcyZ96jAuSfqKJV3ixhbFZJG54wPFY).

The only problem with this method is that, if the link text flows into next line, the underline appears only on the first line!

Remove `display:inline-block` on the `a` element in the above demo and try it out for yourself. So if you need the animation to work on a multi-line text, follow the next method.

**Using** `**background**` **property**

In this method, we use an *underline* background image and position it at the bottom of the link. We set the size to 0 width initially and set it to 100% on hover,

For the background image, we don’t need an actual image. We can use **linear gradient** along with other properties like this.

![Background values to create an underline](https://s3.amazonaws.com/revue/items/images/016/854/060/mail/css2.png?1657521049 "Background values to create an underline")

Background values to create an underline

As you can see, we have used the `background-image` property to set the color of the underline. The background-size property is needed to specify that the image (underline) occupies `100%` width and `2px` height. The `background-position` property is used to specify the position and the last line makes the background image not repeat.

If you use the above CSS, you’ll get an underline right away. But we need an underline only on hover. So, let’s change the second line above to:

![Initial background-size is 0](https://s3.amazonaws.com/revue/items/images/016/854/104/mail/css3.png?1657521334 "Initial background-size is 0")

Initial background-size is 0

And on hover, we change the `background-size` to `100% 2px`. Also, add some transition. This will be the full CSS:

![Full CSS for underline animation](https://s3.amazonaws.com/revue/items/images/016/854/116/mail/css4.png?1657521445 "Full CSS for underline animation")

Full CSS for underline animation

Unlike the previous method, this underline flows into multiple lines. See it for yourself in the [working demo](http://click.revue.email/ss/c/DMfKibboC_ZTmX8uI5IvEHTAKakfkolK60BzI4_Gwe9npESu-KPLAQUMxJ1a0eMapa2FvgPD8lZKc76LSIV_Y6PUlriSERiHeGAnmiTe_TGulQMfml2oEgVoj44YuRALBle1GIpyB1YGdw_Fj-gSUx9O1eyD0rrRhVeqKv5Pr7LQhyz7vNxWejcrcrDWg5wrafFP7eC49q0kX4JdeKE7ePu44WkFTgjHyzCoqEKeUho/3np/r9wFEUR-SiazLBU6TV6v-Q/h4/0A8mNcsh5uAXtUDY8qKS9j3BADK_3y9O2aJO9RZb06s).

**Bonus**

If you want the underline to animate from center instead of left to right, change the `background-position` value to center bottom.

On hover, the line appears from left to right. On leaving the mouse, if you want it to exit to the right like the below demo:

![Starts from left and leaves to right](https://s3.amazonaws.com/revue/items/images/016/854/184/original/animation2.gif?1657521861 "Starts from left and leaves to right")

Starts from left and leaves to right

You need to change the `background-position` to following:

![Change in background-position values](https://s3.amazonaws.com/revue/items/images/016/854/203/mail/css5.png?1657521987 "Change in background-position values")

Change in background-position values

If you found the `background` properties and their values confusing, I encourage you to visit the MDN docs for [background-image](http://click.revue.email/ss/c/i4W3jH19ejJsNqtlezSpO2vnaek6RQie8bYJdO-O-AE3TSORT-5qweJOIaUYnkVsCqPLuWvHyKB8Tbiudl2JLdS6X2WOgvbboNmXOnOL4aqcJjEE6_nFyO-lVs3JTWqdxHXVkqnr56_bNUDpr560m10Q9_3UDXEZXSFWkvtzKbYzmHdi1izqrRdzGyQE3nHfy0Mu1J0BkWy48a1dkdDzSg/3np/r9wFEUR-SiazLBU6TV6v-Q/h5/vPOBEsRPMTOtngg932syiJMFke8O41uSUJn4PFaSix0), [background-position](http://click.revue.email/ss/c/i4W3jH19ejJsNqtlezSpO2vnaek6RQie8bYJdO-O-AE3TSORT-5qweJOIaUYnkVsCqPLuWvHyKB8Tbiudl2JLf4nUReYr8tvLb91KoU9tdMIOxssXpZjHw2zp0mL3EuL8em7QYEvJaM1YaEQ2-XEpJhd-Bo3VfehSfXx7m0K3dr6xXwJ4HwbwCuSU2DYM0MeXUI3KPi4WfGC8JYYIiyOIw/3np/r9wFEUR-SiazLBU6TV6v-Q/h6/tw8JpqB3Z13EVJTcfzwGx3xHVUPPdgNPBHAKxOZNGsw) and [background-size](http://click.revue.email/ss/c/i4W3jH19ejJsNqtlezSpO2vnaek6RQie8bYJdO-O-AE3TSORT-5qweJOIaUYnkVsCqPLuWvHyKB8Tbiudl2JLRjlMftw15aT8Q4n4MfYOMkfZqze0N4tkg6Oz-156v1xdA6JycMFV25R9ouBDAu3l47jVw_CxnvtcQX1qOnDTV9R8s_XOt1gGPz-_cz_FDgBidVJAvvzHavgdYll2lv3oQ/3np/r9wFEUR-SiazLBU6TV6v-Q/h7/X4VYf7_Ez9vfDT466kZNI-DIDatSUg3Zaf9-skIjoWA).

That’s a wrap! Hope you learnt something new this week. Reply to this email and let me know if you are particularly interested in learning a trick you’ve seen somewhere.
