<h1>Acid Rain</h1>

![image](https://user-images.githubusercontent.com/63907151/219901675-b753c2b9-3a5b-4c96-a977-ae4d8c529838.png)


1. Z-Index
The naïve way is to use an outer div, centered with margins, or if don't want to pollute the markup, use the padding for the same goals. Every div placed inside of it shall have the same width and height and, here comes the interesting part, position: absolute;. This will not only an easier positioning with margins relative to the outer div, but also the usage of z-index. We pile up the shapes as in the task and set up border-radius.

```
<div id="o">
  <div id="a"></div>
  <div id="b"></div>
  <div id="c"></div>
</div>
<style>
  body {
    margin: 0;
    background: #0B2429;
  }
  #o {
    margin: 30px 80px;
    width: 250px;
    height: 240px;
  }
  #o div {
    width: 120px;
    height: 120px;
    position: absolute;
  }
  #a {
    z-index: 1;
    margin: 0px 120px;
    background: #F3AC3C;
    border-radius: 60px;
  }
  #b {
    z-index: 2;
    margin: 60px 60px;
    background: #998235;
    border-radius: 60px 0px 60px 60px;
  }
  #c {
    z-index: 3;
    margin: 120px 0px;
    background: #F3AC3C;
    border-radius: 60px 0px 60px 60px;
  }
</style>
```

2. Box Shadow
This one is inspired by the shortest solution of the very first battle. We make two divs, one of them will be a circle. The second one has a squared border on one side and a box shadow. No need for z-index, because every next box-shadow is placed behind the previous. Five values, two mandatory ones for X and Y offsets, Blur, spread, and the color. By now you should have somehow realized what you gotta do. This is really the main part of the solution, other things like cascading, overwriting and nth-of-type() are nothing more than an attempt to reduce the amount of code in a "smart" way.

```
<div></div>
<div></div>

<style>
* {
  background: #0B2429;
}

div {
  width: 120px;
  height: 120px;
  margin: 30px 192px;
  border-radius: 60px;
  background: #F3AC3C;
}

div:nth-of-type(2) {
  margin: -30px 72px;
  box-shadow: 60px -60px #998235;
  border-radius: 60px 0 60px 60px;
}
</style>
```

3. Sixty
Just for the sake of trying out something new and noticing quite a relationship of all of the values to sixty, I decided why not. We don't need SASS, we need much less – custom properties. We define a property --sixty and place to the wildcard so that it is available through cascading. Then we do some calc() magic and the rest is the same as above

```
<div></div>
<div></div>

<style>
* {
  background: #0B2429;
  --sixty: 60px;
}

div {
  width: calc(2 * var(--sixty));
  height: calc(2 * var(--sixty));
  margin: calc(0.5 * var(--sixty)) calc(3 * var(--sixty) + 0.2 * var(--sixty));
  border-radius: var(--sixty);
  background: #F3AC3C;
}

div:nth-of-type(2) {
  margin: calc(-0.5 * var(--sixty)) calc(var(--sixty) + 0.2 * var(--sixty));
  box-shadow: var(--sixty) calc(-1 * var(--sixty)) #998235;
  border-radius: var(--sixty) 0 var(--sixty) var(--sixty);
}
</style>
```
