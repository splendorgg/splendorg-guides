---
title: Scss
---



# Compiling Scss into Css
To compile SCSS files into CSS in real-time, use the following com
```bash
sass --watch inputDirectory:outputDirectory
```
- Replace inputDirectory with the folder containing your SCSS files.
- Replace outputDirectory with the folder where you want the compiled CSS files to be saved.
- The --watch flag ensures that any changes in SCSS files are automatically compiled into CSS.

---

# Mixins
Mixins allow you to create reusable blocks of SCSS code with configurable parameters.

_ mixins.scss
```scss
@mixin flex-row($justify-content: space-between,$align-items.center, $gap:0){
	display:flex;
	justify-content:$justify-content;
	align-items:$align-items;
	gap:$gap;
}
```

stlye.scss
```scss
@use 'mixins';

.navbar{
	@include mixins.flex-row;
	.nav-list{
		@include mixins.flex-row($gap:32px);
	}
}
```
---

# Variables
style.scss
```scss
$desktop-width:1024px;

.nav-link{
	width:$desktop-width;
}
```

---

# Themes
SCSS allows you to define themes with specific colors or styles that can be reused across your project.

theme.scss
```scss
$primary-color: #C778DD;
$gray-color: #ABB2BF;

:export{
	primary-color:$primary-color;
	gray-color:$gray-color;
}
```

style.scss
```scss
@use 'theme' as *;

.nav-link{
	color:$gray-color;
}
```

---

# Inheritance(@extend)
```scss
%button-base{
	background-color:transparent;
	border: 1px solid $primary-color;
	padding: 8px 16px;
}

button{
	@extend %button-base;
	&.success{ // <button class="success">
		border: 1px solid green;
	}
	&.warning{ // <button class="warning">
		border: 1px solid red;
	}
}


```