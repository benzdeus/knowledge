# Styled Components 

เป็น library ที่ช่วยให้เราสร้าง component จาก html element ต่างๆ เช่นแท็ก div, span, a, p หรืออื่นๆ และจะสามารถกำหนด style ให้ code เพื่อตกแต่งความสวยงามให้กับรูปแบบการแสดงผลบนเว็บไซต์ 

```js
//ต้องทำการ import ไฟล์.css มาด้วย
import '.CssExmple';

<div className="div-sub">
  <div className="div-color">Hi, I am Example</div>
  <label id="name-css">ชื่อ-สกุล</label>
  <input type="text" placeholder="กรุณากรอกข้อมูล">
  </input>
  <button type="submit">เพิ่มข้อมูล</button>
</div>
```

- การกำหนด Style ให้ Components 

```css
/* การกำหนด style จากชื่อ class */
.div-color{
    font-size:14px,
    color: blue,
    display:inline-block
}
```
```css
/* การกำหนด style จากแท็ก HTML */
input{
    border: 1px solid #deded,
    border-radius: 8px,
    display:block,
    padding:10px,
    width:100%
}
```

```css
/* การกำหนด style จากเข้ามากแท็กแม่สู่แท็กลูก */
.div-sub > button{
 border-radius: 8px,
 background-color: green,
 width:100%
 color:#ffffff
}

```
```css
/* การกำหนด style จาก id */
#name-css{
 font-size:14px,
 color: blue,
 display:inline-block
}

```
