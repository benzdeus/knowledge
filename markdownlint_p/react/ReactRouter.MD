# React Router

การสร้างเส้นทางในการเข้าถึง Component เพื่อให้แสดงข้อมูลและเชื่อมโยง Component ในแต่ล่ะหน้า

ติดตั้ง react-router-dom โดยพิมพ์คำสั่ง

```npm
npm i react-router-dom
```

import react-router-dom ในไฟล์ที่ต้องการสร้างเส้นทางให้กับหน้าเว็บ

```js
import { BrowserRouter as Router, Switch, Route, Link } from "react-router-dom";
```

เรียกใช้ Router หรือ property ของ react-router-dom เพื่อสร้าง Router

```js
import { BrowserRouter as Router, Switch, Route, Link } from "react-router-dom";

function GetRouter() {
  return (
    <Router>
      <div>
        <ul className="horizontal-menu">
          <li>
            <Link to="/">หน้าแรก</Link>
          </li>
          <li>
            <Link to="/data">ข้อมูล</Link>
          </li>
        </ul>
        <Switch>
          {/* exact คือบอกว่านี้คือหน้าแรกของเว็บ */}
          <Route path="/" exact>
            <Home />
          </Route>
          <Route path="/data">
            <Data/>
          </Route>
        </Switch>
      </div>
    </Router>
  );
}
export default GetRouter;

function Home() {
  return <h2>Home</h2>;
}

function Data() {
  return <h2>Data</h2>;
}
```
