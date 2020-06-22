# Positioning content
For the last few chapter we have been creating single column layout where contents are flowing vertically.But when it comes to real website we need multicolumn layout and css helps us to do that.  

**There are few methods to do that**
1. **Positioning With inline-block** 
Usually to create an outline we use block level element and as we know block level element takes the full width and to stack one after another we will need to chnage its display properties to **_inline-block_**  
For example:-  
```
<header>..........</header>
  <aside>.........</aside><!--
  --><section>.........</section>
  <footer>............</footer>  
   <!-- CSS -->  
    *, *:before, *:after {
    box-sizing: border-box;
  }
   section, aside {
    display: inline-block;
    margin: 32px 1.5%;
  }
  aside {
    width: 30%;
  }
  section {
    width: 63%;
  }
```  
In the above example we have chnage the display properties of aside and section to inline block to stack one after another. As you see in the above code I used border-box value to the box-sizing for every element. Generally the best box-sizing value to use is border-box beacuse whatever the width we give to an element its padding and border doesnt effect the width of the element.  
2. **Positioning With Float**  
Another way we can position the element one after another on a page is with **_Float_** Property.The float comes with three different values: left, right, and none.  
For example:-  
```
 <!-- HTML -->
  <header>..........</header>
  <aside>.........</aside>
  <section>.........</section>
  <footer>............</footer>
  <!-- CSS -->
  *, *:before, *:after {
    box-sizing: border-box;
  }
   aside {
    float: left;
    width: 30%;
    margin: 32px 1.5%;
  }
  section {
    float: right;
    width: 63%;
    margin: 32px 1.5%;
  }
  footer {
    clear: both;
  }
```
In the above example we have seen that to put one after another we used float properties in section and aside and after using float it break the flow of the page and put it one after another and by doing so it changes the display properties of the element. A block level elements may start covering the space according to the content it wraps. To fix this behavior we can apply some fixed width according to the need. As all upcoming element will flow around the floated element, that's why the footer is in the gutter between the aside and section. To get rid of this we can apply clear: both on the footer.  

## Clearing and Containing the Float  
**Clearing the floats**  
The clear property in CSS accepts three different values, left, right and both. The left value will clear the left floats and right will clear right floats. Both value will clear both the right and left floats and it is safer to apply.  
For example  
```
  div {
    clear: both;
  }
```
**Containig the float**  
However, clearing floats won't return each and everything to normal. One of the most popular problems you may encounter with a parent containing floated elements. There are several way to conatin the float but the best way to do is **_clearfix technique_**  
**clearfix technique**  
One of the most effective ways to contain floats is the clearfix method. The clearfix technique is more preferable and has advantages over other techniques.  
For example:-  
```
 <!-- HTML -->
  <header>..........</header>
  <div class="clearfix">
    <aside>.........</aside>
    <section>.........</section>
  </div>
  <footer>............</footer>
   <!-- CSS -->
   *, *:before, *:after {
    box-sizing: border-box;
  }
  aside {
    float: left;
    width: 30%;
    margin: 32px 1.5%;
  }
  section {
    float: right;
    width: 63%;
    margin: 32px 1.5%;
  }
  <!-- clearfix technique -->
  .clearfix:before, .clearfix:after {
  content: "";
    display: table;
  }
  .parent:after {
    clear: both;
  }
```
In above example to contain the float we have used class clearfix to parent div and wrote css using psuedo element to do so.The before and after pseudo-element will create a hidden element above and below the parent class. We created a table-cell using display: table to the pseudo-elements. This is to make the block-level element so that it should take full available width above and below the element. The display: block would also work fine, but display: table will ensure consistency for the older version of internet explorer.  
At the end to the :after pseudo-element, we also applied clear: both. This is to clear floats so that the next upcoming element does not get wrapped around the floated elements.  

## Uniquely Positioning Element  
Sometimes we may need more control over the position of the element which inline block or float wont be able to do that In such cases `position` property comes into play. The position property accepts four different values, `static, relative, absolute, fixed.`  
**Position static**  
By default, every element in a document is a `static` element and does not accept any box-offset properties. It will be in the normal flow of the page, won't be repositioned.  

**Position relative**  
It accept all box-offset properties i.e, left right top and bottom.We can precisely position the element by shifting it from its default position in any direction(top, right, bottom, or left). Although it accept all box-offset properties it still remain in the flow of page and its original position remain empty no other element takes that place the relatively positioned element can overlap or underlap other elements, without disturbing their original positions. It won't push or shifts other elements on the page.  
For Example:-  
```
  <div class="box box-1">......</div>
  <div class="box box-2">......</div>
  <div class="box box-3">......</div>

  .box {
    width: 100px;
    height: 100px;
    background: green;
  }
  .box-2 {
    position: relative;
    top: 60px;
    left: 60px;
  }
```
In the above example There are three boxes and each box is having the same styles. But we only position the second box relatively. The second box will shift from the top towards the bottom and left towards the right by 60px. But it won't disturb the position of the other two boxes on the page. Also, the original position of the element will be maintained.  
As per the priorities between the top and bottom top will get the priorities and from left and right it depends on the language from whichever side the particular language get started that side will get the priorities.  

**Position absolute**  
The absolutely positioned elements accept all the box-offsets however they are removed from the normal flow of the page. Upon removing from the normal of the page the elements lose its original position. And that lost position will be taken by the upcoming element. As the element is removed from the original flow it can position in relation to parent which is either described as relative or absolute or it will position according to the body.  
The display properties also changes the block level element start behaving as inline level element and inline level element start accepting height and width properties.  
If there is no box-offset properties applied then the element will be on its original position but on the Z axis.  
```
 <div class="box box-1">......</div>
  <section class="parent-box">
    <div class="box box-2">......</div>
  </section>
  <div class="box box-3">......</div>


  box {
    width: 100px;
    height: 100px;
    background: green;
  }
  .parent-box {
    position: relative;
  }
  .box-2 {
    position: absolute;
    right: 0;
    bottom: 0;
  }
```
Here, the box-2 is absolutely positioned with relative to its parent, because the parent-box has been relatively positioned. Therefore the box-2 will sit at the right bottom corner of the parent-box.  
If the absolute element has the fixed width and height then the priorities will go to top between top and bottom and for left and right depend on the language.  
But if the absolute element has not fixed width and height then the element will start from both top and bottom side. As a result, covering the specified height of the relative parent or else covering the whole height of the body. The same goes for the left and right offset.  

**Position Fixed**  
Position fixed is similar to absolute positioning. However, the fixed positioning will be always relative to the browser viewport. The fixed positioned elements do not scroll with the page. Its position will be fixed relative to the browser viewport no matter where you stand on the page.  
For example:-
```
.box {
    position: fixed;
    right: 60px;
    bottom: 60px;
  }
```
## z-index  
When we start positioning elements using position property, an element may be placed on top of another. Using z-index property we can decide the order of an element, which will be on top and which will be at the bottom.The z-index property only works with relative, absolute, and fixed elements. By default, every element has 0 value for the z-index property. The element with the highest z-index value will appear on top and with the lowest value will at the bottom.





