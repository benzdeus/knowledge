# Event 
คือเหตุการณืต่างๆที่เกิดขึ้น เช่น ผู้ใช้คลิกเมาส์ ผู้ใช้กดปุ่มบนคีย์บอร์ด การพิมพ์ข้อมูลลงในฟอร์ม เป็นต้น ความหมายของ Action. Action คือการกระทำใดๆเมื่อมีเหตุการณืเกิดขึ้น

- ข้อยกตัวอย่างคร่าวๆ 2 Event 
   
  - onChange คือ action ที่กระทำเมื่อมีการพิมพ์
  - onSubmit คือ action ที่กระทำเมื่อกดปุ่ม

```js
const Example = () =>{
   const inputName = (event) =>{
      console.log(event.target.value)
   }
   const saveData = () =>{
      console.log("บันทึกข้อมูลเรียบร้อย")
   }
    return (
    <div className="div-sub">
     <form onSubmit={saveData}>
       <div className="div-color">Hi, I am Example</div>
       <label id="name-css">ชื่อ-สกุล</label>
       <input type="text" placeholder="กรุณากรอกข้อมูล" onChange={inputName}>
       </input>
       <button type="submit">เพิ่มข้อมูล</button>
     </form>  
    </div>
     )
}
export default Example;
``` 