# useState

Sate เป็นตัวแปรที่เก็บข้อมูลภายใน Component จะคล้ายกับ props(ไม่สามารถเปลี่ยนแปลงค่าได้) แต่ state จะสามารถเปลี่ยนแปลงค่าได้ หรือ จะเรียกอีกแบบว่า Stateful ส่วน props จะเรียกอีกหนึ่งความหมายว่า Stateless

## การใช้งาน useState การ set state แบบทั่วไป

```js
// จะใช้ useState ต้อง import useState เข้ามาก่อน
import React, { useEffect, useState } from "react";
import "./custom.css";
import { v4 as uuid_v4 } from "uuid";

export default function FormComponent(props) {
  //ประกาศค่าเริ่มต้นให้ state
  const [title, setTitle] = useState("");
  const [amount, setAmount] = useState(0);

  const inputTitle = (event) => {
    //set ค่าเข้าไปใน Function state
    setTitle(event.target.value);
  };

  const inputAmount = (event) => {
    //set ค่าเข้าไปใน Function state
    setAmount(event.target.value);
  };

  const saveItem = (event) => {
    event.preventDefault();
    const dataItem = {
      id: uuid_v4(),
      title: title,
      amount: Number(amount),
    };
    props.onAddItem(dataItem);
    setAmount(0);
    setTitle("");
  };

  return (
    <div>
      <form onSubmit={saveItem}>
        <div className="form-group ">
          <label>ชื่อรายการ</label>
          //นำค่าที่ได้จาก state ไปใช้งานหรือแสดงผลลัพธ์ ex. state ชื่อ title
          <input
            type="text"
            placeholder="ระบุชื่อรายการของคุณ"
            onChange={inputTitle}
            value={title}
          />
        </div>

        <div className="form-group ">
          <label>ชื่อรายการ</label>
          //นำค่าที่ได้จาก state ไปใช้งานหรือแสดงผลลัพธ์ ex. state ชื่อ amount
          <input
            type="number"
            placeholder="(+ รายรับ , -รายจ่าย)"
            onChange={inputAmount}
            value={amount}
          />
        </div>

        <button type="submit" className="btn">
          เพิ่มข้อมูล
        </button>
      </form>
    </div>
  );
}
```

## การ set ค่าใน state ที่ยังคงค่าเดิม และนำค่า state ใหม่มาต่อหน้า หรือต่อท้าย

```js
const initData = [
  { id: 1, title: "ค่ารักษาพยาบาล", amount: 2000 },
  { id: 2, title: "ค่าขนม", amount: 1000 },
  { id: 3, title: "ค่าเครื่องสำอาง", amount: 5000 },
];

const [items, setItem] = useState(initData);

// สมมุติ newItem เป็นก้อนข้อมูลที่ส่งมาจากการทำงาน function onAddNewItem
const newItem = [{ id: 4, title: "ค่าท่องเที่ยว", amount: 20000 }];

const onAddNewItem = (newItem) => {
  setItem((prevItem) => {
    return [newItem, ...prevItem];
  });
};

// ผลลัพธ์ที่ได้ จะนำข้อมูลเข้ามาใหม่มาต่อหน้าสุด
console.log(items);
items: [
  { id: 4, title: "ค่าท่องเที่ยว", amount: 20000 },  
  { id: 1, title: "ค่ารักษาพยาบาล", amount: 2000 },
  { id: 2, title: "ค่าขนม", amount: 1000 },
  { id: 3, title: "ค่าเครื่องสำอาง", amount: 5000 },
];
```
