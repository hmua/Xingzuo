

#### 组合多种style、weight
```CSS
@font-face {
  font-family: "DroidSerif";
  src: url("DroidSerif-Regular-webfont.ttf") format("truetype");
  font-weight: normal;
  font-style: normal;
}
@font-face {
  font-family: "DroidSerif";
  src: url("DroidSerif-Italic-webfont.ttf") format("truetype");
  font-weight: normal;
  font-style: italic;
}
@font-face {
  font-family: "DroidSerif";
  src: url("DroidSerif-Bold-webfont.ttf") format("truetype");
  font-weight: bold;
  font-style: normal;
}
@font-face {
  font-family: "DroidSerif";
  src: url("DroidSerif-BoldItalic-webfont.ttf") format("truetype");
  font-weight: bold;
  font-style: italic;
}
```

#### 更简练的格式：
```CSS
@font-face {
  font-family: 'Klavika';
  src: url(../fonts/Klavika-Regular.otf) format('truetype') font-weight-normal,
       url(../fonts/Klavika-Bold.otf) format('truetype') font-weight-bold,
       url(../fonts/Klavika-Bold-Italic.otf) format('truetype') font-italic font-weight-bold;
}
```
摘录自：https://stackoverflow.com/questions/28279989/multiple-font-weights-one-font-face-query

#### 23年6月2日，今天又[看到一种写法](https://stackoverflow.com/a/71851290)
```css
@font-face {
  font-family: 'NoEmojiAstronomy';
  src: local("Apple Symbol"), local("Segoe UI Symbol"), local("Arial Unicode MS"), local("Menlo"), local("sans-serif");
  unicode-range: U+263C-2653;
}
```
