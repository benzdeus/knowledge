# ChildrenToParent

การส่งข้อมูลจากลูกสู่แม่ หรือจะเรียกอีกแบบคือการส่งข้อมูลแบบ bottom up จะแตกต่างจากการส่งข้อมูลแบบ props ก็คือ Properties(คุณสมบัติ) ของ Component นั้นๆ
ที่ใช้ส่ง คุณสมบัติ ระหว่าง Component นั้น หรือแม่ไปสู่ลูก

## การทำงาน

- ลูกและแม่ต้องประกาศรับ props
- แม่สร้างสตัคข้อมูล หรือ สร้างฟังก์ชั่นการทำงาน และส่งกระจายไปลูกที่ต้องการใช้ฟังก์ชั่นในการทำงาน
- ลูกรับฟังก์ชั่นการทำงานแบบ props และส่งข้อมูลกลับไปหาแม่พร้อมฟังก์ชั่นการทำงาน

## ไฟล์แม่ Parent

```js
import React, { useState } from "react";
// ไฟล์ลูกที่ทำหน้าที่ส่ง/รับข้อมูลจากแม่
import FormComponent from "./FormComponent";
import Transaction from "./Transaction";

function IncomeAndExpenses() {
  const design = { color: "red", textAlign: "center", fontSize: "1.5rem" };

// ข้อมูลที่ต้องการส่งไปให้ลูก
  const initData = [
    { id: 1, title: "ค่ารักษาพยาบาล", amount: 2000 },
    { id: 2, title: "ค่าขนม", amount: 1000 },
    { id: 3, title: "ค่าเครื่องสำอาง", amount: 5000 },
  ];

  const [items, setItem] = useState(initData);

// Function ที่ต้องการส่งไปให้ลูก
  const onAddNewItem = (newItem) => {
    setItem((prevItem) => {
      return [newItem, ...prevItem];
    });
  };

  return (
    <>
      <div className="container">
        <h1 style={design}>แอพบัญชีรายรับ-รายจ่าย</h1>

        // ส่ง props function ไปให้ลูก 
        <FormComponent onAddItem={onAddNewItem} />
        // ส่ง props data ไปให้ลูก 
        <Transaction items={items} />

      </div>
    </>
  );
}
export default IncomeAndExpenses;
```

## ไฟล์แม่ Children props Data

```js
import React from 'react'
import Item from './Item'

export default function Transaction(props) {
    // ประกาศตัวแปรรับ props data จากแม่
    const { items } = props
    return (
        <ul className=''>
            {items.map((element) => {
                return <Item {...element} key={element.id}/>
            })}
        </ul>
    )
}

```
## ไฟล์แม่ Children props Function

```js
import React, { useEffect, useState } from 'react'
import "./custom.css"
import { v4 as uuid_v4 } from "uuid";

export default function FormComponent(props) {
  const [title, setTitle] = useState("")
  const [amount, setAmount] = useState(0)
  const [formValid, setFormValid] = useState(false)

  const inputTitle = (event) => {
    setTitle(event.target.value)
  }

  const inputAmount = (event) => {
    setAmount(event.target.value)
  }

  const saveItem = (event) => {
    event.preventDefault()
    const dataItem = {
      id: uuid_v4(),
      title: title,
      amount: Number(amount)
    }
    // รับ props func จากแม่ และส่งก้อนข้อมูลกลับไปให้แม่
    props.onAddItem(dataItem)
    setAmount(0)
    setTitle('')
  }

  useEffect(()=>{
    const checkData = title.trim().length > 0 && amount !== 0
    setFormValid(checkData)
  },[title,amount])

  return (
    <div>
      <form onSubmit={saveItem} >
        <div className='form-group '>
          <label>ชื่อรายการ</label>
          <input type="text" placeholder='ระบุชื่อรายการของคุณ' onChange={inputTitle} value={title} />
        </div>
        <div className='form-group '>
          <label>ชื่อรายการ</label>
          <input type="number" placeholder='(+ รายรับ , -รายจ่าย)' onChange={inputAmount} value={amount} />
        </div>
          <button type='submit' className='btn' disabled={!formValid}>เพิ่มข้อมูล</button>
      </form>
    </div>
  )
}

```