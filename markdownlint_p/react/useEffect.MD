# useEffect

ผลกระทบที่เกิดขึ้นภายใน component ใช้เมื่อต้องการทราบการการเปลี่ยนแปลงส่งผลให้ render component ใหม่อีกครั้ง เป็น Hook ที่มีปัจจัยภายนอกเข้ามาเกี่ยวข้องกับตัว function component เช่น การแก้ไขพวก window, title หรือเรียก lifecycle ของ React เช่น componentDidMount
componentDidUpdate เป็นต้น

- กำหนดให้ useEffect ทำงานก็ต่อเมื่อมีการเปลี่ยนแปลงค่าเท่านั้น ในตัวอย่างนี้ useEffect จะทำงานก็ต่อเมื่อ title และ amount เมื่อมีการเปลี่ยนแปลงค่า

```js
// useEffect จะทำงานเมื่อโหลดหน้าครั้งแรก และจะทำงานอีกครั้งเมื่อผู้ใช้งานมีการพิมพ์(title)และป้อนจำนวนเต็ม(amount)ที่มากกว่า 0

useEffect(() => {
  const checkData = title.trim().length > 0 && amount !== 0;
  setFormValid(checkData);
}, [title, amount]);
```

- ใส่ [] เพื่อแก้ปัญหาการทำงานซ้ำของ useEffect โดย effect เกิดขึ้นครั้งเดียวตอน render ครั้งแรก โดยที่เราจะมี array ที่เป็น argument ส่งไปเป็นค่า [] เพื่อบอก React ว่า effect นี้ไม่ได้ขึ้นอยู่กับ props หรือ state ใดๆ เพื่อให้ไม่ต้อง re-run อีก แต่จะทำงานทุกครั้งที่มีการ render หน้าใหม่

```js
useEffect(() => {
  alert("สวัสดีวัยรุ่นไทย");
}, []);
```

- คำสั่งการหน่วงเวลาเราจะใช้ setTimeout ที่เป็น Method สำหรับการตั้งเวลาการทำงานตามที่กำหนดแล้วไม่ทำอีก โดยหากเขียนแบบ Class Component นั้นเราจะวาง setTimeout ไว้ที่ componentDidMount แต่ถ้าเราใช้ hook ก็คือวางในส่วนของ useEffect นั่นเอง

```js
// setTimeout เขียนแบบ Class Component
componentDidMount () {
setTimeout(()=>{
 alert("สวัสดีวัยรุ่นไทย")
},1000);
}
```

```js
// setTimeout เขียนแบบ hook
useEffect(() => {
  setTimeout(() => {
    alert("สวัสดีวัยรุ่นไทย");
  }, 1000);
});
```
